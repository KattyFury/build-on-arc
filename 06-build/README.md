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
- **Ở Giai đoạn 2, mọi vị trí/kích thước phải neo theo tỷ lệ màn hình, không phải pixel cố định.** Hardcode px (VD "cao 80px", "cách 40px") chỉ đúng trên đúng một kích thước màn hình – khách dùng máy nhỏ hơn/lớn hơn là vỡ layout ngay. Dùng đơn vị co giãn (`flex-grow`, `%`, `vh`/`vw`, `cqh`) cho mọi khoảng cách lấy từ hệ lưới ở Bước 4. Tailwind CSS v4 không build được class `flex-[N]` (arbitrary value phân số) – dùng `style={{ flex: "N 1 0" }}` inline.
- **Bắt AI tự kiểm tra bằng số đo, đừng để nó (và bạn) đoán bằng mắt.** Xem mục 2 phần dưới.
- **Build app không phải thả cho AI tự làm hết.** Có lúc phải tự tay tạo tài khoản, lấy API key, tạo database, deploy smart contract – cứ làm rồi sửa, ai cũng chật vật ở bước này.

## 5 thứ làm bạn chậm gấp nhiều lần

Rút từ quá trình build thật của [`KattyFury/ezwallet`](https://github.com/KattyFury/ezwallet) – ví crypto cho người dùng phổ thông, chạy thật trên Arc Testnet. Không phải vì dự án khó, mà vì 5 cái bẫy dưới đây lặp đi lặp lại. Tránh được là nhanh hơn hẳn:

1. **Không đọc chữ ký hàm thật của SDK trước khi gọi.** Một màn quan trọng (câu hỏi bảo mật) hiện RỖNG TRẮNG, chặn cả luồng tạo ví – dò nguyên nhân bằng cách đoán rồi thử-sai trên production tốn nhiều lượt vẫn sai. Root cause thật: gọi hàm SDK theo kiểu object trong khi hàm đó nhận **tham số vị trí** – đọc thẳng file `.d.ts` trong `node_modules` (30 giây) ra ngay, nhưng chỉ đọc SAU khi đã đoán mò nhiều vòng. Đụng SDK lạ, cư xử lạ: đọc chữ ký hàm thật trước, đừng đoán từ triệu chứng.
2. **Sửa giao diện mà không nhìn thấy được kết quả.** Bắt AI dựng cách tự kiểm tra trước khi sửa: chụp màn hình headless ở nhiều kích thước máy (390px và 375px – đo cả hai, vì lỗi tràn chữ chỉ lộ ra ở máy hẹp hơn), đo toạ độ từng khối bằng script chứ không đoán bằng mắt.
3. **Sửa code mà quên sửa test trong cùng lúc.** Một lần sửa thuật toán gợi ý số tiền nhưng quên đồng bộ file test tương ứng – bộ test báo đỏ suốt **9 ngày** dù app chạy đúng, vì nhìn quen thấy đỏ riết rồi bỏ qua, test mất hẳn tác dụng cảnh báo. Sửa logic ở đâu, sửa test ngay trong cùng một lượt, đừng tách ra "làm sau".
4. **Đổ lỗi cho code của mình trước khi đo.** Ba lần trong một phiên tưởng lỗi do code, hoá ra không phải: chữ tiếng Việt mất dấu khi gửi qua Telegram (do cách gọi lệnh dòng lệnh trên Windows mã hoá sai, không phải server); một tính năng đổi tiền báo lỗi "không tìm được đường" (do hạ tầng bên thứ ba hết thanh khoản test, không phải code); một lỗi tràn giao diện tưởng mới xuất hiện (kiểm bằng cách lùi lại phiên bản code cũ thì hoá ra đã tràn từ trước). Đo trước, đổ lỗi sau.
5. **Gặp giới hạn kỹ thuật thật thì né bằng cách đọc kỹ hơn, không phải đổi ẩu.** RPC công cộng giới hạn số lượng request rất chặt – phản xạ đầu là retry liên tục khi gặp lỗi, mà retry dày lại tự đâm vào chính giới hạn đó, thành vòng lặp tự giết mình. Sửa đúng: gộp nhiều lệnh đọc thành một request (Multicall), giãn cách giữa các lần thử lại, và khi chưa chắc số liệu thì hiện dấu `…` chứ không vẽ số `0` giả – vẽ `0` sai với một app tiền bạc là làm người dùng tưởng mất tiền thật.

Chi tiết từng lỗi (kèm nguyên nhân kỹ thuật thật) nằm ở [`HANDOFF.md`](https://github.com/KattyFury/ezwallet/blob/main/HANDOFF.md) của repo đó, đặc biệt mục "Gotchas" và "Bài học chính".

## Kết quả cuối

Một website để người khác vào trải nghiệm thật, đã qua tay người ngoài test và đã sửa theo những gì họ chê.

## Chia sẻ sản phẩm

Đừng ngại đăng lên X, Arc House, Discord – và đừng ngại những góp ý khó nghe, feedback người dùng giúp hoàn thiện sản phẩm tốt hơn. Cấu trúc bài đăng đơn giản:

1. Giới thiệu bản thân
2. Vì sao làm dapp này, xây dựng thế nào, mất bao lâu
3. Giới thiệu sản phẩm, mời trải nghiệm

## Ví dụ

[`KattyFury/ezwallet`](https://github.com/KattyFury/ezwallet) không được build theo đúng trình tự 3 giai đoạn của bước này (dự án có trước series), nên Giai đoạn 1 và 2 không tách bạch rõ ràng thành hai đợt riêng như prompt trên mô tả – logic và giao diện phát triển đan xen qua nhiều buổi. Đây là điều nên nói thẳng, không giả vờ khớp hoàn toàn: **làm đúng 3 giai đoạn tách bạch vẫn là cách nhanh hơn** cách EZwallet đã đi, không phải ngược lại.

Bù lại, EZwallet đã đi xa hơn hẳn tới **Giai đoạn 3** – phần mà một dự án mới build song song với series chưa kịp chạm tới, vì nó đòi hỏi người dùng thật. Ba câu chuyện thật, đúng tinh thần "ghi lại mọi lời chê, sửa dần, lặp tới khi không ai chê được nữa":

**1. Thuật toán gợi ý số tiền – sửa 3 lần mới đúng.** Bản đầu làm tròn theo luỹ thừa 10 (0,5 → 5 → 50...), tưởng hợp lý trên giấy. Người dùng thật gõ 14,55 thì bị gợi ý nhảy hẳn sang "10 · 15 · 20" – bước nhảy quá thô ngay tại các mốc chục. Sửa lần 2 vẫn còn kẽ hở ở mốc 10 (9,99 bước 0,5 mà 10,0 nhảy thẳng lên bước 5). Lần 3 mới đúng: chỉ một bậc nhảy duy nhất, tại đúng một mốc. Bài học: **thấy đúng trên giấy không có nghĩa đúng khi người thật gõ số thật** – phải chờ phản hồi rồi sửa, không phải cố đoán đúng ngay từ đầu.

**2. Cỡ icon – chốt sau khi lệch về cả hai phía.** Icon 48px + chữ 17px → người dùng chê "nhỏ quá". Chỉnh lên icon 64px + chữ 30px → chê tiếp "to quá". Chốt ở giữa (56px + 21px) mới vừa. Bài học: phản hồi đầu tiên không phải là điểm chốt, mà là một hướng để dò – đẩy quá tay theo một lời chê dễ tạo ra lời chê ngược lại.

**3. Thông báo nhận tiền đến rất chậm – bug nghiêm trọng hơn vẻ ngoài.** Người dùng báo "thông báo tới rất lâu". Truy ra: hàm tên là "poll" (ngụ ý hỏi lặp lại) nhưng thực chất chỉ gọi đúng một lần lúc mở màn – đứng yên ở một màn thì tiền về cũng không ai hỏi lại. Vì đây là app cho người lớn tuổi xử lý tiền bạc, im lặng ở đúng màn hình tiền là lỗi nặng ngang một crash, không phải lỗi vặt bỏ qua được. Sửa: hỏi lặp lại theo nhịp khác nhau tuỳ màn (đang đứng chờ nhận tiền thì hỏi dày hơn), và hỏi ngay khi người dùng quay lại mở app.

> Cả ba đều bắt đầu từ đúng bước 3 và 4 của Giai đoạn 3: đưa cho người thật dùng, và ghi lại lời chê dù có vẻ nhỏ. Không có bước đó thì cả ba lỗi này vẫn nằm im, "chạy được" trên giấy nhưng sai khi chạm vào người dùng thật.

---

Series tới đây là hết. Có thể sẽ có thêm tập bonus: *1 Prompt Đưa Bạn Từ Ý Tưởng Đến Sản Phẩm Hoàn Chỉnh.*
