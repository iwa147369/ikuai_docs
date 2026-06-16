# IPv6 Configuration

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/ipv6.html

## I. Overview

IPv6 is the next-generation IP protocol designed to replace IPv4. iKuai routers support IPv6 for both WAN and LAN, including multi-line IPv6 service.

---

## II. External Network (WAN) Setup

| Parameter | Description |
|---|---|
| Interface | WAN line that supports IPv6 |
| Access Method | DHCPv6 client (dynamic), static IP, or relay mode (v3.7.6+) |
| IPv6 Prefix | Assigned by the ISP |
| Client DUID Identifier | Random or default (v3.7.12+) |
| Address & Gateway | Auto-obtain or manually enter ISP-provided values |
| DNS Servers | Primary and secondary IPv6 DNS from ISP |

**Relay Mode:** When the optical modem operates in router mode and provides only one IPv6 address, relay mode allows downstream devices and secondary routers to also obtain that address.

---

## III. Internal Network (LAN) Setup

| Parameter | Description |
|---|---|
| Configuration Type | Auto-acquire (from WAN prefix), Static, or Relay mode |
| Prefix Allocation Length | Auto, /60, /62, or /64. Note: a /64 ISP prefix can only fully allocate to one LAN port |

**DHCPv6 Modes:**

| Mode | Description |
|---|---|
| Stateful | Server manages and assigns addresses from a pool |
| Stateless | Clients auto-configure using MAC address and Router Advertisements (RA) |
| Stateful + Stateless | Hybrid; server assigns addresses and also sends RA |

---

## IV. Multi-Line IPv6 Service

**Prerequisites:**
- Router bound to iKuai Cloud platform
- Service activated via the cloud console
- Enterprise version: 3 lines by default; Free version: 1 line

**Setup:**
1. Enable the service via **iKuai Cloud → Network Inspection → IPv6 Multi-Line Service**.
2. Configure WAN ports with IPv6 support.
3. Bind LAN interfaces to specific WAN lines.
4. Configure prefix static allocation rules for load distribution.

---

## V. Relay Mode Example

**Topology:** Optical modem → Main router → Secondary router / computer

1. Enable **WAN relay** on the main router.
2. Enable **LAN relay** and select the interface connected to the secondary device.
3. Configure the secondary router's WAN/LAN per ISP specifications.

> Single-layer relay only; one-to-one line mapping.

---

## VI. Troubleshooting

| Issue | Solution |
|---|---|
| Slow IPv6 web access | Disable IPv6 DNS if the website doesn't support IPv6 |
| Cannot obtain IPv6 prefix | Set optical modem to bridge mode; let the router handle PPPoE authentication |
| Need to disable IPv6 access | Enable stateful-only DHCPv6 with MAC blacklist, or configure ACL IPv6 protocol filters |

---

## VII. Version Requirements

| Feature | Minimum Version |
|---|---|
| Multi-line IPv6 | v3.7.3+ |
| Docker interface support | v3.7.4+ |
| Relay mode | v3.7.6+ |
| DUID identifier customization | v3.7.12+ |
