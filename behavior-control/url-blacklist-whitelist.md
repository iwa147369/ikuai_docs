# URL Blacklist/Whitelist (网址黑白名单)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/mjtt.html

## I. Overview

Controls which websites LAN clients can access, using either blacklist or whitelist mode.

---

## II. Modes

| Mode | Behavior |
|---|---|
| Blacklist | All domains are accessible by default; listed domains are blocked. |
| Whitelist | All domains are blocked by default; only listed domains are accessible. |

---

## III. Wildcard Matching

- `sohu.com` or `*.sohu.com` — blocks the domain and all its subdomains.
- `*.sohu.*` — matches any domain containing `sohu` in the middle segment (e.g., `sohu.net`, `sohu.org`).
- `xiaozz.net:2016` — blocks only port 2016 on `xiaozz.net`; other ports remain accessible.

---

## IV. Whitelist Mode Notes

- **Allow external links in whitelist** — when enabled, HTTP requests to domains not in the whitelist are permitted if they originate as external links from a whitelisted page. This does **not** apply to HTTPS.
- WeChat and QQ require additional whitelist entries for images to load properly:
  - Add `^[0-9.]+` (IP-format domains)
  - Add `wx.qlogo.cn`

---

## V. Common Issues

### Whitelist mode blocks too much
Ensure all required domains (including CDN and API endpoints) are added. For WeChat/QQ, add the image domain entries listed above.

### HTTPS sites cannot be blocked/allowed
URL blacklist/whitelist parses HTTP traffic only. HTTPS sites cannot be controlled via this feature — use Application Protocol Control instead.
