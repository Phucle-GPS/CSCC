# CSCC – Giám sát chiếu sáng công cộng

Phần mềm giám sát hệ thống chiếu sáng đường phố **từ xa qua Bản đồ 3D và SCADA**, kèm điều khiển tủ và quản lý sự cố. Chạy trên trình duyệt điện thoại và máy tính, cài được như app (PWA).

**Mở:** https://phucle-gps.github.io/CSCC/

## Các mục trong trang
| Mục | Nội dung |
|---|---|
| 🗺️ **Bản đồ 3D** (trang mở đầu) | TBA → tủ → tuyến → cột đèn trên mạng đường phố. Dòng điện chạy trong cáp, đèn sáng/tắt theo số đo, vùng nghi đứt cáp nhấp nháy đỏ, ghim 📍 vị trí sự cố. Chạm vào tủ/cột để xem số liệu, điều khiển, đánh dấu. |
| 📟 **SCADA** | Sơ đồ một sợi tự vẽ: thanh cái, CB tổng, CB nhánh, contactor K1/K2, dòng từng tuyến, dãy cột. Bấm thiết bị để điều khiển. |
| 🎛️ **Điều khiển** | Danh sách tủ, điều khiển hàng loạt; từng tủ có Đo lường, Sơ đồ tủ 3D, Vào/Ra, Điện năng, Lịch, Nhật ký. |
| 🚨 **Cảnh báo** | Một danh sách sự cố chung cho cả bản đồ, SCADA và tủ: vị trí ước tính, giao tổ, Zalo, báo cáo ngày, Excel. |
| ⚙️ **Cài đặt** | Kết nối MQTT, PIN điều khiển, tổ đội, danh sách tủ, giả lập sự cố (Demo). |

## Ước tính vị trí đứt cáp
Tủ đo dòng từng tuyến. Dòng giảm bao nhiêu bóng (≈ 0,68 A/bóng LED 150 W) thì suy ra đứt sau cột số mấy, cách tủ bao nhiêu mét. Giảm 1–2 bóng → nghi hỏng bóng lẻ; ≥ 3 bóng → nghi đứt cáp.

## Dữ liệu mạng
Khối `NET` ở đầu phần script của `index.html` mô tả TBA, tủ, đường, tuyến, số cột (1 đơn vị toạ độ = 3,3 m). Sửa theo bản vẽ tuyến thật để có mô hình khu vực mình. Mã tủ phải trùng `CABINET_ID` trong firmware; tủ thật gửi bản tin lên broker sẽ tự gắn vào bản đồ.

## Bật GitHub Pages (làm 1 lần)
Settings → Pages → Source: **Deploy from a branch** → Branch **main**, thư mục **/ (root)** → Save.

## Lưu ý
- Chế độ Demo là mạng mẫu 3 tủ · 6 tuyến · 42 cột. Broker MQTT công cộng chỉ để thử; dùng thật cần broker riêng có mật khẩu.
- Đo dòng từng tuyến (`r`, `rcb`) và đóng lại CB từ xa (`rcb`, `cb`) là phần mở rộng – xem `firmware/README.md`.
- Firmware mới kiểm tra cú pháp, chưa biên dịch trên bộ công cụ ESP32 thật – chạy thử trên Wokwi trước.
- Mọi đấu nối vào điện 220/380 V do thợ điện có chuyên môn thực hiện.
- `ban-do-chieu-sang.html` chỉ còn chuyển hướng về `./#/ban-do` cho link cũ.
- Three.js r128 (MIT) kèm trong `vendor/`.
