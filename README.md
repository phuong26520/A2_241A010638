# A2_241A010638

## Thông tin sinh viên

- Họ tên: Nguyễn Hoài Phương
- MSSV: 241A010638
- Lớp: LTTTBDD
- Học phần: INT4211 – Lập trình trên các thiết bị di động
- Bài lab: Lab A2 – Xử lý sự kiện vòng đời, lưu trạng thái & Git/GitHub

## Giới thiệu
Ứng dụng là đồng hồ bấm giờ được viết bằng Java và XML trên Android. Ứng dụng có thể bắt đầu, tạm dừng và đặt lại thời gian. Thời gian được tính bằng `SystemClock.elapsedRealtime()` và giao diện được cập nhật định kỳ bằng `Handler`.

Ứng dụng cũng xử lý vòng đời của Activity và lưu trạng thái bằng `onSaveInstanceState`, vì vậy thời gian và trạng thái không bị mất khi xoay màn hình.

## Chức năng chính

- Bắt đầu đồng hồ bằng nút **Bắt đầu**.
- Tạm dừng đồng hồ bằng nút **Tạm dừng**.
- Đặt lại thời gian về `00:00.0` bằng nút **Đặt lại**.
- Hiển thị trạng thái đang chạy hoặc tạm dừng.
- Hiển thị số lần Activity được tạo lại.
- Ghi log các callback vòng đời Activity.
- Lưu và khôi phục thời gian, trạng thái đồng hồ và danh sách vòng khi Activity được tạo lại.

## Xử lý vòng đời

- `onResume`: bật lại việc cập nhật giao diện nếu đồng hồ đang chạy.
- `onPause`: dừng ticker để tránh tiếp tục cập nhật giao diện khi Activity không còn ở phía trước.
- `onStop`: xử lý tùy chọn tự động tạm dừng khi ứng dụng ra nền.
- `onDestroy`: luôn gỡ các callback của `Handler`.
- `onSaveInstanceState`: lưu trạng thái vào `Bundle`.
- `onCreate`: đọc lại trạng thái đã lưu khi Activity được tạo lại.

## Bài nâng cao

### NC1 – Nút Vòng (Lap)

Khi đồng hồ đang chạy hoặc đang tạm dừng, người dùng có thể bấm nút **Vòng** để lưu lại thời gian hiện tại. Các mốc thời gian được hiển thị thành danh sách bên dưới nút.

Danh sách vòng được lưu bằng `ArrayList<String>`. Trong `onSaveInstanceState`, danh sách được đưa vào `Bundle` bằng `putStringArrayList`. Khi Activity được tạo lại, danh sách được đọc lại bằng `getStringArrayList`, nên các mốc vòng vẫn còn sau khi xoay màn hình.

Khi bấm **Đặt lại**, thời gian và danh sách vòng được xóa.

### NC2 – Dừng khi ra nền

Ứng dụng có CheckBox **Dừng khi ra nền**. Khi CheckBox được chọn và Activity chuyển sang trạng thái dừng, phương thức `onStop()` sẽ gọi `pauseStopwatch()` để đồng hồ tự động tạm dừng.

Trạng thái của CheckBox cũng được lưu vào `Bundle` trong `onSaveInstanceState`. Khi Activity được tạo lại, CheckBox được khôi phục đúng trạng thái trước đó.

Nếu không chọn CheckBox, đồng hồ không tự động tạm dừng khi người dùng nhấn Home. Khi mở lại ứng dụng, thời gian vẫn được tính tiếp dựa trên mốc `SystemClock.elapsedRealtime()`.

## Tài nguyên và kỹ thuật sử dụng

- Java.
- XML layout.
- `Handler` và `Runnable` để cập nhật đồng hồ mỗi 100 ms.
- `SystemClock.elapsedRealtime()` để đo khoảng thời gian.
- `Bundle` để lưu trạng thái tạm thời.
- `LinearLayout` và `ScrollView` để bố trí giao diện và danh sách vòng.
- `res/values/strings.xml` để quản lý nội dung hiển thị.
- Đơn vị `dp` cho kích thước giao diện và `sp` cho cỡ chữ.

## Cách chạy

1. Mở thư mục project bằng Android Studio.
2. Chờ Gradle đồng bộ xong.
3. Chọn máy ảo hoặc thiết bị Android thật.
4. Nhấn **Run** để chạy ứng dụng.
5. Dùng Logcat với bộ lọc:

```text
tag:A2_241A010638
```

## Nội dung cần kiểm tra

- Bấm Bắt đầu, Tạm dừng và Đặt lại.
- Bấm Vòng để tạo nhiều mốc thời gian.
- Xoay màn hình và kiểm tra thời gian, trạng thái và danh sách vòng vẫn được giữ.
- Tick Dừng khi ra nền, bấm Bắt đầu rồi nhấn Home.
- Mở lại ứng dụng và kiểm tra đồng hồ đã tự động tạm dừng.
- Kiểm tra Logcat có các callback vòng đời và dòng xử lý NC2.

## Bằng chứng báo cáo

- Ảnh giao diện đồng hồ đang chạy.
- Ảnh danh sách các mốc Vòng.
- Ảnh sau khi xoay màn hình, chứng minh dữ liệu không bị mất.
- Ảnh CheckBox Dừng khi ra nền và trạng thái đồng hồ sau khi quay lại ứng dụng.
- Ảnh Logcat của kịch bản Activity được tạo lại và khôi phục trạng thái.
- Ảnh Git Log có ít nhất 3 commit.
- Ảnh repository GitHub ở chế độ Private.
