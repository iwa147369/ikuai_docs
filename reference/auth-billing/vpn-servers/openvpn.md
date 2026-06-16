# OpenVPN Server (OpenVPN服务端)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzjf/fhry/openvpn.html

## I. Overview

OpenVPN is an SSL/TLS-based VPN using the OpenSSL library. It supports both Layer 2 (TAP) and Layer 3 (TUN) virtual interfaces, LZO compression, and flexible authentication methods. All traffic runs over a single IP port (default UDP 1194).

---

## II. Field Reference

| Field | Description |
|---|---|
| Generate Client Config | Export the server configuration (including CA certificate) for use by clients. |
| Show Log | Display server startup and client connection log. |
| Server Port | Default: **1194** (IANA official OpenVPN port). |
| VPN Subnet / Mask | IP address pool and mask for VPN clients. |
| Authentication Mode | Account-based, or static key (tls-auth / tls-crypt). Static key requires firmware v3.5.3+. |
| Tunnel Protocol | **UDP** (default, recommended). Use **TCP** when the link has high latency or packet loss. |
| Tunnel Type | **TUN** (Layer 3 IP tunnel) or **TAP** (Layer 2 Ethernet tunnel). |
| Encryption Algorithm | Encrypts data in transit. |
| LZO Compression | Compresses tunnel data (saves bandwidth; uses additional CPU). |
| MTU | Default: **1400** (recommended: link MTU − 100). |
| CA Certificate | Root certificate used to sign server and client certificates. |
| Server Certificate / Private Key | Server identity certificate pair. |
| Push Routes | Subnets pushed to clients — clients route traffic for these subnets through the VPN. Supports remarks (v3.7.16+). |
| Additional Config | Advanced raw OpenVPN configuration directives for expert users. |

---

## III. Mutual LAN Access Setup (iKuai ↔ iKuai)

To enable bidirectional LAN access between OpenVPN server and client:

1. **Server:** Configure **Push Routes** with the server's local LAN subnet.
2. **Server:** In Account Management, create a VPN account with a **fixed IP** (must be within the address pool range).
3. **Server:** Add a **Static Route** — destination = client's LAN subnet, next-hop = the client's fixed VPN IP.
4. **Client:** Configure the VPN, enable **Accept Server Pushed Routes**.

> When iKuai acts as both ends, the fixed IP for the VPN account **must be within** the address pool range. An IP outside the pool will cause dial-in failure.

---

## IV. Notes

- Fixed IPs for OpenVPN accounts **must be inside** the address pool range (opposite to PPTP/L2TP where they must be outside).
- When the server topology is **NET30**, the server cannot access the client's LAN.
- Clients must enable **Accept Server Pushed Routes** to reach the server's pushed subnets.

---

## V. Common Issues

### Client and server LAN cannot reach each other
1. Check routing table for correct routes to the remote subnet with no conflicts.
2. Ping the remote LAN gateway; if reachable but downstream devices are not, check their firewall and gateway.
3. Use Route Trace to find where the path fails.
