<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Enterprise Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --slate: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--slate); scroll-behavior: smooth; margin: 0; overflow-x: hidden; }
        
        .hero-bg {
            background: linear-gradient(rgba(15, 23, 42, 0.85), rgba(15, 23, 42, 0.85)),
                        url('https://images.unsplash.com/photo-1600585154340-be6199f7e009?auto=format&fit=crop&w=1600&q=80');
            background-size: cover; background-position: center;
        }

        .glass-panel {
            background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(20px);
            border-radius: 2.5rem; border: 1px solid white; box-shadow: 0 40px 100px rgba(0,0,0,0.08);
        }

        .step { display: none; }
        .step.active { display: block; animation: slideFade 0.5s ease-out; }
        @keyframes slideFade { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        .input-matrix {
            width: 100%; padding: 1.25rem; border-radius: 1.25rem; border: 2px solid #f1f5f9;
            font-weight: 600; outline: none; transition: 0.3s; background: #fff; appearance: none;
        }
        .input-matrix:focus { border-color: var(--neon); box-shadow: 0 0 20px rgba(0, 242, 255, 0.1); }

        .btn-elite {
            background: var(--slate); color: white; padding: 1.3rem; border-radius: 1.25rem;
            font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; transition: 0.4s;
        }
        .btn-elite:hover { background: var(--neon); color: var(--slate); transform: translateY(-3px); }

        .feature-card { background: white; border-radius: 2rem; border: 1px solid #f1f5f9; transition: 0.4s; cursor: pointer; }
        .feature-card:hover { border-color: var(--neon); transform: translateY(-10px); }
    </style>
</head>
<body>

    <header class="hero-bg h-[60vh] flex flex-col items-center justify-center text-center px-6 text-white relative">
        <h1 class="text-5xl md:text-8xl font-black italic tracking-tighter uppercase leading-none">U.S. HOME<br>IMPROVEMENTS</h1>
        <p class="text-cyan-400 font-bold tracking-[0.5em] text-[10px] mt-8 uppercase">Nationwide Certified Contractor Matrix</p>
        <div class="mt-10">
            <a href="#portal" class="bg-white text-slate-900 px-10 py-4 rounded-full font-black text-xs uppercase hover:bg-cyan-400 transition">Start Qualification</a>
        </div>
    </header>

    <section id="portal" class="max-w-3xl mx-auto -mt-20 px-4 mb-32 relative z-20">
        <div class="glass-panel p-10 md:p-16 border-t-[10px] border-slate-900">
            <form id="masterLeadForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black italic mb-8 uppercase">01. Qualification</h2>
                    <div class="space-y-6">
                        <select id="homeowner" class="input-matrix" required>
                            <option value="">Property Ownership Status?</option>
                            <option value="Yes">I am the Homeowner</option>
                            <option value="No">I am a Renter</option>
                        </select>
                        <select id="service" class="input-matrix" required onchange="checkWindows()">
                            <option value="">Select Upgrade Service</option>
                            <option value="Windows">Replacement Windows</option>
                            <option value="Doors">Security Entry Doors</option>
                            <option value="Roofing">Architectural Roofing</option>
                            <option value="Solar">Solar Energy Matrix</option>
                        </select>
                        <div id="winDiv" class="hidden">
                            <select id="winCount" class="input-matrix">
                                <option value="">Quantity of Windows?</option>
                                <option value="1-5">1 - 5 Windows</option>
                                <option value="6-10">6 - 10 Windows</option>
                                <option value="11-20">11 - 20 Windows</option>
                                <option value="20+">20+ Units</option>
                            </select>
                        </div>
                        <button type="button" onclick="goNext('step2')" class="btn-elite">Continue</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black italic mb-8 uppercase">02. Timing & Eligibility</h2>
                    <div class="space-y-6">
                        <select id="ready" class="input-matrix" required>
                            <option value="">Project Timeline</option>
                            <option value="ASAP">As Soon As Possible</option>
                            <option value="3-Months">Within 3 Months</option>
                            <option value="6-Months">Within 6 Months</option>
                            <option value="1-Year">In a Year</option>
                        </select>
                        <select id="credit" class="input-matrix" required>
                            <option value="">Estimated Credit Score</option>
                            <option value="Excellent (720+)">Excellent (720+)</option>
                            <option value="Good (660-719)">Good (660-719)</option>
                            <option value="Fair (600-659)">Fair (600-659)</option>
                        </select>
                        <button type="button" onclick="goNext('step3')" class="btn-elite">Schedule Visit</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black italic mb-8 uppercase">03. Deployment Window</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                        <input type="date" id="appDate" class="input-matrix" required>
                        <select id="appTime" class="input-matrix">
                            <option>Morning (8AM-12PM)</option>
                            <option>Afternoon (12PM-4PM)</option>
                        </select>
                    </div>
                    <button type="button" onclick="goNext('step4')" class="btn-elite">Final Details</button>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-2xl font-black italic mb-8 uppercase">04. Contact Protocol</h2>
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Name" class="input-matrix" required>
                        <input type="number" id="cAge" placeholder="Age" class="input-matrix" required>
                        <input type="email" id="cEmail" placeholder="Email Address" class="input-matrix" required>
                        <input type="tel" id="cPhone" placeholder="Phone Number" class="input-matrix" required>
                        <input type="text" id="cAddr" placeholder="Street Address" class="input-matrix" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="text" id="cState" placeholder="State" class="input-matrix" required>
                            <input type="number" id="cZip" placeholder="Zip" class="input-matrix" required>
                        </div>
                        <button type="submit" class="btn-elite bg-cyan-500 text-slate-900">Get Free Quote</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-6xl mx-auto px-6 mb-32 grid md:grid-cols-4 gap-8">
        <div class="feature-card p-6"><h4 class="font-black uppercase text-xs italic">Windows Matrix</h4></div>
        <div class="feature-card p-6"><h4 class="font-black uppercase text-xs italic">Security Doors</h4></div>
        <div class="feature-card p-6"><h4 class="font-black uppercase text-xs italic">Roofing Elite</h4></div>
        <div class="feature-card p-6"><h4 class="font-black uppercase text-xs italic">Solar Power</h4></div>
    </section>

    <div id="adminHQ" class="fixed inset-0 bg-slate-900/98 backdrop-blur-3xl z-[5000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-6xl mx-auto">
            <h2 class="text-3xl font-black italic text-cyan-400 mb-10 border-b border-white/10 pb-4">HQ DATA COMMAND</h2>
            <div id="loginBox" class="max-w-xs mx-auto py-20">
                <input type="password" id="pin" class="w-full p-6 bg-white/5 border border-white/10 rounded-2xl mb-4 text-center text-4xl" placeholder="KEY">
                <button onclick="unlock()" class="btn-elite bg-cyan-500 text-slate-900">UNLOCK</button>
            </div>
            <div id="dash" class="hidden grid md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
            <button onclick="location.reload()" class="mt-10 opacity-30 text-xs">DISCONNECT</button>
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

        function goNext(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function checkWindows() {
            document.getElementById('winDiv').classList.toggle('hidden', document.getElementById('service').value !== 'Windows');
        }

        document.getElementById('masterLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                name: document.getElementById('cName').value,
                age: document.getElementById('cAge').value,
                phone: document.getElementById('cPhone').value,
                address: document.getElementById('cAddr').value,
                state: document.getElementById('cState').value,
                zip: document.getElementById('cZip').value,
                owner: document.getElementById('homeowner').value,
                service: document.getElementById('service').value,
                windows: document.getElementById('winCount').value || 'N/A',
                readiness: document.getElementById('ready').value,
                credit: document.getElementById('credit').value,
                date: document.getElementById('appDate').value,
                time: document.getElementById('appTime').value,
                ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { alert("Qualified!"); location.reload(); });
        });

        let taps = 0, last = 0;
        document.addEventListener('click', () => {
            if(Date.now() - last < 400) taps++; else taps = 1; last = Date.now();
            if(taps === 5) document.getElementById('adminHQ').classList.remove('hidden');
        });

        function unlock() {
            if(document.getElementById('pin').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('dash').classList.remove('hidden');
                sync();
            }
        }

        function sync() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val();
                let h = '';
                for(let k in leads) {
                    h = `<div class="bg-white/5 border-l-4 border-cyan-400 p-6 rounded-r-2xl">
                        <p class="font-black italic uppercase text-lg">${leads[k].name} (${leads[k].age})</p>
                        <p class="text-xs text-gray-400">${leads[k].phone} | ${leads[k].state}</p>
                        <div class="mt-4 text-[10px] text-cyan-400 font-bold">
                            SERVICE: ${leads[k].service} (${leads[k].windows})<br>
                            CREDIT: ${leads[k].credit} | READY: ${leads[k].readiness}<br>
                            APPT: ${leads[k].date} @ ${leads[k].time}
                        </div>
                        <button onclick="db.ref('leads/${k}').remove()" class="mt-4 text-[8px] text-red-500">DELETE</button>
                    </div>` + h;
                }
                document.getElementById('dash').innerHTML = h || 'No Leads.';
            });
        }
    </script>
</body>
</html>
