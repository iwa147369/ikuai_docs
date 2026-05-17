# Static Routes

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/94829.html

## I. Overview

Static routes are routing entries manually configured by the administrator. They do not update automatically when network topology changes — the admin must update them manually. Static routes are suitable for simple, stable network environments where the topology is well understood.

---

## II. Configuration

![Static Route Settings](https://www.ikuai8.com/images/jtly111.png)

| Field | Description |
|---|---|
| Protocol Stack | IPv4 or IPv6. IPv6 support requires firmware v3.7.16+. |
| Line | Which interface (WAN or LAN) to use to reach the destination subnet. |
| Destination Address | The target subnet to route toward. |
| Subnet Mask | The subnet mask for the destination network. |
| Gateway | The next-hop IP address. |
| Metric | Route priority. Lower metric = higher priority. |

---

## III. Example

**Goal:** Allow PC1 (connected to the primary router) to access devices on the secondary router's LAN (e.g. PC2).

![Network Diagram](https://www.ikuai8.com/images/support/hf1.png)

Add a static route on the primary router pointing to the secondary router's LAN:

![Static Route Config](https://www.ikuai8.com/images/support/jtly2.png)

---

## IV. Route Selection Logic

When multiple routes conflict:

1. The route with the **lower metric** takes precedence.
2. If metrics are equal and destination addresses match but subnet masks differ, the route with the **more specific (larger) mask** takes precedence.

![Route Priority Example](https://www.ikuai8.com/attached/php/upload/image/20181127/1543312402195149.png)

In the example above, `/24` (255.255.255.0) takes precedence over `/16`.

---

## V. Full-Network Default Route

iKuai does not support entering a traditional default route (`0.0.0.0/0`). To create an equivalent full-network static route pointing back to a specific next-hop, use these two entries:

- `0.0.0.1 / 255.128.0.0` (covers `0.0.0.0–127.255.255.255`)
- `128.0.0.0 / 255.128.0.0` (covers `128.0.0.0–255.255.255.255`)

![Full-Network Route](https://www.ikuai8.com/images/jtly1111.jpg)

Together these two entries cover the entire IPv4 address space.
