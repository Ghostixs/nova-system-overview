# Roadmap

[Project overview](../README.md) · [Current state](current-state.md)

Reconciled October 4, 2026. This is a dependency plan, not authorization to act.

## Completed

- Reconciled service baseline and retained bounded boot-recovery evidence.
- Gate inventory, identity-bound filename/type and media validation, real ClamAV and trusted Defender adapters.
- Private source qualification/checkpoints; canonical 471-test suite and separate 8-test deployment suite passed without skips.
- Isolated production staging, separate release destination, consumer exclusion and Sonarr import hold.
- Bounded production coordinator, persistent ledger, completion ingress and download-client move integration.
- Offline production path through real PASSED and RELEASED, normal restart/replay checks, current VPN routing and bounded tunnel-down blocking.

## Current

**Final Pilot Admission + Sonarr Import Boundary** is in progress. None of its objectives is marked complete; the offline production proof remains the latest accepted milestone.

**Acquisition disabled; live pilot NOT READY.** The deployed wrapper accepts an offline fixture convention, with an unresolved 16 MiB probe/admission constraint whose exact scope is being investigated. Exact live admission and post-RELEASED Sonarr import remain unqualified. The controlled proof does not establish general sub-2-GiB support.

## Next

1. Qualify exact admission and size/file-set fit, plus the read-only per-package Sonarr handoff and rollback. Keep a no-grab checkpoint.
2. With explicit owner authorization, run one interactive acquisition from one approved source; require real validation and RELEASED before import and Jellyfin discovery.
3. Review the pilot, then qualify unattended admission, event/retry/recovery behavior, operator alerts and supported content scope before enabling normal acquisition.

Large or unsupported packages remain held. No automatic RSS/search, broad acquisition or retention deletion follows from the offline result.

## Later

- Broader application restore and independent recovery coverage.
- More complete health checks, alerts, provisioning and observability retention.
- Separately qualified parser sizes, multifile/sidecar support and large-media policy where justified.
- Evaluated read-only MCP and retrieval, then advanced home automation and voice under human control.
- Nova-native memory, routing and action concepts after meaningful evaluation and permission tests.

These remain separate from the current media objective. Safe bounded pilot work should not wait for every possible infrastructure improvement. See the [Gate case study](case-study-download-security-gate.md) for the qualification limits.
