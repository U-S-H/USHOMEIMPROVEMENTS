<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | Professional National Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon-blue: #2563eb; --neon-cyan: #06b6d4; --glass: rgba(255, 255, 255, 0.8); }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f0f4f8; color: #1e293b; overflow-x: hidden; }
        
        /* Modern Neon Effects */
        .neon-glow { box-shadow: 0 0 20px rgba(37, 99, 235, 0.15); border: 1px solid rgba(37, 99, 235, 0.2); }
        .neon-text { color: var(--neon-blue); text-shadow: 0 0 8px rgba(37, 99, 235, 0.3); }
        
        .hero-gradient { background: radial-gradient(circle at top right, #eff6ff, #ffffff); position: relative; padding: 120px 20px; }
        .hero-gradient::before { content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 100%; background: url('https://www.transparenttextures.com/patterns/cubes.png'); opacity: 0.05; }

        .glass-card { background: var(--glass); backdrop-filter: blur(12px); border-radius: 32px; border: 1px solid rgba(255,255,255,0.4); box-shadow: 0 30px 60px -12px rgba(0,0,0,0.08); transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1); }
        .glass-card:hover { transform: translateY(-5px); box-shadow: 0 40px 80px -15px rgba(37, 99, 235, 0.1); }

        .step-form { display: none; }
        .step-form.active { display: block; animation: slideIn 0.6s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: scale(0.95); } to { opacity: 1; transform: scale(1); } }

        .input-pro { width: 100%; padding: 18px; border: 2px solid #e2e8f0; border-radius: 16px; font-weight: 600; transition: 0.3s; background: white; margin-bottom: 15px; }
        .input-pro:focus { border-color: var(--neon-blue); box-shadow: 0 0 15px rgba(37, 99, 235, 0.1); outline: none; }
        
        .btn-action { background: linear-gradient(135deg, var(--neon-blue), var(--neon-cyan)); color: white; padding: 20px; border-radius: 16px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; }
        
        .matrix-card { background: white; border-radius: 24px; overflow: hidden; border: 1px solid #f1f5f9; transition: 0.4s; }
        .matrix-card:hover { transform: scale(1.03) rotate(1deg); box-shadow: 0 20px 30px rgba(0,0,0,0.05); }
        .matrix-card img { width: 100%; height: 140px; object-fit: cover; }
        
        .badge-live { display: inline-flex; align-items: center; gap: 6px; background: #ecfdf5; color: #059669; padding: 4px 12px; border-radius: 50px; font-size: 10px; font-weight: 800; }
    </style>
</head>
<body>

    <nav class="bg-white/80 backdrop-blur-md border-b px-8 py-4 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" class="h-11 w-11 rounded-2xl shadow-lg border">
            <div>
                <span onclick="toggleAdmin()" class="block font-black text-sm uppercase tracking-tighter cursor-pointer neon-text">U.S. Home Improvement</span>
                <div class="badge-live uppercase">● Verified 50-State Network</div>
            </div>
        </div>
        <div class="hidden lg:flex gap-8 text-[11px] font-extrabold uppercase text-slate-400 tracking-widest">
            <span>California Hub</span>
            <span class="text-blue-600">Licensed Experts</span>
            <span>Est. 2026</span>
        </div>
    </nav>

    <header class="hero-gradient text-center">
        <div class="max-w-4xl mx-auto px-6">
            <h1 class="text-5xl md:text-7xl font-extrabold uppercase italic tracking-tighter mb-6 leading-none">
                National <span class="neon-text">Upgrade</span> Hub
            </h1>
            <p class="text-lg text-slate-500 font-semibold max-w-2xl mx-auto leading-relaxed">
                Connect with local authorized contractors for premium home improvements. Guaranteed licensing, bonding, and lifetime warranties.
            </p>
        </div>
    </header>

    <main class="max-w-xl mx-auto px-6 -mt-20 mb-32">
        <div class="glass-card p-10">
            <form id="trustedForm">
                <div class="step-form active" id="step1">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4 tracking-[0.2em]">01. Project Scope</label>
                    <select id="mainService" class="input-pro" onchange="generateQuestions()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Matrix System</option>
                        <option value="Siding">Exterior Siding</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Luxury Remodel</option>
                        <option value="Garage">Garage Door Systems</option>
                        <option value="Deck">Custom Decking</option>
                    </select>
                    <select id="isOwner" class="input-pro" required>
                        <option value="Yes">I am the Homeowner</option>
                        <option value="No">I am a Tenant / Manager</option>
                    </select>
                    <button type="button" onclick="nextStep('step2')" class="btn-action">Get Free Quote</button>
                </div>

                <div class="step-form" id="step2">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4 tracking-[0.2em]">02. Technical Assessment</label>
                    <div id="dynamicContainer"></div>
                    <button type="button" onclick="nextStep('step3')" class="btn-action">Finalize Details</button>
                </div>

                <div class="step-form" id="step3">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4 tracking-[0.2em]">03. Personal Information</label>
                    <input type="text" id="custName" placeholder="Full Legal Name" class="input-pro" required>
                    <input type="text" id="custAddress" placeholder="Site Street Address" class="input-pro" required>
                    <div class="grid grid-cols-2 gap-4">
                        <input type="text" id="custZip" placeholder="Zip Code" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Mobile Number" class="input-pro" required>
                    </div>
                    <input type="email" id="custEmail" placeholder="Email for Estimates" class="input-pro" required>
                    
                    <div class="grid grid-cols-2 gap-4">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appTime" class="input-pro" required>
                            <option value="Morning">Morning Window</option>
                            <option value="Afternoon">Afternoon Window</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Authorize Local Dispatch</button>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-5xl mx-auto px-8 mb-40 text-center">
        <h3 class="font-black text-xs uppercase tracking-[0.5em] text-slate-400 mb-16">Core Matrix Portfolio</h3>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8">
            <div class="matrix-card"><img src="./WA_1776549716792.jpeg"><h4>Roofing</h4></div>
            <div class="matrix-card"><img src="./WA_1776549781247.jpeg"><h4>Solar Power</h4></div>
            <div class="matrix-card"><img src="./WA_1776549555727.jpeg"><h4>Windows</h4></div>
            <div class="matrix-card"><img src="./WA_1776549622236.jpeg"><h4>Doors</h4></div>
            <div class="matrix-card"><img src="./WA_1776549862258.jpeg"><h4>Kitchen</h4></div>
            <div class="matrix-card"><img src="./WA_1776549917709.jpeg"><h4>Bathroom</h4></div>
            <div class="matrix-card"><img src="./WA_1776550066723.jpeg"><h4>Garage</h4></div>
            <div class="matrix-card"><img src="./WA_1776549990293.jpeg"><h4>Deck</h4></div>
        </div>
    </section>

    <footer class="bg-white border-t py-24 px-8 text-slate-800">
        <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-16">
            <div>
                <h4 class="font-black uppercase text-xs mb-8 tracking-widest neon-text">U.S. Corporate HQ</h4>
                <p class="font-bold text-sm leading-relaxed text-slate-500">
                    702 Main Street, Woodland<br>
                    California 95695, USA<br>
                    Licensed Network ID: #CA-786-2026
                </p>
                <p class="mt-4 text-xs font-black lowercase text-blue-600">ushomeimprovement07@gmail.com</p>
            </div>
            <div>
                <h4 class="font-black uppercase text-xs mb-8 tracking-widest text-slate-400">Our Operations</h4>
                <p class="text-xs font-bold leading-relaxed text-slate-500 uppercase italic">
                    We operate a nationwide authorized network. Once your appointment is confirmed, our local licensed contractor from your specific state will contact you for a technical site survey.
                </p>
            </div>
            <div>
                <h4 class="font-black uppercase text-xs mb-8 tracking-widest text-slate-400">Security & Privacy</h4>
                <div class="flex flex-col gap-3 text-[10px] font-black uppercase">
                    <span class="cursor-pointer hover:text-blue-600">Privacy & Data Encryption</span>
                    <span class="cursor-pointer hover:text-blue-600">Consumer Rights (CCPA)</span>
                    <span class="text-slate-300 mt-4">© 2026 National Matrix Hub</span>
                </div>
            </div>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-slate-50 z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-6 mb-10">
            <h2 class="text-2xl font-black uppercase italic tracking-tighter">Matrix Control Center</h2>
            <button onclick="toggleAdmin()" class="bg-red-50 text-red-600 px-6 py-2 rounded-xl font-black text-xs uppercase">Close</button>
        </div>
        <div id="authPanel" class="text-center py-20">
            <input type="password" id="pin" class="input-pro max-w-[260px] text-center text-3xl" placeholder="PIN">
            <button onclick="accessTerminal()" class="btn-action max-w-[260px] mt-4">Unlock Admin</button>
        </div>
        <div id="leadsList" class="hidden grid gap-6 pb-20"></div>
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
            document.querySelectorAll('.step-form').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function generateQuestions() {
            const service = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicContainer');
            let h = '';

            const items = {
                'Windows': ['Estimated Window Count', 'Window Frame Material (Vinyl, Wood, etc.)'],
                'Roofing': ['Current Roof Condition', 'Square Footage (Approx)'],
                'Solar': ['Monthly Electric Bill', 'Roof Orientation'],
                'Siding': ['Material Type Wanted', 'Approx Square Footage']
            };

            const selected = items[service] || ['Project Details', 'Estimated Budget'];

            selected.forEach((q, index) => {
                h += `<p class="text-[11px] font-black uppercase text-slate-400 mb-2">${q}</p>
                      <select id="sel${index}" class="input-pro" onchange="toggleM(${index})">
                        <option value="Standard">Standard Option</option>
                        <option value="Premium">Premium Upgrade</option>
                        <option value="Manual">Manual Entry (Specify)...</option>
                      </select>
                      <input type="text" id="man${index}" placeholder="Type details here..." class="input-pro hidden">`;
            });

            container.innerHTML = h;
        }
        generateQuestions();

        function toggleM(idx) {
            const s = document.getElementById(`sel${idx}`);
            const m = document.getElementById(`man${idx}`);
            if(s.value === 'Manual') m.classList.remove('hidden'); else m.classList.add('hidden');
        }

        document.getElementById('trustedForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const service = document.getElementById('mainService').value;
            const data = {
                service: service,
                owner: document.getElementById('isOwner').value,
                details: `${document.getElementById('sel0')?.value === 'Manual' ? document.getElementById('man0').value : document.getElementById('sel0')?.value} | ${document.getElementById('sel1')?.value === 'Manual' ? document.getElementById('man1').value : document.getElementById('sel1')?.value}`,
                name: document.getElementById('custName').value,
                address: document.getElementById('custAddress').value,
                zip: document.getElementById('custZip').value,
                phone: document.getElementById('custPhone').value,
                email: document.getElementById('custEmail').value,
                appointment: `${document.getElementById('appDate').value} @ ${document.getElementById('appTime').value}`,
                timestamp: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                alert(`SUCCESS! Your appointment for ${service} is authorized. A local licensed contractor from your area will reach out to you within 24 hours.`);
                location.reload();
            });
        });

        function toggleAdmin() { document.getElementById('adminPanel').classList.toggle('hidden'); }
        function accessTerminal() {
            if(document.getElementById('pin').value === "786") {
                document.getElementById('authPanel').classList.add('hidden');
                document.getElementById('leadsList').classList.remove('hidden');
                syncLeads();
            }
        }

        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-8 border rounded-3xl bg-white shadow-sm relative">
                        <span class="bg-blue-600 text-white px-4 py-1.5 rounded-full text-[10px] font-black absolute top-6 right-8 uppercase">${data[k].service}</span>
                        <h4 class="text-2xl font-black uppercase mb-1">${data[k].name}</h4>
                        <p class="font-bold text-slate-400 mb-6">📍 ${data[k].address} (${data[k].zip})</p>
                        <div class="grid md:grid-cols-2 gap-6 py-6 border-t border-slate-100">
                            <div class="text-[11px] uppercase font-bold text-slate-600">
                                <p>📞 Phone: ${data[k].phone}</p>
                                <p>✉️ Email: ${data[k].email}</p>
                            </div>
                            <div class="text-[11px] uppercase font-bold text-blue-600">
                                <p>👤 Owner: ${data[k].owner}</p>
                                <p>🛠 Specs: ${data[k].details}</p>
                            </div>
                        </div>
                        <div class="bg-slate-50 p-4 rounded-2xl flex justify-between items-center">
                            <span class="text-[10px] font-black uppercase text-slate-500">📅 ${data[k].appointment}</span>
                            <button onclick="delLead('${k}')" class="text-red-500 font-black text-xs uppercase">Delete</button>
                        </div>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || '<p class="text-center font-bold text-slate-300">Terminal Empty</p>';
            });
        }
        function delLead(id) { if(confirm('Delete permanently?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
