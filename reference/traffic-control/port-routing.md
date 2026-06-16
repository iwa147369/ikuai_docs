# Port Routing (端口分流)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/ea195/1a5c9.html

## I. Overview

Route traffic based on port number — direct specific LAN clients accessing specific destination ports to a particular WAN line or next-hop gateway.

---

## II. Configuration

Two routing methods are available:

### Method 1 — WAN Line

![Port Routing - WAN Line](https://www.ikuai8.com/images/contents/20220929163547-749545d37ab833f69feb350ae4ef0b4a.png)

Select the protocol, specify the WAN line, enter the source IP address, and set the destination port.

### Method 2 — Next-Hop Gateway

![Port Routing - Next-Hop](https://www.ikuai8.com/images/contents/20220929163547-4742f1b0e9bd5f00f09ef7c0be97d1fd.png)

Specify a next-hop gateway IP. As long as the next-hop is reachable, traffic exits through it — similar to a static route. Supports source address, destination address, source port, and destination port filtering.

![Port Routing Fields](https://www.ikuai8.com/images/contents/20220929163547-208997ff70e1e4f7791e75c4969a76c8.png)

**Line Binding:** When checked, if the assigned line drops, traffic stays on that line and does not auto-switch to a healthy one.

**Load Balancing Modes** (applies when multiple WAN lines are selected with WAN Line method):

| Mode | Behavior |
|---|---|
| New Connection Count | Assigns connections in round-robin proportion |
| Source IP | Same source IP always uses the same interface |
| Source IP + Source Port | Same source IP+port uses the same interface |
| Source IP + Destination IP | Same source+destination IP pair uses the same interface |
| Source IP + Destination IP + Destination Port | Most granular sticky key; most balanced distribution |
| Primary/Backup Mode | Traffic uses the primary line; switches to backup if primary fails. Line order in the list determines primary/backup. Requires firmware v3.4.5+ |

> **Note:** Load balancing mode is only available when routing type is "WAN Line" with multiple lines selected. Next-hop gateway mode does not support load balancing.

---

### IP Geolocation Routing

Route traffic based on destination IP's geographic origin (China domestic vs. international). Requires firmware v3.7.20+.

Activation: Bind the device to iKuai Cloud, download the "iKuai" app, and enable IP geolocation routing from the app.

![IP Geolocation 1](https://www.ikuai8.com/images/ipgsd1.png)
![IP Geolocation 2](https://www.ikuai8.com/images/ipgsd111.png)

---

> **Notes:**
> - Destination address and source port can usually be left blank. Only fill in destination address if you need to route to a specific external server.
> - Rules are evaluated against all rules; when rules conflict, the later-added rule takes effect.
