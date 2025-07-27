# n8n Automation Projects


## Projects Included

### 1. Lead Scoring Automation (POSTMAN)
- Receives lead data as JSON via webhook (API call)
- Automates scoring of incoming leads based on company size, budget, and email domain.
- Stores results in Google Sheets.
- Sends notifications to Slack for high-value leads.

### 2. Lead Source Simulation (Lead-Source)
- Simulates lead data generation on a schedule.
- Processes leads and scores them.
- Demonstrates automation from simulated data to database and notifications.


#### Projects Overview
1. Lead Scoring and Notification Workflow
Receives leads via webhook (e.g., from Postman API call).

Calculates a custom lead score based on employee count, budget, and email domain.

Stores scored leads in Google Sheets.

Sends Slack notifications for high-value leads (score > 60).

Sends notifications for lower score leads separately.

2. Lead Source Simulator Workflow
Simulates lead submissions on a schedule.

Uses the same scoring logic and processes leads identically.

Demonstrates automation of lead source simulation and follow-up.

##### Setup & Usage
Prerequisites:
An n8n Cloud or self-hosted n8n instance.

Google Sheets API credentials (OAuth or Service Account).

Slack app token with permission to send messages to your workspace.

Import Workflows:
Import the JSON workflow files (My workflow.json and REM Waste-Lead Source.json) into your n8n instance.

Set up credentials for Google Sheets and Slack in n8n.

Update Google Sheets node to point to your own spreadsheet.

Update Slack node with your Slack channel(s).

Run the Workflows:
For the Lead Scoring workflow, send POST requests with leads JSON payload to the webhook URL.

For the Lead Source Simulator, activate the scheduled trigger node to simulate lead submissions automatically.

JSON Lead Payload Format:
The workflows expect leads in this JSON structure:

{
  "submissionBatchId": "BATCH-20250727-003",
  "receivedAt": "2025-07-27T13:54:21Z",
  "leads": [
    {
      "firstName": "Liam",
      "lastName": "Parker",
      "email": "liam.parker@techwave.com",
      "phone": "+1-555-111-2222",
      "company": "TechWave Solutions",
      "jobTitle": "Head of Engineering",
      "leadSource": "Website Form",
      "industry": "Cloud Computing",
      "employees": 750,
      "budget": 250000,
      "notes": "Interested in scalable infrastructure solutions.",
      "productsOfInterest": ["Cloud Platform X", "Data Analytics Suite"],
      "customField": "Initial Inquiry"
    }
  ]
}

Lead Scoring Logic:
Employees > 500 → +30 points

Employees > 100 → +15 points

Budget > 150,000 → +25 points

Budget > 50,000 → +10 points

Business email (non-personal domains) → +15 points

Notes:
Phone numbers are normalized (removing symbols) before saving.

Slack messages are formatted using markdown for clarity.

Leads with a score > 60 trigger "high-value" Slack alerts; others go to a separate channel.
