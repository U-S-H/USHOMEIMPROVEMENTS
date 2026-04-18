<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Excellence</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --premium-blue: #0f172a; --accent-pink: #ff007a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: var(--premium-blue); scroll-behavior: smooth; }

        /* Smooth Neon Slide Header */
        .neon-hero {
            background: linear-gradient(-45deg, #f8fafc, #e2e8f0, #f1f5f9, #ffffff);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            border-bottom: 1px solid #e2e8f0;
        }
        @keyframes gradientBG { 0% {background-position: 0% 50%;} 50% {background-position: 100% 50%;} 100% {background-position: 0% 50%;} }

        .glass-card {
            background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(20px);
            border-radius: 2rem; border: 1px solid #e2e8f0; box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.05);
        }

        .step { display: none; }
        .step.active { display: block; animation: slideUp 0.5s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .input-premium {
            width: 100%; padding: 1.2rem; border-radius: 1rem; border: 2px solid #f1f5f9;
            font-weight: 600; outline: none; transition: 0.3s;
        }
        .input-premium:focus { border-color: var(--neon); box-shadow: 0 0 15px rgba(0, 242, 255, 0.2); }

        .btn-action {
            background: var(--premium-blue); color: white; padding: 1.2rem; border-radius: 1rem;
            font-weight: 800; text-transform: uppercase; letter-spacing: 1px; transition: 0.4s;
        }
        .btn-action:hover { background: var(--neon); color: var(--premium-blue); transform: scale(1.02); }

        .service-box {
            background: white; border-radius: 1.5rem; border: 1px solid #f1f5f9; transition: 0.4s; overflow: hidden;
        }
        .service-box:hover { border-color: var(--neon); transform: translateY(-10px); }
        .service-box img { width: 100%; height: 200px; object-fit: cover; }

        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.7); z-index: 1000; align-items: center; justify-content: center; padding: 20px; }
        .modal-box { background: white; padding: 40px; border-radius: 2rem; max-width: 600px; width: 100%; max-height: 80vh; overflow-y: auto; }
    </style>
</head>
<body>

    <header class="neon-hero min-h-[60vh] flex flex-col items-center justify-center text-center px-6 relative overflow-hidden">
        <h1 onclick="handleAdminTap()" class="cursor-default select-none text-4xl md:text-7xl font-extrabold tracking-tighter uppercase leading-none z-10">
            U.S. HOME<br><span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-500 to-blue-600">IMPROVEMENT</span>
        </h1>
        <div class="mt-8 z-10">
            <img src="./WA_1776550450872.jpeg" alt="Logo" class="h-16 w-16 mx-auto rounded-full border-4 border-white shadow-xl mb-4">
            <p class="text-[10px] font-black tracking-[0.6em] uppercase text-slate-400">Nationwide Excellence Matrix 2026</p>
        </div>
        
        <div class="absolute top-10 left-10 w-64 h-64 bg-cyan-100 rounded-full mix-blend-multiply filter blur-3xl opacity-30 animate-pulse"></div>
        <div class="absolute bottom-10 right-10 w-64 h-64 bg-blue-100 rounded-full mix-blend-multiply filter blur-3xl opacity-30 animate-pulse"></div>
    </header>

    <section id="portal" class="max-w-2xl mx-auto -mt-20 px-4 mb-24 relative z-20">
        <div class="glass-card p-8 md:p-12">
            <form id="masterForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-extrabold mb-6 uppercase">01. Select Service</h2>
                    <div class="space-y-4">
                        <select id="service" class="input-premium" required>
                            <option value="">Choose Upgrade Path...</option>
                            <option value="Windows">Windows Replacement</option>
                            <option value="Doors">Entry Doors</option>
                            <option value="Roofing">Roofing Matrix</option>
                            <option value="Solar">Solar Deployment</option>
                            <option value="Kitchen">Kitchen Remodel</option>
                            <option value="Bathroom">Bathroom Remodel</option>
                        </select>
                        <button type="button" onclick="goNext('step2')" class="btn-action w-full">Next Step</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-extrabold mb-6 uppercase">02. Verify Identity</h2>
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Name" class="input-premium" required>
                        <input type="tel" id="cPhone" placeholder="Phone Number" class="input-premium" required>
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-premium" required>
                        <button type="submit" class="btn-action w-full bg-cyan-500 !text-slate-900">Authorize Quote</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-6xl mx-auto px-6 mb-24">
        <div class="grid md:grid-cols-3 gap-8 text-center">
            <div class="p-6">
                <div class="text-3xl mb-4">🏠</div>
                <h4 class="font-bold uppercase text-sm tracking-widest">Lifetime Guarantee</h4>
                <p class="text-xs text-slate-400 mt-2">Premium quality materials backed by our national warranty matrix.</p>
            </div>
            <div class="p-6">
                <div class="text-3xl mb-4">💳</div>
                <h4 class="font-bold uppercase text-sm tracking-widest">Zero Down Financing</h4>
                <p class="text-xs text-slate-400 mt-2">Flexible payment protocols tailored to your credit profile.</p>
            </div>
            <div class="p-6">
                <div class="text-3xl mb-4">✅</div>
                <h4 class="font-bold uppercase text-sm tracking-widest">Certified Experts</h4>
                <p class="text-xs text-slate-400 mt-2">Licensed, bonded, and fully insured field technicians.</p>
            </div>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 mb-32">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
            <div class="service-box"><img src="./WA_1776549555727.jpeg"><p class="p-4 font-bold text-xs uppercase">Windows</p></div>
            <div class="service-box"><img src="./WA_1776549622236.jpeg"><p class="p-4 font-bold text-xs uppercase">Doors</p></div>
            <div class="service-box"><img src="./WA_1776549716792.jpeg"><p class="p-4 font-bold text-xs uppercase">Roofing</p></div>
            <div class="service-box"><img src="./WA_1776549781247.jpeg"><p class="p-4 font-bold text-xs uppercase">Solar</p></div>
        </div>
    </section>

    <footer class="bg-slate-900 py-16 text-white/50 text-center px-6">
        <div class="flex justify-center gap-8 mb-8 text-[10px] font-bold uppercase tracking-widest">
            <button onclick="openModal('privacy')" class="hover:text-white">Privacy Policy</button>
            <button onclick="openModal('terms')" class="hover:text-white">Terms of Service</button>
            <button onclick="openModal('details')" class="hover:text-white">Company Details</button>
        </div>
        <p class="text-[9px] font-black tracking-[0.5em] uppercase">U.S. HOME IMPROVEMENT • 2026 • ESTABLISHED NETWORK</p>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-6 hidden overflow-y-auto">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-between items-center mb-10 border-b pb-6">
                <h2 class="text-3xl font-black uppercase italic">HQ Lead Matrix</h2>
                <button onclick="closeAdmin()" class="text-red-500 font-bold uppercase text-xs">Close HQ</button>
            </div>
            <div id="authBox" class="text-center py-20">
                <input type="password" id="pinInput" class="input-premium max-w-xs text-center text-4xl mb-4" placeholder="****">
                <button onclick="verifyAdmin()" class="btn-action w-full max-w-xs mx-auto block">Access Leads</button>
            </div>
            <div id="leadContainer" class="hidden space-y-4"></div>
        </div>
    </div>

    <div id="modal" class="modal" onclick="closeModal()">
        <div class="modal-box" onclick="event.stopPropagation()">
            <div id="modalBody"></div>
            <button onclick="closeModal()" class="btn-action w-full mt-8">Close Matrix</button>
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

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            db.ref('leads').push({
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                service: document.getElementById('service').value,
                zip: document.getElementById('cZip').value,
                timestamp: new Date().toLocaleString()
            }).then(() => { alert("Submission Authorized!"); location.reload(); });
        });

        // Modals
        const mData = {
            privacy: '<h3 class="text-2xl font-black mb-4">PRIVACY POLICY</h3><p class="text-xs font-bold leading-relaxed uppercase">We use advanced encryption protocols to secure your project data. Your information is never sold to 3rd party marketers.</p>',
            terms: '<h3 class="text-2xl font-black mb-4">TERMS OF SERVICE</h3><p class="text-xs font-bold leading-relaxed uppercase">U.S. Home Improvement acts as a national network connecting homeowners with certified installers. Quotes are subject to on-site verification.</p>',
            details: '<h3 class="text-2xl font-black mb-4">COMPANY DETAILS</h3><p class="text-xs font-bold leading-relaxed uppercase">National Headquarters: Enterprise Division<br>Status: Certified Network 2026<br>Coverage: 50 States Continental US</p>'
        };
        function openModal(type) { document.getElementById('modalBody').innerHTML = mData[type]; document.getElementById('modal').style.display = 'flex'; }
        function closeModal() { document.getElementById('modal').style.display = 'none'; }

        // ADMIN LOGIC
        let tapCount = 0;
        let tapTimer;
        function handleAdminTap() {
            tapCount++;
            clearTimeout(tapTimer);
            if(tapCount === 4) {
                document.getElementById('adminPanel').classList.remove('hidden');
                tapCount = 0;
            }
            tapTimer = setTimeout(() => tapCount = 0, 1500);
        }

        function verifyAdmin() {
            if(document.getElementById('pinInput').value === "786") {
                document.getElementById('authBox').classList.add('hidden');
                document.getElementById('leadContainer').classList.remove('hidden');
                syncLeads();
            }
        }

        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const data = snap.val();
                let html = '';
                for(let k in data) {
                    html += `<div class="p-6 border rounded-2xl flex justify-between items-center shadow-sm">
                        <div>
                            <p class="text-[10px] font-black text-cyan-500 uppercase">${data[k].service}</p>
                            <h4 class="font-bold text-xl">${data[k].name}</h4>
                            <p class="text-xs font-bold text-slate-400">${data[k].phone} | ZIP: ${data[k].zip}</p>
                        </div>
                        <button onclick="delLead('${k}')" class="text-red-500 text-[10px] font-black border border-red-100 px-4 py-2 rounded-full hover:bg-red-50">DELETE</button>
                    </div>`;
                }
                document.getElementById('leadContainer').innerHTML = html || 'NO LEADS IN MATRIX';
            });
        }
        function delLead(id) { if(confirm('Delete this record?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
    </script>
</body>
</html>
