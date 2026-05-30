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
    </style>
</head>
<body class="min-h-screen">

    <nav class="glass-panel border-b border-indigo-500/30 p-6 flex justify-between items-center shadow-2xl">
        <h1 class="text-3xl font-black tracking-widest text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-indigo-500 neon-text">ITA106 - FUTURE LAB</h1>
        <div class="text-xs font-mono bg-indigo-950 px-4 py-1 rounded border border-indigo-500">SYSTEM: ACTIVE</div>
    </nav>

    <main class="max-w-7xl mx-auto p-6 grid grid-cols-1 lg:grid-cols-4 gap-6">
        <div class="glass-panel p-4 rounded-2xl">
            <h2 class="font-bold text-lg mb-4 text-cyan-400">Lab Sequence (1-8)</h2>
            <div id="labList" class="space-y-2"></div>
        </div>

        <div class="lg:col-span-3 space-y-6">
            <div id="mainContent" class="hidden space-y-6">
                <div class="glass-panel p-8 rounded-2xl border-l-4 border-cyan-400">
                    <h2 id="labHeader" class="text-4xl font-black text-white neon-text">Lab 1</h2>
                </div>

                <!-- CSV Visualization -->
                <div class="glass-panel p-6 rounded-2xl">
                    <h3 class="font-bold text-lg mb-4 text-emerald-400">Data Visualization Module</h3>
                    <input type="file" id="csvFile" accept=".csv" class="mb-4 block w-full text-sm text-gray-300">
                    <div id="columnSelector" class="hidden mb-4 p-2 bg-slate-900 rounded">
                        <label class="text-xs font-bold text-emerald-400">CHỌN CỘT CSV:</label>
                        <select id="colSelect" class="bg-slate-800 text-white p-2 rounded ml-2" onchange="updateChartFromCSV()"></select>
                    </div>
                    <div class="w-full h-64 bg-slate-950/50 p-4 rounded-xl">
                        <canvas id="myChart"></canvas>
                    </div>
                </div>

                <!-- Code Execution -->
                <div class="glass-panel p-6 rounded-2xl">
                    <h3 class="font-bold text-lg mb-4 text-cyan-400">Code Execution (Python)</h3>
                    <textarea id="c1" class="w-full h-20 bg-slate-950/50 text-emerald-400 p-4 rounded-xl font-mono text-xs border border-emerald-900" placeholder="Nhập dãy số: 10, 20, 30, 40"></textarea>
                    <button onclick="drawFromCode()" class="mt-4 bg-emerald-600 px-6 py-2 rounded-lg font-bold text-sm hover:bg-emerald-500">VẼ BIỂU ĐỒ TỪ CODE</button>
                </div>
            </div>
        </div>
    </main>

    <script>
        let myChart = null;
        let csvData = [];

        // --- Cũ: Vẽ từ CSV ---
        document.getElementById('csvFile').addEventListener('change', function(e) {
            Papa.parse(e.target.files[0], {
                header: true, skipEmptyLines: true,
                complete: function(results) {
                    csvData = results.data;
                    const headers = Object.keys(csvData[0]);
                    const select = document.getElementById('colSelect');
                    select.innerHTML = headers.map(h => `<option value="${h}">${h}</option>`).join('');
                    document.getElementById('columnSelector').classList.remove('hidden');
                    updateChartFromCSV();
                }
            });
        });

        function updateChartFromCSV() {
            const col = document.getElementById('colSelect').value;
            renderChart(csvData.map(row => parseFloat(row[col]) || 0), `Cột: ${col}`);
        }

        // --- Mới: Vẽ từ Code ---
        function drawFromCode() {
            const codeInput = document.getElementById('c1').value;
            const data = codeInput.split(',').map(val => parseFloat(val.trim())).filter(val => !isNaN(val));
            if (data.length > 0) {
                renderChart(data, "Dữ liệu từ Code");
            } else {
                alert("Vui lòng nhập dãy số hợp lệ cách nhau bằng dấu phẩy");
            }
        }

        function renderChart(data, label) {
            const ctx = document.getElementById('myChart').getContext('2d');
            if (myChart) myChart.destroy();
            myChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: data.map((_, i) => i + 1),
                    datasets: [{ label: label, data: data, backgroundColor: '#8b5cf6' }]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });
        }

        function loadLab(id) {
            document.getElementById('mainContent').classList.remove('hidden');
            document.getElementById('labHeader').innerText = `Lab Session 0${id}`;
        }
        for(let i=1; i<=8; i++) {
            const btn = document.createElement('button');
            btn.className = "w-full text-left px-4 py-3 rounded-lg hover:bg-indigo-600/30 transition text-sm font-mono border border-transparent";
            btn.innerText = `[SESSION_0${i}]`;
            btn.onclick = () => loadLab(i);
            document.getElementById('labList').appendChild(btn);
        }
    </script>
</body>
</html>
