# Case Study: Diagnosing and Recovering a Hidden Restart Loop

## The problem

The download workflow was unavailable even though its container appeared to be running. The application process repeatedly started and disappeared, but Docker did not report a container crash or restart.

This made the first symptom misleading. A container-level status check suggested stability while the user-facing application was never becoming ready.

## Requirements and constraints

- Restore the application without disrupting the healthy VPN gateway.
- Preserve configuration and download state.
- Avoid an unplanned upgrade during incident recovery.
- Keep a clear rollback path.
- Verify the user-facing behavior, not only the container state.

## Discovery and evidence

The investigation compared several evidence sources:

- Container and process-supervisor state
- Application startup behavior and retained logs
- Listener and HTTP readiness
- File ownership and permissions
- Persistent configuration state
- VPN namespace health
- Resource and port availability
- Application version behavior
- Upstream issue and source history

The key clue was that the application exited successfully rather than crashing. The container's supervisor then started it again, creating a loop that Docker's restart counter did not show.

## Root cause

The deployed qBittorrent 5.2.1 build treated a stale single-instance lock as evidence that another local application instance was active. In the container environment, an empty host identifier caused the version's lock comparison to accept the stale record before checking stronger evidence such as the old process or boot information.

The upstream behavior was corrected in a later release.

## Alternatives considered

The investigation tested or reviewed several competing explanations:

- Configuration corruption
- File ownership or permission failure
- Download-path drift
- Web UI configuration mismatch
- Database or session corruption
- Port collision
- VPN gateway failure
- Environment mismatch
- Resource exhaustion

These were either ruled out as the immediate trigger or recorded as separate follow-up issues. Keeping them separate prevented the recovery from turning into a broad, risky change.

## Smallest safe repair

1. Stop only the affected application container.
2. Confirm its application and supervisor processes were stopped.
3. Create and verify an offline backup of the persistent configuration.
4. Move the stale lock into a restricted quarantine location rather than deleting it.
5. Restart the same container without changing the VPN gateway, network, image, paths, or unrelated settings.
6. Run acceptance checks against the process, listener, HTTP response, authentication boundary, namespace attachment, and new logs.

## Verification

The application returned to stable readiness. The process remained present, the Web UI became reachable, the expected authentication boundary responded, the VPN namespace relationship remained intact, and the short restart loop did not recur during the acceptance window.

The original state and lock artifact remained available for rollback and analysis.

## Durable follow-up

The immediate repair did not pretend to fix every contributing issue. The older application version still contained the defect, the image tag needed stronger reproducibility, and broader path questions remained separate.

The current runtime now uses a pinned qBittorrent image containing a newer release. The recovery record remains useful because it explains why the failure was hard to see and how to test for it.

## What this demonstrates

- Requirements discovery under incomplete information
- Evidence-led troubleshooting
- Ability to distinguish container health from application health
- Controlled change scope
- Backup and rollback planning
- Cross-component reasoning across application, storage, process, and network layers
- Clear documentation of verified results and remaining risk
- Judgment about what not to change during an incident

## Relation to business systems analysis

The technical details are specific, but the method is broadly applicable to enterprise systems work. Start with the real user impact, translate ambiguity into testable hypotheses, coordinate around dependencies, preserve recoverability, document the decision, and verify the workflow that matters to the user.
