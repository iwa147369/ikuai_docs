# PPTP VPN Client

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/vpn/pptp.html

## I. Overview

Configuration page for iKuai acting as a **PPTP VPN client** — dialing into a remote PPTP server.

---

## II. Configuration

![PPTP List](https://www.ikuai8.com/images/support/pptp1.png)

Click **Add**.

![PPTP Add](https://www.ikuai8.com/images/pptp123.jpg)

| Field | Description |
|---|---|
| Connection Name | Must start with `PPTP` (e.g., `pptp1`). Used to identify the dial connection. |
| Service Port | Port used to reach the server. Must match the server setting. Default: 1723. |
| Server Address / Domain | IP or hostname of the PPTP server. |
| Username | Account configured on the PPTP server. |
| Password | Password for the account. |
| MTU | Maximum Transmission Unit — max packet size in bytes. Tied to the network interface. |
| MRU | Maximum Receive Unit — similar to MTU but for the PPP link layer. |
| Line | The WAN line the VPN uses for its outbound connection. |
| Redial Interval | How many minutes after a successful connection before it redials. |
| Scheduled Redial | Enable to set specific times to disconnect and reconnect. |

![PPTP Example](https://www.ikuai8.com/images/support/pptp2.png)

**Local IP:** Assigned automatically from the PPTP server's address pool. Cannot be filled manually. If empty after connecting, the dial was not successful.

> **Note:** When assigning a fixed IP to a VPN account, use an IP **outside** the server's default address pool range — the server does not reserve pool IPs for fixed-IP accounts, which can cause IP conflicts and prevent affected clients from accessing the network.

> **Capacity:** Keep total VPN client connections at 30 or fewer to ensure stability. Actual maximum depends on hardware.

---

## III. Common Issues

### Block secondary routers causes PPTP line to stop working

![Secondary Router Issue](https://www.ikuai8.com/attached/php/upload/image/20170302/1488438283217418.png)

If the upstream router (Router A) has "Block Secondary Routers" enabled, downstream clients through Router B cannot use the PPTP VPN to reach the internet. Disable this feature on Router A.

### Domain routing not working with PPTP

1. Check whether multi-WAN DNS is configured (or intentionally not configured).
2. Test with a port routing rule pointing the test machine specifically to the PPTP line.

### EAP encryption on Windows 2003 server causes dial failure

If iKuai logs show an EAP error, the Windows 2003 VPN server has EAP authentication enabled. iKuai does not support EAP. Uncheck EAP on the server.

![EAP Error](https://www.ikuai8.com/attached/php/upload/image/20170505/1493977243493467.png)

![EAP Fix](https://www.ikuai8.com/attached/php/upload/image/20170505/1493979192537919.jpg)

### VPN client and server LAN cannot reach each other

1. Check the current routing table — verify a route exists for the peer's LAN subnet, and that there are no conflicting routes.
2. Ping the peer's LAN gateway. If the gateway is reachable but devices behind it are not, check whether those devices have a firewall enabled or lack a properly configured gateway.
3. Use tracert to trace the path — identify which gateway loses the next hop.

### PPTP dial failure troubleshooting

![PPTP Troubleshoot](https://www.ikuai8.com/images/support/pptp11.png)
