---
title: "Worklog Tuần 9"
date: 2026-06-13
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
### Mục tiêu tuần 9 (13/06 - 19/06/2026):

* Nắm vững kiến trúc Serverless và các lợi ích (Không quản lý máy chủ, trả tiền theo lượng dùng)
* Xây dựng backend Serverless sử dụng AWS Lambda và Amazon API Gateway
* Lưu trữ và truy xuất dữ liệu bằng Amazon DynamoDB (Cơ sở dữ liệu NoSQL)
* Bảo mật API bằng IAM và API Gateway authorizers
* Giám sát và gỡ lỗi ứng dụng serverless bằng AWS X-Ray và CloudWatch

### Các công việc cần triển khai trong tuần này:

| Giai đoạn | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 13/06 | - Giới thiệu về khái niệm Serverless (Lambda, API Gateway, DynamoDB) <br> - Thiết kế kiến trúc cho ứng dụng To-Do serverless | 13/06/2026 | 13/06/2026 | Tài liệu Serverless |
| 14/06 | - Tạo bảng Amazon DynamoDB `ToDoItems` với Partition Key là `id` <br> - Tìm hiểu các chế độ Read/Write capacity của DynamoDB | 14/06/2026 | 14/06/2026 | Phần DynamoDB |
| 15/06 | - Tạo IAM Role với quyền hạn tối thiểu (least-privilege) cho Lambda <br> - Viết các AWS Lambda functions (Node.js/Python) cho các thao tác CRUD | 15/06/2026 | 15/06/2026 | Phần Lambda |
| 16/06 | - Cấu hình Amazon API Gateway làm cổng giao tiếp cho Lambda <br> - Thiết lập RESTful routes (GET, POST, PUT, DELETE) và CORS | 16/06/2026 | 16/06/2026 | Phần API Gateway |
| 17/06 | - Kiểm thử các API endpoints bằng Postman hoặc cURL <br> - Tích hợp API Gateway với Lambda dùng Proxy Integration | 17/06/2026 | 17/06/2026 | Kiểm thử API |
| 18/06 | - Triển khai xác thực API sử dụng Amazon Cognito User Pools hoặc API Keys <br> - Bật AWS X-Ray để theo dõi phân tán (distributed tracing) | 18/06/2026 | 18/06/2026 | Bảo mật & Giám sát |
| 19/06 | - Đọc CloudWatch Logs của các quá trình thực thi Lambda <br> - Dọn dẹp tài nguyên serverless | 19/06/2026 | 19/06/2026 | Tổng kết & Dọn dẹp |

### Kết quả đạt được tuần 9:

* **Backend Serverless:**
  * Triển khai thành công một REST API hoàn toàn Serverless mà không cần khởi tạo server nào.
* **Tích hợp Database:**
  * Thiết kế và sử dụng DynamoDB để lưu trữ dữ liệu NoSQL nhanh chóng, dễ dàng mở rộng.
* **Bảo mật & Tracing:**
  * Bảo vệ các endpoint của API và bật X-Ray tracing để phân tích hiệu suất và nút thắt cổ chai.

### Những bài học quan trọng:

1. **Mô hình Trả-theo-dùng (Pay-as-you-go):** Điện toán Serverless chỉ tính phí dựa trên thời gian tính toán thực tế, rất tiết kiệm cho các workload biến động.
2. **Bản chất phi trạng thái (Stateless):** Các hàm Lambda là stateless, cần lưu trữ bên ngoài như DynamoDB để duy trì dữ liệu ứng dụng.
3. **Quản lý API:** API Gateway đơn giản hóa việc định tuyến, giới hạn lưu lượng (throttling) và phân quyền, đóng vai trò là điểm vào bảo mật cho microservices.
