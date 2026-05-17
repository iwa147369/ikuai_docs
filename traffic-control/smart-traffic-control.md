# Smart Traffic Control (智能流控)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/79f4e.html

## I. Overview

Protocol-based bandwidth management on iKuai routers. Traffic control (流控) is **rate limiting**, not traffic routing — it limits how much bandwidth a protocol can use, it does not determine which WAN line traffic exits through.

Four modes are available: **Off**, **Smart Mode**, **Manual Mode**, and **DingTalk Mode**. The default state is Off.

---

## II. Configuration

### 1. Smart Mode

Smart mode automatically manages protocol priorities using preset profiles. Configure three things: priority preset, line selection, and (optionally) per-IP rate limits.

#### ① Priority Presets

**Custom** — Manually order protocol priorities using the drag-and-drop priority table.

![Custom Priority](https://en.ikuai8.com/attached/php/upload/image/20180627/1530091453989264.png)

**Web Priority** — Prioritizes web browsing traffic. Customizable port list (default: ports 80, 443).

![Web Priority](https://www.ikuai8.com/images/wyyx.jpg)

**Gaming Priority** — Prioritizes gaming traffic. Recommended for gaming environments.

![Gaming Priority](https://www.ikuai8.com/images/yxyx.jpg)

**Video Priority** — Prioritizes video streaming and live streaming. Recommended for entertainment-focused environments.

![Video Priority](https://www.ikuai8.com/images/lkyx.jpg)

**Download Priority** — Dedicates bandwidth to download clients (P2P, download managers). Use with caution — this will deprioritize all other traffic.

![Download Priority](https://www.ikuai8.com/images/xzyx.jpg)

---

#### ② Line Selection

![Line Selection](https://www.ikuai8.com/images/support/znlk.png)

Lines are disabled by default. To enable smart traffic control:
1. Set the upstream/downstream bandwidth for each WAN line
2. Click **Enable** on the line

> **Note:** Adding a line to smart traffic control means the protocol rate limits apply to traffic on that line. Lines not added are unconstrained.

---

#### ③ Independent Rate Limiting

Apply a separate rate limit to specific IP addresses, independent of the smart mode protocol rules.

![Independent Rate Limit](https://en.ikuai8.com/attached/php/upload/image/20170918/1505724116257134.png)

> **Important:**
> - When multiple IPs or an IP range are entered, the upload/download values are **shared** across all those IPs — not per-device.
> - Independent rate limiting only works when smart traffic control is enabled. It has no effect if smart mode is off.

---

### 2. Manual Mode

Allows fully custom protocol priority and bandwidth rules.

![Manual Mode](https://www.ikuai8.com/images/support/znlk1.png)

| Field | Description |
|---|---|
| Name | Custom name for this policy |
| Line | The WAN line(s) this policy applies to |
| Protocol | The application protocol to rate-limit |
| Priority | Priority when line is saturated. 0 = highest, 7 = lowest |
| LAN IP | Restrict this policy to specific internal client IPs |
| Per-Line Up/Down | Min guaranteed and max allowed bandwidth for this protocol on the selected line(s) |
| Per-Device Up/Down | Max upload/download for a single client device using this protocol on the selected line |
| Schedule | Time period during which this policy is active |
| Status | Enabled / Disabled |

> **Note:** Manual mode is a DIY feature. Configure it according to your actual usage environment to achieve the best results.

---

#### Special Protocol Categories

| Protocol | Description |
|---|---|
| HTTP | Web traffic (port 80) |
| Unknown Application | Traffic the router cannot identify — large packets (> 500B). Generally video, downloads, etc. |
| Small Packets | Traffic the router cannot identify — small packets (≤ 500B). Generally gaming and similar latency-sensitive traffic |
| Custom Protocol | Protocols you define yourself in **Traffic Control → Protocol Library** |

> "Small Packets" and "Unknown Application" were split from the original single "Unknown Application" category. 500B is the dividing threshold.

---

#### How Priority Works

Priority is **relative** — it only matters when multiple policies exist. A single policy in isolation has no effective priority.

Protocols with **no traffic control rule** have no assigned priority and can compete for bandwidth with any controlled protocol freely.

Priority levels: Highest → High → Medium → Low → Lowest.

---

#### Per-Line Up/Down Explained

**Left value (minimum guaranteed):** The protocol is always guaranteed at least this much bandwidth on the selected line, regardless of priority pressure from other protocols.

**Right value (maximum):** The maximum bandwidth this protocol can use. `0` means unlimited (auto). Subject to priority constraints — higher-priority protocols can reduce a lower-priority protocol down to its guaranteed minimum.

**If multiple WAN lines are selected:** Set the per-line values as if it were a single line's bandwidth (each line is controlled independently).

**Worked example (10M total bandwidth):**

- Video: guaranteed 3M, max 8M (priority: Medium)
- Download: guaranteed 3M, max 8M (priority: Lowest)

Scenario 1 — Only download traffic: download reaches 8M (its maximum).

Scenario 2 — Download at 8M, then video starts and needs 5M: Download is pushed down by video's higher priority to 5M (10M − 5M). Video gets its 5M.

Scenario 3 — Video wants 8M but download has a 3M guarantee: Download's 3M guarantee is protected. Video can only reach 7M (10M − 3M guaranteed for download). Even if download is only actually using 1–2M at that moment, the guarantee holds.

> **The guaranteed bandwidth floor overrides all priority rules.** Think of it as a reserved seat that no higher-priority protocol can take away.

> **Constraint:** The sum of all minimum guaranteed values across all policies must not exceed the line's total bandwidth (upload and download separately).

---

#### Per-Device Up/Down

The maximum upload/download for a single client device, scoped to the protocol and LAN IP specified in this policy.

---

### 3. DingTalk Mode

A joint iKuai + Alibaba DingTalk feature. Combines iKuai's DPI (Deep Packet Inspection) application recognition engine with DingTalk's organizational user structure to manage bandwidth dynamically.

Unlike static rate limiting, DingTalk mode triggers only when network congestion reaches a threshold — bandwidth utilization is higher when the network is idle.

- Prioritizes by **person** first: when congestion occurs, users in the high-speed tier get priority.
- Prioritizes by **protocol** second: web browsing and DingTalk are highest priority by default; P2P downloads and video are lowest.

![DingTalk Mode Config](https://en.ikuai8.com/attached/php/upload/image/20181213/1544670074891554.png)

> **Note:**
> 1. DingTalk smart traffic control applies to the person — including any devices connected via that person's shared access password.
> 2. Both the router's DingTalk mode and the DingTalk mobile app must have smart traffic control configured.

---

## III. Traffic Control Settings Reference

![Traffic Control Reference](https://www.ikuai8.com/attached/php/upload/image/20170829/1503992247243227.png)

---

## IV. Common Issues

### Manual traffic control is rate limiting, not routing

The **Line** field in manual mode means: "when traffic using this protocol travels over this WAN line, apply these limits." It does **not** route traffic to that line. The line selection in traffic control and the line selection in Protocol Routing are separate concepts.

### Manual traffic control isn't taking effect

1. **Check the status:**
   - If it shows "Closed" — smart mode (一键流控) is active, which overrides manual mode. Disable smart mode first.
   - If it shows "Enabled" — verify that policies are actually added and set to Enabled status.
2. **Verify WAN line bandwidth is correctly configured.** Traffic control needs accurate bandwidth values in the WAN settings.
   - Example: 10M upload, 100M download → enter **1280 KB** upload, **12800 KB** download.
   - Conversion: 1 MB = 8 Mb; 1 Mb = 128 KB.
