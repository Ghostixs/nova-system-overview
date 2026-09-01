# Observability

Nova's observability layer is designed to answer four practical questions:

1. Is the platform reachable?
2. Are host and service resources changing in a meaningful way?
3. What did a service report before or during a failure?
4. Can the evidence be connected to a documented operating decision?

## Current components

| Component | Role | Status | Verification boundary |
|---|---|---|---|
| Prometheus | Metrics collection | **Working** | Server readiness and three authoritative target classes are verified. |
| Windows exporter | Windows host metrics | **Working** | Current target health is verified; private labels and addresses are withheld. |
| Native Node Exporter | WSL2 Linux host metrics | **Working** | Native service and Prometheus target health are verified. |
| Docker Node Exporter | Container-platform metric perspective | **Working** | Current target health is verified; individual metric coverage is not exhaustively audited. |
| Grafana | Visualization | **Partial** | Runtime and state integrity verified; dashboard and data-source behavior is not fully exercised publicly. |
| Loki | Log storage | **Partial** | Runtime readiness verified; ingestion and retention are not fully verified. |
| Promtail | Log collection | **Partial** | Runtime and log access documented; delivery continuity and collection scope need review. |
| Uptime Kuma | Availability checks | **Working** | Healthy runtime verified; private monitors and notifications are not published. |
| Homepage | Operational navigation | **Working** | Direct readiness verified; private service metadata is omitted. |
| cAdvisor | Additional container metrics | **Planned / absent** | No runtime container; the production boot verifier requires it to remain absent. |

## Public data flow

```text
Windows host metrics ─┐
WSL2 host metrics ────┼─> Prometheus ─> Grafana
Docker host metrics ──┘

Container logs ─> Promtail ─> Loki ─> Grafana
Availability targets ─> Uptime Kuma
Service metadata ─> Homepage
```

## Cold-start convergence

Prometheus can return ready before an exporter has completed its first successful scrape. Nova Boot Recovery therefore separates server readiness from target readiness.

After Prometheus is ready, the verifier polls the three authoritative target classes every five seconds for up to 60 seconds, bounded by the remaining 300-second global deadline. It succeeds immediately when all three are up and cAdvisor remains absent. A final failure report names each target state without logging every poll.

This design was driven by a real cold-boot race rather than a hypothetical requirement.

## Operational lessons

- A running container is not the same as a tested application.
- A ready metrics server is not the same as ready targets.
- A dashboard is only as trustworthy as its source, freshness, and query.
- Logs can improve recovery and also create a privacy risk.
- Alerting without ownership and response guidance creates noise rather than reliability.
- Observability configuration belongs in source control, while runtime logs and service data do not.

## Next verification work

- Validate a small set of decision-focused Grafana dashboards.
- Verify Loki ingestion, retention, and access controls.
- Review Promtail scope so sensitive logs are not collected unnecessarily.
- Test Uptime Kuma notifications and define ownership.
- Reconcile stale cAdvisor declarative intent.
- Add application-native health checks where practical.

## Portfolio privacy

No dashboard screenshots, target addresses, hostnames, labels, or raw reports are published. The public diagrams and status tables communicate architecture and evidence without exposing the operational environment.
