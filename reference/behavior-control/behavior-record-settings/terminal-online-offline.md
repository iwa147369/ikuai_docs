# Terminal Online/Offline Records (终端上下线记录)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/feqef/twgh.html

## I. Overview

Shows online and offline events for LAN clients routed through iKuai.

![Terminal Online/Offline Records](https://www.ikuai8.com/images/support/zdsxxjl.png)

Each record includes: client IP and MAC, cumulative upload/download traffic, total online duration, device type (e.g., PC, AndroidXX), and remarks.

---

## II. Notes

- Records are retained for a maximum of **1 month**. Requires a log partition larger than **300 MB** for the full month.
- If the **"Auto-Clear at Midnight"** option is enabled in Terminal Monitoring, connected devices are cleared at midnight each day, and their traffic history is logged here — even without explicitly enabling the Terminal Online/Offline Record option in Behavior Record Settings.
- If a dedicated behavior record partition is mounted, records use that partition instead of the system log partition.

---

## III. Common Issues

### No records appear

1. **Terminal Online/Offline Records** is not enabled in Behavior Record Settings.
2. Disk is 512 MB or smaller.
3. No clients are routing through iKuai.

### Some IPs are missing

1. IP or MAC is in the Exempt from Recording list.
2. Device is behind a secondary router — use that router's WAN IP.

### Retention summary

- Max: **6 months** for URL browsing and behavior records (auto-delete oldest 5% when 75% full).
- **1 month** for IM records and terminal records (partition > 300 MB required).
- With syslog external output: unlimited (firmware v3.6.4+).
