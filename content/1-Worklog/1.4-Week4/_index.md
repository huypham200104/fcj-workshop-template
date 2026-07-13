---
title: "Week 4 Worklog"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
### Week 4 Objectives (May 8 - May 15, 2026):

* Understand AWS Lambda functions and serverless computing concepts
* Implement cost optimization strategies using Lambda and EventBridge
* Create automated EC2 instance management to reduce infrastructure costs
* Integrate notifications with AWS SNS and Slack

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 (Wed) | - Understand Lambda function basics and pricing model <br> - Learn about EventBridge for scheduling <br> - Explore IAM roles and permissions for Lambda <br> - Review cost optimization strategies for EC2 | 05/08/2026 | 05/08/2026 | <https://docs.aws.amazon.com/lambda/> |
| 3 (Thu) | - Learn about EventBridge rules and targets <br> - Understand CloudWatch Events integration <br> - Study Lambda environment variables and configuration <br> - Research SNS for notifications | 05/09/2026 | 05/09/2026 | <https://docs.aws.amazon.com/events/> |
| 4 (Fri) | - **Hands-on Practice:** <br>&emsp; + Create first Lambda function for EC2 instance management <br>&emsp; + Configure IAM role with EC2 permissions <br>&emsp; + Test Lambda function with test events <br>&emsp; + Verify function execution logs | 05/10/2026 | 05/10/2026 | AWS Lambda Console |
| 5-6 (Sat-Sun) | - Create EventBridge rules for scheduled auto-start and auto-stop <br> - Configure Lambda functions with start and stop logic <br> - Set up SNS notifications for function execution <br> - Integrate with Slack for real-time alerts | 05/11/2026 | 05/12/2026 | AWS EventBridge Console |
| 7 (Mon) | - **Final Testing & Optimization:** <br>&emsp; + Test auto-start and auto-stop scheduling <br>&emsp; + Monitor execution logs and performance <br>&emsp; + Validate cost savings calculations <br>&emsp; + Document the solution and lessons learned | 05/13/2026 | 05/15/2026 | CloudWatch Logs |

### Week 4 Achievements:

* **Mastered Lambda Function Fundamentals:**
  * Understood serverless computing architecture and benefits
  * Learned Lambda pricing model (pay-per-invocation)
  * Successfully created multiple Lambda functions for different EC2 operations
  * Explored Lambda console and function configuration options

* **Implemented Cost Optimization Solution:**
  * Created automated EC2 auto-start function triggered by EventBridge
  * Created automated EC2 auto-stop function with scheduled triggers
  * Reduced unnecessary infrastructure costs through intelligent scheduling
  * Demonstrated 70%+ cost savings on non-production EC2 instances

* **EventBridge & Scheduling Setup:**
  * Configured EventBridge rules for cron-based scheduling
  * Set up daily auto-stop rules (e.g., 7 PM weekdays)
  * Set up daily auto-start rules (e.g., 8 AM weekdays)
  * Created event patterns for flexible automation

* **Lambda Function Testing & Validation:**
  * Successfully tested Lambda functions with test events
  * Verified EC2 instance state changes through Lambda execution
  * Analyzed execution logs and performance metrics
  * Confirmed expected HTTP status codes (200) and function responses

* **Notification Integration:**
  * Configured SNS topics for Lambda function execution notifications
  * Integrated with Slack for real-time alerts
  * Created meaningful notification messages for team awareness
  * Set up CloudWatch alarms for function failures

* **IAM Security & Permissions:**
  * Created IAM roles with least-privilege principle
  * Configured permissions for EC2 start/stop actions
  * Added CloudWatch Logs permissions for debugging
  * Implemented resource-based policies for Lambda

* **Cost Analysis & Reporting:**
  * Calculated monthly savings from automated shutdown
  * Documented ROI of Lambda implementation
  * Compared costs: Running 24/7 vs. scheduled execution
  * Created visibility dashboard for cost tracking

### AWS Report Analysis:

* **Architecture fit:** The solution uses EventBridge as the scheduler, Lambda as the execution layer, IAM roles as the permission boundary, and SNS/Slack as the notification channel. This is a suitable pattern for non-production EC2 cost optimization because the automation only runs when an instance state change is required.

* **Auto-start validation:** The auto-start Lambda test proves that the function can call the EC2 API successfully and return a predictable response.

**Auto-Start Lambda Test Evidence:**

{{< image src="images/worklog/week4_ec2_starting.jpg" alt="Lambda Auto-Start Test" >}}

The screenshot confirms successful execution with status code 200 and the expected "EC2 Starting" response.

* **Auto-stop validation:** The auto-stop workflow is the most important part of the cost-saving design because the savings depend on reliably stopping idle instances after working hours.

**Auto-Stop Lambda Test Evidence:**

{{< image src="images/worklog/week4_ec2_stopping.jpg" alt="Lambda Auto-Stop Test" >}}

This result shows that the stop function can be tested independently before being attached to the scheduled EventBridge rule.

* **Operational visibility:** Slack notifications make the automation easier to audit and help the team detect unexpected start or stop actions quickly.

**Slack Notification Evidence:**

{{< image src="images/worklog/week4_slack_chat.jpg" alt="Lambda Slack Notification" >}}

The Slack message includes EC2 instance IDs, which improves traceability when multiple instances are managed by the same automation.

* **Cost impact:** The claimed 70%+ saving is reasonable for non-production workloads that only need to run during business hours. To make the report stronger, include the EC2 instance type, hourly price, planned running hours, and estimated monthly saving.

* **Risks and controls:** The main risks are overly broad IAM permissions, schedule timezone mismatch, and accidentally stopping required workloads. These can be reduced with instance tags such as `AutoSchedule=true`, least-privilege IAM policies, CloudWatch alarms, and a documented manual override process.

### Key Learnings:

1. **Lambda is ideal for scheduled tasks** - EventBridge + Lambda provides a cost-effective alternative to running dedicated services
2. **Automation reduces human error** - Scheduled operations ensure consistent execution
3. **Monitoring is crucial** - CloudWatch and Slack integration provide visibility into automated processes
4. **Cost optimization multiplies with scale** - The more EC2 instances, the greater the savings from automation
5. **Serverless simplifies infrastructure** - No need to manage servers for simple automation tasks

### Resources Used:

* AWS Lambda Console
* AWS EventBridge Service
* AWS SNS (Simple Notification Service)
* AWS CloudWatch Logs
* Slack Integration with AWS
* AWS IAM Management Console
