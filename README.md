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
        :root { --primary: #0f172a; --accent: #2563eb; --success: #10b981; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; scroll-behavior: smooth; }
        
        .hero-v3 { background: linear-gradient(rgba(15, 23, 42, 0.92), rgba(15, 23, 42, 0.85)), url('https://images.unsplash.com/photo-1581094794329-c8112a89af12?auto=format&fit=crop&w=1600&q=80') center/cover no-repeat fixed; }
        .glass-blur { background: rgba(255, 255, 255, 0.85); backdrop-filter: blur(20px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; outline: none; transition: 0.4s; font-size: 14px; background: #fff; }
        .input-pro:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px 32px; border-radius: 16px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; border: none; transition: 0.4s; box-shadow: 0 12px 24px rgba(37, 99, 235, 0.25); width: 100%; }
        .btn-elite:hover { transform: translateY(-4px); box-shadow: 0 18px 36px rgba(37, 99, 235, 0.35); }

        .page-section { display: none; }
        .page-section.active { display: block; animation: contentFade 0.7s ease-out; }
        @keyframes contentFade { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 30px; box-shadow: 0 30px 60px -12px rgba(0,0,0,0.25); display: none; flex-direction: column; z-index: 6000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 22px; color: white; display: flex; align-items: center; gap: 12px; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); }
    </style>
</head>
<body>

    <nav class="glass-blur sticky top-0 z-[5000] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-10 w-10 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer shadow-lg">US</div>
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase leading-none tracking-tight">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic">Enterprise National Hub</span>
            </div>
        </div>
        <div class="hidden lg:flex gap-8 text-[10px] font-black uppercase">
            <button onclick="showPage('home')" class="text-slate-400 hover:text-blue-600">Home</button>
            <button onclick="showPage('estimate')" class="text-slate-400 hover:text-blue-600">Price Estimator</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-2 rounded-full">Get Quote</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="w-3 h-3 bg-emerald-500 rounded-full"></div>
                <h4 class="font-black uppercase text-[11px]">Senior Dispatch Support</h4>
                <button onclick="toggleChat()" class="ml-auto text-xl">✕</button>
            </div>
            <div id="chat-feed">
                <div class="bubble bubble-admin">Agent-786 is online. How can I help with your survey?</div>
            </div>
            <div class="p-5 border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="Type..." class="w-full text-xs outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs">SEND</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[5500]">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-v3 py-48 px-6 text-center text-white">
            <h1 class="text-6xl md:text-9xl font-black uppercase italic leading-[0.8] mb-12 tracking-tighter">Premium <br><span class="text-blue-500">Upgrades</span></h1>
            <p class="max-w-xl mx-auto text-blue-100 font-bold text-xs uppercase tracking-widest mb-16">Certified Inspections & National Logistics Hub.</p>
            <div class="flex flex-col md:flex-row gap-4 justify-center">
                <button onclick="showPage('form')" class="btn-elite max-w-[300px]">Start Survey</button>
                <button onclick="showPage('estimate')" class="bg-white/10 backdrop-blur px-8 py-4 rounded-2xl font-black uppercase text-[12px] border border-white/20">Price Calculator</button>
            </div>
        </header>

        <div class="py-24 px-8 max-w-7xl mx-auto grid md:grid-cols-3 gap-8 text-center">
            <div class="p-10 bg-white border rounded-[40px] shadow-xl">
                <div class="text-4xl mb-4">🪟</div>
                <h3 class="font-black uppercase italic mb-2">Windows</h3>
                <p class="text-[10px] text-slate-400 font-bold uppercase">Energy Efficient Replacement</p>
            </div>
            <div class="p-10 bg-white border rounded-[40px] shadow-xl">
                <div class="text-4xl mb-4">☀️</div>
                <h3 class="font-black uppercase italic mb-2">Solar</h3>
                <p class="text-[10px] text-slate-400 font-bold uppercase">Power Matrix Systems</p>
            </div>
            <div class="p-10 bg-white border rounded-[40px] shadow-xl">
                <div class="text-4xl mb-4">🏗️</div>
                <h3 class="font-black uppercase italic mb-2">Roofing</h3>
                <p class="text-[10px] text-slate-400 font-bold uppercase">Elite Installation</p>
            </div>
        </div>
    </section>

    <section id="estimate" class="page-section py-24 px-8">
        <div class="max-w-2xl mx-auto bg-white border p-12 rounded-[50px] shadow-2xl text-center">
            <h2 class="text-3xl font-black uppercase italic mb-8">Instant <span class="text-blue-600">Estimator</span></h2>
            <div class="space-y-6">
                <select id="calcSvc" class="input-pro">
                    <option value="6000">Window Replacement (Avg)</option>
                    <option value="15000">Premium Roofing (Avg)</option>
                    <option value="25000">Solar Power System (Avg)</option>
                </select>
                <input type="number" id="calcSqft" placeholder="Approx Square Footage" class="input-pro">
                <button onclick="calculateCost()" class="btn-elite">Calculate Range</button>
                <div id="calcResult" class="hidden mt-10 p-8 bg-blue-50 rounded-3xl border-2 border-blue-100">
                    <p class="text-[10px] font-black uppercase text-blue-600 mb-2">Projected Investment</p>
                    <h3 id="rangeText" class="text-4xl font-black italic text-slate-900">$0 - $0</h3>
                    <p class="text-[8px] mt-4 text-slate-400 font-black uppercase">*Subject to final inspection</p>
                </div>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-20 bg-white">
        <div class="max-w-3xl mx-auto px-6">
            <div class="bg-white p-12 rounded-[48px] shadow-2xl border border-slate-50 relative overflow-hidden">
                <form id="v3Form">
                    <h3 class="text-2xl font-black uppercase italic text-slate-900 mb-10">Site Authorization Terminal</h3>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro" required>
                        <input type="tel" id="vPhone" placeholder="Primary Phone" class="input-pro" required>
                    </div>
                    <select id="vSvc" class="input-pro mb-6" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                    </select>
                    <input type="text" id="vAddr" placeholder="Physical Site Address" class="input-pro mb-10" required>
                    <button type="submit" class="btn-elite">Authorize & Transmit</button>
                </form>

                <div id="vReceipt" class="hidden text-center py-10">
                    <div class="text-6xl mb-8">🎖️</div>
                    <h3 class="text-3xl font-black uppercase italic text-slate-900">Success</h3>
                    <div class="bg-slate-950 text-white p-10 rounded-[35px] my-10 text-left border-4 border-blue-600 shadow-2xl">
                        <p class="text-[10px] font-black text-blue-400 uppercase mb-4 tracking-widest text-center">Official Document</p>
                        <p class="text-[11px] font-bold uppercase mb-2">ID: <span id="rTid" class="text-emerald-400"></span></p>
                        <p class="text-[11px] font-bold uppercase">Name: <span id="rName"></span></p>
                    </div>
                    <button onclick="location.reload()" class="text-blue-600 font-black text-[10px] uppercase underline">Return</button>
                </div>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b pb-8">
                <h3 class="text-3xl font-black uppercase italic">Master <span class="text-blue-600">Terminal</span></h3>
                <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-6 py-2 rounded-full font-black text-[10px] uppercase">Exit</button>
            </div>
            
            <div id="authBox" class="text-center py-32">
                <input type="password" id="pin" class="input-pro max-w-[300px] text-center text-3xl mb-6 shadow-xl" placeholder="••••">
                <br><button onclick="unlock()" class="btn-elite max-w-[300px]">Authorize</button>
            </div>
            
            <div id="hubData" class="hidden">
                <div class="grid md:grid-cols-4 gap-8 mb-12">
                    <div class="bg-slate-900 text-white p-10 rounded-[40px] text-center">
                        <p class="text-[10px] font-black opacity-50 mb-2 uppercase">Total Leads</p>
                        <h2 id="totalLeads" class="text-6xl font-black italic">0</h2>
                    </div>
                    <div class="md:col-span-3 bg-white border p-10 rounded-[40px]">
                        <canvas id="leadsChart" height="100"></canvas>
                    </div>
                </div>
                <div id="adminLeads" class="grid lg:grid-cols-2 gap-6"></div>
            </div>
        </div>
    </div>

    <script>
        const firebaseConfig = {
            apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA",
            authDomain: "ushomes07.firebaseapp.com",
            databaseURL: "https://ushomes07-default-rtdb.firebaseio.com",
            projectId: "ushomes07",
            storageBucket: "ushomes07.firebasestorage.app",
            messagingSenderId: "24299478735",
            appId: "1:24299478735:web:5ec1ac023ef15e186521ba"
        };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const userId = "SIG-" + Math.floor(100000 + Math.random() * 899999);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo(0,0); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        // ESTIMATOR LOGIC
        function calculateCost() {
            const base = parseInt(document.getElementById('calcSvc').value);
            const sqft = parseInt(document.getElementById('calcSqft').value) || 0;
            const min = base + (sqft * 5);
            const max = base + (sqft * 12);
            document.getElementById('rangeText').innerText = `$${min.toLocaleString()} - $${max.toLocaleString()}`;
            document.getElementById('calcResult').classList.remove('hidden');
        }

        // SUBMISSION
        document.getElementById('v3Form').onsubmit = (e) => {
            e.preventDefault();
            const tid = "US-DISPATCH-" + Math.floor(100000 + Math.random() * 900000);
            const data = { tid, name: document.getElementById('vName').value, phone: document.getElementById('vPhone').value, svc: document.getElementById('vSvc').value, addr: document.getElementById('vAddr').value, ts: new Date().toLocaleString() };
            db.ref('leads').push(data).then(() => {
                document.getElementById('v3Form').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('rTid').innerText = tid;
                document.getElementById('rName').innerText = data.name;
            });
        };

        // ADMIN HUB
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } setTimeout(()=>taps=0,2000); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        let leadsChart;
        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                let h = '', total = 0, counts = { Windows: 0, Solar: 0, Roofing: 0 };
                snap.forEach(l => {
                    const v = l.val(); total++;
                    if(counts[v.svc] !== undefined) counts[v.svc]++;
                    h += `<div class="p-8 bg-slate-50 border rounded-[35px]">
                        <p class="text-[8px] font-black uppercase text-blue-600 mb-2">${v.tid}</p>
                        <h4 class="text-xl font-black italic mb-4">${v.name}</h4>
                        <div class="text-[10px] font-bold text-slate-400 space-y-1">
                            <p>📞 ${v.phone}</p><p>🛠 ${v.svc}</p><p>📍 ${v.addr}</p>
                        </div>
                    </div>`;
                });
                document.getElementById('adminLeads').innerHTML = h;
                document.getElementById('totalLeads').innerText = total;
                updateChart(counts);
            });
        }

        function updateChart(c) {
            const ctx = document.getElementById('leadsChart').getContext('2d');
            if(leadsChart) leadsChart.destroy();
            leadsChart = new Chart(ctx, { type: 'bar', data: { labels: Object.keys(c), datasets: [{ data: Object.values(c), backgroundColor: '#2563eb', borderRadius: 10 }] }, options: { plugins: { legend: { display: false } }, scales: { y: { display: false } } } });
        }
    </script>
</body>
</html>
