# LỬA TRẠI CUỐI CÙNG — BỘ THÔNG SỐ KHỞI TẠO

Ngày 27/10/2026 • Dữ liệu đề xuất cho prototype, chưa được chạy mô phỏng hoặc playtest.

Tài liệu này làm rõ các hệ số còn cần đưa vào bảng dữ liệu khi lập trình. Nếu mâu thuẫn, kế hoạch chính quyết định phạm vi và quy tắc; hệ số trong bộ này được thay đổi qua báo cáo cân bằng có phiên bản. ID trong bảng là ID nội dung đề xuất, phải giữ ổn định khi phát hành save đầu tiên.

## 1. Quy ước chung

- Thời gian dữ liệu tính bằng mili giây; bảng trình bày bằng giây cho dễ đọc.
- Tỷ lệ lưu dưới dạng phần trăm điểm cơ sở hoặc quy ước số thống nhất; không trộn 20 với 0,20 trong cùng schema.
- `r` là cấp kỹ năng/nội tại, từ 1 đến 3. Cấp 0 là chưa học.
- Bắt đầu có 1 điểm kỹ năng; mỗi lần tăng cấp từ 2 đến 30 thêm 1; mỗi boss lần đầu thêm 1: tối đa 36 điểm. Mỗi cấp kỹ năng/nội tại tiêu 1 điểm.
- Mở hướng Cuồng chiến ngay từ đầu; Hộ vệ sau boss 1; Độc sư sau boss 3. Mở hướng không tự cấp toàn bộ kỹ năng. Đổi phân bổ điểm miễn phí ở trại, hoàn đủ điểm.
- Mang 3 kỹ năng và 2 nội tại. Không có mana trong 1.0; nhịp dùng kỹ năng được điều khiển bằng hồi chiêu và quy tắc.
- Kỹ năng sát thương có thể crit và hút máu trên phần đánh trực tiếp nếu không ghi khác. Độc, phản đòn và nổ do hiệu ứng dây chuyền không crit, không hút máu.
- Kỹ năng nhắm mục tiêu hiện tại; kỹ năng diện rộng đánh tối đa 5 mục tiêu. Không cho bắn trượt vào mục tiêu đã chết.
- Bình Nhà thuốc là hiệu ứng riêng, không chiếm một trong ba ô kỹ năng.

## 2. Chín kỹ năng chủ động

| ID | Tên | Hệ số theo r | Hồi chiêu | Điều kiện/chú ý |
|---|---|---|---|---|
| skill.berserker.flurry | Chém liên hoàn | 2 đòn, mỗi đòn `(0,8 + 0,15*(r-1))*ATK` | 6 giây | Mỗi đòn là một hit; hiệu ứng đòn thứ năm chỉ đếm hit đánh thường, không đếm kỹ năng |
| skill.berserker.rage | Cuồng nộ | Tăng tốc độ đánh `30 + 5*(r-1)%` trong 5 giây | 14 giây | Áp dụng cap tốc độ chung; không cộng dồn nhiều lần lên chính nó |
| skill.berserker.blood | Hồi huyết | Hồi `18 + 6*(r-1)%` HP tối đa | 14 giây | Quy tắc mặc định dùng khi HP dưới 40%; không hồi vượt HP tối đa |
| skill.guardian.shield | Khiên sắt | Khiên `20 + 5*(r-1)%` HP, tồn tại 5 giây | 12 giây | Áp dụng giới hạn tổng khiên; khiên mới không làm mới vô hạn khiên cũ |
| skill.guardian.challenge | Khiêu chiến | Giảm sát thương địch gây ra `15 + 5*(r-1)%` trong 4 giây | 16 giây | Ngắt một lần niệm chiêu có thể ngắt khi sử dụng; boss vẫn áp dụng thời gian kháng ngắt riêng |
| skill.guardian.counter | Phản kích | Đánh `1,6 + 0,2*(r-1)` ATK; phản 25% HP mất do đòn trực tiếp trong 4 giây | 10 giây | Phản đòn không sinh phản đòn; không phản độc hoặc sát thương môi trường |
| skill.poison.dart | Phi tiêu độc | Đánh `0,8 + 0,1*(r-1)` ATK, thêm 1 tầng độc | 5 giây | Tăng cấp tăng hit đầu; sát thương độc lấy quy tắc độc chung |
| skill.poison.erode | Bào mòn | Giảm DEF `20 + 5*(r-1)%` trong 6 giây | 12 giây | Không cộng nhiều bản cùng hiệu ứng; mức mạnh hơn thay mức yếu hơn |
| skill.poison.burst | Bùng độc | Tiêu tối đa 5 tầng độc; gây `(0,7 + 0,1*(r-1))*ATK` mỗi tầng lên mục tiêu chính, 50% lên mục tiêu khác | 10 giây | Mặc định chỉ dùng khi có ít nhất 3 tầng; không crit/hút máu; không tự đặt độc |

Boss kháng ngắt trong 8 giây sau lần ngắt thành công. UI phân biệt “không thể ngắt chiêu này” với “đang kháng ngắt”. Không kích hoạt hồi chiêu của kỹ năng nếu điều kiện không hợp lệ và kỹ năng chưa thực sự được dùng.

## 3. Chín nội tại

| ID | Tên | Tác dụng theo r | Giới hạn |
|---|---|---|---|
| passive.berserker.leech | Hút máu | Thêm `3*r%` hút máu | Cap hút máu chung 15% |
| passive.berserker.desperate | Cuồng chiến | Dưới 40% HP tăng `10 + 5*(r-1)%` ATK | Kiểm tra trên HP hiện tại; bỏ buff khi vượt ngưỡng |
| passive.berserker.combo | Chuỗi đòn | Mỗi đánh thường liên tiếp thêm `r%` sát thương đánh thường, tối đa 5 tầng | Mất khi đổi mục tiêu hoặc 3 giây không đánh; không buff kỹ năng |
| passive.guardian.armor | Giáp bền | Tăng `8*r%` DEF | Cộng vào nhóm % DEF, chịu cap giảm sát thương |
| passive.guardian.explode | Khiên nổ | Tạo khiên gây `0,5*r*ATK` sát thương quanh chủ | Một lần mỗi 2 giây; không tự tạo khiên |
| passive.guardian.steadfast | Kiên định | Khi HP dưới 35%, giảm sát thương nhận thêm `3*r%` | Áp dụng một lần sau giáp; không vượt giới hạn tổng giảm sát thương dự án chốt qua cân bằng |
| passive.poison.stack | Tích độc | Tăng sát thương độc `8*r%` | Không đổi số tầng tối đa 5 |
| passive.poison.spread | Lây độc | Hạ mục tiêu có độc: chuyển `min(r, số tầng hiện có)` sang tối đa 2 địch gần nhất | Độc chuyển giữ thời gian còn lại; không tự nổ hoặc tạo chuỗi vô hạn |
| passive.poison.hunter | Săn kẻ suy yếu | Mục tiêu từ 3 tầng độc nhận thêm `4*r%` sát thương từ chủ | Không khuếch đại hai lần cùng một sự kiện sát thương |

Giới hạn tổng giảm sát thương sau khi tính giáp và các buff: tối đa 85%. Ví dụ giáp giảm 75% và buff giảm tiếp 10% thì nhân `0,25*0,90`, không cộng thành 85% một cách mặc định. Sau tất cả mới chặn ở tối đa 85% để nhân vật không bất tử.

## 4. Đồng hành và Nhà thuốc

Cấp huấn luyện chung `t` từ 1 đến 10; sát thương đồng hành lấy ATK của chủ trong snapshot, áp dụng giáp mục tiêu, không crit hoặc hút máu trong bản đầu.

| ID | Hành động | Hệ số |
|---|---|---|
| companion.ash_wolf | Cắn mỗi 3 giây, ưu tiên địch ít HP | `(0,35 + 0,025*(t-1))*ATK`; làm chậm tốc độ đánh mục tiêu 10% trong 2 giây |
| companion.lantern_keeper | Hồi máu cho chủ khi HP dưới 60%, hồi chiêu 10 giây | `4 + 0,5*(t-1)%` HP tối đa |
| companion.coal_golem | Tạo khiên khi chủ chưa có khiên, hồi chiêu 12 giây | `6 + 0,5*(t-1)%` HP tối đa trong 4 giây; thêm 5% giảm sát thương nhận cho chủ khi có khiên |

Chi phí huấn luyện từ t lên t+1: `round(120*1,5^(t-1))` vàng và `round(5*1,4^(t-1))` vật liệu vùng cao nhất đã mở. Không có thao tác tăng từ cấp 10 lên 11.

Nhà thuốc cấp b cho 1 lần dùng bình mỗi trận, kích hoạt tự động khi HP dưới 30%; hồi `15 + 3*(b-1)%` HP tối đa. Được nạp lại khi bắt đầu trận mới; chu kỳ farm/offline tính bình theo cùng luật. Bình không thể cứu một đòn đã đưa HP về 0. Mọi nguồn hồi máu chịu chỉ số tăng hồi phục; không vượt HP tối đa.

## 5. Năm ô trang bị và thuộc tính phụ

Cấp vật phẩm `i` từ 1 đến 30, thường theo chặng n đang farm. Cường hóa không đổi cấp vật phẩm.

| Ô | Chỉ số chính cơ bản trước phẩm/cường hóa |
|---|---|
| Vũ khí | `18 + 5*i` ATK |
| Giáp | `90 + 15*i` HP |
| Mũ | `6 + 2*i` DEF |
| Nhẫn | `2 + 0,15*i` điểm phần trăm crit |
| Bùa | `4 + 0,4*i` phần trăm tăng hiệu quả hồi máu nhận |

Hệ số chỉ số chính theo phẩm: Thường 1,00; Ma thuật 1,10; Hiếm 1,20; Huyền thoại 1,20. Huyền thoại nổi bật nhờ hiệu ứng, không tự có mọi chỉ số lớn hơn Hiếm. Cường hóa +n nhân chỉ số chính với `1 + 0,04*n`; affix và hiệu ứng riêng không tăng theo cường hóa.

Affix lấy ngẫu nhiên trong khoảng tại cấp i=10 dưới đây, rồi nhân `f(i)=0,5+0,05*i`. Các tỷ lệ là điểm phần trăm cộng vào nhóm tương ứng. Không sinh trùng ID affix trên cùng món.

| ID affix | Khoảng tại i=10 | Ô được phép |
|---|---|---|
| affix.attack_flat | 6–18 ATK | Vũ khí, nhẫn |
| affix.health_flat | 30–90 HP | Giáp, mũ, bùa |
| affix.defense_flat | 4–12 DEF | Giáp, mũ |
| affix.attack_pct | 2–5% ATK | Vũ khí, bùa |
| affix.attack_speed | 2–4% tốc độ | Vũ khí, nhẫn |
| affix.crit_chance | 2–4 điểm % crit | Vũ khí, nhẫn |
| affix.crit_damage | 4–10 điểm % hệ số crit | Vũ khí, bùa |
| affix.leech | 1–2 điểm % hút máu | Vũ khí, nhẫn |
| affix.healing | 3–6% hiệu quả hồi máu | Giáp, bùa |
| affix.shield_power | 3–6% lượng khiên | Giáp, mũ, bùa |
| affix.poison_damage | 3–7% sát thương độc | Vũ khí, bùa |
| affix.cooldown | 1–3 điểm % giảm hồi chiêu | Mũ, nhẫn |

Chỉ số chạm cap vẫn hiển thị lượng dư trong tooltip để người chơi biết nên đổi món khác. Chế tạo mẫu thường đã mở tạo phẩm Ma thuật cố định; không tạo Huyền thoại ngẫu nhiên bằng vàng trong 1.0.

## 6. Danh mục 30 mẫu trang bị

Các mẫu thường là danh tính hình ảnh và nhóm bảng rơi, dùng công thức ô tương ứng; không viết 21 công thức riêng. Cấp vật phẩm được tạo theo chặng, nên một mẫu cũ có thể xuất hiện với cấp cao hơn.

| ID | Tên | Ô | Nhóm |
|---|---|---|---|
| item.rust_blade | Kiếm Rỉ | Vũ khí | Thường |
| item.hunter_axe | Rìu Thợ Săn | Vũ khí | Thường |
| item.thorn_dagger | Dao Gai | Vũ khí | Thường |
| item.chapel_spear | Giáo Tu Viện | Vũ khí | Thường |
| item.forge_hammer | Búa Lò Rèn | Vũ khí | Thường |
| item.leather_coat | Áo Da Vá | Giáp | Thường |
| item.ash_mail | Giáp Tro | Giáp | Thường |
| item.chapel_plate | Giáp Tu Viện | Giáp | Thường |
| item.black_iron_plate | Giáp Sắt Đen | Giáp | Thường |
| item.cloth_hood | Mũ Vải | Mũ | Thường |
| item.hunter_cap | Mũ Thợ Săn | Mũ | Thường |
| item.bell_helm | Mũ Chuông Vỡ | Mũ | Thường |
| item.forge_helm | Mũ Thợ Rèn | Mũ | Thường |
| item.copper_ring | Nhẫn Đồng | Nhẫn | Thường |
| item.briar_ring | Nhẫn Dây Gai | Nhẫn | Thường |
| item.vow_ring | Nhẫn Lời Thề | Nhẫn | Thường |
| item.ember_ring | Nhẫn Than Hồng | Nhẫn | Thường |
| item.wood_charm | Bùa Gỗ | Bùa | Thường |
| item.tooth_charm | Bùa Nanh | Bùa | Thường |
| item.bell_charm | Bùa Mảnh Chuông | Bùa | Thường |
| item.cinder_charm | Bùa Tàn Lửa | Bùa | Thường |
| item.legend.fifth_cut | Nhát Chém Thứ Năm | Vũ khí | Huyền thoại |
| item.legend.quick_spark | Tia Lửa Vội | Vũ khí | Huyền thoại |
| item.legend.last_thirst | Cơn Khát Cuối | Vũ khí | Huyền thoại |
| item.legend.ember_wall | Tường Than Hồng | Giáp | Huyền thoại |
| item.legend.ash_shelter | Mái Tro | Giáp | Huyền thoại |
| item.legend.hollow_crown | Vương Miện Rỗng | Mũ | Huyền thoại |
| item.legend.plague_loop | Vòng Lây Nhiễm | Nhẫn | Huyền thoại |
| item.legend.fifth_venom | Giọt Độc Thứ Năm | Bùa | Huyền thoại |
| item.legend.shared_flame | Ngọn Lửa Chung | Bùa | Huyền thoại |

Hiệu ứng Huyền thoại v1:

| ID rút gọn | Hiệu ứng |
|---|---|
| fifth_cut | Mỗi đòn đánh thường thứ năm thêm một hit 100% ATK; hit thêm không tăng bộ đếm |
| quick_spark | Crit từ đánh trực tiếp giảm 0,5 giây hồi chiêu còn lại của kỹ năng lâu nhất; tối đa một lần mỗi 3 giây; không rút dưới 0 |
| last_thirst | Dưới 40% HP thêm 5 điểm % hút máu, chịu cap chung |
| ember_wall | Tạo khiên gây nổ 60% ATK quanh chủ, tối đa một lần mỗi 2 giây; không sinh khiên |
| ash_shelter | Khi một khiên của chủ hết do thời gian hoặc bị phá, hồi 5% HP tối đa, tối đa một lần mỗi 6 giây; khiên bị thay thế không kích hoạt |
| hollow_crown | Phản đòn làm giảm ATK mục tiêu 10% trong 3 giây; không cộng dồn với chính nó |
| plague_loop | Hạ địch đang trúng độc chuyển thêm 1 tầng sang tối đa 2 địch; gộp với Lây độc nhưng vẫn cap 5 tầng/mục tiêu |
| fifth_venom | Đạt 5 tầng độc gây thêm 120% ATK sát thương độc, mỗi mục tiêu tối đa một lần mỗi 6 giây; không tiêu tầng, không tự kích hoạt lại |
| shared_flame | Chủ dùng kỹ năng làm hiệu quả hành động kế tiếp của đồng hành tăng 30%; một buff chờ, không cộng dồn |

Bảng boss: boss 1–2 rơi ba món Huyền thoại đầu; boss 3–4 rơi ba món tiếp; boss 5–6 rơi ba món cuối. Trong nhóm mỗi món trọng số bằng nhau; đồ trùng có thể phân giải. Chọn boss mục tiêu giúp thu hẹp bảng rơi. Không yêu cầu sưu tập đủ chín món để kết thúc game.

## 7. Quái và độ khó chặng

Với chặng `n` từ 1 đến 30:

```text
HP nền = round(150 * 1,14^(n-1))
ATK nền = round(12 * 1,12^(n-1))
DEF nền = 5 + 3*n
Cấp quái = n
Tốc độ nền = 0,6 đòn/giây
```

Sáu vai trò quái dùng ở mỗi vùng:

| Vai trò | HP | ATK | DEF | Tốc độ | Đặc tính |
|---|---:|---:|---:|---:|---|
| Cân bằng | ×1,0 | ×1,0 | ×1,0 | ×1,0 | Mốc so sánh |
| Nhanh | ×0,7 | ×0,75 | ×0,6 | ×1,5 | Nhiều hit nhỏ |
| Đỡ đòn | ×1,5 | ×0,7 | ×1,5 | ×0,8 | Trận lâu hơn |
| Đánh mạnh | ×0,9 | ×1,4 | ×0,8 | ×0,7 | Có thời gian tích lực |
| Hỗ trợ | ×0,8 | ×0,5 | ×0,8 | ×0,8 | Hồi một đồng minh mỗi 10 giây, tối đa 5% HP của mục tiêu |
| Bầy đàn | ×0,45 | ×0,45 | ×0,5 | ×1,0 | Xuất hiện theo nhóm 3, tổng áp lực phải được mô phỏng |

Tên vùng một: Sói Tro, Dơi Cành, Lợn Gai, Gấu Cháy, Nấm Đèn, Bọ Than. Vùng hai: Tu Sĩ Rỗng, Dơi Chuông, Giáp Câm, Người Gác Cổng, Kẻ Giữ Hương, Chuột Đá. Vùng ba: Thợ Mỏ Tro, Tia Lửa Sống, Giáp Lò, Búa Lạc, Người Châm Lửa, Bọ Sắt. Các tên theo thứ tự ánh xạ sáu vai trò trong bảng.

Elite dùng vai trò có sẵn, HP ×2,0, ATK ×1,25 và thêm một đặc tính cảnh báo rõ; mỗi vùng hai biến thể. Boss bắt đầu với HP nền ×5,0, ATK nền ×1,6 và tốc độ nền ×0,8, sau đó chỉnh riêng qua mô phỏng cơ chế. Không tự tăng toàn bộ hệ số cùng lúc để giải quyết boss quá dễ.

Chặng thường luân phiên 1–3 quái theo áp lực dự kiến; chặng có ba quái phải giảm tổng HP/ATK từng con theo budget trận. Thưởng là thưởng cho cả trận, không cấp nguyên thưởng trận cho mỗi con. Đội hình cuối cùng được khóa trong task E01/E02 sau khi đo thời gian và tỷ lệ thắng.

## 8. Công trình, mở khóa và chi phí ban đầu

| Công trình | Cấp 1 | Cấp 2 | Cấp 3 | Cấp 4 | Cấp 5 |
|---|---|---|---|---|---|
| Lò rèn | Phân giải/cường hóa | Chế tạo mẫu đã mở | Đổi dòng phụ | Khóa một dòng khi đổi | Giảm 10% phí vàng rèn, không giảm phế liệu |
| Nhà thuốc | Bình 15% HP | 18% HP | 21% HP | 24% HP | 27% HP |
| Sảnh đồng hành | Mang một đồng hành | Trần huấn luyện 4 | Trần 6 | Trần 8 | Trần 10 |
| Bàn bản đồ | Farm An toàn, dự báo | Săn tinh anh | Thám hiểm | Lưu cấu hình thứ hai | Đánh dấu tuyến yêu thích và bảng thưởng chi tiết |

Sảnh cấp 1 cho trần huấn luyện 2. Bàn bản đồ vẫn có thể xem tuyến và phần thưởng cơ bản ngay từ cấp 1; nâng cấp không giấu thông tin thiết yếu. Các bộ lọc túi đồ luôn có sẵn sau hướng dẫn, không bị khóa bởi công trình.

Cấp công trình 1 nhận theo hướng dẫn/mốc mở khóa, không phải mua trước khi có chức năng farm. Lò rèn và Bàn bản đồ mở trong vùng đầu; Nhà thuốc sau boss 1; Sảnh sau boss 2.

Chi phí từ cấp b lên b+1: `round(250*2^(b-1))` vàng và `round(20*1,8^(b-1))` vật liệu phù hợp. Giới hạn cấp công trình theo tiến trình: sau boss 1 tối đa 2; sau boss 2 tối đa 3; sau boss 4 tối đa 4; sau boss 6 tối đa 5. Nếu một chức năng bắt buộc đang nằm sau cổng quá muộn trong thử nghiệm, chuyển mở khóa thay vì buộc người chơi chờ.

Chi phí chế tạo mẫu Ma thuật: `round(100*1,1^(i-1))` vàng, `round(5*1,07^(i-1))` vật liệu vùng và 5 phế liệu. Đổi dòng lần đầu: 150 vàng + 10 phế liệu, mỗi lần tiếp theo trên cùng món nhân phí 1,5, chặn ở 5 lần mức cơ sở; khóa dòng còn lại nhân 2 phí. Giữ dòng cũ vẫn tiêu phí đã hiển thị. Không cho hoàn tác bằng đóng cửa sổ sau khi kết quả đã commit.

## 9. Dữ liệu bắt buộc trước khi đánh dấu một nội dung hoàn thành

Mỗi kỹ năng: ID, tên/chuỗi mô tả, kiểu mục tiêu, hệ số, hồi chiêu, thời lượng, điều kiện dùng, tag sát thương, tag kích hoạt, icon và trường test tham chiếu.

Mỗi quái/boss: ID, vai trò, cấp, hệ số, hành động, tín hiệu cảnh báo, cửa sổ ngắt, nhóm thưởng, animation và điều kiện kết thúc pha.

Mỗi chặng: ID, vùng, đội hình, điều kiện mở, phần thưởng lần đầu, bảng thưởng lặp, mốc farm và tham chiếu bối cảnh.

Mỗi món: ID, ô, nhóm phẩm, công thức chỉ số chính, pool affix, hiệu ứng, nguồn rơi, icon, giá phân giải. Mẫu thường không cố định một phẩm khi sinh đồ.

Mỗi công trình/đồng hành: ID, điều kiện mở, giới hạn cấp, chi phí, tác dụng theo cấp và hình ảnh. Validator phải chặn tham chiếu nội dung chưa tồn tại.

Không coi bộ thông số này là bằng chứng game đã cân bằng. Đầu ra cần có sau task E05 là bảng so sánh build, thời gian trận, đường tài nguyên, tỷ lệ rơi và các chỉnh sửa dựa trên kết quả chạy thật.
