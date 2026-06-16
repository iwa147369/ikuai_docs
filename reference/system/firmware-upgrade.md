# Firmware Upgrade (版本升级)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/1d4fe.html

## I. Overview

Upgrade or downgrade the iKuai router's firmware version and signature library versions.

---

## II. Configuration

### Firmware Version Upgrade

Upload a firmware package and click **Upgrade** to apply it. Click **Check for New Version** to see if a newer firmware is available online.

![Firmware Upgrade](https://www.ikuai8.com/images/support_202109/bbsj.png)

**Notes:**
1. The router reboots during an upgrade. After uploading the package, you can choose **Restart Now** or **Restart Later** — if postponing, restart the router manually at a convenient time.
2. File extension: 2.X firmware uses `.patch`; 3.X firmware uses `.bin`.
3. Downgrading uses the same process — upload an older firmware package and apply it.
4. Enterprise and free editions **cannot** be upgraded to each other.

**Online upgrade notes:**
- Requires a stable internet connection. If the connection is unstable, use a local package instead.
- Official hardware can also be upgraded through the iKuai Cloud platform or by checking for new versions online.

![Online Version Check](https://www.ikuai8.com/images/lyxtbb.jpg)

---

### Protocol Signature Library

![Protocol Library](https://www.ikuai8.com/images/support_202109/xykbb.jpg)

Shows the currently running protocol signature library version. Upgrading this library **does not cause a router reboot or network interruption** — new connections and protocols immediately use the updated signatures.

### Communication Tool Signature Library

![Communication Tool Library](https://www.ikuai8.com/images/support_202109/txgjtzjbb.jpg)

Supports the behavior logging feature under **Behavior Control → Behavior Control Settings → Behavior Log Settings**.

### Website Signature Library

![Website Library](https://www.ikuai8.com/images/support_202109/wzkbb.jpg)

Supports the **Block Entertainment Websites** feature under Behavior Control.

### Auto-Update Settings

![Auto-Update](https://www.ikuai8.com/images/support_202109/tzkzdsj.jpg)

**Signature Library Auto-Update:** When enabled, signature libraries are updated automatically when new versions are released. The router does not reboot during updates.

![Security Policy Auto-Update](https://www.ikuai8.com/images/support_202109/aqclzdsj.jpg)

**Security Policy Auto-Update:** When enabled, security policies are updated automatically. No reboot required.
