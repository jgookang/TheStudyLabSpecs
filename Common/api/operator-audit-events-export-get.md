## Spec: GET /api/v1/operator/audit/events/export

**Type**: `API Endpoint`  
**Location**: `Common/api/operator-audit-events-export-get.md`  
**Updated**: 2026-03-29  
**Status**: `Ready`

---

### Purpose

> Export filtered audit events as JSON lines for incident timeline and archival workflows.

---

### Endpoint

- GET /api/v1/operator/audit/events/export

---

### Auth

- Operator token header is required.
- Header name default: `x-operator-token`
- Token value comes from backend operator config.
- Origin must be in the configured allowlist.

---

### Query Parameters

- Supports all query parameters from:
- `GET /api/v1/operator/audit/events`
- Additional:
- `format` (optional, currently supports `jsonl`, default `jsonl`)

---

### Response

- `200 OK`
- Content-Type: `application/x-ndjson; charset=utf-8`
- Body: one JSON object per line

```text
{"id":"audit_41","timestamp":"2026-03-29T01:23:24.900Z","event":"auth.refresh","outcome":"failure"}
{"id":"audit_42","timestamp":"2026-03-29T01:23:25.010Z","event":"auth.rate_limit","outcome":"blocked"}
```

---

### Validation Rules

- Unsupported `format` returns `400 INVALID_AUDIT_EXPORT_FORMAT`.
- Invalid query values return `400 INVALID_AUDIT_QUERY`.

---

### Errors

- `400 INVALID_AUDIT_QUERY`
- `400 INVALID_AUDIT_EXPORT_FORMAT`
- `401 OPERATOR_AUTH_REQUIRED`
- `403 OPERATOR_FORBIDDEN`
- `403 ORIGIN_NOT_ALLOWED`

---

### Client Notes

- Recommended for support tooling exports and post-incident trace capture.
