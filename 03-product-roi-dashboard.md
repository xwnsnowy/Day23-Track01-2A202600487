# 03 — Product ROI Dashboard (Nhóm)

## 0. Thông tin nhóm

| Trường                      | Trả lời                                                                                                                                                                                                      |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Nhóm                        | Nhóm 3 người                                                                                                                                                                                                 |
| Thành viên + phần phụ trách | Nguyễn Tiến Thành (2A202600487): Case Klarna + Part A; Nguyễn Thành Đại Khánh (2A202600404): Case Morgan Stanley + Part B metrics; Bùi Trọng Anh (2A202600010): Case JPMorgan + Part C-D + tổng hợp red-team |
| Product chọn phân tích      | AI Chatbot Assistant for SME Customer Support                                                                                                                                                                |
| Người dùng chính            | Agent CS, Team Lead, QA Lead                                                                                                                                                                                 |
| Link repo / file nộp cuối   | Cập nhật sau khi push GitHub                                                                                                                                                                                 |

## 1. Case Comparison (tóm tắt dùng cho dashboard)

| Trường                             | Case thành công / tín hiệu tốt                                              | Case cảnh báo / thất bại                                            |
| ---------------------------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| Case                               | Morgan Stanley AI Assistant                                                 | JPMorgan AI usage dashboards                                        |
| AI được dùng trong workflow nào?   | Advisor tra cứu tri thức nội bộ + chuẩn bị phản hồi có kiểm soát compliance | Theo dõi usage công cụ AI coding của kỹ sư qua dashboard nội bộ     |
| Người dùng chính là ai?            | Wealth advisors, compliance reviewers                                       | Software engineers, engineering managers                            |
| Họ đo metric gì?                   | Adoption cao trong nhóm mục tiêu, giảm thời gian tìm thông tin              | Tần suất/mức độ sử dụng AI tools theo cá nhân hoặc team             |
| Metric đó chứng minh được gì?      | Trust-by-design giúp adoption bền hơn trong môi trường rủi ro               | Chứng minh mức độ hoạt động (activity) của việc dùng công cụ AI     |
| Metric đó chưa chứng minh được gì? | Chưa chứng minh đầy đủ client outcomes dài hạn                              | Chưa chứng minh productivity, quality code hay business impact thực |
| Thiếu metric nào?                  | Retention, NPS, quality score độc lập                                       | Cycle time, defect/rework rate, dev trust/satisfaction, outcome KPI |
| Bài học cho dashboard nhóm         | Chỉ scale khi có trust architecture                                         | Tránh dùng usage làm KPI chính; đo outcome + quality guardrail      |

**Bài học nhóm sẽ áp dụng vào dashboard:**

```markdown
Dashboard nhóm phải tránh vanity metric usage.
Mỗi quyết định scale phải dựa trên bộ chỉ số ghép: Productivity + Quality + Trust + Value.
Nếu quality/trust xuống dưới ngưỡng thì chuyển pivot ngay, không mở rộng theo cảm tính.
Không dùng dashboard cá nhân để xếp hạng mức dùng AI; ưu tiên đo completion + quality ở cấp workflow/team.
```

## Part A — Adoption Context

### A.1 Thách thức nhóm chọn

| Trường                                 | Trả lời                                                                                                                                 |
| -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Thách thức áp dụng AI                  | Đã có AI chatbot hỗ trợ CS nhưng team đang đo nặng usage/volume, thiếu quality/trust nên khó quyết định scale đúng.                     |
| Tình huống xuất phát từ ai / ở đâu?    | Team Customer Support SME của một ngân hàng số (ticket chat inbound cao, áp lực SLA).                                                   |
| Dấu hiệu bị kẹt                        | Deflection tăng nhưng case phức tạp escalated nhiều, QA rework tăng, manager chưa tự tin mở rộng sang tất cả ca làm việc.               |
| Vì sao thách thức này đáng giải quyết? | Nếu đo sai, tổ chức có thể mở rộng sai hướng: ngắn hạn giảm chi phí nhưng dài hạn giảm CSAT, tăng complaint và mất niềm tin khách hàng. |

### A.2 Sản phẩm / công cụ AI

| Trường                                   | Trả lời                                                                                                            |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Tên sản phẩm / công cụ AI                | AI Chatbot Assistant for SME Customer Support                                                                      |
| Người dùng chính                         | Agent CS, CS team lead, QA lead                                                                                    |
| Bối cảnh sử dụng                         | Xử lý ticket chat inbound cho khách SME trong giờ hành chính và giờ cao điểm cuối ngày.                            |
| Mục tiêu kinh doanh / học tập / vận hành | Giảm thời gian xử lý ticket, tăng số ticket hoàn thành đúng SLA, giữ chất lượng trả lời ổn định cho case phức tạp. |
| Không nằm trong phạm vi                  | Voice call channel, fraud investigation, legal dispute case cấp độ cao.                                            |

### A.3 2-4 Quy trình chính

| #   | Tên quy trình          | Vai trò AI                                 | Điểm người kiểm tra                                | Khi AI sai thì xử lý thế nào?                                                     |
| --- | ---------------------- | ------------------------------------------ | -------------------------------------------------- | --------------------------------------------------------------------------------- |
| 1   | Triage ticket đầu vào  | Classify + Recommend priority              | Team lead kiểm tra mẫu ngẫu nhiên 10%/ngày         | Nếu phân loại sai: override nhãn, ghi reason code, cập nhật rule set mỗi tuần     |
| 2   | Draft phản hồi ban đầu | Generate response draft theo KB nội bộ     | Agent bắt buộc review trước khi gửi                | Nếu draft sai: agent sửa thủ công, đánh dấu error type để retrain prompt/template |
| 3   | Handoff case phức tạp  | Summarize hội thoại và đề xuất hướng xử lý | Senior agent duyệt summary trước khi chuyển tier 2 | Nếu summary thiếu ý: bổ sung thủ công theo checklist và escalate manual           |

### A.4 Chẩn đoán nhanh ADKAR

| Stage         | Câu hỏi                                            | Nhận định nhóm                                                      |
| ------------- | -------------------------------------------------- | ------------------------------------------------------------------- |
| Awareness     | Người dùng có biết AI này giúp gì không?           | Có, đa số agent hiểu AI giúp soạn nháp và phân loại nhanh.          |
| Desire        | Người dùng có muốn dùng không?                     | Trung bình thấp, một số agent sợ bị đánh giá theo số lần dùng tool. |
| Knowledge     | Người dùng có biết dùng đúng không?                | Chưa đồng đều giữa ca sáng/chiều, prompt quality chênh lệch.        |
| Ability       | Người dùng có đủ access, thời gian, kỹ năng không? | Có access nhưng thiếu checklist xử lý case phức tạp khi AI sai.     |
| Reinforcement | Có cơ chế khiến họ quay lại dùng không?            | Chưa có coaching loop rõ theo từng workflow.                        |

Barrier chính:

```markdown
Desire + Reinforcement là điểm nghẽn chính: agent lo bị đo usage thay vì chất lượng, nên dùng đối phó.
```

### A.5 3 Tactic áp dụng

| Tactic                                                                       | Nhắm vào barrier nào?     | Áp dụng cho quy trình nào? | Người phụ trách | Khi nào hoàn thành? |
| ---------------------------------------------------------------------------- | ------------------------- | -------------------------- | --------------- | ------------------- |
| Track team-specific impact (đo outcome theo workflow, không đo prompt count) | Desire + Reinforcement    | Cả 3 quy trình             | CS Ops Manager  | Tuần 2              |
| Weekly show-and-tell (chia sẻ case tốt/case lỗi và cách sửa)                 | Knowledge + Reinforcement | Quy trình 2, 3             | QA Lead         | Tuần 3              |
| AI playbook + escalation checklist chuẩn hóa                                 | Ability                   | Quy trình 1, 2, 3          | Team Lead       | Tuần 2              |

## Part B — ROI Dashboard

### B.1 Chỉ số toàn sản phẩm

| Lớp đo             | Chỉ số                                                     | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu               | Người phụ trách | Rủi ro từ phản biện                | Sửa ở v2                                                            |
| ------------------ | ---------------------------------------------------------- | -----------: | -------: | --------------------------- | --------------- | ---------------------------------- | ------------------------------------------------------------------- |
| Activation         | % agent hoàn thành first AI-assisted ticket trong tuần đầu |          58% |      85% | App telemetry + ticket logs | Training Lead   | Có thể ép dùng cho đủ số           | Đổi KPI từ "đã mở tool" sang "hoàn thành ticket + không bị QA fail" |
| Retention / Value  | % ticket hoàn thành trong SLA 24h                          |          72% |      88% | CRM report                  | CS Ops Manager  | SLA tăng do đẩy case dễ cho AI     | Bổ sung phân tách SLA theo độ phức tạp case                         |
| Trust hoặc Quality | CSAT trung bình case có AI assist                          |        4.0/5 |  >=4.3/5 | Post-chat survey            | CX Lead         | CSAT trung bình che khuất case khó | Thêm CSAT theo tier complexity (simple/medium/complex)              |

### B.2 Chỉ số theo từng quy trình

### Quy trình 1 — Triage ticket đầu vào

| Lớp đo       | Chỉ số                                   | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu             | Người phụ trách | Rủi ro từ phản biện               | Sửa ở v2                                   |
| ------------ | ---------------------------------------- | -----------: | -------: | ------------------------- | --------------- | --------------------------------- | ------------------------------------------ |
| Activation   | % ticket đi qua AI triage                |          63% |      90% | Triage logs               | CS Ops Analyst  | Chạy số bằng cách triage qua loa  | Gắn thêm điều kiện triage accepted by lead |
| Engagement   | % ca làm việc dùng triage >= 5 ticket/ca |          49% |      75% | Shift usage report        | Team Lead       | Dùng cho đủ ngưỡng                | Đổi sang chỉ số "triage accepted rate"     |
| Productivity | Median thời gian gán queue (phút)        |          7.8 |    <=3.5 | CRM event timestamps      | CS Ops Manager  | Nhanh nhưng sai queue             | Pair với quality row bên dưới              |
| Quality      | Tỷ lệ phân loại đúng queue lần đầu       |          76% |    >=90% | QA sample + re-route logs | QA Lead         | QA sample không đại diện          | Tăng sample case phức tạp từ 10% lên 20%   |
| Trust        | Tỷ lệ override nhãn triage của lead      |          24% |    <=12% | Override logs             | Team Lead       | Override thấp do lead bỏ kiểm tra | Random audit 2 lần/tuần                    |
| Value        | Chi phí xử lý mỗi ticket (VND)           |        46000 |    33000 | Finance + CRM             | Finance BP      | Cost giảm do cắt quality          | Khóa rule: cost chỉ đạt nếu QA >= ngưỡng   |

### Quy trình 2 — Draft phản hồi ban đầu

| Lớp đo       | Chỉ số                                                  | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu           | Người phụ trách | Rủi ro từ phản biện                  | Sửa ở v2                                           |
| ------------ | ------------------------------------------------------- | -----------: | -------: | ----------------------- | --------------- | ------------------------------------ | -------------------------------------------------- |
| Activation   | % agent dùng AI draft ít nhất 1 lần/ca                  |          61% |      85% | Draft tool logs         | Team Lead       | Dùng 1 lần tượng trưng               | Đổi sang % ticket gửi bằng AI draft + agent review |
| Engagement   | Trung bình số ticket/agent/ca dùng draft đúng quy trình |          4.1 |      7.0 | Workflow logs           | CS Ops Analyst  | Spam draft không gửi                 | Thêm ràng buộc must-link draft-to-send             |
| Productivity | AHT cho ticket mức đơn giản (phút)                      |         11.5 |    <=7.5 | CRM handling time       | CS Ops Manager  | Chỉ nhanh ở case dễ                  | Báo cáo tách theo complexity tier                  |
| Quality      | QA pass rate của phản hồi gửi khách                     |          82% |    >=93% | QA checklist            | QA Lead         | QA bias theo người chấm              | Chuẩn hóa rubric + chấm chéo                       |
| Trust        | Escalation rate sau phản hồi đầu tiên                   |          18% |    <=10% | Escalation logs         | CX Lead         | Escalation giảm do đóng ticket sớm   | Theo dõi reopen trong 72h                          |
| Value        | Tickets/agent/day                                       |           35 |       50 | Daily operations report | CS Ops Manager  | Throughput tăng nhưng complaint tăng | Bắt buộc kèm complaint guardrail                   |

### Quy trình 3 — Handoff case phức tạp

| Lớp đo       | Chỉ số                                        | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu              | Người phụ trách   | Rủi ro từ phản biện                   | Sửa ở v2                                   |
| ------------ | --------------------------------------------- | -----------: | -------: | -------------------------- | ----------------- | ------------------------------------- | ------------------------------------------ |
| Activation   | % case phức tạp có AI summary trước handoff   |          54% |      80% | Handoff logs               | Senior Agent Lead | Summary có mà không dùng              | Track summary utilized by tier 2           |
| Engagement   | % tier-2 agent phản hồi "summary đủ dùng"     |          48% |      75% | Weekly survey + ops review | Tier-2 Manager    | Self-report thiên lệch                | Bổ sung check thực tế từ reopen logs       |
| Productivity | Thời gian hiểu context trước khi xử lý (phút) |         14.0 |    <=8.0 | Tier-2 handling logs       | Tier-2 Manager    | Nhanh nhưng miss context              | Pair với reopen + quality                  |
| Quality      | Tỷ lệ reopen trong 72h (case phức tạp)        |          16% |     <=8% | Reopen logs                | QA Lead           | Reopen thấp do đóng chậm              | Theo dõi thêm first-contact resolution     |
| Trust        | CSAT case phức tạp                            |        3.7/5 |  >=4.2/5 | Post-case survey           | CX Lead           | Mẫu CSAT thấp                         | Trigger reminder survey ở case tier 3      |
| Value        | Tỷ lệ giữ SLA với case tier 3                 |          52% |      75% | SLA dashboard              | Ops Manager       | SLA tăng bằng cách trì hoãn phân loại | Lock timestamp theo first customer message |

## Part C — Dashboard Mock (6 tiles)

```text
┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 1: PRODUCT HEALTH             │ │ TILE 2: TRIAGE WORKFLOW            │
│ Metric: SLA<24h completion rate    │ │ Metric: First-time queue accuracy  │
│ Current: 72%  Target: 88%          │ │ Current: 76%  Target: 90%          │
│ Status: AMBER                      │ │ Status: AMBER                      │
│ Action if red: freeze scale wave   │ │ Action if red: tighten QA sample   │
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 3: DRAFT RESPONSE             │ │ TILE 4: TRUST / QUALITY            │
│ Metric: AHT simple ticket          │ │ Metric: CSAT complex cases         │
│ Current: 11.5m Target: <=7.5m      │ │ Current: 3.7/5 Target: >=4.2/5     │
│ Status: RED                        │ │ Status: RED                        │
│ Action if red: coaching by shift   │ │ Action if red: mandatory handoff   │
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 5: VALUE                      │ │ TILE 6: DECISION                   │
│ Metric: Cost per ticket            │ │ Continue / Pivot / Kill: PIVOT     │
│ Current: 46,000  Target: 33,000    │ │ Metric mạnh nhất: QA pass + CSAT   │
│ Status: AMBER                      │ │ Before scale: fix trust guardrail  │
│ Action if red: stop auto-expansion │ │ Owner: CS Ops Manager              │
└────────────────────────────────────┘ └────────────────────────────────────┘
```

## Part D — Memo Quyết định

```markdown
# Memo Quyết Định Cuối — AI Chatbot Assistant for SME Support

1. Nhóm khuyến nghị: pivot, chưa scale rộng.

2. Chỉ số mạnh nhất để bảo vệ quyết định là:
   CSAT case phức tạp (hiện tại 3.7/5 so với mục tiêu >=4.2/5) kèm reopen 72h (16% so với mục tiêu <=8%).
   Hai chỉ số này cho thấy trust và quality chưa đạt, nên chưa đủ điều kiện scale.

3. Chi so/giả định nhóm đã sửa sau phản biện là:
   V1: đo engagement bằng prompt count/agent/day.
   V2: đổi thành % ticket completed with AI draft + QA pass + no reopen 72h.
   Lý do: V1 dễ bị spam và không chứng minh kết quả workflow; V2 gắn trực tiếp vào output và quality.

4. Trước khi scale, nhóm phải:
   1. Chuẩn hóa escalation checklist cho case phức tạp — QA Lead — deadline T+7 ngày.
   2. Chạy coaching theo ca cho nhóm có QA pass <85% — Team Lead — deadline T+10 ngày.
   3. Thiết lập decision gate tuần: nếu CSAT case phức tạp <4.0 hoặc reopen >10% thì giữ chế độ pivot — CS Ops Manager — deadline T+14 ngày.
```

## 6. Red-team và sửa v2

### Nhóm mình đi red-team nhóm khác

| Vai nhóm được giao | Nhóm bị phản biện | 3 câu hỏi / rủi ro nhóm mình nêu                                                                               |
| ------------------ | ----------------- | -------------------------------------------------------------------------------------------------------------- |
| CFO                | Nhóm A            | 1) Cost saving có đi kèm quality không? 2) Data source nào chống self-report bias? 3) Ngưỡng dừng dự án là gì? |

### Nhóm mình bị red-team

| Red-team risk | Metric / giả định bị chất vấn                 | Nhóm sửa gì ở v2?                            |
| ------------- | --------------------------------------------- | -------------------------------------------- |
| 1             | Đo engagement bằng prompt count dễ bị chạy số | Đổi sang % workflow completion kèm QA pass   |
| 2             | CSAT trung bình che khuất case khó            | Tách CSAT theo complexity tier               |
| 3             | Throughput tăng nhưng có thể tăng lỗi         | Thêm guardrail reopen 72h và escalation rate |

### Ít nhất 2 thay đổi cụ thể từ v1 sang v2

| #   | V1 có vấn đề gì?                | V2 sửa thành gì?                         | Vì sao sửa này tốt hơn?                    |
| --- | ------------------------------- | ---------------------------------------- | ------------------------------------------ |
| 1   | Engagement đo bằng prompt count | Đo % ticket completed with AI + QA pass  | Đo outcome thật thay vì activity           |
| 2   | Chỉ dùng CSAT trung bình        | Tách CSAT theo simple/medium/complex     | Phát hiện rủi ro ở case khó rõ hơn         |
| 3   | Chưa có ngưỡng dừng mở rộng     | Thêm decision gate tuần theo CSAT/reopen | Biến dashboard thành công cụ ra quyết định |

## 7. Checklist trước khi nộp

- [x] Có 1 product cụ thể, không chọn "AI cho cả công ty".
- [x] Có 2-4 workflow chính.
- [x] Mỗi workflow có vai trò AI, human review và failure path.
- [x] Có rào cản ADKAR chính.
- [x] Dashboard có metric toàn product và metric theo workflow.
- [x] Không chỉ đo usage: login, prompt count, DAU/MAU.
- [x] Có baseline, target, data source và owner cho các metric chính.
- [x] Có ít nhất 1 metric Quality, Trust hoặc Value.
- [x] Có Red-team risk và Fix.
- [x] Có ít nhất 2 thay đổi rõ từ v1 sang v2.
- [x] Decision Memo có continue / pivot / kill.
