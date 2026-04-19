<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | Official National Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #0f172a; }
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 32px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.08); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; font-size: 14px; outline: none; }
        .input-pro:focus { border-color: var(--accent); background: #f8fafc; }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 16px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; }
        .matrix-card { background: white; border-radius: 28px; overflow: hidden; border: 1px solid #f1f5f9; }
        .matrix-card img { width: 100%; height: 240px; object-fit: cover; }
        .step-form { display: none; }
        .step-form.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        #notification-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 15px 25px; border-radius: 50px; box-shadow: 0 15px 35px rgba(0,0,0,0.1); border-left: 6px solid #059669; display: none; z-index: 9999; }
    </style>
</head>
<body>

    <div id="notification-toast"><p id="notif-text" class="text-[11px] font-bold text-slate-700"></p></div>

    <nav class="bg-white border-b px-6 py-5 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3" id="adminTrigger" onclick="handleTap()">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border">
            <div>
                <span class="block font-black text-sm uppercase text-blue-900">U.S. Home Improvement LLC</span>
                <span class="block text-[9px] font-extrabold text-emerald-600 uppercase italic">● Licensed National Contractor Network</span>
            </div>
        </div>
    </nav>

    <header class="py-16 px-6 text-center bg-slate-50">
        <h1 class="text-4xl font-black uppercase italic tracking-tighter mb-4 text-slate-900">National <span class="text-blue-600">Dispatch</span> Hub</h1>
        <p class="text-slate-500 font-bold uppercase text-[10px] tracking-[0.4em]">Authorized For Professional Site Estimates</p>
    </header>

    <main class="max-w-xl mx-auto px-6 -mt-10 mb-32 relative z-10">
        <div class="glass-card p-8 md:p-12">
            <form id="proDispatchForm">
                <div class="step-form active" id="step1">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4">01. Select Service</label>
                    <select id="mainService" class="input-pro mb-4" onchange="loadMeta()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power System</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                    </select>
                    <select id="isOwner" class="input-pro" required>
                        <option value="Yes">Homeowner</option>
                        <option value="No">Tenant</option>
                    </select>
                    <button type="button" onclick="goStep('step2')" class="btn-action mt-6">Continue</button>
                </div>

                <div class="step-form" id="step2">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4">02. Project Details</label>
                    <div id="dynamicContainer"></div>
                    <button type="button" onclick="goStep('step3')" class="btn-action">Next</button>
                </div>

                <div class="step-form" id="step3">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4">03. Site Authorization</label>
                    <input type="text" id="custName" placeholder="Full Name" class="input-pro mb-3" required>
                    <input type="email" id="custEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="text" id="custAddress" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-3">
                        <input type="text" id="custZip" placeholder="Zip" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Phone" class="input-pro" required>
                    </div>
                    <div class="grid grid-cols-2 gap-3 mb-6">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="10am-1pm">10AM - 1PM</option>
                            <option value="1pm-4pm">1PM - 4PM</option>
                            <option value="4pm-7pm">4PM - 7PM</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Submit Dispatch</button>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-6xl mx-auto px-6 mb-32 grid md:grid-cols-2 gap-8">
        <div class="matrix-card">
            <img src="./WA_1776549716792.jpeg">
            <div class="p-6"><h4 class="font-black text-blue-900 uppercase text-xs mb-2">Roofing Mastery</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Lifetime architectural shingles & leak-proof technology. Nationwide certified installation crews.</p></div>
        </div>
        <div class="matrix-card">
            <img src="./WA_1776549555727.jpeg">
            <div class="p-6"><h4 class="font-black text-blue-900 uppercase text-xs mb-2">Energy Windows</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Custom energy-efficient window systems designed to lower utility costs. Triple-pane sealing included.</p></div>
        </div>
    </section>

    <footer class="bg-slate-900 py-16 px-8 text-white text-center">
        <h4 class="font-black text-blue-400 uppercase text-xs mb-4">U.S. Home Improvement LLC</h4>
        <p class="text-[9px] text-slate-400 uppercase max-w-lg mx-auto leading-loose">
            Registered LLC: 702 Main Street, Woodland, CA 95695. <br>
            Privacy Policy: We protect all consumer data under federal encryption standards. Dispatch is subject to local contractor availability.
        </p>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-4 mb-6"><h3 class="font-black">ADMIN TERMINAL</h3><button onclick="closeAdmin()" class="text-red-500 font-bold uppercase">Exit</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="PIN"><button onclick="unlock()" class="btn-action max-w-[200px]">Unlock</button></div>
        <div id="leadsList" class="hidden space-y-4 pb-20"></div>
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

        let taps = 0, tapT;
        function handleTap() { taps++; clearTimeout(tapT); if(taps >= 5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } tapT = setTimeout(()=>taps=0,2000); }

        function goStep(id) { document.querySelectorAll('.step-form').forEach(s=>s.classList.remove('active')); document.getElementById(id).classList.add('active'); }

        function loadMeta() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicContainer');
            const opts = { 'Windows': ['1-10','11-20','21+'], 'Roofing': ['Shingle','Metal','Tile'] };
            const current = opts[s] || ['Standard','Premium'];
            container.innerHTML = `<select id="spec" class="input-pro mb-3">${current.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>`;
        }
        loadMeta();

        document.getElementById('proDispatchForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('mainService').value,
                name: document.getElementById('custName').value,
                email: document.getElementById('custEmail').value,
                phone: document.getElementById('custPhone').value,
                address: document.getElementById('custAddress').value,
                zip: document.getElementById('custZip').value,
                spec: document.getElementById('spec').value,
                appointment: `${document.getElementById('appDate').value} (${document.getElementById('appSlot').value})`,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { alert("Success!"); location.reload(); });
        });

        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        
        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-6 border rounded-2xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] absolute top-4 right-4 uppercase">${data[k].service}</span>
                        <h4 class="text-xl font-black uppercase text-blue-900">${data[k].name}</h4>
                        <p class="text-blue-600">📧 ${data[k].email}</p>
                        <p>📍 ${data[k].address} (Zip: ${data[k].zip})</p>
                        <p>📞 ${data[k].phone}</p>
                        <p>🛠 Spec: ${data[k].spec}</p>
                        <p class="text-emerald-600">📅 Appt: ${data[k].appointment}</p>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black">DELETE</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Leads';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
