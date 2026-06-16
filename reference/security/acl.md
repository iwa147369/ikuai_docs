# ACL Rules (ACL规则)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/aqsz/acl.html

## I. Overview

An Access Control List (ACL) is a set of rules on a router interface that controls inbound and outbound traffic. ACL rules can filter traffic, restrict or allow specific devices, and force traffic through specific ports or WAN lines.

---

## II. Field Reference

![ACL Rule](https://www.ikuai8.com/images/aclgz222.jpg)

| Field | Description |
|---|---|
| Protocol Stack | IPv4 or IPv6. Requires firmware v3.7.0+. |
| Protocol | The protocol type this rule applies to (e.g., TCP, UDP, ICMP, Any). |
| Action | **Allow** or **Block**. |
| Direction | **In** — traffic entering the router from LAN or WAN. **Forward** — traffic the router receives and forwards onward. |
| Original Direction | Match packets from the initiating side (the client sending the request). |
| Reply Direction | Match packets from the responding side (the server replying). |
| Source Address | Starting address for the rule. Supports IPv6 MAC groups (v3.7.7+). For IPv6 MAC addresses: block-access rules work; allow-access rules currently do not. |
| Destination Address | Ending address. Supports IPv6 MAC groups (v3.7.7+). Can be left blank to match all destinations. |
| IPv6 Suffix Match | For IPv6 addresses, specify a fixed suffix to prevent the rule from breaking when the device gets a new IPv6 prefix. Example: `240e:1234:xxxx:xxxx:xxxx:AAAA/::AAAA` matches any prefix + `:AAAA` suffix. |
| Source Port | The source port to match. Optional. |
| Destination Port | The destination port to match. Optional. Protocol must be specified to add ports. |
| Ingress Interface | The interface traffic comes in from. |
| Egress Interface | The interface traffic goes out through. |

> **Important:** Traffic between devices on the **same subnet** does not pass through the router and is **not subject to ACL rules**.

> **Priority:** When rules conflict, **Allow** has higher priority than **Block**.

### IP Geolocation (IP归属地)

Source and destination addresses can be filtered by geographic region (city/province). To use this feature, bind the device to iKuai Cloud and activate it through the iKuai App.

**Notes:**
- IPv6 addresses do not support geolocation filtering.
- Source and destination cannot both be set to geographic regions simultaneously.

---

## III. Usage Examples

### Block a specific LAN IP from accessing a specific port

Block `192.168.15.2` from accessing port 80:
- Source Address: `192.168.15.2`
- Protocol: TCP
- Destination Port: 80
- Action: Block

### Block a specific LAN IP from accessing the internet

- Source Address: `192.168.15.2`
- Protocol: Any
- Action: Block, Direction: Forward

### Force a LAN IP to use a specific WAN line

Combine with Port Routing (set the IP to use WAN2 via port routing), then add an ACL rule to block that IP from using WAN1.

### Block traffic between LAN and extended IP subnets

- LAN: `192.168.200.0/24` | Extended IP: `192.167.200.0/24`
- Source Address: one subnet, Destination Address: the other

### Block all clients except a specific IP from accessing the internet

1. First rule — Block all: Source: LAN subnet, Action: Block
2. Second rule — Allow specific IP: Source: `192.168.200.101`, Action: Allow

### Allow only some IPs to access the internal network

1. Block all IPs from accessing the router's LAN IP range.
2. Allow specific IP(s) to access the LAN IP range.

### Block a LAN IP from the internet, except one specific external IP

1. Block `10.0.0.2` from accessing the internet.
2. Allow `10.0.0.2` to access `192.168.50.100`.
