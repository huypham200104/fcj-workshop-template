---
title: "Worklog Tuần 8"
date: 2026-06-06
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
### Mục tiêu tuần 8 (06/06 - 12/06/2026):

* Tiếp tục triển khai ứng dụng FCJ Management bằng cách tạo Auto Scaling Group (ASG)
* Cấu hình Dynamic Scaling Policies dựa trên CPU Utilization
* Tìm hiểu Predictive Scaling sử dụng CloudWatch metrics tùy chỉnh đã chuẩn bị
* Kiểm thử chịu tải (Stress test) ứng dụng để quan sát quá trình scale in và scale out
* Phân tích log hoạt động scaling và vòng đời của ASG

### Các công việc cần triển khai trong tuần này:

| Giai đoạn | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 06/06 | - Ôn lại khái niệm ASG và tích hợp với Application Load Balancer <br> - Xử lý lỗi unhealthy target từ tuần trước | 06/06/2026 | 06/06/2026 | Tài liệu ASG Workshop |
| 07/06 | - Tạo Auto Scaling Group `FCJ-Management-ASG` <br> - Gắn ASG vào Target Group và ALB hiện có <br> - Thiết lập minimum, maximum và desired capacity | 07/06/2026 | 07/06/2026 | Phần tạo ASG |
| 08/06 | - Cấu hình Dynamic Target Tracking Scaling Policy <br> - Đặt mục tiêu CPU utilization ở mức 50% để kích hoạt scale-out | 08/06/2026 | 08/06/2026 | Phần Dynamic Scaling |
| 09/06 | - Cấu hình Predictive Scaling Policy sử dụng custom CloudWatch metrics <br> - Phân tích dữ liệu lịch sử để dự báo lưu lượng | 09/06/2026 | 09/06/2026 | Phần Predictive Scaling |
| 10/06 | - Thực hiện stress test bằng công cụ như Apache JMeter hoặc AWS FIS <br> - Giám sát CloudWatch alarms kích hoạt scale-out | 10/06/2026 | 10/06/2026 | Phần Stress Testing |
| 11/06 | - Quan sát hành vi scale-in sau khi giảm tải <br> - Xác minh ứng dụng luôn khả dụng trong quá trình scaling | 11/06/2026 | 11/06/2026 | Quan sát Scaling |
| 12/06 | - Dọn dẹp tài nguyên (EC2, ASG, ALB, RDS, VPC) để tránh phát sinh chi phí <br> - Tổng kết bài học | 12/06/2026 | 12/06/2026 | Workshop Cleanup |

### Kết quả đạt được tuần 8:

* **Cấu hình Auto Scaling Group:**
  * Tạo thành công và gắn ASG vào Application Load Balancer.
  * Cấu hình chính sách Target Tracking để tự động điều chỉnh số lượng instance dựa trên traffic.
* **Predictive Scaling:**
  * Triển khai predictive scaling để chủ động khởi chạy instance trước các đợt tăng traffic dự kiến.
* **Kiểm thử và Giám sát:**
  * Xác minh hoạt động của ASG dưới tải cao.
  * Theo dõi các hoạt động scaling và health check để đảm bảo tính sẵn sàng cao cho ứng dụng.

### Những bài học quan trọng:

1. **Tích hợp ASG và ALB:** Auto Scaling Group hoạt động trơn tru với Load Balancer để tự động phân phối traffic đến các instance mới.
2. **Chính sách Scaling:** Việc chọn đúng chính sách (Dynamic hay Predictive) phụ thuộc vào pattern của workload. Predictive scaling rất phù hợp cho traffic có tính chu kỳ.
3. **Tối ưu chi phí:** ASG giúp đảm bảo chỉ chạy số lượng instance cần thiết, tối ưu hóa chi phí mà vẫn giữ vững hiệu năng.
