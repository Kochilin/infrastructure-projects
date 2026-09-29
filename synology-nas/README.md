# Synology NAS reconfiguration and security hardening

**Period:** 2026  
**Context:** WGU capstone for a live entertainment company (client name withheld)

This case study applies the same discipline as the [homelab](../homelab/) work — inventory, least privilege, remote access without broad exposure, and backups you can restore — to a real organization's requirements on a Synology NAS.

## Problem

The NAS was in daily use for shared storage and backup, but access and hardening had drifted: share layout did not match how teams worked, permissions were broader than needed, administrative access lacked strong controls, and backup success was not proven with restore drills. Remote access risked depending on wide exposure of the management plane.

## Approach

Reconfigure in place rather than replace. Align shared folders to real workflows, tighten who can do what, harden admin access (MFA and firewall), move remote access to Tailscale, and treat Hyper Backup as incomplete until a restore drill passes.

## Implementation

- Redesigned shared folder layout to match how teams actually use the system
- Applied least-privilege share and account permissions
- Enabled MFA on administrative access
- Tightened the firewall on the NAS management plane
- Introduced Tailscale for controlled remote access instead of broad exposure
- Configured Hyper Backup with documented retention
- Ran restore drills to verify backup usefulness, not only job success

Sanitized diagram: [`architecture.md`](architecture.md).

## Outcome

A hardened Synology NAS aligned to organizational use: clearer shares, least-privilege access, MFA-protected admin paths, management plane not broadly exposed, Tailscale-based remote access, and backup design that includes a tested restore path. Client name and environment specifics stay out of this write-up by design.
