# LAN / WAN Settings (Interface Configuration)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/vaqw.html

## I. Overview

Basic LAN/WAN configuration, including NIC binding, LAN IP address, and WAN connection type settings.

---

## II. How to Use

### 1. Interface Status

![Interface Status](https://www.ikuai8.com/images/support/nwwsz1.png)

Displays the current link status of all WAN and LAN ports.

---

### 2. Adding a LAN Port

**Step 1:** Click **Add Configuration** and select a free (unbound) NIC.

![Select Free NIC](https://www.ikuai8.com/attached/php/upload/image/20170914/1505376765951440.png)

**Step 2:** Set the NIC purpose to **LAN (Internal Network)**.

![Set to LAN](https://www.ikuai8.com/images/wkyt.png)

After binding, the configuration looks like this:

![LAN Config](https://www.ikuai8.com/images/lan3.png)

**[IP Address / Subnet Mask]** — This is the gateway address for all terminals connected to this LAN.

> **Note:** Only a **free (unbound)** NIC can be assigned to a LAN. If the NIC is already in use, unbind it first to free it, then rebind it. NIC binding can also be done from the Chinese text console, but the console only supports binding LAN1 and WAN1.

**Advanced Settings:**

| Field | Description |
|---|---|
| Work Mode | Full-duplex, half-duplex, or auto-negotiation. Leave as default in most cases. |
| NIC Speed | 10M / 100M / 1000M / 10000M. Leave as default in most cases. |
| LAN Inter-Access Control | When enabled, allows other LAN segments to access this LAN. |
| Clone MAC | Enter a MAC address here if you need to spoof the NIC's MAC address. |
| Extended IP | Add additional IP subnets to a single NIC. Useful for Web Portal auth on a separate IP range. The extended IP subnet can communicate directly with the primary LAN IP subnet. |

---

### 3. Adding a WAN Port

**Step 1:** Click **Add Configuration** and select a free NIC.

![Select Free NIC for WAN](https://www.ikuai8.com/attached/php/upload/image/20170915/1505447051427317.png)

**Step 2:** Set the NIC purpose to **WAN (External Network)**. USB-extended NICs are also supported.

![Set to WAN](https://www.ikuai8.com/images/wan22.png)

After binding:

![WAN Config](https://www.ikuai8.com/images/wan2.png)

#### Connection Types

Five WAN connection types are supported:

![Connection Type Selection](https://www.ikuai8.com/attached/php/upload/image/20170915/1505449083468173.png)

---

#### ① Static IP (Fixed IP)

Use this when the ISP provides a fixed public IP address (common for fiber/leased-line connections). Enter the IP, subnet mask, and gateway.

![Static IP](https://www.ikuai8.com/attached/php/upload/image/20170915/1505449237930108.png)

---

#### ② DHCP (Dynamic IP)

Use this when the ISP assigns an IP automatically. After selecting DHCP and saving, click **Connect** — the IP, mask, and gateway fields will populate automatically.

![DHCP](https://www.ikuai8.com/images/support_202109/dhcp111.png)

> **Note:** The correct sequence for DHCP setup is:
> 1. Select **DHCP** as the connection type
> 2. Click **Save**
> 3. Click **Connect**

---

#### ③ ADSL / PPPoE Dial-Up

Enter the ISP-provided username and password. After a successful dial, the status shows **Connected** and the IP, gateway, and DNS fields auto-populate.

![PPPoE Config](https://www.ikuai8.com/images/support_202109/adsl12.png)

![PPPoE Details](https://www.ikuai8.com/images/support_202109/adsl13.png)

- **Scheduled Redial** — Set a specific time to disconnect and reconnect.
- **Interval Redial** — Set an interval (in minutes) after which the connection will automatically redial.

---

#### ④ Physical NIC Hybrid Mode (Multi-Dial on One Line)

Allows multiple dial-up sessions on a single physical NIC and line simultaneously, stacking bandwidth. Supports mixing Static IP, DHCP, and PPPoE on the same NIC.

![Hybrid Mode](https://www.ikuai8.com/images/support_202109/ww1.png)

> **Note:** Whether multi-dial can successfully stack bandwidth depends on your ISP. Some regions support it, others do not. Test with your actual ISP.

**Multi-Dial Assistant settings:**

| Field | Description |
|---|---|
| Concurrent Dial Count | Set this to match the number of dial entries you have added manually |
| Abnormal IP Detection | If the dialed IP starts with a blacklisted prefix (e.g. 10., 172., 192., 168.), the router automatically redials. Redial interval: 10 seconds. |

![Abnormal IP](https://www.ikuai8.com/attached/php/upload/image/20170915/1505459208183063.png)

**Disconnect & Concurrent Redial settings:**

![Redial Config](https://www.ikuai8.com/attached/php/upload/image/20170915/1505461046334358.png)

![Multi-Dial](https://www.ikuai8.com/images/support/ww.png)

| Field | Description |
|---|---|
| Block redial on disconnect | When set, a dropped line does not auto-redial unless the dropout count threshold is reached |
| Disconnect detection cycle | How often to check for disconnected lines |
| Disconnect detection time window | Only check for disconnects within this time window |
| Disconnect detection interval | Check dropout count every N minutes |
| Disconnect count threshold | Redial all sessions when N dials have dropped |
| Server Name | Force dial to a specific server. Leave blank unless required by ISP. |
| Scheduled Redial | Disconnect and reconnect at a scheduled time |
| Interval Redial | Reconnect after every N minutes of connected time |

---

#### ⑤ VLAN-Based Hybrid Mode

Requires a VLAN-capable switch. Multiple ISP lines connect to the VLAN switch, which aggregates them onto a single WAN port on the router. Supports Static IP, DHCP, and PPPoE mixed on the same physical port.

![VLAN Hybrid](https://www.ikuai8.com/images/support/nwwsz11.png)

**VLAN Static IP:** Enter the VLAN ID, name, IP, subnet mask, and gateway.

![VLAN Static](https://www.ikuai8.com/images/support/nwwsz22.png)

> QinQ (double-tagged VLAN) is supported. Enter outer VLAN first, then inner VLAN, separated by `.` (e.g. `100.200`).

![QinQ Static](https://www.ikuai8.com/images/vlan200.jpg)

**VLAN DHCP:** Enter the VLAN ID and name. IP is obtained automatically.

![VLAN DHCP](https://www.ikuai8.com/images/support/nwwsz44.png)

![QinQ DHCP](https://www.ikuai8.com/images/vlan300.jpg)

**VLAN PPPoE:** Enter the VLAN ID, PPPoE username, and password.

![VLAN PPPoE](https://www.ikuai8.com/images/support/nwwsz66.png)

![VLAN PPPoE QinQ](https://www.ikuai8.com/images/support_202109/vlan500.jpg)

---

### Common WAN Settings

| Field                  | Description                                                                                                                                      |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Default Gateway        | Check this on one WAN port to make it the default route. Default is WAN1. All traffic uses the default gateway unless routing rules override it. |
| Auto Failover          | When enabled, if a WAN line drops, traffic automatically switches to another available line. Only needed with multiple WAN lines.                |
| Connection Time Window | When enabled, this WAN line is only active during the specified time range.                                                                      |
| Line Detection         | Configures the ping/HTTP check mechanism to verify WAN connectivity.                                                                             |

> **Note on auto failover behavior with multiple WANs:**
> - **Multi-WAN Load Balancing:** If one line drops, traffic automatically flows over the remaining healthy lines.
> - **Port/Protocol Routing with multiple lines selected:** Only **PPPoE** lines trigger failover to another line when they drop. Static IP and DHCP lines that fail will fall back to the **default gateway** line only.
> - **PPPoE line with IP obtained but detection failed:** Routing rules to that line still apply — failover to another line is **not** triggered in this case.
