# Incident: Ubuntu VM failed to boot after installation

**Environment:** Proxmox VM `100`, Ubuntu Server, SeaBIOS, 25 GiB SCSI disk

## Symptom
On reboot, the console displayed `Boot failed: not a bootable disk` and fell through to network/PXE boot.

## Checks
- The VM boot order listed the virtual disk first.
- The SCSI virtual disk existed on `local-lvm`.
- The installer ISO had been removed from the virtual CD/DVD device.

## Remediation performed
1. Reattached the Ubuntu installation ISO and temporarily booted from it.
2. Reinstalled Ubuntu using the existing 25 GiB virtual disk.
3. Selected entire-disk partitioning without guest LVM for simplicity.
4. Verified the storage summary included a BIOS GRUB spacer partition and an ext4 root partition.
5. Finished installation, removed installation media, and booted from the virtual disk.

## Outcome
Ubuntu subsequently booted, completed first-boot initialization, and accepted local and SSH logins.

## Lesson
Distinguish a missing/invalid guest bootloader from an incorrect boot order. Inspect the disk and firmware mode before assuming the hypervisor has failed.
