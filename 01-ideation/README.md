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

**Đây là gợi ý để có điểm bắt đầu, không phải rào chắn.** Có ý tưởng rồi thì check thử có khớp 1 trong 4 hướng này không – không khớp cái nào cũng không sao, không loại. Chỉ cần ý tưởng có dùng đặc thù kỹ thuật thật của Arc (USDC làm gas, finality nhanh, gas sponsorship...), không phải mọi ý tưởng hay đều nhét vừa vào 1 trong 4 gạch đầu dòng đó. Chưa có ý tưởng thì đây là điểm bắt đầu để gợi hướng.

Ý tưởng có nhắc tới cái gì cụ thể của Arc hoặc hệ sinh thái quanh nó (tên token, cơ chế, tính năng chưa chắc đã sống) thì tra ngay lúc này – đừng để dồn tới Câu 3 mới phát hiện tiền đề sai, lúc đó đã lỡ tưởng tượng cả ý tưởng trên nền sai.

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

Hỏi trước: Bạn có ý tưởng chưa, hay còn chưa biết build gì? Có rồi thì vặn thử ý tưởng đó. Chưa có thì gợi ý theo câu 0.

CÂU 0: Định hướng Arc
Gợi ý 4 định hướng Arc: Peer-to-peer payments, eCommerce checkout, Stablecoin FX, Agentic economy – đây là GỢI Ý để có điểm bắt đầu, không phải rào chắn. Có ý tưởng rồi thì check thử có khớp 1 trong 4 hướng này không; không khớp cái nào cũng KHÔNG loại, chỉ cần ý tưởng dùng đặc thù kỹ thuật thật của Arc (USDC làm gas, finality nhanh, gas sponsorship...). Chưa có ý tưởng thì đây là điểm bắt đầu để gợi hướng.
Nếu ý tưởng nhắc tới cái gì cụ thể của Arc hoặc hệ sinh thái quanh nó (tên token, cơ chế, tính năng chưa chắc đã sống) – tra nhanh ngay bây giờ, đừng để dồn tới câu 3 mới phát hiện tiền đề sai.

CÂU 1: Thật, và đúng đối tượng
Xác định mình làm cho ai, trong chính xã hội Việt Nam. Arc định hướng builder địa phương làm cho người địa phương. KHÔNG bắt buộc phải giải quyết một vấn đề – thứ vui, thứ người ta thật sự muốn dùng cũng tính. Nhưng nó phải là thứ mình hoặc người mình biết THẬT SỰ làm ngoài đời, không tưởng tượng ra. Hỏi thêm: yêu cầu quan trọng nhất của sản phẩm này là gì (nhanh? rẻ? riêng tư? vui?) – câu này sẽ dùng lại ở câu 3 để loại phương án.

CÂU 2: Dẫn đầu hay cạnh tranh
Ý tưởng có lead mảng này không? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh là gì? Nhắc mình: ưu điểm KHÔNG bắt buộc phải là công nghệ, hiểu văn hoá/thói quen bản địa cũng là lợi thế.

CÂU 3: Khả thi (cửa tối thiểu trước khi qua Bước 2, không phải lần kiểm duy nhất)
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

## Ví dụ: Tip & Lì xì đi qua 4 câu

Đây là kết quả chạy thật prompt trên với **TapTip** – lúc dự án này còn build song song với series, giờ đã tách sang repo riêng [`KattyFury/taptip`](https://github.com/KattyFury/taptip). Bản đầy đủ: [`docs/01-ideation.md`](https://github.com/KattyFury/taptip/blob/main/docs/01-ideation.md).

**Câu 0 – Định hướng Arc.** Peer-to-peer payments.

**Câu 1 – Thật, và đúng đối tượng.** Gửi **tip** (bất cứ lúc nào) và **lì xì** (dịp Tết) – hai hành vi có thật trong đời sống người Việt, không phải thói quen nghĩ ra. Yêu cầu quan trọng nhất: **tốc độ**. Cả người gửi lẫn người nhận đều không cần biết gì về crypto, chỉ đăng nhập bằng email; ví được tạo tự động phía sau.

**Câu 2 – Dẫn đầu hay cạnh tranh.** Chưa ai làm mảng này trên Arc – nó quá nhỏ để dự án lớn để ý. App tip ở nước khác (Ấn Độ chẳng hạn) thì không gắn với văn hoá lì xì Việt Nam. Lợi thế nằm ở **đặc thù văn hoá, không phải công nghệ** – và đó vẫn là một câu trả lời hợp lệ.

**Câu 3 – Khả thi.** Hỏi AI của docs.arc.io, xác nhận được từng mảnh:

| Cần gì | Kết quả |
|---|---|
| Ví ẩn sau email | Circle Wallets (dev-controlled), qua `@circle-fin/adapter-circle-wallets` – user không thấy seed phrase |
| Không bắt user trả gas | Arc hỗ trợ ERC-4337 + Paymaster → app trả gas thay user |
| Đủ nhanh | Finality dưới 1 giây, benchmark thực tế **<350ms** |
| Phí chịu được | ~$0.01/giao dịch, max $0.20 – hợp lý với khoản $0.50–$20 |

**Và thứ KHÔNG có sẵn:** không có UI dựng sẵn cho luồng "gửi qua email", chỉ có `kit.send()` ở tầng SDK. Phần đăng nhập email + gửi tới email người khác phải tự build.

> Chỗ đáng học nhất ở câu 3 không phải cái bảng, mà là **một quyết định loại bớt**. Docs trả lời rằng dùng Circle Wallets hay Privy đều được. Nhưng yêu cầu số một ở câu 1 là *nhanh*, mà Privy bắt user tự ký từng giao dịch – thêm một nhịp chờ. Nên loại Privy, chọn Circle Wallets developer-controlled. Hai thứ cùng "khả thi" vẫn có thể một cái phá mất thứ mình cần nhất.

## Prompt này từng hụt chỗ nào

Bản đầu của prompt chạy ra được ý tưởng, nhưng lộ 5 chỗ hụt (# 1-5). Bốn chỗ hụt sau (# 6-9) lộ ra ở một lượt thử thật khác, với một ý tưởng không khớp thẳng vào 4 hướng Arc và có dùng nhiều cơ chế khác nhau của Arc lẫn ngoài Arc – đúng kiểu tình huống bản đầu của Câu 0 và Câu 3 chưa xử lý được. Đã sửa hết vào khối prompt ở trên.

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| 1 | Câu hỏi feasibility viết bằng tiếng Việt → AI của docs trả lời sơ sài | Bắt viết **bằng tiếng Anh** |
| 2 | Hỏi chung chung "có hỗ trợ X không" → nhận về câu trả lời chung chung | Bắt hỏi thẳng tên SDK, tên kiến trúc, con số |
| 3 | Docs đưa 2 lựa chọn, suýt kết luận "cả hai đều được" | Bắt đối chiếu lại **yêu cầu quan trọng nhất** ở câu 1 để loại – và thêm hẳn câu hỏi "yêu cầu quan trọng nhất là gì" vào câu 1 để có cái mà đối chiếu |
| 4 | **Nặng nhất:** AI ngồi phản ứng theo người dùng thay vì dẫn | Thêm khối *"Cách làm việc"* lên đầu prompt: bạn DẪN, chủ động vặn, chưa hài lòng thì hỏi tiếp, đừng cho qua |
| 5 | Xong câu 3 rồi đứng im, phải nhắc hai lần mới tổng hợp | Bắt tự động làm 2 việc cuối: xuất case study + rút lỗi quy trình |
| 6 | Câu 0 đọc như danh sách đóng – ý tưởng không khớp hướng nào trong 4 gạch đầu dòng thì không rõ có bị loại hay không | Ghi rõ đây là gợi ý để có điểm bắt đầu, không phải rào chắn – không khớp cũng không sao miễn có dùng đặc thù kỹ thuật thật của Arc |
| 7 | Ý tưởng nhắc tới chi tiết cụ thể của Arc (tên token, cơ chế) không được kiểm tra ngay từ đầu – tiền đề sai chỉ lộ ra muộn ở câu 3, sau khi đã tưởng tượng cả ý tưởng trên nền đó | Thêm nhắc ngay ở câu 0: ý tưởng nhắc thứ cụ thể của Arc thì tra ngay, đừng để dồn |
| 8 | Câu 3 được thiết kế như một bước làm 1 lần duy nhất, nhưng feasibility thật ra cần tra liên tục xuyên suốt Bước 1-3 – ý tưởng càng đi sâu càng lộ thêm chi tiết kỹ thuật cụ thể cần verify, app có thể dùng nhiều cơ chế Arc khác nhau chứ không phải một | Ghi rõ câu 3 là cửa TỐI THIỂU trước khi qua Bước 2, không phải lần duy nhất – hễ chốt dùng cơ chế Arc cụ thể nào ở bước sau, quay lại tra ngay lúc đó |
| 9 | docs.arc.io bị hỏi cả câu hỏi không liên quan gì tới Arc (tokenomics/roadmap của token hay dự án khác) – AI của docs trả lời bừa vì ngoài phạm vi của nó | Tách rõ: câu hỏi thuộc cơ chế Arc thì hỏi docs.arc.io, câu hỏi ngoài Arc thì tự search web riêng |

Lỗi số 4 là lỗi làm hỏng nhiều nhất trong lượt đầu. Prompt bảo AI "hỏi bạn từng câu" nhưng không bảo nó *dẫn*, nên nó thành thư ký ghi chép: bạn nói gì nó gật nấy, chỉ góp ý khi bạn đã nói xong. Bạn tự dẫn được thì cần gì cố vấn.

Lỗi số 8 là lỗi nặng nhất trong lượt thứ hai, và dễ tái phát nhất nếu không ghi rõ: bất kỳ bước nào có chữ "kiểm tra khả thi" cũng dễ bị đọc thành một cửa làm-một-lần-rồi-quên, trong khi bản chất công việc đó là tra cứu liên tục mỗi khi có thêm một quyết định kỹ thuật mới.
