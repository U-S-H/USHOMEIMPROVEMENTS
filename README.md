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
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; scroll-behavior: smooth; }
        .hero-v3 { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.85)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
        .glass-blur { background: rgba(255, 255, 255, 0.85); backdrop-filter: blur(20px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; outline: none; transition: 0.4s; font-size: 14px; background: #fff; }
        .input-pro:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px 32px; border-radius: 16px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; border: none; transition: 0.4s; box-shadow: 0 12px 24px rgba(37, 99, 235, 0.25); width: 100%; }
        
        .page-section { display: none; }
        .page-section.active { display: block; animation: contentFade 0.7s ease-out; }
        @keyframes contentFade { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .form-step { display: none; }
        .form-step.active { display: block; animation: stepFade 0.5s ease; }
        @keyframes stepFade { from { opacity: 0; transform: translateX(10px); } to { opacity: 1; transform: translateX(0); } }

        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 30px; box-shadow: 0 30px 60px -12px rgba(0,0,0,0.25); display: none; flex-direction: column; z-index: 6000; overflow: hidden; border: 1px solid #f1f5f9; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); }
    </style>
</head>
<body>

    <nav class="glass-blur sticky top-0 z-[5000] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <div onclick="handleAdminTap()" class="h-12 w-12 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer shadow-lg">US</div>
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic">Enterprise National Hub</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-full text-[10px] font-black uppercase">Get Quote</button>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="bg-[#0f172a] p-5 text-white flex items-center gap-3">
                <div class="w-2 h-2 bg-emerald-500 rounded-full"></div>
                <h4 class="font-black uppercase text-[10px]">Senior Dispatch Support</h4>
                <button onclick="toggleChat()" class="ml-auto opacity-50">✕</button>
            </div>
            <div id="chat-feed" class="flex-1 p-5 overflow-y-auto bg-slate-50 flex flex-col gap-3"></div>
            <div class="p-4 border-t bg-white flex gap-2">
                <input type="text" id="chat-input" placeholder="Type message..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-[10px] uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-14 h-14 bg-slate-900 rounded-full shadow-2xl flex items-center justify-center text-white text-xl z-[5500]">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-v3 py-56 px-6 text-center text-white">
            <span class="bg-blue-600/20 text-blue-400 border border-blue-600/30 px-4 py-1 rounded-full text-[10px] font-black uppercase tracking-widest mb-8 inline-block">Authorized National Network</span>
            <h1 class="text-6xl md:text-9xl font-black uppercase italic mb-8 leading-none">The Elite <br><span class="text-blue-500">Standard</span>.</h1>
            <button onclick="showPage('form')" class="btn-elite max-w-[350px]">Start Free Evaluation</button>
        </header>
    </section>

    <section id="form" class="page-section py-20 bg-white px-6">
        <div class="max-w-2xl mx-auto bg-white p-10 md:p-16 rounded-[48px] shadow-2xl border border-slate-100">
            <div class="mb-10 flex gap-2">
                <div id="dot1" class="h-2 flex-1 bg-blue-600 rounded-full"></div>
                <div id="dot2" class="h-2 flex-1 bg-slate-100 rounded-full"></div>
                <div id="dot3" class="h-2 flex-1 bg-slate-100 rounded-full"></div>
            </div>

            <form id="v3Form">
                <div class="form-step active" id="step1">
                    <h3 class="text-2xl font-black uppercase italic mb-8 text-slate-900">What project are we starting?</h3>
                    <div class="grid grid-cols-1 gap-4">
                        <select id="vSvc" class="input-pro" required>
                            <option value="">Select Service...</option>
                            <option value="Windows">Windows Replacement</option>
                            <option value="Roofing">Roofing Installation</option>
                            <option value="Solar">Solar Power Matrix</option>
                            <option value="Garage">Garage & Exterior</option>
                        </select>
                        <select id="vTimeline" class="input-pro" required>
                            <option value="">Timeline...</option>
                            <option value="Immediate">ASAP</option>
                            <option value="1-3 Months">1-3 Months</option>
                            <option value="Planning">Future Planning</option>
                        </select>
                    </div>
                    <button type="button" onclick="nextStep(2)" class="btn-elite mt-8">Next Step</button>
                </div>

                <div class="form-step" id="step2">
                    <h3 class="text-2xl font-black uppercase italic mb-8 text-slate-900">Site & Eligibility</h3>
                    <input type="text" id="vAddr" placeholder="Physical Address (City, State, Zip)" class="input-pro mb-4" required>
                    <select id="vCredit" class="input-pro mb-8" required>
                        <option value="">Credit Score Range...</option>
                        <option value="720+">Excellent (720+)</option>
                        <option value="660-719">Good (660-719)</option>
                        <option value="Below 660">Building (Below 660)</option>
                    </select>
                    <div class="flex gap-4">
                        <button type="button" onclick="nextStep(1)" class="w-1/3 bg-slate-100 text-slate-500 font-bold rounded-xl">Back</button>
                        <button type="button" onclick="nextStep(3)" class="btn-elite flex-1">Final Step</button>
                    </div>
                </div>

                <div class="form-step" id="step3">
                    <h3 class="text-2xl font-black uppercase italic mb-8 text-slate-900">Transmission Details</h3>
                    <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro mb-4" required>
                    <input type="tel" id="vPhone" placeholder="Mobile Number" class="input-pro mb-4" required>
                    <div class="grid grid-cols-2 gap-4 mb-8">
                        <input type="date" id="vDate" class="input-pro" required>
                        <select id="vTime" class="input-pro" required>
                            <option value="Morning">Morning</option>
                            <option value="Afternoon">Afternoon</option>
                        </select>
                    </div>
                    <div class="flex gap-4">
                        <button type="button" onclick="nextStep(2)" class="w-1/3 bg-slate-100 text-slate-500 font-bold rounded-xl">Back</button>
                        <button type="submit" class="btn-elite flex-1">Authorize & Send</button>
                    </div>
                </div>
            </form>

            <div id="vReceipt" class="hidden text-center py-10 animate-pulse">
                <h3 class="text-4xl font-black text-blue-600 mb-4 uppercase italic">Authorized</h3>
                <p class="text-xs font-bold text-slate-500 uppercase">Tracking ID: <span id="displayTid" class="text-slate-900 font-black"></span></p>
                <button onclick="location.reload()" class="underline text-[10px] font-black uppercase mt-12 block mx-auto text-slate-400">New Request</button>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-8 md:p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b-2 pb-8">
                <div>
                    <h3 class="text-3xl font-black uppercase italic">Master <span class="text-blue-600">Terminal</span></h3>
                    <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mt-1">Enterprise Analytics & Leads</p>
                </div>
                <div id="adminControls" class="hidden flex gap-4">
                    <button onclick="exportToExcel()" class="bg-emerald-600 text-white px-6 py-3 rounded-xl text-[10px] font-black">EXPORT EXCEL</button>
                    <button onclick="closeAdmin()" class="bg-red-500 text-white px-8 py-3 rounded-xl text-[10px] font-black">EXIT</button>
                </div>
            </div>
            
            <div id="authBox" class="text-center py-32">
                <input type="password" id="pin" class="input-pro max-w-[300px] text-center text-3xl mb-6 shadow-xl" placeholder="••••">
                <br><button onclick="unlock()" class="btn-elite max-w-[300px]">Access Node</button>
            </div>
            
            <div id="hubData" class="hidden">
                <div class="grid md:grid-cols-4 gap-6 mb-12">
                    <div class="bg-slate-900 text-white p-6 rounded-3xl">
                        <p class="text-[9px] font-black uppercase opacity-50">Total Leads</p>
                        <h2 id="statTotal" class="text-4xl font-black italic">0</h2>
                    </div>
                    <div class="bg-blue-600 text-white p-6 rounded-3xl col-span-2">
                        <p class="text-[9px] font-black uppercase opacity-50">Portfolio Distribution</p>
                        <canvas id="leadsChart" height="80"></canvas>
                    </div>
                </div>

                <div class="grid lg:grid-cols-3 gap-12">
                    <div class="lg:col-span-2 space-y-6" id="adminLeads"></div>
                    <div id="adminChats" class="space-y-4"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const cid = "SIG-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        // FORM STEPS
        function nextStep(s) {
            document.querySelectorAll('.form-step').forEach(step => step.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
            for(let i=1; i<=3; i++) document.getElementById('dot'+i).className = (i<=s) ? 'h-2 flex-1 bg-blue-600 rounded-full' : 'h-2 flex-1 bg-slate-100 rounded-full';
        }

        // CHAT & FORM SYNC
        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + cid).push({ text: txt, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + cid).on('value', snap => {
            let h = `<div class="bubble bubble-admin">U.S. Enterprise Support Online. Agent-786 ready.</div>`;
            snap.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        document.getElementById('v3Form').onsubmit = (e) => {
            e.preventDefault();
            const tid = "US-ELITE-" + Math.floor(100000 + Math.random() * 900000);
            const data = {
                tid: tid, name: document.getElementById('vName').value, phone: document.getElementById('vPhone').value,
                svc: document.getElementById('vSvc').value, credit: document.getElementById('vCredit').value,
                addr: document.getElementById('vAddr').value, appt: document.getElementById('vDate').value + " | " + document.getElementById('vTime').value,
                ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('v3Form').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('displayTid').innerText = tid;
            });
        };

        // ADMIN ELITE LOGIC
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5) { document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { 
            document.getElementById('authBox').classList.add('hidden'); 
            document.getElementById('hubData').classList.remove('hidden'); 
            document.getElementById('adminControls').classList.remove('hidden');
            syncAdmin(); 
        } }

        let leadChart;
        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                let h = '', total = 0, counts = { Windows:0, Roofing:0, Solar:0, Garage:0 };
                snap.forEach(l => {
                    const v = l.val(); const k = l.key; total++;
                    if(counts[v.svc] !== undefined) counts[v.svc]++;
                    h += `<div class="p-6 bg-slate-50 rounded-[30px] border-2 border-transparent hover:border-blue-500 transition">
                        <div class="flex justify-between mb-4"><span class="bg-slate-900 text-white px-3 py-1 rounded-full text-[8px] font-black uppercase">${v.tid}</span> <button onclick="del('leads/${k}')" class="text-red-500 font-black text-[9px] uppercase">Erase</button></div>
                        <h4 class="text-lg font-black italic uppercase">${v.name}</h4>
                        <div class="grid grid-cols-2 gap-4 mt-4 text-[10px] font-bold text-slate-500 uppercase">
                            <p>📞 ${v.phone}</p><p>🛠 ${v.svc}</p><p>💳 Credit: ${v.credit}</p><p>📍 ${v.addr}</p>
                        </div>
                    </div>`;
                });
                document.getElementById('adminLeads').innerHTML = h || 'Terminal Clear.';
                document.getElementById('statTotal').innerText = total;
                updateChart(counts);
            });
        }

        function updateChart(counts) {
            const ctx = document.getElementById('leadsChart').getContext('2d');
            if(leadChart) leadChart.destroy();
            leadChart = new Chart(ctx, {
                type: 'bar',
                data: { labels: Object.keys(counts), datasets: [{ data: Object.values(counts), backgroundColor: '#ffffff' }] },
                options: { plugins: { legend: { display: false } }, scales: { y: { display: false }, x: { ticks: { color: '#ffffff', font: { weight: 'bold', size: 8 } } } } }
            });
        }

        function del(p) { if(confirm('Erase permanently?')) db.ref(p).remove(); }
        function exportToExcel() {
            db.ref('leads').once('value', snap => {
                const data = Object.values(snap.val() || {});
                const ws = XLSX.utils.json_to_sheet(data);
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "Leads");
                XLSX.writeFile(wb, "US_Home_Leads_Master.xlsx");
            });
        }
    </script>
</body>
</html>
