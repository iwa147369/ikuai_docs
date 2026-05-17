# Application Protocol Control (应用协议控制)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/behavior-control/17b6e.html

## I. Overview

Controls client internet access by allowing or blocking specific application protocols. Supports two modes:

- **Professional Mode:** The original application protocol control — configure rules directly in the router's web interface.
- **Parental Control Mode:** Configure through the iKuai E-Cloud App. The router page shows the current configuration in read-only mode. Only supported on official iKuai hardware.

---

## II. Field Reference

![Application Protocol Control](https://www.ikuai8.com/images/support/yyxykz.png)

| Field               | Description                                                                                                  |
| ------------------- | ------------------------------------------------------------------------------------------------------------ |
| Protocol            | The application protocol to allow or block (e.g., HTTP, HTTPS, QQ, P2P).                                     |
| Action              | **Allow** or **Block**.                                                                                      |
| Source Address      | The LAN IP range to apply this rule to.                                                                      |
| Destination Address | Usually left blank (matches all destinations).                                                               |
| Schedule            | The recurrence for this rule (daily, weekly, etc.).                                                          |
| Effective Time      | The specific time window during which this rule is active.                                                   |
| Priority            | Rule priority from 0 (highest) to 63 (lowest). When rules conflict, higher priority rules take effect first. |

**Important:** When using Allow rules, you must also add a rule to **allow DNS** — otherwise clients cannot resolve domain names and will be unable to access the internet even when other protocols are allowed.

---

## III. Usage Examples

1. **Block a client from accessing web pages:** Source: `192.168.15.100`, Protocol: HTTP/HTTPS, Action: Block.
2. **Allow only email while blocking everything else:** Block all protocols for the IP, then add Allow rules for SMTP/POP3/IMAP.
