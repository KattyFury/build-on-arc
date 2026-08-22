# Bước 3: Plan chi tiết trước khi code

Có 6 câu mô tả sản phẩm từ Bước 2 rồi. Bước này đưa chúng cho AI bóc tách từng gạch đầu dòng, tìm ra những chỗ còn thiếu – trước khi viết dòng code đầu tiên.

Bước này đi 2 vòng, cùng một cửa sổ Chat: **vòng 1 chốt sản phẩm chạy ra sao**, **vòng 2 chốt mỗi luồng chạy bằng tech gì**. Vòng 2 hay bị bỏ qua nhất, mà bỏ nó thì stack của app là stack AI tự chọn hộ.

## Vì sao cần bước này

Đừng quăng một cái idea sơ sài rồi bảo AI tự chạy. Token hết nhanh khủng khiếp, mà thứ ra đời là dự án của AI chứ chẳng phải của mình. Ngồi plan kỹ trước được 4 cái:

1. **Làm chủ dự án mình build**, thay vì để AI tự biên tự diễn.
2. **Tiết kiệm token**, vì AI biết chính xác phải làm gì, không làm dư mấy tính năng vớ vẩn.
3. **Bịt trước những chỗ AI phải đoán.** AI có xu hướng tự điền vào chỗ còn thiếu. Mình không nói rõ thì nó đoán, đoán sai thì lại tốn token bảo nó sửa đi sửa lại.
4. **Chính lúc ngồi plan mới thấy được chỗ cần làm rõ trong logic.** Build sản phẩm không phải nghề của tụi mình nên nhiều khía cạnh chưa nghĩ tới. Đừng lo, AI sẽ gánh chỗ này.

## Plan chi tiết là như thế nào

Không phải viết một bài văn dài dòng. Là ngồi **trả lời phỏng vấn**: đưa AI mấy gạch đầu dòng mô tả sản phẩm ở Bước 2, bắt nó đóng vai người tư vấn và hỏi ngược lại mình.

Mấu chốt nằm ở câu cuối của prompt: **hỏi một nhóm mỗi lần, chờ trả lời xong mới sang nhóm tiếp**. Bỏ câu đó ra thì AI xổ 30 câu hỏi một lượt, đọc xong không trả lời tử tế được câu nào.

## Vòng 1: prompt phỏng vấn ngược

Copy đoạn dưới, paste vào AI bạn đang dùng:

```
Đóng vai một Senior Product Consultant. Đừng giải pháp ngay. Hãy review ý tưởng của tôi như một buổi Product Discovery, chia thành các nhóm logic và hỏi 3–5 câu hỏi thực tế cho từng nhóm về UX, logic hệ thống, xử lý lỗi, edge cases và bảo mật. Chỉ hỏi một nhóm mỗi lần và đợi tôi trả lời trước khi sang nhóm tiếp theo.

Sau mỗi nhóm tôi trả lời xong, trước khi sang nhóm tiếp: liệt kê lại đúng những câu trong nhóm tôi CHƯA trả lời (im lặng không có nghĩa là pass hay không cần quan tâm), hỏi lại riêng mấy câu đó.

Khi câu trả lời của tôi là "để bên thứ ba lo" (vd nhà cung cấp ví, nhà cung cấp hạ tầng): chỉ chấp nhận nếu câu hỏi gốc là về ĐỘ AN TOÀN của bên thứ ba đó. Nếu câu hỏi gốc là app xử lý tình huống X ra sao, không được để tôi đẩy hết trách nhiệm qua bên thứ ba – hỏi lại.

Khi tôi trả lời "chấp nhận rủi ro, không cần xử lý" cho một câu về bảo mật/rủi ro: đây là câu trả lời hợp lệ và đủ, đừng cố thuyết phục tôi đổi ý – chỉ cần đảm bảo tôi đã THẤY rõ rủi ro trước khi chấp nhận.

Cuối mỗi nhóm, nếu phát hiện 2 quyết định riêng lẻ tôi vừa chấp nhận (mỗi cái nghe hợp lý một mình) khi cộng lại tạo ra rủi ro lớn hơn tổng từng phần, phải chỉ rõ ra sự kết hợp đó ngay, đừng chỉ đánh giá từng quyết định độc lập.

Đây là những gạch đầu dòng mô tả sơ về dự án của mình:
```

Dán 6 câu ở Bước 2 vào ngay sau dòng cuối, rồi gửi.

Sau khi xong hết các nhóm, chủ động hỏi Chat: "Tổng hợp toàn bộ quyết định ở đây thành 1 file duy nhất giúp mình" – bước này hay bị quên vì Chat không tự nhắc, mà không có file thì hỏi đáp biến mất khi đóng tab.

> Dán kèm nếu bạn đang mở cửa sổ chat mới. Nếu dùng chung 1 cửa sổ chat xuyên suốt từ đầu thì bỏ qua – Chat đã có sẵn context, dán lại là thừa.

### Trả lời phỏng vấn sao cho ăn tiền

- **Chốt hẳn, đừng để mở.** "Cái đó tính sau" nghĩa là tới lúc code AI vẫn phải đoán – đúng cái mình đang muốn tránh.
- **Chưa biết thì nói chưa biết**, bảo AI đưa 2-3 phương án kèm đánh đổi rồi tự chọn. Chọn là việc của mình, liệt kê là việc của nó.
- **Câu nào đụng tiền hoặc bảo mật thì đừng để AI chọn giúp.** Nó chọn phương án phổ biến nhất, không phải phương án đúng với sản phẩm của mình.
- **Ghi kết quả ra file.** Hỏi đáp nằm trong cửa sổ chat là thứ sẽ biến mất. Cuối buổi bảo AI tổng hợp toàn bộ quyết định thành một file, để đó cho các bước sau dùng lại.

## Vòng 2: chốt stack cho từng luồng

Xong vòng trên là biết app có những luồng nào, mỗi luồng xử lý ra sao. Còn thiếu đúng một câu: **mỗi luồng đó chạy bằng cái gì.**

Chỗ này gần như ai cũng bỏ qua. Mở Claude Code lên, gõ "build cho mình app tip trên Arc", AI tự chọn framework, tự chọn database, tự chọn thư viện – cài xong mình mới biết mình đang xài cái gì. Nó không chọn bậy đâu, nó chọn thứ nó **quen tay nhất**, tức là thứ phổ biến nhất trên internet. Hai thứ đó không phải lúc nào cũng trùng nhau, mà lúc lòi ra lệch thì đã code cả tuần trên cái stack đó rồi.

Cách chặn: bắt nó khai ra trước khi gõ dòng code đầu tiên. Đúng ba câu, hỏi cho từng luồng một:

1. **Luồng này chạy bằng tech gì?**
2. **Vì sao chọn cái đó?**
3. **Còn những thứ nào khác cũng làm được việc này, và vì sao không dùng chúng?**

Câu 3 mới là câu ăn tiền. Câu 1 với câu 2 thì AI nào cũng trả lời trơn tru – nó luôn có sẵn một lý do nghe rất hợp lý cho thứ nó vừa chọn. Câu 3 bắt nó bày ra cái nó **đã loại**, đọc chỗ đó mới thấy: có thứ bị loại vì lý do không đúng với mình (loại vì "khó cho người mới" trong khi mình có tự code đâu), có thứ bị loại vì nó không biết, và có khi thứ nó loại lại đúng là thứ mình cần.

Hỏi một lần được thêm hai cái nữa:

- **Mình hiểu app mình gồm những mảnh gì.** Sau này hỏng chỗ nào còn biết đường mở đúng chỗ đó ra hỏi, thay vì quăng nguyên repo cho AI đọc lại từ đầu.
- **Biết chỗ nào khó đổi.** Đổi màu nút thì lúc nào đổi cũng được. Đổi database hay đổi nhà cung cấp ví sau khi đã có người dùng thật thì gần như làm lại từ đầu. Chốt sớm được đúng mấy chỗ khó đổi là đủ nguyên bước này có lời.

### Prompt

Copy đoạn dưới, dán vào Chat – tốt nhất là cùng cửa sổ vừa chạy vòng 1:

```
Đóng vai Solution Architect. Mình vừa chốt xong logic sản phẩm, giờ cần chốt stack.

Cách làm việc: bạn dẫn, mình theo.

BƯỚC 0 – trước khi bàn tech: đọc plan của mình rồi liệt kê ra danh sách các luồng bạn thấy, theo thứ tự người dùng gặp chúng. Đợi mình chốt hoặc bổ sung xong mới đi tiếp. Đừng tự đi thẳng vào luồng đầu tiên.

BƯỚC 1 – chốt phần KHUNG DÙNG CHUNG trước: app chạy bằng gì, host ở đâu, dữ liệu người dùng lưu ở đâu. Mấy thứ này không thuộc luồng nào nhưng luồng nào cũng dính, và sau này đổi là đau nhất – nên soi riêng, đừng để nó lọt vào giữa lúc đang bàn luồng đầu tiên.

BƯỚC 2 – đi TỪNG LUỒNG một, hỏi xong luồng này đợi mình chốt rồi mới sang luồng sau. Đừng xổ hết một lượt.

Ràng buộc của mình, tính vào mọi lựa chọn chứ đừng bỏ qua:
- Mình không có nền lập trình, code là AI viết. Cái gì cần tự debug sâu bằng tay thì coi như mình không làm được.
- Chain: [Arc testnet / điền chain của bạn]. Giai đoạn: [chạy testnet trước / lên mainnet luôn].
- Ngân sách: [đang test/demo trên testnet thì mặc định free tier, khỏi hỏi câu này / lên production thật rồi thì free tier thôi hay mình trả được X$ một tháng].
- Mình làm một mình, không có team.

Với khung chung và với MỖI luồng, trả lời đủ 4 phần:
1. Tech chọn. Ghi tên gói/dịch vụ cụ thể, không nói chung chung kiểu "một database".
2. Vì sao chọn nó. Lý do phải gắn với ĐÚNG chỗ này và ràng buộc của mình ở trên. Không nhận lý do kiểu "phổ biến", "chuẩn ngành", "cộng đồng lớn".
3. Ít nhất 2 thứ khác cũng làm được việc này, kèm lý do loại từng cái. Loại vì gì thì nói thẳng cái đó, đừng bịa phương án dở tệ ra cho có. Nếu thật sự chỉ có 1 lựa chọn khả dụng, hoặc chỗ này không cần tech gì (chỉ là một cái link, một màn hình tĩnh), thì nói thẳng như vậy – đừng nặn cho đủ số.
4. Quyết định này về sau đổi dễ hay khó: đổi lúc nào cũng được, hay đổi là phải làm lại phần lớn? Khó đổi thì nói rõ khó ở chỗ nào.

Mình có quyền nói "luồng này bản đầu chưa làm". Nghe vậy thì ghi lại là CHƯA CHỌN rồi đi tiếp – đừng chọn sẵn tech cho thứ mình chưa định làm.

Bốn việc bắt buộc làm trong lúc đi:
- Có sample app hoặc template chính chủ nào bao được NHIỀU luồng cùng lúc không? Có thì đặt thẳng lên bàn cân: fork nguyên nó vs tự ghép từng mảnh – kèm link, và kèm cái mình MẤT khi fork (kéo theo cả đống thư viện không dùng tới, dính cấu trúc của người ta, phải đọc code lạ). Đừng chỉ gợi ý mảnh lẻ cho từng luồng.
- Cái nào tốn tiền thì nói rõ: free tới mức nào, quá mức đó thì bao nhiêu, có bắt gắn thẻ ngay không.
- Cái nào KHÔNG chạy được trên chain mình chọn, hoặc chạy được nhưng thiếu tính năng, phải cảnh báo ngay lúc đề xuất – đừng để mình cài xong mới biết.
- Cái nào đòi điều kiện môi trường mới chạy được – bắt buộc HTTPS, phải khai báo trước domain trên console của nhà cung cấp, phải xin quyền thiết bị (camera, thông báo), không chạy được trên localhost – nói ngay lúc đề xuất, kèm chỗ phải vào khai báo.

Đi hết rồi thì tổng hợp thành một file duy nhất: bảng stack theo luồng, danh sách thứ cần cài, thứ cần đăng ký tài khoản, mục những chỗ phải khai báo/cấu hình trước khi chạy được, và mục riêng liệt kê các quyết định khó đổi.

Đây là plan sản phẩm của mình:
```

> Dán kèm nếu bạn đang mở cửa sổ chat mới. Nếu dùng chung 1 cửa sổ chat xuyên suốt từ đầu thì bỏ qua – Chat đã có sẵn context, dán lại là thừa.

### Đọc câu trả lời sao cho ăn tiền

Năm dấu hiệu thấy là hỏi lại ngay:

| Thấy gì | Nghĩa là | Hỏi lại |
|---|---|---|
| Mấy phương án bị loại toàn thứ dở thấy rõ | Nó dựng bù nhìn cho cái nó đã chọn sẵn | "Kể 2 thứ người ta thật sự đang dùng cho việc này, rồi hẵng loại" |
| Lý do chọn là "phổ biến", "chuẩn ngành", "cộng đồng lớn" | Chưa xét gì tới app của mình | "Lý do đó đúng với luồng nào của mình? Nói theo luồng cụ thể" |
| Một luồng gọi tên tận 4-5 thư viện | Đang gom đồ nghề quen tay | "Bỏ bớt cái nào mà luồng vẫn chạy được?" |
| Không thứ nào bị đánh dấu là khó đổi | Nó chưa nghĩ tới chuyện phải đổi | "3 tháng nữa có người dùng thật, đổi cái nào là phải làm lại?" |
| Luồng nào cũng đúng 2 phương án thay thế, đều tăm tắp | Đang nặn cho đủ số chứ không cân thật | "Luồng nào thật ra chỉ có 1 lựa chọn? Nói thẳng đi" |

Còn một câu đáng hỏi cuối buổi, không nhét vào prompt vì tuỳ người: **"Nếu bạn là người phải bảo trì app này một mình trong 1 năm, bạn có chọn y hệt không?"** Câu này hay lòi ra chỗ nó chọn cho nhanh chứ không chọn cho bền.

> Chốt stack không phải là khoá cứng vĩnh viễn. Nó có nghĩa từ đây trở đi, đổi stack là **quyết định của mình** và có ghi lý do – chứ không phải AI lẳng lặng đổi giữa chừng, mình biết sau cùng.

File tổng hợp của vòng này để cạnh file vòng 1. Bước 5 sẽ mở đúng nó ra để biết phải cài gì.

## Ví dụ: Product Discovery của TapTip

Đây là kết quả chạy thật prompt trên. Bản đầy đủ: [`example/docs/03-planning.md`](../example/docs/03-planning.md).

Chia làm 5 nhóm, mỗi nhóm 3-4 quyết định:

| Nhóm | Quyết định đáng chú ý |
|---|---|
| Login & Onboarding | Khôi phục qua email OTP, không phải cơ chế passkey theo thiết bị – chấp nhận rủi ro vì tiền tip nhỏ |
| Ví & Nạp/Rút | Testnet: nạp/rút = faucet only, rút bị disable |
| Luồng gửi/quét QR | QR người nhận là QR tĩnh, không đổi, không hết hạn – giống số tài khoản |
| Xử lý lỗi & Edge case | Balance không đủ: nút vượt quá balance bị disable từ đầu, không để quét xong mới báo lỗi |
| Bảo mật | Bảo mật lưu key của Circle Wallets là trách nhiệm của Circle, không phải app tự thêm lớp bảo vệ |

> Chỗ đáng học nhất là ở nhóm Bảo mật: hai quyết định riêng lẻ đều nghe hợp lý – "không cần xác thực thêm khi gửi" (để giữ tốc độ) và "không giới hạn số tiền mỗi lần gửi" – nhưng cộng lại nghĩa là ai cầm được điện thoại đã mở khoá thì rút sạch ví không cần thêm bước nào. Đây là trade-off được **nhìn thấy và chấp nhận có chủ đích**, không phải bị bỏ sót.

### Stack TapTip chốt ra sao

Đây là stack thật của [`example/app`](../example/app), chốt xong trước khi vòng 2 được viết thành prompt – nên đọc ngược lại thì thấy đúng 4 phần mà prompt đang bắt trả lời:

| Chỗ | Chọn gì | Vì sao | Loại cái gì, vì sao | Đổi sau này |
|---|---|---|---|---|
| Khung chung | Fork [`circlefin/arc-p2p-payments`](https://github.com/circlefin/arc-p2p-payments) (Next.js + Supabase) | Sample app chính chủ đã có sẵn passkey + gasless P2P, đúng thứ Bước 2-3 chốt | Tự dựng trên Cloudflare Workers/Pages – stack quen tay của tác giả ở dự án khác, nhưng dựng lại từ đầu đúng thứ người ta cho không | Khó |
| Dữ liệu người dùng | Giữ Supabase của app mẫu | Auth + bảng dữ liệu + realtime nằm sẵn trong đó | Đổi sang Cloudflare KV: phải viết lại auth + data layer + realtime, tức là vứt gần hết giá trị của việc fork | Khó |
| Ví + ký giao dịch | Circle Modular Wallets (passkey, `paymaster: true` để app trả gas) | Ví ẩn sau passkey, người 60 tuổi không phải biết ví là gì | Ví tự sinh lưu trong máy: mất máy là mất tiền | Khó – đổi là người dùng mất ví |
| Quét QR | `html5-qrcode` | Chạy thẳng trong trình duyệt, có sẵn đường lùi "nhập ảnh từ kho ảnh" khi không có quyền camera | – | Dễ, đổi thư viện khác lúc nào cũng được |
| Quy đổi VNĐ | **Chưa chọn** | Có trong PRD nhưng bản đầu hoãn: cần tỷ giá thật, không hardcode | – | – |

Hai dòng cuối mới là chỗ đáng học. Một cái **dễ đổi** nên không cần cân lâu. Một cái được quyền trả lời **"bản đầu chưa làm"** – không chọn tech cho thứ chưa định làm, đỡ được một dependency thừa.

> **Fork rẻ hơn tự dựng, nhưng không free.** Đo ngay trong repo: `example/app/package.json` vẫn kéo theo `openai`, `pdf-parse`, `mammoth`, `millify`, và cả `viem` lẫn `web3` – không file nào trong `app/`, `components/`, `lib/` import chúng. Chưa kể 2 lỗi có sẵn của app mẫu phải tự vá: một file client bị `import` nhưng không tồn tại trong repo gốc, và một lỗi type ở route webhook. Fork là nhận cả đồ thừa lẫn nợ của người ta – biết trước thì đỡ hoảng, nên prompt bắt AI nói luôn cái mất chứ không chỉ khoe cái được.

*(Prompt vòng 2 viết sau khi TapTip đã chốt stack, nên nó được kiểm bằng cách chạy lại với chính spec TapTip, và sau đó với một ý tưởng khác đang thử thật trên testnet – tổng 7 chỗ hụt tìm ra ở hai lượt đó đã sửa vào prompt, xem bảng dưới.)*

## Prompt này từng hụt chỗ nào

### Vòng 1 – 5 chỗ, tìm ra lúc chạy thật với TapTip

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| 1 | Trả lời "để bên thứ ba lo" được chấp nhận cả khi câu hỏi là "app xử lý lỗi ra sao" – né tránh trách nhiệm thay vì trả lời đúng phạm vi | Chỉ chấp nhận đẩy qua bên thứ ba nếu câu hỏi gốc là về độ an toàn của bên đó |
| 2 | Trả lời đúng 1 câu trong nhóm 4-5 câu rồi dừng, coi cả nhóm đã xong | Bắt liệt kê lại câu chưa trả lời trước khi qua nhóm tiếp – im lặng không phải là pass |
| 3 | Hai quyết định riêng lẻ hợp lý cộng lại thành rủi ro lớn hơn, không ai chỉ ra | Bắt chỉ rõ tổ hợp rủi ro cuối mỗi nhóm, không chỉ đánh giá từng quyết định độc lập |
| 4 | AI có xu hướng thuyết phục đổi ý khi user nói "chấp nhận rủi ro, không care" | Ghi rõ đây là câu trả lời hợp lệ và đủ – việc của AI là đảm bảo user *thấy* rủi ro, không phải ép tránh rủi ro |
| 5 | Xong nhiều nhóm rồi không ai chủ động tổng hợp thành file, hỏi đáp nằm rải trong chat | Thêm bước cuối: chủ động hỏi Chat tổng hợp thành 1 file duy nhất |

### Vòng 2 – 7 chỗ, tìm ra lúc chạy khô và lúc thử thật

| # | Hụt gì | Sửa thế nào |
|---|---|---|
| 1 | Bảo "đi từng luồng một" nhưng không bắt chốt danh sách luồng trước. Chạy khô: AI tự gom "đăng nhập + tạo ví" làm một luồng và bỏ luôn luồng quy đổi VNĐ có trong PRD | Thêm BƯỚC 0: liệt kê luồng, đợi mình chốt/bổ sung rồi mới bàn tech |
| 2 | Khung dùng chung (app chạy bằng gì, host ở đâu, data để đâu) không thuộc luồng nào, nên bị quyết lén trong lúc bàn luồng đầu tiên – mấy luồng sau mặc nhiên kế thừa. Đúng loại quyết định khó đổi nhất lại là loại duy nhất không bị soi | Thêm BƯỚC 1: chốt khung chung riêng, cũng đủ 4 phần như một luồng |
| 3 | Hỏi "luồng nào có sample app dùng lại được" tức là hỏi theo từng luồng → chỉ ra được mảnh lẻ, không bao giờ ra được "fork nguyên app mẫu" (đúng thứ TapTip đã làm) | Hỏi thẳng: có sample app nào bao được NHIỀU luồng cùng lúc không, rồi đặt lên bàn cân fork nguyên vs tự ghép – kèm cái mình MẤT khi fork |
| 4 | Ép đủ 2 phương án thay thế cho mọi luồng đẻ ra rác. Luồng Nạp/rút trên testnet chỉ là một link tới Circle Faucet, không có tech nào để chọn, AI vẫn nặn ra "tự build faucet riêng" | Cho phép nói thẳng "chỉ có 1 lựa chọn" hoặc "chỗ này không cần tech gì" |
| 5 | Không có chỗ đánh dấu "bản đầu chưa làm". Quy đổi VNĐ nằm trong PRD nhưng TapTip cố ý hoãn – prompt không cho nói vậy nên AI vẫn chọn sẵn nguồn tỷ giá | Cho phép trả lời "luồng này bản đầu chưa làm" → ghi CHƯA CHỌN, không chọn tech |
| 6 | Hỏi tiền, hỏi chain, quên môi trường chạy: cái nào đòi HTTPS, đòi khai báo domain trước, đòi quyền thiết bị. Đây đúng là chỗ ngốn thời gian nhất lúc TapTip build thật (Passkey Domain Config trên Circle Console là mục riêng, khác Allowed Domain của Client Key) | Thêm việc bắt buộc thứ tư: cảnh báo điều kiện môi trường ngay lúc đề xuất, kèm chỗ phải vào khai báo. Ràng buộc thêm dòng giai đoạn testnet/mainnet |
| 7 | Ngân sách hỏi cứng cho mọi dự án, kể cả lúc đã nói rõ đây là demo/hackathon chạy trên testnet – câu hỏi vô nghĩa, chẳng ai cân đo chi phí hạ tầng lúc đó | Đổi câu ngân sách thành có điều kiện: bỏ qua nếu đang ở giai đoạn testnet/demo, chỉ hỏi khi tính lên production |

Xong bước này mới qua Bước 4, vẽ wireframe để chốt mỗi màn hình trông ra sao trước khi cho AI code.
