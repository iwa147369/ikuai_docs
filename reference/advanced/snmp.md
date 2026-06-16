# SNMP Server (SNMP服务端)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/2019-12-13-06-35-05/snmp.html

## I. Overview

SNMP (Simple Network Management Protocol) allows external network management software (NMS) to monitor and query iKuai router status — including system parameters, CPU temperature, connection count, network interfaces, memory usage, and AP information.

iKuai supports SNMP **v2c** and **v3**. IPv6 access supported from firmware v3.7.9+.

---

## II. Basic Settings

| Field | Description |
|---|---|
| Enable | Toggle the SNMP server on/off. |
| Listen Port | Default: **161**. |
| Physical Location | (Optional) Description of where this device is located. |
| System Description | (Optional) Alias or description for this device. |

---

## III. Version Settings

### SNMPv2

| Field | Description |
|---|---|
| Community Name | Must match the SNMP client configuration. |
| Permission | Read-only or Read/Write. |
| Allowed Client IP | Specific IPs that can query this device. Leave blank to allow all. |

### SNMPv3

| Field | Description |
|---|---|
| Username | Must match the SNMP client. |
| Permission | Read-only or Read/Write. |
| Security Level | **Auth only** — authenticates but does not encrypt. **Auth + Encryption** — both authentication and encrypted data transfer (even if the client only enables auth, it can still connect but data will be unencrypted). |
| Auth Mode | **SHA** or **MD5**. |
| Auth Password | Authentication credential. |
| Encryption Mode | **AES** or **DES**. |
| Encryption Password | Encryption credential. |

---

## IV. Supported OIDs

### System Parameters

| OID | Description | Method |
|---|---|---|
| `.1.3.6.1.2.1.1.1.0` | System description | GET |
| `.1.3.6.1.2.1.1.3.0` | System uptime | GET |
| `.1.3.6.1.2.1.1.4.0` | System contact | GET |
| `.1.3.6.1.2.1.1.5.0` | System name | GET |
| `.1.3.6.1.2.1.1.6.0` | System location | GET |

### Network Interfaces (partial)

| OID | Description | Method |
|---|---|---|
| `.1.3.6.1.2.1.2.1.0` | Number of interfaces | GET |
| `.1.3.6.1.2.1.2.2.1.2` | Interface description | WALK |
| `.1.3.6.1.2.1.2.2.1.5` | Interface speed (bps) | WALK |
| `.1.3.6.1.2.1.2.2.1.8` | Interface operational status (up/down) | WALK |
| `.1.3.6.1.2.1.2.2.1.10` | Interface input bytes | WALK |
| `.1.3.6.1.2.1.2.2.1.16` | Interface output bytes | WALK |
| `1.3.6.1.2.1.31.1.1.1.6` | Interface input bytes (high capacity) | WALK |
| `1.3.6.1.2.1.31.1.1.1.10` | Interface output bytes (high capacity) | WALK |

> CPU temperature and connection count monitoring supported from firmware v3.7.6+.

---

## V. Notes

- SNMP clients need compatible software (e.g., PRTG, Zabbix, iReasoning MIB Browser).
- Configure the client with the same protocol version and credentials as the server.
