# 08 — Reports & System Settings

**Actor/Role:** Admin, Teacher, Parent

**Status:** ✅ 8 use cases / 8 APIs done

**Source of truth:** [ReportController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/ReportController.cs), [SchoolYearsController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/SchoolYearsController.cs), [SemestersController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/SemestersController.cs), [EventLogsController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/EventLogsController.cs), [ReportService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/ReportService.cs), [SchoolYearService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/SchoolYearService.cs), [SemesterService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/SemesterService.cs)

---

## 8.1 Create Report

**Diagrams:** [create-report.mmd](sequence-diagram/apis/create-report.mmd) · [create-report.class.mmd](sequence-diagram/classes/create-report.class.mmd)

**Trigger:** Admin, Giáo viên hoặc Phụ huynh yêu cầu khởi tạo tệp báo cáo học tập tổng quan.

**Summary:** Xác thực phân tích AI (`AnalyzeId`) chỉ định phải tồn tại và tài khoản trẻ em tương ứng phải chứa ít nhất một kết quả bài tập đã được lưu chính thức (`IsFinalized == true`), sau đó khởi tạo báo cáo.

---

## 8.2 Get List Reports

**Diagrams:** [get-list-reports.mmd](sequence-diagram/apis/get-list-reports.mmd) · [get-list-reports.class.mmd](sequence-diagram/classes/get-list-reports.class.mmd)

**Trigger:** Người dùng xem danh sách các báo cáo học tập được xuất ra.

**Summary:** Truy xuất danh sách báo cáo chưa bị xóa phân trang. Áp dụng quy tắc phân quyền: Admin được xem tất cả; Giáo viên chỉ được xem báo cáo của học sinh thuộc các lớp học do giáo viên đó giảng dạy; Phụ huynh chỉ được xem báo cáo thuộc về con mình.

---

## 8.3 Create School Year

**Diagrams:** [create-school-year.mmd](sequence-diagram/apis/create-school-year.mmd) · [create-school-year.class.mmd](sequence-diagram/classes/create-school-year.class.mmd)

**Trigger:** Admin thiết lập niên khóa học mới trên hệ thống.

**Summary:** Xác thực ngày bắt đầu phải trước ngày kết thúc (BR-43). Không được trùng lặp thời gian hoạt động với niên khóa khác. Chỉ cho phép tối đa một niên khóa duy nhất ở trạng thái hoạt động (Active) tại cùng một thời điểm (BR-44).

---

## 8.4 Update School Year

**Diagrams:** [update-school-year.mmd](sequence-diagram/apis/update-school-year.mmd) · [update-school-year.class.mmd](sequence-diagram/classes/update-school-year.class.mmd)

**Trigger:** Admin cập nhật thông tin niên khóa học.

**Summary:** Đảm bảo thời gian học của niên khóa hợp lệ và không chồng lấn thời gian với các niên khóa khác. Chặn cập nhật trạng thái Active nếu đã tồn tại một niên khóa Active khác trên hệ thống.

---

## 8.5 Create Semester

**Diagrams:** [create-semester.mmd](sequence-diagram/apis/create-semester.mmd) · [create-semester.class.mmd](sequence-diagram/classes/create-semester.class.mmd)

**Trigger:** Admin thiết lập học kỳ mới trong niên khóa học.

**Summary:** Xác thực niên khóa học liên kết phải tồn tại. Thời gian bắt đầu và kết thúc của học kỳ phải nằm trọn trong khoảng thời gian của niên khóa học. Không chồng chéo khoảng thời gian giữa các học kỳ thuộc cùng một niên khóa. Đồng thời kiểm tra tài khoản giáo viên phụ trách học kỳ phải tồn tại và đang hoạt động.

---

## 8.6 Update Semester

**Diagrams:** [update-semester.mmd](sequence-diagram/apis/update-semester.mmd) · [update-semester.class.mmd](sequence-diagram/classes/update-semester.class.mmd)

**Trigger:** Admin cập nhật thông tin học kỳ.

**Summary:** Thực hiện lại đầy đủ các ràng buộc về tính toàn vẹn thời gian học kỳ trong niên khóa học, kiểm tra chồng lấn thời gian học kỳ (ngoại trừ chính ID học kỳ này) và cập nhật thông tin giáo viên quản lý.

---

## 8.7 Get Event Logs By Result

**Diagrams:** [get-event-logs-by-result.mmd](sequence-diagram/apis/get-event-logs-by-result.mmd) · [get-event-logs-by-result.class.mmd](sequence-diagram/classes/get-event-logs-by-result.class.mmd)

**Trigger:** Người dùng xem dòng nhật ký hành động ghi nhận của bé trong một lượt chơi bài tập VR cụ thể (các sự kiện bắt đầu, trả lời câu hỏi, hoàn thành...).

**Summary:** Kiểm tra phân quyền truy cập kết quả của người dùng tương tự như truy xuất chi tiết kết quả. Sau đó, lấy toàn bộ danh sách sự kiện từ bảng `EventLogs` liên kết với `resultId`.

---

## 8.8 Get Event Logs By Child

**Diagrams:** [get-event-logs-by-child.mmd](sequence-diagram/apis/get-event-logs-by-child.mmd) · [get-event-logs-by-child.class.mmd](sequence-diagram/classes/get-event-logs-by-child.class.mmd)

**Trigger:** Giáo viên hoặc Phụ huynh xem toàn bộ tiến trình lịch sử hoạt động chơi của bé trên hệ thống.

**Summary:** Xác thực quyền sở hữu hoặc dạy học đối với bé chỉ định. Sau đó truy xuất toàn bộ danh sách log sự kiện liên kết trực tiếp với học sinh đó.
