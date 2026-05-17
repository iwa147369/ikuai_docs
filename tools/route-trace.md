# Route Trace (路由追踪)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/yygj/2c876.html

## I. Overview

Traceroute identifies the path taken by packets to reach a destination, showing each intermediate router hop. Useful for diagnosing where connectivity breaks down.

---

## II. How to Use

![Route Trace](https://www.ikuai8.com/images/support/lyzz.png)

| Field | Description |
|---|---|
| IP Address / Domain | The destination to trace. |
| Source Interface | Which iKuai interface to send the trace from. |
| Max Hops | How many hops to display (the trace stops at this count). |
| Timeout per Hop | How long to wait for a reply from each hop (in milliseconds). |

---

## III. How It Works

Traceroute sends packets with incrementally increasing TTL values. Each router that receives a packet decrements the TTL by 1. When the TTL reaches 0, the router returns an ICMP "Time Exceeded" message, revealing its IP address. By starting with TTL=1 and incrementing, traceroute maps each hop along the path.

Some routers silently drop expired TTL packets and do not respond — these appear as `* * *` in the results.
