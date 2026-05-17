# PPPoE Server (PPPoE服务端)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/fhry/pppoe.html

## I. Overview

iKuai can act as a PPPoE server, enabling LAN clients to dial in using PPPoE credentials. This allows per-user bandwidth control, accounting, and access management.

---

## II. Field Reference

| Field | Description |
|---|---|
| Service Status | Enable or disable the PPPoE server. |
| PPPoE Service Name | Identifier for this PPPoE server when multiple PPPoE servers exist on the network. Clients can specify this name when dialing. |
| Server Address | Virtual IP address of the PPPoE server. |
| Primary/Backup DNS | DNS servers pushed to clients after successful dial-in. Use valid public DNS. |
| Authentication Mode | See modes below. |
| Excess Account Action | When a shared-count limit is reached: ① Kick the earlier session (new login takes over). ② Reject the new login. |
| Client Address Pool | IP range assigned to dial-in clients, bound to a specific LAN interface. Only `lan1` has a default pool — add pools for other LAN ports manually. |
| LAN Cross-Access Rate Limit | Whether multi-LAN dial-in clients are subject to rate limits when accessing each other. |
| Block Client Cross-Access | Prevent dial-in clients from communicating with each other. |
| Force Client Dial-up | When enabled, clients can only access the internet via PPPoE — direct LAN access is blocked (use with ACL to exempt specific IPs). |
| Force Server Name Validation | Client's configured service name must match the server's name exactly; otherwise dial-in fails. |
| Enhanced Disconnect Detection | After LCP fails, also checks internal traffic monitoring. Only kicks the client if both LCP and internal monitoring show no activity. |
| VLAN Binding | Account's configured VLAN must match the client's VLAN at dial-in time. Supports QinQ (format: `outer.inner`). |
| NIC Binding | Account must belong to the specific LAN port the client dials in from. |
| MTU / MRU | Maximum Transmission/Receive Unit for PPP frames. |
| LCP Detection | Link Control Protocol keepalive. 3s per packet; 20 missed = client kicked. |
| Scheduled Server Restart | Periodic restart of the PPPoE service (temporarily disconnects all clients). |
| Scheduled User Disconnect | Disconnect clients that have been online longer than the configured duration. |

### Authentication Modes

| Mode | Description |
|---|---|
| Local Account | Uses accounts created in **Auth & Billing → Account Management** (type: PPPoE). |
| Local Account + Empty Password | Clients can dial in with the account name only, no password required. Designed to block secondary routers that require a password to save. Note: accounts in the management page must still have a non-empty password. |
| Any User Dial-in | Any username/password is accepted — no credential check. |
| Third-party RADIUS | Integrates with external RADIUS systems (Lingfeng, Lanhaizhuyue, Zhuomai). |

---

## III. Notes

- The default client address pool only covers `lan1`. To allow dial-in from `lan2` or other interfaces, add a pool for that interface.
- After clicking **OK**, also scroll to the bottom and click **Save**.
- Fixed IPs for PPPoE accounts must be **outside** the address pool range — the server does not reserve pool IPs for fixed-IP accounts, which can cause duplicate assignments.

---

## IV. Common Issues

### A specific client should not need to dial in
1. Enable **Force Client Dial-up** on the PPPoE server.
2. Assign the exempt client a static IP on the same subnet as the LAN interface.
3. Add an ACL rule in **Security Settings → ACL Rules** to allow that IP to forward traffic without dialing in.

### Other LAN ports cannot dial in
Add a client address pool for the other LAN interface on the PPPoE server settings page.

### Cannot dial in at all
Check whether WEB authentication is enabled with **Authenticate All IPs** — if the PPPoE address pool subnet is included, clients cannot dial in. Change to **Authenticate Partial IPs** and exclude the PPPoE pool subnet.
