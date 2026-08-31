# Current State

Last runtime inspection: **August 30, 2026**

## How to read this page

**Working** means current runtime evidence supports the component. It does not mean every feature or user journey was tested. When the application had no Docker health check or the complete data flow was not independently exercised, the limitation is stated directly.

No private addresses, hostnames, paths, domains, identifiers, credentials, or application data are included.

## Platform and access

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Windows 11 | Host operating environment | **Working** | User-confirmed environment and current host context | Host security policy was not audited for publication. |
| WSL2 and Ubuntu | Linux engineering and runtime environment | **Working** | Current kernel and operating-system inspection | Exact host identity is withheld. |
| Docker | Container runtime | **Working** | Current runtime inventory showed the active service layer | Two old test containers were exited and are not part of Nova. |
| Git and private GitHub source | Change history and engineering source | **Working** | Private repository and remote were verified | The private repository and history remain private. |
| Tailscale | Private host-level networking | **Working** | Windows service was running; WSL daemon was inactive as expected | Routes, peers, ACLs, addresses, and device names were not published. |
| Homepage | Service navigation | **Working** | Container was running and healthy | Private links and service widgets are withheld. |
| Caddy | Reverse proxy | **Working** | Container was running; recent source history documents routing recovery | Routes and domains are withheld. |
| Portainer | Container administration | **Partial** | Container was running; recovery documentation exists | Privileged access and recovery controls require continued review. |

## Observability

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Prometheus | Metrics collection | **Working** | Container running; current configuration contained multiple scrape jobs | Complete target health and retention were not independently verified. |
| Node Exporter | Linux host metrics | **Working** | Container running | Individual metric coverage was not audited. |
| Grafana | Dashboards and visualization | **Partial** | Container running | Grafana had restart history, and dashboards and data sources were not fully exercised. |
| Loki | Log storage | **Partial** | Container running | Active ingestion and retention were not fully verified. |
| Promtail | Log collection | **Partial** | Container running; reviewed documentation confirms log-source access | Delivery continuity and sensitive-log handling need continued review. |
| Uptime Kuma | Availability monitoring | **Working** | Container running and healthy | Monitor targets and notifications remain private and were not fully audited. |

## Home, credentials, and AI interface

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Home Assistant | Home automation | **Working** | Container running | Entities, locations, devices, and automations are private. |
| Vaultwarden | Credential management | **Working** | Container running and healthy | Configuration, database content, and recovery material are private. |
| Open WebUI | AI experimentation interface | **Partial** | Container running and healthy | No production RAG, dependable local-model orchestration, or autonomous action claim is made. |

## Media operations

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Jellyfin | Media playback | **Working** | Container running and healthy | Media, users, libraries, and paths are private. |
| Jellyseerr | Request workflow | **Working** | Container running | Application-level health was not independently exercised. |
| Sonarr | Series management | **Working** | Container running | Library and download details are private. |
| Radarr | Film management | **Working** | Container running | Library and download details are private. |
| Prowlarr | Indexer coordination | **Working** | Container running | Provider configuration is private. |
| Bazarr | Subtitle management | **Working** | Container running | Library paths and providers are private. |
| qBittorrent | Download client | **Working** | Container running on a pinned current image; prior recovery was documented and verified | User data, paths, and network details are private. |
| Gluetun | VPN gateway for the download workflow | **Working** | Container running and healthy | Provider, endpoint, and credential details are private. |
| Recyclarr | Configuration synchronization | **Working** | Container running | Application-level schedule and configuration were not fully audited. |
| FlareSolverr | Supporting request service | **Working** | Container running | Application-level health was not independently exercised. |

## Native Nova software and roadmap

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Nova Awareness | Docker-event monitoring prototype | **In Development** | Source and historical event records were inspected | Not deployed, no persistent service definition, and no dependable test suite. |
| Nova Core | Model-independent knowledge foundation | **In Development** | Early SQLite and model source was inspected | Incomplete packages, conflicting storage designs, and no deployment. |
| cAdvisor | Additional container metrics | **Planned** | Definition exists but no running container was found | Deployment intent must be reconciled. |
| RAG-backed memory | Retrieval-supported personal memory | **Planned** | Design material only | No working embedding or retrieval pipeline is verified. |
| Agent routing | Model and tool coordination | **Planned** | Roadmap material only | No production agent router is verified. |
| MCP integration | Standardized tool access | **Planned** | Roadmap material only | No completed MCP integration is verified. |
| Human-approved AI actions | Controlled automation | **Planned** | Safety principle and roadmap only | Approval, permissions, logging, rollback, and evaluation must be designed first. |
| Voice, robotics, and wearables | Future interfaces | **Planned** | Long-term ideas only | No operational capability is claimed. |

## Current operational truth

The strongest verified claim is that Nova has a functioning self-hosted infrastructure foundation with many currently running services and a growing operational knowledge base. The most important unfinished work is not adding more tools. It is reducing configuration drift, strengthening recovery coverage, validating observability end to end, and building AI capabilities with evidence and human control.
