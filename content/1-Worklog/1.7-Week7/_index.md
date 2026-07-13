---
title: "Week 7 Worklog"
date: 2026-05-30
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---
### Week 7 Objectives (May 30 - June 5, 2026):

* Understand the architecture for deploying the FCJ Management application with Auto Scaling Group readiness
* Prepare the networking layer with VPC, public/private subnets, route tables, and security groups
* Launch and configure EC2 instances for application deployment and administration
* Create and seed an Amazon RDS MySQL database for the FCJ Management application
* Deploy the Node.js application and prepare custom CloudWatch metrics for predictive scaling
* Create a Launch Template and Application Load Balancer, then verify the result up to section 5 of the workshop

### Current Scope:

This report covers the work completed up to **section 5 - Result Verification** of the workshop. Section 6, **Create Auto Scaling Group**, has not been completed yet, so this report does not claim that the Auto Scaling Group rollout is finished.

### Tasks to be carried out this week:

| Period | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| May 30 | - Review the Auto Scaling Group workshop introduction <br> - Understand the role of Launch Templates, Application Load Balancer, Target Group, and Auto Scaling Group <br> - Define the target architecture for the FCJ Management application | 05/30/2026 | 05/30/2026 | <https://000006.awsstudygroup.com/vi/1-introduction/> |
| May 31 | - Create the VPC `AutoScaling-Lab` <br> - Configure public and private subnets across multiple Availability Zones <br> - Enable auto-assign public IPv4 for public subnets <br> - Create security groups for the application and database tiers | 05/31/2026 | 05/31/2026 | Network preparation section |
| June 1 | - Launch the FCJ Management EC2 instance using Amazon Linux 2023 <br> - Configure key pair and SSH access <br> - Connect to the instance and verify server access | 06/01/2026 | 06/01/2026 | EC2 preparation section |
| June 2 | - Create the Amazon RDS MySQL database and DB subnet group <br> - Configure database security group access from the application tier <br> - Import seed data into the `awsfcjuser` database | 06/02/2026 | 06/02/2026 | RDS and database setup sections |
| June 3 | - Install Node.js, npm, PM2, and required application dependencies <br> - Clone and configure the FCJ Management application <br> - Configure `.env` database connection values <br> - Start the application process with PM2 | 06/03/2026 | 06/03/2026 | Web server deployment section |
| June 4 | - Prepare custom CloudWatch metrics for predictive scaling <br> - Upload CPU utilization and instance count metric data to CloudWatch <br> - Create an AMI from the configured EC2 instance <br> - Create the Launch Template from the AMI | 06/04/2026 | 06/04/2026 | Metrics and Launch Template sections |
| June 5 | - Create the Target Group for the application <br> - Create the Application Load Balancer `FCJ-Management-LB` <br> - Verify the Load Balancer resource map and current target health <br> - Document the result and remaining work before section 6 | 06/05/2026 | 06/05/2026 | Load Balancer and Result Verification sections |

### Week 7 Achievements:

* **Networking Preparation:**
  * Created the base VPC and subnet layout for the FCJ Management application
  * Separated public access and private database placement through subnet design
  * Configured security groups for SSH, HTTP/application traffic, and MySQL access

* **EC2 Access and Application Host Setup:**
  * Launched an Amazon Linux 2023 EC2 instance
  * Connected to the instance successfully through SSH
  * Prepared the instance as the base server for the FCJ Management application

* **Database Setup:**
  * Created an Amazon RDS MySQL database for application data
  * Configured database access from the application security group
  * Imported and verified seed data in the `awsfcjuser` database

* **Web Application Preparation:**
  * Installed Node.js tooling and prepared the FCJ Management source code
  * Configured the application to connect to the RDS database
  * Used PM2 to run the Node.js application as a background process

* **Metrics and Scaling Preparation:**
  * Prepared custom CloudWatch metrics under the `FCJ Management Custom Metrics` namespace
  * Uploaded CPU utilization and group instance count metric data for later predictive scaling practice
  * Verified that the metrics appeared in CloudWatch

* **Launch Template and Load Balancer:**
  * Created a reusable AMI from the configured application server
  * Created a Launch Template for future EC2 instances
  * Created the Target Group and Application Load Balancer
  * Reached the result verification step before moving on to Auto Scaling Group creation

### Evidence and Analysis:

* **SSH access to EC2:** The first SSH session confirms that the Amazon Linux 2023 instance was reachable and ready for configuration.

{{< image src="images/worklog/week7_ssh_private_instance.jpg" alt="SSH access to Amazon Linux 2023 EC2 instance" >}}

* **Application host access:** The MobaXterm session shows successful SSH access to the FCJ Management server, confirming that remote administration was working.

{{< image src="images/worklog/week7_ssh_web_instance.jpg" alt="MobaXterm SSH session to FCJ Management EC2 instance" >}}

* **Database data verification:** The MySQL result shows seeded customer data in the `awsfcjuser` database, confirming that the database setup and data import were completed.

{{< image src="images/worklog/week7_database_seeded.jpg" alt="MySQL seeded data for FCJ Management application" >}}

* **Custom CloudWatch metrics:** The graph shows `WSCustomCPUUTILIZATION` and `WSCustomGroupInstances` under the custom metrics namespace. These metrics are preparation data for predictive scaling in later sections.

{{< image src="images/worklog/week7_custom_metrics.jpg" alt="CloudWatch custom metrics for predictive scaling preparation" >}}

* **Load Balancer resource map:** The Application Load Balancer was created and mapped to the Target Group. The current target shows unhealthy health checks, which means the Load Balancer path exists but still needs follow-up troubleshooting before continuing to the Auto Scaling Group step.

{{< image src="images/worklog/week7_load_balancer_resource_map.jpg" alt="Application Load Balancer resource map for FCJ Management" >}}

### AWS Report Analysis:

* **Architecture fit:** The work completed this week prepares the core layers required before Auto Scaling Group creation: network, compute baseline, database, reusable AMI, Launch Template, Target Group, Load Balancer, and CloudWatch custom metrics.

* **Readiness for Auto Scaling:** Creating an AMI and Launch Template is necessary because the future Auto Scaling Group needs a repeatable way to launch identical application instances.

* **Database dependency:** The application depends on RDS connectivity. Verifying seeded data before load balancing reduces troubleshooting complexity because it confirms the data layer is available before scaling the application layer.

* **Monitoring preparation:** Uploading custom metrics early prepares the environment for predictive scaling. These metrics are not the final scaling policy yet, but they provide the historical-like data needed for later predictive scaling exercises.

* **Known issue:** The Load Balancer resource map shows the target as unhealthy. The likely causes to check next are health check path/port, application process status, security group rules, and whether the Node.js application is listening on the expected port.

### Key Learnings:

1. **Auto Scaling requires a stable base image** - AMI and Launch Template preparation ensure new instances can launch with consistent application configuration.
2. **RDS access should be validated early** - Database connectivity and seed data verification prevent hidden application errors later.
3. **ALB health checks are strict** - A working EC2 instance is not enough; the target must respond correctly on the configured health check port and path.
4. **Custom metrics support advanced scaling** - Predictive scaling depends on historical or prepared metrics, so metric preparation must happen before policy testing.
5. **The current work is not the final ASG rollout** - The implementation currently stops at result verification before section 6.

### Resources Used:

* Auto Scaling Group Workshop: <https://000006.awsstudygroup.com/vi/1-introduction/>
* Amazon VPC
* Amazon EC2
* Amazon RDS for MySQL
* Amazon CloudWatch Metrics
* Amazon Machine Image (AMI)
* EC2 Launch Template
* Elastic Load Balancing - Application Load Balancer
