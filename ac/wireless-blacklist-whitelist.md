# Wireless Blacklist / Whitelist

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ac/2019-05-13-07-41-45.html

## I. Overview

Wireless Blacklist/Whitelist controls which terminal devices (by MAC address) are allowed or denied access to specific SSIDs or APs.

**Requirements:** AP firmware v1.5.0+ and router version 3.4.0+

---

## II. Control Modes

| Mode | Behavior |
|---|---|
| Blacklist | All wireless terminals are allowed by default; MAC addresses in the blacklist cannot connect |
| Whitelist | All wireless terminals are blocked by default; only MAC addresses in the whitelist can connect |

---

## III. Configuration Fields

| Field | Description |
|---|---|
| Terminal MAC | Individual MAC address or MAC group to apply the rule to |
| SSID | The wireless network name this rule applies to |
| AP | The specific AP(s) this rule applies to |
| Time Schedule | Days and times when the rule is active |
| Remark | Custom label for the rule |

---

## IV. Important Constraint

When multiple terminal MAC addresses share the same rule, each MAC address can only belong to **one policy**. If a MAC address appears in multiple policies, only the **first configured policy** takes effect.

---

## V. Practical Examples

1. **Block a specific device from one SSID** — Add the device MAC to the blacklist and specify the target SSID.
2. **Block a specific device from all SSIDs** — Add the device MAC to the blacklist without specifying an SSID.
3. **Restrict access to authorized devices only** — Switch to whitelist mode and add the allowed MAC addresses.
