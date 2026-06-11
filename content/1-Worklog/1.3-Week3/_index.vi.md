---
title: "Worklog Tuần 3"
date: 2026-05-02
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 3 (02/05 - 15/05/2026):

* Hiểu vai trò của Amazon CloudWatch trong việc giám sát tài nguyên AWS và ứng dụng
* Thực hành CloudWatch Metrics, Logs, Logs Insights, Metric Filters, Alarms và Dashboards
* Chuyển đổi application logs thành metrics có thể đo lường để phục vụ monitoring
* Cấu hình email notification thông qua Amazon SNS khi alarm vượt ngưỡng
* Xây dựng CloudWatch dashboard để tập trung các tín hiệu giám sát quan trọng

### Các công việc cần triển khai trong tuần này:

| Giai đoạn | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 02/05 - 04/05 | - Đọc tổng quan Amazon CloudWatch workshop <br> - Nắm các khái niệm CloudWatch: metrics, logs, alarms và dashboards <br> - Chuẩn bị môi trường workshop và tài nguyên EC2 | 02/05/2026 | 04/05/2026 | <https://000008.awsstudygroup.com/vi/> |
| 05/05 - 07/05 | - Khảo sát CloudWatch Metrics <br> - So sánh EC2 metrics và custom CWAgent metrics <br> - Dùng search expressions để lọc metrics <br> - Thêm annotations và điều chỉnh cách hiển thị biểu đồ | 05/05/2026 | 07/05/2026 | CloudWatch Metric section |
| 08/05 - 10/05 | - Thực hành metric math expressions như sort và filter top metrics <br> - Tạo dynamic labels để legend biểu đồ rõ ràng hơn <br> - Phân tích process memory metrics trong namespace CloudWatch Agent | 08/05/2026 | 10/05/2026 | CloudWatch Metric section |
| 11/05 - 13/05 | - Làm việc với CloudWatch Logs và Logs Insights <br> - Query application logs theo từ khóa như `ERROR` và `WARN` <br> - Tạo metric filter từ error logs trong `/var/log/messages` | 11/05/2026 | 13/05/2026 | CloudWatch Logs section |
| 14/05 - 15/05 | - Tạo CloudWatch Alarm cho error logs <br> - Cấu hình SNS email subscription và xác nhận subscription <br> - Thêm alarm widget vào CloudWatch Dashboard <br> - Tổng hợp kết quả và ghi nhận bài học | 14/05/2026 | 15/05/2026 | CloudWatch Alarms and Dashboards sections |

### Kết quả đạt được tuần 3:

* **CloudWatch Metrics:**
  * Xem và so sánh EC2 metrics với custom CWAgent metrics
  * Dùng search expressions để tìm nhanh metrics cần theo dõi
  * Áp dụng metric math để sort và filter metrics hiển thị trên biểu đồ
  * Tạo dynamic labels giúp legend của biểu đồ dễ đọc hơn

* **CloudWatch Logs và Logs Insights:**
  * Làm việc với application logs được lưu trong CloudWatch Logs
  * Query logs bằng Logs Insights để xác định các sự kiện `ERROR` và `WARN`
  * Hiểu cách log queries hỗ trợ troubleshooting và root-cause analysis nhanh hơn

* **Triển khai Metric Filter:**
  * Tạo metric filter cho error logs từ `/var/log/messages`
  * Chuyển đổi log events thành CloudWatch metric có thể đo lường
  * Sử dụng metric namespace `ec2-logs` và metric name `/var/log/messages - ERROR`

* **CloudWatch Alarm và SNS Notification:**
  * Tạo alarm `PythonApplicationErrorAlarm` để theo dõi số lượng error logs
  * Cấu hình threshold để alarm được kích hoạt khi error logs vượt ngưỡng mong muốn
  * Tạo và xác nhận SNS topic subscription để nhận email notification

* **CloudWatch Dashboard:**
  * Tạo dashboard `CloudWatch-Workshop`
  * Thêm alarm widget vào dashboard
  * Dùng dashboard để tập trung thông tin monitoring và dễ review trạng thái vận hành

### Minh chứng và phân tích:

* **Biểu đồ metrics và dynamic labels:** Ảnh dưới đây cho thấy CloudWatch Metrics sử dụng namespace `CWAgent` và metric `procstat_memory_rss`. Dynamic labels giúp phân biệt process, instance và metric ngay trong phần legend của biểu đồ.

{{< image src="images/worklog/week3_cloudwatch_metrics.jpg" alt="CloudWatch Metrics with dynamic labels" >}}

* **Xác nhận SNS subscription:** Email từ AWS Notifications chứng minh SNS topic đã được tạo và cần xác nhận email subscription trước khi có thể nhận thông báo từ alarm.

{{< image src="images/worklog/week3_sns_subscription.jpg" alt="AWS SNS subscription confirmation email" >}}

* **Kết quả CloudWatch Dashboard:** Dashboard có widget `PythonApplicationErrorAlarm`, giúp theo dõi trạng thái alarm về error logs tại một màn hình trung tâm.

{{< image src="images/worklog/week3_cloudwatch_dashboard.jpg" alt="CloudWatch Workshop dashboard with alarm widget" >}}

### Phân tích báo cáo AWS tuần 3:

* **Mức phù hợp của kiến trúc:** CloudWatch Metrics, Logs, Metric Filters, Alarms, SNS và Dashboards tạo thành một luồng observability hoàn chỉnh. Logs ghi nhận hành vi thô của ứng dụng, metric filters chuyển log quan trọng thành chỉ số đo được, alarms đánh giá ngưỡng, SNS gửi thông báo, và dashboards gom trạng thái vận hành vào một nơi.

* **Giá trị vận hành:** Luồng này hữu ích vì giảm thời gian phát hiện lỗi ứng dụng. Thay vì phải kiểm tra log EC2 thủ công, hệ thống có thể hiển thị số lượng lỗi và gửi thông báo khi vượt ngưỡng.

* **Chất lượng monitoring:** Dynamic labels và dashboard widgets giúp dữ liệu dễ đọc hơn khi có nhiều instances hoặc processes. Đây là yếu tố quan trọng nếu mở rộng cách monitoring này cho nhiều EC2 instances.

* **Rủi ro và kiểm soát:** Các rủi ro chính gồm alarm quá nhiễu, quên xác nhận SNS subscription, và metric filter không khớp đúng log pattern. Có thể giảm rủi ro bằng cách test filter pattern, chọn threshold thực tế, xác nhận SNS subscription, và xem lại alarm history sau khi triển khai.

### Những bài học quan trọng:

1. **Metrics giúp đo lường hành vi hệ thống** - CloudWatch Metrics hỗ trợ so sánh mức sử dụng tài nguyên và phát hiện xu hướng bất thường.
2. **Logs Insights tăng tốc troubleshooting** - Query logs theo từ khóa và khoảng thời gian nhanh hơn nhiều so với đọc raw logs thủ công.
3. **Metric Filters kết nối logs và alarms** - Log pattern quan trọng có thể được chuyển thành metric để phục vụ alerting tự động.
4. **SNS cần được xác nhận** - Email notifications chỉ hoạt động sau khi subscription được confirm.
5. **Dashboards cải thiện khả năng quan sát** - Dashboard gom alarms và metrics vào một nơi để monitoring dễ hơn.

### Tài liệu & Công cụ sử dụng:

* AWS CloudWatch Workshop: <https://000008.awsstudygroup.com/vi/>
* Amazon CloudWatch Metrics
* Amazon CloudWatch Logs và Logs Insights
* CloudWatch Metric Filters
* CloudWatch Alarms
* Amazon SNS
* CloudWatch Dashboards
