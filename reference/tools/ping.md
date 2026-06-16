# PING Test (PING测试)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/yygj/ping.html

## I. Overview

Ping sends ICMP echo requests to a target address and reports response time. Use it to verify network connectivity and measure latency.

---

## II. How to Use

![Ping Test](https://www.ikuai8.com/images/ping33.jpg)

| Field | Description |
|---|---|
| IP Address / Domain | The destination to ping. |
| Protocol Stack | IPv4 or IPv6. |
| Protocol Type | ICMP or TCP. When TCP is selected, a port number is required (requires firmware v3.7.10+). |
| Source Interface | Specify which iKuai interface to send pings from (e.g., LAN1, WAN1, WAN2). Leave blank to use the default. |
| Ping Count | The number of ping packets to send. |

---

## III. Understanding Results

- **Reply from X.X.X.X: bytes=32 time=Xms TTL=X** — connection is working; lower time = faster connection.
- **Request timed out** — the target is unreachable or ICMP is blocked.

> **Note:** Some addresses or regions block ICMP traffic, causing ping to time out even when the destination is reachable.

**Bandwidth unit reference:**
- 100 Mbps ≈ 12.5 MB/s ≈ 12,207 KB/s
- 1 Mbps ≈ 120 KB/s (practical estimate accounting for overhead)
