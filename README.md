# Daily Open Case Aging & Action Reminder Automation

## Project Overview

Built a scheduled Microsoft Power Automate workflow to automate daily monitoring of open support cases.

The workflow reads case data from Excel stored in OneDrive, identifies open and aging cases, groups cases by agent, sends personalized Microsoft Teams reminders, and provides management with a consolidated daily summary.

> All data used in this project is synthetic and created for portfolio purposes.

## Business Problem

Support teams may manage hundreds of open cases across multiple agents. Manually reviewing case aging every day is repetitive and can result in older cases being overlooked.

The goal was to automate this monitoring process and proactively highlight cases requiring attention.

## Business Rule

- Open case age **0–5 days** → `OPEN`
- Open case age **>5 days** → `ACTION REQUIRED`
- Each agent receives one consolidated reminder containing their open cases.
- Management receives one daily team-level summary.

## Dataset

The synthetic dataset contains:

- 500 support cases
- 25 agents
- 300 open cases
- 200 closed cases

Key fields include:

`Case_ID`, `Agent_Name`, `Agent_Email`, `Status`, `Created_Date`, `Priority`, `Product`, and `Country`.

## Automation Workflow

1. A scheduled Recurrence trigger starts the workflow.
2. Excel Online retrieves the case dataset from OneDrive.
3. Filter Array selects only Open cases.
4. Case aging is calculated from Created Date.
5. Cases older than five days are identified as requiring action.
6. Agent details are extracted and duplicate agents are removed.
7. Apply to Each processes each unique agent.
8. The workflow filters the open cases belonging to the current agent.
9. Select formats Case ID, Age and Action Status.
10. The case array is consolidated into one readable message.
11. Microsoft Teams sends a personalized reminder to each agent.
12. After agent processing is complete, management receives one consolidated summary.

## Workflow Overview

![Power Automate Flow](screenshots/flow-overview.png)

## Agent Reminder

Each agent receives one consolidated reminder containing their open cases and aging status.

![Agent Reminder](screenshots/agent-reminder.png)

Example output:

`CASE-10064 | Age: 6 Days | ACTION REQUIRED`

`CASE-10264 | Age: 5 Days | OPEN`

## Manager Summary

Management receives one daily summary containing:

- Total Open Cases
- Action Required (>5 Days)
- Cases Within 5 Days

![Manager Summary](screenshots/manager-summary.png)

## Testing Approach

The project uses 25 synthetic agents to simulate a multi-agent support environment.

During testing, all synthetic agents were temporarily mapped to a single authorized Microsoft Teams test account. This allowed dynamic routing, agent-level filtering, case-aging logic, and personalized reminders to be validated without requiring 25 real Microsoft 365 accounts.

In a production implementation, each agent would have a valid organizational email/UPN and the workflow would dynamically route each reminder to the appropriate agent.

The public dataset uses fictional `@example.com` email addresses.

## Process Improvement

### AS-IS

Agents or managers manually review open cases and determine which cases require attention.

### TO-BE

`Case Data → Filter Open Cases → Calculate Aging → Identify Action Required Cases → Group by Agent → Agent Reminder → Manager Summary`

The automated process reduces repetitive monitoring and provides proactive visibility into aging cases.

## Power Automate Concepts Used

- Scheduled Cloud Flow
- Excel Online (Business)
- OneDrive for Business
- Filter Array
- Select
- Apply to Each
- Dynamic Content
- Power Automate Expressions
- Array Functions
- Dynamic Recipient Routing
- Microsoft Teams Connector

## Key Technical Logic

Excel dates returned by the connector were handled using Excel serial-date conversion before calculating case age.

Cases were classified dynamically using the five-day business rule.

The formatted case array was consolidated using `join()` so each agent receives one Teams message containing all of their open cases rather than separate messages for individual cases.

## Skills Demonstrated

- Business Process Analysis
- Process Improvement
- Workflow Automation
- Business Rule Implementation
- Data Filtering & Transformation
- Operational Reporting
- Case Aging Analysis
- Dynamic Routing
- Microsoft Power Automate
- Testing & Troubleshooting

## Data Privacy

This repository contains only synthetic portfolio data.

No real customer information, employee information, support cases, credentials, or proprietary organizational data is included.
