<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; }
        .nav-sticky { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(10px); border-bottom: 1px solid #e2e8f0; position: sticky; top: 0; z-index: 100; }
        .hero-bg { background: linear-gradient(rgba(30, 58, 138, 0.85), rgba(30, 58, 138, 0.85)), url('./WA_1776549402525.jpeg'); background-size: cover; background-position: center; }
        .step-panel { display: none; }
        .step-panel.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        .input-pro { width: 100%; padding: 12px; border: 1px solid #cbd5e1; border-radius: 8px; margin-bottom: 12px; font-weight: 600; outline-color: #1e3a8a; }
        .btn-pro { background: #1e3a8a; color: white; padding: 15px; border-radius: 8px; font-weight: 800; width: 100%; text-transform: uppercase; cursor: pointer; border: none; }
        .service-card { background: white; border-radius: 12px; overflow: hidden; border: 1px solid #e2e8f0; text-align: center; transition: 0.3s; }
        .service-card:hover { transform: translateY(-5px); border-color: #2563eb; }
        .service-img { width: 100%; height: 130px; object-fit: cover; }
    </style>
</head>
<body>

    <nav class="nav-sticky py-4 px-6 flex justify-between items-center">
        <div class="flex items-center gap-2">
            <img src="./WA_1776550450872.jpeg" class="h-8 w-8 rounded-full border">
            <span onclick="handleAdminTap()" class="font-black text-sm tracking-tight uppercase cursor-pointer">U.S. Home Improvement</span>
        </div>
        <div class="text-[9px] font-bold text-blue-600 border border-blue-100 px-2 py-1 rounded">EST. 2026</div>
    </nav>

    <header class="hero-bg py-16 px-6 text-center text-white">
        <h1 class="text-4xl font-extrabold tracking-tighter mb-2 uppercase">Quality Excellence</h1>
        <p class="text-blue-200 text-[10px] font-bold uppercase tracking-[0.4em]">National Contractor Network</p>
    </header>

    <main class="max-w-md mx-auto -mt-10 px-4 mb-20">
        <div class="bg-white rounded-3xl p-8 shadow-xl border-t-4 border-blue-800">
            <form id="leadForm">
                <div class="step-panel active" id="s1">
                    <label class="text-[10px] font-bold text-slate-400 uppercase mb-2 block">Choose Service</label>
                    <select id="service" class="input-pro" required>
                        <option value="Roofing">Roofing Solutions</option>
                        <option value="Solar">Solar Panels</option>
                        <option value="Windows">Windows & Doors</option>
                        <option value="Garage">Garage & Deck</option>
                    </select>
                    <input type="text" id="cName" placeholder="Full Name" class="input-pro" required>
                    <button type="button" onclick="goStep('s2')" class="btn-pro">Next: Location</button>
                </div>

                <div class="step-panel" id="s2">
                    <input type="text" id="address" placeholder="Street Address" class="input-pro" required>
                    <div class="flex gap-3">
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-pro" required>
                        <select id="owner" class="input-pro" required>
                            <option value="Homeowner">Homeowner</option>
                            <option value="Tenant">Tenant</option>
                        </select>
                    </div>
                    <button type="button" onclick="goStep('s3')" class="btn-pro">Next: Schedule</button>
                </div>

                <div class="step-panel" id="s3">
                    <div class="flex gap-3">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appTime" class="input-pro" required>
                            <option value="Morning">Morning</option>
                            <option value="Afternoon">Afternoon</option>
                        </select>
                    </div>
                    <input type="tel" id="cPhone" placeholder="Phone Number" class="input-pro" required>
                    <button type="submit" class="btn-pro">Book Appointment</button>
                </div>
            </form>
        </div>
    </main>

    <section class="px-6 mb-20 max-w-4xl mx-auto">
        <h3 class="text-center font-bold uppercase text-sm mb-8 tracking-widest">Authorized Services</h3>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
            <div class="service-card"><img src="./WA_1776549716792.jpeg" class="service-img"><h4>Roofing</h4></div>
            <div class="service-card"><img src="./WA_1776549781247.jpeg" class="service-img"><h4>Solar Hub</h4></div>
            <div class="service-card"><img src="./WA_1776549555727.jpeg" class="service-img"><h4>Windows</h4></div>
            <div class="service-card"><img src="./WA_1776549622236.jpeg" class="service-img"><h4>Doors</h4></div>
            <div class="service-card"><img src="./WA_1776550199723.jpeg" class="service-img"><h4>Gutters</h4></div>
            <div class="service-card"><img src="./WA_1776550133465.jpeg" class="service-img"><h4>Siding</h4></div>
            <div class="service-card"><img src="./WA_1776549990291.jpeg" class="service-img"><h4>Interior</h4></div>
            <div class="service-card"><img src="./WA_1776549862258.jpeg" class="service-img"><h4>Kitchen</h4></div>
        </div>
    </section>

    <footer class="bg-white border-t py-12 px-6">
        <div class="max-w-4xl mx-auto grid md:grid-cols-2 gap-8 text-[11px] font-bold text-slate-400 uppercase">
            <div>
                <h4 class="text-blue-800 mb-2">Company Details</h4>
                <p>U.S. Home Improvement is a nationwide certified contractor network. We provide licensed and insured professionals for all home projects.</p>
            </div>
            <div class="space-y-2">
                <p onclick="alert('Privacy: Data is secured.')" class="cursor-pointer hover:text-blue-600">Privacy Policy</p>
                <p onclick="alert('Terms: Inspection required.')" class="cursor-pointer hover:text-blue-600">Terms of Service</p>
            </div>
        </div>
        <p class="text-center mt-10 text-[8px] tracking-[0.5em]">© 2026 U.S. Home Improvement</p>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[200] p-6 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-4 mb-6"><h3 class="font-bold uppercase">Leads</h3><button onclick="closeAdmin()" class="text-red-500 font-bold">EXIT</button></div>
        <div id="auth" class="text-center py-10">
            <input type="password" id="pin" class="input-pro max-w-[200px] text-center" placeholder="PIN">
            <button onclick="unlock()" class="btn-pro max-w-[200px] mt-4">Unlock</button>
        </div>
        <div id="leads" class="hidden"></div>
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

        function goStep(id) {
            document.querySelectorAll('.step-panel').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        document.getElementById('leadForm').addEventListener('submit', (e) => {
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
            db.ref('leads').push(data).then(() => { alert("Appointment Fixed!"); location.reload(); });
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
                    h += `<div class="p-4 border rounded mb-2 text-[11px] font-bold">
                        <p class="text-blue-600">${data[k].service}</p>
                        <p>NAME: ${data[k].name} | TEL: ${data[k].phone}</p>
                        <p>ADDR: ${data[k].address}</p>
                        <button onclick="del('${k}')" class="text-red-500 mt-2">Delete</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = h || 'No Leads';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
    </script>
</body>
</html>
