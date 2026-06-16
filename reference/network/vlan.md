# VLAN Settings

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/vlan.html

## I. Overview

VLAN (Virtual Local Area Network) logically segments LAN devices into separate network groups using software, rather than separate physical hardware. VLAN support is available on Layer-2 and above managed switches.

**VLAN Termination:** When a device receives a tagged frame, it strips the VLAN tag(s) and then performs Layer-3 forwarding or other processing. The tags are only meaningful before termination — the subsequent forwarding does not rely on them.

---

## II. Configuration

### Prerequisites

To use VLAN settings:
1. You need a **VLAN-capable managed switch**.
2. If using iKuai APs, configure AP SSID VLAN on the AP side.

### iKuai Router VLAN Setup (Layer-2 Switch)

When connecting iKuai to a Layer-2 VLAN switch, configure the following on the router:

1. Create the VLAN and assign a virtual IP address.
2. **IP Address** — This becomes the default gateway for all clients in that VLAN.
3. **VLAN Name** — Must follow the format `VLAN` + number (e.g. `VLAN2`, `VLAN10`).

![VLAN Settings](https://www.ikuai8.com/images/support/vlansz.png)

The VLAN ID configured here must match the VLAN ID on the switch. Connect the router's **LAN port** directly to the switch's **trunk port**.

> **Notes:**
> - The VLAN IDs on iKuai must match those configured on the switch.
> - If the switch has a management IP address, ensure it does not conflict with VLAN IPs.
> - Do not add the VLAN subnet to the LAN port's extended IP — it is not needed.

### Example: Cisco 2960 Layer-2 Switch Configuration

```
Switch(config)#vlan 2
Switch(config-vlan)#exit
Switch(config)#vlan 3
Switch(config-vlan)#exit
Switch(config)#interface fastEthernet 0/2
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan2      ! assign port to VLAN2
Switch(config-if)#exit
Switch(config)#interface fastEthernet 0/3
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan3      ! assign port to VLAN3
Switch(config-if)#exit
Switch(config)#interface fastEthernet 0/24     ! trunk port to iKuai
Switch(config-if)#switchport mode trunk
Switch(config-if)#switchport trunk allowed vlan 2,3,4
```

---

### Layer-3 Switch Configuration

When using a Layer-3 (multilayer) switch with routing enabled, **do not configure VLANs on iKuai**. Instead:

- Configure static routes on both the Layer-3 switch and iKuai pointing toward each other's subnets.
- On iKuai, add a static route for the subnets behind the switch. In the static route, **do not select "Auto" for the line** — select the specific LAN port the switch is connected to.

Example Layer-3 switch config:

```
R1(config)#vlan 2
R1(config)#exit
R1(config)#interface fastEthernet 1/0
R1(config-if)#switchport mode access
R1(config-if)#switchport access vlan 2
R1(config-if)#exit
R1(config)#int vlan 2
R1(config-if)#ip add 172.16.100.1 255.255.255.0   ! VLAN gateway IP
R1(config-if)#exit
R1(config)#interface fastEthernet 0/0
R1(config)#no switchport                           ! enable routed interface
R1(config)#no shutdown
R1(config-if)#ip address 172.16.1.2 255.255.255.0  ! interface toward iKuai
R1(config-if)#exit
R1(config)#ip route 0.0.0.0 0.0.0.0 fastEthernet 0/0  ! default route to iKuai
```

---

### Extended IP on VLANs

VLAN settings support extended IPs, allowing multiple virtual gateway addresses under the same VLAN. Clients in the same VLAN can obtain IPs from different subnets.

![VLAN Extended IP](https://www.ikuai8.com/images/vlan800.jpg)

---

## III. Common Issues

### Layer-3 switch configured — VLAN clients can't reach iKuai

1. **If the switch is used as Layer-2:** Configure VLAN and trunk on the switch; connect trunk port to iKuai LAN; configure matching VLAN IDs on iKuai's VLAN settings page.

2. **If the switch is used as Layer-3:** Do not configure VLANs on iKuai. Instead, add static routes on iKuai pointing to the switch's subnets. When configuring the static route, **select the specific LAN port** (not "Auto") that the switch is connected to.

### Does iKuai VLAN support QinQ?

Yes, iKuai VLAN supports QinQ (double-tagged VLAN). See the QinQ configuration guide for details.
