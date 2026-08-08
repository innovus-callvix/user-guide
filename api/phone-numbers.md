# Phone Numbers API

Base URL: `/api/workspace/numbers`  
Auth: JWT + `X-Workspace-Id`

---

## Phone number object

```json
{
  "id": "uuid",
  "workspace_id": "uuid",
  "number": "+14155551234",
  "name": "Sales line",
  "status": "Active",
  "country": { "iso2": "US", "name": "United States", "dial_code": "1" },
  "capabilities": { "voice": true, "sms": true, "mms": true },
  "enable_recording": true,
  "enable_incoming": true,
  "enable_outgoing": true,
  "send_message": "Allowed",
  "forwarding_enabled": false,
  "ivr_enabled": false,
  "voicemail_enabled": true,
  "autoreply_enabled": false,
  "routing_enabled": true,
  "queue_enabled": false,
  "notifications_enabled": true,
  "created_at": "2026-06-01T10:00:00Z"
}
```

---

## List owned numbers

```http
GET /api/workspace/numbers
```

**Query params:**

| Param | Description |
|-------|-------------|
| `page` | Default: 1 |
| `page_size` | 1–100, default: 20 |
| `search` | Search by number or name |
| `country` | ISO2 country code |
| `status` | `Active`, `Expiring`, `Expired` |
| `capability` | `voice`, `sms`, `mms` |

**Response `200`:**
```json
{
  "phone_numbers": [ /* PhoneNumber, … */ ],
  "total": 5,
  "count": 5,
  "per_page": 20,
  "current_page": 1,
  "total_pages": 1
}
```

---

## Get one number

```http
GET /api/workspace/numbers/{id}
```

**Response `200`:** PhoneNumber object.

---

## Browse available numbers — admin+

```http
GET /api/workspace/numbers/available
```

**Query params:**

| Param | Description |
|-------|-------------|
| `country` | ISO2 country code (required) |
| `area_code` | Area code to search within |
| `type` | `local`, `toll-free`, `mobile` |
| `capability` | `voice`, `sms`, `mms` |

**Response `200`:**
```json
{
  "numbers": [
    {
      "phone_number": "+14155550100",
      "friendly_name": "(415) 555-0100",
      "region": "CA",
      "capabilities": { "voice": true, "sms": true }
    }
  ]
}
```

---

## Purchase numbers — admin+

```http
POST /api/workspace/numbers/buy
Content-Type: application/json

{
  "phone_numbers": [
    { "phone_number": "+14155550100", "name": "Sales line" }
  ],
  "price_id": "price_xxx",
  "provider_id": "uuid"
}
```

`phone_number` must be E.164. Charges the workspace subscription or credits.

**Response `200`:** `{ "message": "Phone numbers purchased successfully" }`

---

## Assign agents to a number — admin+

```http
POST /api/workspace/numbers/assignes
Content-Type: application/json

{
  "number_id": "uuid",
  "agent_ids": ["uuid-1", "uuid-2"]
}
```

---

## Get agents assigned to a number

```http
GET /api/workspace/number/agents?number_id={uuid}
```

---

## Get numbers assigned to an agent

```http
GET /api/workspace/assigned/numbers?agent_id={uuid}
```

---

## Select outbound number (agent's default)

```http
POST /api/workspace/number/select
Content-Type: application/json

{ "number_id": "uuid" }
```

```http
GET /api/workspace/number/select
```

---

## Update number name — admin+

```http
PATCH /api/workspace/numbers/{id}/basic
Content-Type: application/json

{ "name": "Support line" }
```

---

## Release a number — admin+

```http
DELETE /api/workspace/numbers/{id}
```

**Response `204 No Content`.** Permanent — the number is returned to Twilio's pool.

---

## Renew an expired number — admin+

```http
POST /api/workspace/numbers/{id}/renew
```

Available during the 7-day grace window after expiry.

---

## Number settings

Each sub-resource follows the pattern `GET /api/workspace/numbers/{id}/{setting}` (all roles) and `PATCH` (admin+).

| Setting | Path suffix |
|---------|-------------|
| Notification & recording | `/notification-settings` |
| Call forwarding | `/forwarding` |
| IVR | `/ivr` |
| Voicemail | `/voicemail` |
| Auto-reply SMS | `/autoreply` |
| Routing | `/routing` |
| Queue | `/queues` |
| Schedule settings | `/schedule/settings` |
| Business hours | `/schedule/business-hours` |
| Holidays | `/schedule/holidays` |

### Example — update voicemail

```http
PATCH /api/workspace/numbers/{id}/voicemail
Content-Type: application/json

{
  "enabled": true,
  "timeout_seconds": 20,
  "greeting_text": "You've reached us after hours. Leave a message."
}
```

### Example — set business hours

```http
PUT /api/workspace/numbers/{id}/schedule/business-hours
Content-Type: application/json

[
  { "day": "monday", "open": "09:00", "close": "17:00" },
  { "day": "tuesday", "open": "09:00", "close": "17:00" },
  { "day": "saturday", "open": null, "close": null }
]
```

A `null` open/close means closed that day.
