# Bán skill trên GitHub — funnel tham khảo (thực thi gọi skill cuối)

eskill BUILD skill — KHÔNG tự lo delivery/bán. Quy trình bán trên GitHub chia cho skill cuối:

- **Đẩy repo lên GitHub + release/tag** → gọi `ehub` (docs/gh-cli.md · repo-standard §7 semver/changelog/release)
- **Funnel Telegram bán hàng** (bot chốt khách, cấp quyền) → gọi `egram`

eskill chỉ giữ:
- `references/checklist-thuong-mai.md` — checklist an toàn khi bán (leak scan, LICENSE, README đồng bộ, cài skill lạ)
- `references/openai-yaml.md` + `agents/openai.yaml` — metadata marketplace/UI

Bẫy: đừng nhét delivery vào eskill (đã gỡ scripts/sell/ ở 1.9.0 — mâu thuẫn routing). Cần script bán → tạo bằng ehub rồi để egram vận hành funnel.
