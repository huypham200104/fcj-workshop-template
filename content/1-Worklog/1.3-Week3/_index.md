---
title: "Week 3 Worklog"
date: 2026-05-02
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}

### Week 3 Objectives (May 2 - May 15, 2026):

* Understand the role of Amazon CloudWatch in monitoring AWS resources and applications
* Practice working with CloudWatch Metrics, Logs, Logs Insights, Metric Filters, Alarms, and Dashboards
* Convert application logs into measurable metrics for operational monitoring
* Configure email notifications through Amazon SNS when an alarm threshold is reached
* Build a CloudWatch dashboard to centralize important monitoring signals

### Tasks to be carried out this week:

| Period | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| May 2 - May 4 | - Review the Amazon CloudWatch workshop overview <br> - Understand CloudWatch concepts: metrics, logs, alarms, and dashboards <br> - Prepare the workshop environment and EC2 resources | 05/02/2026 | 05/04/2026 | <https://000008.awsstudygroup.com/vi/> |
| May 5 - May 7 | - Explore CloudWatch Metrics <br> - Compare EC2 and CWAgent metrics <br> - Use search expressions to filter metrics <br> - Add annotations and adjust graph display options | 05/05/2026 | 05/07/2026 | CloudWatch Metric section |
| May 8 - May 10 | - Practice metric math expressions such as sorting and filtering top metrics <br> - Create dynamic labels for clearer metric legends <br> - Analyze process memory metrics from the CloudWatch Agent namespace | 05/08/2026 | 05/10/2026 | CloudWatch Metric section |
| May 11 - May 13 | - Work with CloudWatch Logs and Logs Insights <br> - Query application logs by keyword such as `ERROR` and `WARN` <br> - Create a metric filter from `/var/log/messages` error logs | 05/11/2026 | 05/13/2026 | CloudWatch Logs section |
| May 14 - May 15 | - Create a CloudWatch Alarm for error logs <br> - Configure SNS email subscription and confirm the subscription <br> - Add the alarm widget to a CloudWatch Dashboard <br> - Review results and document lessons learned | 05/14/2026 | 05/15/2026 | CloudWatch Alarms and Dashboards sections |

### Week 3 Achievements:

* **CloudWatch Metrics:**
  * Viewed and compared EC2 metrics and custom CWAgent metrics
  * Used search expressions to quickly find relevant metrics
  * Applied metric math to sort and filter displayed metrics
  * Created dynamic labels to make metric legends easier to read

* **CloudWatch Logs and Logs Insights:**
  * Worked with application logs stored in CloudWatch Logs
  * Queried logs using Logs Insights to identify `ERROR` and `WARN` events
  * Learned how log queries support faster troubleshooting and root-cause analysis

* **Metric Filter Implementation:**
  * Created a metric filter for error logs from `/var/log/messages`
  * Converted log events into a measurable CloudWatch metric
  * Used the metric namespace `ec2-logs` and metric name `/var/log/messages - ERROR`

* **CloudWatch Alarm and SNS Notification:**
  * Created the `PythonApplicationErrorAlarm` alarm for error log count monitoring
  * Configured the threshold condition so the alarm is triggered when error logs exceed the expected limit
  * Created and confirmed the SNS topic subscription for email notifications

* **CloudWatch Dashboard:**
  * Created the `CloudWatch-Workshop` dashboard
  * Added the alarm widget to the dashboard
  * Used the dashboard to centralize monitoring information for easier operational review

### Evidence and Analysis:

* **Metric visualization and dynamic labels:** The screenshot below shows CloudWatch Metrics using the `CWAgent` namespace and the `procstat_memory_rss` metric. Dynamic labels help distinguish process, instance, and metric information directly in the graph legend.

{{< image src="images/worklog/week3_cloudwatch_metrics.jpg" alt="CloudWatch Metrics with dynamic labels" >}}

* **SNS subscription confirmation:** The email notification from AWS Notifications confirms that the SNS topic was created and required email subscription confirmation before alarm notifications could be received.

{{< image src="images/worklog/week3_sns_subscription.jpg" alt="AWS SNS subscription confirmation email" >}}

* **CloudWatch Dashboard result:** The dashboard contains the `PythonApplicationErrorAlarm` widget, allowing the error log alarm state to be monitored from one central screen.

{{< image src="images/worklog/week3_cloudwatch_dashboard.jpg" alt="CloudWatch Workshop dashboard with alarm widget" >}}

### AWS Report Analysis:

* **Architecture fit:** CloudWatch Metrics, Logs, Metric Filters, Alarms, SNS, and Dashboards form a complete observability flow. Logs capture raw application behavior, metric filters convert important log patterns into measurable signals, alarms evaluate thresholds, SNS delivers notifications, and dashboards provide a consolidated operational view.

* **Operational value:** This workflow is useful because it reduces the time needed to detect application errors. Instead of manually checking EC2 logs, the system can surface error counts and notify the owner when the threshold is crossed.

* **Monitoring quality:** Dynamic labels and dashboard widgets improve readability when multiple instances or processes are monitored. This is important for scaling the same monitoring approach to more EC2 instances.

* **Risks and controls:** The main risks are noisy alarms, missing SNS confirmation, and metric filters that do not match the expected log pattern. These risks can be reduced by testing filter patterns, choosing realistic thresholds, confirming SNS subscriptions, and reviewing alarm history after deployment.

### Key Learnings:

1. **Metrics provide measurable system behavior** - CloudWatch Metrics help compare resource usage and detect unusual trends.
2. **Logs Insights improves troubleshooting** - Querying logs by keyword and time range is faster than manually reading raw logs.
3. **Metric Filters connect logs and alarms** - Important log patterns can become metrics that support automated alerting.
4. **SNS confirmation is required** - Email notifications only work after the subscription is confirmed.
5. **Dashboards improve visibility** - A dashboard brings alarms and metrics together for easier monitoring.

### Resources Used:

* AWS CloudWatch Workshop: <https://000008.awsstudygroup.com/vi/>
* Amazon CloudWatch Metrics
* Amazon CloudWatch Logs and Logs Insights
* CloudWatch Metric Filters
* CloudWatch Alarms
* Amazon SNS
* CloudWatch Dashboards
