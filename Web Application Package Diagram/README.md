# Web Application Package Diagram — GodotXR.FE

Thư mục này chứa sơ đồ gói kiến trúc **Web Application Package Diagram** (React 19 + TypeScript + Vite) của ứng dụng Frontend **GodotXR.FE**, được tối ưu hóa tên gói khớp 100% với cấu trúc mã nguồn thực tế.

---

## 📂 Danh Sách File Trong Thư Mục

| Tên File | Mô Tả & Cách Sử Dụng |
| :--- | :--- |
| **`web-application-package-diagram.png`** | 🖼️ **Hình ảnh sơ đồ gói PNG** (dùng để dán trực tiếp vào báo cáo Word/Docx hoặc trình chiếu). |
| **`web-application-package-diagram.drawio`** | 📐 **File Draw.io Native** (mở trực tiếp bằng phần mềm Draw.io bằng menu `File -> Open` để chỉnh sửa hình khối, màu sắc). |
| **`web-application-package-diagram.puml`** | 📄 **File mã nguồn PlantUML** (mở trong VS Code có extension PlantUML hoặc dán vào `Arrange -> Insert -> Advanced -> PlantUML` trên draw.io). |

---

## 🏗️ Cấu Trúc Phân Lớp Trong Sơ Đồ

1. **Thành phần Trung tâm (`app/`)**:
   - **`auth`**: Phân hệ xác thực (Đăng nhập, Đăng ký, Quên mật khẩu).
   - **`browse`**: Phân hệ duyệt trang chủ công khai & danh mục bài học VR (`public/`, `learning-content/`).
   - **`management`**: Phân hệ quản trị Lớp học, Học sinh, Bài học & Kết quả VR (`admin/`, `teacher/`, `parent/`, `learning-result/`).
   - **`api`**: Tầng dịch vụ giao tiếp REST API (`services/apiClient.ts`, `authService.ts`, v.v.).

2. **Các Gói Hỗ Trợ Xung Quanh**:
   - **`actions`**: Các hàm điều hướng & xử lý sự kiện action.
   - **`hooks`**: Custom React Hooks trong `src/hooks/` (`useLogin`, `useUserManagement`, `useClassroomManagementApi`, `useLearningResultApi`, v.v.).
   - **`services`**: Tầng dịch vụ xử lý câu lệnh truy vấn lấy dữ liệu trực tiếp trong `src/services/` (`userService.ts`, `resultService.ts`, `analyzeService.ts`, v.v.).
   - **`lib`**: Thư viện dùng chung chứa các gói con **`types`**, **`validations`**, **`realtime`**.
   - **`constants`**: Các hằng số cấu hình hệ thống & menu navigation.
   - **`contexts`**: React Contexts quản lý state toàn cục.
   - **`public`**: Kho tài nguyên tĩnh (Images, SVGs, Fonts).
   - **`components`**: Các React UI Components dùng chung (Tables, Modals, Forms, Charts).
   - **`stores`**: Bộ nhớ lưu trữ phiên làm việc (Local Storage / Session Storage).
