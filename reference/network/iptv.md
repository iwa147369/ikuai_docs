# IPTV Pass-through

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/iptv.html

## I. Overview

IPTV Pass-through allows IPTV signals to pass through the router transparently to TV set-top boxes, without excessive protocol conversion. This enables **single-line multiplexing** — delivering both internet and IPTV service over one network cable.

---

## II. Pass-through Types

| Type | Description |
|---|---|
| Network Port Pass-through | An unbound LAN port receives VLAN-tagged IPTV data from the WAN port; the TV box connects directly to that port |
| VLAN Pass-through | A specified VLAN ID is forwarded transparently to the internal network; the TV connects via a VLAN-capable switch or AP |

---

## III. Supported Topologies

- **Topology 1:** Optical Modem → Router → TV
- **Topology 2:** Optical Modem → POE Router → AP → TV

---

## IV. Configuration Example

**Optical Modem:** Unbind VLAN 101/102 from default ports, then rebind to LAN1 using VLAN binding mode with IDs 101 and 102.

**Router:**
1. Select pass-through mode (Network Port or VLAN).
2. Configure the WAN port, VLAN ID, and the corresponding LAN port.
3. The TV receives IPTV service; other connected devices maintain normal internet access.
