# 02 — User & Role Management

**Actor/Role:** Admin, Teacher, Parent

**Status:** ✅ 11 use cases / 11 APIs done

**Source of truth:** [UsersController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/UsersController.cs), [RolesController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/RolesController.cs), [UserService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/UserService.cs), [RoleService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/RoleService.cs)

---

## 2.1 Get List Users

**Diagrams:** [get-list-users.mmd](sequence-diagram/apis/get-list-users.mmd) · [get-list-users.class.mmd](sequence-diagram/classes/get-list-users.class.mmd)

**Trigger:** Admin truy cập trang danh sách tài khoản người dùng trên hệ thống.

**Summary:** Truy xuất danh sách người dùng phân trang từ cơ sở dữ liệu (chỉ lấy tài khoản hoạt động và chưa bị xóa mềm), bao gồm thông tin vai trò (Role).

**Known gaps found in source (if any):** None.

---

## 2.2 Get User By ID

**Diagrams:** [get-user-by-id.mmd](sequence-diagram/apis/get-user-by-id.mmd) · [get-user-by-id.class.mmd](sequence-diagram/classes/get-user-by-id.class.mmd)

**Trigger:** Người dùng xem thông tin cá nhân chi tiết.

**Summary:** Lấy thông tin chi tiết của một tài khoản theo mã ID định danh từ cơ sở dữ liệu.

**Known gaps found in source (if any):** None.

---

## 2.3 Create Account

**Diagrams:** [create-account.mmd](sequence-diagram/apis/create-account.mmd) · [create-account.class.mmd](sequence-diagram/classes/create-account.class.mmd)

**Trigger:** Admin điền thông tin để tạo tài khoản mới cho Giáo viên hoặc Phụ huynh.

**Summary:** Tạo tài khoản ở trạng thái chưa kích hoạt (`IsActive = false`), băm mật khẩu tạm thời tự sinh, tạo mã token xác thực gửi email kích hoạt và thông tin mật khẩu tạm thời cho người dùng.

**Known gaps found in source (if any):** None.

---

## 2.4 Update User Profile

**Diagrams:** [update-user-profile.mmd](sequence-diagram/apis/update-user-profile.mmd) · [update-user-profile.class.mmd](sequence-diagram/classes/update-user-profile.class.mmd)

**Trigger:** Người dùng thay đổi thông tin cá nhân (Avatar, tên, số điện thoại, giới tính, chuyên môn).

**Summary:** Kiểm tra trùng lặp email mới nếu có chỉnh sửa email, cập nhật các thuộc tính và lưu thay đổi vào cơ sở dữ liệu.

**Known gaps found in source (if any):** None.

---

## 2.5 Delete User (Lock)

**Diagrams:** [delete-user.mmd](sequence-diagram/apis/delete-user.mmd) · [delete-user.class.mmd](sequence-diagram/classes/delete-user.class.mmd)

**Trigger:** Admin thực hiện xóa tài khoản người dùng.

**Summary:** Thực hiện khóa và xóa mềm tài khoản bằng cách gán `IsDeleted = true` và `DeletedAt = DateTime.UtcNow`.

**Known gaps found in source (if any):** None.

---

## 2.6 Get Current User Children Profiles

**Diagrams:** [get-children-profiles.mmd](sequence-diagram/apis/get-children-profiles.mmd) · [get-children-profiles.class.mmd](sequence-diagram/classes/get-children-profiles.class.mmd)

**Trigger:** Phụ huynh truy cập xem danh sách hồ sơ các bé của mình.

**Summary:** Lấy thông tin tài khoản phụ huynh hiện tại cùng danh sách liên kết các ChildProfile tương ứng.

**Known gaps found in source (if any):** None.

---

## 2.7 Get List Roles

**Diagrams:** [get-list-roles.mmd](sequence-diagram/apis/get-list-roles.mmd) · [get-list-roles.class.mmd](sequence-diagram/classes/get-list-roles.class.mmd)

**Trigger:** Admin xem danh sách các vai trò trong hệ thống.

**Summary:** Truy xuất danh sách vai trò phân trang hoạt động và chưa bị xóa mềm từ database.

**Known gaps found in source (if any):** None.

---

## 2.8 Get Role By ID

**Diagrams:** [get-role-by-id.mmd](sequence-diagram/apis/get-role-by-id.mmd) · [get-role-by-id.class.mmd](sequence-diagram/classes/get-role-by-id.class.mmd)

**Trigger:** Admin xem chi tiết thông tin một vai trò.

**Summary:** Tìm kiếm và lấy thông tin vai trò theo ID.

**Known gaps found in source (if any):** None.

---

## 2.9 Create Role

**Diagrams:** [create-role.mmd](sequence-diagram/apis/create-role.mmd) · [create-role.class.mmd](sequence-diagram/classes/create-role.class.mmd)

**Trigger:** Admin nhập thông tin vai trò mới và tạo.

**Summary:** Kiểm tra trùng lặp vai trò theo tên, nếu hợp lệ thì thêm vai trò mới vào DB ở trạng thái hoạt động.

**Known gaps found in source (if any):** None.

---

## 2.10 Update Role

**Diagrams:** [update-role.mmd](sequence-diagram/apis/update-role.mmd) · [update-role.class.mmd](sequence-diagram/classes/update-role.class.mmd)

**Trigger:** Admin thay đổi mô tả hoặc cập nhật trạng thái hoạt động của vai trò.

**Summary:** Kiểm tra trùng lặp tên vai trò cập nhật, ghi nhận thay đổi và lưu vào DB.

**Known gaps found in source (if any):** None.

---

## 2.11 Delete Role

**Diagrams:** [delete-role.mmd](sequence-diagram/apis/delete-role.mmd) · [delete-role.class.mmd](sequence-diagram/classes/delete-role.class.mmd)

**Trigger:** Admin yêu cầu xóa một vai trò.

**Summary:** Thực hiện đánh dấu xóa mềm `IsDeleted = true` và `IsActive = false` cho vai trò.

**Known gaps found in source (if any):** None.
