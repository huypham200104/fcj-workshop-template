---
title: "Worklog Tuần 4"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4 (8/5 - 15/5/2026):

* Hiểu rõ về AWS Lambda functions và kiến trúc serverless computing
* Triển khai các chiến lược tối ưu hóa chi phí sử dụng Lambda và EventBridge
* Xây dựng giải pháp tự động quản lý EC2 instances để giảm chi phí hạ tầng
* Tích hợp thông báo từ AWS SNS và Slack

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 (Thứ 4) | - Hiểu Lambda function cơ bản và mô hình giá <br> - Tìm hiểu EventBridge để lên lịch sự kiện <br> - Tìm hiểu IAM roles và quyền cho Lambda <br> - Khảo sát các chiến lược tối ưu hóa chi phí EC2 | 08/05/2026 | 08/05/2026 | <https://docs.aws.amazon.com/lambda/> |
| 3 (Thứ 5) | - Tìm hiểu EventBridge rules và targets <br> - Hiểu CloudWatch Events integration <br> - Tìm hiểu Lambda environment variables <br> - Nghiên cứu SNS cho thông báo | 09/05/2026 | 09/05/2026 | <https://docs.aws.amazon.com/events/> |
| 4 (Thứ 6) | - **Thực hành:** <br>&emsp; + Tạo Lambda function đầu tiên quản lý EC2 <br>&emsp; + Cấu hình IAM role với quyền EC2 <br>&emsp; + Test Lambda function với test events <br>&emsp; + Kiểm tra execution logs | 10/05/2026 | 10/05/2026 | AWS Lambda Console |
| 5-6 (Thứ 7-CN) | - Tạo EventBridge rules cho auto-start và auto-stop <br> - Cấu hình Lambda functions với logic start/stop <br> - Thiết lập SNS notifications <br> - Tích hợp với Slack để nhận cảnh báo | 11/05/2026 | 12/05/2026 | AWS EventBridge Console |
| 7 (Thứ 2) | - **Test & Tối ưu hóa:** <br>&emsp; + Test lên lịch auto-start/stop <br>&emsp; + Giám sát logs và hiệu suất <br>&emsp; + Xác thực tính toán tiết kiệm chi phí <br>&emsp; + Ghi chép giải pháp và bài học | 13/05/2026 | 15/05/2026 | CloudWatch Logs |

### Kết quả đạt được tuần 4:

* **Nắm vững kiến thức Lambda Function:**
  * Hiểu rõ kiến trúc serverless computing và lợi ích của nó
  * Nắm được mô hình giá Lambda (pay-per-invocation)
  * Tạo thành công nhiều Lambda functions cho các thao tác EC2 khác nhau
  * Khám phá Lambda console và các tùy chọn cấu hình functions

* **Triển khai giải pháp tối ưu hóa chi phí:**
  * Tạo hàm auto-start EC2 được kích hoạt bởi EventBridge
  * Tạo hàm auto-stop EC2 với lên lịch trigger
  * Giảm chi phí hạ tầng không cần thiết thông qua lên lịch thông minh
  * Chứng minh tiết kiệm được 70%+ chi phí trên các EC2 instances không phải production

* **Thiết lập EventBridge & Lên lịch sự kiện:**
  * Cấu hình EventBridge rules cho lên lịch dựa trên cron
  * Thiết lập auto-stop hàng ngày (ví dụ: 19:00 ngày làm việc)
  * Thiết lập auto-start hàng ngày (ví dụ: 08:00 ngày làm việc)
  * Tạo event patterns cho automation linh hoạt

* **Test & Xác thực Lambda Functions:**
  * Test thành công Lambda functions với test events
  * Xác minh thay đổi trạng thái EC2 instances qua Lambda execution
  * Phân tích execution logs và performance metrics
  * Xác nhận expected HTTP status codes (200) và responses

* **Tích hợp thông báo:**
  * Cấu hình SNS topics cho Lambda function execution notifications
  * Tích hợp với Slack để nhận cảnh báo real-time
  * Tạo thông báo có ý nghĩa để team biết được
  * Thiết lập CloudWatch alarms cho function failures

* **IAM Security & Quyền hạn:**
  * Tạo IAM roles theo nguyên tắc least-privilege
  * Cấu hình quyền cho EC2 start/stop actions
  * Thêm CloudWatch Logs permissions để debug
  * Triển khai resource-based policies cho Lambda

* **Phân tích Chi phí & Báo cáo:**
  * Tính toán tiết kiệm hàng tháng từ auto-shutdown
  * Ghi chép ROI của triển khai Lambda
  * So sánh chi phí: Chạy 24/7 vs. lên lịch
  * Tạo dashboard theo dõi chi phí

### Phân tích báo cáo AWS tuần 4:

* **Mức phù hợp của kiến trúc:** Giải pháp dùng EventBridge để lập lịch, Lambda làm lớp thực thi, IAM role làm ranh giới phân quyền, và SNS/Slack làm kênh thông báo. Đây là mô hình phù hợp cho tối ưu chi phí EC2 non-production vì automation chỉ chạy khi cần thay đổi trạng thái instance.

* **Xác thực auto-start:** Kết quả test Lambda auto-start cho thấy function có thể gọi EC2 API thành công và trả về response ổn định.

**Minh chứng test Lambda Auto-Start:**

{{< image src="images/worklog/week4_ec2_starting.jpg" alt="Lambda Auto-Start Test" >}}

Ảnh này xác nhận function chạy thành công với status code 200 và response mong đợi là "EC2 Starting".

* **Xác thực auto-stop:** Luồng auto-stop là phần quan trọng nhất trong thiết kế tiết kiệm chi phí vì mức tiết kiệm phụ thuộc vào việc dừng các instance rảnh sau giờ làm việc một cách ổn định.

**Minh chứng test Lambda Auto-Stop:**

{{< image src="images/worklog/week4_ec2_stopping.jpg" alt="Lambda Auto-Stop Test" >}}

Kết quả này cho thấy function stop có thể được test độc lập trước khi gắn vào EventBridge rule theo lịch.

* **Khả năng quan sát vận hành:** Slack notifications giúp automation dễ được audit hơn và giúp team phát hiện nhanh các hành động start/stop bất thường.

**Minh chứng thông báo Slack:**

{{< image src="images/worklog/week4_slack_chat.jpg" alt="Lambda Slack Notification" >}}

Thông báo Slack có hiển thị EC2 instance IDs, giúp truy vết tốt hơn khi nhiều instance được quản lý bởi cùng một automation.

* **Tác động chi phí:** Mức tiết kiệm 70%+ là hợp lý với workload non-production chỉ cần chạy trong giờ làm việc. Để báo cáo thuyết phục hơn, nên bổ sung instance type, đơn giá theo giờ, số giờ chạy theo lịch, và ước tính tiết kiệm hàng tháng.

* **Rủi ro và kiểm soát:** Các rủi ro chính gồm IAM policy quá rộng, lệch timezone khi lập lịch, và dừng nhầm workload cần chạy liên tục. Có thể giảm rủi ro bằng instance tag như `AutoSchedule=true`, IAM least-privilege, CloudWatch alarms, và quy trình manual override rõ ràng.

### Những bài học quan trọng:

1. **Lambda lý tưởng cho các tác vụ có lên lịch** - EventBridge + Lambda cung cấp giải pháp cost-effective thay thế cho việc chạy dedicated services
2. **Automation giảm lỗi con người** - Các thao tác có lên lịch đảm bảo thực thi nhất quán
3. **Monitoring là rất quan trọng** - CloudWatch và Slack integration cung cấp visibility vào các quy trình tự động
4. **Tối ưu hóa chi phí tăng theo quy mô** - Càng nhiều EC2 instances thì tiết kiệm càng lớn từ automation
5. **Serverless đơn giản hóa hạ tầng** - Không cần quản lý servers cho các tác vụ automation đơn giản

### Tài liệu & Công cụ sử dụng:

* AWS Lambda Console
* AWS EventBridge Service
* AWS SNS (Simple Notification Service)
* AWS CloudWatch Logs
* Slack Integration with AWS
* AWS IAM Management Console
