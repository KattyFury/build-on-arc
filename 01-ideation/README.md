# Bước 1: Lên ý tưởng

Bước đầu tiên khi build trên Arc. Đọc phần dưới, lấy prompt paste vào AI bạn đang dùng (Claude, ChatGPT...), AI sẽ hỏi bạn từng câu để ra được một ý tưởng đủ điều kiện, kể cả khi đang chưa có gì trong đầu.

## 4 câu hỏi của một ý tưởng hợp lý

### Câu 0: Định hướng Arc

Arc là chain mới với nhiều tính năng đặc biệt. Nên khai thác những tính năng đặc biệt ấy để build app có sự khác biệt, chứ build dự án đơn thuần thì copy mã nguồn của mấy dự án đình đám lẹ hơn.

Usecase chính Arc định hướng trong [docs.arc.io](https://docs.arc.io):
- **Peer-to-peer payments** – chuyển tiền trực tiếp giữa người với người bằng stablecoin, nhanh, phí thấp, chốt giao dịch chắc chắn
- **eCommerce checkout** – cửa hàng online nhận thanh toán stablecoin, chốt nhanh, có sẵn phần tuân thủ
- **Stablecoin FX** – đổi giữa các stablecoin theo thời gian thực, giá minh bạch, phí đoán trước được
- **Agentic economy** – AI agent tự phối hợp, tự giao kèo và tự thanh toán cho nhau
- **Prediction markets** – thị trường dự đoán phi tập trung, kết quả chốt bằng oracle, giao dịch token vị thế
- **Borrow and lend** – giao thức vay/cho vay có tài sản thế chấp, vay thẳng bằng USDC

**Câu 0 chỉ là điểm bắt đầu cho người chưa có ý tưởng, không phải bộ lọc.** Chưa biết build gì thì 6 hướng này là chỗ để bắt đầu nghĩ. Có ý tưởng rồi thì **bỏ qua Câu 0, đi thẳng Câu 1** – đừng đem ý tưởng ra so với 6 gạch đầu dòng này, khớp hay không khớp đều không nói lên ý tưởng tốt hay dở. Ý tưởng có tận dụng được đặc thù kỹ thuật của Arc (USDC làm gas, finality nhanh, Memo, gas sponsorship...) hay không thì để Câu 3 soi, không phải ở đây.

> Danh sách này đổi theo docs. Lúc series mới viết, docs.arc.io chỉ có 4 hướng đầu – 2 hướng sau (Prediction markets, Borrow and lend) được Arc thêm vào sau. Trước khi dùng, mở docs ra xem lại một lượt cho chắc.

Một điều áp cho cả người đã có ý tưởng: ý tưởng có nhắc tới cái gì cụ thể của Arc hoặc hệ sinh thái quanh nó (tên token, cơ chế, tính năng chưa chắc đã sống) thì tra ngay lúc này – đừng để dồn tới Câu 3 mới phát hiện tiền đề sai, lúc đó đã lỡ tưởng tượng cả ý tưởng trên nền sai.

### Câu 1: Thật, và đúng đối tượng

Xác định mình đang làm cho ai, trong chính xã hội Việt Nam. Arc định hướng builder địa phương làm cho người địa phương, những thứ gần gũi như bỏ heo, chơi hụi, từ thiện, lì xì... đều biến thành app được.

**Không nhất thiết phải giải quyết một vấn đề.** Thứ vui, thứ mình thích, thứ người ta thật sự muốn dùng cũng tính. Lì xì đâu giải quyết vấn đề gì – nhưng cả nước vẫn lì xì mỗi năm. App vui mà có người dùng thì đáng build hơn app "giải quyết nỗi đau" mà chẳng ai mở lần thứ hai.

Cái không được nới: nó phải là thứ **chính mình hoặc người mình biết thật sự làm ngoài đời**. Không ngồi tưởng tượng ra một thói quen rồi build app cho cái thói quen đó.

### Câu 2: Dẫn đầu hay cạnh tranh

Ý tưởng có lead mảng này không, tức chưa ai làm? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh của mình là gì. Build một DEX trong 3 tháng, sao không fork Uniswap? Thứ người khác đã làm rất tốt thì tay ngang rất khó cạnh tranh, phải chỉ ra được điểm hơn hẳn.

Ưu điểm cạnh tranh **không bắt buộc phải là công nghệ**. Hiểu một thói quen của người Việt mà công ty nước ngoài không hiểu cũng là một lợi thế, đôi khi còn khó copy hơn.

### Câu 3: Khả thi

Nhiều ý tưởng AI đưa ra nghe hay nhưng không làm được, hoặc quá khó với team nhỏ. Cách chắc ăn: soạn một câu hỏi feasibility rồi vào [docs.arc.io](https://docs.arc.io), mở khung chat AI trong đó mà hỏi.

**Đây không phải một bước làm một lần rồi xong.** Ý tưởng ở Bước 1 mới là bản thô – Bước 2, 3 sẽ khui ra thêm chi tiết kỹ thuật cụ thể (dùng SDK nào, cơ chế ví nào...), app có thể dùng nhiều cơ chế Arc khác nhau chứ không chỉ một. Hễ lúc nào chốt phải dùng một cơ chế cụ thể của Arc, tra docs.arc.io ngay lúc đó, đừng đợi dồn lại. Câu 3 ở đây là cửa **tối thiểu** trước khi qua Bước 2 – xác nhận hướng đi lớn có khả thi không, không phải xác nhận hết mọi chi tiết sẽ gặp về sau.

Cũng cần tách rõ nguồn tra cứu: câu hỏi thuộc **cơ chế của Arc** (SDK, kiến trúc on-chain, tốc độ, phí, tính năng còn sống hay chưa) thì hỏi docs.arc.io. Câu hỏi **không thuộc Arc** (tokenomics/roadmap của dự án hay token khác, tính năng của bên thứ ba) thì tự search web riêng – ép AI của docs.arc.io trả lời ngoài phạm vi của nó, nó sẽ đoán bừa chứ không biết thật.

Ba điều quyết định câu trả lời có xài được hay không:

1. **Hỏi bằng tiếng Anh.** AI của docs trả lời chính xác và đầy đủ hơn hẳn khi hỏi bằng đúng ngôn ngữ của tài liệu.
2. **Đừng hỏi hời hợt.** "Arc có hỗ trợ X không?" thì nhận lại câu trả lời chung chung đúng bằng câu hỏi. Hỏi thẳng vào cơ chế: tên SDK, tên kiến trúc (account abstraction, Paymaster, gas sponsorship), con số cụ thể.
3. **Nó liệt kê 2-3 lựa chọn thì đừng nhận cả hai.** Câu trả lời hay có kiểu "bạn dùng A hoặc B đều được". Đem từng cái đối chiếu ngược lại yêu cầu gốc của mình để loại – hai thứ cùng khả thi trên giấy vẫn có thể xung khắc với thứ mình cần.

Và nhớ hỏi luôn **cái gì KHÔNG có sẵn**. Biết trước phải tự build phần nào đáng giá ngang với biết phần nào có sẵn.

## Prompt để AI guide bạn từ đầu

Copy đoạn dưới, paste vào AI bạn đang dùng:

```
Bạn là cố vấn giúp mình lên ý tưởng build app trên Arc network (docs.arc.io).

CÁCH LÀM VIỆC – quan trọng nhất, đọc kỹ:
Bạn DẪN, mình theo. Ở mỗi câu, bạn chủ động đặt câu hỏi thách thức, chỉ ra chỗ mình nói chưa hợp lý, ép mình làm rõ hơn. ĐỪNG ngồi đợi mình nói hết rồi mới góp ý – mình đến đây để được dẫn, không phải để tự dẫn bạn đi theo mình. Chưa hài lòng với câu trả lời của mình thì hỏi tiếp, đừng cho qua.

Đi từng câu một, xong câu này mới sang câu sau.

Hỏi trước: Bạn có ý tưởng chưa, hay còn chưa biết build gì? Có rồi thì BỎ QUA câu 0, vào thẳng câu 1 mà vặn ý tưởng đó. Chưa có thì bắt đầu từ câu 0.
Dù có hay chưa: nếu ý tưởng nhắc tới cái gì cụ thể của Arc hoặc hệ sinh thái quanh nó (tên token, cơ chế, tính năng chưa chắc đã sống) – tra nhanh ngay bây giờ, đừng để dồn tới câu 3 mới phát hiện tiền đề sai.

CÂU 0: Định hướng Arc (CHỈ khi mình chưa có ý tưởng)
Gợi ý 6 định hướng Arc: Peer-to-peer payments, eCommerce checkout, Stablecoin FX, Agentic economy, Prediction markets, Borrow and lend – đây là điểm bắt đầu để gợi hướng cho người chưa có ý tưởng, KHÔNG phải bộ lọc. Mình đã có ý tưởng thì không đem nó ra so với 6 hướng này, không hỏi "ý tưởng thuộc hướng nào", không loại hay ép pivot vì không khớp. Chuyện ý tưởng có dùng được đặc thù kỹ thuật của Arc hay không thì để câu 3 soi.

CÂU 1: Thật, và đúng đối tượng
Xác định mình làm cho ai, trong chính xã hội Việt Nam. Arc định hướng builder địa phương làm cho người địa phương. KHÔNG bắt buộc phải giải quyết một vấn đề – thứ vui, thứ người ta thật sự muốn dùng cũng tính. Nhưng nó phải là thứ mình hoặc người mình biết THẬT SỰ làm ngoài đời, không tưởng tượng ra. Hỏi thêm: yêu cầu quan trọng nhất của sản phẩm này là gì (nhanh? rẻ? riêng tư? vui?) – câu này sẽ dùng lại ở câu 3 để loại phương án.

CÂU 2: Dẫn đầu hay cạnh tranh
Ý tưởng có lead mảng này không? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh là gì? Nhắc mình: ưu điểm KHÔNG bắt buộc phải là công nghệ, hiểu văn hoá/thói quen bản địa cũng là lợi thế.

CÂU 3: Khả thi (cửa tối thiểu trước khi qua Bước 2, không phải lần kiểm duy nhất)
Chỉ ra ý tưởng dùng tới đặc thù kỹ thuật nào của Arc (USDC làm gas, finality nhanh, Memo, gas sponsorship...). Đây là chỗ soi chuyện "có đáng build trên Arc không", không phải câu 0.
Trước khi soạn câu hỏi, tách rõ 2 loại thắc mắc: cái gì thuộc CƠ CHẾ CỦA ARC (SDK, kiến trúc on-chain, tốc độ, phí, tính năng còn sống hay chưa) thì hỏi docs.arc.io. Cái gì KHÔNG thuộc Arc (tokenomics/roadmap của dự án hay token khác, tính năng bên thứ ba) thì bảo mình tự search web riêng – đừng ép docs.arc.io trả lời ngoài phạm vi của nó.

Chốt được ý tưởng rồi, soạn 1 câu hỏi feasibility cho phần thuộc Arc, đưa ra thành khối riêng để dễ copy. Bắt buộc:
- Viết câu hỏi BẰNG TIẾNG ANH (AI của docs trả lời chính xác hơn).
- Hỏi thẳng vào cơ chế kỹ thuật cụ thể: tên SDK, tên kiến trúc (account abstraction, Paymaster, gas sponsorship...), con số (tốc độ, phí). KHÔNG hỏi chung chung kiểu "does Arc support X".
- Hỏi luôn cái gì KHÔNG có sẵn, phần nào phải tự build.
Kèm hướng dẫn: "Copy đoạn trên, vào docs.arc.io, mở khung chat AI của Docs, paste vào rồi gửi. Xong đem câu trả lời quay lại đây."
Đọc câu trả lời để đánh giá khả thi. Nếu nó đưa ra nhiều lựa chọn kiến trúc song song thì TUYỆT ĐỐI KHÔNG kết luận "cả hai đều được" – đem từng cái đối chiếu lại yêu cầu quan trọng nhất ở câu 1 để loại bớt, rồi nói rõ vì sao loại.

Nhắc mình: đây là cửa TỐI THIỂU trước khi qua Bước 2, không phải lần kiểm feasibility duy nhất của cả dự án. Bước 2, 3 sẽ khui thêm chi tiết kỹ thuật cụ thể – hễ tới lúc phải chốt dùng đúng một cơ chế nào đó của Arc, quay lại hỏi docs.arc.io ngay lúc đó, đừng đợi gộp lại review một lần.

XONG CÂU 3 THÌ TỰ ĐỘNG LÀM 2 VIỆC NÀY, ĐỪNG ĐỢI MÌNH NHẮC:
1. Tổng hợp toàn bộ thành một case study gọn (4 câu + kết luận pass/không pass), định dạng markdown để mình copy đi lưu.
2. Rút ra những lỗi quy trình vừa gặp trong lúc chạy 4 câu này – chỗ nào mình bị hỏi hụt, chỗ nào suýt kết luận sai – viết thành một khối riêng.

Chỗ nào chưa hợp lý thì rèn lại cho hợp lý, xong xuôi hết mới qua Bước 2.
```

## Ví dụ: TapTip và EZwallet đi qua 4 câu

Hai dự án thật của tác giả, cùng hướng Peer-to-peer payments, cùng đối tượng có cả người lớn tuổi – nhưng chốt yêu cầu số một khác nhau, nên đi ra hai app khác hẳn. Đặt cạnh nhau để thấy 4 câu này lọc ra được gì.

### TapTip – chạy thật đúng prompt trên

[`KattyFury/taptip`](https://github.com/KattyFury/taptip) – Tip & Lì xì nhanh trên Arc, từng build song song với series rồi tách ra repo riêng. Đây là kết quả chạy thật prompt trên, bản đầy đủ: [`docs/01-ideation.md`](https://github.com/KattyFury/taptip/blob/main/docs/01-ideation.md).

**Câu 0 – Định hướng Arc.** Peer-to-peer payments.

**Câu 1 – Thật, và đúng đối tượng.** Gửi **tip** (bất cứ lúc nào) và **lì xì** (dịp Tết) – hai hành vi có thật trong đời sống người Việt, không phải thói quen nghĩ ra. Yêu cầu quan trọng nhất: **tốc độ**. Cả người gửi lẫn người nhận đều không cần biết gì về crypto, chỉ đăng nhập bằng email; ví được tạo tự động phía sau.

**Câu 2 – Dẫn đầu hay cạnh tranh.** Chưa ai làm mảng này trên Arc – nó quá nhỏ để dự án lớn để ý. App tip ở nước khác (Ấn Độ chẳng hạn) thì không gắn với văn hoá lì xì Việt Nam. Lợi thế nằm ở **đặc thù văn hoá, không phải công nghệ** – và đó vẫn là một câu trả lời hợp lệ.

**Câu 3 – Khả thi.** Hỏi AI của docs.arc.io, xác nhận được từng mảnh:

| Cần gì | Kết quả |
|---|---|
| Ví ẩn sau email | Circle Wallets (dev-controlled) – user không thấy seed phrase |
| Không bắt user trả gas | Arc hỗ trợ ERC-4337 + Paymaster → app trả gas thay user |
| Đủ nhanh | Finality dưới 1 giây, benchmark thực tế **<350ms** |
| Phí chịu được | ~$0.01/giao dịch, max $0.20 – hợp lý với khoản $0.50–$20 |

**Và thứ KHÔNG có sẵn:** không có UI dựng sẵn cho luồng "gửi qua email", chỉ có `kit.send()` ở tầng SDK. Phần đăng nhập email + gửi tới email người khác phải tự build.

> Chỗ đáng học nhất ở câu 3 là **một quyết định loại bớt**. Docs trả lời rằng dùng Circle Wallets hay Privy đều được. Nhưng yêu cầu số một ở câu 1 là *nhanh*, mà Privy bắt user tự ký từng giao dịch – thêm một nhịp chờ. Nên loại Privy, chọn Circle Wallets developer-controlled.
>
> Và phần sau của câu chuyện còn đáng học hơn: quyết định đúng ở đây **vẫn bị lọt mất lúc code**. App mẫu TapTip fork về (Bước 3) chạy sẵn kiểu ví passkey – mỗi lần tip phải quét Face ID, đúng cái nhịp chờ vừa loại Privy để tránh. Không ai đối chiếu lại code với tài liệu Bước 1, nên app chạy sai kiến trúc gần một tháng, tới lúc kiểm toán mới lòi ra và đổi hẳn sang developer-controlled như đã chốt. Chốt ở Bước 1 xong không có nghĩa là code sẽ tự theo – tới Bước 6 vẫn phải mở lại tài liệu ra đối chiếu. Còn dòng "app trả gas thay user" thì tới giờ vẫn chưa bật: ví đang tự trả gas bằng USDC của chính nó.

### EZwallet – dựng ngược từ quyết định có thật

Đây là dự án thật của tác giả – [`KattyFury/ezwallet`](https://github.com/KattyFury/ezwallet), ví crypto cho người dùng phổ thông/người già ("A crypto wallet simple enough for my mom to use"), chạy thật trên Arc Testnet tại [ezwallet.cash](https://ezwallet.cash). Dự án không build theo đúng trình tự 4 câu của bước này (ra đời trước cả series), nên phần dưới **dựng ngược** từ quyết định có thật – không phải chép lại một lượt chat đã xảy ra.

**Câu 0 – Định hướng Arc.** Peer-to-peer payments – gửi, nhận, quét QR.

**Câu 1 – Thật, và đúng đối tượng.** Người dùng phổ thông, cụ thể tới mức lấy mẹ mình làm phép thử. Yêu cầu quan trọng nhất **không phải tốc độ mà là đơn giản**: không seed phrase (đăng nhập bằng email + PIN, khoá giữ bởi Circle MPC), không token gas riêng (Arc dùng thẳng USDC làm gas nên khỏi phải mua thêm một đồng chỉ để trả phí), chữ to, mỗi màn một hành động chính.

**Câu 2 – Dẫn đầu hay cạnh tranh.** Không cạnh tranh bằng công nghệ – ví crypto thiếu gì. Cạnh tranh bằng **đối tượng bị bỏ quên**: hầu hết ví crypto dựng cho người đã hiểu crypto, seed phrase/địa chỉ hex/chọn mạng là rào cản với người mới, và là lý do chặn hẳn với người lớn tuổi. Giống kiểu trả lời của TapTip ("đặc thù văn hoá, không phải công nghệ") nhưng lệch trục: ở đây là **đặc thù đối tượng người dùng**.

**Câu 3 – Khả thi.** Cơ chế Arc thật đã dùng, không phải tra một lần rồi thôi mà gom dần qua nhiều lần build:

| Cần gì | Kết quả |
|---|---|
| Không bắt user mua token gas riêng | Arc dùng USDC làm gas token gốc (18 decimals on-chain) – ví chỉ cần đúng một loại tiền |
| Gửi kèm lời nhắn on-chain | Contract Memo (precompile của Arc) – ghi lời nhắn kèm giao dịch, không cần dịch vụ ngoài |
| Gộp nhiều thao tác vào 1 lần ký | `Multicall3From` – batch approve + swap thành đúng 1 giao dịch, 1 lần nhập PIN (thay vì 2 lần) |
| Đọc số dư nhiều token không tốn nhiều request | `Multicall3` gộp lại 1 lệnh gọi, quan trọng vì RPC công cộng của Arc giới hạn request khá chặt |

**Và thứ KHÔNG có sẵn:** `wrangler` CLI (Cloudflare) không có lệnh gắn custom domain cho Pages – phải tự gọi thẳng REST API mới xong việc này.

> Chỗ đáng học nhất không nằm ở câu 3 mà là một quyết định về sau, cùng tinh thần "loại bớt phương án khả thi trên giấy": ban đầu QR mặc định chỉ vẽ địa chỉ `0x…` trần – đúng chuẩn, khả thi, nhưng địa chỉ EVM giống hệt nhau trên mọi chain nên ví bất kỳ đang mở sai mạng vẫn quét gửi được, tiền sang nhầm chain là mất luôn. Đối tượng là người lớn tuổi, không có cửa tự nhận ra sai mạng. Nên QR bị **khoá cứng vào đúng một mạng Arc**, chấp nhận validate chặt hơn để đổi lấy an toàn – "khả thi" và "an toàn cho đúng đối tượng" không phải lúc nào cũng là một.

## Prompt này từng hụt chỗ nào

Bản đầu của prompt chạy ra được ý tưởng, nhưng lộ 5 chỗ hụt (# 1-5). Bốn chỗ hụt sau (# 6-9) lộ ra ở một lượt thử thật khác, với một ý tưởng không khớp thẳng vào hướng nào của Arc (lúc đó docs mới có 4 hướng) và có dùng nhiều cơ chế khác nhau của Arc lẫn ngoài Arc – đúng kiểu tình huống bản đầu của Câu 0 và Câu 3 chưa xử lý được. Chỗ hụt #10 lộ ra ở lượt chạy với DailyReal (nhật ký ảnh thật, khoá vĩnh viễn trên Arc) – một ý tưởng có sẵn từ đầu và không thuộc hướng nào trong 6 hướng. Đã sửa hết vào khối prompt ở trên.

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| 1 | Câu hỏi feasibility viết bằng tiếng Việt → AI của docs trả lời sơ sài | Bắt viết **bằng tiếng Anh** |
| 2 | Hỏi chung chung "có hỗ trợ X không" → nhận về câu trả lời chung chung | Bắt hỏi thẳng tên SDK, tên kiến trúc, con số |
| 3 | Docs đưa 2 lựa chọn, suýt kết luận "cả hai đều được" | Bắt đối chiếu lại **yêu cầu quan trọng nhất** ở câu 1 để loại – và thêm hẳn câu hỏi "yêu cầu quan trọng nhất là gì" vào câu 1 để có cái mà đối chiếu |
| 4 | **Nặng nhất:** AI ngồi phản ứng theo người dùng thay vì dẫn | Thêm khối *"Cách làm việc"* lên đầu prompt: bạn DẪN, chủ động vặn, chưa hài lòng thì hỏi tiếp, đừng cho qua |
| 5 | Xong câu 3 rồi đứng im, phải nhắc hai lần mới tổng hợp | Bắt tự động làm 2 việc cuối: xuất case study + rút lỗi quy trình |
| 6 | Câu 0 đọc như danh sách đóng – ý tưởng không khớp hướng nào trong mấy gạch đầu dòng đó thì không rõ có bị loại hay không | Ghi rõ đây là gợi ý để có điểm bắt đầu, không phải rào chắn – không khớp cũng không sao miễn có dùng đặc thù kỹ thuật thật của Arc |
| 7 | Ý tưởng nhắc tới chi tiết cụ thể của Arc (tên token, cơ chế) không được kiểm tra ngay từ đầu – tiền đề sai chỉ lộ ra muộn ở câu 3, sau khi đã tưởng tượng cả ý tưởng trên nền đó | Thêm nhắc ngay ở câu 0: ý tưởng nhắc thứ cụ thể của Arc thì tra ngay, đừng để dồn |
| 8 | Câu 3 được thiết kế như một bước làm 1 lần duy nhất, nhưng feasibility thật ra cần tra liên tục xuyên suốt Bước 1-3 – ý tưởng càng đi sâu càng lộ thêm chi tiết kỹ thuật cụ thể cần verify, app có thể dùng nhiều cơ chế Arc khác nhau chứ không phải một | Ghi rõ câu 3 là cửa TỐI THIỂU trước khi qua Bước 2, không phải lần duy nhất – hễ chốt dùng cơ chế Arc cụ thể nào ở bước sau, quay lại tra ngay lúc đó |
| 9 | docs.arc.io bị hỏi cả câu hỏi không liên quan gì tới Arc (tokenomics/roadmap của token hay dự án khác) – AI của docs trả lời bừa vì ngoài phạm vi của nó | Tách rõ: câu hỏi thuộc cơ chế Arc thì hỏi docs.arc.io, câu hỏi ngoài Arc thì tự search web riêng |
| 10 | Sửa ở #6 chưa đủ: prompt vẫn bảo "có ý tưởng rồi thì check thử có khớp 1 trong 6 hướng không", tức vẫn đem ý tưởng có sẵn ra so – Câu 0 vẫn mang dáng một bộ lọc, chỉ là bộ lọc "dễ tính" | Câu 0 chỉ dành cho người chưa có ý tưởng. Có ý tưởng rồi thì bỏ qua, vào thẳng Câu 1. Chuyện có dùng đặc thù kỹ thuật của Arc hay không chuyển sang Câu 3 |

Lỗi số 4 là lỗi làm hỏng nhiều nhất trong lượt đầu. Prompt bảo AI "hỏi bạn từng câu" nhưng không bảo nó *dẫn*, nên nó thành thư ký ghi chép: bạn nói gì nó gật nấy, chỉ góp ý khi bạn đã nói xong. Bạn tự dẫn được thì cần gì cố vấn.

Lỗi số 8 là lỗi nặng nhất trong lượt thứ hai, và dễ tái phát nhất nếu không ghi rõ: bất kỳ bước nào có chữ "kiểm tra khả thi" cũng dễ bị đọc thành một cửa làm-một-lần-rồi-quên, trong khi bản chất công việc đó là tra cứu liên tục mỗi khi có thêm một quyết định kỹ thuật mới.
