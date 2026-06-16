# Kernel Settings

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/2020-07-31-07-00-43/2021-12-22-04-55-12.html

## I. Overview

Kernel settings control TCP/UDP timeout parameters and performance options that affect network connection behavior at the system level.

> Do not modify kernel parameters without a specific reason. Incorrect values can destabilize the system or degrade network performance.

---

## II. TCP Parameters

| Parameter | Description |
|---|---|
| TCP Syn Sent Timeout | Duration for TCP connection requests to time out |
| TCP Syn Received Timeout | Wait time after receiving a SYN before expecting an ACK |
| TCP Established Timeout | Idle timeout for established TCP connections |
| TCP Fin Wait Timeout | Timeout when sending FIN to close a connection |
| TCP Close Wait Timeout | Duration waiting for connection closure |
| TCP Last Ack Timeout | Passive closure timeout |
| TCP Time Wait | Duration in TIME_WAIT state after receiving FIN |
| TCP Close | Connection closure duration |

---

## III. UDP Parameters

| Parameter | Description |
|---|---|
| UDP Timeout | General UDP session timeout |
| UDP Stream Timeout | Timeout for UDP stream connections |

---

## IV. Performance Control

| Option | Description |
|---|---|
| TCP BBR | Toggle the BBR congestion control algorithm on or off |
