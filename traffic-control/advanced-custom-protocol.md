# Advanced Custom Protocol (高级自定义协议)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/lkfl/rqfq/gdfgw.html

## I. Overview

Advanced Custom Protocol lets you capture packets, identify protocol signatures manually, and add them to the router — resolving cases where protocols are misidentified or not recognized at all.

Import/Export is supported: export a configuration from one router and import it into another to avoid re-entering signatures by hand.

---

## II. Configuration

![Advanced Custom Protocol List](https://www.ikuai8.com/images/support/gjzdy.png)

![Advanced Custom Protocol Add](https://www.ikuai8.com/attached/php/upload/image/20170919/1505794929681326.png)

**Signature fields:**

| Field | Description |
|---|---|
| Protocol | `TCP` or `UDP` — the transport protocol of the captured flow. |
| Direction | `CLIENT` (packets sent from the client) or `SERVER` (packets sent from the server). Red = client, blue = server in Wireshark. |
| PacketSeq | The packet sequence number where the signature appears (1-based). Maximum detectable packet index is 7. Can be left blank. |
| Dstport | The destination port(s) on the server. Separate multiple ports with a comma (`,`). |
| Data | The protocol signature string extracted from the captured flow. |
| Len | Signature length. Optional — can be left blank. |

> **Important:** Protocol values must be entered in **uppercase** (e.g., `TCP`, `UDP`).

---

## III. Example — Adding Huya Video Protocol

**Step 1 — Capture packets**

In the router web UI, go to **Application Tools → Packet Capture**. Start a capture while Huya video is running in the background. Download the capture file and open it in Wireshark.

![Packet Capture Tool](https://www.ikuai8.com/images/support/zbgj1.png)

In Wireshark: select a relevant packet → right-click → **Follow Stream** → select the stream type to analyze.

![Wireshark Step 1](https://www.ikuai8.com/images/support/wireshark1.png)

![Wireshark Step 2](https://www.ikuai8.com/images/support/wireshark2.png)

![Wireshark Step 3](https://www.ikuai8.com/images/support/wireshark3.png)

**Step 2 — Add the custom protocol**

Go to **Traffic Control → Custom Protocol → Advanced Custom Protocol**.

- **Protocol Category:** Select the category that best matches what you captured (e.g., video).
- **Protocol Name:** Name it descriptively (e.g., `Huya-Video`).

![Add Custom Protocol](https://www.ikuai8.com/images/support/gjzdyxy1.png)

Fill in the signature fields based on what you extracted from the Wireshark stream view.

![Signature Fields](https://www.ikuai8.com/images/support/gjzdyxy2.png)

**Step 3 — Apply the custom protocol**

Once added, the custom protocol appears in **Protocol Routing** and **Traffic Control** rule editors. Search for the protocol name directly, or find it under its protocol category → **Custom** file.

![Apply Custom Protocol](https://www.ikuai8.com/images/support/yyxykz11.png)

> **Note:** Custom protocols are prefixed with `U-` in the protocol selector to distinguish them from built-in protocols.
