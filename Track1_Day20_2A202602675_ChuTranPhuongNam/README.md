# BÀI LAB DAY 20 — PRODUCT METRICS PACK

* **Họ và tên:** Chử Trần Phương Nam
* **Mã học viên (MHV):** 2A202602675
* **Lớp / Track:** Track 1
* **Dự án thực hiện:** Hệ thống Thương mại Điện tử & Giao vận Đa Chi nhánh (E-Commerce Multi-Branch Retail & Fulfillment Platform — Olist Vietnam)

---

## 🔗 Liên kết tệp Metrics Pack
* **Tệp chi tiết Metrics Pack (00 -> 06):** [Xem file metrics_pack.md](./metrics_pack.md)

---

## 📊 Tóm tắt Hệ thống Product Metrics (Executive Summary)

| Hạng mục | Quyết định sản phẩm cốt lõi | Lý do |
| :--- | :--- | :--- |
| **Persona & Core Job** | **Nguyễn Minh Anh (27 tuổi, NVVP)**<br>Tìm mua đồ gia dụng/tiêu dùng, nhận hàng đúng hẹn, an toàn. | Giải quyết trực tiếp bài toán bận rộn, sợ giao trễ, sợ hàng lỗi. |
| **Core Action** | **Đặt đơn & Nhận hàng giao thành công**<br>(`order_delivered` + không hoàn trả) | Giá trị chỉ thực sự sinh ra khi khách cầm món hàng trên tay, không dừng lại ở click "Đặt mua". |
| **Natural Cadence** | **Monthly (1–2 lần / tháng)** | Khớp với chu kỳ nhận lương và tiêu dùng tự nhiên; không ép Daily/Weekly. |
| **Activation Metric** | **First Delivered Order trong 14 ngày** | Đủ thời gian cho hành trình khám phá, đặt hàng, vận chuyển (2–3 ngày) và trải nghiệm. |
| **North Star Metric (NSM)** | **Monthly Satisfied & On-Time Delivered Orders (MSODO)** | Kết hợp đủ 3 yếu tố: Unit of Value (Đơn giao) + Quality SLA (Đúng hạn OTD, Review $\ge 4\star$, Không trả) + Frequency (Tháng). |
| **Retention Window** | **Monthly Cohort Retention (M1, M2, M3)** | Đo lường tỷ lệ quay lại mua hàng sau mỗi chu kỳ 30 ngày. |
| **Product Loop** | **Progress & Stored Value Loop** | Giảm ma sát reorder (1-click) và tích lũy điểm thưởng thành viên (Loyalty points) làm động lực quay lại tự nhiên. |
| **Event Tracking** | **6 Core Events (`object_action`)** | Ghi nhận chính xác các mốc trạng thái (`order_placed` -> `packed` -> `shipped` -> `delivered` -> `reviewed` -> `returned`) với cơ chế Idempotency. |

---

## 💡 Điều tôi mang về áp dụng cho dự án thật

1. **"Nature trước, Nurture sau":** Không bao giờ được dùng notification, popup hay gamification để ép người dùng quay lại theo một tần suất giả tạo (như ép mua hàng online mỗi ngày). Nurture chỉ có ý nghĩa khi nó phục vụ và khuếch đại nhịp nhu cầu tự nhiên của khách hàng.
2. **Active & Activated:** Người dùng mở app hay đăng nhập chỉ là *Active* (hoạt động bề mặt). Người dùng chỉ thực sự *Activated* khi họ hoàn tất chu trình nhận giá trị cốt lõi đầu tiên (`first_order_delivered`).
3. **North Star Metric phải có Quality Threshold:** Nếu chỉ đo số lượng đơn hàng hay doanh thu thuần túy, đội ngũ sẽ dễ bị cuốn vào việc chạy theo số lượng ảo, hy sinh chất lượng giao vận và biên lợi nhuận. Bộ lọc chất lượng (OTD, Không hoàn trả, Review cao) là rào chắn bắt buộc để tăng trưởng bền vững.
4. **Tracking là hợp đồng giữa Product và Data:** Mỗi event bắn đi phải là một "sự kiện đã hoàn tất" và bắt buộc phải phục vụ tính toán một chỉ số cụ thể trong hệ thống metric.
