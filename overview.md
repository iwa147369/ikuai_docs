# System Overview

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtgk.html

## I. Overview

Detects and displays the router's operating status. The entire page refreshes every **5 seconds**.

---

## II. How to Use

### 1. Overall Layout

![System Overview](https://www.ikuai8.com/images/xitonggaik.png)

As shown above, this is the overall display of the router system overview. The numbered items are explained as follows:

| # | Description |
|---|---|
| 1 | Current router firmware version |
| 2 | App binding status, iKuai Cloud binding status, firmware upgrade notifications, official push notifications, and admin login information |
| 3 | Current CPU temperature, CPU usage, memory usage, and upload/download speeds |
| 4 | Router configuration page navigation bar |
| 5 | Detailed system overview information |

> **Note (Temperature):** Under normal operating conditions, the router temperature is typically **40–70°C** (in environments with adequate cooling). Temperatures slightly above this range, such as 70°C or even 80°C, are generally not a problem and may be due to hardware cooling limitations. Some motherboards have thermal protection set at **105°C**, at which point the system will automatically shut down and can restart once the temperature drops. This threshold may vary by manufacturer.

---

### 2. Router Status

Displays the current router operating status and WAN connection state.

![Router Status](https://www.ikuai8.com/images/support/xtgk1.png)

---

### 3. Speed Status

Displays the current upload and download speeds of the router.

![Speed Status](https://www.ikuai8.com/attached/php/upload/image/20171227/1514347859640832.png)

---

### 4. Connection Status

Displays currently connected devices, total connection count, today's authenticated users, and wired/wireless connected terminals.

![Connection Status](https://www.ikuai8.com/images/support/xtgk2.png)

Clicking the stats navigates to the corresponding page:

- **Connected Devices** → Terminal Monitoring
- **Connections** → Line Monitoring
- **Today's Authenticated** → Online Users
- **Wired / Wireless** → Terminal Monitoring

> **Notes:**
> - **Connected Devices** shows the count of terminals that had traffic within the last **2 minutes**, as tracked in Terminal Monitoring.
> - **Today's Authenticated** shows the number of users authenticated via the Web Portal.

---

### 5. Interface Status

Displays the current WAN and LAN port link status and remaining DHCP pool addresses.

![Interface Status](https://www.ikuai8.com/images/support/xtgk5.png)

Clicking **Details** in the top-right corner navigates to LAN/WAN settings.

> **Note:** Red indicates disconnected; green indicates connected.

---

### 6. AC Status

Displays the AC controller status and 2.4 GHz / 5 GHz band connection status.

![AC Status](https://www.ikuai8.com/attached/php/upload/image/20180817/1534473707318561.png)

- Clicking the **AP connection status icon** navigates to the AP List.
- Clicking the **2.4 GHz / 5 GHz** band access count navigates to the Wireless Terminal List.

> **Note:** The 2.4 GHz/5 GHz access count shows terminals that had traffic within the last **2 minutes**, as tracked in Terminal Monitoring.

---

### 7. Protocol Traffic Distribution (Last 30 Minutes)

Displays a pie chart of protocol traffic usage in the 30 minutes before the last page refresh. You can also switch the view to the **past 1 hour** or **past 1 day**.

![Protocol Traffic](https://www.ikuai8.com/attached/php/upload/image/20171227/1514347601510876.png)

---

### 8. Upload/Download Speed (Last 5 Minutes)

Displays the upload and download speed of LAN clients over the past 5 minutes. All protocols are selected by default.

![Speed Chart](https://www.ikuai8.com/attached/php/upload/image/20171227/1514347659849759.png)

Clicking **Details** in the top-right corner navigates to Protocol Monitoring.
