# Changelog
All notable changes to the Agent Intent Protocol (AIP) specification will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Added
- **TOCTOU Protection (§3.1.6, §3.6.2)**: Full three-layer defense — OpsLocks (concurrent window), `StateFingerprint` + `EvaluationGeneration` (T1→T2), and `/verify` endpoint (T2→T3).
- **`/verify` endpoint (§4.4)**: Cooperative T2→T3 pre-flight check analogous to `iam:SimulatePrincipalPolicy`. Read-only; completes within `verifyTimeoutMs` (default 200ms); returns HTTP 409 `INVALID_PHASE` if request is not `Approved`.
- **`state.drifted.verify` AuditRecord event**: Distinct from `state.drifted`; emitted on `/verify` failure. Both events carry a `window` field (`"T1T2"` or `"T2T3"`) in `details` for audit differentiation.
- **`plan.timeout` AuditRecord event**: Distinct from `plan.aborted`; emitted when `maxPlanDurationSeconds` is exceeded. Required `details` fields documented in event table.
- **`maxNegotiationRounds`** (default 5): Added alongside `negotiationTimeoutSeconds` to bound negotiating-phase round-trips.
- **`STATE_DRIFTED` denial code**: Emitted when state fingerprint comparison fails at human-approval time.
- **`cascadeDepth` field on SafetyPolicy** (default 3): Caps transitive cascade evaluation hops. 0 disables cascade for that policy.
- **`allowCompensating` on SafetyPolicy rules**: TimeWindow and other non-Deny rules can be bypassed for compensating (rollback) requests.
- **`isCompensating` field on AgentRequest**: Set by control plane only; marks a request as a compensating action.
- **`maxPlanDurationSeconds` on IntentPlan**: REQUIRED for dynamic plans; control plane MUST abort and release locks on timeout.
- **`forGeneration` now required in `humanApproval` schema**: Prevents stale-approval attacks by structurally binding an approval to the epoch at which policy was evaluated.
- **`scopeBounds` schema enforcement**: JSON Schema `allOf` if/then rules now enforce that `scopeBounds` is required when `executionMode: scoped`, and `action` is required when `executionMode: single`.
- **Calibration gaming vector documented**: `calibrationError` excludes Denied requests by design (Denied = governance worked). RBAC is the recommended complement control.
- **Workflow step 6.5 (§8)**: Partner SDK calls `/verify` before executing; on failure, emits `state.drifted.verify` and halts.

### Changed
- **Heartbeat failure response**: SHOULD → **MUST** abort execution and release OpsLocks on missed heartbeat.
- **Cascade denial**: SHOULD → **MUST** deny the primary request when any cascading target triggers a Deny rule. Deny on any target overrides RequireApproval everywhere; not subject to human override.
- **AuditRecord retention default**: Raised from 30 days to **365 days** (SOC 2 / PCI-DSS baseline). FedRAMP (3 years) and HIPAA (6 years) callouts added.
- **CEL policy example**: Fixed to use standard action vocabulary (`request.spec.target.uri.startsWith("k8s://prod")`).

## [0.1.0-draft] - Initial Publication

### Added
- Initial drafting of the `0.1.0-draft` proposal.
- Defined core abstractions: `AgentRequest`, `SafetyPolicy`, and `OpsLock`.
- Defined extended conformance capabilities: `IntentPlan`, execution monitoring, and agent reasoning traces.
- Created schemas for `AgentRequest`, `SafetyPolicy`, `AuditRecord`, `OpsLock`, and `IntentPlan`.
- Established `CONTRIBUTING.md` and basic project scaffolding.
- Emphasized distinguishing between action execution frameworks (like MCP) and infrastructure safety governance frameworks (AIP).
- Documented handling of Priority Inflation in Security Considerations to limit priority exploitation by agents.
