# MAC Access Control (MAC访问控制)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/mac.html

## I. Overview

Controls internet access for LAN devices based on their MAC addresses. Supports blacklist and whitelist modes.

---

## II. Modes

![MAC Access Control](https://www.ikuai8.com/images/support_202109/macfwkz1.png)

### Blacklist Mode (default)

All MAC addresses are allowed by default. MACs on the blacklist are blocked from accessing the internet. Add a MAC and configure when the block is active.

### Whitelist Mode

All MAC addresses are blocked by default. Only MACs on the whitelist are allowed to access the internet. Add a MAC and configure when the access is permitted.

**Important notes:**
1. A device added to the blacklist will not receive an IP address from DHCP.
2. Firmware v3.1.1+ and AP v1.4.4+ extend this to **wireless** blacklist/whitelist:
   - Blacklist: all MACs can connect to Wi-Fi by default; listed MACs cannot associate.
   - Whitelist: no MACs can connect to Wi-Fi by default; only listed MACs can associate.
