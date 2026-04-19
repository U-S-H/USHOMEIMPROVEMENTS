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
        
        .hero-v3 { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.85)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; min-height: 80vh; display: flex; align-items: center; justify-content: center; }
        .glass-blur { background: rgba(255, 255, 255, 0.85); backdrop-filter: blur(20px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        
        .input-pro { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: #fff; }
        .input-pro:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px 35px; border-radius: 20px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; border: none; box-shadow: 0 12px 24px rgba(37, 99, 235, 0.25); width: 100%; transition: 0.3s; }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.6s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* Multi-Step Form */
        .form-step { display: none; }
        .form-step.active { display: block; animation: slideIn 0.4s ease; }
        @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }

        /* Chat System */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 350px; height: 500px; background: white; border-radius: 25px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.2); display: none; flex-direction: column; z-index: 9999; border: 1px solid #f1f5f9; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; display: flex; flex-direction: column; gap: 10px; background: #f8fafc; }
        .bubble { padding: 12px 16px; border-radius: 18px; font-size: 13px; max-width: 80%; line-height: 1.5; font-weight: 500; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; border: 1px solid #e2e8f0; }
    </style>
</head>
<body>

    <nav class="glass-blur sticky top-0 z-[5000] px-6 py-4 flex justify-between items-center">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-10 w-10 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer">US</div>
            <div>
                <h1 class="text-[12px] font-black text-slate-900 uppercase leading-none">U.S. Home Improvement</h1>
                <span class="text-[8px] font-bold text-blue-600 uppercase">National Enterprise Hub</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-2 rounded-full text-[10px] font-black uppercase tracking-wider">Get Quote</button>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="bg-slate-900 p-4 text-white flex items-center justify-between">
                <span class="text-[10px] font-black uppercase">Live Support</span>
                <button onclick="toggleChat()" class="text-xs opacity-50">✕</button>
            </div>
            <div id="chat-feed"></div>
            <div class="p-4 bg-white border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="Type message..." class="flex-1 text-xs outline-none font-semibold">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-[10px] uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-6 right-6 w-14 h-14 bg-blue-600 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[9000]">💬</button>
    </div>

    <section id="home" class="page-section active">
        <div class="hero-v3 text-center px-6">
            <div class="max-w-4xl">
                <h1 class="text-6xl md:text-9xl font-black text-white uppercase italic leading-none mb-10">Premium<br><span class="text-blue-500">Contracting</span></h1>
                <button onclick="showPage('form')" class="btn-elite max-w-[300px]">Start Free Survey</button>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-20 bg-white px-6">
        <div class="max-w-xl mx-auto border border-slate-100 p-8 md:p-12 rounded-[40px] shadow-2xl">
            <form id="v3Form">
                <div class="form-step active" id="step1">
                    <h2 class="text-2xl font-black uppercase italic mb-8">Service Portfolio</h2>
                    <select id="vSvc" class="input-pro mb-4" required>
                        <option value="">Choose Service...</option>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Roofing">Roofing & Exterior</option>
                    </select>
                    <button type="button" onclick="nextStep(2)" class="btn-elite">Continue</button>
                </div>
                <div class="form-step" id="step2">
                    <h2 class="text-2xl font-black uppercase italic mb-8">Site Details</h2>
                    <input type="text" id="vAddr" placeholder="Property Address (US)" class="input-pro mb-4" required>
                    <select id="vCredit" class="input-pro mb-8" required>
                        <option value="">Credit Score...</option>
                        <option value="720+">Excellent (720+)</option>
                        <option value="660-719">Good (660-719)</option>
                        <option value="Below 660">Fair/Poor</option>
                    </select>
                    <div class="flex gap-4">
                        <button type="button" onclick="nextStep(1)" class="w-1/2 font-bold text-slate-400">Back</button>
                        <button type="button" onclick="nextStep(3)" class="btn-elite">Finalize</button>
                    </div>
                </div>
                <div class="form-step" id="step3">
                    <h2 class="text-2xl font-black uppercase italic mb-8">Transmission</h2>
                    <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro mb-4" required>
                    <input type="tel" id="vPhone" placeholder="Primary Phone" class="input-pro mb-8" required>
                    <button type="submit" class="btn-elite">Authorize Request</button>
                </div>
            </form>
            <div id="vReceipt" class="hidden text-center py-10">
                <h3 class="text-3xl font-black uppercase italic text-blue-600">Authorized</h3>
                <p class="text-[10px] font-bold text-slate-400 mt-2">CASE ID: <span id="displayTid" class="text-slate-900"></span></p>
                <button onclick="location.reload()" class="mt-10 underline text-[10px] font-black uppercase">New Project</button>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-10">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center border-b pb-8 mb-10">
                <h3 class="text-2xl font-black uppercase italic">Master <span class="text-blue-600">Terminal</span></h3>
                <div id="adminControls" class="hidden flex gap-4">
                    <button onclick="exportToExcel()" class="bg-emerald-500 text-white px-5 py-2 rounded-xl text-[10px] font-black">SECURE EXPORT</button>
                    <button onclick="closeAdmin()" class="bg-red-500 text-white px-5 py-2 rounded-xl text-[10px] font-black">EXIT</button>
                </div>
            </div>

            <div id="authBox" class="text-center py-20">
                <input type="password" id="pin" class="input-pro max-w-[250px] text-center text-2xl mb-6 shadow-lg" placeholder="••••">
                <br><button onclick="unlock()" class="btn-elite max-w-[250px]">Login</button>
            </div>

            <div id="hubData" class="hidden">
                <div class="grid md:grid-cols-4 gap-6 mb-12">
                    <div class="bg-slate-900 text-white p-8 rounded-[30px] col-span-1 text-center">
                        <p class="text-[9px] font-black uppercase opacity-50 mb-1">Queue</p>
                        <h2 id="statTotal" class="text-5xl font-black italic">0</h2>
                    </div>
                    <div class="bg-blue-600 p-8 rounded-[30px] col-span-3 text-white">
                        <canvas id="leadsChart" height="100"></canvas>
                    </div>
                </div>
                <div id="adminLeads" class="grid md:grid-cols-2 gap-6"></div>
            </div>
        </div>
    </div>

    <script>
        // UPDATED CONFIG
        const firebaseConfig = {
            apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA",
            authDomain: "ushomes07.firebaseapp.com",
            databaseURL: "https://ushomes07-default-rtdb.firebaseio.com",
            projectId: "ushomes07",
            storageBucket: "ushomes07.firebasestorage.app",
            messagingSenderId: "24299478735",
            appId: "1:24299478735:web:14f41d56809beac56521ba" // Updated ID
        };

        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const cid = "USER-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        function nextStep(s) { document.querySelectorAll('.form-step').forEach(st => st.classList.remove('active')); document.getElementById('step' + s).classList.add('active'); }

        // CHAT SYNC
        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + cid).push({ text: txt, type: 'user', ts: Date.now() });
            document.getElementById('chat-input').value = '';
        }
        db.ref('chats/' + cid).on('value', snap => {
            let h = `<div class="bubble bubble-admin">Secure signal established. Agent-786 is online.</div>`;
            snap.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            const f = document.getElementById('chat-feed'); f.innerHTML = h; f.scrollTop = f.scrollHeight;
        });

        // FORM SUBMISSION
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

        // ADMIN HUB SECURITY
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5) { document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        
        function unlock() { 
            if(document.getElementById('pin').value === "786") { 
                document.getElementById('authBox').classList.add('hidden'); 
                document.getElementById('hubData').classList.remove('hidden'); 
                document.getElementById('adminControls').classList.remove('hidden'); // Export button shows only on login
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
                    h += `<div class="p-6 bg-slate-50 rounded-[30px] border border-slate-100">
                        <div class="flex justify-between mb-4"><span class="bg-blue-600 text-white px-2 py-1 rounded-lg text-[8px] font-black">${v.tid}</span> <button onclick="db.ref('leads/${k}').remove()" class="text-red-500 font-bold text-[8px]">DELETE</button></div>
                        <h4 class="font-black italic text-lg uppercase">${v.name}</h4>
                        <div class="grid grid-cols-2 gap-2 mt-4 text-[10px] font-bold text-slate-500">
                            <p>📞 ${v.phone}</p><p>🛠 ${v.svc}</p><p>💳 ${v.credit}</p><p>📍 ${v.addr}</p>
                        </div>
                    </div>`;
                });
                document.getElementById('adminLeads').innerHTML = h || 'No Active Leads.';
                document.getElementById('statTotal').innerText = total;
                updateChart(counts);
            });
        }

        function updateChart(c) {
            const ctx = document.getElementById('leadsChart').getContext('2d');
            if(chart) chart.destroy();
            chart = new Chart(ctx, { type:'bar', data: { labels:Object.keys(c), datasets:[{data:Object.values(c), backgroundColor:'#fff'}] }, options: { plugins:{legend:{display:false}}, scales:{y:{display:false}, x:{ticks:{color:'#fff', font:{weight:'bold'}}}} } });
        }

        function exportToExcel() {
            db.ref('leads').once('value', snap => {
                const ws = XLSX.utils.json_to_sheet(Object.values(snap.val() || {}));
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "Leads");
                XLSX.writeFile(wb, "Secure_US_Leads.xlsx");
            });
        }
    </script>
</body>
</html>
