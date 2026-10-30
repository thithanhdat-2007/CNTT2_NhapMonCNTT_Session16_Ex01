# Bài tập Session 16 – Ex01: Quy trình lưu trữ lai cho dự án Số hóa Bảo tàng PTIT

Họ và tên: Thi Thành Đạt  
MSSV: N26DTCN041  
Lớp: CNTT2  
Môn học: Nhập môn Công nghệ thông tin  
Email: thithanhdat111@gmail.com

## 1. Phân tích sự cố và giải pháp

Bạn A chỉ giữ bản thiết kế 3D trên ổ cứng máy mình. Khi ổ bị bad sector, bản đang làm bị hỏng; bản nén gửi qua Zalo cũng không còn tải được. Vì vậy, Zalo không thể thay thế nơi lưu trữ dự án và bản sao lưu.

Em đề xuất dùng Google Drive for desktop ở chế độ **Mirror files**. Khi đó, thư mục dự án có một bản trên SSD để mở và chỉnh sửa bằng phần mềm thiết kế 3D, đồng thời có một bản trên Google Drive. Sau mỗi lần nhấn **Ctrl + S**, phần mềm lưu file vào thư mục trên SSD; ứng dụng Drive tự phát hiện thay đổi và tải bản mới lên Cloud khi có Internet. Cả nhóm cần nhìn trạng thái đồng bộ hoàn tất trước khi coi bản trên Cloud là bản mới nhất.

Sơ đồ luồng dữ liệu:

```text
Phần mềm thiết kế 3D
        │  Ctrl + S
        ▼
Thư mục dự án trên Local SSD (bản làm việc)
        │  Google Drive for desktop tự đồng bộ khi có mạng
        ▼
Google Drive (bản trên Cloud và các phiên bản đã lưu)
        │  Khi SSD hỏng: tải bản đã đồng bộ về máy khác
        ▼
Tiếp tục công việc từ phiên bản còn dùng được
```

Lưu ý: Ctrl + S lưu xuống SSD trước, **không bảo đảm file đã xuất hiện tức thời trên Cloud**. Thời gian tải lên còn phụ thuộc dung lượng bản vẽ, mạng Internet và trạng thái ứng dụng đồng bộ.

## 2. Mất mạng, sập nguồn và xung đột phiên bản

Nếu mất Internet, bạn A vẫn làm việc trên bản được lưu ở SSD. Các thay đổi chưa tải lên sẽ chờ đồng bộ khi máy kết nối lại; không xóa hoặc di chuyển thư mục trong lúc chờ. Nếu máy sập nguồn, sau khi khởi động lại cần mở file kiểm tra lần lưu cuối, mở Drive for desktop và chờ thông báo đồng bộ hoàn tất. Sau đó, kiểm tra trên Google Drive rằng file mới nhất đã có mặt. Nếu SSD hỏng **trước khi tải lên xong**, phần chưa đồng bộ có thể mất; vì thế cần lưu thường xuyên và kiểm tra trạng thái đồng bộ sau mỗi buổi làm việc. Với bản vẽ quan trọng, nhóm giữ thêm một bản sao độc lập vào những mốc đã thống nhất.

File thiết kế 3D thường không tự ghép được các thay đổi của hai người. Nếu hai người cùng sửa một file, nhất là khi một người đang offline, có thể xuất hiện hai bản khác nhau hoặc bản xung đột. Nhóm **giữ cả hai bản**, so sánh thời gian và nội dung bằng phần mềm thiết kế, rồi thống nhất bản ổn định để dùng tiếp; không xóa bản còn lại trước khi kiểm tra. Để tránh lặp lại, mỗi thời điểm chỉ một người phụ trách sửa file gốc và người đó báo cả nhóm sau khi đồng bộ xong.

## 3. Khôi phục bằng lịch sử phiên bản

Khi bản hiện tại bị lỗi nhưng bản tốt đã từng được đồng bộ, em vào Google Drive trên web, chọn file thiết kế 3D rồi mở **File information → Manage versions**. Em xem thời điểm các phiên bản, tải bản ổn định về máy và mở thử bằng phần mềm thiết kế. Sau khi xác nhận bản đó dùng được, em lưu nó làm bản làm việc mới và chờ đồng bộ; bản lỗi vẫn được giữ lại cho tới khi việc khôi phục được kiểm tra xong. Với các mốc quan trọng, có thể chọn **Keep forever** để tránh phiên bản cũ bị dọn tự động.

Lịch sử phiên bản chỉ khôi phục được **những phiên bản đã lên Cloud**. Nó không thể lấy lại phần mới sửa đang nằm duy nhất trên chiếc SSD đã hỏng.

## 4. Ba bước thiết lập đồng bộ cho Designer

1. Cài Google Drive for desktop, đăng nhập tài khoản được nhóm cấp quyền và tạo thư mục `SoHoa_BaoTang_PTIT/ThietKe3D` trong My Drive.
2. Trong **Preferences → Google Drive**, chọn **Mirror files** và chọn vị trí lưu trên SSD còn đủ dung lượng. Đặt thư mục đã đồng bộ này làm nơi mở và lưu file của phần mềm thiết kế 3D.
3. Chuyển bản thiết kế vào thư mục đó, nhấn **Ctrl + S** để thử, đợi Drive báo đồng bộ hoàn tất rồi mở Google Drive trên web để kiểm tra file. Sau này làm việc ngay trong thư mục này và kiểm tra lại trạng thái đồng bộ khi vừa có mạng trở lại.

Kết luận: Quy trình lưu trên SSD và tự đồng bộ lên Cloud giúp nhóm tiếp tục làm việc khi mất mạng, có bản trên Cloud khi máy hỏng và có thể quay về phiên bản ổn định đã đồng bộ. Điều kiện quan trọng là phải kiểm tra việc tải lên đã hoàn tất.

