# Phone Numbers

The Numbers page shows all the phone numbers your workspace owns. Each number can make and receive calls and SMS independently, with its own routing, voicemail, schedule, and more.

![Numbers list](screenshots/numbers-list.png)
*Each number card shows its status, capabilities (Voice/SMS/MMS), and quick-access settings*

---

## Buying a number

Only **Admins** and **Owners** can purchase numbers.

1. Click **Get a Number** (top-right of the Numbers page).
2. Filter by **country**, **area code**, **type** (Local, Toll-free, Mobile), and **capability**.
3. Select a number from the results.
4. Give it a friendly name (e.g. "Sales Line") and click **Buy**.

![Browse available numbers](screenshots/numbers-browse.png)
*Numbers are provisioned instantly and appear in your list within seconds*

---

## Number settings

Click any number to open its settings page. Each number has its own independent configuration across several tabs.

![Number settings page](screenshots/numbers-settings.png)

---

### Routing

Controls how inbound calls are distributed to your team.

![Routing settings](screenshots/numbers-routing.png)

| Option | What it does |
|--------|-------------|
| **Simultaneous ring** | All assigned agents ring at once — first to answer takes the call |
| **Round robin** | Calls rotate across available agents in order |
| **Queue** | Callers wait on hold until an agent is free |

---

### IVR (Interactive Voice Response)

Set up a keypad menu so callers can self-select a department or option.

![IVR settings](screenshots/numbers-ivr.png)

1. Toggle **IVR** on.
2. Record or type a greeting (e.g. "Press 1 for Sales, Press 2 for Support").
3. Assign each key press to a team, agent, or action.
4. Set what happens if no key is pressed (timeout action).

---

### Voicemail

![Voicemail settings](screenshots/numbers-voicemail.png)

- Toggle voicemail on or off.
- Set the **timeout** — how many seconds before unanswered calls go to voicemail.
- Upload a custom **greeting** (MP3 or WAV) or type one for text-to-speech.

---

### Call Forwarding

Forward calls to another number — useful for after-hours routing to a mobile.

![Forwarding settings](screenshots/numbers-forwarding.png)

- Set the destination number.
- Choose whether to forward **all calls** or only **missed calls**.

---

### Auto-Reply SMS

Send an automatic text message when an inbound call is missed.

![Auto-reply settings](screenshots/numbers-autoreply.png)

- Toggle auto-reply on.
- Write your message. Keep it short and helpful.

---

### Business Hours & Schedule

Define when your number is "open". Calls outside business hours follow a separate rule (voicemail, reject, or forward).

![Schedule settings](screenshots/numbers-schedule.png)

1. Set open hours for each day of the week.
2. Add **holidays** — calls on those days follow the closed-hours rule.
3. Save.

---

### AI Agent

Assign an AI voice agent to handle inbound calls automatically.

![AI agent assignment](screenshots/numbers-ai-agent.png)

- Select a published AI agent from the dropdown.
- Toggle it on. From now on, inbound calls to this number go to the AI agent.

See [AI Agents](ai-agents.md) to learn how to build and publish one.

---

## Assigning agents to a number

Go to the number's **Agents** tab to control who receives inbound calls and SMS.

![Assign agents](screenshots/numbers-assign-agents.png)

Click **Assign Agents**, select team members, and save. Only assigned agents will ring when someone calls this number.

---

## Releasing a number

Click **Release Number** from the number's settings. This is permanent — the number is removed from your workspace immediately and can't be recovered.

> Only Admins and Owners can release a number.

---

## Number status

| Status | What it means |
|--------|--------------|
| Active | Working normally |
| Expiring Soon | Renewal due within 7 days |
| Expired | In the 7-day grace window — renew now to keep it |
| Released | Permanently removed |
