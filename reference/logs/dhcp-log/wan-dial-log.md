# WAN Dial Log (外网拨号日志)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzzx/gegge/hrehe.html

## I. Overview

Displays PPPoE dial-up logs for WAN interfaces and VPN client connections. Only WAN lines configured in dial-up (PPPoE) mode generate entries here — static IP or DHCP WAN connections do not appear.

![WAN Dial Log](https://www.ikuai8.com/images/support/wwbh.png)

Clear the log using the Clear button in the top-right corner.

---

## II. Common Error Messages

| Log Message | Meaning | Resolution |
|---|---|---|
| `Timeout waiting for PADO packets, Unable to complete PPPoE Discovery` | PPPoE server not responding. | Disconnect and reconnect after 1 minute; test with a direct PC connection; reboot the ONT/modem. |
| `LCP terminated by peer, Connect time X minutes.` | Server actively disconnected after X minutes of connection time. | Contact ISP to verify account status. |
| `CHAP authentication failed` / `PAP authentication failed` | Authentication failed — wrong credentials, overdue account, or wrong line binding. | Verify account/password; check account status with ISP; verify the account matches this WAN line. |
| `CHAP authentication failed: TOO MANY CONNECTIONS` | Account's concurrent connection limit reached, or the account is still listed as online at the ISP. | Contact ISP to resolve. |
| `check user-name in black list failed` | Account is on the ISP's blacklist. | Contact ISP. |
| `Limit Users Err` | Account login is restricted by ISP. | Contact ISP. |
| `User's Authen Attrib Check Error, Request Deny` | Account does not match the line it is connected to. | Use the correct account for this line, or connect to the correct line. |
| `user passwd error` | Wrong username or password. | Correct the credentials; try a different browser to avoid autofill issues. |
| `Unable to find user in database` | Account does not exist at ISP. | Verify the username. |

**iKuai LCP detection behavior:** By default, sends 1 LCP keepalive packet every 3 seconds; reconnects after 20 consecutive non-responses. Additionally checks for any NIC response — if the NIC has traffic, the session is considered live even if LCP check fails. iKuai does not initiate disconnects unless configured to do so.

---

## III. Log Retention

Max entries: **5,000**. See [System Log](../system-log.md) for the full retention table.
