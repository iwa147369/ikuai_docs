# Line Monitoring

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ztjk/cda78.html

## I. Overview

The Line Monitoring page is the monitoring interface for iKuai's 7-layer traffic control on both LAN and WAN interfaces. It is divided into three sections: **NIC Status**, **Line Monitoring**, and **Line State Detection**.

---

## II. How to Use

### NIC Status

This section displays the monitoring interface for iKuai's LAN and WAN network cards.

![NIC Status](https://www.ikuai8.com/images/support/xljk55.png)

- **Green** – Connected
- **Red** – Not connected
- **Gray** – Not bound

Hovering the mouse over a NIC card displays its details.

![NIC Info](https://www.ikuai8.com/images/support/xljk56.png)

> **Note:** Gray means the NIC is not connected; green means it is connected.

---

### Line Monitoring

Displays the usage status of iKuai's LAN and WAN network cards.

![Line Monitoring](https://www.ikuai8.com/images/support/xljk111.png)

> **Note — Packet Loss Statistics:**
> The packet loss displayed by iKuai is caused by the physical NIC itself — it is **not** caused by router forwarding. The system reads data from the NIC driver level for display purposes only.
>
> Common causes of NIC packet loss:
> 1. NIC hardware failure
> 2. Malformed or incomplete data packets that the NIC discards
> 3. Proprietary protocols on certain devices, e.g. enabling LLDP on a switch
>
> Other unusual causes include lightning strikes and unstable voltage causing abnormal packets. Please troubleshoot these independently.
>
> **Packet loss reference thresholds (normal ranges):**
> - 100 Mbps environment: sustained forwarding above 60 Mbps → packet loss rate below 1/10,000 is normal
> - 1 Gbps environment: sustained forwarding above 200 Mbps → packet loss rate below 5/10,000 is normal

Clicking **WAN Details** opens a chart showing real-time traffic and connection count over the past 5 minutes (requires Enterprise Edition v3.7.16 or later).

![WAN Details](https://www.ikuai8.com/images/support_202109/xianlujkxq.png)

---

### Line State Detection

WAN line detection uses the detection mechanism configured in each WAN port's settings. This section shows each WAN port's IP address, gateway, and automatic failover settings.

![Line State Detection](https://www.ikuai8.com/images/support/xlztjc.png)

**Detection status messages:**

| Status | Meaning |
|---|---|
| Starting PPTP dial | A PPTP dial-up connection is active on this line |
| Starting L2TP dial | An L2TP dial-up connection is active on this line |
| Starting OpenVPN dial | An OpenVPN dial-up connection is active on this line |
| Dial failed | The dial-up connection attempt failed |
| DHCP acquisition failed | DHCP auto-configuration failed; no address obtained |
| Line detection failed | Ping to gateway and DNS both failed |
| Line detection successful | Line detected successfully; internet access is working |
| Physical interface disconnected | The NIC or cable is physically disconnected |
| Outside connection time window | The WAN port has a scheduled time window configured and is currently outside it |
| Interface has no IP/gateway set | The interface is bound but no IP or gateway has been configured |

---

## III. Common Issues

### Line Detection Fails but Connection Seems OK

**How line detection works:**

The detection mechanism is configurable per WAN port:

1. **http + ping www.baidu.com** *(default)* – Checks both HTTP response from Baidu and ping. Either one succeeding counts as success.
2. **http only** – Sends an HTTP request to Baidu and checks the response.
3. **ping only** – Pings a specified domain or IP to verify connectivity.

If line detection fails but the line actually works, it may be because the ISP blocks ICMP (ping). Try switching the detection method.

> **Notes:**
> 1. When using `http + ping` mode, the line is considered up if **either** check succeeds.
> 2. By default, the router always pings the line's gateway. If the gateway responds, the line is considered up.

**Troubleshooting steps for line detection failure:**

1. Connect a computer directly to the modem and check if internet access works. Check for unpaid bills.
2. Verify that the correct NIC is bound to the correct line. Try swapping the NIC or cable.
3. Confirm that the subnet mask provided by the ISP is entered correctly.
4. Switch to a different line detection method.
5. If all the above checks pass, contact your ISP.

---

### WAN Traffic Greater Than LAN Traffic

Possible causes:

1. Enabling **Fanxing** (peer acceleration) causes WAN traffic to exceed LAN traffic.
2. Enabling **video caching** causes WAN traffic to exceed LAN traffic.
3. An ongoing **attack** is generating extra WAN traffic.
4. **P2P interrupted connections** — broken P2P connection requests accumulate on the WAN port. This gradually normalizes over time.

> **Note:** WAN traffic exceeding LAN traffic is **normal** when video caching or Fanxing is enabled.

---

### WAN Traffic Doesn't Match the Forwarding Rate on the Dashboard

- **Line Monitoring** shows the raw rate of traffic arriving at or leaving the NIC — including router's own services like caching and Fanxing. The system reads this directly from the NIC driver level.
- **The dashboard top-right** shows the router's **forwarding rate** — traffic that has been processed by the routing system (e.g., after bandwidth limiting and traffic shaping).

This page refreshes every **5 seconds**.

---

### LAN Port Shows Partial Abnormality

This occurs when a LAN port has extended NIC binding configured, but one of the bound NICs has no cable connected.

---

### WAN Connection Count Is Unbalanced — How to Configure

You can balance connection counts in **Multi-WAN Load Balancing**:

- **Same ISP lines:** Set the load balancing mode to **real-time connection count**, set ISP to **All ISPs**, and set load ratios based on the bandwidth provided by the ISP.

  ![Same ISP](https://www.ikuai8.com/images/support/dxfz99.png)

- **Different ISP lines:** Set the load balancing mode to **real-time connection count**, select the corresponding ISP for each line, and set load ratios based on bandwidth.

  ![Different ISP](https://www.ikuai8.com/images/support/dxfz88.png)
