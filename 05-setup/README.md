# Bước 5: Setup môi trường

Đã có 2 file spec – một về tính năng (Bước 3), một về giao diện (Bước 4). Bước này dựng môi trường để code: cài công cụ, nối GitHub, chuẩn bị để Claude Code làm việc trong đúng thư mục dự án.

## Vì sao cần bước này

Đây là chỗ nhiều người mới hay khựng lại nhất – nghe tới terminal, Node.js, Git, MCP server là thấy ngợp, không biết cài cái gì trước cái gì sau. Không cần tự mò: AI hướng dẫn từng bước một, mình chỉ chạy lệnh và dán kết quả lại.

Giả định lúc bắt đầu: máy sạch, chỉ mới có Claude Desktop + gói Pro, chưa Node.js, chưa Git, chưa GitHub. **Máy bạn đã từng build project khác rồi?** Nói thẳng với AI ngay từ câu đầu – nó sẽ verify từng phần đã có thay vì bắt cài lại từ đầu.

## Prompt

Copy đoạn dưới, paste vào Claude Chat:

```
Đóng vai mentor kỹ thuật, hướng dẫn tôi cài đặt môi trường để code cùng Claude Code trên [Windows / macOS – chọn 1]. Tôi đã có Claude Desktop và gói Pro. [Nếu máy đã build project khác rồi: "Máy tôi đã từng build project khác, có thể đã cài sẵn một số thứ trong danh sách dưới." / Nếu máy sạch trơn: "Máy tôi sạch, chưa có gì khác."]

Trước khi bắt đầu, hỏi tôi máy đã có sẵn phần nào trong danh sách dưới chưa (chạy lệnh version-check tương ứng), rồi chỉ hướng dẫn cài phần còn thiếu – đừng bắt tôi làm lại việc đã xong.

Đi từng bước một, mỗi bước chỉ đưa 1 lệnh terminal, giải thích ngắn gọn lệnh đó làm gì, rồi đợi tôi paste kết quả vào trước khi sang bước tiếp theo. Nếu có lỗi, giúp tôi debug trước khi tiếp tục. Nếu là macOS và tôi chưa có Homebrew, hướng dẫn cài trước.

Các bước cần hoàn thành:

1. Kiểm tra/cài Node.js (bản LTS) và npm
2. Cài Claude Code qua npm
3. Đăng nhập Claude Code bằng tài khoản Pro của tôi
4. Cài Git, kiểm tra hoạt động
5. Hướng dẫn tôi tạo tài khoản GitHub (nếu chưa có) và tạo 1 repo mới
6. Tạo folder project, init git, connect tới repo GitHub vừa tạo
7. Thêm Arc MCP server vào Claude Code (server: https://docs.arc.io/mcp)
8. Verify: hỏi Claude Code 1 câu liên quan Arc Docs để confirm MCP hoạt động
9. Nếu project CHƯA có CLAUDE.md: tạo bằng lệnh dưới. **Nếu đã có rồi thì bỏ qua bước này** – đừng ghi đè, hỏi tôi trước nếu không chắc:

curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md

Đây là template giúp Claude Code làm việc cẩn thận hơn, bớt tự suy diễn, bớt làm phức tạp hơn cần thiết, bớt sửa lan ra ngoài phạm vi. Sau đó thêm phần riêng cho project của tôi vào cuối file (tech stack, coding style, lưu ý bảo mật...)

10. Nếu project CHƯA có file nào ghi trạng thái dự án (MEMORY.md, HANDOFF.md, hay tương đương): tạo MEMORY.md, ghi trạng thái hiện tại (đang làm gì, đã xong gì, bước tiếp theo là gì). **Nếu đã có rồi thì dùng file đó luôn, đừng tạo thêm file trùng vai trò.**

Sau khi xong tất cả, tóm tắt lại cho tôi những gì đã cài, và những lệnh tôi cần nhớ để mở lại môi trường này vào lần sau.
```

Trả lời khi Chat hỏi: chọn Windows hay macOS, log in cái gì thì log in cái đó, lỗi gì thì dán nguyên văn lỗi để Chat debug tiếp – đừng tự sửa rồi báo lại là "vẫn lỗi".

## Kết quả cuối bước

- Một folder dự án đã connect GitHub
- Claude Code chạy được trong folder đó, có Arc MCP để tra Arc Docs trực tiếp
- `CLAUDE.md` + `MEMORY.md` ở gốc dự án – lần sau mở lại không cần kể lại từ đầu
- Một dòng lệnh để mở lại môi trường mỗi lần sau, dạng:

```
cd "đường-dẫn-tới-project"
claude
```

## Ví dụ: TapTip

Máy build TapTip đã từng build dự án khác trước đó (ezwallet), nên Node.js, Git, Claude Code, tài khoản GitHub đều có sẵn – không chạy prompt từ Bước 1 của mục này. Thay vào đó verify từng phần: `node --version`, `git --version`, `claude --version` đều ra kết quả, `claude mcp list` xác nhận Arc MCP đã connect. Verify Arc MCP còn sống bằng cách hỏi thật một câu ("USDC as gas token trên Arc") – trả về đúng nội dung từ docs.arc.io, không phải câu trả lời bịa.

Chi tiết đầy đủ: [`docs/05-setup.md`](https://github.com/KattyFury/taptip/blob/main/docs/05-setup.md) (repo `KattyFury/taptip`).

### Prompt này từng hụt chỗ nào

Prompt giả định **máy sạch trơn** – đúng với người mới lần đầu, nhưng sai với người đã build project khác trên cùng máy. Chạy nguyên bước 1-6 (cài Node, Claude Code, Git, tạo GitHub repo mới) trong trường hợp đó là làm lại việc đã xong, tốn token vô ích.

Hai chỗ cụ thể bị lụt:

1. **Bước 9 (curl CLAUDE.md template)** không tính tới trường hợp project đã có `CLAUDE.md` riêng, chi tiết hơn template gốc – curl đè lên là mất công sức viết trước đó.
2. **Bước 10 (tạo MEMORY.md)** trùng vai trò với `HANDOFF.md` nếu project đã có – tạo thêm là hai file cùng ghi trạng thái, dễ lệch nhau về sau.

**Sửa:** trước khi chạy nguyên prompt, hỏi một câu chốt đầu tiên – *"Máy này đã từng build project nào khác chưa? Nếu có, phần nào trong danh sách dưới đây đã cài rồi?"* – rồi chỉ chạy phần còn thiếu.

Xong bước này mới qua Bước 6, ném 2 file spec vào thư mục dự án và bắt tay build.
