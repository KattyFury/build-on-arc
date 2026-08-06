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

## Ví dụ

> 🚧 **Đang build.** Ví dụ của bước này lấy từ dự án mẫu trong [`example/`](../example/) — dự án đang được build **song song** với series, đúng theo từng bước. Bước nào build xong thì ví dụ của bước đó được viết vào đây, kèm mục *Prompt này từng hụt chỗ nào*.
>
> Làm vậy để mọi câu trong ví dụ đều là thứ đã xảy ra thật, không phải tình huống nghĩ ra cho đẹp bài.

Xong bước này mới qua Bước 4, vẽ wireframe để chốt mỗi màn hình trông ra sao trước khi cho AI code.
