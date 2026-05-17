# Behavior Record Settings (行为记录设置)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/feqef.html

## I. Overview

Enable logging for client browsing history, QQ/IM login activity, and terminal online/offline events.

![Behavior Record Settings](https://www.ikuai8.com/images/xwjlsz1.png)

---

## II. Settings

| Option | Description |
|---|---|
| URL Browsing History | Log the web pages visited by each client. |
| IM Login History | Log QQ login and logout events. |
| Application Traffic Stats | Log the top 20 applications by traffic for each terminal. **Enterprise edition only.** |

**Minimum hardware requirement:** System disk capacity must exceed **512 MB** for behavior records to be stored.

Logged data can be viewed under:
- **Behavior Control → URL Browsing History**
- **Behavior Control → IM Records**

---

## III. Common Issues

### Behavior records are enabled but the log is empty

- Disk capacity is 512 MB or less — must be larger for recording to work.
- No clients are routing through iKuai.

### Some IP addresses are missing from the records

- The IP or MAC is in the **Exempt from Recording** list (**Behavior Control → Behavior Record Settings → Exempt List**).
- The device is not routing through iKuai — or it is behind a secondary router, in which case look up the secondary router's WAN IP instead.

### How long are behavior records kept?

Maximum retention: **6 months**. When the log partition exceeds 75% full, the oldest 5% of records are automatically deleted.

If **syslog external output** is enabled (firmware v3.6.4+), records can be stored externally with no time limit.
