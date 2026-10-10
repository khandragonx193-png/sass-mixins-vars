# Thực hành: Tạo Mixins & Biến để tối ưu CSS

## Mục tiêu đã hoàn thành

- ✅ Tạo **variables** kiểm soát toàn bộ giao diện (màu, font-size, padding, shadow...)
- ✅ Tạo **mixins** giảm lặp code (`button-style`, `box-style`, `heading-style`)
- ✅ Áp dụng mixins & biến vào components
- ✅ Tổ chức theo cấu trúc chuẩn: `abstracts` → `base` → `components`

## Cấu trúc thư mục

```
sass-mixins-vars/
├── abstracts/
│   ├── _variables.scss   # Tất cả biến (colors, fonts, spacing, shadows)
│   └── _mixins.scss      # Mixins tái sử dụng
├── base/
│   └── _typography.scss  # h1, h2 + body
├── components/
│   ├── _buttons.scss     # .button, .button--secondary
│   └── _cards.scss       # .card
├── css/
│   └── styles.css        # Kết quả biên dịch
├── main.scss
├── index.html
└── README.md
```

## CSS trước khi tối ưu

```css
h1 { font-size: 32px; color: #222; }
h2 { font-size: 28px; color: #222; }
.button {
  background: red;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}
.card {
  background: white;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
}
```

## Sau khi tối ưu với Variables + Mixins

**Variables** (`abstracts/_variables.scss`):
```scss
$primary-color: red;
$text-color: #222;
$font-large: 32px;
$font-medium: 28px;
$padding-standard: 10px 20px;
$box-shadow-default: 2px 2px 10px rgba(0, 0, 0, 0.1);
```

**Mixins** (`abstracts/_mixins.scss`):
```scss
@mixin button-style($bg-color) { ... }
@mixin box-style { ... }
@mixin heading-style($size) { ... }
```

**Áp dụng**:
```scss
h1 { @include heading-style($font-large); }
.button { @include button-style($primary-color); }
.card { @include box-style; }
```

## Cách biên dịch

```bash
npx sass main.scss css/styles.css
npx sass main.scss css/styles.css --watch   # chế độ theo dõi
```

## Lợi ích

| Thay đổi muốn làm              | Cách thực hiện                  |
|--------------------------------|---------------------------------|
| Đổi màu nút primary            | Sửa `$primary-color`            |
| Đổi kích thước tiêu đề         | Sửa `$font-large` / `$font-medium` |
| Thêm button màu khác           | `@include button-style(#màu)`   |
| Thêm card mới                  | `@include box-style`            |
