# ALG Settings

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/2020-07-31-07-00-43.html

## I. Overview

ALG (Application Layer Gateway) is a firewall component that inspects and processes application-layer packet payloads. Unlike standard NAT which only rewrites IP addresses and ports in packet headers, ALG handles special protocols where the data payload itself contains IP or port information that must also be translated.

---

## II. Supported Protocols

| Protocol | Description |
|---|---|
| FTP ALG | Application layer gateway for File Transfer Protocol |
| TFTP ALG | Application layer gateway for Trivial File Transfer Protocol |
| SIP ALG | Application layer gateway for Session Initiation Protocol (VoIP) |
| H323 ALG | Application layer gateway for H.323 multimedia communications |

Enable a protocol by checking its corresponding checkbox.

---

## III. Advanced Port Configuration

For FTP, TFTP, and SIP, you can configure **non-standard ports** in addition to the default ports. Enter up to 7 custom ports, separated by commas.

This advanced port option is available in firmware version **3.7.11 and later**.
