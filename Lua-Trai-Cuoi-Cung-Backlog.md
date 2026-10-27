# LỬA TRẠI CUỐI CÙNG — BACKLOG TRIỂN KHAI

Ngày 27/10/2026 • Đọc cùng kế hoạch chính và bộ thông số khởi tạo.

Toàn bộ công việc đang ở trạng thái **chưa triển khai**. Đây là kế hoạch thực hiện, không phải báo cáo đã xây game. Ước lượng là giờ công tập trung của một người quen Godot; từng task bao gồm kiểm tra tại chỗ. Kiểm thử hệ thống, playtest và đóng gói có hạng mục riêng.

Thứ tự ưu tiên: P0 = bắt buộc để chứng minh vòng chơi và bảo vệ dữ liệu; P1 = bắt buộc cho phạm vi 1.0 đã nêu; P2 = hoàn thiện, được giảm trước nếu thiếu lịch. Tính năng thuộc 1.0 bị cắt phải được ghi lại thành thay đổi phạm vi.

## A. Tiền sản xuất — 30 giờ

| ID | Việc | Ưu tiên | Giờ | Phụ thuộc | Điều kiện nghiệm thu |
|---|---|---|---:|---|---|
| A01 | Khóa nền tảng, phạm vi, engine, renderer và export templates | P0 | 5 | — | Có decision record; engine mở được project; không dùng bản preview |
| A02 | Tạo Git, cấu trúc source, quy ước ID và luồng build | P0 | 5 | A01 | Clone sạch mở được; asset nguồn và nội dung tách rõ; bí mật bị loại khỏi Git |
| A03 | Wireframe luồng farm–nâng–boss–quay lại, kiểm tra trên điện thoại | P0 | 8 | A01 | Tối đa 5 tab; nút chính và Back rõ; dự kiến xử lý tai thỏ/chữ lớn |
| A04 | Schema nội dung, save v1 và bảng thông số đầu | P0 | 7 | A01 | Có trường bắt buộc, ID ổn định, giới hạn và fixture ban đầu |
| A05 | Xuất APK/Windows rỗng, cài và cập nhật trên máy thật | P0 | 5 | A02 | Hai bản APK nối tiếp giữ được dữ liệu thử; lưu hướng dẫn build |

## B. Lõi gameplay và chiến đấu — 70 giờ

| ID | Việc | Ưu tiên | Giờ | Phụ thuộc | Điều kiện nghiệm thu |
|---|---|---|---:|---|---|
| B01 | StatCalculator, cấp, XP và giới hạn chỉ số | P0 | 8 | A04 | Fixture chỉ số đạt; không vượt cap; rounding có quy định |
| B02 | Đồng hồ mô phỏng, lượt đánh, seeded RNG và kết quả trận | P0 | 14 | B01 | Cùng input/seed tái hiện kết quả; không phụ thuộc FPS |
| B03 | EffectResolver: độc, khiên, hồi phục, phản đòn, ngắt chiêu | P0 | 12 | B02 | Không kích hoạt lặp vô hạn; thứ tự khiên/HP/hút máu đúng |
| B04 | Trang bị, affix, loot, Dấu Săn và bảo đảm Huyền thoại | P0 | 10 | B02 | Không thưởng trùng; đủ 20 lượt hợp lệ bảo đảm; seed lưu lại được |
| B05 | Lệnh cường hóa, đổi dòng, phân giải, khóa đồ và giao dịch | P0 | 8 | B04 | Không tiền âm; giữ đồ khóa/đang mặc; hoàn nguyên liệu đúng |
| B06 | Kỹ năng, ba mẫu chiến thuật và đồng hành hỗ trợ | P1 | 10 | B03 | Thực thi đúng thứ tự quy tắc; đồng hành không cần hệ trang bị riêng |
| B07 | Mở chặng, thưởng lần đầu, pha boss và giới hạn thời gian trận | P0 | 8 | B03, B04 | Không thưởng lại first clear; boss phát tín hiệu trước chiêu; kết thúc trận luôn xác định |

## C. Save và tiến trình offline — 65 giờ

| ID | Việc | Ưu tiên | Giờ | Phụ thuộc | Điều kiện nghiệm thu |
|---|---|---|---:|---|---|
| C01 | Repository A/B, checksum, sequence và phục hồi lỗi ghi | P0 | 14 | A04, B01 | Chèn lỗi từng bước vẫn nạp được một slot hợp lệ; không tự reset |
| C02 | Migration, validate import và fixture theo schema | P0 | 9 | C01 | Save cũ giữ tài sản; schema tương lai bị từ chối có giải thích |
| C03 | Đánh giá tuyến farm, snapshot và mô phỏng gộp chu kỳ | P0 | 14 | B04, B06, B07 | Dùng tuyến đã vượt; snapshot đủ dữ liệu; giữ thời gian dư và RNG |
| C04 | Settlement giao dịch, báo cáo quay lại và chống cấp lặp trong hồ sơ | P0 | 10 | C01, C03 | Crash trước/sau commit không mất hoặc nhân đôi phần thưởng |
| C05 | Pause/resume, giờ máy bất thường, tối đa 48 giờ và autosave | P0 | 8 | C04 | Home/khóa máy/kill app không tính hai lần; đổi múi giờ không thay elapsed |
| C06 | Xuất/nhập backup qua UI nền tảng và thông báo lỗi lưu | P0 | 10 | C02, D01 | Xuất rồi nhập giữ hồ sơ; hỏng file/hết dung lượng có đường xử lý |

## D. Giao diện — 65 giờ

| ID | Việc | Ưu tiên | Giờ | Phụ thuộc | Điều kiện nghiệm thu |
|---|---|---|---:|---|---|
| D01 | Theme, component chung, điều hướng, safe area và Back | P0 | 10 | A03, A05 | Năm tab nhất quán; vùng chạm đúng trên máy thật |
| D02 | Cảnh chiến đấu, kỹ năng, HP/khiên và tín hiệu boss | P0 | 12 | D01, B02, B03 | Nhìn hiểu diễn biến; UI không quyết định kết quả trận |
| D03 | Túi đồ, so sánh, lọc, khóa và thao tác hàng loạt | P0 | 12 | D01, B04, B05 | 10.000 món không tạo 10.000 control; không chọn nhầm đồ khóa |
| D04 | Nhân vật, kỹ năng, đồng hành và hai cấu hình lưu | P1 | 8 | D01, B06 | Đổi cấu hình ngoài trận; hiển thị nguồn thay đổi chỉ số |
| D05 | Trại, bốn công trình và màn chế tạo | P1 | 9 | D01, B05, E04 | Đủ điều kiện nâng, giá và tác dụng có thể xem trước |
| D06 | Chọn farm, dự báo, cập nhật snapshot và báo cáo quay lại | P0 | 8 | D01, C03, C04 | Phân biệt cấp chuyến đi/cấp hiện tại; nút đóng báo cáo không cấp thưởng |
| D07 | Hướng dẫn theo ngữ cảnh, cài đặt, chữ lớn và giảm hiệu ứng | P0 | 6 | D02, D03, D06 | Hoàn thành vòng đầu không cần giải thích ngoài game; dấu tiếng Việt đầy đủ |

## E. Nội dung và cân bằng — 60 giờ

| ID | Việc | Ưu tiên | Giờ | Phụ thuộc | Điều kiện nghiệm thu |
|---|---|---|---:|---|---|
| E01 | Tuyến một vùng: 10 chặng, 2 boss và 12 mẫu đồ đầu | P0 | 10 | B07, A04 | Chơi được từ bắt đầu đến mở vùng hai bằng asset tạm |
| E02 | Hoàn tất ba vùng, 30 chặng, 18 quái thường và 6 elite | P1 | 10 | E01 | ID/đội hình/bảng rơi đầy đủ; validator không báo lỗi |
| E03 | Hoàn tất 6 boss, 9 kỹ năng, 9 nội tại và 30 mẫu đồ | P1 | 12 | E01, B06 | Mô tả khớp hệ số; mỗi hiệu ứng có giới hạn kích hoạt |
| E04 | Công trình, mở khóa, đồng hành, kinh tế và cốt truyện ngắn | P1 | 8 | E01 | Bốn công trình có 5 cấp; unlock không tự khóa vòng tiến trình |
| E05 | Công cụ mô phỏng, cấu hình chuẩn và báo cáo cân bằng | P0 | 12 | B06, C03, E03 | Có kết quả nhiều seed; so thời gian boss và thưởng farm, phát hiện hướng quá mạnh |
| E06 | Chỉnh vòng chơi sau playtest, khóa content/balance version | P0 | 8 | E04, E05, G03 | Sửa điểm kẹt chính; không dùng Huyền thoại bắt buộc; changelog có lý do |

## F. Mỹ thuật và âm thanh tích hợp — 55 giờ

Phân bổ này giả định asset có sẵn hoặc bộ phận tái sử dụng. Không đủ để một người tự vẽ và hoạt họa toàn bộ danh mục từ số không.

| ID | Việc | Ưu tiên | Giờ | Phụ thuộc | Điều kiện nghiệm thu |
|---|---|---|---:|---|---|
| F01 | Chốt phong cách, kiểm tra asset và manifest giấy phép | P0 | 7 | A03 | Mỗi asset có nguồn; mẫu nhân vật/UI hợp ở kích thước thật |
| F02 | Tích hợp nhân vật, đồng hành, quái và hoạt ảnh | P1 | 16 | F01, D02, E02 | Đủ trạng thái; silhouette boss rõ; atlas và import setting phù hợp |
| F03 | Cảnh vùng, trại và 20 trạng thái công trình ghép bộ phận | P1 | 12 | F01, D05 | Công trình thay đổi dễ thấy; không che UI |
| F04 | Icon, VFX, phản hồi nút và giảm chuyển động | P1 | 10 | F01, D03, E03 | Không dùng màu làm dấu hiệu duy nhất; VFX không can thiệp RNG gameplay |
| F05 | Nhạc/SFX, âm lượng, Credits và hoàn thiện hình ảnh | P1 | 10 | F02, F03, F04 | Asset đóng gói offline; tắt âm độc lập; giấy phép được ghi nhận |

## G. QA, playtest và xuất bản — 55 giờ

| ID | Việc | Ưu tiên | Giờ | Phụ thuộc | Điều kiện nghiệm thu |
|---|---|---|---:|---|---|
| G01 | Runner tự động, smoke headless và validation nội dung | P0 | 7 | A02, B01 | Lệnh chạy được từ checkout sạch; trả mã lỗi khi test fail |
| G02 | Fault injection save, lỗi thời gian và soak offline | P0 | 12 | C05, C06 | Bao phủ ma trận rủi ro; có test report và fixture tái hiện |
| G03 | Tổ chức ba vòng playtest và tổng hợp điểm bỏ chơi | P0 | 12 | B05, D02 | Vòng đầu có thể chạy sớm; kết quả phân biệt lỗi hiểu UI với lỗi cân bằng |
| G04 | Profile máy thấp, kho lớn, mô phỏng 48 giờ và chữ lớn | P0 | 10 | D07, C05, F04 | Có số đo so với ngân sách; sửa nút thắt đã xác định |
| G05 | Thử nâng APK qua phiên bản, hồi quy end-to-end và release candidate | P0 | 8 | E06, F05, G02, G04 | Save giữ nguyên qua cập nhật; chơi máy bay; hoàn thành cốt truyện |
| G06 | Đóng gói, hướng dẫn cài/backup, release notes và kiểm tra kênh phân phối | P1 | 6 | G05, H04 | Có gói bàn giao; yêu cầu hiện hành được xác nhận trước khi đăng |

## H. Tài liệu và quản lý build — 20 giờ

| ID | Việc | Ưu tiên | Giờ | Phụ thuộc | Điều kiện nghiệm thu |
|---|---|---|---:|---|---|
| H01 | Duy trì quyết định thiết kế, danh sách cắt phạm vi và sổ rủi ro | P0 | 5 | A01 | Quyết định thay đổi có ngày/lý do; không gọi bản thiếu phạm vi là 1.0 đủ |
| H02 | Build định kỳ, phiên bản và changelog | P0 | 5 | A05 | Mỗi build truy được source/content/balance; giữ bản có thể thử |
| H03 | Sổ lỗi, kiểm tra cổng chất lượng và rà ước lượng | P0 | 5 | H01 | Lịch được cập nhật sau tuần 2/4/8; lỗi dữ liệu ưu tiên cao nhất |
| H04 | Runbook phát hành, phục hồi và quản lý khóa ký | P0 | 5 | C01, A05 | Khóa ngoài Git; biết build lại, chẩn đoán save và phát bản vá |

## Tổng giờ và đường phụ thuộc quan trọng

| Nhóm | Giờ |
|---|---:|
| A. Tiền sản xuất | 30 |
| B. Lõi gameplay | 70 |
| C. Save/offline | 65 |
| D. Giao diện | 65 |
| E. Nội dung/cân bằng | 60 |
| F. Mỹ thuật/âm thanh | 55 |
| G. QA/phát hành | 55 |
| H. Tài liệu/build | 20 |
| Tổng kế hoạch | **420** |
| Dự phòng, chưa phân vào tính năng | **70** |
| Tổng nguồn lực dự kiến | **490** |

Đường phụ thuộc: A01→A04→B01→B02→B03/B04→B06/B07→C03→C04→C05→G02/G04→G05→G06. C01 và D01 phát triển đan xen từ đầu; C06 cần giao diện nền tảng. Không hiểu bảng là phải xong toàn bộ B mới được làm C hoặc D.

G03 có ba lần thực hiện xuyên suốt: sau prototype, sau một vùng hoàn chỉnh và beta. Không chờ toàn bộ E/F mới thử với người thật. E05 chạy nhiều lần khi bổ sung nội dung, không chỉ một lần cuối.

## Sprint đầu — 10 ngày làm việc, khoảng 70 giờ

| Ngày | Trọng tâm | Bằng chứng cuối ngày |
|---|---|---|
| 1 | A01, bắt đầu A02, xuất APK tối thiểu | Ảnh/video thiết bị mở bản cài; engine được ghi phiên bản |
| 2 | A02, A05 và bản wireframe đầu | Build lặp được; thử cập nhật bản cài |
| 3 | A04, phần A03 cần cho vòng đầu | Schema/fixture và luồng màn hình để lập trình |
| 4 | B01 và test chỉ số | Test tính chỉ số/cap/XP chạy được |
| 5 | B02 phần đánh thường và RNG | Hai thực thể đánh nhau; cùng seed tái hiện |
| 6 | B02, dựng D02 tối thiểu | Xem được một trận; kết quả không đổi theo FPS |
| 7 | B04/B05 phạm vi sáu món, nhận đồ và nâng cấp | Hoàn thành farm–nhận–nâng–đánh lại |
| 8 | B03 tối thiểu và boss đầu | Có khiên/cảnh báo, có thắng/thua rõ |
| 9 | G03 vòng prototype, rà A03 | Quan sát 5 người; lưu điểm vướng và mong muốn thử lại |
| 10 | Sửa điểm vướng chính, chốt H01/H03 | Bản prototype thử được; cập nhật phạm vi và ước lượng |

Đây là lịch phân đoạn task, không có nghĩa các ID lớn đã hoàn tất trong 10 ngày. Task hoàn thiện sau tiếp tục ở sprint sau. Nếu không có APK và vòng farm chạy được ở cuối sprint đầu, dừng tăng nội dung để xử lý nền tảng hoặc độ phức tạp.

## Mẫu ghi một task khi thực hiện

```text
ID / tên:
Mục đích đối với người chơi:
Đầu vào và phụ thuộc:
Thay đổi source/content:
Ảnh hưởng save và migration:
Các lỗi cần xử lý:
Cách kiểm chứng:
Build / bằng chứng:
Giờ thực tế / giờ còn lại:
Trạng thái: chưa làm | đang làm | cần sửa | đã nghiệm thu
```

Chỉ đánh dấu “đã nghiệm thu” khi có bằng chứng tương ứng trong bảng. Nếu số giờ thực tế chênh lớn, sửa kế hoạch phần còn lại; không bù bằng cách bỏ kiểm thử save hoặc âm thầm đổi phạm vi.
