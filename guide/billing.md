# Billing & Credits

## How billing works

Callvix uses a two-layer billing model:

1. **Subscription** — a monthly/yearly Stripe subscription covers your plan tier (number of seats, features). Managed by the workspace owner.
2. **Credits** — a pre-paid balance that is deducted per call minute, per SMS, per AI session. Credits run out → calls stop until you top up.

---

## Plans

Go to **Settings → Subscription** to view and change your plan.

| Plan | Seats | Features |
|------|-------|----------|
| Basic | Up to 5 agents | Calls, SMS, contacts |
| Pro | Up to 20 agents | + AI agents, campaigns, CRM integrations |
| Enterprise | Unlimited | + Priority support, custom limits |

Click **Upgrade** to move to a higher plan (effective immediately, prorated). Click **Downgrade** to schedule a change at the end of your current billing period.

---

## Adding credits

Only the workspace owner can add credits.

1. Go to **Billing → Credits → Add Credits**.
2. Choose an amount.
3. Complete the Stripe payment.

Credits are added to the **owner wallet** instantly.

---

## Auto-refill

Set a minimum balance threshold. When your owner wallet drops below it, Callvix automatically charges your default card and adds credits.

1. Go to **Billing → Credits → Auto-Refill Settings**.
2. Set the **minimum balance** and the **top-up amount**.
3. Save.

---

## Credit distribution to agents

Each agent has their own wallet. The owner wallet funds agent wallets automatically:

- When an agent's balance drops below a configured threshold, credits are transferred from the owner wallet to the agent wallet.
- Agents can also **request credits** if they need more — the request goes to admins/owners for approval.

**Approve a credit request:**
1. Go to **Billing → Credit Requests**.
2. Review pending requests.
3. Approve or deny each one.

---

## Rates

Call and SMS rates depend on the destination country and the direction (inbound / outbound).

To check rates, contact support or review the **Billing Rates** table in your workspace settings.

| Service | How cost is calculated |
|---------|----------------------|
| Outbound call | Per minute (billed in 60-second increments) |
| Inbound call answered | Per minute from the answering agent's wallet |
| Missed inbound call | Minimum 1-minute charge from number owner's wallet |
| Outbound SMS | Flat rate per message |
| Inbound SMS | Flat rate per message from number owner's wallet |
| AI inbound call | Per minute from number owner's wallet (separate AI rate) |
| AI test session | Per minute from agent's wallet |
| Knowledge base embedding | Per 1,000 tokens from agent's wallet |

---

## Payment cards

The owner can manage payment cards under **Billing → Payment Methods**.

- **Add a card** — click **Add Card** and complete the Stripe secure form.
- **Set default** — the default card is charged for subscriptions and credit top-ups.
- **Remove a card** — click **Remove** next to the card (must have at least one card).

---

## Invoices

Admins and owners can view all invoices under **Billing → Invoices**.

- Click an invoice to see the breakdown.
- Download as PDF.
- Open the Stripe invoice page directly.

---

## Cancelling your subscription

Only the workspace owner can cancel.

1. Go to **Settings → Subscription → Cancel**.
2. Confirm the cancellation.

Your subscription stays active until the end of the current billing period. After that, the workspace is downgraded and number renewals stop.
