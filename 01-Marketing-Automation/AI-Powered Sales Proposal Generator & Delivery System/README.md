# AI-Powered Sales Proposal Generator & Delivery System

## Business Problem

Sales teams and agencies lose deals not because their offering is 
weak but because their proposals arrive late, look generic, and 
fail to speak directly to the prospect's specific situation. 
Writing a tailored proposal manually takes hours. When the team 
is busy, proposals get templated and impersonal. When a prospect 
receives a proposal that feels copy-pasted, it signals that the 
business will treat their account the same way. The deeper 
problem is that proposal writing pulls senior people away from 
selling. A business development manager spending three hours 
writing a proposal is a business development manager not making 
calls, attending meetings, or closing deals.

## System Solution

When a sales team member completes a client briefing form with 
the prospect's details, pain points, goals, and budget, the 
system triggers automatically. An AI agent reads the briefing 
and generates a complete, professional sales proposal covering 
an executive summary, problem statement, proposed solution, 
scope of work, investment summary, timeline, call to action, 
and an estimated deal value calculated as the midpoint of the 
selected budget range. A JavaScript parser extracts each 
section from the AI's unstructured output into clean, 
individually addressable fields, including a nested three-phase 
timeline structure. The proposal is reassembled into a final 
document, converted to a file, and delivered to the prospect 
as an email attachment alongside a personalized covering 
message. The sales team receives a Slack notification with 
the full briefing summary, and the proposal is logged to a 
Google Sheets tracker automatically.

## Tools Used

- n8n (automation engine)
- Tally (client briefing intake form)
- Google Gemini (AI proposal generation)
- Gmail (proposal delivery with file attachment)
- Slack (sales team notification)
- Google Sheets (proposal pipeline tracker)

## How to Use This Workflow

1. Download the workflow.json file
2. Open n8n and go to Workflows
3. Click Import and select the file
4. Connect your Tally, Gmail, Slack, Google Sheets, 
   and Gemini credentials
5. Update the Tally form ID to match your own briefing form
6. Update the Slack channel ID to your sales team channel
7. Update the Google Sheets document ID to your 
   proposal tracker
8. Confirm your form's budget range and timeline options 
   match the values referenced in the AI system prompt
9. Activate the workflow and submit a test briefing 
   to confirm end to end execution

## Key Features

- AI Proposal Agent generates a complete seven-section 
  sales proposal personalized to the prospect's industry, 
  pain points, and goals, with no templated or generic content
- AI calculates the estimated deal value as the midpoint of 
  the prospect's selected budget range directly within 
  the proposal generation step
- Regex-based JavaScript parser extracts all seven proposal 
  sections from unstructured AI text into clean, individually 
  addressable fields, including a nested three-phase timeline 
  object built dynamically regardless of phase count
- Proposal is reassembled and converted into a downloadable 
  file, delivered to the prospect as a genuine email 
  attachment rather than inline text
- Sales team receives an instant Slack notification with 
  the full prospect briefing and a 48-hour follow-up reminder
- Every proposal automatically logged to a Google Sheets 
  tracker with prospect details, estimated deal value, 
  date sent, and follow-up date calculated two days out

## Business Impact

- Proposal turnaround time reduced from hours to minutes
- Every prospect receives a tailored proposal that speaks 
  directly to their specific situation and industry
- Sales team freed from manual writing to focus on 
  relationship building and closing
- Consistent proposal quality maintained regardless of 
  who on the team submits the briefing
- Full proposal pipeline tracked automatically with 
  zero manual logging

## Known Limitations

- Proposal is delivered as a plain text file attachment, 
  not a branded PDF document in this version
- No proposal versioning or revision tracking in this version
- Sales team Slack notification and Google Sheets log fire 
  on a separate branch from the Gmail delivery node, meaning 
  a proposal could log as Sent even if the email itself 
  fails to deliver
- Proposal quality depends on the completeness of the 
  briefing form answers submitted by the sales team

## Planned Improvements

- Generate and attach a fully branded PDF proposal using 
  a document generation tool
- Restructure node execution so the Sheets log only fires 
  after Gmail confirms successful delivery
- Build a proposal revision flow where the sales team can 
  request AI revisions before sending
- Connect to a CRM to automatically update the deal stage 
  when a proposal is sent
