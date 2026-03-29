## Spec: Backend Phase 2 Plan

**Type**: `Feature`  
**Location**: `Server/features/backend-phase-2-plan.md`  
**Updated**: 2026-03-29  
**Status**: `In Progress`

---

### Purpose

> Define the first implementation slice after Phase 1 closure, focused on durability and security hardening.

---

### Phase 1 Inputs

- Phase 1 implementation steps 1 through 9 are complete.
- Step 9 client finalization commit:
- `bc99fdf chore(smoke): sync web auth paths and refreshed remote fixtures`
- Post-commit remote smoke passed on `http://127.0.0.1:8080`.

---

### Phase 2 Goals

1. Move session/domain state from in-memory runtime assumptions to durable persistence.
2. Enforce session lifecycle guarantees (expiry, revocation, recovery paths).
3. Add baseline auth hardening controls (rate-limit, audit log, operator tooling).
4. Preserve existing API contracts for web/mobile auth and current feature endpoints.

---

### Workstreams

1. Persistence Foundation
- Select storage approach and migration path.
- Introduce repository boundaries for auth/session and mutable feature data.
- Define seed/bootstrap strategy for local and smoke environments.

2. Session Lifecycle Hardening
- Enforce idle + absolute expiry checks on refresh.
- Add revocation lookup/write flow.
- Define logout/logout-all behavior for multi-session states.

3. Auth Security Hardening
- Add per-route rate limits for login/refresh endpoints.
- Capture audit events for auth success/failure and session mutation.
- Define minimal operator/admin revocation workflow.

4. Verification Expansion
- Add persistence-backed integration tests for auth core and transports.
- Add contract tests for `REFRESH_SESSION_*` and expiry/revocation error envelopes.
- Keep remote smoke path green with unchanged endpoint contracts.

---

### Initial Implementation Slice (Recommended)

1. Add pluggable persistence interfaces while keeping current in-memory adapter as fallback.
2. Wire auth core session/token operations through repository interfaces.
3. Add integration tests that run the same auth flow against persistence-backed adapters.
4. Re-run remote smoke and document outcomes in `Clinet/api/remote-smoke-test-results.md`.

---

### Out of Scope for First Slice

- Full analytics/event warehouse ingestion.
- Advanced anomaly detection and risk scoring.
- Multi-region replication.
