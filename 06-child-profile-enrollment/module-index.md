# 06 — Child Profile & Enrollment

**Actor/Role:** Admin, Teacher, Parent, Child

**Status:** ✅ 14 use cases / 14 APIs done

**Source of truth:** [ChildProfilesController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/ChildProfilesController.cs), [EnrollmentsController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/EnrollmentsController.cs), [ChildProfileService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/ChildProfileService.cs), [EnrollmentService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/EnrollmentService.cs)

---

## 6.1 Get List Child Profiles

**Diagrams:** [get-list-child-profiles.mmd](sequence-diagram/apis/get-list-child-profiles.mmd) · [get-list-child-profiles.class.mmd](sequence-diagram/classes/get-list-child-profiles.class.mmd)

**Trigger:** Admin hoặc Giáo viên xem danh sách học sinh trên hệ thống.

**Summary:** Truy xuất danh sách hồ sơ học sinh phân trang chưa bị xóa mềm từ cơ sở dữ liệu.

**Known gaps found in source (if any):** None.

---

## 6.2 Get Child Profile By ID

**Diagrams:** [get-child-profile-by-id.mmd](sequence-diagram/apis/get-child-profile-by-id.mmd) · [get-child-profile-by-id.class.mmd](sequence-diagram/classes/get-child-profile-by-id.class.mmd)

**Trigger:** Người dùng xem hồ sơ chi tiết của một bé.

**Summary:** Lấy chi tiết thông tin hồ sơ của một học sinh theo ID.

**Known gaps found in source (if any):** None.

---

## 6.3 Get My Children Profiles

**Diagrams:** [get-my-children-profiles.mmd](sequence-diagram/apis/get-my-children-profiles.mmd) · [get-my-children-profiles.class.mmd](sequence-diagram/classes/get-my-children-profiles.class.mmd)

**Trigger:** Phụ huynh đăng nhập dashboard xem danh sách các bé của mình hoặc kính VR Client lấy danh sách trẻ để chọn tài khoản chơi bài tập.

**Summary:** Lấy toàn bộ danh sách hồ sơ trẻ liên kết với parentId (được lấy từ Claims tài khoản phụ huynh đang đăng nhập).

**Known gaps found in source (if any):** None.

---

## 6.4 Create Child Profile

**Diagrams:** [create-child-profile.mmd](sequence-diagram/apis/create-child-profile.mmd) · [create-child-profile.class.mmd](sequence-diagram/classes/create-child-profile.class.mmd)

**Trigger:** Phụ huynh, Giáo viên hoặc Admin thêm mới hồ sơ của bé.

**Summary:** Xác thực tài khoản phụ huynh liên kết (UserId) phải tồn tại và đang hoạt động, sau đó tạo hồ sơ và lưu vào cơ sở dữ liệu.

**Known gaps found in source (if any):** Ràng buộc kiểm tra UserId phụ huynh được kiểm tra ở Service trước khi thêm hồ sơ.

---

## 6.5 Update Child Profile

**Diagrams:** [update-child-profile.mmd](sequence-diagram/apis/update-child-profile.mmd) · [update-child-profile.class.mmd](sequence-diagram/classes/update-child-profile.class.mmd)

**Trigger:** Người dùng chỉnh sửa thông tin hồ sơ trẻ (Avatar, họ tên, tuổi, giới tính, trình độ học tập, ghi chú).

**Summary:** Kiểm tra sự tồn tại của hồ sơ học sinh, nếu có yêu cầu đổi phụ huynh (UserId) thì xác thực tài khoản phụ huynh mới, sau đó tiến hành lưu thông tin cập nhật.

**Known gaps found in source (if any):** None.

---

## 6.6 Delete Child Profile

**Diagrams:** [delete-child-profile.mmd](sequence-diagram/apis/delete-child-profile.mmd) · [delete-child-profile.class.mmd](sequence-diagram/classes/delete-child-profile.class.mmd)

**Trigger:** Admin thực hiện yêu cầu xóa hồ sơ học sinh.

**Summary:** Đánh dấu xóa mềm hồ sơ trẻ (`IsDeleted = true`, `DeletedAt = DateTime.UtcNow`).

**Known gaps found in source (if any):** None.

---

## 6.7 Get List Enrollments

**Diagrams:** [get-list-enrollments.mmd](sequence-diagram/apis/get-list-enrollments.mmd) · [get-list-enrollments.class.mmd](sequence-diagram/classes/get-list-enrollments.class.mmd)

**Trigger:** Người dùng truy cập xem danh sách ghi danh xếp lớp của học sinh.

**Summary:** Lấy danh sách ghi danh cùng thông tin chi tiết liên kết (Trẻ, lớp học, giáo viên, học kỳ) và lọc theo trạng thái, lớp học hoặc trình độ học tập.

**Known gaps found in source (if any):** Thực hiện lọc và phân trang trong bộ nhớ RAM sau khi truy xuất toàn bộ dữ liệu (cần lưu ý tối ưu hóa hiệu năng khi dữ liệu lớn).

---

## 6.8 Get Enrollment By ID

**Diagrams:** [get-enrollment-by-id.mmd](sequence-diagram/apis/get-enrollment-by-id.mmd) · [get-enrollment-by-id.class.mmd](sequence-diagram/classes/get-enrollment-by-id.class.mmd)

**Trigger:** Xem chi tiết một bản ghi ghi danh xếp lớp.

**Summary:** Tìm kiếm thông tin ghi danh cùng đầy đủ các mối liên kết kèm theo theo ID định danh.

**Known gaps found in source (if any):** None.

---

## 6.9 Get Enrollments By Child ID

**Diagrams:** [get-enrollments-by-child.mmd](sequence-diagram/apis/get-enrollments-by-child.mmd) · [get-enrollments-by-child.class.mmd](sequence-diagram/classes/get-enrollments-by-child.class.mmd)

**Trigger:** Người dùng xem lịch sử học tập/ghi danh lớp học của một bé cụ thể.

**Summary:** Truy xuất toàn bộ các ghi danh chưa bị xóa mềm của một bé chỉ định.

**Known gaps found in source (if any):** Lọc trong bộ nhớ RAM sau khi lấy toàn bộ danh sách chi tiết.

---

## 6.10 Create Enrollment (Đăng ký xếp lớp)

**Diagrams:** [create-enrollment.mmd](sequence-diagram/apis/create-enrollment.mmd) · [create-enrollment.class.mmd](sequence-diagram/classes/create-enrollment.class.mmd)

**Trigger:** Admin hoặc Giáo viên tạo yêu cầu xếp lớp cho trẻ.

**Summary:** Xác thực trạng thái hợp lệ, hồ sơ trẻ, sự tồn tại và trạng thái hoạt động của lớp học. Giáo viên chỉ được đăng ký học sinh vào lớp học do mình phụ trách. Chặn đăng ký trùng lặp nếu trẻ đã có ghi danh Active trong lớp này.

**Known gaps found in source (if any):** Ràng buộc giáo viên chỉ được thao tác trên lớp của mình được kiểm tra dựa trên Claims gửi lên.

---

## 6.11 Update Enrollment

**Diagrams:** [update-enrollment.mmd](sequence-diagram/apis/update-enrollment.mmd) · [update-enrollment.class.mmd](sequence-diagram/classes/update-enrollment.class.mmd)

**Trigger:** Admin hoặc Giáo viên chỉnh sửa thông tin ghi danh (ngày ghi danh, trạng thái, chuyển học sinh).

**Summary:** Xác thực thông tin lớp học, cấm Giáo viên sửa ghi danh lớp của giáo viên khác. Nếu thay đổi học sinh hoặc lớp học, kiểm tra trùng lặp ghi danh hoạt động khác.

**Known gaps found in source (if any):** None.

---

## 6.12 Delete Enrollment

**Diagrams:** [delete-enrollment.mmd](sequence-diagram/apis/delete-enrollment.mmd) · [delete-enrollment.class.mmd](sequence-diagram/classes/delete-enrollment.class.mmd)

**Trigger:** Admin hủy bỏ/xóa bản ghi ghi danh của học sinh.

**Summary:** Thực hiện xóa mềm bản ghi ghi danh.

**Known gaps found in source (if any):** None.

---

## 6.13 Transfer Class (Chuyển lớp học)

**Diagrams:** [transfer-class.mmd](sequence-diagram/apis/transfer-class.mmd) · [transfer-class.class.mmd](sequence-diagram/classes/transfer-class.class.mmd)

**Trigger:** Giáo viên hoặc Admin yêu cầu chuyển học sinh sang lớp học mới cùng trình độ.

**Summary:** Chỉ cho phép chuyển lớp đối với ghi danh đang ở trạng thái Active. Lớp học mới phải đang hoạt động và không trùng lặp ghi danh Active khác của trẻ. Giáo viên chỉ được chuyển học sinh sang lớp do mình sở hữu.

**Known gaps found in source (if any):** Nghiệp vụ chuyển lớp cập nhật trực tiếp ClassId của thực thể Enrollment hiện tại.

---

## 6.14 Approve Enrollment (Duyệt xếp lớp)

**Diagrams:** [approve-enrollment.mmd](sequence-diagram/apis/approve-enrollment.mmd) · [approve-enrollment.class.mmd](sequence-diagram/classes/approve-enrollment.class.mmd)

**Trigger:** Admin hoặc Giáo viên phụ trách lớp duyệt yêu cầu đăng ký xếp lớp của trẻ.

**Summary:** Kiểm tra ghi danh đang ở trạng thái Pending. Nếu giáo viên duyệt, bắt buộc lớp học thuộc quyền quản lý của giáo viên đó. Chuyển trạng thái ghi danh thành Active.

**Known gaps found in source (if any):** None.
