# Security Advanced Settings

**Source:** https://www.ikuai8.com/support/ymgn/lyym/aqsz/2020-09-08-03-40-04.html

## I. Overview

Advanced Settings consolidates additional firewall and network protection options for centralized management.

---

## II. PING and Traceroute Controls

| Option | Description |
|---|---|
| Prohibit LAN PING to router | Prevents local clients from pinging the router's LAN and WAN IP addresses |
| Prohibit WAN PING to router | Blocks external networks from pinging the router |
| Prohibit client tracert commands | Prevents users from running traceroute commands |

---

## III. Gaming and Performance

| Option | Description |
|---|---|
| Hijack all PING values | Sets reported game latency to zero. Note: encrypted game traffic (e.g., Tencent games — LOL, CF) cannot be intercepted |
| Discard invalid connection access | Filters corrupted or invalid packets to conserve bandwidth. Generally recommended enabled; disabling may cause download anomalies |

---

## IV. TCP Configuration

| Parameter | Description |
|---|---|
| TCP Maximum Segment Size (TCP-MSS) | Default value is `1400`. Adjust only when needed: try `1360` if IPSec connections fail or authentication issues arise |
