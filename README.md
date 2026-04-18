<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Certified Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon-blue: #00f2ff; --dark-slate: #0f172a; --trust-blue: #1d4ed8; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: var(--dark-slate); scroll-behavior: smooth; }

        /* Premium Soft Glow Header */
        .premium-header {
            background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
            position: relative; overflow: hidden; border-bottom: 1px solid #e2e8f0;
        }

        .glass-panel {
            background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(25px);
            border-radius: 2.5rem; border: 1px solid #f1f5f9; box-shadow: 0 50px 100px -20px rgba(0,0,0,0.1);
        }

        .step { display: none; }
        .step.active { display: block; animation: fadeIn 0.5s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .input-box {
            width: 100%; padding: 1.25rem; border-radius: 1.25rem; border: 2px solid #f1f5f9;
            font-weight: 600; transition: 0.3s; background: #fff;
        }
        .input-box:focus { border-color: var(--neon-blue); box-shadow: 0 0 20px rgba(0, 242, 255, 0.15); outline: none; }

        .btn-premium {
            background: var(--dark-slate); color: white; padding: 1.3rem; border-radius: 1.25rem;
            font-weight: 800; text-transform: uppercase; letter-spacing: 1px; width: 100%; transition: 0.4s;
        }
        .btn-premium:hover { background: var(--trust-blue); transform: translateY(-3px); box-shadow: 0 10px 25px rgba(29, 78, 216, 0.3); }

        .service-card {
            background: white; border-radius: 2rem; border: 1px solid #f1f5f9; transition: 0.4s; overflow: hidden;
        }
        .service-card:hover { border-color: var(--neon-blue); transform: translateY(-10px); box-shadow: 0 20px 40px rgba(0,0,0,0.05); }
        .service-card img { width: 100%; height: 240px; object-fit: cover; }

        .trust-badge { background: #f8fafc; border-radius: 1rem; padding: 1.5rem; border: 1px solid #e2e8f0; }
    </style>
</head>
<body>

    <header class="premium-header py-24 text-center px-6">
        <div class="relative z-10">
            <img src="./WA_1776550450872.jpeg" alt="Logo" class="h-20 w-20 mx-auto rounded-full border-4 border-white shadow-2xl mb-8">
            <h1 onclick="handleAdminTap()" class="cursor-pointer select-none text-5xl md:text-8xl font-extrabold tracking-tighter uppercase leading-none mb-4">
                U.S. HOME<br><span class="text-blue-600">IMPROVEMENT</span>
            </h1>
            <p class="text-xs font-black tracking-[0.6em] text-slate-400 uppercase">Nationwide Certified Contractor Network</p>
        </div>
        <div class="absolute top-0 right-0 w-96 h-96 bg-blue-50 rounded-full filter blur-3xl opacity-50 -mr-20 -mt-20"></div>
    </header>

    <section id="qualify" class="max-w-3xl mx-auto -mt-20 px-4 mb-32 relative z-20">
        <div class="glass-panel p-10 md:p-16 border-t-[10px] border-blue-600">
            <div class="text-center mb-10">
                <h2 class="text-3xl font-black italic uppercase">Project Qualification</h2>
                <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest mt-2">Verify eligibility for national rebates & savings</p>
            </div>

            <form id="leadForm">
                <div class="step active" id="step1">
                    <div class="space-y-6">
                        <select id="service" class="input-box" required>
                            <option value="">Select Priority Project...</option>
                            <option value="Windows">Replacement Windows (Energy Star)</option>
                            <option value="Roofing">Architectural Roofing Systems</option>
                            <option value="Doors">High-Security Entry Doors</option>
                            <option value="Solar">Residential Solar Matrix</option>
                            <option value="Kitchen">Premium Kitchen Remodel</option>
                            <option value="Bathroom">Luxury Bathroom Remodel</option>
                            <option value="Deck">Custom Outdoor Decking</option>
                            <option value="Garage">Advanced Garage Solutions</option>
                        </select>
                        <select id="owner" class="input-box" required>
                            <option value="">Do you own the property?</option>
                            <option value="Yes">Yes, I am the Homeowner</option>
                            <option value="No">No, I am a Tenant</option>
                        </select>
                        <button type="button" onclick="goNext('step2')" class="btn-premium">Check Availability</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <div class="space-y-6">
                        <select id="credit" class="input-box" required>
                            <option value="">Estimated Credit Rating</option>
                            <option value="Excellent">Excellent (720+)</option>
                            <option value="Good">Good (660-719)</option>
                            <option value="Fair">Fair (Below 660)</option>
                        </select>
                        <select id="timing" class="input-box" required>
                            <option value="">Installation Timeline</option>
                            <option value="Immediate">As Soon As Possible</option>
                            <option value="1-3 Months">Within 1-3 Months</option>
                            <option value="Researching">Just Researching</option>
                        </select>
                        <button type="button" onclick="goNext('step3')" class="btn-premium">Final Verification</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Name" class="input-box" required>
                        <input type="tel" id="cPhone" placeholder="Direct Contact Number" class="input-box" required>
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-box" required>
                        <p class="text-[9px] text-slate-400 font-bold uppercase text-center mt-4">By clicking authorize, you agree to our privacy protocols.</p>
                        <button type="submit" class="btn-premium bg-blue-600">Authorize & Get Quote</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 mb-32">
        <div class="grid md:grid-cols-4 gap-6 text-center">
            <div class="trust-badge">
                <h5 class="font-black text-xs uppercase mb-2">Nationwide Network</h5>
                <p class="text-[10px] text-slate-400 font-bold uppercase">Certified in 50 States</p>
            </div>
            <div class="trust-badge">
                <h5 class="font-black text-xs uppercase mb-2">Licensed & Bonded</h5>
                <p class="text-[10px] text-slate-400 font-bold uppercase">Full Liability Coverage</p>
            </div>
            <div class="trust-badge">
                <h5 class="font-black text-xs uppercase mb-2">Energy Star Partner</h5>
                <p class="text-[10px] text-slate-400 font-bold uppercase">Maximum Efficiency</p>
            </div>
            <div class="trust-badge">
                <h5 class="font-black text-xs uppercase mb-2">Zero-Down Plans</h5>
                <p class="text-[10px] text-slate-400 font-bold uppercase">Financing Available</p>
            </div>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 mb-32">
        <div class="text-center mb-16">
            <h3 class="text-4xl font-black italic uppercase">Specialized Solutions</h3>
            <div class="h-1 w-20 bg-blue-600 mx-auto mt-4"></div>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-10">
            <div class="service-card">
                <img src="./WA_1776549555727.jpeg">
                <div class="p-8">
                    <h4 class="font-black uppercase text-sm mb-2 text-blue-600">Energy Windows</h4>
                    <p class="text-xs text-slate-500 leading-relaxed font-bold uppercase">Triple-pane protection with UV shielding. Reduces energy bills by up to 35%.</p>
                </div>
            </div>
            <div class="service-card">
                <img src="./WA_1776549622236.jpeg">
                <div class="p-8">
                    <h4 class="font-black uppercase text-sm mb-2 text-blue-600">Security Doors</h4>
                    <p class="text-xs text-slate-500 leading-relaxed font-bold uppercase">Steel-reinforced entry systems with advanced locking matrix for maximum safety.</p>
                </div>
            </div>
            <div class="service-card">
                <img src="./WA_1776549716792.jpeg">
                <div class="p-8">
                    <h4 class="font-black uppercase text-sm mb-2 text-blue-600">Elite Roofing</h4>
                    <p class="text-xs text-slate-500 leading-relaxed font-bold uppercase">Architectural shingles with 50-year transferrable warranty. Hurricane-rated protection.</p>
                </div>
            </div>
            <div class="service-card">
                <img src="./WA_1776549781247.jpeg">
                <div class="p-8">
                    <h4 class="font-black uppercase text-sm mb-2 text-blue-600">Solar Matrix</h4>
                    <p class="text-xs text-slate-500 leading-relaxed font-bold uppercase">High-output PV panels. Achieve net-zero energy status and government tax credits.</p>
                </div>
            </div>
            <div class="service-card">
                <img src="./WA_1776549862258.jpeg">
                <div class="p-8">
                    <h4 class="font-black uppercase text-sm mb-2 text-blue-600">Kitchen Hub</h4>
                    <p class="text-xs text-slate-500 leading-relaxed font-bold uppercase">Custom cabinetry and premium quartz surfacing. Designed for modern luxury living.</p>
                </div>
            </div>
            <div class="service-card">
                <img src="./WA_1776549917709.jpeg">
                <div class="p-8">
                    <h4 class="font-black uppercase text-sm mb-2 text-blue-600">Luxury Bath</h4>
                    <p class="text-xs text-slate-500 leading-relaxed font-bold uppercase">Spa-grade renovations including walk-in conversions and high-end tile matrix.</p>
                </div>
            </div>
            <div class="service-card">
                <img src="./WA_1776549990293.jpeg">
                <div class="p-8">
                    <h4 class="font-black uppercase text-sm mb-2 text-blue-600">Outdoor Decks</h4>
                    <p class="text-xs text-slate-500 leading-relaxed font-bold uppercase">Weather-resistant composite decking. Expanding your lifestyle to the outdoors.</p>
                </div>
            </div>
            <div class="service-card">
                <img src="./WA_1776550066723.jpeg">
                <div class="p-8">
                    <h4 class="font-black uppercase text-sm mb-2 text-blue-600">Garage Matrix</h4>
                    <p class="text-xs text-slate-500 leading-relaxed font-bold uppercase">Insulated door systems and organizational flooring for high-performance storage.</p>
                </div>
            </div>
        </div>
    </section>

    <footer class="bg-slate-950 py-20 text-white px-6">
        <div class="max-w-6xl mx-auto text-center">
            <img src="./WA_1776550450872.jpeg" class="h-12 mx-auto mb-10 rounded-full border-2 border-white/20">
            <div class="flex flex-wrap justify-center gap-10 mb-16 text-[10px] font-black uppercase tracking-widest text-white/40">
                <button onclick="toggleM('privacy')">Privacy Policy</button>
                <button onclick="toggleM('terms')">Terms of Service</button>
                <button onclick="toggleM('about')">Company Standards</button>
            </div>
            <p class="text-[9px] font-bold tracking-[0.6em] text-white/10 uppercase">U.S. HOME IMPROVEMENT • NATIONAL ENTERPRISE NETWORK • 2026</p>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-6 hidden overflow-y-auto">
        <div class="max-w-5xl mx-auto">
            <div class="flex justify-between items-center border-b pb-6 mb-10">
                <h2 class="text-3xl font-black uppercase italic">HQ Lead Matrix</h2>
                <button onclick="closeAdmin()" class="text-red-500 font-bold text-xs uppercase">Close Panel</button>
            </div>
            <div id="auth" class="text-center py-20">
                <input type="password" id="pin" class="input-box max-w-xs text-center text-4xl mb-4" placeholder="****">
                <button onclick="unlock()" class="btn-premium max-w-xs mx-auto block">Access Matrix</button>
            </div>
            <div id="leads" class="hidden space-y-4"></div>
        </div>
    </div>

    <div id="modal" class="fixed inset-0 bg-black/80 z-[6000] hidden items-center justify-center p-6" onclick="closeM()">
        <div class="bg-white p-10 rounded-[2.5rem] max-w-xl w-full" onclick="event.stopPropagation()">
            <div id="mContent"></div>
            <button onclick="closeM()" class="btn-premium mt-8">Close Matrix</button>
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

        document.getElementById('leadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            db.ref('leads').push({
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                service: document.getElementById('service').value,
                zip: document.getElementById('cZip').value,
                credit: document.getElementById('credit').value,
                timestamp: new Date().toLocaleString()
            }).then(() => { alert("QUALIFICATION AUTHORIZED!"); location.reload(); });
        });

        // Admin
        let taps = 0;
        let timer;
        function handleAdminTap() {
            taps++;
            clearTimeout(timer);
            if(taps === 4) { document.getElementById('adminPanel').classList.remove('hidden'); taps=0; }
            timer = setTimeout(() => taps = 0, 1500);
        }
        function unlock() {
            if(document.getElementById('pin').value === "786") {
                document.getElementById('auth').classList.add('hidden');
                document.getElementById('leads').classList.remove('hidden');
                sync();
            }
        }
        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val();
                let h = '';
                for(let k in data) {
                    h += `<div class="p-6 border-2 border-slate-50 rounded-3xl flex justify-between items-center shadow-sm">
                        <div>
                            <p class="text-[10px] font-black text-blue-600 uppercase">${data[k].service}</p>
                            <h4 class="font-extrabold text-xl">${data[k].name}</h4>
                            <p class="text-xs font-bold text-slate-400 uppercase">${data[k].phone} | ${data[k].zip} | ${data[k].credit}</p>
                        </div>
                        <button onclick="del('${k}')" class="text-red-500 font-black text-[10px] uppercase border border-red-100 px-4 py-2 rounded-full">Delete</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = h || 'NO LEADS';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }

        // Modals
        const mBody = {
            privacy: '<h3 class="text-2xl font-black mb-4">PRIVACY</h3><p class="text-xs font-bold uppercase leading-relaxed text-slate-400">Your data is encrypted using military-grade protocols. We never sell your project identity to outside matrix entities.</p>',
            terms: '<h3 class="text-2xl font-black mb-4">TERMS</h3><p class="text-xs font-bold uppercase leading-relaxed text-slate-400">All quotes are subject to site inspection. U.S. Home Improvement connects certified network partners to qualified homeowners.</p>',
            about: '<h3 class="text-2xl font-black mb-4">STANDARDS</h3><p class="text-xs font-bold uppercase leading-relaxed text-slate-400">1. Certified Network Only<br>2. Guaranteed Labor<br>3. Premium Grade Materials<br>4. Nationwide Warranty Coverage</p>'
        };
        function toggleM(t) { document.getElementById('mContent').innerHTML = mBody[t]; document.getElementById('modal').style.display = 'flex'; }
        function closeM() { document.getElementById('modal').style.display = 'none'; }
    </script>
</body>
</html>
