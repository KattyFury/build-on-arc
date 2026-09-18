# Bước 5: Setup môi trường

Đã có 2 file spec – một về tính năng (Bước 3), một về giao diện (Bước 4). Bước này dựng môi trường để code: cài công cụ, nối GitHub, chuẩn bị để Claude Code làm việc trong đúng thư mục dự án.

## Vì sao cần bước này

Đây là chỗ nhiều người mới hay khựng lại nhất – nghe tới terminal, Node.js, Git, MCP server là thấy ngợp, không biết cài cái gì trước cái gì sau. Không cần tự mò: AI hướng dẫn từng bước một, mình chỉ chạy lệnh và dán kết quả lại.

**Đang đi theo repo này bằng Claude Code?** Vậy Node.js và Claude Code đã có sẵn trên máy rồi (không có thì bạn đã không mở được repo). Cứ bảo Claude Code *"sang Bước 5"* – nó tự chạy lệnh kiểm tra, chỉ cài phần còn thiếu, và chỉ dừng lại ở chỗ cần bạn tự tay làm (đăng nhập GitHub, tạo tài khoản). Thư mục dự án cũng đã có từ Bước 1 (chứa `docs/`), bước này chỉ nối nó với Git/GitHub.

Đi tay bằng Claude Chat thì giả định lúc bắt đầu là máy sạch, chỉ mới có Claude Desktop + gói Pro, chưa Node.js, chưa Git, chưa GitHub. **Máy bạn đã từng build project khác rồi?** Nói thẳng với AI ngay từ câu đầu – nó sẽ verify từng phần đã có thay vì bắt cài lại từ đầu.

## Prompt

Copy đoạn dưới, paste vào Claude Code (hoặc Claude Chat nếu đi tay):

```
Đóng vai mentor kỹ thuật, hướng dẫn tôi cài đặt môi trường để code cùng Claude Code trên [Windows / macOS – chọn 1]. Tôi đã có Claude Desktop và gói Pro. [Nếu máy đã build project khác rồi: "Máy tôi đã từng build project khác, có thể đã cài sẵn một số thứ trong danh sách dưới." / Nếu máy sạch trơn: "Máy tôi sạch, chưa có gì khác."]

Trước khi bắt đầu, hỏi tôi máy đã có sẵn phần nào trong danh sách dưới chưa (chạy lệnh version-check tương ứng), rồi chỉ hướng dẫn cài phần còn thiếu – đừng bắt tôi làm lại việc đã xong.

Đi từng bước một. Nếu bạn tự chạy được lệnh trên máy tôi (Claude Code) thì tự chạy, giải thích ngắn gọn lệnh đó làm gì và báo kết quả. Nếu không (Claude Chat) thì mỗi bước chỉ đưa 1 lệnh terminal, giải thích ngắn gọn, rồi đợi tôi paste kết quả vào trước khi sang bước tiếp theo. Nếu có lỗi, giúp tôi debug trước khi tiếp tục. Nếu là macOS và tôi chưa có Homebrew, hướng dẫn cài trước.

Các bước cần hoàn thành:

1. Kiểm tra/cài Node.js (bản LTS) và npm
2. Cài Claude Code qua npm
3. Đăng nhập Claude Code bằng tài khoản Pro của tôi
4. Cài Git, kiểm tra hoạt động
5. Hướng dẫn tôi tạo tài khoản GitHub (nếu chưa có) và tạo 1 repo mới
6. Folder project: nếu đã có (chứa docs/ từ các bước lên kế hoạch) thì dùng luôn, chưa có thì tạo. Init git, connect tới repo GitHub vừa tạo
7. Thêm Arc MCP server vào Claude Code (server: https://docs.arc.io/mcp)
8. Verify: hỏi Claude Code 1 câu liên quan Arc Docs để confirm MCP hoạt động
9. Nếu project CHƯA có CLAUDE.md: tạo bằng lệnh dưới. **Nếu đã có rồi thì bỏ qua bước này** – đừng ghi đè, hỏi tôi trước nếu không chắc:

curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md

Đây là template giúp Claude Code làm việc cẩn thận hơn, bớt tự suy diễn, bớt làm phức tạp hơn cần thiết, bớt sửa lan ra ngoài phạm vi. Sau đó thêm phần riêng cho project của tôi vào cuối file (tech stack, coding style, lưu ý bảo mật...)

10. Nếu project CHƯA có file nào ghi trạng thái dự án (MEMORY.md, HANDOFF.md, hay tương đương): tạo MEMORY.md, ghi trạng thái hiện tại (đang làm gì, đã xong gì, bước tiếp theo là gì). **Nếu đã có rồi thì dùng file đó luôn, đừng tạo thêm file trùng vai trò.**

11. Đọc file chốt stack (docs/03-stack.md hoặc kết quả Vòng 2 Bước 3): cài đúng các gói trong mục "thứ cần cài", liệt kê cho tôi các tài khoản cần đăng ký và chỗ phải khai báo trước khi chạy (mục "thứ cần đăng ký" + "chỗ phải khai báo"). API key/secret chỉ để trong file môi trường (vd .env.local) đã nằm trong .gitignore – không bao giờ commit.

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

## Ví dụ: TapTip và EZwallet

### TapTip – chạy thật, trên máy đã có sẵn đồ

Máy build [`KattyFury/taptip`](https://github.com/KattyFury/taptip) đã từng build dự án khác trước đó (EZwallet), nên Node.js, Git, Claude Code, tài khoản GitHub đều có sẵn – không chạy prompt từ bước 1 của mục này. Thay vào đó verify từng phần: `node --version`, `git --version`, `claude --version` đều ra kết quả, `claude mcp list` xác nhận Arc MCP đã connect. Verify Arc MCP còn sống bằng cách hỏi thật một câu ("USDC as gas token trên Arc") – trả về đúng nội dung từ docs.arc.io, không phải câu trả lời bịa. Chi tiết: [`docs/05-setup.md`](https://github.com/KattyFury/taptip/blob/main/docs/05-setup.md). Chính lần chạy này lòi ra chỗ hụt "giả định máy sạch trơn" ở dưới.

Chỗ tốn công nhất của TapTip lại nằm ngoài danh sách 10 bước trên – là **tài khoản của nhà cung cấp dịch vụ**, cụ thể là Circle:

- **Mất file khôi phục là mất luôn tài khoản.** Ví developer-controlled của Circle cần một mã bí mật (Entity Secret) kèm một file khôi phục. TapTip làm hỏng tài khoản Circle **hai lần** vì chuyện này. Lần thứ hai: Claude Code truyền sai đường dẫn lưu file, nhưng công cụ của Circle không báo lỗi sớm – mã bí mật vẫn được đăng ký lên server trước rồi bước ghi file mới hỏng – tức Circle đã chốt mã, còn máy mình không có file. Hết đường cứu, phải mở tài khoản thứ ba. Bài học: ngay lúc đăng ký, tự lấy nội dung file ra rồi tự lưu tay, kiểm tra file nằm đó rồi mới đi tiếp.
- **Push lên GitHub không có nghĩa là web đã cập nhật.** TapTip deploy bằng tay (`npm run cf:deploy`), không có gì tự chạy khi push. Đã dính thật: sửa, commit, push xong xuôi, mở web ra vẫn y như cũ. Lúc setup nên hỏi rõ luôn: *"push xong thì cái gì tự chạy, cái gì phải chạy tay?"*

### EZwallet – dựng ngược từ quyết định có thật

Dự án thật của tác giả – [`KattyFury/ezwallet`](https://github.com/KattyFury/ezwallet). Setup của dự án này diễn ra trước cả series nên không chạy đúng prompt trên, nhưng kết quả cuối thì trùng khớp: Node.js, Git, tài khoản GitHub, tài khoản Circle Console đều có sẵn trước khi code dòng đầu tiên.

Có một chỗ setup của EZwallet đi xa hơn nội dung bước này hay nhắc tới, đáng ghi lại làm kinh nghiệm: **Circle Web SDK (login, PIN, swap) không chạy được trên `localhost`** – muốn test các luồng đó phải deploy thật. Giải pháp không phải deploy liên tục để test, mà dựng một **chế độ mock** riêng (`npm run mock`): vào thẳng giao diện với ví giả + số dư giả, bỏ qua đăng nhập/PIN, giả lập gửi/swap thành công – đủ để chỉnh UI/flow nhanh ở máy, chỉ khi nào cần test thật cơ chế ký/tiền mới đẩy lên deploy.

Setup 2 tiến trình chạy song song cũng là kinh nghiệm đáng mang qua dự án khác: 1 terminal chạy proxy API cục bộ giả lập backend thật (để không phải deploy mới test được gọi API), 1 terminal chạy dev server frontend – việc tách 2 tiến trình giúp test API riêng khỏi UI mà không cần đợi build.

### Prompt này từng hụt chỗ nào

Prompt giả định **máy sạch trơn** – đúng với người mới lần đầu, nhưng sai với người đã build project khác trên cùng máy. Chạy nguyên bước 1-6 (cài Node, Claude Code, Git, tạo GitHub repo mới) trong trường hợp đó là làm lại việc đã xong, tốn token vô ích.

Hai chỗ cụ thể bị lụt:

1. **Bước 9 (curl CLAUDE.md template)** không tính tới trường hợp project đã có `CLAUDE.md` riêng, chi tiết hơn template gốc – curl đè lên là mất công sức viết trước đó.
2. **Bước 10 (tạo MEMORY.md)** trùng vai trò với `HANDOFF.md` nếu project đã có – tạo thêm là hai file cùng ghi trạng thái, dễ lệch nhau về sau.

**Sửa:** trước khi chạy nguyên prompt, hỏi một câu chốt đầu tiên – *"Máy này đã từng build project nào khác chưa? Nếu có, phần nào trong danh sách dưới đây đã cài rồi?"* – rồi chỉ chạy phần còn thiếu.

Ba chỗ hụt nữa lòi ra khi đi thử cả series từ đầu tới cuối như một người mới (09/2026):

3. **Prompt viết cho Claude Chat, trong khi người đi theo repo đang đứng sẵn trong Claude Code.** Bắt người ta chép lệnh từ Chat sang terminal rồi chép kết quả ngược lại, trong khi Claude Code tự chạy được. Sửa: prompt cho phép tự chạy nếu chạy được, chỉ đưa lệnh khi đi tay.
4. **Bước 6 "tạo folder project" đụng với thư mục đã có từ Bước 1** (nơi đang giữ `docs/`). Làm đúng từng chữ là ra 2 thư mục. Sửa: có rồi thì dùng luôn.
5. **Không nối với file chốt stack của Bước 3.** Setup xong môi trường chung nhưng không cài đúng gói, không nhắc tài khoản dịch vụ phải đăng ký – sang Bước 6 mới vấp. Sửa: thêm bước 11 đọc file stack, cài đúng gói, liệt kê tài khoản + chỗ khai báo, và giữ secret ngoài git.

Xong bước này mới qua Bước 6, ném 2 file spec vào thư mục dự án và bắt tay build.
