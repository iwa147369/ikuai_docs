# Mesh Quick Connect

**Source:** https://www.ikuai8.com/support/ymgn/lyym/wlsz/mesh.html

## I. Overview

Mesh Quick Connect creates a mesh network using multiple iKuai router nodes that interconnect to extend wireless coverage. It supports both wired and wireless mesh configurations.

**Requirements:** Enterprise firmware version 3.7.12+. Slave devices must have factory default configuration restored before pairing.

**Supported models:** IK-Q3000, IK-Q6000, IK-Q3S, IK-Q90, IK-Q1800, IK-Q1800L, IK-Q85

---

## II. Wired Mesh

**Topology:** Master device (e.g., Q6000) connects to the slave device's (e.g., Q3000) WAN port via LAN cable.

**Steps:**

1. Connect devices per topology diagram.
2. Go to **Network Settings → Mesh Quick Connect** and enable the feature.
3. Verify LED indicators, then click **Start Pairing**.
4. Monitor pairing progress (Q6000: alternating red/green; Q3000: multicolor flashing).
5. Pairing is complete when Q6000 shows steady green and Q3000 shows pink.
6. Stop pairing after the MAC address scan completes.
7. Configure wireless names and test connectivity.

> Mesh slave devices bind to the master's **LAN1** interface by default. If LAN1 has no DHCP service, mesh nodes cannot auto-acquire IP addresses.

---

## III. Wireless Mesh

Same pairing process as wired mesh, but the master connects to the external network without physical cables to slaves. Slaves use the **Mesh button** (press 3× if no lights appear) to enter pairing mode.

---

## IV. Topology Restrictions

- Maximum **4-level hierarchy** including the master router.
- Only **linear chain** topologies are supported.
- Secondary nodes must not connect directly to non-master devices — this creates a loop.
  - Fix: Set the preferred upstream device to the master router.

---

## V. Common Issues

**Q: Why can't the Q6000's 2.5G port function as a wireless mesh node?**

The system automatically selects between wireless and wired mesh based on WAN port detection. When operating as a wireless mesh node, the 2.5G port is reserved for wired mesh. Use the three standard gigabit LAN ports instead.
