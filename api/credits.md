# Credits API

Base URL: `/api/workspace/credits`  
Auth: JWT + `X-Workspace-Id`  
All roles unless noted.

---

## Get balance

```http
GET /api/workspace/credits/balance
```

Returns the caller's wallet balance plus the owner wallet balance.

**Response `200`:**
```json
{
  "agent_balance": "12.50",
  "owner_balance": "245.00",
  "currency": "USD"
}
```

---

## Get wallet config — admin+

```http
GET /api/workspace/credits/config
```

Returns auto-refill thresholds and top-up amounts for owner and agent wallets.

**Response `200`:**
```json
{
  "owner_min_balance": "50.00",
  "owner_topup_amount": "200.00",
  "agent_min_balance": "5.00",
  "agent_topup_amount": "20.00",
  "auto_refill_enabled": true
}
```

---

## Update wallet config — admin+

```http
PATCH /api/workspace/credits/config
Content-Type: application/json

{
  "owner_min_balance": "100.00",
  "owner_topup_amount": "500.00",
  "agent_min_balance": "10.00",
  "agent_topup_amount": "50.00",
  "auto_refill_enabled": true
}
```

**Response `200`:** Updated config.

---

## Load owner wallet (Stripe checkout) — admin+

Starts a Stripe checkout session to add credits to the owner wallet.

```http
POST /api/workspace/credits/load-owner-wallet
Content-Type: application/json

{
  "amount": "200.00",
  "success_url": "https://app.callvix.com/billing?success=1",
  "cancel_url": "https://app.callvix.com/billing"
}
```

**Response `200`:**
```json
{ "checkout_url": "https://checkout.stripe.com/pay/cs_..." }
```

Redirect the owner to `checkout_url` to complete payment.

---

## Credit requests

Agents can request credits from the owner/admins when they need a top-up.

### Create a request

```http
POST /api/workspace/credits/request
Content-Type: application/json

{
  "amount": "25.00",
  "reason": "Needed for outbound campaign next week"
}
```

**Response `201`:**
```json
{
  "id": "uuid",
  "amount": "25.00",
  "reason": "Needed for outbound campaign next week",
  "status": "pending",
  "created_at": "2026-08-08T10:00:00Z"
}
```

### List requests

```http
GET /api/workspace/credits/requests
```

Returns requests made by the authenticated agent (or all requests if admin+).

### Request summary — admin+

```http
GET /api/workspace/credits/requests/summary
```

Returns totals: pending amount, approved this month, denied this month.

### List approvers

```http
GET /api/workspace/credits/approvers
```

Returns agents with admin or owner role who can approve requests.

### Process a request — admin+

```http
PUT /api/workspace/credits/requests/process
Content-Type: application/json

{
  "request_id": "uuid",
  "action": "approve"
}
```

`action`: `approve` or `deny`.

On approval, credits are transferred from the owner wallet to the requesting agent's wallet immediately.

---

## Agent spending trend — admin+

```http
GET /api/workspace/credits/agents/{agent_id}/spending-trend
```

**Query params:** `from` and `to` (dates, `YYYY-MM-DD`).

**Response `200`:**
```json
{
  "agent_id": "uuid",
  "agent_name": "Jane Doe",
  "trend": [
    { "date": "2026-08-01", "spent": "3.45" },
    { "date": "2026-08-02", "spent": "5.10" }
  ],
  "total_spent": "8.55"
}
```
