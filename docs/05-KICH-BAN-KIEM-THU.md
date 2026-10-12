# Kịch bản kiểm thử nghiệm thu — Cho thuê Sân thể thao

> Test case theo use case trong `03-USE-CASE.md`. Phần nền (đăng nhập, phân quyền, đặt lại dữ liệu) dùng TC-SYS-01 đến TC-SYS-10 trong `ZDOCS/03-KIEN-TRUC/USE-CASE-NEN.md` §8.

---

## 1. Cách chạy

| Mục | Nội dung |
| :--- | :--- |
| Môi trường | Chạy cả hai chế độ: dữ liệu mẫu (`mock`) và BE thật (`api`) |
| Ngày chạy | Thứ Hai đến Thứ Sáu, không phải ngày lễ đã khai báo, để lượt "hôm nay" tính giá ngày thường |
| Dữ liệu | Đặt lại dữ liệu demo trước mỗi lượt test, trong khoảng 09:30–11:30 |
| Thứ tự | Chạy theo thứ tự số TC; nhiều TC dùng kết quả của TC trước |
| Thời điểm | Chạy TC-21 đến TC-33 trước 14:00 để lượt tạo "ngay bây giờ" nằm trọn khung Trưa và lượt 14:00 hôm nay chưa bắt đầu |
| Ghi số liệu gốc | Trước TC-23, ghi lại doanh thu ghi nhận hôm nay ở Tổng quan; tiền sân, bán kèm, thu nhập cọc hôm nay ở Báo cáo → Doanh thu |
| Tài khoản | Theo cột "Vai trò", dùng "Đăng nhập nhanh"; vai trò Khách dùng cửa sổ ẩn danh |
| Thiết bị | TC vai trò Nhân viên chạy ở cửa sổ 1280×800; TC vai trò Khách chạy ở 375×812 |
| Đạt | Kết quả thực tế khớp toàn bộ cột "Kết quả mong đợi" |

**Ngày T** là Thứ Ba gần nhất cách hôm nay từ 2 ngày trở lên. **T+2** là Thứ Năm, **T+4** là Thứ Bảy cùng tuần.

**Sân:** cụm Bình Thạnh (05:00–23:00) có PB1, PB2 (pickleball trong nhà), PB3, PB4 (pickleball ngoài trời), CL1, CL2 (cầu lông trong nhà); cụm Thủ Đức (05:00–23:00) có BD1, BD2 (bóng đá 5 người ngoài trời), BD3 (bóng đá 7 người ngoài trời), PB5 (pickleball ngoài trời).

**Bảng giá mỗi giờ:**

| Loại sân | Sáng 05:00–09:00 | Trưa 09:00–16:00 | Chiều tối 16:00–23:00 | Cuối tuần |
| :--- | ---: | ---: | ---: | ---: |
| Pickleball | 140.000 ₫ | 100.000 ₫ | 200.000 ₫ | 220.000 ₫ |
| Cầu lông | 70.000 ₫ | 60.000 ₫ | 100.000 ₫ | 110.000 ₫ |
| Bóng đá 5 người | 250.000 ₫ | 200.000 ₫ | 400.000 ₫ | 450.000 ₫ |
| Bóng đá 7 người | 400.000 ₫ | 300.000 ₫ | 650.000 ₫ | 700.000 ₫ |

Ưu đãi đặt cố định 10%.

**Bán kèm:** Nước suối 10.000 ₫/chai, Revive 15.000 ₫/chai, Nước dừa 25.000 ₫/trái, Thuê vợt cầu lông 20.000 ₫/lượt, Thuê vợt pickleball 30.000 ₫/lượt, Quả cầu lông 25.000 ₫/quả, Bóng pickleball 40.000 ₫/quả, Thuê áo bib 5.000 ₫/áo.

**Khách:** Lê Quốc Thịnh 0938 222 333 có 2 lần không đến trong 60 ngày, đang bị chặn đặt online; Đặng Văn Tú 0908 333 444 có 1 lần không đến trong 60 ngày.

**Lượt cố định cho test (dữ liệu mẫu phải bảo đảm):**

| Ký hiệu | Sân | Thời gian | Khách | Trạng thái, tiền |
| :--- | :--- | :--- | :--- | :--- |
| N1 | PB4 | Hôm nay, bắt đầu trước giờ đặt lại 30 phút (làm tròn xuống mốc 30 phút), 60 phút | Đặng Văn Tú 0908 333 444 | Đã xác nhận, chưa nhận sân; tiền sân 100.000 ₫, cọc 50.000 ₫ |
| R2 | PB5 | Hôm nay 14:00–15:00 | Bùi Thị Ngọc 0906 777 888 | Đã xác nhận; tiền sân 100.000 ₫, cọc 50.000 ₫ |
| R3 | BD2 | Hôm nay 16:00–17:30 | Hồ Văn Phúc 0919 666 777 | Đã xác nhận; tiền sân 600.000 ₫, cọc 300.000 ₫ |
| R1 | PB5 | Hôm nay 21:00–22:00 | Vũ Hoàng Long 0977 222 444 | Đã xác nhận; tiền sân 200.000 ₫, cọc 100.000 ₫ |
| Y1 | CL1 | Ngày mai 18:00–20:00 | Trịnh Hải Yến 0904 321 987 | Chờ xác nhận cọc, khách bấm "Tôi đã chuyển khoản" trước giờ đặt lại 40 phút |
| S1 | PB3 | T+2, 18:30–19:30 | Lý Thanh Sơn 0939 444 555 | Đã xác nhận |

Ngoài ra: ngày T, PB3 và BD1 không có lượt nào; trong 4 tuần từ ngày T, PB3 khung 18:00–20:00 các Thứ Ba, Thứ Năm chỉ có lượt S1; PB1 có ít nhất một lượt trong 14 ngày tới; hôm nay BD3 và CL2 trống từ giờ đặt lại tới 16:00.

---

## 2. Test case

### 2.1. Sân và bảng giá

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-01 | UC-01 | Thêm sân mới | Chủ sân | 1. Sân → Thêm sân 2. Mã `PB6`, tên "Pickleball PB6", cụm Bình Thạnh, loại Pickleball, ngoài trời 3. Lưu 4. Mở `/dat-san`, chọn Pickleball, cụm Bình Thạnh, ngày T | Lịch sân cụm Bình Thạnh có cột PB6; trang đặt sân có PB6, ô 16:00 trở đi ghi 200.000 ₫/giờ |
| TC-02 | UC-01 | Ngừng hoạt động sân còn lượt tương lai | Chủ sân | 1. Mở PB1, chuyển "Ngừng hoạt động" 2. Lưu | Từ chối, hiện số lượt tương lai của PB1; PB1 vẫn hoạt động |
| TC-03 | UC-01 | Khóa bảo trì trùng lượt | Nhân viên, Chủ sân | 1. Nhân viên tạo lượt BD1 ngày T 18:00–19:30 cho Phan Minh Đức 0902 555 666, chọn "Giữ chỗ chờ cọc" 2. Chủ sân: Sân → Lịch khóa, khóa BD1 ngày T 17:00–21:00, lý do "Thay đèn", Lưu 3. Hủy lượt bước 1, bên hủy "Sân", lý do "Sân bảo trì" 4. Lưu khóa lại 5. Mở `/dat-san`, Bóng đá 5 người, cụm Thủ Đức, ngày T | Bước 2 bị chặn, liệt kê lượt của Phan Minh Đức; bước 3 lượt "Đã hủy", không tạo khoản hoàn (chưa cọc); bước 4 lưu được, lưới hiện vùng gạch chéo 17:00–21:00; bước 5 BD1 17:00–21:00 không chọn được |
| TC-04 | UC-02 | Khung giờ chồng, hở, đơn giá sai | Chủ sân | 1. Bảng giá → Sửa khung, đổi Trưa ngày thường thành 09:00–17:00, Lưu 2. Đổi lại 09:00–16:00, đổi Sáng thành 06:00–09:00, Lưu 3. Đổi lại 05:00–09:00, sửa đơn giá pickleball Chiều tối thành 205.000 ₫, Lưu | Bước 1 báo "Khung Trưa chồng khung Chiều tối 16:00–17:00"; bước 2 báo "Chưa có khung cho 05:00–06:00"; bước 3 báo "Đơn giá là bội số 10.000 ₫"; bảng giá không đổi |
| TC-05 | UC-02 | Thêm mặt hàng, đánh dấu tạm hết | Chủ sân, Nhân viên | 1. Chủ sân: Bảng giá → Dịch vụ bán kèm, thêm "Nước điện giải Pocari", nhóm Nước uống, đơn vị chai, 20.000 ₫ 2. Đổi sang Nhân viên, đánh dấu "Nước dừa" tạm hết 3. Mở hộp bán kèm của một lượt đang chơi bất kỳ | Bước 3 có "Nước điện giải Pocari 20.000 ₫"; "Nước dừa" hiện mờ, nhãn "Tạm hết", không chọn được |

### 2.2. Đặt sân tại quầy

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-06 | UC-03 | Đặt sân qua hai khung giá, thu cọc | Nhân viên | 1. Lịch sân, ngày T, kéo chọn PB3 15:30–17:00 2. Nhập 0909 111 222, tên "Nguyễn Văn Hùng" 3. Chọn "Thu cọc ngay" 130.000 ₫ tiền mặt, Lưu | Hộp hiện "15:30–16:00: 50.000 ₫, 16:00–17:00: 200.000 ₫", tiền sân 250.000 ₫, cọc tối thiểu 130.000 ₫ (125.000 ₫ làm tròn lên); lượt mã `DS{yyMMdd}{nnn}` "Đã xác nhận", cọc đã thu 130.000 ₫; khách mới được tạo |
| TC-07 | UC-03 | Trùng lượt, chạm mép | Nhân viên | 1. Ngày T, kéo chọn PB3 16:30–18:00 2. Đổi thành 17:00–18:30 3. Đóng hộp, không lưu | Bước 1 báo "Trùng lượt DS… 15:30–17:00", nút Lưu khóa; bước 2 hợp lệ, tiền sân 300.000 ₫, cọc tối thiểu 150.000 ₫ |
| TC-08 | UC-03 | Ngoài giờ, thời lượng sai | Nhân viên | 1. Ngày T, đặt PB3 bắt đầu 22:30, 60 phút 2. Bắt đầu 22:00, 90 phút 3. Mở danh sách thời lượng | Bước 1, 2 báo "Vượt giờ đóng cửa 23:00"; bước 3 chỉ có 60, 90, 120… tới 240 phút, không có 45 phút |
| TC-09 | UC-03 | Tiền cọc làm tròn lên | Nhân viên | 1. Ngày T, chọn BD1 08:00–09:30 2. Đóng hộp, không lưu | Tiền sân 350.000 ₫ (250.000 ₫ khung Sáng + 100.000 ₫ khung Trưa); cọc tối thiểu 180.000 ₫ (175.000 ₫ làm tròn lên) |
| TC-10 | UC-03 | Giá cuối tuần | Nhân viên | 1. Chọn ngày T+4, PB3 07:00–09:00 2. Đóng hộp, không lưu | Tiền sân 440.000 ₫ (2 giờ × 220.000 ₫), cọc tối thiểu 220.000 ₫ |
| TC-11 | UC-03 | Miễn cọc không đủ điều kiện, giữ chỗ chờ cọc | Nhân viên | 1. Ngày T, đặt PB3 06:00–07:00 cho 0909 111 222 2. Chọn "Miễn cọc" 3. Chọn "Giữ chỗ chờ cọc", giữ hạn mặc định, Lưu | Bước 2 lựa chọn bị khóa, chú thích "Chỉ miễn cọc khi giờ chơi trong 60 phút tới"; bước 3 lượt "Giữ chỗ", tiền sân 140.000 ₫, cọc tối thiểu 70.000 ₫, hạn cọc = thời điểm lưu + 24 giờ |
| TC-12 | UC-03 | Khách đang bị chặn đặt online | Nhân viên | 1. Mở hộp đặt sân, nhập 0938 222 333 2. Đóng hộp, không lưu | Hiện tên Lê Quốc Thịnh, cảnh báo đỏ "2 lần không đến trong 60 ngày, đang bị chặn đặt online"; nhân viên vẫn đặt được nếu thu cọc |

### 2.3. Đặt sân online, xác nhận cọc

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-13 | UC-04 | Đặt sân online | Khách | 1. Mở `/dat-san`, Pickleball, cụm Bình Thạnh, ngày T 2. Chọn PB3 19:00, 120 phút 3. Nhập "Trần Minh Khoa", 0912 345 678, bấm "Giữ sân" 4. Bấm "Tôi đã chuyển khoản" | Bước 1 ô PB3 15:30–17:00 hiện bận; bước 2 tiền sân 400.000 ₫, cọc 200.000 ₫; bước 3 lượt "Giữ chỗ", QR 200.000 ₫ nội dung là mã lượt, đồng hồ 15:00; bước 4 lượt "Chờ xác nhận cọc", hiện mã lượt và link tra cứu |
| TC-14 | UC-04 | Hết hạn giữ chỗ | Khách | 1. Đặt PB3 ngày T 21:00, 60 phút cho "Lâm Gia Huy" 0963 852 741, bấm "Giữ sân" 2. Không bấm chuyển khoản, chờ 16 phút | Bước 1 tiền sân 200.000 ₫, cọc 100.000 ₫; sau bước 2 lượt "Đã hủy", lý do "Hết hạn giữ chỗ"; ô PB3 ngày T 21:00–22:00 trống lại |
| TC-15 | UC-04 | Giới hạn mốc giờ và số điện thoại | Khách | 1. Chọn hôm nay, xem các mốc 2. Mở lịch chọn ngày 3. Đặt bằng 0938 222 333 4. Bằng 0912 345 678, giữ PB3 ngày T 05:00–06:00 5. Bằng 0912 345 678, giữ thêm một lượt bất kỳ | Bước 1 các mốc sớm hơn hiện tại + 60 phút không chọn được; bước 2 không chọn được ngày thứ 15 trở đi; bước 3 báo "Số điện thoại này tạm thời không đặt online được, vui lòng gọi sân"; bước 4 thành công (lượt "Giữ chỗ"); bước 5 báo "Bạn đang có 2 lượt chờ cọc, vui lòng hoàn tất trước" |
| TC-16 | UC-04 | Hai người cùng giữ một khung (chế độ `api`) | Khách | 1. Hai cửa sổ cùng chọn BD1 ngày T 06:00–07:30, nhập 0911 000 001 và 0911 000 002 2. Bấm "Giữ sân" ở hai cửa sổ gần như cùng lúc | Chỉ một lượt "Giữ chỗ" được tạo (tiền sân 375.000 ₫, cọc 190.000 ₫); cửa sổ còn lại báo "Khung giờ vừa có người đặt, vui lòng chọn giờ khác", lưới tải lại |
| TC-17 | UC-05 | Xác nhận cọc | Nhân viên | 1. Tổng quan → danh sách chờ xác nhận cọc, mở lượt của TC-13 2. Bấm "Đã nhận cọc" | Lượt "Đã xác nhận", cọc đã thu 200.000 ₫, phương thức chuyển khoản; lượt rời khỏi danh sách chờ xác nhận |
| TC-18 | UC-05 | Không nhận được tiền cọc | Khách, Nhân viên | 1. Khách đặt PB3 ngày T 08:00–09:00 cho "Phạm Thu Hà" 0905 678 901, bấm "Tôi đã chuyển khoản" 2. Nhân viên mở lượt, bấm "Chưa nhận được", lý do "Không thấy giao dịch" | Bước 1 tiền sân 140.000 ₫, cọc 70.000 ₫; bước 2 lượt "Đã hủy", không tạo khoản hoàn; ô PB3 ngày T 08:00–09:00 trống lại |
| TC-19 | UC-05 | Chờ xác nhận cọc quá 30 phút | Nhân viên | 1. Mở Tổng quan | Lượt Y1 của Trịnh Hải Yến nằm trong danh sách chờ xác nhận cọc, tô đỏ |

### 2.4. Đổi giờ, hủy, hoàn cọc

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-20 | UC-06 | Đổi giờ theo yêu cầu khách | Nhân viên | 1. Ngày T, kéo lượt của TC-06 (PB3 15:30–17:00) thả vào 10:00 cùng sân 2. Chọn bên yêu cầu "Khách", xác nhận | Hộp hiện tiền sân mới 150.000 ₫ (90 phút khung Trưa), chênh lệch −100.000 ₫, cọc giữ nguyên 130.000 ₫, dự kiến còn phải thu 20.000 ₫; lượt nằm ở 10:00–11:30, số lần đổi theo yêu cầu khách là 1 |
| TC-21 | UC-06 | Đổi lần hai; đổi khi còn dưới 6 giờ | Nhân viên | 1. Kéo lượt của TC-20 sang 11:00, bên yêu cầu "Khách" 2. Kéo lượt R2 (PB5 14:00 hôm nay) sang 15:00, bên yêu cầu "Khách" | Bước 1 bị từ chối "Mỗi lượt chỉ đổi theo yêu cầu khách 1 lần"; bước 2 bị từ chối "Khách chỉ đổi được khi còn ít nhất 6 giờ"; cả hai lượt về chỗ cũ |
| TC-22 | UC-06 | Hủy khi còn từ 24 giờ | Nhân viên | 1. Mở lượt của TC-13 (PB3 ngày T 19:00, cọc 200.000 ₫) 2. "Hủy lượt", bên hủy "Khách", lý do "Khách báo hủy", xác nhận | Hệ thống hiện "Hoàn 200.000 ₫ (100%)"; lượt "Đã hủy"; khoản hoàn `HC{yyMMdd}{nn}` 200.000 ₫ "Chờ hoàn"; ô PB3 ngày T 19:00–21:00 trống lại |
| TC-23 | UC-06 | Hủy khi còn dưới 6 giờ | Nhân viên | 1. Mở lượt R2 (PB5 14:00 hôm nay, cọc 50.000 ₫) 2. "Hủy lượt", bên hủy "Khách", xác nhận | Hệ thống hiện "Không hoàn cọc (hủy trước dưới 6 giờ)"; lượt "Đã hủy"; không tạo khoản hoàn; thu nhập cọc hôm nay tăng 50.000 ₫ |
| TC-24 | UC-06 | Sân hủy do thời tiết | Nhân viên | 1. Mở lượt R3 (BD2 16:00 hôm nay, cọc 300.000 ₫) 2. "Hủy lượt", bên hủy "Sân", lý do "Thời tiết", xác nhận | Hệ thống hiện "Hoàn 300.000 ₫ (100%)"; khoản hoàn 300.000 ₫ "Chờ hoàn" |
| TC-25 | UC-06 | Đánh dấu đã hoàn cọc | Nhân viên | 1. Tổng quan → "Hoàn cọc chờ chuyển", mở khoản 300.000 ₫ của TC-24, bấm "Đã hoàn" không nhập mã 2. Mở khoản 200.000 ₫ của TC-22, nhập mã "FT26285123456", bấm "Đã hoàn" | Bước 1 báo lỗi tại ô mã giao dịch; bước 2 khoản "Đã hoàn", rời khỏi danh sách; khoản 300.000 ₫ vẫn "Chờ hoàn" |
| TC-26 | UC-07 | Khách tự hủy khi còn 6–24 giờ | Khách | 1. Mở `/dat-san/tra-cuu`, nhập mã lượt R1 và 0977 222 445 2. Nhập lại đúng 0977 222 444 3. Bấm "Hủy lượt", xác nhận | Bước 1 báo "Không tìm thấy lượt đặt"; bước 2 hiện số điện thoại "0977 *** 444", dòng "Nếu hủy lúc này, bạn được hoàn 50.000 ₫"; bước 3 lượt "Đã hủy", khoản hoàn 50.000 ₫ "Chờ hoàn" hiện ở Tổng quan, thu nhập cọc tăng 50.000 ₫ |

### 2.5. Nhận sân, gia hạn, thanh toán

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-27 | UC-08 | Nhận sân | Nhân viên | 1. Tạo lượt BD3 hôm nay, bắt đầu ở mốc 30 phút hiện tại, 90 phút, khách "Ngô Đức Mạnh" 0903 456 789, thu cọc 230.000 ₫ tiền mặt 2. Bấm "Nhận sân" | Bước 1 tiền sân 450.000 ₫, cọc tối thiểu 230.000 ₫ (225.000 ₫ làm tròn lên), lượt "Đã xác nhận"; bước 2 lượt "Đang chơi", có giờ nhận sân, ô đổi màu xanh lá |
| TC-28 | UC-08 | Nhận sân quá sớm | Nhân viên | 1. Mở lượt của TC-20 (PB3 ngày T 10:00) | Nút "Nhận sân" khóa, chú thích "Nhận sân từ 09:30 ngày {ngày T}" |
| TC-29 | UC-08 | Ghi nhận không đến | Nhân viên, Khách | 1. Mở lượt N1 (PB4 hôm nay, đã quá giờ bắt đầu) 2. Bấm "Không đến", xác nhận 3. Khách mở `/dat-san`, đặt bằng 0908 333 444 | Bước 2 lượt "Không đến", ô của lượt trên lưới trống lại, thu nhập cọc tăng 50.000 ₫; bước 3 báo "Số điện thoại này tạm thời không đặt online được" (Đặng Văn Tú đủ 2 lần không đến trong 60 ngày) |
| TC-30 | UC-09 | Thanh toán có trừ cọc, chuyển khoản | Nhân viên | 1. Mở lượt của TC-27, "Bán kèm" 10 áo bib, 2 nước suối 2. Bấm "Thanh toán" 3. Chuyển khoản, bấm "Đã nhận tiền", "Hoàn tất" | Hộp thanh toán: tiền sân 450.000 ₫, bán kèm 70.000 ₫, tổng 520.000 ₫, cọc đã thu 230.000 ₫, còn phải thu 290.000 ₫; QR 290.000 ₫ nội dung là mã lượt; hóa đơn `HD{yyMMdd}{nnn}`; lượt "Hoàn thành"; bản in có tiền cọc đã trừ |
| TC-31 | UC-08 | Gia hạn giờ chơi | Nhân viên | 1. Tạo lượt CL2 hôm nay, bắt đầu ở mốc 30 phút hiện tại, 60 phút, khách "Tạ Quang Vinh" 0937 123 999, chọn "Miễn cọc" 2. "Nhận sân" 3. Bấm "Gia hạn" 30 phút, xác nhận | Bước 1 tiền sân 60.000 ₫, lượt "Đã xác nhận" không cọc; bước 3 giờ kết thúc lùi 30 phút, tiền sân 90.000 ₫ (thêm 30.000 ₫ khung Trưa) |
| TC-32 | UC-09 | Giảm vượt hạn mức, tiền không đủ | Nhân viên | 1. Lượt của TC-31: "Bán kèm" 2 Revive, 2 thuê vợt cầu lông, 1 quả cầu lông; thử chọn Nước dừa 2. "Thanh toán", giảm 15% 3. Đổi thành giảm 10% 4. Tiền mặt, nhập 150.000 ₫ | Bước 1 bán kèm 95.000 ₫, Nước dừa không chọn được; bước 2 báo "Nhân viên giảm tối đa 10% tiền sân (9.000 ₫)"; bước 3 giảm 9.000 ₫, tổng 176.000 ₫ (90.000 + 95.000 − 9.000), còn phải thu 176.000 ₫; bước 4 nút "Hoàn tất" khóa, hiện "Còn thiếu 26.000 ₫" |
| TC-33 | UC-09 | Thanh toán tiền mặt | Nhân viên | 1. Tiếp TC-32, nhập tiền khách đưa 200.000 ₫ 2. Hoàn tất | Tiền thối 24.000 ₫; hóa đơn tổng 176.000 ₫; lượt "Hoàn thành"; bản in tách tiền sân 60.000 ₫ và gia hạn 30.000 ₫ |

### 2.6. Đặt cố định

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-34 | UC-10 | Tạo lịch cố định có buổi trùng | Nhân viên | 1. Đặt cố định → Tạo lịch: khách "CLB Pickleball Bình Thạnh" 0918 765 432, PB3, Thứ Ba và Thứ Năm, 18:00–20:00, bắt đầu ngày T, 4 tuần 2. Xem danh sách buổi 3. Buổi T+2 chọn "Bỏ qua" 4. Thu cọc tiền mặt, Lưu | Bước 2 có 8 buổi, mỗi buổi 400.000 ₫ − 40.000 ₫ = 360.000 ₫ (buổi rơi vào ngày lễ đã khai báo thì 440.000 ₫ − 44.000 ₫ = 396.000 ₫); buổi T+2 tô đỏ do trùng lượt S1; cọc 360.000 ₫; bước 4 tạo lịch `CD{yyMMdd}{nn}` và 7 lượt con "Đã xác nhận" có biểu tượng lặp trên lưới |
| TC-35 | UC-10 | Hủy một buổi lẻ khi còn từ 24 giờ | Nhân viên | 1. Mở lượt con ngày T của lịch TC-34 2. "Hủy buổi", xác nhận | Buổi "Đã hủy", không phát sinh phí; lịch còn 6 buổi; cọc lịch cố định giữ nguyên 360.000 ₫ |

### 2.7. Tổng quan và báo cáo

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-36 | UC-11 | Doanh thu ghi nhận cập nhật | Chủ sân | 1. Mở Tổng quan 2. So với số đã ghi trước TC-23 | Doanh thu ghi nhận hôm nay tăng 846.000 ₫ (thu nhập cọc 50.000 + 50.000 + 50.000, lượt BD3 520.000, lượt CL2 176.000); danh sách "Hoàn cọc chờ chuyển" có khoản 300.000 ₫ của Hồ Văn Phúc và 50.000 ₫ của Vũ Hoàng Long, không còn khoản 200.000 ₫ của Trần Minh Khoa |
| TC-37 | UC-11 | Nhân viên không xem được báo cáo | Nhân viên | 1. Mở Tổng quan 2. Gõ URL `/reports` 3. Mở Bảng giá | Bước 1 không có nút "Xem báo cáo chi tiết"; bước 2 chuyển tới `/forbidden`; bước 3 chỉ xem được giá, không có nút sửa, chỉ có công tắc "Tạm hết" ở tab Dịch vụ bán kèm |
| TC-38 | UC-12 | Báo cáo doanh thu tách phần | Chủ sân | 1. Báo cáo → Doanh thu → Hôm nay 2. So với số đã ghi trước TC-23 | Tiền sân sau giảm giá tăng 531.000 ₫ (450.000 + 81.000); bán kèm tăng 165.000 ₫ (70.000 + 95.000); thu nhập cọc tăng 150.000 ₫ |

---

## 3. Biên bản chạy thử

| Ngày | Người test | Chế độ | Số TC đạt / tổng | Lỗi ghi nhận |
| :--- | :--- | :--- | :---: | :--- |
| | | | | |
