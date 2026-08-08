# Team & Settings

Manage your workspace members, roles, teams, and personal preferences from the **Settings** section.

---

## Roles

Every workspace member has one of three roles:

| Role | What they can do |
|------|-----------------|
| **Owner** | Full access — billing, subscriptions, number purchases, cancellations. One owner per workspace. |
| **Admin** | Manage agents, numbers, settings, and teams. Cannot manage billing. |
| **Member** | Make calls, send SMS, manage contacts. Cannot change workspace settings. |

---

## Inviting a member

Go to **Settings → Members** and click **Invite Member**.

![Invite member form](screenshots/settings-invite.png)

1. Enter the person's **email address**.
2. Choose their **role** (Admin or Member).
3. Click **Send Invite**.

The invitee receives an email with a link to accept and join. Pending invitations are listed until accepted or cancelled.

---

## Changing a member's role

1. Go to **Settings → Members**.
2. Click the member's name.
3. Change their role and save.

Role changes take effect immediately.

---

## Removing a member

Select the member from the list and click **Remove**. They lose access immediately. Their call and message history stays in the workspace.

---

## Teams

Teams are groups of agents used for call routing. When a call is routed to a team, all online members of that team ring simultaneously.

![Teams list](screenshots/teams-list.png)

**Create a team:**
1. Go to **Settings → Teams**.
2. Click **New Team**, give it a name, and add members.
3. Save.

**Use a team:**
Assign the team to a phone number's routing or IVR settings (see [Phone Numbers](phone-numbers.md)).

---

## Your profile

Go to **Settings → Profile** to update your personal details.

![Profile settings](screenshots/settings-profile.png)

- **Full name** and **profile photo**
- **Do Not Disturb (DND)** — when on, inbound calls won't ring you
- **Ringtone** — choose your preferred incoming call sound
- **Outbound number** — set your default phone number for outgoing calls

---

## Notification preferences

Go to **Settings → Notifications** to control which events send you alerts.

![Notification settings](screenshots/settings-notifications.png)

Toggle on or off:
- Missed call notifications
- New inbound SMS
- Voicemail received
- Team mentions in notes
- Credit balance alerts

---

## Integrations

Go to **Settings → Integrations** to connect Callvix to your CRM or other tools.

![Integrations page](screenshots/settings-integrations.png)

Click **Connect** next to a provider and follow the OAuth flow to authorise access. Once connected, contacts and call activity can sync automatically.

---

## Developer settings

Go to **Settings → Developer** to manage **API keys** and **webhooks** for custom integrations.

![Developer settings](screenshots/settings-developer.png)

- **API Keys** — generate keys for server-to-server access (see [API Reference](../api/authentication.md))
- **Webhooks** — receive real-time events on your own server (see [Webhooks API](../api/webhooks.md))

---

## Billing

Go to **Settings → Billing** to manage your subscription, credits, and payment methods.

![Billing page](screenshots/settings-billing.png)

- View your current plan and usage
- Add or remove payment cards
- Download invoices
- Top up your credit balance
- Set up auto-refill so credits reload automatically

> Only the workspace **Owner** can make billing changes.
