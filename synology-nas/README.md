# Synology NAS reconfiguration and security hardening

**Period:** 2026  
**Context:** Western Governors University IT capstone for a live entertainment company (client withheld)  
[Sanitized solution architecture](architecture.md)

## Problem

A live-entertainment workflow depends on shared media/project storage that different teams can access without receiving unnecessary administrative privileges. The project addressed share organization, permission boundaries, administrative security, recoverable backups and remote access while retaining the existing Synology platform.

## Approach

The design prioritized improving an existing system rather than replacing functioning infrastructure: organize folders around team workflows, reduce privileges, protect administration, constrain management access, and provide remote connectivity without opening the NAS management interface broadly to the Internet.

## Implementation and design

| Area | Work / technology |
| --- | --- |
| Shared storage | Synology DSM shared-folder organization aligned with team use |
| Access control | Role-appropriate share/account permissions and administrative separation |
| Administrative security | MFA and tighter NAS firewall controls |
| Remote connectivity | Tailscale for controlled access |
| Backup | Hyper Backup schedule and retention documentation |
| Recovery | Documented restore approach and recovery considerations |

The project focused on the NAS's existing storage and backup role. It did not require replacing it with a new vendor platform or exposing the DSM management interface through generic Internet port forwarding.

## Engineering decisions illustrated

**Workflow before folder structure.** Organizing shares by how people actually exchange and maintain project assets reduces permission sprawl and simplifies ownership of data.

**Separate administrative and everyday access.** Staff need the relevant shares, not a privileged management session. MFA and firewall restrictions add controls to administrative access.

**Remote access without blanket exposure.** Tailscale provides a managed access path instead of making the NAS management interface generally Internet-facing.

**Backup completion is not recovery proof.** Hyper Backup jobs and retention establish the backup design; a separate restore check is needed to establish recoverability.

## Outcome and validation boundary

The capstone documents a reconfiguration and hardening approach for shared storage, identity/access control, remote connectivity and backup operations on an existing NAS. Backup schedules and retention were documented. Recovery procedures were included in the design; successful restore validation has not been independently verified.

The public narrative is intentionally limited to technical responsibilities and design decisions; operational specifics and identifying client information are excluded.

## Publication boundary

No client name, site details, real configurations, private addresses, device names, serial numbers, screenshots of access settings, credentials or backup destinations are published.
