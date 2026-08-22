# Bước 6: Build

Khâu chuẩn bị xong rồi. Đang có 2 file spec – một về tính năng (Bước 3), một về giao diện (Bước 4). Bước này ném cả hai vào folder dự án và bắt đầu build thật.

## Vì sao chia 3 giai đoạn

Lỗi hay gặp nhất: build xong một màn hình là dành thời gian chăm chút giao diện cho đẹp luôn, rồi mới qua màn tiếp theo. Đến khi phát hiện logic sai hoặc cần đổi flow, phải sửa từ đầu – phần giao diện đã tốn công trước đó gần như bỏ đi, lãng phí token.

Cách tránh: tách hẳn 3 giai đoạn, xong hẳn cái này mới sang cái kia.

| Giai đoạn | Làm gì | Công cụ |
|---|---|---|
| **1 – Logic & flow** | UI để mộc, không cần đẹp. Build từng tính năng theo đúng thứ tự spec, xong cái nào test cái đó | Claude Code |
| **2 – Giao diện** | Chốt hình hài app trên công cụ design trước, rồi mới bắt Code dựng lại | **Claude Design** → Claude Code |
| **3 – Live & sửa theo người dùng** | Đưa sản phẩm cho người thật xài, sửa dần tới khi không ai chê được nữa | Claude Code |

Lý do tách Giai đoạn 2 ra thành một vòng riêng: **sửa giao diện bằng cách tả bằng lời cho Claude Code là cách đắt nhất.** Mỗi lần "nút này dịch xuống tí", "màu này nhạt quá" là một vòng sửa code – chạy lại – chụp màn hình – nhìn – chưa ưng – sửa tiếp. Chốt hình hài ở công cụ design trước, khi nào nhìn đã mắt rồi mới đưa sang Code dựng một lần.

---

## Giai đoạn 1 – Logic và flow

Copy 2 file spec (Bước 3, Bước 4) vào folder dự án. Mở PowerShell, chạy `claude` để mở Claude Code, dán prompt dưới.

```
Đọc toàn bộ folder dự án [tên dự án của bạn] trước khi build.

GIAI ĐOẠN 1 – Logic và flow
Build từng tính năng một theo đúng thứ tự trong file spec tính năng. Với mỗi tính năng, code logic và flow trước, gồm xử lý dữ liệu, điều hướng giữa màn hình, validate, xử lý lỗi đúng theo spec. UI lúc này để mộc, chưa cần đẹp, chỉ cần đủ để test được flow. Sau khi xong 1 tính năng, dừng lại báo tôi test, đợi tôi xác nhận OK rồi mới qua tính năng tiếp theo. Không tự thêm tính năng ngoài spec.

Chưa làm giao diện. Chỉ khi tất cả tính năng trong spec đã được tôi xác nhận chạy đúng logic thì dừng lại báo tôi, tôi sẽ tự chuyển qua giai đoạn 2.

Trước khi bắt đầu, xác nhận lại với tôi bạn hiểu thứ tự build các tính năng là gì dựa theo spec.
```

Claude Code sẽ đọc spec, liệt kê lại thứ tự tính năng sắp build, đợi xác nhận rồi mới bắt đầu. Xong tính năng đầu tiên, nó dừng lại chờ mở app test flow – mọi thứ đúng thì gõ "OK" để nó tiếp tục.

**Tiêu chí "xong" ở Giai đoạn 1: nút bấm đúng vị trí mong muốn + flow chạy đúng, thế là đủ.** Ngứa mắt cỡ nào cũng kệ, đừng bắt AI chỉnh màu/spacing/font lúc này.

---

## Giai đoạn 2 – Giao diện

Ba nhịp, đi đúng thứ tự: **đóng gói → thiết kế tới khi ưng → xuất spec cho Code dựng lại.**

### 2.1. Bảo Claude Code đóng gói spec giao diện

Đừng tự ngồi mô tả app đang trông thế nào – Claude Code đang mở dự án, để nó tự đọc code rồi viết ra. Dán prompt này:

```
Đọc toàn bộ giao diện hiện tại trong dự án rồi viết ra một file spec mô tả CHÍNH XÁC những gì đang có, để tôi mang sang một AI thiết kế khác.

Yêu cầu file spec:
- Sản phẩm là gì, người dùng là ai, chạy trên khổ màn hình nào
- Toàn bộ design token đang dùng: màu, font, cỡ chữ, bo góc, đổ bóng, khoảng cách
- Hệ lưới / cách chia bố cục từng màn
- Liệt kê TỪNG màn: có gì trên đó, đặt ở đâu, chữ hiển thị chính xác là gì, bấm vào thì ra sao
- Các trạng thái: đang tải, trống, lỗi, disabled
- Ràng buộc kỹ thuật nào bắt buộc phải giữ nguyên khi đổi giao diện

Chỉ mô tả hiện trạng. Không góp ý, không đề xuất sửa, không so sánh với tài liệu cũ.
Lưu vào docs/ trong dự án và copy thêm một bản ra Desktop cho tôi dễ lấy.
```

Cái cần là **mô tả hiện trạng**, không phải bản thiết kế mơ ước – Claude Design cần biết nó đang sửa cái gì.

### 2.2. Sang Claude Design, chỉnh tới khi ưng mắt

Mở [Claude Chat](https://claude.ai), đính file spec vừa xuất, rồi bảo nó dựng lại các màn thành bản thiết kế nhìn được.

**Đây là chỗ được phép khó tính, và nên khó tính.** Cứ nói chuyện qua lại tới khi app đúng ý:

- Nút này nên nằm ở đâu, to nhỏ ra sao
- Font gì, cỡ nào, chỗ nào đậm chỗ nào nhạt
- Bảng màu, màu chính là màu gì, màu nhấn dùng vào đâu
- Khoảng cách, bo góc, đổ bóng

Sửa bao nhiêu vòng cũng được – ở đây nó chỉ vẽ lại, **không đụng vào code dự án**, nên sai thì sửa tiếp, không tốn gì ngoài mấy phút. Đây chính là lý do tách giai đoạn này ra: chỗ này lặp rẻ, còn lặp ở Claude Code thì đắt.

Chưa ưng thì **chưa đưa sang Code**. Nhìn còn thấy gợn ở đâu là nói tiếp ở đây.

### 2.3. Ưng rồi thì bảo Claude Design xuất spec

Khi nhìn đã thuận mắt, bảo nó đóng gói lại:

```
Thiết kế tới đây là chốt. Xuất cho tôi một gói bàn giao để đưa cho Claude Code dựng lại trong dự án thật, gồm:
- File mô tả: design token (màu, font, cỡ chữ, bo góc, đổ bóng), hệ lưới, và từng màn có gì đặt ở đâu
- Bản dựng tĩnh của TẤT CẢ các màn ở đúng khổ màn hình thật, để làm bản tham chiếu
- Toàn bộ asset: logo, icon, hình
```

Gói này mang về folder dự án, rồi quay lại Claude Code:

```
Đọc gói bàn giao thiết kế trong [tên folder] rồi dựng lại toàn bộ giao diện cho đúng.

Yêu cầu:
- Gom mọi màu/font/cỡ chữ/bo góc/đổ bóng về MỘT chỗ định nghĩa duy nhất, component chỉ được dùng lại từ đó. Không viết màu hay cỡ chữ trực tiếp trong từng màn.
- Hệ lưới cũng định nghĩa một chỗ dùng chung cho các màn cùng dạng, đừng chép lại ở từng file.
- Mọi kích thước và khoảng cách neo theo tỷ lệ màn hình, không hardcode pixel.
- Icon lấy từ đúng bộ trong gói bàn giao, không tự thay bằng icon library khác.

Làm xong thì tự chạy app, tự chụp màn hình và tự đo lại vị trí các khối, đối chiếu với bản dựng tham chiếu rồi báo tôi số đo. Đừng đoán bằng mắt.
```

**Chỗ dễ mất công nhất:** không có câu "tự chạy, tự chụp, tự đo" cuối cùng thì rất dễ nhận về một bản build *biên dịch sạch nhưng nhìn sai*. Ở dự án mẫu, code pass hết kiểm tra mà nút bấm hiện ra là ô rỗng không có chữ – chỉ chụp ảnh lên mới thấy.

Chưa ưng chỗ nào thì **quay lại 2.2 sửa ở Claude Design**, đừng ngồi tả bằng lời cho Claude Code sửa vặt từng li.

---

## Giai đoạn 3 – Live rồi sửa theo người dùng

Đây mới là giai đoạn quyết định sản phẩm có ai xài không.

1. **Đưa sản phẩm lên live**, có link cho người ngoài vào được.
2. **Tự mình xài thật** như một người dùng bình thường, không phải như người viết ra nó – đi hết flow từ đầu, đừng bỏ qua bước nào vì "biết rồi".
3. **Đưa cho người khác test.** Quan trọng là người *không* biết gì về dự án. Đừng hướng dẫn trước, cứ đưa link rồi ngồi nhìn họ mò – chỗ họ khựng lại chính là chỗ sai, dù bạn thấy nó hiển nhiên.
4. **Ghi lại mọi lời chê**, kể cả lời khó nghe. "Không hiểu bấm gì tiếp" cũng là bug, ngang với app crash.
5. **Sửa dần**: lỗi hiển thị, lỗi logic, chỗ gây hiểu nhầm. Sửa xong đưa test lại.

Lặp tới khi **không ai còn chê được gì nữa** thì mới coi là xong. Không phải xong lúc code chạy được.

> Đừng ngại những góp ý khó nghe. Người dùng chê là người dùng còn quan tâm; đáng sợ hơn là họ vào, không hiểu gì, rồi đi luôn mà không nói gì cả.

---

## Trả lời sao cho ăn tiền

- **Kiên nhẫn đi từng tính năng một.** Đừng để nó gộp nhiều tính năng vào một lượt build vì "cho nhanh".
- **Xong hẳn giai đoạn này mới sang giai đoạn kia.** Logic ổn định trước thì chỉnh giao diện sau không làm gãy flow.
- **Đừng chỉnh giao diện bằng mồm ở Giai đoạn 1.** Ngứa mắt thì ghi lại, để dành xử một lượt ở Giai đoạn 2.
- **Ở Giai đoạn 2, mọi vị trí/kích thước phải neo theo tỷ lệ màn hình, không phải pixel cố định.** Hardcode px (VD "cao 80px", "cách 40px") chỉ đúng trên đúng một kích thước màn hình – khách dùng máy nhỏ hơn/lớn hơn là vỡ layout ngay. Dùng đơn vị co giãn (`flex-grow`, `%`, `vh`/`vw`, `cqh`) cho mọi khoảng cách lấy từ hệ lưới ở Bước 4. Tailwind CSS v4 không build được class `flex-[N]` (arbitrary value phân số) – dùng `style={{ flex: "N 1 0" }}` inline, xem `HANDOFF.md` mục 4.8.
- **Bắt AI tự kiểm tra bằng số đo, đừng để nó (và bạn) đoán bằng mắt.** Xem mục 2 phần dưới.
- **Build app không phải thả cho AI tự làm hết.** Có lúc phải tự tay tạo tài khoản, lấy API key, tạo database, deploy smart contract – cứ làm rồi sửa, ai cũng chật vật ở bước này.

## 5 thứ làm bạn chậm gấp nhiều lần

TapTip (dự án từng build song song với series, giờ ở [`KattyFury/taptip`](https://github.com/KattyFury/taptip)) chỉ có 5 tính năng, lại fork sẵn code nền của Circle – vậy mà mất nhiều buổi. Không phải vì khó, mà vì 5 cái bẫy dưới đây. Tránh được là nhanh hơn hẳn:

1. **Không đọc docs/skill của SDK trước khi code.** Lao vào code rồi mới tra khi gặp lỗi – mất cả buổi cho mấy lỗi mà trang đầu tài liệu đã ghi rõ cách tránh. Đụng SDK lạ thì đọc 5 phút trước, tiết kiệm 5 tiếng sau.
2. **Sửa giao diện mà không nhìn thấy được kết quả.** Sửa layout cả chục vòng theo kiểu đoán, mỗi lần lại phải chụp màn hình gửi cho AI. Bảo AI dựng cách tự kiểm tra trước (chụp màn hình tự động, đo toạ độ từng phần tử) rồi hãy sửa – tìm ra nguyên nhân trong một lần.
3. **Tin rằng code AI viết ra là có tác dụng.** Có lúc AI viết class CSS mà framework không hề dịch ra – sửa mãi layout không nhích một milimet, cứ tưởng do tính sai. Layout không đổi sau khi sửa thì nghi ngờ "code có chạy không" trước, đừng nghi công thức.
4. **Gộp nhiều sửa đổi rồi mới kiểm tra một lượt.** Xoá dòng import mà quên dòng đang dùng nó → app crash. Bắt AI chạy kiểm tra lỗi + tải lại app ngay sau mỗi lần sửa, đừng để dồn.
5. **Né giới hạn kỹ thuật bằng cách đổi trải nghiệm người dùng.** Gặp giới hạn của gói miễn phí, AI đề xuất đổi luôn cách đăng nhập cho nhanh – may mà bắt lại kịp. Giới hạn kỹ thuật không phải lý do để đổi thứ người dùng của bạn sẽ chạm vào mỗi ngày; tìm cách giữ đúng trải nghiệm trước.

Chi tiết từng lỗi (kèm nguyên nhân kỹ thuật thật) nằm ở [`docs/06-build.md`](https://github.com/KattyFury/taptip/blob/main/docs/06-build.md).

## Kết quả cuối

Một website để người khác vào trải nghiệm thật, đã qua tay người ngoài test và đã sửa theo những gì họ chê.

## Chia sẻ sản phẩm

Đừng ngại đăng lên X, Arc House, Discord – và đừng ngại những góp ý khó nghe, feedback người dùng giúp hoàn thiện sản phẩm tốt hơn. Cấu trúc bài đăng đơn giản:

1. Giới thiệu bản thân
2. Vì sao làm dapp này, xây dựng thế nào, mất bao lâu
3. Giới thiệu sản phẩm, mời trải nghiệm

## Ví dụ

TapTip, fork từ [`circlefin/arc-p2p-payments`](https://github.com/circlefin/arc-p2p-payments) – đi đúng 3 giai đoạn trên. Dự án này từng build song song với series, giờ đã tách sang repo riêng [`KattyFury/taptip`](https://github.com/KattyFury/taptip).

**Giai đoạn 1** xong toàn bộ 5 tính năng với UI mộc: [`docs/06-build.md`](https://github.com/KattyFury/taptip/blob/main/docs/06-build.md).

**Giai đoạn 2** đi đủ 3 nhịp:

| Nhịp | Kết quả thật |
|---|---|
| 2.1 Đóng gói spec hiện trạng | [`docs/08-design-spec-hien-trang.md`](https://github.com/KattyFury/taptip/blob/main/docs/08-design-spec-hien-trang.md) – Claude Code tự đọc code viết ra |
| 2.2 Chỉnh ở Claude Design | Đổi hẳn bảng màu (xám/đỏ → trắng/vàng `#FFCC00`/xanh `#0B53BF`), đổi font (Archivo → Nunito + Comfortaa riêng cho con số), dời lại vị trí một số khối |
| 2.3 Xuất gói cho Code dựng lại | Gói [`design_handoff_taptip/`](https://github.com/KattyFury/taptip/tree/main/design_handoff_taptip) (mô tả + bản dựng tĩnh 15 màn + asset) → kết quả build ở [`docs/08-redesign-handoff.md`](https://github.com/KattyFury/taptip/blob/main/docs/08-redesign-handoff.md) |

Đúng như cảnh báo ở 2.3: bản dựng lại **pass hết kiểm tra tự động** (typecheck sạch, build thành công 24 route) mà vẫn có 3 lỗi chỉ lòi ra khi chụp ảnh và đo thật – trong đó có lỗi nút bấm hiện ra thành **ô rỗng không có chữ**. Số đo và cách tìm ra ghi ở mục 7 của file trên.

**Giai đoạn 3 tạm gác** cùng lúc dự án được tách repo – app cần người dùng thật mới có cái để sửa theo, phần này để dành cho lúc quay lại `KattyFury/taptip`.

---

Series tới đây là hết. Có thể sẽ có thêm tập bonus: *1 Prompt Đưa Bạn Từ Ý Tưởng Đến Sản Phẩm Hoàn Chỉnh.*
