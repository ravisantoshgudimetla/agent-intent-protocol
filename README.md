# Agent Intent Protocol (AIP) Specification

The Agent Intent Protocol (AIP) establishes a standard governance framework requiring autonomous agents to explicitly declare their intentions before executing actions within managed infrastructure environments. AIP decouples the decision-making of individual agents from the safety, stability guarantees, and auditability of the overall system.

## The Problem

Autonomous infrastructure agents (e.g., LLM-powered SRE agents, auto-remediators) make real-time decisions to scale services, restart workloads, or modify configurations. Without a centralized governance layer, we risk:
- **Conflicting actions** across swarms of agents.
- **Safety invariant violations** (e.g., accidentally deleting a database).
- **Unauditable autonomous actions** making root cause analysis impossible.
- **Cascading failures** from agents lacking broad system visibility.

## The Solution

AIP requires agents to declare intent *before* acting, enabling a control plane to:
- Enforce safety policies.
- Manage concurrency (`OpsLocks`).
- Maintain a comprehensive audit trail of all autonomous infrastructure operations.

While application-layer interaction protocols like MCP (Model Context Protocol) govern *how* an agent discovers and uses tools, AIP governs *whether* an agent is permitted to execute an infrastructure-mutating action.

## Specification

Read the full specification proposal: [spec.md](spec.md).

## Reference Implementations

- **Kubernetes AIP Control Plane**: Currently under active development in another repository. See `examples/` for example Kubernetes Custom Resource bindings (`AgentRequest`, `SafetyPolicy`, `OpsLock`).

## Contributing

We welcome community feedback to refine the AIP specification. Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to participate.

## License

This project is licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for details.

## Disclaimer

This project is an independent, personal initiative. It is not affiliated with, endorsed by, or related to any current or former employer of the contributors. All work here represents the personal views and efforts of the individual contributors in their personal capacity.
