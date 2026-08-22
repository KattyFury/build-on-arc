# HANDOFF – build-on-arc

> File làm việc của tác giả, không phải nội dung cho người đọc series. Mở máy mới thì đọc file này trước.
> Luật cho Claude Code nằm ở `CLAUDE.md`. File này ghi **đang ở đâu** và **quy định viết bài**.
> **Cập nhật:** 2026-08-22 (tách TapTip ra repo riêng `KattyFury/taptip`, repo này trở về thuần hướng dẫn – xem mục ngay dưới). Trước đó cùng đợt: sửa Bước 1 + Bước 3 Vòng 2 theo lỗi thật tìm ra khi thử với LuckyStaker; thêm Vòng 2 "chốt stack" vào Bước 3, đóng nốt ví dụ + chỗ hụt của Bước 4, dọn sạch em dash.

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
- Dự án từng là ví dụ, giờ ở repo riêng: https://github.com/KattyFury/taptip

## 1. Đang ở đâu

| Bước | Thư mục | Trạng thái |
|---|---|---|
| 1. Lên ý tưởng | `01-ideation/` | ✅ **XONG TRỌN** — lý thuyết + prompt (đã sửa theo lỗi tìm ra qua TapTip lẫn LuckyStaker) + ví dụ thật (TapTip, link ra `taptip` repo) + 9 dòng "prompt từng hụt chỗ nào" |
| 2. Hoàn thiện ý tưởng | `02-hoan-thien-y-tuong/` | ✅ **XONG TRỌN** — prompt + ví dụ thật (TapTip) + "prompt từng hụt chỗ nào" |
| 3. Plan chi tiết | `03-planning/` | ✅ **XONG TRỌN** cả 2 vòng — Vòng 1 (phỏng vấn ngược) + Vòng 2 (chốt stack, dẫn chứng bằng stack thật của TapTip) + 7 dòng "hụt chỗ nào" ở Vòng 2 |
| 4. Wireframe | `04-wireframe/` | ✅ **XONG TRỌN** — lý thuyết + prompt (5 điều bổ sung rút từ lúc code thật) + ví dụ thật (TapTip) + 5 dòng "hụt chỗ nào" |
| 5. Setup môi trường | `05-setup/` | ✅ **XONG TRỌN** — lý thuyết + prompt + ví dụ thật (TapTip) + "prompt từng hụt chỗ nào" |
| 6. Build | `06-build/` | ✅ README xong (3 giai đoạn). Ví dụ Giai đoạn 1+2 đã điền (TapTip). Giai đoạn 3 tạm gác cùng lúc TapTip tách repo — chưa có người dùng thật để viết |

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
