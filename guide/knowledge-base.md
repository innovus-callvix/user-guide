# Knowledge Base

A Knowledge Base is a collection of documents your AI agent reads to answer questions. Instead of guessing, the AI searches your knowledge base on every turn and gives answers grounded in your actual content.

![Knowledge base list](screenshots/kb-list.png)
*Each knowledge base shows how many documents it contains and its current status*

---

## Creating a knowledge base

1. Go to **More → Knowledge Base**.
2. Click **New Knowledge Base**.
3. Give it a name (e.g. "Product FAQ", "Company Policies").
4. Click **Create**.

![Create knowledge base](screenshots/kb-create.png)

---

## Adding content

Once the knowledge base is created, add content to it. You can add as many documents or URLs as you like.

### Upload a file

![Upload document](screenshots/kb-upload-file.png)

1. Open the knowledge base and click **Upload Document**.
2. Select a file from your computer.

Supported formats: **PDF**, **DOCX**, **TXT**

After uploading, the status shows **Processing** while Callvix reads and indexes the content. It changes to **Ready** when done — this usually takes under a minute.

---

### Add a website URL

If your content is already on your website, you can point the knowledge base to it directly.

![Add URL](screenshots/kb-add-url.png)

1. Click **Add URL**.
2. Paste the full URL of the page (e.g. `https://yourcompany.com/faq`).
3. Click **Add**.

Callvix visits the page, extracts the text, and indexes it automatically.

---

## Document statuses

| Status | What it means |
|--------|--------------|
| **Processing** | Being read and indexed — wait a moment |
| **Ready** | Indexed and available to the AI agent |
| **Failed** | Could not be processed — try uploading again |

---

## Deleting a document

Click the **⋯** menu next to any document and select **Delete**. The AI agent will no longer use that content.

---

## Connecting to an AI agent

A knowledge base has no effect until it's attached to an AI agent.

1. Go to **AI Agents → [your agent] → Knowledge tab**.
2. Click **Add Knowledge Base** and select your knowledge base.
3. Save.

The agent will now search the knowledge base on every call turn.

![Attach to agent](screenshots/kb-attach-agent.png)

---

## Tips for good knowledge bases

- **Keep documents focused** — one topic per document is easier for the AI to search.
- **Use clear headings** — the AI uses headings to understand what each section is about.
- **Keep it up to date** — delete outdated documents and re-upload updated versions.
- **Test after changes** — use [Test Agent](ai-agents.md#testing-your-agent) after updating the knowledge base to verify the AI answers correctly.
