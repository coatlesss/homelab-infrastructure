# Incident: Proxmox package and template downloads failed

**Environment:** Proxmox VE on home LAN

## Symptoms
- APT failed to download Proxmox packages, returning `Network is unreachable` for IPv6 targets.
- An initial `wget -4` attempt failed to resolve `download.proxmox.com`.
- IPv4 connectivity to a public IP worked.
- The router's DNS resolved common domains but was unable to return an IPv4 result for the Proxmox download hostname.
- A query to a public resolver did return an IPv4 address.
- A later HTTPS download attempt returned a certificate hostname mismatch.

## Diagnosis
The symptoms pointed to two distinct network problems:
1. No usable IPv6 route to the package endpoint.
2. Inconsistent DNS resolution for the download hostname through the home router.

The HTTPS certificate mismatch was a separate protocol/endpoint issue and was **not** addressed by disabling TLS verification.

## Resolution performed
- Used `Acquire::ForceIPv4=true` for APT updates.
- Configured an alternate public DNS resolver for the Proxmox host.
- Downloaded the required AMD64 template over the supported HTTP endpoint.

## Commands used in diagnosis
```bash
ping -4 -c 3 1.1.1.1
cat /etc/resolv.conf
getent ahostsv4 download.proxmox.com
dig @1.1.1.1 download.proxmox.com A +short
apt-get -o Acquire::ForceIPv4=true update
```

## Lessons
Test the network in layers: link and gateway, internet IP reachability, DNS lookup, protocol behavior, and certificate validation. A successful DNS query does not guarantee that the next transport step will work. Do not bypass certificate checks to force downloads.
