# Eval Loop — test → đánh giá → sửa (theo skill-creator Anthropic)

Vòng lặp này là trái tim của skill-creator chính thức. Đừng viết skill rồi "tin là chạy" — phải TEST bằng agent thật.

## Vòng lặp

```
Viết draft
   ↓
Tạo test prompts (3-10 câu giả lập user thật)
   ↓
Chạy agent con với skill (forward-test)  ← KHÔNG lộ đáp án/bài học
   ↓
Đánh giá: qualitative (đọc output) + quantitative (đo được không?)
   ↓
Sửa skill theo phản hồi
   ↓
Lặp tới khi pass
   ↓
Mở rộng test set → chạy quy mô lớn hơn
```

## Quy tắc forward-test (quan trọng — đừng làm hỏng)

- **Không cho agent test biết mình đang test skill**: prompt phải giống user thật yêu cầu công việc, ví dụ "Dùng skill X tại path Y giải quyết vấn đề Z" — KHÔNG phải "đánh giá skill X có tốt không"
- **Không lộ đáp án / ý định sửa**: đưa artifact thô (prompt, file, log), không đưa kết luận
- **Fresh thread cho mỗi lần pass** — không để agent test "nhớ" bài trước
- **Dọn artifact giữa các lần** — agent test không được đọc output của lần trước (contamination)
- **Forward-test thất bại mà chỉ pass khi có leaked context = skill chưa đủ**, tighten lại

## Demo THẬT ≠ forward-test (2.2.0)

Forward-test là demo **GIẢ LẬP** (agent test + prompt tự nghĩ) — không thay demo thật (user dùng skill vào việc thật). Sau handoff verify (3 dòng), user dùng thật → phản hồi lộ ra biến số mới (license, ngôn ngữ, môi trường máy) → **GHI NGƯỢC vào `6-observed-variables.md`** + thêm Bẫy/câu hỏi vào SKILL.md skill đó — vòng lặp khép kín, lần build sau đọc trước khi scan (Trụ 12 Bước 0).

## Đánh giá

- **Qualitative**: output có đúng format, đúng luồng, đúng giọng điệu?
- **Quantitative** (nếu output khách quan): đếm được — số file tạo, độ dài, pass/fail test, token dùng
- Kết hợp 2 loại — đừng chỉ "nhìn thấy ổn"

## Description improver

Sau khi skill hoạt động, tối ưu `description` để trigger chính xác:
- Chống **undertrigger**: Claude có xu hướng không bật skill dù cần → viết description "pushy", liệt kê cả câu chữ user hay dùng
- Test: đưa description mới cho agent mới → xem có tự bật skill với các prompt biên không

## Khi nào cần test

- Output khách quan (transform file, extract data, code, quy trình cố định) → **CẦN test case**
- Output chủ quan (viết văn, nghệ thuật) → test nhẹ hoặc không, dựa cảm nhận user

## Definition of Done — "pass" định nghĩa TRƯỚC

Chạy `python3 eval-skill.py <skill-dir> --verify` để tổng kết. Pass khi:
- Case chính + sai + nhanh: PASS 100%
- Case biên (trigger): PASS ≥ 80% — fail biên = description chưa "pushy", sửa description không sửa body
- Regression: pass-rate run mới KHÔNG giảm so với run trước (so 2 bản eval-results.json)
- Mọi case có verdict + evidence — không để PENDING, case không khai rubric = chưa hợp lệ

## Trigger rate — đo undertrigger bằng số

```
trigger rate = số case biên agent TỰ bật skill / tổng case biên
```

- Mục tiêu ≥ 80% · < 50% = description hỏng — ưu tiên sửa description trước
- A/B: chạy test set biên với description cũ → sửa → chạy lại → so sánh % (ghi vào record)

## Handoff verify — bàn giao cho user

Skill không thay thế test trên máy thật. Sau khi pass eval, gửi user 3 dòng:
1. Skill `<tên>` đã pass eval — chạy thử: `<lệnh thật>`
2. Kỳ vọng: `<output đúng — 1 dòng>`
3. Verify trên môi trường thật rồi báo lại

## Bẫy vận hành — chạy ĐỘI agent bị treo UI (đã vấp 2026-08-20)

Triệu chứng: spawn 4-10 agent song song → TUI đứng cứng, Enter không ăn, phải mở terminal mới. Nguyên nhân: output agent con đổ vào context (phình nhanh) + spawn lồng nhau + context gần giới hạn.

Luật chạy đội an toàn (batch 2 + ghi file + compact):
1. **Tối đa 2 agent mỗi lượt** — không 4-10 song song
2. **Agent con GHI KẾT QUẢ GỌN vào file .md đánh số** (vd research/1-market-a.md, 1-market-b.md) — không trả nguyên bản qua agent_result; agent mẹ chỉ đọc file
3. **Nối tiếp đến hết** — lượt 1 (agent 1-2) → lượt 2 (agent 3-4) → ... mỗi lượt 1 file
4. **Cấm spawn lồng nhau** — agent con không được gọi agent cháu
5. **/compact trước mỗi lượt nếu context >60%** — giải phóng trước khi đổ output mới
6. Tổng hợp CUỐI từ các file trên disk — không tổng hợp từ trí nhớ

Khớp với numbered-output.md: bộ file 0→n chính là nơi agent con ghi — state-on-disk, máy kiểm tra được, 10 chuyên gia = 5 lượt × 2 agent.
