# 04 — Lesson & Program Management

**Actor/Role:** Admin, Teacher, Parent

**Status:** ✅ 10 use cases / 10 APIs done

**Source of truth:** [ProgramsController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/ProgramsController.cs), [LessonsController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/LessonsController.cs), [ProgramService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/ProgramService.cs), [LessonService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/LessonService.cs)

---

## 4.1 Get List Programs

**Diagrams:** [get-list-programs.mmd](sequence-diagram/apis/get-list-programs.mmd) · [get-list-programs.class.mmd](sequence-diagram/classes/get-list-programs.class.mmd)

**Trigger:** Admin/Teacher xem danh sách các chương trình học hiện có.

**Summary:** Lấy thông tin phân trang các chương trình học từ cơ sở dữ liệu.

**Known gaps found in source (if any):** None.

---

## 4.2 Get Program By ID

**Diagrams:** [get-program-by-id.mmd](sequence-diagram/apis/get-program-by-id.mmd) · [get-program-by-id.class.mmd](sequence-diagram/classes/get-program-by-id.class.mmd)

**Trigger:** Người dùng nhấp xem chi tiết một chương trình học.

**Summary:** Lấy thông tin chi tiết của chương trình học chỉ định kèm theo danh sách các bài học (Lessons) liên kết.

**Known gaps found in source (if any):** None.

---

## 4.3 Create Program

**Diagrams:** [create-program.mmd](sequence-diagram/apis/create-program.mmd) · [create-program.class.mmd](sequence-diagram/classes/create-program.class.mmd)

**Trigger:** Admin thêm mới một chương trình đào tạo.

**Summary:** Tạo chương trình học mới với các thông tin tên chương trình, độ tuổi mục tiêu, ngôn ngữ, mô tả, trạng thái và lưu vào DB.

**Known gaps found in source (if any):** None.

---

## 4.4 Update Program

**Diagrams:** [update-program.mmd](sequence-diagram/apis/update-program.mmd) · [update-program.class.mmd](sequence-diagram/classes/update-program.class.mmd)

**Trigger:** Admin cập nhật thông tin chương trình đào tạo.

**Summary:** Cập nhật các thông tin mô tả, độ tuổi, ngôn ngữ hoặc trạng thái hoạt động của chương trình học.

**Known gaps found in source (if any):** None.

---

## 4.5 Delete Program

**Diagrams:** [delete-program.mmd](sequence-diagram/apis/delete-program.mmd) · [delete-program.class.mmd](sequence-diagram/classes/delete-program.class.mmd)

**Trigger:** Admin thực hiện xóa chương trình học.

**Summary:** Đánh dấu xóa mềm chương trình học (`IsDeleted = true`, `DeletedAt = DateTime.UtcNow`).

**Known gaps found in source (if any):** None.

---

## 4.6 Get List Lessons

**Diagrams:** [get-list-lessons.mmd](sequence-diagram/apis/get-list-lessons.mmd) · [get-list-lessons.class.mmd](sequence-diagram/classes/get-list-lessons.class.mmd)

**Trigger:** Admin/Teacher truy cập xem danh sách các bài học.

**Summary:** Lấy thông tin phân trang các bài học hiện có từ DB.

**Known gaps found in source (if any):** None.

---

## 4.7 Get Lesson By ID

**Diagrams:** [get-lesson-by-id.mmd](sequence-diagram/apis/get-lesson-by-id.mmd) · [get-lesson-by-id.class.mmd](sequence-diagram/classes/get-lesson-by-id.class.mmd)

**Trigger:** Người dùng xem chi tiết một bài học.

**Summary:** Truy xuất thông tin bài học chi tiết từ cơ sở dữ liệu dựa trên ID chỉ định.

**Known gaps found in source (if any):** None.

---

## 4.8 Create Lesson

**Diagrams:** [create-lesson.mmd](sequence-diagram/apis/create-lesson.mmd) · [create-lesson.class.mmd](sequence-diagram/classes/create-lesson.class.mmd)

**Trigger:** Admin/Teacher thêm bài học mới cho một chương trình.

**Summary:** Xác thực mã chương trình liên kết (ProgramId) phải tồn tại và chưa bị xóa mềm, sau đó tiến hành tạo và thêm bài học mới.

**Known gaps found in source (if any):** Ràng buộc kiểm tra ProgramId tồn tại trước khi tạo bài học được xử lý ở tầng Service.

---

## 4.9 Update Lesson

**Diagrams:** [update-lesson.mmd](sequence-diagram/apis/update-lesson.mmd) · [update-lesson.class.mmd](sequence-diagram/classes/update-lesson.class.mmd)

**Trigger:** Admin/Teacher chỉnh sửa thông tin bài học (tên, thứ tự bài học, kỹ năng mục tiêu, thời gian ước tính, điểm tối đa).

**Summary:** Cập nhật các thông số chi tiết của bài học dựa trên ID chỉ định.

**Known gaps found in source (if any):** None.

---

## 4.10 Delete Lesson

**Diagrams:** [delete-lesson.mmd](sequence-diagram/apis/delete-lesson.mmd) · [delete-lesson.class.mmd](sequence-diagram/classes/delete-lesson.class.mmd)

**Trigger:** Admin/Teacher thực hiện xóa một bài học.

**Summary:** Thực hiện xóa mềm bài học bằng cách đổi cờ `IsDeleted = true` và lưu lại thông tin thời gian xóa.

**Known gaps found in source (if any):** None.
