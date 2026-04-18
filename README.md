<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #0f172a; margin: 0; }
        .nav-pro { background: white; border-bottom: 1px solid #f1f5f9; position: sticky; top: 0; z-index: 1000; padding: 15px 20px; }
        
        /* Corporate Banner */
        .hero-banner { background: linear-gradient(rgba(30, 58, 138, 0.9), rgba(30, 58, 138, 0.9)), url('./WA_1776549402525.jpeg'); background-size: cover; background-position: center; padding: 60px 20px; text-align: center; color: white; }
        
        /* Professional Step Form */
        .step-panel { display: none; }
        .step-panel.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .form-container { background: white; border-radius: 20px; border: 1px solid #e2e8f0; box-shadow: 0 15px 30px -10px rgba(0,0,0,0.1); padding: 30px; margin-top: -40px; }
        .input-box { width: 100%; padding: 12px; border: 1px solid #cbd5e1; border-radius: 10px; margin-bottom: 15px; font-weight: 600; outline-color: #1e3a8a; }
        .btn-action { background: #1e3a8a; color: white; padding: 16px; border-radius: 10px; font-weight: 800; width: 100%; text-transform: uppercase; cursor: pointer; border: none; }
        
        /* Service Cards - Matches your screenshots */
        .service-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; padding: 20px; }
        .service-card { background: white; border: 1px solid #f1f5f9; border-radius: 15px; text-align: center; padding-bottom: 15px; overflow: hidden; transition: 0.3s; }
        .service-card:hover { border-color: #2563eb; transform: translateY(-3px); }
        .service-card img { width: 100%; height: 120px; object-fit: cover; }
        .service-card h4 { font-size: 11px; font-weight: 800; color: #1e293b; margin-top: 10px; text-transform: uppercase; letter-spacing: 0.5px; }
    </style>
</head>
<body>

    <nav class="nav-pro flex justify-between items-center">
        <div class="flex items-center gap-2">
            <img src="./WA_1776550450872.jpeg" class="h-8 w-8 rounded-full border">
            <span onclick="handleAdminTap()" class="font-black text-sm tracking-tighter uppercase cursor-pointer">U.S. Home Improvement</span>
        </div>
        <div class="text-[9px] font-bold text-blue-700 bg-blue-50 px-2 py-1 rounded">EST. 2026</div>
    </nav>

    <header class="hero-banner">
        <h1 class="text-3xl font-black uppercase tracking-tighter mb-2">U.S. Home Upgrades</h1>
        <p class="text-blue-200 text-[10px] font-bold uppercase tracking-[0.4em]">Nationwide Certified Matrix 2026</p>
    </header>

    <main class="max-w-md mx-auto px-4 mb-20">
        <div class="form-container">
            <form id="mainMatrixForm">
                <div class="step-panel active" id="s1">
                    <label class="text-[10px] font-black text-slate-400 uppercase mb-2 block">01. Service Path</label>
                    <select id="service" class="input-box" required>
                        <option value="Roofing">Roofing Solutions</option>
                        <option value="Solar">Solar Matrix</option>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Doors">Exterior Doors</option>
                        <option value="Garage">Garage & Deck</option>
                    </select>
                    <input type="text" id="cName" placeholder="Full Legal Name" class="input-box" required>
                    <button type="button" onclick="nextStep('s2')" class="btn-action">Continue</button>
                </div>

                <div class="step-panel" id="s2">
                    <input type="text" id="address" placeholder="Street Address" class="input-box" required>
                    <div class="flex gap-3">
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-box" required>
                        <select id="owner" class="input-box" required>
                            <option value="Homeowner">Homeowner</option>
                            <option value="Tenant">Tenant</option>
                        </select>
                    </div>
                    <button type="button" onclick="nextStep('s3')" class="btn-action">Next Step</button>
                </div>

                <div class="step-panel" id="s3">
                    <div class="flex gap-3">
                        <input type="date" id="appDate" class="input-pro w-full border p-3 rounded-lg mb-4" required>
                        <select id="appTime" class="input-pro w-full border p-3 rounded-lg mb-4" required>
                            <option value="Morning">Morning</option>
                            <option value="Afternoon">Afternoon</option>
                        </select>
                    </div>
                    <input type="tel" id="cPhone" placeholder="Mobile Number" class="input-box" required>
                    <button type="submit" class="btn-action">Authorize Booking</button>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-md mx-auto mb-20">
        <div class="service-grid">
            <div class="service-card"><img src="./WA_1776549716792.jpeg"><h4>Roofing</h4></div>
            <div class="service-card"><img src="./WA_1776549781247.jpeg"><h4>Solar Matrix</h4></div>
            <div class="service-card"><img src="./WA_1776549555727.jpeg"><h4>Windows</h4></div>
            <div class="service-card"><img src="./WA_1776549622236.jpeg"><h4>Doors</h4></div>
            <div class="service-card"><img src="./WA_1776550133465.jpeg"><h4>Siding</h4></div>
            <div class="service-card"><img src="./WA_1776550199723.jpeg"><h4>Gutters</h4></div>
            <div class="service-card"><img src="./WA_1776549990291.jpeg"><h4>Interior</h4></div>
            <div class="service-card"><img src="./WA_1776549862258.jpeg"><h4>Kitchen</h4></div>
        </div>
    </section>

    <footer class="bg-white border-t py-16 px-8 text-slate-400">
        <div class="max-w-md mx-auto space-y-8">
            <div>
                <h4 class="text-[11px] font-black text-blue-800 uppercase mb-3">Company Protocol</h4>
                <p class="text-[10px] font-bold uppercase leading-relaxed">U.S. Home Improvement is a national certified network. All projects are handled by licensed, insured, and verified local professionals.</p>
            </div>
            <div class="flex flex-col gap-3">
                <button onclick="alert('Privacy Protocol: All lead data is encrypted.')" class="text-[10px] font-bold uppercase text-left hover:text-blue-600">Privacy Policy</button>
                <button onclick="alert('Terms: Quotes are preliminary and subject to site check.')" class="text-[10px] font-bold uppercase text-left hover:text-blue-600">Terms of Service</button>
            </div>
            <div class="text-center pt-8 border-t">
                <p class="text-[8px] font-black tracking-[0.5em] uppercase">Official Enterprise © 2026</p>
            </div>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[2000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-4 mb-6">
            <h3 class="font-black italic uppercase">Matrix Leads</h3>
            <button onclick="closeAdmin()" class="text-red-500 font-bold text-xs">EXIT</button>
        </div>
        <div id="auth" class="text-center py-10">
            <input type="password" id="pin" class="input-box max-w-[200px] text-center" placeholder="****">
            <button onclick="unlock()" class="btn-action max-w-[200px] mt-2">Unlock</button>
        </div>
        <div id="leads" class="hidden space-y-4 pb-20"></div>
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
            document.querySelectorAll('.step-panel').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        document.getElementById('mainMatrixForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('service').value,
                name: document.getElementById('cName').value,
                address: document.getElementById('address').value,
                zip: document.getElementById('cZip').value,
                owner: document.getElementById('owner').value,
                appDate: document.getElementById('appDate').value,
                appTime: document.getElementById('appTime').value,
                phone: document.getElementById('cPhone').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                alert("AUTHORIZATION SUCCESSFUL!");
                location.reload();
            });
        });

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
                    h += `<div class="p-5 border rounded-2xl bg-slate-50 relative mb-4">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] font-black uppercase absolute top-4 right-4">${data[k].service}</span>
                        <h4 class="text-lg font-black text-slate-900 mb-2">${data[k].name}</h4>
                        <div class="text-[10px] font-bold text-slate-400 uppercase">
                            <p>📞 Phone: ${data[k].phone}</p>
                            <p>📍 Address: ${data[k].address}</p>
                            <p>📅 Schedule: ${data[k].appDate} (${data[k].appTime})</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-3 text-red-500 font-bold text-[9px] uppercase border-b border-red-100">Delete Record</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = h || 'NO ACTIVE LEADS';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
    </script>
</body>
</html>
