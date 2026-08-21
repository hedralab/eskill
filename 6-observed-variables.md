# 6 — Observed Variables (biến số lộ ra khi DÙNG THẬT — vòng lặp khép kín)

Đọc file này TRƯỚC khi scan biến số (Trụ 12 Bước 0) — nhất là khi build skill cùng họ e-family.

## [2026-08-21] [ehub] license — nhóm QUY TRÌNH
- Triệu chứng: ehub hardcode MIT; user đổi eskill MIT→Non-Commercial→Use-Only 3 lần sau khi push
- Quy tắc/Bẫy đã thêm: ehub Bước 1 hỏi license (--license mit/non-commercial/use-only/all-rights) — không default im lặng (ehub 1.4.0)
- Câu hỏi bắt buộc khi build: "Repo này bán / nội bộ / cá nhân? → license nào?"

## [2026-08-21] [ehub] ngôn ngữ — nhóm NGƯỜI ĐỌC
- Triệu chứng: eskill README EN nhưng CoC/LICENSE/SKILL.md VN lẫn lộn; user phải check từng file
- Quy tắc/Bẫy đã thêm: **1 biến gốc → MỌI file**: --readme-lang điều khiển README + CODE_OF_CONDUCT + LICENSE + LANGUAGE.txt (marker) + audit chéo (ehub 1.5.0)
- Câu hỏi bắt buộc khi build: "Repo cho ai đọc — vi hay en?" (1 lần, dùng cho mọi file)

## [2026-08-21] [ehub] môi trường gh — nhóm MÔI TRƯỜNG
- Triệu chứng: máy 2 tài khoản gh, 1 cái hỏng → gh auth status exit 1 dù account active OK → gate chặn push oan
- Quy tắc/Bẫy đã thêm: gate không tin exit code toàn cục — đối chiếu "Active account: true" (ehub 1.3.2)
- Câu hỏi bắt buộc: "Máy có nhiều account gh không? account phụ hỏng không được chặn account active"

## [2026-08-21] [ehub] quy trình sync — nhóm QUY TRÌNH/CON NGƯỜI
- Triệu chứng: rsync --delete mirror live vô tình xóa .gitignore khỏi repo GitHub (live skill không có file này)
- Quy tắc/Bẫy đã thêm: sync repo = so diff trước, đừng --delete mù; skill live nên có .gitignore (ehub 1.4.1)
- Câu hỏi bắt buộc: "File nào repo cần nhưng live skill không có? (gitignore, CHANGELOG...)"
