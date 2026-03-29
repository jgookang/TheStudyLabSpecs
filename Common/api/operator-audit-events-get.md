## Spec: GET /api/v1/operator/audit/events

**Type**: `API Endpoint`  
**Location**: `Common/api/operator-audit-events-get.md`  
**Updated**: 2026-03-29  
**Status**: `Ready`

---

### Purpose

> Query recent auth audit events for operator troubleshooting and incident response.

---

### Endpoint

- GET /api/v1/operator/audit/events

---

### Auth

- Operator token header is required.
- Header name default: `x-operator-token`
- Token value comes from backend operator config.
- Origin must be in the configured allowlist.

---

### Query Parameters

- `limit` (optional, integer, default `50`, max `200`)
- `event` (optional, exact match)
- `outcome` (optional, exact match)
- `clientType` (optional, `web` or `mobile`)
- `action` (optional, exact match)
- `userId` (optional, exact match)
- `sessionId` (optional, exact match)
- `from` (optional, ISO timestamp, inclusive)
- `to` (optional, ISO timestamp, inclusive)

---

### Response

- `200 OK`
- Body:

```json
{
  "data": {
    "events": [
      {
        "id": "audit_41",
        "timestamp": "2026-03-29T01:23:24.900Z",
        "event": "auth.refresh",
        "outcome": "failure",
        "clientType": "web",
        "action": "web.refresh",
        "ip": "::1",
        "reason": "REFRESH_SESSION_EXPIRED"
      }
    ],
    "count": 1
  }
}
```

---

### Validation Rules

- Invalid `limit` values return `400 INVALID_AUDIT_QUERY`.
- Invalid timestamps return `400 INVALID_AUDIT_QUERY`.
- Results are ordered by newest first.

---

### Errors

- `400 INVALID_AUDIT_QUERY`
- `401 OPERATOR_AUTH_REQUIRED`
- `403 OPERATOR_FORBIDDEN`
- `403 ORIGIN_NOT_ALLOWED`

---

### Client Notes

- Use narrow filters (especially `event` + `from`) in operator UI for faster triage.
