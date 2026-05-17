# System Log (系统日志)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzzx/xtrz.html

## I. Overview

Records system operation events, including: firmware upgrades, system start/shutdown, WAN line detection results, network loop detection, interface detection, and system process monitoring.

![System Log](https://www.ikuai8.com/images/support/xt.png)

---

## II. Log Entry Reference

### System Startup

Appears when the router has restarted or was previously shut down and has now started up again.

### Line Detection Success / Failure

Line detection checks each WAN line (including VPN dial connections) by pinging its gateway and `114.114.114.114` via ICMP. A "line detection failure" is only logged when **both** targets are unreachable or experiencing severe packet loss.

**Q: Is it normal to see "line detection failure" followed 1 minute later by "line detection success"?**
Yes. Detection runs every 30 seconds. When a failure occurs, only the first failure and the eventual recovery are logged — intermediate failed checks are suppressed. The gap between failure and success will always be a multiple of 30 seconds.

### Loop Detection

When a loop is detected on a LAN or WAN interface, the system logs it. Check the corresponding interface for a network loop.

**Loop detection logic:** If an interface receives a packet whose source MAC is the interface's own MAC, it is flagged as a loop.

**Common loop causes:**
1. Both ends of one cable plugged into the same switch (different ports).
2. Two ports on one switch connected to two ports on another switch, forming a ring.
3. Faulty NIC or cable connector.

**Resolution:**
- WAN loop: Replace the NIC or have the ISP check the upstream network.
- LAN loop: Unplug devices one by one to isolate the source, or configure STP on the switch.

### Interface Detection

Logged when a physical interface disconnects. Check for loose RJ45 connectors, intermittent port contacts, or cables being manually unplugged.

### System Process Restart

A system process crashed and was automatically restarted to maintain normal operation.

---

## III. Log Retention

Logs in the Log Center are retained by entry count (circular buffer):

| Log Type | Max Entries |
|---|---|
| System Log | 5,000 |
| Auth Log (PPPoE) | 5,000 |
| ARP Log | 20,000 |
| Auth Log | 20,000 |
| DHCP Log | 20,000 |
| Dynamic DNS Log | 5,000 |
| Operation Log | 5,000 |
| WAN Dial Log | 5,000 |
| Push Notification Log | 500 |
| Wireless Terminal Log | 10,000 |
| Alert Info | 20,000 |
