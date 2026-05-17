# UPnP Settings (UPnP设置)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/upnp.html

## I. Overview

UPnP (Universal Plug and Play) enables devices on a network to automatically create port mappings without manual configuration. It is effectively automatic port forwarding for software that supports UPnP.

This page lets you configure excluded ports, allowed LAN IPs, the default WAN line, and disconnect detection behavior.

---

## II. Configuration

![UPnP Settings](https://www.ikuai8.com/attached/php/upload/image/20180919/1537325987285505.png)

| Field | Description |
|---|---|
| Excluded Ports | Ports that UPnP is not allowed to map. Use `,` to separate non-contiguous ports; use `—` for a continuous range. Leave blank to exclude nothing. |
| Allowed LAN IPs for Mapping | The LAN IP range permitted to create UPnP mappings. `0.0.0.0–255.255.255.255` allows all. Leave blank to disallow all. |
| Default Line | The WAN line that UPnP devices use when creating automatic port mappings. |
| Disconnect Detection | When enabled: checks every 2 minutes whether the UPnP client has any traffic. If no traffic is detected, the associated mapping rules are cleared. Only effective for clients that send UPnP requests periodically — not suitable for clients that send a UPnP request only once at startup. |
| Scheduled Restart | Periodically restart the UPnP service. |

### Per-IP Line Assignment

![UPnP Line Assignment](https://www.ikuai8.com/images/upnp123.jpg)

You can specify that a particular LAN device uses a specific WAN line for its UPnP mappings.

| Field | Description |
|---|---|
| LAN IP | The internal device IP that should use a specific line for UPnP mapping. |
| Line | The WAN line to use for this device's UPnP mappings. |

*Example:* `192.168.15.100` → WAN1 means that device's UPnP mappings are created on WAN1.

---

## III. Priority Order

When multiple inbound access features overlap, the effective priority (firmware v3.4.8+) is:

**Fanshu (繁星) > Port Forwarding > UPnP > NAT1 > DMZ**

(Firmware v3.4.7 and below: Fanshu > Port Forwarding > NAT1 > DMZ > UPnP)

---

## IV. UPnP Status

The **UPnP Status** tab shows all currently active automatic port mappings.

![UPnP Status](https://www.ikuai8.com/images/support/upnp.png)

**Notes:**
- Entries expire after **12 hours** with no renewal from the client device — standard UPnP protocol behavior. This prevents offline devices from leaving stale mappings that accumulate over time and slow down the router.
- **Offline Cleanup:** Removes entries whose source IPs appear in the UPnP status table but are no longer listed in terminal monitoring (i.e., the device is offline).

---

## V. Troubleshooting

If UPnP mapping fails, refer to the diagnostic flowchart:

![UPnP Troubleshooting](https://www.ikuai8.com/images/support/upnp11.jpg)
