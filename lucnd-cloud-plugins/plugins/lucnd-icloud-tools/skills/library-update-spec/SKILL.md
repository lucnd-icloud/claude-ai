---
name: library-update-spec
description: Cập nhật CHANGELOG.md, README.md và các spec/CLAUDE.md của một thư viện .NET (NuGet) khi có phiên bản mới. Dùng khi người dùng gõ /library-update-spec, hoặc yêu cầu "cập nhật spec/changelog/readme cho phiên bản mới" của một thư viện lucnd-icloud. Chỉ sửa file tài liệu, không build, không push NuGet, không commit.
disable-model-invocation: true
allowed-tools: Bash(git diff:*), Bash(git log:*), Bash(git status:*), Read, Edit
---

Cập nhật tài liệu cho phiên bản hiện tại của thư viện đang mở (thư mục làm việc là gốc thư viện, nơi có file `.csproj`). Ghi chú thêm từ người dùng (nếu có): $ARGUMENTS

Quy tắc viết nằm cạnh skill này, đọc đúng khi cần:
- `references/changelog-rules.md` – quy tắc viết `CHANGELOG.md` (bắt buộc đọc ở bước 2).
- `references/readme-rules.md` – quy tắc viết `README.md` (bắt buộc đọc ở bước 4).

## Giới hạn để tiết kiệm token (bắt buộc)

- **Không** dùng Glob/Grep/tìm kiếm toàn repo. **Không** đọc file ngoài: diff ở bước 1, `CLAUDE.md` của thư viện, file `.md` cần sửa, và hai file quy tắc ở trên.
- **Không** đọc cả file `.cs`; dùng nội dung diff. Chỉ `Read` một file `.cs` khi diff không đủ để hiểu thay đổi.
- Sửa bằng `Edit` đúng đoạn cần đổi, **không** ghi đè cả file.
- Không build, không chạy script đóng gói/đẩy gói, không sửa `.cs` hay `.csproj`, không commit.

## Bước 1 – Xác định thay đổi

1. Tìm file dự án ở thư mục hiện tại (`*.csproj`, chỉ cấp đầu, không đệ quy) và đọc `<Version>`.
2. Lấy diff từ lần cập nhật changelog gần nhất, gồm cả thay đổi chưa commit, bằng một lệnh:

   `git diff $(git log -1 --format=%H -- CHANGELOG.md) -w -- "*.cs" "*.csproj"`

   (Nếu chưa có `CHANGELOG.md` thì dùng `git status --short .` và diff với `HEAD`.)
3. Nếu `CHANGELOG.md` đã có mục cho đúng `<Version>` thì chỉ bổ sung vào mục đó, không tạo mục trùng. Diff rỗng thì dừng và báo "không có thay đổi mã nguồn".

## Bước 2 – CHANGELOG.md

`Read` `references/changelog-rules.md`, rồi `Read` 25 dòng đầu của `CHANGELOG.md` để lấy định dạng. `Edit` chèn mục mới ngay dưới dòng `---`, trên phiên bản trước. Chỉ ghi điều có trong diff; điều suy đoán thì nói rõ hoặc hỏi người dùng.

## Bước 3 – Spec và CLAUDE.md theo vùng thay đổi

1. `Read` `CLAUDE.md` của thư viện, lấy **bảng định tuyến/cấu trúc thư mục** (thư mục code ↔ file spec).
2. Từ danh sách file trong diff, chỉ mở spec ứng với thư mục bị đổi. Dùng `Edit` sửa đúng dòng/bảng bị ảnh hưởng: bảng API, danh sách trường, bảng "Class → file" (nếu có), mục lưu ý.
3. Thêm class mới → thêm dòng vào bảng "Class → file"; class bị xóa/đổi tên → sửa hoặc bỏ dòng.
4. Thay đổi làm đổi quy tắc bắt buộc (khởi tạo, thành phần nên dùng, thuộc tính `[Obsolete]`) → sửa đúng dòng đó trong `CLAUDE.md`.
5. Thư viện không có `CLAUDE.md` hoặc không có bảng định tuyến → báo người dùng, không tự đoán file spec.

## Bước 4 – README.md

`Read` `references/readme-rules.md`, rồi `Edit` `README.md` theo bảng "Khi nào phải cập nhật README" trong đó (thêm dòng đầu bảng lịch sử, giữ tối đa 3 dòng, in đậm Breaking; sửa mục Yêu cầu/Cấu hình/Sử dụng nếu liên quan). Không đưa chi tiết dành riêng cho lập trình viên nội bộ vào README.

## Kết thúc

Báo ngắn: phiên bản, danh sách file tài liệu đã sửa, và các điểm không chắc cần người dùng xác nhận.
