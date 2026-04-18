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
        :root { --neon: #00f2ff; --slate: #0f172a; --slate-light: #1e293b; --accent: #334155; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--slate); scroll-behavior: smooth; margin: 0; overflow-x: hidden; }
        
        /* Fixed Hero Background with your link */
        .hero-bg {
            background: linear-gradient(rgba(15, 23, 42, 0.90), rgba(15, 23, 42, 0.85)),
                        url('https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776549402527.jpeg');
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
            letter-spacing: 1px;
        }
        .btn-elite:hover { background: var(--neon); color: var(--slate); transform: translateY(-3px); }
        
        .feature-card {
            background: white; border-radius: 2rem; border: 1px solid #f1f5f9; transition: 0.4s; cursor: pointer;
            overflow: hidden;
        }
        .feature-card:hover { border-color: var(--neon); transform: translateY(-10px); box-shadow: 0 20px 40px rgba(0,0,0,0.05); }
        .feature-card img { width: 100%; height: 12rem; object-fit: cover; transition: 0.5s; }
        .feature-card:hover img { transform: scale(1.05); }
    </style>
</head>
<body>

    <header class="hero-bg h-[65vh] flex flex-col items-center justify-center text-center px-6 text-white relative">
        <div class="absolute top-8 left-8 flex items-center gap-3">
            <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776550450872.jpeg" alt="Logo" class="h-10">
            <span class="text-[10px] font-black tracking-[0.3em] uppercase border-l-2 border-cyan-400 pl-4">National Enterprise</span>
        </div>
        <h1 class="text-5xl md:text-8xl font-black italic tracking-tighter uppercase leading-none mt-10">THE NATIONAL<br>STANDARD</h1>
        <p class="text-cyan-400 font-bold tracking-[0.6em] text-[10px] mt-8 uppercase">Nationwide Certified Contractor Matrix</p>
        <div class="mt-12">
            <a href="#portal" class="bg-white text-slate-900 px-10 py-4 rounded-full font-black text-xs uppercase hover:bg-cyan-400 transition shadow-2xl">Start Qualification</a>
        </div>
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
                            <option value="Build Home">Complete Home Build</option>
                        </select>
                        <div id="winDiv" class="hidden">
                            <label class="text-[10px] font-black uppercase text-slate-400 ml-2 mb-2 block">Quantity of Units</label>
                            <select id="winCount" class="input-matrix">
                                <option value="">How many windows?</option>
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
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">02. Timing & Eligibility</h2>
                    <div class="space-y-6">
                        <select id="ready" class="input-matrix" required>
                            <option value="">Project Timeline</option>
                            <option value="ASAP">As Soon As Possible</option>
                            <option value="2-Months">Within 2 Months</option>
                        </select>
                        <select id="credit" class="input-matrix" required>
                            <option value="">Estimated Credit Rating</option>
                            <option value="Excellent (720+)">Excellent (720+)</option>
                            <option value="Good (660-719)">Good (660-719)</option>
                        </select>
                        <button type="button" onclick="goNext('step3')" class="btn-elite">Schedule Visit</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">03. Deployment Window</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                        <div><input type="date" id="appDate" class="input-matrix" required></div>
                        <div><select id="appTime" class="input-matrix"><option>Morning</option><option>Afternoon</option></select></div>
                    </div>
                    <button type="button" onclick="goNext('step4')" class="btn-elite">Final Details</button>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">04. Contact Protocol</h2>
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Legal Name" class="input-matrix" required>
                        <input type="tel" id="cPhone" placeholder="Phone Number" class="input-matrix" required>
                        <input type="email" id="cEmail" placeholder="Email Address" class="input-matrix" required>
                        <button type="submit" class="btn-elite bg-cyan-500 text-slate-900 shadow-xl shadow-cyan-100">Authorise & Get Quote</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section id="services" class="max-w-7xl mx-auto px-6 mb-32">
        <div class="text-center mb-16">
            <h3 class="text-4xl font-black italic uppercase">National Network Services</h3>
        </div>
        <div class="grid md:grid-cols-3 lg:grid-cols-4 gap-8">
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776549555727.jpeg" alt="Windows" class="rounded-2xl mb-4">
                <h4 class="font-black uppercase text-xs italic">Windows Matrix</h4>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776549622236.jpeg" alt="Doors" class="rounded-2xl mb-4">
                <h4 class="font-black uppercase text-xs italic">Security Entry Doors</h4>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776549716792.jpeg" alt="Roof" class="rounded-2xl mb-4">
                <h4 class="font-black uppercase text-xs italic">Roofing Elite</h4>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776549781247.jpeg" alt="Solar" class="rounded-2xl mb-4">
                <h4 class="font-black uppercase text-xs italic">Solar Matrix</h4>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776549862258.jpeg" alt="Kitchen" class="rounded-2xl mb-4">
                <h4 class="font-black uppercase text-xs italic">Kitchen Remodel</h4>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776549917709.jpeg" alt="Bathroom" class="rounded-2xl mb-4">
                <h4 class="font-black uppercase text-xs italic">Bathroom Remodel</h4>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776549990293.jpeg" alt="Deck" class="rounded-2xl mb-4">
                <h4 class="font-black uppercase text-xs italic">Deck Remodel</h4>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776550066723.jpeg" alt="Garage" class="rounded-2xl mb-4">
                <h4 class="font-black uppercase text-xs italic">Garage Matrix</h4>
            </div>
        </div>
    </section>

    <footer class="bg-slate-900 py-12 text-white/70 px-6 text-center">
        <img src="https://raw.githubusercontent.com/U-S-H/PRIMESOLUTIONS/main/WA_1776550450872.jpeg" alt="Logo" class="h-10 mx-auto mb-6">
        <p class="text-[9px] font-black uppercase tracking-[0.5em]">U.S. HOME IMPROVEMENTS • 2026</p>
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

        function goNext(nextId) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(nextId).classList.add('active');
        }

        function handleServiceSelection() {
            const svc = document.getElementById('service').value;
            document.getElementById('winDiv').classList.toggle('hidden', svc !== 'Windows');
        }

        document.getElementById('masterLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const leadData = {
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                service: document.getElementById('service').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(leadData).then(() => {
                alert("QUALIFIED!");
                location.reload();
            });
        });
    </script>
</body>
</html>
