# CSCC – Chiếu sáng công cộng

App cá nhân giám sát, điều khiển tủ chiếu sáng đường phố và đào tạo vận hành. Chạy trên trình duyệt điện thoại và máy tính, cài được ra màn hình chính như app (PWA).

| Phần | File | Mở trên web |
|---|---|---|
| App điều khiển tủ | `index.html` | https://phucle-gps.github.io/CSCC/ |
| Bản đồ 3D + SCADA + đào tạo | `ban-do-chieu-sang.html` | https://phucle-gps.github.io/CSCC/ban-do-chieu-sang.html |
| Firmware gateway ESP32 | `firmware/` | Xem `firmware/README.md` |

## App điều khiển tủ
- **Tổng quan**: tủ trực tuyến, tủ đang sáng, công suất, điện năng hôm nay, sự cố chưa xong.
- **Tủ**: đo lường 3 pha · sơ đồ 3D có dòng điện chạy và phân đoạn sự cố · vào/ra (6 DI, 4 DO) · điện năng · lịch từng kênh · nhật ký.
- **Điều khiển**: bật/tắt từng kênh hoặc hàng loạt theo khu vực. Lệnh phải bấm xác nhận, chờ tủ phản hồi, có mã PIN tuỳ chọn.
- **Cảnh báo**: giao tổ, chép tin gửi Zalo, báo cáo ngày, xuất Excel.
- **Cài đặt**: kết nối MQTT, chế độ Demo (8 tủ giả lập), giả lập sự cố.

## Bản đồ 3D + SCADA + đào tạo
- Mạng TBA → tủ → tuyến → cột dựng từ khối dữ liệu `NET` ở đầu file. Sửa khối này theo bản vẽ tuyến thật để có mô hình của khu vực mình (1 đơn vị = 3,3 m).
- Sơ đồ một sợi, faceplate điều khiển, cảnh báo kiểu DCS (ACK, giao tổ), ước tính vị trí đứt cáp từ mức sụt dòng.
- 5 bài đào tạo chấm điểm: cắt trộm cáp, xe tông cột, mất điện lưới, contactor không đóng, hỏng bóng lẻ.

## Bật GitHub Pages (làm 1 lần)
Settings → Pages → Source: **Deploy from a branch** → Branch **main**, thư mục **/ (root)** → Save.

## Lưu ý
- Dữ liệu ở chế độ Demo là mẫu. Broker MQTT công cộng chỉ để thử; dùng thật cần broker riêng có mật khẩu.
- Firmware mới kiểm tra cú pháp, chưa biên dịch trên bộ công cụ ESP32 thật – chạy thử trên Wokwi trước.
- Mọi đấu nối vào điện 220/380 V do thợ điện có chuyên môn thực hiện.
- Three.js r128 (MIT) kèm trong `vendor/`.
