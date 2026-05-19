<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ITA106 - Future Data Lab</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            background: radial-gradient(circle at center, #1e1b4b 0%, #0f172a 100%);
            color: #e2e8f0;
        }
        .glass-panel {
            background: rgba(30, 41, 59, 0.6);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .neon-text {
            text-shadow: 0 0 10px rgba(99, 102, 241, 0.8);
        }
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
                    <p class="text-cyan-200/70 mt-2 font-mono italic">Đang tải mô-đun thực hành...</p>
                </div>

                <div class="glass-panel p-6 rounded-2xl">
                    <h3 class="font-bold text-lg mb-4 text-cyan-400">Data Modules</h3>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div class="border border-purple-500/30 bg-purple-950/20 p-6 rounded-xl text-center hover:bg-purple-900/40 transition">
                            <label class="cursor-pointer block"><span class="text-xs font-semibold uppercase">Lý thuyết</span><input type="file" id="theoryInput" class="hidden" onchange="handleFile(event, 'theory')"></label>
                            <div id="theoryPreview" class="mt-2 text-[10px] text-purple-300 font-mono truncate"></div>
                            <a id="theoryLink" href="#" target="_blank" class="hidden mt-2 inline-block bg-purple-600 text-white px-3 py-1 rounded-full text-[10px] font-bold">MỞ FILE</a>
                        </div>
                        <div class="border border-indigo-500/30 bg-indigo-950/20 p-6 rounded-xl text-center hover:bg-indigo-900/40 transition">
                            <label class="cursor-pointer block"><span class="text-xs font-semibold uppercase">Slide Lab</span><input type="file" id="slideInput" class="hidden" onchange="handleFile(event, 'slide')"></label>
                            <div id="slidePreview" class="mt-2 text-[10px] text-indigo-300 font-mono truncate"></div>
                            <a id="slideLink" href="#" target="_blank" class="hidden mt-2 inline-block bg-indigo-600 text-white px-3 py-1 rounded-full text-[10px] font-bold">MỞ FILE</a>
                        </div>
                        <div class="border border-blue-500/30 bg-blue-950/20 p-6 rounded-xl text-center hover:bg-blue-900/40 transition">
                            <label class="cursor-pointer block"><span class="text-xs font-semibold uppercase">Assessment</span><input type="file" id="assessInput" class="hidden" onchange="handleFile(event, 'assess')"></label>
                            <div id="assessPreview" class="mt-2 text-[10px] text-blue-300 font-mono truncate"></div>
                            <a id="assessLink" href="#" target="_blank" class="hidden mt-2 inline-block bg-blue-600 text-white px-3 py-1 rounded-full text-[10px] font-bold">MỞ FILE</a>
                        </div>
                    </div>
                </div>

                <div class="glass-panel p-6 rounded-2xl">
                    <h3 class="font-bold text-lg mb-4 text-cyan-400">Code Execution (Python)</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <textarea id="c1" class="h-32 bg-slate-950/50 text-emerald-400 p-4 rounded-xl font-mono text-xs border border-emerald-900 focus:border-emerald-500" placeholder="Bài 1..."></textarea>
                        <textarea id="c2" class="h-32 bg-slate-950/50 text-emerald-400 p-4 rounded-xl font-mono text-xs border border-emerald-900 focus:border-emerald-500" placeholder="Bài 2..."></textarea>
                        <textarea id="c3" class="h-32 bg-slate-950/50 text-emerald-400 p-4 rounded-xl font-mono text-xs border border-emerald-900 focus:border-emerald-500" placeholder="Bài 3..."></textarea>
                        <textarea id="c4" class="h-32 bg-slate-950/50 text-emerald-400 p-4 rounded-xl font-mono text-xs border border-emerald-900 focus:border-emerald-500" placeholder="Bài 4..."></textarea>
                    </div>
                    <button onclick="saveData()" class="mt-6 w-full bg-cyan-600 text-slate-950 py-4 rounded-xl font-black hover:bg-cyan-400 transition shadow-[0_0_20px_rgba(34,211,238,0.4)]">SAVE DATA SYNC</button>
                </div>
            </div>
        </div>
    </main>

    <script>
        let currentLab = 1;
        const labList = document.getElementById('labList');
        for(let i=1; i<=8; i++) {
            const btn = document.createElement('button');
            btn.className = "w-full text-left px-4 py-3 rounded-lg hover:bg-indigo-600/30 transition text-sm font-mono border border-transparent hover:border-indigo-500/50";
            btn.innerText = `[SESSION_0${i}]`;
            btn.onclick = () => loadLab(i);
            labList.appendChild(btn);
        }

        function loadLab(id) {
            currentLab = id;
            document.getElementById('mainContent').classList.remove('hidden');
            document.getElementById('labHeader').innerText = `Lab Session 0${id}`;
            document.getElementById('c1').value = localStorage.getItem(`lab${id}_c1`) || "";
            document.getElementById('c2').value = localStorage.getItem(`lab${id}_c2`) || "";
            document.getElementById('c3').value = localStorage.getItem(`lab${id}_c3`) || "";
            document.getElementById('c4').value = localStorage.getItem(`lab${id}_c4`) || "";
            loadFileInfo(id, 'theory');
            loadFileInfo(id, 'slide');
            loadFileInfo(id, 'assess');
        }

        function loadFileInfo(labId, type) {
            const sName = localStorage.getItem(`lab${labId}_${type}Name`);
            const sUrl = localStorage.getItem(`lab${labId}_${type}Url`);
            if(sName && sUrl) {
                document.getElementById(`${type}Preview`).innerText = sName;
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
            alert(`Sync Successful: Session 0${currentLab}`);
        }

        function handleFile(event, type) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const url = e.target.result;
                    document.getElementById(`${type}Preview`).innerText = file.name;
                    const link = document.getElementById(`${type}Link`);
                    link.href = url;
                    link.classList.remove('hidden');
                    localStorage.setItem(`lab${currentLab}_${type}Name`, file.name);
                    localStorage.setItem(`lab${currentLab}_${type}Url`, url);
                };
                reader.readAsDataURL(file);
            }
        }
    </script>
</body>
</html>
