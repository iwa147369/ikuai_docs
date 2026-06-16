# IP Rate Limiting (Terminal Rate Limit)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/70793.html

## I. Overview

Per-IP bandwidth rate limiting. Set upload and download speed limits for specific IP addresses or IP ranges.

---

## II. Configuration

Click **Add** to create a new rule.

![IP Rate Limit](https://www.ikuai8.com/images/support/ipxs22.png)

| Field | Description |
|---|---|
| Line | The WAN line this rate limit applies to. |
| LAN IP | The internal IP address or range to limit. |
| Protocol | TCP, UDP, TCP+UDP, or Any. |
| Source Port | The starting port (for port-specific limits). |
| Destination Port | The target destination port to match. |
| Rate Limit Mode | **Individual** (each IP gets its own limit) or **Shared** (all IPs in the range share the limit). |
| Upload | Maximum upload speed. |
| Download | Maximum download speed. |
| Schedule | The time period during which the rule is active. |
| Time Range | Active hours within the schedule. |
| Remark | Optional label. |

![IP Rate Limit Fields](https://www.ikuai8.com/images/support/ipxs11.png)

> **Notes:**
> - The upload/download values define the **maximum** speed the IP(s) can reach — not a guaranteed minimum.
> - When multiple IPs or IP ranges need the same rate limit, combine them into a single rule for easier management.
