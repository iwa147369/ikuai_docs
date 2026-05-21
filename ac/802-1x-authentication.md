# 802.1x Authentication

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ac/802-1x.html

## I. Overview

This guide explains how to configure 802.1X security authentication using a third-party RADIUS server. The example below uses FreeRADIUS on Ubuntu.

**Requirements:**

| AP Models | Minimum AP Firmware |
|---|---|
| X2, X3, W6, W6+ | v1.6.5+ |
| H11, H13, H15, H17, X2, X3, DX3, SW2, W5, S3 | v1.6.6+ |

Router version must be **3.5.4 or higher**.

The RADIUS server and the access points must be able to **communicate bidirectionally**.

---

## II. Configuration Steps

### Step 1 — Install FreeRADIUS

```bash
sudo apt-get install -y freeradius
```

### Step 2 — Configure the RADIUS Server

Edit `/etc/freeradius/3.0/clients.conf` to allow AP access:

- Set `ipv4addr = *` to accept connections from any IP, or specify a restricted IP range.
- Add client credentials including the IP range and a shared secret.

### Step 3 — Add User Accounts

Edit `/etc/freeradius/3.0/users` and add the username and password for each endpoint user that should authenticate via 802.1X.

### Step 4 — Enable and Restart the Service

```bash
sudo systemctl enable freeradius
sudo systemctl restart freeradius
```

### Step 5 — Configure the Router

In the AC Management interface:

1. Open the target SSID's security settings.
2. Set **Security Type** to **802.1X**.
3. Enter the RADIUS server IP address.
4. Enter the authentication port (default: `1812`).
5. Enter the shared secret configured in `clients.conf`.

---

## III. Client Connection

Wireless clients connect to the SSID and are prompted to enter credentials. Authentication succeeds when the username and password match those configured on the RADIUS server.
