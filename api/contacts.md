# Contacts API

Base URL: `/api/workspace/contacts`  
Auth: JWT + `X-Workspace-Id` **or** API Key  
All roles unless noted.

---

## Contact object

```json
{
  "id": "uuid",
  "workspace_id": "uuid",
  "full_name": "Jane Doe",
  "phone_number": "+14155551234",
  "code": "US",
  "email_address": "jane@example.com",
  "address": "1 Market St, San Francisco, CA",
  "company": "Acme Corp",
  "note": "Prefers SMS",
  "status": "active",
  "image_url": "https://...",
  "tags": [{ "id": "uuid", "name": "VIP", "color": "#ff0000" }],
  "created_by": { "id": "uuid", "name": "Agent Name" },
  "created_at": "2026-08-01T10:00:00Z",
  "updated_at": "2026-08-01T10:00:00Z"
}
```

---

## List contacts

```http
GET /api/workspace/contacts
```

**Query params:**

| Param | Type | Description |
|-------|------|-------------|
| `page` | int | Page number (default: 1) |
| `page_size` | int | 1–100 (default: 10) |
| `search` | string | Name, phone, email, or company |
| `status` | string | `active` or `blocked` |
| `created_by` | uuid | Filter by agent who created them |
| `created_from` | date | `YYYY-MM-DD` |
| `created_to` | date | `YYYY-MM-DD` |
| `sort_by` | string | `full_name`, `phone_number`, `created_at`, `updated_at`, `status`, `company`, `email_address`, `address` |
| `sort_order` | string | `asc` or `desc` |

**Response `200`:**
```json
{
  "data": [ /* Contact, … */ ],
  "total": 137,
  "count": 10,
  "per_page": 10,
  "current_page": 1,
  "total_pages": 14
}
```

---

## Get one contact

```http
GET /api/workspace/contacts/{contact_id}
```

**Response `200`:** Contact object. `404` if not found.

---

## Look up by phone number

```http
GET /api/workspace/contacts/phone/{phone_number}
```

`phone_number` must be URL-encoded (e.g. `%2B14155551234`).

**Response `200`:** Contact object. `404` if not found.

---

## Create a contact

```http
POST /api/workspace/contacts
Content-Type: multipart/form-data
```

| Field | Required | Description |
|-------|----------|-------------|
| `full_name` | Yes | Contact's full name |
| `phone_number` | Yes | E.164 or local format |
| `code` | No | ISO2 country code (auto-detected from number) |
| `email_address` | No | |
| `address` | No | |
| `company` | No | |
| `note` | No | |
| `image_url` | No | Image file (form upload) |

**Response `201`:** Created Contact object.

---

## Full update

```http
PUT /api/workspace/contacts/{contact_id}
Content-Type: multipart/form-data
```

Same fields as create. `full_name` and `phone_number` are required.

**Response `200`:** Updated Contact object.

---

## Partial update

```http
PATCH /api/workspace/contacts/{contact_id}
Content-Type: application/json

{
  "company": "New Corp",
  "note": "Updated note"
}
```

Send only the fields to change.

**Response `200`:**
```json
{ "success": true, "message": "Contact updated successfully" }
```

---

## Delete contacts (bulk)

```http
DELETE /api/workspace/contacts
Content-Type: application/json

{ "contact_ids": ["uuid-1", "uuid-2"] }
```

**Response `200`:**
```json
{ "success": true, "message": "Contacts deleted successfully", "data": "2 contacts deleted" }
```

---

## Import contacts — admin+

```http
POST /api/workspace/contacts/import
Content-Type: multipart/form-data

file=@contacts.csv
```

Accepted formats: `.csv`, `.xlsx`. Max size: **10 MB**.

Required CSV columns: `full_name`, `phone_number`  
Optional: `email_address`, `address`, `company`, `note`, `code`

**Response `200`:**
```json
{
  "success": true,
  "message": "Imported 142 contacts. 3 rows failed.",
  "failed_imports": [
    { "row": 5, "reason": "invalid phone number" }
  ]
}
```

Returns `400` if all rows fail.

---

## Export selected — admin+

```http
POST /api/workspace/contacts/export
Content-Type: application/json

{ "contact_ids": ["uuid-1", "uuid-2"] }
```

Returns a `text/csv` file attachment (not the JSON envelope).  
Columns: `ID, FullName, PhoneNumber, EmailAddress, Status, CreatedAt`.

---

## Export all — admin+

```http
GET /api/workspace/contacts/export-all
```

Optional query param `fields` to select columns:  
`?fields=id,full_name,phone_number,email_address,status,address,company,note,code,created_at,updated_at`

Returns a `text/csv` file attachment.
