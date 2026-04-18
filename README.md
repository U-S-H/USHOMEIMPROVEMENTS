<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Contractor Matrix</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --bg: #f8fafc; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; }
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(12px); border: 1px solid white; border-radius: 2rem; box-shadow: 0 20px 50px rgba(0,0,0,0.05); }
        .neon-border { border: 2px solid transparent; transition: 0.3s; }
        .neon-border:hover { border-color: var(--neon); box-shadow: 0 0 20px rgba(0, 242, 255, 0.2); }
        .step { display: none; }
        .step.active { display: block; animation: fadeIn 0.5s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .img-box { width: 100%; height: 200px; border-radius: 1.5rem; overflow: hidden; background: #e2e8f0; }
        .img-box img { width: 100%; height: 100%; object-fit: cover; }
    </style>
</head>
<body class="p-4 md:p-10">

    <div class="max-w-5xl mx-auto mb-6 flex justify-between items-center px-4">
        <div class="flex items-center gap-2">
            <span class="relative flex h-3 w-3"><span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span><span class="relative inline-flex rounded-full h-3 w-3 bg-green-500"></span></span>
            <span class="text-[10px] font-bold uppercase tracking-widest text-slate-500">Active in all 50 U.S. States</span>
        </div>
        <div class="text-[10px] font-bold text-blue-600 uppercase">Verified Contractor Network</div>
    </div>

    <header class="text-center mb-12">
        <h1 class="text-4xl font-black italic tracking-tighter">U.S. HOME IMPROVEMENTS</h1>
        <p class="text-[9px] font-bold text-cyan-500 uppercase tracking-[0.4em] mt-2">The National Home Modernization Matrix</p>
    </header>

    <main class="max-w-2xl mx-auto mb-20">
        <div class="glass p-8 md:p-12 neon-border">
            <form id="masterForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">01. Select Specific Upgrade</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <button type="button" onclick="next(2, 'service', 'Replacement Windows')" class="p-5 bg-white rounded-2xl border-2 border-slate-50 text-left font-bold hover:border-cyan-400 transition">🪟 Windows Only</button>
                        <button type="button" onclick="next(2, 'service', 'Entry Doors')" class="p-5 bg-white rounded-2xl border-2 border-slate-50 text-left font-bold hover:border-cyan-400 transition">🚪 Doors Only</button>
                        <button type="button" onclick="next(2, 'service', 'Elite Roofing')" class="p-5 bg-white rounded-2xl border-2 border-slate-50 text-left font-bold hover:border-cyan-400 transition">🏠 Architectural Roof</button>
                        <button type="button" onclick="next(2, 'service', 'Solar Matrix')" class="p-5 bg-white rounded-2xl border-2 border-slate-50 text-left font-bold hover:border-cyan-400 transition">☀️ Solar Power</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">02. Service Location</h2>
                    <select id="state" class="w-full p-5 bg-white border-2 border-slate-50 rounded-2xl font-bold outline-none mb-6">
                        <option value="">Select Your State</option>
                        <option value="California">California</option><option value="Texas">Texas</option><option value="Florida">Florida</option><option value="New York">New York</option>
                        <option value="Other">Other U.S. State</option>
                    </select>
                    <button type="button" onclick="showStep('step3')" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase">Verify Coverage</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">03. Final Details</h2>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" class="w-full p-5 bg-white border-2 border-slate-50 rounded-2xl outline-none" required>
                        <input type="tel" id="phone" placeholder="Phone (For Contractor Match)" class="w-full p-5 bg-white border-2 border-slate-50 rounded-2xl outline-none" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="date" id="appDate" class="p-5 bg-white border-2 border-slate-50 rounded-2xl outline-none" required>
                            <input type="number" id="zip" placeholder="Zip Code" class="p-5 bg-white border-2 border-slate-50 rounded-2xl outline-none" required>
                        </div>
                        <button type="submit" class="w-full bg-cyan-500 text-slate-900 p-6 rounded-2xl font-black uppercase shadow-xl shadow-cyan-200">Submit to Matrix</button>
                    </div>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-5xl mx-auto mb-20">
        <h2 class="text-center font-black uppercase tracking-widest text-slate-400 mb-10 text-xs">National Contractor Details & Features</h2>
        <div class="grid md:grid-cols-3 gap-8">
            <div class="glass p-6 neon-border">
                <div class="img-box mb-6"><img src="https://images.unsplash.com/photo-1509644851169-2acc08aa25b5?w=600" alt="Windows"></div>
                <h3 class="font-black italic uppercase text-lg">Window Matrix</h3>
                <p class="text-[10px] text-slate-500 font-bold uppercase mt-2 leading-relaxed">Double-pane insulated glass with argon gas fill. 99% UV protection and sound reduction technology available in all states.</p>
            </div>
            <div class="glass p-6 neon-border">
                <div class="img-box mb-6"><img src="https://images.unsplash.com/photo-1632759162353-19c9a543fe79?w=600" alt="Roof"></div>
                <h3 class="font-black italic uppercase text-lg">Contractor Roofs</h3>
                <p class="text-[10px] text-slate-500 font-bold uppercase mt-2 leading-relaxed">Certified GAF & Owens Corning installers. Shingle, metal, and flat roof systems with lifetime transferable warranties.</p>
            </div>
            <div class="glass p-6 neon-border">
                <div class="img-box mb-6"><img src="https://images.unsplash.com/photo-1517581177682-a085bb7ffb15?w=600" alt="Doors"></div>
                <h3 class="font-black italic uppercase text-lg">Entry Systems</h3>
                <p class="text-[10px] text-slate-500 font-bold uppercase mt-2 leading-relaxed">Fiberglass and steel reinforced entry doors. High-security multipoint locking systems and custom architectural designs.</p>
            </div>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 bg-slate-900/98 backdrop-blur-2xl z-[1000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-between items-center mb-10 border-b border-white/10 pb-6">
                <h2 class="text-3xl font-black italic text-cyan-400 tracking-tighter">NATIONAL HQ COMMAND</h2>
                <button onclick="location.reload()" class="bg-red-500/20 text-red-500 border border-red-500/20 px-4 py-1 rounded-full text-[10px] font-bold">DISCONNECT</button>
            </div>
            <div id="loginBox" class="max-w-xs mx-auto py-20 text-center">
                <input type="password" id="adminKey" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl mb-4 text-center text-3xl outline-none" placeholder="****">
                <button onclick="unlock()" class="w-full bg-cyan-500 text-slate-900 p-5 rounded-2xl font-black uppercase">Verify ID</button>
            </div>
            <div id="dashboard" class="hidden grid md:grid-cols-2 gap-4"></div>
        </div>
    </div>

    <footer class="text-center py-10 opacity-30 border-t border-slate-200 mt-20">
        <p class="text-[8px] font-black uppercase tracking-[0.5em]">U.S. Home Improvements National Enterprise • 50 State Network</p>
    </footer>

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

        let lead = { state: 'N/A' };

        function showStep(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function next(s, k, v) {
            if(k) lead[k] = v;
            showStep('step' + s);
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            lead.name = document.getElementById('name').value;
            lead.phone = document.getElementById('phone').value;
            lead.state = document.getElementById('state').value;
            lead.date = document.getElementById('appDate').value;
            lead.zip = document.getElementById('zip').value;
            lead.timestamp = new Date().toLocaleString();

            db.ref('leads').push(lead).then(() => {
                alert("QUALIFIED! National Specialist will contact you.");
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
                        <p class="text-xs text-gray-400 mt-4 font-medium italic">📞 ${data[id].phone} | 📅 Visit: ${data[id].date}</p>
                    </div>` + h;
                }
                document.getElementById('dashboard').innerHTML = h || 'No leads in the matrix.';
            });
        }
    </script>
</body>
</html>
