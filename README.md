# Hướng dẫn anh em build on Arc

Series hướng dẫn build app trên Arc network, đi từng bước từ lên ý tưởng tới sản phẩm chạy được. Mỗi bước có sẵn prompt để AI (Claude, ChatGPT...) guide bạn trực tiếp, không cần đã rành Arc từ trước.

## Cấu trúc

- [`01-ideation/`](01-ideation/README.md) — lên ý tưởng, đủ 4 tiêu chí: đúng định hướng, xác định khách hàng, nên tồn tại, khả thi (xong)
- [`02-hoan-thien-y-tuong/`](02-hoan-thien-y-tuong/README.md) — hoàn thiện ý tưởng thành 6 câu PRD + rút core value (xong)
- [`03-planning/`](03-planning/README.md) — AI hỏi ngược lại mình về UX, logic, xử lý lỗi, edge case, bảo mật trước khi code (xong)
- `04-wireframe/` — wireframe trước khi code (đang làm)
- `05-setup/` — setup môi trường, có bản dùng Terminal và bản không cần Terminal cho newbie (đang làm)

Đi lần lượt từng bước, xong bước nào mới qua bước đó.

## Quy định: ví dụ xuyên suốt

Mọi bước trong series dùng **chung một ví dụ duy nhất là EZwallet** — [ezwallet.cash](https://ezwallet.cash), mã nguồn [KattyFury/ezwallet](https://github.com/KattyFury/ezwallet) (MIT). Bước sau nối tiếp bước trước trên cùng sản phẩm đó.

Hai lý do: người đọc chỉ phải nạp bối cảnh một lần rồi theo được tới cuối, và EZwallet là sản phẩm chạy thật nên mọi câu trả lời trong ví dụ đều kiểm chứng được, không phải giả định.

Quy định cho bước viết sau:
- Mỗi bước có đúng **một** mục ví dụ, đặt tên `## Ví dụ: ...`, đứng ngay sau phần lý thuyết của bước đó.
- Ví dụ phải nối tiếp kết quả EZwallet ở bước trước, không dựng lại từ đầu và không đổi sang sản phẩm khác.
- Chỉ nói những gì EZwallet làm thật. Cần dẫn chứng thì lấy từ repo ezwallet, không tự chế con số.
