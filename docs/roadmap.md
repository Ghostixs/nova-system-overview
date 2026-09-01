# Roadmap

This roadmap describes direction, not promised delivery dates. A roadmap item remains planned until current implementation evidence proves otherwise.

<p align="center">
  <img src="../assets/branding/nova-builder-roadmap.webp" alt="Illustrated Nova builder beside a Building Nova neon sign" width="720">
</p>

## Current foundation

- Maintain infrastructure stability across Docker and WSL2
- Maintain the production-validated post-logon convergence verifier and its frozen V1 safety boundary
- Continue service recovery and configuration reconciliation
- Expand useful metrics, logs, uptime checks, and operational dashboards
- Reduce drift between runtime, source control, and documentation
- Improve backup coverage, integrity verification, and recovery instructions
- Preserve private networking and clear trust boundaries
- Keep operating procedures understandable and repeatable

## Near term

- Resolve remaining documentation and configuration drift
- Improve Git source-of-truth practices for deployment definitions
- Verify backup coverage and perform isolated restore tests
- Establish failure-domain-separated backup copies for critical state
- Strengthen authentication, secret handling, and privileged integration boundaries
- Review mutable image tags and improve version reproducibility
- Validate monitoring targets, dashboards, retention, and notification paths

## Later

- Build and evaluate a RAG-backed personal memory prototype
- Compare embedding and retrieval approaches with measurable test questions
- Define provenance and confidence behavior for retrieved information
- Explore agent routing without granting uncontrolled action authority
- Evaluate MCP-enabled tools within explicit permission boundaries
- Add human-approved actions with audit logs and rollback paths
- Compare local and cloud model selection for privacy, quality, and cost
- Explore voice and multimodal interfaces
- Explore robotics, Raspberry Pi, wearable, and ambient interfaces

## Gates before AI action capability

Future actions should not move from concept to implementation until these questions have clear answers:

1. What exact problem does the action solve?
2. What data and systems can it access?
3. How are credentials and permissions isolated?
4. What evidence supports the model's decision?
5. What happens when retrieval is incomplete or wrong?
6. Where is human approval required?
7. What is logged, and how is sensitive data protected?
8. How can the action be reversed?
9. How will quality and failure behavior be evaluated?
10. Who owns the handoff when automation stops?

## Explicitly not complete

- Production RAG memory
- Working embedding and retrieval pipeline
- NovaVault persistent AI memory
- Production agent routing
- Completed MCP integration
- Autonomous AI agents
- Human-approved AI actions
- Dependable local-model orchestration
- Finished Discord AI assistant
- Voice-first assistant
- Robotics or wearable integration
