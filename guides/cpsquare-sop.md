# SOP: VM Architecture & Network Connection Guide
**Document Type:** Standard Operating Procedure  
**Version:** 1.1  
**Last Updated:** May 2026  
**Audience:** End Users / Non-Technical Staff  

---

## Table of Contents
1. [Overview](#1-overview)
2. [System Architecture](#2-system-architecture)
3. [IP Address Reference](#3-ip-address-reference)
4. [How to Access Systems](#4-how-to-access-systems)
5. [Network Topology](#5-network-topology)
6. [Daily Operations](#6-daily-operations)
7. [Troubleshooting](#7-troubleshooting)
8. [USB-to-Ethernet Device Replacement Guide](#8-usb-to-ethernet-device-replacement-guide)
9. [Contact & Escalation](#9-contact--escalation)

---

## 1. Overview

This document describes the current network infrastructure for the office, built on a virtualized platform. The system uses a single physical PC running **Proxmox**, a free virtualization platform, which hosts the **iKuai** virtual router that manages all internet traffic for the office.

### What This System Does
- Connects the office to the internet via a public IP address
- Manages and separates network traffic for different user groups (VIP, Normal, Guest)
- Provides centralized control over bandwidth and internet access

### Key Components

| Component | What It Is | Role |
|---|---|---|
| **Proxmox** | Virtualization platform on physical PC | Runs virtual machines |
| **iKuai VM** | Virtual router software | Manages internet & network |
| **USB NIC** | USB-to-Ethernet adapter | Connects internal network |
| **WiFi Router (AP Mode)** | Wireless access point | Provides WiFi to devices |
| **Managed Switch** | Network switch | Connects all devices |

---

## 2. System Architecture

### Physical Hardware

```
Physical PC (Proxmox Host)
├── CPU:  8 cores
├── RAM:  16 GB
├── HDD:  256 GB
├── NIC1: Built-in LAN (nic0) → connects to ISP
└── NIC2: USB-to-Ethernet   → connects to internal network
```

### Virtual Machines

```
Proxmox Host
└── VM 100: iKuai Router
    ├── RAM:  4 GB (allocated)
    ├── HDD:  50 GB (allocated)
    ├── CPU:  2 cores
    ├── eth0 (WAN) → Internet via NIC1
    └── eth1 (LAN) → Internal network via USB NIC
```

### How It All Connects

```
Internet (ISP)
      │
      │ Public IP: x.x.x.x
      │
   [NIC1 - nic0]
      │
   [vmbr0 - Bridge]
      │
   [iKuai VM - eth0/WAN]
      │
   [iKuai VM - eth1/LAN]
      │
   [vmbr1 - Bridge]
      │
   [USB NIC]
      │
   [AP Wifi / Switch]
      │
   [End Devices - Phones, PCs, etc.]
```

---

## 3. IP Address Reference

### Public IP Addresses (Internet-facing)

| IP Address | Purpose | Notes |
|---|---|---|
Updating ...

---

### Private IP Addresses (Internal network)

| IP Address | Device | How to Access |
|---|---|---|
| `192.168.0.51` | Proxmox Web UI | https://192.168.0.51:8006 |
| `192.168.9.1` | iKuai Web UI - LAN gateway | http://192.168.9.1 |
| `192.168.9.100–200` | DHCP pool (end devices) | Auto-assigned |

---

### VLAN Network Segments

| VLAN | Name | Subnet | Gateway | Who Uses It |
|---|---|---|---|---|
| VLAN 10 | LIVE DV | `172.16.10.0/24` | `172.16.10.1` | DV team |
| VLAN 20 | LIVE DZ | `172.16.20.0/24` | `172.16.20.1` | DZ team |
| VLAN 30 | USE | `172.16.30.0/24` | `172.16.30.1` | Other users |

---

## 4. How to Access Systems

### 4.1 Access Proxmox Web UI

**When to use:** Managing virtual machines, checking server status, starting/stopping VMs.

**Requirements:** Must be connected to the office network (WiFi or LAN cable).

**Steps:**
1. Open a web browser (Chrome, Firefox, Edge)
2. Type in the address bar: `https://192.168.0.51:8006`
3. Login with:
   - Username: `root`
   - Password: *(ask administrator)*
   - Realm: `Linux PAM standard authentication`
4. Click **Login**

> ⚠️ **Important:** Do not change any settings unless instructed. Incorrect changes may disconnect all users from the internet.

---

### 4.2 Access iKuai Web UI

**When to use:** Checking internet status, viewing connected devices, managing bandwidth.

**Requirements:** Must be connected to the office network.

**Steps:**
1. Open a web browser
2. Type in the address bar: `http://192.168.9.1`
3. Login with:
   - Username: `admin`
   - Password: *(ask administrator)*
4. Click **Login**

**Main pages to know:**

| Page | Chinese Name | What It Shows |
|---|---|---|
| System Overview | 系统概况 | Internet status, connected devices |
| WAN Settings | 外网设置 | Internet connection status |
| LAN Settings | 内外网设置 | Internal network status |
| DHCP | DHCP设置 | Devices with assigned IPs |
| Traffic Monitor | 状态监控 | Real-time bandwidth usage |

---

### 4.3 Start iKuai VM (if it is not running)

**Via Proxmox Web UI:**
1. Login to Proxmox: `https://192.168.0.51:8006`
2. In the left panel, click **VM 100 (iKuai)**
3. Click the **Start** button (▶) at the top
4. Wait 30–60 seconds for iKuai to boot
5. Verify: try accessing `http://192.168.9.1`

**Via SSH/Console:**
```bash
# SSH into Proxmox
ssh root@192.168.0.51

# Start iKuai VM
qm start 100

# Check status
qm status 100
# Expected output: status: running
```

---

### 4.4 Properly Shutdown the System

> ⚠️ **Always follow this order** to avoid data loss or configuration corruption.

**Step 1 — Shutdown iKuai VM first:**

Via Proxmox Web UI:
1. Login to `https://192.168.0.51:8006`
2. Click **VM 100 (iKuai)**
3. Click **Shutdown** (not Stop)
4. Wait until status shows **stopped**

Via SSH:
```bash
ssh root@192.168.0.51
qm shutdown 100
qm wait 100
qm status 100   # Must show: status: stopped
```

**Step 2 — Shutdown Proxmox:**

Via Web UI:
1. Click node **promox** in left panel
2. Click **Shell**
3. Type: `shutdown -h now`

Via SSH:
```bash
shutdown -h now
```

---

## 5. Network Topology

### Full Network Diagram

```
┌─────────────────────────────────────────────────────┐
│                    INTERNET                         │
│              ISP Public IP Range                    │
└──────────────────────┬──────────────────────────────┘
                       │
                       │ WAN: x.x.x.x
                       │
┌──────────────────────▼──────────────────────────────┐
│                 PROXMOX HOST                        │
│              (Physical PC Server)                   │
│  Management IP: 192.168.0.51                        │
│                                                     │
│  ┌──────────────────────────────────────────────┐   │
│  │              iKuai VM (VM 100)               │   │
│  │                                              │   │
│  │  eth0 (WAN): x.x.x.x                         │   │
│  │  eth1 (LAN): 192.168.9.1                     │   │
│  │                                              │   │
│  │  VLANs:                                      │   │
│  │    LIVE DV (VLAN 10): 172.16.10.1/24         │   │
│  │    LIVE DZ (VLAN 20): 172.16.20.1/24         │   │
│  │    USE     (VLAN 30): 172.16.30.1/24         │   │
│  └──────────────────────────────────────────────┘   │
└──────────────────────┬──────────────────────────────┘
                       │ USB NIC
                       │
              ┌────────▼─────────┐
              │  Managed Switch  │
              │  RG-ES224GC-V2   │
              └──┬──────┬──────┬─┘
                 │      │      │
            ┌────▼─┐ ┌──▼───┐ ┌▼─────┐
            │ AP 1 │ │ AP 2 │ │ AP 3 │  ...
            │VLAN10│ │VLAN20│ │VLAN30│
            └──────┘ └──────┘ └──────┘
             DV team  DZ team  Others
```

---

## 6. Daily Operations

### 6.1 Check Internet Status

1. Login to iKuai: `http://192.168.9.1`
2. Go to **系统概况 (System Overview)**
3. Check WAN status:
   - 🟢 Green = Internet connected
   - 🔴 Red = Internet disconnected

### 6.2 Check Connected Devices

1. Login to iKuai: `http://192.168.9.1`
2. Go to **状态监控 (Status Monitor)** → **终端连接**
3. View all currently connected devices with their IP and MAC address

### 6.3 Restart iKuai (if internet is down)

1. Login to Proxmox: `https://192.168.0.51:8006`
2. Click **VM 100 (iKuai)**
3. Click **Shutdown** → wait 30 seconds
4. Click **Start**
5. Wait 60 seconds → test internet connection

### 6.4 Check VM is Running

Via Proxmox Web UI:
- VM 100 (iKuai) should show status: **running** ✅

Via SSH:
```bash
ssh root@192.168.0.51
qm list
# VM 100 should show: running
```

---

## 7. Troubleshooting

### Problem: Cannot access iKuai Web UI (`http://192.168.9.1`)

| Step | Action |
|---|---|
| 1 | Make sure device is connected to office WiFi |
| 2 | Check iKuai VM is running in Proxmox |
| 3 | Try accessing via IP: `http://192.168.9.1` |
| 4 | Restart iKuai VM (see Section 6.3) |
| 5 | If still fails → contact IT administrator |

---

### Problem: Cannot access Proxmox (`https://192.168.0.51:8006`)

| Step | Action |
|---|---|
| 1 | Must be on office network (not guest WiFi) |
| 2 | Try adding exception for SSL warning in browser |
| 3 | Check physical PC is powered on |
| 4 | Try SSH: `ssh root@192.168.0.51` |
| 5 | If still fails → check physical PC directly |

---

### Problem: Internet is down for all users

| Step | Action |
|---|---|
| 1 | Check ISP modem LED — is it connected? |
| 2 | Login to iKuai → check WAN status |
| 3 | In iKuai: **外网设置** → **wan1** → click **重拨 (Reconnect)** |
| 4 | If WAN shows connected but no internet → restart iKuai VM |
| 5 | If still fails → contact ISP |

---

### Problem: Internet is down for specific VLAN only

| Step | Action |
|---|---|
| 1 | Login to iKuai → **流控分流** → check policy rules |
| 2 | Check VLAN configuration: **VLAN设置** |
| 3 | Check DHCP is running for that VLAN: **DHCP设置** |
| 4 | Restart affected devices |
| 5 | If still fails → contact IT administrator |

---

## 8. USB-to-Ethernet Device Replacement Guide

> **For IT Staff Only**  
> This section covers procedures when the USB-to-Ethernet (USB NIC) adapter needs to be replaced due to failure, damage, or upgrade.

---

### 8.1 Why USB NIC Matters

The USB NIC is the critical link between the Proxmox host and the internal network (Switch → AP → End devices). If it fails or is replaced:

```
USB NIC failure impact:
  ❌ All WiFi users lose internet access
  ❌ iKuai LAN interface goes down
  ❌ DHCP stops working for end devices
  ✅ WAN (ISP connection) still works
  ✅ Proxmox management still accessible
```

---

### 8.2 Before Replacing — Record Current Device Info

```bash
# SSH into Proxmox
ssh root@192.168.0.51

# Record current USB NIC details
ip link show | grep -A2 enx
# Note down:
#   Interface name: enxXXXXXXXXXXXX
#   MAC address: XX:XX:XX:XX:XX:XX

# Check current bridge membership
brctl show vmbr1
# Note down which interface is in vmbr1

# Check current /etc/network/interfaces
cat /etc/network/interfaces
# Save or screenshot this file
```

> 📋 **Fill in before replacing:**
> - Old interface name: `enx___________`
> - Old MAC address: `__:__:__:__:__:__`
> - Bridge it belongs to: `vmbr1`

---

### 8.3 Step-by-Step Replacement Procedure

#### Step 1: Notify users
> Inform all office users that internet will be interrupted for approximately **5–10 minutes**.

#### Step 2: Shutdown iKuai VM gracefully
```bash
ssh root@192.168.0.51
qm shutdown 100
qm wait 100
qm status 100
# Must show: status: stopped
```

#### Step 3: Remove old USB NIC
- Unplug the old USB-to-Ethernet adapter from the PC
- Wait 5 seconds

#### Step 4: Plug in new USB NIC
- Insert the new USB-to-Ethernet adapter
- Wait 10–15 seconds for the driver to load

#### Step 5: Identify new interface name
```bash
# Check new interface appeared
ip link show

# Look for new interface starting with "enx" or "eth"
# Example output:
#   enxaabbccddeeff: <BROADCAST,MULTICAST> mtu 1500 ...
#   link/ether aa:bb:cc:dd:ee:ff

# Also check dmesg for confirmation
dmesg | tail -20 | grep -i "usb\|eth\|enx"
```

#### Step 6: Update /etc/network/interfaces
```bash
# Edit network config
nano /etc/network/interfaces

# Find vmbr1 section:
# OLD (replace this):
auto vmbr1
iface vmbr1 inet manual
    bridge-ports enxOLDMACADDRESS   ← change this line
    bridge-stp off
    bridge-fd 0

# NEW (replace with new interface name):
auto vmbr1
iface vmbr1 inet manual
    bridge-ports enxNEWMACADDRESS   ← new interface name
    bridge-stp off
    bridge-fd 0

# Save: Ctrl+X → Y → Enter
```

#### Step 7: Create udev rule to pin interface name (prevent future rename issues)
```bash
# Create permanent name rule based on MAC address
nano /etc/udev/rules.d/10-usb-nic.rules

# Add this line (replace MAC with new device MAC):
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="usblan0"

# Save and reload udev
udevadm control --reload-rules
udevadm trigger
```

#### Step 8: Add new interface to bridge manually
```bash
# Bring up new interface
ip link set enxNEWINTERFACE up

# Add to bridge
ip link set enxNEWINTERFACE master vmbr1

# Verify bridge membership
brctl show vmbr1
# Must show enxNEWINTERFACE under vmbr1
```

#### Step 9: Apply network configuration
```bash
systemctl restart networking

# Verify vmbr1 is up
ip link show vmbr1
# Must show: state UP
```

#### Step 10: Start iKuai VM
```bash
qm start 100
qm status 100
# Must show: status: running
```

#### Step 11: Verify connectivity
```bash
# Check traffic on vmbr1
ip -s link show vmbr1
# RX/TX packets should increase after ~30 seconds

# Check bridge has correct port
brctl show vmbr1
```

Then from an end device connected to WiFi:
- Connect to office WiFi
- Check if IP is assigned (should be 172.16.x.x or 192.168.9.x)
- Test internet access

---

### 8.4 Verification Checklist

After replacement, verify all items below:

| Check | Command / Action | Expected Result |
|---|---|---|
| New USB NIC detected | `ip link show` | New `enx...` interface visible |
| Interface in bridge | `brctl show vmbr1` | New interface listed under vmbr1 |
| vmbr1 UP | `ip link show vmbr1` | `state UP` |
| iKuai VM running | `qm status 100` | `status: running` |
| iKuai LAN reachable | `ping 192.168.9.1` | Replies received |
| iKuai Web UI | Open `http://192.168.9.1` | Login page loads |
| End device gets IP | Connect device to WiFi | Gets 172.16.x.x IP |
| Internet works | Browse on end device | Website loads |

---

### 8.5 Common Issues After USB NIC Replacement

#### Issue: New interface not appearing
```bash
# Check if USB device is recognized
lsusb
# Should show new USB NIC device

# Check kernel log
dmesg | grep -i "usb\|ethernet\|cdc" | tail -20

# If driver missing, install common USB NIC drivers
apt install r8168-dkms        # Realtek
apt install linux-firmware    # General firmware
```

---

#### Issue: vmbr1 shows UP but no traffic
```bash
# Interface may not be in bridge
ip link set enxNEWINTERFACE master vmbr1

# Check cable connection
ethtool enxNEWINTERFACE | grep "Link detected"
# Must show: Link detected: yes
```

---

#### Issue: USB NIC disconnects randomly after replacement
```bash
# Disable USB power saving
for device in /sys/bus/usb/devices/*/power/control; do
    echo 'on' > $device
done

# Make permanent
nano /etc/rc.local
# Add before "exit 0":
for device in /sys/bus/usb/devices/*/power/control; do
    echo 'on' > $device
done
```

---

#### Issue: Interface name changes after reboot
```bash
# Verify udev rule is correct
cat /etc/udev/rules.d/10-usb-nic.rules

# Check MAC address matches new device
ip link show enxNEWINTERFACE
# Confirm MAC matches rule

# Reload udev
udevadm control --reload-rules
udevadm trigger

# Update /etc/network/interfaces to use fixed name "usblan0"
```

---

### 8.6 Rollback Procedure (If Replacement Fails)

If the new USB NIC does not work and you need to revert to the old one:

```bash
# Step 1: Shutdown iKuai VM
qm shutdown 100 && qm wait 100

# Step 2: Remove new USB NIC, re-plug old USB NIC

# Step 3: Restore /etc/network/interfaces
# Replace new interface name back to old interface name
nano /etc/network/interfaces

# Step 4: Restart networking
systemctl restart networking

# Step 5: Re-add old interface to bridge
ip link set enxOLDINTERFACE up
ip link set enxOLDINTERFACE master vmbr1

# Step 6: Start iKuai VM
qm start 100

# Step 7: Verify
brctl show vmbr1
qm status 100
```

---

## 9. Contact & Escalation

### Escalation Path

```
Level 1: End User
  → Try troubleshooting steps in Section 7
  → If unresolved after 5 minutes → escalate

Level 2: IT Administrator
  → Login to Proxmox/iKuai
  → Check logs and configs
  → USB NIC issues → refer to Section 8
  → If unresolved → escalate

Level 3: External Support
  → ISP support line (for internet issues)
  → Hardware vendor support
```

### Important Contacts

| Contact | Details |
|---|---|
| IT Administrator | *(fill in)* |
| ISP Support | *(fill in)* |
| Proxmox Web UI | https://192.168.0.51:8006 |
| iKuai Web UI | http://192.168.9.1 |

---

## Appendix: Quick Command Reference

> For IT staff only

```bash
# SSH into Proxmox
ssh root@192.168.0.51

# VM Management
qm list                    # List all VMs
qm start 100               # Start iKuai VM
qm shutdown 100            # Graceful shutdown iKuai
qm status 100              # Check VM status

# Network
ip link show                          # Show all interfaces
ip addr show                          # Show all IP addresses
brctl show                            # Show bridge members
brctl show vmbr1                      # Show vmbr1 bridge members
ip -s link show vmbr1                 # Show bridge traffic stats
ip link set enxXXXXXX master vmbr1    # Add interface to bridge

# USB NIC
lsusb                                 # List USB devices
dmesg | grep -i "usb\|enx" | tail -20 # USB kernel log
ethtool enxXXXXXX | grep "Link"       # Check link status

# Shutdown system safely
qm shutdown 100 && qm wait 100 && shutdown -h now
```

---

## Appendix: Change Log

| Version | Date | Changes |
|---|---|---|
| 1.0 | May 2026 | Initial document |
| 1.1 | May 2026 | Added Section 8: USB-to-Ethernet Device Replacement Guide |

---