<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ITA106 - Future Data Lab</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.2/papaparse.min.js"></script>
    <style>
        body { background: radial-gradient(circle at center, #1e1b4b 0%, #0f172a 100%); color: #e2e8f0; }
        .glass-panel { background: rgba(30, 41, 59, 0.6); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .neon-text { text-shadow: 0 0 10px rgba(99, 102, 241, 0.8); }
        table { border-collapse: collapse; width: 100%; }
        th, td { padding: 8px; text-align: left; border: 1px solid #334155; }
        th { background-color: #1e293b; }
    </style>
</head>
<body class="min-h-screen">

    <nav class="glass-panel border-b border-indigo-500/30 p-6 flex justify-between items-center shadow-2xl">
        <h1 class="text-3xl font-black tracking-widest text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-indigo-500 neon-text">ITA106 - FUTURE LAB</h1>
    </nav>

    <main class="max-w-7xl mx-auto p-6 grid grid-cols-1 lg:grid-cols-4 gap-6">
        <div class="glass-panel p-4 rounded-2xl">
            <h2 class="font-bold text-lg mb-4 text-cyan-400">Lab Sequence (1-8)</h2>
            <div id="labList" class="space-y-2"></div>
        </div>

        <div class="lg:col-span-3 space-y-6">
            <div id="mainContent" class="hidden space-y-6">
                <div class="glass-panel p-6 rounded-2xl">
                    <h3 class="font-bold text-lg mb-4 text-emerald-400">Data Visualization Module</h3>
                    
                    <div class="flex gap-4 mb-4">
                        <input type="file" id="csvFile" accept=".csv" class="block w-full text-sm text-gray-300">
                    </div>
                    
                    <div id="columnSelector" class="hidden mb-4 p-2 bg-slate-900 rounded">
                        <select id="colSelect" class="bg-slate-800 text-white p-2 rounded" onchange="updateChartFromCSV()"></select>
                    </div>

                    <div class="w-full h-64 bg-slate-950/50 p-4 rounded-xl mb-4">
                        <canvas id="myChart"></canvas>
                    </div>

                    <!-- Bảng thống kê -->
                    <div id="statsPanel" class="mb-4 p-4 bg-indigo-950/50 rounded-lg border border-indigo-500/50 text-indigo-200 font-mono text-sm hidden">
                        Phân tích thống kê: <span id="statsValue" class="text-cyan-400 font-bold"></span>
                    </div>

                    <!-- Bảng dữ liệu CSV -->
                    <div id="tableContainer" class="overflow-x-auto bg-slate-900 p-4 rounded-xl text-xs max-h-60 overflow-y-auto">
                        <h4 class="text-emerald-400 mb-2 font-bold uppercase">Bản dữ liệu CSV (Preview)</h4>
                        <table id="csvTable"></table>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <script>
        let csvData = [];
        let myChart = null;

        function calculateStats(data) {
            const cleanData = data.filter(n => !isNaN(n)).sort((a, b) => a - b);
            if (cleanData.length === 0) return { iqr: 0, mean: 0 };
            const q1 = cleanData[Math.floor(cleanData.length * 0.25)];
            const q3 = cleanData[Math.floor(cleanData.length * 0.75)];
            const mean = cleanData.reduce((a, b) => a + b, 0) / cleanData.length;
            return { iqr: (q3 - q1).toFixed(2), mean: mean.toFixed(2) };
        }

        document.getElementById('csvFile').addEventListener('change', function(e) {
            Papa.parse(e.target.files[0], {
                header: true, skipEmptyLines: true,
                complete: function(results) {
                    csvData = results.data;
                    renderTable(csvData);
                    const headers = Object.keys(csvData[0]);
                    const select = document.getElementById('colSelect');
                    select.innerHTML = headers.map(h => `<option value="${h}">${h}</option>`).join('');
                    document.getElementById('columnSelector').classList.remove('hidden');
                    updateChartFromCSV();
                }
            });
        });

        function renderTable(data) {
            const table = document.getElementById('csvTable');
            table.innerHTML = '';
            if (data.length === 0) return;
            const headers = Object.keys(data[0]);
            let html = `<thead><tr>${headers.map(h => `<th>${h}</th>`).join('')}</tr></thead><tbody>`;
            data.slice(0, 10).forEach(row => {
                html += `<tr>${headers.map(h => `<td>${row[h]}</td>`).join('')}</tr>`;
            });
            html += '</tbody>';
            table.innerHTML = html;
        }

        function updateChartFromCSV() {
            const col = document.getElementById('colSelect').value;
            const values = csvData.map(row => parseFloat(row[col]) || 0);
            
            // Cập nhật biểu đồ
            const ctx = document.getElementById('myChart').getContext('2d');
            if (myChart) myChart.destroy();
            myChart = new Chart(ctx, {
                type: 'bar',
                data: { labels: csvData.map((_, i) => i + 1), datasets: [{ label: col, data: values, backgroundColor: '#8b5cf6' }] },
                options: { responsive: true, maintainAspectRatio: false }
            });

            // Cập nhật thống kê
            const stats = calculateStats(values);
            document.getElementById('statsPanel').classList.remove('hidden');
            document.getElementById('statsValue').innerText = `IQR = ${stats.iqr} | Trung bình = ${stats.mean}`;
        }

        function loadLab(id) {
            document.getElementById('mainContent').classList.remove('hidden');
        }
        for(let i=1; i<=8; i++) {
            const btn = document.createElement('button');
            btn.className = "w-full text-left px-4 py-3 rounded-lg hover:bg-indigo-600/30 transition text-sm font-mono";
            btn.innerText = `[SESSION_0${i}]`;
            btn.onclick = () => loadLab(i);
            document.getElementById('labList').appendChild(btn);
        }
    </script>
</body>
</html>
