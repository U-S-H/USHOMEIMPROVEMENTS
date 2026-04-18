<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #fcfcfc; color: #1e293b; margin: 0; overflow-x: hidden; }
        .nav-sticky { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(10px); border-bottom: 1px solid #f1f5f9; position: sticky; top: 0; z-index: 1000; }
        
        .hero-section { background: linear-gradient(rgba(15, 23, 42, 0.8), rgba(15, 23, 42, 0.8)), url('./WA_1776549402525.jpeg'); background-size: cover; background-position: center; padding: 80px 20px; text-align: center; color: white; }
        
        .step-panel { display: none; }
        .step-panel.active { display: block; animation: slideUp 0.4s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .form-glass { background: white; border-radius: 24px; border: 1px solid #e2e8f0; box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.05); }
        .input-pro { width: 100%; padding: 14px; border-radius: 12px; border: 1px solid #e2e8f0; background: #f8fafc; font-weight: 600; margin-bottom: 12px; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: #2563eb; background: white; box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }

        .btn-matrix { background: #1e3a8a; color: white; padding: 16px; border-radius: 12px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; width: 100%; cursor: pointer; border: none; transition: 0.3s; }
        .btn-matrix:hover { background: #1e40af; transform: translateY(-2px); }

        .service-card { background: white; border: 1px solid #f1f5f9; border-radius: 16px; overflow: hidden; transition: 0.3s; }
        .service-card:hover { transform: translateY(-5px); box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1); border-color: #2563eb; }
        .service-img { width: 100%; height: 140px; object-fit: cover; }
    </style>
</head>
<body>

    <nav class="nav-sticky py-4 px-6 flex justify-between items-center">
        <div class="flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" class="h-9 w-9 rounded-full border shadow-sm">
            <span onclick="handleAdminTap()" class="font-extrabold text-sm tracking-tighter uppercase cursor-pointer select-none">U.S. Home Improvement</span>
        </div>
        <div class="hidden md:flex gap-6 text-[10px] font-bold uppercase tracking-widest text-slate-400">
            <a href="#matrix" class="hover:text-blue-600">Qualification</a>
            <a href="#services" class="hover:text-blue-600">Services</a>
            <span class="text-blue-600 bg-blue-50 px-2 py-1 rounded">Network Active</span>
        </div>
    </nav>

    <header class="hero-section">
        <h1 class="text-4xl md:text-7xl font-black mb-4 tracking-tighter">NATIONAL UPGRADE<br>SOLUTIONS</h1>
        <p class="text-blue-300 text-[10px] font-bold uppercase tracking-[0.6em]">Certified Contractor Matrix 2026</p>
    </header>

    <section id="matrix" class="max-w-xl mx-auto -mt-16 px-4 mb-24">
        <div class="form-glass p-8 md:p-12 border-t-[10px] border-blue-800">
            <div class="text-center mb-10">
                <span class="bg-blue-50 text-blue-700 px-4 py-1 rounded-full text-[10px] font-black uppercase">Project Authorization Portal</span>
            </div>

            <form id="matrixForm">
                <div class="step-panel active" id="s1">
                    <select id="service" class="input-pro" required>
                        <option value="Windows">Replacement Windows</option>
                        <option value="Roofing">Architectural Roofing</option>
                        <option value="Solar">Solar Matrix Hub</option>
                        <option value="Kitchen">Luxury Kitchen Remodel</option>
                        <option value="Bath">Bathroom Renovation</option>
                    </select>
                    <input type="text" id="cName" placeholder="Full Legal Name" class="input-pro" required>
                    <input type="email" id="cEmail" placeholder="Official Email Address" class="input-pro" required>
                    <button type="button" onclick="nextStep('s2')" class="btn-matrix">Check Eligibility</button>
                </div>

                <div class="step-panel" id="s2">
                    <input type="text" id="address" placeholder="Residential Street Address" class="input-pro" required>
                    <div class="grid grid-cols-2 gap-3">
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-pro" required>
                        <select id="owner" class="input-pro" required>
                            <option value="Homeowner">Homeowner</option>
                            <option value="Tenant">Tenant</option>
                        </select>
                    </div>
                    <select id="credit" class="input-pro" required>
                        <option value="Excellent">720+ Excellent Credit</option>
                        <option value="Good">660-719 Good Credit</option>
                        <option value="Fair">Fair Credit Profile</option>
                    </select>
                    <button type="button" onclick="nextStep('s3')" class="btn-matrix">Confirm Schedule</button>
                </div>

                <div class="step-panel" id="s3">
                    <div class="grid grid-cols-2 gap-3 mb-4">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appTime" class="input-pro" required>
                            <option value="Morning">Morning Window</option>
                            <option value="Afternoon">Afternoon Window</option>
                        </select>
                    </div>
                    <input type="tel" id="cPhone" placeholder="Direct Phone Number" class="input-pro" required>
                    <button type="submit" class="btn-matrix">Authorize Submission</button>
                </div>
            </form>
        </div>
    </section>

    <section id="services" class="max-w-6xl mx-auto px-6 mb-24">
        <h3 class="text-center font-black text-2xl uppercase italic tracking-tighter mb-12">Authorized Service Catalog</h3>
        <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-5 gap-4">
            <div class="service-card"><img src="./WA_1776549402525.jpeg" class="service-img"><h4>Main Exterior</h4></div>
            <div class="service-card"><img src="./WA_1776549555727.jpeg" class="service-img"><h4>Windows</h4></div>
            <div class="service-card"><img src="./WA_1776549622236.jpeg" class="service-img"><h4>Entry Doors</h4></div>
            <div class="service-card"><img src="./WA_1776549716792.jpeg" class="service-img"><h4>Roofing</h4></div>
            <div class="service-card"><img src="./WA_1776549781247.jpeg" class="service-img"><h4>Solar Energy</h4></div>
            <div class="service-card"><img src="./WA_1776549862258.jpeg" class="service-img"><h4>Luxury Kitchen</h4></div>
            <div class="service-card"><img src="./WA_1776549917709.jpeg" class="service-img"><h4>Master Bath</h4></div>
            <div class="service-card"><img src="./WA_1776549990291.jpeg" class="service-img"><h4>Interior Design</h4></div>
            <div class="service-card"><img src="./WA_1776550066723.jpeg" class="service-img"><h4>Smart Home</h4></div>
            <div class="service-card"><img src="./WA_1776550133465.jpeg" class="service-img"><h4>Siding</h4></div>
            <div class="service-card"><img src="./WA_1776550199723.jpeg" class="service-img"><h4>Gutters</h4></div>
        </div>
    </section>

    <footer class="bg-white border-t py-20 px-6">
        <div class="max-w-4xl mx-auto grid md:grid-cols-2 gap-12">
            <div>
                <h4 class="font-black uppercase text-xs text-blue-800 mb-4">About the Network</h4>
                <p class="text-[11px] font-bold text-slate-400 uppercase leading-relaxed">U.S. Home Improvement connects homeowners with certified, insured, and licensed local contractors. Our mission is to provide high-quality energy-efficient upgrades across the nation.</p>
            </div>
            <div class="flex flex-col gap-3">
                <button onclick="alert('Privacy Policy: We encrypt all lead data.')" class="text-[10px] font-bold text-slate-400 text-left uppercase hover:text-blue-600">Privacy Policy</button>
                <button onclick="alert('Terms: Quotes are based on site inspection.')" class="text-[10px] font-bold text-slate-400 text-left uppercase hover:text-blue-600">Terms of Service</button>
                <p class="text-[9px] font-black text-slate-300 uppercase mt-4">Corporate ID: US-HI-2026-HQ</p>
            </div>
        </div>
        <div class="text-center mt-20 border-t pt-10">
            <p class="text-[8px] font-black tracking-[0.5em] text-slate-300 uppercase">© 2026 Certified Enterprise Hub. All Rights Reserved.</p>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[2000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-6 mb-8">
            <h2 class="font-black italic uppercase">Matrix Leads</h2>
            <button onclick="closeAdmin()" class="text-red-500 font-bold text-xs uppercase">Exit</button>
        </div>
        <div id="auth" class="text-center py-20">
            <input type="password" id="pin" class="input-pro max-w-[200px] text-center text-4xl mb-4" placeholder="****">
            <button onclick="unlock()" class="btn-matrix max-w-[200px]">Access</button>
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

        document.getElementById('matrixForm').addEventListener('submit', (e) => {
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
                alert("Success! Your project is authorized.");
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
                    h += `<div class="p-6 border rounded-2xl bg-slate-50 relative mb-4">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] font-black uppercase absolute top-4 right-4">${data[k].service}</span>
                        <h4 class="text-xl font-black text-slate-900 mb-4">${data[k].name}</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-2 text-[10px] font-bold text-slate-400 uppercase">
                            <p>📞 Phone: <span class="text-slate-900">${data[k].phone}</span></p>
                            <p>📍 Address: <span class="text-slate-900">${data[k].address}, ${data[k].zip}</span></p>
                            <p>📅 Date: <span class="text-blue-700">${data[k].appDate} (${data[k].appTime})</span></p>
                            <p>🏠 Info: <span class="text-slate-900">${data[k].owner} | ${data[k].credit}</span></p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-bold text-[9px] uppercase">Delete</button>
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
