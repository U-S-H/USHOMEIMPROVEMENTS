<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Matrix</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fdfdfd; color: #0f172a; }
        
        /* Modern Glass Cards */
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 24px; box-shadow: 0 10px 30px -5px rgba(0,0,0,0.04); }
        .input-pro { width: 100%; padding: 14px; border: 2px solid #f1f5f9; border-radius: 12px; font-weight: 600; font-size: 14px; outline: none; background: #fff; }
        .input-pro:focus { border-color: var(--accent); }
        
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px; border-radius: 12px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; }

        .step-form { display: none; }
        .step-form.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Screenshot Matching Grid Design */
        .matrix-card { background: white; border-radius: 24px; overflow: hidden; box-shadow: 0 4px 20px rgba(0,0,0,0.05); text-align: center; padding-bottom: 20px; transition: 0.3s; }
        .matrix-card:hover { transform: translateY(-5px); }
        .matrix-card img { width: 100%; height: 200px; object-fit: cover; }
        .matrix-card h4 { font-size: 12px; font-weight: 800; color: #1e3a8a; text-transform: uppercase; margin-top: 15px; letter-spacing: 1px; }
        
        .badge-dispatch { background: #ecfdf5; color: #059669; padding: 4px 12px; border-radius: 50px; font-size: 10px; font-weight: 800; display: inline-block; margin-top: 4px; }
    </style>
</head>
<body>

    <nav class="bg-white border-b px-6 py-5 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3" id="adminTrigger" onclick="handleSecurityTap()">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border">
            <div>
                <span class="block font-black text-sm uppercase tracking-tighter text-blue-900">U.S. Home Improvement</span>
                <div class="badge-dispatch uppercase italic">● Licensed National Dispatch</div>
            </div>
        </div>
    </nav>

    <header class="py-12 px-6 text-center">
        <h1 class="text-3xl font-black uppercase italic tracking-tighter mb-4">Request <span class="text-blue-600">Professional</span> Estimate</h1>
        <p class="text-slate-400 font-bold uppercase text-[9px] tracking-[0.3em]">Connecting You to Authorized Local Crews</p>
    </header>

    <main class="max-w-xl mx-auto px-6 mb-24">
        <div class="glass-card p-8">
            <form id="proDispatchForm">
                <div class="step-form active" id="step1">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-3">01. Choose Service</label>
                    <select id="mainService" class="input-pro mb-4" onchange="loadOptions()" required>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power System</option>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Doors">Doors Installation</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                        <option value="Garage">Garage Door Systems</option>
                        <option value="Deck">Custom Decking</option>
                    </select>
                    <select id="isOwner" class="input-pro" required>
                        <option value="Yes">Yes, I am the Homeowner</option>
                        <option value="No">No, I am a Tenant</option>
                    </select>
                    <button type="button" onclick="goStep('step2')" class="btn-action mt-6">Continue</button>
                </div>

                <div class="step-form" id="step2">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-3">02. Specific Requirements</label>
                    <div id="dynamicContainer"></div>
                    <button type="button" onclick="goStep('step3')" class="btn-action">Set Appointment</button>
                </div>

                <div class="step-form" id="step3">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-3">03. Dispatch Details</label>
                    <input type="text" id="custName" placeholder="Full Name" class="input-pro mb-3" required>
                    <input type="text" id="custAddress" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-3">
                        <input type="text" id="custZip" placeholder="Zip" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Phone Number" class="input-pro" required>
                    </div>
                    
                    <div class="grid grid-cols-2 gap-3 mb-4">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="">Select Time Slot</option>
                            <option value="Morning (10AM - 1PM)">10:00 AM - 1:00 PM</option>
                            <option value="Afternoon (1PM - 4PM)">1:00 PM - 4:00 PM</option>
                            <option value="Evening (4PM - 7PM)">4:00 PM - 7:00 PM</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Request Dispatch</button>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-5xl mx-auto px-6 mb-32 grid grid-cols-2 gap-6">
        <div class="matrix-card"><img src="./WA_1776549716792.jpeg"><h4>Roofing</h4></div>
        <div class="matrix-card"><img src="./WA_1776549781247.jpeg"><h4>Solar</h4></div>
        <div class="matrix-card"><img src="./WA_1776549555727.jpeg"><h4>Windows</h4></div>
        <div class="matrix-card"><img src="./WA_1776549622236.jpeg"><h4>Doors</h4></div>
        <div class="matrix-card"><img src="./WA_1776549862258.jpeg"><h4>Bathroom</h4></div>
        <div class="matrix-card"><img src="./WA_1776549917709.jpeg"><h4>Kitchen</h4></div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-6"><h3 class="font-black">ADMIN DISPATCH HQ</h3><button onclick="closeAdmin()" class="text-red-500 font-bold">EXIT</button></div>
        <div id="authPanel" class="text-center py-20">
            <p class="text-[10px] font-bold text-slate-400 uppercase mb-4 tracking-widest">Verification Required</p>
            <input type="password" id="pin" class="input-pro max-w-[240px] text-center mb-4 text-2xl tracking-[10px]" placeholder="****">
            <button onclick="unlock()" class="btn-action max-w-[240px]">Access Terminal</button>
        </div>
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

        // 5-TAP SECURITY SYSTEM
        let tapCount = 0;
        let tapTimer;
        function handleSecurityTap() {
            tapCount++;
            clearTimeout(tapTimer);
            if(tapCount >= 5) {
                document.getElementById('adminPanel').classList.remove('hidden');
                tapCount = 0;
            }
            tapTimer = setTimeout(() => { tapCount = 0; }, 2000); // Resets if no tap for 2 seconds
        }

        function goStep(id) {
            document.querySelectorAll('.step-form').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function loadOptions() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicContainer');
            let h = '';
            const opts = {
                'Windows': [{ l: 'Window Count?', o: ['1-5','6-10','11-20','21+'] }, { l: 'Material?', o: ['Vinyl','Wood','Fiberglass'] }],
                'Roofing': [{ l: 'Material?', o: ['Shingles','Metal','Tile'] }],
                'Siding': [{ l: 'Style?', o: ['Vinyl','Wood','Fiber Cement'] }],
                'Solar': [{ l: 'Monthly Bill?', o: ['$50-$150','$151-$300','$301+'] }]
            };
            const items = opts[s] || [{ l: 'Details', o: ['Standard','Premium'] }];
            items.forEach((item, i) => {
                h += `<p class="text-[10px] font-black text-slate-400 uppercase mb-2">${item.l}</p>
                      <select id="q${i}" class="input-pro mb-3" onchange="toggleM(${i})">
                        ${item.o.map(o => `<option value="${o}">${o}</option>`).join('')}
                        <option value="Manual">Manual Entry...</option>
                      </select>
                      <input type="text" id="m${i}" placeholder="Enter specific details" class="input-pro hidden mb-3">`;
            });
            container.innerHTML = h;
        }
        loadOptions();

        function toggleM(idx) {
            const s = document.getElementById(`q${idx}`);
            const m = document.getElementById(`m${idx}`);
            if(s.value === 'Manual') m.classList.remove('hidden'); else m.classList.add('hidden');
        }

        document.getElementById('proDispatchForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('mainService').value,
                owner: document.getElementById('isOwner').value,
                spec1: document.getElementById('q0')?.value === 'Manual' ? document.getElementById('m0').value : document.getElementById('q0')?.value,
                name: document.getElementById('custName').value,
                address: document.getElementById('custAddress').value,
                zip: document.getElementById('custZip').value,
                phone: document.getElementById('custPhone').value,
                appointment: `${document.getElementById('appDate').value} (${document.getElementById('appSlot').value})`,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { alert("Authorization Sent! Local contractor will call you."); location.reload(); });
        });

        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-5 border rounded-2xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] absolute top-4 right-4 uppercase font-black">${data[k].service}</span>
                        <h4 class="text-lg font-black uppercase text-blue-900">${data[k].name}</h4>
                        <p>📍 ${data[k].address}</p>
                        <div class="mt-4 border-t pt-3 flex flex-col gap-1">
                            <p>📞: ${data[k].phone}</p>
                            <p>🛠 Spec: ${data[k].spec1 || 'N/A'}</p>
                            <p class="text-emerald-700 font-black">📅 Appt: ${data[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-3 text-red-500 font-black uppercase text-[8px]">Delete Lead</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Active Leads';
            });
        }
        function del(id) { if(confirm('Delete permanently?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
