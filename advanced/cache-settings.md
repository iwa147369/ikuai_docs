# Cache Settings (缓存设置)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/2019-12-13-06-35-05/19e77.html

## I. Overview

Caches video and application data locally on an attached storage device. When other clients access the same content, it is served from the local cache instead of re-fetching from the internet, saving WAN bandwidth.

Supported platforms: USB storage (U disk or external hard drive, must be formatted as **EXT** format).

Currently supported content: **Youku, Tencent Video, Tudou** (web, app, and desktop client — unencrypted content only).

---

## II. Configuration

### Disk Status
After attaching a disk, you can format it, view capacity and status, and clear the cache.

### Video Cache
Check **Cache Switch** to enable.

### Application Cache
Check **Cache Switch** to enable.

### Cache Settings

| Field | Description |
|---|---|
| Cache Size | Space allocated for caching (integers only, no decimals). Calculate as: total disk capacity − 243 MB − 1 GB (the 1 GB is reserved for Linux system swap). |
| Inactive Cache Time | How long unmatched (uncached-again) content stays on disk. Default: **2880 minutes**. |
| Minimum Access Threshold | How many times a resource must be accessed before it starts being cached. Default: **1** (recommended). Lower = more caching; higher = fewer cache entries but less resource usage. |

### Line Settings
- Set upload/download bandwidth limits for caching traffic per WAN line (0 = unlimited).
- When multiple lines are enabled, set a **weight ratio** — higher weight = higher probability of using that line for cache fetches.
- Line states: **Enabled**, **Disabled**, **Invalid**.
- If no line is enabled, cache traffic goes through the default gateway.
- The cache line takes priority over traffic control load-balancing rules for cached protocols.

---

## III. Notes

1. Minimum hard disk size: **4 GB** for video cache.
2. Recommended RAM: **4 GB or more**. Minimum usable RAM after recognition: **2800 MB**.
3. iKuai caches by domain name only — accessing video sites by IP address cannot be cached.
4. If the configured cache size is smaller than the disk (e.g., 10 GB cache on a 30 GB disk), overflow content is stored in a temp directory using the remaining free space. The temp directory holds at most **100 files**.
5. Encrypted content from Tencent Video, Youku, and Tudou cannot be cached.
6. Setting a high threshold consumes more system resources (disk I/O, RAM) and may slow performance.
