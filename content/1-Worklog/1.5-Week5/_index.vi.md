---
title: "Worklog Tuần 5"
date: 2026-05-16
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 5 (16/05 - 22/05/2026):

* Hiểu mục đích của AWS Web Application Firewall (AWS WAF) trong việc bảo vệ web application
* Triển khai và kiểm thử ứng dụng mẫu OWASP Juice Shop thông qua Amazon CloudFront
* Tạo Web ACL và liên kết Web ACL với CloudFront distribution
* Dùng AWS managed rule groups để chặn các tấn công phổ biến như XSS và SQL injection
* Tạo custom WAF rules cho request headers, query strings và logic matching phức tạp hơn
* Theo dõi request thông qua sampled requests, CloudWatch metrics và WAF logging

### Các công việc cần triển khai trong tuần này:

| Giai đoạn | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 16/05 | - Đọc tổng quan AWS WAF workshop <br> - Hiểu Web ACLs, rule groups, rule actions và tích hợp CloudFront <br> - Chuẩn bị môi trường workshop | 16/05/2026 | 16/05/2026 | <https://000026.awsstudygroup.com/vi/> |
| 17/05 | - Triển khai ứng dụng mẫu OWASP Juice Shop <br> - Kiểm tra truy cập thông qua CloudFront distribution domain <br> - Xác nhận ứng dụng hoạt động trước khi bật WAF protection | 17/05/2026 | 17/05/2026 | Sample web app section |
| 18/05 | - Tạo Web ACL tên `waf-workshop-juice-shop` <br> - Associate Web ACL với CloudFront distribution <br> - Thêm AWS managed rule groups: Core Rule Set và SQL Database | 18/05/2026 | 18/05/2026 | Web ACL managed rules section |
| 19/05 | - Kiểm thử payload XSS và SQL injection bằng `curl` <br> - Xác nhận malicious requests trả về `403 Forbidden` <br> - Review cách managed rules bảo vệ application | 19/05/2026 | 19/05/2026 | Web ACL managed rules section |
| 20/05 | - Tạo custom rule `MyCustomRule-X-TomatoAttack` <br> - Chặn request có header `X-TomatoAttack` <br> - Review blocked requests trong sampled requests | 20/05/2026 | 20/05/2026 | Custom Rule section |
| 21/05 | - Thực hành tạo advanced custom rule bằng JSON <br> - Dùng logic AND/OR cho header và query-string matching <br> - Kiểm thử rule với action Count và Block | 21/05/2026 | 21/05/2026 | Advanced Custom Rule and Testing sections |
| 22/05 | - Bật WAF request logging thông qua Kinesis Data Firehose và S3 <br> - Redact sensitive fields như `Cookie` <br> - Tạo test requests và ghi nhận kết quả | 22/05/2026 | 22/05/2026 | Logging section |

### Kết quả đạt được tuần 5:

* **Ứng dụng mẫu:**
  * Triển khai OWASP Juice Shop làm mục tiêu kiểm thử
  * Truy cập ứng dụng thông qua CloudFront distribution URL
  * Xác nhận ứng dụng hoạt động trước khi bật các WAF rules

* **Web ACL và Managed Rules:**
  * Tạo Web ACL cho ứng dụng Juice Shop
  * Associate Web ACL với CloudFront distribution
  * Thêm AWS managed rule groups để phát hiện và chặn các threat phổ biến
  * Xác thực khả năng bảo vệ trước request XSS và SQL injection

* **Triển khai Custom Rule:**
  * Tạo custom rule chặn request có header `X-TomatoAttack`
  * Kiểm thử custom rule bằng `curl`
  * Xác minh request khớp rule bị block và xuất hiện trong sampled requests

* **Advanced Rule Logic:**
  * Thực hành định nghĩa rule trực tiếp bằng JSON
  * Dùng logical statements như AND và OR cho điều kiện matching phức tạp
  * Kiểm thử kết hợp query parameter và header trước khi áp dụng blocking chặt hơn

* **Logging và Monitoring:**
  * Review sampled requests để xác định rule nào đã block từng request
  * Dùng khái niệm CloudWatch/WAF metrics để kiểm tra hành vi rule
  * Thực hành request logging qua Kinesis Data Firehose và S3
  * Áp dụng redaction cho sensitive fields như cookies

### Minh chứng và phân tích:

* **OWASP Juice Shop qua CloudFront:** Ứng dụng mẫu đã được triển khai và truy cập thành công thông qua CloudFront distribution. Điều này xác nhận application hoạt động trước khi kiểm thử WAF rules.

{{< image src="images/worklog/week5_juice_shop_cloudfront.jpg" alt="OWASP Juice Shop through CloudFront" >}}

* **Kiểm thử managed rules:** Payload XSS và SQL injection được gửi bằng `curl`. Cả hai request đều trả về `403 Forbidden`, cho thấy managed rule groups đã chặn malicious traffic.

{{< image src="images/worklog/week5_waf_block_test.jpg" alt="AWS WAF blocks XSS and SQL injection test requests" >}}

* **Review sampled requests:** Màn hình sampled requests của WAF hiển thị các request bị block bởi AWS managed rules và custom rule `MyCustomRule-X-TomatoAttack`. Phần này giúp xác định rule nào xử lý từng request.

{{< image src="images/worklog/week5_waf_sampled_requests.jpg" alt="AWS WAF sampled requests showing blocked rules" >}}

* **Tạo request để kiểm thử logging:** Các request test được tạo từ command line sau khi bật logging. Bước này hỗ trợ kiểm tra request logs và xác nhận hoạt động WAF có thể được audit sau khi traffic được xử lý.

{{< image src="images/worklog/week5_waf_logging_test.jpg" alt="AWS WAF logging test request generation" >}}

### Phân tích báo cáo AWS tuần 5:

* **Mức phù hợp của kiến trúc:** AWS WAF được đặt trước application thông qua CloudFront, phù hợp để lọc traffic trước khi request tới origin. Web ACL trở thành lớp policy trung tâm cho managed rules, custom rules, sampled request inspection, metrics và logging.

* **Giá trị của managed rules:** AWS managed rule groups hữu ích để thêm lớp bảo vệ cơ bản trước các mẫu tấn công phổ biến. Kết quả `403 Forbidden` xác nhận Core Rule Set và SQL-related protections hoạt động với payload đã kiểm thử.

* **Giá trị của custom rules:** Custom rules cần thiết khi application có dấu hiệu threat theo ngữ cảnh riêng, ví dụ header `X-TomatoAttack` trong workshop. Điều này cho thấy WAF không chỉ bảo vệ theo rule chung mà còn có thể tùy biến theo hành vi ứng dụng.

* **Cách kiểm thử rule:** Dùng `Count` trước khi `Block` là cách triển khai an toàn hơn vì giảm nguy cơ chặn nhầm user hợp lệ. Sampled requests và metrics giúp xác thực rule có match đúng traffic mong muốn hay không.

* **Logging và quyền riêng tư:** WAF logging tăng khả năng audit vì log thể hiện request details, rule actions và hành vi matching. Redact sensitive fields như `Cookie` là cần thiết để giảm rủi ro lộ dữ liệu riêng tư trong logs.

### Những bài học quan trọng:

1. **Web ACL là ranh giới policy** - WAF protection được tổ chức thông qua Web ACL gắn với tài nguyên như CloudFront distribution.
2. **Managed rules giúp tạo baseline nhanh** - AWS managed rule groups hỗ trợ chặn các nhóm tấn công phổ biến mà không cần tự viết toàn bộ rules.
3. **Custom rules xử lý threat theo ngữ cảnh ứng dụng** - Matching header và query string giúp WAF thích ứng với hành vi cụ thể của application.
4. **Count mode giúp rollout an toàn hơn** - Kiểm thử bằng Count giúp đánh giá rule trước khi chuyển sang Block.
5. **Logging cần thiết cho audit** - Sampled requests và WAF logs giúp giải thích request nào bị chặn và lý do bị chặn.

### Tài liệu & Công cụ sử dụng:

* AWS Web Application Firewall Workshop: <https://000026.awsstudygroup.com/vi/>
* AWS WAF Console
* Amazon CloudFront
* OWASP Juice Shop
* AWS Managed Rules
* Amazon CloudWatch Metrics
* Amazon Kinesis Data Firehose
* Amazon S3
