# Tài Xỉu / Chẵn Lẻ / Bầu Cua — server mới

Bản này được tạo dựa trên `server.js` cũ bạn cung cấp, giữ giao thức Socket.IO `ducnghia` và hai endpoint PHP cũ:

- `POST {PHP_BASE_URL}/websocket/game.html` với `getgame=true`
- `POST {PHP_BASE_URL}/websocket/socket.io.html` để gửi kết quả

## Cấu hình

1. Sao chép `.env.example` thành `.env` (không commit `.env`).
2. Đặt `PHP_BASE_URL` là URL website PHP.
3. Đặt `GAME_KEYCODE` trùng với khóa mà PHP kiểm tra. Không dùng giá trị mẫu.
4. Đặt `ADMIN_TOKEN` thành chuỗi ngẫu nhiên dài và cập nhật client quản trị để gửi token cùng event `admin`.
5. `ALLOWED_ORIGINS` phải khớp origin của website, không thêm dấu `/` ở cuối là tốt nhất.
6. Chạy `npm install` rồi `npm start`. Kiểm tra `/health`.

## Lưu ý quan trọng

- Server này không thay thế PHP/MySQL. Nó vẫn cần endpoint PHP và database tương thích với source cũ.
- Nếu PHP không có route `.html` như trên, phải sửa URL endpoint cho đúng rewrite thực tế.
- Đã thêm kiểm tra lỗi HTTP/JSON, health check, origin allowlist và sửa vòng lặp dùng chung. Quyền admin bị khóa mặc định nếu chưa có `ADMIN_TOKEN`; client quản trị cũ cần được cập nhật để truyền token.
- Không đưa mật khẩu MySQL, token, file `.env` hoặc log chứa thông tin cá nhân lên GitHub.
- Đây là bản chuyển đổi mã nguồn, chưa được kiểm thử end-to-end với database thực tế.
