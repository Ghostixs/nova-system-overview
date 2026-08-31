# Build History

This history highlights verified technical and operational milestones. It is not a claim that Nova has progressed in a straight line. Several milestones exposed drift or recovery gaps that became the next area of work.

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

## What the history demonstrates

Nova's progress is less about adding the largest possible number of applications and more about improving operational maturity:

- Inspect first
- Preserve state
- Change the smallest necessary component
- Test the observable outcome
- Record limitations
- Keep private information private
- Revisit the source of truth when evidence changes
