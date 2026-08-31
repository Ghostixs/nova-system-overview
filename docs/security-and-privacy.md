# Security and Privacy

## Public repository boundary

This repository was created from newly written public-safe material in a clean staging directory. It does not reuse the private Nova repository or its Git history.

The following categories are intentionally excluded:

- Passwords, API keys, tokens, certificates, and private keys
- Environment files and secret-bearing configuration
- Private addresses, hostnames, domains, routes, and device identities
- Tailscale peer information and private access URLs
- Home Assistant entities, locations, personal data, and automation details
- Application databases, logs, user records, and personal media information
- Backup paths, backup payloads, checksums, and recovery secrets
- Docker socket details and exploit-relevant configuration
- Screenshots containing service URLs, browser context, usernames, or operational data

## Validation performed before publication

- Inspected the private repository state and confirmed it remains private.
- Scanned the private Git history with Gitleaks.
- Scanned the private source roots with Gitleaks.
- Scanned the technical documentation vault with Gitleaks.
- Confirmed that runtime data and backup areas contain sensitive findings and excluded them completely.
- Created the public repositories from clean directories with new Git histories.
- Scanned every public staged file before commit and again before publication.
- Searched public files for private addresses, email addresses, hostnames, URLs, secret patterns, and unsupported AI claims.
- Omitted screenshots and used sanitized SVG and Mermaid diagrams instead.

## Current private-system considerations

The private environment is an active learning system, not a hardened commercial platform. Ongoing work includes:

- Reducing privileged integration exposure
- Reviewing service reachability and host firewall policy
- Improving authentication coverage
- Replacing mutable image tags where practical
- Strengthening secret retirement and rotation practices
- Improving off-host backups and restore testing
- Reconciling missing or stale deployment definitions
- Reviewing log collection and retention for sensitive information

Exact live weaknesses and configuration details are not published because doing so would make the private system easier to attack.

## Responsible AI boundary

Nova does not currently have production RAG, autonomous agents, completed MCP integration, or dependable action orchestration.

Any future AI action design should include:

- Least-privilege permissions
- Explicit user approval
- Clear source provenance
- Confidence and uncertainty handling
- Audit logs that avoid sensitive-data leakage
- Test cases for harmful or incorrect behavior
- Human handoff rules
- Reversible actions and recovery procedures

## Safe example policy

Files under `examples/` are synthetic. Their service names, ports, networks, volumes, and placeholder values do not represent the private deployment.
