# Contacts

The Contacts page is your address book. Every person your team calls or messages can be saved here with their details, tags, and history.

![Contacts list](screenshots/contacts-list.png)
*Switch between grid and table view using the icons top-right*

---

## Adding a contact

Click **Add Contact** (top-right of the Contacts page).

![Add contact form](screenshots/contacts-add-form.png)
*Only Full Name and Phone Number are required — everything else is optional*

Fill in:
- **Full Name** *(required)*
- **Phone Number** *(required)*
- **Country** — auto-detected from the number prefix
- **Email**, **Company**, **Address**, **Note** — all optional
- **Tags** — pick from existing tags or create new ones
- **Photo** — upload a profile picture

Click **Save Contact** when done.

---

## Finding a contact

Use the **Search** bar at the top to find contacts by name, phone number, email, or company.

Use the **Filter** button to narrow down by:
- Status (Active / Blocked)
- Tags
- Date added
- Added by (which team member)

![Contact search and filter](screenshots/contacts-filter.png)

---

## Contact profile

Click any contact to open their full profile.

![Contact profile](screenshots/contacts-profile.png)
*The profile shows all details, tags, notes, and the full communication history with that contact*

From the profile you can:
- **Edit** any field
- **Call** the contact directly
- **Send a message**
- **Block** or **Unblock** the contact
- View the full conversation history

---

## Tags

Tags help you group and filter contacts (e.g. `VIP`, `Lead`, `Support`).

**Create a tag:**
Go to **Settings → Tags**, click **New Tag**, give it a name and a colour.

**Apply a tag:**
Open a contact → Edit → click the Tags field → select or type a tag name.

![Contact tags](screenshots/contacts-tags.png)

---

## Importing contacts

Admins and owners can bulk-import contacts from a CSV or Excel file.

1. Click **Import** on the Contacts page.
2. Download the **template file** to see the correct column format.
3. Fill in your contacts and upload the file.

![Bulk import dialog](screenshots/contacts-import.png)
*Any rows that fail (invalid number, missing name) are listed in the import summary*

**Required columns:** `full_name`, `phone_number`  
**Optional columns:** `email_address`, `company`, `address`, `note`

---

## Exporting contacts

Click **Export** to download your contacts as a CSV file.

- **Export selected** — tick the contacts you want first
- **Export all** — exports everything matching your current filter

---

## Blocking a contact

Open the contact profile and click **Block**. Blocked contacts are flagged and won't be routed to your agents for inbound calls. To undo, click **Unblock** from the same profile.
