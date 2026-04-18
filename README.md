<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Enterprise Matrix</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --slate: #1e293b; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f1f5f9; color: var(--slate); overflow-x: hidden; }
        
        .glass-ui { 
            background: rgba(255, 255, 255, 0.85); 
            backdrop-filter: blur(20px); 
            border: 1px solid white; 
            border-radius: 2.5rem; 
            box-shadow: 0 30px 60px -12px rgba(0, 0, 0, 0.05); 
        }

        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.5s cubic-bezier(0.19, 1, 0.22, 1) forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .btn-choice { 
            width: 100%; padding: 1.25rem; background: white; border: 2px solid #f1f5f9; border-radius: 1.5rem; 
            text-align: left; font-weight: 700; transition: 0.3s; display: flex; justify-content: space-between; 
        }
        .btn-choice:hover { border-color: var(--neon); transform: scale(1.02); box-shadow: 0 10px 20px rgba(0, 242, 255, 0.1); }

        .img-container { width: 100%; height: 220px; border-radius: 1.5rem; overflow: hidden; background: #e2e8f0; }
        .img-container img { width: 100%; height: 100%; object-fit: cover; }
        
        input, select { 
            width: 100%; padding: 1.1rem; border-radius: 1.1rem; border: 2px solid #f1f5f9; 
            font-weight: 600; outline: none; transition: 0.3s; 
        }
        input:focus { border-color: var(--neon); }
    </style>
</head>
<body class="p-4 md:p-8">

    <nav class="max-w-6xl mx-auto flex justify-between items-center mb-10">
        <div>
            <h1 class="text-2xl font-black italic tracking-tighter leading-none">U.S. HOME IMPROVEMENTS</h1>
            <p class="text-[9px] text-cyan-600 font-bold uppercase tracking-[0.4em] mt-1">National Contractor Network</p>
        </div>
        <div class="hidden md:flex gap-4 items-center">
            <span class="text-[10px] font-black uppercase text-slate-400">Status: Active in All States</span>
            <div class="h-4 w-[1px] bg-slate-200"></div>
            <img src="https://upload.wikimedia.org/wikipedia/commons/0/07/Better_Business_Bureau_logo.svg" class="h-4 opacity-50">
        </div>
    </nav>

    <main class="max-w-2xl mx-auto mb-20">
        <div class="glass-ui p-8 md:p-12 border-t-8 border-slate-900">
            <form id="matrixForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">01. Choose Service</h2>
                    <div class="space-y-3">
                        <button type="button" onclick="next(2, 'service', 'Replacement Windows')" class="btn-choice"><span>🪟 Replacement Windows</span> <span>→</span></button>
                        <button type="button" onclick="next(2, 'service', 'Security Entry Doors')" class="btn-choice"><span>🚪 Professional Entry Doors</span> <span>→</span></button>
                        <button type="button" onclick="next(2, 'service', 'Elite Roofing')" class="btn-choice"><span>🏠 Architectural Roofing</span> <span>→</span></button>
                        <button type="button" onclick="next(2, 'service', 'Solar Systems')" class="btn-choice"><span>☀️ Solar Generation Matrix</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">02. Region & Language</h2>
                    <div class="space-y-4">
                        <select id="userState" required>
                            <option value="">Select Your State (All 50 Available)</option>
                            <option value="CA">California</option><option value="TX">Texas</option><option value="FL">Florida</option><option value="NY">New York</option><option value="Other">Other U.S. State</option>
                        </select>
                        <select id="userLang">
                            <option value="English">Preferred Language: English</option>
                            <option value="Spanish">Preferred Language: Español</option>
                        </select>
                        <button type="button" onclick="showStep('step3')" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase tracking-widest mt-4">Confirm Location</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">03. Schedule Visit</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <input type="date" id="appDate" required>
                        <select id="appTime">
                            <option>Morning (8AM-12PM)</option>
                            <option>Afternoon (12PM-4PM)</option>
                            <option>Evening (4PM-7PM)</option>
                        </select>
                    </div>
                    <button type="button" onclick="showStep('step4')" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase tracking-widest mt-6">Set Appointment</button>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">04. Final Protocol</h2>
                    <div class="space-y-4">
                        <input type="text" id="userName" placeholder="Full Legal Name" required>
                        <input type="tel" id="userPhone" placeholder="Mobile Number" required>
                        <input type="text" id="userAddr" placeholder="Street Address" required>
                        <button type="submit" class="w-full bg-cyan-500 text-slate-900 p-6 rounded-3xl font-black uppercase text-lg shadow-xl shadow-cyan-200 mt-4">Submit Application</button>
                    </div>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-6xl mx-auto grid md:grid-cols-4 gap-6 mb-20">
        <div class="glass-ui p-6">
            <div class="img-container mb-4"><img src="https://images.unsplash.com/photo-1509644851169-2acc08aa25b5?w=500"></div>
            <h3 class="font-black italic uppercase text-sm">Windows</h3>
            <p class="text-[9px] font-bold text-slate-400 mt-2 uppercase tracking-widest leading-relaxed">Impact rated architectural glass systems.</p>
        </div>
        <div class="glass-ui p-6">
            <div class="img-container mb-4"><img src="https://images.unsplash.com/photo-1517581177682-a085bb7ffb15?w=500"></div>
            <h3 class="font-black italic uppercase text-sm">Entry Doors</h3>
            <p class="text-[9px] font-bold text-slate-400 mt-2 uppercase tracking-widest leading-relaxed">High-security reinforced fiberglass & steel.</p>
        </div>
        <div class="glass-ui p-6">
            <div class="img-container mb-4"><img src="https://images.unsplash.com/photo-1632759162353-19c9a543fe79?w=500"></div>
            <h3 class="font-black italic uppercase text-sm">Roofing</h3>
            <p class="text-[9px] font-bold text-slate-400 mt-2 uppercase tracking-widest leading-relaxed">Lifetime shingles with wind-seal technology.</p>
        </div>
        <div class="glass-ui p-6">
            <div class="img-container mb-4"><img src="https://images.unsplash.com/photo-1513694490325-24b3dc52a21c?w=500"></div>
            <h3 class="font-black italic uppercase text-sm">Solar</h3>
            <p class="text-[9px] font-bold text-slate-400 mt-2 uppercase tracking-widest leading-relaxed">Tier 1 Monocrystalline generation panels.</p>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 bg-slate-900/98 backdrop-blur-3xl z-[1000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-6xl mx-auto pt-10 pb-20">
            <div class="flex justify-between items-center mb-16 border-b border-white/10 pb-6">
                <h2 class="text-3xl font-black italic text-cyan-400">HQ DATA COMMAND</h2>
                <button onclick="location.reload()" class="bg-red-500/20 text-red-500 px-4 py-1 rounded text-[10px] font-bold">CLOSE</button>
            </div>
            <div id="loginBox" class="max-w-xs mx-auto text-center py-20">
                <input type="password" id="adminKey" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl mb-4 text-center text-4xl outline-none" placeholder="****">
                <button onclick="unlock()" class="w-full bg-cyan-600 text-slate-900 p-5 rounded-2xl font-black uppercase">Verify ID</button>
            </div>
            <div id="dashboard" class="hidden grid md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
        </div>
    </div>

    <script>
        // Firebase Config
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

        let lead = {};

        function showStep(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function next(s, k, v) {
            if(k) lead[k] = v;
            showStep('step' + s);
        }

        document.getElementById('matrixForm').addEventListener('submit', (e) => {
            e.preventDefault();
            lead.name = document.getElementById('userName').value;
            lead.phone = document.getElementById('userPhone').value;
            lead.address = document.getElementById('userAddr').value;
            lead.state = document.getElementById('userState').value;
            lead.lang = document.getElementById('userLang').value;
            lead.date = document.getElementById('appDate').value;
            lead.time = document.getElementById('appTime').value;
            lead.timestamp = new Date().toLocaleString();

            db.ref('leads').push(lead).then(() => {
                alert("APPLICATION AUTHORIZED! 🚀");
                location.reload();
            });
        });

        // Secret Admin (5 rapid taps)
        let t = 0, l = 0;
        document.addEventListener('click', () => {
            if(Date.now() - l < 400) t++; else t = 1; l = Date.now();
            if(t === 5) document.getElementById('adminPortal').classList.remove('hidden');
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('dashboard').classList.remove('hidden');
                sync();
            }
        }

        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val();
                let h = '';
                for(let id in data) {
                    h = `
                    <div class="bg-white/5 border-l-4 border-cyan-400 p-6 rounded-r-2xl">
                        <div class="flex justify-between items-start">
                            <div><h4 class="font-black italic uppercase">${data[id].name}</h4><p class="text-cyan-400 text-[9px] font-bold uppercase">${data[id].service}</p></div>
                            <span class="text-[9px] font-bold text-gray-500 uppercase">${data[id].state}</span>
                        </div>
                        <p class="text-xs text-gray-400 mt-4 font-medium italic">📞 ${data[id].phone} | 📅 Visit: ${data[id].date} (${data[id].time})</p>
                        <button onclick="db.ref('leads/${id}').remove()" class="text-[8px] mt-4 opacity-30 hover:opacity-100 uppercase font-bold">Delete Lead</button>
                    </div>` + h;
                }
                document.getElementById('dashboard').innerHTML = h || 'No leads yet.';
            });
        }
    </script>
</body>
</html>
