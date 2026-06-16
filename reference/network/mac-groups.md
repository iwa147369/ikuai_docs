# MAC Groups (MAC分组)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/cswq/mac.html

## I. Overview

Group LAN MAC addresses for easier management. Once a MAC group is created, other configuration pages (such as MAC rate limiting) can reference the group by name instead of entering individual MAC addresses.

---

## II. Configuration

![MAC Group](https://www.ikuai8.com/images/support/macfz111.png)

| Field | Description |
|---|---|
| Group Name | A unique label for this group. Used to identify the group in other settings pages. |
| MAC List | The MAC addresses to include in the group. One or more MACs can be added. |

> **Note:** A MAC group must be created here before it can be selected in other rule configurations such as MAC rate limiting. When used in access control rules: **block-access** rules work with MAC groups; **allow-access** rules currently do not take effect with MAC groups.
