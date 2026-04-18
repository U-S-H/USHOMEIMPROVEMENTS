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
        :root { --neon: #00f2ff; --slate: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--slate); scroll-behavior: smooth; }
        
        .glass-card { 
            background: rgba(255, 255, 255, 0.95); 
            backdrop-filter: blur(20px); 
            border: 1px solid white; 
            border-radius: 2.5rem; 
            box-shadow: 0 25px 50px rgba(0,0,0,0.06); 
        }

        .step { display: none; }
        .step.active { display: block; animation: slideIn 0.5s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        .input-field { 
            width: 100%; padding: 1.2rem; border-radius: 1.25rem; border: 2px solid #f1f5f9; 
            font-weight: 600; outline: none; transition: 0.3s; background: white;
        }
        .input-field:focus { border-color: var(--neon); box-shadow: 0 0 15px rgba(0, 242, 255, 0.1); }

        .btn-main { 
            background: var(--slate); color: white; padding: 1.3rem; border-radius: 1.25rem; 
            font-weight: 800; text-transform: uppercase; transition: 0.4s; width: 100%;
        }
        .btn-main:hover { background: var(--neon); color: var(--slate); transform: scale(1.02); }

        .policy-text { font-size: 12px; line-height: 1.7; color: #475569; text-align: justify; }
    </style>
</head>
<body>

    <header class="relative h-[70vh] flex items-center justify-center bg-slate-900 overflow-hidden">
        <img src="https://images.unsplash.com/photo-1600585154340-be6199f7e009?auto=format&fit=crop&w=1600&q=80" class="absolute inset-0 w-full h-full object-cover opacity-40">
        <div class="relative z-10 text-center px-6">
            <h1 class="text-5xl md:text-7xl font-black italic text-white tracking-tighter uppercase leading-none">U.S. HOME<br>IMPROVEMENTS</h1>
            <p class="text-cyan-400 font-bold tracking-[0.5em] text-xs mt-6 uppercase">Certified National Contractor Network</p>
            <div class="mt-10 flex flex-wrap justify-center gap-4">
                <a href="#portal" class="bg-white text-slate-900 px-10 py-4 rounded-full font-black text-xs uppercase hover:bg-cyan-400 transition">Get Free Estimate</a>
                <a href="#about" class="border border-white/40 text-white px-10 py-4 rounded-full font-black text-xs uppercase hover:bg-white/10 transition">View Services</a>
            </div>
        </div>
    </nav>

    <section id="portal" class="max-w-3xl mx-auto -mt-24 px-4 mb-32 relative z-20">
        <div class="glass-card p-10 md:p-16 border-t-[10px] border-slate-900">
            <form id="masterLeadForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black italic mb-8 uppercase tracking-tight">01. Project Qualification</h2>
                    <div class="space-y-5">
                        <label class="text-[10px] font-black uppercase text-slate-400 tracking-widest ml-1">Select Service Category</label>
                        <select id="service" class="input-field" required>
                            <option value="Windows">Energy-Efficient Windows</option>
                            <option value="Doors">High-Security Entry Doors</option>
                            <option value="Roofing">Architectural Roofing Systems</option>
                            <option value="Solar">Residential Solar Matrix</option>
                        </select>
                        
                        <label class="text-[10px] font-black uppercase text-slate-400 tracking-widest ml-1">Estimated Credit Score</label>
                        <select id="credit" class="input-field" required>
                            <option value="Excellent (720+)">Excellent (720+)</option>
                            <option value="Good (660-719)">Good (660-719)</option>
                            <option value="Fair (600-659)">Fair (600-659)</option>
                            <option value="Building (Below 600)">Building (Below 600)</option>
                        </select>
                        <button type="button" onclick="showStep('step2')" class="btn-main mt-6">Next Phase: Geographic Matching</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black italic mb-8 uppercase tracking-tight">02. Regional Distribution</h2>
                    <div class="space-y-5">
                        <input type="text" id="state" class="input-field" placeholder="Target State (e.g. Florida)" required>
                        <select id="lang" class="input-field">
                            <option value="English">Communication: English</option>
                            <option value="Spanish">Communication: Español</option>
                        </select>
                        <button type="button" onclick="showStep('step3')" class="btn-main mt-6">Next Phase: Schedule Visit</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black italic mb-8 uppercase tracking-tight">03. Inspection Schedule</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-400 tracking-widest">Preferred Date</label>
                            <input type="date" id="date" class="input-field" required>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-400 tracking-widest">Arrival Window</label>
                            <select id="time" class="input-field">
                                <option>Morning (8AM - 12PM)</option>
                                <option>Afternoon (12PM - 4PM)</option>
                                <option>Evening (4PM - 7PM)</option>
                            </select>
                        </div>
                    </div>
                    <button type="button" onclick="showStep('step4')" class="btn-main mt-8">Final Phase: Verification</button>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-2xl font-black italic mb-8 uppercase tracking-tight">04. Contact Verification</h2>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Legal Name" class="input-field" required>
                        <input type="email" id="email" placeholder="Email Address" class="input-field" required>
                        <input type="tel" id="phone" placeholder="Contact Number" class="input-field" required>
                        <input type="text" id="address" placeholder="Property Street Address" class="input-field" required>
                        <button type="submit" class="btn-main mt-6 shadow-2xl shadow-cyan-200">Secure Free Estimate</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section id="about" class="max-w-6xl mx-auto px-6 mb-40">
        <div class="grid md:grid-cols-2 gap-20 items-center">
            <div class="space-y-8">
                <h3 class="text-4xl font-black italic uppercase tracking-tighter">Premium Service Benefits</h3>
                <p class="text-slate-500 font-semibold leading-relaxed">U.S. Home Improvements sets the national standard for residential modernization. Our specialized contractor network ensures every project meets elite federal standards.</p>
                <div class="space-y-6">
                    <div class="flex gap-5">
                        <div class="text-cyan-500 font-black text-xl">01</div>
                        <div><h4 class="font-black uppercase text-sm">Asset Valuation</h4><p class="text-xs text-slate-400 font-bold uppercase mt-1">High-end upgrades significantly increase property resale value.</p></div>
                    </div>
                    <div class="flex gap-5">
                        <div class="text-cyan-500 font-black text-xl">02</div>
                        <div><h4 class="font-black uppercase text-sm">Thermal Efficiency</h4><p class="text-xs text-slate-400 font-bold uppercase mt-1">Reduce monthly energy consumption by up to 45% with our Matrix series.</p></div>
                    </div>
                    <div class="flex gap-5">
                        <div class="text-cyan-500 font-black text-xl">03</div>
                        <div><h4 class="font-black uppercase text-sm">Legal Compliance</h4><p class="text-xs text-slate-400 font-bold uppercase mt-1">100% Licensed, Bonded, and Insured contractors in all 50 states.</p></div>
                    </div>
                </div>
            </div>
            <div class="rounded-[4rem] bg-slate-200 h-[500px] overflow-hidden shadow-2xl border-[12px] border-white">
                <img src="https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&fit=crop&w=800&q=80" class="w-full h-full object-cover">
            </div>
        </div>
    </section>

    <footer class="bg-white border-t border-slate-100 pt-24 pb-12">
        <div class="max-w-6xl mx-auto px-6 grid md:grid-cols-3 gap-16">
            <div>
                <h4 class="font-black italic uppercase mb-6 text-sm tracking-widest">Corporate Mission</h4>
                <p class="policy-text">Our objective is to deliver sustainable, high-security residential solutions across the United States. We leverage advanced technology and elite craftsmanship to redefine the American home experience.</p>
            </div>
            <div>
                <h4 class="font-black italic uppercase mb-6 text-sm tracking-widest">Privacy Protocol</h4>
                <p class="policy-text">User data, including credit estimation and contact vectors, is secured via end-to-end encryption. Information is strictly utilized for contractor matching and appointment logistics. No third-party data distribution is permitted.</p>
            </div>
            <div>
                <h4 class="font-black italic uppercase mb-6 text-sm tracking-widest">National Benefits</h4>
                <p class="policy-text">Every U.S. Home Improvements client receives a complimentary on-site inspection, access to zero-down federal financing programs, and a lifetime transferable structural warranty.</p>
            </div>
        </div>
        <div class="text-center mt-24 opacity-20 text-[10px] font-black uppercase tracking-[0.6em]">
            U.S. Home Improvements National Enterprise Network • 2026
        </div>
    </footer>

    <div id="adminPortal" class="fixed inset-0 bg-slate-900/98 backdrop-blur-3xl z-[5000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center mb-16 border-b border-white/10 pb-8">
                <h2 class="text-4xl font-black italic text-cyan-400">HQ DATA COMMAND</h2>
                <button onclick="location.reload()" class="bg-red-500/20 text-red-500 border border-red-500/20 px-8 py-3 rounded-full text-[10px] font-black uppercase">Disconnect</button>
            </div>
            <div id="loginBox" class="max-w-md mx-auto py-20 text-center">
                <input type="password" id="adminKey" class="w-full p-8 bg-white/5 border border-white/10 rounded-3xl text-center text-5xl mb-8 outline-none focus:border-cyan-400" placeholder="KEY">
                <button onclick="unlock()" class="btn-main bg-cyan-500 text-slate-900">Access Leads</button>
            </div>
            <div id="dashboard" class="hidden grid md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
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
            window.scrollTo({top: 0, behavior: 'smooth'});
        }

        document.getElementById('masterLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const leadData = {
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

            db.ref('leads').push(leadData).then(() => {
                alert("APPLICATION AUTHORIZED! A National Specialist will contact you within 24 hours.");
                location.reload();
            });
        });

        // HQ Portal Access (5 Taps)
        let t = 0, l = 0;
        document.addEventListener('click', () => {
            const now = Date.now();
            if(now - l < 400) t++; else t = 1; l = now;
            if(t === 5) document.getElementById('adminPortal').classList.remove('hidden');
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('dashboard').classList.remove('hidden');
                sync();
            } else { alert("ACCESS DENIED"); }
        }

        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val();
                let html = '';
                for(let id in data) {
                    html = `
                    <div class="bg-white/5 border-l-4 border-cyan-400 p-8 rounded-r-3xl relative">
                        <div class="flex justify-between mb-4">
                            <h4 class="font-black italic text-xl uppercase">${data[id].name}</h4>
                            <span class="bg-cyan-500 text-slate-900 px-2 py-1 rounded text-[9px] font-black">${data[id].state}</span>
                        </div>
                        <div class="space-y-3 text-xs text-gray-400 font-bold italic">
                            <p>📧 Email: ${data[id].email}</p>
                            <p>📞 Phone: ${data[id].phone}</p>
                            <p>📍 Addr: ${data[id].address}</p>
                            <div class="bg-white/5 p-4 rounded-xl mt-6 border border-white/5">
                                <p class="text-cyan-400">🛡️ Service: ${data[id].service}</p>
                                <p class="text-white">💳 Credit: ${data[id].credit}</p>
                                <p class="text-white">📅 Appt: ${data[id].date} (${data[id].time})</p>
                                <p class="text-[9px] mt-2 opacity-50">Lang: ${data[id].lang}</p>
                            </div>
                        </div>
                        <button onclick="db.ref('leads/${id}').remove()" class="text-[9px] mt-6 text-red-500 opacity-30 hover:opacity-100 uppercase">Delete Record</button>
                    </div>` + html;
                }
                document.getElementById('dashboard').innerHTML = html || 'No data stream detected.';
            });
        }
    </script>
</body>
</html>
