# Multi-WAN Load Balancing (多线负载)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/ea195.html

## I. Overview

Multi-WAN load balancing serves two purposes depending on the ISP setup:

- **Same ISP, multiple lines** — Balance traffic across lines and aggregate bandwidth.
- **Different ISPs, multiple lines** — Route traffic to the appropriate ISP's line based on destination IP (e.g. Unicom traffic exits via the Unicom line), optimizing routing and speed.

---

## II. Configuration

![Multi-WAN Load Balance](https://www.ikuai8.com/attached/php/upload/image/20180109/1515467916188241.png)

### Load Balancing Mode

| Mode | Behavior |
|---|---|
| Real-time Connection Count | Dynamically adjusts assignment to keep connection count proportionally balanced across lines. Balanced connections ≠ balanced traffic. |
| New Connection Count | Assigns new connections in round-robin proportions without checking current interface load. |
| Real-time Traffic | Balances based on current traffic load, keeping bandwidth proportionally distributed. |
| Source IP + Destination IP | Connection-count balancing (new connections as base), but ensures same source+destination IP pair always uses the same interface. More stable than pure connection balancing. |
| Source IP + Destination IP + Destination Port | Like above, but adds destination port to the sticky key — more granular and more balanced than the previous mode. |
| Source IP | Connection-count balancing, but keeps all traffic from the same source IP on the same interface. |
| Source IP + Source Port | Connection-count balancing, with source IP+port as the sticky key. |

**Recommendations:**
- For PPPoE dial lines: use **Real-time Connection Count** — many ISPs limit connections per dial session; balancing connection count prevents any single line from getting congested.
- For sessions that must not split across lines (specific protocol/website/IP): use **Source IP + Destination IP** or **Source IP + Destination IP + Destination Port**.
- If post-load speed tests are disappointing: try **Source IP** or **Source IP + Source Port**.

---

### ISP Routing (运营商)

![ISP Routing](https://www.ikuai8.com/attached/php/upload/image/20170918/1505728259199645.png)

Each WAN line can be assigned an ISP tag. Traffic destined for that ISP's IP ranges will preferentially exit through the corresponding line.

Built-in ISP tags: **All**, **Telecom (电信)**, **Unicom (联通)**, **Mobile (移动)**, **Education (教育)**. Custom ISPs can also be added.

| Rule | Description |
|---|---|
| All | The line handles all traffic regardless of ISP |
| Specific ISP | Only destination IPs belonging to that ISP exit through this line |

> **Notes:**
> - If all WAN lines are from the same ISP, set the ISP to **All** for each line.
> - Custom ISP entries: one IP/CIDR per line (e.g. `192.168.6.1/24`). Maximum 5,000 entries per batch; add more using the same ISP name in additional batches.
> - Rules are matched in order — first match wins. Earlier rules take priority.

---

### Load Ratio (负载比例)

Default ratio: `1`. For lines in the same policy, set the ratio to the simplified proportion of their bandwidths.

Example: 10M + 30M Telecom lines → ratio `1:3`.

> **Important:** The ratio is relative to other lines **within the same policy**. It has no effect on lines in different policies.

![Load Ratio Config](https://www.ikuai8.com/attached/php/upload/image/20180730/1532917001717018.png)

---

## III. Multi-WAN Scenario Examples

### Scenario 1 — Same ISP, bandwidth aggregation

**Environment:** 2+ Telecom lines, same bandwidth (e.g. 4M upload / 100M download each).

**Goal:** Aggregate bandwidth across all lines.

**Config:** Add all lines to one policy, ISP = All, ratio = 1:1 (or matching proportions).

![Scenario 1](https://www.ikuai8.com/attached/php/upload/image/20180730/1532916898766383.png)

> Only same-ISP lines should be placed in a single "All ISP" policy.

---

### Scenario 2 — Telecom + Unicom, ISP-based routing

**Environment:** 1 Telecom line + 1 Unicom line.

**Goal:** Telecom traffic (and gaming) exits via Telecom; Unicom traffic exits via Unicom; other traffic uses the default gateway.

**Config:** Create one policy for Telecom (ISP = Telecom) and one for Unicom (ISP = Unicom).

![Scenario 2](https://www.ikuai8.com/attached/php/upload/image/20180730/1532916914972273.png)

---

### Scenario 3 — 2 Telecom + 1 Unicom

**Environment:** 2 Telecom lines + 1 Unicom line.

**Goal:** Unicom traffic exits via Unicom; all other traffic is load-balanced across the two Telecom lines.

**Config:** Policy 1: Unicom line, ISP = Unicom. Policy 2: Both Telecom lines, ISP = All, ratio proportional to bandwidth.

![Scenario 3](https://www.ikuai8.com/attached/php/upload/image/20180730/1532916931911702.png)

---

### Scenario 4 — Mixed lines with protocol routing

**Environment:** 1 Telecom fiber + 1 Unicom fiber + 3 Mobile ADSL + 1 Telecom ADSL.

**Goal:** Telecom and Unicom fiber lines handle gaming; all other traffic is distributed to ADSL lines.

**Config:** Use ISP-specific routing to assign gaming protocol traffic to Telecom/Unicom fiber; use protocol routing (分流) to send remaining traffic to ADSL lines. Protocol routing has higher priority than load balancing.

![Scenario 4 config](https://www.ikuai8.com/images/support/dxfz11.png)

![Scenario 4 detail](https://www.ikuai8.com/attached/php/upload/image/20180730/1532916968414983.png)

---

## IV. Load Ratio Examples

### Case 1 — Matching upload and download ratios

Two Telecom lines: 10M symmetric and 20M symmetric.
- Upload ratio: 10:20 = 1:2
- Download ratio: 10:20 = 1:2
- Ratios match → set policy ratio to **1:2**.

Two Telecom lines: 2M/10M and 4M/20M.
- Upload: 1:2, Download: 1:2 → set ratio to **1:2**.

### Case 2 — Upload and download ratios conflict

Two Telecom lines: 10M symmetric fiber + 2M/20M ADSL.
- Upload ratio: 10:2 = 5:1
- Download ratio: 10:20 = 1:2
- Ratios cannot be unified → **do not use load balancing** for these two lines.
- Instead: use the 10M fiber as the default gateway and configure protocol routing to use the ADSL line for specific traffic.

### Case 3 — Approximately matching ratios

Two Telecom lines: 2M/20M + 4M/50M.
- Upload: 1:2
- Download: 20:50 ≈ 2:5 ≈ 1:2 (approximate)
- Ratios are close → set ratio to **1:2**, then monitor line usage and adjust (try 1:3 or 2:3) or combine with protocol routing to balance load.

> **Summary for setting ratios:**
> 1. All lines in a policy must be from the same ISP.
> 2. Calculate simplified ratios for both upload and download separately.
> 3. If upload and download ratios match exactly — use that ratio directly.
> 4. If ratios approximately match — use the approximate ratio and tune with monitoring.
> 5. If ratios cannot be unified — do not combine those lines in a single load balancing policy. Use default gateway + protocol routing instead.
