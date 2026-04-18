<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Matrix</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --brand: #1e40af; --accent: #0ea5e9; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; margin: 0; padding: 0; }
        
        .hero-gradient { background: linear-gradient(135deg, #1e40af 0%, #0369a1 100%); }
        
        .step-container { display: none; }
        .step-container.active { display: block; animation: fadeIn 0.5s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .glass-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 2rem;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.1);
        }

        .input-field {
            width: 100%; padding: 1rem; border-radius: 1rem; border: 2px solid #e2e8f0;
            font-weight: 600; outline: none; transition: 0.3s;
        }
        .input-field:focus { border-color: var(--brand); box-shadow: 0 0 0 4px rgba(30, 64, 175, 0.1); }

        .primary-btn {
            background: var(--brand); color: white; padding: 1.2rem; border-radius: 1rem;
            font-weight: 800; text-transform: uppercase; letter-spacing: 1px; width: 100%; transition: 0.3s;
        }
        .primary-btn:hover { background: #1e3a8a; transform: translateY(-2px); }
    </style>
</head>
<body>

    <nav class="bg-white border-b sticky top-0 z-50 py-4 px-6 flex justify-between items-center">
        <div class="flex items-center gap-2">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-full border shadow-sm">
            <span onclick="handleAdminTap()" class="font-extrabold tracking-tighter uppercase text-sm cursor-pointer select-none">U.S. Home Improvement</span>
        </div>
        <div class="text-[10px] font-bold text-blue-600 uppercase tracking-widest hidden md:block">Verified Enterprise 2026</div>
    </nav>

    <header class="hero-gradient py-16 text-center px-6 text-white">
        <h1 class="text-4xl md:text-6xl font-extrabold tracking-tight mb-4 uppercase">Quality Excellence</h1>
        <p class="text-blue-100 text-xs font-bold uppercase tracking-[0.4em]">National Certified Contractor Network</p>
    </header>

    <main class="max-w-xl mx-auto -mt-12 px-4 mb-20">
        <div class="glass-card p-8 md:p-12">
            <div id="formStatus" class="text-center mb-8">
                <span class="bg-blue-100 text-blue-700 px-4 py-1 rounded-full text-[10px] font-black uppercase">Official Quote Portal</span>
            </div>

            <form id="mainLeadForm">
                <div class="step-container active" id="step1">
                    <div class="space-y-4">
                        <select id="service" class="input-field" required>
                            <option value="">Choose Service...</option>
                            <option value="Windows">Replacement Windows</option>
                            <option value="Roofing">Architectural Roofing</option>
                            <option value="Solar">Solar Energy Matrix</option>
                            <option value="Kitchen">Kitchen Remodeling</option>
                            <option value="Bathroom">Bathroom Renovation</option>
                        </select>
                        <input type="text" id="cName" placeholder="Full Legal Name" class="input-field" required>
                        <input type="email" id="cEmail" placeholder="Email Address" class="input-field" required>
                        <button type="button" onclick="nextStep('step2')" class="primary-btn">Next: Location</button>
                    </div>
                </div>

                <div class="step-container" id="step2">
                    <div class="space-y-4">
                        <input type="text" id="address" placeholder="Street Address" class="input-field" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="text" id="cZip" placeholder="Zip Code" class="input-field" required>
                            <select id="owner" class="input-field" required>
                                <option value="">Ownership?</option>
                                <option value="Homeowner">Homeowner</option>
                                <option value="Tenant">Tenant</option>
                            </select>
                        </div>
                        <select id="credit" class="input-field" required>
                            <option value="">Credit Score?</option>
                            <option value="Excellent">720+ Excellent</option>
                            <option value="Good">660-719 Good</option>
                            <option value="Fair">Fair Profile</option>
                        </select>
                        <button type="button" onclick="nextStep('step3')" class="primary-btn">Next: Schedule</button>
                    </div>
                </div>

                <div class="step-container" id="step3">
                    <div class="space-y-4">
                        <div class="grid grid-cols-2 gap-4">
                            <input type="date" id="appDate" class="input-field" required>
                            <select id="appTime" class="input-field" required>
                                <option value="Morning">Morning</option>
                                <option value="Afternoon">Afternoon</option>
                                <option value="Evening">Evening</option>
                            </select>
                        </div>
                        <input type="tel" id="cPhone" placeholder="Phone Number" class="input-field" required>
                        <button type="submit" class="primary-btn !bg-blue-700">Authorize Quote</button>
                    </div>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-5xl mx-auto px-6 grid grid-cols-2 md:grid-cols-4 gap-6 mb-20">
        <div class="bg-white p-4 rounded-3xl border text-center shadow-sm">
            <img src="./WA_1776549555727.jpeg" class="rounded-2xl mb-4 w-full h-32 object-cover">
            <h4 class="font-bold text-[10px] uppercase">Windows</h4>
        </div>
        <div class="bg-white p-4 rounded-3xl border text-center shadow-sm">
            <img src="./WA_1776549716792.jpeg" class="rounded-2xl mb-4 w-full h-32 object-cover">
            <h4 class="font-bold text-[10px] uppercase">Roofing</h4>
        </div>
        <div class="bg-white p-4 rounded-3xl border text-center shadow-sm">
            <img src="./WA_1776549781247.jpeg" class="rounded-2xl mb-4 w-full h-32 object-cover">
            <h4 class="font-bold text-[10px] uppercase">Solar Hub</h4>
        </div>
        <div class="bg-white p-4 rounded-3xl border text-center shadow-sm">
            <img src="./WA_1776549862258.jpeg" class="rounded-2xl mb-4 w-full h-32 object-cover">
            <h4 class="font-bold text-[10px] uppercase">Kitchen</h4>
        </div>
    </section>

    <footer class="bg-slate-900 py-12 text-center text-white/40">
        <p class="text-[10px] font-bold tracking-[0.4em] uppercase mb-2">U.S. Home Improvement • National Enterprise</p>
        <p class="text-[8px] uppercase tracking-widest">© 2026 Certified Contractor Network. All Rights Reserved.</p>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[100] p-6 hidden overflow-y-auto">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-between items-center mb-8 pb-4 border-b">
                <h2 class="text-2xl font-black uppercase italic">HQ Lead Matrix</h2>
                <button onclick="closeAdmin()" class="text-red-500 font-bold text-xs">EXIT</button>
            </div>
            <div id="auth" class="text-center py-12">
                <input type="password" id="pin" class="input-field max-w-xs text-center text-4xl mb-4" placeholder="****">
                <button onclick="unlock()" class="primary-btn max-w-xs mx-auto block">Unlock Matrix</button>
            </div>
            <div id="leads" class="hidden space-y-4 pb-20"></div>
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

        function nextStep(id) {
            document.querySelectorAll('.step-container').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        document.getElementById('mainLeadForm').addEventListener('submit', (e) => {
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
                alert("Success! Your consultation is scheduled.");
                location.reload();
            });
        });

        // Admin Protocol
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
                    h += `<div class="p-6 border rounded-3xl bg-slate-50 relative">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded-full text-[8px] font-black uppercase absolute top-4 right-4">${data[k].service}</span>
                        <h4 class="text-xl font-bold text-slate-900">${data[k].name}</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-2 mt-4 text-[10px] font-bold text-slate-500 uppercase">
                            <p>📞 Phone: <span class="text-slate-900">${data[k].phone}</span></p>
                            <p>📧 Email: <span class="text-slate-900">${data[k].email}</span></p>
                            <p>📍 Address: <span class="text-slate-900">${data[k].address}, ${data[k].zip}</span></p>
                            <p>📅 Appt: <span class="text-blue-700">${data[k].appDate} (${data[k].appTime})</span></p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black text-[9px] uppercase">Delete Record</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = h || 'No Active Leads';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
    </script>
</body>
</html>
