# 04 — Reflection (Cá nhân)

---

## 1 metric hoặc 1 giả định tôi sẽ sửa

**Metric tôi muốn sửa:** Timestamp Click-Through Rate (CTR)

Trong dashboard v1, tôi dùng **Timestamp CTR (47%)** là primary metric để đưa ra quyết định **CONTINUE** cho SVWorkspace. Tuy nhiên, sau khi nghe red-team và nhìn lại, tôi nhận ra CTR là metric đúng nhưng **chưa đủ** — vì nó chỉ đo _hành động trong phiên_ (intra-session behavior), không đo _giá trị học tập thực sự_ mà người dùng nhận được.

Vấn đề cụ thể: Một sinh viên có thể click timestamp 10 lần trong một buổi nhưng không hiểu thêm được gì — chỉ vì giao diện trông hấp dẫn. CTR cao không tự động chứng minh **learning outcome** đã cải thiện.

Ở v2, tôi sẽ **ghép CTR với một learning proxy metric**: ví dụ tỷ lệ sinh viên trả lời đúng câu hỏi ôn tập sau khi dùng extension, hoặc thời gian ôn lại cùng một khái niệm giảm qua các lần. Chỉ khi CTR đi cùng learning signal thực sự thì mới nên dùng để scale.

Bài học: **Outcome metric quan trọng hơn engagement metric** — dù engagement dễ đo hơn.
