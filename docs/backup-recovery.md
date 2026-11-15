# Proxmox VM backup and recovery exercise

**Status:** Backup creation and restore performed. In-guest validation evidence should be added only if retained.

## Objective
Practice restoring a complete Linux virtual machine without modifying the original workload.

## Procedure performed
1. Created a Proxmox backup of Ubuntu VM `100`.
2. Confirmed the backup task reported `TASK OK`.
3. Restored the archive into a separate test VM with ID `101`.
4. Isolated or removed the restored VM's virtual network interface to avoid a duplicate static IP.
5. Removed the temporary recovery VM afterward to reclaim disk space.

## Verification evidence
- Backup task: reported successful.
- Restore task: reported successful.
- A separate login/boot and file-integrity verification is ideal; **do not claim that it passed unless separately documented**.

## Suggested next validation
On a *future* isolated restore:
```bash
hostname
whoami
lsblk
test -d /home/<your-user> && echo "home exists"
```
Also verify a known test file's checksum before and after restoring.

## Limitations
This backup was saved on the same physical SSD as the original VM. It protects against some guest-level mistakes but **not** SSD or whole-host failure. Next improvement: add an external disk or a remote backup target, and perform a documented end-to-end restore.
