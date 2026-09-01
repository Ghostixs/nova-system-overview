<p align="center">
  <img src="assets/banner.svg" alt="Nova, a self-hosted personal operations platform" width="100%">
</p>

<p align="center">
  <strong>Private by design. Observable by default. Honest about what is still being built.</strong>
</p>

Nova is a private, self-hosted personal operations platform that I design and operate across Windows, WSL2, and Docker. It brings infrastructure, monitoring, automation, documentation, recovery practices, and responsible AI experiments into one system I can understand, test, and improve.

This repository is a security-sanitized portfolio and case study. It explains the architecture and the work without publishing the private source repository, live configuration, credentials, addresses, hostnames, service data, or personal information.

<p align="center">
  <img src="assets/branding/nova-project-hero.webp" alt="Illustrated Nova builder at a purple-lit coding desk with Nova neon signage" width="880">
</p>

## Project status

Last runtime inspection: **August 31, 2026**

The technical evidence column records what was verified. The final column explains the practical meaning without changing the status or its limitations.

| Area | Status | What the evidence supports | Plain-language summary |
|---|---|---|---|
| Docker and WSL2 foundation | **Working** | The current WSL2 environment runs a persistent 22-container service layer. | Nova's core services are running together on a stable local foundation. |
| Boot recovery | **Validated** | A Windows AtLogOn task launches a passive WSL2 verifier with bounded convergence. Repeated cold boots ended healthy with no unexpected container recreation. | After a restart, Nova waits for core services to come online and verifies that they returned safely. |
| Service access and navigation | **Working** | Homepage and Caddy passed direct and routed availability checks across the Windows/WSL boundary. | The main dashboard and service routes are reachable from the host environment. |
| Observability | **Working foundation** | Prometheus verified three authoritative host/exporter target classes. Grafana, Loki, Promtail, Node Exporter, and Uptime Kuma were running; dashboard, alert, and retention coverage still varies. | Nova can monitor the health of its main systems, though monitoring coverage is still growing. |
| Home automation | **Working** | Home Assistant was running. Internal entities, locations, and automations remain private. | Home-automation services are available, while private household details remain unpublished. |
| Media workflow | **Working** | Request, management, download, VPN, subtitle, and playback services were running. Media data and private paths are not published. | The end-to-end media toolchain is operating, but no personal library or download details are exposed. |
| Backup and recovery | **Partial** | Recovery artifacts, controlled repair procedures, and boot verification exist. Off-host coverage and isolated restore testing are not complete for every service. | Nova has documented recovery options, but not every service yet has complete off-site backup and restore proof. |
| AI experimentation | **Experimental** | Open WebUI was healthy at inspection. Production RAG, agent routing, MCP integration, and autonomous actions are not verified. | The current AI interface can be tested, but advanced Nova intelligence is not a production capability yet. |
| Nova-native software | **In Development** | Nova Core and Nova Awareness source prototypes exist but are not deployed services. | Nova's own software is being built but is not running as a live service yet. |
| Advanced AI operations | **Planned** | RAG evaluation, persistent AI memory, agent routing, MCP tools, and human-approved actions remain roadmap work. | More advanced AI and tool-use capabilities are on the roadmap and have not been built yet. |

## Why I built Nova

I wanted a place where I could learn the full lifecycle of technical operations instead of studying each tool in isolation. Nova gives me a real environment in which to discover requirements, connect systems, troubleshoot failures, protect state, document decisions, and improve the experience of operating the whole platform.

The project is also a practical response to common operational problems:

- Service sprawl without a clear source of truth
- Configuration drift between intended and live state
- Limited visibility into health, metrics, and logs
- Recovery knowledge that exists only in one person's memory
- Asynchronous startup behavior hidden by fixed delays
- Automation ideas that need explicit safety and approval boundaries
- AI concepts that are easy to describe but much harder to validate responsibly

## Verified current capabilities

- Docker-based self-hosted environment under Linux and WSL2
- Private host-level networking through Tailscale
- Homepage navigation and Caddy reverse-proxy services
- Prometheus metrics with three verified authoritative target classes
- Grafana visualization, Loki logs, Promtail collection, Node Exporter, and Uptime Kuma
- Production-validated, fail-closed post-logon convergence verification
- Home Assistant for home-automation experimentation
- Jellyfin-centered media workflow with request, library, indexer, subtitle, download, and VPN components
- Vaultwarden for private credential management
- Open WebUI as an AI experimentation interface
- Git-based source control for engineering material
- Documented backup, recovery, troubleshooting, and verification procedures

## Architecture

<p align="center">
  <img src="diagrams/nova-public-architecture.svg" alt="Sanitized Nova architecture diagram" width="980">
</p>

The diagram shows trust boundaries and service groups rather than live network details. Open the [full-size diagram](diagrams/nova-public-architecture.svg), or see [Architecture](docs/architecture.md) for the evidence model and design decisions.

Nova's boot path is documented separately because startup convergence is easier to understand as a sequence. Open the [Boot Recovery sequence diagram](diagrams/nova-boot-recovery.svg), or read the [Boot Recovery V1 case study](docs/case-study-boot-recovery.md) for the engineering constraints, failure modes, and cold-boot validation.

## About the Builder

**Designed, built, operated, tested, and documented by Jacque.**

Nova is an ongoing systems and platform engineering project focused on reliability, observability, automation, and recoverable infrastructure.

## Technology stack

| Layer | Technologies |
|---|---|
| Host and runtime | Windows 11, WSL2, Ubuntu, systemd, Docker, Git |
| Private access | Tailscale, Caddy |
| Boot verification | Windows Task Scheduler, PowerShell, Bash, bounded health and dependency gates |
| Observability | Prometheus, Grafana, Loki, Promtail, Node Exporter, Uptime Kuma |
| Interfaces | Homepage, Portainer, Open WebUI |
| Home automation | Home Assistant |
| Media operations | Jellyfin, Jellyseerr, Sonarr, Radarr, Prowlarr, Bazarr, qBittorrent, Gluetun, Recyclarr, FlareSolverr |
| Documentation | Markdown, Mermaid, Obsidian, operational runbooks |
| AI roadmap | Retrieval evaluation, human review, model routing concepts, MCP concepts |

## Selected engineering work

- Diagnosed runtime/source drift and rebuilt an evidence-backed operating baseline
- Recovered stateful services from stale cross-distro bind mounts without resetting application state
- Diagnosed a qBittorrent restart loop, preserved state, applied a minimal repair, and verified recovery with acceptance checks
- Reconciled reverse-proxy and media storage paths after routing and mount failures
- Built authoritative Windows, WSL2, and container telemetry
- Designed a passive boot verifier with fail-closed VPN checks and bounded convergence
- Used repeated real cold boots to isolate Docker, VPN, proxy, and telemetry timing races
- Built operational trackers, verification queues, recovery records, and public-safe architecture maps
- Separated observed evidence from assumptions, prototypes, and roadmap ideas

## Current limitations

- The private environment still has configuration and documentation drift to resolve.
- Some services lack application-level health checks.
- Observability targets are verified, but dashboard, alert, notification, and retention coverage is not uniform.
- Backup coverage is uneven, and not every critical service has an off-host copy and isolated restore test.
- The boot verifier observes and classifies convergence; it is not a general-purpose remediation engine.
- Security hardening is ongoing. Privileged integrations and service exposure require continued review.
- Nova Core and Nova Awareness are prototypes, not dependable platform services.
- No production RAG, agent, MCP, or autonomous-action capability is claimed.

## Responsible AI and human control

Nova's AI roadmap starts with an operational rule: the model is not the source of truth. Evidence, source provenance, approval boundaries, and recoverability matter more than an impressive demo.

Planned AI workflows will be evaluated for answer quality, failure behavior, permissions, logging, and human handoff before any action capability is considered. Actions that affect systems or data should remain explicit, reviewable, and reversible.

## Roadmap

- **Current foundation:** stability, bounded boot verification, observability, documentation, backups, private access, and operational dashboards
- **Near term:** curate source drift, improve restore testing, and strengthen authentication, secret handling, and image reproducibility
- **Later:** RAG-backed memory, retrieval evaluation, agent routing, MCP-enabled tools, human-approved actions, model selection, voice interfaces, and hardware experimentation

Read the complete [Roadmap](docs/roadmap.md).

## Documentation

For a concise interview walkthrough: [Architecture](docs/architecture.md) -> [Boot Recovery V1 case study](docs/case-study-boot-recovery.md) -> [Current state](docs/current-state.md) -> [Roadmap](docs/roadmap.md).

| Document | Purpose |
|---|---|
| [Architecture](docs/architecture.md) | Sanitized structure, trust boundaries, and data flows |
| [Current state](docs/current-state.md) | Component-by-component evidence and limitations |
| [Build history](docs/build-history.md) | Selected milestones and what changed |
| [Observability](docs/observability.md) | Metrics, logs, availability, and verification boundaries |
| [Operations and recovery](docs/operations-and-recovery.md) | Change safety, backups, boot verification, and recovery method |
| [Security and privacy](docs/security-and-privacy.md) | Publication boundaries and security posture |
| [Lessons learned](docs/lessons-learned.md) | Practical technical and operational takeaways |
| [Boot Recovery V1 case study](docs/case-study-boot-recovery.md) | Bounded post-logon convergence across Windows, WSL2, Docker, VPN, proxy, and telemetry |
| [qBittorrent recovery case study](docs/case-study-qbittorrent-recovery.md) | Evidence-led diagnosis and minimal repair |

## Privacy and security

The private Nova repository and its Git history have not been published or copied here. This repository contains newly written documentation, synthetic examples, and sanitized diagrams only. Screenshots were intentionally omitted because a useful screenshot could also disclose operational details.

For more information, read [Security and privacy](docs/security-and-privacy.md) and [SECURITY.md](SECURITY.md).
