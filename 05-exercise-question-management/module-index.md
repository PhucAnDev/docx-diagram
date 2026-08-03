# 05 — Exercise & Question Management

**Actor/Role:** Admin, Teacher, Parent, Child

**Status:** ✅ 15 use cases / 15 APIs done

**Source of truth:** [ExercisesController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/ExercisesController.cs), [ExerciseQuestionsController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/ExerciseQuestionsController.cs), [ExerciseTypesController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/ExerciseTypesController.cs), [ExerciseService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/ExerciseService.cs), [ExerciseQuestionService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/ExerciseQuestionService.cs), [ExerciseTypeService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/ExerciseTypeService.cs)

---

## 5.1 Get List Exercises

**Diagrams:** [get-list-exercises.mmd](sequence-diagram/apis/get-list-exercises.mmd) · [get-list-exercises.class.mmd](sequence-diagram/classes/get-list-exercises.class.mmd)

**Trigger:** Người dùng truy cập xem danh sách các bài tập luyện tập trên dashboard hoặc ứng dụng client.

**Summary:** Truy xuất thông tin phân trang các bài tập hoạt động chưa bị xóa mềm theo bộ lọc bài học, loại bài tập, giáo viên phụ trách hoặc trạng thái bài tập.

**Known gaps found in source (if any):** None.

---

## 5.2 Get Exercise By ID

**Diagrams:** [get-exercise-by-id.mmd](sequence-diagram/apis/get-exercise-by-id.mmd) · [get-exercise-by-id.class.mmd](sequence-diagram/classes/get-exercise-by-id.class.mmd)

**Trigger:** Người dùng xem chi tiết bài tập hoặc trẻ tải thông tin bài tập về thiết bị VR.

**Summary:** Lấy thông tin chi tiết của một bài tập theo ID định danh kèm danh sách câu hỏi.

**Known gaps found in source (if any):** None.

---

## 5.3 Create Exercise

**Diagrams:** [create-exercise.mmd](sequence-diagram/apis/create-exercise.mmd) · [create-exercise.class.mmd](sequence-diagram/classes/create-exercise.class.mmd)

**Trigger:** Giáo viên hoặc Admin nhấn Tạo bài tập mới.

**Summary:** Thực hiện kiểm tra các quy định nghiệp vụ:
- `DurationLimit > 0` (giới hạn thời gian phải lớn hơn 0 - `BR-67`).
- Mức độ khó phải nằm trong danh mục hợp lệ (`BR-68`).
- Chặn trực tiếp thiết lập `Status = Active` khi chưa có câu hỏi (`BR-70`).
- Xác thực giáo viên, bài học và chương trình chứa bài học hoạt động, loại bài tập hoạt động (`BR-56`, `BR-62`, `BR-63`, `BR-66`).

**Known gaps found in source (if any):** Ràng buộc cấm tạo bài tập trạng thái `Active` ngay lập tức để ép luồng giáo viên phải thêm câu hỏi trước khi kích hoạt.

---

## 5.4 Update Exercise

**Diagrams:** [update-exercise.mmd](sequence-diagram/apis/update-exercise.mmd) · [update-exercise.class.mmd](sequence-diagram/classes/update-exercise.class.mmd)

**Trigger:** Giáo viên chỉnh sửa thông tin bài tập và nhấn Lưu.

**Summary:** Kiểm tra các ràng buộc tương tự lúc tạo mới. Riêng trạng thái bài tập chỉ được chuyển thành `Active` khi bài tập đã có ít nhất một câu hỏi hợp lệ chưa bị xóa (`BR-70`).

**Known gaps found in source (if any):** Check `entity.ExerciseQuestions.Any(q => !q.IsDeleted)` tại service khi đổi trạng thái sang Active.

---

## 5.5 Delete Exercise

**Diagrams:** [delete-exercise.mmd](sequence-diagram/apis/delete-exercise.mmd) · [delete-exercise.class.mmd](sequence-diagram/classes/delete-exercise.class.mmd)

**Trigger:** Giáo viên hoặc Admin xóa bài tập.

**Summary:** Chặn xóa nếu bài tập đã có lịch sử làm bài (historical Results) từ học sinh (`BR-72`), nếu an toàn thì đánh dấu xóa mềm bài tập.

**Known gaps found in source (if any):** None.

---

## 5.6 Get List Questions

**Diagrams:** [get-list-questions.mmd](sequence-diagram/apis/get-list-questions.mmd) · [get-list-questions.class.mmd](sequence-diagram/classes/get-list-questions.class.mmd)

**Trigger:** Giáo viên quản lý danh sách câu hỏi của bài tập.

**Summary:** Lấy danh sách câu hỏi luyện tập phân trang theo bài tập hoặc giáo viên thiết lập.

**Known gaps found in source (if any):** None.

---

## 5.7 Get Question By ID

**Diagrams:** [get-question-by-id.mmd](sequence-diagram/apis/get-question-by-id.mmd) · [get-question-by-id.class.mmd](sequence-diagram/classes/get-question-by-id.class.mmd)

**Trigger:** Người dùng xem chi tiết một câu hỏi.

**Summary:** Tìm kiếm câu hỏi chưa bị xóa theo ID chỉ định.

**Known gaps found in source (if any):** None.

---

## 5.8 Create Question

**Diagrams:** [create-question.mmd](sequence-diagram/apis/create-question.mmd) · [create-question.class.mmd](sequence-diagram/classes/create-question.class.mmd)

**Trigger:** Giáo viên nhấp tạo câu hỏi mới cho một bài tập.

**Summary:** Xác thực các trường bắt buộc (câu hỏi, câu trả lời, loại - `BR-69`), phần mở rộng định dạng file âm thanh/hình ảnh hợp lệ (`BR-71`), giáo viên hợp lệ, và bài tập liên kết tồn tại (`BR-60`).

**Known gaps found in source (if any):** Phân tích phần mở rộng của URL file (Audio/Image) được kiểm tra an toàn bằng phân tách URI trong code C#.

---

## 5.9 Update Question

**Diagrams:** [update-question.mmd](sequence-diagram/apis/update-question.mmd) · [update-question.class.mmd](sequence-diagram/classes/update-question.class.mmd)

**Trigger:** Giáo viên chỉnh sửa chi tiết câu hỏi.

**Summary:** Kiểm tra các ràng buộc đầu vào và cập nhật thông tin câu hỏi.

**Known gaps found in source (if any):** None.

---

## 5.10 Delete Question

**Diagrams:** [delete-question.mmd](sequence-diagram/apis/delete-question.mmd) · [delete-question.class.mmd](sequence-diagram/classes/delete-question.class.mmd)

**Trigger:** Giáo viên nhấn xóa câu hỏi.

**Summary:** Chỉ được phép xóa mềm câu hỏi nếu bài tập cha của nó chưa có lịch sử làm bài (`BR-72`).

**Known gaps found in source (if any):** Chặn xóa gián tiếp qua kiểm tra liên kết kết quả bài tập cha.

---

## 5.11 Get List Exercise Types

**Diagrams:** [get-list-exercise-types.mmd](sequence-diagram/apis/get-list-exercise-types.mmd) · [get-list-exercise-types.class.mmd](sequence-diagram/classes/get-list-exercise-types.class.mmd)

**Trigger:** Người dùng xem các loại bài tập (phát âm, thẻ hình, v.v.).

**Summary:** Lấy thông tin phân trang của các loại bài tập đang hoạt động.

**Known gaps found in source (if any):** None.

---

## 5.12 Get Exercise Type By ID

**Diagrams:** [get-exercise-type-by-id.mmd](sequence-diagram/apis/get-exercise-type-by-id.mmd) · [get-exercise-type-by-id.class.mmd](sequence-diagram/classes/get-exercise-type-by-id.class.mmd)

**Trigger:** Xem chi tiết loại bài tập.

**Summary:** Tìm kiếm thông tin loại bài tập theo ID.

**Known gaps found in source (if any):** None.

---

## 5.13 Create Exercise Type

**Diagrams:** [create-exercise-type.mmd](sequence-diagram/apis/create-exercise-type.mmd) · [create-exercise-type.class.mmd](sequence-diagram/classes/create-exercise-type.class.mmd)

**Trigger:** Admin thêm một loại hình bài tập mới.

**Summary:** Kiểm tra trùng lặp tên loại hình, nếu hợp lệ thì lưu vào cơ sở dữ liệu.

**Known gaps found in source (if any):** None.

---

## 5.14 Update Exercise Type

**Diagrams:** [update-exercise-type.mmd](sequence-diagram/apis/update-exercise-type.mmd) · [update-exercise-type.class.mmd](sequence-diagram/classes/update-exercise-type.class.mmd)

**Trigger:** Admin chỉnh sửa thông tin loại hình bài tập.

**Summary:** Kiểm tra trùng tên loại hình. Đặc biệt chặn vô hiệu hóa (deactivate) nếu loại bài tập này đang được các bài tập đang hoạt động (Active) sử dụng (`BR-62`).

**Known gaps found in source (if any):** None.

---

## 5.15 Delete Exercise Type

**Diagrams:** [delete-exercise-type.mmd](sequence-diagram/apis/delete-exercise-type.mmd) · [delete-exercise-type.class.mmd](sequence-diagram/classes/delete-exercise-type.class.mmd)

**Trigger:** Admin yêu cầu xóa một loại bài tập.

**Summary:** Chặn xóa nếu còn bài tập chưa bị xóa đang liên kết với loại bài tập này (`BR-62`). Nếu an toàn thì đánh dấu xóa mềm.

**Known gaps found in source (if any):** None.
