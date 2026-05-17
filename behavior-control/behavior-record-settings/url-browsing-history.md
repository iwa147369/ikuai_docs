# URL Browsing History (网址浏览记录)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/feqef/83d05.html

## I. Overview

Shows the web pages visited by each LAN client routed through iKuai, along with IP/MAC and timestamp information.

![URL Browsing History](https://www.ikuai8.com/images/support_202109/wzlljl1.png)

---

## II. Common Issues

### No records appear

1. **URL Browsing History** is not enabled in **Behavior Control → Behavior Record Settings**.
2. The system disk is 512 MB or smaller — must exceed 512 MB to store records.
3. No clients are routing through iKuai.

### Some IPs are missing from records

1. The IP or MAC is in the Exempt from Recording list.
2. The device doesn't route through iKuai — if behind a secondary router, use the secondary router's WAN IP to look up activity.

### How long are records kept?

Records are stored in the log partition and auto-cleaned when the partition exceeds **80% full** (circular overwrite). If a dedicated **behavior record** partition is mounted, that partition is used instead of the system log partition.

With **syslog external output** (firmware v3.6.4+), records can be sent to an external server with no time limit.
