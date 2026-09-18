# Bước 4: Vẽ wireframe

Có bản plan chi tiết từ Bước 3 rồi – tới lúc vẽ khung sườn từng màn hình, trước khi code UI thật.

## Vì sao cần bước này

Nhảy vào code luôn thì AI tự bịa layout theo cảm tính của nó. Code xong nhìn không đúng ý lại phải sửa, mà sửa layout tốn token hơn nhiều so với sửa lúc mới là mấy cái khung. Vẽ wireframe trước giúp mình và AI thống nhất layout từ đầu, code một lần là ra.

## Prompt

Copy đoạn dưới, paste vào Claude Chat:

```
Đóng vai Senior Product Designer. Dựa trên spec sản phẩm mình đã đưa ở các bước trước, vẽ wireframe cho từng màn hình, ưu tiên đúng layout/tỷ lệ hơn đẹp, chỉ khung + label chức năng. Hỏi platform và đề xuất hệ lưới phù hợp, chờ xác nhận trước khi vẽ. Chỗ nào spec chưa rõ layout thì hỏi tôi, đừng tự suy diễn. Vẽ theo từng nhóm màn hình, chờ xác nhận rồi mới sang nhóm tiếp.

HỆ LƯỚI VÀ CON SỐ – luật cứng, áp cho mọi màn:
- Chốt 1 khung gốc cố định trước (vd mobile 390×844). Mọi số đo tính trên khung này.
- Lưới nhiều hàng NHIỀU cột: ưu tiên 12 hoặc 15 hàng, 12 hoặc 15 cột. Chia càng mịn càng đặt được nhiều cỡ khối mà vẫn thẳng hàng.
- Khai đủ 4 thứ: số hàng/cột, bề rộng 1 cột + chiều cao 1 hàng, khe giữa hàng/cột, lề. KHÔNG chia đều khung cho N – giữa các hàng có khe.
- Bề rộng cột, chiều cao hàng, khe, mọi khoảng cách, mọi kích thước khối/nút/box: BỘI SỐ CỦA 8 (8, 16, 24, 32, 40, 48...). Khung không chia chẵn thì phần dư dồn hết vào lề (trên/dưới, hai bên) – lề là chỗ DUY NHẤT được phép ra số lẻ, không rải lẻ vào từng hàng.
- Cỡ chữ: BỘI SỐ CỦA 3 (12, 15, 18, 21, 24, 30, 36...). Chốt 1 thang chữ 4-5 bậc dùng cho cả app, màn nào cũng chỉ lấy từ thang đó.
- Nút bấm và mọi vùng chạm cao tối thiểu 48 – đủ cho ngón tay. Hàng lưới thấp hơn 48 thì nút phải trải 2 hàng, hoặc chọn lưới ít hàng hơn.
- Viết ra phép tính: (số cột × bề rộng cột) + (số khe × khe) + 2 × lề = bề rộng khung, và tương tự cho chiều dọc. Phép tính không khớp thì chưa được vẽ.

Mỗi màn liệt kê đủ N hàng, hàng nào trống cũng phải ghi ra là trống – đừng chỉ kể mấy hàng có nội dung.

Chỗ nào hiển thị nội dung thay đổi được (số dư, tên người, ngày giờ, danh sách): hỏi mình giá trị ngắn nhất và dài nhất có thể ra, rồi ghi rõ khi độ dài đổi thì layout xử lý sao – cụm chữ đứng yên tại chỗ hay được phép nhảy.

Màn nào phụ thuộc hệ điều hành hoặc trình duyệt (hướng dẫn cài app vào màn hình chính, xin quyền camera, quyền thông báo) thì vẽ đủ biến thể, đừng vẽ mỗi bản iPhone rồi coi như xong.

Màn nào có dữ liệu hoặc phải chờ thì vẽ đủ trạng thái xấu: đang tải, trống chưa có gì, lỗi/mất mạng, không được cấp quyền.

XONG HẾT CÁC NHÓM MÀN THÌ TỰ ĐỘNG, ĐỪNG ĐỢI MÌNH NHẮC: tổng hợp thành 1 file markdown duy nhất gồm khung gốc + hệ lưới (kèm phép tính) + thang chữ + từng màn liệt kê theo hàng/cột + trạng thái xấu của từng màn – để mình mang sang bước build.

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
- **Số nào cũng phải thuộc một thang, không có số tuỳ hứng.** Chữ theo bội số của 3, khoảng cách và kích thước khối theo bội số của 8. Nghe khắt khe, nhưng chính cái khắt khe đó làm cả app trông "đều": mắt người không đọc ra được 17px hay 19px, nhưng đọc ra được một màn mà khoảng cách chỗ 14 chỗ 18 chỗ 20.

## Hệ lưới mẫu cho mobile

Khung 390×844 (cỡ iPhone phổ thông), lưới **15 cột × 12 hàng**:

| Chiều | Chia | Phép tính | Phần dư |
|---|---|---|---|
| Ngang | 15 cột × 16px, khe 8px | 15×16 + 14×8 = **352** | 390 − 352 = 38 → lề 19 mỗi bên |
| Dọc | 12 hàng × 56px, khe 8px | 12×56 + 11×8 = **760** | 844 − 760 = 84 → trên 48 (thanh trạng thái), dưới 36 (thanh home) |

Cái hay của bộ số này: cột, hàng, khe đều là bội số của 8, nên **khối trải qua bao nhiêu cột/hàng cũng ra bội số của 8** – rộng k cột = 24k − 8 (1 cột 16, 4 cột 88, 8 cột 184, full 352), cao k hàng = 64k − 8 (1 hàng 56, 2 hàng 120, 3 hàng 184). Muốn nút cao 56, card cao 184, không cần nghĩ – đếm hàng là ra.

Vì sao dọc 12 mà không 15: 15 hàng thì 1 hàng chỉ còn 40px, nút cao 1 hàng là nhỏ hơn cỡ ngón tay chạm thoải mái (~48px) – với người lớn tuổi càng khó bấm. 12 hàng cho nút 56px, dư đúng đủ chỗ cho thanh trạng thái và thanh home. Khối vuông (QR, camera): 8 cột × 3 hàng = 184×184 khớp lưới; cần vuông to hơn thì lấy bề rộng theo cột rồi cho cao bằng rộng, chấp nhận mép dưới không chạm vạch hàng.

Thang chữ mẫu, 5 bậc, đều bội số của 3:

| Bậc | Cỡ | Dùng cho |
|---|---|---|
| Số lớn | 36 | Số dư, số tiền chính |
| Tiêu đề | 24 | Tên màn |
| Nội dung | 18 | Chữ trên nút, nội dung chính |
| Phụ | 15 | Mô tả, nhãn |
| Chú thích | 12 | Giờ, ghi chú nhỏ |

Không bắt buộc đúng bộ này – app của bạn có thể cần 15 hàng (màn nhiều nội dung, nút trải 2 hàng), 12 cột, hoặc khe 16. Bắt buộc là **luật**: có khung gốc, có khe, mọi số thuộc thang.

**Máy khác kích thước thì sao?** Code đúng theo px trên khung gốc, rồi lúc chạy thì **phóng/thu nguyên cả khung một lượt** cho vừa màn máy thật (CSS `transform: scale(...)`), chứ không để từng khối tự co giãn riêng. Từng khối tự co giãn là mỗi máy lệch một kiểu, không khớp bản vẽ nữa – TapTip dính đúng chuyện này (xem ví dụ dưới). Cái giá: máy có tỷ lệ khác 390×844 sẽ dư một dải trống ở cạnh, đổi lại mọi máy đều thấy đúng cái mình vẽ.

## Ví dụ: Wireframe TapTip và EZwallet

### TapTip – chạy thật đúng prompt trên

[`KattyFury/taptip`](https://github.com/KattyFury/taptip), bản đầy đủ: [`docs/04-wireframe.md`](https://github.com/KattyFury/taptip/blob/main/docs/04-wireframe.md) (v1) và [`docs/04-wireframe-v2.md`](https://github.com/KattyFury/taptip/blob/main/docs/04-wireframe-v2.md) (v2).

Chốt trước khi vẽ: platform **PWA**, khung 375×812, **chia dọc 10 hàng**. Xong rồi rút ra 2 nguyên tắc áp cho mọi màn – đây mới là thứ giữ cả bộ màn hình đồng nhất, chứ không phải từng màn vẽ đẹp riêng:

- Nội dung chính luôn căn giữa vùng **hàng 1-6**
- Nút hành động luôn nằm ở **hàng 9**: hoặc 1 nút full-width, hoặc cặp "Quay lại" (1/3 trái) + nút chính (2/3 phải)

| Màn | Hàng 1-6 | Hàng 9 | Hàng 10 |
|---|---|---|---|
| Đăng nhập | Input email → 6 ô nhập OTP | Quay lại 1/3 + Tiếp tục 2/3 | trống |
| Thiết lập Passkey | Icon FaceID + mô tả | Quay lại 1/3 + Bật passkey 2/3 | "Bỏ qua, dùng email/OTP" |
| Home | Balance (hàng 1) · QR to (2-5) · chú thích "Cho người khác quét để nhận tip" (6) | Tip ngẫu nhiên 1/3 + Tip 2/3 | Icon menu ☰ |

Home cố tình **không có bottom nav** – mọi thứ phụ đẩy hết vào popup của icon ☰, để hàng 2-5 dành trọn cho QR. App này mở ra là để chìa QR cho người ta quét, không phải để lướt.

Ở v2, chỉ vẽ lại **những màn có đổi thật**, màn nào không nhắc thì giữ bản v1 – đỡ được nguyên một vòng vẽ lại cả bộ. Thêm một quy tắc chung mới cho mọi popup: rộng cố định 3/4 màn, cao tự co theo nội dung, tất cả popup dùng chung một khuôn, không tự vẽ kiểu riêng.

> Chỗ đáng học đầu tiên là con số **"mỗi hàng ~81.2px"** trong bản v1. Nó đúng trên đúng một cái màn hình 812px, và tới lúc code thật thì `h-40`, `mt-10` làm vỡ layout ngay trên máy khác kích thước. Lúc đó cách sửa là chuyển hết sang tỷ lệ – và chính cách sửa đó lại gây ra lỗi ngay dưới đây.
>
> Chỗ đáng học thứ hai tới muộn hơn nhiều. Tháng 9 tác giả tự vẽ lại toàn bộ app trên Figma, và lưới thật trong Figma là **15 hàng, mỗi hàng cách nhau 8px** – không phải "chia đều N hàng". Giữa các hàng có khe hở, nên 1 hàng không bằng 1/N chiều cao màn. Muốn khớp Figma từng pixel, TapTip cuối cùng **khoá cứng khung 390×844 rồi phóng to/thu nhỏ cả khung** theo màn máy thật, thay vì cho từng khối tự co giãn. Xem thêm EZwallet ngay dưới – dính đúng chuyện khe hở này.

### EZwallet – dựng ngược từ quyết định có thật

Dự án thật của tác giả – [`KattyFury/ezwallet`](https://github.com/KattyFury/ezwallet). Không chạy đúng prompt trên (dự án có trước series), nhưng độc lập chốt ra **đúng cùng một hệ lưới 10 hàng** như TapTip v1 – dấu hiệu tốt cho thấy đây không phải luật riêng của một app, mà là cách hợp lý để bố cục màn hình mobile chữ to cho người lớn tuổi.

- Nội dung chính của mỗi màn nằm trong vùng linh hoạt ở giữa
- Nút hành động luôn nằm ở **hàng 9**: một nút rộng 3/4 màn, hoặc cặp nút chia đôi – **hàng 10 chỉ dành riêng cho thanh điều hướng 4 tab chính**, không lẫn với nút hành động của từng màn

| Màn | Nội dung | Hàng 9 | Hàng 10 |
|---|---|---|---|
| Home (Gửi) | Số dư (1-2) · danh sách token (3-5.5) · thông báo (7-8) | 3 action-card: Dán · Quét QR · Danh bạ | Thanh điều hướng 4 tab |
| Swap | 3 khối chia đều: You pay/You receive · thanh trượt % + gợi ý số chẵn | Nút Swap (rộng 3/4 màn, đồng tâm với action-card ở Home) | (đã gộp vào Service Hub, hàng 10 đổi thành chữ "Exit") |
| Màn phụ (Ngôn ngữ, Bảo mật, Giới thiệu...) | Hàng 1 = tiêu đề, nội dung hàng 2 trở xuống | Nút "Quay lại" hoặc cặp Quay lại/Xác nhận | Trống – màn phụ không có thanh điều hướng |

Bốn màn chính (Gửi/Nhận/Lịch sử/Menu) giữ nguyên hàng 10 cho thanh điều hướng xuyên suốt cả app; mọi màn phụ mở ra từ đó thì hàng 10 bỏ trống, nút hành động dồn hết vào hàng 9 – đúng nguyên tắc "nút hành động luôn ở một chỗ cố định" mà bước này dạy, chỉ khác điểm neo cụ thể so với TapTip.

> Chỗ đáng học nhất không phải hệ lưới (đã đúng ngay từ đầu, độc lập với series) mà là hai lỗi layout thật xảy ra SAU khi hệ lưới đã chốt, đúng kiểu lỗi mà bước này cố tránh: (1) một màn quên khai `grid-template-columns: minmax(0,1fr)` cho container – một chuỗi chữ không xuống dòng đủ dài là kéo phình cả cột, lệch nguyên màn hình; (2) một lưới 2 cột ép ô vuông cứng bằng `aspectRatio:1` mà không tính chữ dài tràn ra ngoài trên màn hẹp – bỏ ép vuông, để `gridAutoRows:'1fr'` cho các ô tự cao bằng nhau mới hết tràn. Cả hai đều là lỗi *sau khi có wireframe đúng*, vì wireframe không thể lường trước từng dòng CSS – nhưng "vẽ đủ N hàng, hàng nào cũng phải khai rõ" (luật bước này) là đúng thứ giảm được loại lỗi thứ hai.

> Và một lỗi thứ ba, nằm ngay trong chính hệ lưới "đã đúng từ đầu": code chia màn thành 10 hàng bằng nhau, mỗi hàng 84.4px (844 ÷ 10). Nhưng lưới thật trong Figma có **khe 16px giữa các hàng**, nên 1 hàng thật chỉ cao 70px ((844 − 9×16) ÷ 10). Thiếu đúng cái khe đó mà cả app lệch khoảng 14px suốt nhiều tháng – nhìn bằng mắt không ra, tới lúc đo từng pixel so với Figma mới thấy. TapTip ở trên thì lệch kiểu khác: chiều cao hàng co giãn theo cửa sổ trình duyệt trong khi Figma vẽ trên khung cố định, nên mỗi máy lệch một kiểu. Hai app, hai lỗi khác nhau, cùng một gốc: **"chia đều N hàng" chưa đủ để mô tả một hệ lưới** – phải khai luôn khe giữa các hàng, và khung gốc đang vẽ là bao nhiêu.

## Prompt này từng hụt chỗ nào

Tám chỗ, đều lòi ra lúc đem wireframe đi code thật ở Bước 6 – không chỗ nào nhìn bản vẽ mà thấy được. Chỗ #1-5 từ lần đầu build TapTip, #6-8 từ đợt cả TapTip lẫn EZwallet dựng lại theo Figma (09/2026):

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| 1 | Hệ lưới ra bằng px ("mỗi hàng ~81.2px") tính trên đúng 1 màn 812px, code theo đó là vỡ layout trên màn khác kích thước | Lần sửa đầu: bắt phát biểu bằng tỷ lệ 1/N. **Lần sửa sau (#6, #7) đảo lại cách này**: giữ px trên 1 khung gốc cố định, rồi phóng/thu nguyên khung |
| 2 | Chỉ liệt kê hàng có nội dung, hàng trống bỏ lửng. Lúc code, khối nội dung nuốt luôn phần dư nên tỷ lệ thật lệch hẳn so với lưới đã tính | Bắt liệt kê đủ N hàng, hàng trống cũng phải ghi ra là trống |
| 3 | Không hỏi nội dung động dài ngắn cỡ nào. Balance vẽ mẫu "1.250.000đ", tới lúc số dư đổi thì cả cụm nhảy vị trí, phải quay lại sửa thành ô rộng cố định | Bắt hỏi giá trị ngắn nhất/dài nhất, và ghi rõ độ dài đổi thì layout xử lý sao |
| 4 | Màn "Thêm app vào màn hình chính" vẽ đúng một bản Safari trên iPhone, Android mở lên là hướng dẫn sai hoàn toàn | Bắt vẽ đủ biến thể cho màn phụ thuộc hệ điều hành/trình duyệt |
| 5 | Chỉ vẽ trạng thái đẹp. Thiếu màn lịch sử lúc chưa có giao dịch nào, thiếu màn không được cấp quyền camera | Bắt vẽ đủ trạng thái xấu: đang tải, trống, lỗi/mất mạng, bị từ chối quyền |
| 6 | "Mỗi hàng bằng 1/N chiều cao" bỏ quên khe giữa các hàng. EZwallet chia 844 ÷ 10 = 84.4px/hàng trong khi lưới thật là 70px + khe 16px – cả app lệch ~14px nhiều tháng | Bắt khai đủ 4 thứ: số hàng/cột, kích thước 1 hàng/cột, khe, lề – và viết phép tính cộng lại ra đúng khung |
| 7 | Lưới tỷ lệ co giãn theo cửa sổ trình duyệt, nhưng bản vẽ nằm trên khung cố định – mỗi máy lệch một kiểu, không máy nào khớp bản vẽ. TapTip phải khoá cứng khung 390×844 rồi phóng/thu cả khung | Bắt chốt 1 khung gốc trước khi vẽ; code theo px trên khung đó, phóng/thu nguyên khung khi chạy |
| 8 | Không có thang số, mỗi chỗ một con số tuỳ hứng. TapTip từng có cỡ chữ 32/24/20/16 trong code trong khi Figma là 15/19/23/35, bản vẽ còn có cả cỡ 24 lẫn 23, 20 lẫn 19 – phải ngồi chuẩn hoá lại tay; lề 25px, hàng 48.8px | Chữ theo bội số của 3, khoảng cách và kích thước khối theo bội số của 8, thang chữ 4-5 bậc dùng chung cả app |
| 9 | Prompt không bảo tổng hợp kết quả – vẽ xong nhiều nhóm màn, không có file nào để mang sang Bước 6. Lòi ra khi đi thử cả series như một người mới | Thêm bước cuối tự động: 1 file gồm khung, lưới kèm phép tính, thang chữ, từng màn theo hàng/cột |
| 10 | Chạy khô bộ lưới mẫu 15 hàng trên khung 844: mỗi hàng chỉ còn 40px, nút 1 hàng nhỏ hơn cỡ ngón tay chạm thoải mái | Thêm luật vùng chạm tối thiểu 48; lưới mẫu đổi sang 12 hàng × 56px |
| 11 | Đọc lại bản sửa: luật vừa bắt lề là bội số của 8, vừa bảo phần dư dồn vào lề – khung 390 hay 844 thì phần dư gần như không bao giờ chia hết cho 8, AI sẽ kẹt giữa hai luật | Lề là chỗ duy nhất được phép lẻ, mọi thứ bên trong lưới vẫn bội số của 8 |

Xong bước này mới qua Bước 5, setup môi trường để bắt đầu code.
