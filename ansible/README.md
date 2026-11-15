
# Ansible Infrastructure Automation

## Overview

This project demonstrates automated Linux server administration using Ansible and SSH.

An Ubuntu Server control node manages a Debian 13 LXC container hosted on Proxmox VE.

## Infrastructure

| Component | Description |
|---|---|
| Control node | Ubuntu Server VM 100 |
| Managed node | Debian 13 LXC container 201 |
| Automation | Ansible |
| Web server | Nginx |
| Authentication | SSH keys |

## Features

- Automated Nginx installation
- Automated service startup and enablement
- Automated webpage deployment
- Remote Linux administration over SSH
- Idempotent configuration management

## Results

Successfully deployed and updated a custom Nginx webpage using Ansible.

Verified idempotence by rerunning the playbook and receiving `changed=0`.

## Usage

Create an inventory from `inventory.example.ini` and replace the placeholder IP address with your own managed server's address.

Run:

```bash
ansible all -m ping
ansible-playbook setup-webserver.yml -K
```

## Skills Demonstrated

Linux administration, Ansible, YAML, SSH authentication, Nginx, infrastructure automation, and configuration management.
