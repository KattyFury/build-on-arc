# Bước 2: Hoàn thiện ý tưởng

Có ý tưởng từ Bước 1 rồi, đến lúc viết ra rõ ràng để cả bạn và AI đều hiểu đang build cái gì.

## Vì sao cần bước này

Nhiều người có idea xong là nhảy vào code luôn. Kết quả là sản phẩm nay thiếu sót chỗ này, mai dư thừa chỗ kia. AI là trợ lý giúp build sản phẩm, nếu chính mình còn chưa hiểu sản phẩm của mình là gì, làm được gì và không nên làm gì, thì AI cũng không hiểu được.

## 6 câu cần trả lời

1. App này là gì?
2. Ai sẽ dùng nó?
3. Nó giải quyết vấn đề gì?
4. Nó có những tính năng nào?
5. Người dùng sẽ sử dụng nó ra sao?
6. Nó không được làm những gì?

Không cần viết dài, chỉ cần đủ rõ để cả bạn và AI đều hiểu đang build cái gì.

## Rút ra core value

Tới đây AI mới biết mình muốn build cái gì, chưa biết mình tin vào điều gì. Core value không phải feature, không phải slogan. Nó là niềm tin khiến mình quyết định build sản phẩm này.

Phép test: bỏ hết tên sản phẩm và chi tiết feature ra khỏi câu core value. Nếu câu đó vẫn đứng vững như một niềm tin độc lập, đúng rồi. Nếu phải nhắc tới sản phẩm mới hiểu được, đó vẫn là mô tả sản phẩm, chưa phải core value.

## Prompt để AI làm PRD với bạn

Copy đoạn dưới, paste vào Claude Chat. Nhớ dán kèm kết quả Bước 1 vào chỗ đánh dấu ở cuối.

```
Bạn là Product Manager giúp mình viết PRD cho app đang định build trên Arc network.

CÁCH LÀM VIỆC — quan trọng nhất, đọc kỹ:
Bạn DẪN, mình theo. Hỏi từng câu một, xong câu này mới sang câu sau. Ở mỗi câu, bạn chủ động vặn lại câu trả lời của mình: chỗ nào mơ hồ thì bắt nói rõ, chỗ nào ôm đồm thì bắt cắt bớt, chỗ nào mâu thuẫn với câu trước thì chỉ ra ngay. ĐỪNG gật đầu cho qua rồi sang câu kế — mình đến để được vặn, không phải để được khen.

Câu trả lời của mình mà chung chung kiểu "ai dùng cũng được", "làm cho tiện lợi" thì HỎI LẠI, đừng ghi vào PRD.

6 CÂU CẦN TRẢ LỜI:
1. App này là gì? (một câu, người không biết crypto đọc phải hiểu)
2. Ai sẽ dùng nó? (cụ thể tới mức hình dung được một người thật, không phải "người dùng phổ thông")
3. Nó giải quyết vấn đề gì — hoặc mang lại điều gì? (không bắt buộc phải giải quyết vấn đề; vui, tiện, đáng nhớ cũng là câu trả lời hợp lệ)
4. Nó có những tính năng nào? (liệt kê hết, rồi bắt mình chọn ra tính năng NÀO KHÔNG CÓ THÌ APP VÔ NGHĨA)
5. Người dùng sẽ sử dụng nó ra sao? (kể lại thành một luồng từ lúc mở app tới lúc xong việc)
6. Nó KHÔNG được làm những gì? (câu này quan trọng nhất và hay bị trả lời qua loa nhất — ép mình kể ít nhất 4 ranh giới, gồm cả mấy thứ nghe có vẻ hay ho mà mình cố tình không làm)

Ở câu 4 và 6, đối chiếu lại YÊU CẦU QUAN TRỌNG NHẤT mà mình đã chốt ở Bước 1. Tính năng nào phá mất yêu cầu đó thì phải chỉ ra và bắt mình cân nhắc bỏ.

SAU 6 CÂU — RÚT CORE VALUE:
Core value không phải feature, không phải slogan. Nó là niềm tin khiến mình quyết định build sản phẩm này.
Bắt mình viết ra, rồi CHẠY PHÉP TEST: bỏ hết tên sản phẩm và chi tiết tính năng ra khỏi câu đó. Còn đứng vững như một niềm tin độc lập thì đạt. Phải nhắc tên sản phẩm mới hiểu được thì chưa đạt — nói thẳng là chưa đạt và bắt viết lại, đừng cho qua.

XONG THÌ TỰ ĐỘNG LÀM 2 VIỆC NÀY, ĐỪNG ĐỢI MÌNH NHẮC:
1. Tổng hợp thành một PRD gọn (6 câu + core value), định dạng markdown để mình copy đi lưu.
2. Rút ra những lỗi quy trình vừa gặp trong lúc chạy — chỗ nào mình bị hỏi hụt, chỗ nào suýt ghi vào PRD một câu chung chung — viết thành một khối riêng.

Đây là kết quả Bước 1 của mình:
[DÁN KẾT QUẢ BƯỚC 1 VÀO ĐÂY]
```

## Ví dụ

> 🚧 **Đang build.** Ví dụ của bước này lấy từ dự án mẫu trong [`example/`](../example/) — dự án đang được build **song song** với series, đúng theo từng bước. Bước nào build xong thì ví dụ của bước đó được viết vào đây, kèm mục *Prompt này từng hụt chỗ nào*.
>
> Làm vậy để mọi câu trong ví dụ đều là thứ đã xảy ra thật, không phải tình huống nghĩ ra cho đẹp bài.

Xong bước này mới qua Bước 3, mô tả chi tiết từng tính năng, luồng sử dụng và giao diện để AI biết phải build như thế nào.
