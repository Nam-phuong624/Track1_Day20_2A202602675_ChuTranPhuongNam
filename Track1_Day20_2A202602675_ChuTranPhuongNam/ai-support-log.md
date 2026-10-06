# AI SUPPORT LOG (NHẬT KÝ SỬ DỤNG AI)

**Học viên:** Chử Trần Phương Nam  
**Mã học viên:** 2A202602675  
**Dự án:** E-Commerce Multi-Branch Retail & Fulfillment Platform  

---

### 1. AI đã giúp tôi ở đâu?
* Hỗ trợ đọc nhanh và tổng hợp cấu trúc dữ liệu từ thư mục dự án `E-Commerce-Data-Pipeline-End-to-End-main` (các bảng `orders`, `order_items`, `order_reviews`, `fact_sales_performance`, `fact_operations_delivery` và báo cáo phân tích kinh doanh 2024).
* Gợi ý brainstorm các trường thông tin chuẩn hóa theo template của bài lab (Core Action Card, Action Nature Card, Retention 6 thành phần).
* Hỗ trợ chuẩn hóa tên gọi 6 Core Events theo đúng quy ước `object_action` và soạn thảo 2 tiêu chí nghiệm thu (Acceptance Criteria) chặt chẽ về mặt kỹ thuật dữ liệu (Idempotency và State Transition).

---

### 2. AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?
* **Đề xuất Core Action sai bản chất ban đầu:** AI ban đầu có xu hướng gợi ý chọn hành vi `order_placed` (bấm đặt mua) hoặc `product_searched` làm Core Action vì dễ tracking ngay trên giao diện web/app. Đây là lỗi kinh điển nhầm lẫn giữa thao tác giao diện (UI click) với hành vi nhận giá trị thật.
* **Đề xuất Cadence theo quán tính dashboard:** AI ban đầu đề xuất theo dõi D7 Retention và DAU/WAU theo thói quen của các sản phẩm digital thông thường, không phản ánh đúng chu kỳ nhận lương và mua sắm tiêu dùng định kỳ theo tháng của khách hàng văn phòng.
* **North Star Metric thiếu Quality Threshold:** AI ban đầu đề xuất NSM là "Tổng số đơn hàng thành công hàng tháng" (Gross Orders), bỏ qua rủi ro đơn hàng bị giao trễ quá hạn (OTD thấp) hoặc bị hoàn trả do vỡ hỏng.

---

### 3. Tôi đã tự sửa hoặc quyết định lại điều gì?
* **Quyết định lại Core Action:** Chuyển từ `order_placed` sang **Đặt hàng và nhận giao hàng thành công** (`order_delivered` kèm điều kiện không hoàn trả trong 7 ngày) để đảm bảo giá trị cốt lõi được hiện thực hóa trọn vẹn.
* **Quyết định lại Cadence & Retention Window:** Kiên quyết chuyển từ nhịp Daily/Weekly sang **Monthly Cadence** (chu kỳ 30 ngày) tương ứng với nhịp tiêu dùng sinh hoạt và dòng tiền lương thực tế của Persona Nguyễn Minh Anh.
* **Thiết lập công thức NSM chuẩn 3 thành phần:** Tự tay định nghĩa chỉ số **MSODO (Monthly Satisfied & On-Time Delivered Orders)** tích hợp bộ 3 điều kiện chất lượng: Giao đúng hạn SLA ($\le 0	ext{ ngày trễ}$) + Không bị trả hàng + Điểm đánh giá $\ge 4\star$.
* **Thiết kế Product Loop dựa trên Stored Value:** Xây dựng vòng lặp dựa trên tích lũy điểm thưởng (Loyalty points) và lưu trữ thông tin (1-click reorder) làm động lực quay lại tự nhiên, loại bỏ hoàn toàn việc dựa dẫm vào push notification spam.
