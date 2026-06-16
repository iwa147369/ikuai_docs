# ARP Binding (ARP绑定)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/aqsz/arp.html

## I. Overview

ARP (Address Resolution Protocol) resolves IP addresses to MAC addresses. ARP binding is used for LAN access control and protection against ARP spoofing/viruses. By binding a specific IP to a specific MAC address, the network becomes more secure and stable.

---

## II. Binding Modes

### Block Non-Bound MACs from Accessing the Internet

Only ARP-bound clients can access the internet; unbound clients are blocked. Firmware v3.7.6+ allows selecting which LAN interface(s) to apply this restriction to.

![Block Non-Bound](https://www.ikuai8.com/images/support_202109/arp11.png)

### Compatible with DHCP Static Assignment

The router automatically adds bound MAC–IP pairs to DHCP Static Assignment in the background. These entries do not appear in the DHCP Static Assignment list.

### Normal Binding vs. Unique Binding

- **Normal Binding:** Binds an IP to a MAC. Multiple entries may coexist.
- **Unique Binding:** Strict one-to-one binding. Devices in unique binding mode cannot be reached by web authentication pages and cannot access the internet unless explicitly permitted.

### Import / Export

Export the ARP binding list as a TXT file. Import also requires TXT format. Import/export only works with entries in the **Bound** state.

**Import notes:**
1. The import format must exactly match the format exported by iKuai — mismatched IP/MAC pairs or incorrect format will fail.
2. Do **not** use "Block Non-Bound MACs" and "Auto-Scan and Bind MACs" at the same time — the block feature will not work.
3. Do **not** bind WAN port ARP entries. ISPs may replace upstream equipment at any time; a bound WAN ARP will break internet connectivity when the upstream device changes. Signs of this problem: disconnecting after ~1 minute, or WAN showing an exclamation mark while a direct PC connection works.

---

## III. Common Issues

### ARP list shows IPs outside the router's LAN subnet

Auto-scan can discover devices physically connected to the router, including the WAN interface's IP and link-local (169.254.x.x) addresses. This is normal.

### ARP binding MAC/IP doesn't match the actual client

ARP binding only associates a MAC with an IP address — it does not cause the DHCP server to assign that IP to the device. To assign a fixed IP, configure DHCP Static Assignment instead.

### Clients get a different IP than their ARP binding

The LAN interface's DHCP service is not enabled, or another DHCP server is running on the network.

### Web authentication behavior when "Block Non-Bound MACs" is enabled

| Binding State | Web Authentication Behavior |
|---|---|
| Unbound | Authentication page appears normally; internet access requires successful auth. |
| Normal Binding | Authentication page appears normally; internet access requires successful auth. |
| Unique Binding | Authentication page cannot appear; internet access is blocked. |
