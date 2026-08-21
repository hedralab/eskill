# Numbered Output — bộ file 0→n (học egram): TỰ ĐỘNG sinh, ghi ngay, duyệt từng lớp

Pattern gốc từ egram: agent TỰ TẠO bộ file đánh số trong thư mục dự án (0-logic → 1-menu → ... → 5-month) rồi làm việc theo từng lớp — mỗi file 1 lớp, user duyệt + fix xong mới sang lớp sau. Kết quả: dễ dùng, không mất state, máy kiểm tra được.

## BẮT BUỘC — agent TỰ sinh, không chờ user hỏi

Ngay khi bắt đầu làm việc với bất kỳ dự án nào (skill / bot / tool / repo / research), agent TỰ TẠO bộ file đánh số 0→n trong thư mục làm việc — skeleton trước, điền dần theo kết quả từng bước. KHÔNG chờ user yêu cầu.

## Pipeline skill bán (eskill)

- 0-goal.txt — GỐC: câu trả lời BƯỚC 0 (SPIN + Mom Test). Ghi NGAY từng câu khi user trả lời.
- 1-market.txt — Trụ 11: người mua + nỗi đau + đối thủ + giá (research 1 trang)
- 2-plan.txt — Section 7: kết luận 1 trang (ANSWER → SCQA → MECE → rủi ro → **biến số đã quét Trụ 12 — BẮT BUỘC dòng `VÒNG ĐỜI: semver=…, changelog=…`** → next actions)
- 3-SKILL.md — draft theo spec (frontmatter, <500 dòng, refs 1 cấp)
- 4-eval.md — 5 test prompt + rubric TRƯỚC khi chạy eval
- 5-check.md — checklist thương mại (leak scan, LICENSE, README đồng bộ)
- 6-observed-variables.md — vòng lặp khép kín (2.2.0): biến số lộ ra khi DÙNG THẬT — format: `## [ngày] [skill] [biến số] — nhóm` + triệu chứng + quy tắc/Bẫy đã thêm + câu hỏi bắt buộc khi build

## Dự án KHÔNG phải skill — cùng nguyên tắc, file theo dự án

Bộ file cụ thể tùy loại dự án, GIỮ NGUYÊN nguyên tắc: 0 = GỐC (ý user) · số tăng = thứ tự build · mỗi file 1 lớp · duyệt tuần tự từng cái.

- Bot Telegram (egram): 0-logic.txt (bản chất bot) → 1-menu.txt → 2-seed.txt (tin realtime) → 3-daily.txt → 4-week.txt → 5-month.txt
- Tool/script: 0-goal.txt → 1-plan.txt → 2-logic.txt → 3-code.py → 4-test.txt → 5-run.txt
- Repo/website: 0-goal.txt → 1-structure.txt → 2-content.txt → 3-design.txt → 4-build.txt → 5-check.txt

Nếu chưa rõ bộ file nào phù hợp: hỏi user 1 câu ("dự án này có mấy lớp chính?") hoặc tự đề xuất bộ 0→n rồi trình để user duyệt.

## docs/ — tủ tài liệu dự án (sinh kèm bộ file)

Mỗi dự án có thêm thư mục `docs/` bên cạnh bộ file 0→n — lưu tài liệu dùng lại được:

- `docs/requirement.md` — yêu cầu đã chốt với user (không phải suy diễn)
- `docs/decisions.md` — quyết định + lý do (ADR 1 dòng/cái)
- `docs/api-<tên>.md` — API/service docs đã fetch (docs-driven HARD GATE — `references/docs-driven.md`)
- `docs/benchmark-<mảng>.md` — kim chỉ nam top-1 đã verify (`references/top1-benchmark.md`)
- `docs/log.md` — nhật ký build (bước nào xong, ai duyệt gì)

Máy kiểm tra được: build tiếp mà thiếu docs nào thì bổ sung trước.

## 6 quy tắc

1. Sinh skeleton NGAY khi bắt đầu — trước khi hỏi/hành động; ghi câu trả lời user vào file 0 NGAY khi nhận, không giữ trong hội thoại (state trên disk, restart/compact không mất)
2. File sau phụ thuộc file trước — duyệt TỪNG LỚP: user fix file 0 → điều chỉnh các lớp sau
3. Skeleton trước, điền dần — sinh khung ngay, điền theo kết quả từng bước
4. Số thứ tự = thứ tự build = thứ tự duyệt — user không cần hỏi tiếp theo làm gì
5. Mỗi dự án 1 bộ file RIÊNG, độc lập — không mở/copy bộ file dự án khác
6. Máy kiểm tra được: đủ file? thiếu file nào? nội dung từng file có đúng lớp không? — quy trình thành checklist chạy được

## Code mẫu (khởi tạo bộ file — chạy ngay ở bước đầu)

```bash
mkdir -p docs
# skill bán:
touch 0-goal.txt 1-market.txt 2-plan.txt 3-SKILL.md 4-eval.md 5-check.md
# dự án khác: đặt tên theo bộ file đã chốt, vd bot:
touch 0-logic.txt 1-menu.txt 2-seed.txt 3-daily.txt 4-week.txt 5-month.txt
```

## Ví dụ nội dung 0-goal.txt (ghi khi user trả lời, 1 câu/câu)

```
# Mục tiêu
- Bot/skill làm gì: ...
- Ai dùng: ...
- Vị thế người đăng/dùng (bán / portfolio / dev / nội bộ): ...
- Nỗi đau đang giải quyết: ...
```

## Checklist trước khi build

- [ ] Bộ file 0→n đã sinh trong thư mục dự án (skeleton) — KHÔNG đợi user hỏi
- [ ] 0-goal.txt có câu trả lời THẬT của user (không phải suy diễn model)
- [ ] (skill bán) 1-market.txt đủ: người mua + nỗi đau + 2 đối thủ + giá
- [ ] (skill bán) 2-plan.txt 1 trang: ANSWER đầu tiên + MECE + rủi ro + next actions
- [ ] (skill bán) 3-SKILL.md draft xong → validate PASS
- [ ] (skill bán) 4-eval.md có 5 test prompt + rubric
- [ ] (skill bán) 5-check.md: leak scan + LICENSE + README đồng bộ
- [ ] docs/ có requirement + decisions (tối thiểu) — API docs nếu có
- [ ] Mỗi lớp user duyệt xong mới sang lớp sau
