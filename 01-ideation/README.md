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

## Ví dụ: EZwallet đi qua 4 câu

Case study thật, sản phẩm đã chạy được: [ezwallet.cash](https://ezwallet.cash) — ví crypto đơn giản đến mức mẹ mình cũng dùng được.

**Câu 0 — Định hướng Arc.** Khớp usecase *Peer-to-peer payments*: gửi và nhận stablecoin giữa người với người. Chạm thêm *Stablecoin FX* ở phần đổi USDC ↔ EURC. Quan trọng hơn là nó ăn đúng thứ chỉ Arc mới có: **USDC chính là token trả phí** của chain, nên có thể bỏ luôn bước "mua token gas trước khi chuyển tiền" — chain khác không bỏ được bước này.

**Câu 1 — Vấn đề thật, đúng đối tượng.** Vấn đề tự trải qua, không đoán: mọi ví từng đưa cho người không chơi crypto đều chết ở đúng một chỗ — màn hình seed phrase. 12 từ tiếng Anh ngẫu nhiên, "ghi ra giấy, mất là mất tiền". Đối tượng là người chưa từng đụng crypto, đặc biệt người lớn tuổi mắt kém. Thước đo cụ thể tới mức một câu: *mẹ mình có dùng được không?*

**Câu 2 — Dẫn đầu hay cạnh tranh.** Ví thì đầy rồi: MetaMask, Coinbase Wallet, Trust Wallet. Không giả vờ là chưa ai làm. Điểm hơn hẳn nằm ở chỗ chọn khác: mấy ví kia làm cho người **đã** hiểu crypto và cố làm mọi thứ; EZwallet cố tình chỉ làm 4 việc (gửi / nhận / đổi / danh bạ), cho người **chưa** hiểu gì. Cụ thể là bỏ hẳn seed phrase (email + PIN 6 số), bỏ luôn dApp browser — vì đó chính là chỗ người già bị lừa. Cạnh tranh ở "ai dùng được", không cạnh tranh ở "có bao nhiêu tính năng".

**Câu 3 — Khả thi.** Trước khi code, xác nhận từng mảnh đều đã có sẵn, không phải tự phát minh:

| Cần gì | Dùng cái có sẵn |
|---|---|
| Đăng nhập không seed phrase | Circle User-Controlled Wallets (MPC giữ khoá, PIN ký từng giao dịch) |
| Không phải mua token gas | Arc dùng USDC làm native gas |
| Lời nhắn đi kèm tiền | Memo precompile của Arc |
| Đổi tiền | Circle Stablecoin Kit, route qua LiFi |

Kết quả sau khi làm thật: phí đo được dưới $0.01/giao dịch, chạy trên Arc Testnet, và người làm không có nền lập trình.

> Chú ý cách trả lời câu 2 và câu 3: không câu nào là "sẽ", "dự kiến", "chắc là được". Câu 2 chỉ ra điểm hơn **cụ thể** thay vì nói "UX tốt hơn". Câu 3 chỉ đúng tên thứ có sẵn để dùng thay vì nói "về mặt kỹ thuật thì khả thi". Trả lời được ở mức này mới nên qua Bước 2.
