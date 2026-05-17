# WEB Auth Service (WEB认证服务)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/web.html

## I. Overview

WEB authentication (captive portal) requires LAN clients to authenticate through a web page before they can access the internet. The iKuai router displays service status and acts as the enforcement point; all authentication configuration is done on the **iKuai Cloud platform**.

---

## II. Setup Steps

### Step 1 — Register an iKuai Cloud account
Register at the iKuai Cloud platform: `http://yun.ikuai8.com`

### Step 2 — Bind the router to iKuai Cloud
1. Log in to the cloud platform and copy the **Binding Code** (unique device identifier).
2. Paste it into the router web UI under **System Settings → iKuai Cloud Binding**.
3. After binding, the device appears in the cloud platform under **Device Management**.

### Step 3 — Configure WEB authentication on the cloud platform
1. In the cloud platform, go to **Network Management → [Device] → Auth Configuration**.
2. Enable authentication and fill in venue/scene details.
3. Select an authentication method (SMS, WeChat, password, etc.).
4. Configure **Exempt IPs** (partial IP auth — only listed IPs require auth; others bypass).
5. Configure Portal settings (captive portal page, restrictions).
6. Click **Finish and Apply** at the bottom of the page. Configuration syncs to the router in approximately **5 minutes**.

---

## III. Authentication Status

Once WEB auth is enabled, the router UI shows the current status, authentication mode, and the rate limits applied by that mode.

---

## IV. Authentication Roaming

When multiple iKuai routers are in the same LAN and share the same **auth group ID and secret key**, users authenticated on one router are recognized on others — no re-authentication required (roaming).

---

## V. Notes

- WEB authentication is **MAC-based IP validation**. The router must correctly identify the client's MAC address.
- **PPPoE, VPN, and traffic from Layer 3 devices (secondary routers) cannot use WEB authentication.**
- If "Authenticate All IPs" is selected on the cloud platform, PPPoE and VPN address ranges are also included — this will prevent PPPoE dial-in.

---

## VI. Common Issues

### Authenticated clients reconnect and must re-authenticate
Clear the ARP binding table on the router.

### SMS authentication — no SMS received
Set the DHCP primary DNS to `223.5.5.5` and backup DNS to `223.6.6.6`. Apply the same DNS settings on the mobile device.

### Mobile devices cannot trigger the auth page on Wi-Fi
Check whether **Network Switching** or **Data Acceleration** is enabled on the router. Disable those features and test again.
