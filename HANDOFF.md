# HANDOFF – build-on-arc

> File làm việc của tác giả, không phải nội dung cho người đọc series. Mở máy mới thì đọc file này trước.
> Luật cho Claude Code nằm ở `CLAUDE.md`. File này ghi **đang ở đâu** và **quy định viết bài**.
> **Cập nhật:** 2026-08-07

---

## 0. Repo này là gì

Series hướng dẫn build app trên Arc, viết cho người Việt không rành crypto và không có nền lập trình, **kèm luôn dự án mẫu trong `example/`**. Nội dung gốc là loạt bài "Build on Arc bằng Claude Code" trên X của [@0xhieuxyz](https://x.com/0xhieuxyz) — repo này là bản có nhà, vì X thì bài chết sau 48 giờ.

- GitHub: https://github.com/KattyFury/build-on-arc (public)
- Local: `D:\Files\Claude\build_on_arc\build-on-arc`

## 1. Đang ở đâu

| Bước | Thư mục | Trạng thái |
|---|---|---|
| 1. Lên ý tưởng | `01-ideation/` | ✅ **XONG TRỌN** — lý thuyết + prompt v2 + ví dụ thật + mục "prompt từng hụt chỗ nào" |
| 2. Hoàn thiện ý tưởng | `02-hoan-thien-y-tuong/` | ✅ **XONG TRỌN** — prompt đã sửa theo 5 lỗi tìm được (câu 1 lẫn thông số kỹ thuật, câu 2 quên vai người gửi, câu 4 hỏi trừu tượng, câu 6 bị lạc đề, core value nhét thông số) + ví dụ thật + "prompt từng hụt chỗ nào" |
| 3. Plan chi tiết | `03-planning/` | ✅ **XONG TRỌN** — prompt đã sửa theo 5 lỗi tìm được (đẩy trách nhiệm bên thứ ba, bỏ sót câu trong nhóm, tổ hợp rủi ro, ép đổi ý khi user đã chấp nhận rủi ro, quên tổng hợp file) + ví dụ thật + "prompt từng hụt chỗ nào" |
| 4. Wireframe | `04-wireframe/` | ✅ Lý thuyết + prompt xong, **đã chạy thật** (`example/docs/04-wireframe.md`). README chưa viết mục Ví dụ + "prompt từng hụt chỗ nào" |
| 5. Setup môi trường | `05-setup/` | ✅ **XONG TRỌN** — lý thuyết + prompt (đã sửa sau khi chạy thật) + ví dụ thật + mục "prompt từng hụt chỗ nào" (`example/docs/05-setup.md`) |
| 6. Build | `06-build/` | ✅ README xong (2 giai đoạn: logic/flow trước, giao diện sau + prompt). Chưa chạy thật — chờ code TapTip |
| Dự án mẫu | `example/` | Bước 1-4 xong phần spec/design (docs 01-04). Chưa có code. Tên app: **TapTip**, platform: **PWA** |

**Dự án mẫu: TapTip — Tip & Lì xì nhanh trên Arc.** Gửi tip bất cứ lúc nào + lì xì dịp Tết, đăng nhập bằng email + passkey, ví ẩn phía sau bằng Circle Wallets, app trả gas thay user. Yêu cầu số một là **tốc độ**.

**Ví dụ EZwallet đã gỡ khỏi cả 3 bước (08-06, user chốt).**

**Quyết định stack (08-07):** Bỏ khung "Tech Stack – Locked" copy từ CLAUDE.md của ezwallet — không áp dụng cho series này, mỗi dự án tự chọn stack. `example/` (TapTip) fork [`circlefin/arc-p2p-payments`](https://github.com/circlefin/arc-p2p-payments) (Next.js + Supabase + Circle Modular Wallets/Passkey) thay vì code từ đầu trên Cloudflare Workers/Pages — lý do: sample app đã có sẵn passkey + gasless P2P đúng spec Bước 2-3, review kỹ hơn xem chi tiết `CLAUDE.md` mục Tech Stack.

### Vòng lặp đã chạy thật 1 lần (Bước 1, 08-06)

Chạy prompt → lòi 5 lỗi quy trình → sửa prompt → ghi lại chỗ hụt. Hai commit tách đôi đúng luật: `ed8510d` (example) + `ba5d481` (hướng dẫn). **Cách này chạy được, cứ thế mà làm tiếp cho Bước 2.**

Lỗi nặng nhất tìm ra: prompt bảo AI "hỏi bạn từng câu" nhưng không bảo nó **DẪN** → AI thành thư ký ghi chép, ngồi đợi user nói xong mới góp ý. Đã thêm khối *"Cách làm việc"* lên đầu prompt. **Bài học chung: prompt nào cũng phải nói rõ ai dẫn ai theo** — áp dụng luôn khi viết prompt cho Bước 4, 5, 6.

## 2. CÁCH LÀM VIỆC — build song song

Đây là quyết định lớn nhất của repo, đừng làm khác:

1. Chạy bước N với user (mình đóng đúng vai prompt trong bài mô tả)
2. Build phần tương ứng vào `example/`
3. Prompt hụt chỗ nào, hỏi thiếu, hỏi thừa → **sửa README của bước đó** + ghi vào mục *"Prompt này từng hụt chỗ nào"*
4. **Tách commit:** một commit build `example/`, một commit sửa hướng dẫn

Lý do tách commit: `git log` trở thành bằng chứng cho người đọc thấy prompt tiến hoá thế nào, không phải xịn sẵn từ đầu. Không series nào làm phần này.

## 3. VIỆC TIẾP THEO

**08-07: Bước 1-5 đều XONG TRỌN** — lý thuyết + prompt (đã sửa từ lỗi chạy thật) + ví dụ thật + "prompt từng hụt chỗ nào" cho cả 5 bước.

**Bước 6:** user gửi nội dung — ngắn, không theo khuôn 4 mục như 1-5 (không có "prompt từng hụt chỗ nào" vì đây là bước code thật, không phải chạy 1 prompt cố định). Nội dung chính: tách 2 giai đoạn build (Giai đoạn 1 logic/flow trước, để UI mộc, xong 1 tính năng dừng lại chờ user test rồi mới qua tính năng tiếp; Giai đoạn 2 mới áp UI theo wireframe, làm từng màn dừng lại chờ duyệt). Kèm 1 prompt để dán vào Claude Code sau khi đã ném 2 file spec (Bước 3 + Bước 4) vào folder dự án. User tự nhận "bước 6 thực ra chả có gì" — đây là bước cuối, sau đó là hướng dẫn đăng bài chia sẻ sản phẩm, và series coi như kết thúc (có thể có thêm tập bonus).

**Việc kế tiếp khi quay lại:** viết `06-*/README.md` (chưa đặt tên thư mục — có thể `06-build/`) từ nội dung user gửi, rồi bắt tay code TapTip thật: fork `circlefin/arc-p2p-payments`, ném `example/docs/03-planning.md` + `example/docs/04-wireframe.md` vào, chạy đúng quy trình 2 giai đoạn.

## 4. QUY ĐỊNH VIẾT BÀI

### 4.1 Ví dụ xuyên suốt

**Đây là chỗ DUY NHẤT giữ quy định viết bài.** `README.md` chỉ nói cho người đọc biết dự án mẫu là gì, không chép lại mấy luật dưới đây — cố ý, để khỏi có hai bản lệch nhau.

Mọi bước dùng chung dự án trong `example/`.

- Mỗi bước đúng **một** mục ví dụ, tên `## Ví dụ: ...`, đứng ngay sau phần lý thuyết.
- Nối tiếp bước trước, không dựng lại từ đầu, không đổi sản phẩm giữa chừng.
- **Chỉ nói những gì `example/` làm thật.** Dẫn chứng thì trỏ vào file thật, không chế số liệu.
- **Cách viết ví dụ:** đừng bịa câu hỏi rồi bịa câu trả lời. Lấy **quyết định có thật** trong `example/` rồi dựng ngược lại thành tình huống đã sinh ra nó.

### 4.2 Tiêu chí ý tưởng đã nới (08-06)

Bước 1 Câu 1 ban đầu bắt ý tưởng phải giải **vấn đề thiết thực**. User nới ra: **thứ vui, thứ mình thích, thứ người ta thật sự muốn dùng cũng được tính** — lì xì không giải quyết vấn đề gì cả nhưng vẫn đáng build.

Cái **không** nới: vẫn phải là thứ mình hoặc người mình biết **thật sự làm ngoài đời**, không ngồi tưởng tượng ra.

### 4.3 Note dán spec dưới mọi prompt

Mọi prompt chuyển giao cần spec bước trước (Bước 2 trở đi) phải kèm câu ghi chú ngay dưới khối prompt:

> Dán kèm nếu bạn đang mở cửa sổ chat mới. Nếu dùng chung 1 cửa sổ chat xuyên suốt từ đầu thì bỏ qua — Chat đã có sẵn context, dán lại là thừa.

Lý do: giả định mặc định "mỗi bước một cửa sổ Chat mới" chỉ đúng với một cách dùng, không phải cách duy nhất. Không note rõ thì người dùng 1 chat xuyên suốt sẽ dán thừa, tốn token vô ích.

### 4.4 Giọng văn

Tiếng Việt đời thường, xưng "mình" / "anh em" như bài gốc trên X. Câu ngắn. Không sáo. Bảng khi so sánh, blockquote cho ghi chú đáng nhớ. Mỗi bước kết bằng một câu dẫn sang bước sau.

**Dấu gạch dài: chỉ dùng en dash `–` (U+2013), không dùng em dash `—` (U+2014)** — luật gốc nằm trong `CLAUDE.md`.

> 🔴 **NỢ – VIỆC ĐẦU TIÊN NÊN LÀM KHI QUAY LẠI.** Đếm 08-06: **80 chỗ đang dùng em dash sai luật**, rải khắp repo (01: 21 · example/docs: 18 · README: 11 · HANDOFF: 10 · 02: 9 · example/README: 7 · 03: 3 · CLAUDE.md: 1). Phần lớn do chính mình viết vào mấy phiên gần đây, không phải bài cũ.
>
> ⚠️ **ĐỪNG replace-all mù.** Có chỗ phải GIỮ em dash: dòng phát biểu luật trong `CLAUDE.md` và dòng ngay trên đây — chúng phải in ra ký tự em dash làm ví dụ, thay đi là luật tự mâu thuẫn. Cách an toàn: bỏ qua `CLAUDE.md` và mục 4.3 này khi thay, quét 6 file còn lại.

## 5. Git

Remote `origin` = GitHub, branch `main`. Xong việc là commit + push ngay, đừng để commit nằm im ở local.

## 6. Tools tham khảo – dùng ở Bước 6 (code UI thật), KHÔNG dùng ở Bước 4

Bước 4 (wireframe) cố tình bỏ hết style, chỉ khung + label chức năng – mấy tool dưới đây đều thuộc chuyện style/component thật nên chỉ có ích lúc code, không có ích lúc vẽ khung.

- **21st.dev** – https://21st.dev/ – marketplace React+Tailwind, prompt sẵn cho Claude Code/Cursor/v0
- **Astryx (Meta)** – https://astryx.atmeta.com/ – design system chính thức Meta, React 19 + StyleX, 160+ component – hơi nặng đô cho app nhỏ như `example/`
- **Magic UI** – https://magicui.design/ – component + animation React+Tailwind
- **ui-ux-pro-max-skill** – https://github.com/nextlevelbuilder/ui-ux-pro-max-skill – AI skill sinh design system (màu, font, style) theo project, 114,271 sao (verify qua GitHub API 08-07, số thật cao hơn số đồn)
- **taste-skill** – https://github.com/Leonxlnx/taste-skill (site: tasteskill.dev) – skill chống AI sinh UI "generic slop", 73,405 sao (verify qua GitHub API 08-07)
