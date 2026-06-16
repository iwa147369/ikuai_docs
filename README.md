# iKuai Router Documentation

English translation of the iKuai (爱快) soft router documentation.
Source: https://www.ikuai8.com/support/ymgn/lyym/

---

## Table of Contents

- [System Overview](reference/overview.md)

---

### Status Monitor

Real-time visibility into what the router is doing. Covers per-client traffic usage (IPv4 and IPv6), WAN line health, CPU/memory load, active protocol distribution, traffic diversion statistics, and whether traffic-control policies are firing correctly. Also shows connected IP camera management shortcuts, SNMP-monitored switch status, and cloud-registered peripheral devices.

- [Line Monitoring](reference/status-monitor/line-monitoring.md)
- [Terminal Monitoring](reference/status-monitor/terminal-monitoring.md)
- [IPv6 Terminal Monitoring](reference/status-monitor/ipv6.md)
- [Protocol Monitoring](reference/status-monitor/protocol-monitoring.md)
- [Load Monitoring](reference/status-monitor/load-monitoring.md)
- [Policy Monitoring](reference/status-monitor/policy-monitoring.md)
- [Traffic Diversion Monitoring](reference/status-monitor/diversion-monitoring.md)
- [Camera Monitoring](reference/status-monitor/camera-monitoring.md)
- [Switch Monitoring](reference/status-monitor/switch-monitoring.md)
- [Peripheral Device Monitoring](reference/status-monitor/peripheral-monitoring.md)

---

### Network Settings

Core network infrastructure configuration. This is where you set up WAN connections, hand out IPs via DHCP, configure DNS resolution, segment the network with VLANs, define NAT behavior, create address groups for reuse elsewhere, and set up port forwarding, UPnP, DMZ, static routes, and VPN client tunnels.

- [WAN Settings](reference/network/wan.md)
- [WiFi Settings](reference/network/wifi.md)
- [IPv6 Configuration](reference/network/ipv6.md)
- **DHCP**
  - [DHCP Server](reference/network/dhcp-server.md)
  - [Static Leases](reference/network/dhcp-static.md)
  - [Terminal List](reference/network/dhcp-terminal-list.md)
- **DNS**
  - [DNS Settings](reference/network/dns.md)
  - [Multi-WAN DNS](reference/network/dns-multi-wan.md)
- [VLAN](reference/network/vlan.md)
- [NAT](reference/network/nat.md)
- [IP Groups](reference/network/ip-groups.md)
- [MAC Groups](reference/network/mac-groups.md)
- [Static Routes](reference/network/static-routes.md)
- [Current Routing Table](reference/network/routing-table.md)
- [IGMP Proxy](reference/network/igmp.md)
- [IPTV Pass-through](reference/network/iptv.md)
- [Mesh Quick Connect](reference/network/mesh.md)
- [Port Forwarding](reference/network/port-forwarding.md)
- [UPnP](reference/network/upnp.md)
- [DMZ](reference/network/dmz.md)
- **VPN Clients**
  - [VPN Client Overview](reference/network/vpn-client.md)
  - [PPTP Client](reference/network/vpn-pptp.md)
  - [L2TP Client](reference/network/vpn-l2tp.md)
  - [IPSec VPN](reference/network/vpn-ipsec.md)
  - [OpenVPN Client](reference/network/vpn-openvpn.md)

---

### Traffic Control

Bandwidth management and multi-WAN routing. Smart Traffic Control applies protocol-aware QoS across all clients automatically. Rate limiting caps upload/download per IP or MAC. Multi-WAN load balancing spreads connections across lines and can steer specific protocols, ports, or domains to preferred WAN exits. Upload/download separation lets upstream and downstream traffic take different WAN paths.

- [Smart Traffic Control](reference/traffic-control/smart-traffic-control.md)
- [IP Rate Limit](reference/traffic-control/ip-rate-limit.md)
- [MAC Rate Limit](reference/traffic-control/mac-rate-limit.md)
- [Multi-WAN Load Balance](reference/traffic-control/multi-wan-load-balance.md)
- [Upload/Download Separation](reference/traffic-control/upload-download-separation.md)
- [Protocol Routing](reference/traffic-control/protocol-routing.md)
- [Port Routing](reference/traffic-control/port-routing.md)
- [Domain Routing](reference/traffic-control/domain-routing.md)
- [Custom Protocol](reference/traffic-control/custom-protocol.md)
- [Advanced Custom Protocol](reference/traffic-control/advanced-custom-protocol.md)

---

### AC Management (Wireless)

Centralized management of iKuai-compatible wireless access points (APs). The router acts as a wireless controller (AC), pushing configuration to all connected APs, grouping them for bulk changes, and showing which wireless clients are connected to which AP. Supports 802.1X/RADIUS authentication, per-MAC/SSID blacklist/whitelist controls, wireless Terminal VLAN assignment, automated channel and power optimization, and batch AP firmware upgrades. Requires compatible AP hardware running iKuai AP firmware.

- [AC Management Demo](reference/ac/ac-management-demo.md)
- [Wireless Overview](reference/ac/wireless-overview.md)
- [AP List](reference/ac/ap-list.md)
- [AP Groups](reference/ac/ap-groups.md)
- [AP System Upgrade](reference/ac/ap-system-upgrade.md)
- [Wireless Terminals](reference/ac/wireless-terminals.md)
- [Wireless Terminal VLAN](reference/ac/wireless-terminal-vlan.md)
- [Wireless Blacklist/Whitelist](reference/ac/wireless-blacklist-whitelist.md)
- [Wireless Network Optimization](reference/ac/wireless-network-optimization.md)
- [802.1x Authentication](reference/ac/802-1x-authentication.md)

---

### Security Settings

Access control at the packet level. ACL rules allow or block traffic based on IP, port, protocol, and direction. ARP binding ties IP addresses to specific MAC addresses to prevent spoofing and unauthorized access. Connection limiting caps the number of concurrent sessions per IP to protect against abuse or runaway connections. Cloud Firewall adds IPS, antivirus, and threat intelligence as a cloud-activated service. Advanced Settings covers PING/traceroute restrictions, gaming latency tweaks, and TCP-MSS tuning.

- [ACL Rules](reference/security/acl.md)
- [ARP Binding](reference/security/arp.md)
- [Connection Limit](reference/security/connection-limit.md)
- [Cloud Firewall](reference/security/cloud-firewall.md)
- [Advanced Settings](reference/security/advanced-settings.md)

---

### Behavior Control

Per-client internet behavior policies. Block secondary routers sharing the connection, enforce per-protocol allow/deny rules, restrict which QQ accounts can log in from which IPs, block or whitelist websites by domain, intercept and redirect HTTP traffic, and log browsing and IM activity for auditing. All controls apply to HTTP traffic; HTTPS requires protocol-level rules.

- [Network Sharing Control](reference/behavior-control/network-sharing-control.md)
- [Application Protocol Control](reference/behavior-control/app-protocol-control.md)
- [Terminal Name Management](reference/behavior-control/terminal-name-management.md)
- [MAC Access Control](reference/behavior-control/mac.md)
- [QQ Blacklist/Whitelist](reference/behavior-control/qq.md)
- **Behavior Records**
  - [Behavior Record Settings](reference/behavior-control/behavior-record-settings.md)
  - [URL Browsing History](reference/behavior-control/behavior-record-settings/url-browsing-history.md)
  - [IM Records](reference/behavior-control/behavior-record-settings/im-records.md)
  - [Terminal Online/Offline Records](reference/behavior-control/behavior-record-settings/terminal-online-offline.md)
  - [Exempt from Recording](reference/behavior-control/behavior-record-settings/exempt-recording.md)
- **URL Blacklist/Whitelist**
  - [URL Blacklist/Whitelist](reference/behavior-control/url-blacklist-whitelist.md)
  - [Custom URL Library](reference/behavior-control/url-blacklist-whitelist/custom-url-library.md)
  - [Block Entertainment Websites](reference/behavior-control/url-blacklist-whitelist/block-entertainment.md)
- **URL Redirect**
  - [URL Redirect](reference/behavior-control/url-redirect.md)
  - [Keyword Replacement](reference/behavior-control/url-redirect/keyword-replacement.md)
  - [Parameter Replacement](reference/behavior-control/url-redirect/parameter-replacement.md)

---

### Auth & Billing

Authentication and account management for multi-tenant or ISP-style deployments. Clients can be required to log in via PPPoE dial-up or a captive portal (WEB auth) before getting internet access. Push notifications interrupt HTTP browsing to display messages or expiry alerts. VPN server modes (PPPoE, L2TP, PPTP, OpenVPN) allow remote access. Accounts track quotas, expiry dates, and shared session limits.

- **Push Notifications**
  - [Real-time Notification](reference/auth-billing/realtime-notification.md)
  - [Periodic Notification](reference/auth-billing/realtime-notification/periodic-notification.md)
  - [Dial User Expiry Notification](reference/auth-billing/realtime-notification/expiry-notification.md)
  - [Expiry Reminder](reference/auth-billing/realtime-notification/expiry-reminder.md)
- **VPN Servers**
  - [PPPoE Server](reference/auth-billing/vpn-servers/pppoe.md)
  - [L2TP Server](reference/auth-billing/vpn-servers/l2tp.md)
  - [PPTP Server](reference/auth-billing/vpn-servers/pptp.md)
  - [OpenVPN Server](reference/auth-billing/vpn-servers/openvpn.md)
- [WEB Auth Service](reference/auth-billing/web-auth.md)
- **Accounts**
  - [Account Management](reference/auth-billing/accounts/account-management.md)
  - [Internet Access Code](reference/auth-billing/accounts/access-code.md)

---

### System Settings

Router-level configuration that affects the entire system. Covers the core operating mode (NAT/route/bypass), acceleration, time sync, admin accounts, remote access, firmware upgrades, config backup/restore, cloud platform binding, disk partition management for extended storage (behavior logs, video cache, FTP, etc.), dual-machine hot standby failover, ALG for special protocols (FTP/SIP/H.323), app integration (DingTalk/WeChat Work), CPU interrupt tuning, and kernel TCP/UDP timeout parameters.

- [Basic Settings](reference/system/basic-settings.md)
- [Restart / Shutdown](reference/system/restart-shutdown.md)
- [Hardware Info](reference/system/hardware-info.md)
- [Hot Standby](reference/system/hot-standby.md)
- [iKuai Cloud Binding](reference/system/cloud-binding.md)
- [Firmware Upgrade](reference/system/firmware-upgrade.md)
- [System Backup](reference/system/firmware-upgrade/system-backup.md)
- [Application Binding](reference/system/app-binding.md)
- [ALG Settings](reference/system/alg-settings.md)
- [CPU Interrupt Control](reference/system/cpu-interrupt.md)
- [Kernel Settings](reference/system/kernel-settings.md)
- **Admin**
  - [Account Settings](reference/system/admin/account-settings.md)
  - [Remote Access](reference/system/admin/remote-access.md)
- [Disk Management](reference/system/disk-management.md)
- [RAID Management](reference/system/disk-management/raid.md)
- [File Management](reference/system/disk-management/file-management.md)

---

### Log Center

Event history for every major subsystem. Logs cover system startup/shutdown, admin operations, authentication attempts (PPPoE/VPN/WEB), ARP attacks, DHCP assignments, push notification delivery, WAN dial-in/dial-out events, DDNS updates, and wireless client connections. Most logs are circular buffers with fixed entry limits; some require a minimum disk size.

- [System Log](reference/logs/system-log.md)
- [Operation Log](reference/logs/system-log/operation-log.md)
- [Message Notifications](reference/logs/system-log/message-notifications.md)
- [Authentication Log](reference/logs/auth-log.md)
- [ARP Log](reference/logs/auth-log/arp-log.md)
- [Wireless Terminal Log](reference/logs/auth-log/wireless-terminal-log.md)
- [DHCP Log](reference/logs/dhcp-log.md)
- [Push Notification Log](reference/logs/dhcp-log/push-notification-log.md)
- [WAN Dial Log](reference/logs/dhcp-log/wan-dial-log.md)
- [Dynamic DNS Log](reference/logs/dhcp-log/ddns-log.md)

---

### Tools

Built-in diagnostic and calculation utilities. Use these to test connectivity (PING, route trace), measure actual line throughput (speed test), run an automated health check across all subsystems, trace subnet math, or trigger a full router self-diagnostic scan that flags disk errors, rogue DHCP servers, ARP conflicts, and PPPoE anomalies.

- [PING Test](reference/tools/ping.md)
- [Route Trace](reference/tools/route-trace.md)
- [Line Speed Test](reference/tools/speed-test.md)
- [Router Diagnostics](reference/tools/diagnostics.md)
- [Subnet Calculator](reference/tools/subnet-calculator.md)
- [Health Check](reference/tools/health-check.md)

---

### Advanced Applications

Optional services that extend the router beyond basic routing. Includes video/app caching to save WAN bandwidth, a KVM-based virtual machine environment for running third-party OS images on the same hardware, a DDNS client, FTP and HTTP file servers, Wake-on-LAN, port mirroring for traffic analysis, SNMP for network monitoring integration, and Cross-Layer 3 Application for applying MAC-based policies through Layer 3 switches.

- [Wake on LAN](reference/advanced/wake-on-lan.md)
- [Cache Settings](reference/advanced/cache-settings.md)
- [Cache Status](reference/advanced/cache-status.md)
- [Virtual Machine](reference/advanced/virtual-machine.md)
- [Port Mirroring](reference/advanced/port-mirroring.md)
- [Dynamic DNS](reference/advanced/dynamic-dns.md)
- [FTP Service](reference/advanced/ftp.md)
- [HTTP Service](reference/advanced/http.md)
- [Cross-Layer 3 Application](reference/advanced/cross-layer3.md)
- [SNMP Server](reference/advanced/snmp.md)

---

### Guides & Operational Docs

Standalone guides and internal operational documentation that extend beyond the iKuai web UI reference above. Includes infrastructure SOPs, a running list of known issues, and network access setup guides.

- [CPSquare VM Architecture & Network SOP](guides/cpsquare-sop.md)
- [Known Issues](guides/known-issues.md)
- [Xray (VLESS + REALITY) Setup with Multi-Node Failover](guides/xray-reality-setup.md) — personal censorship-circumvention on Ubuntu 20.04, scoped to your own devices, with multi-node IP failover, optional web panels (3X-UI / Marzban), and a domain-name section.
