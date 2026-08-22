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
- **Hệ lưới là tỷ lệ, không phải pixel cố định.** Con số kiểu "mỗi hàng ~81.2px" chỉ để hình dung trên MỘT kích thước màn hình cụ thể lúc vẽ khung – khi code thật phải chuyển thành tỷ lệ co giãn (`flex-grow`, `%`, `vh`/`vw`), không hardcode px. Máy khách xài màn hình nhỏ hơn/lớn hơn mà thiết kế cứng theo px thì layout vỡ ngay. Nếu code bằng Tailwind CSS v4, dùng `style={{ flexGrow: N }}` inline thay vì class `flex-[N]` – bản v4 không build class đó thành CSS thật.

## Ví dụ: Wireframe EZwallet

Dự án thật của tác giả – [`KattyFury/ezwallet`](https://github.com/KattyFury/ezwallet). Không chạy đúng prompt trên (dự án có trước series), nhưng độc lập chốt ra **đúng cùng một hệ lưới 10 hàng** – dấu hiệu tốt cho thấy đây không phải luật riêng của một app, mà là cách hợp lý để bố cục màn hình mobile chữ to cho người lớn tuổi.

- Nội dung chính của mỗi màn nằm trong vùng linh hoạt ở giữa
- Nút hành động luôn nằm ở **hàng 9**: một nút rộng 3/4 màn, hoặc cặp nút chia đôi – **hàng 10 chỉ dành riêng cho thanh điều hướng 4 tab chính**, không lẫn với nút hành động của từng màn

| Màn | Nội dung | Hàng 9 | Hàng 10 |
|---|---|---|---|
| Home (Gửi) | Số dư (1-2) · danh sách token (3-5.5) · thông báo (7-8) | 3 action-card: Dán · Quét QR · Danh bạ | Thanh điều hướng 4 tab |
| Swap | 3 khối chia đều: You pay/You receive · thanh trượt % + gợi ý số chẵn | Nút Swap (rộng 3/4 màn, đồng tâm với action-card ở Home) | (đã gộp vào Service Hub, hàng 10 đổi thành chữ "Exit") |
| Màn phụ (Ngôn ngữ, Bảo mật, Giới thiệu...) | Hàng 1 = tiêu đề, nội dung hàng 2 trở xuống | Nút "Quay lại" hoặc cặp Quay lại/Xác nhận | Trống – màn phụ không có thanh điều hướng |

Bốn màn chính (Gửi/Nhận/Lịch sử/Menu) giữ nguyên hàng 10 cho thanh điều hướng xuyên suốt cả app; mọi màn phụ mở ra từ đó thì hàng 10 bỏ trống, nút hành động dồn hết vào hàng 9 – đúng nguyên tắc "nút hành động luôn ở một chỗ cố định" mà bước này dạy, chỉ khác điểm neo cụ thể so với TapTip.

> Chỗ đáng học nhất không phải hệ lưới (đã đúng ngay từ đầu, độc lập với series) mà là hai lỗi layout thật xảy ra SAU khi hệ lưới đã chốt, đúng kiểu lỗi mà bước này cố tránh: (1) một màn quên khai `grid-template-columns: minmax(0,1fr)` cho container – một chuỗi chữ không xuống dòng đủ dài là kéo phình cả cột, lệch nguyên màn hình; (2) một lưới 2 cột ép ô vuông cứng bằng `aspectRatio:1` mà không tính chữ dài tràn ra ngoài trên màn hẹp – bỏ ép vuông, để `gridAutoRows:'1fr'` cho các ô tự cao bằng nhau mới hết tràn. Cả hai đều là lỗi *sau khi có wireframe đúng*, vì wireframe không thể lường trước từng dòng CSS – nhưng "vẽ đủ N hàng, hàng nào cũng phải khai rõ" (luật bước này) là đúng thứ giảm được loại lỗi thứ hai.

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
