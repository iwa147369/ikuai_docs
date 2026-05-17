# Wake on LAN (网络唤醒)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/2019-12-13-06-35-05/11d27.html

## I. Overview

Remotely power on LAN devices using Wake-on-LAN (WoL) magic packets. Requires ATX power supply and motherboard BIOS/software support.

---

## II. Usage

### Immediate Wake
Enter the target device's MAC address and click **Wake**.

### Scheduled Wake
Click **Add Scheduled Wake** to create a timed wake rule.

---

## III. Field Reference

| Field | Description |
|---|---|
| MAC | 12-character MAC address in colon-separated format (e.g., `AA:BB:CC:DD:EE:FF`). |
| Wake | Click to send the WoL magic packet immediately. |
| Cycle | Recurrence period for scheduled wake (daily, weekly, etc.). |
| Date | Specific date for the wake event (e.g., `2017-09-14`). |
| Time | Time of day for the wake event (e.g., `00:00`). |
| Remark | Label for this entry. If blank, the remark is pulled from Terminal Name Management. If the MAC already exists in Terminal Name Management, update the remark there. |

---

## IV. Notes

- The status in the Wake on LAN list refreshes every **5 seconds** (asynchronous — only the table updates, not the full page).
- An invalid MAC address triggers an error popup: "Input MAC is incorrect!"
