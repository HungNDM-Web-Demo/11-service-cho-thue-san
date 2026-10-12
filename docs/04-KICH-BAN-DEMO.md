# Kịch bản demo — Cho thuê Sân thể thao

> Dùng khi trình bày cho chủ sân pickleball, cầu lông, bóng đá mini. Thời lượng 12–15 phút. Đi theo một ngày của cụm sân: khách đặt online và chuyển cọc, nhân viên nhận đặt qua điện thoại, giữ sân cố định cho câu lạc bộ, xử lý hủy và trời mưa, giao sân, bán nước, thu tiền, chủ sân xem công suất.

---

## 1. Chuẩn bị trước buổi demo

- [ ] Mở sẵn link demo, thử "Đăng nhập nhanh" cả 3 vai trò
- [ ] Đặt lại dữ liệu demo (thanh công cụ demo → Đặt lại dữ liệu) để có lượt đặt 90 ngày qua và 14 ngày tới tính theo hôm nay
- [ ] Đổi tên sân, logo, màu theo thương hiệu khách (Cài đặt → Thương hiệu) nếu đã biết
- [ ] Mở tablet hoặc thu trình duyệt về 1280×800 để chiếu Lịch sân như ở quầy
- [ ] Chuẩn bị một điện thoại mở sẵn trang `/dat-san` (vai khách), một điện thoại có app ngân hàng để quét thử QR (chỉ để xem, không chuyển tiền)
- [ ] Ghi nhớ bảng giá mẫu: pickleball ngày thường Sáng 140.000 ₫, Trưa 100.000 ₫, Chiều tối 200.000 ₫ mỗi giờ, cuối tuần 220.000 ₫; bóng đá 5 người Chiều tối 400.000 ₫ mỗi giờ
- [ ] Mở trước Lịch sân hôm nay, tìm một lượt ngoài trời buổi chiều (để hủy do mưa ở bước 7) và một lượt đã quá giờ chưa nhận sân (bước 9)

| Link | Ghi chú |
| :--- | :--- |
| FE | `http://localhost:3111` hoặc link online |
| Trang đặt sân cho khách | `http://localhost:3111/dat-san` |
| Swagger | `https://localhost:7111/swagger` (khi khách hỏi về tích hợp) |

| Tài khoản | Vai trò | Dùng để cho xem |
| :--- | :--- | :--- |
| `admin` | Quản trị viên | Phân quyền, thương hiệu |
| `quanly` | Chủ sân | Tổng quan, sân, bảng giá, khóa bảo trì, báo cáo công suất |
| `nhanvien` | Nhân viên | Lịch sân, xác nhận cọc, đặt sân, đặt cố định, hủy và hoàn cọc, nhận sân, bán kèm, thanh toán |

Mật khẩu: giá trị `DEMO_PASSWORD` trong `.env`, hoặc bấm "Đăng nhập nhanh".

---

## 2. Câu chuyện demo

> Mở đầu: "Anh/chị hình dung hôm nay cụm sân mình đang chạy 10 sân, điện thoại và Zalo réo liên tục. Em đi đúng một ngày ở quầy để anh/chị thấy phần mềm đỡ cho mình chỗ nào."

| # | Vai trò | Thao tác | Điểm cần nhấn mạnh |
| :---: | :--- | :--- | :--- |
| 1 | Chủ sân | Đăng nhập, mở Tổng quan: công suất hôm nay, doanh thu ghi nhận, tiền cọc đang giữ, 3 danh sách việc cần làm | Ngồi ở nhà vẫn biết sân kín tới đâu, cọc đang giữ bao nhiêu, quầy còn việc gì chưa xử lý |
| 2 | Khách | Trên điện thoại mở trang đặt sân: chọn Pickleball, cụm Bình Thạnh, tối nay; thấy ô trống kèm giá; chọn PB2 19:00, 90 phút → tiền sân 300.000 ₫, cọc 150.000 ₫ (ngày thường; cuối tuần 330.000 ₫, cọc 170.000 ₫); nhập tên, số điện thoại; QR cọc và đồng hồ 15 phút hiện ra; bấm "Tôi đã chuyển khoản" | Khách tự xem sân trống, không phải nhắn hỏi "tối nay còn sân không"; sân được giữ 15 phút, không ai đặt chồng |
| 3 | Nhân viên | Đổi vai trò sang Nhân viên: lượt vừa đặt nằm trong "Chờ xác nhận cọc"; đối chiếu app ngân hàng, bấm "Đã nhận cọc"; xem tin xác nhận giả lập | Cọc vào là xác nhận một chạm; khách không chuyển thì 15 phút sau sân tự trống lại |
| 4 | Nhân viên | Khách gọi điện đặt bóng đá 5 người tối mai 18:00–19:30: kéo chọn ô trên Lịch sân → 600.000 ₫, cọc tối thiểu 300.000 ₫ (nếu mai là ngày thường); thử kéo sang ô đã có người → báo trùng; chọn "Giữ chỗ chờ cọc" 2 giờ | Không thể xếp trùng sân; khách hẹn chuyển cọc sau thì có hạn rõ ràng, quá hạn tự nhả sân |
| 5 | Nhân viên | Đặt pickleball 15:30–17:00 ngày thường: hệ thống tách 30 phút khung Trưa 50.000 ₫ và 60 phút khung Chiều tối 200.000 ₫, tổng 250.000 ₫ | Giá giờ cao điểm, cuối tuần, ngày lễ tự tính, nhân viên mới cũng không tính sai |
| 6 | Nhân viên | Câu lạc bộ xin sân cố định Thứ Ba, Thứ Năm 18:00–20:00 trong 8 tuần: hệ thống liệt kê 16 buổi, mỗi buổi 360.000 ₫ (giảm 10%), chỉ ra buổi bị trùng → chuyển sang sân bên cạnh; thu cọc 360.000 ₫ | Giữ sân cho khách quen cả tháng chỉ một lần thao tác; buổi trùng được phát hiện trước, không để hai nhóm cùng tới một sân |
| 7 | Nhân viên | Khách báo hủy lượt còn khoảng 10 giờ nữa: hệ thống tự tính hoàn 50% cọc; trời đổ mưa: hủy lượt sân ngoài trời chiều nay, chọn "Thời tiết" → hoàn 100%; khoản hoàn hiện trong "Hoàn cọc chờ chuyển", chuyển xong bấm "Đã hoàn" | Chính sách hoàn cọc áp tự động, không cãi nhau với khách; khoản nào chưa trả lại khách đều nằm trong danh sách |
| 8 | Nhân viên | Đội bóng tới: bấm "Nhận sân"; bán 10 áo bib, 6 chai nước; đội xin đá thêm 30 phút → "Gia hạn"; chơi xong bấm "Thanh toán": tiền sân, bán kèm, trừ cọc, còn phải thu; chuyển khoản QR, in hóa đơn | Nước, áo bib, giờ đá thêm đều vào một hóa đơn; tiền cọc tự trừ, không thu thiếu, không thu trùng |
| 9 | Nhân viên | Một lượt quá giờ 15 phút khách chưa tới: bấm "Không đến" → giữ cọc, phần giờ còn lại trên sân trống để bán cho khách vãng lai đang chờ | Sân không bị bỏ trống vô ích; khách hay bỏ sân 2 lần trong 60 ngày tự bị chặn đặt online |
| 10 | Chủ sân | Đổi sang Chủ sân, mở Bảng giá: tăng giá khung Chiều tối cuối tuần, thêm ngày lễ 01/01 áp giá cuối tuần; khóa sân PB4 sáng mai để thay lưới | Đổi giá một chỗ, mọi lượt đặt mới áp ngay; khóa bảo trì báo ngay lượt nào bị ảnh hưởng |
| 11 | Chủ sân | Mở Báo cáo, tab Công suất: bảng nhiệt giờ × thứ cho thấy 5:00–7:00 và 17:00–21:00 kín, 10:00–15:00 vắng; tab Doanh thu tách tiền sân, bán kèm, thu nhập cọc | Biết sân nào, giờ nào đang lãng phí để làm giá giờ vàng hoặc khuyến mãi khung trưa |
| 12 | Quản trị viên | Đổi sang Quản trị viên, bỏ quyền "Hủy lượt đặt" của vai trò Nhân viên, đổi sang Nhân viên thấy nút hủy biến mất; đổi màu thương hiệu | Phân quyền tới từng nút; giao diện mang thương hiệu của sân |

> Kết: "Toàn bộ dữ liệu anh/chị vừa thấy là dữ liệu mẫu. Bản triển khai thật sẽ nhập sân, bảng giá, chính sách cọc của sân mình, gắn link đặt sân vào nhóm Zalo, Facebook của sân."

---

## 3. Câu hỏi khách hay hỏi

| Câu hỏi | Trả lời gợi ý |
| :--- | :--- |
| Có tự xác nhận khi khách chuyển cọc không, khỏi phải dò app ngân hàng? | Demo để nhân viên bấm xác nhận. Bản triển khai nối dịch vụ báo biến động số dư (webhook ngân hàng) hoặc cổng VNPay, MoMo để tự xác nhận khi tiền về. |
| Pickleball bên em có đánh vãng lai, xé vé theo người, có làm được không? | Demo tính tiền theo sân. Bản triển khai thêm "buổi chơi ghép": mở khung giờ, bán vé theo người, đủ người thì ghép sân. |
| Có thẻ thành viên, gói 10 giờ trả trước không? | Demo chưa có. Làm được khi triển khai: khách mua gói giờ, mỗi lượt trừ dần, tự báo khi sắp hết. |
| Chính sách cọc, hoàn cọc bên em khác thì sao? | Mức cọc, các mốc hoàn (24 giờ, 6 giờ) và tỉ lệ hoàn là cấu hình; bản triển khai chỉnh theo chính sách của sân. |
| Trời mưa thì xử lý thế nào? | Hủy với lý do "Thời tiết" thì hoàn 100% cọc, hoặc đổi sang sân trong nhà, giờ khác không tính lần đổi của khách. |
| Có nhiều cụm sân, mỗi cụm một quầy được không? | Có, demo đang chạy 2 cụm. Bản triển khai có thể giới hạn mỗi nhân viên chỉ thấy cụm của mình. |
| Có quản lý kho nước, số vợt cho thuê không? | Demo chỉ có trạng thái còn bán, tạm hết. Có sẵn demo Quản lý kho; bản triển khai trừ kho khi bán và đếm số vợt đang cho thuê. |
| Có bật tắt đèn sân theo lịch đặt không? | Cần khảo sát thiết bị. Có thể nối công tắc thông minh để tự bật đèn 5 phút trước giờ chơi và tắt khi hết giờ. |
| Có gửi tin Zalo nhắc khách trước giờ chơi không? | Demo ghi tin giả lập vào nhật ký. Bản triển khai nối Zalo ZNS hoặc SMS brandname, phí theo tin. |
| Nhân viên có xem được doanh thu không? | Nhân viên thấy Tổng quan trong ngày để làm việc, không xem được báo cáo nếu chủ sân không cấp quyền. |

---

## 4. Sau buổi demo

- [ ] Ghi lại yêu cầu khách nêu thêm vào `01-TONG-QUAN-NGHIEP-VU.md`
- [ ] Ghi lại số cụm, số sân từng loại, bảng giá và chính sách cọc, hoàn cọc hiện tại của sân
- [ ] Ghi lại kênh khách đặt sân nhiều nhất (điện thoại, Zalo, nhóm Facebook) và ngân hàng sân đang dùng để nhận cọc
- [ ] Gửi link demo, link `/dat-san` và tài khoản `nhanvien`, `quanly` cho khách tự trải nghiệm (nếu đồng ý)
