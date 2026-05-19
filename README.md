<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ITA106 - Hệ Thống Quản Lý Lab Cao Cấp</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-slate-100 min-h-screen">

    <nav class="bg-indigo-900 text-white shadow-xl p-6 flex justify-between items-center">
        <h1 class="text-2xl font-bold tracking-tight">ITA106 - Lab Management Portal</h1>
        <div class="text-sm bg-indigo-800 px-4 py-1 rounded-full">Trạng thái: Đã lưu cục bộ</div>
    </nav>

    <main class="max-w-7xl mx-auto p-6 grid grid-cols-1 lg:grid-cols-4 gap-6">
        
        <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-200">
            <h2 class="font-bold text-lg mb-4 text-indigo-900">Danh sách Lab (1-8)</h2>
            <div id="labList" class="space-y-2"></div>
        </div>

        <div class="lg:col-span-3 space-y-6">
            <div id="mainContent" class="hidden space-y-6">
                <div class="bg-white p-8 rounded-2xl shadow-sm border-l-8 border-indigo-600">
                    <h2 id="labHeader" class="text-3xl font-extrabold text-slate-900">Lab 1</h2>
                    <p class="text-slate-500 mt-2">Hệ thống tự động lưu trữ code và tệp của bạn.</p>
                </div>

                <div class="bg-white p-6 rounded-2xl shadow-sm">
                    <h3 class="font-bold text-lg mb-4 text-indigo-900">Tài nguyên & Tệp đính kèm</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <!-- Slide -->
                        <div class="border-2 border-dashed border-slate-200 p-6 rounded-xl text-center hover:border-indigo-400 transition">
                            <label class="cursor-pointer block">
                                <span class="text-sm font-semibold">Tải Slide lên</span>
                                <input type="file" id="slideInput" class="hidden" onchange="handleFile(event, 'slide')">
                            </label>
                            <div id="slidePreview" class="mt-2 text-xs text-indigo-600 font-bold"></div>
                            <a id="slideLink" href="#" target="_blank" class="hidden mt-2 inline-block bg-indigo-100 text-indigo-700 px-3 py-1 rounded-full text-xs font-bold hover:bg-indigo-200">Mở Slide</a>
                        </div>
                        <!-- Assessment -->
                        <div class="border-2 border-dashed border-slate-200 p-6 rounded-xl text-center hover:border-indigo-400 transition">
                            <label class="cursor-pointer block">
                                <span class="text-sm font-semibold">Tải Assessment lên</span>
                                <input type="file" id="assessInput" class="hidden" onchange="handleFile(event, 'assess')">
                            </label>
                            <div id="assessPreview" class="mt-2 text-xs text-indigo-600 font-bold"></div>
                            <a id="assessLink" href="#" target="_blank" class="hidden mt-2 inline-block bg-indigo-100 text-indigo-700 px-3 py-1 rounded-full text-xs font-bold hover:bg-indigo-200">Mở Assessment</a>
                        </div>
                    </div>
                </div>

                <div class="bg-white p-6 rounded-2xl shadow-sm">
                    <h3 class="font-bold text-lg mb-4 text-indigo-900">Soạn thảo Code (Bài 1-4)</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <textarea id="c1" class="h-32 bg-slate-900 text-emerald-400 p-4 rounded-xl font-mono text-sm shadow-inner" placeholder="Bài 1..."></textarea>
                        <textarea id="c2" class="h-32 bg-slate-900 text-emerald-400 p-4 rounded-xl font-mono text-sm shadow-inner" placeholder="Bài 2..."></textarea>
                        <textarea id="c3" class="h-32 bg-slate-900 text-emerald-400 p-4 rounded-xl font-mono text-sm shadow-inner" placeholder="Bài 3..."></textarea>
                        <textarea id="c4" class="h-32 bg-slate-900 text-emerald-400 p-4 rounded-xl font-mono text-sm shadow-inner" placeholder="Bài 4..."></textarea>
                    </div>
                    <button onclick="saveData()" class="mt-6 w-full bg-indigo-600 text-white py-4 rounded-xl font-bold hover:bg-indigo-700 transition shadow-lg">Lưu tiến độ Lab này</button>
                </div>
            </div>
        </div>
    </main>

    <script>
        let currentLab = 1;

        const labList = document.getElementById('labList');
        for(let i=1; i<=8; i++) {
            const btn = document.createElement('button');
            btn.className = "w-full text-left px-4 py-3 rounded-xl hover:bg-indigo-50 transition font-medium text-slate-700";
            btn.innerText = `Lab ${i}`;
            btn.onclick = () => loadLab(i);
            labList.appendChild(btn);
        }

        function loadLab(id) {
            currentLab = id;
            document.getElementById('mainContent').classList.remove('hidden');
            document.getElementById('labHeader').innerText = `Thực hành Lab ${id}`;
            
            // Tải Code
            document.getElementById('c1').value = localStorage.getItem(`lab${id}_c1`) || "";
            document.getElementById('c2').value = localStorage.getItem(`lab${id}_c2`) || "";
            document.getElementById('c3').value = localStorage.getItem(`lab${id}_c3`) || "";
            document.getElementById('c4').value = localStorage.getItem(`lab${id}_c4`) || "";
            
            // Tải File (Slide và Assessment)
            loadFileInfo(id, 'slide');
            loadFileInfo(id, 'assess');
        }

        function loadFileInfo(labId, type) {
            const sName = localStorage.getItem(`lab${labId}_${type}Name`);
            const sUrl = localStorage.getItem(`lab${labId}_${type}Url`);
            if(sName && sUrl) {
                document.getElementById(`${type}Preview`).innerText = "Tệp: " + sName;
                const link = document.getElementById(`${type}Link`);
                link.href = sUrl;
                link.classList.remove('hidden');
            } else {
                document.getElementById(`${type}Preview`).innerText = "";
                document.getElementById(`${type}Link`).classList.add('hidden');
            }
        }

        function saveData() {
            localStorage.setItem(`lab${currentLab}_c1`, document.getElementById('c1').value);
            localStorage.setItem(`lab${currentLab}_c2`, document.getElementById('c2').value);
            localStorage.setItem(`lab${currentLab}_c3`, document.getElementById('c3').value);
            localStorage.setItem(`lab${currentLab}_c4`, document.getElementById('c4').value);
            alert(`Đã lưu tiến độ Lab ${currentLab}!`);
        }

        function handleFile(event, type) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const url = e.target.result;
                    document.getElementById(`${type}Preview`).innerText = "Tệp: " + file.name;
                    const link = document.getElementById(`${type}Link`);
                    link.href = url;
                    link.classList.remove('hidden');
                    // Lưu vào localStorage
                    localStorage.setItem(`lab${currentLab}_${type}Name`, file.name);
                    localStorage.setItem(`lab${currentLab}_${type}Url`, url);
                };
                reader.readAsDataURL(file);
            }
        }
    </script>
</body>
</html>
