# IPv4 Terminal Monitoring

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ztjk/7cf09.html

## I. Overview

The IPv4 page displays real-time information about internal network hosts monitored by the iKuai flow control router, including traffic, connections, and protocol distribution across internal networks, protocols, policies, lines, and the system.

The page auto-refreshes every 2 seconds.

---

## II. Main Functions

### View Device Details

Click **Details** on any terminal to see:

- Basic information
- Active connection specifics
- Historical records
- Traffic distribution by protocol

### Connection Information

For each active connection, the page shows:

| Field | Description |
|---|---|
| Protocol Name | Protocol type being used |
| External Routing Address | The WAN path used |
| Connection Status | Connected, Stateless, Waiting, or Closed |
| Target Address | Destination IP being accessed |
| Target Port | Destination port |

**Connection states:**

| State | Meaning |
|---|---|
| Connected | TCP three-way handshake completed |
| Stateless | No connection state (UDP shows as `--`) |
| Waiting | TCP request sent, awaiting response |
| Closed | Four-way handshake complete, connection terminated |

### Block Internet Access

Click **Prohibit Online** to block a specific device from accessing the network. Blocked devices appear in **Behavior Control → MAC Access Control**.

### Edit Device Notes

Device descriptions can be edited here and sync automatically across DHCP settings, ARP binding, and terminal name management pages.

---

## III. Common Issues

**Device shows an IP but no traffic:**
Check PPPoE settings, web authentication configuration, firewall ACL rules, ARP binding status, and MAC access controls.

**Device exists on the network but doesn't appear on the IPv4 page:**
The monitoring system only tracks clients with traffic activity within the past 2 minutes.
