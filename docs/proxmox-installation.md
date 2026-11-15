# Proxmox installation and host administration

**Status:** Implemented — November 2026

## Objective
Turn a refurbished mini PC into a remotely managed virtualization host for Linux administration and infrastructure operations labs.

## Hardware
- Lenovo ThinkCentre M710q Tiny
- Intel Core i3-6100T
- 8 GB RAM
- 256 GB SSD

## Implementation
1. Enabled Intel virtualization in Lenovo firmware settings.
2. Prepared the x86-64 Proxmox VE 9.2 installation USB.
3. Installed Proxmox VE to the internal SSD with a simple ext4-based configuration.
4. Configured a host management IP, gateway, and DNS.
5. Logged into the HTTPS management interface on port 8006.
6. Disabled subscription-only repositories and enabled the no-subscription repository.
7. Applied available host updates, handling an unavailable IPv6 download route.

## Verification
- Proxmox dashboard reachable from a separate PC.
- Host summary showed processor, RAM, and local storage.
- Package metadata refresh and updates worked using reachable IPv4 paths.
- Guest VM and LXC container were subsequently created and administered from the GUI.

## Operational notes
- Keep the management interface restricted to the trusted LAN.
- A no-subscription repository is appropriate for a personal lab but is not an enterprise support contract.
- Keep firmware, host, and guest changes documented and recoverable.

## Evidence to add
- Sanitized host summary screenshot
- Sanitized VM/container inventory screenshot
- Repository configuration screenshot, with identifying details removed

See [DNS and IPv6 troubleshooting](../troubleshooting/ipv6-dns-issues.md).
