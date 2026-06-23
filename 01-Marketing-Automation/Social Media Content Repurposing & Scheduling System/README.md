# Social Media Content Repurposing & Scheduling System

## Business Problem

Marketing teams and content creators inside small and mid-sized 
businesses face the same bottleneck every week: they have ideas 
and long-form content but not enough time or bandwidth to adapt 
that content for every platform consistently. A blog post that 
could generate five LinkedIn posts, three X posts, and two 
newsletter blurbs sits untouched because repurposing feels like 
starting from scratch. The result is inconsistent posting, 
underutilized content, and a social media presence that goes 
quiet the moment the team gets busy with client work.

## System Solution

When a content piece or idea is submitted through a Tally form, 
the system passes it to ContentForge AI, a custom-configured AI 
writing engine built on Google Gemini. ContentForge AI generates 
three platform-specific content pieces simultaneously: a LinkedIn 
post of 150 to 300 words with a strong hook and call-to-action, 
an X post within the 280-character limit, and a newsletter teaser 
of two to three curiosity-driven sentences. All outputs are logged 
to a Google Sheets content calendar with a pending review status 
and the full content package is sent to the team on Slack for 
approval before scheduling.

## Tools Used

- n8n (automation engine)
- Tally (content submission form)
- Google Gemini (AI content generation via ContentForge AI)
- Google Sheets (content calendar logging)
- Slack (team review notification)

## How to Use This Workflow

1. Download the workflow.json file
2. Open n8n and go to Workflows
3. Click Import and select the file
4. Connect your Tally, Google Sheets, Slack, 
   and Gemini credentials
5. Update the Tally form ID to match your own form
6. Update the Slack channel ID to your content review channel
7. Update the Google Sheets document ID to your content calendar
8. Activate the workflow and submit a test content idea to confirm

## Key Features

- Custom AI persona (ContentForge AI) configured with platform 
  knowledge, tone rules, behavioral guardrails, and structured 
  output format
- Generates LinkedIn post, X post, and newsletter teaser 
  from a single content submission
- Tone selector on the intake form allows the business to 
  control output style across professional, conversational, 
  and bold
- Regex-based JavaScript parser extracts three separate content 
  blocks from a single AI text response without requiring JSON
- Content calendar logging to Google Sheets with date, platform, 
  content, and review status populated automatically
- Full content package delivered to the team via Slack with 
  clear visual formatting for easy review
- Merge node consolidates all three platform logging 
  branches before triggering the Slack notification, 
  ensuring the team alert only fires after all content 
  has been successfully logged to the content calendar

## Business Impact

- Content team stops rewriting the same idea three times 
  for three platforms
- Posting consistency maintained even during busy 
  client delivery periods
- Content calendar populated automatically with 
  every submission
- Team reviews and approves AI output instead of 
  writing from scratch
- One person with one idea can maintain a multi-platform 
  presence without a full content team

## Known Limitations

- All three platform outputs are logged in a single 
  Google Sheets row, preventing independent status 
  tracking per platform
- Content is generated but not auto-published, a human 
  review and approval step is required before posting
- No brand voice training in this version, tone is 
  controlled by form selection only
- System generates one set of outputs per submission, 
  no A/B variation in this version
- Switch node functions as a pass-through rather than 
  a true conditional router since all three content 
  fields are always populated on successful AI execution

## Planned Improvements

- Separate each platform output into its own Sheets row 
  for independent status tracking and approval
- Connect to a scheduling tool such as Buffer or Hootsuite 
  to auto-publish approved content
- Add brand voice training by including example posts 
  in the AI system prompt
- Build a Slack approval flow where the team can approve 
  or reject content directly without opening Sheets
