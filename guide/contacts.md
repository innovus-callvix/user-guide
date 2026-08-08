# Contacts

## Adding a contact

1. Go to **Contacts → Add Contact**.
2. Fill in the required fields:
   - **Full Name** (required)
   - **Phone Number** (required, E.164 or local format)
   - **Country** (auto-detected from number prefix)
3. Optionally add: email, company, address, note, tags, and a profile photo.
4. Click **Save**.

---

## Finding a contact

Use the **Search** bar at the top of the Contacts list. You can search by:
- Name
- Phone number
- Email
- Company

**Filter** the list by:
- Status (active / blocked)
- Tags
- Created by (which agent added them)
- Date range

---

## Editing a contact

Click any contact to open their profile. Click **Edit** to update any field. Changes take effect immediately across all conversations with that contact.

---

## Blocking a contact

On a contact's profile, click **Block**. Blocked contacts:
- Cannot initiate inbound calls or SMS that are routed to agents.
- Are shown with a `blocked` badge in the contact list.

To unblock, open the contact and click **Unblock**.

---

## Tags

Tags let you organise contacts into groups (e.g. `VIP`, `Lead`, `Support`).

**Create a tag:**
1. Go to **Settings → Tags** (or from the contact edit form).
2. Click **New Tag**, enter a name and pick a color.

**Apply a tag to a contact:**
- From the contact edit form, click the Tags field and select a tag.
- Multiple tags can be applied to one contact.

**Filter by tag:** In the Contacts list, use the Tag filter to show only contacts with a specific tag.

---

## Importing contacts

Admins and owners can bulk-import contacts from a CSV or Excel file.

1. Go to **Contacts → Import**.
2. Download the **template file** to see the required column format.
3. Fill in your contacts and upload the file.
4. Review the import summary — any rows that failed (invalid number, missing name) are listed separately.

Required columns: `full_name`, `phone_number`  
Optional columns: `email_address`, `address`, `company`, `note`, `code` (country ISO2)

---

## Exporting contacts

Admins and owners can export contacts to CSV.

- **Export selected:** Check the contacts you want, then click **Export Selected**.
- **Export all:** Click **Export All** — downloads all contacts matching your current filter.

Exported columns: ID, Full Name, Phone Number, Email, Status, Created At (and optional fields if chosen).

---

## Deleting contacts

Select one or more contacts using the checkboxes, then click **Delete**. Deletion is permanent — there is no undo.
