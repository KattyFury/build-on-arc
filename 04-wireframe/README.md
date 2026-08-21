# Bước 4: Vẽ wireframe

Có bản plan chi tiết từ Bước 3 rồi – tới lúc vẽ khung sườn từng màn hình, trước khi code UI thật.

## Vì sao cần bước này

Nhảy vào code luôn thì AI tự bịa layout theo cảm tính của nó. Code xong nhìn không đúng ý lại phải sửa, mà sửa layout tốn token hơn nhiều so với sửa lúc mới là mấy cái khung. Vẽ wireframe trước giúp mình và AI thống nhất layout từ đầu, code một lần là ra.

## Prompt

Copy đoạn dưới, paste vào Claude Chat:

```
Đóng vai Senior Product Designer. Dựa trên spec sản phẩm mình đã đưa ở các bước trước, vẽ wireframe cho từng màn hình, ưu tiên đúng layout/tỷ lệ hơn đẹp, chỉ khung + label chức năng. Hỏi platform và đề xuất hệ lưới phù hợp, chờ xác nhận trước khi vẽ. Chỗ nào spec chưa rõ layout thì hỏi tôi, đừng tự suy diễn. Vẽ theo từng nhóm màn hình, chờ xác nhận rồi mới sang nhóm tiếp.

Hệ lưới phải phát biểu bằng TỶ LỆ: chia màn thành N hàng, mỗi hàng bằng 1/N chiều cao màn. Px chỉ ghi trong ngoặc cho dễ hình dung, không phải con số để code theo.

Mỗi màn liệt kê đủ N hàng, hàng nào trống cũng phải ghi ra là trống – đừng chỉ kể mấy hàng có nội dung.

Chỗ nào hiển thị nội dung thay đổi được (số dư, tên người, ngày giờ, danh sách): hỏi mình giá trị ngắn nhất và dài nhất có thể ra, rồi ghi rõ khi độ dài đổi thì layout xử lý sao – cụm chữ đứng yên tại chỗ hay được phép nhảy.

Màn nào phụ thuộc hệ điều hành hoặc trình duyệt (hướng dẫn cài app vào màn hình chính, xin quyền camera, quyền thông báo) thì vẽ đủ biến thể, đừng vẽ mỗi bản iPhone rồi coi như xong.

Màn nào có dữ liệu hoặc phải chờ thì vẽ đủ trạng thái xấu: đang tải, trống chưa có gì, lỗi/mất mạng, không được cấp quyền.

Đây là spec sản phẩm của mình (PRD + Product Discovery):
[DÁN NỘI DUNG BƯỚC 2 VÀ BƯỚC 3 VÀO ĐÂY]
```

> Dán kèm nếu bạn đang mở cửa sổ chat mới. Nếu dùng chung 1 cửa sổ chat xuyên suốt từ đầu thì bỏ qua – Chat đã có sẵn context, dán lại là thừa.

Mấu chốt nằm ở câu "hỏi platform và đề xuất hệ lưới, chờ xác nhận trước khi vẽ, chỗ nào chưa rõ thì hỏi": bỏ câu đó ra AI sẽ tự đoán layout theo cảm tính, đúng cái mình đang muốn tránh.

## Trả lời sao cho ăn tiền

- **Chốt platform trước khi để AI đề xuất hệ lưới.** Grid cho mobile khác hẳn grid cho web.
- **Đừng duyệt qua loa.** Nút to/nhỏ sai, nút đặt sai vị trí (VD nằm quá xa tầm tay khi dùng một tay) là chuyện nhỏ lúc còn là khung, tốn gấp nhiều lần token nếu để tới lúc thành sản phẩm mới sửa.
- **Rút rule chung sau khi sửa vài màn đầu**, rồi áp cho toàn bộ màn còn lại – ví dụ nút hành động luôn nằm cố định một vị trí, cỡ chữ số tiền/label đồng bộ. Làm vậy để cả bộ màn hình đồng nhất, không cái nào lệch.
- **Không biết đẹp/hợp lý là gì thì tham khảo web2** – app cùng nhóm chức năng (app chuyển tiền thì xem app ngân hàng) đã được hàng triệu người dùng thử rồi.
- **Hệ lưới là tỷ lệ, không phải pixel cố định.** Con số kiểu "mỗi hàng ~81.2px" chỉ để hình dung trên MỘT kích thước màn hình cụ thể lúc vẽ khung – khi code thật phải chuyển thành tỷ lệ co giãn (`flex-grow`, `%`, `vh`/`vw`), không hardcode px. Máy khách xài màn hình nhỏ hơn/lớn hơn mà thiết kế cứng theo px thì layout vỡ ngay. Nếu code bằng Tailwind CSS v4, dùng `style={{ flexGrow: N }}` inline thay vì class `flex-[N]` – bản v4 không build class đó thành CSS thật (xem chi tiết ở `HANDOFF.md` mục 4.8).

## Ví dụ: Wireframe TapTip

Kết quả chạy thật prompt trên. Bản đầy đủ: [`example/docs/04-wireframe.md`](../example/docs/04-wireframe.md).

Chốt trước khi vẽ: platform **PWA**, khung 375×812, **chia dọc 10 hàng**. Xong rồi rút ra 2 nguyên tắc áp cho mọi màn – đây mới là thứ giữ cả bộ màn hình đồng nhất, chứ không phải từng màn vẽ đẹp riêng:

- Nội dung chính luôn căn giữa vùng **hàng 1-6**
- Nút hành động luôn nằm ở **hàng 9**: hoặc 1 nút full-width, hoặc cặp "Quay lại" (1/3 trái) + nút chính (2/3 phải)

| Màn | Hàng 1-6 | Hàng 9 | Hàng 10 |
|---|---|---|---|
| Đăng nhập | Input email → 6 ô nhập OTP | Quay lại 1/3 + Tiếp tục 2/3 | trống |
| Thiết lập Passkey | Icon FaceID + mô tả | Quay lại 1/3 + Bật passkey 2/3 | "Bỏ qua, dùng email/OTP" |
| Home | Balance (hàng 1) · QR to (2-5) · chú thích "Cho người khác quét để nhận tip" (6) | Tip ngẫu nhiên 1/3 + Tip 2/3 | Icon menu ☰ |

Home cố tình **không có bottom nav** – mọi thứ phụ đẩy hết vào popup của icon ☰, để hàng 2-5 dành trọn cho QR. App này mở ra là để chìa QR cho người ta quét, không phải để lướt.

> Chỗ đáng học nhất là con số **"mỗi hàng ~81.2px"** trong bản wireframe. Nó đúng trên đúng một cái màn hình 812px, và tới lúc code thật thì `h-40`, `mt-10` làm vỡ layout ngay trên máy khác kích thước. Hệ lưới là **tỷ lệ**, px chỉ để hình dung. Bản prompt giờ bắt phát biểu hệ lưới bằng tỷ lệ ngay từ đầu, đỡ được nguyên một vòng sửa ở Bước 6.

## Prompt này từng hụt chỗ nào

Năm chỗ, đều lòi ra lúc đem wireframe đi code thật ở Bước 6 – không chỗ nào nhìn bản vẽ mà thấy được:

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| 1 | Hệ lưới ra bằng px ("mỗi hàng ~81.2px"), code theo px là vỡ layout trên màn hình khác kích thước | Bắt phát biểu hệ lưới bằng tỷ lệ 1/N chiều cao, px chỉ để trong ngoặc |
| 2 | Chỉ liệt kê hàng có nội dung, hàng trống bỏ lửng. Lúc code, khối nội dung nuốt luôn phần dư nên tỷ lệ thật lệch hẳn so với lưới đã tính | Bắt liệt kê đủ N hàng, hàng trống cũng phải ghi ra là trống |
| 3 | Không hỏi nội dung động dài ngắn cỡ nào. Balance vẽ mẫu "1.250.000đ", tới lúc số dư đổi thì cả cụm nhảy vị trí, phải quay lại sửa thành ô rộng cố định | Bắt hỏi giá trị ngắn nhất/dài nhất, và ghi rõ độ dài đổi thì layout xử lý sao |
| 4 | Màn "Thêm app vào màn hình chính" vẽ đúng một bản Safari trên iPhone, Android mở lên là hướng dẫn sai hoàn toàn | Bắt vẽ đủ biến thể cho màn phụ thuộc hệ điều hành/trình duyệt |
| 5 | Chỉ vẽ trạng thái đẹp. Thiếu màn lịch sử lúc chưa có giao dịch nào, thiếu màn không được cấp quyền camera | Bắt vẽ đủ trạng thái xấu: đang tải, trống, lỗi/mất mạng, bị từ chối quyền |

Xong bước này mới qua Bước 5, setup môi trường để bắt đầu code.
