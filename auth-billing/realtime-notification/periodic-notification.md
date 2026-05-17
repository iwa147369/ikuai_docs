# Periodic Notification (定期通知)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/4b60b/8af47.html

## I. Overview

Pushes an HTTP notification page to LAN clients on a recurring schedule (weekly). Unlike Real-time Notification (one-time), Periodic Notification can repeat.

**Note:** HTTPS pages cannot be hijacked — only HTTP traffic triggers the redirect.

---

## II. Configuration

### Notification Content
- **Notification Content** — the message body displayed to clients.
- **Redirect Page** — URL clients land on after clicking "Acknowledged, go online." Default: `http://www.baidu.com`.

### Push Schedule
| Field | Description |
|---|---|
| Push Cycle | Select specific days of the week (or every day) to push the notification. |
| Push Time | The time of day to trigger the push. |

### Recipients
| Field | Description |
|---|---|
| Dial-up Users | Push to PPPoE dial-up users when they connect. |
| Listed LAN Users | Add IPs (single, range, or group) to receive the notification. |
| Show Countdown | Countdown in seconds before auto-dismissal. `0` = no countdown; without it, clients must click manually — port 80 redirect persists. |

---

## III. Common Issues

### Periodic notification has no effect
1. No recipient option is checked.
2. **Save and Send** was not clicked.
3. The client's IP is not in the recipient list.
4. The scheduled push time has not been reached yet.

### A specific client should be exempt
Remove that client's IP from the list and save.

### Client cannot click "Acknowledged, go online"
Remove the client's IP from the list and save; have the client restart their browser or device.

### No prompt when opening websites
Only HTTP sites trigger the redirect. HTTPS sites cannot be intercepted.
