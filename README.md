<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e40af; --accent: #06b6d4; --dark: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: var(--dark); scroll-behavior: smooth; }

        .glass-container {
            background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(30px);
            border-radius: 2.5rem; border: 1px solid #f1f5f9; box-shadow: 0 50px 100px -20px rgba(0,0,0,0.1);
        }

        .step { display: none; }
        .step.active { display: block; animation: slideUp 0.6s cubic-bezier(0.16, 1, 0.3, 1); }
        @keyframes slideUp { from { opacity: 0; transform: translateY(40px); } to { opacity: 1; transform: translateY(0); } }

        .input-premium {
            width: 100%; padding: 1.2rem; border-radius: 1.25rem; border: 2px solid #f1f5f9;
            font-weight: 700; transition: 0.3s; background: #fff; outline: none;
        }
        .input-premium:focus { border-color: var(--accent); box-shadow: 0 0 25px rgba(6, 182, 212, 0.1); }

        .btn-action {
            background: var(--dark); color: white; padding: 1.4rem; border-radius: 1.25rem;
            font-weight: 800; text-transform: uppercase; letter-spacing: 2px; width: 100%; transition: 0.4s;
        }
        .btn-action:hover { background: var(--primary); transform: translateY(-3px); box-shadow: 0 15px 30px rgba(30, 64, 175, 0.2); }

        .card-pro {
            background: white; border-radius: 2.5rem; border: 1px solid #f1f5f9; transition: 0.5s; overflow: hidden;
        }
        .card-pro:hover { border-color: var(--accent); transform: translateY(-10px); }
        .card-pro img { width: 100%; height: 280px; object-fit: cover; }
    </style>
</head>
<body>

    <header class="py-24 text-center px-6 bg-slate-50/50 border-b border-slate-100 relative overflow-hidden">
        <div class="relative z-10">
            <img src="./WA_1776550450872.jpeg" alt="Logo" class="h-24 w-24 mx-auto rounded-full border-4 border-white shadow-2xl mb-8">
            <h1 onclick="handleAdminTap()" class="cursor-pointer select-none text-5xl md:text-8xl font-extrabold tracking-tighter uppercase leading-none mb-4">
                U.S. HOME<br><span class="text-blue-700">IMPROVEMENT</span>
            </h1>
            <p class="text-[11px] font-black tracking-[0.8em] text-slate-400 uppercase">National Certified Appointment Matrix</p>
        </div>
        <div class="absolute top-0 right-0 w-80 h-80 bg-cyan-100 rounded-full filter blur-3xl opacity-30 -mr-20 -mt-20"></div>
    </header>

    <section class="max-w-3xl mx-auto -mt-20 px-4 mb-32 relative z-20">
        <div class="glass-container p-10 md:p-16 border-t-[14px] border-blue-700">
            <div class="text-center mb-12">
                <span class="bg-blue-50 text-blue-700 px-5 py-2 rounded-full text-[10px] font-black uppercase tracking-widest">Free Consultation & Quote Hub</span>
            </div>

            <form id="ultimateForm">
                <div class="step active" id="step1">
                    <h3 class="text-xs font-black text-slate-400 uppercase mb-6 tracking-widest">01. Project Identity</h3>
                    <div class="space-y-6">
                        <select id="service" class="input-premium" required>
                            <option value="">Choose Service Path...</option>
                            <option value="Windows">Replacement Windows (Energy Star)</option>
                            <option value="Roofing">Architectural Roofing Systems</option>
                            <option value="Doors">High-Security Entry Doors</option>
                            <option value="Solar">Solar Energy Deployment</option>
                            <option value="Kitchen">Kitchen Luxury Remodel</option>
                            <option value="Bathroom">Luxury Bath Matrix</option>
                        </select>
                        <input type="text" id="cName" placeholder="Full Legal Name" class="input-premium" required>
                        <input type="email" id="cEmail" placeholder="Professional Email Address" class="input-premium" required>
                        <button type="button" onclick="goNext('step2')" class="btn-action">Verify Location</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h3 class="text-xs font-black text-slate-400 uppercase mb-6 tracking-widest">02. Eligibility & Location</h3>
                    <div class="space-y-6">
                        <input type="text" id="address" placeholder="Residential Street Address" class="input-premium" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="text" id="cZip" placeholder="Zip Code" class="input-premium" required>
                            <select id="owner" class="input-premium" required>
                                <option value="">Ownership?</option>
                                <option value="Homeowner">Homeowner</option>
                                <option value="Tenant">Tenant</option>
                            </select>
                        </div>
                        <select id="credit" class="input-premium" required>
                            <option value="">Credit Profile Rating</option>
                            <option value="Excellent">720+ (Excellent)</option>
                            <option value="Good">660-719 (Standard)</option>
                            <option value="Fair">Fair Profile</option>
                        </select>
                        <button type="button" onclick="goNext('step3')" class="btn-action">Select Schedule</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h3 class="text-xs font-black text-slate-400 uppercase mb-6 tracking-widest">03. Consultation Schedule</h3>
                    <div class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div>
                                <label class="text-[10px] font-black text-slate-400 uppercase mb-2 block">Available Date</label>
                                <input type="date" id="appDate" class="input-premium" required>
                            </div>
                            <div>
                                <label class="text-[10px] font-black text-slate-400 uppercase mb-2 block">Available Window</label>
                                <select id="appTime" class="input-premium" required>
                                    <option value="Morning">Morning (8AM - 12PM)</option>
                                    <option value="Afternoon">Afternoon (12PM - 4PM)</option>
                                    <option value="Evening">Evening (4PM - 7PM)</option>
                                </select>
                            </div>
                        </div>
                        <input type="tel" id="cPhone" placeholder="Mobile Contact Protocol" class="input-premium" required>
                        <button type="submit" class="btn-action bg-blue-700">Authorize Appointment</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 mb-32">
        <div class="text-center mb-16">
            <h3 class="text-4xl font-black italic uppercase">Nationwide Certified Solutions</h3>
            <div class="h-1.5 w-24 bg-blue-700 mx-auto mt-4"></div>
        </div>
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-12">
            <div class="card-pro"><img src="./WA_1776549555727.jpeg"><div class="p-8"><h4 class="font-black text-sm uppercase text-blue-700 mb-2">Elite Windows</h4><p class="text-xs font-bold text-slate-400 uppercase leading-relaxed">Energy Star certified triple-pane matrix.</p></div></div>
            <div class="card-pro"><img src="./WA_1776549622236.jpeg"><div class="p-8"><h4 class="font-black text-sm uppercase text-blue-700 mb-2">Security Doors</h4><p class="text-xs font-bold text-slate-400 uppercase leading-relaxed">High-impact steel-reinforced entry systems.</p></div></div>
            <div class="card-pro"><img src="./WA_1776549716792.jpeg"><div class="p-8"><h4 class="font-black text-sm uppercase text-blue-700 mb-2">Premier Roofing</h4><p class="text-xs font-bold text-slate-400 uppercase leading-relaxed">Lifetime architectural shingle protection.</p></div></div>
            <div class="card-pro"><img src="./WA_1776549781247.jpeg"><div class="p-8"><h4 class="font-black text-sm uppercase text-blue-700 mb-2">Solar Hub</h4><p class="text-xs font-bold text-slate-400 uppercase leading-relaxed">Residential solar deployment & tax matrix.</p></div></div>
            <div class="card-pro"><img src="./WA_1776549862258.jpeg"><div class="p-8"><h4 class="font-black text-sm uppercase text-blue-700 mb-2">Kitchen Luxury</h4><p class="text-xs font-bold text-slate-400 uppercase leading-relaxed">Custom cabinetry & artisan quartz surfacing.</p></div></div>
            <div class="card-pro"><img src="./WA_1776549917709.jpeg"><div class="p-8"><h4 class="font-black text-sm uppercase text-blue-700 mb-2">Spa Renovations</h4><p class="text-xs font-bold text-slate-400 uppercase leading-relaxed">High-end bath conversions & tile design.</p></div></div>
        </div>
    </section>

    <footer class="bg-slate-950 py-24 text-center px-6 text-white/40">
        <div class="flex justify-center gap-10 mb-10 text-[10px] font-black uppercase tracking-[0.4em]">
            <button onclick="toggleM('privacy')">Privacy</button>
            <button onclick="toggleM('terms')">Terms</button>
            <button onclick="toggleM('standards')">Standards</button>
        </div>
        <p class="text-[9px] font-bold tracking-[0.7em] uppercase">U.S. HOME IMPROVEMENT • NATIONAL HQ • 2026</p>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[9000] p-6 hidden overflow-y-auto">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center border-b border-slate-100 pb-8 mb-12">
                <h2 class="text-4xl font-black uppercase italic tracking-tighter">HQ Lead Matrix</h2>
                <button onclick="closeAdmin()" class="bg-red-50 text-red-500 font-black text-[10px] px-6 py-3 rounded-full uppercase">Disconnect</button>
            </div>
            <div id="auth" class="text-center py-20">
                <input type="password" id="pin" class="input-premium max-w-xs text-center text-5xl mb-6 border-slate-200" placeholder="****">
                <button onclick="unlock()" class="btn-action max-w-xs mx-auto block">Authorize Matrix Access</button>
            </div>
            <div id="leads" class="hidden space-y-8 pb-32"></div>
        </div>
    </div>

    <div id="modal" class="fixed inset-0 bg-black/90 z-[9999] hidden items-center justify-center p-6" onclick="closeM()">
        <div class="bg-white p-12 rounded-[3rem] max-w-xl w-full" onclick="event.stopPropagation()">
            <div id="mContent"></div>
            <button onclick="closeM()" class="btn-action mt-10">Return to Portal</button>
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

        document.getElementById('ultimateForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('service').value,
                name: document.getElementById('cName').value,
                email: document.getElementById('cEmail').value,
                address: document.getElementById('address').value,
                zip: document.getElementById('cZip').value,
                owner: document.getElementById('owner').value,
                credit: document.getElementById('credit').value,
                appDate: document.getElementById('appDate').value,
                appTime: document.getElementById('appTime').value,
                phone: document.getElementById('cPhone').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                alert("AUTHORIZATION COMPLETE! Your Specialist Appointment is Set.");
                location.reload();
            });
        });

        // Secret Admin Protocol
        let taps = 0, timer;
        function handleAdminTap() {
            taps++; clearTimeout(timer);
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
                const leads = snap.val(); let html = '';
                for(let k in leads) {
                    html += `<div class="p-10 border border-slate-100 rounded-[3rem] bg-white shadow-xl flex flex-col lg:flex-row justify-between items-start lg:items-center gap-8">
                        <div class="flex-1 space-y-4">
                            <div class="flex flex-wrap gap-2">
                                <span class="bg-blue-600 text-white px-4 py-1 rounded-full text-[9px] font-black uppercase tracking-tighter">${leads[k].service}</span>
                                <span class="bg-cyan-50 text-cyan-700 px-4 py-1 rounded-full text-[9px] font-black uppercase tracking-tighter">📅 ${leads[k].appDate} | ${leads[k].appTime}</span>
                            </div>
                            <h4 class="text-3xl font-black text-slate-900 leading-none">${leads[k].name}</h4>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-x-12 gap-y-2 text-[11px] font-bold text-slate-400 uppercase tracking-tight">
                                <p>📧 Email: <span class="text-slate-900">${leads[k].email}</span></p>
                                <p>📞 Phone: <span class="text-slate-900">${leads[k].phone}</span></p>
                                <p class="md:col-span-2">📍 Address: <span class="text-slate-900">${leads[k].address}, ${leads[k].zip}</span></p>
                                <p>🏠 Status: <span class="text-slate-900">${leads[k].owner}</span></p>
                                <p>💳 Credit: <span class="text-blue-600">${leads[k].credit}</span></p>
                            </div>
                        </div>
                        <button onclick="del('${k}')" class="text-red-500 font-black text-[10px] border-2 border-red-50 px-10 py-5 rounded-3xl hover:bg-red-500 hover:text-white transition-all">DELETE ENTRY</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = html || '<p class="text-center font-black text-slate-200 py-40 uppercase">No Data in Matrix</p>';
            });
        }
        function del(id) { if(confirm('Permanent Delete?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }

        // Legal Modals
        const mText = {
            privacy: '<h3 class="text-3xl font-black italic uppercase mb-6">Privacy Policy</h3><p class="text-xs font-bold uppercase text-slate-400 leading-relaxed">Enterprise encryption protocols active. Your personal project data is never shared outside the certified network.</p>',
            terms: '<h3 class="text-3xl font-black italic uppercase mb-6">Terms of Service</h3><p class="text-xs font-bold uppercase text-slate-400 leading-relaxed">Quotes are subject to final on-site verification by a certified technician. Appointments must be confirmed via mobile contact.</p>',
            standards: '<h3 class="text-3xl font-black italic uppercase mb-6">Our Standards</h3><p class="text-xs font-bold uppercase text-slate-400 leading-relaxed">1. National Certification Only<br>2. Energy Star Compliant<br>3. Lifetime Transferrable Warranties</p>'
        };
        function toggleM(t) { document.getElementById('mContent').innerHTML = mText[t]; document.getElementById('modal').style.display = 'flex'; }
        function closeM() { document.getElementById('modal').style.display = 'none'; }
    </script>
</body>
</html>
