# Bước 3: Plan chi tiết trước khi code

Có 6 câu mô tả sản phẩm từ Bước 2 rồi. Bước này đưa chúng cho AI bóc tách từng gạch đầu dòng, tìm ra những chỗ còn thiếu — trước khi viết dòng code đầu tiên.

## Vì sao cần bước này

Đừng quăng một cái idea sơ sài rồi bảo AI tự chạy. Token hết nhanh khủng khiếp, mà thứ ra đời là dự án của AI chứ chẳng phải của mình. Ngồi plan kỹ trước được 4 cái:

1. **Làm chủ dự án mình build**, thay vì để AI tự biên tự diễn.
2. **Tiết kiệm token**, vì AI biết chính xác phải làm gì, không làm dư mấy tính năng vớ vẩn.
3. **Bịt trước những chỗ AI phải đoán.** AI có xu hướng tự điền vào chỗ còn thiếu. Mình không nói rõ thì nó đoán, đoán sai thì lại tốn token bảo nó sửa đi sửa lại.
4. **Chính lúc ngồi plan mới thấy được chỗ cần làm rõ trong logic.** Build sản phẩm không phải nghề của tụi mình nên nhiều khía cạnh chưa nghĩ tới. Đừng lo, AI sẽ gánh chỗ này.

## Plan chi tiết là như thế nào

Không phải viết một bài văn dài dòng. Là ngồi **trả lời phỏng vấn**: đưa AI mấy gạch đầu dòng mô tả sản phẩm ở Bước 2, bắt nó đóng vai người tư vấn và hỏi ngược lại mình.

Mấu chốt nằm ở câu cuối của prompt: **hỏi một nhóm mỗi lần, chờ trả lời xong mới sang nhóm tiếp**. Bỏ câu đó ra thì AI xổ 30 câu hỏi một lượt, đọc xong không trả lời tử tế được câu nào.

## Prompt

Copy đoạn dưới, paste vào AI bạn đang dùng:

```
Đóng vai một Senior Product Consultant. Đừng giải pháp ngay. Hãy review ý tưởng của tôi như một buổi Product Discovery, chia thành các nhóm logic và hỏi 3–5 câu hỏi thực tế cho từng nhóm về UX, logic hệ thống, xử lý lỗi, edge cases và bảo mật. Chỉ hỏi một nhóm mỗi lần và đợi tôi trả lời trước khi sang nhóm tiếp theo.

Sau mỗi nhóm tôi trả lời xong, trước khi sang nhóm tiếp: liệt kê lại đúng những câu trong nhóm tôi CHƯA trả lời (im lặng không có nghĩa là pass hay không cần quan tâm), hỏi lại riêng mấy câu đó.

Khi câu trả lời của tôi là "để bên thứ ba lo" (vd nhà cung cấp ví, nhà cung cấp hạ tầng): chỉ chấp nhận nếu câu hỏi gốc là về ĐỘ AN TOÀN của bên thứ ba đó. Nếu câu hỏi gốc là app xử lý tình huống X ra sao, không được để tôi đẩy hết trách nhiệm qua bên thứ ba — hỏi lại.

Khi tôi trả lời "chấp nhận rủi ro, không cần xử lý" cho một câu về bảo mật/rủi ro: đây là câu trả lời hợp lệ và đủ, đừng cố thuyết phục tôi đổi ý — chỉ cần đảm bảo tôi đã THẤY rõ rủi ro trước khi chấp nhận.

Cuối mỗi nhóm, nếu phát hiện 2 quyết định riêng lẻ tôi vừa chấp nhận (mỗi cái nghe hợp lý một mình) khi cộng lại tạo ra rủi ro lớn hơn tổng từng phần, phải chỉ rõ ra sự kết hợp đó ngay, đừng chỉ đánh giá từng quyết định độc lập.

Đây là những gạch đầu dòng mô tả sơ về dự án của mình:
```

Dán 6 câu ở Bước 2 vào ngay sau dòng cuối, rồi gửi.

Sau khi xong hết các nhóm, chủ động hỏi Chat: "Tổng hợp toàn bộ quyết định ở đây thành 1 file duy nhất giúp mình" — bước này hay bị quên vì Chat không tự nhắc, mà không có file thì hỏi đáp biến mất khi đóng tab.

> Dán kèm nếu bạn đang mở cửa sổ chat mới. Nếu dùng chung 1 cửa sổ chat xuyên suốt từ đầu thì bỏ qua — Chat đã có sẵn context, dán lại là thừa.

## Trả lời sao cho ăn tiền

- **Chốt hẳn, đừng để mở.** "Cái đó tính sau" nghĩa là tới lúc code AI vẫn phải đoán — đúng cái mình đang muốn tránh.
- **Chưa biết thì nói chưa biết**, bảo AI đưa 2-3 phương án kèm đánh đổi rồi tự chọn. Chọn là việc của mình, liệt kê là việc của nó.
- **Câu nào đụng tiền hoặc bảo mật thì đừng để AI chọn giúp.** Nó chọn phương án phổ biến nhất, không phải phương án đúng với sản phẩm của mình.
- **Ghi kết quả ra file.** Hỏi đáp nằm trong cửa sổ chat là thứ sẽ biến mất. Cuối buổi bảo AI tổng hợp toàn bộ quyết định thành một file, để đó cho các bước sau dùng lại.

## Ví dụ: Product Discovery của TapTip

Đây là kết quả chạy thật prompt trên. Bản đầy đủ: [`example/docs/03-planning.md`](../example/docs/03-planning.md).

Chia làm 5 nhóm, mỗi nhóm 3-4 quyết định:

| Nhóm | Quyết định đáng chú ý |
|---|---|
| Login & Onboarding | Khôi phục qua email OTP, không phải cơ chế passkey theo thiết bị — chấp nhận rủi ro vì tiền tip nhỏ |
| Ví & Nạp/Rút | Testnet: nạp/rút = faucet only, rút bị disable |
| Luồng gửi/quét QR | QR người nhận là QR tĩnh, không đổi, không hết hạn — giống số tài khoản |
| Xử lý lỗi & Edge case | Balance không đủ: nút vượt quá balance bị disable từ đầu, không để quét xong mới báo lỗi |
| Bảo mật | Bảo mật lưu key của Circle Wallets là trách nhiệm của Circle, không phải app tự thêm lớp bảo vệ |

> Chỗ đáng học nhất là ở nhóm Bảo mật: hai quyết định riêng lẻ đều nghe hợp lý — "không cần xác thực thêm khi gửi" (để giữ tốc độ) và "không giới hạn số tiền mỗi lần gửi" — nhưng cộng lại nghĩa là ai cầm được điện thoại đã mở khoá thì rút sạch ví không cần thêm bước nào. Đây là trade-off được **nhìn thấy và chấp nhận có chủ đích**, không phải bị bỏ sót.

## Prompt này từng hụt chỗ nào

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| 1 | Trả lời "để bên thứ ba lo" được chấp nhận cả khi câu hỏi là "app xử lý lỗi ra sao" — né tránh trách nhiệm thay vì trả lời đúng phạm vi | Chỉ chấp nhận đẩy qua bên thứ ba nếu câu hỏi gốc là về độ an toàn của bên đó |
| 2 | Trả lời đúng 1 câu trong nhóm 4-5 câu rồi dừng, coi cả nhóm đã xong | Bắt liệt kê lại câu chưa trả lời trước khi qua nhóm tiếp — im lặng không phải là pass |
| 3 | Hai quyết định riêng lẻ hợp lý cộng lại thành rủi ro lớn hơn, không ai chỉ ra | Bắt chỉ rõ tổ hợp rủi ro cuối mỗi nhóm, không chỉ đánh giá từng quyết định độc lập |
| 4 | AI có xu hướng thuyết phục đổi ý khi user nói "chấp nhận rủi ro, không care" | Ghi rõ đây là câu trả lời hợp lệ và đủ — việc của AI là đảm bảo user *thấy* rủi ro, không phải ép tránh rủi ro |
| 5 | Xong nhiều nhóm rồi không ai chủ động tổng hợp thành file, hỏi đáp nằm rải trong chat | Thêm bước cuối: chủ động hỏi Chat tổng hợp thành 1 file duy nhất |

Xong bước này mới qua Bước 4, vẽ wireframe để chốt mỗi màn hình trông ra sao trước khi cho AI code.
