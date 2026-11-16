# Quy tắc viết CHANGELOG.md

Áp dụng cho `CHANGELOG.md` của mọi thư viện/dự án. Changelog là bản ghi **đầy đủ** của từng phiên bản dành cho lập trình viên nâng cấp: có gì mới, có gì đổi, và app cũ cần làm gì. README chỉ giữ vài phiên bản gần nhất (xem `readme-rules.md`).

Tuân thủ [Semantic Versioning](https://semver.org/lang/vi/) và tinh thần Keep a Changelog.

## 1. Cấu trúc file

```markdown
# Nhật ký thay đổi (Changelog)

<Một đoạn giới thiệu: nơi ghi, tuân thủ Semantic Versioning.>

---

## [<Phiên bản>] - <yyyy-MM-dd>

<Tóm tắt 1–2 câu nếu bản này có chủ đề chung (tùy chọn).>

### ⚠️ Thay đổi gây lỗi tương thích (Breaking)
### ✨ Thêm mới (Added)
### 🔄 Thay đổi (Changed)
### 🗑️ Loại bỏ (Deprecated / Removed)
### 🐛 Sửa lỗi (Fixed)
### 🔒 Bảo mật (Security)
### 📌 Ghi chú nâng cấp
```

- Mục mới thêm **ngay dưới dòng `---`**, trên phiên bản trước; không sửa mục của phiên bản đã phát hành (trừ khi sửa lỗi chính tả hoặc bổ sung thiếu sót).
- Chỉ giữ nhóm có nội dung; giữ nguyên thứ tự nhóm như trên.
- Ngày theo định dạng `yyyy-MM-dd`, là ngày phát hành, không phải ngày viết.
- Mỗi phiên bản phát hành có đúng một mục, khớp với `Version` trong file dự án.

## 2. Phân loại thay đổi

| Nhóm | Dùng khi |
|---|---|
| **Breaking** | Xóa hoặc đổi tên thành phần công khai; đổi kiểu, chữ ký, giá trị enum; đổi hành vi mặc định; đổi khoảng phiên bản phụ thuộc bắt buộc. Code cũ biên dịch lỗi hoặc chạy khác đi. |
| **Added** | Thêm thành phần công khai, tính năng, tùy chọn mới mà code cũ không bị ảnh hưởng. |
| **Changed** | Đổi nội bộ hoặc đổi hành vi không làm hỏng code cũ: nâng phiên bản phụ thuộc, tinh chỉnh, định dạng lại. |
| **Deprecated / Removed** | Đánh dấu `[Obsolete]` hoặc gỡ bỏ thành phần đã cảnh báo từ trước. |
| **Fixed** | Sửa lỗi. |
| **Security** | Sửa vấn đề bảo mật: lỗ hổng, rò rỉ dữ liệu, xác thực/phân quyền sai, phụ thuộc có lỗ hổng đã biết. Nêu loại vấn đề và phiên bản bị ảnh hưởng; **không** mô tả chi tiết cách khai thác. Nếu bản vá buộc app đổi code hoặc cấu hình thì ghi thêm vào Breaking và Ghi chú nâng cấp. |
| **Ghi chú nâng cấp** | Các bước app cũ cần làm, thứ tự phải gán, điều cần kiểm tra sau khi nâng. |

Chọn số phiên bản theo Semantic Versioning: Breaking → tăng phiên bản chính (hoặc theo quy ước của dự án nếu khác), Added → tăng phụ, Fixed/Security/Changed nhỏ → tăng bản vá.

## 3. Cách viết từng dòng

- Bắt đầu bằng **tên file, class hoặc thành phần in đậm**, sau dấu hai chấm là mô tả ngắn một câu.
- Viết điều người dùng thấy và cần làm, không kể quá trình nội bộ ("đổi tên biến", "dọn code" chỉ ghi khi có ảnh hưởng).
- Breaking phải nêu rõ: cái gì bị xóa/đổi, thay bằng gì, app cũ sửa thế nào.
- Mỗi phiên bản luôn có một dòng nâng `Version` (từ bản cũ lên bản mới) ở nhóm Changed.
- Tên kiểu, phương thức, thuộc tính, lệnh để trong dấu backtick.
- Chỉ ghi điều có thật trong diff hoặc đã được xác nhận. Điều suy đoán (ví dụ hành vi phía server) phải nói rõ là suy ra, hoặc hỏi lại trước khi ghi.

## 4. Không đưa vào changelog

- Nội dung build, đóng gói, khóa publish, đường dẫn máy cá nhân.
- Thay đổi chỉ trong tài liệu hoặc công cụ hỗ trợ không ảnh hưởng người dùng thư viện (ghi một dòng gộp nếu cần, ví dụ "bổ sung tài liệu").
- Dữ liệu nhạy cảm: khóa, token, mật khẩu, địa chỉ nội bộ thật.
- Chi tiết cách khai thác một lỗ hổng chưa được vá rộng rãi; mục Security chỉ nêu loại vấn đề và cách nâng cấp.

## 5. Quan hệ với tài liệu khác

| Khi phát hành phiên bản mới | Việc phải làm |
|---|---|
| Thêm mục vào CHANGELOG | Thêm một dòng đầu bảng "Lịch sử thay đổi" trong README, giữ tối đa 3 dòng, in đậm Breaking |
| Có Breaking | Ghi trong "Ghi chú nâng cấp" và cập nhật spec/hướng dẫn liên quan |
| Đổi khoảng phiên bản phụ thuộc hoặc target framework | Cập nhật mục "Yêu cầu và tương thích" trong README |
