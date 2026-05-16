<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Thời Báo Công Nghệ & Cuộc Sống</title>
    <!-- Tích hợp Tailwind CSS để làm giao diện nhanh -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
    </style>
</head>
<body class="bg-gray-50 text-gray-900">

    <!-- HEADER / NAVIGATION -->
    <header class="bg-white shadow-md sticky top-0 z-50">
        <div class="container mx-auto px-4 py-4 flex justify-between items-center">
            <a href="#" class="text-2xl font-bold text-red-600 tracking-wider">THỜI BÁO 24H</a>
            <nav class="hidden md:flex space-x-6 font-semibold text-gray-700">
                <a href="#" class="hover:text-red-600 transition">Trang chủ</a>
                <a href="#" class="hover:text-red-600 transition">Chính trị</a>
                <a href="#" class="hover:text-red-600 transition">Công nghệ</a>
                <a href="#" class="hover:text-red-600 transition">Kinh doanh</a>
                <a href="#" class="hover:text-red-600 transition">Giải trí</a>
            </nav>
            <div class="flex items-center space-x-4">
                <button class="bg-red-600 text-white px-4 py-1.5 rounded text-sm font-medium hover:bg-red-700">Đăng nhập</button>
            </div>
        </div>
    </header>

    <!-- MAIN CONTENT CONTAINER -->
    <main class="container mx-auto px-4 py-8">
        
        <!-- SECTION 1: TIN TIÊU ĐIỂM (BREAKING NEWS) -->
        <section class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-12">
            <!-- Bài viết lớn bên trái -->
            <div class="lg:col-span-2 bg-white rounded-lg overflow-hidden shadow-sm hover:shadow-md transition">
                <img src="https://images.unsplash.com/photo-1526374965328-7f61d4dc18c5?w=800" alt="Tin chính" class="w-full h-96 object-cover">
                <div class="p-6">
                    <span class="text-xs font-bold text-red-600 uppercase tracking-wider">Công nghệ</span>
                    <h1 class="text-2xl md:text-3xl font-bold mt-2 mb-3 hover:text-red-600 cursor-pointer">
                        Trí tuệ nhân tạo (AI) thay đổi cục diện thị trường lao động toàn cầu trong năm 2026 như thế nào?
                    </h1>
                    <p class="text-gray-600 leading-relaxed mb-4">
                        Các báo cáo mới nhất cho thấy sự bùng nổ của các mô hình AI thế hệ mới đang buộc các doanh nghiệp phải tái cấu trúc hệ thống nhân sự, mở ra nhiều cơ hội nhưng cũng không ít thách thức...
                    </p>
                    <div class="text-xs text-gray-400">Theo Nguyễn Văn A • 2 giờ trước</div>
                </div>
            </div>

            <!-- Cột tin tức phụ bên phải -->
            <div class="space-y-6">
                <h3 class="text-lg font-bold border-b-2 border-red-600 pb-2">TIN ĐỌC NHIỀU</h3>
                
                <div class="flex space-x-4">
                    <span class="text-3xl font-extrabold text-gray-300">01</span>
                    <div>
                        <a href="#" class="font-semibold hover:text-red-600 line-clamp-2">Giá vàng hôm nay tiếp tục biến động mạnh trước áp lực lạm phát</a>
                        <span class="text-xs text-gray-400">Kinh doanh</span>
                    </div>
                </div>

                <div class="flex space-x-4">
                    <span class="text-3xl font-extrabold text-gray-300">02</span>
                    <div>
                        <a href="#" class="font-semibold hover:text-red-600 line-clamp-2">Chính sách năng lượng xanh mới được thông qua tại Nghị viện</a>
                        <span class="text-xs text-gray-400">Chính trị</span>
                    </div>
                </div>

                <div class="flex space-x-4">
                    <span class="text-3xl font-extrabold text-gray-300">03</span>
                    <div>
                        <a href="#" class="font-semibold hover:text-red-600 line-clamp-2">Đội tuyển bóng đá quốc gia chuẩn bị cho chiến dịch săn vé World Cup</a>
                        <span class="text-xs text-gray-400">Thể thao</span>
                    </div>
                </div>
            </div>
        </section>

        <hr class="border-gray-200 my-8">

        <!-- SECTION 2: DANH SÁCH TIN TỨC MỚI (Tự động load bằng JavaScript) -->
        <section>
            <h2 class="text-2xl font-bold text-gray-800 mb-6 flex items-center">
                <span class="w-2 h-6 bg-red-600 inline-block mr-2"></span>Tin mới cập nhật
            </h2>
            <!-- Nơi JavaScript sẽ bơm dữ liệu bài viết vào đây -->
            <div id="news-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- Các bài viết mẫu sẽ hiển thị ở đây -->
            </div>
        </section>

    </main>

    <!-- FOOTER -->
    <footer class="bg-gray-900 text-gray-400 mt-12 py-8 border-t border-gray-800">
        <div class="container mx-auto px-4 text-center">
            <p class="font-bold text-white mb-2">THỜI BÁO 24H - TRANG TIN ĐIỆN TỬ MÔ PHỎNG</p>
            <p class="text-sm">&copy; 2026 Bản quyền thuộc về Web Developer. Phát triển phục vụ mục đích học tập.</p>
        </div>
    </footer>

    <!-- Nhúng file xử lý logic Javascript -->
    <script src="script.js"></script>
</body>
</html>
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trang Quản Trị - Đăng Bài Viết</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
</head>
<body class="bg-gray-100 font-sans">

    <div class="container mx-auto px-4 py-10 max-w-2xl">
        <div class="flex justify-between items-center mb-6">
            <h1 class="text-2xl font-bold text-gray-800">Hệ thống Đăng bài</h1>
            <a href="index.html" class="text-sm text-blue-600 hover:underline">Xem Trang Chủ &rarr;</a>
        </div>

        <!-- FORM ĐĂNG BÀI -->
        <div class="bg-white p-6 rounded-lg shadow-md">
            <form id="article-form" class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700">Tiêu đề bài viết</label>
                    <input type="text" id="title" required class="mt-1 w-full p-2 border border-gray-300 rounded focus:ring-2 focus:ring-red-500 outline-none">
                </div>

                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700">Danh mục</label>
                        <select id="category" class="mt-1 w-full p-2 border border-gray-300 rounded outline-none">
                            <option value="Chính trị">Chính trị</option>
                            <option value="Công nghệ">Công nghệ</option>
                            <option value="Kinh doanh">Kinh doanh</option>
                            <option value="Giải trí">Giải trí</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700">Thời gian hiển thị</label>
                        <input type="text" id="time" placeholder="Ví dụ: Vừa xong, 5 phút trước" required class="mt-1 w-full p-2 border border-gray-300 rounded outline-none">
                    </div>
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700">Link ảnh bao bì (URL)</label>
                    <input type="url" id="image" placeholder="https://example.com/image.jpg" required class="mt-1 w-full p-2 border border-gray-300 rounded outline-none">
                </div>

                <div>
                    <label class="block text-sm font-medium text-gray-700">Mô tả ngắn (Tóm tắt)</label>
                    <textarea id="summary" rows="3" required class="mt-1 w-full p-2 border border-gray-300 rounded outline-none"></textarea>
                </div>

                <button type="submit" class="w-full bg-red-600 text-white p-2 rounded font-bold hover:bg-red-700 transition">
                    Xuất bản bài viết
                </button>
            </form>
        </div>
    </div>

    <!-- Nhúng cùng file script.js để dùng chung bộ nhớ -->
    <script src="script.js"></script>
</body>
</html>
