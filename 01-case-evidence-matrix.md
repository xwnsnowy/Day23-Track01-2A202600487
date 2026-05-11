# 01 — Case Evidence Matrix (Cá nhân, Block 2)

## A. Case Evidence Matrix — cá nhân

| Trường                             | Trả lời                                                                                                                                                                                                                |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Case                               | Klarna AI Assistant (OpenAI case + Reuters follow-up)                                                                                                                                                                  |
| AI được dùng trong workflow nào?   | Workflow chăm sóc khách hàng qua chat: AI xử lý câu hỏi phổ biến, tự trả lời phần lớn ticket, chuyển tiếp các case phức tạp cho human agent.                                                                           |
| Người dùng chính là ai?            | 1) Customer support operations team (quản lý hiệu suất CS), 2) Agent CS, 3) Khách hàng dùng kênh chat hỗ trợ.                                                                                                          |
| Họ đo metric gì?                   | Khoảng 2.3 triệu cuộc chat được AI xử lý; AI xử lý ~2/3 volume chat; thời gian xử lý giảm; năng lực vận hành được mô tả tương đương ~700 FTE.                                                                          |
| Metric đó thuộc layer nào?         | Productivity, một phần Value (cost/throughput proxy).                                                                                                                                                                  |
| Metric đó chứng minh được gì?      | AI có thể tăng throughput và giảm cycle time ở workflow CS; tự động hóa tạo tác động vận hành rõ ở giai đoạn đầu (volume cao, xử lý nhanh).                                                                            |
| Metric đó chưa chứng minh được gì? | Chưa chứng minh bền vững về Quality/Trust: khách có hài lòng hơn không, case phức tạp có được xử lý tốt không, escalation/complaint có tăng không; chưa chứng minh đầy đủ business value dài hạn ngoài cost proxy.     |
| Thiếu metric nào?                  | 1) CSAT theo mức độ phức tạp case, 2) Escalation rate theo tier, 3) Complaint/reopen rate, 4) First-contact resolution cho case phức tạp, 5) Human handoff quality, 6) Retention/NPS theo cohort trước-sau triển khai. |
| Rủi ro lớn nhất                    | Tối ưu quá mức theo deflection/volume/cost làm giảm trải nghiệm khách hàng ở case khó; dashboard “nhìn đẹp” về năng suất nhưng che khuất suy giảm chất lượng và niềm tin.                                              |
| Bài học cho dashboard nhóm         | Không dùng 1 chỉ số usage/productivity làm chỉ số chính. Phải ghép bộ metric theo cặp: Productivity + Quality + Trust + Value; có decision rule rõ (continue/pivot/kill) khi quality/trust xuống dưới ngưỡng.          |

## Nguồn dùng cho case

- OpenAI Klarna case: https://openai.com/index/klarna/
- Reuters (Klarna điều chỉnh trọng tâm, bổ sung yếu tố con người): https://www.reuters.com/business/swedens-klarna-shifts-ai-focus-cost-cuts-growth-2025-09-10/

## Câu chốt cá nhân

```markdown
Case Klarna dạy tôi rằng: volume và tốc độ có thể tăng rất nhanh khi đưa AI vào CS workflow.

Nhưng chỉ số đó chưa đủ để kết luận thành công dài hạn nếu chưa đo đồng thời chất lượng xử lý case phức tạp và niềm tin khách hàng.

Vì vậy dashboard nhóm tôi phải có paired metrics (Productivity + Quality + Trust + Value) và rule dừng/pivot khi quality giảm.
```

## Tự kiểm tra

- [x] Không chỉ kể chuyện case.
- [x] Có nêu metric cụ thể.
- [x] Có nói metric chứng minh được gì và chưa chứng minh được gì.
- [x] Có ít nhất 1 bài học áp dụng vào dashboard nhóm.
