# RAID Management

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/2019-12-13-02-14-28/raid.html

## I. Overview

RAID (Redundant Array of Independent Disks) combines multiple drives into a single logical disk group to increase capacity, improve performance, or add redundancy.

---

## II. RAID Types

| Type | Description |
|---|---|
| RAID 0 | Stripes data across drives to increase read/write speed and total capacity. If any drive fails, all data is lost. |
| RAID 1 | Mirrors data across drives so data is preserved if one drive fails. Best used with drives of identical capacity. |

---

## III. Configuration

**Required fields:**

- **Disk Members** — Select the drives to include in the array
- **RAID Type** — RAID 0 or RAID 1
- **Format Disk** — Format the selected drives before creating the array

**Limits:**

- Minimum 2 drives required
- Maximum 26 RAID arrays supported
- For RAID 1, matching drive capacities are recommended

---

## IV. After Creation

1. The system generates a virtual disk: `rda` (RAID 0) or `rdb` (RAID 1).
2. Use the **Quick Partition** feature to partition the virtual disk.
3. Bind the partition to a business type:
   - Standard storage
   - Behavior logging
   - Cache acceleration
   - File transfer
   - Other
4. Access and manage files through **Disk Management → File Management**.
