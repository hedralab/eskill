# Simulation & Variable Scan — logic gốc rễ (Trụ 12)

Trước khi build, ĐẶT VỊ THẾ người dùng → MÔ PHỎNG kịch bản → QUÉT MỌI BIẾN SỐ → rồi mới viết. Mục tiêu: skill tạo ra không sót biến số (học từ 2 bẫy thật khi build ehub 2026-08-21).

## Vì sao (2 bẫy đã vấp — ehub)

1. **Quên biến số vòng đời** — build xong mới phát hiện "đẩy lên GitHub cần quy tắc phiên bản" → phải bổ sung semver/changelog/release sau
2. **Quên biến số người đọc** — output (README/tin nhắn/báo cáo) viết thuần khô, người dùng không hiểu nổi giá trị → phải viết lại theo inside + bố trí

## Quy trình 5 bước (chạy TRƯỚC khi viết SKILL.md)

1. **Đặt vị thế người dùng** — persona + giai đoạn vòng đời: dùng lần đầu / hằng ngày / nâng cấp / ra mắt / gặp lỗi
2. **Mô phỏng 5 kịch bản** — chính (luồng chính) · biên (trigger/cạnh) · lỗi (error path) · vòng đời (update/version/release) · ra mắt (người đọc/output)
3. **Quét biến số 5 nhóm** (checklist dưới) — liệt kê HẾT, đừng dừng ở hiển nhiên
4. **Đối chiếu độ phủ** — biến số nào skill đã xử lý? chưa → thành mảng mới hoặc Bẫy trong SKILL.md
5. **Ghi vào 2-plan.txt** — biến số + cách xử lý, TRƯỚC khi viết draft

## Checklist biến số 6 nhóm

- **INPUT**: rỗng · sai format · ký tự đặc biệt/không dấu · kích thước tối đa · input lạ (file/URL/emoji)
- **LỖI**: mất mạng · auth/token chết · rate limit (429) · crash/exception · lỗi service thứ 3 · retry có giới hạn
- **VÒNG ĐỜI**: version bump (semver) · changelog (Keep a Changelog) · release/tag · backward-compat · deprecated
- **NGƯỜI ĐỌC (inside)**: hook 3 giây · lợi ích định lượng (Hopkins) · từ khóa họ tự tìm (SEO) · trình độ persona · bố trí F-pattern · screenshot/demo · CTA rõ ràng · layout khoa học (HIG)
- **MÔI TRƯỜNG**: OS (macOS/Linux/Windows) · python version · sandbox/quyền · dependency · idempotent chạy lại
- **QUY TRÌNH/CON NGƯỜI**: ai review · ai release/push · ai duyệt · quy trình cập nhật sau này (bẫy 1 ehub thực chất là lỗi QUY TRÌNH, không chỉ kỹ thuật)

## Khung kiểm tra output (template nào cũng qua trước khi chốt)

- Người đọc 10s hiểu được gì?
- Dòng đầu có hook đánh nỗi đau?
- Lợi ích có số cụ thể?
- Có screenshot/demo (nếu UI)?
- Từ khóa họ tìm có trong output?
- Có 1 hành động rõ ràng?
- Bố trí theo F-pattern, cấp tiêu đề rõ?
- Biến số vòng đời (version/release) đã có quy tắc?

## Ví dụ before/after (bẫy 2 — README khô → inside)

Before (khô): `# etax` + "Báo cáo thuế/PnL từ OKX." + mục Cách dùng trống — người đọc 10s không biết lợi ích gì.
After (inside): `# etax — Hoàn phí 20% OKX tự động mỗi lệnh` + `> Không cần mở web, không tính tay — số đúng từng ngày.` + mục "Vì sao etax?" (2-3 lợi ích có số) + 1 lệnh bắt đầu.
Đối chiếu: hook đầu · số cụ thể · ngôn ngữ người tìm ("hoàn phí OKX") · CTA rõ.

## Delivery — gọi skill cuối (có gate)

eskill BUILD skill, KHÔNG tự lo delivery. Muốn đẩy lên GitHub → gọi `ehub`; bot Telegram → `egram`. **Gate trước khi gọi ehub:** repo ĐÃ có CHANGELOG + version đồng bộ mọi file — chưa có thì bổ sung trước (handoff phải kiểm tra được, không vô điều kiện).
