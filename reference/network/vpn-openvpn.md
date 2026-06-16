# OpenVPN Client

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/vpn/openvpn.html

## I. Overview

Configuration page for iKuai acting as an **OpenVPN client** — connecting to a remote OpenVPN server.

---

## II. Configuration

![OpenVPN List](https://www.ikuai8.com/images/support/open-VPN.png)

Click **Add**.

![OpenVPN Add](https://www.ikuai8.com/images/support_202109/openvpn1.png)

| Field | Description |
|---|---|
| Connection Name | A name for this dial connection (e.g., `OpenVPN1`). |
| Server IP / Domain | IP or hostname of the OpenVPN server. |
| Service Port | Port used by the OpenVPN service. IANA-assigned default: 1194. |
| Auth Method | **Account Auth** (username/password), **Static Key (tls-auth)**, or **Static Key (tls-crypt)**. |
| Username | Account on the OpenVPN server (for account auth). |
| Password | Account password. |
| Line | The WAN line used for the VPN connection. |
| Tunnel Protocol | **UDP** (recommended — more efficient); **TCP** (use when the link has high latency or packet loss, since UDP without retransmission over lossy links causes the upper protocols to retransmit excessively). |
| Tunnel Type | **TUN** — Layer 3 IP tunneling. **TAP** — Layer 2 Ethernet (can carry any L2 traffic). |
| Encryption Algorithm | Data encryption for the tunnel. |
| LZO Compression | Compress traffic to save bandwidth; uses additional CPU resources. |
| MTU | Recommended value: link MTU − 100. |
| CA Certificate | Certificate used to sign the server (and optionally client) certificate. Verifies the server's identity. |
| Client Certificate / Client Private Key | Paired; required only if the non-iKuai server requires client certificate verification. |
| Server Route Push | **Enabled** — accept routes pushed by the server and route matching traffic through the VPN. **Disabled** — ignore pushed routes. |
| Add Route | Manually specify subnets to route through this VPN (same effect as a static route). |
| Scheduled Redial | Set specific times to disconnect and reconnect. |
| Additional Config | Raw OpenVPN config directives for advanced users. Useful for options the iKuai UI doesn't expose (e.g., `cipher AES-128-GCM`). |
| Local IP | Assigned from the server's address pool. Read-only. Empty = dial not successful. |

![OpenVPN Certificate Fields](https://www.ikuai8.com/attached/php/upload/image/20170920/1505879900864343.png)

![OpenVPN Route Push](https://www.ikuai8.com/images/support/open-VPN1.png)

**Certificate notes:**
- iKuai as server does not validate client certificates — client cert/key can be left blank.
- If the peer (non-iKuai) server requires client certificate validation, the client cert is provided by the server.
- If both ends are iKuai: copy the CA certificate from the server to the client.
- To use a custom certificate: generate it with OpenVPN SSL tools. If unsure, the default certificate and key work fine.

> **Capacity:** Keep total OpenVPN clients at around 200 or fewer. Actual maximum depends on hardware.

---

## III. Common Issues

### Fixed IP must be within the pool range

Unlike PPTP/L2TP, OpenVPN requires a fixed IP assignment to be **within** the server's address pool range. Using an IP outside the pool will cause dial failure.

### iKuai does not support TLS verification

If the peer server requires TLS verification (separate from tls-auth/tls-crypt), disable it on the server.

### VPN client and server LAN cannot reach each other

1. Check the routing table for routes to the peer's subnet and for conflicts.
2. Ping the peer's LAN gateway. If reachable but devices behind it are not, check for firewalls or missing gateways.
3. Use tracert to find which hop loses the path.

### Windows client traffic not going through the VPN

Edit the OpenVPN `.ovpn` client config file:

```
#redirect-gateway def1 bypass-dns
# Uncomment this to route all traffic through VPN. Comment out to use local internet.

#route-nopull
# Uncomment to prevent the VPN from adding any routes on this machine.
# All traffic will go through the local internet regardless of VPN.
```

### OpenVPN dial failure troubleshooting

![OpenVPN Troubleshoot](https://www.ikuai8.com/images/support/open-VPN11.png)
