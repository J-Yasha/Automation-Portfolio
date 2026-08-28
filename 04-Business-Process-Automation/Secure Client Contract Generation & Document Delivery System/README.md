# Secure Client Contract Generation & Document Delivery System

## Business Problem

Agencies and freelance service providers often begin client work before a signed contract exists. Verbal agreements get misremembered, and scope discussions handled only through email threads are never formalized. When a dispute arises over deliverables, payment terms, or timeline, there is no clean document either party can point to. Separately, any system that receives external submissions is exposed to abuse if that endpoint accepts requests from anyone without verification.

## System Solution

When a deal is confirmed, contract details are submitted through a secured intake endpoint that validates a shared secret carried in the request header before processing anything further. Once validated, an AI agent drafts the full contract body based on the engagement details submitted. The contract is inserted into a Google Doc, converted into a real PDF, and stored in a dedicated folder created per client. The client receives the PDF by email, the internal team is notified on Slack with a contract summary and a link to the stored document, and the contract is logged in a tracker sheet. Any request that fails the secret validation is rejected immediately, and the team is alerted on Slack with the source IP and timestamp of the blocked attempt.

## Tools Used

- n8n (workflow orchestration)
- Webhook node (secured intake with header-based secret validation)
- Google Gemini AI (contract drafting)
- Google Docs (document creation and text insertion)
- Google Drive (per-client folder storage and PDF export)
- Gmail (client delivery)
- Slack (internal notifications and security alerts)
- Google Sheets (contract tracker)

## How to Use

1. Send a POST request to the workflow's webhook URL.
2. Include a header carrying the correct shared secret value.
3. Include a JSON body with the engagement details: client name, client email, service provider name, scope of work, deliverables, contract value, currency, payment terms, timeline, start date, and end date.
4. If the secret is missing or incorrect, the request is rejected and the team is alerted on Slack. No further processing occurs.
5. If the secret is valid, the workflow drafts the contract, generates the PDF, delivers it to the client, notifies the team, and logs the contract in the tracker sheet automatically.

## Key Features

- Secured webhook intake that rejects any request not carrying the correct shared secret header
- AI agent that drafts a complete contract covering parties, scope, deliverables, payment terms, timeline, and standard clauses
- Real PDF generation through Google Docs, not a text or inline attachment
- Dedicated Google Drive folder created automatically per client
- Client delivery by email with the PDF properly attached
- Internal Slack notification with contract summary and document link
- Contract tracker in Google Sheets logging client, value, dates, and status
- Automatic internal Slack alert on any rejected, unauthorized request

## Business Impact

- Every client engagement begins with a real, signed-ready document instead of an email thread
- Contract turnaround reduced from hours of manual drafting to minutes
- Legal and operational exposure reduced by formalizing every engagement before work begins
- Public-facing intake protected from unauthorized or malicious submissions
- Full contract pipeline visibility maintained automatically without a dedicated contract management tool

## Known Limitations

- Contract status updates from Sent to Signed are manual, there is no e-signature platform integration
- The webhook secret is a single shared value, not a per-client or rotating credential
- PDF formatting is functional but not branded with a company letterhead or design system

## Planned Improvements

- Integrate an e-signature platform such as DocuSign or SignWell to automate the signed status update
- Add branded PDF styling using a company letterhead and consistent typography
- Rotate or scope the webhook secret per client submission for stronger security posture
