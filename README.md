<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Certified Enterprise</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        body { font-family: 'Inter', sans-serif; background-color: #f8fafc; color: #1e293b; margin: 0; }
        .nav-glass { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(10px); border-bottom: 1px solid #e2e8f0; sticky: top; z-index: 100; }
        
        .hero-banner { background: linear-gradient(rgba(30, 58, 138, 0.9), rgba(30, 58, 138, 0.9)), url('./WA_1776549402525.jpeg'); background-size: cover; background-position: center; }
        
        .step-panel { display: none; }
        .step-panel.active { display: block; animation: fadeIn 0.5s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .card-shadow { box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05); border: 1px solid #e2e8f0; transition: 0.3s; }
        .card-shadow:hover { transform: translateY(-5px); border-color: #2563eb; }

        .input-pro { width: 100%; padding: 14px; border-radius: 8px; border: 1px solid #cbd5e1; font-weight: 500; outline: none; margin-bottom: 15px; }
        .input-pro:focus { border-color: #2563eb; ring: 2px #2563eb; }

        .btn-main { background: #1e3a8a; color: white; padding: 16px; border-radius: 8px; font-weight: 800; text-transform: uppercase; width: 100%; transition: 0.2s; border: none; cursor: pointer; }
        .btn-main:hover { background: #1e40af; }

        .service-img { width: 100%; height: 160px; object-fit: cover; border-radius: 12px 12px 0 0; }
    </style>
</head>
<body>

    <nav class="nav-glass py-4 px-6 flex justify-between items-center sticky top-0">
        <div class="flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-full border shadow-sm">
            <span onclick="handleAdminTap()" class="font-black text-sm tracking-tighter uppercase cursor-pointer select-none">U.S. Home Improvement</span>
        </div>
        <div class="hidden md:flex gap-6 text-[10px] font-bold uppercase tracking-widest text-slate-500">
            <a href="#about" class="hover:text-blue-600">Company</a>
            <a href="#services" class="hover:text-blue-600">Services</a>
            <a href="#portal" class="bg-blue-600 text-white px-3 py-1 rounded">Get Quote</a>
        </div>
    </nav>

    <header class="hero-banner py-20 px-6 text-center text-white">
        <h1 class="text-4xl md:text-7xl font-extrabold mb-4 leading-tight">NATIONAL HOME<br>EXCELLENCE</h1>
        <p class="text-blue-200 text-xs font-bold uppercase tracking-[0.5em] mb-8">Certified Contractor Network Since 2026</p>
    </header>

    <main id="portal" class="max-w-xl mx-auto -mt-16 px-4 mb-24">
        <div class="bg-white rounded-[2rem] p-8 md:p-12 shadow-2xl border-t-8 border-blue-800">
            <div class="text-center mb-8">
                <span class="bg-blue-50 text-blue-700 px-4 py-1 rounded-full text-[10px] font-black uppercase tracking-tighter">Authorized Quote Matrix</span>
            </div>

            <form id="proEnterpriseForm">
                <div class="step-panel active" id="s1">
                    <label class="text-[11px] font-black text-slate-400 uppercase">01. Service Path</label>
                    <select id="service" class="input-pro mt-2" required>
                        <option value="Windows">Replacement Windows (Energy Star)</option>
                        <option value="Roofing">Architectural Roofing Systems</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Luxury Kitchen Remodel</option>
                        <option value="Bath">Spa Bath Renovation</option>
                    </select>
                    <input type="text" id="cName" placeholder="Full Legal Name" class="input-pro" required>
                    <input type="email" id="cEmail" placeholder="Professional Email" class="input-pro" required>
                    <button type="button" onclick="goStep('s2')" class="btn-main">Verify Eligibility</button>
                </div>

                <div class="step-panel" id="s2">
                    <label class="text-[11px] font-black text-slate-400 uppercase">02. Location Details</label>
                    <input type="text" id="address" placeholder="Street Address" class="input-pro mt-2" required>
                    <div class="grid grid-cols-2 gap-4">
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-pro" required>
                        <select id="owner" class="input-pro" required>
                            <option value="Homeowner">Homeowner</option>
                            <option value="Tenant">Tenant</option>
                        </select>
                    </div>
                    <select id="credit" class="input-pro" required>
                        <option value="Excellent">Credit: 720+ Excellent</option>
                        <option value="Good">Credit: 660-719 Good</option>
                        <option value="Fair">Credit: Fair Profile</option>
                    </select>
                    <button type="button" onclick="goStep('s3')" class="btn-main">Set Schedule</button>
                </div>

                <div class="step-panel" id="s3">
                    <label class="text-[11px] font-black text-slate-400 uppercase">03. Consultation Window</label>
                    <div class="grid grid-cols-2 gap-4 mt-2">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appTime" class="input-pro" required>
                            <option value="Morning">Morning (8-12)</option>
                            <option value="Afternoon">Afternoon (12-4)</option>
                            <option value="Evening">Evening (4-7)</option>
                        </select>
                    </div>
                    <input type="tel" id="cPhone" placeholder="Contact Number (Protocol)" class="input-pro" required>
                    <button type="submit" class="btn-main !bg-blue-800">Authorize Submission</button>
                </div>
            </form>
        </div>
    </main>

    <section id="services" class="max-w-6xl mx-auto px-6 mb-24">
        <h3 class="text-center font-black text-2xl uppercase italic mb-12 tracking-tighter">Enterprise Solutions Matrix</h3>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776549402525.jpeg" class="service-img"><h4>Exterior</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776549555727.jpeg" class="service-img"><h4>Windows</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776549622236.jpeg" class="service-img"><h4>Doors</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776549716792.jpeg" class="service-img"><h4>Roofing</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776549781247.jpeg" class="service-img"><h4>Solar</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776549862258.jpeg" class="service-img"><h4>Kitchen</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776549917709.jpeg" class="service-img"><h4>Bath</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776549990291.jpeg" class="service-img"><h4>Interior</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776550066723.jpeg" class="service-img"><h4>Smart</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776550133465.jpeg" class="service-img"><h4>Siding</h4></div>
            <div class="card-shadow bg-white rounded-xl"><img src="./WA_1776550199723.jpeg" class="service-img"><h4>Gutters</h4></div>
        </div>
    </section>

    <section id="about" class="bg-white py-20 px-6 border-t">
        <div class="max-w-4xl mx-auto grid md:grid-cols-2 gap-16">
            <div>
                <h4 class="font-black uppercase text-sm mb-4 text-blue-700">Company Standards</h4>
                <p class="text-xs font-semibold text-slate-500 leading-relaxed uppercase">U.S. Home Improvement is a national network of certified contractors. We specialize in high-efficiency upgrades and energy-certified installations. All projects are backed by our 2026 Quality Assurance Guarantee.</p>
            </div>
            <div class="space-y-4">
                <button onclick="showModal('privacy')" class="block text-[10px] font-bold uppercase tracking-widest text-slate-400 hover:text-blue-600">Privacy Policy</button>
                <button onclick="showModal('terms')" class="block text-[10px] font-bold uppercase tracking-widest text-slate-400 hover:text-blue-600">Terms of Service</button>
                <button onclick="showModal('licensing')" class="block text-[10px] font-bold uppercase tracking-widest text-slate-400 hover:text-blue-600">Licensing & Compliance</button>
            </div>
        </div>
    </section>

    <footer class="bg-slate-900 py-16 text-center text-white/30 border-t border-white/5">
        <img src="./WA_1776550450872.jpeg" class="h-12 w-12 mx-auto rounded-full grayscale opacity-50 mb-6">
        <p class="text-[10px] font-black tracking-[0.6em] uppercase mb-2">U.S. Home Improvement • National HQ</p>
        <p class="text-[8px] uppercase tracking-widest">Official Certified Enterprise Network © 2026 All Rights Reserved.</p>
    </footer>

    <div id="modal" class="fixed inset-0 bg-black/80 z-[200] hidden items-center justify-center p-6">
        <div class="bg-white p-10 rounded-3xl max-w-lg w-full">
            <div id="modalContent"></div>
            <button onclick="closeModal()" class="btn-main mt-8">Close Portal</button>
        </div>
    </div>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[300] p-8 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-6 mb-8">
            <h3 class="text-2xl font-black uppercase italic tracking-tighter">HQ Lead Terminal</h3>
            <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-6 py-2 rounded-full font-bold text-[10px]">DISCONNECT</button>
        </div>
        <div id="auth" class="text-center py-20">
            <input type="password" id="pin" class="input-pro max-w-[250px] text-center text-4xl mb-4" placeholder="****">
            <button onclick="unlock()" class="btn-main max-w-[250px] mx-auto block">Unlock Matrix</button>
        </div>
        <div id="leads" class="hidden space-y-6 pb-40"></div>
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

        document.getElementById('proEnterpriseForm').addEventListener('submit', (e) => {
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
                alert("AUTHORIZATION SUCCESSFUL! Your appointment is locked.");
                location.reload();
            });
        });

        // Modal Logic
        const contents = {
            privacy: '<h4 class="font-black text-2xl uppercase mb-4">Privacy Protocol</h4><p class="text-xs text-slate-500 font-bold uppercase leading-relaxed">Your data is encrypted using national enterprise standards. We never sell your personal project details to third-party entities.</p>',
            terms: '<h4 class="font-black text-2xl uppercase mb-4">Terms of Service</h4><p class="text-xs text-slate-500 font-bold uppercase leading-relaxed">All quotes are subject to site inspection. Estimates provided via the matrix are preliminary and based on national average material costs.</p>',
            licensing: '<h4 class="font-black text-2xl uppercase mb-4">Licensing</h4><p class="text-xs text-slate-500 font-bold uppercase leading-relaxed">Certified Enterprise ID: 2026-USHI-07. All contractors are verified, insured, and licensed in their respective jurisdictions.</p>'
        };
        function showModal(t) { document.getElementById('modalContent').innerHTML = contents[t]; document.getElementById('modal').style.display = 'flex'; }
        function closeModal() { document.getElementById('modal').style.display = 'none'; }

        // Admin Protocol (4 Taps on Logo/Name)
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
                    h += `<div class="p-6 border rounded-2xl bg-slate-50 relative card-shadow">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] font-black uppercase absolute top-4 right-4">${data[k].service}</span>
                        <h4 class="text-xl font-black text-slate-900 mb-4">${data[k].name}</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-x-12 gap-y-2 text-[10px] font-bold text-slate-400 uppercase">
                            <p>📞 Phone: <span class="text-slate-900">${data[k].phone}</span></p>
                            <p>📧 Email: <span class="text-slate-900">${data[k].email}</span></p>
                            <p class="md:col-span-2">📍 Address: <span class="text-slate-900">${data[k].address}, ${data[k].zip}</span></p>
                            <p>📅 Schedule: <span class="text-blue-700">${data[k].appDate} (${data[k].appTime})</span></p>
                            <p>🏠 Status: <span class="text-slate-900">${data[k].owner} | ${data[k].credit}</span></p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black text-[9px] uppercase border-b border-red-200">Delete Record</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = h || 'NO ACTIVE DATA IN MATRIX';
            });
        }
        function del(id) { if(confirm('Delete permanently?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
    </script>
</body>
</html>
