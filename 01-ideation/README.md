# Bước 1: Lên ý tưởng

Bước đầu tiên khi build trên Arc. Đọc phần dưới, lấy prompt paste vào AI bạn đang dùng (Claude, ChatGPT...), AI sẽ hỏi bạn từng câu để ra được một ý tưởng đủ điều kiện, kể cả khi đang chưa có gì trong đầu.

## 4 câu hỏi của một ý tưởng hợp lý

### Câu 0: Định hướng Arc

Arc là chain mới với nhiều tính năng đặc biệt. Nên khai thác những tính năng đặc biệt ấy để build app có sự khác biệt, chứ build dự án đơn thuần thì copy mã nguồn của mấy dự án đình đám lẹ hơn.

Usecase chính Arc định hướng trong [docs.arc.io](https://docs.arc.io):
- Peer-to-peer payments
- eCommerce checkout
- Stablecoin FX
- Agentic economy

Có ý tưởng rồi thì check ý tưởng có khớp 1 trong 4 hướng này không. Chưa có ý tưởng thì đây là điểm bắt đầu.

### Câu 1: Thật, và đúng đối tượng

Xác định mình đang làm cho ai, trong chính xã hội Việt Nam. Arc định hướng builder địa phương làm cho người địa phương, những thứ gần gũi như bỏ heo, chơi hụi, từ thiện, lì xì... đều biến thành app được.

**Không nhất thiết phải giải quyết một vấn đề.** Thứ vui, thứ mình thích, thứ người ta thật sự muốn dùng cũng tính. Lì xì đâu giải quyết vấn đề gì — nhưng cả nước vẫn lì xì mỗi năm. App vui mà có người dùng thì đáng build hơn app "giải quyết nỗi đau" mà chẳng ai mở lần thứ hai.

Cái không được nới: nó phải là thứ **chính mình hoặc người mình biết thật sự làm ngoài đời**. Không ngồi tưởng tượng ra một thói quen rồi build app cho cái thói quen đó.

### Câu 2: Dẫn đầu hay cạnh tranh

Ý tưởng có lead mảng này không, tức chưa ai làm? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh của mình là gì. Build một DEX trong 3 tháng, sao không fork Uniswap? Thứ người khác đã làm rất tốt thì tay ngang rất khó cạnh tranh, phải chỉ ra được điểm hơn hẳn.

Ưu điểm cạnh tranh **không bắt buộc phải là công nghệ**. Hiểu một thói quen của người Việt mà công ty nước ngoài không hiểu cũng là một lợi thế, đôi khi còn khó copy hơn.

### Câu 3: Khả thi

Nhiều ý tưởng AI đưa ra nghe hay nhưng không làm được, hoặc quá khó với team nhỏ. Cách chắc ăn: soạn một câu hỏi feasibility rồi vào [docs.arc.io](https://docs.arc.io), mở khung chat AI trong đó mà hỏi.

Ba điều quyết định câu trả lời có xài được hay không:

1. **Hỏi bằng tiếng Anh.** AI của docs trả lời chính xác và đầy đủ hơn hẳn khi hỏi bằng đúng ngôn ngữ của tài liệu.
2. **Đừng hỏi hời hợt.** "Arc có hỗ trợ X không?" thì nhận lại câu trả lời chung chung đúng bằng câu hỏi. Hỏi thẳng vào cơ chế: tên SDK, tên kiến trúc (account abstraction, Paymaster, gas sponsorship), con số cụ thể.
3. **Nó liệt kê 2-3 lựa chọn thì đừng nhận cả hai.** Câu trả lời hay có kiểu "bạn dùng A hoặc B đều được". Đem từng cái đối chiếu ngược lại yêu cầu gốc của mình để loại — hai thứ cùng khả thi trên giấy vẫn có thể xung khắc với thứ mình cần.

Và nhớ hỏi luôn **cái gì KHÔNG có sẵn**. Biết trước phải tự build phần nào đáng giá ngang với biết phần nào có sẵn.

## Prompt để AI guide bạn từ đầu

Copy đoạn dưới, paste vào AI bạn đang dùng:

```
Bạn là cố vấn giúp mình lên ý tưởng build app trên Arc network (docs.arc.io).

CÁCH LÀM VIỆC — quan trọng nhất, đọc kỹ:
Bạn DẪN, mình theo. Ở mỗi câu, bạn chủ động đặt câu hỏi thách thức, chỉ ra chỗ mình nói chưa hợp lý, ép mình làm rõ hơn. ĐỪNG ngồi đợi mình nói hết rồi mới góp ý — mình đến đây để được dẫn, không phải để tự dẫn bạn đi theo mình. Chưa hài lòng với câu trả lời của mình thì hỏi tiếp, đừng cho qua.

Đi từng câu một, xong câu này mới sang câu sau.

Hỏi trước: Bạn có ý tưởng chưa, hay còn chưa biết build gì? Có rồi thì vặn thử ý tưởng đó. Chưa có thì gợi ý theo câu 0.

CÂU 0: Định hướng Arc
Gợi ý 4 định hướng Arc: Peer-to-peer payments, eCommerce checkout, Stablecoin FX, Agentic economy. Có ý tưởng rồi thì check ý tưởng có khớp 1 trong 4 hướng này không.

CÂU 1: Thật, và đúng đối tượng
Xác định mình làm cho ai, trong chính xã hội Việt Nam. Arc định hướng builder địa phương làm cho người địa phương. KHÔNG bắt buộc phải giải quyết một vấn đề — thứ vui, thứ người ta thật sự muốn dùng cũng tính. Nhưng nó phải là thứ mình hoặc người mình biết THẬT SỰ làm ngoài đời, không tưởng tượng ra. Hỏi thêm: yêu cầu quan trọng nhất của sản phẩm này là gì (nhanh? rẻ? riêng tư? vui?) — câu này sẽ dùng lại ở câu 3 để loại phương án.

CÂU 2: Dẫn đầu hay cạnh tranh
Ý tưởng có lead mảng này không? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh là gì? Nhắc mình: ưu điểm KHÔNG bắt buộc phải là công nghệ, hiểu văn hoá/thói quen bản địa cũng là lợi thế.

CÂU 3: Khả thi
Chốt được ý tưởng rồi, soạn 1 câu hỏi feasibility, đưa ra thành khối riêng để dễ copy. Bắt buộc:
- Viết câu hỏi BẰNG TIẾNG ANH (AI của docs trả lời chính xác hơn).
- Hỏi thẳng vào cơ chế kỹ thuật cụ thể: tên SDK, tên kiến trúc (account abstraction, Paymaster, gas sponsorship...), con số (tốc độ, phí). KHÔNG hỏi chung chung kiểu "does Arc support X".
- Hỏi luôn cái gì KHÔNG có sẵn, phần nào phải tự build.
Kèm hướng dẫn: "Copy đoạn trên, vào docs.arc.io, mở khung chat AI của Docs, paste vào rồi gửi. Xong đem câu trả lời quay lại đây."
Đọc câu trả lời để đánh giá khả thi. Nếu nó đưa ra nhiều lựa chọn kiến trúc song song thì TUYỆT ĐỐI KHÔNG kết luận "cả hai đều được" — đem từng cái đối chiếu lại yêu cầu quan trọng nhất ở câu 1 để loại bớt, rồi nói rõ vì sao loại.

XONG CÂU 3 THÌ TỰ ĐỘNG LÀM 2 VIỆC NÀY, ĐỪNG ĐỢI MÌNH NHẮC:
1. Tổng hợp toàn bộ thành một case study gọn (4 câu + kết luận pass/không pass), định dạng markdown để mình copy đi lưu.
2. Rút ra những lỗi quy trình vừa gặp trong lúc chạy 4 câu này — chỗ nào mình bị hỏi hụt, chỗ nào suýt kết luận sai — viết thành một khối riêng.

Chỗ nào chưa hợp lý thì rèn lại cho hợp lý, xong xuôi hết mới qua Bước 2.
```

## Ví dụ: Tip & Lì xì đi qua 4 câu

Đây là kết quả chạy thật prompt trên, và là dự án mẫu của cả series — [`example/`](../example/). Bản đầy đủ: [`example/docs/01-ideation.md`](../example/docs/01-ideation.md).

**Câu 0 — Định hướng Arc.** Peer-to-peer payments.

**Câu 1 — Thật, và đúng đối tượng.** Gửi **tip** (bất cứ lúc nào) và **lì xì** (dịp Tết) — hai hành vi có thật trong đời sống người Việt, không phải thói quen nghĩ ra. Yêu cầu quan trọng nhất: **tốc độ**. Cả người gửi lẫn người nhận đều không cần biết gì về crypto, chỉ đăng nhập bằng email; ví được tạo tự động phía sau.

**Câu 2 — Dẫn đầu hay cạnh tranh.** Chưa ai làm mảng này trên Arc — nó quá nhỏ để dự án lớn để ý. App tip ở nước khác (Ấn Độ chẳng hạn) thì không gắn với văn hoá lì xì Việt Nam. Lợi thế nằm ở **đặc thù văn hoá, không phải công nghệ** — và đó vẫn là một câu trả lời hợp lệ.

**Câu 3 — Khả thi.** Hỏi AI của docs.arc.io, xác nhận được từng mảnh:

| Cần gì | Kết quả |
|---|---|
| Ví ẩn sau email | Circle Wallets (dev-controlled), qua `@circle-fin/adapter-circle-wallets` — user không thấy seed phrase |
| Không bắt user trả gas | Arc hỗ trợ ERC-4337 + Paymaster → app trả gas thay user |
| Đủ nhanh | Finality dưới 1 giây, benchmark thực tế **<350ms** |
| Phí chịu được | ~$0.01/giao dịch, max $0.20 — hợp lý với khoản $0.50–$20 |

**Và thứ KHÔNG có sẵn:** không có UI dựng sẵn cho luồng "gửi qua email", chỉ có `kit.send()` ở tầng SDK. Phần đăng nhập email + gửi tới email người khác phải tự build.

> Chỗ đáng học nhất ở câu 3 không phải cái bảng, mà là **một quyết định loại bớt**. Docs trả lời rằng dùng Circle Wallets hay Privy đều được. Nhưng yêu cầu số một ở câu 1 là *nhanh*, mà Privy bắt user tự ký từng giao dịch — thêm một nhịp chờ. Nên loại Privy, chọn Circle Wallets developer-controlled. Hai thứ cùng "khả thi" vẫn có thể một cái phá mất thứ mình cần nhất.

## Prompt này từng hụt chỗ nào

Bản đầu của prompt chạy ra được ý tưởng, nhưng lộ 5 chỗ hụt. Đã sửa hết vào khối prompt ở trên.

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| 1 | Câu hỏi feasibility viết bằng tiếng Việt → AI của docs trả lời sơ sài | Bắt viết **bằng tiếng Anh** |
| 2 | Hỏi chung chung "có hỗ trợ X không" → nhận về câu trả lời chung chung | Bắt hỏi thẳng tên SDK, tên kiến trúc, con số |
| 3 | Docs đưa 2 lựa chọn, suýt kết luận "cả hai đều được" | Bắt đối chiếu lại **yêu cầu quan trọng nhất** ở câu 1 để loại — và thêm hẳn câu hỏi "yêu cầu quan trọng nhất là gì" vào câu 1 để có cái mà đối chiếu |
| 4 | **Nặng nhất:** AI ngồi phản ứng theo người dùng thay vì dẫn | Thêm khối *"Cách làm việc"* lên đầu prompt: bạn DẪN, chủ động vặn, chưa hài lòng thì hỏi tiếp, đừng cho qua |
| 5 | Xong câu 3 rồi đứng im, phải nhắc hai lần mới tổng hợp | Bắt tự động làm 2 việc cuối: xuất case study + rút lỗi quy trình |

Lỗi số 4 là lỗi làm hỏng nhiều nhất. Prompt bảo AI "hỏi bạn từng câu" nhưng không bảo nó *dẫn*, nên nó thành thư ký ghi chép: bạn nói gì nó gật nấy, chỉ góp ý khi bạn đã nói xong. Bạn tự dẫn được thì cần gì cố vấn.
