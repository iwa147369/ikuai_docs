# Protocol Monitoring

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ztjk/7de6a.html

## I. Overview

This page shows the traffic usage broken down by application protocol.

---

## II. How to Use

### Protocol Traffic Pie Chart

Displays the traffic share of each protocol category.

![Protocol Pie Chart](https://www.ikuai8.com/images/support_202109/xy1.png)

> **Note:** The "Last 30 Minutes" pie chart shows the **total** traffic share for each protocol summed over the past 30 minutes — it is not an average.
>
> **Clear Protocol Traffic** — Clicking this button clears all displayed traffic data except for the network connection count, which is not cleared.

---

### Protocol Upload/Download Chart

Displays the upload and download traffic data for LAN hosts per protocol.

![Protocol Traffic Chart](https://www.ikuai8.com/images/support/xyjk1.png)

- Highlighted protocols are selected for display; greyed-out ones are not selected.
- Click on any protocol name below the chart to toggle it on/off and view its individual traffic curve.

![Protocol Selection](https://www.ikuai8.com/images/support_202109/xy2.png)

> **Refresh interval:** This page auto-refreshes every **2 seconds**.

---

## III. Common Issues

### Data still appears after a factory reset

Resetting the router to factory defaults does **not** clear the protocol monitoring data.

---

### How long are the Protocol Monitoring / Policy Monitoring / Load Monitoring logs kept?

Log retention is calculated automatically based on the available log partition size:

| Log Partition Free Space | Retention Period |
|---|---|
| > 300 MB | 31 days |
| > 200 MB | 20 days |
| > 100 MB | 15 days |
| > 50 MB | 10 days |
| > 10 MB | 7 days |
| < 10 MB | 1 day |
