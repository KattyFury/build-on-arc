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

### Câu 3: Khả thi

Nhiều ý tưởng AI đưa ra nghe hay nhưng không làm được, hoặc quá khó với team nhỏ. Cho AI đọc docs.arc.io trước, bàn sơ tính khả thi kỹ thuật, thậm chí vào Docs chat với AI trong đó để xác nhận trước khi qua Bước 2.

## Prompt để AI guide bạn từ đầu

Copy đoạn dưới, paste vào AI bạn đang dùng:

```
Bạn là cố vấn giúp mình lên ý tưởng build app trên Arc network (docs.arc.io).

Hỏi trước: Bạn có ý tưởng chưa, hay còn chưa biết build gì? Có rồi thì hỏi vài câu thử thách ý tưởng đó. Chưa có thì gợi ý theo câu 0.

CÂU 0: Định hướng Arc
Gợi ý 4 định hướng Arc: Peer-to-peer payments, eCommerce checkout, Stablecoin FX, Agentic economy. Có ý tưởng rồi thì check ý tưởng có khớp 1 trong 4 hướng này không.

CÂU 1: Thật, và đúng đối tượng
Xác định mình làm cho ai, trong chính xã hội Việt Nam. Arc định hướng builder địa phương làm cho người địa phương. KHÔNG bắt buộc phải giải quyết một vấn đề — thứ vui, thứ người ta thật sự muốn dùng cũng tính. Nhưng nó phải là thứ mình hoặc người mình biết THẬT SỰ làm ngoài đời, không tưởng tượng ra.

CÂU 2: Dẫn đầu hay cạnh tranh
Ý tưởng có lead mảng này không? Nếu đã có dự án làm rồi, ưu điểm cạnh tranh là gì?

CÂU 3: Khả thi
Chốt được ý tưởng rồi, tổng hợp thành 1 câu hỏi feasibility, đưa ra thành khối riêng để dễ copy, kèm hướng dẫn: "Copy đoạn trên, vào docs.arc.io, mở khung chat AI của Docs, paste vào rồi gửi. Xong đem câu trả lời quay lại đây." Đọc câu trả lời để đánh giá khả thi kỹ thuật.

Chỗ nào chưa hợp lý thì rèn lại cho hợp lý, xong xuôi hết mới qua Bước 2.
```

## Ví dụ

> 🚧 **Đang build.** Ví dụ của bước này lấy từ dự án mẫu trong [`example/`](../example/) — dự án đang được build **song song** với series, đúng theo từng bước. Bước nào build xong thì ví dụ của bước đó được viết vào đây, kèm mục *Prompt này từng hụt chỗ nào*.
>
> Làm vậy để mọi câu trong ví dụ đều là thứ đã xảy ra thật, không phải tình huống nghĩ ra cho đẹp bài.
