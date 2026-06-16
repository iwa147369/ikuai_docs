# Health Check (健康检测)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/yygj/b50c6.html

## I. Overview

Health Check monitors whether the router is running normally. When **Active Health Monitoring** is enabled, if the system remains in an unhealthy state for the configured duration, the router automatically restarts. This serves as a watchdog: if the router freezes or hangs, it reboots itself.

An unhealthy state is defined as: missing system processes or service anomalies.

![Health Check](https://www.ikuai8.com/images/support/jkjc.png)

---

## II. Common Issues

### The router restarts automatically during operation

Possible causes:
1. A scheduled restart was configured in the router settings.
2. Unexpected power loss.
3. Active Health Monitoring is enabled and the router detected an unhealthy state (e.g., a process crashed or a service failed), triggering an automatic reboot.
