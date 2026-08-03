# 07 — Results, Speech Performance & AI Analysis

**Actor/Role:** Admin, Teacher, Parent, Child

**Status:** ✅ 8 use cases / 8 APIs done

**Source of truth:** [ResultsController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/ResultsController.cs), [FilesController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/FilesController.cs), [PronunciationDetailsController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/PronunciationDetailsController.cs), [AnalyzeController.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Api/Controllers/AnalyzeController.cs), [ResultService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/ResultService.cs), [AnalyzeService.cs](file:///d:/do%20an/FE%20and%20BE/godotxr-be/GodotXR.Application/Services/AnalyzeService.cs)

---

## 7.1 Upload Session Audio & Replay

**Diagrams:** [upload-session-audio.mmd](sequence-diagram/apis/upload-session-audio.mmd) · [upload-session-audio.class.mmd](sequence-diagram/classes/upload-session-audio.class.mmd)

**Trigger:** Phụ huynh (hoặc thiết bị VR thông qua tài khoản phụ huynh) tải lên tệp tin âm thanh ghi âm tổng hợp (`voice.wav`) và metadata buổi chơi bài tập dạng JSON sau khi bé hoàn thành.

**Summary:** API sinh ra một `folderId` định dạng Guid làm thư mục riêng trên MinIO, sau đó tải tệp tin metadata.json và file voice.wav lên MinIO lưu trữ phục vụ phát lại.

---

## 7.2 Upload Audio Chunk

**Diagrams:** [upload-audio-chunk.mmd](sequence-diagram/apis/upload-audio-chunk.mmd) · [upload-audio-chunk.class.mmd](sequence-diagram/classes/upload-audio-chunk.class.mmd)

**Trigger:** Thiết bị VR tải trực tiếp từng phân đoạn âm thanh luyện nói ngắn (chunk) của bé lên trong lúc đang thực hiện bài tập.

**Summary:** API đẩy tệp âm thanh wav chunk lên MinIO theo đường dẫn phân mảnh có chứa `SessionId` và `ChunkIndex`, đồng thời trả về presigned URL của chunk để tải về phát lại hoặc gửi đi đánh giá.

---

## 7.3 Submit VR Result

**Diagrams:** [submit-vr-result.mmd](sequence-diagram/apis/submit-vr-result.mmd) · [submit-vr-result.class.mmd](sequence-diagram/classes/submit-vr-result.class.mmd)

**Trigger:** Kính VR gửi kết quả tổng hợp sau khi trẻ hoàn thành một Bài tập VR (bao gồm các chỉ số điểm số, thời lượng chơi, danh sách từ phát âm lỗi chi tiết và danh sách log sự kiện hành động).

**Summary:** Hệ thống xác thực sự tồn tại của học sinh và bài tập. Thực hiện lưu kết quả tổng quan vào bảng `Results`, lưu các lỗi phát âm chi tiết âm vị vào bảng `PronunciationDetails` và lưu log hành động vào bảng `EventLogs`.

---

## 7.4 Assess Speech Chunk

**Diagrams:** [assess-speech-chunk.mmd](sequence-diagram/apis/assess-speech-chunk.mmd) · [assess-speech-chunk.class.mmd](sequence-diagram/classes/assess-speech-chunk.class.mmd)

**Trigger:** Ứng dụng yêu cầu chấm điểm phát âm cho một chunk wav cụ thể của trẻ theo văn bản mẫu.

**Summary:** Nếu khóa Azure Speech chưa được cấu hình, hệ thống sẽ trả về kết quả chấm điểm giả lập ngẫu nhiên (Mock Assessment). Khi đã có cấu hình, hệ thống tải chunk âm thanh từ MinIO và gửi yêu cầu chấm điểm tới dịch vụ Azure Speech API (phương thức Pronunciation Assessment) rồi trả về kết quả chấm điểm chi tiết.

---

## 7.5 Get Pronunciation Details

**Diagrams:** [get-pronunciation-details.mmd](sequence-diagram/apis/get-pronunciation-details.mmd) · [get-pronunciation-details.class.mmd](sequence-diagram/classes/get-pronunciation-details.class.mmd)

**Trigger:** Người dùng (Admin, Giáo viên phụ trách hoặc Phụ huynh của bé) xem danh sách các lỗi âm vị/phát âm chi tiết của một kết quả bài tập.

**Summary:** Kiểm tra quyền truy cập của người dùng đối với hồ sơ học sinh liên kết với kết quả, sau đó truy xuất trực tiếp danh sách chi tiết lỗi phát âm từ bảng `PronunciationDetails`.

---

## 7.6 Update Teacher Feedback

**Diagrams:** [update-teacher-feedback.mmd](sequence-diagram/apis/update-teacher-feedback.mmd) · [update-teacher-feedback.class.mmd](sequence-diagram/classes/update-teacher-feedback.class.mmd)

**Trigger:** Giáo viên nhập nhận xét và đánh giá cho kết quả bài tập của học sinh.

**Summary:** Cập nhật nội dung chuỗi nhận xét vào thuộc tính `FeedbackText` của thực thể kết quả bài tập (`Result`) được chỉ định.

---

## 7.7 Create AI Analysis

**Diagrams:** [create-ai-analysis.mmd](sequence-diagram/apis/create-ai-analysis.mmd) · [create-ai-analysis.class.mmd](sequence-diagram/classes/create-ai-analysis.class.mmd)

**Trigger:** Admin hoặc Giáo viên gửi yêu cầu tạo phân tích tâm lý/học tập của trẻ qua AI.

**Summary:** Hệ thống kiểm tra sự tồn tại của hồ sơ trẻ, lưu lại thông tin phân tích AI bao gồm các chỉ số đánh giá giọng nói, điểm số hành vi, điểm tự tin, chi tiết phân tích và gợi ý khuyến nghị từ AI.

---

## 7.8 Get Child AI Analysis

**Diagrams:** [get-child-ai-analysis.mmd](sequence-diagram/apis/get-child-ai-analysis.mmd) · [get-child-ai-analysis.class.mmd](sequence-diagram/classes/get-child-ai-analysis.class.mmd)

**Trigger:** Giáo viên, Admin hoặc Phụ huynh xem lịch sử các phân tích AI của trẻ.

**Summary:** Kiểm tra phân quyền truy cập hồ sơ học sinh, sau đó trả về danh sách các phân tích AI được sắp xếp mới nhất lên đầu của trẻ.
