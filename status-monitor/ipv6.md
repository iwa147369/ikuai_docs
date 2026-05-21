# IPv6 Terminal Monitoring

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ztjk/7cf09/ipv6.html

## I. Overview

The IPv6 page displays real-time connection information for IPv6 hosts on the internal network, similar to the IPv4 monitoring page.

---

## II. Connection Fields

| Field | Description |
|---|---|
| Protocol Name | Protocol type used for the target connection |
| Route | External network path used |
| External Address | Router WAN address during the connection |
| Source Port | Local port number used by the client |
| Destination Address | Target IP being accessed |
| Destination Port | Port on the target being reached |
| Traffic | Cumulative upload and download data |
| Connection Status | Current link state |

---

## III. Connection States

| State | Meaning |
|---|---|
| Connected | TCP three-way handshake completed |
| Stateless | No connection (UDP shows as `--`) |
| Waiting | TCP request sent, awaiting response |
| Closed | Four-way handshake complete, connection terminated |

---

## IV. Filter Options

- **Protocol type** — Filter by TCP, UDP, ICMPv6, or all
- **Network line/route** — Filter by WAN line
