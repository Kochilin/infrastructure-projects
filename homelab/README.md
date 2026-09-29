# Homelab infrastructure

**Period:** January 2025 – present

## Problem

Home compute, storage, networking, backup, and automation grew as separate one-offs. There was no single inventory, no clear network segmentation, and no documented path to restore from backup. Rebuilding meant tribal knowledge, not a plan.

## Approach

Treat the lab as a small infrastructure practice: document the stack, separate network roles, back up with an explicit restore path, and prefer products that can be rebuilt from notes rather than remembered setups.

## Implementation

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

Work focused on:

- Segmenting the home network and setting firewall policy and local DNS on OPNsense with Unbound
- Running hypervisor and container workloads against a written inventory
- Putting shared storage and media mounts on ZFS via OpenMediaVault
- Defining Proxmox Backup Server jobs with a restore procedure, not only a successful job log
- Running Home Assistant OS as a virtual machine on Proxmox VE
- Running Nginx Proxy Manager as an LXC on Proxmox VE
- Running Plex on the bare-metal Docker host
- Fronting selected services so access does not require exposing the whole LAN
- Using NUT for UPS monitoring on the hosts
- Using Tailscale for controlled remote access

Sanitized diagram: [`architecture.md`](architecture.md).

## Outcome

A documented lab that can be explained and rebuilt from these notes: clear product roles, segmented network and DNS, ZFS-backed storage, PBS-backed restore path, and remote access without broad LAN exposure. Day-to-day detail stays in private notes; this folder is the public summary.
