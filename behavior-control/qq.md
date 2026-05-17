# QQ Blacklist/Whitelist (QQ黑白名单)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/qq.html

## I. Overview

Controls which QQ accounts can log in from specific LAN clients, using blacklist or whitelist mode.

---

## II. Field Reference

![QQ Blacklist/Whitelist](https://www.ikuai8.com/images/support/qq.png)

| Field | Description |
|---|---|
| Control Mode | **Blacklist** — listed QQ numbers are blocked. **Whitelist** — only listed QQ numbers are allowed. |
| QQ Number | The QQ account number to control. |
| Internal IP | The LAN client IP this rule applies to. |
| Schedule | The recurrence period for this rule. |

---

## III. Important Notes

1. Each rule applies only to the specific LAN IP configured in that rule.
2. Do **not** enable blacklist and whitelist simultaneously. When both exist, the block policy (whitelist = block all) takes precedence, preventing all terminals from logging in.
3. This feature does not work for **mobile QQ clients** — mobile QQ uses encrypted protocols that cannot be parsed.
