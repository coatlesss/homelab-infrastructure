# HTTP service monitoring with Uptime Kuma

**Status:** Operational monitor verified as UP. Simulated DOWN/recovery and notification evidence still to be added.

## Objective
Separate application monitoring from the monitored service, allowing an HTTP service to be checked independently of the guest running it.

## Architecture
- Ubuntu VM `100`: Nginx web server
- Debian 13 AMD64 LXC container `200`: Uptime Kuma
- Uptime Kuma checks Nginx over HTTP on the private LAN.

## Implementation
1. Created an unprivileged Debian LXC container.
2. Installed Node.js, npm, Git, and Uptime Kuma.
3. Used SQLite for the small monitoring installation.
4. Created an HTTP(s) monitor for the Ubuntu Nginx endpoint.
5. Confirmed the monitor displayed the service as green/UP.

## Incident-response test — to document
1. Verify the monitor reports UP.
2. On the Ubuntu VM: `sudo systemctl stop nginx`.
3. Record the monitor reporting DOWN after the configured interval/retries.
4. Restore Nginx: `sudo systemctl start nginx`.
5. Record the monitor returning to UP and write down detection/recovery times.

Do not label these tests completed until the transitions have been observed.

## Limitations
The monitoring container and monitored VM share one physical Proxmox host. Monitoring therefore cannot reliably alert on complete host or power loss. An external monitor or second machine would improve fault independence.

## Next improvements
- Enable restart-on-boot and verify it after a container restart.
- Configure an alert destination and send a test notification.
- Add monitoring for SSH/TCP services and container health.
