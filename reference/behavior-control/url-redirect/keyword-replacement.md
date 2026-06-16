# Keyword Replacement (关键字替换)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/url/d4280.html

## I. Overview

Replaces search keywords in HTTP requests. When a client submits a search query matching the configured keyword, the keyword is replaced with the configured value before the request is forwarded.

**Note:** HTTP only — HTTPS traffic cannot be modified.

---

## II. Field Reference

| Field | Description |
|---|---|
| Source URL | The search site to match (fuzzy or exact). |
| Replace Keyword | The original keyword to intercept and replace. |
| Replace Value | The value to substitute in place of the keyword. |
| Exclude Value | Keywords to exempt from replacement. |
| Redirect Rate | Probability (%) that the replacement is applied. |
| IP/MAC Group | Limit this rule to specific LAN clients. |
| Schedule | Time period when this rule is active. |

---

## III. Example

**Goal:** When a client searches `qwe` on Sogou, replace it with `456`.

- Source URL: `sogou.com` (fuzzy match)
- Replace Keyword: `qwe`
- Replace Value: `456`

Result: The search query is silently changed to `456` before being sent to Sogou.

---

## IV. Notes

- Only works for **HTTP** requests. HTTPS search traffic (most modern search engines) cannot be modified.
- Each search engine uses a different URL parameter for the query string — see Parameter Replacement for parameter-level control.
