# DHCP Static Assignment

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/dhcp/jtfp.html

## I. Overview

Allows LAN clients using DHCP to always receive a specific (fixed) IP address, bound by their MAC address.

---

## II. How to Use

![Static Assignment List](https://www.ikuai8.com/images/support_202109/dhcpjtfp111.jpg)

Add MAC-to-IP bindings here. You can also configure preferred/alternate DNS per static entry (firmware v3.7.12+). When a device with a bound MAC requests an IP, it always receives the assigned IP.

**Two ways to add a static assignment:**

### Method 1 — Manual Entry

Click **Add** and enter the IP address and the client's MAC address.

![Manual Add](https://www.ikuai8.com/images/support/tyy62.png)

> **Note:** The manually entered IP must be within the corresponding DHCP address pool's subnet range.

### Method 2 — From DHCP Terminal List

Go to **DHCP Terminal List**, select a client, and click **Add to Static Assignment**.

![From Terminal List](https://www.ikuai8.com/images/support/dhcpzdlb1.png)

---

## III. Common Issues

### Client gets a different IP than what was assigned

1. DHCP server is not running (no DHCP pool configured).
2. The static IP is outside the LAN port's subnet range.
   - Example: LAN1 is `192.168.0.1/24` (range `192.168.0.1–192.168.0.254`), but the static assignment is `192.168.5.10` — these are different subnets, so the binding fails.
3. The client already has a lease and hasn't renewed yet. Wait for the lease to expire, then restart the client to obtain the new IP.
4. The client's MAC address is not in the binding list.
5. Another DHCP server on the LAN is responding first.

### What does "Compatible with ARP binding list as static assignment" do?

DHCP static assignment fixes a user's IP address so they always get the same IP when connecting. Checking **Compatible with ARP binding as static assignment** causes all entries in the ARP binding list to act as static DHCP assignments — they will not appear in the static assignment list UI, but the binding is enforced.
