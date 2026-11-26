# CSCC – Giám sát chiếu sáng công cộng

Phần mềm giám sát hệ thống chiếu sáng đường phố **từ xa qua Bản đồ 3D và SCADA**, kèm điều khiển tủ và quản lý sự cố. Chạy trên trình duyệt điện thoại và máy tính, cài được như app (PWA).

**Mở:** https://phucle-gps.github.io/CSCC/

## Các mục trong trang
| Mục | Nội dung |
|---|---|
| 🗺️ **Bản đồ** (trang mở đầu) | Nền CAD và toàn bộ dữ liệu của **LIGHTING-GIS** (Q1, Q3, Bình Thạnh, Phú Nhuận): 874 tủ, 16.200 trụ, 15.382 đoạn cáp ngầm/nổi, ranh phường, sông, tên đường. Xem 2D kiểu CAD hoặc 3D, nền tối/sáng, lọc theo quận, tìm tủ/trụ/địa chỉ. Dòng điện chạy trong cáp, đèn sáng/tắt theo số đo, đoạn nghi đứt nhấp nháy đỏ, ghim 📍 sự cố. |
| 📟 **SCADA** | Lưới trạng thái 874 tủ theo quận; chọn tủ để xem sơ đồ một sợi: CB tổng, K1/K2, dòng 3 pha so với dòng chuẩn tính từ danh mục đèn GIS, dãy trụ theo từng tuyến. |
| 🎛️ **Điều khiển** | Danh sách tủ, điều khiển hàng loạt; từng tủ có Đo lường, Sơ đồ tủ 3D, Vào/Ra, Điện năng, Lịch, Nhật ký. |
| 🚨 **Cảnh báo** | Một danh sách sự cố chung cho cả bản đồ, SCADA và tủ: vị trí ước tính, giao tổ, Zalo, báo cáo ngày, Excel. |
| ⚙️ **Cài đặt** | Kết nối MQTT, PIN điều khiển, tổ đội, danh sách tủ, giả lập sự cố (Demo). |

## Ước tính vị trí đứt cáp
App dựng cây cáp của từng tủ từ dữ liệu GIS (trụ → trụ cha → tủ) và tính dòng chuẩn của từng trụ từ công suất, loại đèn (LED/HPS…). Khi dòng tổng của tủ giảm, app tìm trụ mà **toàn bộ nhánh phía sau** có dòng bằng lượng bị mất → nghi đứt cáp giữa trụ đó và trụ trước, kèm tên đường và số mét theo cáp từ tủ. Giảm 1–2 bóng → nghi hỏng bóng lẻ. Chỉ cần tủ đo dòng tổng, không cần đo từng tuyến. Hệ số hiệu chỉnh tự học khi tủ chạy bình thường.

## Dữ liệu mạng (LIGHTING-GIS)
App đọc `pack.gz` và `base.gz` của repo **LIGHTING-GIS**: ưu tiên `../LIGHTING-GIS/` (cùng tên miền Pages), dự phòng `raw.githubusercontent.com`. Cập nhật dữ liệu ở LIGHTING-GIS là CSCC tự dùng bản mới. Toạ độ VN-2000 (m).

**Mã tủ** trong firmware (`CABINET_ID`) đặt **trùng mã KNTT của LIGHTING-GIS** (ví dụ `T002.04`, `EC04.15`) hoặc mã PE; tủ thật gửi bản tin lên broker sẽ tự gắn vào đúng vị trí trên bản đồ và SCADA.

## Tự đồng bộ với LIGHTING-GIS
| Đối tượng | Đồng bộ |
|---|---|
| **Trụ đèn** | Vị trí (kể cả trụ đã dời sát mép đường), tên, loại trụ, trụ xoá, trụ vẽ thêm |
| **Cần đèn** | Loại cần (theo thống kê cần đèn), hướng xoay của trụ và của từng cần |
| **Bộ đèn** | Loại (LED/HPS/MH/trang trí), công suất, số bộ – dùng để tính dòng chuẩn |
| **Cáp, tủ** | Đoạn cáp vẽ thêm/xoá/đổi ngầm-nổi, vị trí tủ |

- **Chỉnh sửa chung** (lưu trên máy chủ Apps Script của LIGHTING-GIS): kéo về **mỗi 60 giây** và khi mở lại app. Cần đăng nhập tài khoản LIGHTING-GIS (quyền *Chỉ xem* là đủ) ở **Cài đặt → Đồng bộ với LIGHTING-GIS**; nếu trình duyệt đã đăng nhập LIGHTING-GIS thì CSCC tự dùng phiên đó (cùng tên miền).
- **Dữ liệu gốc** `pack.gz`: kiểm tra bản mới **mỗi 15 phút**.
- Sau mỗi lần đồng bộ, cây cáp, dòng chuẩn, định vị đứt cáp, bản đồ và SCADA tính lại; sự cố đang mở và giả lập được giữ theo mã trụ.
- Phóng to bản đồ để thấy **cần đèn và bộ đèn** vẽ theo hướng thật, màu theo loại đèn (xanh LED, cam HPS, tím MH, hồng trang trí).

## Lớp bản đồ và mô hình trụ 3D
- Nút **🗂️ Lớp** trên bản đồ: bật/tắt nền đường, sông, ranh phường, tên đường, cáp ngầm, cáp nổi, trụ, cần + bộ đèn, quầng sáng, tủ, nhãn trụ, dòng điện. App nhớ lựa chọn trên máy.
- Chế độ **3D** khi phóng to: trụ thép côn / bê tông / trang trí có đế, cần đèn cong vươn theo hướng và độ vươn trong LIGHTING-GIS, bộ đèn ở đầu cần (mặt đèn sáng khi đèn đang sáng), đèn trang trí dạng quả cầu. Chỉ dựng các trụ quanh chỗ đang xem để máy yếu vẫn chạy được.

## Bật GitHub Pages (làm 1 lần)
Settings → Pages → Source: **Deploy from a branch** → Branch **main**, thư mục **/ (root)** → Save.

## Lưu ý
- Chế độ Demo giả lập cả 874 tủ theo dữ liệu GIS (bản tin 10 s/lần); giả lập sự cố tại trụ bằng nút 🧪 trên thẻ trụ hoặc ở Cài đặt.
- Dữ liệu chia kênh K1/K2 chưa có trong GIS nên mọi đèn tạm coi là K1 (cả đêm).
- Broker MQTT công cộng chỉ để thử; dùng thật cần broker riêng có mật khẩu.
- Đo dòng từng tuyến (`r`, `rcb`) và đóng lại CB từ xa (`rcb`, `cb`) là phần mở rộng – xem `firmware/README.md`.
- Firmware mới kiểm tra cú pháp, chưa biên dịch trên bộ công cụ ESP32 thật – chạy thử trên Wokwi trước.
- Mọi đấu nối vào điện 220/380 V do thợ điện có chuyên môn thực hiện.
- `ban-do-chieu-sang.html` chỉ còn chuyển hướng về `./#/ban-do` cho link cũ.
- Three.js r128 (MIT) kèm trong `vendor/`.
