# NAT Rules

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/nat.html

## I. Overview

NAT (Network Address Translation) is a WAN access technology that translates private (internal) IP addresses into legal public IP addresses. It solves the problem of limited public IPv4 addresses and also helps protect internal hosts from external attacks by hiding them behind the router's public IP.

---

## II. How to Use

![NAT Rules](https://www.ikuai8.com/images/support/natzf.png)

Three actions are available:

### Filter

When the router operates in NAT mode, all internal traffic is NAT-translated by default. The **Filter** action exempts a specific IP or IP range from NAT translation — traffic from that IP exits without being translated.

Use case: Special environments where certain hosts must use their original source address.

### Source NAT (SNAT)

Translates the **source address** of outgoing packets. You can specify both the incoming interface and the outgoing interface.

Use case: Internal clients routing through a WAN line that uses NAT mode — their private IPs must be translated to the WAN line's public IP before exiting.

### Destination NAT (DNAT)

Translates the **destination address** of incoming packets. Only the incoming interface can be specified.

| Field | Description |
|---|---|
| In Interface | The interface where the traffic arrives |
| Out Interface | The interface through which the traffic exits (SNAT only) |

---

## III. Examples

### Example A — Mixed routing modes on two WAN lines

**Environment:**
- WAN1 (China Telecom) — must use routed mode
- WAN2 (China Unicom) — must use NAT mode

**Goal:** Both lines work simultaneously.

**Configuration:**
1. In **System Settings → Basic Settings**, set the system to **Routed Mode** — this allows internal traffic to exit through WAN1 normally.
2. For WAN2: traffic arriving at WAN2 in routed mode will be rejected by the ISP gateway (which only accepts WAN2's own IP). Create a Source NAT rule to translate the client's IP to WAN2's external IP.

Example: Client `192.168.1.100` exits through WAN2 (external IP `2.2.2.2`).

![NAT SNAT Rule](https://www.ikuai8.com/images/n.png)

First, use port/protocol routing to route client `192.168.1.100` out through WAN2:

![Port Routing](https://www.ikuai8.com/images/support/dc.png)

Then create a Source NAT rule: when traffic from `192.168.1.100` exits through WAN2, translate the source to `2.2.2.2` (WAN2's external IP).

---

### Example B — Multiple public IPs on a single WAN line

**Environment:** One fiber line with two public IPs: `1.1.1.1` and `2.2.2.2`.

**Goal:** Route some LAN clients through `1.1.1.1` and others through `2.2.2.2`.

![Multi-IP NAT](https://www.ikuai8.com/images/support/natgz222.png)

Create two Source NAT rules, each mapping a different LAN subnet to a different public IP on the same WAN interface.

---

### NAT Filter Example

Exempt a specific IP from NAT:

![NAT Filter](https://www.ikuai8.com/images/support/natgz.png)

With this rule, `192.168.0.2` is not translated when exiting through WAN2 — it uses its original private IP and therefore cannot access the internet via WAN2.

---

> **Important:** The NAT translation address must be an IP address that actually exists on the WAN interface being used. Using an IP that does not exist on that WAN will cause the translated traffic to fail.
