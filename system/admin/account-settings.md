# Account Settings (账号设置)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/bea01/e284e.html

## I. Overview

Manages the accounts and permissions used to log into the iKuai router's web management interface.

> **Default account:** username `admin`, password `admin` (super administrator). The default account cannot have its role changed.

---

## II. Configuration

![Account Settings](https://www.ikuai8.com/images/support/zhsz.png)

| Field | Description |
|---|---|
| Username | The login account name. Displayed in plain text. |
| Password | The login password. Stored encrypted and not displayed after saving. |
| Permission Group | **Super Administrator** — full read/write access, role cannot be changed. **Custom** — configurable permissions. |
| Allowed Access IP | Restricts which IP addresses can log in using this account. Default `0.0.0.0` allows all IPs. Set to a specific IP or range to restrict access. Supports ranges like `192.168.1.2–192.168.1.100`. |
| Login Session Timeout | How long before an idle session is automatically logged out. Range: 5–999 minutes. |
| Password Security Reminder | When enabled, the router periodically reminds users to change their password. Period range: 1–999 days. |

> **Note on Allowed Access IP format:** Use a hyphen (`-`) for ranges — e.g., `192.168.1.2-192.168.1.100`. Using a slash (`/`) is not supported for this field — the system interprets the part after `/` as a subnet mask.

> **Cloud remote access:** If accessing the router via iKuai Cloud remote management, add `127.0.0.1` to the Allowed Access IP field for that account.

---

## III. Common Issues

### "Your IP is not allowed to log in"

This appears when the **Allowed Access IP** restriction is set and you are logging in from a different IP. To recover: connect a monitor and keyboard to the router, access the console menu, and choose **Restore Web Management Password** — this resets the super administrator account so you can log in again.

### Forgot the web management password

Connect a monitor and keyboard to the router. In the console menu, press **7** (Restore Web Management Password). The account and password will both be reset to `admin`.

### Difference between super administrator and regular administrator

The default `admin` account is a super administrator — its permissions cannot be modified. Regular administrator accounts support custom permission settings.

### Purpose of the Allowed Access IP field

Once set, the account can only be used to log in from the specified IP address, providing additional access control security.
