# Three-Minute Interview Walkthrough

## 1. Twenty-second description

Nova is my private, self-hosted personal operations platform. I built it to learn how infrastructure, observability, automation, documentation, recovery, and responsible AI concepts fit together in a real operating environment. This repository is a sanitized case study, so it explains the work without exposing the live system.

## 2. The operational problem

I had multiple useful services, but I needed more than a collection of containers. I wanted a system I could understand, monitor, recover, and improve. That meant solving configuration drift, making service state visible, documenting dependencies, and creating repeatable recovery practices.

## 3. The architecture

The environment runs on a Windows 11 host with WSL2 and Ubuntu. Docker provides the service layer. Tailscale provides private host-level access. The containers are grouped into access and dashboards, observability, home automation, media operations, credential management, and AI experimentation.

The working observability foundation includes Prometheus, Grafana, Loki, Promtail, Node Exporter, and Uptime Kuma. Home Assistant and a Jellyfin-centered media workflow are also running. Open WebUI is available for experimentation, but I do not describe it as a completed RAG or agent platform.

## 4. What I implemented and learned

I configured and connected the services, investigated differences between source files and live state, created operating and recovery documentation, and worked through real failures. The project taught me to treat source control, runtime evidence, backups, restore testing, access boundaries, and user documentation as connected parts of one operational system.

## 5. Difficult troubleshooting example

One service looked healthy at the container level, but the application inside it was repeatedly exiting through a successful path. I traced the problem to a stale lockfile and a version-specific defect. I ruled out permissions, port conflicts, VPN health, and resource exhaustion, then stopped only the affected component, backed up its state, preserved the evidence, applied the smallest repair, and verified the process, listener, HTTP response, authentication boundary, network relationship, and logs.

That was valuable because it required both technical investigation and operational judgment about what not to change.

## 6. Security and privacy

The public portfolio was written from scratch in a separate directory. The private repository, live configuration, history, service data, network details, credentials, and screenshots are not included. I ran secret scans against the private source areas and the public staging directories before publication.

## 7. What remains incomplete

The infrastructure foundation is much more mature than the AI layer. Nova Core and Nova Awareness are source prototypes, not deployed services. Production RAG memory, embedding and retrieval evaluation, agent routing, MCP tools, and human-approved AI actions remain planned. Backup and observability coverage also need more end-to-end verification.

## 8. Relevance to an AI Business Systems Analyst role

Nova demonstrates how I approach a business-systems problem: discover the actual state, translate ambiguity into a workflow, connect technical and user requirements, document decisions, protect recoverability, and measure the observable result. The AI roadmap also reflects the way I would approach enterprise AI, with clear use cases, governance, human review, permissions, evaluation, and honest status reporting.

## Suggested closing sentence

What I am proudest of is not that Nova contains a long list of tools. It is that I can explain what is working, what is incomplete, why specific decisions were made, and how I would safely take the next step.
