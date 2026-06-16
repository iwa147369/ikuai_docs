# IM Records (IM记录)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/feqef/im.html

## I. Overview

Shows QQ login and logout events for LAN clients routed through iKuai.

![IM Records](https://www.ikuai8.com/images/1123.png)

Records include: QQ account number, login/logout time, client IP, and MAC address.

**Remarks** shown are synced from the MAC remark system (or from the PPPoE account remark if applicable).

---

## II. Retention

IM records are stored for a maximum of **1 month**, regardless of disk size. Requires a log partition larger than **300 MB** to retain one month of data.

If a dedicated behavior record partition is mounted, records are stored there instead of the system log partition.

With **syslog external output** (firmware v3.6.4+), records can be sent externally with no time limit.

---

## III. Common Issues

### No IM records appear

1. **IM Login History** is not enabled in **Behavior Control → Behavior Record Settings**.
2. System disk is 512 MB or smaller.
3. No clients are routing through iKuai.

### Some IPs are missing from records

1. The IP or MAC is in the Exempt from Recording list.
2. The device routes through a secondary router — use the secondary router's WAN IP instead.
