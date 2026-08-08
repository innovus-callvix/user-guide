# AI Voice Agents

AI voice agents let you deploy a fully automated voice assistant that handles inbound (and outbound) calls without a human agent. The AI speaks, listens, and responds in real time using your knowledge base.

---

## How it works

```
Caller → Twilio → AI Worker (Python)
                      ├── Deepgram STT  (speech → text)
                      ├── Groq LLM      (text → response)
                      ├── Deepgram TTS  (response → speech)
                      └── Knowledge Base (RAG via pgvector)
```

The AI searches your knowledge base on every turn to ground its answers in your content.

---

## Creating an AI agent

1. Go to **AI Agents → New Agent**.
2. Fill in:
   - **Name** — internal label (e.g. "Support Bot").
   - **Greeting** — the first thing the AI says when someone calls.
   - **System Prompt** — instructions for how the AI should behave. Be specific: tone, topics it can/cannot discuss, how to handle escalations.
   - **Voice** — choose from the available Deepgram voices (different accents and genders).
   - **Language** — the language the AI will speak and understand.
   - **Knowledge Base** — attach one or more knowledge bases (see below).
3. Click **Save**.

---

## Knowledge bases

A knowledge base is a collection of documents the AI searches when answering questions.

**Create a knowledge base:**
1. Go to **AI Agents → Knowledge Bases → New Knowledge Base**.
2. Give it a name.
3. Add content:
   - **Upload a file** — PDF, DOCX, or TXT (max 50 MB).
   - **Add a URL** — paste a website URL; Callvix will crawl and index its content.
4. Wait for the status to change to **Ready** — processing takes a moment for large documents.

**Attach to an agent:**
- In the AI agent's settings, select one or more knowledge bases under **Knowledge Base**.

**Delete a document:**
- Open the knowledge base, find the document, and click **Delete**.

---

## Testing an AI agent

Before going live, test the agent in your browser:

1. Open the agent and click **Test Agent**.
2. Allow microphone access.
3. Speak naturally — the agent responds in real time via your browser speakers.
4. When done, click **End Session**.

The test uses your browser microphone and speakers. No phone or Twilio minute is charged, but a session-based credit is deducted.

---

## Publishing and assigning to a number

An agent must be **Published** before it can handle real calls.

1. Open the agent and click **Publish**.
2. Go to **Phone Numbers → [your number] → AI Agent**.
3. Assign the published agent.
4. Toggle the AI agent on.

From now on, inbound calls to that number are answered by the AI agent.

---

## AI Campaigns

Use AI campaigns to automatically dial a list of contacts and have the AI agent speak to each one.

**Create a campaign:**
1. Go to **AI Campaigns → New Campaign**.
2. Select the AI agent to use.
3. Choose a phone number to dial from.
4. Upload a contact list (CSV with `phone_number` column).
5. Set the schedule (start time, max concurrent calls, timezone).
6. Click **Launch**.

Monitor progress from the campaign detail page — see live call counts, completion rate, and per-contact outcomes.

---

## Credits

AI features consume credits from the agent's wallet (for test sessions and document embedding) or the phone number owner's wallet (for live inbound AI calls).

| Action | Cost |
|--------|------|
| Embedding documents on deploy | Per 1,000 tokens (set by `AI_EMBEDDING_RATE_PER_1K`) |
| Test agent sessions | Per minute (set by `AI_SESSION_RATE_PER_MIN`) |
| Live inbound AI call | Per minute (from `billing_rates` table, `sell_rate_4`) |
