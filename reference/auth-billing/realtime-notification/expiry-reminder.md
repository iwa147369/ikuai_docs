# Expiry Reminder (到期提醒)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/4b60b/b4c5d.html

## I. Overview

Proactively reminds clients that their account is about to expire, a configurable number of days in advance. The reminder is shown as an HTTP redirect page; the user must click **"I understand"** to continue browsing.

Unlike Expiry Notification (shown after expiry), this feature warns users *before* the account expires.

**Note:** HTTPS pages cannot be hijacked — only HTTP traffic triggers the redirect.

---

## II. Configuration

### Reminder Template

Default template:

```
============用户宽带到期提醒============
您好！尊敬的用户: $user
您的带宽服务即将到期，系统将于 $date 停止服务，
为了避免网络断线，请在到期前，通过以下联系方式办理续费手续，谢谢。
客服电话：13800138000
客服QQ ：123456
办理地址：XX路XX号
```

- `$user` — replaced with the account username.
- `$date` — replaced with the expiry date.
- **Do not change the variable format.** Incorrect format causes the feature to malfunction.

### Timing Settings
| Field | Description |
|---|---|
| Days Before Expiry | How many days before expiry to start showing the reminder. Default: 5 days. |
| Daily Reminder Time | The time of day to trigger the reminder push. |

The daily reminder only fires within the configured "days before expiry" window.

### Redirect Page
- Default redirect: `http://www.baidu.com`. If blank, the user is returned to the page they were originally accessing.

### Countdown
- **Show Countdown** — set a countdown (seconds) before auto-dismissal. `0` = no countdown; without it, the user must manually click "I understand" — the port 80 redirect persists until they do.

---

## III. Common Issues

### Reminder shows incorrect expiry date/time
The `$user` or `$date` variable format in the template is wrong. Reconfigure the template.

### No reminder appears when opening websites
Only HTTP sites trigger the redirect. HTTPS sites (e.g., Baidu) cannot be intercepted.
