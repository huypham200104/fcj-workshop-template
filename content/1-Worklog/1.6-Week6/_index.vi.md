---
title: "Worklog Tuần 6"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 6 (23/05 - 29/05/2026):

* Hiểu cách AWS Backup tập trung hóa hoạt động backup và restore cho tài nguyên AWS
* Chuẩn bị hạ tầng workshop bằng Amazon S3 và AWS CloudFormation
* Tạo Backup Plan, Backup Rule, Backup Vault và Resource Assignment
* Bật thông báo backup và restore thông qua Amazon SNS
* Chạy on-demand backup cho EC2 instance và xác thực kết quả backup job
* Kiểm thử restore automation bằng AWS Lambda và xác minh trạng thái restore qua CloudWatch Logs và email notification

### Các công việc cần triển khai trong tuần này:

| Giai đoạn | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 23/05 | - Đọc phần giới thiệu AWS Backup workshop <br> - Hiểu backup planning, RTO, RPO, recovery points và restore validation <br> - Xác định các dịch vụ dùng trong lab: S3, CloudFormation, EC2, SNS, Lambda, CloudWatch và AWS Backup | 23/05/2026 | 23/05/2026 | <https://000013.awsstudygroup.com/vi/1-introduce/> |
| 24/05 | - Tạo S3 bucket cho source files của workshop <br> - Upload CloudFormation template và Lambda function package <br> - Chuẩn bị S3 object URLs để deploy stack | 24/05/2026 | 24/05/2026 | Preparation section |
| 25/05 | - Deploy hạ tầng lab bằng CloudFormation <br> - Cấu hình stack parameters như notification email, S3 bucket name và Lambda package path <br> - Kiểm tra stack outputs gồm application URL và resource identifiers | 25/05/2026 | 25/05/2026 | Infrastructure deployment section |
| 26/05 | - Tạo Backup Plan `BACKUP-LAB` <br> - Cấu hình backup rule hằng ngày `BACKUP-LAB-RULE` <br> - Tạo Backup Vault `BACKUP-LAB-VAULT` <br> - Gán EC2 resources vào backup plan bằng tags | 26/05/2026 | 26/05/2026 | Backup plan section |
| 27/05 | - Bật Backup Vault notifications với Amazon SNS <br> - Cấu hình các event như `BACKUP_JOB_COMPLETED` và `RESTORE_JOB_COMPLETED` <br> - Xác nhận email hoàn tất backup được gửi thành công | 27/05/2026 | 27/05/2026 | Notification section |
| 28/05 | - Tạo on-demand backup cho EC2 instance <br> - Theo dõi Backup job đến trạng thái `Completed` <br> - Kiểm tra recovery point ARN được tạo | 28/05/2026 | 28/05/2026 | Test restore section |
| 29/05 | - Xác thực restore testing qua AWS Backup Restore jobs <br> - Kiểm tra CloudWatch Logs của restore test Lambda function <br> - Xác nhận HTTP 200 validation và cleanup notification email | 29/05/2026 | 29/05/2026 | Test restore section |

### Kết quả đạt được tuần 6:

* **Lập kế hoạch AWS Backup:**
  * Hiểu cách AWS Backup quản lý backup policies từ một dịch vụ tập trung
  * Hiểu vì sao RTO và RPO nên được xác định theo từng workload
  * Tạo luồng backup theo plan thay vì phụ thuộc vào snapshot thủ công

* **Chuẩn bị hạ tầng:**
  * Tạo S3 bucket để lưu CloudFormation template và Lambda package
  * Deploy hạ tầng hỗ trợ bằng CloudFormation
  * Chuẩn bị EC2 instance, SNS topic và Lambda restore test function cho bài lab

* **Backup Plan và Resource Assignment:**
  * Tạo backup plan `BACKUP-LAB`
  * Tạo backup rule `BACKUP-LAB-RULE` và backup vault `BACKUP-LAB-VAULT`
  * Gán EC2 resources vào plan bằng tag-based resource selection
  * Dùng default AWS Backup IAM role cho backup và restore operations

* **Tích hợp Notification:**
  * Bật Backup Vault notifications thông qua SNS
  * Nhận email notification khi backup job hoàn tất thành công
  * Xác nhận nội dung notification có recovery point ARN, resource ARN và backup job ID

* **Xác thực Backup và Restore:**
  * Tạo on-demand backup cho EC2 instance
  * Kiểm tra restore job đạt trạng thái `Completed`
  * Review CloudWatch Logs cho restore test và cleanup activities
  * Xác nhận restore validation thành công với HTTP 200 và restored resource đã được cleanup

### Minh chứng và phân tích:

* **Thông báo backup job:** Email notification xác nhận AWS Backup job đã hoàn tất thành công và tạo recovery point cho EC2 resource.

{{< image src="images/worklog/week6_backup_notification.jpg" alt="AWS Backup job completed notification email" >}}

* **Restore job completed:** Trang AWS Backup Jobs hiển thị restore job ở trạng thái `Completed`, xác nhận quá trình restore đã chạy thành công.

{{< image src="images/worklog/week6_restore_job_completed.jpg" alt="AWS Backup restore job completed" >}}

* **Restore Lambda logs:** CloudWatch Logs cho thấy restore test function được thực thi, xóa EC2 resource tạm sau khi restore và gửi thông báo xác nhận cuối cùng.

{{< image src="images/worklog/week6_restore_lambda_logs.jpg" alt="CloudWatch Logs for AWS Backup restore test Lambda" >}}

* **Email Restore Test Status:** Email restore status xác nhận data recovery validation thành công với HTTP 200 và restored resource mới tạo đã được cleanup.

{{< image src="images/worklog/week6_restore_test_status.jpg" alt="AWS Backup restore test status email" >}}

### Phân tích báo cáo AWS tuần 6:

* **Mức phù hợp của kiến trúc:** Luồng triển khai kết hợp AWS Backup để điều phối backup, S3 và CloudFormation để deploy lab, SNS để gửi notification, Lambda để tự động kiểm thử restore, và CloudWatch Logs để quan sát quá trình thực thi. Đây là kiến trúc backup thực tế vì nó xác minh khả năng khôi phục, không chỉ kiểm tra việc bản sao lưu có tồn tại.

* **Độ tin cậy backup:** Backup plan với backup vault và tag-based resource assignment giúp giảm thao tác thủ công và kiểm soát phạm vi backup rõ ràng hơn. Recovery point ARN trong notification giúp truy vết từng backup job đã hoàn tất.

* **Xác thực restore:** Restore job và HTTP 200 validation là phần quan trọng nhất của bài lab. Backup chỉ thật sự có giá trị khi application có thể được khôi phục và xác minh trong recovery objective mong muốn.

* **Giá trị automation:** Lambda restore test giảm công sức vận hành bằng cách tự động xác thực restored resource và cleanup sau khi kiểm thử. Cách này giúp quá trình validation lặp lại được và hạn chế chi phí.

* **Rủi ro và kiểm soát:** Các rủi ro chính gồm quên xác nhận SNS, tag resource sai, IAM permissions quá rộng, và restore test để lại resource tạm đang chạy. Có thể giảm rủi ro bằng tag standard rõ ràng, IAM least-privilege, review CloudWatch Logs và kiểm tra cleanup tự động.

### Những bài học quan trọng:

1. **Backup cần được kiểm thử restore** - Backup job hoàn tất chưa đủ để chứng minh dữ liệu có thể khôi phục.
2. **Backup Plans chuẩn hóa bảo vệ dữ liệu** - AWS Backup Plans giúp quản lý tần suất backup, vault và resource assignment dễ hơn.
3. **SNS tăng khả năng nhận biết vận hành** - Email notifications giúp operator biết khi backup và restore hoàn tất.
4. **Lambda có thể tự động hóa validation** - Restore test có thể kiểm tra health của application và xóa restored resource tạm.
5. **CloudWatch Logs rất cần cho troubleshooting** - Logs thể hiện luồng restore test, cleanup action và final confirmation.

### Tài liệu & Công cụ sử dụng:

* AWS Backup Workshop: <https://000013.awsstudygroup.com/vi/1-introduce/>
* AWS Backup Console
* Amazon S3
* AWS CloudFormation
* Amazon EC2
* Amazon SNS
* AWS Lambda
* Amazon CloudWatch Logs
