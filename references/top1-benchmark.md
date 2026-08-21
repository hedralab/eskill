# Top-1 Benchmark — tìm + verify + lưu kim chỉ nam (Trụ 2)

Mỗi mảng lớn của skill = 1 chuẩn ĐÃ CHỨNG MINH (kim chỉ nam), không viết theo ý kiến model. Reference này là quy trình tìm ra chuẩn đó: tiêu chí → tìm ứng viên → verify → lưu.

## Vì sao

Skill viết theo "cảm giác đúng" = skill mơ hồ, agent làm theo kiến thức chung. Skill viết theo 1 chuẩn top-1 = agent có cột mốc rõ ràng, output đạt chuẩn ngành. Ví dụ egram: BotFather (core) · Apple HIG (UX) · Stripe (bảo mật) · 12-Factor (vận hành) · GitHub Actions (realtime) · Apple Writing (nội dung) · AARRR (growth) · OKX (báo cáo/PnL).

## Quy trình 4 bước

1. **Định nghĩa tiêu chí top-1** cho mảng đang build (vd mảng "chuẩn UI" → tiêu chí: có spec chính thức, ngành công nhận, tài liệu đầy đủ, có ví dụ thực tế)
2. **Tìm ứng viên** — ít nhất 3 nguồn, không chỉ 1:
   - Docs chính thức của nền tảng/ngành (stripe.com/docs, core.telegram.org, developers.facebook.com, apple.com/design...)
   - `gh search repos --sort stars` + bộ lọc ngôn ngữ/topic — repo được dùng nhiều nhất là tín hiệu adoption
   - Benchmark/tiêu chuẩn công bố (Google UX Playbook, Nielsen Norman, ISO, OWASP...)
   - Community consensus: subreddit/forum/issue nhiều vote, bài viết được trích dẫn rộng
3. **Verify trước khi tin** — 2 nguồn độc lập xác nhận:
   - Chuẩn được nhắc trong docs chính thức của nền tảng liên quan?
   - Số liệu adoption thật (stars, downloads, % dùng trong survey)?
   - Có ví dụ thực tế dùng chuẩn đó đạt kết quả tốt?
   - Cảnh báo: chuẩn "hot" trên mạng xã hội ≠ top-1 (viral ≠ đúng); model đề xuất ≠ đã chứng minh
4. **Lưu kết quả** — 2 nơi:
   - `references/benchmark-<mảng>.md` — 1 trang: tên chuẩn + vì sao top-1 (đạt tiêu chí nào) + URL nguồn + ngày verify
   - SKILL.md (mục tương ứng) — 1 dòng: "kim chỉ nam: X — xem references/benchmark-X.md"

## Checklist

- [ ] Mỗi mảng lớn đã có 1 kim chỉ nam rõ tên
- [ ] Ít nhất 3 ứng viên được cân nhắc (không chỉ docs của 1 nguồn)
- [ ] Verify ≥ 2 nguồn độc lập (docs chính thức + adoption thật)
- [ ] File `benchmark-<mảng>.md` có: tên + lý do + URL + ngày
- [ ] SKILL.md ghi 1 dòng kim chỉ nam mỗi mảng
