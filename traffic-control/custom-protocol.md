# Custom Protocol

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/rqfq.html

## I. Overview

Custom Protocol allows administrators to define their own traffic classification rules for use in traffic control policies. It requires knowledge of the target traffic's destination ports or source IP and port information.

> For more complex matching requirements, see [Advanced Custom Protocol](advanced-custom-protocol.md).

---

## II. Configuration Fields

| Field | Description |
|---|---|
| Protocol Name | User-defined name for this custom protocol |
| Source Address | Source IP or network to match |
| Destination Address | Destination IP or network to match |
| Protocol Type | TCP, UDP, or other |
| Port Number | Destination port number to match |

---

## III. Example

To classify traffic where source `1.1.1.1` accesses destination `2.2.2.2` on TCP port 80 as "Custom Web Protocol":

- **Protocol Name:** Custom Web Protocol
- **Source Address:** 1.1.1.1
- **Destination Address:** 2.2.2.2
- **Protocol Type:** TCP
- **Port:** 80
