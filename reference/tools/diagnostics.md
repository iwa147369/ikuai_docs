# Router Diagnostics (路由体检)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/yygj/7a28c.html

## I. Overview

Runs automated diagnostics to check:
- Disk and memory health
- WAN line connectivity
- Whether other DHCP servers exist on the LAN
- Whether other PPPoE servers exist on the LAN
- Whether ARP conflicts exist on the LAN

---

## II. How to Use

![Router Diagnostics](https://www.ikuai8.com/images/support/lytj.png)

Click **Quick Scan** to start the diagnostics. Click **Stop** to abort.

> **Note:** Line detection currently does not cover IPSec or OpenVPN connections.

---

## III. Common Issues

### `/dev/sda3` and `/dev/sda5` are both in read-only mode

Try reinstalling the system. If the issue persists after reinstalling, replace the hard drive.

### `/dev/sda5` is in read-only mode or partition not found

For official iKuai hardware: return for warranty service. For non-official (DIY) setups: reformat the disk or replace the disk and reinstall the system.

### DHCP detection shows an anomaly

Another DHCP server is present on the LAN — typically a consumer router with its LAN port connected to the same switch as iKuai's LAN port. Find that device and disable its DHCP function.

### Gateway conflict detected

A device on the LAN has an IP address that conflicts with iKuai's LAN interface address. Resolve by either changing iKuai's LAN IP, or changing the conflicting device's IP.
