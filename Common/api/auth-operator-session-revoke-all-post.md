## Spec: POST /api/v1/auth/operator/sessions/revoke-all

**Type**: `API Endpoint`  
**Location**: `Common/api/auth-operator-session-revoke-all-post.md`  
**Updated**: 2026-03-29  
**Status**: `Ready`

---

### Purpose

> Revoke every active session for one user, optionally scoped by client type.

---

### Endpoint

- POST /api/v1/auth/operator/sessions/revoke-all

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
  "userId": "u1",
  "clientType": "web",
  "reason": "security_reset"
}
```

---

### Response

- `200 OK`
- Body:

```json
{
  "ok": true,
  "userId": "u1",
  "clientType": "web",
  "revokedCount": 2,
  "revokedSessionIds": ["sess_7", "sess_8"]
}
```

---

### Validation Rules

- `userId` is required and must be a non-empty string.
- `clientType` is optional and when present must be `web` or `mobile`.
- `reason` is optional and defaults to operator revoke-all reason.
- User must exist in auth domain; unknown user returns explicit not found.

---

### Errors

- `400 INVALID_OPERATOR_REVOKE_ALL_PAYLOAD`
- `400 INVALID_JSON_PAYLOAD`
- `401 OPERATOR_AUTH_REQUIRED`
- `403 OPERATOR_FORBIDDEN`
- `403 ORIGIN_NOT_ALLOWED`
- `404 OPERATOR_USER_NOT_FOUND`

---

### Client Notes

- Use for account takeover response or forced re-auth workflows.
- Keep the returned revoked id list in operator audit trail systems.
