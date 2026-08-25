# Cursor Agent Skills — kim chỉ nam vận hành trong Cursor

Nguồn: skill nội bộ Cursor `create-skill` + `migrate-to-skills` (`~/.cursor/skills-cursor/` — **chỉ đọc**, không ghi vào đó).

Dùng khi skill đích chạy trên **Cursor Agent** (personal `~/.cursor/skills` hoặc project `.cursor/skills`). Bổ sung agentskills.io — không thay thế.

## 1. Chỗ cài (bắt buộc đúng)

| Loại | Path | Phạm vi |
|---|---|---|
| **Personal** | `~/.cursor/skills/<name>/` | Mọi project trên máy |
| **Project** | `<repo>/.cursor/skills/<name>/` | Chỉ repo đó (commit cùng repo) |
| **CẤM** | `~/.cursor/skills-cursor/` | Reserved — Cursor built-in, hệ thống quản |

Canonical e-family: repo GitHub (vd `Projects/e-family/<skill>`) + **symlink** `~/.cursor/skills/<name> → repo` (như egram). Đừng copy 2 bản lệch nhau.

## 2. Description — discovery trong Cursor

Description được inject vào system prompt → agent **tự quyết** có đọc skill không.

1. **Ngôi thứ 3** — ✅ `Processes Excel…` · ❌ `I can help…` / `You can use…`
2. **WHAT + WHEN** trong ≤1024 ký tự + **trigger phrases** user hay gõ
3. Pushy vừa đủ (chống undertrigger) — không spam từ khóa rác
4. Ví dụ chuẩn Cursor:
   ```yaml
   description: Review code for quality and security following team standards. Use when reviewing pull requests, examining code changes, or when the user asks for a code review.
   ```

## 3. `disable-model-invocation`

| Giá trị | Khi nào |
|---|---|
| `true` (mặc định Cursor create-skill) | Skill chỉ khi user **gọi tên** / chỉ định rõ — tránh auto-load nặng |
| *omit* / không set | Agent **được phép** tự bật từ context (ambient) |

Quy tắc eskill:
- Skill **hiến pháp / trade / nguy hiểm** (ealpha, kill-switch) → cân nhắc auto (omit) **hoặc** pin project — đừng để im lặng khi user sửa bot live
- Skill **một lần / admin** (migrate, rename) → `disable-model-invocation: true`
- Skill **thường xuyên trong flow** (egram khi sửa Telegram) → omit + description pushy

## 4. Viết body cho Cursor (token = tiền)

- Agent đã thông minh — chỉ thêm kiến thức **nó không có** (domain, bẫy, SoT path, lệnh máy này)
- `SKILL.md` **< 500 dòng**; chi tiết → `references/` **1 cấp**
- Workflow có checklist copy được; ví dụ input→output cụ thể
- User đưa câu chữ verbatim → **giữ nguyên** trong skill, không paraphrase
- Có context hội thoại → **suy ra** skill, đừng hỏi lại đủ 6 câu nếu đã đủ

### Pattern Cursor khuyến nghị

| Pattern | Dùng khi |
|---|---|
| Template | Output format cố định (report, PR body) |
| Examples | Chất lượng phụ thuộc mẫu (commit message) |
| Workflow + checklist | Nhiều bước, cần track |
| Conditional workflow | Tạo mới vs sửa cũ |
| Feedback loop | Validate → sửa → validate lại (gate FAIL rõ) |

### Anti-pattern Cursor

- Path kiểu Windows `scripts\foo.py`
- Liệt kê 5 thư viện ngang hàng không default
- Thông tin theo ngày tháng sẽ chết → dùng mục "Current / Old (deprecated)"
- Tên skill mơ hồ: `helper`, `utils`, `tools`
- Ref lồng sâu `a → b → c` (Cursor có thể đọc thiếu)

## 5. Pin kích hoạt trên Cursor

1. **Personal skill** đã nằm `~/.cursor/skills/<name>` → hiện trong agent skills list
2. **Project skill** → `.cursor/skills/<name>` trong repo
3. **Luôn bật cứng** (hiến pháp project): rule `.cursor/rules/*.mdc` với `alwaysApply: true` nhắc "đọc skill X trước khi…" — hoặc pin trong instructions project
4. Migrate rule "Applied intelligently" (có description, không globs, không alwaysApply) → skill: xem `migrate-to-skills`

Không dựa một mình `.deepseek/instructions.md` nếu user chạy **Cursor** — phải có path Cursor ở trên.

## 6. Checklist ship skill cho Cursor

- [ ] `name` = tên thư mục; không ghi vào `skills-cursor/`
- [ ] `description` ngôi 3 · WHAT+WHEN · trigger
- [ ] Quyết định rõ: `disable-model-invocation` hay auto
- [ ] Body < 500 dòng · refs 1 cấp
- [ ] Personal symlink hoặc project path đã trỏ đúng repo GitHub
- [ ] Smoke: session mới → user nói câu trigger → agent **đọc** SKILL.md (không chỉ liệt kê)
- [ ] (Hiến pháp) pin rule/instructions Cursor nếu undertrigger nguy hiểm

## 7. Khác agentskills.io / Claude Code

| | agentskills.io | Cursor |
|---|---|---|
| Discover | description | description (+ optional disable-model-invocation) |
| Cài | linh hoạt | `~/.cursor/skills` hoặc `.cursor/skills` |
| Built-in | — | `~/.cursor/skills-cursor` (đừng đụng) |
| Pin | tùy host | skills dir + optional `.cursor/rules` |
