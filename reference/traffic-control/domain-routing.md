# Domain Routing (域名分流)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/ea195/75960.html

## I. Overview

Route traffic for specific domain names through specific WAN lines.

---

## II. Configuration

**Example:** Route all LAN client traffic to `baidu.com` through WAN2.

![Domain Routing Config](https://www.ikuai8.com/images/contents/20220929163547-72b94dd37011fc744dbce26869af6094.png)

**Domain entry format:** Enter `baidu.com` to route all domains ending in `baidu.com` (i.e., the domain and all its subdomains) through the specified line.

**Prerequisite:** Domain routing requires Multi-WAN DNS to be configured first. Go to **Network Settings → DNS Settings → Multi-WAN DNS** and set a DNS server for each WAN line.

![Multi-WAN DNS](https://www.ikuai8.com/images/support/dxldns.png)

**Rule priority:** Rules are evaluated in the order they were added. Earlier rules have higher priority; once a match is found, evaluation stops.

---

## III. Common Issues

### Routing priority order

When multiple routing features are active simultaneously, the priority from highest to lowest is:

**Static Routes > Domain Routing > Port Routing > Protocol Routing > Multi-WAN Load Balance > Default Gateway**

### Domain routing not working

1. The assigned WAN line is down — verify the line is healthy.
2. Multi-WAN DNS is not configured — domain routing relies on DNS to resolve domain names per line. Without multi-WAN DNS, the router cannot direct DNS responses to the correct interface.

---

## IV. Limits

- Maximum **255 rules** total.
- Each rule supports at most **1,000 domain entries**.
