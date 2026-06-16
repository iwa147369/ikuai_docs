# iKuai Cloud Binding (爱快云绑定)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/c542c.html

## I. Overview

Bind this iKuai router to the iKuai Cloud platform for centralized management and web authentication.

Three binding methods are supported: **verification code**, **QR code**, and **binding code**.

---

## II. Configuration

### Method 1 — Binding Code

1. Register an account at the iKuai Cloud platform (https://yun.ikuai8.com).

   ![Cloud Registration](https://www.ikuai8.com/images/121ed2323123edr.png)

   Click "Register Account" and fill in the required information.

   ![Register Form](https://www.ikuai8.com/images/121ed2323123edr1.png)

2. Log in to the cloud platform. The binding code is displayed on the dashboard.

   ![Binding Code](https://www.ikuai8.com/images/121ed2323123edr2.png)

   Copy the binding code. On the router, select **Binding Code** as the method, paste the code, set a device alias, and save.

   ![Router Binding](https://www.ikuai8.com/images/bdm.png)

   ![Cloud Binding Settings](https://www.ikuai8.com/images/support_202109/yunbd.png)

3. After binding, the router appears in the cloud platform's device list.

   ![Cloud Device List](https://www.ikuai8.com/images/support_202109/wlxj.png)

### Method 2 — Verification Code (Phone Number)

1. On the router, select **Verification Code** as the binding method.

   ![Verification Code](https://www.ikuai8.com/images/yzm.png)

   Enter your phone number and click "Get Verification Code."

   > **Note:** If the phone number is not yet registered on the cloud platform, it will be automatically registered.

2. Enter the account credentials, verification code, and device alias, then save.

   ![Verification Save](https://www.ikuai8.com/images/support_202109/wx10.png)

   After saving, a **service code** is available on this page for contacting iKuai technical support.

   > **Version requirements for service code:**
   > - Router firmware: v3.6.6+
   > - iKuai E-Cloud App: v4.2.3+
   > - iKuai Cloud website: no version restriction (2.X can obtain a code but cannot use it for remote debugging — upgrade to 3.X for full functionality)

3. If this phone number was not previously registered, log into the cloud platform using SMS authentication.

   ![SMS Login](https://www.ikuai8.com/images/121ed2323123edr6.png)

4. Set a password for the account via **Profile → Account Security**.

   ![Account Security](https://www.ikuai8.com/images/121ed2323123edr7.png)

### Method 3 — QR Code

1. Select **QR Code** as the binding method.

   ![QR Code](https://www.ikuai8.com/images/121ed2323123edr9.png)

   > **Note:** The QR code is valid for **120 seconds**. Generate a new one if it expires.

2. Scan the QR code using the iKuai E-Cloud App. Set a device alias and save.

   ![QR Scan](https://www.ikuai8.com/images/121ed2323123edr10.png)

---

## III. Common Issues

### "Local network error"

**Cause:**
1. The WAN port is not configured, or the configured WAN port cannot reach the internet.
2. DNS is misconfigured — the router cannot resolve domain names.

**Fix:**
1. Check and configure the WAN port so it can communicate with the internet.
2. Set a valid, working DNS server address.

### "Unknown error" or "This username does not exist"

**Cause:** Browser compatibility issue.

**Fix:** Use Google Chrome. Other browsers may have compatibility problems that will be resolved in future updates.

### Display errors or loading failures

Ensure the router has a stable internet connection and the DNS server is reachable.
