## Spec: POST /api/v1/auth/operator/sessions/revoke

**Type**: `API Endpoint`  
**Location**: `Common/api/auth-operator-session-revoke-post.md`  
**Updated**: 2026-03-29  
**Status**: `Ready`

---

### Purpose

> Revoke a single auth session by session id for operator support workflows.

---

### Endpoint

- POST /api/v1/auth/operator/sessions/revoke

---

### Auth

- Operator token header is required.
- Header name default: `x-operator-token`
- Token value comes from backend operator config.
- Origin must be in the configured allowlist.

---

### Request

- Headers:
- `Content-Type: application/json`
- `x-operator-token: <operator-token>`
- JSON body:

```json
{
  "sessionId": "sess_12",
  "reason": "manual_review"
}
```

---

### Response

- `200 OK`
- Body:

```json
{
  "ok": true,
  "sessionId": "sess_12",
  "revoked": true
}
```

---

### Validation Rules

- `sessionId` is required and must be a non-empty string.
- `reason` is optional and defaults to operator revoke reason.
- Revoke is idempotent:
- when a session is already revoked or missing, return `revoked: false`.

---

### Errors

- `400 INVALID_OPERATOR_REVOKE_PAYLOAD`
- `400 INVALID_JSON_PAYLOAD`
- `401 OPERATOR_AUTH_REQUIRED`
- `403 OPERATOR_FORBIDDEN`
- `403 ORIGIN_NOT_ALLOWED`

---

### Client Notes

- Intended for operator/admin tools only.
- Caller should log `revoked: false` outcomes for troubleshooting.
