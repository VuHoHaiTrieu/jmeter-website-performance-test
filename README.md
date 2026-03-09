# Website Performance Test using Apache JMeter

## 1. Giới thiệu

Bài thực hành kiểm thử hiệu năng website vnexpress.net sử dụng Apache JMeter.

Mục tiêu của bài test:

* Đo thời gian phản hồi của website (Response Time)
* Đánh giá khả năng xử lý request (Throughput)
* Kiểm tra tỷ lệ lỗi (Error Rate)

Công cụ sử dụng: **Apache JMeter 5.6.3**

---

# 2. Kịch bản kiểm thử

## Thread Group 1 – Basic Test

Cấu hình:

* Number of Users: 10
* Loop Count: 5
* Request: HTTP GET Homepage

Kết quả:

| Metric                | Value            |
| --------------------- | ---------------- |
| Total Requests        | 50               |
| Average Response Time | 3548 ms          |
| Min Response Time     | 696 ms           |
| Max Response Time     | 12970 ms         |
| Error Rate            | 0%               |
| Throughput            | 2.1 requests/sec |

Nhận xét:

Website phản hồi trung bình khoảng **3.5 giây** khi có 10 người dùng. Không xuất hiện lỗi trong quá trình kiểm thử.

---

## Thread Group 2 – Heavy Load Test

Cấu hình:

* Number of Users: 50
* Ramp-up Period: 30 seconds
* Requests:

  * Homepage
  * Blog Page

Kết quả:

| Metric                | Value            |
| --------------------- | ---------------- |
| Total Requests        | 100              |
| Average Response Time | 378 ms           |
| Error Rate            | 0%               |
| Throughput            | 3.1 requests/sec |

Nhận xét:

Website vẫn hoạt động ổn định khi tải tăng lên 50 users. Response time trung bình giảm xuống còn khoảng **0.38 giây**.

---

## Thread Group 3 – Custom Scenario

Cấu hình:

* Number of Users: 20
* Duration: 60 seconds
* Requests:

  * Products Page
  * About Page

Kết quả:

| Metric                | Value             |
| --------------------- | ----------------- |
| Total Requests        | 1664              |
| Average Response Time | 381 ms            |
| Error Rate            | 5.47%             |
| Throughput            | 27.6 requests/sec |

Nhận xét:

Khi số lượng request tăng cao trong 60 giây, server vẫn duy trì response time tốt (~0.38s) nhưng bắt đầu xuất hiện lỗi (~5%).

---

# 3. Kết luận

Qua các kịch bản kiểm thử:

* Website hoạt động ổn định với tải nhẹ và trung bình.
* Khi tải cao trong thời gian dài, hệ thống bắt đầu xuất hiện lỗi.
* Điều này cho thấy cần tối ưu thêm hệ thống để xử lý tải lớn.

---

# 4. Tài liệu đính kèm

* File JMeter test plan: [website-performance-test.jmx](./website-performance-test.jmx)
* Kết quả kiểm thử CSV
* Screenshot kết quả Summary Report
