# AI Campaigns

An AI Campaign lets your AI agent automatically call a list of contacts — without any human involvement. Use it for appointment reminders, lead follow-ups, surveys, or any outbound outreach at scale.

![AI Campaigns list](screenshots/ai-campaigns-list.png)
*Each campaign card shows its status, contact count, and completion rate*

---

## Creating a campaign

Click **New Campaign** on the AI Campaigns page.

![Create campaign dialog](screenshots/ai-campaigns-create.png)

Fill in:

| Field | What to enter |
|-------|--------------|
| **Campaign Name** | A name for your own reference (e.g. "Q1 Follow-up") |
| **From Number** | The phone number the AI will call from |
| **AI Agent** | The published agent that will handle the calls |

Click **Create & Continue** to move to the contacts step.

> The AI agent must be **published** before it can be selected here. See [AI Agents](ai-agents.md).

---

## Uploading contacts

After creating the campaign, upload the list of people to call.

![Upload contacts](screenshots/ai-campaigns-upload-contacts.png)

1. Click **Upload Contacts**.
2. Upload a **CSV file** with at least a `phone_number` column.
3. Review the preview — check that numbers look correct.
4. Click **Confirm Upload**.

The contacts list is shown on the campaign detail page after upload.

---

## Launching a campaign

When your contacts are uploaded and you're ready to go:

1. Open the campaign detail page.
2. Click **Launch Campaign**.
3. Confirm the action.

![Campaign detail page](screenshots/ai-campaigns-detail.png)
*The detail page shows real-time progress: calls placed, answered, completed, and failed*

The campaign status changes to **Running**. The AI agent begins dialling contacts automatically.

---

## Campaign statuses

| Status | What it means |
|--------|--------------|
| **Draft** | Created but not yet launched |
| **Running** | Actively dialling contacts |
| **Paused** | Manually paused — resume any time |
| **Completed** | All contacts have been called |

---

## Pausing and resuming

From the campaign detail page, click **Pause** to stop dialling temporarily. Click **Resume** to continue from where it left off.

---

## Viewing results

The campaign detail page updates in real time:

- **Total contacts** — how many numbers were uploaded
- **Called** — how many have been dialled so far
- **Answered** — how many connected successfully
- **Completed** — how many conversations finished
- **Failed** — numbers that couldn't be reached

Click any contact row to see the outcome and transcript of that individual call.

---

## Tips for better campaigns

- Keep the AI agent's greeting short and clear — callers decide in the first 5 seconds.
- Upload only valid, opted-in phone numbers.
- Test the agent with [Test Agent](ai-agents.md#testing-your-agent) before launching a large campaign.
- Start small (50–100 contacts) to verify quality before scaling up.
