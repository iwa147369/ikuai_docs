# IPSec VPN

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/vpn/ipsecvpn.html

## I. Overview

IPSec is an IETF open security framework for the network layer. It combines the AH (Authentication Header) and ESP (Encapsulating Security Payload) protocols with IKE (Internet Key Exchange) for key negotiation and management.

**Authentication methods:**
- **Pre-shared Key** — simpler to configure, broadly compatible. Special characters are not supported.
- **Self-signed Certificate** — higher security through cryptographic key/certificate verification.

**IKE versions:**
- **IKEv1** — older; requires at least 6 message exchanges; has Main Mode and Aggressive Mode.
- **IKEv2** — simplified; 4 messages for one SA pair, 2 more per additional SA pair.

---

## II. Configuration

### Field Reference

| Field | Description |
|---|---|
| Status | Enable or disable this IPSec connection. |
| Name | Label to distinguish multiple IPSec connections. |
| Remote IP / Domain | The peer router's WAN IP or domain name. Leave blank to act as a passive (server-only) endpoint. |
| Local Subnet | This router's LAN subnet (e.g., `192.168.1.0/24`). Use `0.0.0.0/0` for all subnets. |
| Remote Subnet | Peer's LAN subnet(s). Multiple subnets can be added. |
| Line | The WAN line to use for establishing the IPSec tunnel. |
| IKE Version | `IKEv1` or `IKEv2`. Both ends must use the same version. |
| IKE Negotiation Mode | IKEv1 only. **Main Mode** (bidirectional auth, more secure) or **Aggressive Mode** (unidirectional auth, higher success rate). Both ends must use the same mode. |
| IKE SA Lifetime | How long before the IKE SA is renegotiated. |
| IKE Proposal | Encryption, authentication, and key exchange algorithms. Both ends must match (IKEv1: both must match or both auto; IKEv2: one can be auto, the other specific). |
| Auth Method | **Pre-shared Key** or **Self-signed Certificate**. |
| Pre-shared Key | Simple key shared between both ends. No special characters. |
| Local ID / Remote ID | Identity labels. Must match the peer's corresponding field. Cannot be identical to each other. Cannot be empty when using certificates (must match the certificate common name). |
| Local Private Key | Paired with Local Certificate for certificate auth. |
| Local Certificate | Paired with Local Private Key. |
| Remote Certificate | Provided by the peer; used to verify the peer's identity. |
| ESP SA Lifetime | How long before the ESP SA is renegotiated. |
| ESP Encryption Algorithm | Encryption algorithm for the IPSec tunnel. |
| ESP Auth Algorithm | Authentication algorithm for the IPSec tunnel. |
| Allow Compression | Compresses traffic to save bandwidth; uses additional CPU resources. |
| DPD Detection | Dead Peer Detection behavior. `clear` = do not reconnect on failure. `hold` = buffer matching traffic and renegotiate. `restart` = immediately renegotiate. Use `restart` with IKEv1; any mode is valid with IKEv2. |

### Example — Initiator and Responder Config

![IPSec Topology](https://www.ikuai8.com/attached/php/upload/image/20170112/1484215832821457.jpg)

Enable the service and configure basic info on the initiator:

![Initiator Basic Config](https://www.ikuai8.com/attached/php/upload/image/20170920/1505880884659194.png)

Enable the service on the responder:

![Responder Basic Config](https://www.ikuai8.com/attached/php/upload/image/20170920/1505880992288496.png)

Initiator IKE/Auth config:

![Initiator IKE Config](https://www.ikuai8.com/attached/php/upload/image/20170920/1505881125611645.png)

Responder IKE/Auth config:

![Responder IKE Config](https://www.ikuai8.com/attached/php/upload/image/20170920/1505881142948777.png)

---

## III. Important Notes

1. Both ends must use the **same IKE version**.
2. IKEv1: both ends must use the **same negotiation mode** (Main or Aggressive).
3. IKEv1: IKE proposals must match exactly. If using auto-negotiation, both ends must select auto.
4. IKEv1: only **one remote subnet** can be specified.
5. Both iKuai devices, IKEv2, multiple remote subnets: the peer's **Local Subnet must be `0.0.0.0/0`**.
6. Local ID and Remote ID **cannot be the same** and cannot be empty.
7. IKEv2: IKE proposals must match. If one end uses auto-negotiation, the other can specify concrete parameters.
8. **Without NAT:** Either router can be the initiator or responder.
9. **With NAT:** The server-side router must leave "Remote IP/Domain" blank (passive mode). Start the server first, then the client. The server side must not be behind NAT.
10. Dynamic IP or NAT environment: leave the remote IP/Domain field blank to act as a passive endpoint.
11. If disconnected, the router checks and attempts reconnection every **6 minutes**.
12. iKuai does **not support PFS** (Perfect Forward Secrecy).
13. When IPSec uses a pre-shared key: L2TP client rules must **not** also use a pre-shared key — this causes L2TP dial failure. (Enterprise v3.6.8+ resolves this when identities are set.)

> **Capacity:** Keep total VPN client connections at 30 or fewer. Actual maximum depends on hardware.

---

## IV. Common Issues

### VPN client and server LAN cannot reach each other

1. Ping the peer's LAN gateway. If reachable but internal devices are not, check for firewalls or misconfigured gateways on those devices.
2. Use tracert to find which hop breaks the path.

> **Note:** Since firmware v3.4.6, inter-VPN access no longer requires the "Web Access Control" checkbox — **except for IPSec VPN**, which still requires it.

### IPSec dial failure troubleshooting

![IPSec Troubleshoot](https://www.ikuai8.com/images/ip.jpg)

---

## V. Technical Background

**AH vs ESP:**
- **AH** (Authentication Header): Provides data source verification, integrity, and replay protection. No encryption.
- **ESP** (Encapsulating Security Payload): Provides encryption, data source verification, integrity, and replay protection.

**IKEv2 exchange process:**
- **Initial Exchange** (4 messages): Establishes IKE SA + first IPSec SA pair.
- **Create Child SA Exchange** (2 messages): Adds additional SA pairs or renegotiates the IKE SA.
- **Informational Exchange**: Carries control messages (errors, notifications) under IKE SA protection.

IKEv2 reduces IKEv1's minimum 6 messages to 4, making connection setup faster.
