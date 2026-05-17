# Terminal Monitoring — IPv4

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ztjk/7cf09.html

## I. Overview

The IPv4 page is the global monitoring interface for iKuai's traffic control router. It displays information related to LAN hosts, protocols, policies, line usage, and system monitoring.

![IPv4 Overview](https://www.ikuai8.com/images/ipv4111.png)

---

## II. How to Use

### IPv4 Terminal List

Displays real-time information about all active LAN hosts.

![IPv4 Terminal List](https://www.ikuai8.com/images/ipv4111.png)

> **Notes:**
> - The "Owner" column will not appear unless DingTalk is bound.
> - Terminal online/offline records are always logged under **Behavior Control → Terminal Online/Offline Records**, regardless of whether that setting is explicitly enabled — this is a system-level behavior.
> - **Refresh interval:** The IPv4 page auto-refreshes every **2 seconds**.

---

### 1. Viewing Terminal Details

Click **Details** in the Actions column to see more information for any IP address, including: Basic Info, Connection Details, History, and Traffic Distribution.

![Details Link](https://www.ikuai8.com/images/ipv412345.jpg)

**[Basic Info]** — Shows basic terminal information (using 172.16.10.100 as an example):

![Basic Info](https://www.ikuai8.com/images/support_202109/ipv412.jpg)

> **Refresh interval:** Terminal detail information auto-refreshes every **3 seconds**.

**[Connection Details]** — Shows real-time connections for the terminal:

![Connection Details](https://www.ikuai8.com/images/support_202109/ipv413.jpg)

Example: Connection #3 in the screenshot shows DingTalk. This client is accessing `203.119.169.179` on port 443 using local port 51025, forwarded via WAN address `172.16.19.207`.

Filter options:
- **All Protocols** — Filter by TCP, UDP, ICMP, or all protocols
- **All Lines** — Filter by which WAN line the connection uses

| Field | Description |
|---|---|
| Protocol Name | The application protocol used to access the destination |
| Protocol Type | The transport protocol type (TCP/UDP/etc.) |
| Line | The WAN line this connection uses |
| Destination Address | The target IP address being accessed |
| Destination Port | The port receiving data on the remote end |
| WAN Address | The router's WAN IP through which the connection is forwarded |
| Local Port | The local port used by the client for this connection |
| Connection State | The current state of the connection |

**Connection states:**

| State | Meaning |
|---|---|
| Connected | Three-way handshake completed; connection established |
| Stateless | No connection state (typical for UDP, shown as `--`) |
| Waiting | TCP SYN sent, waiting for remote response |
| CLOSE | TCP four-way handshake completed; connection closed |

**[Traffic Distribution]** — Shows traffic breakdown by protocol for this terminal:

![Traffic Distribution](https://www.ikuai8.com/images/support_202109/ipv414.jpg)

**[History]** — Shows the terminal's online/offline history:

![History](https://www.ikuai8.com/images/support_202109/ipv4415.jpg)

> **Note:** You must enable **Terminal Online/Offline Recording** for history to be recorded and viewable.

Log retention by partition size:

| Partition Size | Retention |
|---|---|
| > 300 MB | 1 month |
| > 200 MB | 20 days |
| > 100 MB | 15 days |
| > 50 MB | 10 days |
| > 10 MB | 7 days |
| < 10 MB | 1 day |

---

### 2. Blocking Internet Access

Click **Block Internet** in the Actions column to block a device from accessing the internet.

![Block Internet](https://www.ikuai8.com/images/ipv2.jpg)

Blocked devices can be viewed and managed under **Behavior Control → MAC Access Control**.

> **Note:** PPPoE and VPN addresses cannot be blacklisted here, because blacklisting is MAC-based.

---

### 3. Editing the Device Remark

Click **Edit Remark** in the Actions column to add or change the remark (label) for a device.

![Edit Remark](https://www.ikuai8.com/images/xgbz.jpg)

The remark will be visible in the Remark column after saving.

> **Note:** The remark set in **Account Management** takes priority over the remark set here in IPv4.

Remarks are synchronized across all of the following pages — a change in any one updates the others:

1. Status Monitoring → IPv4
2. Network Settings → DHCP Settings → DHCP Static Assignment (for IP-based remarks)
3. Security Settings → ARP Binding
4. Behavior Control → Behavior Records → Terminal Name Management (for MAC-based remarks)
5. Behavior Control → Behavior Record Viewer

---

## III. Common Issues

### IP appears in IPv4 but has almost no traffic

Check the following:

1. Is **PPPoE forced dial** enabled? The corresponding LAN port cannot access the internet without dialing.
2. Is **Web Portal authentication** enabled? Check if the IP falls within the authentication address pool — if it does, the device cannot browse without authenticating.
3. **Security Settings → ACL** — Is there a rule blocking this IP?
4. **Security Settings → ARP Binding** — Is "block non-bound devices" or "unique binding" enabled? If the IP's MAC doesn't match the binding, it cannot access the internet.
5. **Behavior Control → MAC Access Control** — Is the corresponding MAC address blocked?
6. Is **router mode** enabled in an environment that doesn't support it?
7. The terminal genuinely had no traffic during this time period.

---

### A device is on the LAN but doesn't appear in IPv4

The IPv4 list only shows clients that have had traffic in the **last 2 minutes**.

---

### Data still appears after a factory reset

Resetting the router to factory defaults does **not** clear the IPv4 monitoring data.

---

### The "Owner" column doesn't appear, or has no data

- DingTalk is not bound → the "Owner" column is not shown.
- User groups are not configured → no owner data is available.
