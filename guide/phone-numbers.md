# Phone Numbers

## Buying a number

1. Go to **Phone Numbers → Browse Available**.
2. Filter by country, area code, type (local, toll-free, mobile), or capability (voice / SMS / MMS / fax).
3. Select a number and click **Buy** — only admins and owners can purchase numbers.
4. The number is provisioned immediately via Twilio and appears in your number list.

Each number has a monthly renewal fee that is charged automatically from your workspace subscription.

---

## Number settings

Click any phone number to open its settings panel. Each number has independent configuration for:

### Routing
How inbound calls are distributed to agents.

| Mode | Behaviour |
|------|-----------|
| **Simultaneous ring** | All assigned agents ring at once; first to answer wins |
| **Round robin** | Calls rotate across available agents in order |
| **Queue** | Callers wait on hold; agents take calls one at a time |

### IVR (Interactive Voice Response)
A keypad menu that lets callers self-select a department or option.
- Configure menu options, each routed to a team or agent.
- Set a timeout and a fallback action if no key is pressed.

### Voicemail
- Toggle on/off.
- Upload a custom greeting (MP3 / WAV) or use text-to-speech.
- Set the timeout after which unanswered calls go to voicemail.

### Forwarding
- Forward all calls (or only missed calls) to another number.
- Useful for after-hours forwarding to a mobile.

### Auto-Reply SMS
- Send an automatic SMS when a call to this number is missed.
- Customise the message text.

### Schedule (Business hours)
- Define open hours per day of the week.
- Add holidays — calls on those days follow the closed-hours rule.
- Closed-hours action: voicemail, reject, or forward.

### AI Agent
- Assign an AI voice agent to handle inbound calls instead of (or as fallback for) human agents.
- See [AI Voice Agents](ai-agents.md).

### Notifications & Recording
- Toggle call recording on/off for this number.
- Configure which events trigger push notifications to assigned agents.

---

## Assigning agents to a number

1. Open the number's settings and go to **Agents**.
2. Click **Assign Agents** and select agents from your team.
3. Only assigned agents receive inbound calls and SMS on that number.

---

## Selecting your outbound number

Each agent can choose which phone number to use for outbound calls:

1. Go to your **Agent Profile**.
2. Under **Outbound Number**, select from the numbers assigned to you.

---

## Releasing a number

Only admins and owners can release (delete) a number.

1. Open the number and click **Release Number**.
2. Confirm the action.

Releasing a number removes it from Twilio immediately. Calls and SMS to that number will stop working. This cannot be undone.

---

## Number lifecycle

| Status | Meaning |
|--------|---------|
| Active | Healthy, in service |
| Expiring soon | Monthly renewal due within 7 days |
| Expired | Past renewal date — in a 7-day grace window |
| Released | Permanently removed |

During the 7-day grace window, you can manually renew the number. After that it is returned to the pool and may be purchased by someone else.
