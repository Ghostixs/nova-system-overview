# Building a Fail-Closed Media Acquisition Pipeline

[Project overview](../README.md) · [Current state](current-state.md) · [Roadmap](roadmap.md)

**October 4, 2026: deployed and offline-qualified through RELEASED. Internet acquisition remains disabled. The live acquisition pilot is not ready.**

NOVA is my personal infrastructure engineering project across Windows, Linux, WSL2 and Docker. This case study describes how I separated untrusted downloads, validation, release and import. It is an account of a bounded engineering qualification, with explicit limits on what was proved.

## Problem

The original media automation design gave download clients and media managers broad access to a shared filesystem. That made the workflow convenient, but it did not establish a clear point at which downloaded bytes became eligible for import. A scanner result alone could not solve the problem: a consumer that could already read the file might import it before validation or during a move.

I needed a practical workflow that preserved existing library state while making the trust transitions explicit. The design had to fail closed when a parser, scanner, runtime dependency or identity check failed, and retain enough evidence to diagnose and recover without silently approving content.

## Design and boundaries

The deployed portion uses isolated Linux staging, a durable validation ledger and a separate release destination. Media managers cannot see staging or moving release content. The download client performs the supported move; the Gate decides whether the observed result satisfies the release contract.

![Gate sequence with validation, held/rejected outcomes and separate release/import decisions](../diagrams/nova-gate-sequence.svg)

[Open diagram](../diagrams/nova-gate-sequence.svg) · [Mermaid source](../diagrams/nova-gate-sequence.mmd)

The sequence includes future acquisition and import steps so the intended user journey is visible. Its dashed future handoff is not a completed capability.

| Boundary | Decision |
|---|---|
| Untrusted Staging | Inventory exact files while controlling producer writes; consumers have no access. |
| Validation Gate | Accept only current, trusted evidence bound to the package, file identity, policy and attempt. |
| PASSED | Validation succeeded. No move follows merely from this state. |
| RELEASE_PENDING | A separately authorized, durable release intent exists; movement is still in progress. |
| RELEASED | The supported move completed and final identity was reverified. |
| Media Manager / Library | Import needs a separately qualified consumer handoff. |

**PASSED is not release permission. RELEASED is not IMPORTED.** The conceptual journey is `DOWNLOADING → VALIDATING → PASSED → RELEASE_PENDING → RELEASED → IMPORTED`; it omits intermediate Gate states for readability. IMPORTED is a media-manager outcome, not an added Gate state. Incomplete or unsupported evidence results in a hold; adverse evidence prevents progress and requires review.

## Layered validation

The same live package and inventory generation must pass:

1. **Path and inventory checks:** establish the permitted file set and content identity.
2. **Filename/type policy:** correlate naming with actual file evidence.
3. **libmagic:** inspect the file signature through the qualified launcher.
4. **Sandboxed FFprobe:** check supported media structure under bounded input and execution limits.
5. **ClamAV:** require a completed, current, clean result within its supported size range.
6. **Microsoft Defender:** obtain an exact-file result through the trusted Windows boundary.
7. **Final identity revalidation:** confirm that the evidence still describes the bytes being approved.

Runtime resources and scanner definitions are part of that contract. Drift or incomplete execution stops progress. Historical receipts remain available for interpretation and replay, but cannot grant new execution or release authority. Synthetic and imported evidence cannot impersonate a live validator.

Two scanners reduce risk; clean results do not prove absolute safety. Unsupported content stays held rather than being accepted by a fallback assumption.

## The asynchronous move lesson

One important result came from observing the actual cross-filesystem move. The download client's API acknowledged the request before the operation finished. A destination file with the expected final size was already visible while the client still reported moving.

Across **ten moving-state observations**, the Gate stayed in RELEASE_PENDING. It committed RELEASED only after terminal client state, the expected destination and file set, source disposition, and final content identity all satisfied the contract.

This is why the whole release directory must remain hidden from consumers. A final-looking filename, file size or successful HTTP response is insufficient evidence. The proposed import handoff exposes only the exact released package after the decision is durable.

## Failure handling and recovery

The work exposed several ordinary operational failure modes: a library update changed a pinned runtime identity, scanner database layout changed, sandbox startup encountered a resource limit, and production service restrictions blocked a scanner launch. Each stopped validation rather than being converted into approval.

An initial production attempt exhausted its bounded retry budget. I preserved that failed attempt and its history. After scanner preflight demonstrated that the runtime defect was resolved, a separately authorized fresh offline package completed on attempt one with no validator retry. The old attempt was not reset, relabeled or made eligible again.

Normal service restarts were tested at PASSED and RELEASED. The durable ledger survived; PASSED did not trigger an automatic move, and RELEASED did not trigger a duplicate scan or move. A repeated completion signal for an existing package was rejected as new work. These results cover the tested restart/replay cases, not every possible crash or power-loss scenario.

## Verification and current status

| Evidence | Result | Limit |
|---|---|---|
| Canonical isolated core suite | **471/471 passed, zero skips** | Source regression evidence, not deployment approval by itself |
| Separate deployment boundary suite | **8/8 passed, zero skips** | Bounded admission, configuration and producer-control checks |
| Real offline production validation | All mandatory live layers passed; durable PASSED | A disposable single-file fixture within the current parser limit |
| Actual download-client move | RELEASE_PENDING → RELEASED | Controlled offline cross-filesystem move; no Internet media acquisition |
| Normal restart and completion replay | PASSED/RELEASED preserved; no duplicate action | Does not qualify arbitrary interruption modes |
| VPN boundary | Current egress and bounded tunnel-down blocking verified | Tested condition only; no universal network-failure claim |
| Consumer exclusion | No media-manager import; existing media unchanged | Import behavior remains a separate qualification |

The Gate is deployed with persistent state and real completion ingress. Qualification ended with no test torrents or payloads left in staging/release and acquisition disabled. **Offline end-to-end qualification stops at RELEASED.**

The wrapper still admits only the offline fixture convention, and the latest completed qualification used a **16 MiB** probe/admission constraint. Its precise scope and whether it limits the whole file are being investigated; no larger-input production readiness is established. It is not ready for arbitrary movie or episode downloads. ClamAV's engine ceiling remains **2,147,483,647 bytes**, with a slightly lower conservative adapter limit; larger content remains held. Being below that scanner ceiling does not establish parser or package support.

The current engineering campaign is **Final Pilot Admission + Sonarr Import Boundary**. It is in progress, with no completed result yet. Its next gates are production-shaped admission, correct scoping/qualification of the 16 MiB constraint and a read-only, per-package Sonarr import handoff. A compatible item/source, meaningful denial tests, rollback and a no-grab checkpoint must precede explicit owner authorization for one Internet pilot. Automatic acquisition, broader file sets and larger-media policy remain later work.

## Engineering takeaways

- Put trust boundaries in filesystem visibility as well as application settings.
- Treat runtime dependencies, signatures and evidence provenance as part of the input contract.
- Separate asynchronous acknowledgement, completion and consumer access.
- Make retries and recovery preserve history instead of erasing failures.
- Test the actual Windows/WSL/Linux boundary; Unix permissions alone do not establish cross-platform isolation.
- Keep qualification levels visible so a green test suite cannot be mistaken for a finished production workflow.

## Human-governed AI engineering

The owner sets objectives, protected state and authorization boundaries. FORGE/ORION planning roles organize scoped campaigns; Codex assists with implementation, diagnosis, tests and evidence. Each phase has acceptance criteria. Safe in-scope defects use **FIX AND CONTINUE**; accepted milestones use **CHECKPOINT AND CONTINUE**; missing authority or unsafe ambiguity requires **HARD STOP** for the affected scope.

This is an engineering workflow with human review and retained evidence. It does not grant an autonomous agent standing control over production. See [Operations and recovery](operations-and-recovery.md#human-governed-ai-engineering).
