# SMS & Messaging

## Sending an SMS

1. Open a **Conversation** or go to **Messages → New Message**.
2. Enter the recipient's phone number or search your contacts.
3. Select which of your phone numbers to send from.
4. Type your message and click **Send**.

Each SMS costs one credit at the rate for the destination country. MMS (images) is supported — attach an image using the paperclip icon.

---

## Receiving SMS

Inbound SMS messages arrive in the **Conversations** panel. Callvix groups calls and SMS with the same contact into a single conversation thread so you have the full context.

When an inbound SMS arrives:
- A real-time notification appears in the app (and as a push notification on mobile).
- One credit is deducted from the phone number owner's wallet.
- If **auto-reply** is configured on that number, a reply is sent automatically.

---

## Conversations

Each conversation groups all messages and calls between your workspace and a specific phone number/contact.

From a conversation you can:
- Read the full message history
- Send a reply
- Make or receive a call to the same contact
- Add a **note** visible only to your team
- See the contact's details in the sidebar

Mark a conversation as **read** or **unread**. Unread conversations are highlighted in the list.

---

## Auto-reply

Set up an automatic SMS reply for missed calls or out-of-hours contacts.

1. Go to **Phone Numbers → [your number] → Auto-Reply**.
2. Toggle auto-reply on.
3. Write the message text (supports merge tags like `{caller_name}`).
4. Save.

The auto-reply fires when a call to that number is missed (no agent answers). One credit is deducted per auto-reply sent.

---

## Smart reply suggestions

In any conversation, click **Suggest Reply** to get AI-generated response options based on the conversation history. Choose one to insert it into the message box, then edit and send.

---

## Message status

| Status | Meaning |
|--------|---------|
| Sent | Delivered to Twilio for dispatch |
| Delivered | Confirmed received by the destination carrier |
| Failed | Could not be delivered — check the number and credits |
| Received | Inbound message from a contact |
