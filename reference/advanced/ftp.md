# FTP Service (FTP服务)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/2019-12-13-06-35-05/ftp.html

## I. Overview

iKuai can host an FTP server for file transfer within the LAN or over the internet (WAN access supported from firmware v3.7.6+). Files are stored on a disk partition configured as **General Storage**.

---

## II. Setup

### Step 1 — Create a storage partition
Go to **System Settings → Disk Management → Disk Partition**. Create a partition and bind it to **General Storage**. Set a mount path (e.g., `/data`).

### Step 2 — Create a directory
In **System Settings → Disk Management → File Management**, open the mounted partition and create a folder for FTP storage.

### Step 3 — Configure FTP service
Go to **Advanced Applications → FTP Service**, enable the service, and click **Add**.

---

## III. Field Reference

| Field | Description |
|---|---|
| Username / Password | Credentials for this FTP account. For anonymous access, username must be `anonymous`; password can be anything. |
| Permission | **Read-only** or **Read/Write**. |
| FTP Directory | The path to the storage folder. Find the path in File Management and copy it. |
| Upload Speed | Limit the upload rate for this account (0 = unlimited). |
| Download Speed | Limit the download rate for this account. |
| Server Port | Default: **21**. If changed, clients must specify the custom port when connecting. |
| Allow WAN Access | Enable external access to the FTP server (firmware v3.7.6+). |

---

## IV. Accessing the FTP Server

**Upload files:** Either use File Management on the router web UI to upload to the mounted partition, or connect via an FTP client and copy files in.

**Download files (browser):** Enter `ftp://192.168.1.1` in the browser address bar, then log in with the FTP account credentials.

**Download files (file browser):** Open the system file explorer, navigate to `ftp://192.168.1.1`, and copy files locally.

---

## V. Notes

- Files must be uploaded **after** the FTP service is configured.
- Anonymous user's username must be exactly `anonymous`.
- If the server port is changed, always include the port in the connection address.
- IPv6 access supported from firmware v3.7.10+.
