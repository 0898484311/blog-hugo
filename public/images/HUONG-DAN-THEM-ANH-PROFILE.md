# Hướng dẫn thêm ảnh Profile

## Cách 1: Đặt ảnh trong thư mục static (Đơn giản nhất) ✅

1. **Đặt ảnh của bạn vào thư mục này** với tên: `profile.jpg`
   - Đường dẫn đầy đủ: `static/images/profile.jpg`
   
2. **Yêu cầu về ảnh:**
   - Tên file: `profile.jpg` (hoặc `profile.png`, `profile.webp`)
   - Kích thước đề xuất: 200x200px hoặc 400x400px (ảnh vuông)
   - Format: JPG, PNG, hoặc WebP
   - Ảnh sẽ tự động được resize thành hình tròn

3. **Cập nhật đường dẫn trong `hugo.toml`** (đã được cấu hình sẵn):
   ```toml
   imageUrl = "/images/profile.jpg"
   ```

## Cách 2: Đặt ảnh trong thư mục assets (Để Hugo tự động xử lý)

1. **Tạo thư mục** `assets/images/` (nếu chưa có)

2. **Đặt ảnh vào** `assets/images/profile.jpg`

3. **Cập nhật đường dẫn trong `hugo.toml`:**
   ```toml
   imageUrl = "images/profile.jpg"  # Không có dấu / ở đầu
   ```

## Lưu ý

- Profile mode đã được bật (`enabled = true`) trong `hugo.toml`
- Ảnh sẽ hiển thị ở trang chủ khi profile mode được bật
- Nếu không muốn dùng profile mode, đặt `enabled = false` trong `hugo.toml`
- Ảnh sẽ tự động được resize theo `imageWidth` và `imageHeight` trong cấu hình

## Sau khi thêm ảnh

Chạy lại Hugo server để xem kết quả:
```bash
hugo server
```

