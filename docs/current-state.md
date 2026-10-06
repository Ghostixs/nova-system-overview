# Current State

Latest Gate evidence: **October 4 final-admission checkpoint**, reconciled **October 6, 2026**. This is dated evidence, not a new live audit. The platform baseline was reconciled September 24. Non-Gate service tables below retain their August 31 scope and were not broadly re-audited for this update.

## How to read this page

**Working** means current runtime evidence supports the component. It does not mean every feature or user journey was tested. When an application had no Docker health check or the complete data flow was not independently exercised, the limitation is stated directly.

No private addresses, hostnames, paths, domains, identifiers, credentials, or application data are included.

## Download Security Gate

| Qualification level | Verified state |
|---|---|
| Source | 471/471 canonical Gate tests and 26/26 deployment/admission tests, zero skips |
| Runtime | Real filename/type, libmagic, FFprobe and both scanners completed for the same live offline package |
| Production topology | Isolated staging, separate release destination and consumer exclusion; Sonarr import handling held |
| Deployment | Bounded coordinator, durable ledger and completion ingress deployed |
| Offline end-to-end | Qualified through RELEASED, including actual move observations and normal restart/replay |
| Production admission | QUALIFIED; pinned read-only disk input resolves the whole-file 16 MiB issue; 6.6 MB, 25 MB and 130 MB production-shaped fixtures reached RELEASED |
| Sonarr release visibility | DESIGN QUALIFIED / NOT YET APPLIED; read-only disposable 130 MB copy preserved source hash |
| Live pilot | READY PENDING OWNER AUTHORIZATION FOR SONARR/PILOT TRANSACTION; Internet acquisition NOT PERFORMED |
| Normal automatic acquisition | Disabled and unqualified |

The completed offline campaign left no test torrents or staging/release payloads. Sonarr imported nothing; existing media was unchanged. Current VPN egress and a bounded tunnel-down fail-closed check passed. An earlier exhausted attempt remains preserved.

**PASSED ≠ RELEASED; RELEASED ≠ IMPORTED.** Files below the scanner ceiling are not automatically supported by the stricter parser/package contract. Large and unsupported content stays held. See the [Gate case study](case-study-download-security-gate.md).

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

| Component | Current evidence | Limit |
|---|---|---|
| Jellyfin | Application-state restore previously verified; playback service retained | No new request-to-Jellyfin pilot completed |
| Jellyseerr | Existing request interface | Acquisition is deliberately disabled |
| Sonarr | Library-only visibility; Completed Download Handling OFF | Read-only disposable copy design qualified; production transaction not yet applied |
| Radarr | Library-only visibility; existing configuration preserved | Outside the first pilot |
| Prowlarr / Arr indexers | Disabled at the final checkpoint | No source or grab authorized by documentation |
| qBittorrent | Attached to isolated staging/release; real completion and move exercised | Production admission qualified beyond 16 MiB; no Internet acquisition at the selected checkpoint |
| Gluetun | Tunnel routing, forwarding synchronization and bounded tunnel-down blocking verified | No claim covering every failure mode |
| Other media support services | Earlier runtime evidence retained | No new feature qualification in this campaign |

## Native Nova software and roadmap

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Nova Awareness | System-context prototype | **In Development** | Source and historical event records were inspected | Not deployed as a dependable service. |
| Nova Core | Model-independent knowledge foundation | **In Development** | Early database and model source was inspected | Incomplete packages and no production deployment. |
| RAG-backed memory | Retrieval-supported personal memory | **Planned** | Design material only | No working embedding or retrieval pipeline is verified. |
| Agent routing and MCP | Model and tool coordination | **Planned** | Roadmap material only | No production router or completed MCP integration is verified. |
| Human-approved AI actions | Controlled automation | **Planned** | Safety principle and roadmap only | Approval, permissions, logging, rollback, and evaluation must be designed first. |

## Current operational truth

NOVA has a reconciled service foundation and a deployed Gate qualified through a controlled offline release. It has not yet restored normal Internet acquisition. Production admission and read-only release visibility design are qualified. The next step is the explicitly authorized single-item Sonarr/pilot transaction. Broader backup/restore and observability gaps remain separate work. See [Roadmap](roadmap.md).
