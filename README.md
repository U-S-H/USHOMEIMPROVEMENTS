<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | National Dispatch</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; }
        .glass-card { background: white; border-radius: 32px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.08); border: 1px solid #f1f5f9; }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; font-size: 14px; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 16px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; }
        .step-form { display: none; }
        .step-form.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        #receipt-screen { display: none; text-align: center; }
    </style>
</head>
<body>

    <nav class="bg-white border-b px-6 py-5 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3" id="adminTrigger" onclick="handleTap()">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border">
            <div>
                <span class="block font-black text-sm uppercase text-blue-900">U.S. Home Improvement LLC</span>
                <span class="block text-[9px] font-extrabold text-emerald-600 uppercase italic">● Authorized Dispatch Terminal</span>
            </div>
        </div>
    </nav>

    <main class="max-w-xl mx-auto px-6 py-12 relative z-10">
        <div class="glass-card p-8 md:p-12" id="main-container">
            
            <form id="proDispatchForm">
                <div class="step-form active" id="step1">
                    <h2 class="text-2xl font-black uppercase italic mb-6">Start Your <span class="text-blue-600">Project</span></h2>
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-2">Category</label>
                    <select id="mainService" class="input-pro mb-4" onchange="loadQualifiers()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power System</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                    </select>
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-2">Ownership Status</label>
                    <select id="isOwner" class="input-pro mb-6" required>
                        <option value="Yes">I am the Legal Homeowner</option>
                        <option value="No">I am a Tenant / Renter</option>
                    </select>
                    <button type="button" onclick="goStep('step2')" class="btn-action">Next Step</button>
                </div>

                <div class="step-form" id="step2">
                    <h2 class="text-xl font-black uppercase italic mb-6">Qualifying <span class="text-blue-600">Details</span></h2>
                    <div id="dynamicContainer"></div>
                    
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-2 mt-4">Estimated Credit Score (For Financing)</label>
                    <select id="creditScore" class="input-pro mb-6" required>
                        <option value="Excellent (720+)">Excellent (720+)</option>
                        <option value="Good (660-719)">Good (660-719)</option>
                        <option value="Fair (600-659)">Fair (600-659)</option>
                        <option value="Poor (Below 600)">Poor (Below 600)</option>
                    </select>

                    <button type="button" onclick="goStep('step3')" class="btn-action">Final Step</button>
                </div>

                <div class="step-form" id="step3">
                    <h2 class="text-xl font-black uppercase italic mb-6">Authorized <span class="text-blue-600">Schedule</span></h2>
                    <input type="text" id="custName" placeholder="Full Name" class="input-pro mb-3" required>
                    <input type="email" id="custEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="text" id="custAddress" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-3">
                        <input type="text" id="custZip" placeholder="Zip" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Mobile Phone" class="input-pro" required>
                    </div>
                    <div class="grid grid-cols-2 gap-3 mb-6">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="10am-1pm">10:00 AM - 1:00 PM</option>
                            <option value="1pm-4pm">1:00 PM - 4:00 PM</option>
                            <option value="4pm-7pm">4:00 PM - 7:00 PM</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Confirm Appointment</button>
                </div>
            </form>

            <div id="receipt-screen">
                <div class="text-emerald-500 text-6xl mb-4">✔</div>
                <h2 class="text-2xl font-black uppercase italic text-blue-900">Appointment Set!</h2>
                <p class="text-slate-500 text-xs font-bold uppercase mt-2">Please save this receipt for your records.</p>
                <div class="mt-8 p-6 bg-slate-50 rounded-2xl text-left border border-dashed border-slate-300">
                    <p class="text-[10px] text-slate-400 font-black uppercase">Service Category</p>
                    <p id="r-service" class="font-black text-blue-900 mb-3"></p>
                    
                    <p class="text-[10px] text-slate-400 font-black uppercase">Homeowner Name</p>
                    <p id="r-name" class="font-black text-slate-700 mb-3"></p>

                    <p class="text-[10px] text-slate-400 font-black uppercase">Authorized Schedule</p>
                    <p id="r-date" class="font-black text-emerald-600 mb-3"></p>

                    <p class="text-[10px] text-slate-400 font-black uppercase">Site Location</p>
                    <p id="r-address" class="font-black text-slate-700"></p>
                </div>
                <p class="text-[9px] font-bold text-slate-400 mt-6 uppercase italic">A local licensed contractor will call you at the provided number to verify dispatch.</p>
                <button onclick="location.reload()" class="mt-8 text-blue-600 font-black uppercase text-xs">Back To Home</button>
            </div>

        </div>
    </main>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-4 mb-6"><h3 class="font-black italic text-blue-900">HQ DISPATCH TERMINAL</h3><button onclick="closeAdmin()" class="text-red-500 font-black">EXIT</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="ENTER PIN"><button onclick="unlock()" class="btn-action max-w-[200px]">ACCESS</button></div>
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

        function loadQualifiers() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicContainer');
            const data = {
                'Windows': [{l:'Window Count', o:['1-5','6-10','11-20','21+']},{l:'Frame Type', o:['Vinyl','Wood','Aluminum']}],
                'Roofing': [{l:'Current Material', o:['Asphalt','Metal','Tile']},{l:'Any Leaks?', o:['No Leaks','Minor Leaks','Emergency Leaks']}],
                'Solar': [{l:'Monthly Bill', o:['$50-150','$151-300','$301+']},{l:'Roof Exposure', o:['Full Sun','Partial Shade','Heavy Shade']}]
            };
            const current = data[s] || [{l:'Project Timeline', o:['Immediate','1-3 Months','Planning Only']}];
            container.innerHTML = current.map((item, i) => `
                <p class="text-[9px] font-black text-slate-400 uppercase mb-2 mt-4">${item.l}</p>
                <select id="q${i}" class="input-pro mb-3">
                    ${item.o.map(o=>`<option value="${o}">${o}</option>`).join('')}
                </select>
            `).join('');
        }
        loadQualifiers();

        document.getElementById('proDispatchForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const service = document.getElementById('mainService').value;
            const name = document.getElementById('custName').value;
            const address = document.getElementById('custAddress').value;
            const appt = `${document.getElementById('appDate').value} @ ${document.getElementById('appSlot').value}`;

            const data = {
                service: service,
                owner: document.getElementById('isOwner').value,
                credit: document.getElementById('creditScore').value,
                name: name,
                email: document.getElementById('custEmail').value,
                phone: document.getElementById('custPhone').value,
                address: address,
                zip: document.getElementById('custZip').value,
                spec: document.getElementById('q0')?.value || 'Standard',
                appointment: appt,
                timestamp: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                // Show Receipt Screen
                document.getElementById('proDispatchForm').style.display = 'none';
                document.getElementById('receipt-screen').style.display = 'block';
                document.getElementById('r-service').innerText = service.toUpperCase();
                document.getElementById('r-name').innerText = name;
                document.getElementById('r-date').innerText = appt;
                document.getElementById('r-address').innerText = address;
            });
        });

        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        
        function sync() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="p-6 border-2 border-slate-100 rounded-3xl bg-white relative mb-4 text-[11px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded-full text-[8px] absolute top-4 right-4 uppercase font-black">${leads[k].service}</span>
                        <h4 class="text-lg font-black uppercase italic text-blue-900 mb-2">${leads[k].name}</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-x-6 gap-y-2 text-slate-600">
                            <p>📧 Email: <span class="text-blue-600 underline">${leads[k].email}</span></p>
                            <p>📞 Phone: <span class="text-slate-900">${leads[k].phone}</span></p>
                            <p>📍 Address: ${leads[k].address} (${leads[k].zip})</p>
                            <p>👤 Owner: ${leads[k].owner}</p>
                            <p>💳 Credit: <span class="text-orange-600">${leads[k].credit}</span></p>
                            <p>🛠 Spec: ${leads[k].spec}</p>
                            <p class="col-span-full mt-3 pt-3 border-t text-emerald-600 font-black uppercase italic">📅 Appt: ${leads[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black border-t w-full pt-4 text-center">DELETE PERMANENTLY</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Active Leads';
            });
        }
        function del(id) { if(confirm('Delete Lead?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
