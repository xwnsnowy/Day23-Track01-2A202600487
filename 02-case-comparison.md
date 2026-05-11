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

## References

1. Morgan Stanley. “Launch of AI @ Morgan Stanley Debrief.” Morgan Stanley Press Release, 2024.
   - Dùng để chứng minh: AI @ Morgan Stanley Assistant được rollout từ 2023; 98% Financial Advisor teams adopted the Assistant; Debrief hỗ trợ ghi chú meeting, action items, draft email và lưu vào Salesforce.

2. OpenAI. “Morgan Stanley uses AI evals to shape the future of wealth management.” OpenAI Customer Story.
   - Dùng để chứng minh: Morgan Stanley dùng AI để hỗ trợ financial advisors truy xuất insight nhanh hơn; document access tăng từ 20% lên 80%; advisors có thêm thời gian cho client relationships.

3. Morgan Stanley. “Artificial Intelligence: Firmwide Team.”
   - Dùng để chứng minh: Morgan Stanley triển khai AI theo hướng human-centric, có controls và oversight.

4. Klarna. “Klarna AI assistant handles two-thirds of customer service chats in its first month.” Klarna Press Release, 2024.
   - Dùng để chứng minh: AI assistant xử lý 2/3 customer service chats; tương đương workload của 700 full-time agents; resolution time giảm từ 11 phút xuống dưới 2 phút.

5. OpenAI. “Klarna’s AI assistant does the work of 700 full-time agents.” OpenAI Customer Story, 2024.
   - Dùng để chứng minh: 2.3 triệu conversations trong tháng đầu; 2/3 customer service chats; tương đương 700 agents; CSAT ngang human agents theo công bố ban đầu; repeat inquiries giảm 25%; resolution time dưới 2 phút.

6. Bloomberg. “Klarna Slows AI-Driven Job Cuts With Call for Real People.” 2025.
   - Dùng để chứng minh: Klarna thừa nhận cách tiếp cận cost-cutting bằng AI trong customer service đã đi quá xa và cần đưa con người trở lại.

7. Fortune. “As Klarna flips from AI-first to hiring people again...” 2025.
   - Dùng để chứng minh: Klarna quay lại tuyển người và CEO nhấn mạnh khách hàng luôn cần lựa chọn gặp human support.

8. Customer Experience Dive. “Klarna changes its AI tune and again recruits humans for customer service.” 2025.
   - Dùng để chứng minh: Sau hơn một năm quảng bá AI chatbot làm workload của 700 representatives, Klarna quay lại dùng người cho customer service.

9. AP News. “AI shakes up the call center industry, but some tasks are still better left to the humans.” 2025.
   - Dùng để chứng minh: Trong ngành call center, AI phù hợp với tác vụ lặp lại nhưng human agents vẫn quan trọng với case phức tạp/sensitive; Klarna là ví dụ về việc đưa người trở lại.

## Tự kiểm tra

- [x] Có 1 case thành công và 1 case cảnh báo.
- [x] Có nêu metric cụ thể cho cả 2 case.
- [x] Có nói rõ metric chứng minh được gì và chưa chứng minh được gì.
- [x] Có bài học áp dụng trực tiếp sang dashboard nhóm.
