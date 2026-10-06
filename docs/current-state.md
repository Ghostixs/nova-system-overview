# Current State

Latest media evidence: **October 6, 2026 — live owner-driven Level 1 production acceptance**. This documentation update uses retained acceptance evidence; it is not a separate new runtime audit. The platform baseline was reconciled September 24. Non-Gate service tables below retain their August 31 scope and were not broadly re-audited for this update.

## How to read this page

**Working** means current runtime evidence supports the component. It does not mean every feature or user journey was tested. When an application had no Docker health check or the complete data flow was not independently exercised, the limitation is stated directly.

No private addresses, hostnames, paths, domains, identifiers, credentials, or application data are included.

## NOVA Media Level 1

**NOVA Media Level 1 is operational in owner-attended, publisher-restricted gated mode.**

**Live owner-driven acquisition, validation, release, import and Jellyfin delivery verified.**

| Status | Current accepted scope |
|---|---|
| Mode | **LEVEL 1 — OWNER-ATTENDED MANUAL GATED** |
| Owner workflow | **LIVE PRODUCTION ACCEPTED** through installed Windows operator interface |
| Per-item APPROVE / post-validation RELEASE | **REQUIRED / REQUIRED** |
| Gate security authority | **PRESERVED** |
| Sonarr import / Jellyfin / cleanup | **VERIFIED** for the owner-approved Gran Dillama transaction |
| Emergency stop | **PRODUCTION QUALIFIED** |
| Latest regression | **614 PASS, zero skips**: 471 Gate + 26 deployment + 30 policy/stop + 8 import evidence + 79 owner workflow |
| Indexers / RSS / automatic search | **DISABLED / OFF / OFF** |
| Radarr / Level 2 | **DEFERRED / NOT ENABLED** |
| Normal Level 1 use / current phase | **READY / USE AND OBSERVE** |

Approval applies only to the exact reviewed item. No acquisition precedes APPROVE; no release precedes genuine Gate PASSED and personal RELEASE. One transaction, approved publisher inputs and supported mappings only; arbitrary torrents refused. Automatic discovery remains intentionally disabled.

The recorded clean resting state has zero torrents/transient payloads, restored Sonarr staging/release exclusion and Completed Download Handling OFF. Canonical media and Gate evidence remain. Failed first attempt, separately authorized recovery and fresh-approved success are preserved as distinct events.

Earlier architecture/admission, >16 MiB fixtures, release safety, restart/recovery and disposable import qualification remain historical foundations. The unchanged scanner ceiling holds oversized content; no >2 GiB support is claimed. See the [Gate / NOVA Media case study](case-study-download-security-gate.md).

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
| Jellyfin | Owner-approved Gran Dillama import and delivery verified; existing media/history preserved | Delivery is not an autonomous or general catalogue acquisition claim |
| Jellyseerr | Existing request interface retained | Accepted acquisition uses the installed owner workflow; automated discovery remains disabled |
| Sonarr | Exact released-package import production-verified; library-only resting visibility; CDH OFF after cleanup | No staging visibility; temporary read-only exposure only after durable RELEASED |
| Radarr | Existing configuration preserved | Acquisition DEFERRED; outside accepted Level 1 scope |
| Prowlarr / Arr indexers | Disabled at the final checkpoint | No source or grab authorized by documentation |
| qBittorrent | Real owner-approved Internet acquisition and controlled release verified; zero resting torrents | One supported transaction; personal APPROVE and RELEASE; arbitrary torrents refused |
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

NOVA Media Level 1 is operational within approved attended publisher/mapping scope. The implementation campaign is complete for that scope; use and observe actual friction before optional expansion. Indexers/RSS/search stay disabled, Radarr deferred and Level 2 not enabled by policy. Broader platform backup/observability gaps remain separate. See [Roadmap](roadmap.md).
