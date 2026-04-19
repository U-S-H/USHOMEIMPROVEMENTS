<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Authorized Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; --success: #059669; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; }
        .hero-gradient { background: linear-gradient(135deg, #1e3a8a 0%, #1e40af 100%); position: relative; }
        .hero-gradient::after { content: ''; position: absolute; bottom: 0; left: 0; width: 100%; height: 8px; background: var(--accent); }
        
        .step-form { display: none; }
        .step-form.active { display: block; animation: slideIn 0.3s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }

        .glass-card { background: white; border: 1px solid #e2e8f0; border-radius: 24px; box-shadow: 0 20px 25px -5px rgba(0,0,0,0.1); }
        .input-pro { width: 100%; padding: 14px; border: 2px solid #f1f5f9; border-radius: 12px; font-weight: 600; font-size: 15px; outline: none; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        .btn-action { background: var(--primary); color: white; padding: 18px; border-radius: 12px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; }

        .grid-matrix { display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px; padding: 20px; }
        .matrix-card { background: white; border-radius: 20px; overflow: hidden; border: 1px solid #f1f5f9; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); text-align: center; }
        .matrix-card img { width: 100%; height: 130px; object-fit: cover; }
        .matrix-card h4 { font-size: 11px; font-weight: 800; color: var(--primary); text-transform: uppercase; padding: 12px 0; }
        
        .trust-badge { display: flex; align-items: center; gap: 8px; background: #ecfdf5; color: #065f46; padding: 6px 12px; border-radius: 50px; font-size: 9px; font-weight: 800; }
    </style>
</head>
<body>

    <nav class="bg-white border-b px-6 py-4 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-full border shadow-sm">
            <div>
                <span onclick="toggleAdmin()" class="block font-black text-xs uppercase tracking-tighter cursor-pointer">U.S. Home Improvement</span>
                <div class="trust-badge uppercase">● California Licensed #786-092</div>
            </div>
        </div>
        <div class="hidden md:block text-[10px] font-black text-slate-400 uppercase tracking-widest">National Headquarters</div>
    </nav>

    <header class="hero-gradient py-12 px-6 text-center text-white">
        <h1 class="text-3xl font-black uppercase italic tracking-tighter mb-2">Qualified Upgrade Matrix</h1>
        <p class="text-[10px] font-bold uppercase tracking-[0.4em] text-blue-200">Official Contractor Hub • Nationwide 2026</p>
    </header>

    <main class="max-w-md mx-auto px-4 -mt-8 mb-20 relative z-10">
        <div class="glass-card p-8">
            <form id="qualifyForm">
                <div class="step-form active" id="step1">
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-3">01. Selection</label>
                    <p class="text-xs font-bold mb-4">What kind of home improvements are you looking for?</p>
                    <select id="mainService" class="input-pro mb-4" onchange="updateSub()" required>
                        <option value="Roofing">Roofing Solutions</option>
                        <option value="Solar">Solar Panels</option>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Doors">Entry Doors</option>
                        <option value="Garage">Garage System</option>
                        <option value="Deck">Custom Decking</option>
                        <option value="Kitchen">Kitchen Remodel</option>
                        <option value="Bathroom">Bathroom Remodel</option>
                        <option value="Siding">Exterior Siding</option>
                    </select>
                    <select id="isOwner" class="input-pro mb-4" required>
                        <option value="">Are you the home owner?</option>
                        <option value="Yes">Yes, I am the owner</option>
                        <option value="No">No, I am a tenant</option>
                    </select>
                    <button type="button" onclick="goStep('step2')" class="btn-action">Next Step</button>
                </div>

                <div class="step-form" id="step2">
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-3">02. Qualification Matrix</label>
                    <div id="subQuestions"></div>
                    <select id="creditScore" class="input-pro mb-4" required>
                        <option value="">Estimated Credit Score?</option>
                        <option value="Excellent">720+ (Excellent)</option>
                        <option value="Good">660-719 (Good)</option>
                        <option value="Fair">600-659 (Fair)</option>
                        <option value="Needs Work">Below 600</option>
                    </select>
                    <button type="button" onclick="goStep('step3')" class="btn-action">Authorize Appointment</button>
                </div>

                <div class="step-form" id="step3">
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-3">03. Verification</label>
                    <input type="text" id="custAddress" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="flex gap-2">
                        <input type="text" id="custZip" placeholder="Zip" class="input-pro mb-3" required>
                        <input type="text" id="custName" placeholder="Full Name" class="input-pro mb-3" required>
                    </div>
                    <input type="email" id="custEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="tel" id="custPhone" placeholder="Phone Number" class="input-pro mb-3" required>
                    <div class="flex gap-2 mb-4">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appTime" class="input-pro" required>
                            <option value="Morning">Morning</option>
                            <option value="Afternoon">Afternoon</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Confirm & Submit</button>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-4xl mx-auto px-6 mb-20 text-center">
        <h2 class="font-black uppercase text-[10px] tracking-widest text-slate-400 mb-10 italic">Premium Portfolio</h2>
        <div class="grid-matrix">
            <div class="matrix-card"><img src="./WA_1776549716792.jpeg"><h4>Roofing</h4></div>
            <div class="matrix-card"><img src="./WA_1776549781247.jpeg"><h4>Solar Panels</h4></div>
            <div class="matrix-card"><img src="./WA_1776549555727.jpeg"><h4>Windows</h4></div>
            <div class="matrix-card"><img src="./WA_1776549622236.jpeg"><h4>Doors</h4></div>
            <div class="matrix-card"><img src="./WA_1776549862258.jpeg"><h4>Kitchen</h4></div>
            <div class="matrix-card"><img src="./WA_1776549917709.jpeg"><h4>Bathroom</h4></div>
            <div class="matrix-card"><img src="./WA_1776550066723.jpeg"><h4>Garage</h4></div>
            <div class="matrix-card"><img src="./WA_1776549990293.jpeg"><h4>Deck</h4></div>
        </div>
    </section>

    <footer class="bg-slate-900 py-16 px-8 text-white">
        <div class="max-w-4xl mx-auto grid md:grid-cols-3 gap-12 text-[10px] font-bold uppercase text-slate-400">
            <div>
                <h4 class="text-blue-400 mb-4">Headquarters</h4>
                <p class="leading-relaxed">
                    702 Main Street<br>
                    Woodland, California 95695<br>
                    United States
                </p>
            </div>
            <div>
                <h4 class="text-blue-400 mb-4">Authorized Support</h4>
                <p class="lowercase mb-2">ushomeimprovement07@gmail.com</p>
                <p>National Service Network</p>
            </div>
            <div>
                <h4 class="text-blue-400 mb-4">Policy Hub</h4>
                <div class="flex flex-col gap-2">
                    <span onclick="alert('Secured')" class="cursor-pointer">Privacy Policy</span>
                    <span onclick="alert('Verified')" class="cursor-pointer">Terms of Service</span>
                    <span class="text-slate-700 mt-2">© 2026 MATRIX HUB</span>
                </div>
            </div>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-4 mb-6"><h3 class="font-black uppercase">Leads HQ</h3><button onclick="toggleAdmin()" class="text-red-500 font-bold">EXIT</button></div>
        <div id="authPanel" class="text-center py-10">
            <input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="PIN">
            <button onclick="unlock()" class="btn-action max-w-[200px]">Unlock</button>
        </div>
        <div id="leadsList" class="hidden space-y-4 pb-10"></div>
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
            document.querySelectorAll('.step-form').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function updateSub() {
            const s = document.getElementById('mainService').value;
            const c = document.getElementById('subQuestions');
            let h = '';
            if(s === 'Windows') {
                h = `<select id="sq1" class="input-pro mb-4"><option value="">How many windows?</option><option value="3-5">3-5</option><option value="6-10">6-10</option><option value="11+">11+</option></select>
                     <select id="sq2" class="input-pro mb-4"><option value="">Type of windows?</option><option value="Vinyl">Vinyl</option><option value="Wood">Wood</option></select>`;
            } else if(s === 'Roofing') {
                h = `<select id="sq1" class="input-pro mb-4"><option value="">Current roof type?</option><option value="Shingles">Shingles</option><option value="Metal">Metal</option><option value="Tile">Tile</option></select>`;
            } else {
                h = `<p class="text-[10px] uppercase font-bold text-blue-600 mb-4 italic">Standard nationwide qualifying applied.</p>`;
            }
            c.innerHTML = h;
        }
        updateSub();

        document.getElementById('qualifyForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('mainService').value,
                isOwner: document.getElementById('isOwner').value,
                credit: document.getElementById('creditScore').value,
                q1: document.getElementById('sq1')?.value || 'N/A',
                q2: document.getElementById('sq2')?.value || 'N/A',
                name: document.getElementById('custName').value,
                address: document.getElementById('custAddress').value,
                zip: document.getElementById('custZip').value,
                email: document.getElementById('custEmail').value,
                phone: document.getElementById('custPhone').value,
                appDate: document.getElementById('appDate').value,
                appTime: document.getElementById('appTime').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { alert("Authorized! Our Woodland CA team will call you soon."); location.reload(); });
        });

        function toggleAdmin() { document.getElementById('adminPanel').classList.toggle('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-4 border rounded-2xl bg-slate-50 relative mb-4 text-[11px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] font-black absolute top-4 right-4 uppercase">${data[k].service}</span>
                        <h4 class="text-lg font-black">${data[k].name}</h4>
                        <p>📍 ${data[k].address} | 📞 ${data[k].phone}</p>
                        <div class="mt-2 text-blue-800 uppercase text-[9px]">
                            <p>OWNER: ${data[k].isOwner} | CREDIT: ${data[k].credit}</p>
                            <p>DETAILS: ${data[k].q1} / ${data[k].q2}</p>
                            <p>APPOINTMENT: ${data[k].appDate} (${data[k].appTime})</p>
                        </div>
                        <button onclick="del('${k}')" class="text-red-500 mt-2 font-black">DELETE</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Leads';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
