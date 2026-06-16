# Authentication Log (认证日志)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzzx/fe4g.html

## I. Overview

Records all user authentication events: web authentication, PPPoE dial authentication, and VPN dial authentication.

![Auth Log](https://www.ikuai8.com/images/support/rzrz.png)

---

## II. How to Use

View authentication method, time, IP address, and MAC address for each event. Filter by date range, event type, and authentication type.

Use the error messages in log entries to diagnose issues:

| Log Message | Meaning |
|---|---|
| Wrong password or username does not exist | Verify the account credentials and authentication type (e.g., don't use a VPN account for PPPoE). |
| User actively disconnected | The client disconnected on its own — expected behavior. |
| Account start time not reached | The account's configured start date is in the future. |
| User no response | After dialing in, the router checks the client's online status via LCP. If the client stops responding, it is kicked offline. |
| Server actively disconnected | Account was manually kicked from the online user list, account expired, or the auth service was stopped. |
| MAC binding error | The account has a specific MAC address bound to it, but the connecting device has a different MAC. |
| Account disabled | The account has been manually disabled. |
| Account expired | The account has passed its expiry date (current firmware shows a renewal prompt when expired users try to access the web). |
| Duplicate login | Default shared-device count is 1. When a second device logs in with the same account, the first session is kicked. |

Export logs as CSV or TXT using the **Export** button. Clear all logs with **Clear All**.

---

## III. Common Issues

### Web Authentication Issues

| Error Message | Cause |
|---|---|
| MAC address does not exist | Client authenticated via PPPoE, VPN, or through a Layer 3 switch — no MAC is available at that point. |
| MAC binding error | Account has a fixed MAC configured, but the connecting device's MAC doesn't match. |
| Incorrect password | Wrong password entered for fixed-password or user-based authentication. |
| Coupon does not exist | Coupon code not found in the router's coupon list. |
| Coupon already used | Coupon has already been redeemed by another device. |
| Daily free trial expired | The free trial time configured on the cloud platform has been used up for today. |
| This authentication type is not enabled | Browser cache issue or the authentication method was changed and saved. |

### Internal Dial (PPPoE Server) Issues

**Log shows "user no response":**

1. **PC issues:** Recreate the broadband connection, reboot the PC, re-seat the cable after dialing, or check if the PC crashed after dialing.
2. **LAN environment issues:** Test the line, swap switch ports, or do a direct PC-to-router LAN test. Check for broadcast storms or ARP attacks blocking internal traffic.
3. **Enhanced disconnect detection:** If PPPoE server has enhanced LCP detection enabled, LCP failure triggers a forced disconnect.

---

## IV. Log Retention

Max entries: **20,000** (Auth Log). See [System Log](system-log.md) for the full retention table.
