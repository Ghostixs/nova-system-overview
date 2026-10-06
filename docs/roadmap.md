# Roadmap

[Project overview](../README.md) · [Current state](current-state.md)

Reconciled October 6, 2026 to live owner-driven Level 1 production acceptance. This is a dependency plan, not authorization to act.

## Complete within approved Level 1 scope

- Gate architecture, production deployment and authenticated admission.
- Controlled release, moving-state safety and tested restart/recovery.
- First Internet acquisition, Sonarr import and Jellyfin delivery.
- Level 1 policy and production enablement.
- Production-qualified emergency Level 0 rollback and Level 1 re-entry.
- Installed owner-facing workflow and first live owner-driven production transaction.
- Latest retained aggregate regression: **614 PASS, zero skips**.

## Current normal operation

**LEVEL 1 — OWNER-ATTENDED MANUAL GATED**

**NOVA Media Level 1 is operational in owner-attended, publisher-restricted gated mode.**

The owner personally approves every exact item and separately issues RELEASE only after real Gate validation. Approved publisher inputs and supported mappings only; arbitrary torrents refused; one active transaction; Gate mandatory; emergency stop available.

**INDEXERS DISABLED; RSS OFF; AUTOMATIC SEARCH OFF; RADARR DEFERRED; LEVEL 2 NOT ENABLED.** These controls are the approved policy, not an acceptance failure.

## Current phase: USE AND OBSERVE

The approved implementation campaign is operationally complete. Use the existing mode and observe actual friction. This update starts no new engineering campaign.

## Optional media expansions

- Additional approved publisher/mapping support.
- Subtitle/sidecar support.
- Radarr qualification.
- A >2 GiB media strategy; current support remains below the unchanged scanner ceiling.
- UX improvements identified through actual use.
- Level 2 automation only after a deliberate future owner decision.

None is a blocker to accepted Level 1 operation.

## Later

- Broader application restore and independent recovery coverage.
- More complete health checks, alerts, provisioning and observability retention.
- Separately qualified parser sizes, multifile/sidecar support and large-media policy where justified.
- Evaluated read-only MCP and retrieval, then advanced home automation and voice under human control.
- Nova-native memory, routing and action concepts after meaningful evaluation and permission tests.

These remain separate from accepted Level 1 operation. Prior qualification milestones remain in build history; optional improvements do not reopen the completed implementation campaign. See the [Gate case study](case-study-download-security-gate.md) for the qualification limits.
