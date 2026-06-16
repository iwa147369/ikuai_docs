# DHCP Terminal List

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/dhcp/zdlb.html

## I. Overview

Displays information about all clients that have obtained an IP address from the DHCP server.

---

## II. How to Use

![DHCP Terminal List](https://www.ikuai8.com/images/support/dhcpzdlb11.png)

| Field / Action | Description |
|---|---|
| Bound Interface | The LAN interface the client is connected to |
| Status | How the IP was assigned (see below) |
| Add to Blacklist | Blocks the device's MAC address from accessing the internet. To remove the block, go to **Behavior Control → MAC Blacklist** |
| Add to Static Assignment | Binds this client's current IP to its MAC address, so it always receives the same IP via DHCP |
| One-Click IP Reclaim | Reclaim offline IPs or all IPs in the pool. Available in firmware v3.5.0+ |

**Status values:**

| Status | Meaning |
|---|---|
| Dynamic | IP was assigned dynamically from the DHCP pool |
| Static | IP was assigned via a DHCP static binding — the client always gets this specific IP |
| Scan Assigned | The router detected this IP already in use on the LAN and reserved it to prevent ARP conflicts |

---

## III. Common Issues

### A client doesn't appear in the terminal list

1. DHCP is not enabled — no entries will be shown.
2. The client has a manually configured static IP, not obtained via DHCP.
3. The client's IP was assigned by a **different DHCP server** on the LAN (not iKuai), or the entry is covered by a **DHCP static assignment** or the **Compatible with ARP Binding** option.

To diagnose: check **Log Center → Function Logs → DHCP Log**. If there is no DHCP request entry for the client's MAC address, the device is not obtaining its IP through the iKuai router.
