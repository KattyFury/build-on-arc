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

> ⚠️ Đừng dán từng lượt hội thoại của Chat ngược vào Code. Một bước chỉ mang về **một** kết quả chốt – không thì bạn đang trả tiền token cho đúng một việc là chép chính tả.

## Mỗi bước có gì

Bước nào cũng cùng một hình dạng, quen một bước là quen hết:

1. **Lý thuyết** – bước này để làm gì, vì sao đừng bỏ qua
2. **Prompt** – khối copy được, dán thẳng vào Chat
3. **Ví dụ** (một số bước) – quyết định có thật từ một dự án thật, đi qua đúng bước đó
4. **Prompt này từng hụt chỗ nào** – bản đầu của prompt sai ở đâu, sửa thế nào

Mục 4 là thứ ít series nào có, và có ở **mọi** bước. Prompt trong đây không phải viết một lần là xong – nó được đem đi chạy thử, hụt chỗ nào thì sửa, và chỗ hụt được ghi lại nguyên vẹn. Xem `git log` là thấy nó tiến hoá thế nào.

## Cấu trúc

| Bước | Làm gì | Prompt |
|---|---|---|
| [`01-ideation/`](01-ideation/README.md) | Lên ý tưởng, qua đủ 4 câu: đúng định hướng Arc, đúng đối tượng, có điểm hơn, khả thi | ✅ |
| [`02-hoan-thien-y-tuong/`](02-hoan-thien-y-tuong/README.md) | Viết ý tưởng thành 6 câu PRD + rút core value | ✅ |
| [`03-planning/`](03-planning/README.md) | 2 vòng: AI hỏi ngược bạn về UX/logic/lỗi/bảo mật, rồi chốt stack cho từng luồng | ✅ |
| [`04-wireframe/`](04-wireframe/README.md) | Vẽ wireframe chốt từng màn trước khi code, kèm hệ lưới áp cho mọi màn | ✅ |
| [`05-setup/`](05-setup/README.md) | Setup môi trường rồi bắt đầu build | ✅ |
| [`06-build/`](06-build/README.md) | Build theo 3 giai đoạn: logic/flow → giao diện qua Claude Design → live rồi sửa theo người dùng | ✅ |

Đi lần lượt từng bước, xong bước nào mới qua bước đó.

## Về dự án mẫu

Repo này **thuần hướng dẫn** – không giữ code dự án mẫu song song bên trong. Từng thử cách đó với TapTip (Tip & Lì xì nhanh trên Arc, build song song với series), nhưng việc vừa viết guide vừa vá bug/deploy một app thật khiến công việc chính bị xao nhãng – nên đã tách TapTip ra [`KattyFury/taptip`](https://github.com/KattyFury/taptip), quay lại sau.

Mục "Ví dụ" ở một số bước vẫn còn vì dẫn chứng những quyết định có thật từ TapTip lúc nó còn là dự án mẫu ở đây – link trỏ sang repo mới. Prompt vẫn phải chạy thử thật trước khi đăng (không nhất thiết build trong repo này), và chỗ hụt tìm ra được ghi vào mục "Prompt này từng hụt chỗ nào" của từng bước.

*(Quy định viết bài dành cho tác giả nằm ở `HANDOFF.md`, không để ở đây cho khỏi lệch hai chỗ.)*
