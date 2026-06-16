# IP Groups (Terminal Group Settings)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/cswq.html

## I. Overview

Group LAN IP addresses into named sets for easier management. Once a group is created, it can be selected by name in other configuration pages (such as traffic control, routing policies, etc.) instead of entering individual IPs each time.

---

## II. Configuration

![IP Group Settings](https://www.ikuai8.com/images/support_202109/fz1.png)

| Field | Description |
|---|---|
| Group Name | A unique label for this group. Used to identify it when selected in other pages. |
| Address Pool | When checked, this group can be bound to an address pool in Account Management. |
| IP List | The IP addresses in this group. Supports single IPs and IP ranges. |

> **Notes:**
> - Groups must be created here before they can be referenced in other settings (traffic control, routing rules, etc.).
> - Maximum 1,000 entries per group. One CIDR notation entry (e.g. `192.168.1.0/24`) counts as one entry.
> - If a group's name is changed, all policies that reference the old group name must be updated to select the new name.
