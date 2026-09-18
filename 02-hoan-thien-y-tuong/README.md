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

> Dán kèm nếu bạn đang mở cửa sổ chat mới. Nếu dùng chung 1 cửa sổ chat xuyên suốt từ đầu thì bỏ qua – Chat đã có sẵn context, dán lại là thừa.

```
Bạn là Product Manager giúp mình viết PRD cho app đang định build trên Arc network.

CÁCH LÀM VIỆC – quan trọng nhất, đọc kỹ:
Bạn DẪN, mình theo. Hỏi từng câu một, xong câu này mới sang câu sau. Ở mỗi câu, bạn chủ động vặn lại câu trả lời của mình: chỗ nào mơ hồ thì bắt nói rõ, chỗ nào ôm đồm thì bắt cắt bớt, chỗ nào mâu thuẫn với câu trước thì chỉ ra ngay. ĐỪNG gật đầu cho qua rồi sang câu kế – mình đến để được vặn, không phải để được khen.

Câu trả lời của mình mà chung chung kiểu "ai dùng cũng được", "làm cho tiện lợi" thì HỎI LẠI, đừng ghi vào PRD.

6 CÂU CẦN TRẢ LỜI:
1. App này là gì? (một câu, người không biết crypto đọc phải hiểu – MÔ TẢ SẢN PHẨM, không liệt kê thông số kỹ thuật như tốc độ hay con số. Thấy mình lẫn thông số vào thì tách riêng, không cho vào câu 1.)
2. Ai sẽ dùng nó? (cụ thể tới mức hình dung được một người thật, không phải "người dùng phổ thông". NẾU app có từ 2 vai trò trở lên – vd người gửi và người nhận – hỏi riêng từng vai, đừng mặc định vai còn lại giống vai đầu.)
3. Nó giải quyết vấn đề gì – hoặc mang lại điều gì? (không bắt buộc phải giải quyết vấn đề; vui, tiện, đáng nhớ cũng là câu trả lời hợp lệ)
4. Nó có những tính năng nào? (liệt kê hết, rồi hỏi bằng tình huống cụ thể: "giả sử phải cắt bớt 1 tính năng để kịp deadline, cắt cái nào?" – đừng hỏi trừu tượng kiểu "cái nào core", câu đó luôn nhận về "cái nào cũng core".)
5. Người dùng sẽ sử dụng nó ra sao? (kể lại thành một luồng từ lúc mở app tới lúc xong việc)
6. Nó KHÔNG được làm những gì? (câu này quan trọng nhất và hay bị trả lời qua loa nhất – ép mình kể ít nhất 4 ranh giới. Câu trả lời lạc sang chi tiết thiết kế khác thì KÉO LẠI đúng câu hỏi gốc, không tính câu lạc đề vào ranh giới.)

Ở câu 4 và 6, đối chiếu lại YÊU CẦU QUAN TRỌNG NHẤT mà mình đã chốt ở Bước 1. Tính năng nào phá mất yêu cầu đó thì phải chỉ ra và bắt mình cân nhắc bỏ.

SAU 6 CÂU – RÚT CORE VALUE:
Core value không phải feature, không phải slogan. Nó là niềm tin khiến mình quyết định build sản phẩm này.
Bắt mình viết ra, rồi CHẠY PHÉP TEST: bỏ hết tên sản phẩm và chi tiết tính năng ra khỏi câu đó. Còn đứng vững như một niềm tin độc lập thì đạt. Phải nhắc tên sản phẩm mới hiểu được thì chưa đạt – nói thẳng là chưa đạt và bắt viết lại, đừng cho qua. Thấy câu trả lời nhét thông số kỹ thuật hiện tại vào (vd "1 giây", "tức thì") thì hỏi thêm: "nếu con số này đổi, niềm tin có đổi theo không?" – đổi theo thì đó là chi tiết implementation tạm thời, không phải core value.

XONG THÌ TỰ ĐỘNG LÀM 2 VIỆC NÀY, ĐỪNG ĐỢI MÌNH NHẮC:
1. Tổng hợp thành một PRD gọn (6 câu + core value), định dạng markdown để mình copy đi lưu.
2. Rút ra những lỗi quy trình vừa gặp trong lúc chạy – chỗ nào mình bị hỏi hụt, chỗ nào suýt ghi vào PRD một câu chung chung – viết thành một khối riêng.

Đây là kết quả Bước 1 của mình:
[DÁN KẾT QUẢ BƯỚC 1 VÀO ĐÂY]
```

## Ví dụ: PRD của TapTip và EZwallet

### TapTip – chạy thật 2 lần, v1 và v2

[`KattyFury/taptip`](https://github.com/KattyFury/taptip) chạy prompt này thật **hai lần**: bản v1 lúc mới lên ý tưởng, bản v2 sau 3 tuần có app thật trong tay. Bản đầy đủ: [`docs/02-hoan-thien-y-tuong.md`](https://github.com/KattyFury/taptip/blob/main/docs/02-hoan-thien-y-tuong.md) (v1) và [`docs/02-v2-hoan-thien-y-tuong.md`](https://github.com/KattyFury/taptip/blob/main/docs/02-v2-hoan-thien-y-tuong.md) (v2).

**PRD v1:**

**App:** Lì xì và tip nhanh chóng cho bất kỳ ai, chỉ bằng cách log in bằng email.

**Ai dùng:** Cả người gửi lẫn người nhận có thể là người lớn tuổi, ít rành công nghệ (mẹ/bà, khoảng 60 tuổi) – phải tự thao tác được ngay từ lần đầu, không cần ai chỉ.

**Mang lại điều gì:** So với chuyển khoản ngân hàng (xác thực mỗi giao dịch), app chỉ xác thực một lần lúc mở app (passkey), sau đó gửi không cần duyệt lại – vì số tiền nhỏ.

**Tính năng core (thiếu thì app vô nghĩa):** đăng nhập email + passkey, nạp/rút, màn hình chính (Balance + QR code của mình + Nạp/Rút/Lịch sử), chọn số tiền có sẵn hoặc nhập số khác, quét QR người nhận gửi ngay không cần xác nhận thêm, chỉ hỗ trợ USDC quy đổi VNĐ. Nice-to-have: nút Random rút túi mù.

**Ranh giới:** không hoàn tiền sau khi gửi, không token khác ngoài USDC, không chat kèm tin nhắn, không giới hạn số tiền mỗi lần gửi.

**Core value:** Tip tiền và lì xì nhanh như trao tay.

**v2 đổi gì, vì sao.** Lý do viết lại không nằm ở sản phẩm: tài khoản Circle cũ mất khoá (xem Bước 5), database cũ tự ngủ sau mấy ngày không dùng (xem Bước 3) – đằng nào cũng phải viết lại code, nên tận dụng chạy lại luôn Bước 2 bằng những gì đã học từ app thật:

| Chỗ | v1 | v2 |
|---|---|---|
| Chọn số tiền | Chọn số có sẵn hoặc gõ số khác, mỗi lần gửi | **Tip Setting**: 4 mức cài sẵn ($1 / $3 / $10 / tự nhập), chọn 1 mức làm mặc định. Bấm Tip là vào thẳng màn quét, mức vừa gửi giữ nguyên cho lần sau |
| Quy đổi VNĐ | Nằm trong core | Đẩy sang roadmap – cần nguồn tỷ giá thật, chưa chọn được thì không làm |
| Hiển thị ví | Không nhắc | Rút gọn `0x_NNNNN` (5 số cuối) – chỉ để đọc cho dễ, không dùng làm dữ liệu gửi/nhận |
| Ranh giới "không giới hạn số tiền" | Một dòng | Viết thẳng cái giá phải trả: điện thoại đã mở khoá rơi vào tay người khác + không giới hạn + không xác nhận = mất ví trong một lần chạm. Chấp nhận, vì là app tip số nhỏ |
| Core value | Tip tiền và lì xì nhanh như trao tay | **Gửi tiền nên nhanh và đơn giản như trao tận tay – không phải như làm thủ tục ngân hàng** |

> Chỗ đáng học là dòng core value. Bản v1 vẫn còn nhắc "tip", "lì xì" – bỏ tên tính năng ra thì câu đó gãy, tức là nó vẫn đang mô tả sản phẩm. Bản v2 bỏ hết chi tiết đi mà vẫn đứng vững như một niềm tin: gửi tiền cho người khác không nên giống làm thủ tục. Chạy phép test của bước này lần hai, trên chính câu mình từng cho qua, mới thấy lần đầu mình cho qua hơi dễ.

### EZwallet – dựng ngược từ README thật

Dự án thật của tác giả – [`KattyFury/ezwallet`](https://github.com/KattyFury/ezwallet). Cũng như Bước 1, dự án này ra đời trước series nên phần dưới dựng ngược từ [`README.md`](https://github.com/KattyFury/ezwallet/blob/main/README.md) thật của repo – tình cờ README đó đã viết gần đúng khuôn 6 câu, vì cùng một cách nghĩ.

**App:** A crypto wallet simple enough for my mom to use.

**Ai dùng:** Người dùng phổ thông, không rành crypto – ví dụ cụ thể xuyên suốt là "mẹ mình", một người thật chứ không phải "target audience" chung chung.

**Giải quyết vấn đề gì:** Hầu hết ví crypto dựng cho người đã hiểu crypto. Seed phrase, token gas riêng, địa chỉ hex, chọn mạng – mỗi thứ là một bức tường với người mới, và là lý do chặn hẳn với người lớn tuổi.

**Tính năng core:** đăng nhập email + PIN (không seed phrase), gửi kèm lời nhắn, nhận bằng QR, lịch sử + biên lai. **Nice-to-have thêm dần sau:** swap bằng thanh trượt %, danh bạ (đặt tên cho địa chỉ), kho QR lưu sẵn, hiển thị đa tiền tệ (USDC/EURC/VNĐ).

**Người dùng sẽ sử dụng ra sao:** Mở app → tạo ví bằng email (nhận mã, đặt PIN 6 số) → Nạp tiền test qua Circle faucet (Menu → Deposit tự copy địa chỉ + mở link faucet) → gửi cho người khác hoặc quét QR của họ.

**Ranh giới:** chỉ chạy Testnet, chưa lên mainnet, mặc định tiếng Anh (tiếng Việt dịch xong hoàn chỉnh nhưng không tự bật theo máy), không hỗ trợ đăng nhập Google, QR chỉ đọc được QR ví crypto chứ không phải QR đời thường (mã vạch sản phẩm, QR ngân hàng...), chưa qua audit bảo mật.

**Core value:** *"EZwallet was built on a simple belief: everyone should be able to own their own money, without needing to become a crypto expert."* Bỏ hết tên sản phẩm, câu này vẫn đứng vững như một niềm tin độc lập – đúng bài kiểm tra core value của bước này, dù câu này được viết ra trước khi series có bài kiểm tra đó.

## Prompt này từng hụt chỗ nào

Prompt đã có sẵn khối *"Cách làm việc"* từ bài học Bước 1, nhưng chạy thật lộ thêm 5 chỗ hụt riêng của bước này:

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| 1 | Câu 1 (mô tả app) lẫn thông số kỹ thuật (vd "dưới 1s") vào câu mô tả sản phẩm | Ghi rõ câu 1 là mô tả sản phẩm, tách riêng thông số kỹ thuật ra khỏi câu này |
| 2 | Câu 2 (đối tượng dùng) trả lời một chiều – chỉ tả người NHẬN, quên người GỬI dù cả hai đều là user thật | Với app có ≥2 vai trò, bắt hỏi riêng từng vai, không mặc định vai còn lại giống vai đầu |
| 3 | Câu 4 hỏi "cái nào core" → nhận về "cái nào cũng core" | Đổi thành tình huống cụ thể: "giả sử phải cắt 1 cái để kịp deadline, cắt cái nào?" |
| 4 | Câu 6 (ranh giới) bị né bằng cách trả lời sang chi tiết thiết kế khác | Bắt kéo lại đúng câu hỏi gốc, không tính câu lạc đề vào ranh giới |
| 5 | Core value nhét thông số kỹ thuật hiện tại (vd "1s", "instant") vào làm niềm tin | Test bằng câu "nếu con số này đổi, niềm tin có đổi theo không" – đổi theo thì chưa phải core value |

Xong bước này mới qua Bước 3, mô tả chi tiết từng tính năng, luồng sử dụng và giao diện để AI biết phải build như thế nào.
