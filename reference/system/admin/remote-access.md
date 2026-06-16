# Remote Access (远程访问)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/bea01/51e30.html

## I. Overview

Configure remote login to the router via web browser or Telnet. Also provides technical support report export.

---

## II. Configuration

### Access Control

| Field                  | Description                                                                                                                                                                                                                |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Telnet Server          | When enabled, you can log in to the router's console interface via Telnet — the same menu-driven interface shown on an attached monitor.                                                                                   |
| Force HTTPS Web Access | When enabled, the web management interface must be accessed using HTTPS (e.g., `https://192.168.9.1`).                                                                                                                     |
| HTTP Access Port       | The port used for HTTP access to the web interface. Default: 80.                                                                                                                                                           |
| HTTPS Access Port      | The port used for HTTPS access to the web interface.                                                                                                                                                                       |
| WAN Web Access Control | When enabled, the web interface can be accessed from the WAN (internet). Access is via the router's public WAN IP plus the configured port. IPv4 and IPv6 access can be independently allowed (requires firmware v3.7.6+). |

**Port access examples** (using the default management IP `192.168.9.1`):
- Default port 80: access via `192.168.9.1` (port 80 is the default HTTP port and can be omitted).
- Changed to port 880: access via `http://192.168.9.1:880`.
- WAN access: `<public-IP-or-DDNS>:<port>`.

> **Note:** The colon (`:`) in the address must be typed in **English/half-width** mode.

### Custom SSL Certificate

Upload your own SSL certificate for the web management interface instead of the self-signed certificate. This improves security and eliminates browser certificate warnings.

| Field | Description |
|---|---|
| Custom SSL Certificate | Enable/disable the custom certificate feature. |
| Certificate (CRT) | Paste the contents of the SSL certificate file (text format). |
| Private Key (KEY) | Paste the contents of the SSL private key file (text format). |
| Remarks | An optional label — typically the domain name this certificate covers. |

*Example flow using Tencent Cloud:*
1. Log in to Tencent Cloud → Domains & Websites → SSL Certificates.
2. Purchase or apply for a free SSL certificate, then download it.
3. Extract the archive and select the **Nginx** server certificate files.
4. Paste the `.crt` file content into the Certificate field and the `.key` file into the Private Key field.

> **Note:** If the router uses a dynamic public IP, pair this feature with the router's **Dynamic DNS** feature.

### Remote Maintenance

This channel is reserved for iKuai developers only — it is not available to users. It is disabled by default. Enable it only when an iKuai developer explicitly requests access to backend data.

### Technical Support Report

When the internal network behaves abnormally (e.g., router reboots, NIC packet loss), export a technical support report for diagnostic purposes.

---

## III. Common Issues

### Technical support report exported via cloud remote control cannot be opened

When exporting a report through iKuai Cloud's remote management, the downloaded file **has no file extension**. Manually add the `.gz` extension to open it.
