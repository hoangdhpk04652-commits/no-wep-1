<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hệ Thống Nộp Bài & Quản Lý Bài Tập ITA106</title>
    <!-- Nhúng thư viện biểu đồ chuyên nghiệp Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        /* ==========================================
           1. THIẾT LẬP BIẾN MÀU SẮC & KHỞI TẠO CHUNG
           ========================================== */
        :root {
            --primary-color: #1e293b;
            --secondary-color: #2563eb;
            --success-color: #16a34a;
            --warning-color: #ea580c;
            --danger-color: #dc2626;
            --bg-color: #f1f5f9;
            --card-bg: #ffffff;
            --text-color: #1e293b;
            --border-color: #cbd5e1;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            width: 100%;
            min-height: 100vh;
        }

        /* ==========================================
           2. THANH TIÊU ĐỀ TRÊN CÙNG (HEADER)
           ========================================== */
        header {
            background-color: var(--primary-color);
            color: white;
            padding: 40px 20px;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            width: 100%;
        }

        header h1 {
            font-size: 32px;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 10px;
        }

        header p {
            opacity: 0.9;
            font-size: 16px;
        }

        /* ==========================================
           3. BỐ CỤC TRÀN TOÀN BỘ MÀN HÌNH CHÍNH (CONTAINER)
           ========================================== */
        .container {
            width: 100%;
            max-width: 100%; /* Đảm bảo tràn 100% màn hình, không bị bóp nghẹt chiều rộng */
            margin: 0;
            padding: 40px 40px; /* Tạo khoảng trống đệm nhẹ ở 2 bên rìa ngoài */
            display: grid;
            grid-template-columns: 1fr 1fr; /* Chia đôi màn hình cực rộng, cân xứng 2 bên */
            gap: 40px;
            box-sizing: border-box;
        }

        /* Khi màn hình dọc (iPad, Điện thoại) sẽ tự xếp dọc */
        @media (max-width: 1100px) {
            .container {
                grid-template-columns: 1fr;
                padding: 20px 15px;
            }
        }

        /* Khung Panel màu trắng bọc nội dung */
        .panel {
            background-color: var(--card-bg);
            border-radius: 12px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.08);
            padding: 40px;
            width: 100%;
            border-top: 5px solid var(--secondary-color);
            box-sizing: border-box;
        }

        .panel-right {
            border-top-color: var(--success-color);
        }

        .panel-title {
            margin-top: 0;
            color: var(--primary-color);
            border-bottom: 3px solid #f1f5f9;
            padding-bottom: 18px;
            font-size: 24px;
            font-weight: 700;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        /* ==========================================
           4. BIỂU MẪU & CÁC Ô NHẬP LIỆU (FORM)
           ========================================== */
        .form-group {
            margin-bottom: 25px;
        }

        .form-group label {
            display: block;
            font-weight: 600;
            margin-bottom: 10px;
            font-size: 16px;
            color: #334155;
        }

        .form-group select, 
        .form-group input, 
        .form-group textarea {
            width: 100%;
            padding: 14px 18px;
            border: 2px solid var(--border-color);
            border-radius: 8px;
            font-size: 16px;
            font-family: inherit;
            box-sizing: border-box;
            outline: none;
            transition: all 0.2s ease-in-out;
            background-color: #f8fafc;
        }

        .form-group select:focus, 
        .form-group input:focus {
            border-color: var(--secondary-color);
            background-color: #ffffff;
            box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.15);
        }

        /* KHU VỰC TRÌNH BIÊN TẬP CODE MÀU ĐEN CHUYÊN NGHIỆP */
        .form-group textarea.code-editor {
            font-family: 'Fira Code', 'Courier New', Courier, monospace;
            background-color: #0f172a !important; /* Luôn giữ màu đen đậm chất terminal */
            color: #38bdf8 !important; /* Màu chữ xanh lập trình rực rỡ */
            padding: 20px;
            min-height: 380px;
            font-size: 15px;
            line-height: 1.7;
            border: 2px solid #334155;
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.5);
        }

        .form-group textarea.code-editor:focus {
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.2), inset 0 2px 4px rgba(0, 0, 0, 0.5);
        }

        /* ==========================================
           5. THIẾT KẾ CÁC NÚT BẤM (BUTTONS)
           ========================================== */
        .btn-container {
            display: flex;
            gap: 15px;
            margin-top: 30px;
        }

        .btn {
            flex: 1;
            background-color: var(--secondary-color);
            color: white;
            border: none;
            padding: 16px 24px;
            font-size: 16px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 700;
            text-align: center;
            transition: all 0.2s ease;
            box-shadow: 0 4px 6px rgba(37, 99, 235, 0.2);
            display: inline-flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
        }

        .btn:hover {
            opacity: 0.95;
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(37, 99, 235, 0.3);
        }

        .btn:active {
            transform: translateY(0);
        }

        .btn-success {
            background-color: var(--success-color);
            box-shadow: 0 4px 6px rgba(22, 163, 74, 0.2);
        }
        
        .btn-success:hover {
            box-shadow: 0 6px 12px rgba(22, 163, 74, 0.3);
        }

        /* ==========================================
           6. HIỂN THỊ DANH SÁCH LỊCH SỬ NỘP BÀI
           ========================================== */
        .submitted-list {
            margin-top: 30px;
        }

        .submitted-item {
            background: #f8fafc;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 15px;
            position: relative;
            transition: all 0.2s ease;
        }

        .submitted-item:hover {
            border-color: var(--secondary-color);
            background-color: #f0fdf4;
        }

        .submitted-item h5 {
            margin: 0 0 8px 0;
            font-size: 16px;
            font-weight: 700;
            color: var(--primary-color);
        }

        .submitted-item p {
            margin: 0;
            font-size: 14px;
            color: #64748b;
        }

        .status-badge {
            position: absolute;
            top: 20px;
            right: 20px;
            background: #dcfce7;
            color: #15803d;
            padding: 4px 12px;
            border-radius: 6px;
            font-size: 13px;
            font-weight: 700;
        }

        /* ==========================================
           7. TRÌNH BIỂU DIỄN KẾT QUẢ MINH HỌA
           ========================================== */
        .demo-area {
            margin-top: 25px;
            padding: 20px;
            background: #f8fafc;
            border-radius: 8px;
            border: 2px dashed #cbd5e1;
        }

        .demo-area strong {
            display: block;
            font-size: 16px;
            margin-bottom: 12px;
            color: var(--primary-color);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 14px;
            margin-top: 15px;
            background-color: #ffffff;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0,0,0,0.02);
        }

        th, td {
            padding: 12px 15px;
            border-bottom: 1px solid #e2e8f0;
            text-align: left;
        }

        th {
            background: #f1f5f9;
            color: #334155;
            font-weight: 700;
        }

        .chart-box {
            height: 250px;
            margin-top: 20px;
            position: relative;
            width: 100%;
        }

        /* Chân trang */
        footer {
            text-align: center;
            padding: 30px 20px;
            color: #64748b;
            font-size: 14px;
            background-color: #f1f5f9;
            border-top: 1px solid #e2e8f0;
            margin-top: 60px;
        }
    </style>
</head>
<body>

    <!-- PHẦN ĐẦU TRANG -->
    <header>
        <h1>Cổng Nộp Bài Tập Lập Trình & Khoa Học Dữ Liệu</h1>
        <p>Môn học: ITA106 | Quản lý, chạy thực nghiệm và đẩy mã nguồn trực tuyến</p>
    </header>

    <!-- KHU VỰC HIỂN THỊ CHÍNH -->
    <div class="container">
        
        <!-- CỘT BÊN TRÁI: KHUNG ĐIỀN THÔNG TIN & NHẬP CODE (PHÓNG TO CỰC ĐẠI) -->
        <div class="panel">
            <div class="panel-title">📤 Đẩy Mã Nguồn Nộp Bài</div>
            
            <form id="submission-form">
                <div class="form-group">
                    <label for="student-name">Họ và tên sinh viên:</label>
                    <input type="text" id="student-name" placeholder="Ví dụ: Nguyễn Văn A" required>
                </div>

                <div class="form-group">
                    <label for="student-id">Mã số sinh viên (MSSV):</label>
                    <input type="text" id="student-id" placeholder="Ví dụ: PK01234" required>
                </div>

                <div class="form-group">
                    <label for="exercise-select">Chọn bài tập nộp:</label>
                    <select id="exercise-select" onchange="updateCodeTemplate()">
                        <option value="1">Bài 1: Khám phá dữ liệu ban đầu (2đ)</option>
                        <option value="2">Bài 2: Làm sạch dữ liệu (2đ)</option>
                        <option value="3">Bài 3: Phát hiện Outliers dữ liệu (2đ)</option>
                        <option value="4">Bài 4: Sơ đồ quy trình Pipeline (2đ)</option>
                    </select>
                </div>

                <div class="form-group">
                    <label for="code-area">Mã nguồn (Python / JavaScript / HTML):</label>
                    <textarea id="code-area" class="code-editor" rows="15" required></textarea>
                </div>

                <div class="form-group">
                    <label for="note-area">Ghi chú hoặc phân tích thêm (Nếu có):</label>
                    <textarea id="note-area" rows="4" placeholder="Nhập các nhận xét về kết quả hoặc thuật toán của bạn vào đây..."></textarea>
                </div>

                <div class="btn-container">
                    <button type="submit" class="btn">🚀 Đẩy Code Nộp Bài</button>
                    <button type="button" class="btn btn-success" onclick="exportToTXT()">💾 Xuất file Báo Cáo (.txt)</button>
                </div>
            </form>

            <h4 style="margin-top: 40px; border-top: 2px solid #f1f5f9; padding-top: 25px; color: var(--primary-color);">Lịch sử đẩy code thành công:</h4>
            <div class="submitted-list" id="log-list">
                <div class="submitted-item">
                    <span class="status-badge">Đã đồng bộ</span>
                    <h5>Bài 1: Khám phá dữ liệu ban đầu</h5>
                    <p>Người nộp: Hệ thống mẫu | Thời gian: Vừa xong</p>
                </div>
            </div>
        </div>

        <!-- CỘT BÊN PHẢI: TRÌNH MÔ PHỎNG & ĐỒ THỊ MINH HỌA -->
        <div class="panel panel-right">
            <div class="panel-title">📊 Trình Mô Phỏng Kết Quả Toán Học</div>
            <p style="font-size: 15px; color: #64748b; margin-bottom: 20px;">Trình giả lập này giúp bạn kiểm thử, trực quan hóa dữ liệu tự động cho các bài tập vừa nộp.</p>
            
            <div style="margin-bottom: 25px;">
                <button class="btn btn-success" style="width: 100%;" onclick="runSimulation()">Kích hoạt Chạy thử nghiệm thuật toán</button>
            </div>

            <!-- Demo Bài 1 -->
            <div class="demo-area">
                <strong>[Xem trước Bài 1] 10 dòng dữ liệu & Thống kê mô tả:</strong>
                <table>
                    <thead>
                        <tr><th>STT</th><th>Diện tích (m²)</th><th>Giá (Tỷ VNĐ)</th><th>Phân loại</th></tr>
                    </thead>
                    <tbody id="demo-table-body">
                        <tr><td>1</td><td>45</td><td>1.5</td><td>Chung cư</td></tr>
                        <tr><td>2</td><td>60</td><td>2.4</td><td>Nhà phố</td></tr>
                        <tr><td>3</td><td>120</td><td>6.5</td><td>Biệt thự</td></tr>
                        <tr><td>4</td><td>300</td><td>28.0</td><td>Biệt thự (Nhiễu)</td></tr>
                    </tbody>
                </table>
                <div style="font-size:13px; margin-top:10px; color:#1e293b; font-weight: 600;" id="demo-stats">
                    Tính toán tự động: Trung bình Diện tích = 131.25 m² | Giá trung bình = 9.6 Tỷ VNĐ
                </div>
            </div>

            <!-- Demo Bài 2 & 3 -->
            <div class="demo-area" id="demo-clean-area" style="display:none;">
                <strong>[Xem trước Bài 2 & 3] Làm sạch dữ liệu & Phát hiện Outliers:</strong>
                <p style="font-size:14px; margin-bottom: 15px; color: #16a34a; font-weight: 600; line-height: 1.7;">
                    ✔ Điền giá trị trung vị cho dữ liệu trống thành công.<br>
                    ✔ Loại bỏ bản ghi trùng lặp một cách tự động.<br>
                    ⚠ <b>Cảnh báo bất thường (IQR/Z-score):</b> Dữ liệu căn hộ 300m² có giá 28 Tỷ vượt ngưỡng quy định 1.5*IQR.
                </p>
                <div class="chart-box">
                    <canvas id="demo-chart"></canvas>
                </div>
            </div>

            <!-- Demo Bài 4 -->
            <div class="demo-area">
                <strong>[Xem trước Bài 4] Sơ đồ Pipeline Khoa học dữ liệu:</strong>
                <div style="text-align:center; margin-top:15px;">
                    <svg width="100%" height="70" viewBox="0 0 600 70" style="background:#fff; border:1px solid #cbd5e1; border-radius:6px;">
                        <g font-size="11" font-weight="bold" text-anchor="middle" fill="#fff">
                            <rect x="5" y="15" width="85" height="40" rx="5" fill="#1e293b"/><text x="47.5" y="39">Thu thập</text>
                            <rect x="105" y="15" width="85" height="40" rx="5" fill="#dc2626"/><text x="147.5" y="39">Làm sạch</text>
                            <rect x="205" y="15" width="85" height="40" rx="5" fill="#2563eb"/><text x="247.5" y="39">EDA</text>
                            <rect x="305" y="15" width="85" height="40" rx="5" fill="#ea580c"/><text x="347.5" y="39">Đặc trưng</text>
                            <rect x="405" y="15" width="85" height="40" rx="5" fill="#16a34a"/><text x="447.5" y="39">Train</text>
                            <rect x="505" y="15" width="85" height="40" rx="5" fill="#9333ea"/><text x="547.5" y="39">Đánh giá</text>
                        </g>
                    </svg>
                </div>
            </div>
        </div>

    </div>

    <!-- CHÂN TRANG -->
    <footer>
        <p>Bản quyền phục vụ nộp bài tập môn ITA106 - Đại học FPT © 2026</p>
    </footer>

    <!-- LOGIC HOẠT ĐỘNG JAVASCRIPT -->
    <script>
        // Mẫu code tự động nạp cho từng bài tập để nộp nhanh
        const codeTemplates = {
            "1": `# BÀI 1: KHÁM PHÁ DỮ LIỆU BAN ĐẦU\\nimport pandas as pd\\nimport numpy as np\\n\\n# Đọc file dữ liệu thô\\ndf = pd.read_csv("data.csv")\\n\\n# 1. Hiển thị 10 dòng đầu\\nprint("10 dòng dữ liệu đầu tiên:")\\nprint(df.head(10))\\n\\n# 2. Đếm số lượng dòng, cột\\nprint(f"Kích thước file: {df.shape}")\\n\\n# 3. Phân tích thống kê mô tả\\nprint("Thông số thống kê cơ bản:")\\nprint(df.describe())`,
            "2": `# BÀI 2: LÀM SẠCH DỮ LIỆU\\nimport pandas as pd\\n\\ndf = pd.read_csv("data.csv")\\n\\n# Điền giá trị trung vị vào ô trống cột Price\\ndf['price'] = df['price'].fillna(df['price'].median())\\n\\n# Loại bỏ các dòng bị trùng lặp\\ndf = df.drop_duplicates()\\n\\nprint("Dữ liệu sau khi làm sạch thành công:")\\nprint(df.info())`,
            "3": `# BÀI 3: PHÁT HIỆN BIẾN ĐỘNG BẤT THƯỜNG (OUTLIERS)\\nimport numpy as np\\n\\nq1 = df['price'].quantile(0.25)\\nq3 = df['price'].quantile(0.75)\\niqr = q3 - q1\\n\\nlower_bound = q1 - 1.5 * iqr\\nupper_bound = q3 + 1.5 * iqr\\n\\noutliers = df[(df['price'] < lower_bound) | (df['price'] > upper_bound)]\\nprint(f"Số lượng bản ghi bị nghi là Outliers: {len(outliers)}")`,
            "4": `# BÀI 4: THIẾT KẾ SƠ ĐỒ QUY TRÌNH KHOA HỌC DỮ LIỆU PIPELINE\\ndef run_data_pipeline():\\n    print("Step 1: Thu thập dữ liệu")\\n    print("Step 2: Làm sạch dữ liệu")\\n    print("Step 3: Khám phá dữ liệu EDA")\\n    print("Step 4: Trích xuất đặc trưng")\\n    print("Step 5: Huấn luyện mô hình")\\n    print("Step 6: Đánh giá mô hình")\\n\\nrun_data_pipeline()`
        };

        function updateCodeTemplate() {
            const select = document.getElementById("exercise-select").value;
            document.getElementById("code-area").value = codeTemplates[select];
        }

        // Tự động nạp code Bài 1 khi vừa mở trang
        window.onload = function() {
            updateCodeTemplate();
        };

        // Nhận diện sự kiện nút nộp bài
        document.getElementById("submission-form").addEventListener("submit", function(e) {
            e.preventDefault();
            const name = document.getElementById("student-name").value;
            const id = document.getElementById("student-id").value;
            const exercise = document.getElementById("exercise-select");
            const exerciseText = exercise.options[exercise.selectedIndex].text;

            const logList = document.getElementById("log-list");
            const item = document.createElement("div");
            item.className = "submitted-item";
            item.innerHTML = `
                <span class="status-badge" style="background:#dbeafe; color:#1e40af;">Vừa nộp</span>
                <h5>${exerciseText}</h5>
                <p>Sinh viên: ${name} (${id}) | Trạng thái: Đã đồng bộ lên hệ thống</p>
            `;
            logList.insertBefore(item, logList.firstChild);
            alert("Chúc mừng! Mã nguồn bài làm của bạn đã được đẩy lên hệ thống thành công!");
        });

        // Vẽ biểu đồ thực nghiệm
        let currentChart = null;
        function runSimulation() {
            document.getElementById("demo-clean-area").style.display = "block";
            const ctx = document.getElementById("demo-chart").getContext("2d");
            if(currentChart) { currentChart.destroy(); }

            currentChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Giá trị thông thường', 'Giá trị dị biệt (Outlier)'],
                    datasets: [{
                        label: 'Kết quả phân tích Giá nhà (Tỷ VNĐ)',
                        data: [2.8, 28.0],
                        backgroundColor: ['#2563eb', '#dc2626'],
                        borderRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false }
                    }
                }
            });
            alert("Mô phỏng toán học thực thi thành công!");
        }

        // Xuất file text
        function exportToTXT() {
            const name = document.getElementById("student-name").value || "Vo_Danh";
            const id = document.getElementById("student-id").value || "00000";
            const code = document.getElementById("code-area").value;
            const textContent = `BAO CAO BAI TAP MON ITA106\\n-------------------------\\nSinh vien thuc hien: ${name}\\nMSSV: ${id}\\n\\n[MA NGUON BAI LAM CHI TIET]:\\n${code}`;
            
            const blob = new Blob([textContent], { type: "text/plain;charset=utf-8" });
            const link = document.createElement("a");
            link.href = URL.createObjectURL(blob);
            link.download = `Baitap_ITA106_${id}.txt`;
            link.click();
        }
    </script>
</body>
</html>
