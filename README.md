<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ITA106 - Quản Lý Lab Cá Nhân</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body class="bg-slate-50 min-h-screen">

    <nav class="bg-indigo-900 text-white shadow-lg p-6">
        <h1 class="text-2xl font-bold">Portal Quản Lý & Nộp Bài ITA106</h1>
    </nav>

    <main class="max-w-7xl mx-auto p-6 grid grid-cols-1 lg:grid-cols-4 gap-6">
        
        <!-- Sidebar chọn Lab -->
        <div class="bg-white p-4 rounded-xl shadow-md border-r border-slate-200">
            <h2 class="font-bold text-lg mb-4">Danh sách Lab (1-8)</h2>
            <div id="labList" class="space-y-2"></div>
        </div>

        <!-- Khu vực hiển thị chi tiết theo Lab -->
        <div class="lg:col-span-3 space-y-6">
            
            <!-- Thông tin Lab -->
            <div class="bg-white p-6 rounded-xl shadow-md border-l-8 border-indigo-700">
                <h2 id="labHeader" class="text-2xl font-bold text-indigo-900">Vui lòng chọn Lab</h2>
                <p id="labStatus" class="text-sm text-slate-500 mt-2">Chọn một mục từ danh sách bên trái để tải tệp và nộp code.</p>
            </div>

            <!-- Khu vực tải file -->
            <div id="fileZone" class="bg-white p-6 rounded-xl shadow-md hidden">
                <h3 class="font-bold mb-4">Tệp đính kèm cho Lab này</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="border-2 border-dashed border-slate-300 p-4 rounded-lg text-center">
                        <p class="text-xs text-slate-500">Tải Slide (Lab này)</p>
                        <input type="file" class="w-full mt-2 text-xs">
                    </div>
                    <div class="border-2 border-dashed border-slate-300 p-4 rounded-lg text-center">
                        <p class="text-xs text-slate-500">Tải Assessment</p>
                        <input type="file" class="w-full mt-2 text-xs">
                    </div>
                </div>
            </div>

            <!-- Khu vực code từng bài -->
            <div id="codeZone" class="bg-white p-6 rounded-xl shadow-md hidden">
                <h3 class="font-bold mb-4">Soạn thảo Code (Bài 1-4)</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <textarea id="c1" class="h-24 bg-slate-900 text-emerald-400 p-3 rounded font-mono text-xs" placeholder="Bài 1..."></textarea>
                    <textarea id="c2" class="h-24 bg-slate-900 text-emerald-400 p-3 rounded font-mono text-xs" placeholder="Bài 2..."></textarea>
                    <textarea id="c3" class="h-24 bg-slate-900 text-emerald-400 p-3 rounded font-mono text-xs" placeholder="Bài 3..."></textarea>
                    <textarea id="c4" class="h-24 bg-slate-900 text-emerald-400 p-3 rounded font-mono text-xs" placeholder="Bài 4..."></textarea>
                </div>
                <button onclick="saveData()" class="mt-4 w-full bg-indigo-700 text-white py-2 rounded font-bold">Lưu & Nộp Code</button>
            </div>
        </div>
    </main>

    <script>
        const labList = document.getElementById('labList');
        
        for(let i=1; i<=8; i++) {
            const btn = document.createElement('button');
            btn.className = "w-full text-left px-4 py-2 rounded-lg hover:bg-indigo-100 transition font-medium text-slate-700";
            btn.innerText = `Lab ${i}`;
            btn.onclick = () => {
                document.getElementById('labHeader').innerText = `Thực hành Lab ${i}`;
                document.getElementById('labStatus').innerText = "Đã tải dữ liệu cấu hình cho Lab này.";
                document.getElementById('fileZone').classList.remove('hidden');
                document.getElementById('codeZone').classList.remove('hidden');
            };
            labList.appendChild(btn);
        }

        function saveData() {
            alert("Đã lưu nội dung và gửi file đính kèm cho Lab hiện tại!");
        }
    </script>
</body>
</html>
