---
title: "Week 6 Worklog"
date: 2026-05-23
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---
### Week 6 Objectives (May 23 - May 29, 2026):

* Understand how AWS Backup centralizes backup and restore operations for AWS resources
* Prepare workshop infrastructure using Amazon S3 and AWS CloudFormation
* Create a Backup Plan, Backup Rule, Backup Vault, and Resource Assignment
* Enable backup and restore notifications through Amazon SNS
* Run an on-demand backup for an EC2 instance and validate the backup job result
* Test restore automation using AWS Lambda and verify restore status through CloudWatch Logs and email notifications

### Tasks to be carried out this week:

| Period | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| May 23 | - Review the AWS Backup workshop introduction <br> - Understand backup planning, RTO, RPO, recovery points, and restore validation <br> - Identify the services used in the lab: S3, CloudFormation, EC2, SNS, Lambda, CloudWatch, and AWS Backup | 05/23/2026 | 05/23/2026 | <https://000013.awsstudygroup.com/vi/1-introduce/> |
| May 24 | - Create an S3 bucket for workshop source files <br> - Upload the CloudFormation template and Lambda function package <br> - Prepare S3 object URLs for stack deployment | 05/24/2026 | 05/24/2026 | Preparation section |
| May 25 | - Deploy the lab infrastructure using CloudFormation <br> - Configure stack parameters such as notification email, S3 bucket name, and Lambda package path <br> - Review stack outputs including the application URL and resource identifiers | 05/25/2026 | 05/25/2026 | Infrastructure deployment section |
| May 26 | - Create the `BACKUP-LAB` Backup Plan <br> - Configure the `BACKUP-LAB-RULE` daily backup rule <br> - Create the `BACKUP-LAB-VAULT` Backup Vault <br> - Assign EC2 resources to the backup plan using tags | 05/26/2026 | 05/26/2026 | Backup plan section |
| May 27 | - Enable Backup Vault notifications with Amazon SNS <br> - Configure events such as `BACKUP_JOB_COMPLETED` and `RESTORE_JOB_COMPLETED` <br> - Confirm that backup completion emails are delivered | 05/27/2026 | 05/27/2026 | Notification section |
| May 28 | - Create an on-demand backup for the EC2 instance <br> - Monitor the Backup job until it reaches `Completed` <br> - Review the generated recovery point ARN | 05/28/2026 | 05/28/2026 | Test restore section |
| May 29 | - Validate restore testing through AWS Backup Restore jobs <br> - Review CloudWatch Logs for the restore test Lambda function <br> - Confirm HTTP 200 validation and cleanup notification email | 05/29/2026 | 05/29/2026 | Test restore section |

### Week 6 Achievements:

* **AWS Backup Planning:**
  * Learned how AWS Backup manages backup policies from a centralized service
  * Understood why RTO and RPO should be defined per workload
  * Created a plan-based backup workflow instead of relying on manual snapshots

* **Infrastructure Preparation:**
  * Created an S3 bucket to store the CloudFormation template and Lambda package
  * Deployed supporting infrastructure with CloudFormation
  * Prepared an EC2 instance, SNS topic, and Lambda restore test function for the lab

* **Backup Plan and Resource Assignment:**
  * Created the `BACKUP-LAB` backup plan
  * Created the `BACKUP-LAB-RULE` backup rule and `BACKUP-LAB-VAULT` backup vault
  * Assigned EC2 resources to the plan using tag-based resource selection
  * Used the default AWS Backup IAM role for backup and restore operations

* **Notification Integration:**
  * Enabled Backup Vault notifications through SNS
  * Received email notification when the backup job completed successfully
  * Confirmed that notification content included the recovery point ARN, resource ARN, and backup job ID

* **Backup and Restore Validation:**
  * Created an on-demand backup for the EC2 instance
  * Verified that the restore job reached `Completed`
  * Reviewed CloudWatch Logs for restore test and cleanup activities
  * Confirmed restore validation succeeded with HTTP 200 and the restored resource was cleaned up

### Evidence and Analysis:

* **Backup job notification:** The email notification confirms that an AWS Backup job completed successfully and generated a recovery point for the EC2 resource.

{{< image src="images/worklog/week6_backup_notification.jpg" alt="AWS Backup job completed notification email" >}}

* **Restore job completed:** The AWS Backup Jobs page shows the restore job status as `Completed`, confirming that restore execution was successful.

{{< image src="images/worklog/week6_restore_job_completed.jpg" alt="AWS Backup restore job completed" >}}

* **Restore Lambda logs:** CloudWatch Logs show restore test function execution, cleanup of the temporary restored EC2 resource, and final confirmation messages.

{{< image src="images/worklog/week6_restore_lambda_logs.jpg" alt="CloudWatch Logs for AWS Backup restore test Lambda" >}}

* **Restore test status email:** The restore status email confirms that data recovery validation succeeded with HTTP 200 and the newly created restored resource was cleaned up.

{{< image src="images/worklog/week6_restore_test_status.jpg" alt="AWS Backup restore test status email" >}}

### AWS Report Analysis:

* **Architecture fit:** The workflow combines AWS Backup for backup orchestration, S3 and CloudFormation for lab deployment, SNS for notification, Lambda for automated restore validation, and CloudWatch Logs for execution visibility. This is a practical backup architecture because it validates that recovery is possible, not only that backup files exist.

* **Backup reliability:** A backup plan with a backup vault and tagged resource assignment reduces manual effort and makes the backup scope easier to control. The recovery point ARN in the notification provides traceability for each completed backup job.

* **Restore validation:** The restore job and HTTP 200 validation are the most important parts of the lab. A backup is only useful when the application can be restored and verified within the expected recovery objective.

* **Automation value:** The Lambda restore test reduces operational effort by automatically validating the restored resource and cleaning it up afterward. This keeps validation repeatable while controlling cost.

* **Risks and controls:** The main risks are missing SNS confirmation, incorrect resource tags, overly broad IAM permissions, and restore tests leaving temporary resources running. These can be reduced with clear tag standards, least-privilege IAM roles, CloudWatch log review, and automated cleanup checks.

### Key Learnings:

1. **Backups need restore testing** - A completed backup job alone does not prove that recovery works.
2. **Backup Plans standardize protection** - AWS Backup Plans make backup frequency, vault selection, and resource assignment easier to manage.
3. **SNS improves operational awareness** - Email notifications make backup and restore completion visible to operators.
4. **Lambda can automate validation** - Restore tests can verify application health and remove temporary restored resources.
5. **CloudWatch Logs are essential for troubleshooting** - Logs show the restore test flow, cleanup action, and final confirmation.

### Resources Used:

* AWS Backup Workshop: <https://000013.awsstudygroup.com/vi/1-introduce/>
* AWS Backup Console
* Amazon S3
* AWS CloudFormation
* Amazon EC2
* Amazon SNS
* AWS Lambda
* Amazon CloudWatch Logs
