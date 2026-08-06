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

Đây là những gạch đầu dòng mô tả sơ về dự án của mình:
```

Dán 6 câu ở Bước 2 vào ngay sau dòng cuối, rồi gửi.

## Trả lời sao cho ăn tiền

- **Chốt hẳn, đừng để mở.** "Cái đó tính sau" nghĩa là tới lúc code AI vẫn phải đoán — đúng cái mình đang muốn tránh.
- **Chưa biết thì nói chưa biết**, bảo AI đưa 2-3 phương án kèm đánh đổi rồi tự chọn. Chọn là việc của mình, liệt kê là việc của nó.
- **Câu nào đụng tiền hoặc bảo mật thì đừng để AI chọn giúp.** Nó chọn phương án phổ biến nhất, không phải phương án đúng với sản phẩm của mình.
- **Ghi kết quả ra file.** Hỏi đáp nằm trong cửa sổ chat là thứ sẽ biến mất. Cuối buổi bảo AI tổng hợp toàn bộ quyết định thành một file, để đó cho các bước sau dùng lại.

## Ví dụ: EZwallet bị hỏi những gì

Vẫn là sản phẩm đã đi qua Bước 1 và Bước 2. Đây là những câu hỏi lòi ra lúc plan mà lúc viết 6 câu mô tả không hề nghĩ tới:

**Nhóm UX**

- *"Kéo thanh trượt 100% là đổi sạch số dư — vậy lấy gì trả phí giao dịch?"* → Chừa cứng 1 USDC. Số khả dụng hiện ra cho người dùng luôn là số dư trừ đi khoản chừa này, nên không bao giờ rơi vào cảnh có tiền mà không chuyển được.
- *"Cho xem số dư quy ra tiền quen thuộc thì người ta có tưởng mình đang giữ đồng tiền đó không?"* → Tên token thật (USDC / EURC / cirBTC) luôn hiện ở danh sách token, lịch sử và biên lai. Lớp quy đổi chỉ là cách hiển thị, không được phép làm người dùng hiểu sai mình đang cầm cái gì.

**Nhóm logic hệ thống**

- *"Danh bạ lưu ở máy, đổi máy là mất. Mà đồng bộ lên server thì hai máy sửa khác nhau, lấy bản nào?"* → Bản sửa mới nhất thắng, theo mốc thời gian. Không gộp kiểu union — union làm lệnh xoá không bao giờ ăn: xoá một liên hệ xong mở máy kia lên là nó sống lại.

**Nhóm xử lý lỗi**

- *"Bấm Gửi, mạng lag, người dùng sốt ruột bấm thêm lần nữa thì sao?"* → Mỗi lần gửi đi kèm một khoá chống trùng, trùng khoá thì chỉ vào một giao dịch duy nhất.
- *"Đọc số dư từ chain hỏng thì màn hình hiện gì?"* → Hiện `…`, tuyệt đối không vẽ số 0. Vẽ 0 là làm người dùng tưởng mất sạch tiền.
- *"Nhập sai PIN thì màn PIN đóng lại hay đứng nguyên?"* → Đứng nguyên cho nhập lại, chỉ đóng khi thành công hoặc gặp lỗi không cứu được. Quên hẳn PIN thì có luồng khôi phục bằng câu hỏi bảo mật đặt lúc tạo ví.

**Nhóm bảo mật**

- *"Sao lưu danh bạ lên server, thì server căn cứ vào đâu để tin đây đúng là ví của người này?"* → Server tự hỏi Circle bằng phiên đăng nhập để lấy địa chỉ ví, không tin địa chỉ do client khai. Ảnh đại diện trong danh bạ thì không bao giờ rời khỏi máy.

> Không phải câu nào cũng có câu trả lời đẹp. Chỗ sao lưu danh bạ vẫn còn một lỗ: phiên đăng nhập hiện chỉ cần biết email là cấp được, nên ai biết email là đọc được sổ danh bạ (tiền thì không đụng tới được, vì chuyển tiền bắt buộc qua PIN). Biết từ lúc plan nên nó được ghi thẳng vào danh sách nợ kỹ thuật, và không đem đi quảng cáo là "sao lưu đám mây an toàn". **Biết mà chấp nhận có chủ đích khác hẳn với không biết.**

Để ý là không câu nào ở trên là câu về tính năng. Tính năng thì đã liệt kê xong ở Bước 2 rồi. Toàn bộ giá trị của bước này nằm ở mấy chữ "thì sao", "lấy cái nào", "hiện gì" — và đó đúng là loại câu dễ bị bỏ qua nhất khi ngồi một mình.

Chi phí sửa cũng chênh nhau đúng ở chỗ đó. Chốt "chừa 1 USDC trả phí" lúc plan là một dòng quyết định. Phát hiện ra nó sau khi build xong màn đổi tiền là sửa lại thanh trượt, sửa số khả dụng, sửa cả phần kiểm tra trước khi gửi — và thường là phát hiện bằng cách có người dùng thật bị kẹt.

Xong bước này mới qua Bước 4, vẽ wireframe để chốt mỗi màn hình trông ra sao trước khi cho AI code.
