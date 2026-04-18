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

        /* Premium Nav */
        nav { backdrop-filter: blur(15px); background: rgba(255,255,255,0.8); position: sticky; top: 0; z-index: 1000; border-bottom: 1px solid #f1f5f9; }

        .glass-panel {
            background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(30px);
            border-radius: 3rem; border: 1px solid #f1f5f9; box-shadow: 0 50px 100px -20px rgba(0,0,0,0.12);
        }

        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.7s cubic-bezier(0.16, 1, 0.3, 1); }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(50px); } to { opacity: 1; transform: translateY(0); } }

        .input-premium {
            width: 100%; padding: 1.4rem; border-radius: 1.5rem; border: 2px solid #f1f5f9;
            font-weight: 700; transition: 0.3s; background: #fff; outline: none; font-size: 1rem;
        }
        .input-premium:focus { border-color: var(--accent); box-shadow: 0 0 30px rgba(6, 182, 212, 0.15); }

        .btn-ultimate {
            background: linear-gradient(135deg, var(--dark) 0%, #1e293b 100%);
            color: white; padding: 1.5rem; border-radius: 1.5rem;
            font-weight: 800; text-transform: uppercase; letter-spacing: 2px; width: 100%; transition: 0.5s;
        }
        .btn-ultimate:hover { transform: scale(1.02) translateY(-4px); box-shadow: 0 20px 40px rgba(0,0,0,0.1); }

        .service-card {
            border-radius: 3rem; overflow: hidden; border: 1px solid #f1f5f9; transition: 0.6s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .service-card:hover { transform: translateY(-15px); border-color: var(--accent); box-shadow: 0 30px 60px rgba(0,0,0,0.05); }
    </style>
</head>
<body>

    <nav class="py-4 px-6 flex justify-between items-center">
        <div class="flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-full border">
            <span onclick="handleAdminTap()" class="font-black tracking-tighter uppercase text-sm cursor-pointer">U.S. Home Improvement</span>
        </div>
        <div class="hidden md:flex gap-8 text-[10px] font-black uppercase tracking-widest text-slate-400">
            <span>Verified Network</span>
            <span>National HQ</span>
            <span class="text-blue-600">Free Quotes Active</span>
        </div>
    </nav>

    <header class="py-24 text-center px-6 bg-gradient-to-b from-slate-50 to-white relative overflow-hidden">
        <div class="relative z-10 max-w-4xl mx-auto">
            <h1 class="text-6xl md:text-9xl font-extrabold tracking-tighter leading-none mb-6">
                QUALITY<br><span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-700 to-cyan-500">EXCELLENCE.</span>
            </h1>
            <p class="text-[12px] font-black tracking-[0.8em] text-slate-400 uppercase mb-12">America's Trusted Home Upgrade Matrix</p>
        </div>
    </header>

    <section class="max-w-4xl mx-auto -mt-24 px-4 mb-40 relative z-20">
        <div class="glass-panel p-10 md:p-20 border-t-[15px] border-blue-700">
            <div class="text-center mb-16">
                <span class="bg-blue-50 text-blue-700 px-6 py-2 rounded-full text-[10px] font-black uppercase tracking-widest mb-6 inline-block">Enterprise Scheduling Protocol</span>
                <h2 class="text-4xl font-black italic uppercase">Project Authorization</h2>
            </div>

            <form id="masterForm">
                <div class="step active" id="step1">
                    <div class="space-y-6">
                        <select id="service" class="input-premium" required>
                            <option value="">Select Service Path...</option>
                            <option value="Windows">Energy Star Windows</option>
                            <option value="Roofing">Architectural Roofing</option>
                            <option value="Solar">Solar Matrix Deployment</option>
                            <option value="Kitchen">Luxury Kitchen Remodel</option>
                        </select>
                        <input type="text" id="cName" placeholder="Full Legal Name" class="input-premium" required>
                        <input type="email" id="cEmail" placeholder="Official Email Protocol" class="input-premium" required>
                        <button type="button" onclick="goNext('step2')" class="btn-ultimate">Verify Location</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <div class="space-y-6">
                        <input type="text" id="address" placeholder="Residential Street Address" class="input-premium" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="text" id="cZip" placeholder="Zip Code" class="input-premium" required>
                            <select id="owner" class="input-premium" required>
                                <option value="">Ownership Status?</option>
                                <option value="Owner">Homeowner</option>
                                <option value="Tenant">Tenant</option>
                            </select>
                        </div>
                        <select id="credit" class="input-premium" required>
                            <option value="">Credit Score Rating</option>
                            <option value="Excellent">720+ Excellent</option>
                            <option value="Good">660-719 Good</option>
                            <option value="Fair">Fair Profile</option>
                        </select>
                        <button type="button" onclick="goNext('step3')" class="btn-ultimate">Schedule Consultation</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <div class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <input type="date" id="appDate" class="input-premium" required>
                            <select id="appTime" class="input-premium" required>
                                <option value="Morning">Morning Window</option>
                                <option value="Afternoon">Afternoon Window</option>
                                <option value="Evening">Evening Window</option>
                            </select>
                        </div>
                        <input type="tel" id="cPhone" placeholder="Direct Contact Number" class="input-premium" required>
                        <button type="submit" class="btn-ultimate bg-blue-700">Authorize Submission</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 mb-40">
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-10">
            <div class="service-card bg-slate-50 p-4"><img src="./WA_1776549555727.jpeg" class="rounded-[2rem]"><h4 class="mt-6 font-black uppercase text-xs text-center pb-4 text-blue-700">Elite Windows</h4></div>
            <div class="service-card bg-slate-50 p-4"><img src="./WA_1776549716792.jpeg" class="rounded-[2rem]"><h4 class="mt-6 font-black uppercase text-xs text-center pb-4 text-blue-700">Elite Roofing</h4></div>
            <div class="service-card bg-slate-50 p-4"><img src="./WA_1776549781247.jpeg" class="rounded-[2rem]"><h4 class="mt-6 font-black uppercase text-xs text-center pb-4 text-blue-700">Solar Hub</h4></div>
            <div class="service-card bg-slate-50 p-4"><img src="./WA_1776549862258.jpeg" class="rounded-[2rem]"><h4 class="mt-6 font-black uppercase text-xs text-center pb-4 text-blue-700">Luxury Kitchen</h4></div>
        </div>
    </section>

    <footer class="bg-slate-950 py-32 text-center text-white/20 px-6">
        <p class="text-[10px] font-black tracking-[0.8em] uppercase mb-4">U.S. HOME IMPROVEMENT • NATIONAL ENTERPRISE</p>
        <p class="text-[8px] uppercase tracking-widest">© 2026 Nationwide Certified Contractor Network. All Rights Reserved.</p>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[9999] p-8 hidden overflow-y-auto">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b pb-8">
                <h2 class="text-4xl font-black uppercase italic tracking-tighter">HQ Matrix Terminal</h2>
                <button onclick="closeAdmin()" class="bg-red-50 text-red-500 font-black text-[10px] px-8 py-4 rounded-full uppercase tracking-widest">Exit Secure Matrix</button>
            </div>
            <div id="auth" class="text-center py-24">
                <input type="password" id="pin" class="input-premium max-w-xs text-center text-6xl mb-8 tracking-tighter" placeholder="****">
                <button onclick="unlock()" class="btn-ultimate max-w-xs mx-auto block">Access Leads</button>
            </div>
            <div id="leads" class="hidden space-y-10 pb-40"></div>
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
            const payload = {
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
            db.ref('leads').push(payload).then(() => {
                alert("APPLICATION AUTHORIZED! A senior specialist will contact you.");
                location.reload();
            });
        });

        // Secret Admin
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
                    h += `<div class="p-12 border border-slate-100 rounded-[3.5rem] bg-white shadow-2xl flex flex-col lg:flex-row justify-between items-start lg:items-center gap-10">
                        <div class="flex-1">
                            <div class="flex gap-3 mb-4">
                                <span class="bg-blue-600 text-white px-5 py-1.5 rounded-full text-[10px] font-black uppercase">${data[k].service}</span>
                                <span class="bg-slate-100 text-slate-500 px-5 py-1.5 rounded-full text-[10px] font-black uppercase">📅 ${data[k].appDate}</span>
                            </div>
                            <h4 class="text-4xl font-black text-slate-900 mb-6 leading-none tracking-tighter">${data[k].name}</h4>
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-x-12 gap-y-3 text-[11px] font-bold text-slate-400 uppercase tracking-wide">
                                <p>📧 Email: <span class="text-slate-900">${data[k].email}</span></p>
                                <p>📞 Phone: <span class="text-slate-900">${data[k].phone}</span></p>
                                <p class="md:col-span-2">📍 Location: <span class="text-slate-900">${data[k].address}, ${data[k].zip}</span></p>
                                <p>🏠 Status: <span class="text-slate-900">${data[k].owner}</span></p>
                                <p>💳 Credit: <span class="text-blue-700">${data[k].credit}</span></p>
                            </div>
                        </div>
                        <button onclick="del('${k}')" class="text-red-500 font-black text-[10px] border-2 border-red-50 px-10 py-6 rounded-[2rem] hover:bg-red-500 hover:text-white transition-all shadow-lg">DELETE RECORD</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = h || '<p class="text-center font-black text-slate-200 py-40 text-4xl uppercase italic">No Active Matrix</p>';
            });
        }
        function del(id) { if(confirm('Delete permanently?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
    </script>
</body>
</html>
