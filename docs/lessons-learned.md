# Lessons Learned

## The runtime is evidence, not a story

Documentation, source files, and plans can all become stale. A useful systems analyst compares them with the live environment, records the conflict, and avoids rewriting history just to make the sources agree.

## Running is not the same as healthy

A container can be running while its application is failing. The qBittorrent incident demonstrated this clearly: the container remained up while the application repeatedly exited through a successful code path. Verification must include the behavior users depend on.

## Recovery and remediation are different tasks

The safest immediate repair may restore service without resolving the underlying version or architecture problem. Combining recovery, upgrades, path changes, and cleanup into one action makes rollback harder and evidence less clear.

## Preserve evidence before changing state

A backup is useful for recovery. A preserved artifact is also useful for understanding what happened. Moving a stale file to restricted quarantine provided both rollback value and diagnostic evidence.

## A backup is not a recovery capability until it is tested

Creating an archive, checking its integrity, and documenting prerequisites are important steps. They do not prove that the application can be restored in isolation. Restore testing and failure-domain separation remain separate controls.

## Observability should support decisions

Metrics and logs are not valuable because they fill dashboards. They are valuable when they help identify a change, confirm a hypothesis, establish impact, or verify recovery. The next observability improvements should focus on those decisions.

## Security improvements can conflict with availability

Secret migrations, version updates, and access-control changes are worthwhile, but they should not be combined casually with an active incident. A controlled sequence protects both security and service continuity.

## AI labels need evidence

A directory named `memory`, a vector database, or a working chat interface does not prove RAG, dependable retrieval, or an agent system. Honest status language makes the roadmap more credible and makes evaluation easier.

## Startup is convergence, not a timestamp

A user logon, a running WSL2 environment, and a ready Docker engine are separate events. Real cold boots exposed multiple independent races that warm tests did not. Bounded polling with a global deadline produced better evidence than adding a larger fixed delay.

## Preserve stronger safety invariants while waiting

A transient unhealthy VPN signal was not automatically safe or unsafe. The decisive invariant was whether the firewall remained fail-closed while container identity and restart count stayed stable. Readiness allowances should never weaken the control they are waiting to verify.

## Cross-platform loopback assumptions need testing

Linux loopback inside WSL2 did not represent Docker Desktop's Windows-host publication. The correct probe resolved the host boundary dynamically and sent the same hostname/SNI request a client depends on. Network namespaces should be treated as architecture, not an implementation detail.

## Readiness has layers

Prometheus server readiness did not prove that exporters had completed successful scrapes. Separating server readiness from target convergence prevented a false production failure and made the final evidence more precise.

## Documentation is part of user enablement

The best runbook reduces the amount of private context someone needs before acting safely. Writing clear evidence, limitations, acceptance checks, and rollback steps is the technical equivalent of making the system easier to support.

## What I would do differently

- Establish the source repository and deployment-definition rules earlier.
- Define health checks and recovery requirements when adding a service.
- Separate persistent data, configuration, secrets, and logs consistently from the beginning.
- Add fewer services at a time and close the documentation loop before expanding.
- Treat AI evaluation and approval design as foundational requirements, not final polish.
