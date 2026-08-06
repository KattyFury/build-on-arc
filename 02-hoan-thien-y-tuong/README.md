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

## Ví dụ: 6 câu của EZwallet

Vẫn là ý tưởng đã qua Bước 1 ([ezwallet.cash](https://ezwallet.cash)), giờ viết ra thành 6 câu.

1. **App này là gì?** Ví stablecoin mobile-first, ẩn hết thuật ngữ kỹ thuật, dùng quen tay như app ngân hàng.
2. **Ai sẽ dùng nó?** Người chưa từng đụng crypto, không biết ví hay địa chỉ hay gas là gì — đặc biệt người lớn tuổi, mắt kém.
3. **Nó giải quyết vấn đề gì?** Seed phrase, địa chỉ `0x` dài ngoằng, phải mua token gas riêng mới chuyển được tiền. Mỗi thứ là một bức tường khiến người không rành tech không dùng được crypto dù muốn.
4. **Nó có những tính năng nào?** Đăng nhập email + PIN 6 số; gửi kèm lời nhắn nằm trên blockchain; nhận bằng QR, đặt sẵn số tiền và lưu vào kho QR; đổi tiền bằng cách kéo thanh trượt %; danh bạ có ảnh; lịch sử kèm biên lai lưu về máy; xem số dư theo đồng tiền quen thuộc.
5. **Người dùng sẽ sử dụng nó ra sao?** Mở app, nhập email nhận mã một lần rồi đặt PIN 6 số. Gửi thì chọn tên trong danh bạ hoặc quét QR, gõ số tiền, kèm lời nhắn. Nhận thì đưa QR của mình ra. Đổi tiền thì kéo thanh trượt.
6. **Nó không được làm những gì?** Không seed phrase. Không hiện địa chỉ `0x` làm mặc định. Không bắt gõ số thập phân khi đổi tiền. Không có dApp browser — cố ý, vì đó là chỗ người già bị lừa. Không giữ tiền hộ, không hứa lãi, không token, không airdrop.

> Câu 6 là câu hay bị bỏ nhất và cũng đáng giá nhất. "Không có dApp browser" nghe như thiếu tính năng, nhưng chính nó ngăn AI tự ý thêm vào một thứ phá hỏng sản phẩm ở tháng thứ ba. Viết ranh giới ra sớm rẻ hơn gỡ ra sau nhiều.

## Rút ra core value

Tới đây AI mới biết mình muốn build cái gì, chưa biết mình tin vào điều gì. Core value không phải feature, không phải slogan. Nó là niềm tin khiến mình quyết định build sản phẩm này.

Phép test: bỏ hết tên sản phẩm và chi tiết feature ra khỏi câu core value. Nếu câu đó vẫn đứng vững như một niềm tin độc lập, đúng rồi. Nếu phải nhắc tới sản phẩm mới hiểu được, đó vẫn là mô tả sản phẩm, chưa phải core value.

### Core value của EZwallet

> Con người không cần thích nghi với crypto. Crypto phải thích nghi với con người, đơn giản đến mức ai cũng dùng được mà vẫn giữ trọn quyền sở hữu tiền của mình.

Chạy qua phép test: trong câu đó không có chữ "EZwallet", không có chữ "PIN", không có chữ "thanh trượt". Bỏ hết sản phẩm đi câu vẫn đứng vững như một niềm tin. Đạt.

Đem so với mấy câu dễ nhầm là core value:

| Câu | Thực ra là gì |
|---|---|
| "Đăng nhập bằng email + PIN, không seed phrase" | Feature |
| "Ví crypto đơn giản đến mức mẹ mình cũng dùng được" | Slogan — hay, nhưng phải nhắc tới sản phẩm mới hiểu |
| "Crypto phải thích nghi với con người, không phải ngược lại" | Core value |

Có câu này rồi thì mỗi lần phân vân "thêm tính năng này không", hỏi lại nó là ra. Thêm dApp browser vào ví cho người già? Bắt người ta thích nghi với crypto. Không thêm.

Xong bước này mới qua Bước 3, mô tả chi tiết từng tính năng, luồng sử dụng và giao diện để AI biết phải build như thế nào.
