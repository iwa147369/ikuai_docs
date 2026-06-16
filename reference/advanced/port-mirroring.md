# Port Mirroring (端口镜像)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/2019-12-13-06-35-05/5871a.html

## I. Overview

Forwards all traffic from one or more source ports to a designated destination port for monitoring or analysis. The destination port is called the **mirror port**; the source ports are the **mirrored ports**.

Use cases: network monitoring, traffic analysis, fault diagnosis.

---

## II. Field Reference

| Field | Description |
|---|---|
| Bidirectional Traffic | Mirror both inbound and outbound traffic from the mirrored port. |
| Mirror Port | The destination port — receives a copy of traffic from the mirrored port. |
| Mirrored Port | The source port — its traffic is copied to the mirror port. |

---

## III. Example

Mirror LAN1 to WAN1:
- **Mirrored Port:** LAN1
- **Mirror Port:** WAN1

All traffic on LAN1 (in and out) is duplicated and forwarded to WAN1.

---

## IV. Notes

The mirror port must handle at least as much throughput as the mirrored port — and potentially more (since it receives both directions). Ensure the mirror port has sufficient bandwidth.
