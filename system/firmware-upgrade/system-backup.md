# System Backup (系统备份)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/1d4fe/xtbf.html

## I. Overview

Back up the router's configuration to a file, or restore a previous backup.

---

## II. Configuration

| Action | Description |
|---|---|
| Export Current Config | Exports the current configuration to a local file. This file can later be uploaded to restore the configuration. |
| Latest Backup Time | Shows the timestamp of the most recent backup. |
| Upload Backup | Upload a previously exported backup file to the router. |
| Backup Current Config | Saves the current configuration as a backup entry. **Backs up configuration only — not the firmware version.** |
| Restore Default Settings | Restores all configuration to defaults, but **retains** data such as logs and browsing history. |
| Factory Reset | Restores all configuration to defaults **and clears all data**. |

### Restore from Backup — Two Methods

**Method 1: Upload a backup file**
1. Click **Choose File** and select the backup file saved on your computer.
2. Confirm the upload — the file appears in the backup list.
3. Click **Restore**, confirm, and restart the router.

**Method 2: Restore from a listed backup**
Click the **Restore** button next to an existing backup entry in the list.

---

## III. Important Notes

1. Backup files can be downloaded to your computer via the Download button.
2. Reinstalling the system clears all disk data — download backup files locally before reinstalling.
3. System backups take effect only after restarting the router.
4. After uploading a backup file, it does not restore immediately — it appears in the backup list. Click Restore and then restart to apply it.
5. **Different hardware:** After restoring a backup to different hardware, all NIC bindings must be reconfigured.

### NIC Import Behavior

When importing a backup to a different device, NIC mapping no longer checks MAC addresses — it maps by port order (smallest to largest). If the two devices have different port counts, only the interface (WAN/LAN) configuration is imported for ports that have no corresponding NIC.

| Platform | Port 1 | Port 2 | Port 3 | Port 4 | ... |
|---|---|---|---|---|---|
| x86 | eth0 | eth1 | eth2 | eth3 | ethX |
| ARM | veth1 | veth2 | veth3 | veth4 | vethX |

### Cloud Binding Import

When restoring a backup, a dialog offers the option to **sync cloud platform binding info**:
- If the device is **already bound** to iKuai Cloud before restoring: checking this option will **not** change the existing cloud binding.
- If the device is **not yet bound**: checking this option and entering a cloud alias will cause the device to automatically bind to the cloud after it connects to the internet.

> **Note:** If a cloud alias is entered during import, the system hostname (**System Settings → Basic Settings → Device Name**) is also updated to match, regardless of whether cloud binding succeeds.

Backup file name length limit: **64 characters**.
