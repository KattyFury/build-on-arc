# Hướng dẫn anh em build on Arc

Series hướng dẫn build app trên Arc network, đi từng bước từ lên ý tưởng tới sản phẩm chạy được. Mỗi bước có sẵn prompt để AI (Claude, ChatGPT...) guide bạn trực tiếp, không cần đã rành Arc từ trước.

## Bắt đầu

**1. Cài Claude Code + VS Code.** Chưa cài thì đọc bài này: [hướng dẫn setup](https://x.com/0xhieuxyz/status/2082123528573448506).

**2. Clone repo này về, mở bằng Claude Code.**

```bash
git clone https://github.com/KattyFury/build-on-arc.git
cd build-on-arc
claude
```

**3. Nói với Claude Code đúng một câu:**

> Đọc CLAUDE.md rồi dẫn tôi đi từ Bước 1.

Xong. Nó tự biết đưa prompt nào, lưu kết quả vào đâu, khi nào sang bước sau.

### Nếu không muốn dùng Claude Code

Vẫn làm tay được, không sao: mở thư mục của bước, copy khối prompt trong đó dán vào [Claude Chat](https://claude.ai), nói chuyện xong thì tự lưu kết quả lại thành file. Claude Code chỉ giúp bạn khỏi phải nhớ mình đang ở đâu.

## Cách hoạt động: Chat để nghĩ, Code để giữ và để làm

| Bước | Công cụ | Vì sao |
|---|---|---|
| 1 → 4 | **Claude Chat** (web) | Hỏi đáp qua lại và vẽ spec thì Chat nhanh hơn hẳn |
| 5 trở đi | **Claude Code** | Đụng file thật, chạy lệnh thật |
| Riêng phần giao diện ở Bước 6 | **Claude Design** rồi mới về Code | Chốt hình hài ở chỗ lặp rẻ trước, đưa sang Code dựng một lần |

Claude Code làm người dẫn đường xuyên suốt: nó đưa bạn prompt của bước đang tới, bạn mang sang Chat nói chuyện cho xong, rồi mang **kết quả chốt** về cho Code lưu vào `docs/` trong dự án của bạn.

> ⚠️ Đừng dán từng lượt hội thoại của Chat ngược vào Code. Một bước chỉ mang về **một** kết quả chốt — không thì bạn đang trả tiền token cho đúng một việc là chép chính tả.

## Mỗi bước có gì

Bước nào cũng cùng một hình dạng, quen một bước là quen hết:

1. **Lý thuyết** — bước này để làm gì, vì sao đừng bỏ qua
2. **Prompt** — khối copy được, dán thẳng vào Chat
3. **Ví dụ** — dự án mẫu trong [`example/`](example/) đi qua đúng bước đó
4. **Prompt này từng hụt chỗ nào** — bản đầu của prompt sai ở đâu, sửa thế nào

Mục 4 là thứ ít series nào có. Prompt trong đây không phải viết một lần là xong — nó được đem đi dùng thật, hụt chỗ nào thì sửa, và chỗ hụt được ghi lại nguyên vẹn. Xem `git log` là thấy nó tiến hoá thế nào.

## Cấu trúc

| Bước | Làm gì | Prompt | Ví dụ |
|---|---|---|---|
| [`01-ideation/`](01-ideation/README.md) | Lên ý tưởng, qua đủ 4 câu: đúng định hướng Arc, đúng đối tượng, có điểm hơn, khả thi | ✅ | ✅ |
| [`02-hoan-thien-y-tuong/`](02-hoan-thien-y-tuong/README.md) | Viết ý tưởng thành 6 câu PRD + rút core value | ✅ | ✅ |
| [`03-planning/`](03-planning/README.md) | 2 vòng: AI hỏi ngược bạn về UX/logic/lỗi/bảo mật, rồi chốt stack cho từng luồng | ✅ | ✅ vòng 1 |
| [`04-wireframe/`](04-wireframe/README.md) | Vẽ wireframe chốt từng màn trước khi code | ✅ | 🚧 |
| [`05-setup/`](05-setup/README.md) | Setup môi trường rồi bắt đầu build | ✅ | ✅ |
| [`06-build/`](06-build/README.md) | Build theo 3 giai đoạn: logic/flow → giao diện qua Claude Design → live rồi sửa theo người dùng | ✅ | ✅ |
| [`example/`](example/) | **Dự án mẫu, build song song với series** — TapTip, Tip & Lì xì nhanh trên Arc | — | — |

Đi lần lượt từng bước, xong bước nào mới qua bước đó.

## Về dự án mẫu

Ví dụ ở mọi bước đều lấy từ **cùng một dự án** trong [`example/`](example/): *Tip & Lì xì nhanh trên Arc*. Bước sau nối tiếp bước trước trên đúng dự án đó, không đổi sản phẩm giữa chừng — bạn chỉ phải nạp bối cảnh một lần rồi theo được tới cuối.

Nó được build **song song với series**: viết xong bước nào thì đem đúng bước đó ra dùng để build tiếp. Nên mọi câu trong phần ví dụ là thứ đã xảy ra thật, không phải tình huống nghĩ ra cho đẹp bài — kể cả mấy chỗ làm sai rồi phải quay lại sửa.

> ⚠️ `example/` là dự án của tụi mình, để bạn tham chiếu. **Dự án của bạn build ở thư mục riêng, đừng build đè vào đây.**

*(Quy định viết bài dành cho tác giả nằm ở `HANDOFF.md`, không để ở đây cho khỏi lệch hai chỗ.)*
