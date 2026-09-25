# Expert — ehub ship (2026-09-25)

IN: working tree 2.8.0 · OUT: push + release GitHub.

## Cổng ehub

- `--leak` mặc định: sạch.
- `--check`: thiếu `LANGUAGE.txt` (cảnh báo scaffold mới — repo cũ public, không thêm file cho có).
- Sanitize 1 dòng brand nội bộ trong `6-observed-variables.md` trước public.
- Đồng bộ version còn sót: README `2.4.0` → `2.8.0`; `eval-results.json` → `2.8.0`.

## Việc ship

Repo đã có: https://github.com/hedralab/eskill — không `gh repo create`.
Commit + `git push origin main` + `gh release create v2.8.0` (tag latest; bỏ qua tag 2.5/2.6/2.7 vì chưa từng phát hành, đã bị 2.8.0 thay).
Không force push, không skip hook, không secret.
