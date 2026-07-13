---
title: "Week 9 Worklog"
date: 2026-06-13
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
### Week 9 Objectives (June 13 - June 19, 2026):

* Understand Serverless architecture and its benefits (No server management, pay-for-value)
* Build a Serverless backend using AWS Lambda and Amazon API Gateway
* Store and retrieve data using Amazon DynamoDB (NoSQL database)
* Secure APIs using IAM and API Gateway authorizers
* Monitor and troubleshoot serverless applications using AWS X-Ray and CloudWatch

### Tasks to be carried out this week:

| Period | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| June 13 | - Introduction to Serverless Concepts (Lambda, API Gateway, DynamoDB) <br> - Design the architecture for a simple serverless To-Do application | 06/13/2026 | 06/13/2026 | Serverless Workshop |
| June 14 | - Create an Amazon DynamoDB table `ToDoItems` with Partition Key `id` <br> - Understand DynamoDB Read/Write capacity modes | 06/14/2026 | 06/14/2026 | DynamoDB section |
| June 15 | - Create an IAM Role with least-privilege permissions for Lambda <br> - Write AWS Lambda functions (Node.js/Python) for CRUD operations | 06/15/2026 | 06/15/2026 | Lambda section |
| June 16 | - Configure Amazon API Gateway as the front door for Lambda <br> - Set up RESTful routes (GET, POST, PUT, DELETE) and CORS | 06/16/2026 | 06/16/2026 | API Gateway section |
| June 17 | - Test the API endpoints using Postman or cURL <br> - Integrate API Gateway with Lambda using Proxy Integration | 06/17/2026 | 06/17/2026 | API Testing |
| June 18 | - Implement API authentication using Amazon Cognito User Pools (optional) or API Keys <br> - Enable AWS X-Ray for distributed tracing | 06/18/2026 | 06/18/2026 | Security & Monitoring |
| June 19 | - Review CloudWatch Logs for Lambda executions <br> - Clean up serverless resources | 06/19/2026 | 06/19/2026 | Review & Cleanup |

### Week 9 Achievements:

* **Serverless Backend:**
  * Successfully deployed a fully functional Serverless REST API without provisioning any servers.
* **Database Integration:**
  * Designed and utilized DynamoDB for fast, scalable NoSQL data storage.
* **Security & Tracing:**
  * Secured the API endpoints and enabled X-Ray tracing to understand invocation bottlenecks.

### Key Learnings:

1. **Pay-as-you-go Model:** Serverless computing charges only for the compute time consumed, making it highly cost-effective for variable workloads.
2. **Stateless Nature:** Lambda functions are stateless, requiring external storage like DynamoDB to persist application data.
3. **API Management:** API Gateway simplifies request routing, throttling, and authorization, acting as a robust entry point for microservices.
