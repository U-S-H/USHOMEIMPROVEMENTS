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
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--slate); scroll-behavior: smooth; }
        
        .glass-card { 
            background: rgba(255, 255, 255, 0.9); 
            backdrop-filter: blur(20px); 
            border: 1px solid rgba(255,255,255,1); 
            border-radius: 2.5rem; 
            box-shadow: 0 20px 50px rgba(0,0,0,0.04); 
        }

        .step { display: none; }
        .step.active { display: block; animation: slideIn 0.5s ease; }
        @keyframes slideIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .input-field { 
            width: 100%; padding: 1.1rem; border-radius: 1.2rem; border: 2px solid #f1f5f9; 
            font-weight: 600; outline: none; transition: 0.3s; background: white;
        }
        .input-field:focus { border-color: var(--neon); box-shadow: 0 0 15px rgba(0, 242, 255, 0.1); }

        .btn-action { 
            background: var(--slate); color: white; padding: 1.2rem; border-radius: 1.2rem; 
            font-weight: 800; text-transform: uppercase; transition: 0.3s; width: 100%;
        }
        .btn-action:hover { background: var(--neon); color: var(--slate); transform: translateY(-2px); }

        .policy-box { font-size: 11px; line-height: 1.6; color: #64748b; }
    </style>
</head>
<body>

    <header class="relative h-[60vh] flex items-center justify-center overflow-hidden bg-slate-900">
        <img src="https://images.unsplash.com/photo-1600585154340-be6199f7e009?auto=format&fit=crop&w=1600&q=80" class="absolute inset-0 w-full h-full object-cover opacity-50">
        <div class="relative z-10 text-center px-4">
            <h1 class="text-4xl md:text-6xl font-black italic text-white tracking-tighter uppercase">U.S. HOME IMPROVEMENTS</h1>
            <p class="text-cyan-400 font-bold tracking-[0.4em] text-xs mt-4 uppercase">National Qualified Contractor Matrix</p>
            <div class="mt-8 flex justify-center gap-4">
                <a href="#portal" class="bg-white text-slate-900 px-8 py-3 rounded-full font-black text-xs uppercase hover:bg-cyan-400 transition">Get Free Quote</a>
                <a href="#about" class="border border-white/30 text-white px-8 py-3 rounded-full font-black text-xs uppercase hover:bg-white/10 transition">Our Services</a>
            </div>
        </div>
    </header>

    <section id="portal" class="max-w-3xl mx-auto -mt-20 px-4 mb-24 relative z-20">
        <div class="glass-card p-8 md:p-14 border-t-8 border-cyan-500">
            <form id="qualifyForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black italic mb-6 uppercase">01. Qualify Your Project</h2>
                    <div class="space-y-4">
                        <label class="text-[10px] font-black uppercase text-slate-400 ml-2">Select Primary Service</label>
                        <select id="service" class="input-field" required>
                            <option value="Windows">Replacement Windows</option>
                            <option value="Doors">Professional Entry Doors</option>
                            <option value="Roofing">Elite Architectural Roofing</option>
                            <option value="Solar">Solar Energy Systems</option>
                        </select>
                        
                        <label class="text-[10px] font-black uppercase text-slate-400 ml-2">Estimated Credit Score (For Financing)</label>
                        <select id="credit" class="input-field" required>
                            <option value="Excellent (720+)">Excellent (720+)</option>
                            <option value="Good (660-719)">Good (660-719)</option>
                            <option value="Fair (600-659)">Fair (600-659)</option>
                            <option value="Building (Below 600)">Building (Below 600)</option>
                        </select>
                        <button type="button" onclick="showStep('step2')" class="btn-action mt-4">Next: Location & Language</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black italic mb-6 uppercase">02. Regional Assignment</h2>
                    <div class="space-y-4">
                        <input type="text" id="state" class="input-field" placeholder="Enter Your State (e.g. California)" required>
                        <select id="lang" class="input-field">
                            <option value="English">Preferred Language: English</option>
                            <option value="Spanish">Preferred Language: Español</option>
                        </select>
                        <button type="button" onclick="showStep('step3')" class="btn-action mt-4">Next: Appointment Visit</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black italic mb-6 uppercase">03. Schedule Free Quote</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="text-[9px] font-black uppercase text-slate-400 ml-2">Preferred Date</label>
                            <input type="date" id="date" class="input-field" required>
                        </div>
                        <div>
                            <label class="text-[9px] font-black uppercase text-slate-400 ml-2">Time Slot</label>
                            <select id="time" class="input-field">
                                <option>Morning (8AM-12PM)</option>
                                <option>Afternoon (12PM-4PM)</option>
                                <option>Evening (4PM-7PM)</option>
                            </select>
                        </div>
                    </div>
                    <button type="button" onclick="showStep('step4')" class="btn-action mt-6">Final Step: Contact Info</button>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-2xl font-black italic mb-6 uppercase">04. Confirm Application</h2>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" class="input-field" required>
                        <input type="email" id="email" placeholder="Email Address" class="input-field" required>
                        <input type="tel" id="phone" placeholder="Phone Number" class="input-field" required>
                        <input type="text" id="address" placeholder="Property Address" class="input-field" required>
                        <button type="submit" class="btn-action mt-4 shadow-xl shadow-cyan-200">Get My Free Quote Now</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section id="about" class="max-w-6xl mx-auto px-4 mb-32">
        <div class="grid md:grid-cols-2 gap-16 items-center">
            <div class="space-y-6">
                <h3 class="text-3xl font-black italic uppercase">Why Choose U.S. Home Improvements?</h3>
                <p class="text-slate-500 font-medium">Humari company United States mein gharon ko modern aur energy-efficient banane ke liye best solutions deti hai. Humara network 100% certified contractors se juda hua hai jo aapke ghar ki value barhate hain.</p>
                <ul class="space-y-4">
                    <li class="flex gap-4"><span class="text-cyan-500 font-black">✓</span> <strong>Direct Savings:</strong> Energy-efficient windows aur solar se aapke bills 40% tak kam ho sakte hain.</li>
                    <li class="flex gap-4"><span class="text-cyan-500 font-black">✓</span> <strong>Lifetime Security:</strong> Har installation par hum lifetime warranty aur safety assurance dete hain.</li>
                    <li class="flex gap-4"><span class="text-cyan-500 font-black">✓</span> <strong>National Coverage:</strong> Aap kisi bhi state mein hon, humara specialist aapke ghar visit karega.</li>
                </ul>
            </div>
            <div class="h-96 bg-slate-200 rounded-[3rem] overflow-hidden border-4 border-white shadow-xl">
                <img src="https://images.unsplash.com/photo-1513694490325-24b3dc52a21c?auto=format&fit=crop&w=800&q=80" class="w-full h-full object-cover">
            </div>
        </div>
    </section>

    <footer class="bg-white pt-20 pb-10 border-t border-slate-100">
        <div class="max-w-6xl mx-auto px-4 grid md:grid-cols-3 gap-12">
            <div>
                <h4 class="font-black italic mb-4 uppercase">Company Mission</h4>
                <p class="policy-box">U.S. Home Improvements ka maqsad har ghar ko mehfooz aur modern banana hai. Hum quality materials aur elite craftsmanship ke zariye customers ka bharosa jeet-te hain.</p>
            </div>
            <div>
                <h4 class="font-black italic mb-4 uppercase">Privacy Policy</h4>
                <p class="policy-box">Aapka data (Email, Phone, Credit Score) hamare pas end-to-end encrypted mehfooz hai. Hum aapki permission ke bagair data kisi third party ko nahi dete. Data sirf contractor matching aur appointment verification ke liye use kiya jata hai.</p>
            </div>
            <div>
                <h4 class="font-black italic mb-4 uppercase">Service Benefits</h4>
                <p class="policy-box">Humare customers ko milta hai: Free on-site inspection, zero-down financing options, federal energy rebates, aur 24/7 customer support team ka sath.</p>
            </div>
        </div>
        <div class="text-center mt-20 opacity-30 text-[9px] font-black uppercase tracking-[0.5em]">
            © 2026 U.S. Home Improvements National Enterprise Network
        </div>
    </footer>

    <div id="adminPortal" class="fixed inset-0 bg-slate-900/98 backdrop-blur-3xl z-[5000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b border-white/10 pb-6">
                <h2 class="text-3xl font-black italic text-cyan-400 uppercase">HQ Global Command</h2>
                <button onclick="location.reload()" class="bg-red-500 px-4 py-1 rounded text-[10px] font-bold">EXIT</button>
            </div>
            <div id="loginBox" class="max-w-xs mx-auto py-20 text-center">
                <input type="password" id="adminKey" class="w-full p-5 bg-white/10 rounded-2xl mb-4 text-center text-3xl outline-none border border-white/10" placeholder="KEY">
                <button onclick="unlock()" class="btn-action bg-cyan-500 text-slate-900">Unlock Data Matrix</button>
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
        }

        document.getElementById('qualifyForm').addEventListener('submit', (e) => {
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
                alert("CONGRATULATIONS! You are qualified for a Free Quote. Our specialist will call you soon.");
                location.reload();
            });
        });

        // HQ Access (5 taps)
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
                    <div class="bg-white/5 border-l-4 border-cyan-400 p-6 rounded-r-2xl relative group">
                        <div class="flex justify-between">
                            <h4 class="font-black italic uppercase text-lg">${data[id].name}</h4>
                            <span class="text-cyan-400 text-[9px] font-bold uppercase">${data[id].service}</span>
                        </div>
                        <div class="mt-4 space-y-2 text-[11px] text-gray-400 font-medium italic">
                            <p>📧 Email: ${data[id].email}</p>
                            <p>📞 Phone: ${data[id].phone}</p>
                            <p>📍 State: ${data[id].state}</p>
                            <p>🏠 Addr: ${data[id].address}</p>
                            <p class="text-white mt-4 bg-white/10 p-2 rounded">💳 Credit: ${data[id].credit}</p>
                            <p class="text-cyan-400">📅 Appt: ${data[id].date} (${data[id].time})</p>
                        </div>
                        <button onclick="db.ref('leads/${id}').remove()" class="text-[8px] mt-4 opacity-20 group-hover:opacity-100">DELETE</button>
                    </div>` + h;
                }
                document.getElementById('dashboard').innerHTML = h || 'Scanning for data...';
            });
        }
    </script>
</body>
</html>
