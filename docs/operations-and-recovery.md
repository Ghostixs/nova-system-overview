# Operations and Recovery

Nova is most useful to me when it behaves like an operational system rather than a collection of containers. That means a change is not finished when a service starts. It is finished when the result is verified, the recovery path is understood, and the evidence is documented.

## Change workflow

1. Inspect the relevant runtime, source, and documentation.
2. Identify conflicts and unknowns before choosing a fix.
3. Define the smallest reasonable change.
4. Preserve state and record a rollback path.
5. Change only the affected component.
6. Verify application behavior, not only container state.
7. Record the result, remaining limitations, and next safe step.

## Recovery posture

The private environment contains documented recovery artifacts and procedures for selected services. During prior work, backups were created before risky repairs and checked for integrity, structure, permissions, or required state.

The current posture remains **Partial** because:

- Not every service has equivalent coverage.
- Some recovery artifacts remain in the same failure domain as the live system.
- Not every backup has passed an isolated application restore test.
- Some deployment definitions and runtime state still need reconciliation.
- Recovery evidence can itself contain sensitive data and must remain private.

## A real troubleshooting example

The qBittorrent recovery case is the clearest example of the operating method.

A container appeared to be running, but the application inside it was repeatedly exiting successfully and restarting under its process supervisor. The investigation compared process behavior, application logs, file state, version behavior, permissions, network conditions, and upstream source information.

The repair stopped only the affected service, created and checked an offline backup, preserved the stale lock artifact rather than deleting evidence, restarted the existing container, and verified continuous process, listener, HTTP, authentication-boundary, VPN-namespace, and log behavior.

Read [Case study: qBittorrent recovery](case-study-qbittorrent-recovery.md).

## Recovery controls I am improving

- Failure-domain-separated backup copies
- Isolated restore testing
- Deployment definition coverage
- Version pinning and reconstruction evidence
- Clear ownership and permissions on recovery material
- Runbooks that separate emergency recovery from broader upgrades
- Verification criteria that another person can follow

## Why this matters beyond a homelab

The same habits apply to enterprise systems work:

- Translate an ambiguous symptom into a testable problem.
- Coordinate around risk and impact.
- Distinguish immediate recovery from long-term remediation.
- Protect user and system data.
- Communicate what was verified and what remains unknown.
- Create a repeatable process instead of relying on memory.
