# DMZ Host (DMZ主机)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/feqs/dmz.html

## I. Overview

DMZ (Demilitarized Zone) exposes a single internal server completely to the internet. Any traffic arriving at the designated WAN IP/interface is forwarded to the DMZ host as if the external host were directly connecting to the internal server.

This is the simplest way to fully expose a server behind the router without configuring individual port forwards — but it provides no firewall protection for that host.

---

## II. Configuration

![DMZ Settings](https://www.ikuai8.com/images/support/111.jpg)

| Field | Description |
|---|---|
| Mapping Type | **WAN Interface** — traffic arriving on the selected interface is forwarded to the DMZ host. **WAN IP** — traffic arriving on the specified public IP is forwarded. |
| External Address | The WAN interface (or WAN IP) to match inbound traffic against. |
| Internal Address | The LAN IP of the internal server to expose. |
| Excluded Protocol | Protocols used by the router itself (e.g., for management access) that should not be forwarded to the DMZ host. Used together with Excluded Ports. |
| Excluded Ports | Ports reserved for the router's own use that should not be forwarded to the DMZ host. Used together with Excluded Protocol. |

> **Note:** If the Fanshu (繁星) relay service is enabled on the router, UDP ports 4096 and above may be occupied by default.

---

## III. Example

**Environment:**
- Primary router: LAN1 = `192.168.15.1`, WAN1 = `192.168.1.33`, WAN2 = `192.168.1.34`, web admin port = 880
- Secondary router: WAN = `192.168.15.254`, LAN = `192.168.33.253`, web admin port = 81

**Goal:** Expose the secondary router's admin page via the primary router's WAN IP.

**Steps:**

1. On the secondary router, enable **Allow IPv4 and IPv6 Access**.

   ![Enable access](https://www.ikuai8.com/images/support_202109/dmz1.png)

2. On the primary router, configure a DMZ rule pointing to the secondary router's LAN address. Exclude the primary router's own admin port (880) in the DMZ rule so it remains accessible.

   ![DMZ Config](https://www.ikuai8.com/images/support/dmzzj.png)

3. Verify from an external network that accessing the primary router's WAN IP reaches the secondary router's admin page.

   ![Verification](https://www.ikuai8.com/images/support/dmzzj1.png)

---

## IV. Notes

- **Priority order** (firmware v3.4.8+): Fanshu (繁星) > Port Forwarding > UPnP > NAT1 > DMZ
  (v3.4.7 and below: Fanshu > Port Forwarding > NAT1 > DMZ > UPnP)
- **One rule per line:** A given WAN line can only match one DMZ rule. If multiple rules target the same line, only the first rule takes effect — subsequent rules on the same line are ignored.
