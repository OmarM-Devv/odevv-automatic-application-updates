# n8n Automatic Application Updates

A personal job-application tracking workflow built in n8n. It listens for Gmail messages, filters out irrelevant emails, uses AI to decide whether an email is related to an application, writes the result to a Google Sheet, and sends Discord notifications for application updates and approaching deadlines.

This repository contains a single exported workflow file: `workflow.json`.

## What the workflow does

- Monitors incoming Gmail messages in real time
- Filters out non-job-related emails and promotions
- Uses OpenAI to classify email content and extract application details
- Appends or updates a row in a Google Sheet with details such as:
  - Company
  - Role
  - Date applied
  - Status
  - Action deadline
- Runs on a schedule to check pending applications
- Calculates how many days remain before a required action
- Sends Discord alerts when:
  - a new application status changes
  - a deadline is approaching
  - an application needs attention

## Workflow overview

The exported workflow includes these major stages:

1. Gmail Trigger
   - Watches for new email activity
2. Relevance Filter
   - Ignores spam, promotions, and unrelated messages
3. AI Classification
   - Uses an OpenAI model to identify whether the message is about a job application
4. Sheet Update
   - Adds or updates application data in Google Sheets
5. Scheduled Review
   - Checks tracked applications for pending follow-ups
6. Discord Notifications
   - Sends user-facing reminders and status messages

## Repository contents

- `workflow.json` — the complete n8n workflow export

## Prerequisites

Before importing this workflow, make sure you have:

- An n8n instance running
- A Gmail account with OAuth access
- A Google Sheets document and access permissions
- An OpenAI API key and a model available in your n8n setup
- A Discord bot and user ID for notifications

## Setup instructions

1. Open n8n and import `workflow.json`.
2. Configure credentials for:
   - Gmail
   - Google Sheets
   - OpenAI
   - Discord
3. Update the Google Sheets nodes to point to your spreadsheet and sheet.
4. Set the Discord user ID for notifications in the relevant node configuration.
5. Review and adjust the workflow fields if you want different statuses, deadline logic, or notification timing.
6. Activate the workflow and test with a sample email.

## Example Google Sheet structure

The workflow expects a sheet with columns similar to:

| COMPANY | ROLE | DATE APPLIED | STATUS | ACTION DEADLINE |
| --- | --- | --- | --- | --- |
| Example Corp | Software Engineer | 2026-09-22 | TO APPLY | 2026-09-27 |

The workflow uses the company name as the matching key for updates, which helps prevent duplicate rows for the same application.

## Status handling

The workflow is designed to track application progress using statuses such as:

- TO APPLY
- ASSESSMENT
- INTERVIEW
- UNKNOWN
- APPLIED
- REJECTED

These values are used both for tracking and for deciding when to send reminders.

## Notes

- This project is not a standalone application with a package.json or server runtime. It is an n8n automation workflow export.
- You may need to customize the AI prompt and Google Sheets field mappings for your own workflow and job-tracking needs.
- For best results, review the workflow nodes after import to validate credentials, document IDs, and notification settings.

## Typical use case

This workflow is useful for anyone who wants to:

- keep track of job applications in one spreadsheet
- reduce inbox noise from recruitment emails
- automate status follow-ups
- get reminders before deadlines or scheduled responses are due

## Future improvements

Possible enhancements include:

- adding a dedicated job board or tracker dashboard
- storing more metadata per application
- integrating with email labels or filters
- sending alerts to Slack or Telegram instead of Discord
- using a custom database or Airtable instead of Google Sheets
