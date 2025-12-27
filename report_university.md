BÁO CÁO ĐỒ ÁN/PROJECT

Tên đồ án: Website Blog cá nhân (Hugo + PaperMod)

Sinh viên: [Họ và tên]

Mã sinh viên: [MSSV]

Lớp: [Lớp]

Giảng viên hướng dẫn: [Tên GV]

Khoa/Ngành: [Khoa - Ngành]

Trường: [Tên Trường]

Thời gian thực hiện: [Tháng Năm]

-----------------------------

LỜI CAM ĐOAN

Tôi xin cam đoan đây là kết quả làm việc của cá nhân/tập thể (ghi rõ) trong quá trình thực hiện đồ án. Mọi ý tưởng, đoạn mã hoặc nội dung tham khảo đã được trích dẫn đầy đủ.

Người làm đồ án (ký tên): _____________________

-----------------------------

LỜI CẢM ƠN

Trân trọng cảm ơn giảng viên hướng dẫn, bạn bè và tất cả những người đã góp ý, hỗ trợ trong quá trình hoàn thành đồ án.

-----------------------------

TÓM TẮT (ABSTRACT)

Báo cáo trình bày quá trình thiết kế và triển khai một website blog cá nhân sử dụng trình tạo site tĩnh Hugo và theme PaperMod. Mục tiêu của dự án là xây dựng nền tảng để chia sẻ bài viết kỹ thuật về Java, JavaScript và các chủ đề lập trình, đồng thời đáp ứng các yêu cầu cơ bản về SEO, phân loại nội dung, và tối ưu hiệu năng.

Từ khoá: Hugo, PaperMod, blog tĩnh, SEO, website tĩnh

-----------------------------

MỤC LỤC

1. Giới thiệu
2. Mục tiêu và phạm vi
3. Tổng quan công nghệ
4. Phân tích và thiết kế
5. Triển khai
6. Kiểm thử và đánh giá
7. Kết luận và hướng phát triển
8. Tài liệu tham khảo
9. Phụ lục

-----------------------------

1. GIỚI THIỆU

1.1 Bối cảnh

Trong thời đại số, việc chia sẻ kiến thức qua blog là phương thức hiệu quả để lưu trữ và phổ biến bài viết chuyên môn. Site tĩnh có lợi thế về tốc độ, bảo mật và chi phí hosting thấp.

1.2 Mục tiêu

- Xây dựng một blog cá nhân dễ quản lý, thân thiện với SEO.
- Cho phép phân loại bài viết, tag, tìm kiếm và trang tĩnh như About, Projects.
- Tối ưu hóa tài nguyên (CSS/JS, hình ảnh) để tải nhanh.

1.3 Phạm vi

Xây dựng frontend tĩnh bằng Hugo và PaperMod; không bao gồm hệ thống backend động (ví dụ user management, login).

-----------------------------

2. TỔNG QUAN CÔNG NGHỆ

2.1 Hugo

Hugo là một static site generator viết bằng Go, nổi bật với tốc độ build nhanh và cấu trúc rõ ràng.

2.2 Theme PaperMod

PaperMod cung cấp giao diện responsive, nhiều cấu hình, hỗ trợ tối ưu SEO sẵn có.

2.3 Công cụ và môi trường

- Hệ điều hành phát triển: Windows
- Lệnh phát triển: `hugo server`
- Lệnh build: `hugo --minify`

-----------------------------

3. PHÂN TÍCH VÀ THIẾT KẾ

3.1 Yêu cầu chức năng

- Hiển thị danh sách bài viết, bài chi tiết.
- Phân loại theo categories và tags.
- Tìm kiếm nội dung.
- Trang About và Projects.

3.2 Thiết kế kiến trúc

- Cấu trúc thư mục chính:
  - `content/` : bài viết và trang
  - `layouts/` : template và partials
  - `assets/` : nguồn CSS/JS
  - `static/` : tài nguyên tĩnh
  - `public/` : output sau khi build

-----------------------------

4. TRIỂN KHAI

4.1 Tổ chức nội dung

Tất cả bài viết đặt dưới `content/posts/`. Trang tìm kiếm nằm tại `content/search/index.md`.

4.2 Tùy chỉnh giao diện

Tinh chỉnh một vài partials trong `layouts/partials/` (ví dụ `extend_footer.html`, `index_profile.html`) để thêm thông tin cá nhân và liên kết mạng xã hội.

4.3 Tối ưu tài nguyên

- Sử dụng minify cho CSS/JS khi build.
- Nén ảnh và đặt các ảnh trong `static/images/`.

-----------------------------

5. KIỂM THỬ VÀ ĐÁNH GIÁ

5.1 Kiểm thử chức năng

- Kiểm tra hiển thị bài viết, phân trang, tag, categories.
- Kiểm tra hoạt động tìm kiếm.

5.2 Kiểm tra tương thích

- Kiểm tra responsive trên mobile và desktop.

5.3 Kiểm thử hiệu năng và SEO

- Kiểm tra sitemap, robots và meta tags.

-----------------------------

6. KẾT LUẬN VÀ HƯỚNG PHÁT TRIỂN

6.1 Kết luận

Dự án cung cấp một blog tĩnh ổn định, dễ triển khai và phù hợp cho chia sẻ kiến thức. Sử dụng Hugo và PaperMod giúp rút ngắn thời gian phát triển.

6.2 Hướng phát triển

- Thêm CI/CD (GitHub Actions) để tự động build và deploy.
- Tích hợp hệ thống bình luận (Disqus/Staticman).
- Cải thiện SEO nâng cao (JSON-LD, schema.org).

-----------------------------

7. TÀI LIỆU THAM KHẢO

- Hugo Documentation - https://gohugo.io
- PaperMod Theme - https://github.com/adityatelange/paper-mod

-----------------------------

8. PHỤ LỤC

- Danh sách file cấu trúc project (chỉ mục rút gọn):
  - `content/`
  - `layouts/`
  - `assets/css/`, `assets/js/`
  - `static/images/`

-----------------------------

Ghi chú: Thay phần thông tin cá nhân (tên, MSSV, giảng viên, khoa, thời gian) theo mẫu trường trước khi nộp. Có thể yêu cầu xuất ra PDF/Word nếu cần.
