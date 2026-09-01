# Current State

Last runtime inspection: **August 31, 2026**

## How to read this page

**Working** means current runtime evidence supports the component. It does not mean every feature or user journey was tested. When an application had no Docker health check or the complete data flow was not independently exercised, the limitation is stated directly.

No private addresses, hostnames, paths, domains, identifiers, credentials, or application data are included.

## Platform and access

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Windows | Host operating environment | **Working** | User-confirmed environment and real cold-boot evidence | Host security policy is not published. |
| WSL2 and Ubuntu | Linux engineering and runtime environment | **Working** | Current kernel, systemd, and cold-boot inspection | Exact host identity is withheld. |
| Docker | Container runtime | **Working** | 22 expected persistent containers retained identity through production boot validation | Unrelated test artifacts are excluded from the Nova inventory. |
| Boot Recovery V1 | Passive post-logon convergence verification | **Validated** | Scheduled and real cold-boot tests ended with exit 0 and no unexpected container recreation | Private paths, task principal, and raw reports are withheld. |
| Git and private source | Change history and engineering source | **Working** | Private repository and remote were verified | Working-tree details and private history remain private. |
| Tailscale | Private host-level networking | **Working** | Host-level service and private-access topology verified | Routes, peers, ACLs, addresses, and device names are not published. |
| Homepage | Service navigation | **Working** | Container and direct readiness verified | Private links and service widgets are withheld. |
| Caddy | Reverse proxy | **Working** | Direct and named-route probes passed across the Windows/WSL boundary | Routes and domains are withheld. |
| Portainer | Container administration | **Partial** | Runtime and recovery documentation exist | Privileged access and recovery controls require continued review. |

## Observability

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Prometheus | Metrics collection | **Working** | Server readiness and three authoritative target classes verified, including cold-start convergence | Private target addresses and labels are withheld. |
| Node Exporter | Host metrics | **Working** | Windows, native WSL2, and Docker exporter classes verified through Prometheus | Individual metric coverage is not exhaustively audited. |
| Grafana | Dashboards and visualization | **Partial** | Runtime and database integrity verified | Dashboard and data-source behavior is not fully exercised publicly. |
| Loki | Log storage | **Partial** | Runtime readiness verified | Ingestion, retention, and sensitive-log handling need continued review. |
| Promtail | Log collection | **Partial** | Runtime and log-source access documented | Delivery continuity and collection scope need continued review. |
| Uptime Kuma | Availability monitoring | **Working** | Runtime and healthy container state verified | Monitor targets and notifications remain private. |
| cAdvisor | Additional container metrics | **Planned / absent** | No current runtime container; production verifier requires absence | Historical declarative intent still needs reconciliation. |

## Home, credentials, and AI interface

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Home Assistant | Home automation | **Working** | Application reachability passed production boot verification | Entities, locations, devices, and automations are private. |
| Vaultwarden | Credential management | **Working** | Recovery, upgrade, health, and routed access were validated | Configuration, database content, and recovery material are private. |
| Open WebUI | AI experimentation interface | **Experimental** | Persistent state was recovered and application health is verified | No production RAG, dependable local-model orchestration, or autonomous action claim is made. |

## Media operations

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Jellyfin | Media playback | **Working** | Persistent state, media visibility, and health were recovered and verified | Media, users, libraries, and paths are private. |
| Jellyseerr | Request workflow | **Working** | Application state and directory mappings were reconciled | Request history is private. |
| Sonarr and Radarr | Library management | **Working** | Persistent state, canonical mounts, and application APIs were verified | Library and download details are private. |
| Prowlarr and Bazarr | Indexer and subtitle coordination | **Working** | Persistent state and current dependency topology were verified | Provider configuration is private. |
| qBittorrent | Download client | **Working** | Pinned image, persistent state, canonical mount, Web UI, namespace, and outbound VPN path verified | User data, paths, and network details are private. |
| Gluetun | VPN gateway | **Working** | Native WireGuard, fail-closed firewall, tunnel health, namespace, and bounded boot convergence verified | Provider, endpoint, and credential details are private. |
| Recyclarr and FlareSolverr | Supporting automation services | **Working** | Current runtime presence verified | Schedule and provider details are private; one deployment definition remains unresolved. |

## Native Nova software and roadmap

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Nova Awareness | System-context prototype | **In Development** | Source and historical event records were inspected | Not deployed as a dependable service. |
| Nova Core | Model-independent knowledge foundation | **In Development** | Early database and model source was inspected | Incomplete packages and no production deployment. |
| RAG-backed memory | Retrieval-supported personal memory | **Planned** | Design material only | No working embedding or retrieval pipeline is verified. |
| Agent routing and MCP | Model and tool coordination | **Planned** | Roadmap material only | No production router or completed MCP integration is verified. |
| Human-approved AI actions | Controlled automation | **Planned** | Safety principle and roadmap only | Approval, permissions, logging, rollback, and evaluation must be designed first. |

## Current operational truth

Nova has a functioning self-hosted foundation, a verified multi-layer boot-convergence mechanism, a canonical media workflow, and authoritative host telemetry. The most important unfinished work is reducing remaining source drift, strengthening recovery coverage, improving application-native health checks, and building AI capabilities with evidence and human control.
