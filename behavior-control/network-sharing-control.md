# Network Sharing Control (网络分享控制)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/12b86.html

## I. Overview

Blocks secondary routers (NAT devices) behind iKuai from accessing the internet. Specific secondary routers can be exempted.

---

## II. Configuration

![Network Sharing Control](https://www.ikuai8.com/images/support_202109/jzejly.png)

| Field | Description |
|---|---|
| Block Secondary Routers | Enable to block all secondary/NAT routers from internet access. |
| Custom TTL | Set a custom TTL value (range: 1–64). Requires firmware v3.7.6+. |
| Block Schedule | Configure when the block is active. |
| Allowed IP Range / Group | Specific IPs or IP groups that are exempted and allowed through even when blocking is enabled. |

---

## III. Common Issues

### Some secondary routers cannot be blocked

Routers using non-standard protocols may not be detected and blocked.

### Can portable WiFi hotspots (e.g., 360 WiFi, Cheetah WiFi) be blocked?

No — portable WiFi hotspots of this type cannot currently be blocked.
