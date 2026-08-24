# Backend Package Diagram — GodotXR.BE

Thư mục này chứa sơ đồ gói kiến trúc **Backend Package Diagram** (.NET 9 Clean Architecture) của dự án **GodotXR.BE**.

---

## 📂 Danh Sách File Trong Thư Mục

| Tên File | Mô Tả & Cách Sử Dụng |
| :--- | :--- |
| **\`backend-package-diagram.png\`** | 🖼️ **Hình ảnh sơ đồ gói PNG** (dùng để dán trực tiếp vào báo cáo Word/Docx hoặc trình chiếu). |
| **\`backend-package-diagram.drawio\`** | 📐 **File Draw.io Native** (mở trực tiếp bằng phần mềm Draw.io bằng menu \`File -> Open\` để chỉnh sửa hình khối, màu sắc). |
| **\`backend-package-diagram.puml\`** | 📄 **File mã nguồn PlantUML** (mở trong VS Code có extension PlantUML hoặc dán vào \`Arrange -> Insert -> Advanced -> PlantUML\` trên draw.io). |

---

## 🏗️ Cấu Trúc Phân Lớp Trong Sơ Đồ

1. **API Layer (\`GodotXR.Api\`)**:
   - \`Controllers\`: 17 REST API Controllers (\`AuthController\`, \`UsersController\`, \`ClassroomsController\`, \`ResultsController\`, v.v.).
   - \`Middlewares\`: Bộ lọc lỗi toàn cục & Jwt Processing Middleware.
   - \`Extensions\`: Phương thức mở rộng DI (\`DependencyInjection.cs\`) và Claims (\`ClaimsPrincipalExtensions.cs\`).
   - \`Payloads\`: DTOs hợp đồng Request/Response HTTP (\`Contracts/\`).

2. **Domain Layer (\`GodotXR.Domain\`)**:
   - \`Entities\`: 18 thực thể cốt lõi (\`User\`, \`Role\`, \`ChildProfile\`, \`Result\`, \`Classroom\`, v.v.).
   - \`Interfaces\`: Data contract Interfaces (\`IRepositories\` & \`IUnitOfWork\`).
   - \`Common\`: Kiểu dùng chung (\`RoleEnum\`, \`BaseEntity\`).

3. **Application Layer (\`GodotXR.Application\`)**:
   - \`Services\`: 33 Dịch vụ nghiệp vụ (\`UserService\`, \`AuthService\`, \`LessonService\`, \`ResultService\`, \`AnalyzeService\`, \`MinIOService\`, v.v.).
   - \`Dtos\`: Data Transfer Objects.
   - \`Validations\` / \`Exceptions\` / \`Utils\`: Bộ công cụ kiểm tra dữ liệu, ngoại lệ nghiệp vụ & xử lý audio.
   - \`Configurations\`: AutoMapper Profiles (\`ApplicationProfile.cs\`).
   - \`Hubs\`: Realtime SignalR notification hubs.

4. **Infrastructure Layer (\`GodotXR.Infrastructure\`)**:
   - \`Entity Configurations\`: Cấu hình EF Core Fluent API mappings.
   - \`Context\`: \`AppDbContext\` & \`DbFactory\`.
   - \`Repositories\`: Triển khai thực tế của Repository Pattern & UnitOfWork.
   - \`Migrations\`: Bản ghi dịch chuyển CSDL EF Core.
