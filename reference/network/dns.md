# DNS Settings

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/dns.html

## I. Overview

DNS (Domain Name System) is a distributed database on the internet that maps domain names to IP addresses, allowing users to browse the web by hostname rather than by raw IP. The DNS protocol runs over UDP on port 53.

- **DNS Proxy** — The router acts as a DNS proxy server, forwarding client DNS queries to an upstream DNS server.
- **DNS Reverse Proxy** — The router acts as a local DNS server. Add domain-to-IP mappings directly on the router; matching queries resolve locally.
- **Multi-WAN DNS** — Traffic leaving through each WAN port uses the DNS server configured for that specific line.

---

## II. How to Use

### DNS Acceleration Service

This section covers DNS Cache mode, DNS Proxy (UDP) mode, DNS Proxy (DoH) mode, Third-Party Proxy, and Reverse Proxy.

![DNS Acceleration](https://www.ikuai8.com/images/DNS11.png)

| Field | Description |
|---|---|
| Aging Time | How long (in seconds) before stale cached records are cleared. Default: **300 seconds**. Mainly applies to cache mode. (v3.7.20+) |
| Block AAAA Records (IPv6) | When checked, IPv6 DNS resolution is disabled. (v3.7.7+) |

> **Note:** Enabling "Block AAAA Records" may cause IPv6 connectivity checks to fail even when the IPv6 address is correct.

![Block AAAA](https://www.ikuai8.com/images/ipv6123.png)

---

### DNS Cache Mode

![Cache Mode](https://www.ikuai8.com/images/huancms.png)

When a client requests a domain, the router first checks its local cache for a matching IP. If found, it replies immediately from the cache. If not, it performs a normal DNS lookup and caches the result for future requests.

This reduces DNS response time by serving local replies.

> **Note:** Cache mode does **not** support clients pointing their DNS at the router's gateway address (DNS Proxy mode does support this).
>
> If clients show a "WLAN security risk" warning, try switching off cache mode or changing to another DNS mode.

---

### DNS Proxy (UDP) Mode

![Proxy Mode](https://www.ikuai8.com/images/dailms.png)

| Field | Description |
|---|---|
| Primary DNS | The upstream DNS server to use (e.g. ISP's DNS). |
| Secondary DNS | Fallback DNS; only used if the primary doesn't respond. |

**How it works:** DNS proxy only takes effect when clients have their DNS set to the router's LAN IP (gateway address). The router then forwards client queries to the configured upstream DNS server.

---

### DNS Proxy (DoH — DNS over HTTPS) Mode

![DoH Mode](https://www.ikuai8.com/images/daildoh.png)

DoH encrypts DNS queries over HTTPS, protecting user privacy by preventing ISPs or man-in-the-middle actors from intercepting or hijacking DNS lookups.

| Field | Description |
|---|---|
| DoH Request URL | The DNS-over-HTTPS endpoint. iKuai defaults to Tencent Cloud DNS. Contact your DNS provider for their DoH URL. |

---

### DNS Force Proxy

When **Force Client DNS Proxy** is enabled, the router intercepts all outbound DNS traffic and redirects it through the configured DNS proxy — regardless of what DNS server the client has configured.

Effect: No matter what DNS address is set on a client device, the router overrides it and uses the proxy DNS configured on this page.

---

### Third-Party Proxy Mode

![Third-Party Proxy](https://www.ikuai8.com/images/disanfdl.png)

Forces all LAN clients to use a specified third-party DNS server (typically an internal DNS server you host yourself). The router ensures that the third-party DNS server itself is not intercepted when performing its own upstream lookups.

| Field | Description |
|---|---|
| Alternate DNS 1 / 2 / 3 | Additional fallback DNS servers for third-party proxy mode. (v3.7.7+) |

---

### DNS Reverse Proxy

![Reverse Proxy](https://www.ikuai8.com/images/dnsfxdl.jpg)

The router acts as a local DNS server. When a client requests a domain, the router first checks local entries. If a match is found, the local IP is returned. Otherwise, the query goes to the primary DNS upstream.

Supports Proxy mode (resolving specific domains toward a target server). Requires firmware v3.7.9+.

**Supported domain formats:** `*.ikuai8.com`, `ikuai8.com`, or a specific FQDN.  
**Not supported:** `*.ikuai8.*` wildcard patterns.

| Field | Description |
|---|---|
| Domain | The domain to resolve locally. |
| Proxy IP Type | IPv4 or IPv6. |
| Proxy IP | The IP address to return for the matched domain. |
| Effective IP Range | Which LAN IPs this rule applies to. Can be an IP address or range. |

> **Important:** For reverse proxy to work correctly:
> 1. Enable **DNS Proxy Service**
> 2. Enable **Force Client DNS Proxy**
> 3. Client DNS must be set to the LAN gateway address
>
> In **cache mode** or **force proxy mode**, reverse proxy is active. In standard proxy mode, reverse proxy only works if clients are pointed at the gateway IP — it does not work if clients use an external DNS directly.

---

## III. Common Issues

### How to configure DNS in a multi-WAN environment

1. **If port-based routing is configured** and port 80 traffic routes over a specific WAN line — set DNS to the DNS server for that line.
2. **If all WAN lines are from the same ISP** (load balancing, identical DNS) — configure DNS normally; all lines share the same DNS.
3. **If multiple ISPs are in use** with load balancing and protocol routing — configure the **default gateway line's DNS** as primary DNS. This is because DNS resolution happens first (before protocol matching rules apply), so DNS traffic initially exits through the default gateway line.

### What does "DNS Proxy Service" do?

Enables the router to act as a DNS server for the LAN. Internal clients can point their DNS at the router's gateway IP.

### What does "Force Client DNS Proxy" do?

Overrides whatever DNS address clients have configured. All DNS queries passing through the router are redirected to the DNS configured on this page.

### How to configure DNS for a dual-ISP setup (e.g. gaming cafes)

A common pattern in China: southern regions use China Telecom as primary, China Unicom as backup; northern regions use Unicom as primary, Telecom as backup. In edge cases (e.g. 100M Telecom + 10M Unicom), test actual DNS resolution speed to determine which should be primary.

### Why isn't reverse proxy taking effect?

Ensure all three conditions are met:
1. **DNS Proxy Service** is enabled
2. **Force Client DNS Proxy** is enabled
3. The client's DNS is set to the LAN gateway address

### If both multi-WAN DNS and proxy are enabled, which takes effect?

Multi-WAN DNS takes priority over DNS Proxy.

### Cache mode vs. proxy mode — which is better?

Cache mode is generally faster. Advantages of cache mode:
1. Supports multiple DNS servers
2. Supports different DNS servers per WAN line
3. Unused cache entries are cleared after 5 minutes
4. Active cache entries refresh at half the TTL value from the DNS server response

### If both DNS settings (proxy) and multi-WAN DNS are configured, which applies?

1. **DNS proxy + multi-WAN DNS:** Only the multi-WAN DNS entry for the default gateway line takes effect. The router itself uses the default gateway for its own DNS queries, so only the matching multi-WAN entry applies.
2. **DNS cache + multi-WAN DNS:** Both take effect — DNS traffic going out different WAN ports gets cached separately per line.
3. Reverse proxy requires proxy mode with force proxy enabled.
4. **Never set the router's gateway address as the primary/secondary DNS** in the DNS proxy settings — this will prevent clients from accessing the internet.
