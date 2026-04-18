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
        :root { --neon: #00f2ff; --slate: #0f172a; --slate-light: #1e293b; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--slate); scroll-behavior: smooth; margin: 0; overflow-x: hidden; }
        
        /* Hero Section with Your Image */
        .hero-bg {
            background: linear-gradient(rgba(15, 23, 42, 0.85), rgba(15, 23, 42, 0.80)),
                        url('./WA_1776549402527.jpeg');
            background-size: cover; background-position: center;
        }

        .glass-panel {
            background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(20px);
            border-radius: 2.5rem; border: 1px solid white; box-shadow: 0 40px 100px rgba(0,0,0,0.08);
        }

        /* Animations */
        .step { display: none; }
        .step.active { display: block; animation: slideFade 0.5s ease-out; }
        @keyframes slideFade { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        .input-matrix {
            width: 100%; padding: 1.25rem; border-radius: 1.25rem; border: 2px solid #f1f5f9;
            font-weight: 600; outline: none; transition: 0.3s; background: #fff;
        }
        .input-matrix:focus { border-color: var(--neon); box-shadow: 0 0 20px rgba(0, 242, 255, 0.1); }

        .btn-elite {
            background: var(--slate); color: white; padding: 1.3rem; border-radius: 1.25rem;
            font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; transition: 0.4s;
        }
        .btn-elite:hover { background: var(--neon); color: var(--slate); transform: translateY(-3px); }
        
        .feature-card {
            background: white; border-radius: 2rem; border: 1px solid #f1f5f9; transition: 0.4s; overflow: hidden;
        }
        .feature-card:hover { border-color: var(--neon); transform: translateY(-10px); }
        .feature-card img { width: 100%; height: 200px; object-fit: cover; }
    </style>
</head>
<body>

    <header class="hero-bg h-[70vh] flex flex-col items-center justify-center text-center px-6 text-white relative">
        <div class="absolute top-8 left-8 flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" alt="Logo" class="h-12">
            <span class="text-[10px] font-black tracking-[0.3em] uppercase border-l-2 border-cyan-400 pl-4">National Enterprise</span>
        </div>
        <h1 class="text-5xl md:text-8xl font-black italic tracking-tighter uppercase leading-none mt-10">THE NATIONAL<br>STANDARD</h1>
        <p class="text-cyan-400 font-bold tracking-[0.6em] text-[10px] mt-8 uppercase">Nationwide Certified Contractor Matrix</p>
    </header>

    <section id="portal" class="max-w-3xl mx-auto -mt-24 px-4 mb-32 relative z-20">
        <div class="glass-panel p-10 md:p-16 border-t-[10px] border-slate-900 shadow-2xl">
            <form id="masterLeadForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">01. Project Criteria</h2>
                    <div class="space-y-6">
                        <select id="homeowner" class="input-matrix" required>
                            <option value="">Property Ownership Status?</option>
                            <option value="Yes">I am the Homeowner</option>
                            <option value="No">I am a Renter</option>
                        </select>
                        <select id="service" class="input-matrix" required onchange="handleServiceSelection()">
                            <option value="">Select Upgrade Service</option>
                            <option value="Windows">Replacement Windows</option>
                            <option value="Doors">Security Entry Doors</option>
                            <option value="Roofing">Architectural Roofing</option>
                            <option value="Solar">Residential Solar Matrix</option>
                            <option value="Kitchen">Kitchen Remodeling</option>
                            <option value="Bathroom">Bathroom Remodeling</option>
                            <option value="Deck">Deck Remodeling</option>
                            <option value="Garage">Garage Matrix</option>
                        </select>
                        <button type="button" onclick="goNext('step2')" class="btn-elite">Continue</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">02. Timing & Eligibility</h2>
                    <div class="space-y-6">
                        <select id="ready" class="input-matrix" required>
                            <option value="">Project Timeline</option>
                            <option value="ASAP">As Soon As Possible</option>
                            <option value="2-Months">Within 2 Months</option>
                            <option value="Flexible">I'm Flexible</option>
                        </select>
                        <select id="credit" class="input-matrix" required>
                            <option value="">Estimated Credit Rating</option>
                            <option value="Excellent (720+)">Excellent (720+)</option>
                            <option value="Good (660-719)">Good (660-719)</option>
                            <option value="Fair (600-659)">Fair (600-659)</option>
                        </select>
                        <button type="button" onclick="goNext('step3')" class="btn-elite">Final Step</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">03. Contact Protocol</h2>
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Legal Name" class="input-matrix" required>
                        <input type="tel" id="cPhone" placeholder="Phone Number" class="input-matrix" required>
                        <input type="email" id="cEmail" placeholder="Email Address" class="input-matrix" required>
                        <input type="text" id="cAddr" placeholder="Street Address" class="input-matrix" required>
                        <button type="submit" class="btn-elite bg-cyan-500 text-slate-900">Authorise & Get Quote</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 mb-32">
        <div class="text-center mb-16">
            <h3 class="text-4xl font-black italic uppercase">National Network Services</h3>
            <p class="text-slate-400 font-bold uppercase text-[10px] tracking-widest mt-2">Serving All 50 States Across the Continental U.S.</p>
        </div>
        <div class="grid md:grid-cols-3 lg:grid-cols-4 gap-8">
            <div class="feature-card p-6"><img src="./WA_1776549555727.jpeg" class="rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Windows Matrix</h4></div>
            <div class="feature-card p-6"><img src="./WA_1776549622236.jpeg" class="rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Security Doors</h4></div>
            <div class="feature-card p-6"><img src="./WA_1776549716792.jpeg" class="rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Roofing Elite</h4></div>
            <div class="feature-card p-6"><img src="./WA_1776549781247.jpeg" class="rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Solar Matrix</h4></div>
            <div class="feature-card p-6"><img src="./WA_1776549862258.jpeg" class="rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Kitchen Remodel</h4></div>
            <div class="feature-card p-6"><img src="./WA_1776549917709.jpeg" class="rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Bathroom Remodel</h4></div>
            <div class="feature-card p-6"><img src="./WA_1776549990293.jpeg" class="rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Deck Remodel</h4></div>
            <div class="feature-card p-6"><img src="./WA_1776550066723.jpeg" class="rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Garage Matrix</h4></div>
        </div>
    </section>

    <footer class="bg-slate-900 py-16 text-white/40 text-center px-6">
        <img src="./WA_1776550450872.jpeg" alt="Logo" class="h-10 mx-auto mb-6 grayscale brightness-200">
        <p class="text-[9px] font-black uppercase tracking-[0.5em]">U.S. HOME IMPROVEMENTS • NATIONAL NETWORK • 2026</p>
    </footer>

    <div id="adminHQ" class="fixed inset-0 bg-slate-950 z-[5000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-5xl mx-auto py-10">
            <h2 class="text-3xl font-black italic text-cyan-400 uppercase mb-10">HQ Lead Matrix</h2>
            <div id="loginGate" class="text-center py-20">
                <input type="password" id="adminPin" class="p-6 bg-white/5 border border-white/10 rounded-2xl text-center text-4xl mb-4" placeholder="PIN">
                <button onclick="unlockHQ()" class="btn-elite">Login</button>
            </div>
            <div id="dash" class="hidden grid gap-6"></div>
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

        document.getElementById('masterLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                service: document.getElementById('service').value,
                credit: document.getElementById('credit').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                alert("QUALIFIED! We will contact you shortly.");
                location.reload();
            });
        });

        // Admin Access
        let taps = 0;
        document.addEventListener('click', () => {
            taps++;
            if(taps === 10) document.getElementById('adminHQ').classList.remove('hidden');
            setTimeout(() => taps = 0, 3000);
        });

        function unlockHQ() {
            if(document.getElementById('adminPin').value === "786") {
                document.getElementById('loginGate').classList.add('hidden');
                document.getElementById('dash').classList.remove('hidden');
                syncLeads();
            }
        }

        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val();
                let html = '';
                for(let k in leads) {
                    html += `<div class="bg-white/5 p-6 rounded-2xl border-l-4 border-cyan-400">
                        <p class="font-bold uppercase text-cyan-400">${leads[k].service}</p>
                        <h3 class="text-xl font-black">${leads[k].name}</h3>
                        <p>📞 ${leads[k].phone} | 💳 ${leads[k].credit}</p>
                    </div>`;
                }
                document.getElementById('dash').innerHTML = html;
            });
        }
    </script>
</body>
</html>
