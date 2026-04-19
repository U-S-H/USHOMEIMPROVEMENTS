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
        :root { --tesla-blue: #2563eb; --slate-900: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; }
        
        /* Tesla Style Hero */
        .hero-premium { 
            background: linear-gradient(rgba(15, 23, 42, 0.8), rgba(15, 23, 42, 0.7)), 
            url('https://images.unsplash.com/photo-1513694203232-719a280e022f?auto=format&fit=crop&w=1600&q=80') center/cover; 
            min-height: 90vh; display: flex; align-items: center; justify-content: center; text-align: center;
        }

        .glass-card { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(20px); border-radius: 40px; border: 1px solid rgba(0,0,0,0.05); transition: 0.4s; }
        .glass-card:hover { transform: translateY(-10px); box-shadow: 0 40px 80px -20px rgba(0,0,0,0.1); }
        
        .btn-tesla { background: var(--tesla-blue); color: white; padding: 22px 40px; border-radius: 100px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; transition: 0.4s; border: none; cursor: pointer; }
        .btn-tesla:hover { background: #1d4ed8; transform: scale(1.05); }

        .page-section { display: none; }
        .page-section.active { display: block; animation: teslaFade 0.8s ease; }
        @keyframes teslaFade { from { opacity: 0; } to { opacity: 1; } }

        #chat-window { position: fixed; bottom: 100px; right: 25px; width: 350px; height: 500px; background: white; border-radius: 30px; box-shadow: 0 30px 60px rgba(0,0,0,0.2); display: none; flex-direction: column; overflow: hidden; z-index: 9999; }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-[5000] bg-white/80 backdrop-blur-md px-8 py-5 flex justify-between items-center border-b">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-10 w-10 bg-black rounded-lg flex items-center justify-center text-white font-bold">US</div>
            <div>
                <h1 class="text-xs font-black uppercase tracking-tighter">U.S. Home Improvement</h1>
                <p class="text-[8px] text-blue-600 font-bold uppercase">Authorized Enterprise</p>
            </div>
        </div>
        <div class="hidden md:flex gap-8">
            <button onclick="showPage('home')" class="text-[10px] font-black uppercase tracking-widest text-slate-400">Home</button>
            <button onclick="showPage('estimator')" class="text-[10px] font-black uppercase tracking-widest text-slate-400">Estimator</button>
            <button onclick="showPage('form')" class="btn-tesla py-2 px-6 text-[10px]">Get Quote</button>
        </div>
    </nav>

    <section id="home" class="page-section active">
        <div class="hero-premium px-6">
            <div class="max-w-4xl">
                <h1 class="text-6xl md:text-8xl font-black text-white uppercase italic leading-none mb-10">Future of<br><span class="text-blue-500">Living</span></h1>
                <div class="flex flex-col md:flex-row gap-6 justify-center">
                    <button onclick="showPage('form')" class="btn-tesla">Schedule Installation</button>
                    <button onclick="showPage('estimator')" class="bg-white/10 text-white border border-white/20 px-10 py-5 rounded-full font-bold uppercase text-xs backdrop-blur-md">Price Estimator</button>
                </div>
            </div>
        </div>

        <div class="py-24 px-8 max-w-7xl mx-auto grid md:grid-cols-3 gap-10">
            <div class="glass-card p-12 text-center">
                <div class="text-5xl mb-6">🏘️</div>
                <h3 class="text-xl font-black uppercase italic mb-4">Elite Windows</h3>
                <p class="text-sm text-slate-500 font-medium leading-relaxed mb-6">Tesla-grade energy glass for maximum efficiency.</p>
                <button onclick="showPage('form')" class="text-blue-600 font-black text-[10px] uppercase underline">Learn More</button>
            </div>
            <div class="glass-card p-12 text-center">
                <div class="text-5xl mb-6">⚡</div>
                <h3 class="text-xl font-black uppercase italic mb-4">Solar Matrix</h3>
                <p class="text-sm text-slate-500 font-medium leading-relaxed mb-6">High-density solar panels for zero energy costs.</p>
                <button onclick="showPage('form')" class="text-blue-600 font-black text-[10px] uppercase underline">Configure</button>
            </div>
            <div class="glass-card p-12 text-center">
                <div class="text-5xl mb-6">🏗️</div>
                <h3 class="text-xl font-black uppercase italic mb-4">Roofing Hub</h3>
                <p class="text-sm text-slate-500 font-medium leading-relaxed mb-6">Industrial strength roofing built for a lifetime.</p>
                <button onclick="showPage('form')" class="text-blue-600 font-black text-[10px] uppercase underline">Get Quote</button>
            </div>
        </div>
    </section>

    <section id="estimator" class="page-section py-24 px-8 bg-slate-50">
        <div class="max-w-3xl mx-auto glass-card p-12 md:p-20 text-center">
            <h2 class="text-4xl font-black uppercase italic mb-10">Instant <span class="text-blue-600">Estimator</span></h2>
            <div class="grid gap-6 text-left">
                <label class="text-[10px] font-black uppercase text-slate-400">Choose Service</label>
                <select id="calcSvc" class="w-full p-5 bg-white border rounded-2xl font-bold">
                    <option value="6000">Windows Replacement</option>
                    <option value="18000">Premium Roofing</option>
                    <option value="28000">Solar Power Matrix</option>
                </select>
                <label class="text-[10px] font-black uppercase text-slate-400">Property Area (Sq.Ft)</label>
                <input type="number" id="calcSq" placeholder="e.g. 2500" class="w-full p-5 bg-white border rounded-2xl font-bold">
                <button onclick="doTeslaCalc()" class="btn-tesla mt-6">Generate Estimate</button>
            </div>
            <div id="resBox" class="hidden mt-12 p-10 bg-slate-900 text-white rounded-[40px] text-center">
                <p class="text-[10px] font-black uppercase text-blue-400 mb-2">Projected Investment</p>
                <h3 id="resAmt" class="text-5xl font-black italic">$0</h3>
                <p class="text-[8px] mt-6 opacity-40 uppercase">Based on local U.S. labor and material averages.</p>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-24 px-8">
        <div class="max-w-xl mx-auto glass-card p-12 relative overflow-hidden">
            <div id="bar" class="absolute top-0 left-0 h-1 bg-blue-600 transition-all duration-700" style="width: 33%"></div>
            <form id="v3Form">
                <div class="form-step active" id="step1">
                    <h2 class="text-2xl font-black uppercase italic mb-10">Step 1: Solution</h2>
                    <select id="vSvc" class="w-full p-5 bg-slate-50 border rounded-2xl font-bold mb-8">
                        <option value="Windows">Windows</option>
                        <option value="Solar">Solar</option>
                        <option value="Roofing">Roofing</option>
                    </select>
                    <button type="button" onclick="next(2)" class="btn-tesla w-full">Continue</button>
                </div>
                <div class="form-step" id="step2">
                    <h2 class="text-2xl font-black uppercase italic mb-10">Step 2: Property</h2>
                    <input type="text" id="vAddr" placeholder="Street Address" class="w-full p-5 bg-slate-50 border rounded-2xl font-bold mb-4">
                    <select id="vCredit" class="w-full p-5 bg-slate-50 border rounded-2xl font-bold mb-8">
                        <option value="720+">Excellent (720+)</option>
                        <option value="660-719">Good (660-719)</option>
                        <option value="Below 660">Standard</option>
                    </select>
                    <div class="flex gap-4">
                        <button type="button" onclick="next(1)" class="w-1/3 font-bold text-slate-400">Back</button>
                        <button type="button" onclick="next(3)" class="btn-tesla flex-1">Final Step</button>
                    </div>
                </div>
                <div class="form-step" id="step3">
                    <h2 class="text-2xl font-black uppercase italic mb-10">Step 3: Contact</h2>
                    <input type="text" id="vName" placeholder="Full Name" class="w-full p-5 bg-slate-50 border rounded-2xl font-bold mb-4">
                    <input type="tel" id="vPhone" placeholder="Mobile Number" class="w-full p-5 bg-slate-50 border rounded-2xl font-bold mb-8">
                    <button type="submit" class="btn-tesla w-full">Get Free Consultation</button>
                </div>
            </form>
            <div id="vReceipt" class="hidden text-center py-10">
                <div class="text-5xl mb-6">✅</div>
                <h3 class="text-3xl font-black uppercase italic">Project Logged</h3>
                <p class="text-[10px] text-slate-400 mt-4 uppercase font-bold tracking-widest">Tracking ID: <span id="tid" class="text-blue-600"></span></p>
                <button onclick="location.reload()" class="mt-12 text-[10px] font-black uppercase underline">New Request</button>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b pb-8">
                <h3 class="text-2xl font-black uppercase italic">Command <span class="text-blue-600">Center</span></h3>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-8 py-2 rounded-full text-[10px] font-black uppercase">Exit Terminal</button>
            </div>
            
            <div id="authBox" class="text-center py-24">
                <input type="password" id="pin" class="p-6 bg-slate-50 border-2 rounded-3xl text-4xl text-center mb-8 max-w-xs shadow-xl" placeholder="••••">
                <br><button onclick="unlock()" class="btn-tesla">Decrypt Terminal</button>
            </div>

            <div id="hubData" class="hidden">
                <div class="grid md:grid-cols-4 gap-8 mb-16">
                    <div class="bg-black text-white p-12 rounded-[50px] text-center">
                        <p class="text-[10px] font-black uppercase opacity-40 mb-2">Total Queue</p>
                        <h2 id="total" class="text-7xl font-black italic">0</h2>
                    </div>
                    <div class="bg-white border p-12 rounded-[50px] col-span-3">
                        <canvas id="teslaChart" height="100"></canvas>
                    </div>
                </div>
                <div id="adminLeads" class="grid md:grid-cols-3 gap-8"></div>
            </div>
        </div>
    </div>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="bg-black p-5 text-white flex justify-between items-center">
                <span class="text-[10px] font-black uppercase tracking-widest">Live Dispatch</span>
                <button onclick="toggleChat()" class="opacity-40 text-xs">✕</button>
            </div>
            <div id="chat-feed" class="flex-1 p-5 overflow-y-auto bg-slate-50 flex flex-col gap-3"></div>
            <div class="p-5 bg-white border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="Ask a specialist..." class="flex-1 text-xs font-bold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-[10px]">SEND</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-blue-600 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[8000] hover:scale-110 transition">💬</button>
    </div>

    <script>
        // MASTER FIREBASE CONFIG
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
        const sessionID = "ENTERPRISE-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo(0,0); }
        function toggleChat() { const w = document.getElementById('chat-window'); w.style.display = (w.style.display === 'flex') ? 'none' : 'flex'; }
        function next(s) { 
            document.querySelectorAll('.form-step').forEach(st => st.classList.remove('active')); 
            document.getElementById('step' + s).classList.add('active'); 
            document.getElementById('bar').style.width = (s * 33.3) + "%";
        }

        // TESLA CALCULATOR LOGIC
        function doTeslaCalc() {
            const base = parseInt(document.getElementById('calcSvc').value);
            const sq = parseInt(document.getElementById('calcSq').value) || 0;
            const estimate = base + (sq * 7);
            document.getElementById('resAmt').innerText = `$${estimate.toLocaleString()}`;
            document.getElementById('resBox').classList.remove('hidden');
        }

        // LEAD TRANSMISSION
        document.getElementById('v3Form').onsubmit = (e) => {
            e.preventDefault();
            const tid = "DIS-" + Math.floor(10000 + Math.random() * 90000);
            const data = { tid, name:document.getElementById('vName').value, phone:document.getElementById('vPhone').value, svc:document.getElementById('vSvc').value, addr:document.getElementById('vAddr').value, ts:new Date().toLocaleString() };
            db.ref('leads').push(data).then(() => {
                document.getElementById('v3Form').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('tid').innerText = tid;
            });
        };

        // CHAT LOGIC
        function sendMsg() {
            const t = document.getElementById('chat-input').value; if(!t) return;
            db.ref('chats/' + sessionID).push({ text: t, type: 'user', ts: Date.now() });
            document.getElementById('chat-input').value = '';
        }
        db.ref('chats/' + sessionID).on('value', snap => {
            let h = `<div class="p-4 bg-white border self-start rounded-2xl rounded-bl-none text-[11px] font-bold">Secure terminal active. How can we help you?</div>`;
            snap.forEach(m => { const v = m.val(); h += `<div class="p-4 ${v.type==='user'?'bg-blue-600 text-white self-end rounded-br-none':'bg-white border text-slate-900 self-start rounded-bl-none'} rounded-2xl text-[11px] font-bold max-w-[80%]">${v.text}</div>`; });
            const f = document.getElementById('chat-feed'); f.innerHTML = h; f.scrollTop = f.scrollHeight;
        });

        // ADMIN TERMINAL
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5) { document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncLeads(); } }

        let myChart;
        function syncLeads() {
            db.ref('leads').on('value', snap => {
                let h = '', total = 0, counts = { Windows:0, Solar:0, Roofing:0 };
                snap.forEach(l => {
                    const v = l.val(); const k = l.key; total++;
                    if(counts[v.svc] !== undefined) counts[v.svc]++;
                    h += `<div class="p-8 glass-card border-none bg-slate-50">
                        <div class="flex justify-between items-center mb-6"><span class="bg-black text-white px-3 py-1 rounded-full text-[8px] font-black">${v.tid}</span> <button onclick="db.ref('leads/${k}').remove()" class="text-red-500 font-bold text-[8px]">ERASE</button></div>
                        <h4 class="font-black italic text-xl uppercase mb-4">${v.name}</h4>
                        <div class="space-y-3 text-[10px] font-bold text-slate-500 uppercase">
                            <p>📞 ${v.phone}</p><p>🛠 ${v.svc}</p><p>📍 ${v.addr}</p>
                        </div>
                    </div>`;
                });
                document.getElementById('adminLeads').innerHTML = h || 'Empty.';
                document.getElementById('total').innerText = total;
                updateTeslaChart(counts);
            });
        }

        function updateTeslaChart(c) {
            const ctx = document.getElementById('teslaChart').getContext('2d');
            if(myChart) myChart.destroy();
            myChart = new Chart(ctx, { type:'bar', data: { labels:Object.keys(c), datasets:[{data:Object.values(c), backgroundColor:'#2563eb', borderRadius: 20}] }, options: { plugins:{legend:{display:false}}, scales:{y:{display:false}, x:{ticks:{font:{weight:'bold', size:9}}}} } });
        }
    </script>
</body>
</html>
