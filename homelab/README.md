# Homelab infrastructure

**Period:** January 2025–present  
**Scope:** Personal infrastructure for networking, virtualization, storage, containers, backup, automation and remote administration  
[Logical architecture](architecture.md)

## Problem

As individual services accumulated, the lab needed a coherent design: network separation, clear service ownership, repeatable deployment notes and more than one way to recover after a host or storage failure. A successful backup job alone was not enough of an operating plan.

## Design approach

I treated the homelab as a small infrastructure environment instead of a collection of unrelated devices. Core design choices were to separate trust zones, assign roles to hosts, distinguish VM/LXC workloads from a dedicated Docker host, and document backup and access paths. Detailed inventory and recovery instructions stay private; this public case study explains the architecture and decisions.

## Architecture and implementation

| Area | Technology and role |
| --- | --- |
| Routing and segmentation | OPNsense firewall; separate network zones and inter-zone policy |
| Switching and wireless | Cisco SG350 managed switching and UniFi access points |
| DNS | Unbound on OPNsense and an AdGuard Home service |
| Virtualization | Proxmox VE for virtual machines and LXC services |
| VM/LXC backup | Proxmox Backup Server on a separate system |
| Shared storage | OpenMediaVault on Debian with ZFS mirrored storage |
| Container services | Docker Compose on a separate bare-metal Linux host |
| Remote administration | Tailscale, including subnet-routing capability |
| Application access | Nginx Proxy Manager for selected internal web services |
| Automation and media | Home Assistant OS VM; Plex and associated services on Docker |
| Power awareness | Network UPS Tools (NUT) |

**Network design.** I use distinct zones for management, trusted devices, IoT, guest traffic and lab workloads, with the firewall controlling permitted crossings. Managed switching and wireless carry the relevant networks; DNS and remote connectivity are explicit infrastructure services rather than incidental application settings.

**Workload placement.** Proxmox hosts VM and LXC workloads, including Home Assistant OS and infrastructure services such as Nginx Proxy Manager and AdGuard Home. A separate Docker Compose host runs the media/application stack. This separates the hypervisor's lifecycle from the larger container workload.

**Storage and recovery.** OpenMediaVault provides ZFS-backed storage consumed by other systems. Proxmox Backup Server receives scheduled VM/LXC backups; the Docker host has a separate Restic backup schedule and retention policy. The recovery model therefore distinguishes restoring hypervisor workloads, application data and storage instead of implying PBS backs up everything.

**Access and operations.** Tailscale supports remote administration without publishing the entire LAN. Nginx Proxy Manager fronts selected applications. NUT provides UPS status to hosts and supports power-aware operations. Inventory, changes and recovery notes are maintained privately.

## Engineering decisions illustrated

- Use dedicated backup infrastructure rather than depend on the production hypervisor as the only recovery location.
- Use different backup mechanisms for Proxmox workloads and Docker-host application data.
- Keep network segmentation and the remote-access path separate from application-level reverse proxying.
- Document logical dependencies so an outage can be diagnosed or rebuilt in an understandable order.

## Outcome and scope of validation

An operating personal lab with defined host responsibilities, segmented networking, ZFS-backed shared storage, scheduled PBS and Restic backups, and managed remote access. This write-up documents the recovery design; it does **not** claim a full bare-metal disaster-recovery exercise has been completed. The diagram is intentionally logical, not a rack or cabling schematic.

## Publication boundary

No live configs, private network ranges, device names, serial numbers, rack photos, credentials, or externally reachable endpoints are included.
