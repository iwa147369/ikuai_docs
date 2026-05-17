# Dynamic DNS (动态域名)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/2019-12-13-06-35-05/60588.html

## I. Overview

Dynamic DNS (DDNS) binds a fixed domain name to a dynamically changing WAN IP address. Even when the ISP-assigned IP changes, external users can reach your services using the same domain name.

---

## II. Supported Providers

| Provider | Notes |
|---|---|
| Oray (花生壳) | `http://www.oray.com/` |
| 3322 | `http://www.pubyun.com/` |
| DNSPod | `https://www.dnspod.cn/` |
| Aliyun (阿里云) | `https://www.aliyun.com/` |
| Huawei Cloud | Supported from firmware v3.4.5+ |
| Cloudflare | `https://dash.cloudflare.com` |

iKuai supports wildcard (pan-domain) resolution for DNSPod and Aliyun.

---

## III. Field Reference

| Field | Description |
|---|---|
| Provider | Select the DDNS provider. |
| Domain | The domain registered with the provider. Must have an **A record** created — without it, DNS resolution will fail. |
| Account / Password | Credentials for the DDNS provider. Some providers use an ID + secret key instead of account + password. |
| Resolved IP Type | **Interface IP** — uses the WAN port's IP. **Internet Exit IP** — uses the public/NAT IP. Firmware v3.7.0+ required for Internet Exit IP. |
