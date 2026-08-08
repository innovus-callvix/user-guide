# Team Management

## Roles

Every member of a workspace has one of three roles:

| Role | What they can do |
|------|-----------------|
| **Owner** | Full access: billing, subscriptions, number purchasing, adding/removing cards, cancellation. Only one owner per workspace. |
| **Admin** | Manage agents, numbers, settings, teams, contacts (bulk), and CRM integrations. Cannot manage billing or transfer ownership. |
| **Member** | Make and receive calls, send SMS, manage their own contacts. Cannot change workspace settings. |

---

## Inviting a team member

Admins and owners can invite new members.

1. Go to **Settings → Team → Invite Member**.
2. Enter the person's email address.
3. Choose their role (Admin or Member — only the owner can make another admin).
4. Click **Send Invite**.

The invitee receives an email with a link. They must click it to accept, create their account (or sign in), and join the workspace.

**Pending invitations** are listed under **Settings → Team → Pending Invites**. You can re-send or cancel an invite from there.

---

## Changing a member's role

1. Go to **Settings → Team**.
2. Click the agent's name.
3. Change their role and save.

Role changes take effect immediately — including for any API keys that agent has created (keys always reflect the agent's current role).

---

## Removing a member

1. Go to **Settings → Team**.
2. Select the member(s) you want to remove.
3. Click **Remove from workspace**.

Removed agents lose all access immediately. Their call/message history stays in the workspace.

---

## Do Not Disturb (DND)

Each agent can toggle **Do Not Disturb** from their profile or the mobile app. When DND is on:
- Inbound calls are not routed to that agent.
- They still appear in the agent list but show as unavailable.

---

## Teams

Teams are groups of agents used for routing inbound calls.

**Create a team:**
1. Go to **Settings → Teams → New Team**.
2. Give the team a name and add members.
3. Save.

**Use a team in routing:**
- Assign a team to an IVR option or direct routing group on a phone number.
- Calls routed to a team ring all online members of that team simultaneously.

Teams can be updated at any time — routing adjusts immediately.

---

## Agent devices

Each agent can register multiple devices (browser, iOS, Android) to receive inbound calls and push notifications.

- Devices are registered automatically when you sign in on a new device.
- To remove a device, go to **Profile → Devices** and click **Remove**.
- All devices are removed automatically when an agent leaves the workspace.

---

## Ringtone & notification settings

Each agent can customise:
- **Ringtone** — choose from the available options under **Profile → Ringtone**.
- **Notification settings** — control which events trigger push notifications (missed calls, new SMS, voicemail, etc.) under **Profile → Notifications**.
