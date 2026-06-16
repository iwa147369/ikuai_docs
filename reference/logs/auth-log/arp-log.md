# ARP Log (ARP日志)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/rzzx/fe4g/arp.html

## I. Overview

Records ARP attack events detected by the router.

![ARP Log](https://www.ikuai8.com/images/support/arp.png)

---

## II. ARP Attack Types

**1. Simple spoofing attack**
Sends forged ARP packets to deceive the router and target hosts. The attacker makes itself appear as a legitimate host. Common within the same subnet.

**2. Sniffing in a switched environment**
By combining ARP spoofing with a man-in-the-middle position, the attacker intercepts traffic between two hosts.

**3. MAC flooding**
Floods the switch's ARP table to overflow it, disrupting normal communication across the network.

**4. ARP-based DoS**
Sends massive connection requests using ARP to hide the attacker's real IP. The attacked host becomes overwhelmed and cannot serve legitimate users.

---

## III. Defense Methods

1. **IP + MAC access control:** Trust relationships built on both IP and MAC together are more secure than IP alone.
2. **Static ARP cache:** Manually set static ARP entries (`arp -s IP MAC`) so forged ARP packets cannot overwrite the binding. Note: static entries are lost on reboot.
3. **ARP cache timeout:** Shorten the timeout to reduce the window for ARP table overflow attacks.
4. **Proactive monitoring:** Record correct IP–MAC mappings at a known-good time and regularly compare against current state.

---

## IV. Log Retention

Max entries: **20,000**. See [System Log](../system-log.md) for the full retention table.
