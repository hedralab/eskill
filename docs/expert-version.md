# Expert — version / latest (2026-09-25)

IN: local `~/.cursor/skills/eskill` · OUT: 2.8.0 có phải bản mới nhất để ship không.

## So sánh

| Nguồn | Version |
|---|---|
| Local SKILL.md / `.version-bump.json` | **2.8.0** (working tree, chưa commit trước lượt này) |
| GitHub `main` SKILL.md | **2.5.0** (`e30ffbc`) |
| GitHub latest release/tag | **v2.4.0** (2026-08-21) |
| Repo | https://github.com/hedralab/eskill (public) |

`main` local = `origin/main` (0 ahead / 0 behind). Bản 2.6–2.8 chỉ nằm working tree.

## Spec ngoài repo

- [agentskills.io/specification](https://agentskills.io/specification) — `dateModified` 2026-08-04 (trước 2.8.0). Field: name, description, license, compatibility, metadata, **allowed-tools** (experimental). eskill `spec-rules.md` đã có allowed-tools. Không thiếu field bắt buộc.
- Cursor `create-skill` (`~/.cursor/skills-cursor/create-skill`): name + description + `disable-model-invocation`. 2.5.0 đã đóng gói `references/cursor-skills.md`. Không field mới bắt buộc.
- Changelog nội bộ: 2.8.0 (2026-08-27) = đội theo việc skill, cấm Gọn/Hiệu quả/Eval, cấm eprompt. Đúng bản product mới nhất.

## Kết luận

Local **ahead** GitHub. Không pull. Không bump 2.9.0. Ship **2.8.0**.
