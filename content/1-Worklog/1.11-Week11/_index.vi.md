---
title: "Worklog Tuần 11"
date: 2026-06-27
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---
### Mục tiêu tuần 11 (27/06 - 03/07/2026):

* **Khởi động Final Project:** Bắt đầu xây dựng hệ thống Helpdesk Portal (theo phong cách Jira Service Management / Freshservice).
* **Thiết lập Frontend:** Xây dựng giao diện Dashboard hiện đại, responsive, sử dụng tông màu chủ đạo AWS Orange, Trắng và Dark Gray. Host Frontend trên S3, phân phối qua CloudFront và bảo vệ bằng AWS WAF.
* **Thiết lập Backend Cốt lõi:** Xây dựng kiến trúc Serverless với API Gateway, AWS Lambda, Amazon DynamoDB (lưu trữ Ticket) và Amazon S3 (lưu trữ file đính kèm).
* **Tích hợp CI/CD:** Tự động hóa quá trình deploy cho cả Frontend và Backend bằng AWS CodeCommit, CodeBuild và CodePipeline.

### Các công việc cần triển khai trong tuần này:

| Giai đoạn | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 27/06 | - Kickoff dự án và phân tích kiến trúc <br> - Thiết lập CI/CD pipeline (CodeCommit, CodeBuild, CodePipeline) để tự động deploy Frontend lên S3 và Backend lên Lambda | 27/06/2026 | 27/06/2026 | Sơ đồ Kiến trúc |
| 28/06 | - Phát triển các component UI lõi (Dashboard, Sidebar cố định, Header, Card thống kê) <br> - Đảm bảo tính Responsive cho Desktop, Tablet và Mobile | 28/06/2026 | 28/06/2026 | Yêu cầu UI/UX |
| 29/06 | - Xây dựng Data Table có tính năng Phân trang (Pagination), Search, Filter và Sort <br> - Thêm các yếu tố trải nghiệm người dùng (Modal xác nhận, Toast Notification, Loading Spinner) | 29/06/2026 | 29/06/2026 | Tài liệu Framework UI |
| 30/06 | - Thiết kế lược đồ (schema) DynamoDB cho Database lưu Ticket <br> - Khởi tạo S3 bucket lưu trữ file đính kèm của Ticket | 30/06/2026 | 30/06/2026 | Tài liệu DynamoDB |
| 01/07 | - Lập trình Backend lõi (Ticket Handler Lambda) để tạo, đọc và cập nhật Ticket <br> - Cấu hình Amazon API Gateway route và tích hợp với Lambda | 01/07/2026 | 01/07/2026 | Tài liệu Lambda & API GW |
| 02/07 | - Deploy Frontend lên S3 và thiết lập CloudFront distribution <br> - Kết nối Frontend gọi API Backend (Đảm bảo Frontend không chứa business logic) | 02/07/2026 | 02/07/2026 | Hosting S3 tĩnh |
| 03/07 | - Cấu hình AWS WAF bảo vệ CloudFront chặn các truy cập độc hại <br> - Kiểm thử tích hợp cuối tuần và sửa lỗi | 03/07/2026 | 03/07/2026 | Tài liệu AWS WAF |

### Kết quả đạt được tuần 11:

* **Tự động hóa CI/CD:**
  * Tách biệt thành công luồng Pipeline của Frontend và Backend. Bất cứ code nào đẩy lên CodeCommit đều kích hoạt CodeBuild và tự động deploy cập nhật lên S3/CloudFront hoặc AWS Lambda.
* **Giao diện Frontend Hiện đại:**
  * Hoàn thiện layout cơ sở cho Helpdesk Portal. Giao diện chạy mượt mà trên đa thiết bị, mang phong cách chuyên nghiệp giống Jira Service Management, có đầy đủ Data Table, Modal và Spinner.
* **Hệ thống Backend Serverless Cơ bản:**
  * Sử dụng API Gateway làm cổng giao tiếp duy nhất. Dữ liệu Ticket được lưu an toàn vào DynamoDB và tính năng upload file đính kèm lên S3 hoạt động tốt.

### Những bài học quan trọng:

1. **Phân tách trách nhiệm (Separation of Concerns):** Việc tuân thủ nguyên tắc không xử lý nghiệp vụ ở Frontend giúp ứng dụng trở nên nhẹ, bảo mật cao và dễ dàng bảo trì.
2. **Quy trình Tự động:** Hoàn tất CI/CD ngay từ Ngày 1 giúp nhóm tiết kiệm cực kỳ nhiều thời gian cho việc deploy thủ công, tập trung tối đa 100% vào việc code tính năng.
3. **Bảo mật tại Edge (CloudFront + WAF):** Đặt WAF ở CloudFront giúp chặn các luồng request xấu ngay từ mạng biên (Edge), giúp tiết kiệm chi phí gọi Lambda và bảo vệ an toàn cho Backend.
