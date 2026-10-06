# Build History

This history highlights verified technical and operational milestones. It is not a claim that Nova has progressed in a straight line. Several milestones exposed drift or recovery gaps that became the next area of work.

<p align="center">
  <img src="../assets/branding/nova-builder-engineering.webp" alt="Illustrated Nova builder actively coding in a purple-lit workspace" width="340">
</p>

## July 2026: Native concepts and early prototypes

- Defined a model-independent direction for Nova Core.
- Built early SQLite-backed knowledge structures.
- Built a Nova Awareness prototype that watched Docker events and published standardized event records through a small in-process event bus.
- Captured historical event records during testing.
- Identified that these components were prototypes, not deployed platform services.

## August 2026: Runtime discovery and documentation baseline

- Inspected the live Docker environment and compared it with available deployment source.
- Documented the running service inventory, architecture, trust boundaries, monitoring stack, storage questions, and verification gaps.
- Separated verified current state from intended architecture and stale project records.
- Identified missing deployment definitions, mutable image tags, incomplete health checks, and uneven recovery coverage.

## August 2026: qBittorrent incident recovery

- Investigated a restart loop that did not present as a normal crash.
- Traced the behavior to a stale single-instance lock and an application-version defect.
- Ruled out permissions, port collision, VPN health, resource exhaustion, and several configuration theories.
- Stopped only the affected service, created and verified an offline state backup, preserved the stale artifact, applied the smallest repair, and ran acceptance checks.
- Later moved the runtime to a pinned image containing the upstream fix.

Read the complete public-safe [case study](case-study-qbittorrent-recovery.md).

## August 2026: Recovery and source-control improvements

- Created and documented recovery artifacts for selected critical services.
- Recorded integrity checks and recovery prerequisites.
- Established the private Git repository and remote source history.
- Recovered and reconciled Caddy routing and network configuration.
- Continued separating runtime data, secrets, backup artifacts, and source-controlled material.

## August 30, 2026: Portfolio verification

- Re-inspected the live runtime rather than relying on older documentation.
- Verified the Windows Tailscale service, WSL2 environment, private repository status, and current Docker inventory.
- Confirmed that 22 Nova service containers were running, plus two unrelated exited test containers.
- Confirmed that the public portfolio source was written in a clean location with new Git history.
- Ran secret scans against private source roots, private Git history, technical documentation, and all public staging files.
- Kept runtime data and backups out of public staging after the scanner confirmed that those private areas contain sensitive material.

## August 31, 2026: Production-validated boot convergence

- Built a thin Windows AtLogOn launcher that delegates verification to WSL2.
- Added a 22-container identity manifest and passive Linux verifier.
- Validated syntax, prohibited-command boundaries, exit-code propagation, and mutation-free execution.
- Used repeated real cold boots to expose independent Docker, proxy-boundary, telemetry-scrape, and VPN-health timing races.
- Replaced fixed assumptions with bounded polling: 150 seconds for Docker, 90 seconds for VPN convergence, 60 seconds for authoritative telemetry, and 300 seconds globally.
- Preserved fail-closed VPN behavior while allowing safe transient convergence.
- Completed final cold-boot validation with exit 0 and no unexpected container recreation.

Read the [Boot Recovery V1 case study](case-study-boot-recovery.md).

## What the history demonstrates

Nova's progress is less about adding the largest possible number of applications and more about improving operational maturity:

- Inspect first
- Preserve state
- Change the smallest necessary component
- Test the observable outcome
- Record limitations
- Keep private information private
- Revisit the source of truth when evidence changes

## September–October 2026: Download Security Gate

The media pipeline evolved from shared filesystem access into distinct staging, validation, release and import boundaries:

1. Durable inventory/ledger and current-versus-historical identity handling established the evidence contract.
2. Filename/type and sandboxed media validation were joined by real ClamAV and trusted Windows Defender evidence.
3. Release enforcement separated validation success from download-client movement and final consumer access.
4. Isolated production staging and a separate release destination removed raw/moving content from media-manager visibility.
5. Production deployment added bounded completion ingress and persistent recovery. An initial attempt exhausted its retry budget and remained preserved.
6. On October 4, scanner preflight and a fresh offline package completed real PASSED → RELEASED on attempt one. Normal restart/replay and bounded VPN failure checks passed. Retained suites: 471 core + 8 deployment tests, zero skips.

That scanner-preflight campaign ended empty of test payloads, without production import or Internet acquisition. Its 8-test count is historical.

7. The later Final Pilot Admission + Sonarr Import Boundary campaign qualified production admission without the offline-only wrapper, resolved the whole-file 16 MiB cutoff through pinned read-only disk input, and released 6.6 MB, 25 MB and 130 MB production-shaped fixtures. Disposable Sonarr copied the 130 MB release read-only with source hash preserved. Retained suites: **471/471 Gate + 26/26 deployment**.

**Production admission and release boundary qualified; one owner-authorized controlled Internet pilot remains.** The production Sonarr transaction remains unapplied, CDH OFF and Internet acquisition NOT PERFORMED in the selected final-admission checkpoint. Documentation was reconciled October 6; no new runtime audit is claimed.

Read [Building a Fail-Closed Media Acquisition Pipeline](case-study-download-security-gate.md). Earlier milestones above retain their original evidence dates.
