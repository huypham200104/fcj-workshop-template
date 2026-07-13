---
title: "Week 12 Worklog"
date: 2026-07-04
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---
### Week 12 Objectives (July 4 - July 30, 2026):

* **Authentication & Security:** Implement Amazon Cognito for User/Staff login, and secure API Gateway with JWT Authorizers. Apply AWS KMS for data encryption.
* **Event-Driven Notifications:** Build an asynchronous notification flow using Amazon SQS (FIFO), AWS Lambda (Notification Worker), and Amazon SES to send emails. Configure Dead Letter Queue (DLQ) for failed messages.
* **Monitoring & Backup:** Centralize logs, metrics, and errors using Amazon CloudWatch. Set up CloudWatch Alarms to trigger Amazon SNS for error alerts. Configure AWS Backup for DynamoDB and S3.
* **Final Delivery:** Finalize the project, perform end-to-end testing, and prepare the internship completion report.

### Tasks to be carried out this week:

| Period | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| July 4 | - Set up Amazon Cognito User Pools for authentication <br> - Integrate Cognito into Frontend and pass JWT Tokens to API Gateway <br> - Configure API Gateway Authorizers to verify JWT tokens | 07/04/2026 | 07/04/2026 | AWS Cognito Docs |
| July 5 | - Create Amazon SQS FIFO Queue and Dead Letter Queue (DLQ) <br> - Update Ticket Handler Lambda to publish notification events to SQS | 07/05/2026 | 07/05/2026 | AWS SQS Docs |
| July 6 | - Develop Notification Worker Lambda to read from SQS and send emails via Amazon SES <br> - Test failure scenarios to verify messages are routed to the DLQ | 07/06/2026 | 07/06/2026 | AWS SES Integration |
| July 7 | - Implement AWS KMS to encrypt sensitive data <br> - Set up AWS Backup to schedule automated backups for DynamoDB (PITR) and Amazon S3 | 07/07/2026 | 07/07/2026 | AWS Security & Backup |
| July 8 | - Configure CloudWatch to monitor API Logs, Lambda Logs, and system metrics <br> - Create CloudWatch Alarms to trigger Amazon SNS for developer alerts on errors/threshold breaches | 07/08/2026 | 07/08/2026 | CloudWatch & SNS |
| July 9 | - Conduct full End-to-End System Testing (Desktop & Mobile) <br> - Verify all features: Ticket Creation, Search/Filter/Sort, Notifications, UI Feedback | 07/09/2026 | 07/09/2026 | QA Testing |
| July 10 | - Final Project Presentation Preparation <br> - Complete the Internship Report and wrap up the FCJ Bootcamp | 07/10/2026 | 07/10/2026 | Presentation Docs |

### Week 12 Achievements:

* **Robust Event-Driven Notifications:**
  * Successfully decoupled ticket processing and email notifications using SQS FIFO. Handled failure resilience flawlessly using DLQ.
* **Comprehensive Security Layer:**
  * System is now secured with Amazon Cognito (JWT validation at API Gateway). All data at rest is encrypted via AWS KMS, and critical data is protected by AWS Backup.
* **Proactive Monitoring:**
  * Developers are instantly alerted via SNS when CloudWatch detects an API spike or Lambda execution errors, ensuring quick issue resolution.
* **Successful Project Completion:**
  * The Serverless Helpdesk Portal functions exactly as designed, meeting all UI requirements and Serverless architecture standards.

### Key Learnings:

1. **Asynchronous Architecture:** Decoupling services using Amazon SQS makes the application much more resilient. If SES fails to send an email, the ticket creation process is not blocked, and the DLQ captures the failure for later retry.
2. **Security at Every Layer:** Utilizing Cognito for Auth, WAF for Edge protection, API Gateway Authorizers for access control, and KMS for encryption ensures enterprise-grade security.
3. **Observability is Critical:** In a Serverless environment, having centralized logging and alerting (CloudWatch + SNS) is the only reliable way to troubleshoot and maintain system health proactively.
