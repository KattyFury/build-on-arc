# Hướng dẫn anh em build on Arc

Series hướng dẫn build app trên Arc network, đi từng bước từ lên ý tưởng tới sản phẩm chạy được. Mỗi bước có sẵn prompt để AI (Claude, ChatGPT...) guide bạn trực tiếp, không cần đã rành Arc từ trước.

## Trước khi bắt đầu: cài Claude Code + VS Code

Chưa cài thì đọc bài này trước: [hướng dẫn setup Claude Code + VS Code](https://x.com/0xhieuxyz/status/2082123528573448506).

Cài rồi thì clone repo này về, mở bằng Claude Code — nó tự đọc `CLAUDE.md` và biết cách dẫn bạn đi từng bước.

```bash
git clone https://github.com/KattyFury/build-on-arc.git
```

## Bước nào dùng công cụ nào

| Bước | Công cụ | Vì sao |
|---|---|---|
| 1 → 4 | **Claude Chat** (web) | Hỏi đáp qua lại và vẽ spec thì Chat nhanh hơn hẳn |
| 5 trở đi | **Claude Code** | Đụng file thật, chạy lệnh thật |

**Claude Code đóng vai người dẫn đường xuyên suốt**: nó đưa bạn prompt của từng bước, bạn mang sang Chat nói chuyện, xong thì mang kết quả chốt về cho Code lưu lại. Chat để nghĩ, Code để giữ và để làm.

Đừng dán từng lượt hội thoại của Chat ngược vào Code — một bước chỉ mang về **một** kết quả chốt thôi, không thì đốt token cho đúng một việc là chép chính tả.

## Cấu trúc

- [`01-ideation/`](01-ideation/README.md) — lên ý tưởng, đủ 4 tiêu chí: đúng định hướng, xác định khách hàng, nên tồn tại, khả thi (xong)
- [`02-hoan-thien-y-tuong/`](02-hoan-thien-y-tuong/README.md) — hoàn thiện ý tưởng thành 6 câu PRD + rút core value (xong)
- [`03-planning/`](03-planning/README.md) — AI hỏi ngược lại mình về UX, logic, xử lý lỗi, edge case, bảo mật trước khi code (xong)
- `04-wireframe/` — wireframe trước khi code (đang làm)
- `05-setup/` — setup môi trường (đang làm)
- `example/` — **dự án mẫu, build song song với series** (đang làm)

Đi lần lượt từng bước, xong bước nào mới qua bước đó.

## Quy định: ví dụ xuyên suốt

Mọi bước dùng **chung một ví dụ duy nhất** là dự án mẫu trong [`example/`](example/) — một dự án nhỏ, build thật, và **build song song với chính series này**: viết xong bước nào thì đem bước đó ra dùng để build tiếp `example/`.

Hai lý do: người đọc chỉ phải nạp bối cảnh một lần rồi theo được tới cuối, và vì dự án được build thật nên mọi câu trả lời trong ví dụ đều là thứ đã xảy ra, không phải tình huống nghĩ ra cho đẹp bài.

Quy định cho bước viết sau:
- Mỗi bước có đúng **một** mục ví dụ, đặt tên `## Ví dụ: ...`, đứng ngay sau phần lý thuyết của bước đó.
- Ví dụ phải nối tiếp kết quả ở bước trước, không dựng lại từ đầu và không đổi sang sản phẩm khác giữa chừng.
- Chỉ nói những gì `example/` làm thật. Cần dẫn chứng thì trỏ vào file thật, không chế số liệu.
- Prompt của bước nào cũng phải **đem đi dùng thật rồi mới đăng**. Dùng thấy hụt chỗ nào thì sửa prompt và ghi lại nó từng hụt gì ở mục *"Prompt này từng hụt chỗ nào"*.

> ⚠️ `example/` là dự án của tụi mình, để bạn đọc tham chiếu. **Dự án của bạn build ở thư mục riêng, đừng build đè vào đây.**
