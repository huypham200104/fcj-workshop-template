---
title: "Worklog Tuần 10"
date: 2026-06-20
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---
### Mục tiêu tuần 10 (20/06 - 26/06/2026):

* Nắm vững các thực tiễn DevOps và Tích hợp liên tục / Triển khai liên tục (CI/CD) trên AWS
* Lưu trữ mã nguồn sử dụng AWS CodeCommit (hoặc tích hợp GitHub)
* Tự động hóa quy trình build và test bằng AWS CodeBuild
* Triển khai ứng dụng tự động thông qua AWS CodeDeploy
* Điều phối toàn bộ quy trình sử dụng AWS CodePipeline

### Các công việc cần triển khai trong tuần này:

| Giai đoạn | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 20/06 | - Giới thiệu về AWS Developer Tools và khái niệm CI/CD <br> - Thiết lập repository trên AWS CodeCommit (hoặc kết nối GitHub) | 20/06/2026 | 20/06/2026 | Tài liệu CI/CD |
| 21/06 | - Đẩy mã nguồn ứng dụng và file `buildspec.yml` lên repository | 21/06/2026 | 21/06/2026 | Phần Source Control |
| 22/06 | - Tạo dự án AWS CodeBuild <br> - Cấu hình môi trường build và đảm bảo quá trình biên dịch, chạy test thành công | 22/06/2026 | 22/06/2026 | Phần Build |
| 23/06 | - Chuẩn bị môi trường đích (EC2 instances hoặc ECS cluster) để triển khai <br> - Cài đặt CodeDeploy agents lên các EC2 instance đích | 23/06/2026 | 23/06/2026 | Chuẩn bị Deployment |
| 24/06 | - Tạo AWS CodeDeploy application và deployment group <br> - Thêm file `appspec.yml` để định nghĩa các hook cho vòng đời triển khai | 24/06/2026 | 24/06/2026 | Phần CodeDeploy |
| 25/06 | - Xây dựng AWS CodePipeline hoàn chỉnh kết nối các bước Source, Build, và Deploy <br> - Commit một thay đổi code để kích hoạt pipeline tự động chạy | 25/06/2026 | 25/06/2026 | Phần Pipeline |
| 26/06 | - Xác minh thay đổi đã được triển khai trên ứng dụng đích <br> - Đọc log thực thi pipeline và dọn dẹp tài nguyên | 26/06/2026 | 26/06/2026 | Kiểm tra & Dọn dẹp |

### Kết quả đạt được tuần 10:

* **Pipeline Tự động:**
  * Xây dựng thành công một CI/CD pipeline đầu cuối, tự tự động build, test và deploy code sau mỗi lần commit.
* **Thành phần Infrastructure as Code:**
  * Sử dụng `buildspec.yml` và `appspec.yml` để khai báo các bước build và triển khai một cách rõ ràng.
* **Triển khai không gián đoạn (Zero Downtime):**
  * Hiểu cách CodeDeploy thực hiện rolling update để duy trì tính khả dụng của ứng dụng trong quá trình triển khai bản cập nhật.

### Những bài học quan trọng:

1. **Nhanh nhẹn và Tốc độ:** CI/CD tăng tốc đáng kể chu kỳ phát hành và giảm thiểu lỗi do thao tác thủ công khi deploy.
2. **Khả năng truy vết:** CodePipeline cung cấp giao diện trực quan về quá trình release, giúp dễ dàng nhận biết lỗi xảy ra ở công đoạn nào.
3. **Kiến trúc tách rời:** Việc sử dụng các công cụ chuyên biệt cho Source (CodeCommit), Build (CodeBuild), và Deploy (CodeDeploy) tạo ra một quy trình DevOps linh hoạt và dễ module hóa.
