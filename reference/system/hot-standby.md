# Dual-Machine Hot Standby

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/2019-05-13-07-25-35.html

## I. Overview

Dual-Machine Hot Standby enables automatic failover between two iKuai gateways. When the active gateway goes offline, the standby gateway takes over all traffic within seconds — no manual intervention required.

---

## II. Supported Topologies

- **Multi-line environment** — Multiple WAN connections with dual-gateway protection
- **Single-line environment** — Single external connection with a backup gateway

---

## III. Operating Modes

| Mode | Behavior |
|---|---|
| Master-Backup | One device handles all traffic; the other activates only on failure |
| Load-Sharing | Both devices operate simultaneously and share traffic |

---

## IV. Configuration Fields

### Heartbeat Link

| Field | Description |
|---|---|
| Device Name | Local and remote router identifiers |
| Heartbeat Interface | The interface used for heartbeat communication |
| Interface IP | IP of the heartbeat interface (`--` if abnormal) |
| Status | Normal or Abnormal |

### Master-Backup Status

| Field | Description |
|---|---|
| Work Mode | Must match on both devices |
| Priority | Higher priority = active device. If equal, the device with the larger heartbeat IP becomes master |

### Hot Standby Settings

| Field | Description |
|---|---|
| External Network Detection | Recommended enabled; pings a target IP/domain to confirm WAN reachability |
| Detection Cycle | 1–30 seconds; failover triggers after 3 consecutive failures |
| Heartbeat Interface | Physical interface for heartbeat traffic |
| Remote IP | Remote device's heartbeat IP (same subnet, different address) |
| Virtual Gateway | A shared unused IP on the same subnet; **must be identical on both devices** |

---

## V. Configuration Example (Multi-line)

| Device | LAN1 | LAN2 (Heartbeat) |
|---|---|---|
| Router A | Virtual GW: 188.188.188.1 | 10.10.10.2 |
| Router B | Virtual GW: 188.188.188.1 | 10.10.10.1 |

Both devices must use the **same virtual gateway address** on the transmission link.

---

## VI. Important Notes

1. Firmware versions must match on both devices.
2. Both routers must be configured with the same hot standby mode.
3. The backup device's DHCP service is disabled while in standby.
4. Transmission link virtual gateways must be identical on both ends.
5. Failover takes approximately **6 seconds** after 3 failed detection cycles.
6. A single interface cannot serve as both heartbeat and transmission link.
7. Layer 2 connectivity is required between the two routers.
8. Maximum 32 virtual gateway entries supported.
9. Version compatibility: Enterprise ↔ Enterprise; Free ↔ Free only.
10. Web authentication sessions remain active during failover; PPPoE users must re-dial.
11. DHCP pools must use the virtual gateway address as their gateway.
