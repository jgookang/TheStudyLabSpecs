## Spec: PostgreSQL Smoke Evidence

**Type**: `Ops Note`  
**Location**: `Server/backend/postgres-smoke-evidence.md`  
**Updated**: 2026-03-29  
**Status**: `In Progress`

---

### Purpose

> Track restart-smoke execution status for PostgreSQL persistence mode.

---

### Latest Attempt (Blocked)

- Captured at (UTC): `2026-03-29T06:35:21.378Z`
- Captured at (KST): `2026-03-29 15:35:21`
- Command:
- `npm.cmd run smoke:postgres`
- Input mode:
- `PERSISTENCE_DRIVER=postgres`
- Result:
- failed before runtime validation path due missing `pg` package in sandbox.
- Blocking reason:
- npm dependency install is blocked by sandbox network/permission policy.

---

### Next Successful Run Criteria

- `npm.cmd install` completed in network-enabled environment.
- `npm.cmd run smoke:postgres` returns JSON `"status": "passed"`.
- Restart validation confirms:
- first boot login/mutation success
- second boot refresh success
- persisted dashboard plan status check success

---

### Source of Truth

- Implementation repo evidence:
- `TheStudyLabServer/docs/postgres-smoke-evidence.md`
