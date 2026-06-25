# Automated Invoice Generation & Payment Follow-Up System

## Business Problem

Freelancers, agencies, and professional service businesses lose 
significant revenue every month, not because clients refuse to pay, 
but because the follow-up process is manual, inconsistent, and easy 
to deprioritize when the team is busy delivering work. Invoices are 
created late, sent from personal email threads, and followed up on 
only when cash flow becomes a problem. The result is delayed 
payments, awkward client conversations, and a finance process that 
depends entirely on one person remembering to chase money.

## System Solution

This system operates as two coordinated workflows inside a single 
n8n canvas. The first flow triggers when a client intake form is 
Submitted on Tally. It generates a unique invoice reference 
automatically calculates the due date, logs the invoice to a 
Google Sheets payment tracker with a status of UNPAID, notifies 
the team on Slack, and sends the client a confirmation email with 
their full invoice summary.

The second flow runs on a daily schedule. It reads every row in 
the payment tracker and evaluates each unpaid invoice against its 
due date and reminder stage. Invoices that are overdue and have 
not yet received a first reminder trigger a polite reminder email 
to the client, a Slack alert to the team, and an update to the 
tracker marking the first reminder as sent. Invoices that have 
already received a first reminder and remain unpaid trigger a 
firmer second reminder email, a separate Slack escalation alert, 
and a tracker update marking the second reminder as sent.

## Tools Used

- n8n (automation engine)
- Tally (client intake form)
- Gmail (invoice confirmation and reminder emails)
- Google Sheets (payment tracker and reminder stage logging)
- Slack (team notifications for invoice sent and reminders triggered)

## How to Use This Workflow

1. Download the workflow.json file
2. Open n8n and go to Workflows
3. Click Import and select the file
4. Connect your Tally, Gmail, Google Sheets, and Slack credentials
5. Update the Tally form ID to match your own form
6. Update the Google Sheets document ID to your payment tracker
7. Update the Slack channel IDs to your team notification channel
8. Set the payment window in the Code node to match your 
   standard invoice terms
9. Activate both triggers and submit a test form entry to confirm

## Key Features

- Unique invoice reference generated automatically using the 
  submission year and Tally submission ID
- Invoice logged to Google Sheets immediately upon form submission 
  with client name, email, service, amount, currency, invoice ID, 
  date sent, due date, payment status, and reminder stage
- Client receives a professional invoice confirmation email within 
  seconds of form submission
- Daily scheduled flow reads the payment tracker and evaluates 
  every unpaid invoice automatically
- Two-stage reminder sequence with a polite first reminder and a 
  firmer second reminder sent at defined intervals
- Tracker updated after each reminder stage so the payment log 
  always reflects the current status
- Separate Slack notifications for invoice sent, first reminder 
  triggered, and second reminder triggered with escalation guidance

## Business Impact

- Invoice sent within seconds of a project being marked complete, 
  not days later
- Payment follow-up runs automatically without anyone tracking 
  due dates manually
- Full payment tracker maintained in real time with zero 
  manual data entry
- Overdue invoices never fall through the cracks because a 
  human forgot to follow up
- Professional and consistent client communication at every 
  stage of the payment process

## Known Limitations

- Invoice is sent as a formatted email, not a PDF document 
  in this version
- Payment window is calculated as a fixed number of days from 
  submission rather than being set per client on the intake form
- Payment status must be updated manually in Google Sheets 
  when a client pays
- Follow-up sequence has two stages only with no automatic 
  escalation after the second reminder
- IF node false branches have no logging, skipped rows are 
  handled silently

## Planned Improvements

- Generate and attach a PDF invoice using a document 
  generation tool
- Add a due date field to the intake form so payment terms 
  can be set per client
- Connect to a payment gateway such as Paystack or Flutterwave 
  to detect payments automatically and update the tracker 
  without manual input
- Add a third escalation stage that notifies the business owner 
  directly if payment is not received after both reminders