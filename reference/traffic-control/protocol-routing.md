# Protocol Routing (协议分流)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/ea195/c2c94.html

## I. Overview

In a multi-WAN environment, route specific application protocols out through specific WAN lines.

**Enhanced Routing (增强分流):** When enabled, increases the success rate of protocol identification and routing.

> **Note:** "Unknown Application" and "Small Packets" protocols cannot be routed this way. All other recognizable protocols can be routed.

---

## II. Configuration

Assign a protocol to a WAN line. Click **Add**, select the routing line, select the protocol(s), enter the source IP address, then confirm.

![Protocol Routing](https://www.ikuai8.com/images/support/xy.png)

**Line Binding:** When checked, if the assigned line drops, traffic stays on that line (even when down) and does not automatically switch to a healthy line.
(Hardware firmware v3.5.4+; free firmware v3.5.2+)

![Protocol Routing Detail](https://www.ikuai8.com/images/xyfl222.jpg)

**Load distribution modes (when multiple lines are selected):**

| Mode | Behavior |
|---|---|
| New Connection Count | Assigns connections in round-robin proportion |
| Source IP | Traffic from the same source IP uses the same interface |
| Source IP + Destination IP | Same source+destination IP pair always uses the same interface |

> **Limit:** A single protocol routing rule cannot contain more than 64 protocol entries — exceeding this causes the rule to fail.

---

## III. Example

**Goal:** Route download and video traffic from `192.168.1.2`–`192.168.1.200` through WAN2.

![Protocol Routing Example](https://www.ikuai8.com/images/xyfl123.jpg)

Fill in the source address range. Do not leave the source address blank — use a specific IP or range (e.g. `192.168.1.2-192.168.1.200`).

**How it works:** The most recently added rule has higher priority. If time schedules don't conflict, each rule is active during its own time window. All rules are matched; when rules conflict, the later-added one takes effect.

---

## IV. Routing Priority Order

When multiple routing features are configured simultaneously:

**Static Routes > Domain Routing > Port Routing > Protocol Routing > Multi-WAN Load Balance > Default Gateway**

---

## V. Common Issues

### Line failover behavior

When multiple lines are selected in a protocol routing rule and one drops:
- **PPPoE lines:** Traffic redistributes to the remaining lines.
- **DHCP or Static IP lines:** All traffic falls back to the **default gateway** line.

### Protocol routing not working

1. Verify the routing line works by itself — test single-line access, and check **System Status → Line Monitoring** for detection success.
2. Protocol misidentification — the router may not recognize the protocol on first encounter.
3. Protocol recognized but routing fails on the first pass — this is expected behavior:
   - When a protocol flow first passes through iKuai, the router identifies it and caches the result (protocol name → destination IP).
   - The first time, routing may not succeed. On subsequent connections to the same destination, the cache matches and routing succeeds.
   - Cache is cleared on router reboot or fresh install.
   - The cache grows over time, improving routing success rates.
   - Example: A streaming service may use many different server IPs; after all IPs are cached, routing will succeed consistently.

### Using manual traffic control after protocol routing

- Protocols routed to a specific line: set their traffic control values against that line's bandwidth.
- "Unknown Application" and "Small Packets" always use the default gateway — set their traffic control against the default gateway's bandwidth.
- Add a fallback traffic control rule for protocol-routed protocols on the default gateway line, in case routing fails for a session.

### Protocol routing with manual traffic control — which line to use

When a protocol is routed to a specific line, configure its traffic control using that line's bandwidth. Unrouted protocols use the default gateway's bandwidth.

---

## VI. Scenario Examples

### Scenario 1 — Telecom + Unicom, ISP-specific gaming traffic

**Environment:** WAN1 = Telecom, WAN2 = Unicom

**Goal:** Gaming traffic bound for Telecom IPs exits via WAN1; gaming traffic bound for Unicom IPs exits via WAN2; all other traffic exits via WAN1 (default gateway).

**Config:**
1. In WAN settings, set WAN1 (Telecom) as the default gateway. Do not configure multi-WAN load balancing.

   ![Default Gateway](https://www.ikuai8.com/images/support_202109/mrwg12.png)

2. Add a protocol routing rule: gaming protocols → WAN2 (Unicom), with ISP = Unicom.
3. Add another rule: gaming protocols → WAN1 (Telecom), with ISP = Telecom.

Telecom gaming traffic matches the Telecom rule and exits via WAN1. Unicom gaming traffic matches the Unicom rule and exits via WAN2. Everything else uses the default gateway (WAN1).
