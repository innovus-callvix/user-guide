# Calls API

Base URL: `/api/workspace`  
Auth: JWT + `X-Workspace-Id`  
All roles unless noted.

---

## Make an outbound call

```http
POST /api/workspace/outbound-call
Content-Type: application/json

{
  "to": "+14155551234",
  "from": "+18005550100",
  "agent_id": "uuid"
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `to` | Yes | Destination number (E.164) |
| `from` | Yes | Your Twilio number to call from |
| `agent_id` | Yes | Agent initiating the call |

**Response `200`:**
```json
{
  "call_sid": "CA1234567890abcdef",
  "status": "initiated"
}
```

Credits are deducted from the agent's wallet per minute once the call is answered.

---

## List calls

```http
GET /api/workspace/calls
```

**Query params:**

| Param | Type | Description |
|-------|------|-------------|
| `page` | int | Page number (default: 1) |
| `page_size` | int | 1–100 (default: 20) |
| `direction` | string | `inbound` or `outbound` |
| `status` | string | `completed`, `missed`, `failed`, `no-answer`, `busy`, `in-progress` |
| `agent_id` | uuid | Filter by agent |
| `phone_number` | string | Filter by workspace number |
| `from_date` | date | `YYYY-MM-DD` |
| `to_date` | date | `YYYY-MM-DD` |
| `search` | string | Search by caller number |

**Response `200`:**
```json
{
  "data": [
    {
      "call_sid": "CA...",
      "direction": "outbound",
      "status": "completed",
      "from": "+18005550100",
      "to": "+14155551234",
      "duration": 142,
      "billing_duration": 180,
      "started_at": "2026-08-08T10:00:00Z",
      "ended_at": "2026-08-08T10:02:22Z",
      "agent_id": "uuid",
      "agent_name": "Jane Doe",
      "note": "",
      "has_recording": true,
      "has_transcript": true
    }
  ],
  "total": 530,
  "count": 20,
  "per_page": 20,
  "current_page": 1,
  "total_pages": 27
}
```

---

## Start call recording

```http
POST /api/workspace/calls/{call_sid}/recording/start
```

Starts recording an in-progress call. Recording must be enabled on the number.

**Response `200`:** `{ "success": true }`

---

## Stop call recording

```http
POST /api/workspace/calls/{call_sid}/recording/stop
```

**Response `200`:** `{ "success": true }`

---

## Get transcript

```http
GET /api/workspace/calls/{call_sid}/transcript
```

Returns the auto-generated word-by-word transcript for a completed call.

**Response `200`:**
```json
{
  "call_sid": "CA...",
  "transcript": [
    { "speaker": "agent", "text": "Hello, how can I help?", "timestamp": 0.5 },
    { "speaker": "customer", "text": "I need help with my account.", "timestamp": 3.1 }
  ]
}
```

Returns `404` if no transcript exists for the call.

---

## Get or create call summary

```http
POST /api/workspace/calls/{call_sid}/summary
```

Returns an existing AI-generated summary, or creates one if it doesn't exist yet.

**Response `200`:**
```json
{
  "call_sid": "CA...",
  "summary": "The customer called about a billing issue. Agent confirmed the account and escalated to billing team.",
  "created_at": "2026-08-08T10:05:00Z"
}
```

---

## Update call note

```http
PATCH /api/workspace/calls/{call_sid}/note
Content-Type: application/json

{ "note": "Follow up scheduled for Friday." }
```

**Response `200`:** `{ "success": true }`

---

## Live calls (prefeed)

```http
GET /api/workspace/live-calls/prefeed
```

Returns the current snapshot of all active calls in the workspace. Used to initialise the live monitor before WebSocket updates begin.

**Response `200`:**
```json
{
  "calls": [
    {
      "call_sid": "CA...",
      "direction": "inbound",
      "status": "in-progress",
      "from": "+14155551234",
      "agent_id": "uuid",
      "agent_name": "Jane Doe",
      "started_at": "2026-08-08T10:00:00Z"
    }
  ]
}
```
