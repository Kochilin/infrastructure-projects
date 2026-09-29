# Synology NAS solution architecture (sanitized)

Conceptual access-and-recovery model, not a depiction of an identifiable deployment.

```mermaid
flowchart TB
  STAFF[Team members] --> ROLE[Role-appropriate access]
  ROLE --> SHARES[DSM shared folders]

  ADM[Administrators] --> MFA[Administrative MFA]
  MFA --> POLICY[Management-plane firewall policy]
  POLICY --> DSM[DSM administration]

  REMOTE[Authorized remote users] --> TS[Tailscale access path]
  TS --> POLICY
  TS --> ROLE

  SHARES --> HB[Hyper Backup schedule / retention]
  HB --> COPY[Backup destination - withheld]
  COPY -. recovery procedure .-> RESTORE[Restore validation checkpoint]
```

## Control boundaries

- Staff share access and DSM administrative access are separate functions.
- Tailscale is an access transport; it does not replace DSM permissions, MFA or firewall policy.
- Hyper Backup configuration documents the backup process. The restore-validation checkpoint is a **required verification step**, not a claim that a drill has already passed.
- Arrows describe responsibility and data/control flow, not actual ACLs, routes, public endpoints or site topology.

No client or production identifiers appear here.
