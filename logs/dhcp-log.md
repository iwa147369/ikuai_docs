# DHCP Log (DHCP日志)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzzx/gegge.html

## I. Overview

Records IP address allocation events by the DHCP server, including requests from LAN devices.

> **Note:** DHCP logs only appear when the DHCP service is enabled. If DHCP is disabled, this log will be empty.

![DHCP Log](https://www.ikuai8.com/images/dhcp12.jpg)

---

## II. DHCP Protocol Background

The DHCP address assignment process:

1. **Discovery:** The client broadcasts a DHCP Discovery packet (source: `0.0.0.0`, destination: `255.255.255.255`) to find available DHCP servers. All DHCP servers on the network respond.

2. **Offer:** Each responding DHCP server selects an available IP from its pool (performs a ping conflict check first), then sends a DHCP Offer containing the proposed IP and lease options.

3. **Request:** The client broadcasts a DHCP Request accepting one of the offers. All other DHCP servers see this broadcast and withdraw their offers.

4. **Acknowledgment:** The selected DHCP server sends a DHCP ACK confirming the lease. The client begins using the assigned IP.

**IP selection priority (iKuai DHCP server):**
1. Existing IP–MAC binding in the table.
2. The client's previously assigned IP.
3. The IP requested in the Discovery packet (if available).
4. An IP from the configured subnet pool.

---

## III. Log Retention

Max entries: **20,000**. See [System Log](xtrz.md) for the full retention table.
