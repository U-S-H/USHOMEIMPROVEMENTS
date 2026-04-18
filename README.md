<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Enterprise</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --slate: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--slate); margin: 0; padding: 0; overflow-x: hidden; }
        
        .hero-gradient { background: linear-gradient(rgba(15, 23, 42, 0.8), rgba(15, 23, 42, 0.8)), url('https://images.unsplash.com/photo-1600585154340-be6199f7e009?auto=format&fit=crop&w=1600&q=80'); background-size: cover; background-position: center; }
        
        .glass-panel { background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(15px); border-radius: 2rem; border: 1px solid #e2e8f0; box-shadow: 0 20px 40px rgba(0,0,0,0.05); }

        .step { display: none; }
        .step.active { display: block; animation: fadeIn 0.4s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .input-box { width: 100%; padding: 1rem; border-radius: 1rem; border: 2px solid #f1f5f9; font-weight: 600; outline: none; transition: 0.3s; background: #fff; appearance: none; }
        .input-box:focus { border-color: var(--neon); }

        .btn-matrix { background: var(--slate); color: white; padding: 1.2rem; border-radius: 1rem; font-weight: 800; text-transform: uppercase; width: 100%; transition: 0.3s; cursor: pointer; border: none; }
        .btn-matrix:hover { background: var(--neon); color: var(--slate); transform: scale(1.02); }

        .service-card { background: white; border-radius: 1.5rem; overflow: hidden; border: 1px solid #f1f5f9; transition: 0.3s; }
        .service-card:hover { transform: translateY(-5px); border-color: var(--neon); }
        .img-slot { width: 100%; height: 200px; background: #e2e8f0; position: relative; overflow: hidden; }
        .img-slot img { width: 100%; height: 100%; object-fit: cover; }
    </style>
</head>
<body>

    <header class="hero-gradient h-[60vh] flex flex-col items-center justify-center text-center px-6 text-white">
        <h1 class="text-4xl md:text-6xl font-black italic tracking-tighter uppercase leading-none">U.S. HOME<br>IMPROVEMENTS</h1>
        <p class="text-cyan-400 font-bold tracking-[0.4em] text-[10px] mt-4 uppercase">National Qualified Matrix</p>
        <div class="mt-8 flex gap-4">
            <a href="#portal" class="bg-white text-slate-900 px-6 py-3 rounded-full font-black text-xs uppercase shadow-lg">Get Free Quote</a>
        </div>
    </header>

    <section id="portal" class="max-w-2xl mx-auto -mt-20 px-4 mb-20 relative z-10">
        <div class="glass-panel p-8 md:p-12 border-t-8 border-slate-900">
            <form id="matrixLeadForm">
                <div class="step active" id="step1">
                    <h2 class="text-xl font-black italic mb-6 uppercase">01. Project Type</h2>
                    <div class="space-y-4">
                        <select id="service" class="input-box">
                            <option value="Windows">Energy-Efficient Windows</option>
                            <option value="Doors">High-Security Doors</option>
                            <option value="Roofing">Architectural Roofing</option>
                            <option value="Solar">Residential Solar</option>
                        </select>
                        <select id="credit" class="input-box">
                            <option value="Excellent (720+)">Credit: Excellent (720+)</option>
                            <option value="Good (660-719)">Credit: Good (660-719)</option>
                            <option value="Fair (600-659)">Credit: Fair (600-659)</option>
                        </select>
                        <button type="button" onclick="showStep('step2')" class="btn-matrix">Next: Location</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-xl font-black italic mb-6 uppercase">02. Location</h2>
                    <div class="space-y-4">
                        <input type="text" id="state" class="input-box" placeholder="Your State (e.g. Florida)">
                        <select id="lang" class="input-box">
                            <option value="English">Language: English</option>
                            <option value="Spanish">Language: Español</option>
                        </select>
                        <button type="button" onclick="showStep('step3')" class="btn-matrix">Next: Scheduling</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-xl font-black italic mb-6 uppercase">03. Time Slot</h2>
                    <div class="space-y-4">
                        <input type="date" id="date" class="input-box">
                        <select id="time" class="input-box">
                            <option>Morning (8AM-12PM)</option>
                            <option>Afternoon (12PM-4PM)</option>
                        </select>
                        <button type="button" onclick="showStep('step4')" class="btn-matrix">Final: Contact Info</button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-xl font-black italic mb-6 uppercase">04. Finish Verification</h2>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" class="input-box">
                        <input type="email" id="email" placeholder="Email Address" class="input-box">
                        <input type="tel" id="phone" placeholder="Phone Number" class="input-box">
                        <input type="text" id="address" placeholder="Property Address" class="input-box">
                        <button type="submit" class="btn-matrix bg-cyan-500 text-slate-900">Get Free Estimate</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-6xl mx-auto px-6 mb-24 grid md:grid-cols-3 gap-8">
        <div class="service-card">
            <div class="img-slot"><img src="https://images.unsplash.com/photo-1512917774080-9991f1c4c750?w=500"></div>
            <div class="p-6">
                <h3 class="font-black italic uppercase text-sm">Window Matrix</h3>
                <p class="text-[11px] text-slate-400 font-bold uppercase mt-2">UV Protecting & Impact Resistant.</p>
            </div>
        </div>
        <div class="service-card">
            <div class="img-slot"><img src="https://images.unsplash.com/photo-1632759162353-19c9a543fe79?w=500"></div>
            <div class="p-6">
                <h3 class="font-black italic uppercase text-sm">Roofing Elite</h3>
                <p class="text-[11px] text-slate-400 font-bold uppercase mt-2">Lifetime Guaranteed Protection.</p>
            </div>
        </div>
        <div class="service-card">
            <div class="img-slot"><img src="https://images.unsplash.com/photo-1513694490325-24b3dc52a21c?w=500"></div>
            <div class="p-6">
                <h3 class="font-black italic uppercase text-sm">Solar Power</h3>
                <p class="text-[11px] text-slate-400 font-bold uppercase mt-2">Zero-Down Federal Programs.</p>
            </div>
        </div>
    </section>

    <footer class="bg-white border-t border-slate-100 py-16 px-6">
        <div class="max-w-6xl mx-auto grid md:grid-cols-2 gap-12 text-[12px] font-medium text-slate-500">
            <div>
                <h4 class="font-black italic text-slate-900 uppercase mb-4">Privacy Protocol</h4>
                <p>U.S. Home Improvements secures all project data via encrypted matrices. Information is strictly utilized for contractor matching and inspection logistics. No third-party data distribution is permitted.</p>
            </div>
            <div>
                <h4 class="font-black italic text-slate-900 uppercase mb-4">National Benefits</h4>
                <p>Every qualified property receive a complimentary on-site inspection, access to zero-down federal financing programs, and a lifetime transferable structural warranty.</p>
            </div>
        </div>
        <p class="text-center mt-12 opacity-30 text-[9px] font-black uppercase tracking-widest">© 2026 U.S. Home Improvements</p>
    </footer>

    <div id="adminPortal" class="fixed inset-0 bg-slate-900/98 backdrop-blur-3xl z-[5000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-4xl mx-auto py-10">
            <h2 class="text-2xl font-black italic text-cyan-400 mb-8">HQ DATA COMMAND</h2>
            <div id="loginBox" class="text-center py-20">
                <input type="password" id="adminKey" class="w-full max-w-xs p-4 bg-white/10 rounded-xl mb-4 text-center text-2xl outline-none" placeholder="KEY">
                <button onclick="unlock()" class="btn-matrix max-w-xs bg-cyan-500 text-slate-900 mx-auto block">Unlock</button>
            </div>
            <div id="dashboard" class="hidden grid gap-4"></div>
            <button onclick="location.reload()" class="mt-8 text-xs opacity-50">Exit Command</button>
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

        function showStep(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        document.getElementById('matrixLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const lead = {
                name: document.getElementById('name').value,
                email: document.getElementById('email').value,
                phone: document.getElementById('phone').value,
                address: document.getElementById('address').value,
                service: document.getElementById('service').value,
                credit: document.getElementById('credit').value,
                state: document.getElementById('state').value,
                lang: document.getElementById('lang').value,
                date: document.getElementById('date').value,
                time: document.getElementById('time').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(lead).then(() => {
                alert("Qualified! Specialist will contact you.");
                location.reload();
            });
        });

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
                    h = `<div class="bg-white/5 p-6 rounded-2xl border-l-4 border-cyan-400">
                        <p class="font-black uppercase">${data[id].name} (${data[id].state})</p>
                        <p class="text-xs text-gray-400 italic">${data[id].email} | ${data[id].phone}</p>
                        <p class="text-[10px] mt-2 text-cyan-400 uppercase">${data[id].service} | Credit: ${data[id].credit}</p>
                        <button onclick="db.ref('leads/${id}').remove()" class="text-[8px] mt-4 opacity-30">Delete</button>
                    </div>` + h;
                }
                document.getElementById('dashboard').innerHTML = h || 'No Leads.';
            });
        }
    </script>
</body>
</html>
