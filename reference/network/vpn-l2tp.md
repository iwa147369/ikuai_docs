# L2TP VPN Client

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/vpn/l2tp.html

## I. Overview

Configuration page for iKuai acting as an **L2TP VPN client** — dialing into a remote L2TP server.

---

## II. Configuration

![L2TP List](https://www.ikuai8.com/images/support/l2tp1.png)

Click **Add**.

![L2TP Add](https://www.ikuai8.com/images/L2.jpg)

| Field | Description |
|---|---|
| Connection Name | Must start with `L2TP` (e.g., `L2TP1`). |
| Service Port | Default L2TP port is 1701. Must match the server and must not conflict with other services. |
| Server Address / Domain | IP or hostname of the L2TP server. |
| Username | Account configured on the L2TP server. |
| Password | Password for the account. |
| MTU | Maximum Transmission Unit — max packet size in bytes. |
| MRU | Maximum Receive Unit — PPP link layer concept. |
| Pre-shared Key | Must match the server's pre-shared key. Leave blank if the server does not use one. |
| Local ID | Identifies this router's local identity. Must match the server's "Remote ID" field. Leave blank if not configured on the server. |
| Remote ID | Identifies the peer. Must match the server's "Local ID" field. Leave blank if not configured on the server. |
| Line | The WAN line the VPN uses for its outbound connection. |
| Redial Interval | Minutes after a successful connection before it redials. |
| Scheduled Redial | Set specific times to disconnect and reconnect. |

**Local IP:** Assigned automatically from the server's address pool. Cannot be filled manually. Empty = dial not successful.

![L2TP Example](https://www.ikuai8.com/images/support/l2tp2.png)

> **Note:** When assigning a fixed IP to a VPN account, use an IP **outside** the default address pool range to avoid IP conflicts.

> **Capacity:** Keep total VPN client connections at 30 or fewer. Actual maximum depends on hardware.

---

## III. Common Issues

### Pre-shared key conflict with IPSec

- When a pre-shared key is set in L2TP, you cannot have two L2TP rules pointing to the same server address and WAN line.
- If IPSec VPN is also configured with a pre-shared key, the L2TP pre-shared key will conflict and cause L2TP to fail. (Enterprise firmware v3.6.8+ resolves this when identities are configured.)

### VPN client and server LAN cannot reach each other

1. Check the routing table for routes to the peer's LAN subnet and for conflicts.
2. Ping the peer's LAN gateway. If reachable but devices behind it are not, check for firewalls or misconfigured gateways on those devices.
3. Use tracert to identify which hop breaks the path.

### L2TP dial failure troubleshooting

![L2TP Troubleshoot](https://www.ikuai8.com/images/support/l2tp11.png)
