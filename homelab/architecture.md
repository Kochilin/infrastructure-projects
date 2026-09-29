# Homelab logical architecture

Sanitized product/role diagram. The zones below show **segmentation intent**, not actual VLAN IDs, switch ports, hostnames, addressing, or firewall rule order.

```mermaid
flowchart TB
  NET[Internet / ISP] --> FW[OPNsense firewall]
  FW --> SW[Cisco SG350 managed switching]
  SW --> AP[UniFi Wi-Fi]

  subgraph zones [Logical network zones]
    MGMT[Management]
    TRUST[Trusted devices]
    IOT[IoT]
    GUEST[Guest]
    LAB[Homelab workloads]
  end

  SW --- MGMT
  SW --- TRUST
  SW --- IOT
  AP --- GUEST
  SW --- LAB

  subgraph infra [Infrastructure services]
    UB[Unbound DNS]
    AG[AdGuard Home]
    TS[Tailscale / remote administration]
    NPM[Nginx Proxy Manager]
  end
  FW --- UB
  LAB --- AG
  LAB --- NPM
  TS -. controlled remote path .-> LAB

  subgraph compute [Compute]
    PVE[Proxmox VE]
    HA[Home Assistant OS VM]
    LX[LXC services]
    DOCKER[Separate bare-metal Docker host]
    PLEX[Plex / application containers]
  end
  LAB --> PVE
  LAB --> DOCKER
  PVE --> HA
  PVE --> LX
  LX --> AG
  LX --> NPM
  DOCKER --> PLEX

  subgraph recovery [Storage and recovery]
    OMV[OpenMediaVault / ZFS]
    PBS[Proxmox Backup Server]
    RESTIC[Restic backups]
  end
  PVE -->|VM and LXC backups| PBS
  DOCKER -->|Application data backups| RESTIC
  OMV -. shared storage / mounts .-> PVE
  OMV -. media / data mounts .-> DOCKER

  UPS[NUT / UPS monitoring] -. status .-> PVE
  UPS -. status .-> DOCKER
  UPS -. status .-> OMV
```

## Reading the diagram

- The firewall governs crossing between network zones; lines to zones do not grant unrestricted access.
- Unbound and AdGuard Home are both in the DNS stack. This diagram deliberately does not assert a specific resolver-chain order.
- Proxmox Backup Server and Restic represent **different** backup scopes; the diagram makes no claim that PBS protects bare-metal Docker data.
- Reverse proxying selected web services and remote administration over Tailscale solve different access problems.
- NUT is represented as host-level power monitoring, not an application container.

This is a conceptual map only; exact dependencies, retention settings and restore commands are maintained privately.
