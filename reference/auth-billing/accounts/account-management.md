# Account Management (认证账号管理)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/df305/c0c61.html

## I. Overview

Create and manage authentication accounts for PPPoE, PPTP, L2TP, OpenVPN, IKEv2, and WEB auth. Supports add, edit, delete, enable/disable, bulk import/export, and account renewal.

---

## II. Key Fields

| Field | Description |
|---|---|
| IPv6 Prefix Interface | Bind an IPv6 prefix interface to this account (PPPoE only, firmware v3.7.3+). |
| Plan Type | Service plan assigned to this account. Plans are created in Account Management → Plan Management. |
| Shared Count | Number of simultaneous sessions allowed for this account. |
| Bind VLAN | The VLAN the client must be on when dialing in. Supports QinQ (format: `outer.inner`). Requires PPPoE server VLAN binding enabled. |
| Bind NIC | The LAN port the client must connect from. Requires PPPoE server NIC binding enabled. |
| Bind MAC | The client MAC address this account is restricted to. |
| IP Binding Type | **Fixed IP** — assign a specific IP. **Address Pool** — assign from a pool (for accounts with shared count > 1, supports OpenVPN, PPPoE, L2TP, PPTP, IKEv2). |

### MAC Binding Modes

| Mode | Behavior |
|---|---|
| Manual | Manually enter the client MAC. The field may be left empty. |
| Auto | The first MAC to use this account is recorded automatically. Not recommended when shared count > 1. |

---

## III. Operations

### Add Account
Click **Add**, fill in account details, and save. Firmware v3.7.16+ records the last online/offline time.

### Edit Account
Click the edit button next to an account to modify credentials, plan, type, or other settings.

### Account Renewal
Click the renewal button to extend, change, or cancel a plan subscription.

### User Self-Service Password Change
After a successful dial-in, the user can change their own password:
1. Open a browser and navigate to `http://6.6.6.6/`.
2. Enter the old password, set a new one, and click Submit.
3. The router account password is updated immediately. The current session is not disconnected, but the new password is required for the next login.

---

## IV. Search and Filter

Accounts can be searched by: account name, real name, address, phone, or remarks.

Filter by status: All / Enabled / Disabled / Expired.

Filter by type: PPPoE / PPPoE Passthrough / WEB / PPTP / L2TP / OpenVPN / IKEv2.

---

## V. Import/Export

Accounts can be exported to file or imported from file. When importing accounts from a different system, convert the data to iKuai's account format first.

---

## VI. Notes

- VLAN and NIC binding only apply to **PPPoE** account types.
- VLAN binding supports QinQ: `a.b` where `a` is the outer VLAN and `b` is the inner VLAN, separated by `.`.
- PPPoE server does not reserve address pool IPs — fixed IPs must be **outside** the pool range to avoid duplicates. Exception: OpenVPN fixed IPs must be **inside** the pool range.
- Fixed IP for PPTP/L2TP accounts must be **outside** the server address pool range.
- Fixed IP for OpenVPN accounts must be **inside** the address pool range.
- WEB account type does not support fixed IP assignment.
