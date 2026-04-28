# Hướng dẫn dịch Rust by Example sang tiếng Việt

Tài liệu này mô tả quy trình và các quy tắc để dịch dự án Rust by Example (RBE) sang tiếng Việt.
Để biết các hướng dẫn đóng góp chung, vui lòng xem tệp [CONTRIBUTING.md].

[CONTRIBUTING.md]: https://github.com/rust-lang/rust-by-example/blob/master/CONTRIBUTING.md

## Quy trình dịch thuật

### Chuẩn bị

RBE sử dụng [mdbook-i18n-helpers](https://github.com/google/mdbook-i18n-helpers) làm khung dịch thuật.
Bạn cần cài đặt các công cụ sau:

- GNU gettext utilities (`msgmerge` và `msgcat`)
- mdbook-i18n-helpers (`cargo install mdbook-i18n-helpers`)

### Tạo và cập nhật bản dịch

Vui lòng xem tệp [mdbook-i18n-helpers USAGE](https://github.com/google/mdbook-i18n-helpers/blob/main/i18n-helpers/USAGE.md) để biết chi tiết.
Dưới đây là tóm tắt các lệnh:

#### Tạo tệp mẫu (message template)

Tệp `po/messages.pot` là cần thiết để tạo hoặc cập nhật bản dịch.

```bash
MDBOOK_OUTPUT='{"xgettext": {"pot-file": "messages.pot"}}' \
  mdbook build -d po
```

#### Tạo tài nguyên dịch mới cho tiếng Việt

Mã ngôn ngữ cho tiếng Việt là `vi`.

```bash
msginit -i po/messages.pot -l vi -o po/vi.po
```

#### Cập nhật tài nguyên dịch hiện có

Khi nội dung gốc tiếng Anh thay đổi, hãy chạy lệnh sau để cập nhật tệp `.po`:

```bash
msgmerge --update po/vi.po po/messages.pot
```

#### Theo dõi tiến độ dịch

```bash
msgfmt --statistics po/vi.po
```

### Chỉnh sửa nội dung dịch

Bạn có thể mở tệp `po/vi.po` bằng các trình soạn thảo văn bản hoặc công cụ chuyên dụng như [Poedit](https://poedit.net/).
Hãy viết nội dung dịch vào phần `msgstr`.
Để xem trước bản dịch cục bộ:

```bash
MDBOOK_BOOK__LANGUAGE=vi mdbook build
MDBOOK_BOOK__LANGUAGE=vi mdbook serve
```

## Nguyên tắc dịch thuật cho tiếng Việt

### Phong cách và tông giọng

- **Tông giọng:** Sử dụng văn phong kỹ thuật, rõ ràng, ngắn gọn và lịch sự. Tránh dùng từ ngữ quá trang trọng hoặc quá thân mật.
- **Đại từ:** Sử dụng "chúng ta" hoặc ẩn chủ ngữ khi hướng dẫn. Tránh dùng "tôi" hoặc "mình".
- **Tự nhiên:** Ưu tiên cách diễn đạt tự nhiên trong tiếng Việt thay vì dịch sát từng từ (word-by-word).

### Quy tắc kỹ thuật

- **KHÔNG dịch:**
  - Các từ khóa của Rust (ví dụ: `fn`, `let`, `match`, `impl`).
  - Tên kiểu dữ liệu gốc (ví dụ: `i32`, `String`, `Vec`).
  - Tên tệp và đường dẫn (ví dụ: `main.rs`, `src/lib.rs`).
- **Chú thích trong mã (Code comments):** Cần dịch chú thích để người học dễ hiểu, trừ khi chú thích đó là tên biến hoặc thuật ngữ chuyên môn không nên dịch.
- **Liên kết:** Giữ nguyên các liên kết Markdown trừ khi có phiên bản tiếng Việt tương ứng.

### Quy tắc định dạng và dấu câu

- **Dấu câu:** Sử dụng dấu câu theo chuẩn tiếng Việt (dấu phẩy, dấu chấm sát vào chữ phía trước, có khoảng trắng phía sau).
- **Khoảng trắng:** Thêm một khoảng trắng giữa chữ tiếng Việt và các ký tự Latinh hoặc số để tăng khả năng đọc (ví dụ: "Biến `x` có kiểu `i32`").
- **Thuật ngữ chuyên môn:** Đối với các thuật ngữ quan trọng, có thể viết bản dịch tiếng Việt trước và kèm theo thuật ngữ tiếng Anh trong ngoặc đơn ở lần xuất hiện đầu tiên. Ví dụ: "Sở hữu (ownership)".

## Các lỗi thường gặp và ví dụ

| Nội dung              | Sai                                 | Đúng                             |
| :-------------------- | :---------------------------------- | :------------------------------- |
| Dịch thuật ngữ quá đà | "Cái thùng (crate) này chứa..."     | "Crate này chứa..."              |
| Dấu câu               | "Chào bạn ,chúc mừng ."             | "Chào bạn, chúc mừng."           |
| Chú thích mã          | `// print to console`               | `// in ra màn hình console`      |
| Rust keywords         | `Khai báo một cấu trúc tên là User` | `Khai báo một struct tên là Use` |

## Bảng thuật ngữ (Glossary)

| Thuật ngữ (EN)   | Tiếng Việt                                                 | Ghi chú                       |
| :--------------- | :--------------------------------------------------------- | :---------------------------- |
| Example          | Ví dụ                                                      |                               |
| Snippet          | Đoạn mã                                                    |                               |
| Output           | Kết quả đầu ra / Output                                    |                               |
| Exercise         | Bài tập                                                    |                               |
| Note             | Ghi chú                                                    |                               |
| Ownership        | Quyền sở hữu                                               |                               |
| Borrowing        | Mượn / Việc mượn                                           |                               |
| Lifetime         | Vòng đời / Lifetime                                        |                               |
| Trait            | Trait                                                      | Thường giữ nguyên             |
| Generic          | Tổng quát / Generic                                        |                               |
| Implementation   | Triển khai / Thực thi                                      |                               |
| Binding          | Liên kết / 束縛 (Sử dụng 'Ràng buộc' hoặc 'Liên kết biến') |                               |
| Pattern matching | Khớp mẫu                                                   |                               |
| Destructuring    | Phân rã                                                    |                               |
| Crate            | Crate                                                      | Không nên dịch là "Cái thùng" |
| Module           | Module                                                     |                               |

## Thêm ngôn ngữ vào hệ thống xây dựng

Sau khi hoàn tất bản dịch cơ bản, hãy thêm ngôn ngữ `vi` vào các tệp sau trong kho lưu trữ chính:

- `.github/workflows/rbe.yml`
- `theme/head.hbs`
- `src/bootstrap/src/core/build_steps/doc.rs` (trong kho [rust-lang/rust](https://github.com/rust-lang/rust))

Chi tiết định dạng xem tại mục "Add a language entry" trong tệp `TRANSLATING.md` gốc.
