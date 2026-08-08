# HANDOFF – build-on-arc

> File làm việc của tác giả, không phải nội dung cho người đọc series. Mở máy mới thì đọc file này trước.
> Luật cho Claude Code nằm ở `CLAUDE.md`. File này ghi **đang ở đâu** và **quy định viết bài**.
> **Cập nhật:** 2026-08-07 (giữa phiên — user phải đi công việc, đọc kỹ mục 3 trước khi làm gì tiếp)

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
| Dự án mẫu | `example/` | Spec/design xong (docs 01-05). Code: forked, đang setup backend — xem mục 3 |

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

**08-07: Bước 1-6 đều có README xong** (1,2,3,5 XONG TRỌN kể cả ví dụ; 4 thiếu ví dụ; 6 chưa có ví dụ vì chưa code xong). Cả 2 commit đã push lên GitHub (`593900d`, `261ed53`).

**Bước 6, setup backend cho TapTip — ĐÃ XONG hết phần hạ tầng, sẵn sàng code Giai đoạn 1:**

1. ✅ Fork `circlefin/arc-p2p-payments` → `KattyFury/arc-p2p-payments` → code nằm ở `example/app/` (giữ `LICENSE` Apache-2.0 + `ORIGINAL-README.md` để attribution).
2. ✅ Đối chiếu code sample app với spec — 4 chỗ lệch cần sửa ở Giai đoạn 1: (a) sample dùng tìm-người-nhận, TapTip cần **quét QR** — build mới hoàn toàn; (b) sample có bottom nav, wireframe TapTip **không có**, dùng icon menu (☰); (c) chưa có nút Random (nice-to-have, làm cuối); (d) kiểm tra luồng Nạp có link Circle Faucet theo đúng wireframe chưa.
3. ✅ Backend: giữ **Supabase Cloud**, không đổi Cloudflare KV (lý do: đổi KV mất phần lớn giá trị của việc fork — viết lại auth + data layer + realtime).
4. ✅ Supabase project **`taptip`** (ref `kekdoqyehyozqvuhwsoh`) đã tạo + **migrations đã push xong** (verify: bảng `profiles`/`wallets`/`transactions` có thật). Cách push: KHÔNG dùng được `supabase link` (bug CLI 2.112.0 parse ngày `+00:00`) — dùng thẳng Management API `POST /v1/projects/{ref}/database/query` với toàn bộ SQL nối lại, hiệu quả hơn.
5. ✅ **Circle: đã có account MỚI (08-08)** — account cũ có Entity Secret active từ trước không rõ nguồn gốc (không phải từ ezwallet, không tìm ra recovery file cũ), nên tạo account khác cho sạch thay vì cố reset. Entity Secret mới đã sinh + đăng ký thành công qua SDK (`generateEntitySecret` + `registerEntitySecretCiphertext`).
6. ✅ Vá lỗ hổng của sample app gốc: `app/api/wallet-set/route.ts` import `@/lib/utils/developer-controlled-wallets-client` nhưng file này KHÔNG tồn tại trong repo gốc, package `@circle-fin/developer-controlled-wallets` cũng thiếu trong `package.json`. Đã cài package + tự viết file client (`initiateDeveloperControlledWalletsClient`).
7. ✅ `example/app/.env.local` đầy đủ Supabase + `CIRCLE_API_KEY` + `CIRCLE_ENTITY_SECRET` (KHÔNG commit, đã confirm gitignore). **Recovery file lần này: `C:\tmp\taptip-entity-secret-recovery2\recovery_file_....dat` — PHẢI backup ra chỗ khác an toàn hơn `C:\tmp` (dễ bị dọn mất), chưa làm.**
8. ✅ `npm run dev` chạy thành công, `/sign-in` trả 200, không lỗi runtime — xác nhận app sống được với backend thật.
9. ⚠️ `npm run build` (production) lỗi type ở `app/api/webhooks/circle/route.ts:232` — bug có sẵn của sample app gốc (Supabase query thiếu field `status` trong select nhưng code vẫn đọc), KHÔNG liên quan gì đến phần mình sửa. Chưa fix — không chặn `npm run dev`, để dành sửa khi đụng tới file đó ở Giai đoạn 1.
10. ✅ **Client Key** tạo xong (Web, Allowed Domain `localhost`), điền `NEXT_PUBLIC_CIRCLE_CLIENT_KEY` vào `.env.local`. `npm run dev` chạy lại, `/sign-in` trả 200 — **đủ credentials, backend hoàn chỉnh.**
11. Dọn rác: `C:\tmp\taptip-supabase-dbpass.txt`, `C:\tmp\taptip-entity-secret-recovery\` (recovery file entity secret CŨ, account cũ — không dùng được, xoá luôn), `C:\tmp\register-entity-secret.mjs` — chưa dọn. Recovery file MỚI (`C:\tmp\taptip-entity-secret-recovery2\`) — chưa backup ra chỗ an toàn hơn.

**08-08: Tính năng 1 (Home) ĐÃ XONG VÀ VERIFY THẬT** — không chỉ "chắc là được", có bằng chứng từ log server: `POST /api/setup-wallets 201` (tạo ví qua passkey thành công) → `GET /dashboard 200` → `POST /api/wallet/balance 200` (Home tự fetch balance). Toàn bộ pipeline auth (email OTP) → passkey → ví → Home chạy thật end-to-end.

Trong lúc làm Tính năng 1 còn phát hiện + sửa thêm: sign-in gốc dùng phone+SMS (đổi sang email), Supabase free tier chặn custom email template (cấu hình Gmail SMTP qua Management API để giữ đúng OTP gõ tay thay vì magic link — xem `example/docs/06-build.md`), thiếu Passkey Domain Config trên Circle Console (khác với Client Key's Allowed Domain, phải cấu hình riêng ở mục Modular Wallets → Configurator → Passkey), lỗi tự gây (`useRouter` sót lại sau khi xoá import — bài học: chạy `tsc --noEmit` NGAY sau mỗi lần sửa, không gộp lại). Rebuild lại layout sign-in/code-confirmation/passkey-setup theo đúng grid wireframe thay vì giữ style mặc định sample app.

**08-08: Tính năng 2 (quét QR gửi tiền) — code xong, CHƯA test tay bằng camera thật.** `components/send-flow.tsx` mới: popup chọn số tiền (preset lưu localStorage, xoá có confirm, thêm số tuỳ ý) → quét QR (`html5-qrcode`, camera + upload ảnh) → loading → success tự tắt sau 2s. Tái sử dụng `sendUSDC()` có sẵn trong `web3-provider.tsx` (đã đúng chuẩn skill: `sendUserOperation` + `paymaster: true` — không viết lại). Nối vào nút "Tip" ở Home.

**Đơn giản hoá có chủ đích:** số tiền hiển thị thẳng bằng USDC, CHƯA làm quy đổi VNĐ như PRD nhắc tới (`example/docs/02`) — để dành Giai đoạn 2 vì cần tỷ giá thật, không hardcode.

Type-check sạch, dev server compile "/dashboard" thành công không lỗi runtime (log tự bắt được vì tab đang mở fast-refresh). **Chưa tự tay bấm thử camera quét QR thật** — cần user test.

**08-08: Tính năng 3, 4, 5 — code xong luôn trong 1 mạch, CHƯA test tay:**
- **Tính năng 3 (Nạp/Rút):** menu Home tách 2 nút riêng. "Nạp" tự copy địa chỉ ví + hướng dẫn 3 bước + nút mở Circle Faucet. "Rút" hiện thông báo "chưa khả dụng" + nút "Đã hiểu". Bỏ hẳn `WalletBalance` component cũ khỏi menu (trùng chức năng).
- **Tính năng 4 (Lịch sử):** sửa `components/transactions.tsx` — đổi nhóm theo THÁNG (code gốc) sang nhóm theo **NGÀY** đúng spec, thêm màu đỏ/xanh theo chiều gửi/nhận (trước đó chỉ có dấu +/- không màu). Coi đây là yêu cầu chức năng (phân biệt luồng tiền), không phải thẩm mỹ, nên sửa dù đang ở Giai đoạn 1.
- **Tính năng 5 (Random):** `SendFlow` thêm prop `initialAmount` — có giá trị thì nhảy thẳng vào bước quét QR, bỏ qua bước chọn số tiền. Nút "Ngẫu nhiên" ở Home tự random 0.1–5 USDC (không vượt quá balance) rồi mở `SendFlow` với amount đó.

**GIAI ĐOẠN 1 CODE XONG CẢ 5 TÍNH NĂNG.** Type-check sạch sau mỗi bước, dev server compile không lỗi (kể cả tab thật đang mở tự fast-refresh qua `/dashboard`). Chỉ Tính năng 1 được verify đầy đủ qua log thật (passkey → ví → balance) — Tính năng 2-5 mới dừng ở "code chạy được, không lỗi compile/runtime khi load", CHƯA test tay từng thao tác (bấm nút, quét QR thật, nạp thật, xem lịch sử thật, random thật).

**Việc kế tiếp khi quay lại:** user test tay toàn bộ 5 tính năng, báo lỗi nếu có. Sau khi user xác nhận OK hết mới coi Giai đoạn 1 thật sự xong, chuyển qua Giai đoạn 2 (giao diện, đưa nguyên `docs/04-wireframe.md` áp đồng loạt cho mọi màn — xem mục 4.7). Dọn rác file tạm ở mục 11 phía trên vẫn chưa làm.

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

## 4.6 🔴 BẮT BUỘC đọc trước khi đụng Circle/Arc — đừng tự mò

Trước khi viết bất kỳ code nào đụng tới Circle Wallets hoặc Arc, **load đúng skill/tài nguyên tương ứng trước, đừng tự mò qua docs search rồi thử-sai**. Bài học đau: mất cả buổi vật lộn Entity Secret + Passkey Domain + WebAuthn error vì không load skill `circle:use-modular-wallets` trước khi code — skill đó có sẵn bảng lỗi + rule "ALWAYS complete Console Setup (client key, passkey domain, client URL) before using SDK" ngay từ đầu.

- **Circle Modular Wallets (Passkey, gasless)** → load skill `circle:use-modular-wallets` TRƯỚC. Có bảng lỗi đầy đủ (`NotAllowedError`, `SecurityError`, mã lỗi 155xxx, AA-series), rule bắt buộc (paymaster:true, transport URL path đúng chain, không dùng trên Ethereum mainnet/Solana/Aptos/NEAR).
- **Circle Developer-Controlled Wallets (Entity Secret)** → load skill `circle:use-developer-controlled-wallets` TRƯỚC.
- **Bất kỳ thứ gì khác của Circle** (USDC, Gateway, swap, bridge...) → xem danh sách skill đầy đủ tại https://docs.arc.io/ai/skills, cài qua `/plugin marketplace add circlefin/skills`.
- **Câu hỏi chung về Arc** → Arc MCP đã connect (`docs.arc.io/mcp`), dùng `search_arc_docs`/`query_docs_filesystem_arc_docs` trước khi đoán. Index đầy đủ: https://docs.arc.io/llms.txt.

## 4.7 🔴 Tiêu chí "xong" ở Giai đoạn 1 — đừng lo giao diện

Khi build `example/app` (hoặc bất kỳ dự án nào đang ở Giai đoạn 1 của Bước 6): một tính năng coi là XONG khi **nút bấm đúng vị trí mong muốn + flow chạy đúng** — hết. Không tự ý chỉnh màu, spacing, font, bo góc "cho đẹp hơn chút" giữa lúc đang làm logic. Home (Tính năng 1) đã lỡ làm hơi kỹ styling — không sai nhưng không nên lặp lại, tốn thời gian đáng lẽ dồn cho Giai đoạn 2 làm một lượt nhanh hơn nhiều (đưa nguyên spec `docs/04-wireframe.md` qua một lần, đồng bộ toàn bộ màn thay vì sửa lắt nhắt từng cái).

## 5. Git

Remote `origin` = GitHub, branch `main`. Xong việc là commit + push ngay, đừng để commit nằm im ở local.

## 6. Tools tham khảo – dùng ở Bước 6 (code UI thật), KHÔNG dùng ở Bước 4

Bước 4 (wireframe) cố tình bỏ hết style, chỉ khung + label chức năng – mấy tool dưới đây đều thuộc chuyện style/component thật nên chỉ có ích lúc code, không có ích lúc vẽ khung.

- **21st.dev** – https://21st.dev/ – marketplace React+Tailwind, prompt sẵn cho Claude Code/Cursor/v0
- **Astryx (Meta)** – https://astryx.atmeta.com/ – design system chính thức Meta, React 19 + StyleX, 160+ component – hơi nặng đô cho app nhỏ như `example/`
- **Magic UI** – https://magicui.design/ – component + animation React+Tailwind
- **ui-ux-pro-max-skill** – https://github.com/nextlevelbuilder/ui-ux-pro-max-skill – AI skill sinh design system (màu, font, style) theo project, 114,271 sao (verify qua GitHub API 08-07, số thật cao hơn số đồn)
- **taste-skill** – https://github.com/Leonxlnx/taste-skill (site: tasteskill.dev) – skill chống AI sinh UI "generic slop", 73,405 sao (verify qua GitHub API 08-07)
