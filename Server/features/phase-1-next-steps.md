## Spec: Phase 1 Next Steps

**Type**: `Feature`  
**Location**: `Server/features/phase-1-next-steps.md`  
**Updated**: 2026-03-29  
**Status**: `Done`

---

### Purpose

> Track what is left after backend core implementation so cross-repo rollout can close cleanly.

---

### Current State Summary

- Backend implementation steps 1 through 8 are complete in `TheStudyLabServer`.
- Web/mobile split auth endpoints are implemented and tested.
- Dashboard/read and core mutation endpoints are implemented and tested.
- Remote smoke path has passed with `/api/v1/auth/web/*` endpoints.
- Step 9 cross-repo finalization is complete:
- `TheStudyLab` commit `bc99fdf` finalized smoke script and fixture refresh.
- Post-commit smoke re-run passed on `http://127.0.0.1:8080`.

---

### Phase 1 Closure Checklist (Completed)

1. Finalized Step 9 client repo commit in `TheStudyLab`.
2. Synced `CommonSpecs` smoke runbook/results with latest execution history.
3. Re-ran smoke after final client commit and confirmed no regression.

---

### Next Stage (Phase 2 Kickoff)

1. Define durable persistence strategy for auth/session/domain data.
2. Enforce session lifecycle beyond in-memory runtime (expiry, revocation, recovery).
3. Add auth hardening baseline (rate limits, audit log events, revocation tooling).
4. Expand integration/contract tests for persistence-backed auth flows.
