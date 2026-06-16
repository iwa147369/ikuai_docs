# DHCP Server

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/dhcp/dhcp.html

## I. Overview

DHCP (Dynamic Host Configuration Protocol) is a LAN protocol that automatically assigns IP addresses to devices. It is used to centrally manage IP allocation across all computers on the network.

---

## II. How to Use

![DHCP Server Config](https://www.ikuai8.com/images/support_202109/dhcp222.png)

| Field | Description |
|---|---|
| Service Interface | Select which LAN to serve IPs for (e.g. LAN1, LAN2). Virtual NIC interfaces are also supported (firmware v3.7.6+). |
| Client Address Pool | The IP range to assign, e.g. `192.168.33.1–192.168.33.252`. Must be on the same subnet as the LAN interface IP. |
| Excluded Addresses | Specific IPs within the pool to skip (never assign). Requires firmware v3.7.6+. |
| Subnet Mask | Must match the subnet mask of the corresponding LAN interface. |
| Gateway | The LAN port's IP address. For extended IPs, use the extended IP as gateway. For VLAN pools, use the VLAN IP as gateway. |
| Primary DNS | Preferred DNS server for assigned clients. |
| Secondary DNS | Fallback DNS server when primary cannot resolve. |
| Remaining Addresses | Number of IPs still available to assign. |
| Lease Time | How long (in minutes) a client holds its IP before renewal is required. Default: **120 minutes** (2 hours). |
| Expired Address Hold Time | How long after lease expiry before the IP is reclaimed. Set to `0` to reclaim immediately. |
| Validate Interface IP | Checks that the DHCP gateway is on the same subnet as the LAN IP. Disable this for Layer-3 relay environments. |
| DHCP Relay Only | This policy only acts as a DHCP relay; it does not directly assign IPs to LAN clients. |
| Associated Interface | When a LAN port bridges multiple physical NICs, bind the DHCP pool to a specific physical interface. |
| Custom DHCP Options | Supports option43, option60, option66, option67 (v3.5.2+), option80, option119, option125, option128, option138, option121 (v3.7.6+). |

> **Notes:**
> - The DHCP address pool must be on the **same subnet** as the LAN interface.
> - If both the LAN IP and its extended IP have DHCP pools, the primary LAN pool is allocated first; the extended IP pool fills in afterward.
> - Changing the LAN subnet automatically updates the DHCP pool (firmware v3.7.7+).
> - Firmware v3.7.11 enables DHCP by default on all router LAN ports.

---

## III. Setup Steps

1. Click **Add** in the top-right corner.
2. Fill in the address pool, subnet mask, gateway, primary/secondary DNS. Leave the lease time at default.
3. Click **Confirm**, then **Restart Service**.

> **Important:** The DHCP pool must be on the same subnet as the LAN interface. The gateway must point to the LAN IP address.

---

## IV. Example

- LAN2: IP `192.168.222.1`, mask `255.255.255.0`
- VLAN1: IP `192.168.119.1`, mask `255.255.255.0`

![DHCP Example](https://www.ikuai8.com/images/support_202109/dhcp333.png)

---

## V. Common Issues

### DHCP service won't start

1. No DHCP pool has been added for the corresponding LAN or VLAN port — add one first.
2. Configuration was saved but the green checkmark was not clicked to apply.
3. The address pool range does not match the LAN port's subnet (e.g. LAN1 is `192.168.15.x` but pool is `192.168.16.x`).
4. The LAN port exists in the config but has no NIC bound or no IP address assigned.

### DHCP service shows "Inactive"

1. The address pool was valid when created, but the LAN IP was later changed to a different subnet — pool and LAN are now mismatched.
2. The LAN port the pool referenced has been deleted or unbound.

### Too many LAN devices — running out of IPs

Three solutions:

1. **Expand the subnet mask** — A `/24` mask supports 254 devices. Changing to `/23` (mask `255.255.254.0`) supports 510. Use the **Subnet Calculator** under Application Tools.
2. **Add VLANs** — Use a VLAN-capable switch to segment devices into separate subnets.
3. **Add extended IPs** on the LAN port — Create a second DHCP pool for the extended IP range. Note: primary LAN pool IPs are assigned first; extended pool IPs are assigned after.
