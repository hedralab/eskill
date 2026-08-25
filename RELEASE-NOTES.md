# Release Notes — eSkill

Định dạng theo [Keep a Changelog](https://keepachangelog.com) — version semver, mỗi bản 1 mục.
Quy trình: sửa xong → bump `.version-bump.json` → cập nhật mục này → `gh release create vX.Y.Z`.

## [2.5.0] — 2026-08-25

### Added
- `references/cursor-skills.md` — kim chỉ nam Cursor Agent Skills (`create-skill`): chỗ cài `~/.cursor/skills` vs project `.cursor/skills`, **CẤM** `skills-cursor/`, description ngôi 3, `disable-model-invocation`, pin, checklist ship
- Trụ 1 + bước 3/6 SKILL.md: dual-spec agentskills.io **+** Cursor; template ghi chú `disable-model-invocation`

## [2.4.0] — 2026-08-21

### Added
- `6-observed-variables.md` — skill tự ghi bài học từ DÙNG THẬT (4 mục: license · ngôn ngữ · gh multi-account · rsync sync) — dogfood vòng lặp khép kín
- simulation-variables.md: **Quy tắc gốc "1 biến cho MỌI file"** (root variable) — 1 biến duy nhất + marker file + audit chéo (học từ ehub 1.5.0 --readme-lang + LANGUAGE.txt) — đơn giản hóa từ gốc, hết lẫn ngôn ngữ vĩnh viễn

## [2.3.0] — 2026-08-21

### Changed
- Repo chuyển **100% tiếng Việt** (tạm thời): README · LICENSE · CODE_OF_CONDUCT · agents/openai.yaml — hết lẫn EN/VN (quyết định của user 08-21: "cho nó khỏe")

## [2.2.1] — 2026-08-21

### Fixed
- CODE_OF_CONDUCT.md: tiếng Việt → tiếng Anh (đồng bộ ngôn ngữ public-facing: README EN · LICENSE EN · CoC EN) — vấp khi user check repo thật
- agents/openai.yaml: short_description + default_prompt → tiếng Anh (metadata hiển thị công khai)

## [2.2.0] — 2026-08-21

### Added
- Trụ 12 Bước 0 — vòng lặp khép kín "demo-driven variable capture": đọc `6-observed-variables.md` của skill cùng họ TRƯỚC khi scan (scan a-priori không bắt được biến số use-time: license, ngôn ngữ, môi trường máy)
- numbered-output: pipeline thêm `6-observed-variables.md` (sau 5-check) + format
- eval-loop: ghi rõ "Demo THẬT ≠ forward-test" — phản hồi dùng thật phải ghi ngược vào 6-observed (học từ thực tế: ehub vấp license/ngôn ngữ/gh multi-account khi DÙNG THẬT)

## [2.1.1] — 2026-08-21

### Removed
- .github/PULL_REQUEST_TEMPLATE.md — bỏ (mời PR = mời sửa code = vi phạm license Use-Only; audit đội chuyên gia 08-21)

### Fixed
- CODE_OF_CONDUCT.md: bỏ nhắc "commit, code, wiki edit" (ngụ ý đóng góp code) — Use-Only chỉ nhận phản hồi qua issue
- examples/echeck/SKILL.md: frontmatter license MIT → UseOnly (đồng bộ license repo)

## [2.1.0] — 2026-08-21

### Changed
- LICENSE: Non-Commercial → **Use-Only** (chỉ cho DÙNG — không sửa, không chia sẻ, không bán; mọi quyền khác giữ nguyên)
- README License section + tree: đồng bộ "Use-only"

## [2.0.0] — 2026-08-21

### Changed (breaking)
- LICENSE: MIT → **Non-Commercial** (custom) — dùng/sửa/chia sẻ miễn phí cho mục đích PHI THƯƠNG MẠI; bán/nhúng sản phẩm trả phí cần xin phép trước (MAJOR vì đổi điều khoản pháp lý)
- README: làm sạch 100% tiếng Anh (public-facing) — hết lẫn tiếng Việt ở Release/Install/tree comments

## [1.9.1] — 2026-08-21

### Fixed
- validate-skill.py: regex `name` trong frontmatter dùng `\s*` nuốt newline → `name:` rỗng bắt nhầm dòng `description` làm name (phát hiện bởi forward-test case 4); sửa dùng `[ \t]*` — value phải CÙNG DÒNG; thêm lỗi rõ ràng "frontmatter thiếu name (dòng 'name:' rỗng hoặc không có)"

## [1.9.0] — 2026-08-21

### Changed
- BƯỚC 0 tách 3 mục con (hỏi → sinh file 0→n → mô phỏng/quét biến số) — hết bullet 12 dòng chồng 7 chủ đề (audit đội chuyên gia 08-21)
- GỠ scripts/sell/ khỏi eskill (sales_bot.py · grant_access.sh · verify_payment.py · .env.mẫu) — mâu thuẫn routing "eskill không lo delivery"; archive cục bộ ngoài repo (không push)
- ban-tren-github.md: viết lại thành funnel tham khảo — thực thi delivery gọi ehub (repo/release) + egram (funnel Telegram)

### Added
- Trụ 12 nâng: nhóm biến số thứ 6 QUY TRÌNH/CON NGƯỜI + ví dụ before/after (README khô → inside) + gate trước khi gọi ehub (CHANGELOG + version đồng bộ)
- numbered-output.md: 2-plan.txt BẮT BUỘC dòng "VÒNG ĐỜI: semver=…, changelog=…"
- README: đồng bộ cây cấu trúc (4 references thiếu) + dòng Trụ 12

## [1.8.0] — 2026-08-21

### Changed
- BỎ phần GitHub khỏi eskill — eskill chỉ BUILD skill, không lo delivery; muốn đẩy lên GitHub → gọi skill cuối `ehub` (bot Telegram → `egram`)
- docs-driven.md: gỡ mục "Repo GitHub / push" (chuyển về ehub)

### Added
- Trụ 12 — Simulation & Variable Scan (references/simulation-variables.md): đặt vị thế người dùng → mô phỏng 5 kịch bản (chính/biên/lỗi/vòng đời/ra mắt) → quét 5 nhóm biến số (input/lỗi/vòng đời/người đọc/môi trường) → biến số chưa phủ thành mảng/Bẫy → rồi mới build
- BƯỚC 0: bước mô phỏng + quét biến số bắt buộc trước khi viết SKILL.md (học từ 2 bẫy: ehub quên versioning + README khô) + routing delivery sang skill cuối
- numbered-output.md: 2-plan.txt thêm biến số đã quét (Trụ 12)

## [1.7.0] — 2026-08-21

### Added
- docs-driven.md: mục "Repo GitHub / push" — docs/ bắt buộc có gh-cli.md + benchmark khi dự án đẩy lên GitHub (tham khảo ehub đã áp dụng)
- BƯỚC 0 + numbered-output.md: câu hỏi vị thế người đăng/dùng (bán / portfolio / dev / nội bộ) — README/đóng gói theo persona

## [1.6.0] — 2026-08-21

### Added
- references/top1-benchmark.md — quy trình tìm + verify + lưu kim chỉ nam top-1 (tiêu chí → 3+ ứng viên → verify 2 nguồn độc lập → benchmark file + SKILL.md 1 dòng)
- numbered-output.md: thêm docs/ — tủ tài liệu dự án (requirement, decisions, API docs, benchmark, log) sinh kèm bộ file 0→n

## [1.5.0] — 2026-08-21

### Added
- Workflow bộ file 0→n theo egram — BẮT BUỘC + TỰ ĐỘNG: agent sinh file đánh số ngay khi bắt đầu (0-goal → 1-market → 2-plan → 3-SKILL.md → 4-eval → 5-check), ghi câu trả lời user vào file NGAY khi nhận (state trên disk — restart/compact không mất), user duyệt từng lớp
- numbered-output.md: mở rộng áp dụng cho MỌI dự án (không chỉ skill bán) — ví dụ bộ file bot theo egram (0-logic → 5-month)

## [1.4.3] — 2026-08-20

### Fixed
- Chuyển quy tắc chạy đội agent (2/lượt) từ eval-loop.md lên SKILL.md Quy tắc vàng — luôn trong context khi skill kích hoạt, không phụ thuộc load reference

## [1.4.2] — 2026-08-20

### Added
- eval-loop.md: quy tắc chạy đội agent an toàn (batch 2 agent/lượt → ghi file md → compact → nối tiếp) — chống treo UI khi forward-test với nhiều agent

## [1.4.1] — 2026-08-20

### Updated
- market-research.md theo audit đội chuyên gia: thêm Google Trends/X/Product Hunt/newsletter · storefront thay thế (Lemon Squeezy/Paddle/Ko-fi/BMAC/AppSumo) · bỏ Telegram Stars + MCP dirs khỏi ưu tiên · fix mâu thuẫn funnel bán · quy tắc kèm URL nguồn

## [1.4.0] — 2026-08-20

### Added
- market-research.md Section 8: Nghiên cứu INSIGHT (JTBD + 5 Whys + behavioral observation + outcome-driven) — nỗi đau là triệu chứng, insight là gốc rễ

## [1.3.0] — 2026-08-19

### Added
- references/numbered-output.md: pattern file 0→n (học từ egram) — pipeline 0-goal → 1-market → 2-plan → 3-SKILL.md → 4-eval → 5-check
- Quy tắc vàng mới: ghi từng bước thành file đánh số

## [1.2.0] — 2026-08-19

### Added
- market-research.md Section 6: Post-launch measurement (skills.sh telemetry, GitHub API, kill/pivot/continue)
- market-research.md Section 7: Research → Plan (Minto Pyramid + SCQA + MECE + JTBD)

## [1.1.0] — 2026-08-19

### Added
- Trụ 11 — Market Research: `references/market-research.md` (nỗi đau người dùng, kênh phân phối ngoài GitHub, benchmark top-1, pricing, demand validation)
- BƯỚC 0 mở rộng: nghiên cứu thị trường trước khi build skill bán

## [1.0.0] — 2026-08-19

Bản đầu tiên đủ điều kiện bán. Eval chính thức: **4/5 PASS** + static PASS
(case lớn 3/5 — cần test phiên thật trước khi bán rộng, xem eval-results.json).

### Added
- Forward-test eval loop đầy đủ: 5 case (chính/biên/nhanh/sai/lớn), rubric pre-registered, evidence ghi trong `eval-results.json`
- Quy tắc mới từ eval (2 patch): BƯỚC 0 auto-mode ("không có user → tự quyết, TIẾN HÀNH") + Bước 3 create-first ("bắt tay tạo file NGAY, KHÔNG mở examples khi tạo mới — template là đủ")
- Đóng gói bán: `RELEASE-NOTES.md`, `.version-bump.json`, plugin manifests (Claude Code / Codex / Cursor), `.github/` templates + FUNDING, `CODE_OF_CONDUCT.md`, `.gitignore`, pre-commit, icon
- Version thống nhất semver `1.0.0` trên mọi file (SKILL.md metadata.version · eval-results.json · README · plugin.json · tag)

### Fixed
- README lệch SKILL.md (thiếu 4 references + eval-skill.py + examples/ trong cây cấu trúc)
- 3 file `.bak` còn sót trong gói
- BƯỚC 0 chặn agent chạy tự động (kẹt cứng chờ hỏi user không có)

## [Unreleased]
- Bản EN (bán quốc tế — spec + marketplace đều EN)
- Marketplace registration (skills.sh / plugin marketplace)
- Re-test case "lớn" trên phiên làm việc thật (có user tương tác, không phải sub-agent harness)
