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

### Câu 1: Vấn đề thật, đúng đối tượng

Xác định vấn đề thực tế cần giải và đối tượng khách hàng, trong chính xã hội Việt Nam. Arc định hướng builder địa phương giải vấn đề địa phương, những thứ gần gũi như bỏ heo, chơi hụi, từ thiện, lì xì... đều có thể biến thành app.

Vấn đề đưa ra phải là thứ chính mình hoặc người mình biết đã tự trải qua, không đoán hoặc tưởng tượng ra.

### Câu 2: Dẫn đầu hay cạnh tranh

Ý tưởng có lead mảng này không, tức chưa ai làm? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh của mình là gì. Build một DEX trong 3 tháng, sao không fork Uniswap? Thứ người khác đã làm rất tốt thì tay ngang rất khó cạnh tranh, phải chỉ ra được điểm hơn hẳn.

### Câu 3: Khả thi

Nhiều ý tưởng AI đưa ra nghe hay nhưng không làm được, hoặc quá khó với team nhỏ. Cho AI đọc docs.arc.io trước, bàn sơ tính khả thi kỹ thuật, thậm chí vào Docs chat với AI trong đó để xác nhận trước khi qua Bước 2.

## Prompt để AI guide bạn từ đầu

Copy đoạn dưới, paste vào AI bạn đang dùng:

```
Bạn là cố vấn giúp mình lên ý tưởng build app trên Arc network (docs.arc.io).

Hỏi trước: Bạn có ý tưởng chưa, hay còn chưa biết build gì? Có rồi thì hỏi vài câu thử thách ý tưởng đó. Chưa có thì gợi ý theo câu 0.

CÂU 0: Định hướng Arc
Gợi ý 4 định hướng Arc: Peer-to-peer payments, eCommerce checkout, Stablecoin FX, Agentic economy. Có ý tưởng rồi thì check ý tưởng có khớp 1 trong 4 hướng này không.

CÂU 1: Vấn đề thật, đúng đối tượng
Xác định vấn đề thực tế cần giải và đối tượng khách hàng, trong chính xã hội Việt Nam. Arc định hướng builder địa phương giải vấn đề địa phương.

CÂU 2: Dẫn đầu hay cạnh tranh
Ý tưởng có lead mảng này không? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh là gì?

CÂU 3: Khả thi
Chốt được ý tưởng rồi, tổng hợp thành 1 câu hỏi feasibility, đưa ra thành khối riêng để dễ copy, kèm hướng dẫn: "Copy đoạn trên, vào docs.arc.io, mở khung chat AI của Docs, paste vào rồi gửi. Xong đem câu trả lời quay lại đây." Đọc câu trả lời để đánh giá khả thi kỹ thuật.

Chỗ nào chưa hợp lý thì rèn lại cho hợp lý, xong xuôi hết mới qua Bước 2.
```

## Ví dụ minh họa

Case study thật, đi hết 4 câu.

**Ý tưởng:** platform cho web2 seller tự tạo shop bán digital item (ebook, course, preset...), eCommerce checkout trên Arc.

0. **Định hướng Arc:** đúng usecase eCommerce checkout của Arc.
1. **Vấn đề thật, đúng đối tượng:** web2 seller bán hàng số ở Việt Nam, không cần biết crypto, chỉ cần trải nghiệm dễ như Gumroad.
2. **Dẫn đầu hay cạnh tranh:** Gumroad, Payhip, Stan Store đã làm tốt cho web2 seller rồi, nhưng đều qua Stripe/PayPal, giữ tiền vài ngày, ăn forex, dễ bị chargeback. Điểm hơn hẳn là settlement USDC xuyên biên giới dưới 1 giây.
3. **Khả thi:** check với Docs AI xác nhận cả 3 phần đều có sẵn. Ví riêng từng seller qua Developer-Controlled Wallets, tiền về thẳng ví seller (primarySaleRecipient) không qua nền tảng, tự động trích phí platform (platformFeeRecipient). Checkout/escrow purpose-built, có sẵn arc-escrow để fork. Onboarding không cần seed phrase qua Privy, Crossmint, hoặc Dynamic.
