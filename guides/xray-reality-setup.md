# Guide: Resilient Personal Censorship-Circumvention Setup — Xray (VLESS + REALITY) on Ubuntu 20.04
**Document Type:** Setup Guide
**Version:** 1.0
**Last Updated:** June 2026
**Audience:** Personal use — your own devices only

---

## Scope & Intent

This guide builds a personal circumvention setup so **your own devices** (under 10: 2× Android,
iPhone primary/secondary, tablet, laptop) can reach the open internet (Google, Facebook, etc.)
from inside a censored network, using TLS-camouflaged transport that resists DPI and active probing.

**This is "Version A" — IP *resilience*, not source-IP spoofing.** "Rotation" here means: when one
exit node's IP gets blocked, you fail over to a healthy one to keep *your own* access alive. It is
**not** about presenting many rotating source IPs to a third-party platform to make sessions look
like different users. All exit nodes are servers you control, located **outside** the censored network.

---

## Table of Contents
1. [Overview & Threat Model](#1-overview--threat-model)
2. [Prerequisites](#2-prerequisites)
3. [Architecture](#3-architecture)
4. [Server Setup — Manual Config (Per Node)](#4-server-setup--manual-config-per-node)
5. [Web-Based Management Panels (3X-UI & Marzban)](#5-web-based-management-panels-3x-ui--marzban)
6. [Multi-Node Failover (2–3 Nodes)](#6-multi-node-failover-23-nodes)
7. [Client Setup](#7-client-setup)
8. [Verification](#8-verification)
9. [Maintenance & "IP Burned" Runbook](#9-maintenance--ip-burned-runbook)
10. [Additional: Domain Name Setup](#10-additional-domain-name-setup)
11. [Operational Notes](#11-operational-notes)

---

## 1. Overview & Threat Model

### What this protects against
- **Protocol fingerprinting (DPI):** REALITY makes your traffic look like genuine TLS 1.3 to a real
  website, so there is no "VPN signature" to match.
- **Active probing:** If the firewall probes your server, REALITY borrows a real site's certificate
  and behaves like that site, so the server does not reveal itself as a proxy.
- **SNI blocking:** You present the name of a large, allowed site in the TLS handshake.
- **IP blocklisting:** Multi-node failover (Section 6) lets you switch to a fresh IP when one is burned.

### What it does *not* fully hide
- **Flow metadata** — volume, timing, and duration of the connection to your server IP. The firewall
  cannot read content, but a long, high-throughput flow to a single foreign IP is statistically visible.
  At national scale this is expensive to act on and produces heavy false positives (normal video/cloud
  traffic looks the same), so it is not the primary blocking mechanism for ordinary users. It matters
  mainly for **targeted surveillance of a specific high-value individual** — a different threat model
  than personal access. Mitigations: split-tunnel (Section 7) so only blocked sites use the tunnel,
  and avoid running a single 24/7 max-throughput stream through it if you want to stay quiet.

**Bottom line:** For "a normal person who wants Google/Facebook on their own <10 devices," REALITY plus
IP failover is more than sufficient. No tool offers 100% unobservability.

---

## 2. Prerequisites

| Item | Notes |
|---|---|
| **VPS outside the censored network** | 2–3 small instances. Low-latency regions: Tokyo, Singapore, Korea. Avoid providers based inside the censored country (they sit behind the same firewall). |
| **OS** | Ubuntu 20.04 LTS on each node. |
| **SSH access** | Key-based login recommended (Section 4.1). |
| **A domain name** | Strongly recommended for smooth failover (Section 10). |
| **Client apps** | v2rayNG (Android), Shadowrocket or sing-box (iOS), v2rayN (Windows), sing-box (macOS). |

> Do **not** use a VPS provider located inside the censored country — its egress is censored too,
> so it cannot serve as a free-internet exit.

---

## 3. Architecture

```
   Your devices (inside censored network)
        |
        |  [TLS-camouflaged VLESS + REALITY]
        v
   +--------- firewall / DPI ---------+   <- you cross this once
        |
        v
   node.yourdomain.com  --> DNS points to a HEALTHY node
        |
   +----+----+----------+
   |         |          |
  Node A    Node B    Node C        <- 2–3 exit VPS, identical config, outside censored network
 (Tokyo)  (Singapore) (Korea)
   |         |          |
   +----+----+----------+
        |
        v
   Open internet (Google, Facebook, ...)
```

- Clients connect via a **subscription** listing all nodes, with client-side health-check/url-test.
- Optionally, a **domain** (`node.yourdomain.com`) is repointed via DNS when a node is blocked.

---

## 4. Server Setup — Manual Config (Per Node)

> **Two ways to run a node:** this section (manual `config.json`) or a **web panel** (Section 5).
> Pick one per node — don't run both managing the same Xray instance. The manual route has zero extra
> attack surface; the panel route is easier to operate day-to-day. You can even mix (e.g., a panel on
> your primary, manual on a backup), since clients only care about the resulting share-link.

Repeat this section identically on **every** node so all nodes share the same config and keys.

### 4.1 Initial hardening
```bash
# As root on a fresh Ubuntu 20.04 box
adduser admin
usermod -aG sudo admin

# Copy your SSH public key for the admin user, then test login before disabling root.
# Edit /etc/ssh/sshd_config:  PermitRootLogin no   and   PasswordAuthentication no
systemctl restart ssh

# Basic firewall: allow SSH + 443 only
ufw allow OpenSSH
ufw allow 443/tcp
ufw enable

# Optional: brute-force protection for SSH
apt update && apt install -y fail2ban
systemctl enable --now fail2ban
```

### 4.2 Install Xray-core
```bash
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```

### 4.3 Generate keys and IDs
```bash
# REALITY key pair (note BOTH the Private key and Public key)
xray x25519

# A UUID for the client
xray uuid

# A short ID (keep it; clients need the same value)
openssl rand -hex 8
```
Record:
- `PRIVATE_KEY` (server) / `PUBLIC_KEY` (clients)
- `UUID`
- `SHORT_ID`

### 4.4 Server config
Pick a real, popular "borrow" target that is reachable and not blocked. `www.microsoft.com` is a common,
stable choice. Write `/usr/local/etc/xray/config.json`:

```json
{
  "log": { "loglevel": "warning" },
  "inbounds": [
    {
      "listen": "0.0.0.0",
      "port": 443,
      "protocol": "vless",
      "settings": {
        "clients": [
          { "id": "UUID", "flow": "xtls-rprx-vision" }
        ],
        "decryption": "none"
      },
      "streamSettings": {
        "network": "tcp",
        "security": "reality",
        "realitySettings": {
          "show": false,
          "dest": "www.microsoft.com:443",
          "xver": 0,
          "serverNames": ["www.microsoft.com"],
          "privateKey": "PRIVATE_KEY",
          "shortIds": ["SHORT_ID"]
        }
      },
      "sniffing": { "enabled": true, "destOverride": ["http", "tls", "quic"] }
    }
  ],
  "outbounds": [
    { "protocol": "freedom", "tag": "direct" }
  ]
}
```

Replace `UUID`, `PRIVATE_KEY`, `SHORT_ID`, and the two `www.microsoft.com` values consistently, then:
```bash
systemctl enable --now xray
systemctl restart xray
systemctl status xray --no-pager
```

> Use the **same** UUID / SHORT_ID across all nodes, but each node has its **own** REALITY key pair OR
> a shared one — sharing keys simplifies the subscription. For a small personal setup, reusing the same
> `PRIVATE_KEY`/`PUBLIC_KEY`, `UUID`, and `SHORT_ID` on every node is the easiest to manage; only the
> server IP/hostname differs per node.

---

## 5. Web-Based Management Panels (3X-UI & Marzban)

If you'd rather manage clients, keys, share-links/QR codes, and traffic stats from a browser instead of
hand-editing `config.json`, use a panel. Two approaches are covered: **3X-UI** (one panel per node,
decentralized) and **Marzban** (one central panel for the whole node pool). Both fully support
VLESS + REALITY. Use **one or the other**, not both, on a given setup.

> **Security first — a panel is an admin dashboard exposed on your server.** Before anything else:
> - Set a **strong, unique** admin password and **change the default panel path/port**.
> - Do **not** leave the panel open to the whole internet. Best practice: bind it to `127.0.0.1` and
>   reach it over an **SSH tunnel** (`ssh -L 2053:127.0.0.1:2053 admin@node`), or restrict the panel
>   port in `ufw` to your own IP only.
> - Keep the panel and Xray updated. A stale panel is the most common way these servers get popped.

### 5.1 Option A — 3X-UI (one panel per node, decentralized)

Best when you want each VPS fully independent with no central server to depend on. You log into each
node's own panel and copy its share-link into your clients.

**Install (on each node):**
```bash
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```
The installer walks you through setting the admin user, password, panel port, and web base path.

**Configure a VLESS + REALITY inbound:**
1. Log into `http(s)://<node>:<panel-port>/<web-base-path>` (ideally via SSH tunnel — see the security box).
2. **Inbounds → Add Inbound.**
3. Protocol: **VLESS**; Port: **443**; Flow: **xtls-rprx-vision**.
4. Security: **REALITY**. Click to **auto-generate** the key pair and short ID.
5. Set **Dest/SNI** to a real borrow target (e.g., `www.microsoft.com:443` / `www.microsoft.com`).
6. Add a client (it generates the UUID). Save.
7. Use the inbound's **QR code / share-link** for your devices (Section 7).

Repeat on each node. To keep the subscription simple, you can paste the **same** REALITY key pair, UUID,
and short ID into each node's inbound so only the IP/host differs (matching the manual-config note in 4.4).

> 3X-UI also has a built-in **subscription** feature: enable it to publish one URL listing a client's
> inbounds. With a panel per node, the central **Marzban** approach (5.2) handles multi-node subscriptions
> more cleanly — but per-node subscription links work too.

### 5.2 Option B — Marzban (one central panel for all nodes)

Best for your **2–3 node failover** goal: one dashboard manages every user and node, and each user gets a
**single subscription URL that already includes all nodes** — which pairs directly with the client-side
health-check failover in Section 6.1.

**Architecture:** Marzban's main panel runs on one host (can be one of your VPS or a separate small box);
each exit node runs a lightweight **`marzban-node`** agent that the panel controls.

**Install the main panel:**
```bash
sudo bash -c "$(curl -sL https://github.com/Gozargah/Marzban-scripts/raw/master/marzban.sh)" @ install
```
Then create the admin account:
```bash
marzban cli admin create --sudo
```
Log into the dashboard (default `:8000` — put it behind the SSH tunnel / firewall as above) and:
1. **Host Settings / Core:** add a **VLESS + REALITY** inbound (generate keys/short ID, set the borrow SNI).
2. **Nodes:** add each exit node; install `marzban-node` on that VPS per the panel's instructions and
   connect it. The panel pushes the Xray config to every node.
3. **Users:** create a user — Marzban issues one **subscription link** spanning all connected nodes.

**Attach an exit node (run on each exit VPS):**
```bash
sudo bash -c "$(curl -sL https://github.com/Gozargah/Marzban-scripts/raw/master/marzban-node.sh)" @ install
```
Then register it from the panel's **Nodes** page (paste the node's certificate/connection details).

With Marzban, "adding a fresh node after one is burned" (Section 9 runbook) becomes: spin up the VPS,
install `marzban-node`, attach it in the panel — every user's existing subscription picks it up automatically.

### 5.3 Which to choose

| | 3X-UI | Marzban |
|---|---|---|
| Topology | One panel **per node** | **One central** panel + node agents |
| Best for | Full independence, no central dependency | Your **multi-node failover**, single subscription |
| Subscription across all nodes | Manual (combine per-node links) | **Automatic**, built-in |
| Single point of failure | None (each node standalone) | The central panel (keep it well-secured & backed up) |
| Effort to add/replace a node | Configure the new node's panel | Install agent + attach in panel |

For your setup, **Marzban** is the smoother match; choose **3X-UI** if you prefer each node fully
standalone. Either way, the **manual config (Section 4)** remains a valid fallback and a good way to
understand what the panel generates under the hood.

---

## 6. Multi-Node Failover (2–3 Nodes)

The goal: keep working when one node's IP is blocked. Two complementary mechanisms — use either or both.

### 5.1 Client-side health-check (recommended, simplest)
Build a **subscription** containing all node share-links (Section 7.1). Modern clients (v2rayNG,
sing-box, Shadowrocket) support **url-test / automatic** mode: the app periodically tests each node and
routes through the fastest reachable one. When a node is blocked, the app silently switches. No DNS, no
server changes — this alone gives you working failover across 2–3 nodes.

### 5.2 DNS-based switching (optional, via your domain)
Point `node.yourdomain.com` at your current primary node with a **low TTL** (e.g., 60s). If it gets
blocked, repoint the DNS record to a healthy node — every client follows automatically without re-import.
See Section 10 for the domain setup.

### 5.3 Fast re-provision (when you run low on healthy nodes)
Keep a provider **snapshot/image** of a fully configured node so a fresh IP is a few minutes away:
1. Spin up a new VPS from the snapshot (new IP, same config).
2. Add its share-link to your subscription (or repoint DNS).
3. Retire the blocked node.

Start with **2 nodes** for real failover; **3** gives breathing room if two get burned close together.

---

## 7. Client Setup

### 6.1 Build the share-link(s)
For each node, the VLESS + REALITY link is:
```
vless://UUID@SERVER_IP_OR_HOST:443?encryption=none&flow=xtls-rprx-vision&security=reality&sni=www.microsoft.com&fp=chrome&pbk=PUBLIC_KEY&sid=SHORT_ID&type=tcp&headerType=none#NodeName
```
Make one per node (`#NodeA-Tokyo`, `#NodeB-Singapore`, …). Replace `UUID`, `SERVER_IP_OR_HOST`,
`PUBLIC_KEY`, `SHORT_ID`.

### 6.2 Per-platform import

| Platform | App | Steps |
|---|---|---|
| **Android** (both phones) | **v2rayNG** | `+` → *Import config from clipboard* (paste each link). Group nodes, set mode to **url-test/auto** for failover. |
| **iOS** (both phones) | **Shadowrocket** or **sing-box** | Paste links / add subscription. Set policy to automatic/url-test. |
| **Windows** (laptop) | **v2rayN** | Servers → *Import from clipboard*; enable auto-test/round-robin. |
| **macOS** (laptop) | **sing-box** | Add the same nodes via config/subscription; enable url-test. |
| **Tablet** | Same as its OS (Android/iOS) | As above. |

### 6.3 Split-tunnel routing (recommended)
Route only blocked/foreign destinations through the tunnel; let domestic traffic go direct. This is faster
and reduces the metadata footprint discussed in Section 1. All four clients support a geosite/geoip rule
set — enable the bundled "bypass mainland / direct domestic" routing preset and set the default outbound
to the proxy.

---

## 8. Verification

```bash
# On a client device, after connecting:
# 1. Confirm exit IP belongs to your node (not your real ISP)
#    Visit an "what is my IP" page; it should show the node's region.

# 2. DNS-leak test
#    Use a DNS-leak test site; resolvers should NOT be your local ISP's.

# 3. Failover test
#    On the primary node, stop xray:  systemctl stop xray
#    Within ~30–60s the client should switch to the next node automatically.
#    Restart it afterwards:  systemctl start xray
```
Also confirm Google/Facebook load normally and that a **kill-switch** (if your client offers one) blocks
traffic when no node is reachable, so nothing leaks outside the tunnel.

---

## 9. Maintenance & "IP Burned" Runbook

**Symptom:** One node suddenly stops connecting while others still work → that IP is likely blocked.

1. **Confirm:** From a client, the node fails health-check while others pass. From elsewhere outside the
   censored network the node still responds (so it's a block, not an outage).
2. **Fail over:** Client auto-switches (5.1). If using DNS (5.2), repoint `node.yourdomain.com` to a
   healthy node.
3. **Replace:** Spin up a fresh node from your snapshot (5.3), add its link / update DNS.
4. **Retire:** Remove the burned node from the subscription. Optionally destroy the VPS to stop billing.

**Routine upkeep:**
- `apt update && apt upgrade` on each node periodically.
- Re-run the Xray installer to update: `bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install`
- Keep at least one spare/healthy node in reserve.

---

## 10. Additional: Domain Name Setup

A domain is optional but makes failover and node replacement far smoother — clients connect to a name,
and you change where it points instead of re-importing configs on every device.

### 9.1 What you need
- A registered domain (any registrar).
- Access to its DNS records (the registrar's panel, or a DNS provider like Cloudflare).

### 9.2 Create the node record
Add an **A record** pointing a subdomain at your current primary node:

| Type | Name | Value | TTL |
|---|---|---|---|
| A | `node` | `<primary node IP>` | 60 (low, for fast switching) |

Your clients then use `node.yourdomain.com` instead of a raw IP in the share-link (Section 7.1).

### 9.3 Switching nodes via DNS
When a node is blocked, edit the A record's value to a healthy node's IP. Because TTL is low, clients pick
up the change within ~1 minute — no per-device reconfiguration.

### 9.4 Notes on REALITY + domains
- The **`serverNames` / `sni`** in REALITY is the **borrowed** site (e.g., `www.microsoft.com`) — it is
  *not* your domain and does not need to match it. Your domain is only the connection address.
- If using **Cloudflare**, keep the `node` record **DNS-only (grey cloud)** — do **not** proxy it
  (orange cloud), because REALITY needs a direct TCP connection to your server, not Cloudflare's.
- You can keep separate records per node (`a.yourdomain.com`, `b.yourdomain.com`, …) and list all of them
  in the subscription, combining domain addressing with client-side health-check (5.1).

---

## 11. Operational Notes

- **Keep IPs clean:** prefer reputable providers; freshly allocated IPs with no abuse history last longer.
- **Stay low-profile:** split-tunnel, don't run constant max-throughput streams through a single node.
- **One borrow target, sane choice:** use a large, stable, reachable site for `dest`/`serverNames`.
- **Personal scope only:** this setup is for your own devices' access to the open internet. It is not
  designed for, and should not be used for, evading a third-party platform's abuse/fraud detection.
- **Back up** your `config.json`, keys, UUID, and short ID somewhere safe — losing them means rebuilding.
```
