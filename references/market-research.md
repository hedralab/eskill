# Market Research — Trụ 11: research TRƯỚC, build SAU (top-1: JTBD + Mom Test + Demand Validation)

Lỗi kinh điển: build skill xong mới hỏi có ai cần không. Trụ 11 đảo ngược: nghiên cứu trước, build sau. Bằng chứng 2026-08: top-1 skill thế giới = obra/superpowers (274K ⭐) và mattpocock/skills (223K ⭐) — cả hai bắt đầu từ nỗi đau của CHÍNH TÁC GIẢ, không phải đoán thị trường.

## 1. Năm nỗi đau người dùng phổ biến nhất (research Reddit/HN/PromptBase 2026-08)

1. **Skill bị model bỏ qua** — skill chỉ advisory, model không tự gọi → mất niềm tin. Fix: description trigger mạnh + script deterministic + test thật skill có được gọi không.
2. **Nhầm lẫn khái niệm** — skills vs MCP vs subagents vs commands vs plugins. Fix: SKILL.md nêu rõ khi nào dùng / khi nào KHÔNG (mục Giới hạn).
3. **Hoài nghi chỉ là markdown** — Fix: bằng chứng chạy thật (eval-results.json, smoke test). Điểm eskill ĐÃ có.
4. **Decay** — skill cũ, docs lỗi thời. Fix: version + RELEASE-NOTES + cập nhật định kỳ.
5. **Bảo mật** — skill = script thực thi, sợ RCE / prompt injection. Fix: code review sạch, tối giản quyền, mục an toàn khi cài.

## 2. Kênh phân phối ngoài GitHub (research 2026-08 — có bằng chứng)

- **PromptBase** — kênh DUY NHẤT bán skill.md end-to-end hiện tại: 450K+ users, 2,200+ sellers, 20% phí chợ / 0% link riêng, thanh toán Stripe
- **skills.sh (Vercel)** — discovery + cài 1 lệnh: 8,420 skill, 1.26M installs all-time, miễn phí
- **Claude Code / Codex / Cursor marketplace** — native-install; Codex qua review OpenAI, Cursor bắt buộc open-source, Claude mở marketplace.json không phí
- **Gumroad** — storefront tự bán: 10% + $0.50 (30% nếu qua Discover)
- **Telegram Stars** — bán trong bot: 400M+ user bot/tháng
- **MCP directories (mcp.so / Glama / Arcade.dev)** — cho MCP server, mcp.so có paid placement

Kết luận: GitHub = trust + discovery. PromptBase = kênh bán duy nhất. Gumroad = bán trực tiếp khi có traffic. KHÔNG bán được ngay trên GitHub (không có cổng thanh toán).

## 3. Top-1 làm gì đúng (benchmark obra/superpowers + mattpocock/skills)

1. Skill QUY TRÌNH có ý kiến — không phải reference docs
2. Cài 1 lệnh qua official plugin marketplace
3. Dual install: subscribe (tự cập nhật) hoặc fork (kiểm soát)
4. Tác giả tự dùng hằng ngày (eat own dogfood)
5. Bắt đầu từ nỗi đau cá nhân thật
6. Cộng đồng + newsletter (mattpocock ~60K subscribers)
7. Repo sống: cập nhật liên tục
8. README kể chuyện, positioning rõ: cho ai, giải quyết gì
9. Enterprise path rõ ràng (obra: email sales)
10. Registry-level distribution (skills.sh)

5 GAP mọi ông lớn bỏ lỡ — chỗ skill mới ăn điểm:
1. Không có install-time security verification (NVIDIA SkillSpector tồn tại nhưng ngoài luồng)
2. Không có per-skill semver + changelog
3. Không có usage telemetry (obra tự thú: không biết bao nhiêu người dùng)
4. Không có skill-quality benchmark chung
5. Không có paid distribution tích hợp vào install UX

## 4. Pricing benchmark (research 2026)

- Prompt lẻ: $5-15 · Bundle hệ thống (prompt + workflow + template): $29-69 · Membership: $9-19/tháng
- Người mua trả tiền cho BUNDLE giải quyết 1 nỗi đau — không trả cho prompt lẻ
- Thu nhập thực: beginner $100-500/tháng · niche + direct + subscription: $2K-15K/tháng
- Margin: direct ~3% phí xử lý vs PromptBase 20% vs Gumroad 10%+$0.50

## 5. Demand validation — 5 cách có bằng chứng

1. Founder-pain test: chính tôi có dùng nó hằng tuần không? (PromptBase, superpowers đều từ đây)
2. Pre-sale: bán trước khi build — có người trả tiền = demand thật (Marc Lou pattern)
3. Signal scan: Reddit/HN/search — người ta có đang đau vì vấn đề này?
4. Mom Test: hỏi CUỘC SỐNG, không hỏi anh có cần không (chi tiết: sales-discovery.md)
5. Waitlist / landing page: đo conversion trước khi tốn công build

## Checklist nghiên cứu thị trường (trước khi build skill BÁN)

- [ ] 1 câu: người mua DUY NHẤT + nỗi đau cụ thể của họ
- [ ] Founder-pain test: chính mình dùng hằng tuần không?
- [ ] Scan 3 nơi: Reddit/HN + skills.sh + PromptBase — đã có skill nào chưa, gap gì
- [ ] Benchmark 2 skill top cùng chủ đề — học điểm mạnh, né điểm yếu
- [ ] Định giá theo bundle ($29-69), không theo prompt lẻ ($5)
- [ ] Chọn kênh ≥2: GitHub (trust) + PromptBase (bán) + Gumroad (direct)
- [ ] Demand test tối thiểu TRƯỚC khi build 200 dòng
- [ ] Kế hoạch cập nhật (version + changelog) từ ngày đầu
