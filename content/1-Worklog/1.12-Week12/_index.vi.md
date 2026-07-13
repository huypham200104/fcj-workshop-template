---
title: "Worklog Tuần 12"
date: 2026-07-04
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---
### Mục tiêu tuần 12 (04/07 - 30/07/2026):

* **Bảo mật & Xác thực:** Triển khai Amazon Cognito để quản lý đăng nhập (User/Staff), bảo vệ API Gateway bằng JWT Authorizer. Áp dụng AWS KMS để mã hóa dữ liệu.
* **Hệ thống Thông báo Bất đồng bộ:** Xây dựng luồng xử lý thông báo dùng Amazon SQS (FIFO), AWS Lambda (Notification Worker), và Amazon SES để gửi Email. Cấu hình Dead Letter Queue (DLQ) để xử lý các message bị lỗi.
* **Giám sát & Sao lưu:** Tập trung Logs, Metrics và Errors thông qua Amazon CloudWatch. Cấu hình CloudWatch Alarms kích hoạt Amazon SNS để gửi cảnh báo lỗi. Cấu hình AWS Backup cho DynamoDB và S3.
* **Nghiệm thu Dự án:** Hoàn thiện dự án, kiểm thử toàn bộ hệ thống (End-to-End) và chuẩn bị báo cáo tổng kết thực tập.

### Các công việc cần triển khai trong tuần này:

| Giai đoạn | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 04/07 | - Cấu hình Amazon Cognito User Pools để xác thực người dùng <br> - Tích hợp Cognito vào Frontend, gửi JWT Token xuống API Gateway <br> - Thiết lập API Gateway Authorizer kiểm tra tính hợp lệ của JWT | 04/07/2026 | 04/07/2026 | Tài liệu AWS Cognito |
| 05/07 | - Tạo Amazon SQS FIFO Queue và Dead Letter Queue (DLQ) <br> - Cập nhật Ticket Handler Lambda đẩy các sự kiện cần thông báo vào SQS | 05/07/2026 | 05/07/2026 | Tài liệu AWS SQS |
| 06/07 | - Viết Notification Worker Lambda đọc message từ SQS và gửi Email qua Amazon SES <br> - Kiểm thử kịch bản gửi lỗi để xác nhận message bị đẩy vào DLQ | 06/07/2026 | 06/07/2026 | Tài liệu AWS SES |
| 07/07 | - Ứng dụng AWS KMS để mã hóa các dữ liệu nhạy cảm <br> - Thiết lập AWS Backup tự động sao lưu định kỳ DynamoDB (PITR) và S3 | 07/07/2026 | 07/07/2026 | AWS Security & Backup |
| 08/07 | - Cấu hình CloudWatch theo dõi API Logs, Lambda Logs và Metrics <br> - Tạo CloudWatch Alarms kích hoạt gửi cảnh báo qua Amazon SNS khi phát sinh lỗi | 08/07/2026 | 08/07/2026 | CloudWatch & SNS |
| 09/07 | - Kiểm thử toàn diện hệ thống End-to-End trên các thiết bị (Desktop, Mobile) <br> - Xác nhận mọi tính năng: Tạo Ticket, Search/Filter/Sort, Thông báo, UI Feedback hoạt động tốt | 09/07/2026 | 09/07/2026 | Quy trình Kiểm thử (QA) |
| 10/07 | - Chuẩn bị slide và demo cho buổi thuyết trình Dự án Cuối khóa <br> - Hoàn thành Báo cáo Thực tập và kết thúc chương trình FCJ Bootcamp | 10/07/2026 | 10/07/2026 | Báo cáo Tổng kết |

### Kết quả đạt được tuần 12:

* **Hệ thống Thông báo Bất đồng bộ (Event-Driven):**
  * Tách biệt thành công tiến trình tạo Ticket và gửi Email bằng SQS FIFO. Hệ thống có khả năng tự phục hồi và gom các thông báo lỗi vào DLQ để xử lý sau.
* **Bảo mật Chuyên sâu:**
  * Hệ thống được bảo vệ vững chắc với Cognito (Xác minh JWT tại API). Dữ liệu được mã hóa bằng KMS và sao lưu an toàn với AWS Backup.
* **Khả năng Giám sát Chủ động:**
  * Dev Team nhận được cảnh báo ngay lập tức qua SNS mỗi khi CloudWatch phát hiện lỗi gọi API hoặc lỗi thực thi Lambda, giúp rút ngắn thời gian xử lý sự cố.
* **Hoàn thành Dự án Xuất sắc:**
  * Helpdesk Portal Serverless hoạt động mượt mà, đáp ứng toàn bộ các yêu cầu khắt khe về UI/UX và chuẩn mực kiến trúc AWS Serverless.

### Những bài học quan trọng:

1. **Kiến trúc Bất đồng bộ (Asynchronous):** Việc chia tách các dịch vụ qua SQS giúp hệ thống vô cùng bền bỉ. Nếu SES gặp sự cố khi gửi mail, tiến trình tạo Ticket của người dùng vẫn không bị ảnh hưởng, và DLQ sẽ lưu lại sự cố để tự động thử lại sau.
2. **Bảo mật đa tầng:** Kết hợp Cognito cho Auth, WAF tại mạng biên, API Gateway Authorizers kiểm soát truy cập và KMS mã hóa dữ liệu mang lại tiêu chuẩn bảo mật cấp doanh nghiệp.
3. **Giám sát là Bắt buộc (Observability):** Trong môi trường Serverless (không có máy chủ để SSH vào xem log), CloudWatch Logs + SNS Alarms là phương pháp duy nhất và đáng tin cậy nhất để bắt lỗi và duy trì trạng thái của hệ thống.
