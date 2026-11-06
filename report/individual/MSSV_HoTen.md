# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV: 2A202603402**
- **Họ và tên: Đỗ Minh Hiếu**
- **SEED** (in ở ô đầu notebook):8817

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☐ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☐ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☐ |

## 2. Kết quả chính

*Chép bảng so sánh cuối Phần 5 (F1 test, F1 SUB 40, p95 ms/tin, USD/1k tin) của chính bạn.*

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

## 7. AI log và điều đã học

| Phần | Bạn hỏi AI gì (prompt) | AI trả lời/viết gì | Bạn đã sửa / kiểm chứng gì |
| 1–3 | Hỏi giải thích khái niệm, cú pháp, đọc lỗi | Gợi ý trên ví dụ khác, chỉ ra lỗi (thứ tự phép tính, shape, nhầm biến val/batch) | Tự viết và sửa code, test ✅ |
| 4 · TODO 4.1 `call_openai` | Viết hàm gọi Chat Completions theo docstring, trả về (text, latency) | Code `OpenAI().chat.completions.create(...)` + `**provider_kwargs(max_tokens)`, đo thời gian bằng `time.perf_counter()` | Đọc lại, hiểu vì sao GPT-6 dùng `max_completion_tokens` + `reasoning_effort="none"`. Test giả lập ✅ |
| 4 · TODO 4.2 `build_classification_prompt` | Viết prompt zero-shot/few-shot, kết thúc bằng `Message: """..."""\nLabel:` | Prompt mô tả nhiệm vụ, yêu cầu trả lời 1 từ, chèn ví dụ few-shot | Không sửa, test ✅ |
| 4 · TODO 4.3 `parse_label` | Đọc nhãn từ câu trả lời LLM (chữ hoa, dấu câu, "Label:", "not spam") | Regex tách từ, kiểm tra "not spam" trước "spam" | Hiểu đây là lỗi của `parse_label_v2` (Bắt lỗi 3). Test ✅ |
| 4 · TODO 4.4 `llm_classify_batch` | Phân loại cả loạt, đo latency, ước tính token/chi phí | Vòng lặp `retry_with_backoff(call_llm)`, None → 0 và đếm `n_invalid`, token ≈ số từ / 0.75 | Test giả lập ✅. Key OpenAI hết credit (429 insufficient_quota) nên không chạy 4.A/4.B thật, đặt `HAS_LLM = False` |
