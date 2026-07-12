# AFP-GOCA PDF Table Extractor & Parser

Dự án này sử dụng công cụ **Docling** (kết hợp OCR Tesseract) để trích xuất dữ liệu, cấu trúc bảng biểu và mô tả kỹ thuật từ tài liệu PDF chuyên ngành **AFP GOCA (Graphics Object Content Architecture)**. Dữ liệu sau khi trích xuất được xử lý tự động bằng **Pandas** và xuất ra định dạng cấu trúc JSON để phục vụ cho các ứng dụng khác (như RAG, Tra cứu, Hệ thống phân tích tài liệu).

## 🚀 Tính năng chính

* **Tự động trích xuất thông minh**: Sử dụng thư viện `docling` để parse PDF phức tạp, tự động nhận diện bố cục, chuyển đổi tài liệu sang Markdown định dạng chuẩn.
* **Xử lý OCR nâng cao**: Tích hợp Tesseract OCR và mô hình mô tả ảnh (SmolVLM) để đọc hiểu các thành phần đồ họa/bảng biểu nằm trong PDF một cách trực quan.
* **Chuẩn hóa & Làm sạch dữ liệu**: Tự động lọc các bảng dữ liệu kỹ thuật, tách bit/byte offset, dọn dẹp khoảng trắng dư thừa và gộp các bảng bị tràn trang một cách thông minh.
* **Định cấu trúc đầu ra (Structured Data)**: Ánh xạ mã lệnh (code/tag) với mô tả kỹ thuật tương ứng và xuất ra tệp tin cấu trúc `table.json` có định dạng rõ ràng.

---

## 🛠️ Yêu cầu hệ thống & Cài đặt

### 1. Cài đặt các công cụ hệ thống (Yêu cầu bắt buộc cho OCR)

Dự án cần có **Tesseract OCR** trên máy tính để xử lý nhận diện chữ từ ảnh.

* **Trên macOS (dùng Homebrew):**

  ```bash
  brew install tesseract
  ```
