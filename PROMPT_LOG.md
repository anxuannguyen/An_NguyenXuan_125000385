# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)
- **Họ và tên:** Nguyễn Xuân An
- **MSSV:** 125000385
- **Tên đề tài Website:** Thiết Kế Website Cửa Hàng Đồ Uống Hiện Đại ("Brew & Chill Coffee")
- **Công cụ AI đã sử dụng:** Google Antigravity (Gemini 3.8 Flash), VS Code / Antigravity IDE

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)
> *Ghi lại prompt tổng quan ban đầu bạn dùng để khởi tạo khung website.*

```text
Bạn là một Senior Front-end Developer với 10 năm kinh nghiệm. Hãy thiết kế và viết mã nguồn hoàn chỉnh (HTML5, CSS3 tích hợp sẵn trong file hoặc style riêng) cho một website cửa hàng đồ uống hiện đại (ví dụ: "Brew & Chill Coffee"). 

Website bắt buộc phải tuân thủ nghiêm ngặt các tiêu chuẩn kỹ thuật sau:

1. Chuẩn Semantic HTML5 (Tối thiểu 7 thành phần ngữ nghĩa):
- Sử dụng đúng thẻ <header> chứa logo và thanh điều hướng chính.
- Sử dụng thẻ <nav> cho menu điều hướng.
- Sử dụng thẻ <main> làm vùng chứa toàn bộ nội dung trọng tâm.
- Sử dụng các thẻ <section> và <article> để phân chia rạch ròi các khối nội dung (Ví dụ: Hero Section, Featured Menu, About Us, Reviews).
- Sử dụng thẻ <aside> cho phần thông tin phụ (Ví dụ: Giờ vàng giảm giá hoặc tin tức nhanh).
- Sử dụng thẻ <footer> cho chân trang (thông tin liên hệ, copyright, mạng xã hội).

2. Kỹ thuật CSS & CSS Variables:
- Khai báo đầy đủ block :root với các CSS Variables quản lý hệ thống design tokens:
  + Màu sắc: --primary-color, --secondary-color, --accent-color, --text-color, --bg-color, --card-bg.
  + Typography: --font-main, --font-heading.
  + Spacing & Radius: --spacing-sm, --spacing-md, --spacing-lg, --border-radius.
- Áp dụng triệt để CSS Grid và CSS Flexbox cho việc bố cục layout, đảm bảo tính responsive mượt mà trên cả Mobile và Desktop.

3. Tương tác & Hiệu ứng (Libraries & Custom CSS):
- Tích hợp CDN của Animate.css và áp dụng các class hiệu ứng cho phần tử chính (Tiêu đề, Hero Section, CTA Button).
- Tích hợp thư viện AOS (Animate On Scroll) qua CDN và khởi tạo JS để tạo hiệu ứng cuộn trang mượt mà cho các section.
- Viết thuần bằng CSS cho các hiệu ứng tương tác nâng cao: :hover, :focus cho các nút bấm (scale nhẹ, đổi bóng đổ box-shadow) và các thẻ sản phẩm (cards) có hiệu ứng phóng to ảnh bên trong (zoom-in) kèm hiệu ứng nổi khối.

Yêu cầu đầu ra: Cung cấp toàn bộ mã nguồn HTML và CSS rõ ràng, có chú thích chi tiết bằng tiếng Việt để dễ dàng tùy chỉnh.
không sử dụng jvs, hãy tách htlm và css ra riêng
```

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung Semantic HTML & Hệ thống CSS Variables (`:root`)
- **Prompt đã dùng:**
  > "Hãy kiểm tra lại cấu trúc HTML để đảm bảo tuân thủ nghiêm ngặt chuẩn Semantic HTML5 với ít nhất 7 thành phần ngữ nghĩa. Đảm bảo phân chia rõ ràng giữa `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`. Khai báo đầy đủ block `:root` với bảng màu sắc ấm áp cho quán cà phê đặc sản (Specialty Coffee), font chữ sang trọng và hệ thống spacing chuẩn."
- **Kết quả AI tạo ra:**
  - AI đã phân chia bố cục tổng quan với `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`.
  - Trong CSS, AI đã khởi tạo khối `:root` với đầy đủ các biến: `--primary-color: #d49b57`, `--secondary-color: #1a120d`, `--accent-color: #f38235`, `--text-color: #f7ede2`, `--bg-color: #0d0907`, `--card-bg`, cùng font chữ `Playfair Display` kết hợp `Plus Jakarta Sans`.
- **Nhận xét & Tinh chỉnh của SV:**
  - AI ban đầu còn lạm dụng nhiều thẻ `<div>` bên trong các section và chưa tận dụng hết các thẻ ngữ nghĩa hỗ trợ SEO.
  - Sinh viên yêu cầu AI tinh chỉnh:
    1. Chuyển từng khối đồ uống trong thực đơn thành thẻ `<article class="drink-card">`.
    2. Sử dụng `<figure>` và `<figcaption>` để bọc ảnh sản phẩm thay vì dùng `<div>`.
    3. Thêm thẻ `<aside id="golden-hour">` chứa thông tin Giờ Vàng giảm giá 30% kèm thẻ `<time>` và `<mark>`.
    4. Thêm `<address>` cho khối liên hệ ở `<footer>` và `<details>` / `<summary>` cho mục Hỏi - Đáp (FAQ).

---

### Lần 2: Xử lý Thư viện Hiệu ứng & Ràng buộc "Không Dùng JavaScript"
- **Prompt đã dùng:**
  > "Lưu ý trong đề bài có yêu cầu 'không sử dụng jvs' (không dùng JavaScript). Nếu tích hợp AOS thì bắt buộc phải chạy `AOS.init()` bằng JS, điều này vi phạm yêu cầu. Hãy giải quyết bài toán này như thế nào để vừa có hiệu ứng đẹp mắt vừa thuần 100% HTML5 & CSS3?"
- **Kết quả AI tạo ra:**
  - AI đã phân tích sự mâu thuẫn giữa việc dùng AOS (cần JS) và yêu cầu loại bỏ hoàn toàn JavaScript.
  - Giải pháp của AI:
    1. Tích hợp CDN của **Animate.css** (thư viện 100% CSS thuần) vào thẻ `<head>`: áp dụng các class như `animate__animated animate__fadeInDown`, `animate__fadeInUp`, `animate__pulse animate__infinite` vào Header, Hero Badge, Title và CTA Buttons.
    2. Thay thế AOS bằng thuộc tính CSS hiện đại `html { scroll-behavior: smooth; }` kết hợp các hiệu ứng chuyển động CSS `@keyframes` tự nhiên, đảm bảo không có bất kỳ thẻ `<script>` nào trong mã nguồn.
- **Nhận xét & Tinh chỉnh của SV:**
  - Giải pháp rất chuẩn xác và tuân thủ đúng yêu cầu khắt khe của bài thi/đề tài. Trang web tải nhanh, nhẹ, không phụ thuộc vào script bên thứ ba.

---

### Lần 3: Xử lý Tương tác Phức tạp bằng 100% Pure CSS (Menu Mobile, Filter Tabs, FAQ)
- **Prompt đã dùng:**
  > "Khi không dùng JavaScript, làm thế nào để người dùng trên điện thoại có thể bấm mở menu Hamburger, bấm chọn các danh mục đồ uống (Cà phê pha máy, Cold Brew, Trà) để lọc món, và bấm xem câu hỏi thường gặp FAQ?"
- **Kết quả AI tạo ra:**
  - AI áp dụng các kỹ thuật đỉnh cao của CSS3:
    1. **Mobile Menu:** Dùng *CSS Checkbox Hack* (`<input type="checkbox" id="nav-toggle">` ẩn) kết hợp `<label for="nav-toggle">` và selector `input:checked ~ .main-navigation`. Khi bấm vào nút hamburger, icon 3 sọc tự xoay thành dấu X và menu trượt mượt mà ra từ trên xuống.
    2. **Bộ lọc danh mục (Tabs Filter):** Dùng nhóm các `<input type="radio" name="menu-category">` kết hợp bộ chọn CSS `:checked ~ .menu-grid .drink-card` để tự động ẩn/hiện sản phẩm tương ứng.
    3. **Accordion FAQ:** Tận dụng cặp thẻ ngữ nghĩa HTML5 `<details>` và `<summary>`, tự động đóng/mở mượt mà và xoay icon mũi tên khi active mà không cần 1 dòng code JS nào.
- **Nhận xét & Tinh chỉnh của SV:**
  - Kỹ thuật này thể hiện trình độ Senior Front-end rất cao, giao diện hoạt động trơn tru 100% trên cả Desktop và thiết bị di động.

---

### Lần 4: Tách riêng file HTML & CSS, Hoàn thiện hiệu ứng Hover Nổi Khối 3D & Zoom-in
- **Prompt đã dùng:**
  > "Hãy tách riêng mã nguồn thành 2 file riêng biệt: index.html và style.css. Trong file style.css, hãy viết chi tiết hiệu ứng tương tác nâng cao cho các thẻ sản phẩm (.drink-card): khi rê chuột vào thì thẻ nổi khối 3D lên (translateY, bóng đổ phát sáng) và ảnh sản phẩm bên trong phóng to mượt mà (zoom-in). Nút bấm :hover phải có hiệu ứng scale và glowing box-shadow."
- **Kết quả AI tạo ra:**
  - Tách thành 2 file độc lập [index.html](file:///z:/An_NguyenXuan_125000385/index.html) và [style.css](file:///z:/An_NguyenXuan_125000385/style.css), liên kết chuẩn qua thẻ `<link rel="stylesheet" href="style.css">`.
  - Viết đầy đủ CSS cho `.drink-card`:
    - `transition: transform 0.4s cubic-bezier(0.2, 0.8, 0.2, 1), box-shadow 0.4s, border-color 0.3s;`
    - `:hover`: `transform: translateY(-8px);`, viền sáng màu hổ phách, bóng đổ `--shadow-card-hover`.
  - Viết cho ảnh `.card-img`:
    - `overflow: hidden;` ở khung cha `.image-wrapper`.
    - `:hover .card-img`: `transform: scale(1.12); filter: brightness(1.06); transition: transform 0.6s cubic-bezier(0.25, 1, 0.5, 1);`.
  - Viết cho các nút bấm:
    - `.btn-primary:hover`: `transform: translateY(-3px) scale(1.02); box-shadow: var(--shadow-glow);`.
    - Trạng thái `:focus-visible` có viền outline màu cam hổ phách đạt chuẩn tiếp cận Web Accessibility (A11y).
- **Nhận xét & Tinh chỉnh của SV:**
  - Hiệu ứng thị giác cực kỳ cao cấp (WOW effect), tạo cảm giác sang trọng như các thương hiệu cà phê quốc tế (Starbucks Reserve, % Arabica).
  - Code được chú thích tiếng Việt đầy đủ từng phần, dễ đọc và dễ bảo trì.

---

### Lần 5: Chuẩn hóa thư mục `assets` chứa toàn bộ hình ảnh thực tế của dự án
- **Prompt đã dùng:**
  > "Hãy tạo cho tôi 1 thư mục assets được sử dụng"
  > "File assets chứa các hình ảnh đã được sử dụng trong dự án"
- **Kết quả AI tạo ra:**
  - Khởi tạo thư mục chuẩn `assets/images/` và lưu trữ cục bộ toàn bộ 12 hình ảnh đã sử dụng trong dự án:
    1. `hero-espresso.jpg`: Ảnh ly cà phê Espresso chủ đạo của Hero Section.
    2. `drink-coldbrew-orange.jpg`: Ảnh Cold Brew Cam Vàng Mật Ong.
    3. `drink-salted-caramel.jpg`: Ảnh Salted Caramel Macchiato.
    4. `drink-matcha-latte.jpg`: Ảnh Matcha Latte Uji Kyoto.
    5. `drink-espresso-conpanna.jpg`: Ảnh Espresso Con Panna Cổ Điển.
    6. `drink-tra-dao-cam-sa.jpg`: Ảnh Trà Đào Cam Sả Hoàng Gia.
    7. `drink-sparkling-berry.jpg`: Ảnh Sparkling Wild Berry Tea.
    8. `about-barista.jpg`: Ảnh nghệ nhân Barista pha chế V60 thủ công (About Us).
    9. `avatar-hoang-lan.jpg`: Ảnh đại diện khách hàng Hoàng Lan.
    10. `avatar-tuan-minh.jpg`: Ảnh đại diện khách hàng Trần Tuấn Minh.
    11. `avatar-thuc-anh.jpg`: Ảnh đại diện khách hàng Nguyễn Thục Anh.
    12. `favicon.svg`: Icon tách cà phê bốc khói vector SVG chuẩn nét cao cho trình duyệt.
  - Cập nhật toàn bộ các thẻ `<img>` và `<link rel="icon">` trong [index.html](file:///z:/An_NguyenXuan_125000385/index.html) để nạp trực tiếp từ `assets/images/`.
  - Giữ nguyên cấu trúc file tách rời theo đúng yêu cầu đề bài: [style.css](file:///z:/An_NguyenXuan_125000385/style.css) ở thư mục gốc và liên kết `<link rel="stylesheet" href="style.css">`.
- **Nhận xét & Tinh chỉnh của SV:**
  - Dự án hiện đã hoạt động hoàn toàn offline 100%, không còn phụ thuộc vào kết nối mạng Unsplash bên ngoài. Trang web tải nhanh tức thì và đầy đủ tài nguyên cục bộ sẵn sàng để đóng gói nộp bài.

---

## 3. Tổng kết bài học kinh nghiệm (Key Takeaways & Reflection)

1. **Khả năng làm chủ và định hướng AI (Prompt Engineering):**
   - AI rất thông minh nhưng nếu prompt mơ hồ thì kết quả thường chung chung hoặc dùng thẻ `<div>` tùy tiện.
   - Khi đưa ra các ràng buộc kỹ thuật rõ ràng (Semantic HTML5, CSS Variables, Pure CSS không JS, tách file), AI sẽ phát huy tối đa vai trò là một cộng sự lập trình cấp cao.
2. **Kỹ thuật Pure CSS hiện đại:**
   - Hiểu sâu về các kỹ thuật `:checked pseudo-class`, `<details>/<summary>`, `scroll-behavior` giúp giải quyết được các bài toán tương tác phức tạp mà không làm nặng trang web với JavaScript không cần thiết.
3. **Tư duy thẩm mỹ & Trải nghiệm người dùng (UX/UI):**
   - Việc phối màu theo chủ đề (Tông màu cà phê rang mộc `#1a120d` kết hợp hổ phách `#d49b57` và cam mật ong `#f38235`) cùng các hiệu ứng micro-interactions (zoom-in, float up, glowing shadow) nâng tầm trải nghiệm của người dùng ngay từ cái nhìn đầu tiên.
