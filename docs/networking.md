# Home lab networking

**Status:** Implemented and tested

## Topology
The physical Proxmox host, Ubuntu guest VM, and Debian monitoring container use the existing home Ethernet/LAN. The guest workloads connect through Proxmox's `vmbr0` bridge.

## Work completed
- Configured a static Proxmox management address outside the router's DHCP pool.
- Configured Ubuntu's interface (`ens18`) using Netplan rather than relying on changing DHCP leases.
- Checked potential IP conflicts before assigning the VM address.
- Verified guest-to-internet ICMP connectivity and DNS resolution.
- Diagnosed a host-side difference between IPv6 reachability and IPv4 reachability.
- Investigated router DNS versus public resolver answers for the Proxmox download domain.

## Netplan pattern (illustrative; replace all placeholders)
```yaml
network:
  version: 2
  ethernets:
    ens18:
      dhcp4: false
      addresses:
        - <GUEST_IP>/<PREFIX>
      routes:
        - to: default
          via: <GATEWAY_IP>
      nameservers:
        addresses:
          - <DNS_IP>
```

In a real config, replace the placeholders with valid values. Apply network changes from a console where possible. `sudo netplan try` provides a confirmation/rollback window, useful when working remotely.

## Verification
```bash
ip -4 address show ens18
ip route
ping -4 -c 3 1.1.1.1
getent ahostsv4 ubuntu.com
```

## Security
Keep the router admin page, private topology details, MAC addresses, and internal configuration exports out of the public repository.
