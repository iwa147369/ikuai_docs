# Terminal Name Management (终端名称管理)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/d581a.html

## I. Overview

Add and manage display names (aliases/remarks) for LAN terminals based on their MAC addresses.

![Terminal Name Management](https://www.ikuai8.com/images/support/zdmcgl.png)

---

## II. How to Use

- Search by MAC address or existing remark.
- Add, import, or export MAC remarks.
- Primary use: label devices by MAC for easier identification in management views.

---

## III. Remark Synchronization

Remarks added here are automatically synced across these pages:
- Status Monitoring → Terminal Monitoring
- Network Settings → DHCP → DHCP Terminal List (IP-based remarks)
- Behavior Control → Behavior Record Settings → Terminal Name Management (MAC-based remarks)
- Behavior Control → Behavior Record Viewer
- Security Settings → ARP Binding

Changing a remark on any of these pages updates all others automatically.

**Remark display priority (highest to lowest):**
PPPoE name > PPPoE remark > MAC remark > DHCP hostname
