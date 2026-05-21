# Wireless Terminal VLAN

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ac/vlan.html

## I. Overview

Wireless Terminal VLAN allows specific wireless clients to obtain IP addresses from a designated VLAN network segment based on the SSID they connect to and their MAC address.

**Requirements:** AP firmware version 2.2.0 or higher.

---

## II. Configuration Steps

### Step 1 — Configure VLAN Network Segment

1. Create the VLAN (e.g., VLAN6) and set its gateway (e.g., `192.168.10.1`).
2. Configure a DHCP pool for the VLAN so clients can automatically receive IPs from that segment.

### Step 2 — Configure Wireless Terminal VLAN Rule

Each rule requires three parameters:

| Field | Description |
|---|---|
| VLAN ID | The VLAN to assign the terminal to (e.g., VLAN6) |
| Terminal MAC | The actual hardware MAC address of the device (do not use a randomized MAC) |
| SSID | The wireless network the rule applies to |

### Step 3 — Configure the Switch

Ports connecting the router and APs must be set as **trunk ports** that allow traffic from all relevant VLANs.

Example using an S5018 switch:

1. Add VLAN6 in VLAN membership settings.
2. Set the port connecting to the router as a trunk port; allow VLAN1 and VLAN6.
3. Set the port connecting to the AP as a trunk port; allow VLAN1 and VLAN6.

---

## III. Result

When the configured terminal connects to the specified SSID, it receives an IP address from the designated VLAN segment.

---

## IV. Limitations

- Wireless Terminal VLAN requires AP firmware **v2.2.0 or higher**.
- If **SSID VLAN** is enabled on the same SSID, the Wireless Terminal VLAN feature is **disabled** for that SSID.
- The terminal MAC address field must use the device's real hardware MAC — randomized MACs will not match.
