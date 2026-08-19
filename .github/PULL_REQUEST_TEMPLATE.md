## Mô tả thay đổi

<!-- Tóm tắt: sửa gì, tại sao. Gắn issue nếu có (#123) -->

## Checklist

- [ ] `python3 scripts/validate-skill.py .` PASS
- [ ] Nếu đổi SKILL.md → đồng bộ README + RELEASE-NOTES + version (`.version-bump.json`)
- [ ] Nếu chuẩn bị bán → chạy `validate-skill.py . --leak --brand "..."` PASS
- [ ] Không có file rác (.bak, .DS_Store, *.pyc) trong diff

## Test

<!-- Bằng chứng: validator output, eval-results, smoke test -->
