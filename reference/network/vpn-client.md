# VPN Client

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/vpn.html

## I. Overview

The VPN Client page configures the iKuai router to connect outbound as a VPN client (dial-out). This is distinct from VPN server settings; the router initiates the connection to a remote VPN server.

The example below covers **PPTP client** configuration.

---

## II. Configuration Fields

| Field | Description |
|---|---|
| Dial Name | Must start with "PPTP" (e.g., `pptp1`) |
| Service Port | Port matching the server; PPTP default is `1723` |
| Server Address/Domain | IP address or domain name of the PPTP server |
| Username | Credential created on the VPN server |
| Password | Credential created on the VPN server |
| MTU | Maximum transmission unit — largest packet size the protocol layer can send |
| MRU | Maximum receive unit for the PPP link layer |
| Line Selection | Which physical WAN line to use for the VPN connection |
| Reconnection Interval | Minutes to wait before auto-redialing after a successful connection |
| Scheduled Redialing | Set specific times to disconnect and reconnect automatically |

> The router automatically obtains its local VPN IP from the server's address pool. Manual IP assignment is not possible. If no IP is assigned, the connection has failed.

---

## III. Common Issues

| Issue | Solution |
|---|---|
| Secondary routing prohibition blocks PPTP | Disable this restriction on the upstream router |
| Domain-based traffic splitting fails to load pages | Verify DNS configuration; test with port-based splitting instead |
| Server-side EAP encryption causes dial failure | Disable EAP on the Windows 2003 server |
| VPN client and server internal networks cannot communicate | Check routing tables, test gateway ping, use tracert for path analysis |

---

## IV. Capacity Notes

For stability, keep VPN client connections below **30**. Maximum capacity depends on hardware specifications.
