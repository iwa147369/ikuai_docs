# Subnet Calculator (子网换算)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/yygj/983fb.html

## I. Overview

Calculate the usable IP range and host capacity for a given IP address and subnet mask.

---

## II. How to Use

| Field | Description |
|---|---|
| IP Format | Choose **IP address** (single host) or **IP subnet** (a range). |
| IP / Subnet | Enter the IP address or subnet, along with the prefix length (the number of 1-bits in the mask). |

**Default prefix lengths:**
- Class A (0.0.0.0 – 127.255.255.255): `/8` (mask: 255.0.0.0)
- Class B (128.0.0.0 – 191.255.255.255): `/16` (mask: 255.255.0.0)
- Class C (192.0.0.0 – 223.255.255.255): `/24` (mask: 255.255.255.0)

---

## III. Subnet Mask Reference

A subnet mask is a 32-bit number where a leading sequence of 1s defines the network portion and trailing 0s define the host portion.

| Mask | Binary | Max Hosts |
|---|---|---|
| 255.255.255.0 `/24` | 24 ones + 8 zeros | 254 |
| 255.255.254.0 `/23` | 23 ones + 9 zeros | 510 |
| 255.255.252.0 `/22` | 22 ones + 10 zeros | 1,022 |
| 255.255.248.0 `/21` | 21 ones + 11 zeros | 2,046 |
| 255.255.0.0 `/16` | 16 ones + 16 zeros | 65,534 |
| 255.0.0.0 `/8` | 8 ones + 24 zeros | ~16.7 million |

*Usable hosts = 2^(host bits) − 2 (subtract network and broadcast addresses)*

**Example:** A company has 530 computers. Class B IPs are needed. Minimum prefix: `/22` gives 1,022 hosts (2^10 = 1024 − 2). Mask: `255.255.252.0`.
