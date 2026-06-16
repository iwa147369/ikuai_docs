# Multi-WAN DNS (多线路DNS)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/dns/q.html

## I. Overview

Assign a dedicated DNS server to each WAN line. When DNS traffic exits through a specific WAN line, the router forces it to use that line's configured DNS server for domain resolution.

Supports **import**, **export**, and per-rule **enable/disable**.

![Multi-WAN DNS](https://www.ikuai8.com/images/support/dxldns1.png)

---

## II. How It Works

1. **Traffic must exit the correct line first.** The rule only activates when DNS traffic actually goes out through the matching WAN line.
2. **Post-match rule with highest effective priority.** The DNS replacement happens after routing, so it functions as the last step — and therefore overrides any other DNS assignments for that line.
3. **Domain routing integration.** When a domain is routed to a specific line via domain routing (域名分流), multi-WAN DNS automatically uses that line's DNS entry to resolve that domain. This is especially useful for VPN lines.
4. **Veto power.** Multi-WAN DNS can override DNS servers set elsewhere in the system, but it does not affect Force Proxy or Cache mode settings.

---

## III. Interaction with Other DNS Modes

| Combination | Result |
|---|---|
| DNS Proxy mode + Multi-WAN DNS | Only the default gateway line's DNS policy applies. The router itself always sends DNS from the default gateway, so only that line's multi-WAN DNS rule can match. |
| DNS Cache mode + Multi-WAN DNS | Both work together — cache stores per-interface responses. Requires DNS traffic to actually exit different lines to populate the cache for each. |
| Reverse Proxy + Multi-WAN DNS | Reverse proxy only activates in proxy mode or cache mode. |
| DoH mode + Multi-WAN DNS | Non-domain-routed domains resolve via DoH. Domain-routed domains use the multi-WAN DNS entry for that domain's line. Domain routing has higher priority than force-proxy DNS mode. |

> **Important:** The DNS primary/secondary server fields should contain actual public DNS server addresses — **not the gateway IP**. Setting the gateway as DNS causes clients to fail to resolve domains.

---

## IV. Example — VPN Line with Domain Routing

**Environment:** WAN1 = default Unicom line; VPN = foreign VPN connection.

**Goal:** Foreign websites use the VPN line with its own DNS.

**Steps:**

1. Add a VPN client connection and confirm the Local IP is assigned (dial succeeded).

   ![VPN Dial](https://www.ikuai8.com/attached/php/upload/image/20180125/1516871628430656.png)

2. In **Traffic Control → Routing → Domain Routing**, specify that foreign domains route through the VPN line.

   ![Domain Routing](https://www.ikuai8.com/attached/php/upload/image/20180125/1516871656868297.png)

3. In **Network Settings → DNS Settings → Multi-WAN DNS**, add DNS entries for WAN1 (using ISP DNS) and the VPN line (using a DNS that resolves foreign domains correctly, e.g. 8.8.8.8).

   ![Multi-WAN DNS Config](https://www.ikuai8.com/attached/php/upload/image/20180125/1516871681270026.png)

   With this setup, domain-routed foreign domains use the VPN line's DNS for resolution, ensuring correct IP addresses are returned.
