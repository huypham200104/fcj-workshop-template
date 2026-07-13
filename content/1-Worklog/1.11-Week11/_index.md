---
title: "Week 11 Worklog"
date: 2026-06-27
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---
### Week 11 Objectives (June 27 - July 3, 2026):

* **Final Project Kickoff:** Start building the Serverless Helpdesk Portal (Jira Service Management / Freshservice style).
* **Frontend Setup:** Develop a responsive, modern Dashboard using AWS Orange, White, and Dark Gray color themes. Host on Amazon S3 and deliver via CloudFront protected by AWS WAF.
* **Core Backend Setup:** Build the foundational Serverless architecture using API Gateway, AWS Lambda, and Amazon DynamoDB (for tickets) and Amazon S3 (for ticket attachments).
* **CI/CD Pipeline Integration:** Automate deployment for both Frontend and Backend using AWS CodeCommit, CodeBuild, and CodePipeline.

### Tasks to be carried out this week:

| Period | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| June 27 | - Project kickoff and Architecture analysis <br> - Set up CI/CD pipelines (CodeCommit, CodeBuild, CodePipeline) for automatic deployment of Frontend to S3 and Backend to Lambda | 06/27/2026 | 06/27/2026 | Architecture Diagram |
| June 28 | - Develop core Frontend UI components (Dashboard, fixed Sidebar, Header, Stats Cards) <br> - Ensure responsiveness across Desktop, Tablet, and Mobile | 06/28/2026 | 06/28/2026 | UI/UX Requirements |
| June 29 | - Develop Data Table with Pagination, Search, Filter, and Sort capabilities <br> - Add UX elements (Confirmation Modals, Toast Notifications, Loading Spinners) | 06/29/2026 | 06/29/2026 | Frontend Framework Docs |
| June 30 | - Design DynamoDB schema for the Ticket database <br> - Create an S3 bucket for storing ticket attachments | 06/30/2026 | 06/30/2026 | AWS DynamoDB Docs |
| July 1 | - Develop Core Backend (Ticket Handler Lambda) for creating, reading, and updating tickets <br> - Configure Amazon API Gateway routes and integrations | 07/01/2026 | 07/01/2026 | AWS Lambda & API GW |
| July 2 | - Deploy Frontend to S3 and configure CloudFront distribution <br> - Integrate Frontend with Backend APIs (No business logic in Frontend) | 07/02/2026 | 07/02/2026 | S3 Static Hosting |
| July 3 | - Attach AWS WAF to CloudFront for layer 7 protection <br> - End-of-week integration testing and bug fixing | 07/03/2026 | 07/03/2026 | AWS WAF Docs |

### Week 11 Achievements:

* **CI/CD Automation:**
  * Successfully separated Frontend and Backend pipelines. Any commit to CodeCommit now triggers CodeBuild and automatically deploys to S3/CloudFront or AWS Lambda.
* **Modern Frontend UI:**
  * Completed the base layout for the Helpdesk Portal. The UI is highly responsive, featuring a Jira Service Management look, complete with Data Tables, Modals, and Spinners.
* **Serverless Backend Core:**
  * Set up API Gateway as the sole entry point to trigger Lambda functions. Tickets are successfully stored in DynamoDB, and attachments are uploaded securely to S3.

### Key Learnings:

1. **Separation of Concerns:** By keeping absolutely no business logic on the Frontend, the application remains lightweight, secure, and easier to scale.
2. **Automated Workflows:** Having CI/CD ready from Day 1 drastically reduced the time spent on manual deployments, allowing the team to focus entirely on coding.
3. **WAF & CloudFront Integration:** Placing WAF directly on CloudFront ensures malicious requests are blocked at the edge, saving Lambda invocation costs and protecting backend resources.
