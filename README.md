# Infrastructure projects

Portfolio write-ups for two systems projects. Product names and architecture only — no live configs, hostnames, addresses, or client identifiers.

## Homelab infrastructure

**Period:** January 2025 – present

Personal lab for compute, storage, networking, backup, and home automation. Built to be rebuildable from documentation rather than tribal knowledge.

### Stack

| Layer | Products |
|-------|----------|
| Hypervisor / backup | Proxmox VE, Proxmox Backup Server |
| Storage | OpenMediaVault on Debian with ZFS |
| Containers | Bare-metal Docker |
| Switching / Wi‑Fi | Cisco SG350, UniFi |
| Firewall / DNS | OPNsense with Unbound |
| Remote access | Tailscale |
| Automation / media / edge | Home Assistant, Plex, Nginx Proxy Manager |
| Power monitoring | NUT |

### What it demonstrates

- Segmented home network with firewall policy and local DNS
- Container workloads on a documented inventory
- ZFS-backed shared storage and media mounts
- Backup jobs with an explicit restore path (PBS)
- Reverse proxy and service access without exposing the whole LAN
- Home automation integrated with the same network model

### Constraints for this write-up

No private IPs, hostnames, serials, rack photos, or real config files. Details stay in private notes; this repo is the public summary only.

---

## Synology NAS reconfiguration and security hardening

**Period:** 2026  
**Context:** WGU capstone for a live entertainment company (client name withheld)

Reconfigured and hardened a Synology NAS used for shared storage and backup, with emphasis on least privilege and recoverable backups.

### Work completed

- Shared folder layout aligned to how teams actually use the system
- Least-privilege share and account permissions
- MFA on administrative access
- Firewall tightening on the NAS management plane
- Tailscale for controlled remote access instead of broad exposure
- Hyper Backup jobs with documented retention
- Restore drills to verify backup usefulness, not just job success

### What it demonstrates

- Security hardening on a NAS without a rip-and-replace
- Separation of admin access from day-to-day share use
- Remote access that does not depend on port-forwarding the NAS UI
- Backup design that includes a tested restore path

### Constraints for this write-up

No company name beyond “a live entertainment company.” No private IPs, hostnames, serials, or real configs.

---

## License

Documentation only. All product names belong to their respective owners.
