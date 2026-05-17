# Basic Settings (基础设置)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/jcsz.html

## I. Overview

The Basic Settings page configures core system information for the iKuai router.

---

## II. Configuration

![Basic Settings](https://www.ikuai8.com/images/jcsz11.png)

### System Information

| Field | Description |
|---|---|
| Device Name | A label for this iKuai device. |
| Internet Mode | Three options: **NAT4**, **NAT1**, or **Route Mode**. |
| Link Mode | Three options: **Backbone Mode**, **Bypass Mode**, or **SD-WAN Bridge**. |

**Internet Mode details:**

- **NAT4 (Symmetric NAT):** The most secure NAT type. This is the default.
- **NAT1 (Full Cone NAT):** Less restrictive NAT. Useful for gaming or P2P. Not recommended for general use — it lowers security by reducing barriers for inbound connections from the WAN. Not recommended for CDN nodes or peer-earning projects.
- **Route Mode:** No NAT is applied. LAN IP addresses are forwarded to the WAN unmasked. Use only when all LAN IPs are public addresses. **Port forwarding does not work in route mode.** In route mode, the router itself uses LAN1's IP as its source IP when accessing the internet.

**Link Mode details:**

- **Backbone Mode (主干模式):** Default. Use when iKuai is the primary gateway for the network.
- **Bypass Mode (旁路模式):** Only supported on X86 large routers. Use when iKuai is not the main gateway but needs to manage APs, DingTalk authentication, DingTalk Flash Transfer, or web authentication.
- **SD-WAN Bridge:** Transparent bridge mode. Enables data access between networks without changing the existing network topology.

**Acceleration Mode:**

| Mode | Description |
|---|---|
| Hardware Acceleration | Only supported on MIPS architecture small routers (A120/M1/M20, etc.). Data is forwarded directly through the NIC, bypassing CPU computation. Reduces CPU usage but disables per-NIC traffic statistics. |
| Software Acceleration | Uses the Linux kernel acceleration algorithm. Data still processed by CPU. Equivalent to the old acceleration mode. Some features will stop working when enabled. |

> **Important:** The following features are **disabled** when acceleration mode is enabled:
> Line Monitoring, Protocol Monitoring, Multi-WAN Load Balancing, Protocol Routing, Port Routing, Domain Routing, Upload/Download Separation, Smart Traffic Control, IP Rate Limiting, MAC Rate Limiting, Custom Protocol, Advanced Custom Protocol, auth server rate limiting (PPPoE/web/L2TP/PPTP), ARP Binding (the "block non-bound MACs" feature), and Advanced Settings ping tests.

> **Notes:**
> 1. In NAT mode, all router operations use the WAN IP as the source address.
> 2. In route mode, all router operations (including ping tests and line detection) use the LAN IP.
> 3. Route mode: to access internal ports from outside, see the iKuai FAQ for port access in route mode.

---

### Time Settings

| Field | Description |
|---|---|
| System Time | The time used by all time-based functions on the router. |
| International Timezone | Supports international time zones. Default is UTC+8 (Beijing). |
| Configuration Mode | Use built-in NTP servers or set the time manually. |
| NTP Server | iKuai can act as an NTP server for LAN devices. Custom server address can be specified. |
| Sync Interval | How often to sync from an NTP server. Default: 60 minutes. |
| NTP Service | Enable/disable the NTP server function. Takes effect when LAN devices use the iKuai gateway as their NTP server. |

Modules that use the system time for schedule-based rules (in load order):
**ACL Rules > Port Forwarding > NAT Rules > IP Rate Limiting > MAC Rate Limiting > Port Routing > Protocol Routing**

---

## III. Common Issues

**I selected Full Cone NAT (NAT1) but detection tools still show a different NAT type.**

First, test with the WAN cable connected directly to a PC. The upstream ISP device may also be performing NAT, which causes the final detected NAT type to differ from what iKuai is configured to use. Also, the Fanshu feature has higher port priority and may affect detection results.
