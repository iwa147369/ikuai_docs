# Wireless Overview (AC Management)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ac/ap.html

## I. Overview

### AC (Access Controller)

The iKuai router system includes a built-in AC (wireless controller) module. It provides centralized management of all iKuai APs (Access Points) connected to the router — including pushing default configurations, bulk config changes, monitoring AP status, and performing maintenance operations like restarts and firmware upgrades.

### AP (Access Point)

iKuai APs run a proprietary protocol that allows real-time communication with the AC. This communication covers configuration updates, AP status reporting, and keepalive messages.

**Important:** The AC handles only the control plane. It does not carry user data traffic. Even if the AC fails, APs continue operating normally as long as their gateway remains reachable.

![AC vs AP Architecture](https://www.ikuai8.com/attached/php/upload/image/20170117/1484640941526527.png)

---

## II. Dashboard Panels

### 1. Running Status (refreshes every 10s)

![Wireless Overview](https://www.ikuai8.com/images/support/wxgk1.png)

| Field | Description |
|---|---|
| Online APs | APs currently operating normally |
| Offline APs | APs that are disconnected or malfunctioning |
| Fast Roaming | Count of APs with fast roaming enabled (includes online and offline APs) |
| 5G Priority | Count of APs with 5G priority enabled (includes online and offline APs) |

---

### 2. Terminal Statistics (refreshes every 10s)

| Field | Description |
|---|---|
| 2.4G Online | Number of clients currently connected to 2.4G WiFi |
| 5G Online | Number of clients currently connected to 5G WiFi |
| Peak Online | Highest number of simultaneous online clients today |
| Active Terminals | Clients with combined upload+download > 1 Mbps |
| Inactive Terminals | Clients connected but with zero traffic |

---

### 3. Wireless Network Score (refreshes every 10s)

| Metric | Description |
|---|---|
| User Activity | How actively users are using the network. Higher = more active. |
| Association Stability | Client connection success rate. Higher = easier to connect. |
| Signal Coverage | Coverage quality. Higher = fewer low-signal clients. |
| Airtime Health | Channel utilization. Higher = cleaner channel environment. |
| Network Saturation | How many clients are connected. Higher = more clients. |

---

### 4. Terminal Statistics Chart (refreshes every 30s, updated every 5 min)

![Terminal Statistics Chart](https://www.ikuai8.com/images/support_202109/wxgk123.jpg)

| Chart | Description |
|---|---|
| Online Terminal Statistics | 2.4G and 5G client counts over the past 24 hours, updated every 5 minutes |
| Terminal Brand Distribution | Pie chart of client device brands currently connected |
| Terminal OS Distribution | Pie chart of client operating system types currently connected |

---

### 5. Wireless Network Score Chart (refreshes every 30s)

![Network Score Chart](https://www.ikuai8.com/images/support/wxgk2.png)

| Chart | Description |
|---|---|
| Channel Environment | 24-hour record of 2.4G channel resets, 2.4G noise floor, 5G channel drift, and 5G noise floor (5 min intervals) |
| Terminal Environment | 24-hour record of low-upload, low-download, and poor RSSI client counts (5 min intervals) |

---

### 6. Traffic Statistics (refreshes every 30s)

![Traffic Statistics](https://www.ikuai8.com/images/support/wxgk3.png)

| Chart | Description |
|---|---|
| Real-Time Rate | Upload/download speed over the past 24 hours, sampled every 5 minutes |
| Cumulative Traffic | Total upload/download traffic for today, updated every 5 minutes |

---

### 7. Terminal Association Details (refreshes every 30s)

![Association Details](https://www.ikuai8.com/images/support/wxgk4.png)

Shows the client connection success rate over the past 24 hours, updated every 5 minutes.

---

### 8. Network Transmission Quality (refreshes every 30s)

![Transmission Quality](https://www.ikuai8.com/images/support_202109/wxgk234.jpg)

Shows 2.4G packet loss rate, 5G packet loss rate, and latency over the past 24 hours (5 min intervals).

---

## III. Setup Example

1. Configure a DHCP server on the AC (LAN) to assign IPs to APs. Restart the DHCP service after adding the pool.

   ![DHCP for APs](https://www.ikuai8.com/images/support_202109/dhcpac.png)

2. Enable AC Smart Control on the router.

   ![Enable AC](https://www.ikuai8.com/images/support_202109/wxgk12.png)

3. Navigate to **AC Management → AP List** to see APs come online.

   ![AP List](https://www.ikuai8.com/images/support_202109/aplb11.png)

4. The system uses a built-in default configuration. APs will automatically apply it when they first connect. Customize SSID names and security settings as needed.

> **Notes:**
> - Firmware v2.7.0+: You can disable 2.4G or 5G bands by deleting the corresponding SSID name from the AP config.
> - Firmware v2.7.0+: AP isolation is supported. Clients on the same SSID are isolated from each other. Clients on different SSIDs are not isolated — use SSID VLAN + ACL to achieve inter-SSID isolation.
> - Chinese SSID names are limited to 10 characters to ensure maximum client compatibility.

---

## IV. Common Issues

### Does disabling AC Smart Control turn off the APs?

No. Disabling AC Smart Control only stops the AC from managing APs — APs continue to operate normally. If there are no APs on the network, disabling AC Smart Control stops the router from broadcasting AP discovery packets, reducing unnecessary CPU and network interface usage.
