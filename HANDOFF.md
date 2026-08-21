# HANDOFF – build-on-arc

> File làm việc của tác giả, không phải nội dung cho người đọc series. Mở máy mới thì đọc file này trước.
> Luật cho Claude Code nằm ở `CLAUDE.md`. File này ghi **đang ở đâu** và **quy định viết bài**.
> **Cập nhật:** 2026-08-21 (thêm Vòng 2 "chốt stack cho từng luồng" vào Bước 3, đã chạy khô + sửa 6 chỗ hụt; còn nợ một lượt chạy THẬT. Trước đó: 08-11, 8 fix UI Home + fix bug balance=0, đã push, repo sạch)

## 🚧 08-21: THÊM VÒNG 2 VÀO BƯỚC 3 – CHỐT STACK CHO TỪNG LUỒNG

Thesis của user: bắt AI liệt kê stack dùng cho mỗi luồng, vì sao chọn tech đó, còn tech nào khác làm được và vì sao không dùng. Series trước đó không có chỗ nào chốt stack – Bước 3 chỉ hỏi về sản phẩm, Bước 5 nhảy thẳng vào cài Node/Git/MCP như thể stack đã có sẵn.

Đã làm: `03-planning/README.md` tách thành **Vòng 1** (phỏng vấn ngược, y như cũ) + **Vòng 2** (chốt stack) – lý thuyết, prompt Solution Architect, bảng 4 dấu hiệu câu trả lời dỏm. Cập nhật bảng ở `README.md`.

**Đã chạy khô ngay sau đó (08-21):** đem prompt Vòng 2 chạy lại với spec TapTip, Claude Code đóng cả hai vai (vừa hỏi vừa trả lời). Kết quả: ghép từng mảnh thì ra trúng stack thật (Next.js + Supabase + Circle Modular Wallets + html5-qrcode + qrcode.react + viem, khớp `example/app/package.json`), NHƯNG không đường nào ra được quyết định thật là fork nguyên `arc-p2p-payments` – vì prompt hỏi sample app theo từng luồng nên chỉ ra mảnh lẻ. Lòi ra **6 chỗ hụt**, đã sửa hết vào prompt và ghi thành bảng "Vòng 2 – 6 chỗ" trong `03-planning/README.md`: (1) không chốt danh sách luồng trước, (2) khung dùng chung bị quyết lén trong luồng đầu, (3) hỏi sample app theo luồng thay vì hỏi cái bao nhiều luồng, (4) ép đủ 2 phương án cho mọi luồng đẻ ra rác, (5) không có ô "bản đầu chưa làm", (6) quên hỏi ràng buộc môi trường (HTTPS/domain phải khai báo/quyền thiết bị).

Bằng chứng "cái giá của fork" dùng trong bài, đã verify: `example/app/package.json` có `openai`, `pdf-parse`, `mammoth`, `millify`, cả `viem` lẫn `web3` – grep `app/ components/ lib/` không file nào import chúng.

🔴 **NỢ CÒN LẠI:** vẫn chưa có lượt chạy THẬT (người thật ngồi trả lời trong Chat, không biết trước đáp án). Mục ví dụ vẫn để 🚧, ghi rõ trong README là "chạy khô". Chạy thật xong thì đổi tiêu đề mục đó và bổ sung chỗ hụt mới nếu có.

---

## ✅ 08-11: 8 FIX UI + 2 BUG – ĐÃ XONG HẾT, ĐÃ PUSH

**8 fix UI đã code + verify bằng route preview tạm (Chrome headless, đã xoá sau khi chụp) + push (`9c1bbb8`):** bỏ "your" ở tiêu đề Add to Home Screen, tách riêng bước iOS (Safari)/Android (Chrome) theo user agent, Balance đổi format `Balance: $XXXX` 4 chữ số độ rộng cố định (số 0 dẫn đầu vô hình chứ không ẩn hẳn – tránh cụm nhảy vị trí khi số dư đổi), câu chú thích QR tách 2 dòng, icon Random to bằng icon Back, nút Tip đổi icon sang `Icon.Tip` (nguồn `D:\Files\Claude\icons\tip.svg`, đã xoá `Icon.Send` cũ vì hết chỗ dùng), mảng tròn trang trí góc trái-dưới chuyển vào trong hàng 10 + `overflow-hidden` + đổi đơn vị px cứng sang cqh (hết lấn hàng 9), vùng bấm icon Menu tăng bằng kỹ thuật padding + margin âm, popup Menu redesign toàn bộ (đổi tên thành "Menu", thêm Account + Address rút gọn kèm nút copy, Deposit/Withdraw chung hàng, Tip History riêng, Sign out chữ đỏ `text-destructive`, nút Close đổi từ chữ sang icon X góc phải-trên – bấm ra ngoài popup vốn đã tự đóng sẵn qua Radix, không cần sửa gì thêm).

**✅ Bug "Balance luôn hiện 0" – ĐÃ SỬA + VERIFY THẬT (`04a057c`).** Kiểm tra bằng Supabase Management API + gọi thẳng `/api/wallet/balance`: DB có balance thật, API cũng trả số thật (80 USDC lúc kiểm tra) – tầng server/DB hoàn toàn khoẻ, bug nằm ở kiến trúc client. Root cause: `useWalletBalances()` chỉ fetch khi `isConnected === true` từ `Web3Context` (`components/web3-provider.tsx`) – mà `isConnected` chỉ bật sau khi TOÀN BỘ pipeline WebAuthn/passkey phía client (load credential → `toWebAuthnAccount` → `toCircleSmartAccount` → `createBundlerClient`) chạy xong không lỗi. Bất kỳ trục trặc nào trong chuỗi đó chỉ bị `console.error` nuốt mất, số dư kẹt vĩnh viễn ở 0, không bao giờ báo cho user. **Sửa:** `useWalletBalances(knownAddress?)` giờ ưu tiên fetch thẳng bằng `primaryWallet.wallet_address` (đã biết sẵn từ server, không phụ thuộc WebAuthn) thay vì chờ `account.address` từ Web3Context. `HomeScreen` tự mở một `BalanceProvider` riêng mang địa chỉ thật, che lên `BalanceProvider` gốc ở `app/layout.tsx` (gốc không có địa chỉ nên không làm gì, các chỗ khác không bị ảnh hưởng). Verify bằng route preview tạm (đã xoá): balance hiện đúng 80 USDC ngay khi mount, không cần đợi passkey kết nối xong.

**✅ Câu hỏi "sao Lịch sử có giao dịch dù ví mới tạo" – ĐÃ TRẢ LỜI, không phải bug.** Query thẳng DB: chỉ có đúng 1 ví trong bảng `wallets`, tạo lúc **2026-08-08** (không phải mới), có 6 giao dịch từ 08-08 đến 08-11 hôm nay. Lý do: Circle Modular Wallets/passkey trả về ĐÚNG MỘT địa chỉ ví cố định gắn với passkey đó (deterministic) – đăng nhập lại bằng cùng passkey/tài khoản test từ các phiên trước sẽ luôn ra lại ví cũ đó, không phải ví mới. Đây là ví test đã dùng xuyên suốt từ lúc build Tính năng 1-5 (08-08), không phải hiện tượng lạ.

## 🟢 TRẠNG THÁI NGHỈ 08-11 (trước đó) – đọc trước khi làm gì tiếp

**Repo sạch, `git status` không còn gì.** Link thật đang chạy đúng: https://taptip.kattyfury1403.workers.dev

**Luồng đăng nhập email đã thông suốt lại sau bug nặng nhất session này** (xem mục "BUG MAGIC LINK THAY VÌ OTP" ngay dưới) – OTP gửi đúng mã 6 số, verify thật qua API.

**Dev server đang chạy sẵn** trên máy Dell (`localhost:3000`, PID có thể đổi mỗi lần restart) – nếu tắt rồi mở lại phiên mới thì nhớ `npm run dev` lại trong `example/app`, đã 3 lần user hỏi "sao không chạy local" vì bị tắt sau mỗi lần build production (Next 16 khoá không cho `dev` và `build` chạy cùng lúc trên 1 project).

**3 việc còn treo, chưa ai làm, không khẩn:**
1. Key Resend `RESEND_API_KEY_ADMIN` (Full access) đang KHÔNG dùng cho SMTP nữa (đã đổi sang key Sending access riêng) – an toàn, không phải nợ nữa.
2. `public/logo.png` (logo tay vẽ cũ) không còn code nào tham chiếu – an toàn xoá, để user tự quyết.
3. Guide series (ngoài phần code TapTip): Bước 4 thiếu mục Ví dụ, Bước 6 Giai đoạn 3 (phần viết cho người đọc, khác với code) vẫn "đang chạy" theo bảng trạng thái mục 1 – chưa có ai viết.

**Nếu quay lại làm tiếp:** đọc thẳng mục "BUG MAGIC LINK THAY VÌ OTP" để hiểu bài học PATCH Supabase (không merge từng phần, luôn gửi đủ cụm field liên quan) trước khi đụng vào `config/auth` lần nữa.

## 🔴 BUG MAGIC LINK THAY VÌ OTP (08-11)

**Hậu quả trực tiếp của bug PATCH-xoá-sạch đã ghi ở mục dưới:** lúc sửa `smtp_pass` bằng PATCH chỉ gửi 1 field, Supabase không chỉ xoá `smtp_host/port/user/email` mà còn **xoá luôn `mailer_templates_magic_link_content`** (template email tuỳ chỉnh chứa `{{ .Token }}` cấu hình từ Bước 6) – email OTP tự động rơi về template mặc định của Supabase, vốn chỉ có nút bấm "Sign in" trỏ `{{ .ConfirmationURL }}`, không hề in mã số. Đây chính là lý do màn code-confirmation (nhập 6 số) không nhận được mã – **toàn bộ luồng đăng nhập email bị hỏng từ lúc đó, không phải do chạy local.**

**Đã khôi phục:** `PATCH .../config/auth` với `mailer_subjects_magic_link` + `mailer_templates_magic_link_content` in `{{ .Token }}` rõ ràng (không còn link bấm). Verify bằng cách gọi thẳng `POST /auth/v1/otp` qua API – thành công (không phải chỉ tin build/log).

**Bài học nhắc lại lần 2 (đã note ở mục dưới nhưng vẫn dính):** PATCH endpoint `config/auth` của Supabase Management API **không merge từng phần** – mỗi lần PATCH phải tự biết field nào cùng "cụm" với field mình sửa rồi gửi đủ cả cụm, nếu không cụm còn lại tự về `null`/mặc định. Đã tự kiểm tra lại toàn bộ SMTP + mailer_template sau lần PATCH thứ 2 để chắc không bị xoá tiếp – cả hai còn nguyên.

**User tự tạo key Resend "Sending access" mới** (đúng khuyến nghị ở mục dưới) – đã swap vào `smtp_pass`, key sending CŨ (`re_QgAaW3c1...`, bị invalid) không còn dùng. `.env.local` đã cập nhật.

**Rate limit email tăng tiếp 30 → 100/giờ** vì lúc debug tốn nhiều lượt gửi test (`diag-test-taptip*@resend.dev`) suýt dính rate limit thật giữa chừng.

**2 fix UI nhỏ theo phản hồi màn "Enter the code sent to":**
- Dòng email hiển thị dưới tiêu đề đang thừa hưởng `text-title` (to ngang header) vì `title` nhận cả cụm `<>...<br/><span>{email}</span></>` – thêm `text-lead` riêng cho span email, không đè `text-title` nữa.
- Ô nhập 6 số OTP (`components/ui/input-otp.tsx`) vẫn ở size cũ trước khi `Field` được tăng (`4.3cqh`/`min 34px`, font `text-body`) – đồng bộ lên khớp `Field` mới: `6cqh`/`min 48px`, font `text-lead`.

Đã build + deploy lại lên Cloudflare, verify OTP send thật qua API thành công.

## 🔴 BUG RESEND KEY + CANH GIỮA (08-10)

**Bug nghiêm trọng đã sửa: mọi email OTP fail 100%, không do chạy local.** User hỏi "Error sending magic link email có phải do chạy local" – **không phải**, việc gửi mail xảy ra hoàn toàn ở server Supabase, độc lập máy client. Chẩn đoán bằng cách gọi thẳng `POST /auth/v1/otp` qua API, tái hiện lỗi `500 unexpected_failure`, rồi test trực tiếp `RESEND_API_KEY_SENDING` với chính API Resend → trả về **`"API key is invalid"`** – key gửi mail bị hỏng/vô hiệu ngay từ đầu (không rõ lý do, có thể user đưa nhầm hoặc key bị revoke phía Resend). Test `RESEND_API_KEY_ADMIN` thì gửi được bình thường.

**Sửa tạm:** đổi `smtp_pass` trong Supabase Auth config sang dùng `RESEND_API_KEY_ADMIN` (đã xác nhận hoạt động) thay vì key sending hỏng. **Nợ kỹ thuật:** đang dùng key Full-access cho việc gửi mail hàng ngày, không đúng nguyên tắc least-privilege – nên tạo key "Sending access" MỚI trên Resend dashboard rồi thay lại khi rảnh.

**Bug thật thứ 2 phát hiện giữa chừng: PATCH config Auth của Supabase KHÔNG merge từng phần cho khối SMTP.** Gọi `PATCH .../config/auth` chỉ với `{"smtp_pass": "..."}` (tưởng chỉ đổi 1 field) đã xoá sạch luôn `smtp_host`/`smtp_port`/`smtp_user`/`smtp_admin_email` về `null`! Phải gửi lại TOÀN BỘ field liên quan SMTP trong 1 lần PATCH mới khôi phục đúng. Bài học: PATCH endpoint này không an toàn để sửa "một field", luôn gửi đủ cụm liên quan.

**2 fix UI theo phản hồi user, đã đo bằng `getBoundingClientRect()` thật trước khi sửa:**
- Danh sách 4 bước ở màn "Add to Home Screen": đo được box đã canh giữa tuyệt đối (margin trái phải bằng nhau 55px/55px) nhưng do box rộng full 320px nên chữ (left-align) bắt đầu quá xa tâm màn hình, nhìn lệch trái dù box thì giữa. Sửa: `app/page.tsx`, đổi `<ol>` từ `w-full` sang `w-fit` – box tự co theo dòng dài nhất, `items-center` của `Screen` tự canh giữa. Đo lại: box co còn 227.6px, margin vẫn bằng nhau tuyệt đối (101.2px/101.2px), chữ dồn gần tâm hơn hẳn.
- Ô nhập liệu `Field` (dùng chung sign-in + onboarding): chữ đặt giữa ô trông kỳ, đổi `text-center` → `text-left`.

Đã build + deploy lại lên Cloudflare, verify OTP send thành công thật qua API + verify UI bằng screenshot.

## ✅ ICON BACK + FIELD TO HƠN (08-10)

User phản hồi trên màn "Enter your email to get started": icon nút Quay lại nhỏ, ô nhập email nhỏ. Cả hai đều sửa tại `components/screen.tsx` nên tự động áp dụng đồng bộ cho mọi màn dùng chung (`Field` cũng dùng ở `onboarding`, `BackIcon` dùng ở mọi `BackAction`):
- `BackIcon`: `w-[2cqh] h-[2cqh]` → `w-[3cqh] h-[3cqh]` (tăng 50%).
- `Field`: `h-[4.3cqh] min-h-[36px]` → `h-[6cqh] min-h-[48px]`; `px-3` → `px-4`; font đổi hẳn từ `text-body` sang `text-lead` (to hơn mức tăng chung đã làm trước đó, vì user gọi riêng ô nhập liệu ra là còn nhỏ).

Đã build + deploy lại lên Cloudflare, verify bằng screenshot thật.

## ✅ VỊ TRÍ NỘI DUNG + FONT SIZE (08-10)

**User yêu cầu dời nội dung màn "Add TapTip to your Home Screen" xuống vị trí hàng 3/10, và xác nhận áp dụng luôn cho mọi màn khác dùng chung `Screen`.** Sửa tại nguồn: `components/screen.tsx` – vùng nội dung (2.5→8.0) có thêm spacer cao `3.2cqh` trước `{children}` (cộng với `gap-[1.8cqh]` có sẵn = đúng 5cqh = 0.5 hàng), đẩy nội dung thật sự bắt đầu ở vạch hàng 3.0 thay vì 2.5 – ảnh hưởng toàn bộ màn dùng `Screen` (sign-in, code-confirmation, onboarding, passkey-setup, add-to-home). **Verify bằng đo `getBoundingClientRect()` thật** (dựng ref tạm trong `Screen`, đo xong xoá), kết quả `firstContentChild top row = 3.00` – đúng chính xác ngay lần đầu, không cần chỉnh lại.

**Tăng font toàn app cho dễ đọc với người lớn tuổi** (`app/globals.css`, token dùng chung): `--text-lead` (chữ nút) 21px→24px, `--text-body` (nội dung) 17px→19px, `--text-small` (ghi chú/nhãn nhỏ) 14px→16px. `--text-title`/`--text-figure` giữ nguyên (đã đủ to).

Đã build + deploy lại lên Cloudflare, verify bằng screenshot thật.

## ✅ SKIP PASSKEY + LOGO CHÍNH THỨC (08-10)

**Bug thật: "Skip for now" ở màn passkey-setup lặp vô hạn.** Bản redesign GĐ3 có sẵn nút Skip nhưng chỉ `router.push('/dashboard')` – trong khi `dashboard/page.tsx` tự redirect về `/dashboard/setup-wallet` nếu chưa có `wallet_setup_complete=true` trong `user_metadata`, và `setup-wallet` lại render chính `<PasskeySetup>` → bấm Skip lại → lặp lại từ đầu. **Sửa:** `skipPasskey()` trong `components/passkey-setup.tsx` gọi `supabase.auth.updateUser({ data: { wallet_setup_complete: true } })` trước khi chuyển trang – dùng đúng field mà luồng thật (`app/api/setup-wallets/route.ts`) đã dùng, không bịa field mới. Không có ví thật thì Home tự hiện placeholder "Creating wallet..." (đã có sẵn logic này từ trước).

**Bộ logo/icon chính thức thay cho bản hand-drawn tạm:** user để 3 file gốc ở `D:\Files\Claude\build_on_arc\build-on-arc\items\` (`logo.svg` vuông, `logo-full.svg` có chữ, `PFP.png` cho mạng xã hội – không đụng file này, không phải asset của app). Đã dùng `logo.svg` sinh lại: `public/favicon.svg` (thay bản base64 JPEG cũ sót từ template gốc), `public/icon-192x192.png`, `public/icon-512x512.png`, `app/apple-icon.png` (180×180, file mới, quy ước Next.js tự nhận). `logo-full.svg` đã có sẵn ở `public/` từ bản redesign GĐ3 (khớp byte, không cần sửa) – dùng ở màn Splash.

**Bug thật khi sinh `favicon.ico`:** tool `sharp` sinh PNG qua `.flatten()` (nén nền trắng) làm mất kênh alpha, trong khi Turbopack build-time image processing của Next.js bắt buộc PNG nhúng trong `.ico` phải là RGBA – báo lỗi `The PNG is not in RGBA format!`, build production fail hẳn (không phải chỉ warning). Sửa: thêm `.ensureAlpha()` sau `.flatten()` để ép lại kênh alpha trước khi encode PNG.

**Rác chưa dọn (không xoá tự ý, chỉ ghi lại):** `public/logo.png` (bản hand-drawn cũ) không còn được code nào tham chiếu (Splash đã đổi sang `logo-full.svg`) – an toàn để xoá nhưng để user tự quyết.

Đã build + deploy lại lên Cloudflare, verify 4 file icon trả 200 trên link thật.

## ✅ HẠ TẦNG EMAIL + PASSKEY (08-10, sau khi deploy)

**Passkey lỗi "Invalid credentials" trên link thật:** nguyên nhân là Client Key trong Circle Console vẫn khai Allowed Domain = `localhost` (từ lúc setup ban đầu, xem mục 3 bên dưới) – **khác** với Passkey Domain (Modular Wallets → Configurator → Passkey) mà user đã thêm domain thật vào trước đó. Hai cài đặt này tách biệt hoàn toàn dù cùng nằm trong Circle Console, dễ nhầm là một. User đã tự vào sửa Allowed Domain của Client Key.

**Đổi hạ tầng gửi email OTP: Gmail cá nhân → Resend + domain riêng.** Lý do: mail OTP gửi từ `kattyfury1403@gmail.com` (Gmail cá nhân, cấu hình từ lúc setup Bước 6) nhìn không chuyên nghiệp, dễ bị nghi ngờ phishing. Đã làm (qua API, user chỉ cần tự tạo tài khoản Resend + lấy API key):
- Tạo domain `taptip.0xhieu.xyz` trên Resend (dùng subdomain riêng của domain cá nhân `0xhieu.xyz`, KHÔNG dùng domain gốc – cô lập uy tín gửi mail, khỏi ảnh hưởng domain chính nếu mail test bị đánh spam).
- Thêm 3 DNS record (1 DKIM TXT, 1 SPF MX, 1 SPF TXT) vào Cloudflare zone `0xhieu.xyz` qua API – verify xong gần như ngay lập tức.
- Đổi SMTP config của Supabase (qua Management API) từ Gmail sang `smtp.resend.com`, from address `noreply@taptip.0xhieu.xyz`.
- **2 API key Resend, quyền khác nhau – đừng lẫn:** `RESEND_API_KEY_SENDING` (chỉ gửi mail, dùng làm mật khẩu SMTP) vs `RESEND_API_KEY_ADMIN` (Full access, dùng một lần để tạo/verify domain qua API – không phải bí mật runtime của app).

**Tiện thể sửa luôn rate limit email của Supabase:** `rate_limit_email_sent` đang mặc định = 2 (email/giờ) – **tách biệt với SMTP**, áp dụng dù dùng SMTP riêng hay không, nhiều người tưởng gắn SMTP là hết giới hạn nhưng đây là 2 lớp khác nhau. Đã sửa lên 30 qua Supabase Management API.

**Secrets mới nằm ở `.env.local`, không phải toàn bộ đều là runtime secret của app:**
- `RESEND_API_KEY_SENDING`, `RESEND_API_KEY_ADMIN` – Resend.
- `SUPABASE_ACCESS_TOKEN` – token quyền ADMIN toàn project Supabase (Management API), KHÔNG phải biến app đọc lúc chạy, chỉ lưu lại để dùng cho lần sau khi cần sửa config qua API thay vì bắt user vào dashboard.

## ✅ GIAO DIỆN ENGLISH + FIX UX (08-10)

User yêu cầu đổi hết giao diện sang English (mặc định English, không còn tiếng Việt). Đã đổi toàn bộ string hiển thị ở 11 file (Home, sign-in, code-confirmation, onboarding, passkey-setup, send-flow 4 bước, transactions, chi tiết giao dịch, splash/add-to-home, manifest/layout metadata) + đổi locale ngày giờ từ `vi-VN` sang `en-US`. **Verify bằng script gác cổng, không soát mắt** (đúng luật đã chốt ở dự án khác, áp dụng luôn ở đây): grep toàn bộ `.ts`/`.tsx` tìm ký tự có dấu tiếng Việt, chạy 2 lần (lần 1 lọt sót 1 chuỗi ở `transactions.tsx` do `replace_all` không khớp hết, lần 2 sau khi sửa tay thì sạch 100%).

**Cùng lúc user gửi 8 điểm fix UX, đã làm hết:**
1. Man Add to Home Screen: sửa thành 4 bước (thêm bước "Tap the options menu" trước bước Share).
2. Nút Continue của màn đó chuyển vào đúng hàng 9-10, cao 80% hàng (trước đó dùng pattern cũ `pb-[2vh]` không theo lưới).
3+4. **Áp lưới 10 hàng thật sự** (không phải `flex-1` chung chung) cho `sign-in`, `code-confirmation`, `onboarding`, `passkey-setup`: chia `1 (đệm) + 5 (nội dung, tâm ~hàng 3.5) + 3 (đệm) + 1 (nút, cao 80%)`.
5. Thêm gợi ý domain email (`@gmail.com`, `@icloud.com`) dưới ô nhập ở sign-in – hiện khi đã gõ phần trước `@` mà email chưa hợp lệ, bấm vào là tự điền.
6. Luật độ rộng nút: nút đơn = `w-2/3 mx-auto`; nút đôi (chính/phụ) giữ tỷ lệ 1/3+2/3 đã có sẵn (code-confirmation Back/Continue, home-screen Ngẫu nhiên/Tip) – cả hai đã có margin viền qua `px-5` của layout cha từ trước, không cần thêm.
7. **Bug thật tìm được:** mọi popup (`dialog.tsx`) rộng đúng bằng bề ngang màn hình (`w-full` trên viewport 430px, `max-w-lg`=512px không kích hoạt) → chạm sát lề trái phải. Sửa: `w-[calc(100%-40px)]` khớp quy ước margin 20px dùng khắp app.
8. **Bug thật tìm được – số dư cập nhật chậm:** app có **2 hệ theo dõi số dư tách rời nhau** – `web3-provider.tsx` đọc balance on-chain trực tiếp qua viem và tự refresh ngay sau khi gửi, nhưng **Home screen lại hiển thị balance từ `balanceContext`/`use-wallet-balances.ts`** (đọc cache DB + subscribe Realtime), hệ này không hề được gọi refresh sau khi user tự gửi tiền – chỉ cập nhật khi webhook Circle bắn về, có độ trễ thật. Sửa: `send-flow.tsx` gọi `refreshBalances()` (từ `balanceContext`, không phải từ `web3-provider`) ngay sau khi `sendUSDC` thành công – route `/api/wallet/balance` đọc balance sống từ Circle API nên không phụ thuộc webhook.

**Đã deploy lại lên Cloudflare, verify live bằng Chrome headless đọc DOM thật** (không chỉ tin status code) – `https://taptip.kattyfury1403.workers.dev/sign-in` hiện đúng "Enter your email to get started" / "Send OTP", không còn console error.

**User đã tự thêm domain vào Circle Console → Passkey – việc tay đã xong, đừng nhắc lại.**

**Đã commit + push:** `fb0ad63` (gộp cả code English/UX fix lẫn HANDOFF.md, không tách commit vì đây không phải nội dung hướng dẫn theo bước – xem mục 4.1). Repo sạch, không còn gì chưa lên GitHub tính đến đây.

## ✅ DEPLOY CLOUDFLARE (08-10) – link thật đã chạy, còn 1 việc tay

**Link thật:** https://taptip.kattyfury1403.workers.dev – đã verify bằng Chrome headless đọc được nội dung thật (không chỉ tin status code), `/sign-in` hiện đúng "Nhập email để bắt đầu" + nút "Gửi mã OTP" pill đỏ đúng token.

**Bug đã gặp và sửa xong trên đường deploy:**
- Màn trắng, console lỗi `Uncaught ReferenceError: __name is not defined` – do `next-themes` convert script thành string, esbuild của Wrangler bật `keep-names` mặc định làm hàm `__name` sai scope lúc eval runtime. **Sửa: thêm `"keep_names": false` vào `wrangler.jsonc`** (đã làm, đã build lại + deploy lại + verify lại). Xem https://opennext.js.org/cloudflare/howtos/keep_names.
- **Bài học verify:** `curl -w "%{http_code}"` trả 200 KHÔNG có nghĩa là trang chạy đúng – `(auth-pages)/layout.tsx` là client component chờ `getUser()` xong mới render, curl không chạy JS nên không thấy lỗi. Phải dùng Chrome headless đọc DOM/console thật (`--dump-dom` + `--enable-logging=stderr --v=1` để bắt console error) mới chắc chắn.
- Thử dùng WSL/Ubuntu để né lỗi build trên Windows giữa chừng – **sai hướng, đừng làm lại**, bug `__name` không liên quan gì tới WSL, sửa thẳng trên Windows native (Git Bash) là đủ.

**Việc setup Cloudflare đã xong, không cần làm lại:**
- Đổi `proxy.ts` → `middleware.ts` (Next 16's `proxy.ts` bắt buộc chạy Node.js runtime, `@opennextjs/cloudflare` hiện chưa hỗ trợ – xem opennextjs/opennextjs-cloudflare#962). `middleware.ts` cũ (Edge runtime) vẫn được Next 16 hỗ trợ, chỉ deprecated chứ chưa gỡ.
- Next.js nâng lên 16.3.0 (từ 16.1.6).
- Bỏ hết `NEXT_PUBLIC_VERCEL_URL` (giả định Vercel) khỏi code thật đang dùng – client fetch chuyển sang path tương đối (`/api/...`), 2 chỗ server-side (`app/layout.tsx` metadataBase, `app/api/webhooks/circle/route.ts` self-call) đổi sang biến mới `NEXT_PUBLIC_SITE_URL`/`SITE_URL` (đã set = link thật ở `.env.local` và Cloudflare). Không đụng `app/auth/callback/route.ts` vì đó là code chết (nhánh Developer-Controlled Wallets, TapTip không dùng).
- 6 secret đã đẩy lên Cloudflare Worker `taptip`: `CIRCLE_API_KEY`, `CIRCLE_ENTITY_SECRET`, `NEXT_PUBLIC_CIRCLE_CLIENT_KEY/URL`, `NEXT_PUBLIC_SUPABASE_URL/ANON_KEY`.
- ✅ Domain `taptip.kattyfury1403.workers.dev` đã được user tự thêm vào Circle Console → Modular Wallets → Configurator → Passkey (08-10, user xác nhận).
- Token Cloudflare: đọc từ `D:\Files\Claude\build_on_arc\ezwallet\.env.txt` (`CF_API_TOKEN=`, `CF_ACCOUNT_ID=`) rồi export `CLOUDFLARE_API_TOKEN`/`CLOUDFLARE_ACCOUNT_ID` trước khi chạy lệnh `wrangler`, xem chi tiết memory `cloudflare-api-access`.
- **Đừng đụng WSL/Ubuntu** – thử hướng đó giữa chừng để né lỗi Windows nhưng user chặn lại, quay về sửa thẳng trên Windows native (Git Bash) là đủ, bug `__name` không liên quan gì tới WSL cả.

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
| 3. Plan chi tiết | `03-planning/` | ✅ Vòng 1 **XONG TRỌN**; ⚠️ Vòng 2 (chốt stack, thêm 08-21) có lý thuyết + prompt đã sửa theo 6 chỗ hụt tìm ra lúc **chạy khô**, còn thiếu lượt chạy THẬT + ví dụ thật. Vòng 1: prompt đã sửa theo 5 lỗi tìm được (đẩy trách nhiệm bên thứ ba, bỏ sót câu trong nhóm, tổ hợp rủi ro, ép đổi ý khi user đã chấp nhận rủi ro, quên tổng hợp file) + ví dụ thật + "prompt từng hụt chỗ nào" |
| 4. Wireframe | `04-wireframe/` | ✅ Lý thuyết + prompt xong, **đã chạy thật** (`example/docs/04-wireframe.md`). README chưa viết mục Ví dụ + "prompt từng hụt chỗ nào" |
| 5. Setup môi trường | `05-setup/` | ✅ **XONG TRỌN** — lý thuyết + prompt (đã sửa sau khi chạy thật) + ví dụ thật + mục "prompt từng hụt chỗ nào" (`example/docs/05-setup.md`) |
| 6. Build | `06-build/` | ✅ README xong (3 giai đoạn: logic/flow → giao diện qua Claude Design → live rồi sửa theo người dùng, kèm prompt từng nhịp). GĐ1 + GĐ2 đã chạy thật trên TapTip, ví dụ đã điền. GĐ3 đang chạy |
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

**08-08: Thêm 1 tính năng mới phát sinh giữa chừng (đã hỏi user, không tự thêm lặng lẽ) — hiện tên người thay vì địa chỉ/hash trong Lịch sử.** `components/transactions.tsx` thêm `loadCounterpartyNames()`: lookup `circle_contract_address` của giao dịch → bảng `wallets` (theo `wallet_address`) → bảng `profiles` (theo `profile_id`) → lấy `name`, hiện `"Tip: <tên>"` thay vì hash nếu tìm thấy, fallback về hash cũ nếu không. Đã cập nhật `example/docs/02-hoan-thien-y-tuong.md` (mục "Cập nhật khi build") ghi nhận thay đổi spec này — **PRD giờ không còn khớp 100% với bản gốc chạy Bước 2**, đây là lần đầu spec bị sửa sau khi đã chạy thật, cần nhớ khi viết mục Ví dụ cho Bước 2 sau này. Type-check sạch, dev server compile OK. Cũng CHƯA test tay (cần 2 tài khoản tip qua lại mới thấy tên hiện lên).

**08-08: User đổi hướng — hoàn thiện lẹ để chuyển qua Giai đoạn 2, bớt test kỹ trên PC.** Lý do hợp lý: đây là app mobile, camera QR test trên PC vốn không tối ưu (thiếu/không quen webcam), tốt hơn nên test thật trên điện thoại sau khi có UI thật. Đã làm:
- Tắt (disable) nút "Ngẫu nhiên" theo yêu cầu — user tự set logic lại sau khi xong giao diện, không cần mình động vào nữa trong Giai đoạn 1.
- Sửa race condition camera QR (lỗi `HTML Element with id=taptip-qr-region not found`): `startScanner()` giờ đợi 1 frame nếu DOM chưa kịp commit trước khi khởi tạo `Html5Qrcode`; đổi `console.error` → `console.warn` cho case permission-denied/không có camera (đã xử lý bằng fallback nhập ảnh, không phải crash bất ngờ).
- **Mẹo test camera thật không cần deploy:** điện thoại chung WiFi với PC, mở `http://192.168.110.39:3000` (Network URL dev server tự log ra) — camera thật hoạt động, khỏi cần đụng Cloudflare.

## ✅ 08-09: GIAI ĐOẠN 1 CHỐT — đã chuyển sang GIAI ĐOẠN 2 (giao diện)

User chốt chuyển bước, không test tay hết từng thao tác (chấp nhận, vì sẽ test thật trên điện thoại sau khi có UI thật).

**Layout Home đã khớp lưới 10 hàng CHÍNH XÁC** (đo bằng `getBoundingClientRect` qua Chrome headless, không đoán): balance `0→1`, gap `1→1.5`, QR `1.5→4.5`, gap `4.5→4.75`, chú thích `4.75→5.75`, gap `5.75→8`, nút `8→9` (tâm 8.50), menu `9→10`. Ba cái bẫy tìm ra trên đường: Tailwind v4 không build `flex-[N]` · `flexGrow` một mình chỉ chia phần dư · padding trên hàng bị cộng thêm ngoài tỷ lệ (chi tiết mục 4.8).

**Khung quét QR** sửa xong: `flex-1` → `aspect-square` (hết dải đen letterbox), CSS ép video `object-fit:cover`, `qrbox` đổi từ 250px cố định sang 70% cạnh ngắn.

**Đã dọn 5 component mồ côi do thay đổi của mình gây ra:** `wallet-tab.tsx` (màn gửi cũ, thay bằng `send-flow.tsx`) + 3 file chỉ phục vụ nó (`recipient-search.input`, `transaction-result-dialog`, `virtual-keyboard`) + `wallet-balance.tsx`. Type-check sạch, app chạy bình thường sau khi xoá.

**Gói bàn giao Giai đoạn 2:** [`example/docs/07-design-handoff.md`](example/docs/07-design-handoff.md) — liệt kê 8 màn cần làm giao diện kèm trạng thái từng màn, 3 luật kỹ thuật bắt buộc giữ (lưới tỷ lệ / `flex: "N 1 0"` / không padding trên hàng), cách tự verify bằng Chrome headless, lưu ý nội dung (còn sót tiếng Anh ở onboarding + lịch sử + chi tiết giao dịch), và danh sách code dư từ sample app.

**Bài học đã rút ra và ghi vào repo:** `06-build/README.md` (bản cho người đọc series) + `example/docs/06-build.md` (bản chi tiết kỹ thuật) — 5 thứ làm dự án chậm gấp nhiều lần.

**Brief cho Claude Design (bản tự chứa, để ngoài Desktop):** `C:\Users\Dell\Desktop\TapTip-Design-Brief.md` — 196 dòng, gộp hết PRD + hệ lưới + bố cục từng màn + trạng thái code, đọc file đó là đủ không cần mở repo. Bản trong repo là `example/docs/07-design-handoff.md`.

**Logo (08-09):** user tự vẽ, file gốc `C:\Users\Dell\Desktop\logo.png` (500×500) — bàn tay vàng cầm đồng USDC xanh trên nền cyan bo góc. Đã sinh đủ bộ icon PWA (`public/icon-192x192.png`, `icon-512x512.png`, `web-app-manifest-512x512.png`, `apple-touch-icon.png` 180, `favicon-96x96.png`) + `favicon.ico` (PNG-in-ICO 64×64, ghi cả `app/` lẫn root) bằng `sharp` cài tạm rồi gỡ (`npm install --no-save sharp` → `npm uninstall sharp`). Logo gốc lưu ở `public/logo.png` để sinh lại khi cần. Cũng đổi luôn tên PWA từ **"Arc Pay"** (của sample app) sang **TapTip** trong `app/manifest.ts` + `app/layout.tsx`.

> ⚠️ `public/favicon.svg` vẫn là file SVG cũ của Circle sample app, chưa thay bằng logo TapTip (chỉ thay bản PNG/ICO). Không chặn gì, nhưng nên dọn lúc làm giao diện.

**Việc còn nợ:**
- Dọn rác file tạm: `C:\tmp\taptip-supabase-dbpass.txt`, `C:\tmp\taptip-entity-secret-recovery\` (bản cũ vô dụng), `C:\tmp\register-entity-secret.mjs`; backup recovery file MỚI (`C:\tmp\taptip-entity-secret-recovery2\`) ra chỗ an toàn hơn `C:\tmp`.
- Viết mục Ví dụ + "prompt từng hụt chỗ nào" cho `06-build/README.md` từ kết quả thật (Bước 6 là bước duy nhất chưa có mục Ví dụ).

## ✅ 08-09: GIAI ĐOẠN 2 HOÀN TẤT – đã code hết theo `TapTip Design Spec.dc.html`

User tự viết spec thiết kế Modernist (màu, font Archivo, luật bo góc) vào file gốc repo `TapTip Design Spec.dc.html` (không phải Desktop – lưu ý cho lần sau: file design nằm trong repo, không phải ngoài Desktop). Đã áp hết vào code, đủ 9 việc trong todo list Giai đoạn 2: token màu/font, Home, sign-in/code-confirmation/passkey-setup, onboarding, send-flow 4 bước, transactions + chi tiết giao dịch, màn Splash + Add to Home Screen (route `/` – trước đó không tồn tại, `proxy.ts` ép redirect cứng sang `/sign-in`), sửa lỗi build production, verify bằng Chrome headless.

**Bug thật tìm được, cùng loại "token âm thầm sai" như 3 bẫy flexbox ở Giai đoạn 1 – đọc CSS đã build ra để xác nhận, không đoán:**
- `--radius-xl` bị định nghĩa `calc(var(--radius) + 4px)` (công thức chuẩn shadcn, vốn giả định `--radius` gốc là 8px). Sau khi đổi `--radius: 0rem` cho đúng Modernist, công thức đó cho ra **4px thay vì 12px** – mọi chỗ dùng `rounded-xl` (khung QR, mọi popup qua `dialog.tsx`) đều bị bo góc sai từ đầu buổi tới giờ mà không ai để ý vì nhìn bằng mắt khó phân biệt 4px với 12px trên ảnh chụp nhỏ. Sửa tận gốc: `--radius-xl: 12px` cố định, không tính theo `--radius` nữa.
- Route `/` chưa từng render được `app/page.tsx` (Splash) dù file đã tạo đúng – `proxy.ts` (middleware của repo, không phải `middleware.ts` chuẩn) có rule cứng redirect `/` → `/sign-in` bất kể trạng thái đăng nhập, che mất route mới. Phát hiện bằng `curl -w "%{http_code}"` thấy 307 dù code không có gì sai.
- `npm run build` production fail thật do thiếu field `status` trong `.select()` ở `app/api/webhooks/circle/route.ts:232` (bug có sẵn từ sample app gốc) – thêm field vào là qua, đồng thời sửa luôn bug runtime ẩn (so sánh `existing.status` với field chưa bao giờ được select nên luôn `undefined`).
- `tailwind.config.ts` là file cấu hình kiểu Tailwind v3 sót lại từ sample app gốc, dự án đã chuyển hẳn sang Tailwind v4 (CSS-first qua `@theme` trong `globals.css`) – file đó không còn được dùng nhưng vẫn chặn build vì `import type { Config } from "tailwindcss"` không còn resolve được ở v4. Xoá hẳn (không phải sửa) vì xác nhận không nơi nào khác import nó; `components.json` trỏ `tailwind.config` về rỗng theo đúng convention shadcn cho dự án Tailwind v4.

**Verify:** `npx tsc --noEmit` sạch sau mỗi file sửa (đúng kỷ luật đã rút ra ở Giai đoạn 1 – không gộp nhiều sửa rồi mới check). `npm run build` chạy production thành công, `next start` phục vụ `/` và `/sign-in` trả 200. Chrome headless xác nhận trực quan: splash hiện logo tự vẽ + chữ "TapTip", màn Add to Home Screen hiện 3 bước hướng dẫn tiếng Việt + nút "Tiếp tục" pill đỏ đúng token. `/onboarding` và luồng gửi tiền trong `send-flow.tsx` không verify được bằng Chrome headless vì cần phiên đăng nhập qua passkey (WebAuthn không giả lập được ở headless) – đã đối chiếu code với cấu trúc đã xác nhận đúng của `sign-in.tsx`/`code-confirmation.tsx` thay vì tự dựng hạ tầng auth giả cho một lần kiểm tra.

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

## 4.8 🔴 Layout phải neo theo tỷ lệ màn hình, KHÔNG dùng pixel cố định

Bài học đau thật (08-09, chỉnh layout Home theo grid 10 hàng): dùng `h-40`, `h-20`, `mt-10` (px cố định) tưởng đúng vị trí nhưng chỉ đúng trên đúng 1 kích thước màn hình lúc test — khách xài màn hình khác kích thước là vỡ layout ngay, và bản thân mình cũng tự nhầm vị trí vì không có cách nào verify bằng mắt (không có browser tool để chụp màn hình).

**Quy tắc:** mọi khoảng cách/kích thước xuất phát từ hệ lưới N-hàng (Bước 4) phải quy đổi thành **tỷ lệ co giãn** (`flex`, `%`, `vh`/`vw`), không bao giờ hardcode px. Ví dụ thật đã sửa ở `example/app/components/home-screen.tsx`: toàn bộ trang dùng đúng 1 hệ flex cộng lại bằng tổng số hàng của hệ lưới (VD 10 hàng → tổng = 10), **kể cả các hàng "trống"/spacer cũng phải có flex riêng** — nếu không khối content sẽ tự nuốt hết phần dư, làm sai lệch tỷ lệ thực tế so với hệ lưới đã tính.

### 3 cái bẫy đã thật sự làm hỏng layout (đều tốn nhiều vòng sửa mới ra)

1. **`flexGrow` một mình KHÔNG chia theo tỷ lệ tuyệt đối.** Nó chỉ chia phần *dư* sau khi trừ kích thước nội dung, nên hàng nào nội dung to (QR) tự chiếm nhiều hơn phần của nó → lệch cả lưới. **Bắt buộc dùng `style={{ flex: "N 1 0" }}`** (flexBasis = 0) thì mỗi hàng mới đúng `N/tổng` chiều cao.
2. **Padding trên hàng bị CỘNG THÊM ngoài phần chia tỷ lệ.** Padding là kích thước tối thiểu không co được, nên `py-[1vh]` trên hàng nút làm hàng đó phình từ 83px lên 98px (= 83 + 16.6px padding), đẩy toàn bộ hàng khác co lại ~2%. **Tuyệt đối không đặt padding trên phần tử hàng** — muốn khoảng thở thì cho phần tử con cao theo `%` (VD nút `h-[80%]` + hàng `items-center`).
3. **Phần tử kích thước cố định (ảnh, QR) làm tràn hàng.** Cách sửa: cho nó `height: 100%` + `aspectRatio: "1"` để lấp đúng chiều cao hàng, và `minHeight: 0` cho hàng chứa nó để hàng thật sự co được.

### 🔬 Cách TỰ VERIFY layout — đừng bao giờ đoán bằng mắt nữa

Máy này **có Chrome** (`C:\Program Files\Google\Chrome\Application\chrome.exe`), chạy headless được. Đây là thứ đáng lẽ phải dùng ngay từ đầu thay vì sửa mù rồi bắt user chụp màn hình:

```bash
# 1. Chụp ảnh và TỰ XEM bằng tool Read (Read đọc được file .png)
chrome.exe --headless=new --disable-gpu --hide-scrollbars \
  --window-size=900,932 --screenshot="C:/tmp/shot.png" \
  --virtual-time-budget=8000 "http://localhost:3000/<route>"

# 2. Đo CHÍNH XÁC bằng số: tạo route tạm render component kèm 1 client
#    component chạy getBoundingClientRect() cho từng con của container,
#    quy ra đơn vị "hàng", in vào <pre id="measurements">, rồi:
chrome.exe --headless=new --disable-gpu --window-size=900,932 \
  --virtual-time-budget=8000 --dump-dom "http://localhost:3000/<route>" > C:/tmp/dom.html
# rồi dùng node đọc nội dung thẻ <pre id="measurements"> ra
```

Mẹo: route tạm nên vẽ luôn lưới N hàng (`position:absolute; top:i*10%` + `borderTop`) để so trực tiếp với ảnh user gửi. Component `HomeScreen` đã có sẵn thuộc tính `data-home-root` trên container để script đo bám vào. Xoá route tạm sau khi verify xong. **Lưu ý:** máy KHÔNG có `python3`, dùng `node -e` để parse HTML.

> 🔴 **QUAN TRỌNG — Tailwind v4 không build class `flex-[N]`.** Repo này dùng `tailwindcss@4.2.1`. Đã tự kiểm chứng bằng cách đọc thẳng file CSS đã build (`.next/dev/static/chunks/app_globals_css_*.single.css`): class kiểu `flex-[1.5]`, `flex-[3]` (arbitrary value trên utility `flex`) **không sinh ra rule CSS nào cả** — các arbitrary value khác như `w-[50vw]`, `max-w-[260px]` vẫn build bình thường, chỉ riêng `flex-[N]` bị bỏ qua. Hậu quả: đặt tỷ lệ đúng trên giấy nhưng layout không nhích một chút nào, dễ làm tưởng lầm là do tính sai công thức (đã tốn nhiều vòng sửa mới tìm ra). **Giải pháp:** dùng `style={{ flexGrow: N }}` inline thay vì class Tailwind cho mọi giá trị flex-grow phân số. Muốn biết chắc 1 class Tailwind có thật hay không, đừng đoán qua giao diện — `curl` trang, tìm file `.next/dev/static/chunks/*.css`, `grep` thẳng tên class trong đó.

## 5. Git

Remote `origin` = GitHub, branch `main`. Xong việc là commit + push ngay, đừng để commit nằm im ở local.

## 6. Tools tham khảo – dùng ở Bước 6 (code UI thật), KHÔNG dùng ở Bước 4

Bước 4 (wireframe) cố tình bỏ hết style, chỉ khung + label chức năng – mấy tool dưới đây đều thuộc chuyện style/component thật nên chỉ có ích lúc code, không có ích lúc vẽ khung.

- **21st.dev** – https://21st.dev/ – marketplace React+Tailwind, prompt sẵn cho Claude Code/Cursor/v0
- **Astryx (Meta)** – https://astryx.atmeta.com/ – design system chính thức Meta, React 19 + StyleX, 160+ component – hơi nặng đô cho app nhỏ như `example/`
- **Magic UI** – https://magicui.design/ – component + animation React+Tailwind
- **ui-ux-pro-max-skill** – https://github.com/nextlevelbuilder/ui-ux-pro-max-skill – AI skill sinh design system (màu, font, style) theo project, 114,271 sao (verify qua GitHub API 08-07, số thật cao hơn số đồn)
- **taste-skill** – https://github.com/Leonxlnx/taste-skill (site: tasteskill.dev) – skill chống AI sinh UI "generic slop", 73,405 sao (verify qua GitHub API 08-07)
