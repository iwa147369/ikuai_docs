# Real-time Notification (实时通知)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/4b60b.html

## I. Overview

Pushes an HTTP notification page to LAN clients immediately, one time only. When a client opens an HTTP page, they are redirected to the notification page and must click **"Acknowledged, go online"** to continue browsing.

**Note:** HTTPS pages cannot be hijacked — only HTTP traffic triggers the redirect.

---

## II. Configuration

### Notification Content
- **Notification Content** — the message body displayed to the client.
- **Notification Preview** — click to preview the actual notification page. Content must be saved before previewing.
- **Redirect Page** — the URL clients land on after clicking "Acknowledged, go online." Default: `http://www.baidu.com`. If left blank, clients return to the page they were originally accessing.

### Recipients
| Field | Description |
|---|---|
| Dial-up Users | When checked, PPPoE dial-up users receive the notification when they connect. |
| Listed LAN Users | Add specific IPs (single IP, IP range, or IP group) to receive the notification. |
| Show Countdown | Set a countdown (in seconds) before auto-dismissal. `0` = no countdown; without a countdown, clients must click manually — the port 80 redirect persists until they do. |

**To send:** Click **Save and Send** after configuring recipients.

---

## III. Common Issues

### Real-time notification has no effect
1. No recipient option is checked in the Recipients section.
2. **Save and Send** was not clicked after configuration.

### A specific client should be exempt
Remove that client's IP from the recipient list and save.

### A client cannot click "Acknowledged, go online"
Remove the client's IP from the list and save; have the client restart their browser or device.

### No prompt appears when opening websites
Only HTTP sites trigger the redirect. HTTPS sites (e.g., Baidu, most modern sites) cannot be intercepted.
