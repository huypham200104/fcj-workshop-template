---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---
### Week 2 Objectives:

* Learn and apply AWS Identity and Access Management (IAM) for centralized access control.
* Build an isolated network architecture with VPC, subnets, security groups, and key pairs.
* Set up secure access to private instances through a Bastion Host and EC2 Instance Connect Endpoint.
* Practice network troubleshooting, cost optimization, and resource cleanup after deployment.

**Implementation period:** 25/04/2026 - 01/05/2026

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                               | Start Date | Completion Date | Reference Material |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------ |
| 2   | - Study AWS IAM and practice creating users, groups, roles, and policies <br> - Configure centralized access control based on least privilege                                            | 04/25/2026 | 04/25/2026      |                    |
| 3   | - Build a VPC and split it into Public Subnet and Private Subnet <br> - Organize resources using an isolated network model so critical workloads stay in the private subnet                | 04/26/2026 | 04/27/2026      |                    |
| 4   | - Configure security groups and key pairs (.pem, .ppk) <br> - Restrict SSH access to approved sources and secure servers with proper authentication                                    | 04/28/2026 | 04/28/2026      |                    |
| 5   | - Set up a Bastion Host (Jump Box) to connect from the public machine to the private machine <br> - Use `scp`, `chmod 400`, and verify secure access flow                              | 04/29/2026 | 04/30/2026      |                    |
| 6   | - Deploy a NAT Gateway and configure the route table for the private subnet <br> - Optimize access with EC2 Instance Connect Endpoint (EICE), troubleshoot using Reachability Analyzer <br> - Clean up resources after completion | 05/01/2026 | 05/01/2026      |                    |


### Week 2 Achievements:

* Gained a clear understanding of AWS IAM and how centralized permissions can be controlled for users, groups, and roles.

* Successfully built an isolated network architecture with VPC and subnets, where:
  * Public Subnet is used for internet-facing resources
  * Private Subnet is used for critical workloads to improve security

* Successfully configured security groups and key pairs to control access to EC2 instances using the expected security model.

* Implemented Bastion Host access for public-to-private connectivity and used `scp` and `chmod 400` to secure file transfer and protect sensitive keys.
  ![Bastion Host and NAT Gateway Access](../../images/1-Worklog/week2-bastion-nat-gateway-access.jpg)

* Deployed a NAT Gateway and configured the route table correctly for the private subnet, enabling one-way internet access for updates and package installation.

* Set up and validated EC2 Instance Connect Endpoint (EICE), making it possible to log in directly to a private instance from the browser without a public IP or intermediary host.
  ![EICE Endpoint Successfully Created](../../images/1-Worklog/week2-eice-endpoint-created-available.jpg)
  ![Successful Connection to Private Instance via EICE](../../images/1-Worklog/week2-eice-private-ec2-connection.jpg)

* Used Reachability Analyzer to quickly identify network issues related to security groups or route tables, reducing manual troubleshooting time.

* Learned the proper AWS cleanup procedure, including removing the NAT Gateway, releasing the Elastic IP, and terminating instances to avoid unexpected charges.
