# iKuai Router Documentation

English translation of the iKuai (爱快) soft router documentation.
Source: https://www.ikuai8.com/support/ymgn/lyym/

---

## Table of Contents

- [System Overview](overview.md)

---

### Status Monitor

Real-time visibility into what the router is doing. Covers per-client traffic usage (IPv4 and IPv6), WAN line health, CPU/memory load, active protocol distribution, traffic diversion statistics, and whether traffic-control policies are firing correctly. Also shows connected IP camera management shortcuts, SNMP-monitored switch status, and cloud-registered peripheral devices.

- [Line Monitoring](status-monitor/line-monitoring.md)
- [Terminal Monitoring](status-monitor/terminal-monitoring.md)
- [IPv6 Terminal Monitoring](status-monitor/ipv6.md)
- [Protocol Monitoring](status-monitor/protocol-monitoring.md)
- [Load Monitoring](status-monitor/load-monitoring.md)
- [Policy Monitoring](status-monitor/policy-monitoring.md)
- [Traffic Diversion Monitoring](status-monitor/diversion-monitoring.md)
- [Camera Monitoring](status-monitor/camera-monitoring.md)
- [Switch Monitoring](status-monitor/switch-monitoring.md)
- [Peripheral Device Monitoring](status-monitor/peripheral-monitoring.md)

---

### Network Settings

Core network infrastructure configuration. This is where you set up WAN connections, hand out IPs via DHCP, configure DNS resolution, segment the network with VLANs, define NAT behavior, create address groups for reuse elsewhere, and set up port forwarding, UPnP, DMZ, static routes, and VPN client tunnels.

- [WAN Settings](network/wan.md)
- [WiFi Settings](network/wifi.md)
- [IPv6 Configuration](network/ipv6.md)
- **DHCP**
  - [DHCP Server](network/dhcp-server.md)
  - [Static Leases](network/dhcp-static.md)
  - [Terminal List](network/dhcp-terminal-list.md)
- **DNS**
  - [DNS Settings](network/dns.md)
  - [Multi-WAN DNS](network/dns-multi-wan.md)
- [VLAN](network/vlan.md)
- [NAT](network/nat.md)
- [IP Groups](network/ip-groups.md)
- [MAC Groups](network/mac-groups.md)
- [Static Routes](network/static-routes.md)
- [Current Routing Table](network/routing-table.md)
- [IGMP Proxy](network/igmp.md)
- [IPTV Pass-through](network/iptv.md)
- [Mesh Quick Connect](network/mesh.md)
- [Port Forwarding](network/port-forwarding.md)
- [UPnP](network/upnp.md)
- [DMZ](network/dmz.md)
- **VPN Clients**
  - [VPN Client Overview](network/vpn-client.md)
  - [PPTP Client](network/vpn-pptp.md)
  - [L2TP Client](network/vpn-l2tp.md)
  - [IPSec VPN](network/vpn-ipsec.md)
  - [OpenVPN Client](network/vpn-openvpn.md)

---

### Traffic Control

Bandwidth management and multi-WAN routing. Smart Traffic Control applies protocol-aware QoS across all clients automatically. Rate limiting caps upload/download per IP or MAC. Multi-WAN load balancing spreads connections across lines and can steer specific protocols, ports, or domains to preferred WAN exits. Upload/download separation lets upstream and downstream traffic take different WAN paths.

- [Smart Traffic Control](traffic-control/smart-traffic-control.md)
- [IP Rate Limit](traffic-control/ip-rate-limit.md)
- [MAC Rate Limit](traffic-control/mac-rate-limit.md)
- [Multi-WAN Load Balance](traffic-control/multi-wan-load-balance.md)
- [Upload/Download Separation](traffic-control/upload-download-separation.md)
- [Protocol Routing](traffic-control/protocol-routing.md)
- [Port Routing](traffic-control/port-routing.md)
- [Domain Routing](traffic-control/domain-routing.md)
- [Custom Protocol](traffic-control/custom-protocol.md)
- [Advanced Custom Protocol](traffic-control/advanced-custom-protocol.md)

---

### AC Management (Wireless)

Centralized management of iKuai-compatible wireless access points (APs). The router acts as a wireless controller (AC), pushing configuration to all connected APs, grouping them for bulk changes, and showing which wireless clients are connected to which AP. Supports 802.1X/RADIUS authentication, per-MAC/SSID blacklist/whitelist controls, wireless Terminal VLAN assignment, automated channel and power optimization, and batch AP firmware upgrades. Requires compatible AP hardware running iKuai AP firmware.

- [AC Management Demo](ac/ac-management-demo.md)
- [Wireless Overview](ac/wireless-overview.md)
- [AP List](ac/ap-list.md)
- [AP Groups](ac/ap-groups.md)
- [AP System Upgrade](ac/ap-system-upgrade.md)
- [Wireless Terminals](ac/wireless-terminals.md)
- [Wireless Terminal VLAN](ac/wireless-terminal-vlan.md)
- [Wireless Blacklist/Whitelist](ac/wireless-blacklist-whitelist.md)
- [Wireless Network Optimization](ac/wireless-network-optimization.md)
- [802.1x Authentication](ac/802-1x-authentication.md)

---

### Security Settings

Access control at the packet level. ACL rules allow or block traffic based on IP, port, protocol, and direction. ARP binding ties IP addresses to specific MAC addresses to prevent spoofing and unauthorized access. Connection limiting caps the number of concurrent sessions per IP to protect against abuse or runaway connections. Cloud Firewall adds IPS, antivirus, and threat intelligence as a cloud-activated service. Advanced Settings covers PING/traceroute restrictions, gaming latency tweaks, and TCP-MSS tuning.

- [ACL Rules](security/acl.md)
- [ARP Binding](security/arp.md)
- [Connection Limit](security/connection-limit.md)
- [Cloud Firewall](security/cloud-firewall.md)
- [Advanced Settings](security/advanced-settings.md)

---

### Behavior Control

Per-client internet behavior policies. Block secondary routers sharing the connection, enforce per-protocol allow/deny rules, restrict which QQ accounts can log in from which IPs, block or whitelist websites by domain, intercept and redirect HTTP traffic, and log browsing and IM activity for auditing. All controls apply to HTTP traffic; HTTPS requires protocol-level rules.

- [Network Sharing Control](behavior-control/network-sharing-control.md)
- [Application Protocol Control](behavior-control/app-protocol-control.md)
- [Terminal Name Management](behavior-control/terminal-name-management.md)
- [MAC Access Control](behavior-control/mac.md)
- [QQ Blacklist/Whitelist](behavior-control/qq.md)
- **Behavior Records**
  - [Behavior Record Settings](behavior-control/behavior-record-settings.md)
  - [URL Browsing History](behavior-control/behavior-record-settings/url-browsing-history.md)
  - [IM Records](behavior-control/behavior-record-settings/im-records.md)
  - [Terminal Online/Offline Records](behavior-control/behavior-record-settings/terminal-online-offline.md)
  - [Exempt from Recording](behavior-control/behavior-record-settings/exempt-recording.md)
- **URL Blacklist/Whitelist**
  - [URL Blacklist/Whitelist](behavior-control/url-blacklist-whitelist.md)
  - [Custom URL Library](behavior-control/url-blacklist-whitelist/custom-url-library.md)
  - [Block Entertainment Websites](behavior-control/url-blacklist-whitelist/block-entertainment.md)
- **URL Redirect**
  - [URL Redirect](behavior-control/url-redirect.md)
  - [Keyword Replacement](behavior-control/url-redirect/keyword-replacement.md)
  - [Parameter Replacement](behavior-control/url-redirect/parameter-replacement.md)

---

### Auth & Billing

Authentication and account management for multi-tenant or ISP-style deployments. Clients can be required to log in via PPPoE dial-up or a captive portal (WEB auth) before getting internet access. Push notifications interrupt HTTP browsing to display messages or expiry alerts. VPN server modes (PPPoE, L2TP, PPTP, OpenVPN) allow remote access. Accounts track quotas, expiry dates, and shared session limits.

- **Push Notifications**
  - [Real-time Notification](auth-billing/realtime-notification.md)
  - [Periodic Notification](auth-billing/realtime-notification/periodic-notification.md)
  - [Dial User Expiry Notification](auth-billing/realtime-notification/expiry-notification.md)
  - [Expiry Reminder](auth-billing/realtime-notification/expiry-reminder.md)
- **VPN Servers**
  - [PPPoE Server](auth-billing/vpn-servers/pppoe.md)
  - [L2TP Server](auth-billing/vpn-servers/l2tp.md)
  - [PPTP Server](auth-billing/vpn-servers/pptp.md)
  - [OpenVPN Server](auth-billing/vpn-servers/openvpn.md)
- [WEB Auth Service](auth-billing/web-auth.md)
- **Accounts**
  - [Account Management](auth-billing/accounts/account-management.md)
  - [Internet Access Code](auth-billing/accounts/access-code.md)

---

### System Settings

Router-level configuration that affects the entire system. Covers the core operating mode (NAT/route/bypass), acceleration, time sync, admin accounts, remote access, firmware upgrades, config backup/restore, cloud platform binding, disk partition management for extended storage (behavior logs, video cache, FTP, etc.), dual-machine hot standby failover, ALG for special protocols (FTP/SIP/H.323), app integration (DingTalk/WeChat Work), CPU interrupt tuning, and kernel TCP/UDP timeout parameters.

- [Basic Settings](system/basic-settings.md)
- [Restart / Shutdown](system/restart-shutdown.md)
- [Hardware Info](system/hardware-info.md)
- [Hot Standby](system/hot-standby.md)
- [iKuai Cloud Binding](system/cloud-binding.md)
- [Firmware Upgrade](system/firmware-upgrade.md)
- [System Backup](system/firmware-upgrade/system-backup.md)
- [Application Binding](system/app-binding.md)
- [ALG Settings](system/alg-settings.md)
- [CPU Interrupt Control](system/cpu-interrupt.md)
- [Kernel Settings](system/kernel-settings.md)
- **Admin**
  - [Account Settings](system/admin/account-settings.md)
  - [Remote Access](system/admin/remote-access.md)
- [Disk Management](system/disk-management.md)
- [RAID Management](system/disk-management/raid.md)
- [File Management](system/disk-management/file-management.md)

---

### Log Center

Event history for every major subsystem. Logs cover system startup/shutdown, admin operations, authentication attempts (PPPoE/VPN/WEB), ARP attacks, DHCP assignments, push notification delivery, WAN dial-in/dial-out events, DDNS updates, and wireless client connections. Most logs are circular buffers with fixed entry limits; some require a minimum disk size.

- [System Log](logs/system-log.md)
- [Operation Log](logs/system-log/operation-log.md)
- [Message Notifications](logs/system-log/message-notifications.md)
- [Authentication Log](logs/auth-log.md)
- [ARP Log](logs/auth-log/arp-log.md)
- [Wireless Terminal Log](logs/auth-log/wireless-terminal-log.md)
- [DHCP Log](logs/dhcp-log.md)
- [Push Notification Log](logs/dhcp-log/push-notification-log.md)
- [WAN Dial Log](logs/dhcp-log/wan-dial-log.md)
- [Dynamic DNS Log](logs/dhcp-log/ddns-log.md)

---

### Tools

Built-in diagnostic and calculation utilities. Use these to test connectivity (PING, route trace), measure actual line throughput (speed test), run an automated health check across all subsystems, trace subnet math, or trigger a full router self-diagnostic scan that flags disk errors, rogue DHCP servers, ARP conflicts, and PPPoE anomalies.

- [PING Test](tools/ping.md)
- [Route Trace](tools/route-trace.md)
- [Line Speed Test](tools/speed-test.md)
- [Router Diagnostics](tools/diagnostics.md)
- [Subnet Calculator](tools/subnet-calculator.md)
- [Health Check](tools/health-check.md)

---

### Advanced Applications

Optional services that extend the router beyond basic routing. Includes video/app caching to save WAN bandwidth, a KVM-based virtual machine environment for running third-party OS images on the same hardware, a DDNS client, FTP and HTTP file servers, Wake-on-LAN, port mirroring for traffic analysis, SNMP for network monitoring integration, and Cross-Layer 3 Application for applying MAC-based policies through Layer 3 switches.

- [Wake on LAN](advanced/wake-on-lan.md)
- [Cache Settings](advanced/cache-settings.md)
- [Cache Status](advanced/cache-status.md)
- [Virtual Machine](advanced/virtual-machine.md)
- [Port Mirroring](advanced/port-mirroring.md)
- [Dynamic DNS](advanced/dynamic-dns.md)
- [FTP Service](advanced/ftp.md)
- [HTTP Service](advanced/http.md)
- [Cross-Layer 3 Application](advanced/cross-layer3.md)
- [SNMP Server](advanced/snmp.md)
