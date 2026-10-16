# Current State

Latest evidence: **October 16, 2026 — media client experience live; playback analytics live; full media automation and Nova AI memory core operational**. The October 15-16 media experience pass added skip intro/credits, scrub previews, hover trailers, always-on subtitles, a three-shelf recommendation layer, playback analytics, dashboard media cards, and new-media notifications. The Gate remains stopped and latched as retained evidence.

## How to read this page

**Working** means current runtime evidence supports the component. It does not mean every feature or user journey was tested. When an application had no Docker health check or the complete data flow was not independently exercised, the limitation is stated directly.

No private addresses, hostnames, paths, domains, identifiers, credentials, or application data are included.

## Media pipeline: full automation (supersedes attended Level 1)

**The owner approved full automation on October 10, 2026.** The complete chain ran unattended end-to-end: request interface → indexer search → movie/TV managers → VPN-bound download client → automatic import → media server.

| Status | Current scope |
|---|---|
| Mode | **FULL AUTOMATION (owner-approved)** |
| Chain | Request interface → indexer → managers → VPN-bound client → auto-import → media server |
| Verified | Six titles auto-imported October 10; deletion removes files from disk; automatic re-acquisition after deletion works |
| Seeding | Ratio target with no time cap; completed downloads retained for seeding after import |
| TV backlog | Resumed; 30+ queued items flowing |
| Gate | **RETIRED (owner decision 2026-10-11)** — service stays stopped; evidence and audit chain retained in place |
| Regression | The 614-test Gate suite belongs to the retired attended flow; the automated path has no formal regression suite yet (stated limitation) |

The attended Gate flow, its 614 PASS / zero skips regression, and the owner-driven Gran Dillama transaction remain documented in the Gate case study as historical evidence. They describe a superseded operating mode, not current operation.

## Media client experience (built October 15-16, 2026)

The pipeline below was already automated. This pass made the media server behave like a product.

| Area | Status | Evidence | Public-safe limitation |
|---|---|---|---|
| Skip intro/credits | **Live** | Audio-fingerprint analyzer writes segments into the native media-segment API; scheduled daily; initial pass verified running; skip buttons verified active in the client | Segment accuracy per show varies; credits detection is noisier than intros |
| Scrub previews and chapter images | **Live** | Native trickplay and chapter-image extraction enabled per library through the API; generation verified complete | Storage cost grows with library size |
| Hover trailers | **Live** | Hover-preview plugin active; library identification pass completed: all 29 films identified, 24 with trailer links, 18 of 20 series with trailer links; five films are new releases with no trailers indexed upstream | Hover previews are a web-client feature only |
| Subtitles | **Live** | User policy: always on, English preferred. Automation: quality-scored English-only pipeline, default-on for all movies and series, automatic text-format upgrades, six-hour schedule | A few niche titles have no published English subtitles; a local transcription fallback is a future option |
| Recommendation layer | **Live** | Scrobble history feeds three virtual shelves (50 movie + 50 show recommendations browsable in-app) plus a next-seasons shelf; a privacy-first local engine and a ratings/diary plugin are also installed; scrobble provider excludes the virtual shelves | Recommendation quality depends on watch history volume |
| Playback analytics | **Working** | Analytics service (app + own database) ingests playback reporting: watch time, top titles, device mix, live sessions; local-only exposure | Database backups follow the existing uneven backup coverage |
| Dashboard media cards | **Live** | Continue-watching and recently-added cards served from the deterministic status writer; verified rendering live data | Card data refreshes on the status writer's schedule, not in real time |
| New-media notifications | **Live** | Poster-art notifications wired to the owner's chat surface | Notification scope configurable per event type |

Read the full [media experience case study](case-study-media-experience.md).

## Nova AI core

**The owner declared October 11, 2026: the personal assistant runs on a self-hosted agent runtime as chief of staff + memory core.**

| Component | Status | Evidence |
|---|---|---|
| Daily facts pass | **Live** | Deterministic script writes a facts snapshot every morning (07:00 local); verified writes + archive rotation |
| Daily synthesis | **Live** | AI session (separately-billed open model) writes the morning brief + ranked attention queue (07:15); merge is guard-enforced; verified output |
| Dashboard surface | **Live** | Brief served to intelligence cards via the local reverse proxy; all cards verified returning data |
| Chronicle (event ledger) | **Live** | Append-only JSONL; 23 events seeded (commits + decisions); events never edited, corrections are new events |
| Codex (fact lifecycle) | **Live** | Facts carry current/uncertain/superseded/expired states; supersede-never-delete audit trail; human-readable sync into the knowledge vault |
| Atlas (entity index) | **Live** | Deterministic scan of the knowledge vault; 77 notes → 67 entities |
| Wisdom (patterns) | **Live** | Evidence-linked distilled patterns; advisory only, never auto-applied; distilled on the Sunday weekly pass |
| Evidence enforcement | **Live** | Every attention item must carry a source; source-less items refused at merge (verified exit code) |
| Weekly review | **Live** | Sunday pass: second-brain review + Atlas rebuild + Wisdom distill |

All memory layers are file-based, guard-enforced (writes outside the designated data dirs are refused), stdlib-only, and stored locally. No external memory provider or cloud service is involved; model usage is a separately-billed open model, not the owner's subscription quota.

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
| Jellyfin | Six titles auto-imported October 10; existing media/history preserved; deletion verified to remove files from disk | Delivery is an automated-pipeline claim scoped to the verified run |
| Jellyseerr | Live request interface feeding the automated chain | Verified for the October 10 automation run; edge cases (partial seasons, quality overrides) not exhaustively tested |
| Sonarr | Live TV manager; backlog resumed; imports verified | Verified for the automation run; long-term queue behavior observed, not stress-tested |
| Radarr | Live movie manager; six auto-imports October 10 | Verified for the automation run |
| Prowlarr / Arr indexers | Live indexer search feeding the automation | Indexer health verified by live search |
| qBittorrent | VPN-bound acquisition verified; seeding preserved with ratio target and no time cap | No claim covering every failure mode |
| Gluetun | Tunnel routing, forwarding synchronization and bounded tunnel-down blocking verified | No claim covering every failure mode |
| Other media support services | Earlier runtime evidence retained | No new feature qualification in this campaign |

## Native Nova software and roadmap

| Component | Purpose | Status | Evidence used | Public-safe limitation |
|---|---|---|---|---|
| Nova AI (agent core) | Personal assistant: chief of staff + memory core | **Live** | Owner-declared identity; daily facts→synthesis→dashboard loop verified; weekly review verified | Read-mostly: writes only guarded data files and the brief; no autonomous system actions |
| Chronicle | Append-only event ledger | **Live** | 23 events seeded; append-only behavior verified | Local file storage; no external replication |
| Codex | Fact lifecycle store | **Live** | current/uncertain/superseded/expired states verified with supersession audit trail | Local file storage; human sync into knowledge vault |
| Atlas | Entity index over knowledge vault | **Live** | 77 notes → 67 entities verified | Local file storage |
| Wisdom | Evidence-linked patterns | **Live** | Distilled entries verified; advisory-only rule enforced in prompts | Pattern quality depends on event volume |
| Nova Awareness | System-context prototype | **Historical** | Source and historical event records were inspected | Superseded by the live facts/synthesis pipeline |
| Nova Core | Model-independent knowledge foundation | **Historical** | Early database and model source was inspected | Superseded by the live memory layers |
| RAG-backed memory | Retrieval-supported personal memory | **Planned** | Design material only | No working embedding or retrieval pipeline is verified. |
| Agent routing and MCP | Model and tool coordination | **Planned** | Roadmap material only | No production router or completed MCP integration is verified. |
| Human-approved AI actions | Controlled automation | **Planned** | Safety principle and roadmap only | Approval, permissions, logging, rollback, and evaluation must be designed first. |

## Current operational truth

Full media automation is live (owner-approved October 10) and the Nova AI memory core is operational (verified October 10-11). The attended Gate flow is superseded and the Gate is RETIRED (owner decision 2026-10-11) — the owner chose RETIREMENT on October 11, 2026 (evidence retained). The automation path has no formal regression suite yet; backup/observability gaps remain separate. See [Roadmap](roadmap.md).
