---
title: "Week 8 Worklog"
date: 2026-06-06
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
### Week 8 Objectives (June 6 - June 12, 2026):

* Continue the FCJ Management application deployment by creating an Auto Scaling Group (ASG)
* Configure Dynamic Scaling Policies based on CPU Utilization
* Explore Predictive Scaling using previously uploaded custom CloudWatch metrics
* Stress test the application to observe scaling in and scaling out behaviors
* Analyze scaling activity logs and understand the ASG lifecycle hooks

### Tasks to be carried out this week:

| Period | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| June 6 | - Review ASG concepts and integration with Application Load Balancer <br> - Resolve unhealthy target issues from the previous week | 06/06/2026 | 06/06/2026 | ASG Workshop Documentation |
| June 7 | - Create the Auto Scaling Group `FCJ-Management-ASG` <br> - Attach the ASG to the existing Target Group and ALB <br> - Set minimum, maximum, and desired capacity | 06/07/2026 | 06/07/2026 | ASG Creation section |
| June 8 | - Configure Dynamic Target Tracking Scaling Policy <br> - Set target CPU utilization to 50% for scale-out triggers | 06/08/2026 | 06/08/2026 | Dynamic Scaling section |
| June 9 | - Configure Predictive Scaling Policy using custom CloudWatch metrics <br> - Analyze historical data patterns for capacity forecasting | 06/09/2026 | 06/09/2026 | Predictive Scaling section |
| June 10 | - Perform stress testing using tools like Apache JMeter or AWS Fault Injection Simulator <br> - Monitor CloudWatch alarms triggering scale-out actions | 06/10/2026 | 06/10/2026 | Stress Testing section |
| June 11 | - Observe scale-in behavior after load decreases <br> - Verify application availability during scaling operations | 06/11/2026 | 06/11/2026 | Scaling Observation |
| June 12 | - Clean up resources (EC2, ASG, ALB, RDS, VPC) to prevent unexpected charges <br> - Summarize findings | 06/12/2026 | 06/12/2026 | Workshop Cleanup |

### Week 8 Achievements:

* **Auto Scaling Group Configuration:**
  * Successfully created and attached an Auto Scaling Group to the Application Load Balancer.
  * Configured Target Tracking scaling policies to dynamically adjust instance count based on traffic.
* **Predictive Scaling:**
  * Implemented predictive scaling to proactively launch instances ahead of anticipated traffic spikes.
* **Testing and Monitoring:**
  * Verified ASG functionality under load.
  * Monitored scaling activities and health checks to ensure high availability of the FCJ Management application.

### Key Learnings:

1. **ASG and ALB Integration:** Auto Scaling Groups work seamlessly with Load Balancers to distribute traffic to new instances automatically.
2. **Scaling Policies:** Choosing the right scaling policy (Dynamic vs. Predictive) depends on the workload pattern. Predictive scaling is excellent for predictable cyclical traffic.
3. **Cost Optimization:** ASG ensures you only run the instances you need, optimizing costs while maintaining performance.
