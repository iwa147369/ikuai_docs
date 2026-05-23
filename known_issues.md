# Network Lab Troubleshooting Guide
> Small Business Network: Dual ISP · iKuai · EVE-NG · Proxmox

---

## Table of Contents
1. [Mikrotik Issues](#1-mikrotik-issues)
2. [Cisco C2691 ISP Issues](#2-cisco-c2691-isp-issues)
3. [iKuai Issues](#3-ikuai-issues)
4. [Switch & VLAN Issues](#4-switch--vlan-issues)
5. [Proxmox Issues](#5-proxmox-issues)
6. [USB NIC Issues](#6-usb-nic-issues)
7. [Routing & NAT Issues](#7-routing--nat-issues)
8. [Design Issues](#8-design-issues)

---

## 1. Mikrotik Issues

### 1.1 Interface Renamed After Reboot
**Problem:** After an unexpected reboot in EVE-NG, Mikrotik renames interfaces (ether1 → ether5 → ether9), causing PPPoE server to bind to wrong interface.

**Root Cause:** EVE-NG shuts down nodes abruptly without graceful shutdown, causing Mikrotik to increment interface counter on each boot.

**Solution:**
```routeros
# Fix interface names using default-name
/interface ethernet
set [find default-name="ether1"] name=ether1
set [find default-name="ether2"] name=ether2

# Rebuild PPPoE server on correct interface
/interface pppoe-server server remove 0
/interface pppoe-server server add
  interface=ether1
  service-name=ISP-PPPoE
  default-profile=profile-dynamic
  max-sessions=9
  disabled=no
```

**Prevention:** Always stop nodes properly in EVE-NG before shutting down the host machine.

---

### 1.2 PPPoE Server Not Enabled
**Problem:** iKuai cannot establish PPPoE session with Mikrotik even though configuration looks correct.

**Root Cause:** PPPoE server was not enabled after creation.

**Solution:**
```routeros
/interface pppoe-server server enable 0
/interface pppoe-server server print
# Verify: no "X" (disabled) flag
```

---

### 1.3 PPPoE max-sessions Count
**Problem:** Unable to dial 8 simultaneous PPPoE sessions (1 static + 7 dynamic).

**Root Cause:** `max-sessions=8` counts ALL sessions regardless of profile or username. With 1 static + 7 dynamic = 8 sessions, no buffer remains.

**Solution:**
```routeros
/interface pppoe-server server set 0 max-sessions=9
# Always set max-sessions = total expected sessions + 1 buffer
```

---

### 1.4 Multi-Session with Same Account
**Problem:** Only 1 session allowed per account `user@hinet.net` even with `only-one=no`.

**Root Cause:** Default PPP profile has `only-one=yes`.

**Solution:**
```routeros
/ppp profile set profile-dynamic only-one=no
# Verify
/ppp profile print detail where name="profile-dynamic"
```

---

### 1.5 IP Not Changing on Reconnect
**Problem:** Dynamic IP account always gets the same IP after reconnect in lab environment.

**Root Cause:** Mikrotik caches session state and assigns the lowest available IP from pool sequentially.

**Note:** This is a lab limitation. Real ISPs (e.g., HiNet) have massive IP pools, so reconnecting almost always yields a different IP.

**Workaround:**
```routeros
/ppp secret reset-statistics [find name="user@hinet.net"]
```

---

### 1.6 Default Route Not Working After Adding eth6
**Problem:** Mikrotik static route `0.0.0.0/0 via 10.10.0.1` shows as INACTIVE after adding DHCP client on eth6.

**Root Cause:** DHCP client on eth6 also adds a default route with same distance, causing conflict.

**Solution:**
```routeros
# Remove static route pointing to old loopback
/ip route remove [find gateway="1.1.1.1"]

# Add correct default route via Loopback node
/ip route add dst-address=0.0.0.0/0 gateway=10.10.0.1 distance=1
```

---

## 2. Cisco C2691 ISP Issues

### 2.1 NAT Fails Due to Insufficient RAM
**Problem:** `ip nat inside` command fails with NBAR memory error.

**Root Cause:** C2691 in EVE-NG has very limited RAM (~64MB). NAT + NBAR + CEF together exceed available memory.

**Solution:**
```ios
! Disable NBAR and CEF to free memory
no ip nbar protocol-discovery
no ip cef

! Or increase VM RAM in EVE-NG:
! Right-click node → Edit → RAM: 256MB
```

---

### 2.2 Default Route via Interface (No Next-Hop)
**Problem:** `ip route 0.0.0.0 0.0.0.0 FastEthernet0/1` works for directly connected destinations but fails for remote IPs like 8.8.8.8.

**Root Cause:** Without a specific next-hop IP, Cisco performs ARP for the destination IP directly, which fails for non-local addresses.

**Solution:**
```ios
! Replace interface-only route with specific next-hop
no ip route 0.0.0.0 0.0.0.0 FastEthernet0/1
ip route 0.0.0.0 0.0.0.0 192.168.122.1
# Always specify gateway IP, not just interface
```

---

### 2.3 NAT Access-List Conflict with Web UI Access
**Problem:** With `access-list 1 permit 203.0.113.0 0.0.0.7`, cannot access iKuai web UI at 203.0.113.2 because reply packets get NATted and source IP changes to 192.168.122.140.

**Root Cause:** NAT overload translates reply packets from iKuai (203.0.113.2) when they match the ACL, breaking the TCP session for web UI access.

**Solution:**
```ios
! Deny iKuai WAN IP before permitting subnet
no access-list 1
access-list 1 deny 203.0.113.2 0.0.0.0
access-list 1 permit 203.0.113.0 0.0.0.7
access-list 1 permit 172.16.0.0 0.0.255.255
```

---

### 2.4 RFC5737 Documentation IP Blocked by Internet
**Problem:** Using 203.0.113.0/24 (RFC5737 documentation prefix) as ISP2 subnet causes packets to be blocked by upstream routers.

**Root Cause:** 203.0.113.0/24 is reserved for documentation purposes (RFC5737) and is filtered by real internet routers.

**Solution:**
```ios
! Change ISP2 subnet to private IP range
interface FastEthernet0/0
  no ip address 203.0.113.1 255.255.255.248
  ip address 10.20.0.1 255.255.255.248

! Update NAT ACL accordingly
no access-list 1
access-list 1 deny 10.20.0.2
access-list 1 permit 10.20.0.0 0.0.0.7
access-list 1 permit 172.16.0.0 0.0.255.255
```

---

### 2.5 NAT Not Translating Traffic (Missing ACL)
**Problem:** After removing and re-adding NAT configuration, traffic from end devices cannot reach internet.

**Root Cause:** `ip nat inside source list 1 interface fa0/1 overload` references access-list 1, but the ACL was deleted and not recreated.

**Solution:**
```ios
! Always verify ACL exists after NAT config changes
show access-list 1
! If missing, recreate:
access-list 1 permit [your_subnet] [wildcard]
```

---

## 3. iKuai Issues

### 3.1 wan1 Management Interface Deleted Accidentally
**Problem:** Deleted wan1 (management interface eth0) and lost web UI access.

**Root Cause:** wan1 was the only path from host machine to iKuai web UI.

**Solution:**
```
Option A: Access via other WAN interface
  - Add route on host: sudo ip route add [wan_subnet] via [upstream_gw] dev virbr0
  - Access web UI via wan2 or wan3 IP

Option B: Use iKuai console in EVE-NG/Proxmox
  - Double-click iKuai node → Console
  - Option 1: Re-bind eth0 as WAN
  - Option 2: Set IP 192.168.122.100/24, gateway 192.168.122.1
```

**Prevention:** Always maintain at least one accessible management path before making WAN changes.

---

### 3.2 WAN Priority — Management Interface as Default Gateway
**Problem:** wan1 (management, 192.168.122.x) gets priority 1 (highest), causing all traffic to route through management interface instead of ISP.

**Root Cause:** iKuai assigns priority based on creation order. wan1 created first = priority 1.

**Solution:**
```
Method 1: Set wan2 (ISP) as default gateway
  外网设置 → wan2 → tick "设此条线路为默认网关"
  → Only ONE WAN can be default gateway

Method 2: Use 端口分流 to override
  流控分流 → 端口分流 → Add rule:
  Source: 172.16.0.0/16 (all LAN)
  Output: wan2
  → Policy routing overrides default gateway
```

---

### 3.3 VLAN Name Error
**Problem:** Error "vlan_name parameter error" when saving VLAN configuration.

**Root Cause:** iKuai does not accept uppercase letters in VLAN names.

**Solution:**
```
❌ vlan_LIVE, vlan_USE, vlan_GUEST
✅ vlan_live, vlan_use, vlan_guess
Rules:
  - Lowercase letters only
  - Underscores allowed
  - No spaces, hyphens, or special characters
```

---

### 3.4 Cannot Bind Same Physical NIC to Multiple LANs
**Problem:** Cannot create multiple LAN interfaces on the same physical NIC (eth3).

**Root Cause:** iKuai design: 1 physical port = 1 LAN interface. Unlike MikroTik/pfSense which support sub-interfaces.

**Solution:**
```
Use iKuai VLAN Settings instead of multiple LAN interfaces:
  网络设置 → VLAN设置 → 添加:
  VLAN 10: ID=10, name=vlan_live, IP=172.16.10.1, 线路=lan1
  VLAN 20: ID=20, name=vlan_use,  IP=172.16.20.1, 线路=lan1
  VLAN 30: ID=30, name=vlan_guess,IP=172.16.30.1, 线路=lan1
  
  → All VLANs attach to lan1 (physical eth3)
  → lan1 must have an IP (required by iKuai)
  → lan1 IP becomes native VLAN gateway
```

---

### 3.5 Cannot Use Single NIC for Both WAN and LAN
**Problem:** iKuai does not support Router-on-a-Stick (single NIC for WAN + LAN via VLAN sub-interfaces).

**Root Cause:** iKuai architecture requires dedicated physical interfaces for WAN and LAN.

**Solution:**
```
Topology must have separate physical paths:
  ✅ eth0 → WAN (ISP)
  ✅ eth1 → LAN (Switch/AP)

If only 1 NIC available:
  → Use pfSense/OPNsense/MikroTik CHR instead
  → Or add USB NIC / PCIe NIC
```

---

### 3.6 Static Route Cannot Override Default Gateway
**Problem:** Static route with priority=1 cannot override default gateway with priority=0.

**Root Cause:** iKuai static route minimum priority is 1. Default gateway always has priority 0. Static routes cannot be lower than 0.

**Solution:**
```
Use 端口分流 instead of static route:
Priority order in iKuai:
  静态路由 > 域名分流 > 端口分流 > 协议分流 > 多线负载 > 默认网关

端口分流 overrides 默认网关:
  流控分流 → 端口分流 → Add:
  Source: [subnet]
  Output: [specific WAN]
  → Guaranteed to override default gateway
```

---

### 3.7 IP Conflict with PPPoE Subnet
**Problem:** VLAN IP 192.168.10.1 conflicts with PPPoE local address 192.168.10.1 on Mikrotik.

**Root Cause:** Used same subnet for both iKuai VLAN and Mikrotik PPPoE server local address.

**Solution:**
```
Use different subnet ranges:
  PPPoE: 192.168.10.0/24 (Mikrotik manages)
  VLAN LIVE:  172.16.10.0/24
  VLAN USE:   172.16.20.0/24
  VLAN GUEST: 172.16.30.0/24
  
  Use 172.16.0.0/16 for internal VLANs to avoid conflicts
```

---

## 4. Switch & VLAN Issues

### 4.1 VLAN Not Passing Through Trunk
**Problem:** End devices cannot get DHCP IP even though switch VLAN configuration looks correct.

**Root Cause:** Trunk port not configured or VLAN not added to allowed list.

**Solution:**
```ios
! Verify trunk configuration
show interface trunk
show vlan brief

! Ensure VLANs are allowed on trunk
interface e0/0
  switchport trunk encapsulation dot1q
  switchport mode trunk
  switchport trunk allowed vlan 10,20,30
  switchport trunk native vlan 999
```

---

### 4.2 Inter-VLAN Traffic Not Isolated
**Problem:** Devices in VLAN 10 (LIVE) can ping devices in VLAN 30 (GUEST).

**Root Cause:** iKuai "Allow other LANs to access this LAN" option is enabled by default.

**Solution:**
```
iKuai → 内网设置 → Edit each VLAN:
  □ Allow other LANs to access this LAN  ← UNCHECK

Or use ACL rules if the option is not available:
  安全设置 → ACL → Block inter-VLAN traffic
```

---

## 5. Proxmox Issues

### 5.1 Subscription Warning on Free Version
**Problem:** Proxmox shows "No valid subscription" popup on every login.

**Root Cause:** Enterprise repository configured by default, requires paid subscription.

**Solution:**
```bash
# Disable enterprise repo
echo "# disabled" > /etc/apt/sources.list.d/pve-enterprise.list

# Add free community repo
echo "deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription" \
  > /etc/apt/sources.list.d/pve-install-repo.list

# Remove login popup
sed -i "s/data.status !== 'Active'/false/g" \
  /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js

systemctl restart pveproxy
apt update && apt dist-upgrade -y
```

---

### 5.2 Management IP Configuration
**Problem:** Proxmox assigned wrong management IP during installation, need to change.

**Solution:**
```bash
# Temporary change
ip addr del 192.168.100.251/24 dev vmbr0
ip addr add 192.168.0.51/24 dev vmbr0

# Permanent change
nano /etc/network/interfaces
# Edit: address 192.168.0.51/24
systemctl restart networking
```

---

## 6. USB NIC Issues

### 6.1 USB NIC Not Joining Bridge After Reconnect
**Problem:** After USB NIC disconnects and reconnects, it does not automatically rejoin vmbr1 bridge.

**Root Cause:** Linux bridge does not automatically re-add interface after it disappears and reappears.

**Solution:**
```bash
# Manually add USB NIC to bridge
ip link set enxdc32627b1b5a master vmbr1

# Permanent fix in /etc/network/interfaces
auto vmbr1
iface vmbr1 inet manual
    bridge-ports enxdc32627b1b5a
    bridge-stp off
    bridge-fd 0
    post-up ip link set enxdc32627b1b5a up
```

---

### 6.2 USB NIC Shows state UNKNOWN
**Problem:** USB NIC shows `state UNKNOWN` instead of `UP` even when connected.

**Root Cause:** CDC Ethernet devices (cdc_ether driver) do not report carrier state like regular NICs. `UNKNOWN` is normal behavior for this driver type.

**Verification:**
```bash
ethtool enxdc32627b1b5a | grep "Link detected"
# "Link detected: yes" = working correctly despite UNKNOWN state
```

---

### 6.3 USB NIC Disconnects Unexpectedly
**Problem:** USB NIC randomly disconnects, shown in dmesg as "unregister cdc_ether".

**Root Cause:** USB power saving mode suspends the device when idle.

**Solution:**
```bash
# Disable USB power saving
for device in /sys/bus/usb/devices/*/power/control; do
  echo 'on' > $device
done

# Make permanent via /etc/rc.local or udev rule
```

---

### 6.4 Changing USB NIC — Interface Name Changes
**Problem:** Replacing USB NIC causes interface name to change, breaking vmbr1 bridge configuration.

**Solution:**
```bash
# Create udev rule to pin name to MAC address
nano /etc/udev/rules.d/10-usb-nic.rules

SUBSYSTEM=="net", ACTION=="add", \
ATTR{address}=="dc:32:62:7b:1b:5a", \
NAME="usblan0"

# Update /etc/network/interfaces to use fixed name
bridge-ports usblan0

udevadm control --reload-rules
udevadm trigger
```

---

## 7. Routing & NAT Issues

### 7.1 Traffic Stopped at virbr0 (192.168.122.1)
**Problem:** VPCS devices get "Destination port unreachable" from 192.168.122.1 when pinging 8.8.8.8.

**Root Cause:** libvirt's virbr0 bridge does not masquerade traffic from subnets other than 192.168.122.0/24 to the external interface (wlan0).

**Solution:**
```bash
# Add masquerade rule for additional subnets
sudo iptables -t nat -A POSTROUTING \
  -s 192.168.122.0/24 \
  -o wlan0 \
  -j MASQUERADE
```

---

### 7.2 Ping Works from Router Interface but Not from Downstream Devices
**Problem:** C2691 can ping 8.8.8.8 from fa0/1 but downstream devices (via iKuai) cannot.

**Root Cause:** iKuai NATs internal traffic to its WAN IP (e.g., 10.20.0.2), but C2691's NAT ACL has `deny 10.20.0.2`, blocking this traffic from being NATted to a routable IP.

**Solution:**
```ios
! Remove deny rule for iKuai WAN IP
no access-list 1
access-list 1 permit 10.20.0.0 0.0.0.7
access-list 1 permit 172.16.0.0 0.0.255.255
```

---

### 7.3 Double NAT Causes Web UI Access Issues
**Problem:** After adding NAT on C2691, iKuai web UI becomes inaccessible because reply packets get translated.

**Root Cause:** NAT overload translates all traffic matching the ACL, including return traffic destined for iKuai WAN IP, breaking TCP sessions.

**Solution:**
```ios
! Deny iKuai WAN IP from NAT, permit everything else
access-list 1 deny [iKuai_WAN_IP] 0.0.0.0
access-list 1 permit [iKuai_subnet] [wildcard]
access-list 1 permit [LAN_subnet] [wildcard]
```

---

## 8. Design Issues

### 8.1 Single NIC Architecture Limitation
**Problem:** PC with only 1 physical NIC cannot support dual WAN + LAN for iKuai.

**Root Cause:** iKuai requires dedicated physical interfaces for each function (WAN1, WAN2, LAN).

**Solutions by priority:**
```
1. Add PCIe NIC card (~$15-30) — Most stable
2. Add USB 3.0 Gigabit NIC (~$10-20) — Easy, less stable
3. Use VLAN on managed switch — Complex, no extra hardware
4. Replace iKuai with pfSense/OPNsense — Supports Router-on-a-Stick
```

---

### 8.2 Traffic Hairpinning Through Switch
**Problem:** In topology ISP → Switch → iKuai → Switch → Devices, traffic passes through switch twice, reducing effective bandwidth.

**Root Cause:** Switch positioned between ISP and iKuai forces all traffic to traverse switch both inbound and outbound.

**Recommended topology:**
```
❌ Bad:   ISP → Switch → iKuai
                └──────────────── Devices

✅ Good:  ISP → iKuai → Switch → Devices
```

---

### 8.3 Router-on-a-Stick Not Supported by iKuai
**Problem:** Cannot use single physical interface for both WAN and LAN with VLAN sub-interfaces in iKuai.

**Root Cause:** iKuai architecture enforces physical interface separation between WAN and LAN roles.

**Alternative:** Use MikroTik CHR, pfSense, or OPNsense if Router-on-a-Stick topology is required.

---

## Quick Reference

### Useful Commands

**Mikrotik:**
```routeros
/interface print detail          # Show interfaces with default-name
/ppp active print                # Show active PPPoE sessions
/ip address print                # Show IP assignments
/export file=backup              # Save configuration
/tool traceroute [address]       # Traceroute
```

**Cisco:**
```ios
show ip interface brief          # Interface status
show ip route                    # Routing table
show ip nat translations         # NAT sessions
show access-list 1               # ACL entries
write memory                     # Save config
```

**Proxmox/Linux:**
```bash
ip link show                     # Show interfaces
brctl show                       # Show bridge members
bridge link show                 # Show bridge port states
tcpdump -i [iface] -n            # Capture traffic
ip -s link show [iface]          # Interface statistics
dmesg | grep -i [keyword]        # Kernel log
```

---

## Key Lessons Learned

```
1. Always save config before making changes
2. Maintain at least one management access path at all times
3. Stop EVE-NG nodes gracefully before shutdown
4. iKuai requires dedicated physical NIC per WAN/LAN role
5. Use 172.16.0.0/16 for internal VLANs to avoid ISP subnet conflicts
6. RFC5737 prefixes (192.0.2.x, 198.51.100.x, 203.0.113.x) are blocked on real internet
7. Policy routing (端口分流) takes priority over default gateway in iKuai
8. USB NICs need manual bridge re-attachment after reconnection
9. Proxmox virbr0 only masquerades 192.168.122.0/24 by default
10. Double NAT causes session breakage — minimize NAT layers
```
