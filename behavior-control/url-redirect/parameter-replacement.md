# Parameter Replacement (参数替换)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/url/db5e5.html

## I. Overview

Replaces a specific URL query parameter value in HTTP requests. Unlike Keyword Replacement (which matches the keyword value), this feature targets a named parameter in the URL query string.

**Note:** HTTP only — HTTPS traffic cannot be modified.

---

## II. Field Reference

| Field | Description |
|---|---|
| Source URL | The site to match (fuzzy or exact). |
| Primary Key | The URL parameter name to intercept (e.g., `wd` for Baidu, `query` for Sogou). |
| Replace Value | The value to inject in place of the original parameter value. |
| Exclude Value | Parameter values to exempt from replacement. |
| Redirect Rate | Probability (%) that the replacement is applied. |
| IP/MAC Group | Limit this rule to specific LAN clients. |
| Schedule | Time period when this rule is active. |

---

## III. Common Parameter Keys

| Search Engine | Parameter Key |
|---|---|
| Baidu | `wd` |
| Sogou | `query` |

---

## IV. Notes

- Only works for **HTTP**. HTTPS query strings are encrypted and cannot be intercepted.
- Use this feature when you need to control the parameter name specifically, rather than the keyword text.
