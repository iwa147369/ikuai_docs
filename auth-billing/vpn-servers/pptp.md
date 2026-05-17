# PPTP Server (PPTP服务端)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/fhry/pptp.html

## I. Overview

PPTP (Point-to-Point Tunneling Protocol) is a VPN protocol built on PPP. It supports PAP and EAP authentication and allows remote users to securely access internal networks over the internet.

---

## II. Field Reference

| Field | Description |
|---|---|
| Service Status | Enable or disable the PPTP server. |
| Client Address Pool | IP range assigned to VPN clients after dial-in. Default pool can be used as-is. Must not overlap with other interface subnets. |
| Primary/Backup DNS | DNS pushed to VPN clients. |
| Server Port | Default: **1723**. PC clients do not support custom ports — changing this breaks PC client connections. Other clients must match the server port. |
| MPPE Encryption | Data encryption for the tunnel. Default: **Optional** (matches Windows VPN default). Must match the client's encryption setting. |
| MTU / MRU | Maximum Transmission/Receive Unit for PPP frames. |

---

## III. Notes

- After configuring the server, create accounts in **Auth & Billing → Account Management** (type: PPTP) before clients can dial in.
- Fixed IPs for PPTP accounts must be **outside** the address pool range — the server does not reserve pool IPs for fixed-IP accounts.
- Recommended maximum: **200 concurrent VPN clients** for stability.
- Client encryption mode must match the server's MPPE setting.

---

## IV. Common Issues

### VPN client and server LAN cannot reach each other
1. Check the routing table for a route to the remote subnet; verify no subnet conflicts.
2. Ping the remote LAN gateway. If reachable but downstream devices are not, check their firewall and default gateway settings.
3. Use Route Trace to identify where the path fails.
