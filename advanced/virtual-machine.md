# Virtual Machine (虚拟机)

**Source:** https://www.ikuai8.com/support/ymgn/lyym/2019-12-13-06-35-05/2019-05-13-02-02-08.html

## I. Overview

iKuai supports running virtual machines (VMs) directly on x86 hardware using a built-in KVM/QEMU environment. Third-party OS images (e.g., NAS, Linux distributions) can be uploaded and run alongside the router.

**Requirements:**
- 64-bit firmware
- Recommended RAM: **4 GB or more**
- CPU must support hardware virtualization (Intel VT-x or AMD-V); must be enabled in BIOS
- At least one **General Storage** disk partition

---

## II. Parameter Reference

| Parameter | Description |
|---|---|
| Install Disk | The partition where the VM is installed. Must be a **General Storage** partition. |
| VM Name | Required, must be unique. A folder named after the VM is created automatically in the install directory. |
| Install Path | Auto-generated based on the selected disk. |
| OS Type | Linux, Windows, or Other. |
| CPU Usage % | Maximum percentage of host CPU the VM may use. |
| CPU Core Count | Number of virtual CPU threads. Maximum is determined by the host CPU model. |
| VM Memory | Required. Min: **64 MB**. Max: host available memory − 512 MB (e.g., 2048 MB available → max 1536 MB). |
| Add Disk | Up to **3 virtual disks**. Either create a new disk image or reference an existing one by path. |
| Add NIC | Up to **8 virtual NICs**. Select bridge interface; optionally bind to VLAN. Default: random MAC (editable). Modes: para-virtualized (virtio), PCI passthrough, e1000e, vmxnet3 (last two require firmware v3.7.6+). |
| Add USB | Up to **8 USB devices** (passthrough, subject to guest OS support). |
| Virtual CD-ROM | Specify an ISO file path. Loaded on VM startup. |
| VNC External Access | Default: disabled. When enabled, set a VNC password (default: `123456`). Access via `LAN_IP:VNC_PORT` (e.g., `192.168.1.1:5903`, colon must be ASCII). |
| VNC Port | Must be between **5901–5999**; no duplicate ports. |
| Auto Start | Default: enabled. VM restarts automatically after a router reboot. |
| Auto Start Priority | Order of VM startup (firmware v3.7.6+). |
| UEFI Boot | Enable UEFI firmware for the VM (firmware v3.7.0+). |
| Hardware Acceleration | Allow VM direct access to physical CPU features for better performance (KVM acceleration). Can be disabled for full software emulation. |

---

## III. Usage Example — Install NAS

1. Enable virtualization (VT) in BIOS.
2. Download the NAS installation ISO.
3. Create a **General Storage** partition in Disk Management.
4. Upgrade firmware to v3.3.0+ (64-bit, 4 GB RAM recommended).
5. Use **Quick Partition** to partition the disk.
6. Upload the NAS ISO to the General Storage partition via File Management.
7. Create a new VM and configure disk, RAM, and NIC settings.
8. Add the ISO path to the virtual CD-ROM and save.
9. Click **Power On** and connect via VNC to complete installation.

---

## IV. UEFI VM Setup

1. Enable UEFI in VM settings before first boot.
2. Boot into the UEFI installer and complete installation.
3. When you see "Installation complete, system will restart automatically," immediately and repeatedly press **ESC** to enter the boot settings menu before it reboots automatically.
4. In boot settings, change the default boot order to the installed disk.
5. Press F10 and confirm with **Y** to save, then select **Reset** to reboot normally.

---

## V. Notes

- If available RAM drops below 512 MB, no new VMs can be started.
- VMs boot from the first disk (top of the list by default); if no bootable disk, the CD-ROM is used.
- Max **20 VMs** can be created.
- RAW format images do not support snapshots — use VMDK format for snapshot support.
- PCI NIC passthrough requires the NIC to be in a separate IOMMU group; if NICs share an IOMMU group, passing through one removes the others from the host.
- VM logs viewable from firmware v3.7.6+.
