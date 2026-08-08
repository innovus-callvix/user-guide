# AI Agents API

Base URL: `/api/workspace/ai`  
Auth: JWT + `X-Workspace-Id`  
All roles unless noted.

---

## AI Agent object

```json
{
  "id": "uuid",
  "workspace_id": "uuid",
  "name": "Support Bot",
  "greeting": "Hello! I'm the Callvix support assistant. How can I help you today?",
  "system_prompt": "You are a helpful support agent for Callvix. Answer questions about our VoIP plans...",
  "voice": "aura-2-amalthea-en",
  "language": "en",
  "status": "published",
  "knowledge_bases": ["uuid-1", "uuid-2"],
  "created_by": "uuid",
  "created_at": "2026-08-01T10:00:00Z",
  "updated_at": "2026-08-01T10:00:00Z"
}
```

---

## List available voices

```http
GET /api/workspace/ai/voices
```

**Response `200`:**
```json
{
  "voices": [
    { "id": "aura-2-amalthea-en", "name": "Amalthea", "language": "en", "gender": "female" },
    { "id": "aura-2-orion-en", "name": "Orion", "language": "en", "gender": "male" }
  ]
}
```

---

## Create an agent

```http
POST /api/workspace/ai/agents
Content-Type: application/json

{
  "name": "Support Bot",
  "greeting": "Hello! How can I help you today?",
  "system_prompt": "You are a helpful assistant for Acme Corp...",
  "voice": "aura-2-amalthea-en",
  "language": "en",
  "knowledge_base_ids": ["uuid-1"]
}
```

**Response `201`:** AI Agent object.

---

## List agents

```http
GET /api/workspace/ai/agents
```

---

## Get an agent

```http
GET /api/workspace/ai/agents/{agent_id}
```

---

## Update an agent

```http
PUT /api/workspace/ai/agents/{agent_id}
Content-Type: application/json

{
  "name": "Support Bot v2",
  "system_prompt": "Updated instructions..."
}
```

**Response `200`:** Updated AI Agent object.

---

## Delete an agent

```http
DELETE /api/workspace/ai/agents/{agent_id}
```

**Response `204 No Content`.**

---

## Publish / unpublish

An agent must be published before it can handle real calls.

```http
POST /api/workspace/ai/agents/{agent_id}/publish
```

```http
POST /api/workspace/ai/agents/{agent_id}/unpublish
```

---

## Test an agent (browser voice session)

```http
POST /api/workspace/ai/agents/{agent_id}/test
```

Returns a signed WebSocket URL. Connect to it from the browser to start a voice test session.

**Response `200`:**
```json
{
  "ws_url": "wss://ai-worker.callvix.com/ws/test?agent_id=...&token=..."
}
```

Connect your browser's microphone to the WebSocket. Send binary PCM (16 kHz int16). Receive binary WAV audio back.

---

## Dispatch an outbound AI call

```http
POST /api/workspace/ai/agents/{agent_id}/outbound
Content-Type: application/json

{
  "to": "+14155551234",
  "from": "+18005550100"
}
```

The AI agent will call the number and handle the conversation autonomously.

---

## Assign agent to a phone number — admin+

```http
POST /api/workspace/ai/agents/{agent_id}/numbers
Content-Type: application/json

{ "number_id": "uuid" }
```

---

## Unassign from a number — admin+

```http
DELETE /api/workspace/ai/agents/{agent_id}/numbers/{number_id}
```

---

## Get assignment for a number

```http
GET /api/workspace/numbers/{number_id}/ai-agent
```

---

## Knowledge Bases

### Create

```http
POST /api/workspace/ai/knowledge-bases
Content-Type: application/json

{ "name": "Product FAQ" }
```

**Response `201`:**
```json
{
  "id": "uuid",
  "name": "Product FAQ",
  "document_count": 0,
  "status": "ready",
  "created_at": "2026-08-08T10:00:00Z"
}
```

### List

```http
GET /api/workspace/ai/knowledge-bases
```

### Get one

```http
GET /api/workspace/ai/knowledge-bases/{kb_id}
```

### Delete

```http
DELETE /api/workspace/ai/knowledge-bases/{kb_id}
```

---

## Documents

### Upload a file

```http
POST /api/workspace/ai/knowledge-bases/{kb_id}/documents
Content-Type: multipart/form-data

file=@terms.pdf
```

Accepted: PDF, DOCX, TXT. Max 50 MB.

**Response `201`:**
```json
{
  "id": "uuid",
  "name": "terms.pdf",
  "status": "processing",
  "created_at": "2026-08-08T10:00:00Z"
}
```

Status transitions: `processing` → `ready` (or `failed`). Poll `GET /documents` to check.

### Add a website URL

```http
POST /api/workspace/ai/knowledge-bases/{kb_id}/documents/url
Content-Type: application/json

{ "url": "https://yourcompany.com/faq" }
```

Callvix crawls and indexes the page content.

### Get presigned upload URL (for large files)

```http
GET /api/workspace/ai/knowledge-bases/{kb_id}/documents/presign?filename=large.pdf
```

Upload directly to S3 using the presigned URL, then call the documents endpoint to register.

### List documents

```http
GET /api/workspace/ai/knowledge-bases/{kb_id}/documents
```

### Delete a document

```http
DELETE /api/workspace/ai/knowledge-bases/{kb_id}/documents/{doc_id}
```
