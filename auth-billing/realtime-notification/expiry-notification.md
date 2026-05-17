# Dial User Expiry Notification (拨号用户过期通知)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/4b60b/9db7a.html

## I. Overview

When a PPPoE or VPN account has expired, the user can still dial in successfully — but opening any HTTP page shows an expiry notification instead of the requested page. This allows users to see contact information and arrange renewal.

**Note:** HTTPS pages cannot be hijacked — only HTTP traffic triggers the redirect.

---

## II. Configuration

### Notification Template

The default template:

```
============用户宽带过期通知============
您好！尊敬的用户: $user
您的带宽服务已过期，到期时间 $date ，
通过以下联系方式办理续费手续，谢谢。
客服电话：13800138000
客服QQ ：123456
办理地址：XX路XX号
```

- `$user` — replaced with the account username.
- `$date` — replaced with the expiry date.
- Customize the contact information, but **do not change the variable format** (`$user`, `$date`). Incorrect format causes the feature to malfunction.

### Whitelist
| Field | Description |
|---|---|
| Whitelist Public IP | IPs that expired users are still allowed to reach (e.g., payment portal). |
| Whitelist Domain | Domains that expired users are still allowed to access. |

---

## III. Common Issues

### Expiry notification shows wrong time
The `$user` or `$date` format in the template is incorrect. Reset the template to the correct format.

### User can still dial in after account expires
This is by design — iKuai allows expired accounts to dial in but blocks internet access, showing the notification instead. The user is connected but cannot browse.

### No notification appears when opening websites
Only HTTP sites trigger the redirect. HTTPS sites (e.g., Baidu) cannot be intercepted.
