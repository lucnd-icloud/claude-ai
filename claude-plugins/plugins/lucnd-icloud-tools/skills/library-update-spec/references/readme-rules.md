# Quy tắc viết README.md

Áp dụng cho `README.md` của mọi thư viện/dự án. Nếu README được đóng gói vào NuGet (`PackageReadmeFile`), nó là **trang duy nhất người dùng thấy trên nuget.org**, nên phải tự đủ nội dung. Tài liệu chi tiết (spec, hướng dẫn) và changelog đầy đủ nằm ngoài README và có thể không đi kèm gói.

README trả lời ba câu hỏi: thư viện này làm gì, cài thế nào, dùng ra sao.

## 1. Cấu trúc

Giữ đúng thứ tự. Mục "Có" là bắt buộc, mục khác chỉ thêm khi có nội dung thật.

| # | Mục (dùng đúng tên tiêu đề này) | Bắt buộc | Nội dung |
|---|---|---|---|
| 1 | `# <Tên thư viện>` + 1–2 câu mô tả | Có | Làm gì, cho ai. Không quảng cáo. |
| 2 | `## Chức năng chính` | Có | 3–6 gạch đầu dòng, mỗi dòng một khả năng cụ thể. |
| 3 | `## Yêu cầu và tương thích` | Có | Bảng target framework hỗ trợ và thư viện phụ thuộc kèm khoảng phiên bản. Gộp Requirements, Compatibility và Dependencies vào đây, không tách ba mục. |
| 4 | `## Cài đặt` | Không (bỏ khi gói đã có sẵn trên NuGet) | Một lệnh cài (ví dụ `dotnet add package <PackageId>`) hoặc khai báo `PackageReference`. Chỉ thêm khi gói không lấy được trực tiếp từ nguồn mặc định. |
| 5 | `## Sử dụng` | Có | Ví dụ chạy được, ngắn, theo thứ tự thực tế: khởi tạo → gọi → xử lý kết quả. |
| 6 | `## Cấu hình` | Nếu cần | Bảng thuộc tính/option cấu hình, bắt buộc hay tùy chọn, giá trị mặc định, thứ tự phải gán. |
| 7 | `## Lịch sử thay đổi` | Nên có | Bảng vài phiên bản gần nhất + link tới changelog (xem mục 3). |
| 8 | `## Giấy phép` | Theo chính sách phát hành | Một dòng, khớp với giấy phép khai báo trong file dự án. Thư viện nội bộ ghi: "Thư viện nội bộ (private), chỉ dùng trong tổ chức. Không sao chép hoặc phân phối ra ngoài." Mã nguồn mở thì ghi tên giấy phép (ví dụ MIT). |

Chi tiết kỹ thuật chỉ dành cho lập trình viên nội bộ (ví dụ cơ chế mã hóa, cờ debug) không đưa vào README; để ở tài liệu spec.

## 2. Nội dung từng mục

- **Mô tả:** nói thư viện *chứa gì* và, khi dễ nhầm, *không chứa gì* (ví dụ: không có giao diện, không có logic nghiệp vụ).
- **Ví dụ sử dụng:**
  - Dùng tên kiểu thật, giá trị giả (`https://example.com`, `"..."`); không bao giờ để khóa, token, mật khẩu thật.
  - Nói rõ điều bắt buộc làm trước nếu có (ví dụ phải gán cấu hình trước khi tạo đối tượng).
  - Ví dụ biên dịch được nếu copy; nếu rút gọn thì đánh dấu bằng chú thích `// ...`.
  - Không viết dòng gọi hàm mà bạn chưa kiểm chứng tên; thiếu thì ghi chú bằng lời thay vì đoán.
- **Cấu hình:** liệt kê đủ thuộc tính/option, và cập nhật ngay khi thêm, đổi tên hay xóa.
- **Tương thích:** ghi khoảng phiên bản của phụ thuộc chính. Đổi khoảng này hoặc đổi target framework thì phải cập nhật README.

## 3. Mục lịch sử thay đổi

- Chỉ giữ **tối đa 3 phiên bản gần nhất**, mỗi phiên bản một dòng: phiên bản, ngày, một câu.
- Thay đổi gây lỗi tương thích (Breaking) phải **in đậm** và nêu tên thành phần bị xóa hoặc đổi, vì đây có thể là chỗ duy nhất người dùng thấy.
- Thêm dòng mới ở đầu bảng, không sửa dòng cũ.
- Cuối mục là một link tới changelog đầy đủ. Chi tiết (nhóm Added/Changed, ghi chú nâng cấp) để ở changelog, không chép vào README.

## 4. Quy tắc cho README đóng gói NuGet

- **Link phải là link đầy đủ** (`https://...`). Link tương đối có thể hỏng trên nuget.org vì file được trỏ tới không nằm trong gói và đường dẫn trong repo có thể không trùng gốc repo.
- Không trỏ tới file chỉ có trên máy hoặc trong repo nội bộ mà người dùng không truy cập được.
- Không nhắc tới mục/đoạn của file khác nếu file đó không đi kèm gói.
- Không đưa nội dung build, đóng gói, khóa publish, đường dẫn máy cá nhân.
- Giữ README ngắn: mục 1–5 vừa một màn hình; chi tiết đẩy sang tài liệu ngoài và dùng link đầy đủ.

## 5. Phong cách

- Tiếng Việt, tiêu đề dùng đúng tên ở bảng mục 1.
- Tên kiểu, phương thức, thuộc tính, lệnh để trong dấu backtick.
- Dùng bảng cho dữ liệu có cột (phiên bản, cấu hình), gạch đầu dòng cho khả năng, khối code có chỉ định ngôn ngữ (` ```csharp `).
- Không dùng emoji trong tiêu đề README (changelog thì được).

## 6. Khi nào phải cập nhật README

| Thay đổi | Mục cần sửa |
|---|---|
| Nâng phiên bản | Lịch sử thay đổi (thêm dòng đầu) |
| Đổi target framework hoặc khoảng phiên bản phụ thuộc | Yêu cầu và tương thích |
| Thêm/đổi/xóa thuộc tính cấu hình | Cấu hình, Sử dụng |
| Thêm khả năng mới đáng kể | Chức năng chính |
| Đổi giấy phép | Giấy phép |
