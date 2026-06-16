# Disk Management (磁盘管理)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/2019-12-13-02-14-28.html

## I. Overview

Partition the system disk or attached external disks and assign each partition to a specific service type. This prevents different services from competing for unmanaged disk space and reduces interference between functions.

---

## II. Disk Partition Parameters

### Partition Table

| Column | Description |
|---|---|
| Disk | Physical disk identifier and total capacity. |
| Mount Path | The mount point name set when binding a service — similar to a drive letter in Windows. |
| Partition Name | Partition identifier (e.g., `sda1` = first partition of disk `sda`). |
| Partition Type | Primary partition, logical partition, or unformatted. |
| Partition Size | Partition capacity (auto unit conversion). |
| Bound Service | Fixed partitions (system config and system log) are highlighted in yellow and cannot be changed. Custom partitions can be bound to: **General Storage**, **Youyu Fanshu**, **Video Cache**, **Behavior Log**, or **DingTalk Flash Transfer**. |

### Quick Partition

| Setting | Description |
|---|---|
| Select Disk | Choose which disk to partition. Up to 26 disks supported. |
| Partition Count | Each disk supports up to 8 partitions. The system disk already has 4 default partitions, leaving up to 4 custom ones. The first custom partition on the system disk (sda5) becomes the system log partition. |
| Partition Size | Each partition must be an integer number of GB and at least 1 GB. By default, remaining space is split equally; any remainder goes to the last partition. |

---

## III. Important Notes

1. Up to **26 disks** are supported.
2. Formatting the system config or system log partitions requires a **router restart** to take effect.
3. Each service type (except **General Storage**) can only be bound to **one partition at a time** — the last binding wins if multiple are set.
4. Minimum partition sizes for specific services:
   - Youyu Fanshu: **2 GB**
   - Video Cache: **10 GB**
   - DingTalk Flash Transfer: **5 GB**
   - Other services: no minimum
5. Move/cut operations only work **within the same physical disk**.

---

## IV. Usage Example

1. Click **Quick Partition**, select the target disk, set the number of partitions, and allocate capacity for each.
2. After partitioning, click **Settings** on each partition to configure its **Bound Service** and **Mount Path**. Only **General Storage** partitions support a custom mount path.

---

## V. Common Issues

**What is the benefit of binding a service to a partition?**

Each service gets its own dedicated space, preventing one service from consuming all available disk space and causing other services to fail.
