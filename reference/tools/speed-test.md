# Line Speed Test (线路测速)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/yygj/57d92.html

## I. Overview

Tests the actual upload and download speed of a selected WAN line. Based on the same mechanism as Speedtest.net — sends requests and measures the maximum download throughput.

---

## II. How to Use

![Line Speed Test](https://www.ikuai8.com/images/support/xlcs.png)

Select the WAN line to test, then click the speed test button.

**Notes:**
1. The speed test runs within the current network — it is an included measurement, not an isolated dedicated test.
2. If the maximum and minimum measured speeds differ significantly, re-run the test. A persistent large gap indicates ISP network instability.
3. The test does not interrupt users' existing connections.

---

## III. Common Issues

### "Failed to get resource"

**Cause 1:** DNS misconfiguration preventing domain resolution.
**Fix:** Set a correct DNS server in Network Settings.

**Cause 2:** Interface shows "interface error."
This means the line has not obtained a valid IP address or line detection has failed.
**Fix:** Check the line's connectivity (e.g., for PPPoE — can it dial successfully and get an IP?).

**Cause 3:** Cannot connect to the speed test server.
iKuai's speed test uses Speedtest.net infrastructure. Try opening speedtest.net directly on a PC connected to the same WAN line to compare.

---

## IV. Bandwidth Unit Reference

| Unit       | Equivalent                            |
| ---------- | ------------------------------------- |
| 1 Mbps     | 1,000 Kbps = 1,000,000 bps            |
| 1 MBytes/s | 1,024 KBytes/s = 8 Mbps               |
| 100 Mbps   | ≈ 12,500 KB/s ≈ 12.2 MBytes/s         |
| 1 Mbps     | ≈ 120 KB/s (practical, with overhead) |

> Note: lowercase `b` = bit; uppercase `B` = byte. 1 Byte = 8 bits.
