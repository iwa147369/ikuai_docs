# Upload/Download Path Separation (上下行分离)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/ea195/6a97f.html

## I. Overview

This feature routes the upload (outbound) and download (return) paths of a session through different WAN lines — the outbound packets leave on one line while the inbound reply packets arrive on another.

**How it works:** Only when upload traffic matches the policy rule does the feature activate. The corresponding download traffic for that session then returns via the download line specified in the rule.

If multiple download lines are selected, the load ratio between them is 1:1.

**Network requirements:** The upstream gateway of the upload line must accept packets that have the download line's IP as the source. This depends on the ISP and is not universally supported. Test your environment first.

---

## II. Configuration

![Upload/Download Separation](https://www.ikuai8.com/images/support/sxxfl.png)

| Field | Description |
|---|---|
| Protocol | TCP, UDP, TCP+UDP, ICMP, or Any |
| Upload Line | The WAN line for outbound traffic |
| Download Line | The WAN line for return (inbound) traffic |
| Source Address | The LAN client IP(s) this rule applies to. Leave blank for all. |
| Destination Address | The external destination to match. Leave blank for all. |
| Source Port | The starting port to match. Leave blank for all. |
| Destination Port | The destination port to match. Leave blank for all. |
| Remark | Optional label |

**Priority:** This feature uses a "match-then-apply" mechanism. When upload traffic matches the rule, it takes effect with the highest effective priority — overriding default gateway, load balancing, and protocol routing settings for that session.

Rules are evaluated top-to-bottom; first match wins.

---

## III. Example

**Topology:**

![Example Topology](https://www.ikuai8.com/attached/php/upload/image/20180906/1536223725332958.png)

Primary router: eth1 → LAN1 (192.168.134.1), eth2 → LAN1 extended NIC with extended IP 192.168.133.1. Secondary router: WAN1 and WAN2 connected to the two subnets.

**Config:**

![Example Config](https://www.ikuai8.com/attached/php/upload/image/20180906/1536224664526898.png)

When traffic exits via WAN1, the source IP is masqueraded as 192.168.133.2. The upstream gateway must be able to recognize and forward this IP for the split-path behavior to work.

**Important:** For the download traffic to return on a specific line, the upload traffic must first exit via the corresponding line. If the source IP (`192.168.10.2` in the diagram example) needs to use WAN1 as the upload line, configure WAN1 as the default gateway or create a port/protocol routing rule to direct that IP's traffic to WAN1.

![Additional Example](https://www.ikuai8.com/attached/php/upload/image/20180906/1536224848766234.png)

---

## IV. Common Issues

### Rule conflict resolution

When multiple rules conflict, the first rule (highest position in the list) takes effect.

![Conflict Example](https://www.ikuai8.com/images/support/sxxfl1.png)

### How to test whether your ISP supports this feature

To test if WAN1 supports receiving the WAN2 line's IP as the source address:
1. Copy WAN2's line configuration into WAN1's settings and save.
2. If LAN clients can still browse the internet normally through WAN1 with WAN2's IP configured, the upstream gateway accepts it and the feature will work.
3. Repeat the same test in reverse to verify WAN2.
