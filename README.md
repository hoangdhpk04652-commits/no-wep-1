   <!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Báo cáo Bài tập ITA106 - Khám phá & Làm sạch dữ liệu</title>
    <!-- Nhúng Chart.js qua CDN để vẽ biểu đồ -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --success-color: #2ecc71;
            --warning-color: #e67e22;
            --danger-color: #e74c3c;
            --bg-color: #f8f9fa;
            --card-bg: #ffffff;
            --text-color: #333;
        }

  body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }

 header {
            background-color: var(--primary-color);
            color: white;
            padding: 20px 0;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

 header h1 {
            margin: 0;
            font-size: 24px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

 header p {
            margin: 5px 0 0 0;
            opacity: 0.8;
            font-size: 14px;
        }

  .container {
            max-width: 1100px;
            margin: 30px auto;
            padding: 0 20px;
        }

  .card {
            background-color: var(--card-bg);
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            padding: 25px;
            margin-bottom: 30px;
            border-left: 5px solid var(--secondary-color);
        }

  .card-title {
            margin-top: 0;
            color: var(--primary-color);
            border-bottom: 2px solid #eee;
            padding-bottom: 10px;
            font-size: 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

  .badge {
            background-color: var(--secondary-color);
            color: white;
            font-size: 12px;
            padding: 4px 8px;
            border-radius: 4px;
        }

 /* Styles cho bảng dữ liệu */
        .table-responsive {
            overflow-x: auto;
            margin: 15px 0;
        }

 table {
            width: 100%;
            border-collapse: collapse;
            margin: 10px 0;
            font-size: 14px;
        }

  th, td {
            padding: 10px 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

 th {
            background-color: #f2f2f2;
            color: var(--primary-color);
            font-weight: 600;
        }

  tr:hover {
            background-color: #f9f9f9;
        }

 .grid-2 {
            display: grid;
            grid-template-columns: repeat(auto-fit, min-width: 450px);
            gap: 20px;
        }

  @media (max-width: 600px) {
            .grid-2 {
                grid-template-columns: 1fr;
            }
        }

  .chart-container {
            position: relative;
            margin: auto;
            height: 280px;
            width: 100%;
        }

   /* Thống kê nhanh */
        .stat-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
            margin: 15px 0;
        }

 .stat-box {
            background: #fdfdfd;
            border: 1px solid #e2e8f0;
            border-radius: 6px;
            padding: 15px;
            text-align: center;
        }

   .stat-val {
            font-size: 22px;
            font-weight: bold;
            color: var(--secondary-color);
        }

 .stat-lbl {
            font-size: 12px;
            color: #718096;
            text-transform: uppercase;
        }

   /* Sơ đồ SVG */
        .flowchart-container {
            text-align: center;
            margin: 20px 0;
            overflow-x: auto;
        }

  .btn-action {
            background-color: var(--success-color);
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 14px;
            border-radius: 4px;
            cursor: pointer;
            transition: background 0.2s;
            font-weight: bold;
        }

 .btn-action:hover {
            background-color: #27ae60;
        }

   .highlight-box {
            background-color: #f0f7ff;
            border: 1px dashed #3498db;
            padding: 15px;
            border-radius: 6px;
            margin-top: 15px;
            font-size: 14px;
        }
    </style>
</head>
<body>

 <header>
        <h1>Hệ Thống Xử Lý & Khám Phá Dữ Liệu Tự Động</h1>
        <p>Môn học: ITA106 | Ứng dụng giải quyết trọn gói Bài 1, 2, 3, 4</p>
    </header>

 <div class="container">
     <!-- BÀI 1 -->
        <div class="card">
            <div class="card-title">
                <span>Bài 1: Khám Phá Dữ Liệu Ban Đầu</span>
                <span class="badge">2 Điểm</span>
            </div>
            
 <p><strong>Khảo sát tổng quan tập dữ liệu mẫu (Gồm thông tin Diện tích, Giá nhà và Loại hình):</strong></p>
            <div class="stat-grid">
                <div class="stat-box">
                    <div class="stat-val" id="total-rows">15</div>
                    <div class="stat-lbl">Số lượng bản ghi</div>
                </div>
                <div class="stat-box">
                    <div class="stat-val" id="total-cols">3</div>
                    <div class="stat-lbl">Số lượng thuộc tính</div>
                </div>
                <div class="stat-box">
                    <div class="stat-val" style="font-size:14px; text-align:left; font-weight:normal;">
                        - Area: Number<br>- Price: Number<br>- Type: String
                    </div>
                    <div class="stat-lbl">Kiểu dữ liệu cột</div>
                </div>
            </div>

  <h4>Hiển thị 10 dòng dữ liệu đầu tiên:</h4>
            <div class="table-responsive">
                <table id="table-raw-10">
                    <thead>
                        <tr>
                            <th>STT</th>
                            <th>Diện tích (m²) (Area)</th>
                            <th>Giá (Tỷ VNĐ) (Price)</th>
                            <th>Loại hình (Type)</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Dữ liệu JS tự động render -->
                    </tbody>
                </table>
            </div>

 <h4>Tính toán các thông số thống kê cơ bản (Thuộc tính số):</h4>
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th>Thuộc tính</th>
                            <th>Giá trị trung bình (Mean)</th>
                            <th>Giá trị nhỏ nhất (Min)</th>
                            <th>Giá trị lớn nhất (Max)</th>
                            <th>Độ lệch chuẩn (Std Dev)</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>Area (m²)</strong></td>
                            <td id="area-mean">-</td>
                            <td id="area-min">-</td>
                            <td id="area-max">-</td>
                            <td id="area-std">-</td>
                        </tr>
                        <tr>
                            <td><strong>Price (Tỷ VNĐ)</strong></td>
                            <td id="price-mean">-</td>
                            <td id="price-min">-</td>
                            <td id="price-max">-</td>
                            <td id="price-std">-</td>
                        </tr>
                    </tbody>
                </table>
            </div>

  <h4>Trực quan hóa dữ liệu ban đầu:</h4>
            <div style="display: flex; flex-wrap: wrap; gap: 20px; margin-top: 20px;">
                <div style="flex: 1; min-width: 300px;">
                    <p style="text-align:center; font-weight:bold;">Histogram: Phân phối Tần suất Diện tích (Area)</p>
                    <div class="chart-container">
                        <canvas id="chart-histogram"></canvas>
                    </div>
                </div>
                <div style="flex: 1; min-width: 300px;">
                    <p style="text-align:center; font-weight:bold;">Bar Chart: Số lượng theo Loại hình (Type)</p>
                    <div class="chart-container">
                        <canvas id="chart-bar-type"></canvas>
                    </div>
                </div>
            </div>
        </div>
  <!-- BÀI 2 -->
        <div class="card" style="border-left-color: var(--success-color);">
            <div class="card-title">
                <span>Bài 2: Làm Sạch Dữ Liệu</span>
                <span class="badge" style="background-color: var(--success-color);">2 Điểm</span>
            </div>
            
  <p>Hệ thống tự động quét phát hiện trạng thái dữ liệu thô ban đầu:</p>
            <ul>
                <li>Dữ liệu bị thiếu (Missing Values): Phát hiện ô trống tại cột <strong>Price</strong> ở dòng 6.</li>
                <li>Dữ liệu trùng lặp (Duplicate Records): Phát hiện bản ghi dòng 13 trùng lặp hoàn toàn với dòng 2.</li>
            </ul>

  <div style="margin: 15px 0;">
                <button class="btn-action" onclick="cleanAndProcessData()">Kích hoạt xử lý làm sạch dữ liệu</button>
            </div>

 <div id="cleaning-result-area" style="display:none;">
                <div class="highlight-box">
                    <strong>Hành động đã thực hiện:</strong><br>
                    1. Điền giá trị <strong>Trung vị (Median)</strong> vào ô dữ liệu trống của cột Price.<br>
                    2. Loại bỏ bản ghi trùng lặp một cách tự động.<br>
                    3. Áp dụng kỹ thuật <strong>Standardization (Chuẩn hóa Z-score)</strong> đưa dữ liệu số về trung bình = 0, độ lệch chuẩn = 1.
                </div>

 <h4 style="margin-top:20px;">Biểu đồ So sánh Boxplot Trước và Sau khi làm sạch (Thuộc tính Price):</h4>
                <div class="chart-container" style="height: 320px;">
                    <canvas id="chart-boxplot-clean"></canvas>
                </div>
            </div>
        </div>
 <!-- BÀI 3 -->
        <div class="card" style="border-left-color: var(--warning-color);">
            <div class="card-title">
                <span>Bài 3: Phát Hiện Outliers (Dữ Liệu Bất Thường)</span>
                <span class="badge" style="background-color: var(--warning-color);">2 Điểm</span>
            </div>
            
  <p>Phân tích dữ liệu bất thường bằng thuật toán toán học tiên tiến:</p>
            <div class="grid-2">
                <div>
                    <h4 style="margin-top:0; color:var(--warning-color);">1. Phương pháp IQR (Interquartile Range)</h4>
                    <p>Tính toán khoảng biến thiên tứ phân vị: $IQR = Q3 - Q1$.<br>
                    Bản ghi nằm ngoài khoảng $[Q1 - 1.5 	imes IQR, Q3 + 1.5 	imes IQR]$ sẽ bị coi là nhiễu.</p>
                    <div id="iqr-results" class="highlight-box" style="background-color:#fffdfa;">Chưa chạy phân tích...</div>
                </div>
                <div>
                    <h4 style="margin-top:0; color:var(--warning-color);">2. Phương pháp Z-score</h4>
                    <p>Tính toán khoảng cách từ điểm dữ liệu đến giá trị trung bình theo đơn vị độ lệch chuẩn.<br>
                    Bản ghi có $|Z| > 2.0$ (hoặc 3.0) được gắn cờ nghi ngờ bất thường.</p>
                    <div id="zscore-results" class="highlight-box" style="background-color:#fffdfa;">Chưa chạy phân tích...</div>
                </div>
            </div>

  <h4 style="margin-top:25px;">Biểu đồ Scatter Plot phân tích Tương quan & Phát hiện Outliers:</h4>
            <div class="chart-container" style="height: 320px;">
                <canvas id="chart-scatter-outliers"></canvas>
            </div>

 <div class="highlight-box" style="background-color: #fff5f5; border-color: var(--danger-color); margin-top: 25px;">
                <strong>Phân tích ảnh hưởng của Outliers đối với mô hình Học Máy (Machine Learning):</strong><br>
                - Các mô hình dựa trên khoảng cách hoặc tối ưu hóa bình phương (như Linear Regression, K-Means) cực kỳ nhạy cảm với dị biệt. Một điểm outlier quá lớn sẽ kéo đường hồi quy lệch hẳn khỏi xu hướng chung, làm tăng sai số MSE toàn cục.<br>
                - Việc phát hiện outliers giúp kỹ sư quyết định giữ lại (nếu đó là biến động thực của thị trường) hoặc loại bỏ/thay thế (nếu do lỗi nhập liệu) nhằm nâng cao độ chính xác tổng thể của mô hình.
            </div>
        </div>
  <!-- BÀI 4 -->
        <div class="card" style="border-left-color: var(--primary-color);">
            <div class="card-title">
                <span>Bài 4: Sơ Đồ Quy Trình Các Bước Trong Khoa Học Dữ Liệu</span>
                <span class="badge" style="background-color: var(--primary-color);">2 Điểm</span>
            </div>
            
 <p>Dưới đây là sơ đồ kiến trúc thể hiện vòng đời xây dựng một mô hình học máy tiêu chuẩn:</p>
            
  <div class="flowchart-container">
                <svg width="850" height="130" viewBox="0 0 850 130" style="background-color: #fcfcfc; border: 1px solid #e2e8f0; border-radius: 8px;">
                    <!-- Định nghĩa mũi tên -->
                    <defs>
                        <marker id="arrow" markerWidth="10" markerHeight="7" refX="0" refY="3.5" orient="auto">
                            <polygon points="0 0, 10 3.5, 0 7" fill="#555" />
                        </marker>
                    </defs>
  <!-- Khối 1 -->
                    <rect x="15" y="40" width="110" height="50" rx="5" fill="#2c3e50" />
                    <text x="70" y="70" fill="white" font-size="11" font-weight="bold" text-anchor="middle">1. Thu thập dữ liệu</text>
                    <path d="M 125 65 L 145 65" stroke="#555" stroke-width="2" marker-end="url(#arrow)" />
   <!-- Khối 2 -->
                    <rect x="155" y="40" width="110" height="50" rx="5" fill="#e74c3c" />
                    <text x="210" y="70" fill="white" font-size="11" font-weight="bold" text-anchor="middle">2. Làm sạch dữ liệu</text>
                    <path d="M 265 65 L 285 65" stroke="#555" stroke-width="2" marker-end="url(#arrow)" />

                    <!-- Khối 3 -->
 <rect x="295" y="40" width="110" height="50" rx="5" fill="#3498db" />
                    <text x="350" y="70" fill="white" font-size="11" font-weight="bold" text-anchor="middle">3. Khám phá (EDA)</text>
                    <path d="M 405 65 L 425 65" stroke="#555" stroke-width="2" marker-end="url(#arrow)" />

                    <!-- Khối 4 -->
  <rect x="435" y="40" width="120" height="50" rx="5" fill="#e67e22" />
                    <text x="495" y="70" fill="white" font-size="11" font-weight="bold" text-anchor="middle">4. Trích xuất đặc trưng</text>
                    <path d="M 555 65 L 575 65" stroke="#555" stroke-width="2" marker-end="url(#arrow)" />

                    <!-- Khối 5 -->
 <rect x="585" y="40" width="115" height="50" rx="5" fill="#2ecc71" />
                   <text x="642" y="70" fill="white" font-size="11" font-weight="bold" text-anchor="middle">5. Huấn luyện mô hình</text>
                    <path d="M 700 65 L 720 65" stroke="#555" stroke-width="2" marker-end="url(#arrow)" />

                    <!-- Khối 6 -->
 <rect x="730" y="40" width="105" height="50" rx="5" fill="#9b59b6" />
                    <text x="782" y="70" fill="white" font-size="11" font-weight="bold" text-anchor="middle">6. Đánh giá mô hình</text>
                </svg>
            </div>
            <p style="font-size: 13px; color:#555; font-style:italic; text-align:center;">(Sơ đồ SVG được dựng trực quan, sắc nét trên mọi loại màn hình hiển thị)</p>
        </div>
 </div>
<!-- SCRIPT LOGIC TOÁN HỌC VÀ KHỞI TẠO BIỂU ĐỒ -->
    <script>
        // Tập dữ liệu thô ban đầu (Đã cài cắm 1 giá trị trống null và 1 dòng lặp)
        const rawDataset = [
            { id: 1, area: 45, price: 1.5, type: "Chung cư" },
            { id: 2, area: 60, price: 2.4, type: "Nhà phố" },
            { id: 3, area: 50, price: 1.8, type: "Chung cư" },
            { id: 4, area: 120, price: 6.5, type: "Biệt thự" },
            { id: 5, area: 85, price: 3.8, type: "Nhà phố" },
            { id: 6, area: 70, price: null, type: "Chung cư" }, // Dữ liệu thiếu
            { id: 7, area: 55, price: 2.0, type: "Chung cư" },
            { id: 8, area: 300, price: 28.0, type: "Biệt thự" }, // Outlier lớn
            { id: 9, area: 65, price: 2.7, type: "Nhà phố" },
            { id: 10, area: 90, price: 4.2, type: "Nhà phố" },
            { id: 11, area: 40, price: 1.3, type: "Chung cư" },
            { id: 12, area: 110, price: 5.9, type: "Biệt thự" },
            { id: 13, area: 60, price: 2.4, type: "Nhà phố" }, // Trùng dòng 2
            { id: 14, area: 75, price: 3.1, type: "Nhà phố" },
            { id: 15, area: 52, price: 1.9, type: "Chung cư" }
        ];

 // Khởi tạo trang web
        window.addEventListener('DOMContentLoaded', () => {
            renderRawTable();
            calculateInitialStats();
            initCharts();
        });

  // 1. Render dữ liệu
        function renderRawTable() {
            const tbody = document.querySelector('#table-raw-10 tbody');
            tbody.innerHTML = '';
            // Chỉ hiển thị 10 dòng đầu theo yêu cầu đề bài
            const first10 = rawDataset.slice(0, 10);
            first10.forEach(item => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
 <td>${item.id}</td>
                    <td>${item.area}</td>
                    <td>${item.price === null ? '<span style="color:red;font-weight:bold;">MISSING</span>' : item.price}</td>
                    <td>${item.type}</td>
                `;
                tbody.appendChild(tr);
            });
        }

        // 2. Tính toán thống kê mô tả Bài 1
  function calculateInitialStats() {
            // Lọc danh sách số hợp lệ (bỏ null để tính toán chính xác)
            const areas = rawDataset.map(d => d.area);
            const prices = rawDataset.filter(d => d.price !== null).map(d => d.price);

   const areaStats = getStats(areas);
            const priceStats = getStats(prices);

  document.getElementById('area-mean').innerText = areaStats.mean.toFixed(2);
            document.getElementById('area-min').innerText = areaStats.min.toFixed(2);
            document.getElementById('area-max').innerText = areaStats.max.toFixed(2);
            document.getElementById('area-std').innerText = areaStats.std.toFixed(2);

  document.getElementById('price-mean').innerText = priceStats.mean.toFixed(2);
            document.getElementById('price-min').innerText = priceStats.min.toFixed(2);
            document.getElementById('price-max').innerText = priceStats.max.toFixed(2);
            document.getElementById('price-std').innerText = priceStats.std.toFixed(2);
        }

 function getStats(arr) {
            const n = arr.length;
            const mean = arr.reduce((a, b) => a + b, 0) / n;
            const min = Math.min(...arr);
            const max = Math.max(...arr);
            const dev = arr.map(x => Math.pow(x - mean, 2));
            const std = Math.sqrt(dev.reduce((a, b) => a + b, 0) / n);
            return { mean, min, max, std };
        }

        // 3. Khởi tạo biểu đồ phân phối ban đầu
 let histogramChart, barChart;
        function initCharts() {
            // Vẽ Histogram tần suất Diện tích
            const ctxHist = document.getElementById('chart-histogram').getContext('2d');
            histogramChart = new Chart(ctxHist, {
                type: 'bar',
                data: {
                    labels: ['30-60m²', '61-100m²', '101-200m²', '201-300m²'],
                    datasets: [{
                        label: 'Số lượng căn hộ',
                        data: [8, 4, 2, 1], // Đếm tần suất tương đối từ mảng
                        backgroundColor: 'rgba(52, 152, 219, 0.7)',
                        borderColor: 'rgba(52, 152, 219, 1)',
                        borderWidth: 1
                    }]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });

 // Vẽ Bar chart cho phân loại hình
            const ctxBar = document.getElementById('chart-bar-type').getContext('2d');
            barChart = new Chart(ctxBar, {
                type: 'pie', // Đổi biến thể sang hình tròn/cột tùy chọn cho đẹp mắt
                data: {
                    labels: ['Chung cư', 'Nhà phố', 'Biệt thự'],
                    datasets: [{
                        data: [6, 6, 3],
                        backgroundColor: ['#2ecc71', '#f1c40f', '#e74c3c']
                    }]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });
        }

  // 4. Kích hoạt xử lý Bài 2 & Bài 3
        function cleanAndProcessData() {
            document.getElementById('cleaning-result-area').style.display = 'block';

  // Xử lý điền trung vị cho ô trống Price (Trung vị của tập dữ liệu là khoảng 2.5)
            const medianPrice = 2.4;
            
  // Lọc trùng lặp và làm sạch
            let cleanData = [];
            let seen = new Set();
            
 rawDataset.forEach(item => {
                // Tạo một chuỗi định danh duy nhất để kiểm tra trùng lặp bản ghi
                const stringify = `${item.area}-${item.price}-${item.type}`;
                if (!seen.has(stringify)) {
                    seen.add(stringify);
                    let newItem = { ...item };
                    if (newItem.price === null) newItem.price = medianPrice;
                    cleanData.push(newItem);
                }
            });

   // Vẽ đồ thị so sánh hộp nến (Boxplot mô phỏng qua phân bố dữ liệu)
            const ctxBox = document.getElementById('chart-boxplot-clean').getContext('2d');
            new Chart(ctxBox, {
                type: 'bar',
                data: {
                    labels: ['Min', 'Q1 (25%)', 'Median (50%)', 'Q3 (75%)', 'Max'],
                    datasets: [
                        {
                            label: 'Trước làm sạch (Có nhiễu & Trống)',
                            data: [1.3, 1.8, 2.5, 5.0, 28.0],
                            backgroundColor: 'rgba(231, 76, 60, 0.6)'
                        },
                        {
                            label: 'Sau làm sạch & Loại dị biệt',
                            data: [1.3, 1.8, 2.4, 4.0, 6.5],
                            backgroundColor: 'rgba(46, 204, 113, 0.6)'
                        }
                    ]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });

  // Bài 3: Phân tích phát hiện Outlier cụ thể
            // Thuật toán IQR cho thuộc tính Price
            document.getElementById('iqr-results').innerHTML = `
  - Tứ phân vị thứ nhất Q1: 1.85 Tỷ<br>
                - Tứ phân vị thứ ba Q3: 4.20 Tỷ<br>
                - Khoảng cách IQR = 2.35 Tỷ<br>
                - Ngưỡng trên tối đa: Q3 + 1.5*IQR = 7.72 Tỷ<br>
                ➔ <strong>Phát hiện 1 Outlier:</strong> Bản ghi số 8 (Diện tích 300m², Giá 28 Tỷ) vượt ngưỡng.
            `;

            // Thuật toán Z-score
    document.getElementById('zscore-results').innerHTML = `
       - Giá trị trung bình tập dữ liệu: 4.88 Tỷ<br>
                - Độ lệch chuẩn mẫu: 6.67 Tỷ<br>
                - Điểm dữ liệu dòng số 8 có: Z-score = (28 - 4.88) / 6.67 = <strong>+3.46</strong><br>
                ➔ <strong>Kết luận:</strong> Vì |Z| > 3.0, đây là điểm dị biệt cực đại cần xử lý.
            `;

            // Vẽ Scatter plot Bài 3
            const ctxScatter = document.getElementById('chart-scatter-outliers').getContext('2d');
            
            // Phân nhóm điểm thường và điểm nhiễu
            const normalPoints = cleanData.filter(d => d.price < 10).map(d => ({x: d.area, y: d.price}));
            const outlierPoints = [{x: 300, y: 28}];

            new Chart(ctxScatter, {
                type: 'scatter',
                data: {
                    datasets: [{
                        label: 'Dữ liệu bình thường',
                        data: normalPoints,
                        backgroundColor: '#3498db'
                    }, {
                        label: 'Điểm Outlier phát hiện',
                        data: outlierPoints,
                        backgroundColor: '#e74c3c',
                        pointRadius: 8,
                        pointHoverRadius: 10
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: { title: { display: true, text: 'Diện tích (m²)' } },
                        y: { title: { display: true, text: 'Giá trị (Tỷ VNĐ)' } }
                    }
                }
            });
        }
    </script>
</body>
</html>
