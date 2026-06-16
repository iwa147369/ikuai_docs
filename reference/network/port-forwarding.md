# Port Forwarding (Port Mapping)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/feqs.html

## I. Overview

Port forwarding (also called port mapping) is a form of NAT that translates an external public IP + port to an internal private IP + port. This allows internet users to reach services hosted on internal LAN servers.

---

## II. Configuration

![Port Forwarding](https://www.ikuai8.com/images/dk1.png)

| Field | Description |
|---|---|
| Internal (LAN) Address | The IP address of the internal server to forward traffic to. |
| Internal Port | The port the internal server listens on. |
| Protocol | TCP, UDP, or both. |
| Mapping Type | **WAN Interface** — select a WAN port by name; **WAN IP** — enter the specific public IP. |
| External (WAN) Address | The WAN port or public IP that external clients connect to. |
| External Port | The port number external clients use to reach the service. |
| Allowed Source IPs | (Optional) Restrict access to specific external IP addresses. Leave blank to allow all. |

> **Notes:**
> - For PPPoE dial-up connections, you can use the interface name (e.g. `adsl1`) instead of an IP address in the WAN address field.
> - Multiple port ranges can be combined in one rule (e.g. `80-100,21,200-300`), but the internal and external port lists must match exactly.
> - Firmware v3.4.6+: up to 16 ports or port ranges per rule for the internal port field.

---

## III. Example

**Goal:** Access the secondary router's admin web page (port 81) from outside via the primary router's WAN IP.

**Environment:**
- Primary router LAN: `192.168.15.1/24`, WAN1: `192.168.1.33/24`
- Secondary router WAN: `192.168.15.254/24`, LAN: `192.168.33.253`

**Steps:**

1. On the secondary router, enable remote IPv4 and IPv6 access.

   ![Enable Remote Access](https://www.ikuai8.com/images/dkys11.jpg)

2. On the primary router, add a port forwarding rule:
   - Internal address: `192.168.15.254`
   - Internal port: `81`
   - External port: `81` (or any free external port)
   - WAN address: WAN1

   ![Port Forwarding Rule](https://www.ikuai8.com/images/support/dkys111.png)

3. Access via `<WAN1 IP>:81` from the internet.

---

## IV. Common Issues

### Port forwarding not working

1. Verify the internal server's gateway points to the iKuai LAN IP. If the server does not route through iKuai, forwarding cannot work.
2. Confirm the correct port — distinguish between the service port and the resource port. Test connectivity within the LAN first.
3. Check for port conflicts. External ports 80 and 8080 are frequently blocked or conflicted.
4. If Fanxing (繁星) is enabled, it occupies UDP ports above 4096 by default — check for conflicts.
5. Verify the **Allowed Source IPs** field is not inadvertently blocking access.
6. Some ISPs block specific ports at the carrier level — test with a different port if nothing else helps.

**Mapping priority order (firmware ≥ v3.4.8):**
Fanxing > Port Forwarding > UPnP > NAT1 > DMZ

(Prior to v3.4.8: Fanxing > Port Forwarding > NAT1 > DMZ > UPnP)
