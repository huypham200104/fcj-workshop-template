---
title: "Week 5 Worklog"
date: 2026-05-16
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---
### Week 5 Objectives (May 16 - May 22, 2026):

* Understand the purpose of AWS Web Application Firewall (AWS WAF) in protecting web applications
* Deploy and test the OWASP Juice Shop sample application through Amazon CloudFront
* Create a Web ACL and associate it with a CloudFront distribution
* Use AWS managed rule groups to block common web attacks such as XSS and SQL injection
* Create custom WAF rules for request headers, query strings, and more complex matching logic
* Enable request visibility through sampled requests, CloudWatch metrics, and WAF logging

### Tasks to be carried out this week:

| Period | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| May 16 | - Review the AWS WAF workshop overview <br> - Understand Web ACLs, rule groups, rule actions, and CloudFront integration <br> - Prepare the workshop environment | 05/16/2026 | 05/16/2026 | <https://000026.awsstudygroup.com/vi/> |
| May 17 | - Deploy the OWASP Juice Shop sample web application <br> - Verify access through the CloudFront distribution domain <br> - Confirm the application is reachable before enabling WAF protection | 05/17/2026 | 05/17/2026 | Sample web app section |
| May 18 | - Create a Web ACL named `waf-workshop-juice-shop` <br> - Associate the Web ACL with the CloudFront distribution <br> - Add AWS managed rule groups: Core Rule Set and SQL Database | 05/18/2026 | 05/18/2026 | Web ACL managed rules section |
| May 19 | - Test XSS and SQL injection payloads using `curl` <br> - Confirm malicious requests return `403 Forbidden` <br> - Review how managed rules protect the application | 05/19/2026 | 05/19/2026 | Web ACL managed rules section |
| May 20 | - Create the custom rule `MyCustomRule-X-TomatoAttack` <br> - Block requests that contain the `X-TomatoAttack` header <br> - Review blocked requests in sampled requests | 05/20/2026 | 05/20/2026 | Custom Rule section |
| May 21 | - Practice advanced custom rule creation using JSON <br> - Use AND/OR logic for header and query-string matching <br> - Test rules with count and block actions | 05/21/2026 | 05/21/2026 | Advanced Custom Rule and Testing sections |
| May 22 | - Enable WAF request logging through Kinesis Data Firehose and S3 <br> - Redact sensitive fields such as `Cookie` <br> - Generate test requests and document the result | 05/22/2026 | 05/22/2026 | Logging section |

### Week 5 Achievements:

* **Sample Web Application:**
  * Deployed the OWASP Juice Shop application as the test target
  * Accessed the application through the CloudFront distribution URL
  * Confirmed the application was available before enabling WAF rules

* **Web ACL and Managed Rules:**
  * Created a Web ACL for the Juice Shop application
  * Associated the Web ACL with the CloudFront distribution
  * Added AWS managed rule groups to detect and block common threats
  * Validated protection against XSS and SQL injection requests

* **Custom Rule Implementation:**
  * Created a custom rule to block requests containing the `X-TomatoAttack` header
  * Tested the custom rule using `curl`
  * Verified that matching requests were blocked and appeared in sampled requests

* **Advanced Rule Logic:**
  * Practiced defining rules directly in JSON
  * Used logical statements such as AND and OR for complex request matching
  * Tested query parameter and header combinations before applying stricter blocking logic

* **Logging and Monitoring:**
  * Reviewed sampled requests to identify which rules blocked each request
  * Used CloudWatch/WAF metrics concepts to validate rule behavior
  * Practiced request logging through Kinesis Data Firehose and S3
  * Applied redaction for sensitive fields such as cookies

### Evidence and Analysis:

* **OWASP Juice Shop through CloudFront:** The sample application was deployed and accessed successfully through the CloudFront distribution. This confirms that the application was reachable before WAF rules were tested.

{{< image src="images/worklog/week5_juice_shop_cloudfront.jpg" alt="OWASP Juice Shop through CloudFront" >}}

* **Managed rule blocking test:** XSS and SQL injection payloads were sent using `curl`. Both requests returned `403 Forbidden`, showing that the managed rule groups blocked malicious traffic.

{{< image src="images/worklog/week5_waf_block_test.jpg" alt="AWS WAF blocks XSS and SQL injection test requests" >}}

* **Sampled requests review:** The WAF sampled requests view shows blocked traffic from AWS managed rules and the custom `MyCustomRule-X-TomatoAttack` rule. This makes it possible to identify which rule handled each request.

{{< image src="images/worklog/week5_waf_sampled_requests.jpg" alt="AWS WAF sampled requests showing blocked rules" >}}

* **Logging test requests:** Test requests were generated from the command line after enabling logging. This step supports request-log validation and helps confirm that WAF activity can be audited after the traffic is processed.

{{< image src="images/worklog/week5_waf_logging_test.jpg" alt="AWS WAF logging test request generation" >}}

### AWS Report Analysis:

* **Architecture fit:** AWS WAF is placed in front of the application through CloudFront, which is appropriate for filtering traffic before it reaches the origin. The Web ACL becomes the central policy layer for managed rules, custom rules, sampled request inspection, metrics, and logging.

* **Managed rule value:** AWS managed rule groups are useful for quickly adding baseline protection against common attack patterns. The `403 Forbidden` responses confirm that the Core Rule Set and SQL-related protections are functioning for the tested payloads.

* **Custom rule value:** Custom rules are necessary when the application has context-specific indicators of suspicious traffic, such as the `X-TomatoAttack` header in this workshop. This shows how WAF can go beyond generic protections.

* **Testing approach:** Using `Count` before `Block` is important when deploying new rules because it reduces the risk of accidentally blocking valid users. Sampled requests and metrics help validate whether the rule matches the expected traffic.

* **Logging and privacy:** WAF logging improves auditability because logs show request details, rule actions, and matching behavior. Redacting sensitive fields such as `Cookie` is necessary to reduce exposure of private data in stored logs.

### Key Learnings:

1. **Web ACLs are the policy boundary** - WAF protection is organized through Web ACLs associated with resources such as CloudFront distributions.
2. **Managed rules provide fast baseline protection** - AWS managed rule groups help block common attack categories without writing every rule manually.
3. **Custom rules handle application-specific threats** - Header and query-string matching makes WAF adaptable to the behavior of a specific application.
4. **Count mode supports safer rollout** - Testing with Count helps evaluate a rule before enforcing Block.
5. **Logging is required for auditability** - Sampled requests and WAF logs help explain what was blocked and why.

### Resources Used:

* AWS Web Application Firewall Workshop: <https://000026.awsstudygroup.com/vi/>
* AWS WAF Console
* Amazon CloudFront
* OWASP Juice Shop
* AWS Managed Rules
* Amazon CloudWatch Metrics
* Amazon Kinesis Data Firehose
* Amazon S3
