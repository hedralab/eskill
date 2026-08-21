# eSkill — Meta-skill: tạo Agent Skill chuẩn top-1

eSkill là **skill để tạo skill** — quy trình sản xuất được chưng cất từ
[spec chính thức Agent Skills](https://agentskills.io/specification), vòng eval của Anthropic
[skill-creator](https://github.com/anthropics/skills), và kinh nghiệm thực chiến build/ship
egram + dự án eSeed.

## Tính năng

- **Quy trình 12 trụ**: Core (spec agentskills.io) · UX (Apple HIG) · Validation · Docs & Bẫy ·
  Vận hành (12-Factor) · Eval (skill-creator) · Nội dung (Apple Writing) · Tăng trưởng (AARRR) ·
  Thương mại · Tư vấn (SPIN + Mom Test) · Thị trường (JTBD) ·
  **Simulation & Variable Scan** (đặt vị thế người dùng → mô phỏng 5 kịch bản →
  quét 6 nhóm biến số trước khi viết)
- **Workflow bộ file 0→n**: mỗi lần build sinh 0-goal → 1-market → 2-plan → 3-SKILL.md →
  4-eval → 5-check → 6-observed-variables + docs/ — state trên disk, duyệt từng lớp
- **Quy tắc spec**: frontmatter (name/description/license/compatibility/metadata),
  progressive disclosure (<500 dòng), refs 1 cấp
- **Eval loop**: forward-test bằng prompt giả lập user thật, đánh giá định tính + định lượng
- **Đặt tên** (e-family kiểu Apple: `e` + 1 từ chính — eSkill, eSeed, egram)
- **Validator**: `scripts/validate-skill.py` — bắt frontmatter hỏng, tên sai, refs vỡ,
  SKILL.md quá dài, và rò rỉ (`--leak --brand`)

## Quickstart (3 câu)

1. `Tạo một skill để <việc X> và kiểm tra nó chạy được` — eSkill hỏi ít câu rồi build
2. `Cải thiện skill này: <đường dẫn>` — eSkill áp eval loop và sửa
3. `Validate skill này: <đường dẫn> [--leak]` — chạy validator

## Cấu trúc

```
eskill/
├── SKILL.md                     # quy trình 12 trụ + quy tắc vàng (tiếng Việt)
├── README.md                    # file này
├── LICENSE                      # Use-Only (chỉ cho dùng — tiếng Việt)
├── RELEASE-NOTES.md             # changelog (Keep a Changelog + semver)
├── .version-bump.json           # version hiện tại + danh sách file đồng bộ khi bump
├── CODE_OF_CONDUCT.md           # quy tắc ứng xử
├── .gitignore · .pre-commit-config.yaml
├── agents/openai.yaml           # metadata marketplace/UI
├── .claude-plugin/ · .codex-plugin/ · .cursor-plugin/   # manifest plugin
├── .github/                     # FUNDING + issue templates
├── assets/                      # icon
├── template/SKILL.md            # khung SKILL.md copy dùng ngay (frontmatter đủ field)
├── references/
│   ├── spec-rules.md            # quy tắc spec agentskills.io
│   ├── naming.md                # đặt tên e-family kiểu Apple
│   ├── sales-discovery.md       # SPIN + Mom Test (phỏng vấn bước 0)
│   ├── top1-benchmark.md        # Trụ 2: tìm + verify kim chỉ nam top-1
│   ├── simulation-variables.md  # Trụ 12: mô phỏng + quét biến số
│   ├── numbered-output.md       # workflow bộ file 0→n + docs/ (state trên disk)
│   ├── eval-loop.md             # vòng test → đánh giá → sửa
│   ├── test-prompts-template.md # 5 kiểu test prompt
│   ├── rubric.md                # tiêu chí pass/fail đăng ký trước
│   ├── docs-driven.md           # docs = HARD GATE 100%
│   ├── 12-factor-skills.md      # vận hành skill bền
│   ├── apple-writing.md         # viết SKILL.md ngắn gọn
│   ├── openai-yaml.md           # hướng dẫn agents/openai.yaml
│   ├── checklist-thuong-mai.md  # checklist thương mại + an toàn
│   ├── market-research.md       # Trụ 11: research trước build
│   └── ban-tren-github.md       # Trụ 9: funnel bán — thực thi gọi ehub/egram
├── examples/echeck/             # skill mẫu hoàn chỉnh
└── scripts/
    ├── validate-skill.py        # validator: --leak --brand "a,b"
    └── eval-skill.py            # eval harness: test set + --verify
```

## Release

Version: `2.4.0` — xem [RELEASE-NOTES.md](RELEASE-NOTES.md).
Quy trình: sửa xong → bump `.version-bump.json` → cập nhật RELEASE-NOTES → `gh release create vX.Y.Z`
(chi tiết: `references/ban-tren-github.md`).

## Cài đặt

Khuyên dùng — 1 lệnh qua [skills.sh](https://skills.sh):

```bash
npx skills add hedralab/eskill
```

Claude Code — plugin marketplace:

```
/plugin marketplace add hedralab/eskill
/plugin install eskill
```

Cài tay — copy thư mục vào thư mục skills của agent:

```bash
cp -RL eskill ~/.deepseek/skills/eskill    # DeepSeek TUI (giải symlink)
# or ~/.claude/skills/eskill
# or ~/.codex/skills/eskill
```

**⚠️ Symlink:** trong repo này `skills/eskill` là symlink → `~/.deepseek/.agents/skills/eskill`.
Khi copy/đóng gói, dùng `cp -RL` (hoặc `tar -h`) để giải symlink — `cp -R` thường copy symlink
trần, gói sang máy khác bị vỡ.

## Giấy phép

**Use-Only (chỉ cho dùng).** Xem [LICENSE](LICENSE). Được DÙNG skill này cho mục đích cá nhân
hoặc nội bộ. Sửa đổi, chia sẻ, và dùng thương mại KHÔNG được phép; mọi quyền khác giữ nguyên.
