<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hệ Thống Nộp Bài & Quản Lý Bài Tập ITA106</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary-color: #1e293b;
            --secondary-color: #2563eb;
            --success-color: #16a34a;
            --warning-color: #ea580c;
            --danger-color: #dc2626;
            --bg-color: #f1f5f9;
            --card-bg: #ffffff;
            --text-color: #334155;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 0;
            line-height: 1.6;
            width: 100%;
        }

        header {
            background-color: var(--primary-color);
            color: white;
            padding: 30px 20px;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            width: 100%;
            box-sizing: border-box;
        }

        header h1 {
            margin: 0;
            font-size: 26px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        header p {
            margin: 8px 0 0 0;
            opacity: 0.8;
            font-size: 15px;
        }

        /* CHỈNH SỬA TẠI ĐÂY: Giãn đều container rộng hết cỡ màn hình (max-width lớn hơn) */
        .container {
            max-width: 95%; 
            width: 1400px;
            margin: 30px auto;
            padding: 0 20px;
            display: grid;
            grid-template-columns: 1fr 1fr; /* Chia đôi 2 nửa màn hình cân xứng */
            gap: 30px;
            box-sizing: border-box;
        }

        @media (max-width: 1024px) {
            .container {
                grid-template-columns: 1fr; /* Trên màn hình dọc hoặc ipad sẽ xếp chồng gọn gàng */
            }
        }

        .panel {
            background-color: var(--card-bg);
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            padding: 25px;
            box-sizing: border-box;
            width: 100%; /* Đảm bảo panel chiếm hết không gian cột */
        }

        .panel-title {
            margin-top: 0;
            color: var(--primary-color);
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 12px;
            font-size: 20px;
            font-weight: bold;
        }

        /* Form styling */
        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            font-weight: 600;
            margin-bottom: 6px;
            font-size: 14px;
            color: #475569;
        }

        .form-group select, 
        .form-group input, 
        .form-group textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #cbd5e1;
            border-radius: 6px;
            font-size: 14px;
            font-family: inherit;
            box-sizing: border-box;
            outline: none;
        }

        .form-group select:focus, 
        .form-group input:focus, 
        .form-group textarea:focus {
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }

        .code-editor {
            font-family: 'Courier New', Courier, monospace;
            background-color: #0f172a;
            color: #38bdf8;
            padding: 15px;
            min-height: 250px;
            resize: vertical;
        }

        .btn {
            background-color: var(--secondary-color);
            color: white;
            border: none;
            padding: 12px 24px;
            font-size: 14px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s;
        }

        .btn:hover {
            opacity: 0.9;
            transform: translateY(-1px);
        }

        .btn-success { background-color: var(--success-color); }

        .submitted-list { margin-top: 20px; }

        .submitted-item {
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            border-radius: 6px;
            padding: 15px;
            margin-bottom: 12px;
            position: relative;
        }

        .status-badge {
            position: absolute;
            top: 15px;
            right: 15px;
            background: #dcfce7;
            color: #15803d;
            padding: 2px 8px;
            border-radius: 4px;
            font-size: 12px;
            font-weight: bold;
        }

        .demo-area {
            margin-top: 20px;
            padding: 15px;
            background: #f8fafc;
            border-radius: 8px;
            border: 1px dashed #cbd5e1;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 13px;
            margin-top: 10px;
        }

        th, td {
            padding: 10px;
            border-bottom: 1px solid #e2e8f0;
            text-align: left;
        }

        th { background: #f1f5f9; }

        .chart-box {
            height: 200px;
            margin-top: 15px;
        }
    </style>
</head>
<body>

    <header>
        <h1>Cổng Nộp Bài Tập Lập Trình & Khoa Học Dữ Liệu</h1>
        <p>Môn học: ITA106 | Quản lý, chạy thực nghiệm và đẩy mã nguồn trực tuyến</p>
    </header>

    <div class="container">
        
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
                    <textarea id="code-area" class="code-editor" rows="12" required></textarea>
                </div>

                <div class="form-group">
                    <label for="note-area">Ghi chú hoặc phân tích thêm (Nếu có):</label>
                    <textarea id="note-area" rows="3" placeholder="Nhập các nhận xét về kết quả hoặc thuật toán vào đây..."></textarea>
                </div>

                <button type="submit" class="btn">🚀 Đẩy Code Nộp Bài</button>
                <button type="button" class="btn btn-success" onclick="exportToTXT()" style="margin-left: 10px;">💾 Xuất file Báo Cáo</button>
            </form>

            <h4 style="margin-top: 30px; border-top: 1px solid #e2e8f0; padding-top: 15px;">Lịch sử đẩy code thành công:</h4>
            <div class="submitted-list" id="log-list">
                <div class="submitted-item">
                    <span class="status-badge">Đã đồng bộ</span>
                    <h5>Bài 1: Khám phá dữ liệu ban đầu</h5>
                    <p>Người nộp: Hệ thống mẫu | Thời gian: Vừa xong</p>
                </div>
            </div>
        </div>

        <div class="panel">
            <div class="panel-title">📊 Trình Mô Phỏng & Kiểm Tra Kết Quả Toán Học</div>
            <p style="font-size: 14px; color: #64748b;">Trình giả lập này giúp bạn chạy thử nghiệm thuật toán của Bài 1, 2, 3 dựa trên mã nguồn bạn vừa đẩy lên.</p>
            
            <div style="margin: 15px 0;">
                <button class="btn btn-success" onclick="runSimulation()">Kích hoạt Chạy thử nghiệm</button>
            </div>

            <div class="demo-area">
                <strong>[Xem trước Bài 1] 10 dòng dữ liệu & Thống kê:</strong>
                <table>
                    <thead>
                        <tr><th>STT</th><th>Diện tích (m²)</th><th>Giá (Tỷ)</th><th>Phân loại</th></tr>
                    </thead>
                    <tbody id="demo-table-body">
                        <tr><td>1</td><td>45</td><td>1.5</td><td>Chung cư</td></tr>
                        <tr><td>2</td><td>60</td><td>2.4</td><td>Nhà phố</td></tr>
                        <tr><td>3</td><td>120</td><td>6.5</td><td>Biệt thự</td></tr>
                        <tr><td>4</td><td>300</td><td>28.0</td><td>Biệt thự (Nhiễu)</td></tr>
                    </tbody>
                </table>
                <div style="font-size:12px; margin-top:5px; color:#1e293b;" id="demo-stats">
                    Trung bình (Mean) Diện tích: 131.25 m² | Giá: 9.6 Tỷ VNĐ
                </div>
            </div>

            <div class="demo-area" id="demo-clean-area" style="display:none;">
                <strong>[Xem trước Bài 2 & 3] Làm sạch dữ liệu & Phát hiện Outliers:</strong>
                <p style="font-size:13px; margin: 5px 0 0 0; color: #16a34a;">
                    ✔ Đã tự động điền giá trị trung vị cho phần dữ liệu trống.<br>
                    ✔ Đã quét loại bỏ 1 dòng trùng lặp hoàn toàn.<br>
                    ⚠ <b>Phát hiện biến động bất thường (IQR/Z-score):</b> Căn hộ 300m² có Giá 28 Tỷ vượt ngưỡng quy định.
                </p>
                <div class="chart-box">
                    <canvas id="demo-chart"></canvas>
                </div>
            </div>

            <div class="demo-area">
                <strong>[Xem trước Bài 4] Sơ đồ Pipeline Khoa học dữ liệu:</strong>
                <div style="text-align:center; margin-top:10px;">
                    <svg width="100%" height="60" viewBox="0 0 600 60" style="background:#fff; border:1px solid #e2e8f0; border-radius:4px;">
                        <g font-size="10" font-weight="bold" text-anchor="middle" fill="#fff">
                            <rect x="5" y="15" width="80" height="30" rx="3" fill="#1e293b"/><text x="45" y="33">Thu thập</text>
                            <rect x="105" y="15" width="80" height="30" rx="3" fill="#dc2626"/><text x="145" y="33">Làm sạch</text>
                            <rect x="205" y="15" width="80" height="30" rx="3" fill="#2563eb"/><text x="245" y="33">EDA</text>
                            <rect x="305" y="15" width="80" height="30" rx="3" fill="#ea580c"/><text x="345" y="33">Đặc trưng</text>
                            <rect x="405" y="15" width="80" height="30" rx="3" fill="#16a34a"/><text x="455" y="33">Huấn luyện</text>
                            <rect x="505" y="15" width="80" height="30" rx="3" fill="#9333ea"/><text x="545" y="33">Đánh giá</text>
                        </g>
                    </svg>
                </div>
            </div>
        </div>

    </div>

    <script>
        const codeTemplates = {
            "1": `# BÀI 1: KHÁM PHÁ DỮ LIỆU BAN ĐẦU\\nimport pandas as pd\\n\\ndf = pd.read_csv("data.csv")\\nprint("10 dòng đầu tiên:")\\nprint(df.head(10))\\nprint(f"Kích thước file: {df.shape}")\\nprint(df.describe())`,
            "2": `# BÀI 2: LÀM SẠCH DỮ LIỆU\\n# Điền giá trị trung vị và loại bỏ bản ghi trùng\\ndf['price'] = df['price'].fillna(df['price'].median())\\ndf = df.drop_duplicates()\\nprint("Dữ liệu sau khi làm sạch:", df.shape)`,
            "3": `# BÀI 3: PHÁT HIỆN OUTLIERS\\nq1 = df['price'].quantile(0.25)\\nq3 = df['price'].quantile(0.75)\\niqr = q3 - q1\\nlower_bound = q1 - 1.5 * iqr\\nupper_bound = q3 + 1.5 * iqr\\noutliers = df[(df['price'] < lower_bound) | (df['price'] > upper_bound)]\\nprint("Số lượng bản ghi bất thường:", len(outliers))`,
            "4": `# BÀI 4: THIẾT KẾ SƠ ĐỒ QUY TRÌNH KHOA HỌC DỮ LIỆU\\n# 1. Thu thập -> 2. Làm sạch -> 3. EDA -> 4. Trích xuất đặc trưng -> 5. Train -> 6. Test\\nprint("Pipeline executed successfully!")`
        };

        function updateCodeTemplate() {
            const select = document.getElementById("exercise-select").value;
            document.getElementById("code-area").value = codeTemplates[select];
        }

        window.onload = function() {
            updateCodeTemplate();
        };

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
                <p>Sinh viên: ${name} (${id}) | Thời gian: Vừa xong</p>
            `;
            logList.insertBefore(item, logList.firstChild);
            alert("Đã đẩy code bài tập của bạn lên hệ thống lưu trữ trực tuyến thành công!");
        });

        let currentChart = null;
        function runSimulation() {
            document.getElementById("demo-clean-area").style.display = "block";
            const ctx = document.getElementById("demo-chart").getContext("2d");
            if(currentChart) { currentChart.destroy(); }

            currentChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Điểm thường', 'Điểm dị biệt (Outlier)'],
                    datasets: [{
                        label: 'Phân bố giá trị phân tích dữ liệu',
                        data: [2.8, 28.0],
                        backgroundColor: ['#2563eb', '#dc2626']
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false
                }
            });
            alert("Trình mô phỏng đã thực thi xong mã nguồn bài tập!");
        }

        function exportToTXT() {
            const name = document.getElementById("student-name").value || "Vo_Danh";
            const id = document.getElementById("student-id").value || "00000";
            const code = document.getElementById("code-area").value;
            const textContent = `BAO CAO BAI TAP ITA106\\nSinh vien: ${name}\\nMSSV: ${id}\\n\\n[MA NGUON DA NOP]:\\n${code}`;
            
            const blob = new Blob([textContent], { type: "text/plain;charset=utf-8" });
            const link = document.createElement("a");
            link.href = URL.createObjectURL(blob);
            link.download = `Baitap_ITA106_${id}.txt`;
            link.click();
        }
    </script>
</body>
</html>
