# L2TP Server (L2TP服务端)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/fhry/l2tp.html

## I. Overview

L2TP (Layer 2 Tunneling Protocol) is an industry-standard VPN tunneling protocol. Compared to PPTP, L2TP supports multi-tunnel, packet header compression, and tunnel authentication. L2TP requires a point-to-point connection and is commonly used with IPSec for encryption.

---

## II. Configuration

Enable the L2TP server by checking **Enable** and saving. Refresh the page to confirm it is running.

After enabling the server, create VPN accounts in **Auth & Billing → Account Management** (type: L2TP), then connect from clients using those credentials.

### Client Notes
- If no **Pre-shared Key** is set on the server, do not select "shared key" authentication on the client.
- PC clients do not support specifying a custom port — only the default L2TP port **1701** is supported. Changing the server port will break PC client connections.

---

## III. Notes

- Recommended maximum: **200 concurrent VPN clients** for stability.
- Fixed IPs for VPN accounts must be **outside** the default address pool range. The server does not reserve pool IPs for fixed-IP accounts — duplicate IPs can occur otherwise.
- LAN clients cannot use the router's own WAN IP as the VPN server address for dial-in.

---

## IV. Common Issues

### VPN client and server LAN cannot reach each other
1. Check the routing table — ensure a route to the remote subnet exists and there are no subnet conflicts.
2. Use Ping to test connectivity to the remote LAN gateway. If the gateway is reachable but the device behind it is not, check whether the device has a firewall or incorrect default gateway.
3. Use Route Trace to identify where the path fails.
