# Contributing to the Agent Intent Protocol (AIP)

Thank you for your interest in improving the Agent Intent Protocol (AIP)! We are currently in the `0.1.0-draft` phase and actively welcome feedback, proposals, and refinements from the community.

## How to Contribute

To ensure a smooth and organized process, please adhere to the following guidelines:

### 1. Discuss Before You Draft
Before submitting a Pull Request that introduces significant architectural changes or new specifications, **please open an Issue first**.
- Use the issue tracker to describe the problem, propose your solution, and gather feedback.
- This ensures that your time is well spent and that the community can weigh in on structural changes to the protocol.

### 2. Submitting Pull Requests
- Once your proposal is discussed and approved in an Issue, feel free to open a Pull Request (PR) against `spec.md`.
- Keep PRs focused on a specific change or improvement.
- Ensure your language aligns with RFC 2119 (e.g., MUST, MUST NOT, SHOULD).
- Reference the related Issue number in your PR description.

### 3. Scope of Contributions
Currently, we are focusing on:
- Refining the core abstractions (`AgentRequest`, `SafetyPolicy`, `OpsLock`).
- Clarifying edge cases and conflict resolution loops.
- Improving the JSON schema documentation in Section 9.
- Example platform bindings (e.g., AWS, GCP, generic REST APIs).

*Note: Reference control plane implementations (like the Kubernetes controller) will be managed in separate repositories when mature.*

### 4. Code of Conduct
Please be respectful and constructive in all discussions. We aim to build a welcoming community pushing the boundaries of safe AI-infrastructure operations.

Thank you for contributing!
