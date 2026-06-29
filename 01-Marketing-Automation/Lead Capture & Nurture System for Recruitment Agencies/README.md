# AI-Powered Lead Capture & Nurture System for Recruitment Agencies

## Business Problem

Recruitment agencies running high-volume hiring pipelines face a 
specific and costly problem: candidate drop-off between application 
and first contact. A candidate submits their details, hears nothing 
for days, and accepts an offer elsewhere. Meanwhile, the recruiter 
is manually sorting through a spreadsheet of applications, copying 
data between tools, and sending the same acknowledgment email over 
and over. The operational cost is twofold: qualified candidates are 
lost to slow response times, and recruiters burn hours on 
administrative work that adds no value to the placement process.

## System Solution

This system operates as two coordinated automated flows inside a 
single n8n canvas. The first flow triggers when a candidate submits 
an application through a Tally intake form. An AI qualification 
engine powered by Google Gemini analyzes the candidate's role 
interest, years of experience, employment status, and availability, 
then scores them as STRONG, POTENTIAL, or NOT A FIT with a one-line 
reason. Qualified candidates are logged to a dedicated sheet, 
receive a personalized acknowledgment email within seconds, and 
trigger a Slack notification to the recruitment team with the full 
candidate summary. Not a Fit candidates are logged to a separate 
sheet and receive a professional holding response that declines 
without burning the relationship.

The second flow runs on a daily schedule. It reads the qualified 
candidate tracker, filters for candidates who applied more than 
three days ago, have a status of QUALIFIED, and have not yet 
received a follow-up. Eligible candidates receive a personalized 
check-in email and their row in the tracker is updated to reflect 
that the follow-up was sent.

## Tools Used

- n8n (automation engine)
- Tally (candidate intake form)
- Google Gemini (AI qualification engine)
- Gmail (candidate acknowledgment, holding response, 
  and follow-up emails)
- Google Sheets (qualified candidate tracker and 
  not a fit log)
- Slack (recruitment team notifications)

## How to Use This Workflow

1. Download the workflow.json file
2. Open n8n and go to Workflows
3. Click Import and select the file
4. Connect your Tally, Gmail, Google Sheets, Slack, 
   and Gemini credentials
5. Update the Tally form ID to match your own intake form
6. Update the Google Sheets document ID to your 
   candidate tracker
7. Update the Slack channel ID to your recruitment 
   team channel
8. Confirm the column names in your tracker match 
   the field references in the Code node filter
9. Activate both triggers and submit a test application 
   to confirm

## Key Features

- AI qualification engine scores every candidate as STRONG, 
  POTENTIAL, or NOT A FIT based on experience, availability, 
  and employment status with a one-line reason returned 
  alongside the score
- Qualified candidates receive a personalized acknowledgment 
  email referencing their specific role interest within 
  seconds of applying
- Not a Fit candidates receive a professional holding 
  response and are logged to a separate sheet, keeping 
  the pipeline clean without discarding the relationship
- Recruitment team receives an instant Slack notification 
  with the full candidate profile and AI qualification 
  result for every qualified application
- Daily scheduled follow-up flow filters the tracker 
  using three conditions: qualified status, no prior 
  follow-up sent, and minimum three days since application
- Tracker row updated automatically after follow-up 
  is sent so the pipeline always reflects current 
  candidate status

## Business Impact

- Zero candidates left without a response regardless 
  of application volume
- Recruiters receive pre-qualified candidate summaries 
  instead of raw application data
- Candidate pipeline stays warm automatically through 
  scheduled follow-ups without manual intervention
- Administrative burden on the recruitment team 
  reduced significantly
- Professional candidate experience from the first 
  touchpoint builds agency reputation and reduces drop-off

## Known Limitations

- Qualification is based on form answers only, no CV 
  or document analysis in this version
- No integration with an ATS such as Workable or 
  Greenhouse in this version
- Follow-up sequence is a single check-in, not a 
  multi-stage nurture campaign
- IF node routes STRONG and POTENTIAL candidates 
  through the same qualified track with no distinction 
  between the two scores in downstream handling

## Planned Improvements

- Add CV upload and AI-powered CV analysis to the 
  qualification layer for deeper candidate assessment
- Integrate with an ATS to push qualified candidates 
  directly into the hiring pipeline automatically
- Build a multi-stage nurture sequence for candidates 
  who remain uncontacted after the first follow-up
- Add separate handling for STRONG vs POTENTIAL 
  candidates with differentiated communication tracks