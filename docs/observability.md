# Observability

Nova's observability layer is designed to answer four practical questions:

1. Is the platform reachable?
2. Are host and service resources changing in a meaningful way?
3. What did a service report before or during a failure?
4. Can the evidence be connected to a documented operating decision?

## Current components

| Component | Role | Status | Verification boundary |
|---|---|---|---|
| Prometheus | Metrics collection | **Working** | Container and multiple scrape jobs verified; complete target health and retention not fully tested. |
| Node Exporter | Linux host metrics | **Working** | Runtime verified; individual metric coverage not audited. |
| Grafana | Visualization | **Partial** | Runtime verified; data sources and dashboard behavior not fully exercised during this audit. |
| Loki | Log storage | **Partial** | Runtime verified; active ingestion and retention not fully verified. |
| Promtail | Log collection | **Partial** | Runtime and configured log access documented; delivery continuity not fully tested. |
| Uptime Kuma | Availability checks | **Working** | Runtime and healthy container state verified; private monitor targets and notifications not audited. |
| Homepage | Operational navigation | **Working** | Runtime and healthy container state verified; private service metadata omitted. |
| cAdvisor | Additional container metrics | **Planned** | A definition exists, but no current runtime container was found. |

## Public data flow

```text
Host metrics -> Node Exporter -> Prometheus -> Grafana
Container logs -> Promtail -> Loki -> Grafana
Availability targets -> Uptime Kuma
Service metadata -> Homepage
```

Solid runtime presence does not prove that every arrow is continuously healthy. This is why Grafana, Loki, and Promtail remain **Partial** in the public status model.

## Operational lessons

- A running container is not the same as a tested application.
- A dashboard is only as trustworthy as its source, freshness, and query.
- Logs can improve recovery and also create a privacy risk.
- Alerting without ownership and response guidance creates noise rather than reliability.
- Observability configuration belongs in source control, while runtime logs and service data do not.

## Next verification work

- Confirm every intended Prometheus target and target health.
- Validate Grafana data sources and a small set of decision-focused dashboards.
- Verify Loki ingestion, retention, and access controls.
- Review Promtail scope so sensitive logs are not collected unnecessarily.
- Test Uptime Kuma notifications and define who or what should respond.
- Decide whether cAdvisor is still useful or should be removed from intended architecture.

## Portfolio privacy

No dashboard screenshots were published. Screenshots can expose addresses, service names, paths, user identities, or browser context even when the main chart appears safe. The public diagram and status tables communicate the architecture without that risk.
