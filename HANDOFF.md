# HANDOFF – build-on-arc

> File làm việc, không phải nội dung cho người đọc series. Mở máy mới thì đọc file này trước.
> **Cập nhật:** 2026-08-06

---

## 0. Repo này là gì

Series hướng dẫn build app trên Arc network, viết cho người Việt không rành crypto và không có nền lập trình. Mỗi bước = 1 thư mục = 1 `README.md`. Nội dung gốc là loạt bài **"Build on Arc bằng Claude Code"** đăng trên X của [@0xhieuxyz](https://x.com/0xhieuxyz) — repo này là bản có nhà, vì X thì bài chết sau 48 giờ.

- GitHub: https://github.com/KattyFury/build-on-arc (public)
- Thư mục local: `D:\Files\Claude\build_on_arc\build-on-arc`

## 1. Đang ở đâu

| Bước | Thư mục | Trạng thái |
|---|---|---|
| 1. Lên ý tưởng | `01-ideation/` | ✅ xong — 4 câu (định hướng Arc · vấn đề thật · dẫn đầu hay cạnh tranh · khả thi) + prompt + ví dụ EZwallet |
| 2. Hoàn thiện ý tưởng | `02-hoan-thien-y-tuong/` | ✅ xong — 6 câu PRD + core value + phép test bỏ tên sản phẩm + ví dụ EZwallet |
| 3. Plan chi tiết | `03-planning/` | ✅ xong — prompt Senior Product Consultant (hỏi từng nhóm một) + ví dụ EZwallet |
| 4. Wireframe | `04-wireframe/` | ❌ chưa có |
| 5. Setup môi trường | `05-setup/` | ❌ chưa có |

Working tree sạch, đã push hết. Commit cuối: `c049238`.

## 2. VIỆC TIẾP THEO — Bước 4 (wireframe)

**Đang chờ user paste nội dung Tập 4 từ series X**, giống cách đã làm với Tập 3.

Vì sao chờ chứ không tự viết: bản của user có mấy câu là trải nghiệm thật ("token hết nhanh khủng khiếp", "AI làm chứ chẳng phải anh em làm") — viết hộ sẽ ra giọng generic, mất đúng thứ làm series này đáng đọc. Cách làm đã chạy ổn ở Bước 3: **user paste bài gốc → giữ nguyên luận điểm + giọng văn của user, chỉ thêm phần ví dụ EZwallet và mấy chỗ làm rõ cơ chế.**

Sau Bước 4 thì tới Bước 5 (setup môi trường) — README ghi rõ cần **2 bản: dùng Terminal và không cần Terminal cho newbie**.

## 3. QUY ĐỊNH — đọc trước khi viết bước mới

### 3.1 Ví dụ xuyên suốt (đã ghi trong `README.md`, mục "Quy định")

Mọi bước dùng **chung một ví dụ duy nhất là EZwallet**. Đây là quy định, không phải gợi ý:

- Mỗi bước có **đúng một** mục ví dụ, tên `## Ví dụ: ...`, đặt ngay sau phần lý thuyết.
- Ví dụ phải **nối tiếp** kết quả EZwallet ở bước trước, không dựng lại từ đầu, không đổi sang sản phẩm khác.
- **Chỉ nói những gì EZwallet làm thật.** Cần dẫn chứng thì lấy từ repo ezwallet, không tự chế con số.

Lý do: người đọc chỉ nạp bối cảnh một lần rồi theo tới cuối, và EZwallet là sản phẩm chạy thật nên mọi câu trong ví dụ đều kiểm chứng được.

### 3.2 Lấy dữ kiện EZwallet ở đâu

Repo: https://github.com/KattyFury/ezwallet (public, MIT). Trên máy này nằm ở `D:\Files\Claude\build_on_arc\ezwallet`.

| Cần gì | Đọc file nào |
|---|---|
| Fact sheet, guardrails, câu hỏi khó | `PITCH.md` |
| Trạng thái kỹ thuật thật, quyết định đã chốt, gotcha | `HANDOFF.md` |
| Tính năng, stack, giới hạn | `README.md` |
| Mô hình custody, điểm yếu đã biết | `SECURITY.md` |

**Cách viết ví dụ cho bước mới:** đừng bịa câu hỏi rồi bịa câu trả lời. Lấy **quyết định có thật** trong repo ezwallet rồi dựng ngược lại thành tình huống đã sinh ra nó. Bước 3 làm đúng kiểu này — `GAS_RESERVE_USDC = 1`, luật gộp "bản mới nhất thắng", `idempotencyKey`, "đọc hỏng thì hiện `…` chứ không vẽ 0" đều là code thật.

### 3.3 ⚠️ Guardrail về EZwallet — nói sai là mất uy tín

- **KHÔNG gọi EZwallet là "self-custody" hay "non-custodial"** kiểu tuyệt đối. Đúng là **user-controlled**: khoá do Circle MPC giữ, user ký bằng PIN. (Đã từng sai chỗ này ở Bước 2, sửa rồi — xem `PITCH.md` mục 7 guardrail #3.)
- **Luôn kèm chữ Arc Testnet** khi nhắc tới tiền. Tiền test, không có giá trị thật.
- **Không chế số liệu** người dùng / TVL / số giao dịch.
- **Chưa audit** — không nói đã audit.
- **Chưa được shill tính năng sao lưu danh bạ** cho tới khi test xong trên máy thật (xem mục 5).

### 3.4 Giọng văn

Tiếng Việt đời thường, xưng "mình"/"anh em" như bài gốc trên X. Câu ngắn. Không sáo. Bảng khi so sánh, blockquote cho ghi chú đáng nhớ. Mỗi bước kết bằng một câu dẫn sang bước sau ("Xong bước này mới qua Bước N…").

## 4. Git

Remote `origin` = GitHub, branch `main`. Mở máy khác:

```bash
git clone https://github.com/KattyFury/build-on-arc.git
```

Xong việc là commit + push ngay, đừng để commit nằm im ở local.

## 5. Việc còn nợ ở repo KHÁC (ezwallet) — đừng quên

Không thuộc repo này nhưng đang treo, và nó chặn mục 3.3 gạch cuối:

**Sao lưu danh bạ bằng auth chữ ký PIN đã code + deploy + bật KV xong (08-06), còn đúng 1 việc cần MÁY THẬT:** mở ezwallet.cash trên điện thoại, đăng nhập bằng PIN, xem Console có dòng đỏ `[sync] địa chỉ recover từ chữ ký KHÔNG khớp ví đang mở` không.

- Không có dòng đó → xong, sao lưu chạy thật, và mục 3.3 gạch cuối được gỡ.
- Có → chốt an toàn đã bắt được, sao lưu tự tắt, app không hỏng gì, cần đổi cách verify ở `functions/api/sync.js`.

Chi tiết đầy đủ: `HANDOFF.md` của repo ezwallet, mục 9 việc 2 + checklist mục 3.
