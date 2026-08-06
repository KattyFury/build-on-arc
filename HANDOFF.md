# HANDOFF – build-on-arc

> File làm việc của tác giả, không phải nội dung cho người đọc series. Mở máy mới thì đọc file này trước.
> Luật cho Claude Code nằm ở `CLAUDE.md`. File này ghi **đang ở đâu** và **quy định viết bài**.
> **Cập nhật:** 2026-08-06

---

## 0. Repo này là gì

Series hướng dẫn build app trên Arc, viết cho người Việt không rành crypto và không có nền lập trình, **kèm luôn dự án mẫu trong `example/`**. Nội dung gốc là loạt bài "Build on Arc bằng Claude Code" trên X của [@0xhieuxyz](https://x.com/0xhieuxyz) — repo này là bản có nhà, vì X thì bài chết sau 48 giờ.

- GitHub: https://github.com/KattyFury/build-on-arc (public)
- Local: `D:\Files\Claude\build_on_arc\build-on-arc`

## 1. Đang ở đâu

| Bước | Thư mục | Trạng thái |
|---|---|---|
| 1. Lên ý tưởng | `01-ideation/` | ✅ **XONG TRỌN** — lý thuyết + prompt v2 + ví dụ thật + mục "prompt từng hụt chỗ nào" |
| 2. Hoàn thiện ý tưởng | `02-hoan-thien-y-tuong/` | Lý thuyết + prompt xong (soạn 08-06, CHƯA chạy thật). **Ví dụ: trống** |
| 3. Plan chi tiết | `03-planning/` | Lý thuyết + prompt xong. **Ví dụ: trống** |
| 4. Wireframe | `04-wireframe/` | ❌ chưa có |
| 5. Setup môi trường | `05-setup/` | ❌ chưa có |
| 6. (chưa đặt tên) | — | ❌ chưa có, user nói sẽ gửi nội dung |
| Dự án mẫu | `example/` | Bước 1 xong (`example/docs/01-ideation.md`), chưa có code |

**Dự án mẫu: Tip & Lì xì nhanh trên Arc.** Gửi tip bất cứ lúc nào + lì xì dịp Tết, đăng nhập bằng email, ví ẩn phía sau bằng Circle Wallets dev-controlled, app trả gas thay user qua Paymaster. Yêu cầu số một là **tốc độ** — chính nó là thứ dùng để loại Privy ở câu 3.

**Ví dụ EZwallet đã gỡ khỏi cả 3 bước (08-06, user chốt).** Bước 2 và 3 vẫn là placeholder 🚧, điền khi build tới.

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

**Đang chờ user chạy Bước 2.** Prompt đã soạn xong (`02-hoan-thien-y-tuong/README.md`), đã giao cho user mang sang Chat. Nhận kết quả về thì lưu `example/docs/02-prd.md`, viết mục *Ví dụ* của Bước 2, ghi mục *Prompt này từng hụt chỗ nào*, rồi commit tách đôi.

Prompt Bước 2 soạn theo đúng khung đã sửa ở Bước 1 (khối *Cách làm việc* bắt AI dẫn, tự xuất case study + rút lỗi ở cuối). Thêm 2 thứ riêng của bước này: câu 4 bắt chọn ra **tính năng nào không có thì app vô nghĩa**, câu 6 bắt kể **ít nhất 4 ranh giới**. Cả hai chưa chạy thật lần nào — chạy xong nhớ xem có hụt không.

Sau đó: user sẽ gửi nội dung sơ cho Bước 4, 5, 6.

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

### 4.3 Giọng văn

Tiếng Việt đời thường, xưng "mình" / "anh em" như bài gốc trên X. Câu ngắn. Không sáo. Bảng khi so sánh, blockquote cho ghi chú đáng nhớ. Mỗi bước kết bằng một câu dẫn sang bước sau.

**Dấu gạch dài: chỉ dùng en dash `–` (U+2013), không dùng em dash `—` (U+2014)** — luật gốc nằm trong `CLAUDE.md`.

> 🔴 **NỢ – VIỆC ĐẦU TIÊN NÊN LÀM KHI QUAY LẠI.** Đếm 08-06: **80 chỗ đang dùng em dash sai luật**, rải khắp repo (01: 21 · example/docs: 18 · README: 11 · HANDOFF: 10 · 02: 9 · example/README: 7 · 03: 3 · CLAUDE.md: 1). Phần lớn do chính mình viết vào mấy phiên gần đây, không phải bài cũ.
>
> ⚠️ **ĐỪNG replace-all mù.** Có chỗ phải GIỮ em dash: dòng phát biểu luật trong `CLAUDE.md` và dòng ngay trên đây — chúng phải in ra ký tự em dash làm ví dụ, thay đi là luật tự mâu thuẫn. Cách an toàn: bỏ qua `CLAUDE.md` và mục 4.3 này khi thay, quét 6 file còn lại.

## 5. Git

Remote `origin` = GitHub, branch `main`. Xong việc là commit + push ngay, đừng để commit nằm im ở local.
