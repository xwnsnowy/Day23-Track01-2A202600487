# 02 — Case Comparison (Nhóm)

## Phân công case theo thành viên

- Nguyễn Tiến Thành (2A202600487): Klarna AI Assistant (cá nhân, file 01)
- Nguyễn Thành Đại Khánh (2A202600404): Morgan Stanley AI Assistant
- Bùi Trọng Anh (2A202600010): JPMorgan AI usage dashboard

## So sánh 1 case tín hiệu tốt và 1 case cảnh báo

| Trường                             | Case thành công / tín hiệu tốt                                                                                                           | Case cảnh báo / thất bại                                                                                                          |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Case                               | Morgan Stanley AI Assistant (OpenAI case study)                                                                                          | JPMorgan AI usage dashboards (Business Insider)                                                                                   |
| Workflow có AI                     | Wealth advisors tra cứu knowledge nội bộ, tóm tắt tài liệu, chuẩn bị phản hồi khách hàng với kiểm soát compliance.                       | Theo dõi mức sử dụng AI coding tools của kỹ sư qua dashboard phân loại mức dùng.                                                  |
| Metric chính                       | Tỷ lệ sử dụng cao trong nhóm advisor mục tiêu; thời gian tìm thông tin giảm; năng suất chuẩn bị nội dung tư vấn tăng.                    | Chỉ số tần suất sử dụng công cụ AI theo cá nhân/nhóm (usage tracking dashboard).                                                  |
| Metric đó chứng minh được gì?      | Trust architecture (eval + expert feedback + compliance) có thể giúp adoption cao trong môi trường rủi ro cao.                           | Chứng minh được mức độ hoạt động (activity) và mức tiếp cận công cụ AI giữa các nhóm kỹ sư.                                       |
| Metric đó chưa chứng minh được gì? | Chưa chứng minh đầy đủ kết quả cuối cùng ở tầng business/client outcomes dài hạn (retention, NPS, advisory quality theo cohort).         | Chưa chứng minh productivity thực, quality code, defect rate hay giá trị kinh doanh; có nguy cơ tạo cảm giác bị giám sát.         |
| Thiếu metric nào?                  | 1) Client retention theo cohort, 2) Advisor output quality score độc lập, 3) Complaint/compliance incident trend, 4) NPS theo phân khúc. | 1) Cycle time PR, 2) Defect/rework rate, 3) Incident rate sau release, 4) Dev satisfaction/trust, 5) Business impact per feature. |
| Bài học cho dashboard nhóm         | Scale chỉ khi có trust-by-design, không scale theo usage đơn lẻ.                                                                         | Không dùng usage cá nhân làm KPI chính; phải đo outcome workflow và quality guardrail để tránh Goodhart/coercion.                 |

## Bài học nhóm sẽ áp dụng vào dashboard

```markdown
Case thành công dạy nhóm tôi rằng:
Muốn adoption bền vững phải thiết kế trust architecture trước khi scale (human review, compliance, feedback loop).

Case cảnh báo / thất bại dạy nhóm tôi rằng:
Dashboard usage theo cá nhân không đồng nghĩa tạo giá trị; nếu đo activity thay vì outcome sẽ dễ tạo hành vi đối phó.

Vì vậy dashboard nhóm tôi phải:

1. Đo theo cặp Productivity + Quality + Trust + Value,
2. Có owner và data source cho từng metric,
3. Có rule continue/pivot/kill khi quality hoặc trust xuống dưới ngưỡng.
```

## Tự kiểm tra

- [x] Có 1 case thành công và 1 case cảnh báo.
- [x] Có nêu metric cụ thể cho cả 2 case.
- [x] Có nói rõ metric chứng minh được gì và chưa chứng minh được gì.
- [x] Có bài học áp dụng trực tiếp sang dashboard nhóm.
