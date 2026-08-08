# Messages API

Base URL: `/api/workspace`  
Auth: JWT + `X-Workspace-Id`  
All roles unless noted.

---

## Send an SMS / MMS

```http
POST /api/workspace/outbound-message
Content-Type: application/json

{
  "to": "+14155551234",
  "from": "+18005550100",
  "body": "Hello, this is a follow-up from Callvix.",
  "media_url": "https://..."
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `to` | Yes | Recipient number (E.164) |
| `from` | Yes | Your Twilio number |
| `body` | Yes | Message text (max 1600 chars for SMS; split into segments automatically) |
| `media_url` | No | URL of an image to send as MMS |

**Response `200`:**
```json
{
  "message_sid": "SM1234567890abcdef",
  "status": "sent"
}
```

Credits are deducted from the sending agent's wallet per message.

---

## List conversations

```http
GET /api/workspace/conversations
```

Each conversation groups all messages and calls with a single contact.

**Query params:**

| Param | Type | Description |
|-------|------|-------------|
| `page` | int | Default: 1 |
| `page_size` | int | Default: 20 |
| `search` | string | Search by contact name or number |
| `status` | string | `read` or `unread` |
| `agent_id` | uuid | Filter by agent |

**Response `200`:**
```json
{
  "data": [
    {
      "id": "uuid",
      "contact": {
        "id": "uuid",
        "full_name": "Jane Doe",
        "phone_number": "+14155551234"
      },
      "last_message": {
        "body": "Sure, see you then!",
        "direction": "outbound",
        "created_at": "2026-08-08T09:45:00Z"
      },
      "unread_count": 2,
      "updated_at": "2026-08-08T09:45:00Z"
    }
  ],
  "total": 84,
  "count": 20,
  "per_page": 20,
  "current_page": 1,
  "total_pages": 5
}
```

---

## List communications (calls + messages together)

```http
GET /api/workspace/communications
```

Returns a unified feed of calls and messages for a conversation. Same query params as conversations.

---

## Update a conversation

```http
PATCH /api/workspace/conversation
Content-Type: application/json

{
  "id": "uuid",
  "status": "read"
}
```

Mark a conversation as read or unread.

**Response `200`:** `{ "success": true }`

---

## Conversation notes

Notes are internal team comments on a conversation — not visible to the contact.

### Create a note

```http
POST /api/workspace/conversation/notes
Content-Type: application/json

{
  "conversation_id": "uuid",
  "content": "Customer is on the Pro plan, escalate to billing if needed."
}
```

**Response `201`:** Created note object.

### List notes

```http
GET /api/workspace/conversation/notes?conversation_id={uuid}
```

### Update a note

```http
PATCH /api/workspace/conversation/notes/{id}
Content-Type: application/json

{ "content": "Updated note text." }
```

### Delete a note

```http
DELETE /api/workspace/conversation/notes/{id}
```

**Response `204 No Content`.**

---

## Smart reply suggestion

```http
POST /api/workspace/messages/suggest
Content-Type: application/json

{
  "conversation_id": "uuid",
  "last_message": "I'd like to reschedule my appointment."
}
```

Returns AI-generated reply options based on the conversation history and the agent's knowledge base.

**Response `200`:**
```json
{
  "suggestions": [
    "Of course! What time works best for you?",
    "Happy to help with that. Could you share your availability?",
    "Sure, let me check the calendar. What day were you thinking?"
  ]
}
```
