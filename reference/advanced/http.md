# HTTP Service (HTTP服务)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/2019-12-13-06-35-05/http.html

## I. Overview

iKuai can serve static files over HTTP or HTTPS from a local disk partition. Useful for hosting files or a simple web server on the LAN. WAN access supported from firmware v3.7.6+.

---

## II. Setup

### Step 1 — Create a storage partition
Go to **System Settings → Disk Management → Disk Partition**. Create a partition and bind it to **General Storage** with a mount path.

### Step 2 — Create a directory and upload files
In **System Settings → Disk Management → File Management**, create a folder and upload files to it.

### Step 3 — Configure HTTP service
Go to **Advanced Applications → HTTP Service** and click **Add**.

---

## III. Field Reference

| Field | Description |
|---|---|
| File Directory | Path to the directory containing files to serve. Copy the path from File Management. |
| Access Method | **HTTP** or **HTTPS**. |
| Server Port | Must not conflict with the router's web management port or other services. Ports 80 and 443 are commonly blocked by ISPs for WAN access. |
| Service Domain | (Optional) If specified, the rule applies only to requests for this domain. If blank, applies to all domains. |
| Directory Browsing | Enable to allow listing directory contents. Disable to prevent browsing. |
| Download Speed | Limit the download rate (0 = unlimited). |
| Allow WAN Access | Enable external internet access (firmware v3.7.6+). |

---

## IV. Accessing the HTTP Server

In a browser, enter: `http://192.168.1.1:<port>/filename`

For HTTPS: `https://192.168.1.1:<port>`

---

## V. Notes

- Files must be uploaded **after** the HTTP service is configured.
- The HTTP port must not conflict with the router's own management port.
- Ports 80 and 443 are commonly blocked by ISPs — WAN access on these ports may not work.
- IPv6 access supported from firmware v3.7.10+.
