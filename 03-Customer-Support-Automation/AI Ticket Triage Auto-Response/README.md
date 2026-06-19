# AI-Powered Customer Support Ticket Triage & Auto-Response System

## Business Problem

Small and mid-sized businesses handling customer support through 
email or a contact form face the same problem at scale: every 
message lands in the same inbox, treated with the same priority, 
handled by the same overwhelmed person. A billing emergency sits 
next to a general inquiry. A frustrated customer waits hours for 
a response that could have been sent in seconds. Support staff 
spend most of their time on repetitive questions that have the 
same answer every time. The result is slow response times, 
inconsistent service quality, and a support team burning time 
on work that does not require human judgment.

## System Solution

When a customer submits a support message via a Tally form, 
the system immediately reads the content, classifies the issue 
by category and urgency using an AI agent, sends an instant 
AI-generated response for low and normal priority tickets, 
escalates urgent tickets to the support team on Slack with 
full context, and logs every ticket to a structured Google 
Sheet tracker with category, priority, AI response, and timestamp.
The support team stops firefighting and handles only what 
genuinely requires human judgment.

## Tools Used

- n8n (automation engine)
- Tally (customer support form intake)
- Google Gemini (AI classification and response generation)
- Gmail (automated customer responses)
- Slack (urgent ticket escalation alerts)
- Google Sheets (full ticket logging and tracking)

## How to Use This Workflow

1. Download the workflow.json file
2. Open n8n and go to Workflows
3. Click Import and select the file
4. Connect your Tally, Gmail, Google Sheets, Slack, 
   and Gemini credentials
5. Update the Tally form ID to match your own form
6. Update the Slack channel ID to your escalation channel
7. Activate the workflow and submit a test ticket to confirm

## Key Features

- AI classification engine assigns both a category (billing, 
  delivery, technical, general) and a priority level (urgent, 
  normal, low) to every incoming ticket
- Instant AI-generated resolution email sent to low and normal 
  priority customers without any human involvement
- Urgent tickets trigger an immediate acknowledgment email to 
  the customer and a detailed escalation alert to the support 
  team on Slack
- Every ticket logged to Google Sheets with customer name, 
  email, order number, category, priority, timestamp, issue 
  description, and AI response for full auditability
- Clean data layer using an Edit Fields node that organizes 
  all ticket data into named fields for consistent 
  downstream use

## Business Impact

- Zero unanswered support messages regardless of volume 
  or time of day
- Support team workload reduced by automatically resolving 
  repetitive low-priority inquiries without human involvement
- Urgent issues escalated to a human within seconds, not hours
- Every ticket logged and trackable, no support request 
  ever gets lost
- Consistent response quality across every customer 
  interaction at any hour

## Known Limitations

- Normal and low priority tickets are handled identically 
  with no distinction between response tone or urgency
- No two-way ticket tracking, the system logs the ticket 
  but does not update when the issue is resolved
- Classification accuracy depends on how clearly the 
  customer describes their issue
- No HTML branded email template in this version

## Planned Improvements

- Add separate handling for normal vs low priority tickets 
  with differentiated response tones
- Build a ticket status update flow that marks tickets 
  as resolved when the support team replies
- Add a follow-up sequence for tickets with no resolution 
  confirmation after 48 hours
- Integrate with a proper helpdesk tool such as Freshdesk 
  or Zendesk in a future version