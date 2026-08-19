# Reflection — Lab 19

**Tên:** Xuân Thế Độ
**Cohort:** AI20-K3
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên 50 golden queries, hybrid có Precision@10 trung bình cao nhất (78,6%),
nhỉnh hơn BM25 (77,8%) và vector (73,2%). Với `exact`, BM25 và hybrid cùng
đạt 96,7% vì thuật ngữ xuất hiện nguyên văn. Với `mixed`, hybrid đạt 100%, cao
hơn BM25 97,0% và vector 98,5%, vì RRF kết hợp được cả tín hiệu từ khóa lẫn ngữ
nghĩa. Riêng `paraphrase`, BM25 đạt 33,3%, hybrid 32,0% và vector 24,0%: model
lite `bge-small-en-v1.5` thiên về tiếng Anh nên biểu diễn paraphrase tiếng Việt
chưa tốt; đây là lý do nên thử `bge-m3` trước khi triển khai đa ngữ.

Tôi không dùng hybrid khi truy vấn là mã lỗi, ID hay thuật ngữ exact ổn định:
BM25 rẻ, nhanh và dễ giải thích hơn. Tôi chọn pure vector khi người dùng diễn
đạt tự do, corpus đa ngữ và embedding đã được đánh giá tốt. Hybrid phù hợp làm
mặc định khi traffic chứa nhiều kiểu query và mức tăng recall đáng giá hơn chi
phí chạy hai retriever.

---

## Điều ngạc nhiên nhất khi làm lab này

Model embedding phù hợp ngôn ngữ quan trọng hơn kỳ vọng: vector search không tự
động thắng paraphrase nếu model nền không mạnh cho tiếng Việt.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
