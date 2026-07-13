---
title: "Week 10 Worklog"
date: 2026-06-20
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---
### Week 10 Objectives (June 20 - June 26, 2026):

* Understand DevOps practices and Continuous Integration / Continuous Deployment (CI/CD) on AWS
* Host source code using AWS CodeCommit (or GitHub integration)
* Automate the build and test process using AWS CodeBuild
* Deploy applications automatically using AWS CodeDeploy
* Orchestrate the entire workflow using AWS CodePipeline

### Tasks to be carried out this week:

| Period | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| June 20 | - Introduction to AWS Developer Tools and CI/CD concepts <br> - Set up a repository in AWS CodeCommit (or connect to GitHub) | 06/20/2026 | 06/20/2026 | CI/CD Workshop |
| June 21 | - Push application source code and a `buildspec.yml` file to the repository | 06/21/2026 | 06/21/2026 | Source Control section |
| June 22 | - Create an AWS CodeBuild project <br> - Configure build environments and verify that the build compiles the code and runs tests successfully | 06/22/2026 | 06/22/2026 | Build section |
| June 23 | - Prepare target environments (EC2 instances or ECS cluster) for deployment <br> - Install CodeDeploy agents on target EC2 instances | 06/23/2026 | 06/23/2026 | Deployment Prep |
| June 24 | - Create an AWS CodeDeploy application and deployment group <br> - Add an `appspec.yml` file to define deployment lifecycle hooks | 06/24/2026 | 06/24/2026 | CodeDeploy section |
| June 25 | - Build a full AWS CodePipeline connecting Source, Build, and Deploy stages <br> - Commit a code change to trigger a fully automated pipeline run | 06/25/2026 | 06/25/2026 | Pipeline section |
| June 26 | - Verify the deployed changes on the target application <br> - Review pipeline execution logs and clean up resources | 06/26/2026 | 06/26/2026 | Verification & Cleanup |

### Week 10 Achievements:

* **Automated Pipeline:**
  * Successfully built an end-to-end CI/CD pipeline that automatically builds, tests, and deploys code upon every git commit.
* **Infrastructure as Code elements:**
  * Utilized `buildspec.yml` and `appspec.yml` to define build instructions and deployment steps declaratively.
* **Zero Downtime Deployments:**
  * Learned how CodeDeploy can perform rolling updates to maintain application availability during deployments.

### Key Learnings:

1. **Agility and Speed:** CI/CD significantly speeds up the release cycle and reduces manual errors during deployments.
2. **Traceability:** CodePipeline provides a visual representation of the release process, making it easy to spot where failures occur.
3. **Decoupled Architecture:** Using specific tools for Source (CodeCommit), Build (CodeBuild), and Deploy (CodeDeploy) allows for a flexible and modular DevOps workflow.
