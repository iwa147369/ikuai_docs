# URL Redirect (URL跳转)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/url.html

## I. Overview

Redirects HTTP requests matching a source domain to a different destination domain.

**Note:** HTTPS is not supported — only HTTP traffic can be redirected.

---

## II. Field Reference

| Field | Description |
|---|---|
| Match Type | **Fuzzy** — matches the domain and all subdomains. **Exact** — matches only the specified domain. |
| Source Domain | The domain to match and redirect away from. |
| Destination Domain | The domain to redirect matched requests to. |
| Exclude Value | Domains or paths to exempt from redirection. |
| Redirect Rate | Probability (percentage) that a matched request is redirected. Set to 100% to redirect all. |
| IP Group | Limit this rule to specific LAN client IPs. |
| Effective Time | Schedule (time period) when this rule is active. |

---

## III. Examples

### Precise match
- Source: `www.baidu.com` → Destination: `www.google.com`
- Only requests to `www.baidu.com` are redirected; `map.baidu.com` is not affected.

### Fuzzy match
- Source: `baidu.com` → Destination: `google.com`
- All subdomains of `baidu.com` (e.g., `map.baidu.com`, `news.baidu.com`) are redirected.

### Port redirect
- Source: `xiaozz.net:8080` → Destination: `xiaozz.net:9090`
- Only port 8080 traffic is redirected; other ports are unaffected.

---

## IV. Notes

- URL Redirect only works for **HTTP** traffic. HTTPS cannot be intercepted or redirected.
- Combining redirect rules with whitelist mode in URL Blacklist/Whitelist may cause conflicts.
