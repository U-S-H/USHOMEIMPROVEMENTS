<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; overflow-x: hidden; }
        .hero-v3 { background: linear-gradient(rgba(15,23,42,0.9), rgba(15,23,42,0.8)), url('https://images.unsplash.com/photo-1581094794329-c8112a89af12?auto=format&fit=crop&w=1600&q=80') center/cover; min-height: 80vh; display: flex; align-items: center; justify-content: center; }
        .card-pro { background: white; border-radius: 30px; border: 1px solid #f1f5f9; box-shadow: 0 20px 40px -15px rgba(0,0,0,0.05); transition: 0.3s; }
        .card-pro:hover { transform: translateY(-10px); box-shadow: 0 30px 60px -20px rgba(0,0,0,0.1); }
        .input-pro { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; }
        .input-pro:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37,99,235,0.1); }
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px 35px; border-radius: 20px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; box-shadow: 0 12px 24px rgba(37, 99, 235, 0.25); width: 100%; transition: 0.3s; }
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.6s ease; }
        .form-step { display: none; }
        .form-step.active { display: block; animation: slideIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-[5000] bg-white/90 backdrop-blur-xl px-6 py-4 flex justify-between items-center border-b">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-10 w-10 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer">US</div>
            <div>
                <h1 class="text-[12px] font-black text-slate-900 uppercase">U.S. Home Improvement</h1>
                <span class="text-[8px] font-bold text-blue-600 uppercase tracking-widest italic">Enterprise Grade</span>
            </div>
        </div>
        <div class="flex gap-6">
            <button onclick="showPage('home')" class="text-[10px] font-black uppercase text-slate-400">Home</button>
            <button onclick="showPage('gallery')" class="text-[10px] font-black uppercase text-slate-400">Projects</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-5 py-2 rounded-full text-[10px] font-black uppercase">Get Estimate</button>
        </div>
    </nav>

    <section id="home" class="page-section active">
        <div class="hero-v3 text-center px-6">
            <div class="max-w-4xl">
                <span class="bg-blue-600/20 text-blue-400 px-4 py-1 rounded-full text-[9px] font-black uppercase tracking-widest mb-6 inline-block">Authorized National Network</span>
                <h1 class="text-6xl md:text-9xl font-black text-white uppercase italic leading-none mb-10">Modern<br><span class="text-blue-500">Contracting</span></h1>
                <div class="flex flex-col md:flex-row gap-4 justify-center">
                    <button onclick="showPage('form')" class="btn-elite md:max-w-[300px]">Start Free Survey</button>
                    <button onclick="showPage('estimate')" class="bg-white/10 backdrop-blur text-white px-8 py-5 rounded-2xl font-black uppercase text-[12px] border border-white/20">Price Calculator</button>
                </div>
            </div>
        </div>
        
        <div class="py-24 px-6 max-w-7xl mx-auto grid md:grid-cols-3 gap-8">
            <div class="card-pro p-8 text-center">
                <div class="text-4xl mb-6">🪟</div>
                <h3 class="font-black uppercase mb-4">Windows</h3>
                <p class="text-xs text-slate-500 font-bold leading-loose italic">Energy efficient window replacement with lifetime warranty.</p>
            </div>
            <div class="card-pro p-8 text-center">
                <div class="text-4xl mb-6">☀️</div>
                <h3 class="font-black uppercase mb-4">Solar Power</h3>
                <p class="text-xs text-slate-500 font-bold leading-loose italic">Reduce bills to $0 with our premium solar array matrix.</p>
            </div>
            <div class="card-pro p-8 text-center">
                <div class="text-4xl mb-6">🏠</div>
                <h3 class="font-black uppercase mb-4">Roofing</h3>
                <p class="text-xs text-slate-500 font-bold leading-loose italic">Elite roofing systems designed to withstand any US weather.</p>
            </div>
        </div>
    </section>

    <section id="estimate" class="page-section py-20 px-6">
        <div class="max-w-3xl mx-auto card-pro p-10 md:p-16 text-center">
            <h2 class="text-3xl font-black uppercase italic mb-8">Instant <span class="text-blue-600">Price Estimator</span></h2>
            <div class="space-y-6">
                <select id="calcSvc" class="input-pro">
                    <option value="5000">Windows (Avg $5,000+)</option>
                    <option value="15000">Roofing (Avg $15,000+)</option>
                    <option value="25000">Solar System (Avg $25,000+)</option>
                </select>
                <input type="number" id="calcSqft" placeholder="Approx Square Footage" class="input-pro">
                <button onclick="calculateCost()" class="btn-elite">Calculate Range</button>
                <div id="calcResult" class="hidden mt-8 p-6 bg-blue-50 rounded-2xl border-2 border-blue-200">
                    <p class="text-[10px] font-black uppercase text-blue-600">Estimated Range</p>
                    <h3 id="rangeText" class="text-3xl font-black italic text-slate-900">$0 - $0</h3>
                    <p class="text-[8px] mt-4 text-slate-400 font-bold uppercase italic">*Final price depends on inspection and material quality.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-20 px-6">
        <div class="max-w-xl mx-auto card-pro p-10 md:p-16 relative overflow-hidden">
            <div class="absolute top-0 left-0 h-1 bg-blue-600 transition-all duration-500" id="progressBar" style="width: 33.3%"></div>
            <form id="v3Form">
                <div class="form-step active" id="step1">
                    <h2 class="text-2xl font-black uppercase italic mb-8">Service Selection</h2>
                    <select id="vSvc" class="input-pro mb-8" required>
                        <option value="Windows">Windows</option>
                        <option value="Solar">Solar</option>
                        <option value="Roofing">Roofing</option>
                    </select>
                    <button type="button" onclick="nextStep(2)" class="btn-elite">Next Step</button>
                </div>
                <div class="form-step" id="step2">
                    <h2 class="text-2xl font-black uppercase italic mb-8">Location Details</h2>
                    <input type="text" id="vAddr" placeholder="Property Address (Zip Included)" class="input-pro mb-4" required>
                    <select id="vCredit" class="input-pro mb-8" required>
                        <option value="720+">Excellent (720+)</option>
                        <option value="660-719">Good (660-719)</option>
                        <option value="Other">Other</option>
                    </select>
                    <button type="button" onclick="nextStep(3)" class="btn-elite">Authorize</button>
                </div>
                <div class="form-step" id="step3">
                    <h2 class="text-2xl font-black uppercase italic mb-8">Contact Info</h2>
                    <input type="text" id="vName" placeholder="Full Name" class="input-pro mb-4" required>
                    <input type="tel" id="vPhone" placeholder="Phone Number" class="input-pro mb-8" required>
                    <button type="submit" class="btn-elite">Submit Request</button>
                </div>
            </form>
            <div id="vReceipt" class="hidden text-center py-10">
                <h3 class="text-3xl font-black uppercase italic text-blue-600">Transmitted</h3>
                <p class="text-[10px] font-bold text-slate-400 mt-2">CASE ID: <span id="displayTid" class="text-slate-900 font-black"></span></p>
                <button onclick="location.reload()" class="mt-10 underline text-[10px] font-black">New Project</button>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-10">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center mb-10 border-b pb-8">
                <h3 class="text-2xl font-black uppercase italic">Master <span class="text-blue-600">Terminal</span></h3>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-6 py-2 rounded-xl text-[10px] font-black">EXIT</button>
            </div>
            <div id="authBox" class="text-center py-20">
                <input type="password" id="pin" class="input-pro max-w-[250px] text-center text-2xl mb-6" placeholder="••••">
                <br><button onclick="unlock()" class="btn-elite max-w-[250px]">Login</button>
            </div>
            <div id="hubData" class="hidden grid md:grid-cols-2 gap-6" id="adminLeads"></div>
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
            appId: "1:24299478735:web:14f41d56809beac56521ba"
        };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo(0,0); }
        function nextStep(s) { 
            document.querySelectorAll('.form-step').forEach(st => st.classList.remove('active')); 
            document.getElementById('step' + s).classList.add('active'); 
            document.getElementById('progressBar').style.width = (s * 33.3) + "%";
        }

        // PRICE CALCULATOR LOGIC
        function calculateCost() {
            const base = parseInt(document.getElementById('calcSvc').value);
            const sqft = parseInt(document.getElementById('calcSqft').value) || 0;
            const min = base + (sqft * 5);
            const max = base + (sqft * 12);
            document.getElementById('rangeText').innerText = `$${min.toLocaleString()} - $${max.toLocaleString()}`;
            document.getElementById('calcResult').classList.remove('hidden');
        }

        document.getElementById('v3Form').onsubmit = (e) => {
            e.preventDefault();
            const tid = "DIS-" + Math.floor(10000 + Math.random() * 90000);
            const data = { tid, name:document.getElementById('vName').value, phone:document.getElementById('vPhone').value, svc:document.getElementById('vSvc').value, addr:document.getElementById('vAddr').value, ts:new Date().toLocaleString() };
            db.ref('leads').push(data).then(() => {
                document.getElementById('v3Form').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('displayTid').innerText = tid;
            });
        };

        // ADMIN LOGIC
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5) { document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                let h = '';
                snap.forEach(l => {
                    const v = l.val();
                    h += `<div class="p-6 card-pro">
                        <p class="text-[10px] font-black text-blue-600 mb-2">${v.tid}</p>
                        <h4 class="font-black uppercase italic">${v.name}</h4>
                        <div class="text-[10px] font-bold text-slate-500 mt-4 space-y-1">
                            <p>📞 ${v.phone}</p><p>🛠 ${v.svc}</p><p>📍 ${v.addr}</p>
                        </div>
                    </div>`;
                });
                document.getElementById('hubData').innerHTML = h || 'No leads yet.';
            });
        }
    </script>
</body>
</html>
