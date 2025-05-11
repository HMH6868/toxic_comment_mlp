# Phân loại bình luận độc hại

## Tổng quan dự án

Dự án này là một ứng dụng web cho phép người dùng nhập vào một bình luận và mô hình học máy sẽ phân loại xem bình luận đó có chứa nội dung độc hại hay không. Mô hình được huấn luyện dựa trên một tập dữ liệu các bình luận đã được gán nhãn.

## Tính năng

*   Giao diện web đơn giản để nhập và phân loại bình luận.
*   Sử dụng mô hình Multi-Layer Perceptron (MLP) để phân loại.
*   Cho phép huấn luyện lại mô hình với dữ liệu mới.

## Hướng dẫn Cài đặt

Để thiết lập dự án này trên máy cục bộ của bạn, hãy làm theo các bước dưới đây.

### Điều kiện tiên quyết
Trước khi tiếp tục, đảm bảo rằng bạn đã cài đặt các phần mềm sau trên hệ thống của mình:
*   **Python:** Phiên bản 3.7 trở lên. Bạn có thể tải Python từ [python.org](https://www.python.org/).
*   **pip:** Trình quản lý gói cho Python (thường được cài đặt kèm với Python).
*   **Git:** Hệ thống quản lý phiên bản phân tán (tùy chọn, nếu bạn muốn sao chép mã nguồn từ kho lưu trữ). Bạn có thể tải Git từ [git-scm.com](https://git-scm.com/).

### Các bước cài đặt

1.  **Lấy mã nguồn:**
    *   **Cách 1: Sử dụng Git (khuyến nghị nếu dự án có trên kho lưu trữ):**
        Mở terminal (hoặc Command Prompt/PowerShell trên Windows) và chạy lệnh sau:
        ```bash
        git clone <URL_CUA_KHO_LUU_TRU> ten_thu_muc_du_an
        cd ten_thu_muc_du_an
        ```
        (Thay thế `<URL_CUA_KHO_LUU_TRU>` bằng URL thực tế của kho lưu trữ và `ten_thu_muc_du_an` bằng tên thư mục bạn muốn cho dự án.)
    *   **Cách 2: Tải trực tiếp:**
        Nếu bạn có mã nguồn dưới dạng tệp ZIP, hãy giải nén nó vào một thư mục trên máy tính của bạn và di chuyển vào thư mục đó bằng terminal.

2.  **Tạo và kích hoạt môi trường ảo:**
    Việc sử dụng môi trường ảo giúp cô lập các gói phụ thuộc của dự án, tránh xung đột với các dự án Python khác.
    ```bash
    # Di chuyển vào thư mục gốc của dự án (nếu bạn chưa ở đó)
    # cd ten_thu_muc_du_an 

    # Tạo một môi trường ảo có tên là 'venv' (bạn có thể đặt tên khác nếu muốn)
    python -m venv venv

    # Kích hoạt môi trường ảo:
    # Trên Windows:
    venv\Scripts\activate
    # Trên macOS/Linux:
    source venv/bin/activate
    ```
    Sau khi kích hoạt, bạn sẽ thấy `(venv)` (hoặc tên môi trường ảo của bạn) ở đầu dòng lệnh của terminal.

3.  **Cài đặt các thư viện phụ thuộc:**
    Khi môi trường ảo đã được kích hoạt, cài đặt tất cả các thư viện cần thiết.
    Nếu dự án có tệp `requirements.txt` (khuyến nghị), bạn có thể cài đặt bằng lệnh:
    ```bash
    pip install -r requirements.txt
    ```
    Nếu không có tệp `requirements.txt`, bạn cần cài đặt các thư viện được liệt kê (ví dụ như các thư viện chính của dự án này):
    ```bash
    pip install flask tensorflow scikit-learn pandas numpy openpyxl
    ```
    *Khuyến nghị mạnh mẽ:* Sau khi cài đặt thành công các thư viện theo cách thủ công, bạn nên tạo tệp `requirements.txt`. Điều này giúp người khác (hoặc chính bạn trong tương lai) dễ dàng cài đặt lại môi trường và quản lý các gói phụ thuộc một cách nhất quán:
    ```bash
    pip freeze > requirements.txt
    ```

Sau khi hoàn thành các bước này, môi trường phát triển của bạn đã sẵn sàng. Bạn có thể chuyển sang phần "Sử dụng" để biết cách chạy ứng dụng.

## Sử dụng

### Khởi động nhanh

1.  Chạy ứng dụng:
    ```bash
    python app/app.py
    ```
2.  Khi bạn thấy thông báo `Running on http://127.0.0.1:5000`, hãy mở trình duyệt web và truy cập vào địa chỉ `http://127.0.0.1:5000` để sử dụng giao diện.

### Huấn luyện với dữ liệu mới

Nếu bạn muốn huấn luyện lại mô hình với dữ liệu mới:

1.  **Chuẩn bị dữ liệu:**
    *   Đặt tệp dữ liệu mới của bạn (ví dụ: `new_data.xlsx`) vào thư mục `data/`. Tệp này phải có cấu trúc tương tự như `data/toxic_comments_with_positive.xlsx` (ví dụ: một cột chứa văn bản bình luận và một cột chứa nhãn độc hại/không độc hại).
    *   **Lưu ý:** Cập nhật tên tệp và các cột dữ liệu tương ứng trong tệp `preprocess.py` nếu cần.

2.  **Xóa mô hình và dữ liệu tiền xử lý cũ (nếu có):**
    *   `model/mlp_model.h5`
    *   `model/preprocessed_data.pkl`

3.  **Chạy các kịch bản (script) theo thứ tự sau:**
    ```bash
    python preprocess.py
    python train_model.py
    python app/app.py
    ```

4.  Khi bạn thấy thông báo `Running on http://127.0.0.1:5000`, hãy mở trình duyệt web và truy cập vào địa chỉ `http://127.0.0.1:5000` để sử dụng giao diện với mô hình đã được huấn luyện lại.

## Cấu trúc tệp tin

```
.
├── api/                  # (Có thể dành cho API trong tương lai)
├── app/                  # Chứa mã nguồn ứng dụng Flask
│   ├── app.py            # Tệp chính của ứng dụng Flask
│   ├── comments.db       # Cơ sở dữ liệu SQLite (nếu có sử dụng)
│   ├── static/           # Chứa các tệp tĩnh (CSS, JS, hình ảnh)
│   │   └── uploads/      # Thư mục lưu trữ hình ảnh tải lên (nếu có)
│   └── templates/        # Chứa các mẫu HTML
│       └── index.html    # Trang giao diện chính
├── data/                 # Chứa dữ liệu huấn luyện
│   └── toxic_comments_with_positive.xlsx # Tệp dữ liệu ví dụ
├── model/                # Chứa mô hình đã huấn luyện và dữ liệu tiền xử lý
│   ├── mlp_model.h5      # Tệp mô hình Keras đã huấn luyện
│   └── preprocessed_data.pkl # Tệp dữ liệu đã được tiền xử lý (tokenizer, label encoder)
├── preprocess.py         # Kịch bản tiền xử lý dữ liệu
├── readme.md             # Tệp README này
├── train_model.py        # Kịch bản huấn luyện mô hình
└── venv/                 # Thư mục môi trường ảo (nếu có)
```
