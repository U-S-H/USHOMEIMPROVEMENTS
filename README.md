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
        :root { --main-blue: #1e40af; --neon-cyan: #22d3ee; --slate-dark: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: var(--slate-dark); scroll-behavior: smooth; }

        .premium-glass {
            background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(20px);
            border-radius: 2.5rem; border: 1px solid #f1f5f9; box-shadow: 0 40px 100px -20px rgba(0,0,0,0.1);
        }

        .step { display: none; }
        .step.active { display: block; animation: slideIn 0.5s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }

        .input-pro {
            width: 100%; padding: 1.25rem; border-radius: 1.25rem; border: 2px solid #f1f5f9;
            font-weight: 700; transition: 0.3s; background: #fff; outline: none;
        }
        .input-pro:focus { border-color: var(--neon-cyan); box-shadow: 0 0 20px rgba(34, 211, 238, 0.15); }

        .btn-pro {
            background: var(--slate-dark); color: white; padding: 1.3rem; border-radius: 1.25rem;
            font-weight: 800; text-transform: uppercase; letter-spacing: 1px; width: 100%; transition: 0.4s;
        }
        .btn-pro:hover { background: var(--main-blue); transform: translateY(-3px); box-shadow: 0 10px 25px rgba(30, 64, 175, 0.3); }

        .service-card {
            background: white; border-radius: 2rem; border: 1px solid #f1f5f9; transition: 0.5s; overflow: hidden;
        }
        .service-card:hover { border-color: var(--neon-cyan); transform: translateY(-10px); }
        .service-card img { width: 100%; height: 260px; object-fit: cover; }
        
        .trust-hero { background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%); }
    </style>
</head>
<body>

    <header class="trust-hero py-24 text-center px-6 relative overflow-hidden">
        <div class="relative z-10">
            <img src="./WA_1776550450872.jpeg" alt="Logo" class="h-20 w-20 mx-auto rounded-full border-4 border-white shadow-2xl mb-8">
            <h1 onclick="handleAdminTap()" class="cursor-pointer select-none text-5xl md:text-8xl font-extrabold tracking-tighter uppercase leading-none mb-4">
                U.S. HOME<br><span class="text-blue-700">IMPROVEMENT</span>
            </h1>
            <p class="text-[10px] font-black tracking-[0.6em] text-slate-400 uppercase">Nationwide Certified Enterprise Matrix</p>
        </div>
        <div class="absolute top-0 right-0 w-96 h-96 bg-cyan-50 rounded-full filter blur-3xl opacity-40 -mr-20 -mt-20"></div>
    </header>

    <section id="portal" class="max-w-3xl mx-auto -mt-20 px-4 mb-32 relative z-20">
        <div class="premium-glass p-10 md:p-16 border-t-[12px] border-blue-700">
            <div class="text-center mb-10">
                <span class="bg-blue-50 text-blue-700 px-4 py-1 rounded-full text-[10px] font-black uppercase">Official Qualification Portal</span>
                <h2 class="text-3xl font-black italic uppercase mt-4">Project Verification</h2>
            </div>

            <form id="masterLeadForm">
                <div class="step active" id="step1">
                    <h3 class="font-black uppercase text-xs mb-6 text-slate-400">Step 01: Project Identity</h3>
                    <div class="space-y-6">
                        <select id="service" class="input-pro" required>
                            <option value="">Select Primary Service...</option>
                            <option value="Windows">Replacement Windows (Energy Star)</option>
                            <option value="Roofing">Architectural Roofing Matrix</option>
                            <option value="Doors">High-Security Entry Systems</option>
                            <option value="Solar">Residential Solar Deployment</option>
                            <option value="Kitchen">Professional Kitchen Remodel</option>
                            <option value="Bathroom">Luxury Bathroom Renovation</option>
                        </select>
                        <select id="owner" class="input-pro" required>
                            <option value="">Home Ownership Status?</option>
                            <option value="Owner">I am the Homeowner</option>
                            <option value="Renter">I am a Tenant</option>
                        </select>
                        <button type="button" onclick="goNext('step2')" class="btn-pro">Next: Property Status</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h3 class="font-black uppercase text-xs mb-6 text-slate-400">Step 02: Property Details</h3>
                    <div class="space-y-6">
                        <select id="homeType" class="input-pro" required>
                            <option value="">Property Type?</option>
                            <option value="Single Family">Single Family Home</option>
                            <option value="Townhome">Townhome / Condo</option>
                            <option value="Mobile Home">Mobile Home</option>
                        </select>
                        <select id="income" class="input-pro" required>
                            <option value="">Annual Household Income?</option>
                            <option value="$30k-$50k">$30,000 - $50,000</option>
                            <option value="$50k-$100k">$50,000 - $100,000</option>
                            <option value="$100k+">$100,000+</option>
                        </select>
                        <button type="button" onclick="goNext('step3')" class="btn-pro">Next: Financial Status</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h3 class="font-black uppercase text-xs mb-6 text-slate-400">Step 03: Financial Profile</h3>
                    <div class="space-y-6">
                        <select id="credit" class="input-pro" required>
                            <option value="">Estimated Credit Score</option>
                            <option value="Excellent">Excellent (720+)</option>
                            <option value="Good">Good (660-719)</option>
                            <option value="Fair">Fair (Below 660)</option>
                        </select>
                        <select id="timing" class="input-pro" required>
                            <option value="">Preferred Timeline?</option>
                            <option value="ASAP">Immediately (ASAP)</option>
                            <option value="1-3 Months">Within 1-3 Months</option>
                            <option value="Planning">Just Planning</option>
                        </select>
                        <button type="button" onclick="goNext('step4')" class="btn-pro">Final: Contact Info</button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h3 class="font-black uppercase text-xs mb-6 text-slate-400">Step 04: Authorization</h3>
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Legal Name" class="input-pro" required>
                        <input type="tel" id="cPhone" placeholder="Mobile Contact Protocol" class="input-pro" required>
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-pro" required>
                        <p class="text-[9px] text-slate-400 font-bold uppercase text-center mt-4 italic">Qualified by National Home Improvement Standards.</p>
                        <button type="submit" class="btn-pro bg-blue-700">Authorize Submission</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 mb-32">
        <div class="text-center mb-16">
            <h3 class="text-4xl font-black italic uppercase">Certified Project Matrix</h3>
            <div class="h-1 w-20 bg-blue-700 mx-auto mt-4"></div>
        </div>
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
            <div class="service-card"><img src="./WA_1776549555727.jpeg"><div class="p-6"><h4 class="font-black text-xs uppercase text-blue-700 mb-2">Energy Windows</h4><p class="text-[10px] font-bold text-slate-400 uppercase">Triple-pane UV matrix installation.</p></div></div>
            <div class="service-card"><img src="./WA_1776549622236.jpeg"><div class="p-6"><h4 class="font-black text-xs uppercase text-blue-700 mb-2">Security Doors</h4><p class="text-[10px] font-bold text-slate-400 uppercase">Steel-reinforced entry protocols.</p></div></div>
            <div class="service-card"><img src="./WA_1776549716792.jpeg"><div class="p-6"><h4 class="font-black text-xs uppercase text-blue-700 mb-2">Roofing Systems</h4><p class="text-[10px] font-bold text-slate-400 uppercase">Lifetime architectural shingles.</p></div></div>
            <div class="service-card"><img src="./WA_1776549781247.jpeg"><div class="p-6"><h4 class="font-black text-xs uppercase text-blue-700 mb-2">Solar Matrix</h4><p class="text-[10px] font-bold text-slate-400 uppercase">High-efficiency PV solar units.</p></div></div>
            <div class="service-card"><img src="./WA_1776549862258.jpeg"><div class="p-6"><h4 class="font-black text-xs uppercase text-blue-700 mb-2">Kitchen Hub</h4><p class="text-[10px] font-bold text-slate-400 uppercase">Custom luxury cabinetry & quartz.</p></div></div>
            <div class="service-card"><img src="./WA_1776549917709.jpeg"><div class="p-6"><h4 class="font-black text-xs uppercase text-blue-700 mb-2">Luxury Bath</h4><p class="text-[10px] font-bold text-slate-400 uppercase">Spa-grade renovation matrix.</p></div></div>
            <div class="service-card"><img src="./WA_1776549990293.jpeg"><div class="p-6"><h4 class="font-black text-xs uppercase text-blue-700 mb-2">Outdoor Decking</h4><p class="text-[10px] font-bold text-slate-400 uppercase">Weather-proof composite decks.</p></div></div>
            <div class="service-card"><img src="./WA_1776550066723.jpeg"><div class="p-6"><h4 class="font-black text-xs uppercase text-blue-700 mb-2">Garage Hub</h4><p class="text-[10px] font-bold text-slate-400 uppercase">Insulated high-performance doors.</p></div></div>
        </div>
    </section>

    <footer class="bg-slate-950 py-20 text-white px-6">
        <div class="max-w-6xl mx-auto text-center">
            <div class="flex flex-wrap justify-center gap-10 mb-16 text-[10px] font-black uppercase tracking-widest text-white/40">
                <button onclick="toggleModal('privacy')">Privacy Policy</button>
                <button onclick="toggleModal('terms')">Terms of Service</button>
                <button onclick="toggleModal('details')">Company Details</button>
            </div>
            <p class="text-[9px] font-bold tracking-[0.5em] text-white/10 uppercase">U.S. HOME IMPROVEMENT • NATIONAL ENTERPRISE • 2026</p>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-6 hidden overflow-y-auto">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center border-b pb-6 mb-10">
                <h2 class="text-3xl font-black uppercase italic">HQ Lead Matrix</h2>
                <button onclick="closeAdmin()" class="text-red-500 font-bold text-xs uppercase">Exit</button>
            </div>
            <div id="auth" class="text-center py-20">
                <input type="password" id="pin" class="input-pro max-w-xs text-center text-4xl mb-4" placeholder="****">
                <button onclick="unlock()" class="btn-pro max-w-xs mx-auto block">Authorize Access</button>
            </div>
            <div id="leads" class="hidden space-y-6"></div>
        </div>
    </div>

    <div id="modal" class="fixed inset-0 bg-black/80 z-[6000] hidden items-center justify-center p-6" onclick="closeModal()">
        <div class="bg-white p-10 rounded-[2.5rem] max-w-xl w-full" onclick="event.stopPropagation()">
            <div id="mContent"></div>
            <button onclick="closeModal()" class="btn-pro mt-8">Close Matrix</button>
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
            db.ref('leads').push({
                service: document.getElementById('service').value,
                owner: document.getElementById('owner').value,
                homeType: document.getElementById('homeType').value,
                income: document.getElementById('income').value,
                credit: document.getElementById('credit').value,
                timing: document.getElementById('timing').value,
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                zip: document.getElementById('cZip').value,
                timestamp: new Date().toLocaleString()
            }).then(() => { alert("QUALIFICATION GRANTED!"); location.reload(); });
        });

        // Admin Auth
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
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-8 border-2 border-slate-50 bg-white rounded-[2.5rem] shadow-sm mb-6 flex justify-between items-center">
                        <div class="space-y-2">
                            <span class="bg-blue-50 text-blue-700 px-3 py-1 rounded-full text-[9px] font-black uppercase">${data[k].service}</span>
                            <h4 class="text-2xl font-black text-slate-900">${data[k].name}</h4>
                            <div class="grid grid-cols-2 gap-x-10 gap-y-2 mt-4 text-[11px] font-bold text-slate-500 uppercase">
                                <p>📞 Phone: <span class="text-slate-900">${data[k].phone}</span></p>
                                <p>📍 Zip: <span class="text-slate-900">${data[k].zip}</span></p>
                                <p>🏠 Type: <span class="text-slate-900">${data[k].homeType}</span></p>
                                <p>💰 Income: <span class="text-slate-900">${data[k].income}</span></p>
                                <p>💳 Credit: <span class="text-blue-700">${data[k].credit}</span></p>
                                <p>🕒 Time: <span class="text-slate-900">${data[k].timing}</span></p>
                            </div>
                        </div>
                        <button onclick="del('${k}')" class="text-red-500 font-black text-[10px] border border-red-50 px-6 py-3 rounded-2xl hover:bg-red-500 hover:text-white transition-all">Delete</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = h || 'NO LEADS';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }

        // Modals
        const mData = {
            privacy: '<h3 class="text-2xl font-black mb-4">PRIVACY</h3><p class="text-xs font-bold uppercase text-slate-400">Military-grade encryption for all project data.</p>',
            terms: '<h3 class="text-2xl font-black mb-4">TERMS</h3><p class="text-xs font-bold uppercase text-slate-400">Quotes subject to site inspection by certified network partners.</p>',
            details: '<h3 class="text-2xl font-black mb-4">DETAILS</h3><p class="text-xs font-bold uppercase text-slate-400">National Headquarters Enterprise Network • Serving 50 States.</p>'
        };
        function toggleModal(t) { document.getElementById('mContent').innerHTML = mData[t]; document.getElementById('modal').style.display = 'flex'; }
        function closeModal() { document.getElementById('modal').style.display = 'none'; }
    </script>
</body>
</html>
