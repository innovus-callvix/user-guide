# Authentication

All API requests require authentication. Callvix supports two authentication methods.

---

## Method 1 — JWT (dashboard / interactive sessions)

Obtain a token by signing in, then pass it on every request.

### Sign in

```http
POST /auth/signin
Content-Type: application/json

{
  "email": "you@example.com",
  "password": "yourpassword"
}
```

**Response `200`:**

```json
{
  "access_token": "eyJ...",
  "refresh_token": "eyJ..."
}
```

The access token is short-lived (**15 minutes**). The refresh token is set as an HTTP-only cookie automatically.

### Use the token

Include it in the `Authorization` header on every request that requires a workspace context, along with the `X-Workspace-Id` header:

```http
GET /api/workspace/contacts
Authorization: Bearer eyJ...
X-Workspace-Id: a536ec61-40c1-4f11-85a4-8b5deba3432f
```

### Refresh the token

When the access token expires, exchange the refresh cookie for a new one:

```http
GET /auth/session
```

The response contains a fresh `access_token`.

### Sign out

```http
POST /auth/logout
```

Clears the refresh cookie. To invalidate all sessions across all devices:

```http
POST /auth/logout-all
Authorization: Bearer eyJ...
```

---

## Method 2 — API Key (server-to-server)

API keys are long-lived workspace credentials for integrations. Pass the key in **one** of these headers:

```http
Authorization: ApiKey cvx_live_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

```http
X-API-Key: cvx_live_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

No `X-Workspace-Id` header is needed — the key is bound to a specific workspace.

See [API Keys](../api/api-keys.md) for how to create and manage keys.

---

## Registration flow

New users register in two steps:

**Step 1 — Send OTP:**

```http
POST /auth/otp/send
Content-Type: application/json

{ "email": "you@example.com" }
```

**Step 2 — Verify OTP:**

```http
POST /auth/otp/verify
Content-Type: application/json

{ "email": "you@example.com", "otp": "123456" }
```

**Step 3 — Complete registration:**

```http
POST /auth/register
Content-Type: application/json

{
  "email": "you@example.com",
  "full_name": "Jane Doe",
  "password": "securepassword"
}
```

---

## Password reset

```http
POST /auth/forgot-password
Content-Type: application/json

{ "email": "you@example.com" }
```

The user receives a reset link by email.

```http
POST /auth/reset-password
Content-Type: application/json

{
  "token": "<reset-token-from-email>",
  "new_password": "newsecurepassword"
}
```

---

## Change password (authenticated)

```http
POST /auth/change-password
Authorization: Bearer eyJ...
Content-Type: application/json

{
  "current_password": "old",
  "new_password": "new"
}
```

---

## Rate limits on auth endpoints

Auth endpoints have a dedicated rate limiter:

- **5 requests / minute per IP** (burst of 5)
- After 5 failed login attempts, the IP is temporarily locked out

Exceeding the limit returns `429 Too Many Requests`.

---

## Error responses

```json
{ "message": "invalid credentials", "status": 401 }
```

| Code  | Meaning                                            |
| ----- | -------------------------------------------------- |
| `401` | Missing, invalid, or expired token / key           |
| `403` | Authenticated but not authorized for this resource |
| `429` | Rate limit exceeded                                |
