---
title: "Worklog Tuần 7"
date: 2026-05-30
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---
### Mục tiêu tuần 7 (30/05 - 05/06/2026):

* Hiểu kiến trúc triển khai ứng dụng FCJ Management để chuẩn bị cho Auto Scaling Group
* Chuẩn bị lớp mạng với VPC, public/private subnets, route tables và security groups
* Khởi tạo và cấu hình EC2 instances cho triển khai ứng dụng và quản trị
* Tạo và nạp dữ liệu cho Amazon RDS MySQL database của ứng dụng FCJ Management
* Triển khai Node.js application và chuẩn bị custom CloudWatch metrics cho predictive scaling
* Tạo Launch Template và Application Load Balancer, sau đó kiểm tra kết quả tới phần 5 của workshop

### Phạm vi hiện tại:

Báo cáo này chỉ ghi nhận phần đã làm tới **phần 5 - Kiểm tra kết quả** của workshop. Phần 6, **Tạo Auto Scaling Group**, chưa hoàn thành nên báo cáo không ghi nhận là đã triển khai xong Auto Scaling Group.

### Các công việc cần triển khai trong tuần này:

| Giai đoạn | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 30/05 | - Đọc phần giới thiệu Auto Scaling Group workshop <br> - Hiểu vai trò của Launch Templates, Application Load Balancer, Target Group và Auto Scaling Group <br> - Xác định kiến trúc mục tiêu cho ứng dụng FCJ Management | 30/05/2026 | 30/05/2026 | <https://000006.awsstudygroup.com/vi/1-introduction/> |
| 31/05 | - Tạo VPC `AutoScaling-Lab` <br> - Cấu hình public và private subnets trên nhiều Availability Zones <br> - Bật auto-assign public IPv4 cho public subnets <br> - Tạo security groups cho application tier và database tier | 31/05/2026 | 31/05/2026 | Network preparation section |
| 01/06 | - Khởi tạo EC2 instance FCJ Management bằng Amazon Linux 2023 <br> - Cấu hình key pair và SSH access <br> - Kết nối vào instance và xác nhận server access | 01/06/2026 | 01/06/2026 | EC2 preparation section |
| 02/06 | - Tạo Amazon RDS MySQL database và DB subnet group <br> - Cấu hình database security group cho phép truy cập từ application tier <br> - Import seed data vào database `awsfcjuser` | 02/06/2026 | 02/06/2026 | RDS and database setup sections |
| 03/06 | - Cài Node.js, npm, PM2 và dependencies cần thiết <br> - Clone và cấu hình ứng dụng FCJ Management <br> - Cấu hình `.env` để kết nối tới database <br> - Chạy application bằng PM2 | 03/06/2026 | 03/06/2026 | Web server deployment section |
| 04/06 | - Chuẩn bị custom CloudWatch metrics cho predictive scaling <br> - Upload dữ liệu CPU utilization và instance count lên CloudWatch <br> - Tạo AMI từ EC2 instance đã cấu hình <br> - Tạo Launch Template từ AMI | 04/06/2026 | 04/06/2026 | Metrics and Launch Template sections |
| 05/06 | - Tạo Target Group cho application <br> - Tạo Application Load Balancer `FCJ-Management-LB` <br> - Kiểm tra Load Balancer resource map và tình trạng target hiện tại <br> - Ghi nhận kết quả và phần còn lại trước khi sang phần 6 | 05/06/2026 | 05/06/2026 | Load Balancer and Result Verification sections |

### Kết quả đạt được tuần 7:

* **Chuẩn bị hạ tầng mạng:**
  * Tạo VPC và subnet layout cơ bản cho ứng dụng FCJ Management
  * Tách public access và database private placement bằng thiết kế subnet
  * Cấu hình security groups cho SSH, HTTP/application traffic và MySQL access

* **EC2 Access và Application Host Setup:**
  * Khởi tạo Amazon Linux 2023 EC2 instance
  * Kết nối thành công vào instance qua SSH
  * Chuẩn bị instance làm server nền cho ứng dụng FCJ Management

* **Thiết lập Database:**
  * Tạo Amazon RDS MySQL database cho dữ liệu ứng dụng
  * Cấu hình database access từ application security group
  * Import và xác minh seed data trong database `awsfcjuser`

* **Chuẩn bị Web Application:**
  * Cài đặt Node.js tooling và chuẩn bị source code FCJ Management
  * Cấu hình ứng dụng kết nối tới RDS database
  * Dùng PM2 để chạy Node.js application dưới nền

* **Chuẩn bị Metrics và Scaling:**
  * Chuẩn bị custom CloudWatch metrics trong namespace `FCJ Management Custom Metrics`
  * Upload dữ liệu CPU utilization và group instance count để phục vụ predictive scaling về sau
  * Xác minh metrics đã xuất hiện trong CloudWatch

* **Launch Template và Load Balancer:**
  * Tạo AMI tái sử dụng từ application server đã cấu hình
  * Tạo Launch Template cho các EC2 instances trong tương lai
  * Tạo Target Group và Application Load Balancer
  * Hoàn thành tới bước kiểm tra kết quả trước khi chuyển sang phần tạo Auto Scaling Group

### Minh chứng và phân tích:

* **SSH access vào EC2:** Phiên SSH đầu tiên xác nhận Amazon Linux 2023 instance có thể truy cập và sẵn sàng để cấu hình.

{{< image src="images/worklog/week7_ssh_private_instance.jpg" alt="SSH access to Amazon Linux 2023 EC2 instance" >}}

* **Truy cập application host:** Phiên MobaXterm cho thấy kết nối SSH thành công tới server FCJ Management, xác nhận remote administration hoạt động.

{{< image src="images/worklog/week7_ssh_web_instance.jpg" alt="MobaXterm SSH session to FCJ Management EC2 instance" >}}

* **Xác minh dữ liệu database:** Kết quả MySQL hiển thị seed customer data trong database `awsfcjuser`, xác nhận bước database setup và data import đã hoàn tất.

{{< image src="images/worklog/week7_database_seeded.jpg" alt="MySQL seeded data for FCJ Management application" >}}

* **Custom CloudWatch metrics:** Biểu đồ hiển thị `WSCustomCPUUTILIZATION` và `WSCustomGroupInstances` trong custom metrics namespace. Đây là dữ liệu chuẩn bị cho phần predictive scaling ở các bước sau.

{{< image src="images/worklog/week7_custom_metrics.jpg" alt="CloudWatch custom metrics for predictive scaling preparation" >}}

* **Load Balancer resource map:** Application Load Balancer đã được tạo và liên kết với Target Group. Target hiện đang unhealthy, nghĩa là đường dẫn Load Balancer đã tồn tại nhưng cần troubleshoot thêm trước khi tiếp tục sang bước Auto Scaling Group.

{{< image src="images/worklog/week7_load_balancer_resource_map.jpg" alt="Application Load Balancer resource map for FCJ Management" >}}

### Phân tích báo cáo AWS tuần 7:

* **Mức phù hợp của kiến trúc:** Phần đã làm trong tuần này chuẩn bị các lớp cốt lõi trước khi tạo Auto Scaling Group: network, compute baseline, database, reusable AMI, Launch Template, Target Group, Load Balancer và CloudWatch custom metrics.

* **Mức sẵn sàng cho Auto Scaling:** Việc tạo AMI và Launch Template là cần thiết vì Auto Scaling Group về sau cần một cách lặp lại để khởi tạo các application instances giống nhau.

* **Phụ thuộc database:** Ứng dụng phụ thuộc vào kết nối RDS. Xác minh seed data trước khi cân bằng tải giúp giảm phạm vi troubleshooting vì đã chắc chắn data layer hoạt động.

* **Chuẩn bị monitoring:** Upload custom metrics sớm giúp chuẩn bị môi trường cho predictive scaling. Các metrics này chưa phải scaling policy cuối cùng, nhưng cung cấp dữ liệu dạng lịch sử cần thiết cho bài predictive scaling.

* **Vấn đề hiện tại:** Load Balancer resource map cho thấy target đang unhealthy. Các nguyên nhân cần kiểm tra tiếp theo gồm health check path/port, trạng thái application process, security group rules và việc Node.js application có lắng nghe đúng port hay không.

### Những bài học quan trọng:

1. **Auto Scaling cần base image ổn định** - AMI và Launch Template giúp instance mới có cấu hình ứng dụng nhất quán.
2. **RDS access nên được xác minh sớm** - Database connectivity và seed data verification giúp tránh lỗi ẩn ở các bước sau.
3. **ALB health check rất nghiêm ngặt** - EC2 chạy được chưa đủ; target phải phản hồi đúng port và path health check đã cấu hình.
4. **Custom metrics hỗ trợ scaling nâng cao** - Predictive scaling phụ thuộc vào historical hoặc prepared metrics nên phải chuẩn bị metrics trước khi test policy.
5. **Phần hiện tại chưa phải ASG rollout hoàn chỉnh** - Việc triển khai đang dừng ở kiểm tra kết quả trước phần 6.

### Tài liệu & Công cụ sử dụng:

* Auto Scaling Group Workshop: <https://000006.awsstudygroup.com/vi/1-introduction/>
* Amazon VPC
* Amazon EC2
* Amazon RDS for MySQL
* Amazon CloudWatch Metrics
* Amazon Machine Image (AMI)
* EC2 Launch Template
* Elastic Load Balancing - Application Load Balancer
