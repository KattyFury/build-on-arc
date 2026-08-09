# Bước 6: Build

Khâu chuẩn bị xong rồi. Đang có 2 file spec – một về tính năng (Bước 3), một về giao diện (Bước 4). Bước này ném cả hai vào folder dự án và bắt đầu build thật.

## Vì sao chia 2 giai đoạn

Lỗi hay gặp nhất: build xong một màn hình là dành thời gian chăm chút giao diện cho đẹp luôn, rồi mới qua màn tiếp theo. Đến khi phát hiện logic sai hoặc cần đổi flow, phải sửa từ đầu – phần giao diện đã tốn công trước đó gần như bỏ đi, lãng phí token.

Cách tránh: tách hẳn 2 giai đoạn.

- **Giai đoạn 1 – Logic và flow.** UI để mộc, không cần đẹp. Build từng tính năng theo đúng thứ tự trong spec, xong tính năng nào test ngay tính năng đó.
- **Giai đoạn 2 – Giao diện.** Chỉ bắt đầu khi TOÀN BỘ tính năng đã chạy đúng. Lúc này mới chỉnh nút bấm, màu sắc, chi tiết hiển thị theo wireframe.

## Cách làm

Copy 2 file spec (Bước 3, Bước 4) vào folder dự án. Mở PowerShell, chạy `claude` để mở Claude Code, dán prompt dưới.

## Prompt

```
Đọc toàn bộ folder dự án [tên dự án của bạn] trước khi build.

GIAI ĐOẠN 1 – Logic và flow
Build từng tính năng một theo đúng thứ tự trong file spec tính năng. Với mỗi tính năng, code logic và flow trước, gồm xử lý dữ liệu, điều hướng giữa màn hình, validate, xử lý lỗi đúng theo spec. UI lúc này để mộc, chưa cần đẹp, chỉ cần đủ để test được flow. Sau khi xong 1 tính năng, dừng lại báo tôi test, đợi tôi xác nhận OK rồi mới qua tính năng tiếp theo. Không tự thêm tính năng ngoài spec. Chỉ khi tất cả tính năng trong spec đã được tôi xác nhận chạy đúng logic mới chuyển qua giai đoạn 2.

GIAI ĐOẠN 2 – Giao diện
Lúc này mới áp UI theo đúng file wireframe spec cho toàn bộ app, đảm bảo đồng bộ giữa các màn về layout, spacing, font size. Làm từng màn một, dừng lại cho tôi xem rồi mới qua màn tiếp theo.

Trước khi bắt đầu, xác nhận lại với tôi bạn hiểu thứ tự build các tính năng là gì dựa theo spec.
```

Claude Code sẽ đọc spec, liệt kê lại thứ tự tính năng sắp build, đợi xác nhận rồi mới bắt đầu. Xong tính năng đầu tiên, nó dừng lại chờ mở app test flow – mọi thứ đúng thì gõ "OK" để nó tiếp tục.

## Trả lời sao cho ăn tiền

- **Kiên nhẫn đi từng tính năng một.** Đừng để nó gộp nhiều tính năng vào một lượt build vì "cho nhanh".
- **Giai đoạn 1 xong hết mới sang Giai đoạn 2.** Logic ổn định trước thì chỉnh giao diện sau không làm gãy flow.
- **Tiêu chí "xong" ở Giai đoạn 1: nút bấm đúng vị trí mong muốn + flow chạy đúng, thế là đủ – đừng quan tâm đẹp/xấu.** Ngứa mắt cỡ nào cũng kệ, đừng bắt AI chỉnh màu/spacing/font lúc này. Đưa nguyên spec giao diện qua Chat (hoặc công cụ design riêng) làm một lượt ở Giai đoạn 2 nhanh hơn hẳn so với vừa build logic vừa chăm chút từng màn.
- **Ở Giai đoạn 2, mọi vị trí/kích thước phải neo theo tỷ lệ màn hình, không phải pixel cố định.** Hardcode px (VD "cao 80px", "cách 40px") chỉ đúng trên đúng một kích thước màn hình – khách dùng máy nhỏ hơn/lớn hơn là vỡ layout ngay. Dùng đơn vị co giãn (`flex-grow`, `%`, `vh`/`vw`) cho mọi khoảng cách và kích thước lấy từ hệ lưới ở Bước 4. Tailwind CSS v4 không build được class `flex-[N]` (arbitrary value phân số) – dùng `style={{ flexGrow: N }}` inline, xem `HANDOFF.md` mục 4.8.
- **Build app không phải thả cho AI tự làm hết.** Có lúc phải tự tay tạo tài khoản, lấy API key, tạo database, deploy smart contract – cứ làm rồi sửa, ai cũng chật vật ở bước này.

## 5 thứ làm bạn chậm gấp nhiều lần

Dự án mẫu trong [`example/`](../example/) chỉ có 5 tính năng, lại fork sẵn code nền của Circle – vậy mà mất nhiều buổi. Không phải vì khó, mà vì 5 cái bẫy dưới đây. Tránh được là nhanh hơn hẳn:

1. **Không đọc docs/skill của SDK trước khi code.** Lao vào code rồi mới tra khi gặp lỗi – mất cả buổi cho mấy lỗi mà trang đầu tài liệu đã ghi rõ cách tránh. Đụng SDK lạ thì đọc 5 phút trước, tiết kiệm 5 tiếng sau.
2. **Sửa giao diện mà không nhìn thấy được kết quả.** Sửa layout cả chục vòng theo kiểu đoán, mỗi lần lại phải chụp màn hình gửi cho AI. Bảo AI dựng cách tự kiểm tra trước (chụp màn hình tự động, đo toạ độ từng phần tử) rồi hãy sửa – tìm ra nguyên nhân trong một lần.
3. **Tin rằng code AI viết ra là có tác dụng.** Có lúc AI viết class CSS mà framework không hề dịch ra – sửa mãi layout không nhích một milimet, cứ tưởng do tính sai. Layout không đổi sau khi sửa thì nghi ngờ "code có chạy không" trước, đừng nghi công thức.
4. **Gộp nhiều sửa đổi rồi mới kiểm tra một lượt.** Xoá dòng import mà quên dòng đang dùng nó → app crash. Bắt AI chạy kiểm tra lỗi + tải lại app ngay sau mỗi lần sửa, đừng để dồn.
5. **Né giới hạn kỹ thuật bằng cách đổi trải nghiệm người dùng.** Gặp giới hạn của gói miễn phí, AI đề xuất đổi luôn cách đăng nhập cho nhanh – may mà bắt lại kịp. Giới hạn kỹ thuật không phải lý do để đổi thứ người dùng của bạn sẽ chạm vào mỗi ngày; tìm cách giữ đúng trải nghiệm trước.

Chi tiết từng lỗi (kèm nguyên nhân kỹ thuật thật) nằm ở [`example/docs/06-build.md`](../example/docs/06-build.md).

## Kết quả cuối

Một website để người khác vào trải nghiệm thật.

## Chia sẻ sản phẩm

Đừng ngại đăng lên X, Arc House, Discord – và đừng ngại những góp ý khó nghe, feedback người dùng giúp hoàn thiện sản phẩm tốt hơn. Cấu trúc bài đăng đơn giản:

1. Giới thiệu bản thân
2. Vì sao làm dapp này, xây dựng thế nào, mất bao lâu
3. Giới thiệu sản phẩm, mời trải nghiệm

## Ví dụ

> 🚧 **Đang build.** Ví dụ của bước này lấy từ dự án mẫu trong [`example/`](../example/) – TapTip fork từ [`circlefin/arc-p2p-payments`](https://github.com/circlefin/arc-p2p-payments), build theo đúng 2 giai đoạn ở trên.

---

Series tới đây là hết. Có thể sẽ có thêm tập bonus: *1 Prompt Đưa Bạn Từ Ý Tưởng Đến Sản Phẩm Hoàn Chỉnh.*
