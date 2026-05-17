# Cross-Layer 3 Application (跨三层应用)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/2019-12-13-06-35-05/mnr4.html

## I. Overview

When clients are behind a Layer 3 switch or router, iKuai normally only sees the WAN IP of that device — not the individual client MACs. The Cross-Layer 3 Application feature uses SNMP to query the Layer 3 device for its ARP table, mapping the individual client IPs and MACs through the Layer 3 boundary.

With this information, MAC-based policies (rate limiting, ACL, etc.) can be applied to individual clients behind the Layer 3 device.

> **Exception:** ARP Binding and DHCP blacklist/whitelist do **not** work across Layer 3.

---

## II. Field Reference

| Field | Description |
|---|---|
| Access Frequency | How often to refresh data from the Layer 3 device. Default: `0s` (real-time). Firmware v3.7.0+ required. |
| Service Enable | Enable/disable the feature (default: disabled). |
| Service Status | Auto-detected every 5–10 seconds. "Abnormal" means configuration mismatch between iKuai and the Layer 3 device. |
| SNMP Server IP | The uplink IP of the Layer 3 switch (the IP facing iKuai). |
| Target IPs | Which IPs behind the Layer 3 device to apply Cross-Layer 3 policies to. |
| SNMP Listen Port | Default: **161**. |
| SNMP Protocol Version | **V2** (simpler) or **V3** (adds authentication and optional encryption). |
| Community (V2) | Community string — must match the Layer 3 device's configuration. |
| Username (V3) | Must match the Layer 3 device's SNMPv3 user. |
| Security Level (V3) | **Auth only** or **Auth + Encryption**. |
| Auth Mode | **SHA** or **MD5** — must match the Layer 3 device. |
| Auth Password | Must match the Layer 3 device. |
| Encryption Mode | **AES** or **DES** — must match the Layer 3 device. |
| Encryption Password | Must match the Layer 3 device. |

---

## III. Setup Overview

**On iKuai:**
1. Enable Cross-Layer 3 Application.
2. Enter the Layer 3 device's uplink IP as the SNMP Server IP.
3. Set the protocol version and authentication to match the Layer 3 device.

**On the Layer 3 device:**
1. Enable SNMP server with matching protocol version and authentication.
2. Ensure ARP/IP mapping data is exposed via SNMP.

Both sides must use the same protocol version and credentials.

---

## IV. Notes

- Supports multiple Layer 3 switches simultaneously.
- H3C switches: SNMPv3 username/password must be simple — only alphanumeric characters (no special characters).
- Multiple Layer 3 devices can be added by clicking **Add**.
