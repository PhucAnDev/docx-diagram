# 01 — Authentication & Session Management

**Actor/Role:** Admin, Teacher, Parent, Child

**Status:** ✅ 7 use cases / 7 APIs done

**Source of truth:** [AuthController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/AuthController.cs), [AuthService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Infrastructure/Core/AuthService.cs)

---

## 1.1 Login

**Diagrams:** [login.mmd](sequence-diagram/apis/login.mmd) · [login.class.mmd](sequence-diagram/classes/login.class.mmd)

**Trigger:** Người dùng nhập email và mật khẩu, nhấn Đăng nhập trên UI.

**Summary:** Xác thực thông tin đăng nhập của người dùng qua email và hash mật khẩu BCrypt, nếu thành công thì tạo Access Token (JWT) và Refresh Token (lưu vào Redis cache).

**Known gaps found in source (if any):** None.

---

## 1.2 Refresh Token

**Diagrams:** [refresh-token.mmd](sequence-diagram/apis/refresh-token.mmd) · [refresh-token.class.mmd](sequence-diagram/classes/refresh-token.class.mmd)

**Trigger:** Ứng dụng client gửi yêu cầu cấp lại Access Token khi Token cũ hết hạn.

**Summary:** Kiểm tra tính hợp lệ của Refresh Token từ client đối chiếu với giá trị lưu trong Redis, nếu khớp sẽ cấp mới một cặp Access Token và Refresh Token mới.

**Known gaps found in source (if any):** None.

---

## 1.3 Forgot Password

**Diagrams:** [forgot-password.mmd](sequence-diagram/apis/forgot-password.mmd) · [forgot-password.class.mmd](sequence-diagram/classes/forgot-password.class.mmd)

**Trigger:** Người dùng nhập email và yêu cầu đặt lại mật khẩu.

**Summary:** Hệ thống kiểm tra email tồn tại, sinh mã OTP ngẫu nhiên lưu vào Redis cache và gửi qua email cho người dùng.

**Known gaps found in source (if any):** None.

---

## 1.4 Verify OTP

**Diagrams:** [verify-otp.mmd](sequence-diagram/apis/verify-otp.mmd) · [verify-otp.class.mmd](sequence-diagram/classes/verify-otp.class.mmd)

**Trigger:** Người dùng nhập mã OTP từ email để xác thực.

**Summary:** Hệ thống kiểm tra mã OTP nhập vào có khớp với mã OTP được lưu trong Redis cache của email tương ứng hay không.

**Known gaps found in source (if any):** None.

---

## 1.5 Reset Password

**Diagrams:** [reset-password.mmd](sequence-diagram/apis/reset-password.mmd) · [reset-password.class.mmd](sequence-diagram/classes/reset-password.class.mmd)

**Trigger:** Người dùng nhập mật khẩu mới và mã OTP để đổi mật khẩu.

**Summary:** Xác thực mã OTP, xóa OTP khỏi cache, băm mật khẩu mới bằng BCrypt và cập nhật cột PasswordHash của người dùng trong Database.

**Known gaps found in source (if any):** None.

---

## 1.6 Change Password

**Diagrams:** [change-password.mmd](sequence-diagram/apis/change-password.mmd) · [change-password.class.mmd](sequence-diagram/classes/change-password.class.mmd)

**Trigger:** Người dùng điền mật khẩu hiện tại và mật khẩu mới trong phần cài đặt tài khoản.

**Summary:** Hệ thống kiểm tra mật khẩu hiện tại, băm mật khẩu mới và cập nhật lại thông tin PasswordHash của người dùng.

**Known gaps found in source (if any):** None.

---

## 1.7 Verify Email

**Diagrams:** [verify-email.mmd](sequence-diagram/apis/verify-email.mmd) · [verify-email.class.mmd](sequence-diagram/classes/verify-email.class.mmd)

**Trigger:** Người dùng nhấp vào đường link xác thực email trong hộp thư.

**Summary:** Hệ thống kiểm tra token xác thực gửi lên, nếu khớp và còn hạn thì cập nhật trạng thái IsEmailVerified = true và IsActive = true cho tài khoản.

**Known gaps found in source (if any):** Xử lý đặc biệt khi token giải mã URL chứa ký tự khoảng trắng được thay thế bằng dấu cộng `+` để khắc phục lỗi phân tách chuỗi từ client.
