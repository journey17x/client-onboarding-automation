# Zoho Flow configuration

Flow name: **Client Onboarding Automation**

## Trigger

**Zoho Forms → Form entry submitted** on *Client Onboarding Intake*.

## Actions

### 1. Zoho CRM → Create or update contact
- First Name ← `Name - First Name`
- Last Name ← `Name - Last Name`
- Email ← `Email` (an existing contact with the same email is updated, not duplicated)
- Phone ← `Phone`
- Department ← `Company Name`
- Tag: `Onboarding`

### 2. Zoho Writer → Merge and email document (WorkDrive)
- Template: *Client Welcome Pack Template*
- Merge fields: First Name, Company Name, Service Package, Start Date (pretty format), Project Goals
- Mail type: Attachment – PDF
- From name: Client Success Team
- Recipient: `Email` from the form
- Subject: `Your welcome pack, «First Name»`
- Attachment name: `Welcome Pack - «Company Name»`

### 3. Zoho Projects → Create task list
- Project: Client Onboarding
- Task list name: `Onboarding - «Company Name»`

### 4–6. Zoho Projects → Create task or subtask (×3)
Each task goes into the task list created in step 3 (Tasklist ID ← `Create task list → Task list ID`) and is assigned to the account manager.

| Task | Description |
|---|---|
| Review intake responses | Check the intake answers, confirm package and goals, and flag anything missing before kickoff. |
| Schedule kickoff call | Email the client to book a 30-minute kickoff call close to their preferred start date. |
| Set up client workspace access | Invite the client to the shared workspace and confirm they can access their onboarding documents. |

## Testing

Submit the form with a plus-address (for example `you+test1@gmail.com`) so each test creates its own CRM contact, then check:

1. Zoho Flow → History: the run shows **Completed** with all 7 steps
2. Zoho CRM → Contacts: the new contact
3. Email inbox: the welcome pack PDF
4. Zoho Projects → Client Onboarding → Tasks: the new task list with 3 tasks
