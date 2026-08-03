# 03 — Classroom Management

**Actor/Role:** Admin, Teacher, Parent

**Status:** ✅ 6 use cases / 6 APIs done

**Source of truth:** [ClassroomsController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/ClassroomsController.cs), [ClassroomService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/ClassroomService.cs)

---

## 3.1 Get List Classrooms

**Diagrams:** [get-list-classrooms.mmd](sequence-diagram/apis/get-list-classrooms.mmd) · [get-list-classrooms.class.mmd](sequence-diagram/classes/get-list-classrooms.class.mmd)

**Trigger:** Người dùng truy cập danh sách các lớp học hiện có trên dashboard.

**Summary:** Lấy thông tin phân trang của các lớp học chưa bị xóa mềm, bao gồm thông tin chi tiết về giáo viên phụ trách, chương trình học áp dụng, học kỳ liên kết và số lượng học sinh ghi danh.

**Known gaps found in source (if any):** None.

---

## 3.2 Get Classroom By ID

**Diagrams:** [get-classroom-by-id.mmd](sequence-diagram/apis/get-classroom-by-id.mmd) · [get-classroom-by-id.class.mmd](sequence-diagram/classes/get-classroom-by-id.class.mmd)

**Trigger:** Người dùng nhấp chọn xem chi tiết một lớp học cụ thể.

**Summary:** Truy xuất thông tin chi tiết của một lớp học dựa trên ID chỉ định.

**Known gaps found in source (if any):** None.

---

## 3.3 Create Classroom

**Diagrams:** [create-classroom.mmd](sequence-diagram/apis/create-classroom.mmd) · [create-classroom.class.mmd](sequence-diagram/classes/create-classroom.class.mmd)

**Trigger:** Admin điền thông tin và yêu cầu thiết lập lớp học mới.

**Summary:** Kiểm tra ràng buộc hợp lệ của giáo viên (phải có vai trò Teacher và tài khoản active), chương trình học hoạt động, học kỳ và khoảng thời gian lớp học bắt đầu/kết thúc phải nằm trong khoảng thời gian của học kỳ, sau đó tạo và lưu lớp học mới vào cơ sở dữ liệu.

**Known gaps found in source (if any):** Ràng buộc thời gian lớp học phải khớp với học kỳ liên kết được kiểm tra chặt chẽ ở tầng Service.

---

## 3.4 Update Classroom

**Diagrams:** [update-classroom.mmd](sequence-diagram/apis/update-classroom.mmd) · [update-classroom.class.mmd](sequence-diagram/classes/update-classroom.class.mmd)

**Trigger:** Admin thay đổi thông tin lớp học (tên lớp, giáo viên phụ trách, học kỳ, ngày học) và lưu.

**Summary:** Kiểm tra các ràng buộc hợp lệ tương tự như bước tạo mới đối với giáo viên, chương trình, học kỳ và thời gian biểu, sau đó cập nhật thông tin lớp học.

**Known gaps found in source (if any):** None.

---

## 3.5 Delete Classroom

**Diagrams:** [delete-classroom.mmd](sequence-diagram/apis/delete-classroom.mmd) · [delete-classroom.class.mmd](sequence-diagram/classes/delete-classroom.class.mmd)

**Trigger:** Admin thực hiện yêu cầu xóa lớp học khỏi hệ thống.

**Summary:** Kiểm tra điều kiện: lớp học không có học sinh đang hoạt động và trạng thái lớp không phải là Active (đang hoạt động), sau đó tiến hành đánh dấu xóa mềm lớp học trong cơ sở dữ liệu.

**Known gaps found in source (if any):** Quy tắc nghiệp vụ chặn xóa lớp học đang hoạt động hoặc có học sinh đang ghi danh được áp dụng ở Service.

---

## 3.6 Get Classrooms By Teacher ID

**Diagrams:** [get-classrooms-by-teacher.mmd](sequence-diagram/apis/get-classrooms-by-teacher.mmd) · [get-classrooms-by-teacher.class.mmd](sequence-diagram/classes/get-classrooms-by-teacher.class.mmd)

**Trigger:** Giáo viên truy cập để xem danh sách các lớp học mình được phân công phụ trách.

**Summary:** Kiểm tra tính hợp lệ của tài khoản giáo viên, sau đó lấy danh sách phân trang các lớp học liên kết với mã ID của giáo viên đó.

**Known gaps found in source (if any):** Trả về danh sách trống nếu giáo viên không hợp lệ thay vì lỗi Exception.
