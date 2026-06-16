# Connection Limit (连接数限制)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/aqsz/gfer4.html

## I. Overview

Limits the number of simultaneous connections for a specific IP address and protocol type.

---

## II. Field Reference

![Connection Limit](https://www.ikuai8.com/images/support_202109/ljsxz1.png)

| Field | Description |
|---|---|
| Internal IP | The client IP address (or range) to limit. |
| Protocol | The protocol to limit (TCP, UDP, or Any). |
| External Port | Optional. Limit connections only to a specific destination port. |
| Connection Count | The maximum allowed connections for the specified IP. |

**Important notes:**
1. This only limits connections **routed through the router**. Local LAN-to-router connections (internal traffic) are not limited.
2. Due to implementation constraints, the actual connection count may exceed the limit by 10–20% in some cases. To reliably stay within a target, set the limit to 80% of the desired maximum.
3. Inbound connections from the WAN to the router cannot be limited.

---

## III. Usage Examples

**A. Limit total connections for an IP**

- Internal IP: `1.1.1.1`, Protocol: Any, Connection Count: 128
- Limits all connections from `1.1.1.1` to 128 total.

**B. Limit connections for a specific protocol**

- Internal IP: `1.1.1.1`, Protocol: TCP, Connection Count: 128
- Limits TCP connections from `1.1.1.1` to 128.

**C. Limit connections to a specific port**

- Internal IP: `1.1.1.1`, Protocol: TCP, External Port: 80, Connection Count: 300
- Limits `1.1.1.1`'s connections to port 80 to 300.
