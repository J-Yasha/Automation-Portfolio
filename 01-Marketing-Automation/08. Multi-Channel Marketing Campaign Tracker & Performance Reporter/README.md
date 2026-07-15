# Automated Multi-Channel Marketing Campaign Tracker & Performance Reporter

## Business Problem

Marketing teams running campaigns across multiple channels spend 
hours every week pulling performance data manually. Someone logs 
into Google Ads, exports numbers, logs into Meta, exports more 
numbers, opens a spreadsheet, pastes everything in, writes a 
summary, and sends it to the team. That process happens weekly 
and consumes time that should be spent on strategy and 
optimization. By the time the report is ready, the data is 
already stale and decisions that should have been made three 
days ago are being made today because nobody had the numbers 
until now.

## System Solution

On every Monday morning at 6am, the workflow triggers 
automatically. A dedicated calendar node calculates the current 
date and the previous week date range, which flows consistently 
into every downstream node. The campaign data sheet is read, 
and a JavaScript aggregation node calculates all key metrics 
including CTR, CPC, conversion rate, and ROAS from the raw 
campaign rows. The aggregated metrics are passed to an AI agent 
powered by Google Gemini that generates a structured plain-English 
performance narrative covering overall performance, top performer, 
underperformer, key observations, recommendations, and a numbered 
campaign breakdown. A Code node parses the narrative into named 
fields. The report is delivered simultaneously to the marketing 
team via Slack and to the team lead via Gmail. A Merge node 
ensures both deliveries complete before the master reporting 
sheet logs the full report as a new historical row.

## Tools Used

- n8n (automation engine)
- Google Sheets (campaign data source and master report log)
- Google Gemini (AI performance narrative generation)
- Slack (marketing team report delivery)
- Gmail (team lead report delivery)

## How to Use This Workflow

1. Download the workflow.json file
2. Open n8n and go to Workflows
3. Click Import and select the file
4. Connect your Google Sheets, Gemini, Slack, 
   and Gmail credentials
5. Update the Google Sheets document ID to your 
   campaign data sheet
6. Update the Master Sheet tab ID in the append node
7. Update the Slack channel ID to your marketing 
   team channel
8. Update the Gmail recipient address to your 
   team lead or client email
9. Populate your campaign data sheet with at least 
   five rows of campaign data across different channels
10. Activate the workflow and trigger it manually 
    to confirm before the first scheduled run

## Key Features

- Dedicated calendar node calculates current date and 
  previous week range once and shares these values 
  consistently across all downstream nodes
- JavaScript aggregation layer calculates CTR, CPC, 
  conversion rate, and ROAS from raw campaign data 
  before passing clean metrics to the AI agent
- AI performance analyst generates a structured 
  narrative covering overall performance, top performer, 
  underperformer, key observations, three actionable 
  recommendations, and a numbered campaign breakdown 
  as a single unified output regardless of how many 
  campaigns are included
- Code node parses the AI narrative into named fields 
  including overall narrative, key observations, 
  recommendations, campaign breakdown, and 
  ai overall narrative for flexible downstream use
- Simultaneous report delivery to Slack and Gmail 
  with error resilience on both nodes so one channel 
  failure does not block the other
- Merge node waits for both delivery channels to 
  complete before triggering the master sheet log, 
  ensuring the report is only recorded after successful 
  delivery
- Master sheet logs every report as a new historical 
  row with report date, date range, all aggregated 
  metrics, AI narrative, and report status for 
  trend analysis over time

## Business Impact

- Weekly reporting time reduced from hours of manual 
  work to zero manual effort
- Team receives actionable insights every Monday 
  morning before the work week begins
- Historical report log maintained automatically 
  for trend analysis and client presentations
- AI narrative replaces the need for a senior analyst 
  to interpret raw numbers every week
- Consistent report format delivered on time every 
  week regardless of team bandwidth or workload

## Known Limitations

- Campaign data is entered manually into the Google 
  Sheet, not pulled live from ad platforms via API
- Report covers only the channels represented in 
  the sheet, no automatic channel discovery
- AI narrative quality depends on the completeness 
  and accuracy of the data entered manually
- No anomaly detection in this version, the workflow 
  waits for the weekly schedule rather than alerting 
  the team immediately when a metric drops critically

## Planned Improvements

- Connect directly to Google Ads API and Meta 
  Marketing API to pull live campaign data 
  automatically without manual data entry
- Add a campaign anomaly detector that alerts the 
  team immediately when a metric drops below a 
  defined threshold rather than waiting for 
  the weekly report
- Add visual charts to the report using Google 
  Sheets chart embedding or a charting library
- Build a client-facing version of the report 
  with a simplified narrative and branded formatting