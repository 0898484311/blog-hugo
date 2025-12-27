# Thư mục Images

Thư mục này dùng để chứa các hình ảnh cho blog của bạn.

## Cấu trúc ảnh được sử dụng

### 1. Ảnh Profile (About page)
- **Đường dẫn**: `/images/profile.jpg` hoặc `/images/profile-placeholder.jpg`
- **Kích thước đề xuất**: 200x200px hoặc 400x400px
- **Format**: JPG, PNG, WebP

### 2. Ảnh Cover cho bài viết
- **Đường dẫn**: `/images/socket-java-cover.jpg`
- **Kích thước đề xuất**: 1200x630px (tỷ lệ 1.91:1 cho social media)
- **Format**: JPG, PNG

### 3. Ảnh minh họa trong bài viết
- **Đường dẫn**: `/images/socket-overview.png`
- **Đường dẫn**: `/images/client-server-arch.png`
- **Đường dẫn**: `/images/socket-flow.png`
- **Kích thước đề xuất**: 800-1200px chiều rộng
- **Format**: PNG, JPG, SVG

### 4. Ảnh OG (Open Graph) cho SEO
- **Đường dẫn**: `/images/og-image.png`
- **Kích thước đề xuất**: 1200x630px
- **Format**: PNG, JPG

## Cách thêm ảnh

1. Đặt ảnh vào thư mục `static/images/`
2. Trong file markdown, sử dụng cú pháp:
   ```markdown
   ![Alt text](/images/ten-file.jpg)
   ```
3. Hoặc sử dụng shortcode figure của Hugo:
   ```markdown
   {{< figure src="/images/ten-file.jpg" alt="Mô tả" caption="Chú thích" >}}
   ```

## Lưu ý

- Tên file nên không có khoảng trắng, sử dụng dấu gạch ngang (-) thay thế
- Nén ảnh trước khi upload để tối ưu tốc độ tải trang
- Sử dụng format WebP nếu có thể để giảm dung lượng







