# API Keys

API keys give server-to-server access to your workspace without requiring a user session. They inherit the identity and current role of the agent who created them.

> Requires: **admin** or **owner** role. JWT session + `X-Workspace-Id` header.

---

## Create an API key

```http
POST /api/workspace/api-keys
Authorization: Bearer eyJ...
X-Workspace-Id: <workspace-id>
Content-Type: application/json

{
  "name": "Zapier integration",
  "scopes": ["read", "write"],
  "expires_at": "2027-01-01T00:00:00Z"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Human-readable label (max 100 chars) |
| `scopes` | array | No | `read`, `write`, or `*`. Defaults to `["read"]` |
| `expires_at` | ISO 8601 | No | Key expiry. No value = never expires |

**Response `201`:**
```json
{
  "id": "uuid",
  "name": "Zapier integration",
  "key": "cvx_live_a1b2c3d4e5f6...",
  "key_prefix": "cvx_live_a1b2c3",
  "scopes": ["read", "write"],
  "expires_at": "2027-01-01T00:00:00Z",
  "created_at": "2026-08-08T10:00:00Z"
}
```

> **The `key` field is returned exactly once.** Store it securely — it cannot be retrieved again. Only the `key_prefix` is shown in future requests.

---

## List keys

```http
GET /api/workspace/api-keys
Authorization: Bearer eyJ...
X-Workspace-Id: <workspace-id>
```

**Response `200`:**
```json
[
  {
    "id": "uuid",
    "name": "Zapier integration",
    "key_prefix": "cvx_live_a1b2c3",
    "scopes": ["read", "write"],
    "is_active": true,
    "last_used_at": "2026-08-07T14:30:00Z",
    "expires_at": "2027-01-01T00:00:00Z",
    "created_at": "2026-08-08T10:00:00Z"
  }
]
```

Secrets are never included in list responses.

---

## Revoke a key

```http
DELETE /api/workspace/api-keys/{id}
Authorization: Bearer eyJ...
X-Workspace-Id: <workspace-id>
```

**Response `204 No Content`** — revocation is immediate.

---

## Scopes

| Scope | Grants |
|-------|--------|
| `read` | `GET` and `HEAD` requests only |
| `write` | Everything `read` allows + `POST`, `PUT`, `PATCH`, `DELETE` |
| `*` | Full access (any method) |

A `read`-scoped key calling a `POST` endpoint returns `403 — insufficient API key scope: write`.

---

## Accessible endpoints

API keys use a **default-deny** allowlist. Only these endpoints are accessible with an API key — all others return `403` even if the key's role would allow it:

| Method | Path | Min scope | Role |
|--------|------|-----------|------|
| GET | `/api/workspace/contacts` | read | any |
| POST | `/api/workspace/contacts` | write | any |
| DELETE | `/api/workspace/contacts` | write | any |
| GET | `/api/workspace/contacts/{id}` | read | any |
| PUT | `/api/workspace/contacts/{id}` | write | any |
| PATCH | `/api/workspace/contacts/{id}` | write | any |
| GET | `/api/workspace/contacts/phone/{phone}` | read | any |
| GET | `/api/workspace/contacts/export-all` | read | admin+ |
| POST | `/api/workspace/contacts/export` | write | admin+ |
| POST | `/api/workspace/contacts/import` | write | admin+ |
| GET | `/api/workspace/tags/` | read | any |
| POST | `/api/workspace/tags/` | write | any |
| GET | `/api/workspace/tags/{id}` | read | any |
| PUT | `/api/workspace/tags/{id}` | write | any |
| DELETE | `/api/workspace/tags/{id}` | write | any |
| GET | `/api/workspace/numbers` | read | any |
| POST | `/api/workspace/numbers/buy` | write | owner |

---

## Using the key

```bash
curl https://api.callvix.com/api/workspace/contacts \
  -H "Authorization: ApiKey cvx_live_abc123..."
```

Or:

```bash
curl https://api.callvix.com/api/workspace/contacts \
  -H "X-API-Key: cvx_live_abc123..."
```

---

## Rate limits

| Limit | Default | Keyed by |
|-------|---------|----------|
| Global | 20 req/s, burst 40 | Per IP |
| API key surface | 10 req/s, burst 20 | Per key (falls back to IP) |

`429` response includes a `Retry-After` header.

---

## Security notes

- Keys are stored only as a SHA-256 hash — the raw secret is never persisted.
- A leaked key should be **revoked immediately** and replaced.
- Use short `expires_at` values and the narrowest scope needed.
- Max **20 active keys** per workspace.
