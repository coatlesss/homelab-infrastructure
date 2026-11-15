# Ubuntu Server administration

**Status:** Implemented — November 2026

## Objective
Deploy and remotely administer a Linux guest to practice networking, system services, authentication, and operational troubleshooting.

## Deployment
- Proxmox VM ID: `100`
- Ubuntu Server LTS
- 2 vCPUs; 2 GiB RAM; 25 GiB virtual disk
- VirtIO network attached to Proxmox bridge `vmbr0`
- Guest hostname: `goon-server-01`
- Local administrative user created during Ubuntu installation

## Work completed
1. Installed Ubuntu using a BIOS-compatible disk layout with a BIOS boot partition and ext4 root filesystem.
2. Enabled and verified OpenSSH.
3. Tested SSH authentication from a Windows workstation.
4. Generated an Ed25519 SSH keypair on Windows and installed the *public* key in the guest account's `authorized_keys`.
5. Installed QEMU Guest Agent and enabled its interface in Proxmox.
6. Configured an IPv4 address through Netplan, preserving a route through the LAN gateway and working DNS.
7. Verified IPv4 network connectivity and hostname resolution.
8. Installed Nginx, enabled its systemd service, and verified the default web page from another computer.

## Example operational commands
```bash
hostname -I
systemctl is-active ssh
systemctl is-active qemu-guest-agent
systemctl is-active nginx
sudo systemctl stop nginx
sudo systemctl start nginx
journalctl -u nginx --no-pager -n 50
```

## Safety and reproducibility
- Replace sample LAN information with values appropriate to your own network.
- Test SSH keys before disabling password-based SSH login.
- Use the Proxmox console as an out-of-band fallback when changing guest networking.
- Never publish passwords, private keys, raw `authorized_keys`, or configuration files containing secrets.

## Evidence to add
- Sanitized SSH login and `hostname` output
- QEMU Guest Agent active state
- Browser screenshot of Nginx welcome page
