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
* **Trên Ubuntu/Debian:**
* sudo apt-get install tesseract-ocr

### 2. Cài đặt các thư viện Python

Nên tạo một môi trường ảo (ví dụ dùng conda hoặc venv với Python 3.11) và cài đặt các thư viện sau:

## 📂 Cấu trúc mã nguồn
Dự án xử lý tuần tự qua các bước trong Notebook:

1. Khởi tạo Docling Pipeline: Định cấu hình cho phép OCR và tạo ảnh trang với PdfPipelineOptions.

2. Trích xuất mục lục: Parse trang chỉ định chứa danh mục mã lệnh để xây dựng từ điển đối chiếu (list_code).

3. Parse nội dung chính: Chuyển đổi các trang tài liệu PDF sang dạng Markdown.

4. Lọc và gộp bảng: Lọc các phân đoạn chứa ký tự phân tách bảng |, loại bỏ header nhiễu, liên kết các bảng phân mảnh nếu chúng liên tiếp nhau.

5. Trích xuất siêu dữ liệu: Thu thập thông tin gồm: Tag, Code, Length (Độ dài), và Description (Mô tả chi tiết từ tiêu đề Markdown tương ứng).

6. Lưu kết quả: Xuất toàn bộ dữ liệu có cấu trúc ra file output/table.json.

## 💻 Hướng dẫn sử dụng
1. Đảm bảo đường dẫn tới tệp tài liệu PDF của bạn được cấu hình chính xác trong mã nguồn:
pdf_path = "đường_dẫn_đến_file_AFP-GOCA-Reference.pdf"
Chạy toàn bộ các ô lệnh (cells) trong Jupyter Notebook.

Kết quả sẽ được lưu tại: output/table.json dưới định dạng:
{
    "Tên lệnh / Ý nghĩa": {
        "Tag": "Tên tag (ví dụ: GBAR)",
        "Code": "Mã hex (ví dụ: C1)",
        "Length": "Độ dài dữ liệu",
        "Description": "Chi tiết mô tả chức năng của lệnh..."
    }
}
## 📚 Công nghệ sử dụng
Docling - Bộ parser tài liệu thế hệ mới từ IBM.

Pandas - Xử lý và làm sạch dữ liệu dạng bảng.

Tesseract OCR - Công cụ nhận diện ký tự quang học nguồn mở.

LangChain - Hỗ trợ mở rộng tích hợp cơ sở dữ liệu vector (FAISS) và LLMs cho các tác vụ hỏi đáp về tài liệu (RAG) trong tương lai.
"""
