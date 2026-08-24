# VR Application Package Diagram — GodotXR.Client

Thư mục này chứa sơ đồ gói kiến trúc **VR Application Package Diagram** (Godot Engine 4.x + C# & GDScript + OpenXR) của ứng dụng kính thực tế ảo **xr-app**.

---

## 📂 Danh Sách File Trong Thư Mục

| Tên File | Mô Tả & Cách Sử Dụng |
| :--- | :--- |
| **`vr-application-package-diagram.png`** | 🖼️ **Hình ảnh sơ đồ gói PNG** (dùng để dán trực tiếp vào báo cáo Word/Docx hoặc trình chiếu). |
| **`vr-application-package-diagram.drawio`** | 📐 **File Draw.io Native** (mở trực tiếp bằng phần mềm Draw.io bằng menu `File -> Open` để chỉnh sửa hình khối, màu sắc). |
| **`vr-application-package-diagram.puml`** | 📄 **File mã nguồn PlantUML** (mở trong VS Code có extension PlantUML hoặc dán vào `Arrange -> Insert -> Advanced -> PlantUML` trên draw.io). |

---

## 🏗️ Cấu Trúc Phân Lớp Trong Sơ Đồ

1. **Scenes & Worlds Layer (`Scenes/`)**:
   - **`Worlds`**: Các thế giới 3D thực hành VR (`SupermarketWorld`, `FishingWorld`, `TutorialWorld`, `StarterHub`).
   - **`UIScenes`**: Màn hình giao diện VR 3D (`LoginScene`, `LoadingStage`, `SpectatorScene`).
   - **`PlayerRig`**: Cụm kính VR & chuyển động người chơi (`FOV player`, `LoadingPlatform`).

2. **Scripts & Controllers Layer (`scripts/`)**:
   - **`CoreManager`**: Điều phối luồng trò chơi (`GameManager`, `SupermarketLevelController`, `FishingLevelController`, `SessionData`).
   - **`APIControllers`**: Tầng giao tiếp REST API Backend (`AuthController`, `childprofile-my-child-api`, `result-api`, `FilesApi`).
   - **`SpeechAudio`**: Nhận diện & thu âm giọng nói real-time (`AzureSpeechManager`, `MicInput.cs`, `MicController`).
   - **`TelemetryReplay`**: Thu thập biến đổi 3D & tải dữ liệu phiên VR (`TelementryController`, `SessionUploader.cs`, `ReplayerManager`).
   - **`NPCsEnvironment`**: Hành vi NPC & kích thích phản xạ phát âm.

3. **Prefabs & Assets Layer (`Prefabs/`, `Assets/`)**:
   - **`InteractableObjects`**: Vật phẩm tương tác VR (Hoa quả, Thực phẩm, Cần câu).
   - **`UIPrefabs`**: Giao diện 3D Canvas & Hint Triggers.
   - **`AudioSounds`**: Giọng hướng dẫn & hiệu ứng âm thanh.
   - **`ShadersMaterials`**: Shaders nước & vật liệu môi trường.

4. **Hardware & Plugins Layer (`addons/`)**:
   - **`godot-xr-tools`**: Bộ công cụ điều khiển OpenXR (Locomotion, Grab/Teleport).
   - **`godotopenxrvendors`**: Plugin Meta Quest & Action Map (`openxr_action_map.tres`).
   - **`meshcombiner`**: Tối ưu hóa mô hình 3D cho kính VR độc lập.
