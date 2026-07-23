# AI-Powered Employee Onboarding Automation System

## Business Problem

Growing businesses onboard new employees inconsistently. The HR 
team manually sends welcome emails, creates folders, shares 
documents, assigns tasks, and notifies team members one step at 
a time. When HR is busy, steps get skipped. New hires arrive to 
find their accounts not set up, their manager not notified, and 
their first week unplanned. That experience signals disorganization 
before the employee has done a single day of work. A poor onboarding 
experience directly increases early employee turnover, which costs 
the business significantly more than the time it would have taken 
to do onboarding properly.

## System Solution

When a new hire's details are submitted through a Tally intake 
form, the workflow triggers immediately. An AI agent powered by 
Google Gemini generates a personalized 30-day onboarding task 
schedule specific to the hire's role and department. A JavaScript 
parser extracts the schedule and organizes all hire data into 
clean named fields. The new hire receives a welcome email followed 
immediately by their 30-day schedule email. A Google Drive personal 
folder is created inside the correct department folder automatically. 
A Notion page is created in the Employee Onboarding Hub database. 
A Switch node routes the workflow based on the hire's department, 
sending a notification to the relevant department Slack channel 
and a direct message to the hiring manager. All records are logged 
to a Google Sheet tracker with the hire's full details and 
onboarding status set to In Progress.

## Tools Used

- n8n (automation engine)
- Tally (new hire intake form)
- Google Gemini (AI-generated 30-day onboarding schedule)
- Gmail (welcome email and schedule delivery)
- Google Drive (department and personal folder creation)
- Notion (onboarding records database)
- Slack (department channel and manager notifications)
- Google Sheets (new hire log and onboarding tracker)

## How to Use This Workflow

1. Download the workflow.json file
2. Open n8n and go to Workflows
3. Click Import and select the file
4. Connect your Tally, Gmail, Google Drive, Notion, 
   Slack, Google Sheets, and Gemini credentials
5. Update the Tally form ID to match your intake form
6. Update the Google Drive parent folder IDs to match 
   your Employee Onboarding Hub department folders
7. Update the Notion database ID to your 
   Onboarding Records database
8. Update all Slack channel IDs and user IDs for 
   each department channel and manager
9. Update the Google Sheets document ID to 
   your new hire log
10. Activate the workflow and submit a test form 
    entry to confirm end to end execution

## Key Features

- AI Schedule Agent generates a personalized 30-day 
  onboarding task plan covering orientation, tools and 
  processes, independent contribution, and full 
  integration, tailored specifically to the hire's 
  role and department
- Seven department routes handled by a single Switch 
  node that evaluates the department field from the 
  form submission directly
- Google Drive personal folder created automatically 
  inside the correct department folder using a 
  two-step Drive node sequence that first retrieves 
  the department folder then creates the hire's 
  personal subfolder inside it
- Notion page created in the Employee Onboarding Hub 
  database with all hire details and status set to 
  In Progress automatically
- Department channel Slack notification alerts the 
  entire team before the manager DM fires, ensuring 
  the team hears first
- All seven department manager notification nodes 
  converge into a single Google Sheets Append Row 
  node, keeping the logging architecture clean 
  regardless of which department route fires
- New hire log maintained automatically with name, 
  email, role, department, manager, start date, 
  drive folder link, onboarding status, and 
  date created

## Business Impact

- Every new hire receives the same structured 
  professional onboarding experience regardless 
  of which HR team member is on duty
- HR team manual onboarding workload eliminated 
  entirely for standard hires across all seven departments
- Manager and department team notified automatically 
  before the new hire's first day
- Personalized 30-day task schedule delivered to 
  the new hire without any manual planning
- Onboarding tracker and Notion database maintained 
  automatically for HR reporting and compliance

## Known Limitations

- Notion page URL is not automatically logged to 
  Google Sheets in this version as it requires 
  manual retrieval from the Notion node output
- Role-based routing covers seven predefined 
  departments only, custom or unusual departments 
  require manual handling
- The 30-day task schedule is AI-generated and 
  may need customization per company culture 
  or internal processes
- Slack manager notifications use placeholder 
  user IDs for testing and must be updated to 
  real Slack user IDs before live deployment
- No integration with an HRIS such as BambooHR 
  or Workday in this version

## Planned Improvements

- Capture and log the Notion page URL automatically 
  to Google Sheets after page creation
- Connect to an HRIS to trigger onboarding 
  automatically when a new hire is added to 
  the HR system
- Add a check-in sequence that sends automated 
  week 1, week 2, and week 4 pulse check emails 
  to the new hire
- Build a manager dashboard in Notion that shows 
  all active onboardings and their current status
- Add a completion trigger that updates the 
  onboarding status to Completed automatically 
  after 30 days
