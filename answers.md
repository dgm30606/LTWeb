# 📋 PHIẾU BÀI TẬP 01 — TRÌNH BÀY ANSWERS Dung chat lam lai di

---

## PHẦN A — KIỂM TRA ĐỌC HIỂU (20 điểm)

### Câu A1 (5đ) — HTTP & Browser

**Trả lời:**

Khi bạn gõ `https://shopee.vn` vào trình duyệt và nhấn Enter, đây là **5 bước chính** xảy ra (theo thứ tự):

1. **DNS Lookup** → Trình duyệt gửi yêu cầu đến DNS server để phân giải tên miền `shopee.vn` thành địa chỉ IP.
2. **TCP Connection (3-way Handshake)** → Thiết lập kết nối TCP với máy chủ ở địa chỉ IP đó, sử dụng port 443 (HTTPS).
3. **TLS Handshake** → Tạo liên kết mã hóa an toàn (SSL/TLS) giữa client và server.
4. **HTTP Request** → Trình duyệt gửi HTTP request (GET) để lấy file HTML chính.
5. **HTTP Response & HTML Parsing** → Server trả về HTML document, trình duyệt parse HTML và tạo DOM tree.
6. **Resource Loading** → Trình duyệt phát hiện thẻ `<link>` (CSS), `<script>`, `<img>` → gửi thêm request lấy các tài nguyên này.
7. **Rendering** → Browser render CSS, layout trang, paint pixels lên màn hình (render tree + layout tree).

**Nguồn tham chiếu:** File `01_introduction_html_universe.md` — Phần "HTTP Request & Response Flow"

---

### Câu A2 (5đ) — Semantic HTML

**Trả lời:**

Đoạn HTML dưới đây bị Google đánh giá SEO thấp vì **4 lỗi semantic chính**:

#### Lỗi 1: Dùng `<div class="header">` thay vì `<header>`
```html
<!-- ❌ SAI -->
<div class="header">

<!-- ✅ ĐÚNG -->
<header>
```
**Lý do:** `<header>` là thẻ semantic, Google hiểu đây là phần đầu trang. `<div>` chỉ là container vô nghĩa, SEO không công nhận.

#### Lỗi 2: Dùng `<div class="menu">` thay vì `<nav>`
```html
<!-- ❌ SAI -->
<div class="menu">
    <div><a href="/">Trang chủ</a></div>
    <div><a href="/products">Sản phẩm</a></div>
</div>

<!-- ✅ ĐÚNG -->
<nav>
    <a href="/">Trang chủ</a>
    <a href="/products">Sản phẩm</a>
</nav>
```
**Lý do:** `<nav>` báo hiệu đây là navigation chính, Google xem trọng khi crawl link. Việc dùng `<div>` làm mất thông tin này.

#### Lỗi 3: Dùng `<div class="main">` thay vì `<main>`
```html
<!-- ❌ SAI -->
<div class="main">

<!-- ✅ ĐÚNG -->
<main>
```
**Lý do:** `<main>` định rõ nội dung chính của trang, giúp search engine hiểu trang bố cục tốt hơn.

#### Lỗi 4: Dùng `<div class="product">` thay vì `<article>`
```html
<!-- ❌ SAI -->
<div class="product">
    <div class="title">iPhone 16 Pro</div>
    <div class="price">25.990.000đ</div>
    <div class="image"><img src="iphone.jpg"></div>
</div>

<!-- ✅ ĐÚNG -->
<article>
    <h3>iPhone 16 Pro</h3>
    <p>Mô tả sản phẩm...</p>
    <p><strong>25.990.000đ</strong></p>
    <figure>
        <img src="iphone.jpg" alt="iPhone 16 Pro">
    </figure>
</article>
```
**Lý do:** `<article>` cho biết đây là nội dung độc lập (sản phẩm), Google sẽ index nó riêng. Thêm heading tags (`<h3>`) và `<figure>` giúp tăng SEO.

#### Lỗi 5 (Bổ sung): Dùng `<div class="footer">` thay vì `<footer>`
```html
<!-- ❌ SAI -->
<div class="footer">© 2026 ShopTLU</div>

<!-- ✅ ĐÚNG -->
<footer>© 2026 ShopTLU</footer>
```

**Bản HTML sửa chữa:**
```html
<header>
    <nav>
        <a href="/">Trang chủ</a>
        <a href="/products">Sản phẩm</a>
    </nav>
</header>

<main>
    <article>
        <h3>iPhone 16 Pro</h3>
        <p>Điện thoại flagship mới nhất</p>
        <figure>
            <img src="iphone.jpg" alt="iPhone 16 Pro">
            <figcaption>iPhone 16 Pro — Màu Titan</figcaption>
        </figure>
        <p><strong>25.990.000đ</strong></p>
    </article>
</main>

<footer>© 2026 ShopTLU</footer>
```

**Nguồn tham chiếu:** File `04_semantic_html5.md` — Phần "Semantic tags for better SEO"

---

### Câu A3 (5đ) — Block vs Inline

**Trả lời:**

#### Kết quả hiển thị (Text Art):
```
┌─────────────────────────────────────┐
│ Hộp 1                               │ (block: chiếm toàn bộ chiều rộng)
└─────────────────────────────────────┘
Text A Text B (inline: nằm trên cùng dòng)
┌─────────────────────────────────────┐
│ Hộp 2                               │ (block)
└─────────────────────────────────────┘
Text C Text D (inline: nằm trên cùng dòng)
┌─────────────────────────────────────┐
│ Hộp 3                               │ (block)
└─────────────────────────────────────┘
```

#### Giải thích:

1. **`<div>Hộp 1</div>`** — `<div>` là **block element** → chiếm toàn bộ chiều rộng, xuống dòng mới.
2. **`<span>Text A</span>`** — `<span>` là **inline element** → chỉ chiếm không gian của text, nằm trên cùng dòng với element tiếp theo.
3. **`<span>Text B</span>`** — Vẫn inline, nằm cạnh "Text A" trên cùng dòng.
4. **`<div>Hộp 2</div>`** — Block element, buộc xuống dòng mới (ngay cả khi span trước chưa hết dòng).
5. **`<span>Text C</span>`** + **`<strong>Text D</strong>`** — Cả 2 đều là inline (strong cũng inline), nằm trên cùng dòng.
6. **`<div>Hộp 3</div>`** — Block element, xuống dòng mới.

#### Tại sao?
- **Block elements** (`<div>`, `<h1>`, `<p>`, `<section>`) → Có margin-top/bottom mặc định, luôn bắt đầu trên dòng mới
- **Inline elements** (`<span>`, `<a>`, `<strong>`, `<b>`, `<em>`) → Không có margin-top/bottom, tuân theo chiều chữ (left-to-right)
- Khi block element xuất hiện, nó "reset" dòng hiện tại, tất cả inline element còn lại phải xuống dòng mới

**Nguồn tham chiếu:** File `02_html_structure_semantics.md` — Phần "Block vs Inline Elements"

---

### Câu A4 (5đ) — Table

**Trả lời:**

#### Sự khác nhau giữa `<thead>`, `<tbody>`, `<tfoot>`:

| Phần | Ý Nghĩa | Nội Dung | Ví Dụ |
|-----|---------|---------|-------|
| **`<thead>`** | Table Head (Đầu bảng) | Chứa hàng tiêu đề (header row) | `<th>Tên</th>`, `<th>Giá</th>` |
| **`<tbody>`** | Table Body (Thân bảng) | Chứa các dòng dữ liệu chính | `<tr><td>iPhone</td><td>25tr</td></tr>` |
| **`<tfoot>`** | Table Footer (Chân bảng) | Chứa hàng tóm tắt/ghi chú cuối | `<td colspan="2">Tổng cộng: ...</td>` |

**Ví dụ cụ thể:**
```html
<table>
    <thead>  <!-- Phần tiêu đề -->
        <tr>
            <th>Tên Sản Phẩm</th>
            <th>Giá</th>
        </tr>
    </thead>
    <tbody>  <!-- Phần dữ liệu chính -->
        <tr>
            <td>iPhone 16</td>
            <td>25.990.000đ</td>
        </tr>
        <tr>
            <td>Samsung S25</td>
            <td>24.990.000đ</td>
        </tr>
    </tbody>
    <tfoot>  <!-- Phần chân/tóm tắt -->
        <tr>
            <td colspan="2">Cập nhật: Tháng 4/2026</td>
        </tr>
    </tfoot>
</table>
```

---

#### Tại sao KHÔNG NÊN dùng table để tạo layout trang web? (3 lý do chính)

**Lý do 1: Không Responsive — Khó thích ứng màn hình nhỏ**
- Table dựa trên fixed columns, không thể reflow để phù hợp mobile.
- CSS Grid / Flexbox có thể tự động thay đổi khi màn hình co giãn.
- Ví dụ: Bố cục 2 cột trên desktop → 1 cột trên mobile rất khó với table.

```html
<!-- ❌ SAI: Dùng table làm layout -->
<table>
    <tr>
        <td style="width: 20%;">Sidebar</td>
        <td style="width: 80%;">Main Content</td>
    </tr>
</table>

<!-- ✅ ĐÚNG: Dùng CSS Grid -->
<div style="display: grid; grid-template-columns: 20% 80%;">
    <aside>Sidebar</aside>
    <main>Main Content</main>
</div>
```

**Lý do 2: SEO & Accessibility kém**
- Screen reader đọc table theo hàng/cột (header → data), không hiểu được layout.
- Google crawl table kỳ vọng nó chứa dữ liệu có cấu trúc, không phải layout.
- Người khiếm thị nghe "Bảng 5 cột 10 hàng" sẽ rất bối rối.

**Lý do 3: Hiệu năng kém**
- Table phải load & render toàn bộ trước khi hiển thị (không lazy-load được).
- Nested table (table trong table) làm tăng độ phức tạp, tốc độ render chậm.
- HTML code thừa thãi do nhiều `<tr>`, `<td>`, `colspan`, `rowspan`.

```html
<!-- ❌ SAI: Table layout phức tạp, khó maintain -->
<table>
    <tr>
        <td colspan="2"><table><tr><td>...</td></tr></table></td>
    </tr>
</table>

<!-- ✅ ĐÚNG: Semantic + CSS -->
<header>...</header>
<main>...</main>
<aside>...</aside>
<footer>...</footer>
```

**Kết luận:** Table chỉ nên dùng để hiển thị **dữ liệu dạng bảng** (bảng giá, so sánh sản phẩm, thống kê), KHÔNG dùng cho **layout trang web**.

**Nguồn tham chiếu:** File `05_tables_hyperlinks.md` — Phần "Table Purpose & Semantic Structure"

---

## PHẦN B — THỰC HÀNH CODE (60 điểm)

### Bài B3 — Danh Sách Lỗi & Cách Sửa

**File gốc (có lỗi):** File gốc trong đề bài có **ít nhất 12 lỗi** như sau:

| # | Dòng | Lỗi | Chi Tiết | Cách Sửa |
|---|------|-----|---------|----------|
| 1 | 1 | DOCTYPE không đầy đủ | `<!DOCTYPE>` thiếu `html` | `<!DOCTYPE html>` |
| 2 | 2 | Thiếu `lang` attribute | `<html>` không xác định ngôn ngữ | `<html lang="vi">` |
| 3 | 3 | Thiếu meta tags quan trọng | Không có `charset` và `viewport` | Thêm `<meta charset="UTF-8">` và `<meta name="viewport" content="width=device-width, initial-scale=1.0">` |
| 4 | 4 | Title tag không đóng | `<title>Trang web` thiếu `</title>` | `<title>Trang web</title>` |
| 5 | 5 | Charset format sai | `<meta charset="utf8">` | `<meta charset="UTF-8">` (đúng format chuẩn) |
| 6 | 8 | H1 closing tag sai | `<h1>Welcome to ShopTLU<h1>` → 2 opening tags | `<h1>Welcome to ShopTLU</h1>` |
| 7 | 11 | Anchor closing tag sai | `<a href="home">Trang chủ<a>` → 2 opening tags | `<a href="home">Trang chủ</a>` |
| 8 | 16 | Img thiếu quotes & alt | `<img src=iphone.jpg>` (thiếu quotes, thiếu alt) | `<img src="iphone.jpg" alt="Hình ảnh iPhone 16 Pro">` |
| 9 | 18 | Tag nesting sai thứ tự | `<p>Giá: <b>25.990.000đ</p></b>` → `</p>` đóng trước `</b>` | `<p>Giá: <strong>25.990.000đ</strong></p>` |
| 10 | 24-31 | Table thiếu `<thead>`, `<tbody>` | Dùng `<tr>` trực tiếp trong `<table>` | Wrap tiêu đề trong `<thead>`, dữ liệu trong `<tbody>` |
| 11 | 35 | Duplicate `<main>` tag | Có 2 thẻ `<main>` (dòng 13 & 33) | Chỉ nên có 1 `<main>`, phần "Sidebar" phải dùng `<aside>` |
| 12 | 40 | Footer paragraph không đóng | `<p>Copyright 2026` thiếu `</p>` | `<p>Copyright 2026</p>` |
| 13 | 42 | Thiếu `lang` trong `<html>` | (bổ sung) | Thêm `lang="vi"` |

**Bản HTML đã sửa:** Xem file `debug.html` trong folder `PBT_01/` ✅

**Nguồn tham chiếu:** File `01_introduction_html_universe.md` & `03_html_validation.md`

---

## PHẦN C — SUY LUẬN (20 điểm)

### Câu C1 (10đ) — Thiết kế cấu trúc trang Chi Tiết Sản Phẩm

**HTML Structure (Semantic):**

```html
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chi Tiết Sản Phẩm - ShopTLU</title>
</head>
<body>
    <!-- Header & Navigation -->
    <header>
        <nav>
            <a href="/">Trang Chủ</a>
            <a href="/products">Sản Phẩm</a>
            <a href="/cart">Giỏ Hàng</a>
        </nav>
    </header>

    <main>
        <!-- Breadcrumb Navigation -->
        <nav aria-label="breadcrumb">
            <!-- nav vì đây là điều hướng trang web -->
            <ol>
                <!-- ol (ordered list) vì breadcrumb có thứ tự từ trang chủ → chi tiết -->
                <li><a href="/">Trang Chủ</a></li>
                <li><a href="/products">Điện Thoại</a></li>
                <li><a href="/products/iphone">iPhone</a></li>
                <li aria-current="page">iPhone 16 Pro Max</li>
                <!-- aria-current="page" báo rằng đây là trang hiện tại -->
            </ol>
        </nav>

        <!-- Sản Phẩm Chính (article vì nội dung độc lập) -->
        <article>
            <!-- Section Ảnh Sản Phẩm -->
            <section aria-label="Hình ảnh sản phẩm">
                <!-- section vì đây là phần riêng biệt của trang -->
                <figure>
                    <!-- figure vì chứa một nhóm ảnh có mối liên hệ với nhau -->
                    <img src="iphone-main.jpg" alt="iPhone 16 Pro Max - Màu Titan">
                    <figcaption>Ảnh chính sản phẩm</figcaption>
                </figure>
                <div>
                    <!-- div được dùng ở đây vì đơn thuần là container styling cho gallery ảnh nhỏ -->
                    <img src="thumb1.jpg" alt="Góc 1">
                    <img src="thumb2.jpg" alt="Góc 2">
                    <img src="thumb3.jpg" alt="Góc 3">
                    <img src="thumb4.jpg" alt="Góc 4">
                    <img src="thumb5.jpg" alt="Góc 5">
                </div>
            </section>

            <!-- Section Thông Tin Sản Phẩm -->
            <section aria-label="Thông tin sản phẩm">
                <!-- section vì chứa thông tin chi tiết sản phẩm -->
                <h1>iPhone 16 Pro Max</h1>
                <!-- h1 vì đây là heading chính của trang -->
                
                <div aria-label="Đánh giá">
                    <!-- div được phép vì không có semantic tag phù hợp cho rating stars -->
                    <span>⭐⭐⭐⭐⭐</span>
                    <span>(1.234 đánh giá)</span>
                </div>

                <p>Mô tả sản phẩm: Điện thoại flagship mới nhất từ Apple...</p>

                <div aria-label="Giá tiền">
                    <!-- div để nhóm giá cũ và giá mới -->
                    <p><del>26.990.000đ</del></p>
                    <p><strong>25.990.000đ</strong></p>
                </div>

                <!-- Bảng Thông Số Kỹ Thuật -->
                <table>
                    <!-- table vì đây là dữ liệu tabular (spec sản phẩm) -->
                    <thead>
                        <tr>
                            <th>Thông Số</th>
                            <th>Chi Tiết</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Màn Hình</td>
                            <td>6.9 inch OLED 120Hz</td>
                        </tr>
                        <tr>
                            <td>Chip</td>
                            <td>A18 Pro</td>
                        </tr>
                        <tr>
                            <td>Camera</td>
                            <td>Chính 48MP + Macro 12MP</td>
                        </tr>
                        <tr>
                            <td>Pin</td>
                            <td>4852 mAh, sạc 45 phút</td>
                        </tr>
                    </tbody>
                </table>
            </section>

            <!-- Section Đánh Giá & Bình Luận -->
            <section aria-label="Đánh giá khách hàng">
                <!-- section vì chứa reviews từ người dùng -->
                <h2>Đánh Giá Từ Khách Hàng</h2>
                <article>
                    <!-- article cho mỗi review (nội dung độc lập, có thể syndicate) -->
                    <header>
                        <!-- header cho info người review -->
                        <p><strong>Nguyễn Văn A</strong></p>
                        <time datetime="2026-04-15">15 tháng 4</time>
                    </header>
                    <p>Sản phẩm rất tốt, đúng như mô tả...</p>
                </article>
                <article>
                    <header>
                        <p><strong>Trần Thị B</strong></p>
                        <time datetime="2026-04-14">14 tháng 4</time>
                    </header>
                    <p>Giao hàng nhanh, chất lượng ok...</p>
                </article>
            </section>
        </article>
    </main>

    <!-- Sidebar: Sản Phẩm Tương Tự -->
    <aside aria-label="Sản phẩm liên quan">
        <!-- aside vì nội dung bổ sung, không phải nội dung chính -->
        <h2>Sản Phẩm Tương Tự</h2>
        <ul>
            <!-- ul cho danh sách sản phẩm không có thứ tự -->
            <li><a href="/iphone-16-pro">iPhone 16 Pro</a></li>
            <li><a href="/iphone-16">iPhone 16</a></li>
            <li><a href="/iphone-15-pro">iPhone 15 Pro</a></li>
        </ul>
    </aside>

    <!-- Footer -->
    <footer>
        <!-- footer vì nội dung chân trang (copyright, links) -->
        <nav aria-label="Liên kết chân trang">
            <!-- nav vì chứa links điều hướng -->
            <ul>
                <li><a href="/policy">Chính Sách</a></li>
                <li><a href="/contact">Liên Hệ</a></li>
                <li><a href="/faq">FAQ</a></li>
            </ul>
        </nav>
        <p>&copy; 2026 ShopTLU. All rights reserved.</p>
    </footer>
</body>
</html>
```

**Giải thích lựa chọn semantic tags:**
- `<header>` & `<footer>` → Phần đầu/cuối trang
- `<nav>` → Điều hướng (breadcrumb, main nav)
- `<main>` → Nội dung chính của trang
- `<article>` → Nội dung độc lập (sản phẩm, review)
- `<section>` → Nhóm nội dung có quan hệ (ảnh, thông tin, reviews)
- `<aside>` → Sidebar, nội dung bổ sung
- `<table>` → Dữ liệu tabular (spec kỹ thuật)
- `<figure>` & `<figcaption>` → Ảnh + mô tả
- `<time>` → Timestamp (ngày tháng review)

---

### Câu C2 (10đ) — Phản Biện: Semantic HTML vs Div-Class

**Bài viết (200-300 từ):**

---

**Tiêu đề:** "Tại sao Semantic HTML quan trọng hơn bạn tưởng"

**Nội dung:**

Quan điểm rằng "dùng `<div>` + class cho mọi thứ là đủ" là một sai lầm phổ biến. Semantic HTML không chỉ là "học thêm thẻ", mà là nền tảng của web modern. Dưới đây là lý do tại sao:

**1. SEO & Indexing (Lý do kỹ thuật #1)**

Google crawl HTML không chỉ dựa vào class names (CSS không được Google parse trong lần crawl đầu). Google dựa vào HTML tags để hiểu cấu trúc trang. Ví dụ:

```html
❌ <div class="header"><div class="nav">...<a>Link</a>...</div></div>
✅ <header><nav>...<a>Link</a>...</nav></header>
```

Với cách thứ hai, Google hiểu ngay đây là phần header, nav là phần điều hướng. Với cách thứ nhất, Google phải "đoán" class name, hay bỏ qua nếu không quen thuộc. Kết quả: trang semantic được index tốt hơn, rank cao hơn trên SERP.

**2. Accessibility (Lý do kỹ thuật #2)**

Screen reader (công cụ đọc màn hình cho người khiếm thị) phụ thuộc 100% vào HTML semantics. Khi người dùng quang cảnh một trang web:

```html
❌ <div class="article">
     <div class="title">Tiêu đề bài viết</div>
     <div class="content">...</div>
   </div>
❌ Screen reader: "Nội dung"... "không biết đây là gì"

✅ <article>
     <h1>Tiêu đề bài viết</h1>
     <p>...</p>
   </article>
✅ Screen reader: "Article, heading 1, Tiêu đề bài viết"
```

Người dùng có thể dùng phím tắt skip đến `<article>` tiếp theo, jump đến heading tiếp theo. Với `<div>`, họ phải lướt từng dòng code.

**3. Ví dụ cụ thể:**

**Tiki.vn** (ví dụ trang e-commerce thực tế):
- Khi bạn mở DevTools → Elements, tìm phần sản phẩm
- Tiki dùng `<article>` cho mỗi product card (semantic ✅)
- Giá cố định ở trong `<strong>` hay `<span class="price">` (Google hiểu `<strong>` = quan trọng)
- Kết quả: Snippet Google Shopping hiển thị giá Tiki tự động, không phải Tiki setup hard-coded

vs trang dùng toàn `<div>`:
- Phải dùng structured data (`<script type="application/ld+json">`) để Google hiểu giá
- Thêm công việc, dễ lỗi, khó bảo trì

**4. Trường hợp `<div>` vẫn phù hợp:**

Không phải lúc nào cũng dùng semantic tag. Ví dụ:
```html
✅ <div class="layout-wrapper"> <!-- container styling chỉ -->
     <header>...</header>
     <main>...</main>
   </div>

✅ <div class="grid"> <!-- styling container cho CSS Grid -->
     <article>Product 1</article>
     <article>Product 2</article>
   </div>
```

**Kết luận:** Semantic HTML + CSS Grid/Flexbox + Structured Data = trang web modern, tốt cho SEO, accessibility, và user experience. Đó là lý do mọi trang web lớn (Shopee, Tiki, Facebook) đều tuân theo standard này. Học semantic HTML là đầu tư hợp lý cho sự nghiệp lập trình viên web.

**Nguồn tham chiếu:** File `04_semantic_html5.md` — Phần "Why Semantic HTML Matters"

---

**✅ Tất cả câu trả lời Phần A & C đã hoàn thành!**
