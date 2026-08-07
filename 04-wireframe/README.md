# Bước 4: Vẽ wireframe

Có bản plan chi tiết từ Bước 3 rồi – tới lúc vẽ khung sườn từng màn hình, trước khi code UI thật.

## Vì sao cần bước này

Nhảy vào code luôn thì AI tự bịa layout theo cảm tính của nó. Code xong nhìn không đúng ý lại phải sửa, mà sửa layout tốn token hơn nhiều so với sửa lúc mới là mấy cái khung. Vẽ wireframe trước giúp mình và AI thống nhất layout từ đầu, code một lần là ra.

## Prompt

Copy đoạn dưới, paste vào Claude Chat:

```
Đóng vai Senior Product Designer. Dựa trên spec sản phẩm mình đã đưa ở các bước trước, vẽ wireframe cho từng màn hình, ưu tiên đúng layout/tỷ lệ hơn đẹp, chỉ khung + label chức năng. Hỏi platform và đề xuất hệ lưới phù hợp, chờ xác nhận trước khi vẽ. Chỗ nào spec chưa rõ layout thì hỏi tôi, đừng tự suy diễn. Vẽ theo từng nhóm màn hình, chờ xác nhận rồi mới sang nhóm tiếp.

Đây là spec sản phẩm của mình (PRD + Product Discovery):
[DÁN NỘI DUNG BƯỚC 2 VÀ BƯỚC 3 VÀO ĐÂY]
```

> Dán kèm nếu bạn đang mở cửa sổ chat mới. Nếu dùng chung 1 cửa sổ chat xuyên suốt từ đầu thì bỏ qua — Chat đã có sẵn context, dán lại là thừa.

Mấu chốt nằm ở câu "hỏi platform và đề xuất hệ lưới, chờ xác nhận trước khi vẽ, chỗ nào chưa rõ thì hỏi": bỏ câu đó ra AI sẽ tự đoán layout theo cảm tính, đúng cái mình đang muốn tránh.

## Trả lời sao cho ăn tiền

- **Chốt platform trước khi để AI đề xuất hệ lưới.** Grid cho mobile khác hẳn grid cho web.
- **Đừng duyệt qua loa.** Nút to/nhỏ sai, nút đặt sai vị trí (VD nằm quá xa tầm tay khi dùng một tay) là chuyện nhỏ lúc còn là khung, tốn gấp nhiều lần token nếu để tới lúc thành sản phẩm mới sửa.
- **Rút rule chung sau khi sửa vài màn đầu**, rồi áp cho toàn bộ màn còn lại – ví dụ nút hành động luôn nằm cố định một vị trí, cỡ chữ số tiền/label đồng bộ. Làm vậy để cả bộ màn hình đồng nhất, không cái nào lệch.
- **Không biết đẹp/hợp lý là gì thì tham khảo web2** – app cùng nhóm chức năng (app chuyển tiền thì xem app ngân hàng) đã được hàng triệu người dùng thử rồi.

## Ví dụ

> 🚧 **Đang build.** Ví dụ của bước này lấy từ dự án mẫu trong [`example/`](../example/) – dự án đang được build **song song** với series, đúng theo từng bước. Bước nào build xong thì ví dụ của bước đó được viết vào đây, kèm mục *Prompt này từng hụt chỗ nào*.

Xong bước này mới qua Bước 5, setup môi trường để bắt đầu code.
