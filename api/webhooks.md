# Webhooks API

Callvix can send HTTP POST events to your server whenever something happens in your workspace (call completed, SMS received, recording ready, etc.).

Base URL: `/api/workspace/webhooks`  
Auth: JWT + `X-Workspace-Id` — **admin+**

---

## Webhook event object

```json
{
  "id": "uuid",
  "event": "call.completed",
  "workspace_id": "uuid",
  "data": { /* event-specific payload */ },
  "created_at": "2026-08-08T10:00:00Z"
}
```

Callvix signs every request with an `X-Callvix-Signature` header so you can verify authenticity.

---

## Available events

```http
GET /api/workspace/webhooks/events
```

Returns the full list of supported event types.

Common events:

| Event | Trigger |
|-------|---------|
| `call.initiated` | Outbound call started |
| `call.completed` | Call ended (any direction) |
| `call.missed` | Inbound call not answered |
| `call.recording.ready` | Recording URL available |
| `sms.received` | Inbound SMS arrived |
| `sms.sent` | Outbound SMS dispatched |
| `voicemail.received` | Voicemail recorded |
| `contact.created` | New contact added |
| `agent.status.changed` | Agent DND toggled |

---

## Create a webhook endpoint

```http
POST /api/workspace/webhooks
Content-Type: application/json

{
  "url": "https://your-server.com/callvix-hook",
  "events": ["call.completed", "sms.received"],
  "description": "Main CRM sync hook"
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `url` | Yes | HTTPS endpoint to receive events |
| `events` | Yes | Array of event types to subscribe to. Use `["*"]` for all events |
| `description` | No | Internal label |

**Response `201`:**
```json
{
  "id": "uuid",
  "url": "https://your-server.com/callvix-hook",
  "events": ["call.completed", "sms.received"],
  "is_active": true,
  "created_at": "2026-08-08T10:00:00Z"
}
```

---

## List endpoints

```http
GET /api/workspace/webhooks
```

---

## Update an endpoint

```http
PATCH /api/workspace/webhooks/{id}
Content-Type: application/json

{
  "events": ["call.completed", "call.missed", "sms.received"],
  "is_active": true
}
```

---

## Delete an endpoint

```http
DELETE /api/workspace/webhooks/{id}
```

**Response `204 No Content`.**

---

## Send a test event

```http
POST /api/workspace/webhooks/{id}/test
```

Sends a sample payload to your endpoint so you can verify it's working.

**Response `200`:** `{ "delivered": true, "status_code": 200 }`

---

## View delivery logs

```http
GET /api/workspace/webhooks/{id}/logs
```

Returns the last N delivery attempts for this endpoint, including the response status code and body.

**Response `200`:**
```json
{
  "logs": [
    {
      "event": "call.completed",
      "delivered_at": "2026-08-08T10:01:00Z",
      "response_status": 200,
      "duration_ms": 143
    }
  ]
}
```

---

## Verifying webhook signatures

Callvix adds an `X-Callvix-Signature` header to every delivery. To verify:

1. Take the raw request body.
2. Compute `HMAC-SHA256(body, your_webhook_secret)`.
3. Compare with the header value (constant-time comparison).

```go
import (
    "crypto/hmac"
    "crypto/sha256"
    "encoding/hex"
)

func verify(body []byte, secret, signature string) bool {
    mac := hmac.New(sha256.New, []byte(secret))
    mac.Write(body)
    expected := hex.EncodeToString(mac.Sum(nil))
    return hmac.Equal([]byte(expected), []byte(signature))
}
```

---

## Retry policy

If your endpoint returns a non-2xx response or times out (> 10 seconds), Callvix retries with exponential backoff:

| Attempt | Delay |
|---------|-------|
| 1st retry | 30 seconds |
| 2nd retry | 5 minutes |
| 3rd retry | 1 hour |
| 4th retry | 6 hours |

After 4 retries the event is marked as failed and logged.
