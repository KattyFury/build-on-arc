# HANDOFF – build-on-arc

> File làm việc của tác giả, không phải nội dung cho người đọc series. Mở máy mới thì đọc file này trước.
> Luật cho Claude Code nằm ở `CLAUDE.md`. File này ghi **đang ở đâu** và **quy định viết bài**.
> **Cập nhật:** 2026-10-03 (Câu 0 chỉ cho người chưa có ý tưởng; Claude Design vẽ wireframe; mục "Cần kiểm tra khi build" từ spec DailyReal – xem mục ngay dưới). Trước đó 2026-09-18 (Bước 1 lên 6 hướng Arc; mục "Ví dụ" của 6 bước giờ dùng CẢ TapTip lẫn EZwallet – xem mục ngay dưới). Trước đó 2026-08-22: đổi toàn bộ mục "Ví dụ" từ TapTip sang EZwallet. Cùng ngày trước đó: tách TapTip ra repo riêng `KattyFury/taptip`, repo này trở về thuần hướng dẫn. Trước đó cùng đợt: sửa Bước 1 + Bước 3 Vòng 2 theo lỗi thật tìm ra khi thử với LuckyStaker; thêm Vòng 2 "chốt stack" vào Bước 3, đóng nốt ví dụ + chỗ hụt của Bước 4, dọn sạch em dash.

## ✅ 10-03: HỌC TỪ SPEC DAILYREAL + 2 BÀI HỌC CỦA BUỔI CHẠY

User chạy series với một ý tưởng mới – **DailyReal** (nhật ký ảnh thật, chụp bằng camera trong app, mỗi ảnh một NFT trên Arc, caption mã hoá gửi qua Memo; wireframe 13 màn trên Figma). Spec cuối buổi có 8 mục, đáng học nhất là mục 7 "Cần kiểm tra khi build" (số ước tính, giới hạn chưa rõ, công cụ chưa chắc hỗ trợ Arc, luồng thu phí Arweave chưa chốt) và mục 8 "Để sau". Người giao spec phải dặn riêng "nhớ bảo Claude Code đọc cả mục 7 trước khi viết code" – tức prompt chưa tự lo. DailyReal chưa có repo/link public, nên chỉ nhắc tên + trích đúng nội dung spec, KHÔNG viết mục "Ví dụ" cho nó.

User chốt 2 bài học, đã ghi vào repo:
1. **Câu 0 chỉ là điểm bắt đầu cho người chưa có ý tưởng, không phải bộ lọc.** `01-ideation`: lý thuyết + prompt đổi thành "có ý tưởng rồi thì BỎ QUA câu 0, vào thẳng câu 1"; bỏ câu "check thử có khớp 1 trong 6 hướng"; chuyện "có dùng đặc thù Arc không" chuyển sang Câu 3. Hụt #10 (sửa ở #6 08-21 chưa đủ – vẫn đem ý tưởng ra so). `README.md` bảng cấu trúc đổi mô tả Bước 1.
2. **Bước wireframe gợi ý nhờ Claude Design vẽ cho người chưa biết Figma.** `04-wireframe`: mục mới "Chưa biết Figma? Nhờ Claude Design vẽ" kèm prompt (vẫn là wireframe, chưa style); file tổng hợp đánh số màn để bản vẽ đặt tên khung theo số (như DailyReal 1-13). Hụt #12. `README.md` bảng công cụ thêm dòng Claude Design cho Bước 4.

Học thêm từ spec (mục 7 + 8):
- `03-planning` Vòng 2: file tổng hợp thêm mục "CẦN KIỂM TRA KHI BUILD" (kèm cách kiểm từng dòng, cấm viết số ước tính như số chắc) + mục "ĐỂ SAU". Hụt Vòng 2 #8.
- `06-build` Giai đoạn 1: prompt thêm khối "trước khi viết dòng code đầu tiên" – kiểm từng dòng chưa chắc bằng cách thật, báo bằng chứng, sai thì dừng sửa spec; đọc bản vẽ theo số màn; không build mục "Để sau". Đoạn giải thích dùng ví dụ caption qua Memo công khai vĩnh viễn (lấy từ mục 7 spec DailyReal, không phải chuyện đã xảy ra). Hụt #6.
- `CLAUDE.md`: giao thức thêm ghi chú Bước 1 (bỏ Câu 0 nếu có ý tưởng), Bước 4 (gợi ý Claude Design), Bước 5-6 (tự kiểm mục cần kiểm tra trước khi code).

**Thêm cùng ngày – Arc Studio:** user báo giờ ngoài AI của docs còn có Arc Studio (studio.arc.io), AI chuyên tech hơn docs. Đã verify qua docs chính thức (docs.arc.io/ai/arc-studio + /ai/arc-studio-cli, developers.circle.com/ai/arc-studio): coding agent của Circle, ra 09-18, viết/preview/deploy app + contract lên Arc testnet (không mainnet), có CLI để Claude Code giao việc. Đã sửa `01-ideation` Câu 3 (bảng chia việc docs / Arc Studio / search web, dặn Arc Studio "chỉ thử, chưa build cả app"; prompt soạn thêm khối riêng cho Arc Studio khi cần thử thật) – hụt #11. `ARC-RESOURCES.md` thêm Arc Studio + lệnh cài CLI. User duyệt luôn 2 chỗ còn lại: `06-build` thêm mục "Giao phần smart contract cho Arc Studio" (cài CLI, prompt giao việc, 3 điều nhớ: code ở sandbox phải pull + commit, chỉ testnet, kết quả chưa kiểm) + khối "cần kiểm tra" giao Arc Studio đo trên testnet – hụt #7. `05-setup` thêm bước 8b cài CLI khi app có contract – hụt #6.

**Lỗi CLI trên Windows (đã ghi vào Bước 5-6):** `arc-studio skills install --tool claude-code` báo "Claude Code not found" dù có Claude Code – code gọi `execFileSync('claude')` không tìm ra `claude.cmd`. Vá: chạy tay `claude plugin marketplace add "$(npm root -g)/@circle-fin/arc-studio-cli" --scope user` rồi `claude plugin install arc-studio@arc-studio-cli -y`.

**Trạng thái máy Dell cuối phiên 10-03:** Arc Studio CLI 1.1.3 đã cài global, đã `arc-studio login`, plugin `arc-studio@arc-studio-cli` (scope user) đã gắn vào Claude Code – mở lại Claude Code thì thấy skill `arc-studio` + subagent `arc-studio:arc-studio`. `arc-studio apps` thấy 3 app trên tài khoản: On Chain Photo Diary (có vẻ là DailyReal làm trên web), Arc Studio Product Showcase Builder, Personal AI Agent Workspace. **Chưa cho Arc Studio chạy thật lượt nào.**

**Việc tiếp theo (chờ user chọn):**
1. Thử nhanh: hỏi Arc Studio trên app On Chain Photo Diary (`arc-studio ls --app af34c042-daee-4506-8fe0-4d210274f245`) – ~1 phút.
2. Thử thật mục 7 DailyReal: deploy ERC-721 nhỏ lên Arc testnet, mint 1 token kèm Memo, đo gas thật – 5-20 phút, tốn hạn mức Arc Studio. Kết quả này cũng là phép thử cho mục "Giao phần smart contract cho Arc Studio" ở Bước 6 – chỗ nào hụt thì ghi vào bảng hụt Bước 6.

**Còn nợ:** các sửa này chưa chạy lại với người thật. Khi DailyReal sang Bước 6, xem Claude Code có tự kiểm mục 7 mà không cần dặn không – đó là phép thử của hụt #6 Bước 6.

---

## ✅ 09-18: 6 HƯỚNG ARC + VÍ DỤ DÙNG CẢ TAPTIP LẪN EZWALLET

User yêu cầu 2 việc:

1. **docs.arc.io giờ có 6 usecase, không còn 4** – thêm *Prediction markets* và *Borrow and lend*. Đã sửa `01-ideation/README.md` (danh sách lý thuyết kèm mô tả ngắn từng hướng, khối prompt Câu 0, thêm ghi chú "danh sách đổi theo docs"). Mục "Prompt này từng hụt" giữ nguyên chữ "4 hướng" ở chỗ kể lịch sử (lúc đó docs thật sự có 4), chỉ ghi chú thêm.
2. **Dùng cả ezwallet và taptip làm mẫu ở mỗi bước.** Lệnh này **thay** yêu cầu 08-22 "bỏ taptip" (mục dưới). Mỗi bước giờ có `### TapTip` (chạy thật đúng prompt) rồi `### EZwallet` (dựng ngược). Nội dung TapTip lấy lại từ bản trước commit `90780ee` (đó là kết quả chạy prompt thật), rồi **cập nhật theo những gì xảy ra sau 08-22** – đã đọc thật `taptip/HANDOFF.md` + `docs/02-v2`, `03-planning-v2`, `04-wireframe-v2`:
   - 01: thêm hậu truyện của quyết định loại Privy – code fork về chạy passkey (ký từng giao dịch), trái Bước 1 gần 1 tháng, đổi sang Developer-Controlled 09-02. Gas Station vẫn chưa bật.
   - 02: PRD v1 + bảng v1→v2 + core value v1 (còn nhắc "tip/lì xì") → v2 (niềm tin độc lập).
   - 03: Vòng 1 v1 + tổ hợp rủi ro mới bắt được ở v2 (QR rác). Stack v1 + đúng 2 dòng "Khó" bị đổi thật (Supabase tự pause → D1+KV; Modular Wallets → Developer-Controlled). Số liệu kiểm toán fork 09-02.
   - 04: wireframe v1 + v2 chỉ vẽ lại màn đổi + lưới Figma 15 hàng gap 8px, khoá khung 390×844 rồi scale. EZwallet thêm lỗi thiếu khe 16px giữa hàng (84.4px vs 70px, lệch ~14px nhiều tháng).
   - 05: TapTip verify máy có sẵn + 2 bài học tài khoản: file khôi phục Entity Secret (brick 2 account), push ≠ deploy.
   - 06: 3 giai đoạn TapTip + đợt dựng lại theo Figma tháng 9 (AI tự giữ chi tiết cũ Figma không vẽ – EZwallet dính y hệt) + Giai đoạn 3: gỡ passkey theo phản hồi thật, kiểm toán lòi ra gửi tip chưa từng chạy, **chưa test trên điện thoại thật**.

Cũng sửa: `README.md` mục "Về dự án mẫu" (bảng 2 dự án), `CLAUDE.md` mục Tech Stack (TapTip là Developer-Controlled không passkey, không phải "giấu ví sau passkey").

### 09-18 (tiếp): LUẬT LƯỚI MỚI + ĐI THỬ CẢ SERIES TỪ Ý TƯỞNG TỚI SẢN PHẨM

**User chốt luật (thay luật "tỷ lệ 1/N" cũ):** chữ bội số của 3, khoảng cách + khối bội số của 8, vẫn chia hàng/cột, ưu tiên nhiều hàng nhiều cột (12 hoặc 15). User cũng chốt mục tiêu: **repo phải đưa được người dùng từ ý tưởng tới sản phẩm** – dùng câu này làm thước đo cho mọi thay đổi sau.

- `04-wireframe`: khối prompt có luật "HỆ LƯỚI VÀ CON SỐ" (khung gốc cố định, khai đủ hàng/cột/khe/lề + phép tính, bội 8, chữ bội 3, vùng chạm ≥48, lề là chỗ duy nhất được lẻ) + tự tổng hợp file cuối bước. Mục mới "Hệ lưới mẫu cho mobile": 390×844, **15 cột × 16 / 12 hàng × 56, khe 8** → lề 19, trên 48 / dưới 36; span cột 24k−8, span hàng 64k−8; vuông khớp lưới duy nhất 8 cột × 3 hàng = 184. Thang chữ 36/24/18/15/12. Máy khác cỡ: px trên khung gốc + scale nguyên khung. Bảng hụt lên 11 dòng.
- `06-build`: prompt 2.1/2.2/2.3 + dựng lại mang luật số; bỏ "neo tỷ lệ"; cấm thêm thứ bản thiết kế không vẽ; **thêm prompt deploy** ở Giai đoạn 3; GĐ1 trỏ `docs/`. Thêm mục "Prompt này từng hụt chỗ nào" (trước đó bước 6 THIẾU mục bắt buộc này) – 5 dòng.
- `05-setup`: chạy thẳng trong Claude Code (tự chạy lệnh), dùng lại thư mục dự án đã có từ Bước 1, thêm bước 11 đọc `docs/03-stack.md` cài đúng stack + giữ secret ngoài git. Hụt thêm #3-5.
- `CLAUDE.md`: Bước 3 = 2 lượt (lưu `docs/03-planning.md` + `docs/03-stack.md`), thư mục dự án tạo ở Bước 1, thêm mục "Từ Bước 5 → 6", đích cuối là link chạy thật.
- `README.md`: bảng cấu trúc + câu "đích cuối là link sản phẩm chạy thật".

**5 lượt thử đã chạy (chạy khô, Claude Code tự làm – CHƯA có người thật chạy lại):**
1. Áp lưới mẫu 15×15 vào Home TapTip → hàng 40px, nút < cỡ ngón tay → đổi sang 12 hàng × 56 + luật vùng chạm ≥48.
2. Script kiểm phép tính lưới mẫu (khớp, mọi span chia hết 8) + soi luật mới vào số thật cũ: bắt được hết (hàng 48.8/70, lề 25, chữ 19/23/35/28/22/17/32/20/16).
3. Đi thử cả chuỗi README → CLAUDE.md → Bước 1-6 như người mới: lòi 4 chỗ đứt (Bước 3 hai vòng vs giao thức 1 prompt; Bước 4 không có file kết quả; Bước 5 Chat vs Code + tạo trùng thư mục; Bước 6 không có cách deploy) → đã sửa hết.
4. Quét cả repo tìm luật cũ còn sót (`tỷ lệ`, `1/N`, `cqh`, `flex-grow`) → chỉ còn ở đoạn kể lịch sử. Em dash = 0. Đường dẫn `docs/0N` nhất quán giữa CLAUDE.md/05/06.
5. Đọc lại trọn Bước 4 → lòi mâu thuẫn tự gây: lề vừa bắt bội 8 vừa hứng phần dư → sửa (hụt #11).

**Còn nợ:** chưa có người thật chạy lại prompt Bước 4 mới với một dự án để xem AI có tuân luật số không – nên làm khi có dự án tiếp theo.

---

## ✅ 08-22 (tiếp): ĐỔI VÍ DỤ TỪ TAPTIP SANG EZWALLET

Ngay sau khi tách TapTip ra repo riêng (mục dưới), user chỉ ra: mục "Ví dụ" của 6 bước vẫn giữ TapTip – đó là quyết định Claude Code **tự chọn mà không hỏi lại**, trong khi user đã yêu cầu rõ "ví dụ trỏ ra ezwallet đi, bỏ taptip" ngay lúc bắt đầu tách repo. Bị bỏ sót vì lúc đó đổi sang ezwallet tốn công hơn (phải đọc thật `HANDOFF.md`/`README.md` của ezwallet để không bịa), còn giữ TapTip thì có sẵn nội dung – Claude Code chọn đường rẻ hơn thay vì hỏi user. User xác nhận qua `AskUserQuestion`: đổi sang ezwallet đúng như yêu cầu ban đầu.

**Đã đọc thật** [`KattyFury/ezwallet`](https://github.com/KattyFury/ezwallet) – `README.md` (207 dòng) + `HANDOFF.md` (618 dòng) – trước khi viết lại, đúng luật "chỉ nói những gì làm thật, không chế số liệu". EZwallet **có trước cả series** nên không chạy đúng trình tự 4 câu/6 câu/Product Discovery như TapTip từng làm – mọi ví dụ ở đây đều **dựng ngược** (lấy quyết định có thật, dựng lại tình huống sinh ra nó), không phải chép lại một buổi chạy prompt thật.

**Viết lại cả 6 mục "Ví dụ":**
- **01-ideation:** 4 câu dựng từ README + HANDOFF thật. Câu 3 đổi hẳn ví dụ minh hoạ "loại phương án khả thi" – từ chuyện Circle Wallets vs Privy (TapTip) sang chuyện **từ chối chuẩn EIP-681** dù đúng chuẩn, vì nhiều ví khác bỏ qua field chainId khiến gửi nhầm mạng mất tiền – khả thi trên giấy không bằng an toàn cho đúng đối tượng (người lớn tuổi).
- **02-hoan-thien-y-tuong:** 6 câu PRD khớp gần như nguyên trạng với README thật của ezwallet – tình cờ, không phải cố ép khớp.
- **03-planning:** Vòng 1 giữ đúng 5 nhóm như khung TapTip nhưng đổi callout – EZwallet có story khác hẳn TapTip (không phải "chấp nhận rủi ro rồi để yên" mà là "tự phát hiện lỗ hổng rồi vá thật": auth đồng bộ danh bạ từ `userToken` lỏng lẻo nâng cấp lên chữ ký PIN + nonce). Vòng 2 **nói thẳng bảng thưa hơn TapTip** ở cột "loại gì" – không phải ezwallet thiếu phương án để cân, mà vì lúc build không ai hỏi thẳng câu đó. Đây tự nó là bằng chứng sống cho giá trị của Vòng 2 Bước 3.
- **04-wireframe:** EZwallet **độc lập chốt cùng hệ lưới 10 hàng** như TapTip – dấu hiệu hệ lưới N-hàng là cách hợp lý chứ không phải luật riêng một app. Callout đổi sang 2 bug lưới thật khác (`grid-template-columns` thiếu làm phình cột; `aspectRatio` ép vuông làm tràn chữ trên máy hẹp).
- **05-setup:** Thêm 2 kinh nghiệm TapTip không có: chế độ **mock** (test UI không cần backend thật vì Circle SDK không chạy `localhost`) và setup 2 tiến trình song song (proxy API + dev server).
- **06-build:** Đổi toàn bộ "5 thứ làm chậm" sang bug thật của ezwallet (đọc sai chữ ký hàm SDK, sửa code quên sửa test 9 ngày, retry RPC tự đâm giới hạn...). Mục Ví dụ nói thẳng: **Giai đoạn 1/2 không tách bạch được** vì ezwallet có trước series (không giả vờ khớp), nhưng bù lại viết được **Giai đoạn 3 đầy đủ lần đầu tiên** – TapTip chưa từng tới giai đoạn có người dùng thật. 3 câu chuyện live-iteration thật: thuật toán gợi ý số tiền sửa 3 lần, cỡ icon chốt sau khi lệch cả hai phía, bug thông báo chậm vì hàm tên "poll" mà không có `setInterval`.

**Cũng cập nhật:** `CLAUDE.md` mục Tech Stack (ví dụ stack đổi từ "TapTip fork sample app" sang "EZwallet Circle User-Controlled Wallets, đối lập có chủ đích với Developer-Controlled của TapTip"), `README.md` mục "Về dự án mẫu", bảng trạng thái mục 1 file này.

**Bài học riêng cho Claude Code:** đây là lần THỨ HAI trong phiên này tự ý làm khác yêu cầu rồi không báo lại (lần đầu: hỏi user chọn tech thay vì đề xuất, lúc chạy thử Vòng 2 với LuckyStaker). Cả hai lần đều vì chọn đường ít việc hơn thay vì đường đúng yêu cầu. Khi user đã ra quyết định rõ ràng, làm khác đi – dù có lý do hợp lý (ví dụ: "làm sau tốn công hơn") – vẫn phải nói ra ngay, không lặng lẽ tự chọn.

---

## ✅ 08-22: TÁCH TAPTIP RA REPO RIÊNG – REPO NÀY VỀ THUẦN HƯỚNG DẪN

User: "cảm giác nó không mang lại hiệu quả, còn gây xao nhãng" – việc vừa viết guide vừa vá bug/deploy/vận hành một app thật (TapTip) trong cùng repo làm phân tán khỏi việc chính là viết hướng dẫn. Quyết định: tách hẳn, quay lại TapTip sau ở repo riêng.

**Đã làm:**

1. **Tách lịch sử git bằng `git subtree split --prefix=example -b taptip-history`** (native, không cần cài `git-filter-repo` – công cụ đó không cài được qua pip trong venv hiện tại). Giữ nguyên 39 commit gốc của `example/app` + `example/docs`, `example/README.md` trở thành root của lịch sử mới. Lưu ý môi trường: `git subtree split` treo vô thời hạn nếu không redirect stdin từ `/dev/null` trong Bash tool này – luôn thêm `< /dev/null` khi chạy lệnh git tương tác kiểu này.
2. **Clone nhánh đó ra `D:\Files\Claude\Build on Arc\taptip\`**, đổi tên nhánh thành `main`, gỡ remote cũ.
3. **Copy thêm các file chỉ có 1 commit lịch sử** (không đáng tách riêng): `design_handoff_taptip/`, `TapTip Design Spec.dc.html`, `Frame 2147232707.png`, `items/` (logo).
4. **Viết `HANDOFF.md` mới cho repo `taptip`**, chưng cất từ `HANDOFF.md` cũ của repo này – giữ nguyên toàn bộ build log + bài học kỹ thuật riêng của TapTip (Circle/Supabase/Cloudflare, 3 bẫy layout Tailwind v4), bỏ phần "quy định viết bài" vốn thuộc về guide series.
5. **Viết lại `README.md` của `taptip`** thành README project độc lập (bản cũ trong `example/` đã lỗi thời, ghi sai là "chưa có dòng code nào" dù thực tế đã xong Giai đoạn 1+2 và deploy thật).
6. **Tạo repo GitHub `KattyFury/taptip` (public) + push.** Xác nhận đúng account active (`gh auth status` → KattyFury).
7. **Xoá khỏi repo `build-on-arc`:** `example/`, `design_handoff_taptip/`, `TapTip Design Spec.dc.html`, `Frame 2147232707.png`, `items/` (160 file).
8. **Sửa lại toàn bộ nội dung guide phụ thuộc vào `example/`:**
   - `CLAUDE.md`: viết lại mục "Repo này là gì" (bỏ "kèm luôn dự án mẫu"), mục "THƯ MỤC", luật "Ví dụ xuyên suốt" → đổi thành "Ví dụ là tuỳ chọn, không bắt buộc, dẫn chứng trỏ link ra ngoài repo nếu có". Luật "chạy thật trước khi đăng" giữ nguyên nhưng bỏ ràng buộc phải build trong `example/`.
   - `README.md`: bỏ cột "Ví dụ" khỏi bảng cấu trúc (không còn ✅ đồng loạt vì ví dụ giờ tuỳ chọn), viết lại mục "Về dự án mẫu".
   - 6 file `0N-*/README.md`: **giữ nguyên toàn bộ mục "Ví dụ" + "Prompt này từng hụt chỗ nào"** (đây là "kinh nghiệm", đúng thứ user muốn giữ) – chỉ đổi link `../example/...` sang link GitHub thật `https://github.com/KattyFury/taptip/...`. `04-wireframe` xoá tham chiếu chết tới `HANDOFF.md` mục 4.8 (đã chuyển sang `taptip`).
9. **Rút gọn `HANDOFF.md` của chính repo này** (file bạn đang đọc) – xoá mục "VIỆC TIẾP THEO", "GIAI ĐOẠN 1 CHỐT", "GIAI ĐOẠN 2 HOÀN TẤT", toàn bộ log fix bug 08-10/08-11 (tất cả đã chuyển nguyên vẹn sang `taptip/HANDOFF.md`), mục 4.7 + 4.8 (bài học kỹ thuật riêng của TapTip, cũng đã chuyển). Viết lại mục 1 (bảng trạng thái) và mục 2 (cách làm việc).

**Quyết định giữ lại, không xoá:** mục "Ví dụ" + "Prompt này từng hụt chỗ nào" trong 6 file `0N-*/README.md` vẫn dẫn chứng TapTip – đây là lịch sử thật, xoá đi là mất bằng chứng cho luật "chỉ nói những gì làm thật, không chế số liệu". Link đã trỏ đúng sang `KattyFury/taptip`, verify được như cũ, chỉ khác chỗ ở.

**Việc còn treo:** repo `taptip` local ở `D:\Files\Claude\Build on Arc\taptip\` – dev server/`.env.local`/credentials không di chuyển theo (secrets không commit từ đầu), cần tự dựng lại khi quay lại làm tiếp, xem `taptip/HANDOFF.md` mục "Trạng thái nghỉ".

---

## ✅ 08-21 (tiếp): SỬA BƯỚC 1 + VÒNG 2 BƯỚC 3 THEO LỖI THẬT VỚI LUCKYSTAKER

User thử áp prompt Bước 1 (Lên ý tưởng) và Vòng 2 Bước 3 (chốt stack) cho một dự án testnet khác – **LuckyStaker** (no-loss lottery: gửi USDC vào pool không mất gốc, mỗi tuần xổ toàn bộ lãi cho một người trúng, rút được bất cứ lúc nào). Không phải ví dụ chính thức của series – chỉ dùng để **soi lỗi prompt**, tương tự cách Vòng 2 Bước 3 từng được "chạy khô" với TapTip.

**4 lỗi user chỉ thẳng, đã sửa vào `01-ideation/README.md` và `03-planning/README.md`:**

1. **Câu 0 Bước 1 đọc như danh sách đóng.** LuckyStaker không khớp thẳng cái nào trong 4 hướng Arc (P2P/eCommerce/FX/Agentic) – Claude Code từng đối xử với nó như một vấn đề cần pivot ý tưởng. User chỉnh: **4 hướng chỉ là gợi ý có điểm bắt đầu, không phải rào chắn** – ý tưởng đã có rồi thì không khớp cũng không sao, không loại.
2. **Câu 3 Bước 1 chỉ nói hỏi docs.arc.io, không phân biệt câu hỏi thuộc Arc hay không.** Đã tách rõ: câu hỏi thuộc cơ chế Arc → docs.arc.io; câu hỏi ngoài Arc (tokenomics/roadmap token khác) → tự search web riêng.
3. **Câu 3 Bước 1 bị thiết kế như một cửa làm-một-lần-rồi-xong.** Thực tế feasibility là việc liên tục xuyên suốt Bước 1-3 – mỗi lần chốt dùng cơ chế Arc mới thì tra ngay, không dồn lại. Đã ghi rõ Câu 3 chỉ là cửa **tối thiểu** trước khi qua Bước 2.
4. **Ràng buộc "Ngân sách" trong prompt Vòng 2 Bước 3 hỏi cứng cho mọi dự án** – vô nghĩa với app demo/hackathon chạy testnet (Claude Code tự dính lỗi này khi đóng vai Solution Architect hỏi user về ngân sách cho một app testnet). Đã đổi thành có điều kiện.

**Bảng "Prompt này từng hụt chỗ nào" cập nhật:** `01-ideation/README.md` từ 5 lên 9 dòng, `03-planning/README.md` mục Vòng 2 từ 6 lên 7 dòng. Không viết "Ví dụ 2" cho LuckyStaker – chỉ dùng để tìm lỗi prompt.

🔴 **Bài học riêng cho Claude Code:** lúc chạy thử Vòng 2 với user, Claude Code trượt khỏi vai trò prompt yêu cầu – prompt nói "AI đề xuất, user chốt", Claude Code lại quay sang hỏi user chọn thư viện/kiến trúc như thể user là dev. User phải chỉnh: "tao bảo mày xem như tờ giấy trắng, dắt tao qua các bước... mày lại hỏi các câu off vậy?". Đúng loại lỗi mà Bước 1 từng mắc ở lượt chạy đầu (AI phỏng vấn ngược thay vì dẫn).

---

## ✅ 08-21: VÒNG 2 BƯỚC 3 + ĐÓNG NỐT BƯỚC 4 + DỌN EM DASH

Thesis của user: bắt AI liệt kê stack dùng cho mỗi luồng, vì sao chọn tech đó, còn tech nào khác làm được và vì sao không dùng. Series trước đó không có chỗ nào chốt stack – Bước 3 chỉ hỏi về sản phẩm, Bước 5 nhảy thẳng vào cài Node/Git/MCP như thể stack đã có sẵn.

Đã làm: `03-planning/README.md` tách thành **Vòng 1** (phỏng vấn ngược, y như cũ) + **Vòng 2** (chốt stack) – lý thuyết, prompt Solution Architect, bảng dấu hiệu câu trả lời dỏm. Cập nhật bảng ở `README.md`.

**Đã chạy khô ngay sau đó:** đem prompt Vòng 2 chạy lại với spec TapTip, Claude Code đóng cả hai vai. Kết quả: ghép từng mảnh thì ra trúng stack thật, NHƯNG không đường nào ra được quyết định thật là fork nguyên `arc-p2p-payments` – vì prompt hỏi sample app theo từng luồng nên chỉ ra mảnh lẻ. Lòi ra 6 chỗ hụt, đã sửa hết vào prompt.

**Bước 4** – trước đó thiếu hẳn ví dụ + bảng chỗ hụt dù đã chạy thật từ lâu. Đã viết ví dụ (hệ lưới 10 hàng + 2 nguyên tắc chung) và 5 chỗ hụt rút từ những gì vấp lúc code thật ở Bước 6; prompt Bước 4 bổ sung đúng 5 điều đó.

**Em dash:** dọn sạch toàn bộ file người đọc nhìn thấy, chừa lại `CLAUDE.md` + `HANDOFF.md` có ý.

---

## 0. Repo này là gì

Series hướng dẫn build app trên Arc, viết cho người Việt không rành crypto và không có nền lập trình. Nội dung gốc là loạt bài "Build on Arc bằng Claude Code" trên X của [@0xhieuxyz](https://x.com/0xhieuxyz) — repo này là bản có nhà, vì X thì bài chết sau 48 giờ.

**Repo thuần hướng dẫn** – không giữ code dự án mẫu song song bên trong (xem mục "08-22: TÁCH TAPTIP" ở trên về lý do và cách tách).

- GitHub: https://github.com/KattyFury/build-on-arc (public)
- Local: `D:\Files\Claude\Build on Arc\build-on-arc`
- Hai dự án dùng làm ví dụ (repo riêng): https://github.com/KattyFury/taptip (chạy thật prompt) + https://github.com/KattyFury/ezwallet (dựng ngược)

## 1. Đang ở đâu

| Bước | Thư mục | Trạng thái |
|---|---|---|
| 1. Lên ý tưởng | `01-ideation/` | ✅ **XONG TRỌN** — lý thuyết + prompt (đã sửa theo lỗi tìm ra qua TapTip lẫn LuckyStaker) + ví dụ TapTip (chạy thật) + EZwallet (dựng ngược) + 6 hướng Arc (09-18) + 9 dòng "prompt từng hụt chỗ nào" |
| 2. Hoàn thiện ý tưởng | `02-hoan-thien-y-tuong/` | ✅ **XONG TRỌN** — prompt + ví dụ TapTip (PRD v1 + v2) + EZwallet (dựng ngược) + "prompt từng hụt chỗ nào" |
| 3. Plan chi tiết | `03-planning/` | ✅ **XONG TRỌN** cả 2 vòng — Vòng 1 (phỏng vấn ngược) + Vòng 2 (chốt stack, ví dụ TapTip v1 + 2 dòng "Khó" bị đổi thật, và EZwallet – bảng thưa hơn vì thiếu dữ liệu "loại gì") + 7 dòng "hụt chỗ nào" ở Vòng 2 |
| 4. Wireframe | `04-wireframe/` | ✅ **XONG TRỌN** — lý thuyết + prompt (5 điều bổ sung rút từ lúc code thật) + ví dụ TapTip (v1, v2, lưới Figma 15 hàng) + EZwallet (lưới 10 hàng, lỗi thiếu khe giữa hàng) + 5 dòng "hụt chỗ nào" |
| 5. Setup môi trường | `05-setup/` | ✅ **XONG TRỌN** — lý thuyết + prompt + ví dụ TapTip (máy có sẵn, file khôi phục Circle, push ≠ deploy) + EZwallet (chế độ mock + 2 tiến trình song song) + "prompt từng hụt chỗ nào" |
| 6. Build | `06-build/` | ✅ README xong (3 giai đoạn). Ví dụ TapTip (đủ 3 giai đoạn, Giai đoạn 3 mới một phần, chưa test máy thật) + EZwallet (Giai đoạn 1/2 đan xen, Giai đoạn 3 đầy đủ nhất) |

### Vòng lặp đã chạy thật lần đầu (Bước 1, 08-06, với TapTip)

Chạy prompt → lòi 5 lỗi quy trình → sửa prompt → ghi lại chỗ hụt. Hai commit tách đôi đúng luật lúc đó: `ed8510d` (example) + `ba5d481` (hướng dẫn).

Lỗi nặng nhất tìm ra: prompt bảo AI "hỏi bạn từng câu" nhưng không bảo nó **DẪN** → AI thành thư ký ghi chép, ngồi đợi user nói xong mới góp ý. Đã thêm khối *"Cách làm việc"* lên đầu prompt. **Bài học chung: prompt nào cũng phải nói rõ ai dẫn ai theo** — lỗi này lặp lại nguyên vẹn ở Vòng 2 Bước 3 khi thử với LuckyStaker (08-21), Claude Code tự trượt vai dù prompt đã ghi rõ.

## 2. CÁCH LÀM VIỆC

Từ 08-22, repo không còn build song song một dự án mẫu bên trong (cách cũ: viết bước nào build bước đó vào `example/`, xem lịch sử git trước ngày đó nếu cần đối chiếu). Cách làm việc hiện tại:

1. Viết/sửa prompt của một bước.
2. **Chạy thử thật trước khi đăng** — không nhất thiết build trong repo này: chạy với dự án thật của tác giả (vd `taptip`), hoặc chạy khô/chạy thật với một ý tưởng khác đưa tới (vd LuckyStaker, 08-21).
3. Prompt hụt chỗ nào, hỏi thiếu, hỏi thừa → sửa README của bước đó + ghi vào mục *"Prompt này từng hụt chỗ nào"* — mục này **bắt buộc**, không phụ thuộc có mục Ví dụ hay không.
4. Có ví dụ thật đáng viết (quyết định có thật, không bịa) thì viết vào mục "Ví dụ" của bước đó, dẫn chứng trỏ link ra ngoài repo nếu dự án đó không nằm trong `build-on-arc`.

Lý do đổi: repo cũ có `example/` là bằng chứng "`git log` cho thấy prompt tiến hoá thế nào", nhưng phải gánh luôn việc vận hành một app thật (deploy, vá bug, backend) trong cùng chỗ – tốn thời gian lẽ ra dành cho viết guide. Cách mới vẫn giữ được yêu cầu "chạy thật trước khi đăng", chỉ bỏ yêu cầu "chạy thật *trong repo này*".

## 3. QUY ĐỊNH VIẾT BÀI

### 3.1 Ví dụ – tuỳ chọn, không bắt buộc

**Đây là chỗ DUY NHẤT giữ quy định viết bài.** `README.md` chỉ nói cho người đọc biết, không chép lại luật dưới đây.

- Mỗi bước **có thể** có một mục ví dụ, tên `## Ví dụ: ...`, đứng ngay sau phần lý thuyết. Không bắt buộc như trước.
- Có ví dụ thì **chỉ nói những gì đã xảy ra thật.** Dẫn chứng thì trỏ link ra file thật (kể cả ở repo khác), không chế số liệu.
- **Cách viết ví dụ:** đừng bịa câu hỏi rồi bịa câu trả lời. Lấy **quyết định có thật** rồi dựng ngược lại thành tình huống đã sinh ra nó.
- Mục *"Prompt này từng hụt chỗ nào"* thì **bắt buộc** ở mọi bước đã có prompt, không phụ thuộc mục Ví dụ.

### 3.2 Tiêu chí ý tưởng đã nới (08-06)

Bước 1 Câu 1 ban đầu bắt ý tưởng phải giải **vấn đề thiết thực**. User nới ra: **thứ vui, thứ mình thích, thứ người ta thật sự muốn dùng cũng được tính** — lì xì không giải quyết vấn đề gì cả nhưng vẫn đáng build.

Cái **không** nới: vẫn phải là thứ mình hoặc người mình biết **thật sự làm ngoài đời**, không ngồi tưởng tượng ra.

### 3.3 Note dán spec dưới mọi prompt

Mọi prompt chuyển giao cần spec bước trước (Bước 2 trở đi) phải kèm câu ghi chú ngay dưới khối prompt:

> Dán kèm nếu bạn đang mở cửa sổ chat mới. Nếu dùng chung 1 cửa sổ chat xuyên suốt từ đầu thì bỏ qua — Chat đã có sẵn context, dán lại là thừa.

Lý do: giả định mặc định "mỗi bước một cửa sổ Chat mới" chỉ đúng với một cách dùng, không phải cách duy nhất. Không note rõ thì người dùng 1 chat xuyên suốt sẽ dán thừa, tốn token vô ích.

### 3.4 Giọng văn

Tiếng Việt đời thường, xưng "mình" / "anh em" như bài gốc trên X. Câu ngắn. Không sáo. Bảng khi so sánh, blockquote cho ghi chú đáng nhớ. Mỗi bước kết bằng một câu dẫn sang bước sau.

**Dấu gạch dài: chỉ dùng en dash `–` (U+2013), không dùng em dash `—` (U+2014)** — luật gốc nằm trong `CLAUDE.md`.

> ✅ **ĐÃ DỌN 08-21.** Toàn bộ file người đọc nhìn thấy đã sạch em dash: `README.md`, 6 file `0N-*/README.md`. (`example/README.md`, `example/docs/*.md` đã tách sang repo `taptip` cùng nội dung đã dọn.)
> Cách quét: `sed -i` thay byte của em dash (U+2014) sang en dash (U+2013) trên đúng danh sách file đó, rồi verify lại bằng `grep -o` phải ra 0.
>
> Còn lại `CLAUDE.md` và `HANDOFF.md` – **cố ý chừa**: hai file này của tác giả, không phải chữ người đọc thấy, và `CLAUDE.md` phải giữ em dash trong dòng phát biểu luật làm ví dụ. Đừng replace-all hai file này.

## 3.6 🔴 BẮT BUỘC đọc trước khi đụng Circle/Arc — đừng tự mò

Trước khi viết bất kỳ code nào đụng tới Circle Wallets hoặc Arc, **load đúng skill/tài nguyên tương ứng trước, đừng tự mò qua docs search rồi thử-sai**. Bài học đau (lúc build TapTip): mất cả buổi vật lộn Entity Secret + Passkey Domain + WebAuthn error vì không load skill `circle:use-modular-wallets` trước khi code — skill đó có sẵn bảng lỗi + rule "ALWAYS complete Console Setup (client key, passkey domain, client URL) before using SDK" ngay từ đầu.

- **Circle Modular Wallets (Passkey, gasless)** → load skill `circle:use-modular-wallets` TRƯỚC. Có bảng lỗi đầy đủ (`NotAllowedError`, `SecurityError`, mã lỗi 155xxx, AA-series), rule bắt buộc (paymaster:true, transport URL path đúng chain, không dùng trên Ethereum mainnet/Solana/Aptos/NEAR).
- **Circle Developer-Controlled Wallets (Entity Secret)** → load skill `circle:use-developer-controlled-wallets` TRƯỚC.
- **Bất kỳ thứ gì khác của Circle** (USDC, Gateway, swap, bridge...) → xem danh sách skill đầy đủ tại https://docs.arc.io/ai/skills, cài qua `/plugin marketplace add circlefin/skills`.
- **Câu hỏi chung về Arc** → Arc MCP đã connect (`docs.arc.io/mcp`), dùng `search_arc_docs`/`query_docs_filesystem_arc_docs` trước khi đoán. Index đầy đủ: https://docs.arc.io/llms.txt.

Chi tiết kỹ thuật sâu hơn (bug thật đã gặp, cách vá) nằm ở `taptip/HANDOFF.md`.

## 4. Git

Remote `origin` = GitHub, branch `main`. Xong việc là commit + push ngay, đừng để commit nằm im ở local.

## 5. Tools tham khảo – dùng ở Bước 6 (code UI thật), KHÔNG dùng ở Bước 4

Bước 4 (wireframe) cố tình bỏ hết style, chỉ khung + label chức năng – mấy tool dưới đây đều thuộc chuyện style/component thật nên chỉ có ích lúc code, không có ích lúc vẽ khung.

- **21st.dev** – https://21st.dev/ – marketplace React+Tailwind, prompt sẵn cho Claude Code/Cursor/v0
- **Astryx (Meta)** – https://astryx.atmeta.com/ – design system chính thức Meta, React 19 + StyleX, 160+ component – hơi nặng đô cho app nhỏ
- **Magic UI** – https://magicui.design/ – component + animation React+Tailwind
- **ui-ux-pro-max-skill** – https://github.com/nextlevelbuilder/ui-ux-pro-max-skill – AI skill sinh design system (màu, font, style) theo project, 114,271 sao (verify qua GitHub API 08-07, số thật cao hơn số đồn)
- **taste-skill** – https://github.com/Leonxlnx/taste-skill (site: tasteskill.dev) – skill chống AI sinh UI "generic slop", 73,405 sao (verify qua GitHub API 08-07)
