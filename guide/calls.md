# Calls

## Making an outbound call

1. Click **New Call** (or press the call icon in the dialer).
2. Type the destination number — Callvix accepts E.164 (`+14155551234`) or local formats.
3. Choose your **From** number (one of your workspace phone numbers).
4. Click **Call** — your browser/mobile app will connect you.

Credits are deducted per minute once the call is answered, based on the destination country rate.

---

## Receiving an inbound call

When a call comes in to one of your numbers, Callvix routes it based on the number's settings (see [Phone Number Settings](../guide/phone-numbers.md)):

- **Direct routing** — rings all assigned agents simultaneously.
- **Queue** — callers wait on hold until an agent becomes available.
- **IVR** — callers press keys to reach the right team or option.
- **AI Agent** — the AI handles the call instead of a human agent.
- **Voicemail** — if no agent answers within the timeout.
- **Forward** — redirects the call to another number.

---

## During a call

While on an active call you can:

| Action | How |
|--------|-----|
| Mute / unmute | Click the microphone button |
| Hold | Click Hold — the caller hears hold music |
| Start recording | Click **Record** (if recording is enabled on the number) |
| Stop recording | Click **Stop Recording** |
| Transfer | Coming soon |

---

## After a call

Every completed call creates a record in **Calls** with:

- **Duration** and **status** (completed, missed, no-answer, failed)
- **Recording** — playable directly in the app (if enabled)
- **Transcript** — auto-generated text of the conversation (if transcription is on)
- **Summary** — AI-generated summary of key points
- **Note** — your own freeform note; add or edit it any time

---

## Call history

Go to **Calls** to see all calls for your workspace. Filter by:

- Direction (inbound / outbound)
- Status (completed, missed, failed…)
- Date range
- Agent
- Phone number

Export the full call report as CSV from **Insights → Calls → Export**.

---

## Missed calls

When an inbound call is missed (no agent answers), Callvix:

1. Records it with status `missed`.
2. Deducts a minimum-charge credit from the phone number owner's wallet.
3. Optionally sends an **auto-reply SMS** to the caller (configure under [Number Settings → Auto-Reply](../guide/phone-numbers.md)).
4. Sends a **missed call push notification** to assigned agents.

---

## Recordings

Recording must be enabled on the phone number first (**Number Settings → Notifications & Recording**). Once enabled:

- Recordings start automatically when a call connects (or you can start/stop manually).
- Recordings appear in **Calls** and under **Recordings** in the communication panel.
- Recordings are stored securely and only accessible to authenticated workspace members.

---

## Live call monitor

Admins and owners can watch all active calls in real time from **Live Calls** in the sidebar. Each card shows: caller, agent, duration, and status — updating live via WebSocket.
