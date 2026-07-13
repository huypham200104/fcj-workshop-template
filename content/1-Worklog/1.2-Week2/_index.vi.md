---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---
### Mục tiêu tuần 2:

* Tìm hiểu và vận dụng AWS Identity and Access Management (IAM) để quản lý quyền truy cập tập trung trên AWS.
* Xây dựng hạ tầng mạng cô lập với VPC, Subnets, Security Groups và Key Pairs.
* Thiết lập kết nối an toàn đến máy chủ private thông qua Bastion Host và EC2 Instance Connect Endpoint.
* Thực hành troubleshooting mạng, tối ưu chi phí và dọn dẹp tài nguyên sau khi triển khai.

**Thời gian thực hiện:** 25/04/2026 - 01/05/2026

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                 | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------- |
| 2   | - Tìm hiểu AWS IAM và thực hành tạo user, group, role, policy <br> - Thiết lập quyền truy cập tập trung theo nguyên tắc phân quyền tối thiểu                                              | 17/04/2026   | 17/04/2026      |                |
| 3   | - Xây dựng VPC và chia subnet thành Public Subnet và Private Subnet <br> - Tổ chức tài nguyên theo mô hình mạng cô lập, đảm bảo tài nguyên quan trọng nằm trong Private Subnet | 18/04/2026   | 19/04/2026      |                |
| 4   | - Cấu hình Security Groups và Key Pairs (.pem, .ppk) <br> - Giới hạn truy cập SSH chỉ từ nguồn xác định và bảo vệ máy chủ bằng cơ chế xác thực an toàn                           | 20/04/2026   | 20/04/2026      |                |
| 5   | - Thiết lập Bastion Host (Jump Box) để kết nối từ máy public sang máy private <br> - Thực hiện scp, chmod 400 và kiểm tra luồng truy cập an toàn                                   | 21/04/2026   | 22/04/2026      |                |
| 6   | - Triển khai NAT Gateway và cấu hình Route Table cho private subnet <br> - Tối ưu kết nối với EC2 Instance Connect Endpoint (EICE), dùng Reachability Analyzer để troubleshooting <br> - Thực hiện cleanup tài nguyên sau khi hoàn tất | 23/04/2026   | 24/04/2026      |                |


### Kết quả đạt được tuần 2:

* Hiểu rõ vai trò của AWS IAM trong việc quản lý quyền truy cập tập trung và áp dụng được mô hình phân quyền phù hợp cho người dùng, nhóm và vai trò.

* Xây dựng thành công hệ thống mạng cô lập với VPC và Subnets, trong đó:
  * Public Subnet dùng cho tài nguyên cần truy cập từ Internet
  * Private Subnet dùng cho các tài nguyên quan trọng để tăng mức độ an toàn

* Cấu hình thành công Security Groups và Key Pairs để kiểm soát truy cập vào EC2, chỉ cho phép các kết nối hợp lệ theo đúng yêu cầu bảo mật.

* Thực hiện thành công cơ chế Bastion Host để kết nối từ môi trường public vào máy private, đồng thời sử dụng `scp` và `chmod 400` để đảm bảo quá trình truyền và bảo vệ tệp tin an toàn.
  ![Bastion Host và NAT Gateway Access](/images/1-Worklog/week2-bastion-nat-gateway-access.jpg)

* Triển khai NAT Gateway và cấu hình Route Table chính xác cho Private Subnet, giúp máy private có thể truy cập Internet một chiều để cập nhật và cài đặt gói cần thiết.

* Thiết lập và kiểm tra EC2 Instance Connect Endpoint (EICE), cho phép đăng nhập trực tiếp vào máy private trên trình duyệt mà không cần public IP hay máy trung gian.
  ![EICE Endpoint được tạo thành công](/images/1-Worklog/week2-eice-endpoint-created-available.jpg)
  ![Kết nối thành công vào Private Instance qua EICE](/images/1-Worklog/week2-eice-private-ec2-connection.jpg)

* Sử dụng Reachability Analyzer để xác định nhanh các vấn đề liên quan đến Security Group hoặc Route Table, từ đó rút ngắn thời gian troubleshooting.

* Nắm được quy trình cleanup tài nguyên AWS sau khi sử dụng, bao gồm xóa NAT Gateway, giải phóng Elastic IP và terminate instance để tránh phát sinh chi phí không mong muốn.


