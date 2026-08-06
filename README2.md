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

## Ví dụ: QR Pay

- **App này là gì?** App giúp người dùng phổ thông chuyển và nhận tiền bằng QR, trải nghiệm đơn giản như quét QR ngân hàng.
- **Ai sẽ dùng nó?** Người dùng phổ thông.
- **Nó giải quyết vấn đề gì?** Nạp rút phải thân thiện với người dùng phổ thông.
- **Tính năng nào?** Đăng nhập bằng Gmail, bảo mật bằng passkey và PIN, gửi tiền bằng QR, nhận tiền bằng QR, có lịch sử giao dịch, có danh bạ khách quen, có kho QR thường dùng, hỗ trợ nhiều ngôn ngữ và tiền tệ.
- **Không được làm gì?** Không kết nối ví bên ngoài, không cụm từ khôi phục bí mật.

## Rút ra core value

Tới đây AI mới biết mình muốn build cái gì, chưa biết mình tin vào điều gì. Core value không phải feature, không phải slogan. Nó là niềm tin khiến mình quyết định build sản phẩm này.

Phép test: bỏ hết tên sản phẩm và chi tiết feature ra khỏi câu core value. Nếu câu đó vẫn đứng vững như một niềm tin độc lập, đúng rồi. Nếu phải nhắc tới sản phẩm mới hiểu được, đó vẫn là mô tả sản phẩm, chưa phải core value.

## Ví dụ minh họa: ví dành cho người không biết gì về tech

1. **App này là gì?** Ví crypto tối giản, ẩn hết thuật ngữ kỹ thuật, dùng như app ngân hàng quen thuộc.
2. **Ai sẽ dùng nó?** Người chưa từng đụng crypto, không biết ví, địa chỉ, hay gas là gì.
3. **Nó giải quyết vấn đề gì?** Rào cản kỹ thuật, seed phrase, địa chỉ dài, chọn nhầm mạng, token gas riêng, khiến người không rành tech không dùng được crypto dù muốn.
4. **Tính năng nào?** Đăng nhập email + PIN, gửi/nhận qua QR hoặc danh bạ, xem số dư theo tiền tệ quen thuộc, gas trả bằng chính token đang cầm.
5. **Người dùng sử dụng ra sao?** Mở app, đăng nhập email + PIN, quét QR hoặc chọn liên hệ để gửi, đưa QR cá nhân ra để nhận.
6. **Không được làm gì?** Không bắt nhớ seed phrase, không hiện địa chỉ ví làm mặc định, không bắt chọn mạng thủ công, không giữ tiền hộ người dùng.

Core value, chạy qua phép test bỏ tên sản phẩm: *Self-custody shouldn't be a privilege for the tech-savvy. It should be a right for everyone.*

Xong bước này mới qua Bước 3, mô tả chi tiết từng tính năng, luồng sử dụng và giao diện để AI biết phải build như thế nào.
