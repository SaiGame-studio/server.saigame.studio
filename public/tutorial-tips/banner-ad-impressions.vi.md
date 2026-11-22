Quảng cáo banner được tính tiền theo **lượt hiển thị (impression)**, mỗi lần một quảng cáo hiện ra, chứ không theo thời gian nó nằm trên màn hình. Giữ người chơi ở một màn hình lâu hơn không làm banner kiếm được nhiều tiền hơn.

## Banner được tính như thế nào

- Một impression được tính khi quảng cáo hiện ra và SDK quảng cáo báo về. Nhiều mạng quảng cáo còn yêu cầu quảng cáo phải **xem được (viewable)**: ít nhất 50% diện tích banner nằm trên màn hình trong khoảng 1 giây liên tục.
- Doanh thu xấp xỉ bằng **số impression × eCPM** (tiền kiếm được trên 1.000 impression). Banner hiện 1 giây hay 10 giây đều chỉ tính là một impression.
- Banner **tự làm mới**, thường mỗi 30 đến 60 giây, chỉnh trong dashboard mediation của bạn. Mỗi lần làm mới là một quảng cáo mới và được tính thêm một impression.

## Đừng giữ người chơi lại chỉ để xem banner

Bắt người chơi chờ, ví dụ ở một màn hình sau khi đăng nhập, chỉ để hiện banner sẽ:

- không thêm doanh thu, trừ khi banner kịp làm mới trong lúc chờ,
- làm game có cảm giác chậm, người chơi có thể bỏ đi,
- có thể vi phạm chính sách của mạng quảng cáo. Một số mạng, như Google AdMob, hạn chế quảng cáo ở màn hình loading hoặc màn hình chờ mà người chơi không có gì để làm. Điều này có thể làm giảm giá trị quảng cáo hoặc khiến tài khoản của bạn bị cảnh báo.

## Cách làm tốt hơn

1. Hiện banner ngay khi màn hình mở ra, ví dụ ngay sau khi đăng nhập thành công.
2. Chờ tới khi SDK quảng cáo báo banner đã hiện, cộng thêm khoảng 1 giây để impression đạt chuẩn viewable.
3. Đặt thời gian chờ tối đa, ví dụ 3 giây. Nếu banner load chậm hoặc không có quảng cáo thì vẫn cho vào game.

Hãy đặt banner ở những màn hình người chơi vốn đã ở lâu, như menu hoặc màn hình kết quả, thay vì tạo thêm màn hình chờ cho banner.
