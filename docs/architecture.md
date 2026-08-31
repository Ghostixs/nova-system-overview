# Architecture

## Purpose

Nova is a private personal operations environment. Its mature layer is the self-hosted infrastructure. Native AI memory and action systems remain prototypes or roadmap work.

The public architecture intentionally omits addresses, hostnames, domains, device identities, exact storage paths, service credentials, and security-sensitive routing details.

## Evidence model

Claims in this repository use the following order of authority:

1. Current runtime and service state
2. Current configuration and source files
3. Git working tree and history
4. Reviewed technical documentation
5. Older plans and architecture material

When two sources disagree, the discrepancy is documented as drift. A plan is never promoted to a working capability because a directory or design document exists.

## Status language

| Status | Meaning |
|---|---|
| **Working** | Direct current evidence supports the running component or capability. |
| **Partial** | Important evidence exists, but end-to-end behavior, recovery, or coverage is incomplete. |
| **In Development** | Source or a prototype exists, but it is not a dependable deployed capability. |
| **Planned** | An intended future capability with no current implementation claim. |

## High-level structure

The rendered diagram is available at [nova-public-architecture.svg](../diagrams/nova-public-architecture.svg), with Mermaid source at [nova-public-architecture.mmd](../diagrams/nova-public-architecture.mmd).

At a high level:

1. A Windows 11 host provides the desktop environment and native private networking.
2. WSL2 runs an Ubuntu environment that hosts Docker and the private engineering workspace.
3. Docker runs grouped services for access, observability, home automation, media operations, credentials, and AI experimentation.
4. Git and technical documentation preserve source history, decisions, verification results, and recovery knowledge.
5. Nova-native memory and agent capabilities remain outside the working service layer until they are implemented and evaluated.

## Current service groups

### Access and navigation

Homepage provides a private service entry point. Caddy supplies reverse-proxy functionality. Tailscale runs at the host level rather than as a current Docker workload.

### Observability

Prometheus and Node Exporter provide a metrics foundation. Loki and Promtail provide a logging foundation. Grafana provides visualization. Uptime Kuma provides availability monitoring.

These services were running at inspection. The complete target list, dashboard behavior, alerting, retention, and notification paths were not all independently exercised, so the subsystem is labeled **Partial**.

### Home automation

Home Assistant runs as part of the Docker environment. Its entities, locations, personal data, integrations, and automation logic remain private.

### Media operations

The current environment includes request management, media management, indexer coordination, subtitle support, VPN-routed downloading, and playback. Public documentation explains the workflow at a service-group level without exposing media data or internal paths.

### Credential management

Vaultwarden runs in the private environment. No credential data, database material, recovery values, or configuration details are included publicly.

### AI experimentation

Open WebUI provides a working interface for experimentation. A healthy interface is not evidence of a production retrieval pipeline, dependable model orchestration, autonomous agent, or approved action framework.

### Nova-native prototypes

Nova Core contains early SQLite-backed knowledge-model work and incomplete subsystem structures. Nova Awareness contains a Docker-event monitoring prototype and a small in-process event bus. Neither is deployed as a current platform service.

## Trust boundaries

- **Public repository:** documentation, diagrams, and synthetic examples only
- **Private source repository:** engineering source and deployment material
- **Runtime configuration:** private service definitions and operational settings
- **Persistent service data:** databases, logs, credentials, and personal content
- **Host networking:** private routes, identities, and access policy
- **AI experimentation:** limited to explicit experiments, with production actions still planned

## Architecture decisions that matter

- Keep the private system separate from the public portfolio.
- Treat live evidence as stronger than stale documentation.
- Preserve state before repair and keep rollback steps explicit.
- Separate backup creation from restore verification.
- Avoid presenting a running interface as a completed AI capability.
- Require provenance, permissions, logging, evaluation, and human approval before future action workflows.
