# Load Monitoring (负载监控)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ztjk/bc48e.html

## I. Overview

Displays performance metrics: CPU usage, memory, disk usage, online terminal count, max upload/download rate, and total packet forwarding count.

---

## II. How to Use

### Performance Load

Shows CPU, memory, and disk usage, plus the number of online terminals.

![Performance Load](https://www.ikuai8.com/images/support/fzjk.png)

| Metric | Description |
|---|---|
| CPU Usage | Graph of CPU usage over the last hour. Use the top-right selector to switch between last hour, day, week, or month. Fluctuation is normal — usage varies with traffic load. |
| Memory Usage | Graph of memory usage over the selected time range. |
| Online Terminal Count | Graph of how many terminals were online over the selected time range. |

### Network Load

Shows the maximum upload and download rate and the total packet forwarding count.

![Network Load](https://www.ikuai8.com/images/support/fzjh.png)

---

## III. Common Issues

### Why is there data here after a factory reset?

A factory reset does **not** clear load monitoring history.

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
