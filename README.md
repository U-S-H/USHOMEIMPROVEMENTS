<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; overflow-x: hidden; }
        .hero-v3 { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.85)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; min-height: 85vh; display: flex; align-items: center; justify-content: center; }
        .input-pro { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: #fff; }
        .input-pro:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px 35px; border-radius: 20px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; border: none; box-shadow: 0 12px 24px rgba(37, 99, 235, 0.25); width: 100%; transition: 0.3s; }
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.6s ease; }
        .form-step { display: none; }
        .form-step.active { display: block; animation: slideIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-[5000] bg-white/80 backdrop-blur-xl px-6 py-4 flex justify-between items-center border-b">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-10 w-10 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer">US</div>
            <div>
                <h1 class="text-[12px] font-black text-slate-900 uppercase leading-none">U.S. Home Improvement</h1>
                <span class="text-[8px] font-bold text-blue-600 uppercase">National Enterprise Hub</span>
            </div>
        </div>
        <div class="flex gap-4">
            <button onclick="showPage('home')" class="text-[10px] font-black uppercase text-slate-400 hover:text-blue-600">Home</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-5 py-2 rounded-full text-[10px] font-black uppercase">Get Quote</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window" class="fixed bottom-[100px] right-6 w-[340px] h-[480px] bg-white rounded-[30px] shadow-2xl hidden z-[6000] flex-col overflow-hidden border">
            <div class="bg-slate-900 p-4 text-white flex justify-between items-center">
                <span class="text-[10px] font-black uppercase">Dispatch Center</span>
                <button onclick="toggleChat()">✕</button>
            </div>
            <div id="chat-feed" class="flex-1 p-4 overflow-y-auto bg-slate-50 flex flex-col gap-3"></div>
            <div class="p-4 bg-white border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="How can we help?" class="flex-1 text-xs outline-none font-bold">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-[10px]">SEND</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-6 right-6 w-14 h-14 bg-blue-600 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[5500]">💬</button>
    </div>

    <section id="home" class="page-section active">
        <div class="hero-v3 text-center px-6">
            <div class="max-w-4xl">
                <span class="bg-blue-600/20 text-blue-400 px-4 py-1 rounded-full text-[9px] font-black uppercase tracking-widest mb-6 inline-block">Licensed • Insured • Professional</span>
                <h1 class="text-6xl md:text-9xl font-black text-white uppercase italic leading-none mb-10">Elite Home<br><span class="text-blue-500">Innovation</span></h1>
                <div class="flex flex-col md:flex-row gap-4 justify-center">
                    <button onclick="showPage('form')" class="btn-elite md:max-w-[280px]">Start Project Survey</button>
                    <button onclick="showPage('gallery')" class="bg-white/10 backdrop-blur text-white px-8 py-5 rounded-2xl font-black uppercase text-[12px] border border-white/20">View Gallery</button>
                </div>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-20 bg-white px-6">
        <div class="max-w-xl mx-auto border border-slate-100 p-8 md:p-12 rounded-[40px] shadow-2xl relative overflow-hidden">
            <div class="absolute top-0 left-0 h-1 bg-blue-600 transition-all duration-500" id="progressBar" style="width: 33.3%"></div>
            <form id="v3Form">
                <div class="form-step active" id="step1">
                    <h2 class="text-2xl font-black uppercase italic mb-8">What are we building?</h2>
                    <select id="vSvc" class="input-pro mb-6" required>
                        <option value="">Select Service...</option>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Solar">Solar Matrix</option>
                        <option value="Roofing">Premium Roofing</option>
                    </select>
                    <button type="button" onclick="nextStep(2)" class="btn-elite">Next Step</button>
                </div>
                <div class="form-step" id="step2">
                    <h2 class="text-2xl font-black uppercase italic mb-8">Site & Eligibility</h2>
                    <input type="text" id="vAddr" placeholder="Physical Address (City, State, Zip)" class="input-pro mb-4" required>
                    <select id="vCredit" class="input-pro mb-8" required>
                        <option value="">Estimated Credit Score...</option>
                        <option value="720+">Excellent (720+)</option>
                        <option value="660-719">Good (660-719)</option>
                        <option value="Below 660">Standard</option>
                    </select>
                    <div class="flex gap-4">
                        <button type="button" onclick="nextStep(1)" class="w-1/3 font-bold text-slate-400">Back</button>
                        <button type="button" onclick="nextStep(3)" class="btn-elite flex-1">Final Step</button>
                    </div>
                </div>
                <div class="form-step" id="step3">
                    <h2 class="text-2xl font-black uppercase italic mb-8">Authorization</h2>
                    <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro mb-4" required>
                    <input type="tel" id="vPhone" placeholder="Primary Phone Number" class="input-pro mb-8" required>
                    <div class="flex gap-4">
                        <button type="button" onclick="nextStep(2)" class="w-1/3 font-bold text-slate-400">Back</button>
                        <button type="submit" class="btn-elite flex-1">Authorize Transmission</button>
                    </div>
                </div>
            </form>
            <div id="vReceipt" class="hidden text-center py-10">
                <div class="w-16 h-16 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center mx-auto mb-6">✓</div>
                <h3 class="text-2xl font-black uppercase italic">Project Authorized</h3>
                <p class="text-[10px] font-bold text-slate-400 mt-2">TRACKING ID: <span id="displayTid" class="text-slate-900"></span></p>
                <p class="text-[9px] mt-6 text-slate-400 uppercase font-black">Our senior dispatcher will call you shortly.</p>
                <button onclick="location.reload()" class="mt-8 underline text-[10px] font-black uppercase text-blue-600">New Request</button>
            </div>
        </div>
    </section>

    <section id="gallery" class="page-section py-20 px-6">
        <div class="max-w-6xl mx-auto text-center">
            <h2 class="text-4xl font-black uppercase italic mb-16">The <span class="text-blue-600">Standard</span> of Work</h2>
            <div class="grid md:grid-cols-3 gap-6">
                <div class="h-64 bg-slate-200 rounded-3xl overflow-hidden group relative">
                    <img src="https://images.unsplash.com/photo-1600585154340-be6161a56a0c" class="w-full h-full object-cover">
                    <div class="absolute inset-0 bg-slate-900/60 flex items-center justify-center opacity-0 group-hover:opacity-100 transition">
                        <p class="text-white font-black uppercase text-xs italic">Premium Roofing</p>
                    </div>
                </div>
                <div class="h-64 bg-slate-200 rounded-3xl overflow-hidden group relative">
                    <img src="https://images.unsplash.com/photo-1513694203232-719a280e022f" class="w-full h-full object-cover">
                    <div class="absolute inset-0 bg-slate-900/60 flex items-center justify-center opacity-0 group-hover:opacity-100 transition">
                        <p class="text-white font-black uppercase text-xs italic">Elite Windows</p>
                    </div>
                </div>
                <div class="h-64 bg-slate-200 rounded-3xl overflow-hidden group relative">
                    <img src="https://images.unsplash.com/photo-1508514177221-188b1cf16e9d" class="w-full h-full object-cover">
                    <div class="absolute inset-0 bg-slate-900/60 flex items-center justify-center opacity-0 group-hover:opacity-100 transition">
                        <p class="text-white font-black uppercase text-xs italic">Solar Arrays</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-8 md:p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center border-b pb-8 mb-10">
                <h3 class="text-2xl font-black uppercase italic tracking-tighter">Master <span class="text-blue-600">Terminal</span></h3>
                <div id="adminControls" class="hidden flex gap-3">
                    <button onclick="exportToExcel()" class="bg-emerald-600 text-white px-5 py-2 rounded-xl text-[10px] font-black uppercase">Secure Export</button>
                    <button onclick="closeAdmin()" class="bg-red-500 text-white px-8 py-2 rounded-xl text-[10px] font-black uppercase">Exit</button>
                </div>
            </div>

            <div id="authBox" class="text-center py-24">
                <input type="password" id="pin" class="input-pro max-w-[280px] text-center text-3xl mb-6 shadow-2xl" placeholder="••••">
                <br><button onclick="unlock()" class="btn-elite max-w-[280px]">Access Secure Node</button>
            </div>

            <div id="hubData" class="hidden">
                <div class="grid md:grid-cols-4 gap-6 mb-12">
                    <div class="bg-slate-900 text-white p-8 rounded-[40px] text-center">
                        <p class="text-[9px] font-black uppercase opacity-40 mb-1">Queue Size</p>
                        <h2 id="statTotal" class="text-6xl font-black italic">0</h2>
                    </div>
                    <div class="bg-blue-600 p-8 rounded-[40px] col-span-3 text-white flex items-center">
                        <div class="w-full"><canvas id="leadsChart" height="100"></canvas></div>
                    </div>
                </div>
                <div id="adminLeads" class="grid md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
            </div>
        </div>
    </div>

    <script>
        // FIREBASE MASTER CONFIG
        const firebaseConfig = {
            apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA",
            authDomain: "ushomes07.firebaseapp.com",
            databaseURL: "https://ushomes07-default-rtdb.firebaseio.com",
            projectId: "ushomes07",
            storageBucket: "ushomes07.firebasestorage.app",
            messagingSenderId: "24299478735",
            appId: "1:24299478735:web:14f41d56809beac56521ba"
        };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const cid = "US-HUB-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo(0,0); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        function nextStep(s) { 
            document.querySelectorAll('.form-step').forEach(st => st.classList.remove('active')); 
            document.getElementById('step' + s).classList.add('active'); 
            document.getElementById('progressBar').style.width = (s * 33.3) + "%";
        }

        // LIVE CHAT ENGINE
        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + cid).push({ text: txt, type: 'user', ts: Date.now() });
            document.getElementById('chat-input').value = '';
        }
        db.ref('chats/' + cid).on('value', snap => {
            let h = `<div class="bubble bubble-admin">Secure signal active. Assistant online.</div>`;
            snap.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            const f = document.getElementById('chat-feed'); f.innerHTML = h; f.scrollTop = f.scrollHeight;
        });

        // SURVEY SUBMISSION
        document.getElementById('v3Form').onsubmit = (e) => {
            e.preventDefault();
            const tid = "DIS-" + Math.floor(10000 + Math.random() * 90000);
            const data = { tid, name:document.getElementById('vName').value, phone:document.getElementById('vPhone').value, svc:document.getElementById('vSvc').value, credit:document.getElementById('vCredit').value, addr:document.getElementById('vAddr').value, ts:new Date().toLocaleString() };
            db.ref('leads').push(data).then(() => {
                document.getElementById('v3Form').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('displayTid').innerText = tid;
            });
        };

        // ADMIN TERMINAL
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5) { document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { 
            if(document.getElementById('pin').value === "786") { 
                document.getElementById('authBox').classList.add('hidden'); 
                document.getElementById('hubData').classList.remove('hidden'); 
                document.getElementById('adminControls').classList.remove('hidden');
                syncAdmin(); 
            } 
        }

        let chart;
        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                let h = '', total = 0, counts = { Windows:0, Solar:0, Roofing:0 };
                snap.forEach(l => {
                    const v = l.val(); const k = l.key; total++;
                    if(counts[v.svc] !== undefined) counts[v.svc]++;
                    h += `<div class="p-6 bg-slate-50 rounded-[35px] border-2 border-transparent hover:border-blue-500 transition">
                        <div class="flex justify-between items-center mb-4"><span class="bg-slate-900 text-white px-3 py-1 rounded-full text-[8px] font-black">${v.tid}</span> <button onclick="db.ref('leads/${k}').remove()" class="text-red-500 font-black text-[8px]">DELETE</button></div>
                        <h4 class="font-black italic text-lg uppercase mb-4">${v.name}</h4>
                        <div class="space-y-2 text-[10px] font-bold text-slate-500 uppercase">
                            <p>📞 ${v.phone}</p><p>🛠 ${v.svc}</p><p>💳 Credit: ${v.credit}</p>
                            <div class="flex items-center gap-2 pt-2 border-t mt-2">
                                <p class="truncate">📍 ${v.addr}</p>
                                <a href="https://www.google.com/maps/search/${encodeURIComponent(v.addr)}" target="_blank" class="text-blue-600 underline text-[8px]">MAP</a>
                            </div>
                        </div>
                    </div>`;
                });
                document.getElementById('adminLeads').innerHTML = h || 'Terminal Idle.';
                document.getElementById('statTotal').innerText = total;
                updateChart(counts);
            });
        }

        function updateChart(c) {
            const ctx = document.getElementById('leadsChart').getContext('2d');
            if(chart) chart.destroy();
            chart = new Chart(ctx, { type:'bar', data: { labels:Object.keys(c), datasets:[{data:Object.values(c), backgroundColor:'#fff', borderRadius: 10}] }, options: { plugins:{legend:{display:false}}, scales:{y:{display:false}, x:{ticks:{color:'#fff', font:{weight:'bold'}}}} } });
        }

        function exportToExcel() {
            db.ref('leads').once('value', snap => {
                const ws = XLSX.utils.json_to_sheet(Object.values(snap.val() || {}));
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "Leads");
                XLSX.writeFile(wb, "US_Leads_Master.xlsx");
            });
        }
    </script>
</body>
</html>
