# 03 — Product ROI Dashboard (Cá nhân)

## 0. Thông tin cá nhân

| Trường                    | Trả lời                                                  |
| ------------------------- | -------------------------------------------------------- |
| Tên sinh viên             | Nguyễn Tiến Thành (2A202600487)                          |
| Product chọn phân tích    | Semantic Video Workspace (Chrome Extension)              |
| Người dùng chính          | Sinh viên STEM & Y khoa, Educator                        |
| Dữ liệu pilot             | Pilot 20 sinh viên tại VinUni, tháng 5 2026 (mùa ôn thi) |
| Link repo / file nộp cuối | https://github.com/xwnsnowy/Day23-Track01-2A202600487    |

## 1. Tín hiệu thành công từ pilot

Pilot SVWorkspace với 20 sinh viên VinUni trong 2 tuần mùa ôn thi tháng 5 2026:

| Chỉ số                             | Kết quả           | Ý nghĩa                                                |
| ---------------------------------- | ----------------- | ------------------------------------------------------ |
| Timestamp Click-Through Rate (CTR) | 47% (target: 40%) | ✓ Người dùng tin tưởng AI và dùng nó tìm đúng đoạn cần |
| Thời gian tìm kiếm                 | 23 phút → 41 giây | ✓ Tiết kiệm 96% thời gian rà soát thủ công             |
| Churn sau 2 tuần                   | 0/20 uninstall    | ✓ Chưa có ai bỏ cài đặt → Lock-in mạnh                 |
| Net Promoter Score (NPS)           | 8.2/10            | ✓ Người dùng sẵn sàng giới thiệu cho bạn bè            |
| LTV / CAC ratio (ước tính)         | 5.1x              | ✓ Unit economics bền vững: LTV gấp 5 lần CAC           |

**Bài học ứng dụng vào dashboard:**

- Metric chính không phải là "số lần dùng tool" (vanity metric) mà là **Timestamp CTR** (outcome-driven).
- Chỉ scale khi có bằng chứng rõ về **Time Saved** + **NPS duy trì** + **churn thấp**.
- Cần tracking **Quality nhân viên** (accuracy của timestamp) kèm **Trust từ người dùng** (NPS).
- Nếu CTR hoặc NPS xuống dưới ngưỡng, phải pivot ngay, không mở rộng.

## Part A — Adoption Context

### A.1 Thách thức sản phẩm chọn

| Trường                                 | Trả lời                                                                                                                                                                                                                 |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Thách thức áp dụng AI                  | Sinh viên đã dùng LMS của trường, nhưng không có cách tra cứu nhanh một khái niệm cụ thể trong video bài giảng dài 1-2 tiếng. Cần chứng minh rằng AI semantic search **thực sự tiết kiệm thời gian** trước khi mở rộng. |
| Tình huống xuất phát từ ai / ở đâu?    | 20 sinh viên STEM & Y khoa tại VinUni trong mùa ôn thi cuối kỳ tháng 5 2026 (cao điểm nhu cầu ôn luyện).                                                                                                                |
| Dấu hiệu bị kẹt                        | Sinh viên cảm thấy search feature của YouTube/Canvas chỉ tìm được keyword từ tiêu đề, không tìm được nội dung nói trong bài giảng. Thời gian tìm kiếm vẫn là 15-30 phút mỗi lần.                                        |
| Vì sao thách thức này đáng giải quyết? | Nếu proof-of-concept thất bại (CTR thấp hoặc churn cao), thì giả định về market demand không đúng; nên không nên cấp funding lớn cho v2. Ngược lại, nếu CTR > 40% + NPS > 8, có thể scale sang nhiều trường khác.       |

### A.2 Sản phẩm / công cụ AI

| Trường                                   | Trả lời                                                                                                                                  |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Tên sản phẩm / công cụ AI                | Semantic Video Workspace (Chrome Extension)                                                                                              |
| Người dùng chính                         | Sinh viên STEM (CS, AI, Engineering), sinh viên Y khoa, người học e-learning chuyên sâu                                                  |
| Bối cảnh sử dụng                         | Ôn thi cuối kỳ hoặc làm đồ án: mở Chrome extension khi xem video bài giảng trên YouTube/Canvas LMS, gõ câu hỏi về khái niệm, AI chỉ tới. |
| Mục tiêu kinh doanh / học tập / vận hành | Tiết kiệm 15-30 phút tìm kiếm thủ công mỗi lần, tăng NPS, duy trì churn 0% để xác nhận product-market fit.                               |
| Không nằm trong phạm vi                  | Không tạo video mới, không upload/lưu trữ video của nhà trường, không track cá nhân để xếp hạng sinh viên.                               |

### A.3 3 Quy trình chính

| #   | Tên quy trình               | Vai trò AI                                                    | Điểm người kiểm tra                 | Khi AI sai thì xử lý thế nào?                                       |
| --- | --------------------------- | ------------------------------------------------------------- | ----------------------------------- | ------------------------------------------------------------------- |
| 1   | Semantic Query Processing   | Hiểu câu hỏi tự nhiên của sinh viên, tìm đoạn video liên quan | QA spot-check query trả lời sai     | Ghi log error query, điều chỉnh prompt template, retrain embeddings |
| 2   | Timestamp Extraction & Jump | Trích xuất giây cụ thể từ transcript, điều khiển video player | Spot-check accuracy timestamp >=95% | Nếu timestamp sai >5% → rollback feature, cải thiện accuracy        |
| 3   | User Feedback Collection    | Thu thập rating (👍👎) sau mỗi lượt jump, dùng để improve RAG | Theo dõi feedback rate & sentiment  | Nếu thumbs-down tăng > 20% → tạm dừng scope expand, fix core engine |

### A.4 Chẩn đoán nhanh ADKAR

| Stage         | Câu hỏi                                        | Nhận định                                                                 |
| ------------- | ---------------------------------------------- | ------------------------------------------------------------------------- |
| Awareness     | Sinh viên có biết extension này giúp gì không? | Có, 100% pilot user tìm hiểu qua introduction session 30 phút.            |
| Desire        | Sinh viên có muốn dùng không?                  | Cao, vì mục đích rõ ràng (tiết kiệm thời gian ôn thi). Churn 0 @ 2 tuần.  |
| Knowledge     | Sinh viên có biết dùng đúng không?             | Chưa đồng đều: một số gõ câu hỏi quá cụ thể, một số quá chung chung.      |
| Ability       | Sinh viên có access, kỹ năng, browser support? | Có, cộng với guide document + video tutorial 5 phút đã đủ.                |
| Reinforcement | Có cơ chế khuyến khích quay lại dùng không?    | Yếu: chưa có gamification hay streak. Chỉ có noti khi có câu hỏi hay hay. |

Barrier chính:

```markdown
Reinforcement là điểm yếu: sinh viên muốn dùng (Desire cao) nhưng sau khi ôn thi xong
sẽ gỡ cài để giải phóng dung lượng. Cần tạo hook hằng tháng (ví dụ: Quiz recommendation)
để sinh viên giữ extension qua các mùa học.
```

### A.5 3 Tactic áp dụng

| Tactic                                                                       | Nhắm vào barrier nào?  | Áp dụng cho quy trình nào? | Người phụ trách | Khi nào hoàn thành? |
| ---------------------------------------------------------------------------- | ---------------------- | -------------------------- | --------------- | ------------------- |
| Auto-suggest related quizzes based on search history (keep hook active)      | Reinforcement          | Quy trình 3 feedback       | Product Manager | Tuần 2 sau pilot    |
| Weekly "Top 5 queries" email digest shared in study groups (social proof)    | Desire + Reinforcement | Quy trình 1 + 2            | Content Lead    | Tuần 3 sau pilot    |
| Timestamp accuracy dashboard visible to power users (transparency + control) | Knowledge + Ability    | Quy trình 2                | Engineer        | Tuần 1 sau pilot    |

## Part B — ROI Dashboard

### B.1 Chỉ số toàn sản phẩm

| Lớp đo             | Chỉ số                                                   | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu            | Người phụ trách | Rủi ro từ phản biện                                  | Sửa ở v2                                                            |
| ------------------ | -------------------------------------------------------- | -----------: | -------: | ------------------------ | --------------- | ---------------------------------------------------- | ------------------------------------------------------------------- |
| Activation         | % sinh viên cài extension trong tuần đầu tháng thi       |          85% |      95% | Extension analytics logs | Growth Lead     | Có thể ép cài thông qua forced email                 | Đổi KPI từ "cài" sang "cài + dùng >= 1 lần/ngày trong tuần 1"       |
| Engagement / Value | Timestamp Click-Through Rate (% câu hỏi click timestamp) |          47% |      55% | Extension event tracking | Product Manager | CTR cao nhưng user chỉ dùng 1-2 tháng thi            | Bổ sung "% user active >= 1 lần/tuần sau thi xong" (retention hook) |
| Trust / Retention  | NPS (Net Promoter Score)                                 |          8.2 |    >=8.5 | Post-session survey      | CX Lead         | NPS cao do chỉ hỏi những user cuối cùng, sample bias | Trigger survey random ở tất cả user, không chỉ những người active   |

### B.2 Chỉ số theo từng quy trình

### Quy trình 1 — Semantic Query Processing

| Lớp đo       | Chỉ số                                     | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu            | Người phụ trách | Rủi ro từ phản biện                | Sửa ở v2                                     |
| ------------ | ------------------------------------------ | -----------: | -------: | ------------------------ | --------------- | ---------------------------------- | -------------------------------------------- |
| Activation   | % sinh viên gõ >= 1 câu hỏi trong tuần     |          81% |      90% | Query logs               | Product Manager | Có thể gõ câu hỏi nhưng không có ý | Đổi sang "% query trả lại kết quả khác rỗng" |
| Engagement   | Avg số query/sinh viên/tuần                |          7.2 |     12.0 | Query analytics          | Data Analyst    | Đếm được query rác hoặc thử nghiệm | Lọc query có length >= 5 words               |
| Productivity | Avg latency từ query đến kết quả (giây)    |          1.8 |    <=2.0 | API response times       | Engineer        | Network latency làm giả tốc độ     | Đo latency ở 10th percentile, không median   |
| Quality      | % query return relevant result (>=0.7 sim) |          74% |    >=85% | Manual spot-check + NDCG | QA Lead         | Relevance bias theo annotator      | Blind peer-review 10% query sau mỗi tuần     |
| Trust        | % query user không rate thumbs-down        |          88% |    >=92% | Feedback logs            | CX Lead         | User forget to rate                | Auto-trigger feedback popup sau 3s nếu click |
| Value        | Query-to-CTR conversion (% query → click)  |          47% |    >=52% | Click-through analytics  | Product Manager | CTR cao nhưng user không apply học | Measure "quiz score ↑ sau dùng" as outcome   |

### Quy trình 2 — Timestamp Extraction & Jump

| Lớp đo       | Chỉ số                                                     | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu                    | Người phụ trách | Rủi ro từ phản biện                  | Sửa ở v2                                                     |
| ------------ | ---------------------------------------------------------- | -----------: | -------: | -------------------------------- | --------------- | ------------------------------------ | ------------------------------------------------------------ |
| Activation   | % query có timestamp output được sinh ra                   |          95% |    >=99% | Output logs                      | Engineer        | Có timestamp nhưng sai               | Thêm confidence score, chỉ show nếu >0.8                     |
| Engagement   | % timestamp user actually click on first try               |          47% |    >=55% | Click event tracking             | Product Manager | Click nhưng không dùng đoạn video đó | Measure watch duration at timestamp > 5s                     |
| Productivity | Time from click to watch correct segment (trong 5s)        |        <=2.1 |    <=1.5 | Video player telemetry           | Engineer        | Video buffer time inflate latency    | Filter out buffer events, measure actual seek only           |
| Quality      | Timestamp accuracy (student confirm it was the right part) |          91% |    >=96% | Post-session survey (spot-check) | QA Lead         | Self-report bias from student        | Random quiz: "Minute XY covered what topic?" as ground truth |
| Trust        | % student thumbs-up after watching segment                 |          85% |    >=90% | Rating buttons                   | CX Lead         | User forget to rate / habit bias     | Incentivize: "Helpful? 👍 → unlock monthly digest"           |
| Value        | Repeatable queries (same/similar Q asked by 2+ users)      |          23% |    >=40% | Query similarity graph           | Product Manager | Only power users ask repeated Q      | Target ambassadors to share questions in study groups        |

### Quy trình 3 — User Feedback Collection

| Lớp đo       | Chỉ số                                             | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu              | Người phụ trách | Rủi ro từ phản biện                  | Sửa ở v2                                 |
| ------------ | -------------------------------------------------- | -----------: | -------: | -------------------------- | --------------- | ------------------------------------ | ---------------------------------------- |
| Activation   | % user submit >= 1 feedback (👍 or 👎) / tuần      |          62% |    >=75% | Rating logs                | Growth Lead     | Rate for social proof, not quality   | Show feedback count to reduce bias       |
| Engagement   | Ratio thumbs-up vs thumbs-down                     |          7.1 |    >=8.0 | Sentiment tracking         | Data Analyst    | Self-report: only extreme users rate | Follow up survey "Why not rate earlier?" |
| Productivity | Time spent rating result (sec)                     |          2.3 |    <=1.5 | UI telemetry               | Designer        | Rating UI too slow                   | Move rating buttons from side to inline  |
| Quality      | % negative feedback attributed to timestamp error  |          34% |    <=15% | Feedback category analysis | QA Lead         | Users blame AI when they query wrong | Add "Was the query clear?" checker       |
| Trust        | NPS score calculated from feedback                 |          8.2 |    >=8.5 | Converted from 👍/👎 ratio | CX Lead         | NPS sample too small, selection bias | Target survey to 100% of active users    |
| Value        | % feedback loop close time (AI fix after feedback) |      14 days | <=7 days | Ticket tracking            | Product Manager | Slow iteration due to manual review  | Auto-categorize feedback, weekly retrain |

## Part C — Dashboard Mock (6 tiles)

```text
┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 1: PRODUCT HEALTH             │ │ TILE 2: QUERY PROCESSING           │
│ Metric: Activation rate (cài + dùng)│ │ Metric: Query relevance score      │
│ Current: 85%  Target: 95%          │ │ Current: 74%  Target: 85%          │
│ Status: YELLOW                     │ │ Status: YELLOW                     │
│ Action if red: extend onboarding   │ │ Action if red: retrain embeddings  │
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 3: TIMESTAMP ACCURACY         │ │ TILE 4: USER SATISFACTION (NPS)    │
│ Metric: AI timestamp correctness    │ │ Metric: Net Promoter Score         │
│ Current: 91%  Target: 96%          │ │ Current: 8.2/10  Target: >=8.5     │
│ Status: YELLOW                     │ │ Status: GREEN                      │
│ Action if red: decrease confidence │ │ Action if red: analyze churn cohort│
│ threshold for showing timestamp    │ │                                    │
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 5: BUSINESS METRIC (CTR)      │ │ TILE 6: DECISION               │
│ Metric: Timestamp Click-Through     │ │ Continue / Pivot / Kill: CONTINUE  │
│ Current: 47%  Target: 55%          │ │ Top risk: Churn after exam season  │
│ Status: GREEN                      │ │ Top opportunity: Study group viral  │
│ Action if red: feature ranking fix │ │ Owner: Product Manager             │
└────────────────────────────────────┘ └────────────────────────────────────┘
```

## Part D — Memo Quyết định

```markdown
# Memo Quyết Định Cuối — Semantic Video Workspace (SVWorkspace)

## 1. Khuyến nghị: CONTINUE (với điều kiện gia hạn hook dài hạn)

Dữ liệu pilot 2 tuần mùa ôn thi cho thấy:

- CTR 47% (vượt target 40%): User tin tưởng AI timestamp accuracy
- NPS 8.2/10: Sẵn sàng giới thiệu cho bạn (strong signal)
- Churn 0/20: Không ai gỡ cài trong 2 tuần → product-market fit trong mùa thi
- LTV/CAC = 5.1x: Unit economics bền vững (mô hình B2C sustainable)

**Khuyến nghị:** Mở rộng sang 500 sinh viên tại 3 trường đại học VN (VinUni, HUST, Bách Khoa).

## 2. Chỉ số mạnh nhất để bảo vệ quyết định:

**Primary Metric:** Timestamp CTR ≥ 47%

- Vì nó trực tiếp chứng minh rằng AI semantic search đúng là cứu cánh cho bài toán "tìm kiếm trong video"
- Nó là hành động cụ thể (concrete action), không phải survey hoặc ước tính

**Secondary Metric:** NPS ≥ 8.0 + Monthly Retention Rate ≥ 40% sau mùa thi

- Tại sao cần: CTR cao trong mùa thi không đủ — cần biết user có giữ lại extension ko sau thi xong
- Retention 40% trong tháng post-thi là dấu hiệu họ sẽ dùng lại kỳ thi tới (6 tháng sau)

**Tertiary Metric:** Timestamp Accuracy ≥ 91%

- Vì khi CTR cao nhưng accuracy thấp → user sẽ mất niềm tin nhanh chóng

## 3. Chỉ số / giả định sẽ sửa từ v1 sang v2:

| #   | V1 có vấn đề gì?            | V2 sửa thành gì?                                | Vì sao sửa này tốt hơn?                    |
| --- | --------------------------- | ----------------------------------------------- | ------------------------------------------ |
| 1   | Activation đo bằng % cài    | Đo % cài + dùng >= 1 lần/ngày trong tuần 1      | Cài mà không dùng không có ý nghĩa         |
| 2   | CTR cao nhưng chưa test NPS | Thêm Monthly Retention sau thi xong             | CTR chỉ đúng với mùa thi; cần hook lâu dài |
| 3   | Chưa có decision gate       | Thêm guardrail: nếu Accuracy <85% → pause scale | Timestamp sai quá nhiều sẽ destroy trust   |

## 4. Trước khi scale từ 20 → 500, phải:

| #   | Hành động                                                                            | Chủ trì         | Deadline  | Thất bại nếu                              |
| --- | ------------------------------------------------------------------------------------ | --------------- | --------- | ----------------------------------------- |
| 1   | Chuẩn hóa test case cho timestamp accuracy QA (50 queries từ các môn học khác nhau)  | QA Lead         | T+7 ngày  | Accuracy dưới 85%                         |
| 2   | Deploy version 2 với Monthly Retention hook (quiz recommendation email)              | Engineer        | T+14 ngày | Churn tháng sau thi >60%                  |
| 3   | Setup decision gate hàng tuần: nếu CTR <40% hoặc NPS <7.5 thì dừng recruit sinh viên | Product Manager | T+3 ngày  | Không đặt guardrail → scale sai hướng     |
| 4   | Test LMS compatibility (Canvas, Blackboard, VLO, YouTube) trên tất cả 3 trường       | Engineer        | T+10 ngày | Extension bị block hoặc sai UI ở trường A |

## 5. Theo kỳ vọng sẽ cần tối ưu ở v3 (sau scale 500):

- **CTR sẽ giảm** (từ 47% → ~30-35%) vì cohort bổ sung sẽ có kỹ năng tìm kiếm kém hơn → cần cải thiện UX tìm kiếm
- **Timestamp accuracy sẽ bị challenge** bởi video từ các trường/máy quay khác nhau (audio quality thấp) → cần multiple model ensemble
- **Churn sẽ tăng sau 1 tháng** từ 0% → ~5-8% do mùa thi kết thúc → cần tính toán monetization strategy (freemium → paid)
```

## 6. Red-team và sửa v2

### Nhóm mình đi red-team

| Vai red-team   | Nhóm bị phản biện | 3 câu hỏi / rủi ro nêu                                                                                                                                                                                       |
| -------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CFO / Investor | Nhóm SVWorkspace  | 1) CTR 47% cao nhưng chỉ là mùa thi — churn sẽ tăng thế nào sau mùa thi xong? 2) Unit economics LTV/CAC có duy trì nếu churn tăng lên 30%? 3) Competitive risk: Google sẽ copy idea này trong 3 tháng không? |

### Nhóm bị red-team - Cách phòng thủ

| Red-team risk | Metric / giả định bị chất vấn                    | Sửa gì ở v2?                                                                                |
| ------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------- |
| 1             | CTR 47% nhưng chỉ trong 2 tuần mùa thi           | Thêm Monthly Retention KPI (target: >=40% post-exam); nếu churn 50% → adjust business model |
| 2             | LTV/CAC 5.1x ước tính từ pilot, chưa thực tế     | Chạy paid conversion test với 50 users; định giá 2.5 USD/tháng thay vì 5 USD                |
| 3             | Timestamp accuracy 91% có thể sai do sample bias | Expand QA dataset: 500 queries từ 10 môn học khác nhau, kiểm tra blind peer-review          |
| 4             | Không mention competitive threat                 | Research: Notion AI, Adobe Firefly, Microsoft Copilot có timestamp feature không?           |

### Ít nhất 2 thay đổi cụ thể từ v1 sang v2

| #   | V1 có vấn đề gì?                                    | V2 sửa thành gì?                                      | Vì sao sửa này tốt hơn?                             |
| --- | --------------------------------------------------- | ----------------------------------------------------- | --------------------------------------------------- |
| 1   | Activation đo bằng % cài (không chứng minh sử dụng) | Đo % cài + dùng >= 1 query/ngày trong tuần 1          | Cài mà không dùng không prove adoption              |
| 2   | CTR cao nhưng không track retention after exam      | Thêm Monthly Retention + NPS post-exam                | Mùa thi kết thúc → user sẽ gỡ cài nếu không có hook |
| 3   | Timestamp accuracy đo qua survey self-report        | Blind peer-review QA: 500 random queries x 3 reviewer | Avoid rater bias                                    |

## 7. Checklist trước khi nộp

- [x] Có 1 product cụ thể, không chọn "AI cho cả công ty" → SVWorkspace (Chrome Extension) cho sinh viên
- [x] Có 3 workflow chính (Query Processing, Timestamp Extraction, Feedback Collection)
- [x] Mỗi workflow có vai trò AI, human review (QA) và failure path (error handling)
- [x] Có rào cản ADKAR chính → Reinforcement (churn sau mùa thi)
- [x] Dashboard có metric toàn product (3 metrics) và metric theo workflow (18 rows)
- [x] Không chỉ đo vanity metric → CTR + NPS + Accuracy (outcome + trust)
- [x] Có baseline, target, data source và owner cho các metric chính
- [x] Có metric Quality (Timestamp Accuracy), Trust (NPS + Retention), Value (CTR + LTV/CAC)
- [x] Có Red-team risk và Fix (4 risks identified + mitigation)
- [x] Có 3 thay đổi rõ từ v1 sang v2 (Activation, CTR+Retention, QA accuracy rigor)
- [x] Decision Memo có continue/pivot/kill → CONTINUE với guardrail (Retention + Accuracy)
