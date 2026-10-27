# LỬA TRẠI CUỐI CÙNG — KẾ HOẠCH THỰC HIỆN

Phiên bản kế hoạch: 1.0 • Ngày: 27/10/2026 • Trạng thái: thiết kế đề xuất, chưa triển khai game.

Tài liệu này là đặc tả sản phẩm, thiết kế gameplay, kiến trúc kỹ thuật, kế hoạch nội dung, kiểm thử và phát hành cho một game nhập vai rảnh tay offline. Các con số cân bằng, thời gian phát triển và mục tiêu người chơi là giả thuyết để kiểm chứng, không phải kết quả đã đo.

## 1. Quyết định nền tảng và phạm vi

| Hạng mục | Phương án mặc định để bắt đầu |
|---|---|
| Tên làm việc | Lửa Trại Cuối Cùng; kiểm tra trùng tên trước khi công bố |
| Thể loại | RPG 2D tự động chiến đấu, thu thập trang bị, xây trại |
| Nền tảng đầu tiên | Android, màn hình dọc; bản Windows phục vụ phát triển và thử nghiệm |
| Công nghệ | Godot 4 bản stable, GDScript; khóa phiên bản engine và export templates ngay đầu dự án |
| Phong cách | Fantasy u tối nhưng có cảm giác ấm áp ở trại; nhân vật cách điệu, dễ đọc trên điện thoại |
| Kết nối | Toàn bộ vòng chơi chính hoạt động ở chế độ máy bay, kể cả lần chạy đầu sau cài đặt |
| Dữ liệu | Một hồ sơ chơi chính trên máy, hai bản lưu luân phiên, xuất/nhập bản sao lưu thủ công |
| Ngôn ngữ | Tiếng Việt trước; chuỗi giao diện tách sẵn để dịch sau |
| Đối tượng sử dụng | Người thích cày trang bị, tối ưu chỉ số và chơi các phiên ngắn |
| Mô hình ban đầu | APK beta miễn phí; mô hình thương mại quyết định sau khi thử nghiệm vòng chơi |
| Nhân sự tính lịch | Một lập trình viên quen Godot, 35 giờ/tuần; dùng asset sẵn hoặc hỗ trợ mỹ thuật giới hạn |

Đây là kế hoạch cho một game mới. Không phụ thuộc vào mã nguồn hoặc dữ liệu của game cũ. Nếu đổi sang web hoặc iOS, cần điều chỉnh kiến trúc lưu trữ, xuất bản và lịch thử thiết bị trước khi bắt đầu lập trình.

Godot hỗ trợ xuất Android, lưu dữ liệu trong `user://` và sử dụng giấy phép MIT. Các khả năng này đã được đối chiếu tài liệu chính thức; việc lựa chọn Godot là đánh giá thiết kế cho dự án này. Xem [xuất Android](https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_android.html), [đường dẫn dữ liệu](https://docs.godotengine.org/en/stable/tutorials/io/data_paths.html) và [giấy phép](https://godotengine.org/license/).

## 2. Lời hứa với người chơi và giới hạn thiết kế

“Mỗi chuyến đi giúp tôi mạnh hơn; mỗi món đồ đáng chú ý cho tôi một cách đánh mới; mỗi lần trở về khiến ngôi trại thay đổi.”

Bốn trụ cột:

1. **Tiến bộ nhìn thấy được:** chỉ số tăng, hiệu ứng chiến đấu thay đổi, công trình có hình dáng mới.
2. **Quyết định ít nhưng có giá trị:** chọn vùng farm, đổi kỹ năng, thay món đồ, ưu tiên công trình.
3. **Rảnh tay có chủ đích:** người chơi chuẩn bị trước; tự động chiến đấu thực hiện chiến thuật đã đặt.
4. **Tôn trọng việc nghỉ chơi:** không phạt mất chuỗi đăng nhập, không mất trang bị khi chết, kho chiến lợi phẩm không hết hạn.

Không đưa vào bản 1.0: PvP, giao dịch giữa người chơi, guild, máy chủ, thế giới mở, điều khiển di chuyển tự do, gacha trả phí, quảng cáo bắt buộc, năng lượng chặn chơi, tái sinh xóa tiến trình, chế tạo đồ với hàng chục loại nguyên liệu.

Không dùng “lực chiến” làm điều kiện khóa boss. Có thể hiển thị mức thử thách tham khảo, nhưng người chơi được thắng bằng cách phối hợp hiệu ứng.

## 3. Phạm vi theo mốc

| Hạng mục | Prototype | Bản chơi thử hoàn chỉnh một đoạn | Bản 1.0 |
|---|---:|---:|---:|
| Nhân vật chính | 1 | 1 | 1 |
| Hướng xây dựng | 1 | 2 | 3 |
| Kỹ năng chủ động | 2 | 4 | 9, mỗi hướng 3 |
| Nội tại theo hướng | 1 | 3 | 9, mỗi hướng 3 |
| Vùng / chặng | 1 / 3 | 1 / 10 | 3 / 30 |
| Boss | 1 | 2 | 6 |
| Mẫu trang bị gốc | 6 | 12 | 30, gồm 21 thường và 9 huyền thoại |
| Đồng hành | 0 | 1 | 3, mang theo 1 |
| Công trình | 1 | 2 | 4, mỗi công trình 5 cấp |
| Mô phỏng khi đóng game | Thử nghiệm | Đầy đủ luồng cơ bản | Đầy đủ và kiểm thử lỗi |
| Hình ảnh | Khối màu | Asset tạm nhất quán | Mỹ thuật hoàn thiện trong phạm vi |

Mục tiêu nội dung 1.0: có kết thúc cốt truyện ngắn và hoạt động farm sau kết thúc. Dự kiến 6–10 giờ thao tác chủ động, trải qua khoảng 1–3 tuần với người chơi phiên ngắn; phải đo lại bằng playtest. Không kéo dài nội dung bằng thời gian chờ bắt buộc.

## 4. Vòng chơi và nhịp mở khóa

Vòng ngắn: chọn chặng → tự đánh → nhận vật phẩm → so sánh trang bị → nâng một yếu tố → thử chặng khó hơn.

Vòng trung: tìm món đồ tạo tương tác → đổi kỹ năng hoặc đồng hành → vượt boss → mở vùng và công trình.

Vòng dài: hoàn thiện cách xây nhân vật → phục hồi trại → giải cứu đồng hành → đánh boss cuối → tối ưu các tuyến farm và bộ sưu tập.

| Thời điểm mục tiêu | Trải nghiệm cần đạt |
|---|---|
| 0–1 phút | Vào trận đầu, nhận biết nhân vật đang làm gì; không yêu cầu tài khoản |
| 1–3 phút | Có món đồ đầu, thấy chỉ số và hình ảnh thay đổi khi trang bị |
| 3–7 phút | Chọn kỹ năng đầu; gặp một kẻ địch buộc người chơi chú ý đến cách đánh |
| 7–15 phút | Mở lò rèn, chọn tuyến farm đầu tiên, thấy dự báo phần thưởng khi rời game |
| 15–30 phút | Thử boss đầu; hiểu nguyên nhân thua hoặc thắng |
| Phiên quay lại đầu | Nhận báo cáo, đủ tài nguyên cho ít nhất một nâng cấp có ý nghĩa |
| Sau boss thứ hai | Chọn đồng hành; mở vùng hai và thêm chế độ farm |
| Sau boss thứ tư | Mở đủ ba hướng và ba đồng hành; bắt đầu phối hợp sâu hơn |

Các mốc là mục tiêu trải nghiệm. Nếu người thử mắc kẹt ở phần hướng dẫn, sửa giao diện hoặc nhịp phần thưởng trước khi thêm tính năng.

## 5. Nhân vật, chỉ số và công thức ban đầu

Nhân vật cấp 1 có HP 350, ATK 25, DEF 8, tốc độ 0,8 đòn/giây, chí mạng 10%, sát thương chí mạng 150%. Mỗi cấp cộng 35 HP, 4 ATK và 2 DEF. Cấp tối đa 1.0 là 30.

Sáu nhóm chỉ số trên giao diện: sinh lực, công kích, phòng ngự, tốc độ, chí mạng, hồi phục. Bảng chi tiết mở thêm hút máu, sức mạnh khiên, sát thương độc và giảm hồi chiêu. “Hồi phục” là nhóm chỉ số; hồi máu theo giây và hút máu vẫn được tính riêng.

```text
XP cần từ cấp L lên L+1 = 40 + 15*L + 2*L²
Chỉ số cuối = (chỉ số theo cấp + tổng cộng thẳng) * (1 + tổng % tăng)
Giảm sát thương do giáp = min(0,75; DEF / (DEF + 100 + 10*cấp bên tấn công))
Sát thương thô = ATK * hệ số kỹ năng * (1 + % sát thương phù hợp)
Sát thương sau chí mạng = sát thương thô * hệ số crit nếu lần đánh có crit
Sát thương sau giáp = làm tròn(sát thương sau chí mạng * (1 - giảm sát thương))
```

Sát thương dương tối thiểu là 1. Các hiệu ứng “tăng sát thương nhận” được áp dụng một lần sau giáp, có giới hạn dữ liệu riêng. Các nguồn giảm sát thương khác nhân lần lượt với phần sát thương còn lại sau giáp; tổng mức giảm tối đa 85%. Tốc độ tối đa 2,2 đòn/giây; tỷ lệ crit tối đa 75%; hệ số crit tối đa 300%; hút máu tối đa 15%; giảm hồi chiêu tối đa 40%; tổng khiên tối đa 50% HP tối đa.

Thứ tự xử lý một đòn: kiểm tra mục tiêu → tính sát thương → trừ khiên → trừ HP → hút máu trên HP thực sự bị mất → xử lý sự kiện sau đòn → kiểm tra chết → cấp phần thưởng. Phản đòn và độc không kích hoạt hút máu hoặc phản đòn khác. Mục tiêu đã chết không nhận thêm lượt đánh trong cùng thời điểm.

Thời gian nội bộ dùng mili giây nguyên; sự kiện cùng thời điểm có thứ tự ổn định theo loại sự kiện rồi ID thực thể. RNG phải có seed và lưu được trạng thái để phát lại lỗi.

Chưa coi công thức này là cân bằng cuối. Mỗi thay đổi phải ghi phiên bản balance và được so với các cấu hình chuẩn.

## 6. Ba hướng xây nhân vật và đồng hành

Một nhân vật có thể đổi hướng ở trại miễn phí. Không chia thành ba nhân vật phải cày lại. Mang 3 kỹ năng chủ động, 2 nội tại và 1 đồng hành; kỹ năng khác hướng chỉ mở sau khi đã mở khóa hướng tương ứng. Chiến đấu tự động không có nút gây thêm sát thương bằng chạm liên tục.

| Hướng | Ba kỹ năng | Ba nội tại | Điểm mạnh và giới hạn |
|---|---|---|---|
| Cuồng chiến | Chém liên hoàn; Cuồng nộ; Hồi huyết | Hút máu; Cuồng chiến dưới 40% HP; Chuỗi đòn | Dọn quái nhanh; phải giải bài toán sống sót trước đòn mạnh |
| Hộ vệ | Khiên sắt; Khiêu chiến; Phản kích | Giáp bền; Khiên nổ; Kiên định | Chịu đòn tốt; cần nguồn sát thương để thắng trong giới hạn trận |
| Độc sư | Phi tiêu độc; Bào mòn; Bùng độc | Tích độc; Lây độc; Săn kẻ suy yếu | Đánh lâu và xử lý nhóm; cần bảo vệ khi chưa tích đủ độc |

Chỉ số khởi tạo: Chém liên hoàn gây 2 lần 80% ATK, hồi 6 giây; Khiên sắt tạo khiên 20% HP trong 5 giây, hồi 12 giây; Phi tiêu độc gây 80% ATK và thêm một tầng độc, hồi 5 giây. Các kỹ năng còn lại phải có dữ liệu hệ số, thời lượng, hồi chiêu, điều kiện mục tiêu và mô tả trước khi vào sprint nội dung.

Độc tối đa 5 tầng, mỗi tầng gây 20% ATK lúc đặt độc mỗi giây trong 5 giây; thêm tầng làm mới thời lượng chung. Độc không crit, chịu giảm sát thương do giáp trong 1.0; hiệu ứng Bào mòn giảm DEF tối đa 30%. Khiên nổ chỉ phát tối đa một lần mỗi 2 giây và không tự tạo lại khiên.

| Đồng hành | Vai trò | Kỹ năng đặc trưng | Mở khóa |
|---|---|---|---|
| Sói Tro | Tấn công | Ưu tiên mục tiêu ít HP, cắn làm chậm | Boss 2 |
| Người Giữ Đèn | Hỗ trợ | Chữa cho chủ theo hồi chiêu | Boss 3 |
| Golem Than | Bảo vệ | Tạo khiên, giảm một phần sát thương cho chủ | Boss 4 |

Đồng hành bất tử về mặt trình bày trong bản đầu: chỉ chủ nhận sát thương, đồng hành cung cấp hành động và buff. Không thêm đồ riêng hoặc cây chỉ số riêng. Cấp huấn luyện 1–10 dùng vàng và vật liệu vùng; mọi đồng hành dùng chung cấp huấn luyện để đổi đội không bị phạt.

## 7. Chiến đấu, chiến thuật tự động và boss

Đánh thường tự động. Kỹ năng xét điều kiện mỗi lần đến lượt; có tối đa ba quy tắc, theo thứ tự ưu tiên từ trên xuống:

- Nếu HP dưới ngưỡng đã chọn, dùng hồi phục hoặc khiên.
- Nếu boss đang niệm chiêu có thể ngắt, dùng kỹ năng ngắt.
- Nếu không có điều kiện đặc biệt, dùng kỹ năng khi hết hồi chiêu.

Giao diện dùng mẫu sẵn, chỉ chọn ngưỡng 30/40/50% và bật/tắt quy tắc. Chưa có trình lập trình chiến thuật tự do. Người chơi có thể đổi cấu hình trước trận; không thay đồ giữa trận để tránh khai thác hồi chiêu.

Một trận thường mục tiêu dài 20–45 giây, elite 45–75 giây, boss 60–120 giây. Hết 180 giây coi là thất bại; hiện nguyên nhân có thể xử lý: thiếu sát thương, chết vì chiêu mạnh, hồi phục địch quá cao. Đây là giới hạn kỹ thuật và thiết kế, cần thử với cả ba hướng.

Thua trận: về trại, không mất vàng đã nhận, không mất trang bị, không tụt cấp. Chiến lợi phẩm từ các trận đã thắng được ghi nhận sau từng trận, không chờ xong toàn chuyến.

Khi thử chặng mới, thua thì chờ người chơi chọn lại. Trong chế độ farm đã xác nhận, thua thì nghỉ 30 giây tại trại rồi tự thử lại tuyến; thời gian nghỉ và trận thua đều được tính vào benchmark và mô phỏng offline. Người chơi luôn có thể dừng farm hoặc chọn tuyến an toàn hơn.

| Boss | Cơ chế chính | Dấu hiệu dễ nhận biết | Cách khắc chế gợi ý |
|---|---|---|---|
| 1. Sói Đói Tro | Tích lực rồi vồ mạnh | Thanh niệm chiêu và vòng cảnh báo | Giữ khiên hoặc ngắt chiêu |
| 2. Rễ Mẹ | Tự hồi máu theo đợt | Nụ hoa sáng lên | Dồn sát thương vào cửa sổ hồi; ngắt |
| 3. Kỵ Sĩ Rỗng | Dựng giáp tạm thời | Biểu tượng giáp và thời lượng | Tồn tại qua đợt giáp; giảm DEF |
| 4. Bầy Dơi Chuông | Gọi thêm quái nhỏ | Chuông rung trước khi gọi | Độc lan hoặc sát thương nhiều mục tiêu |
| 5. Thợ Rèn Cháy | Đòn mạnh xen giai đoạn hở | Búa đỏ rồi kiệt sức | Khiên đúng lúc, tăng sát thương lúc hở |
| 6. Kẻ Nuốt Lửa | Kết hợp hai cơ chế đã học | Mỗi pha có dấu hiệu riêng | Chuyển ưu tiên kỹ năng giữa các lần thử |

Không tạo miễn nhiễm tuyệt đối khiến một hướng không thể chơi. Boss gọi lính tính là một trận; chỉ trao thưởng khi boss bị hạ, lính gọi lại không tạo nguồn vàng vô hạn.

## 8. Trang bị, rơi đồ và chống thao tác lặp

Năm ô: vũ khí, giáp, mũ, nhẫn, bùa. 30 mẫu gốc gồm 21 mẫu có thể rơi phẩm Thường/Ma thuật/Hiếm và 9 mẫu Huyền thoại có hiệu ứng riêng. Mỗi vùng có bảng rơi mục tiêu theo ô để người chơi biết nên farm ở đâu.

| Phẩm | Thuộc tính | Nguồn mặc định |
|---|---|---|
| Thường | Chỉ số chính | Quái thường và chế tạo |
| Ma thuật | Chỉ số chính + 1 dòng phụ | Quái thường, elite |
| Hiếm | Chỉ số chính + 2 dòng phụ | Quái thường ít hơn; elite, boss nhiều hơn |
| Huyền thoại | Chỉ số chính + 2 dòng phụ + 1 hiệu ứng riêng | Boss và mốc bảo đảm |

Khi đã có một lần rơi đồ thường: phân bố phẩm ban đầu 70% Thường, 25% Ma thuật, 5% Hiếm. Xác suất có lần rơi đồ được cân bằng riêng theo tuyến; không nhầm các tỷ lệ này với xác suất mỗi quái chết.

Boss sau lần thắng đầu có 5% rơi Huyền thoại theo một lượt thử đủ điều kiện. Lượt thử tiêu một **Dấu Săn**, nhận một dấu mỗi 30 phút hoạt động farm được tính, tối đa giữ 20. Không đủ dấu vẫn đánh boss được và nhận thưởng thông thường. Sau 19 lượt đủ điều kiện liên tiếp không ra Huyền thoại, lượt thứ 20 bảo đảm có một món; ra sớm thì đặt lại bộ đếm. Bộ đếm dùng chung các boss, giữ qua đóng game. Cơ chế này tránh farm boss yếu vô hạn để lấy đồ hiếm quá nhanh; vẫn cần mô phỏng và thử nghiệm tốc độ nhận đồ.

Trong tuyến farm boss đã vượt, mô phỏng offline cũng tích và tiêu dấu theo cùng luật. Những lượt boss không tiêu dấu không tăng bộ đếm bảo đảm. Thắng boss lần đầu thưởng vật phẩm cố định, không làm thay đổi bộ đếm này.

Chín hiệu ứng Huyền thoại đề xuất: đòn thứ năm chém thêm; crit rút ngắn một phần hồi chiêu với giới hạn; máu thấp tăng hút máu; tạo khiên gây nổ; hết khiên hồi ít máu; phản đòn làm yếu địch; độc lan khi hạ địch; đủ 5 tầng độc gây nổ nhỏ có hồi chiêu; đồng hành tăng hiệu quả sau khi chủ dùng kỹ năng. Mỗi hiệu ứng cần tag nguồn và giới hạn kích hoạt, không cho phản ứng lặp vô hạn.

Quy tắc kho:

- Khóa đồ yêu thích; mặc định khóa Huyền thoại vừa nhận; đồ đang mặc không thể phân giải.
- So sánh chỉ số chính và hiệu ứng, không tự mặc đồ chỉ vì điểm tổng cao hơn.
- Lọc theo ô, phẩm, hướng xây dựng; đánh dấu mới; phân giải hàng loạt có bản xem trước.
- Tự phân giải chỉ mở sau hướng dẫn và phải được người chơi bật; loại trừ đồ khóa, đồ đang mặc và Huyền thoại.
- Không bán ô túi trong 1.0. Hiển thị danh sách theo trang/ảo hóa; đồ nhận dư ở kho chiến lợi phẩm, không hết hạn và không bị xóa.
- Cảnh báo dọn kho từ 1.000 món; kiểm thử dữ liệu 10.000 món. Phần thưởng offline được xử lý dạng danh sách dữ liệu, không tạo hàng nghìn node hình ảnh.

## 9. Kinh tế và nâng cấp

Chỉ có bốn nhóm tài nguyên: vàng, phế liệu trang bị, vật liệu riêng của từng vùng và Dấu Săn. XP dùng cho cấp; điểm kỹ năng cấp theo mốc cố định. Không thêm kim cương trả phí trong 1.0.

| Tài nguyên | Nguồn | Nơi tiêu |
|---|---|---|
| Vàng | Thắng trận và farm | Cường hóa, công trình, huấn luyện |
| Phế liệu | Phân giải trang bị | Cường hóa và đổi dòng phụ |
| Vật liệu vùng | Farm ở vùng đó | Công trình, chế tạo mẫu đồ đã mở |
| Dấu Săn | Thời gian farm hợp lệ | Lượt thử đồ Huyền thoại ở boss |

Cường hóa mỗi món tối đa +10, thành công 100%. Mỗi cấp tăng 4% chỉ số chính gốc của món đó, cộng tuyến tính; +10 là +40%. Chi phí để đi từ +n lên +(n+1): `round(75 * 1,6^n)` vàng và `round(3 * 1,5^n)` phế liệu, với n từ 0 đến 9. Phân giải trả lại 70% nguyên liệu cường hóa đã tiêu, không hoàn chi phí đổi dòng phụ. Màn hình xác nhận hiển thị chính xác số thu hồi.

Đổi một dòng phụ tiêu vàng và phế liệu, cho chọn giữ cũ hoặc nhận mới. Khóa dòng thứ hai làm tăng phí. Chưa có thất bại làm hỏng đồ, tụt cấp cường hóa hoặc mất món đồ.

Khởi tạo tốc độ farm tuyến trung tính cho chặng n, trước khi nhân theo tốc độ thắng thực tế:

```text
Vàng/phút tham chiếu = 18 * 1,10^(n-1)
XP/phút tham chiếu = 14 * 1,11^(n-1)
Vật liệu vùng/phút tham chiếu = 1 * 1,08^(n-1)
Số lần rơi đồ trung tính tham chiếu = 1 / 12 phút
```

Đây là đường cong mục tiêu cho bộ cân bằng, không phải phần thưởng cộng thêm ngoài chiến đấu. RewardService phải quy đổi về phần thưởng/trận theo thời gian trận chuẩn; chỉ có một nguồn dữ liệu thưởng để tránh nhân đôi vàng.

Ba chế độ farm điều chỉnh phần thưởng đã tính: An toàn = vàng/XP ×1,2, đồ ×0,7, vật liệu ×0,8; Săn tinh anh = vàng/XP ×0,8, đồ ×1,5, vật liệu ×0,8; Thám hiểm = vàng/XP ×0,8, đồ ×0,7, vật liệu ×1,6. Các hệ số chỉ là điểm bắt đầu; kiểm tra không có lựa chọn vượt trội ở mọi mặt.

Mục tiêu cân bằng: đầu game có nâng cấp nhỏ sau 3–5 phút; giữa game sau 10–20 phút; món đồ tạo tương tác mới khoảng 30–90 phút hoạt động được tính. Không dùng Huyền thoại ngẫu nhiên làm điều kiện bắt buộc vượt cốt truyện.

## 10. Trại và nội dung thế giới

Bối cảnh: một vùng đất bị tro lạnh phủ kín. Người chơi thu hồi các mảnh lửa để nối lại những nơi trú ẩn. Cốt truyện kể bằng đoạn hội thoại ngắn tại boss, vật phẩm và thay đổi trong trại.

| Vùng | Chặng | Quái thường / elite / boss | Hình ảnh và vật liệu |
|---|---:|---:|---|
| Rừng Tro | 1–10 | 6 / 2 / 2 | Rừng tối, than hồng, gỗ cháy |
| Tu Viện Chuông Vỡ | 11–20 | 6 / 2 / 2 | Đá xám, đồng cũ, mảnh chuông |
| Lò Rèn Tàn Dương | 21–30 | 6 / 2 / 2 | Sắt đen, lửa cam, quặng nung |

Boss ở chặng 5 và 10 của mỗi vùng. Sáu loại quái thường mỗi vùng được tái phối hợp thành các đội hình; elite dùng biến thể silhouette và hiệu ứng rõ ràng. Vượt boss chặng 10 mở vùng kế tiếp. Mỗi chặng đã vượt trở thành điểm farm có thể chọn trực tiếp.

| Công trình | Công dụng | Năm cấp thể hiện |
|---|---|---|
| Lò rèn | Cường hóa, phân giải, chế tạo, đổi dòng | Mở lần lượt các chức năng; hình dáng lò lớn dần |
| Nhà thuốc | Bình hồi phục tự dùng trong trận | Tăng hiệu quả; nạp lại khi về trại, không phải mua từng bình |
| Sảnh đồng hành | Chọn đồng hành, huấn luyện chung | Tăng giới hạn huấn luyện và mở tương tác |
| Bàn bản đồ | Chọn tuyến, dự báo thưởng, lưu cấu hình | Mở chế độ farm, hai cấu hình và bảng thưởng chi tiết; lọc túi đồ có sẵn sau hướng dẫn |

Công trình nâng tức thì khi đủ nguyên liệu và mốc boss. Mỗi cấp có hình ảnh đổi ít nhất một bộ phận; 20 trạng thái công trình có thể ghép từ bộ phận dùng chung. Chưa có hàng đợi xây dựng theo giờ.

Sau kết thúc: farm tự chọn ở 30 chặng, hoàn thiện bộ sưu tập 9 Huyền thoại và thử ba cách xây nhân vật. Tháp vô tận và vùng bốn thuộc bản cập nhật, chỉ làm sau khi bản 1.0 cho thấy vòng farm hiện tại đủ tốt.

## 11. Thiết kế tiến trình khi đóng game

**Không cần ứng dụng chạy trong nền.** Khi người chơi mở lại, game tính lượng tiến trình tương ứng với thời gian đã rời ứng dụng, dựa trên bản chụp cấu hình tuyến farm được lưu. Không cấp boss mới hoặc mở vùng mới trong lúc đóng game; các chiến thắng lần đầu cần được giải quyết trong phiên chơi.

Quy trình mở tuyến:

1. Người chơi tự động đánh thắng chặng muốn farm.
2. Chạy phép đánh giá nhanh bằng chính bộ mô phỏng chiến đấu, dùng cấu hình hiện tại và một tập seed cố định; mặc định 10 lượt, yêu cầu ít nhất 9 lượt thắng.
3. Nếu chưa đạt, đề xuất chặng thấp hơn đã vượt. Người chơi vẫn có thể thử thách chặng khó trong phiên chơi.
4. Lưu snapshot: ID chặng, chế độ farm, nhân vật, kỹ năng, quy tắc, đồng hành, cấp công trình, phiên bản balance và dữ liệu cần tính thưởng.
5. Hiển thị dự báo theo giờ và giải thích đây là ước tính. Đổi trang bị hoặc nâng cấp làm snapshot hết hiệu lực và phải đánh giá lại trước khi tiếp tục dùng tuyến đó.

Quy tắc thanh toán:

```text
elapsed = thời gian hiện tại - mốc đã giải quyết gần nhất
eligible = clamp(elapsed, 0, 48 giờ)
reward = settle_farm(snapshot, eligible, rng_state, phần thời gian dư)
```

Giới hạn 48 giờ nhận đủ tốc độ, chưa có trả phí mở rộng. Không nhân thêm một “thưởng offline” ngoài kết quả farm. BattleCore dùng chung luật giữa xem trận và mô phỏng; OfflineService có thể gộp nhiều chu kỳ đã đánh giá để chạy nhanh, nhưng phải kiểm tra sai lệch.

Mỗi tuyến có thời lượng chu kỳ, tỷ lệ thắng, thưởng/trận và mức tiêu dấu được suy ra từ bộ mô phỏng. Bản đầu dùng tốc độ thưởng bảo thủ từ tập đánh giá; không tuyên bố kết quả từng trận offline giống hệt các trận đang xem. Chạy kiểm định cùng cấu hình, nhiều seed, yêu cầu trung bình vàng/XP sai lệch không quá 5%; phần thưởng hiếm kiểm tra bằng phân bố xác suất và bộ đếm bảo đảm, không so vài lượt rơi đơn lẻ.

Lưu phần dư thời gian, tiến độ Dấu Săn và trạng thái RNG. Chia 8 giờ thành nhiều lần mở game không được mất phần dư, tạo thêm lượt rơi hoặc đổi tỷ lệ bảo đảm. Tuyến farm trong phiên chơi cũng dùng các chế độ và luật thưởng này; không thưởng nhiều hơn chỉ vì mở màn hình.

Các nâng cấp nhờ XP hoặc nguyên liệu kiếm được khi đóng game chỉ có hiệu lực cho tuyến sau khi quay lại và xác nhận cấu hình mới. Trong chế độ farm khi mở game, trận đánh cũng dùng snapshot đã xác nhận cho đến khi người chơi dừng hoặc lập lại tuyến; cấp mới và trang bị mới không âm thầm làm thay đổi snapshot. Giao diện hiện cấp đang dùng cho chuyến đi, cấp nhân vật đã nhận và nút “Cập nhật tuyến”. Chế độ vượt chặng mới áp dụng cấp hiện tại khi bắt đầu trận. Đây là quy tắc để dự báo ổn định và so sánh thưởng công bằng; phải kiểm tra khả năng hiểu quy tắc này trong playtest.

Xử lý đồng hồ: trong phiên dùng đồng hồ đơn điệu; qua lần mở lại dùng giờ máy. Giờ bị lùi: không cấp phần thưởng âm, đặt lại mốc an toàn và thông báo ngắn. Giờ nhảy quá xa: nhận tối đa 48 giờ và chốt mốc mới. Không khóa người chơi chờ đến một ngày trong tương lai. Game offline hoàn toàn không thể bảo đảm chống chỉnh giờ hoặc sửa save; ưu tiên không mất dữ liệu và không phạt nhầm.

Rời ứng dụng, tắt máy, hệ điều hành thu hồi tiến trình và chuyển múi giờ đều phải được thử. Thời điểm lưu ở UTC; giao diện hiển thị giờ địa phương. Mô phỏng tạm dừng khi app ẩn; khi quay lại chỉ có một đường giải quyết thời gian để tránh tính cả lượt chiến đấu nền lẫn thưởng offline.

## 12. Giao diện và trải nghiệm sử dụng

Năm tab chính: **Trại – Thám hiểm – Nhân vật – Túi đồ – Chế tạo**. Đồng hành ở Nhân vật; công trình nằm trong Trại và liên kết đến đúng màn hình chức năng. Cài đặt và sao lưu nằm ở menu luôn truy cập được.

Màn thám hiểm:

```text
[Vàng] [Vật liệu]                       [Cài đặt]
[Vùng / Chặng]                 [Chế độ farm]
------------------------------------------------
          CẢNH CHIẾN ĐẤU 2D
   Nhân vật + đồng hành        Quái / Boss
   HP, khiên                  HP, niệm chiêu
------------------------------------------------
[Kỹ năng 1] [Kỹ năng 2] [Kỹ năng 3]
Mục tiêu gần nhất: Vượt Rễ Mẹ để mở vùng mới
[Chọn tuyến] [Thử boss] [Chiến thuật]
------------------------------------------------
[Trại] [Thám hiểm] [Nhân vật] [Túi] [Chế tạo]
```

Màn quay lại: tổng thời gian được tính → ba loại tài nguyên chính → tối đa ba món đáng chú ý → tiến độ đến nâng cấp đã ghim. Phần thưởng được ghi vào save trước khi hiện báo cáo; nút “Tiếp tục” chỉ đóng báo cáo, không cấp lại thưởng.

Nguyên tắc trình bày:

- Một nút hành động chính mỗi khối; tooltip giải thích thuật ngữ ngay tại chỉ số.
- Cỡ chữ nội dung bắt đầu khoảng 16 đơn vị logic; phải kiểm tra kích thước thật trên thiết bị và chế độ chữ lớn 150%.
- Vùng chạm Android ít nhất 48dp sau khi quy đổi theo tỷ lệ màn hình; kiểm tra trên máy thật, không mặc định 48 đơn vị Godot luôn là 48dp.
- Tôn trọng vùng tai thỏ/thanh điều hướng; thử màn nhỏ rộng 360dp, màn dài, tablet và thay đổi kích thước cửa sổ Windows.
- Khóa trải nghiệm Android theo chiều dọc ở bản đầu; kiểm tra không vỡ khi hệ điều hành đổi cấu hình hoặc ở chế độ đa cửa sổ.
- Có giảm hiệu ứng, tắt rung, tắt số sát thương nổi, chỉnh nhạc/SFX riêng. Dùng icon và chữ cùng màu phẩm để hỗ trợ người khó phân biệt màu.
- Nội dung chữ thường đạt tương phản mục tiêu 4,5:1; trạng thái focus và nút quan trọng có phân biệt rõ.
- Nút Back đóng lớp hiện tại trước; không thoát game hoặc mất lựa chọn ngoài ý muốn.
- Đánh giá hỗ trợ trình đọc màn hình trên engine đã chọn; chỉ công bố mức hỗ trợ sau khi thử TalkBack, không tự coi node Godot có sẵn đầy đủ ngữ nghĩa.

Hướng mỹ thuật đề xuất: nền `#11151C`, bề mặt `#1D2632`, chữ `#F1E8DA`, chữ phụ `#BBC5D1`, điểm nhấn lửa `#F6B65B` với chữ tối, màu độc `#95D17C`. Đo tương phản từng cặp thực tế, kể cả nút vô hiệu và trạng thái chọn. Font cần hỗ trợ đủ dấu tiếng Việt, đóng gói trong bản cài; không tải font lúc chạy.

Skill ui-ux-pro-max được dùng để tham khảo bố cục cảm ứng, tương phản, giảm chuyển động và hướng nền tối. Gợi ý bố cục landing page từ lượt tìm đầu không phù hợp màn game nên không được áp dụng.

## 13. Kiến trúc phần mềm

Tách luật game khỏi scene để có thể mô phỏng, thử tự động và cân bằng mà không mở giao diện.

```text
project.godot
src/
  core/         # stats, combat, effects, rewards, economy, seeded RNG
  application/  # commands, progression, farm, offline settlement
  persistence/  # save repository, validation, migrations, import/export
  presentation/ # scenes, controls, animation adapters, view models
  platform/     # lifecycle, clock, Android file handoff
content/
  items/ skills/ enemies/ zones/ buildings/ companions/ balance/
assets/
  characters/ enemies/ backgrounds/ ui/ audio/ fonts/
tests/
  unit/ simulation/ fixtures/ migrations/ integration/
tools/
  validate_content/ simulate_balance/ package_release/
docs/
  decisions/ balance_reports/ test_reports/ licenses/
```

Các lớp và hợp đồng chính:

| Thành phần | Đầu vào / đầu ra | Quy tắc |
|---|---|---|
| StatCalculator | Cấu hình → chỉ số cuối | Không sửa save, không đọc scene |
| BattleSimulator | BattleInput + seed → BattleResult + log tùy chọn | Cùng dữ liệu cho trận hiển thị và thử mô phỏng |
| EffectResolver | Sự kiện → hiệu ứng | Giới hạn chuỗi kích hoạt; không gọi đệ quy vô hạn |
| RewardService | Kết quả hợp lệ → RewardDelta | Chỉ một nguồn công thức và bảng rơi |
| ProgressionService | Thắng lần đầu → mở khóa | Không trùng thưởng lần đầu |
| OfflineService | Snapshot + thời gian + RNG → settlement | Không thao tác giao diện hoặc tự ghi file |
| CommandHandler | Ý định người chơi → state mới hoặc lỗi | Xác thực đủ tài nguyên trước mọi thay đổi |
| SaveRepository | State hợp lệ → bản lưu đã xác nhận | Không báo lưu thành công trước khi kiểm tra |
| ContentValidator | Dữ liệu → danh sách lỗi | Chặn ID trùng, tham chiếu sai và hệ số không hợp lệ |

Dữ liệu nội dung dùng JSON có ID ổn định; validate khi build, đổi sang cấu trúc có kiểu khi nạp. Bảng balance tách khỏi code. UI gửi lệnh `equip_item`, `upgrade_item`, `set_farm_route`; không tự trừ tiền hay sửa túi đồ.

RNG của chiến đấu, rơi đồ và hiệu ứng hình ảnh tách riêng. Thêm hiệu ứng hạt không được thay đổi kết quả rơi đồ. Save phải giữ seed/state hoặc bộ đếm đủ để khôi phục luồng RNG.

Chọn một bộ kiểm thử GDScript tương thích với bản engine đã khóa; khóa phiên bản và giấy phép nếu dùng plugin. Nếu không dùng plugin, viết runner headless nhỏ. Không thêm backend, cơ sở dữ liệu máy chủ hoặc framework web vào bản đầu.

## 14. Save, giao dịch phần thưởng và cập nhật

Tài liệu Godot mô tả serialization và lưu file; thiết kế giao dịch dưới đây là yêu cầu bổ sung của dự án, không phải bảo đảm có sẵn của engine. Xem [Saving games](https://docs.godotengine.org/en/stable/tutorials/io/saving_games.html).

Trường dữ liệu bắt buộc:

```text
schema_version, content_version, balance_version, build_version
profile_id, save_sequence, created_at_utc, updated_at_utc
player(level, xp, skill_unlocks, equipped_ids, presets)
inventory(instances, locked_ids), wallet, material_balances
progress(unlocked_nodes, first_clear_claims, story_flags)
camp(building_levels), companion_unlocks, shared_training_level
farm(route_snapshot, rng_state, leftover_ms, hunt_mark_progress_ms)
offline(last_settled_utc, last_settlement_id, last_report)
loot(pity_count, reward_rng_state), settings
```

Instance trang bị có ID riêng, template ID, cấp vật phẩm, phẩm, affix và cường hóa. Không dùng vị trí mảng làm ID. Timestamp lưu dạng nguyên; tiền và tài nguyên dùng số nguyên 64 bit trong lõi. Nếu tuần tự hóa JSON, quy định giới hạn số an toàn hoặc lưu các số rất lớn dưới dạng chuỗi; không để chuyển đổi float âm thầm làm mất tiền.

Lưu A/B luân phiên trong `user://`. Mỗi bản có số thứ tự và checksum của payload được chuẩn hóa. Ghi sang file tạm ở cùng thư mục → đóng file → đọc lại, parse, validate → thay slot không hoạt động → xác nhận có bản hợp lệ. Khi nạp, chọn slot có sequence lớn nhất trong các slot hợp lệ. Checksum phát hiện hỏng dữ liệu, không phải chống sửa save.

Không giả định mọi thao tác ghi đều nguyên tử trên mọi thiết bị. Nếu quá trình dừng giữa chừng, slot còn lại phải dùng được; thử chèn lỗi tại từng bước. Nếu cả hai slot hỏng, giữ nguyên file để khôi phục, cho nhập bản sao lưu; không tự tạo game mới đè dữ liệu cũ.

Luồng nhận thưởng offline:

1. Đọc state hợp lệ và khóa xử lý settlement trong phiên.
2. Tính RewardDelta từ mốc chưa giải quyết; tạo settlement ID.
3. Áp dụng phần thưởng, cập nhật mốc thời gian, RNG, pity, phần dư và báo cáo vào cùng state mới.
4. Commit toàn bộ state bằng SaveRepository.
5. Chỉ sau khi commit thành công mới hiển thị báo cáo; nếu lỗi ghi, giữ state cũ và cho thử lại.

Khởi động lại sau crash chỉ có hai trạng thái hợp lệ: trước giao dịch hoặc sau giao dịch; không tồn tại trạng thái đã nhận tiền nhưng mốc thời gian chưa cập nhật. Quy tắc tương tự áp dụng cho mua nâng cấp, phân giải và thưởng boss lần đầu. Đảm bảo này nằm trong hồ sơ hiện tại; người dùng nhập lại bản sao cũ vẫn có thể quay lui tiến trình, điều được chấp nhận ở game offline.

Autosave theo mục tiêu tối đa 30 giây tiến trình thường; lưu ngay sau giao dịch quan trọng và khi ứng dụng chuyển nền. Không dựa riêng vào callback thoát ứng dụng. Thông báo rõ nếu không lưu được do hết dung lượng.

Migration: chuyển tuần tự v1→v2→v3, thêm mặc định cho trường thiếu, giữ ID cũ hoặc ánh xạ có chủ đích, không reset nhân vật. Sao lưu trước migration. Đồ có template bị bỏ phải được giữ như vật phẩm legacy hoặc đền bù có quy tắc đã công bố. Từ chối nhập save có schema tương lai bằng thông báo dễ hiểu.

Xuất/nhập: dùng hộp chọn file/chia sẻ phù hợp nền tảng, có bản xem trước hồ sơ và thời điểm. Tạo bản sao của hồ sơ hiện tại trước khi nhập. Chỉ đọc dữ liệu, không nạp đường dẫn scene hoặc thực thi mã từ file nhập; giới hạn kích thước, số món, phạm vi số và độ sâu JSON. Người chơi cần xuất backup trước khi gỡ cài đặt hoặc đổi máy.

## 15. Sản xuất hình ảnh, âm thanh và nội dung

Danh mục asset 1.0 cần chốt trong tuần 2:

- 1 nhân vật chính, 3 bộ nhận diện theo hướng; 4 trạng thái cơ bản: chờ, đánh, trúng đòn, gục.
- 3 đồng hành với chờ/đánh/hỗ trợ; tái dùng khung animation khi phù hợp.
- 18 mẫu quái thường, 6 biến thể elite và 6 boss; silhouette boss phải phân biệt ở kích thước điện thoại.
- 3 cảnh chiến đấu, 1 cảnh trại; 4 bộ công trình ghép thành 20 trạng thái.
- 30 icon trang bị, 18 icon kỹ năng/nội tại, icon tài nguyên và bộ điều hướng nhất quán.
- Khoảng 10 nhóm VFX tái sử dụng: chém, crit, độc, nổ độc, khiên, vỡ khiên, hồi máu, phản đòn, cảnh báo boss, vật phẩm hiếm.
- Mục tiêu 4 bản nhạc loop: trại, thám hiểm, boss, boss cuối; 20–30 SFX dùng chung.
- 6 đoạn gặp boss, 6 đoạn sau chiến thắng, hướng dẫn ngắn, mô tả trang bị và kết thúc ngắn.

Thông số ban đầu: icon nguồn 128×128; sprite nhân vật khoảng 192–256px theo chiều cao; texture atlas theo nhóm tải, tránh một atlas khổng lồ chứa mọi vùng. Chốt lại sau khi xem trên thiết bị. Không dùng một ảnh đầy chữ cho giao diện cần dịch.

Mỗi asset cần manifest ghi nguồn, tác giả, giấy phép, điều kiện ghi công và file sử dụng. Font, nhạc, plugin, asset mua và asset tạo bằng AI đều có bản ghi nguồn riêng. Trang Credits chứa thông tin Godot và giấy phép phụ thuộc. Không cài SDK quảng cáo/analytics ở beta offline.

## 16. Kế hoạch cân bằng và kiểm chứng độ cuốn

Mỗi boss có ba cấu hình chuẩn theo ba hướng, cùng mức tài nguyên đầu tư. Chạy tối thiểu 100 seed/cấu hình/boss cho vòng cân bằng tự động; dùng phân bố thời gian hạ boss, tỷ lệ thắng, lượng hồi phục và sát thương từng nguồn. Có thêm cấu hình thiếu đồ, quá mạnh và cố tình tạo vòng lặp hiệu ứng.

Mục tiêu khởi tạo: cấu hình phù hợp cơ chế có tỷ lệ thắng 70–90% ở mức trang bị thiết kế; cấu hình chưa tối ưu vẫn có đường tiến bộ bằng nâng cấp thông thường. Khiên/hồi phục không tạo trận vô hạn; sát thương độc không vượt mọi hướng ở cả quái đơn lẫn nhóm.

Playtest ba vòng, xin phép người thử trước khi ghi hình hoặc thu nhật ký:

| Vòng | Người thử dự kiến | Cần quan sát | Điều kiện để đi tiếp |
|---|---:|---|---|
| Prototype | 5 | Có hiểu thay đồ làm mạnh lên? Có muốn đánh thêm? | Ít nhất 4/5 tự hoàn thành vòng farm–nâng–thử boss, không được người điều phối làm hộ |
| Bản chơi thử một vùng | 8–10 | Có hiểu cách khắc chế boss và thưởng offline? | Ít nhất 70% giải thích đúng một quyết định build và dự báo farm |
| Beta | 15–20 | Save, quay lại nhiều ngày, mức nhàm chán | Không còn lỗi mất dữ liệu đã biết; xác định và xử lý các điểm bỏ chơi lặp lại |

Đây là cổng chất lượng định tính, mẫu nhỏ không chứng minh giữ chân dài hạn. Tỷ lệ quay lại sau một ngày/bảy ngày chỉ là tín hiệu nếu người tham gia đồng ý ghi nhật ký; không đưa ra cam kết retention hoặc doanh thu.

Nhật ký kỹ thuật chỉ lưu cục bộ: phiên bản, seed lỗi, thời gian phiên, mốc mở khóa, kết quả trận, thao tác nâng cấp, lỗi save. Có nút xem/xuất/xóa; không tự gửi đi. Dùng dữ liệu này để trả lời: người chơi kẹt ở đâu, có bao nhiêu món bị phân giải ngay, hướng nào thống trị và thời gian chờ có tạo quyết định mới không.

## 17. Kiểm thử và yêu cầu hiệu năng

| Nhóm | Trường hợp bắt buộc | Điều kiện đạt |
|---|---|---|
| Luật chiến đấu | Crit, giáp, DOT, khiên, chết cùng thời điểm, phản đòn | Cùng input/seed cho cùng kết quả trên môi trường hỗ trợ |
| Giao dịch | Thiếu tiền, bấm nhanh hai lần, đồ khóa/đang mặc | Không tiền âm, không nhân đôi đồ, không xóa nhầm |
| Save | Dừng tiến trình tại từng bước ghi, hỏng một slot, hết dung lượng | Khôi phục slot hợp lệ; thông báo lỗi; không tự xóa dữ liệu |
| Migration | Fixture tất cả schema đã phát hành | Giữ cấp, tiền, đồ, mở khóa; chuyển đổi có báo cáo |
| Offline | 0 giây, 1 phút, 8 giờ, 48 giờ, 7 ngày | Áp dụng đúng giới hạn, phần dư và một lần settlement |
| Đồng hồ | Lùi giờ, tiến giờ, đổi múi giờ, tắt máy | Không tiền âm, không khóa tiến trình vì mốc tương lai |
| Ngang bằng farm | Mở liên tục so với mô phỏng nhiều seed | Vàng/XP trung bình chênh không quá 5%; loot tuân thủ luật xác suất |
| Vòng đời Android | Home, khóa máy, cuộc gọi, hệ điều hành đóng app | Một đường giải quyết thời gian, save nạp lại được |
| Offline hoàn toàn | Lần chạy đầu ở chế độ máy bay | Mọi nội dung thiết yếu có sẵn; không kẹt tải mạng |
| UI | Màn nhỏ, chữ 150%, Back, tai thỏ, 10.000 món | Không che nút chính, có lọc và thao tác hàng loạt ổn định |
| Cài đặt bản mới | Nâng APK beta N lên N+1 với cùng danh tính ứng dụng | Giữ save, migration đạt; không yêu cầu cài sạch |

Thiết bị mục tiêu ban đầu: Android 10 trở lên, ít nhất một máy RAM 3GB và một máy 6GB, cộng một thiết bị có tỷ lệ màn hình khác. Mức OS tối thiểu là quyết định sản phẩm dự kiến, chỉ chốt sau kiểm tra khả năng xuất của phiên bản engine.

Ngân sách hiệu năng dự kiến: 30 FPS ổn định trên máy thấp, tùy chọn 60 FPS; khởi động lạnh dưới 5 giây; giải quyết 48 giờ offline dưới 2 giây trên máy thấp; RAM đỉnh dưới 250MB; APK thử nghiệm dưới 150MB. Đây là mục tiêu phải đo trên máy thật, không phải thông số đã đạt.

Nếu giải quyết offline quá lâu: gộp chu kỳ và tạo loot bằng dữ liệu, chia công việc thành batch, cập nhật tiến độ, giữ UI phản hồi. Nếu chưa đạt ngưỡng sai lệch với chiến đấu đang xem thì tối ưu tiếp, không âm thầm đổi thưởng. App ẩn không duy trì render hoặc vòng lặp chiến đấu.

## 18. Lộ trình 12 tuần và 2 tuần dự phòng

Ước lượng cho một người quen engine, 35 giờ/tuần: 420 giờ kế hoạch + 70 giờ dự phòng = 490 giờ, tương đương 14 tuần. Nếu phải học Godot hoặc tự vẽ toàn bộ asset, cần ước lượng lại sau prototype; không coi 14 tuần là cam kết cố định. Lịch tương đối tính từ ngày bắt đầu thực tế.

| Thời gian | Đầu ra | Cổng nghiệm thu |
|---|---|---|
| Tuần 1–2 | Repo, engine khóa phiên bản, combat cơ bản, một boss, đồ/nâng cấp bằng asset tạm, APK đầu | Chơi được farm–nâng–thử boss; có playtest 5 người |
| Tuần 3–4 | Một vùng trọn 10 chặng, 2 boss, 2 hướng, save A/B, thưởng offline cơ bản | Đóng/mở lại nhận thưởng đúng; hiểu được build; bản Windows và APK |
| Tuần 5–6 | Hoàn thiện settlement, migration, nhập/xuất, kho đồ, lỗi ghi file, kiểm định farm | Qua các lỗi save/offline nghiêm trọng trước khi mở rộng nội dung |
| Tuần 7–8 | Đủ ba vùng, sáu boss, ba hướng, đồng hành, công trình; nội dung khóa phạm vi | Đi từ game mới đến kết thúc bằng dữ liệu hợp lệ |
| Tuần 9–10 | Mỹ thuật/âm thanh hoàn thiện, cân bằng, tối ưu UI, beta 15–20 người | Chạy nhiều ngày; có báo cáo lỗi, build và balance rõ phiên bản |
| Tuần 11–12 | Sửa beta, tối ưu máy thấp, migration thực tế giữa APK, tài liệu và gói release candidate | Đạt checklist phát hành; không còn lỗi mất dữ liệu đã biết |
| Tuần 13–14 | Dự phòng lỗi thiết bị, cân bằng và sửa vấn đề playtest | Không tự dùng dự phòng để thêm tính năng |

Phân bổ 420 giờ: tiền sản xuất 30; combat/core 70; save/offline 65; UI 65; nội dung/cân bằng 60; mỹ thuật/âm thanh tích hợp 55; QA/xuất bản 55; quản lý tài liệu/build 20. Thực hiện đan xen trong các sprint, không chờ cuối dự án mới thử APK hoặc kiểm thử save.

Backlog chi tiết nằm ở file đi kèm `Lua-Trai-Cuoi-Cung-Backlog.md`. Bộ thông số khởi tạo nằm ở `Lua-Trai-Cuoi-Cung-Thong-so-khoi-tao.md`; đây là dữ liệu để dựng prototype và chạy mô phỏng, chưa phải balance đã kiểm chứng. Chỉ lấy việc vào sprint khi có dữ liệu đầu vào, phụ thuộc và điều kiện nghiệm thu. Mỗi task có bản chạy được hoặc bằng chứng kiểm thử, không chỉ trạng thái “đã code”.

Nếu thiếu thời gian, cắt theo thứ tự: hình ảnh phụ và hội thoại dài → hiệu ứng trang trí → số mẫu đồ thường → nội dung vùng ba chuyển thành cập nhật. Khi cắt vùng, gọi đúng là bản chơi thử hoặc early access; không tuyên bố hoàn thành phạm vi 1.0 ba vùng. Giữ nguyên chất lượng save, vòng farm, khả năng đọc và chế độ máy bay.

## 19. Nguồn lực và ngân sách

Đây là trần chi dự kiến để quản lý dự án, không phải báo giá thị trường hoặc lời khuyên mua hàng:

| Khoản | Trần phân bổ đề xuất |
|---|---:|
| Engine Godot | 0 đồng phí bản quyền engine theo giấy phép đã đối chiếu |
| Asset hình ảnh/icon mua sẵn | 3.000.000 đồng |
| Nhạc, SFX, font nếu cần mua | 1.000.000 đồng |
| Hỗ trợ playtest và mượn/thuê thiết bị | 3.000.000 đồng |
| Dự phòng chi tiền | 2.000.000 đồng |
| Tổng trần tiền mặt ban đầu | 9.000.000 đồng |

Chưa gồm công lao động, thiết bị phát triển mới, phí tài khoản phân phối hoặc dịch vụ mỹ thuật riêng. Công lao động tính riêng bằng `490 giờ × đơn giá nội bộ/giờ`. Nếu không chi tiền, dùng asset được phép sử dụng và thiết bị sẵn có, giảm mức hoàn thiện mỹ thuật theo khả năng; không coi lao động tự làm là không có chi phí.

Không cần ngân sách máy chủ cho phạm vi beta. Không mua asset hoặc mở tài khoản trả phí chỉ vì đã có bảng này; từng khoản mua là quyết định thực thi riêng dựa trên nhu cầu thật và giấy phép phù hợp.

## 20. Rủi ro và cách xử lý

| Rủi ro | Dấu hiệu sớm | Cách xử lý |
|---|---|---|
| Farm nhàm chán | Chỉ bấm nâng số, không muốn đổi đồ | Đưa món tạo tương tác vào sớm; giảm nâng cấp không tạo khác biệt |
| Phạm vi phình | Thêm nghề, pet, tháp trước khi save ổn | Đóng phạm vi theo bảng mốc; tính năng mới vào danh sách sau 1.0 |
| Một hướng thống trị | Thắng hầu hết boss với đầu tư thấp hơn rõ rệt | Chỉnh hệ số và nhịp cơ chế; không vô hiệu hóa hướng khác bằng miễn nhiễm |
| Mất/nhân đôi save | Lỗi khi ghi hoặc mở lại nhiều lần | Save A/B, giao dịch state, fault injection và fixture migration |
| Offline khác mở game | Người chơi thấy phải treo máy mới lợi | Dùng cùng nguồn thưởng, benchmark nhiều seed, sửa sai lệch trước beta |
| Đồ rác quá nhiều | Người thử dành phần lớn phiên để dọn túi | Giảm tần suất rơi, cải thiện lọc, tự phân giải có lựa chọn |
| Thiếu mỹ thuật | Nhiều mẫu không đồng bộ | Bộ asset chung, tái dùng bộ phận, duyệt trên thiết bị từ sớm |
| Chậm trên máy thấp | VFX và kho gây giật | Pool VFX, giới hạn số sát thương, ảo hóa danh sách, profile trước tối ưu |
| Chỉnh giờ/sửa save | Tài nguyên tăng bất thường cục bộ | Chấp nhận giới hạn offline; không mở kinh tế cạnh tranh dựa trên save đó |
| Nhập file lỗi | Crash, số quá lớn, template lạ | Giới hạn input, validate, preview và backup trước nhập |
| Thay nội dung làm gãy farm | Snapshot tham chiếu ID đã xóa | Settle bằng snapshot hợp lệ cũ hoặc migration có bù; cập nhật tuyến có thông báo |

## 21. Định nghĩa hoàn thành và phát hành

Một chức năng hoàn thành khi có dữ liệu, đường vào UI, lỗi được xử lý, save/migration liên quan, kiểm thử phù hợp và bản xuất chạy được. Prototype có thể dùng hình tạm; release candidate phải dùng asset đã kiểm tra giấy phép.

Điều kiện phát hành beta:

- Cài và chơi ở chế độ máy bay, thắng/thua boss, thay đồ, nâng cấp và trở về game hoạt động.
- Có xuất/nhập save; thông báo giới hạn 48 giờ và giới hạn bảo vệ trước sửa giờ rõ ràng.
- Không còn lỗi mất dữ liệu hoặc nhân đôi phần thưởng đã biết; có hướng dẫn báo lỗi và khôi phục.
- Có số build, schema, balance version và log để tái hiện.

Điều kiện phát hành 1.0:

- Đủ phạm vi 3 vùng, 30 chặng, 6 boss, 3 hướng, 3 đồng hành, 4 công trình và kết thúc.
- Có hồ sơ kiểm thử save/offline, kết quả cân bằng và hiệu năng trên thiết bị mục tiêu.
- Cập nhật từ bản beta trước giữ tiến trình; không yêu cầu xóa dữ liệu để nâng phiên bản.
- Credits/giấy phép, mô tả sản phẩm, icon, ảnh chụp và ghi chú phiên bản đầy đủ.
- Kiểm tra lại yêu cầu hiện hành của kênh phân phối ngay trước khi nộp; không dùng thông số SDK trong kế hoạch này thay cho chính sách cửa hàng.

Gói bàn giao: source Git có tag; bảng nội dung và báo cáo cân bằng; APK beta/release candidate đã ký đúng loại; bản Windows thử nghiệm; cấu hình export không chứa bí mật; hướng dẫn build; fixture save và test report; asset/license manifest; changelog; danh sách lỗi còn lại.

Khóa ký và mật khẩu lưu ngoài Git, có bản sao được bảo quản; không đưa vào gói source công khai. Giữ ổn định danh tính ứng dụng và cấu hình ký cho các bản cần cập nhật nối tiếp. Thử rollback ở môi trường test; không hứa hạ phiên bản đọc được schema mới nếu chưa có đường tương thích.

Sau phát hành: theo dõi báo lỗi người chơi tự gửi; ưu tiên mất dữ liệu, không vào game, không nhận thưởng rồi mới cân bằng. Bản vá không reset save. Chỉ mở rộng vùng/nội dung khi vòng chơi hiện tại đã qua thử nghiệm và không còn vấn đề nền tảng.

## 22. Thứ tự bắt tay vào làm ngay

1. Tạo repo mới và ghi quyết định nền tảng; khóa engine, renderer và export templates.
2. Xuất APK có một màn hình trống lên thiết bị thật ngay ngày đầu, xác nhận cài và cập nhật được.
3. Làm combat bằng dữ liệu: một nhân vật, một quái, một boss, sáu món đồ.
4. Làm vòng “farm → nhận đồ → nâng → đánh lại” trước nội dung lớn.
5. Làm save A/B, seed RNG và fixture từ đầu; không chờ game gần xong mới thiết kế save.
6. Sau prototype, thử với 5 người; giữ, sửa hoặc thu hẹp theo bằng chứng.
7. Hoàn thành một vùng cùng save/offline để có bản chơi thử trọn vẹn.
8. Chỉ sau cổng này mới sản xuất đủ nội dung ba vùng và hoàn thiện mỹ thuật.

Sản phẩm đầu tiên cần chứng minh là một vòng chơi nhỏ khiến người chơi muốn thử lại với món đồ vừa nhận. Toàn bộ kế hoạch phát triển dựa vào việc chứng minh được điều đó và bảo vệ được tiến trình đã kiếm.
