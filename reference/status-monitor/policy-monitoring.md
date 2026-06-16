# Policy Monitoring (策略监控)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ztjk/f9f28.html

## I. Overview

Displays the real-time status of traffic control policies once they have been configured.

---

## II. How to Use

By default, shows policy status across all WAN lines. Use the line selector in the top-left to filter by a specific line.

![Policy Monitoring](https://www.ikuai8.com/images/support/cel.png)

> **Note:** This page auto-refreshes every **3 seconds**.

---

## III. Common Issues

### Why is there no data on the page?

Data only appears when Smart Traffic Control is set to **Smart Mode** or **Manual Mode**. If it is set to "Disabled," this page will be empty.

![Traffic Control Mode](https://www.ikuai8.com/attached/php/upload/image/20180716/1531715490761859.png)

### Why don't all WAN lines appear?

The missing lines were not activated when switching to Smart Mode or Manual Mode. Ensure each line is enabled in the traffic control settings.

![Line Activation](https://www.ikuai8.com/attached/php/upload/image/20180716/1531715781727380.png)

### Why is there data here after a factory reset?

A factory reset does **not** clear policy monitoring history.

### How long are monitoring logs retained?

Applies to Protocol Monitoring, Policy Monitoring, and Load Monitoring. Retention is calculated automatically based on remaining log partition space:

| Log Partition Free Space | Retention |
|---|---|
| > 300 MB | 31 days |
| > 200 MB | 20 days |
| > 100 MB | 15 days |
| > 50 MB | 10 days |
| > 10 MB | 7 days |
| < 10 MB | 1 day |
