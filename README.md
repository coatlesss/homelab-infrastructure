# Cloud & Systems Administration Homelab

A hands-on infrastructure lab focused on Linux administration, virtualization, networking, infrastructure monitoring, backup and recovery, and cloud operations.

## Project Overview

This homelab is designed to simulate real-world IT infrastructure administration. The goal is to develop practical skills in deploying, securing, monitoring, troubleshooting, and recovering server environments.

The environment uses Proxmox VE for virtualization, Ubuntu Server for Linux administration, and Debian LXC containers for lightweight services.

## Hardware

| Component | Specification |
|---|---|
| Server | Lenovo ThinkCentre M710q Tiny |
| Processor | Intel Core i3-6100T |
| RAM | 8 GB |
| Storage | 256 GB SSD |
| Hypervisor | Proxmox VE 9.2 |

## Infrastructure

### Virtualization
- Installed and configured Proxmox VE
- Configured local storage and virtual networking
- Deployed an Ubuntu Server virtual machine
- Deployed a Debian LXC container
- Installed and configured the QEMU Guest Agent

### Linux and Network Administration
- Installed Ubuntu Server
- Configured a static IPv4 address
- Set up SSH key-based remote access
- Managed packages and systemd services
- Configured and tested an Nginx web server
- Troubleshot DNS and IPv6 connectivity problems

### Backup and Disaster Recovery
- Created a Proxmox VM backup
- Restored the backup into an isolated test VM
- Practiced recovery verification and cleanup

### Infrastructure Monitoring
- Deployed Uptime Kuma in a Debian LXC container
- Configured HTTP monitoring for Nginx
- Verified service availability through the monitoring dashboard

## Technologies Used

Proxmox VE, Ubuntu Server, Debian Linux, LXC, SSH, Nginx, Uptime Kuma, QEMU Guest Agent, Netplan, systemd.

## Future Improvements

- Configure monitoring notifications and incident response
- Establish an external backup destination
- Deploy a second Proxmox host
- Automate Linux administration with Ansible
- Build Microsoft Azure administration labs
- Document cloud identity, storage, networking, and monitoring exercises

## Project Goals

Demonstrate practical infrastructure administration skills relevant to cloud administrator, systems administrator, cloud operations, and IT infrastructure roles.

This repository documents the environment's configuration, troubleshooting, testing, and ongoing improvements.
