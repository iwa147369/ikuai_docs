# AP Groups

**Source:** https://www.ikuai8.com/support/ymgn/lyym/ac/213.html

## I. Overview

Create AP groups to apply a shared configuration to multiple APs simultaneously. Any AP added to a group uses the group's configuration.

---

## II. How to Use

Click **Add** to create a new group and open the group configuration page.

![AP Group Config](https://www.ikuai8.com/images/support_202109/apfzgjdq1.png)

| Field | Description |
|---|---|
| Force Group Config | When enabled, individual AP overrides within the group are ignored — all APs in the group strictly use the group configuration. When disabled, individual AP overrides are respected. |
| Country/Region | Sets the channel and frequency regulations for all APs in this group. Supported: China, Taiwan, USA. Default: China. Requires AP firmware v2.3.0+. |

> **Note:** When an AP joins a group, it adopts the group's configuration. When it leaves the group, it reverts to its configuration from before joining. Individual settings applied while in the group are not restored after leaving.
