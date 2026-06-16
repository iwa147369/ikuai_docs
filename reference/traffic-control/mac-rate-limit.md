# MAC Rate Limiting (MAC限速)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/70793/mac.html

## I. Overview

Per-MAC-address bandwidth rate limiting. Set upload and download speed limits for specific MAC addresses.

---

## II. Configuration

Click **Add** to create a new rule.

![MAC Rate Limit](https://www.ikuai8.com/images/ipv6xs.jpg)

Enter the MAC address, rate limit mode, upload speed, download speed, schedule, time range, and remark, then save.

| Field | Description |
|---|---|
| Protocol Stack | Limit IPv4 traffic, IPv6 traffic, or both. (IPv6 limiting requires firmware v3.7.7+) |
| Line | The WAN line this rate limit applies to. |
| Rate Limit Mode | **Individual** — each MAC address gets its own limit. **Shared** — multiple MAC addresses share the same bandwidth pool. |
| Upload | Maximum upload speed. |
| Download | Maximum download speed. |
| Schedule | The time period during which the rule is active. |
| Time Range | Active hours within the schedule. |
| Remark | Optional label. |

![MAC Rate Limit Fields](https://www.ikuai8.com/images/ipv6xs1.jpg)

> **Note:** When multiple MAC addresses need rate limiting, combine them into a single rule for easier management rather than creating separate rules for each.
