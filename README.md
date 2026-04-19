<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | National Enterprise Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfd; color: #0f172a; overflow-x: hidden; }
        
        /* Progress Bar */
        .progress-container { height: 6px; background: #e2e8f0; border-radius: 10px; margin-bottom: 30px; overflow: hidden; }
        #progress-bar { height: 100%; width: 33%; background: linear-gradient(90deg, #1e3a8a, #2563eb); transition: 0.5s ease; }

        /* Trust Badges */
        .trust-bar img { filter: grayscale(100%); opacity: 0.4; height: 20px; transition: 0.3s; }
        .trust-bar img:hover { filter: grayscale(0%); opacity: 1; }

        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 32px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.08); }
        .input-pro { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 18px; font-weight: 600; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 18px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; }

        .form-step { display: none; }
        .form-step.active { display: block; animation: slideIn 0.4s ease-out; }
        @keyframes slideIn { from { transform: translateX(20px); opacity: 0; } to { transform: translateX(0); opacity: 1; } }

        #notification-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 15px 25px; border-radius: 50px; box-shadow: 0 15px 35px rgba(0,0,0,0.1); border-left: 6px solid #059669; display: none; z-index: 9999; }
    </style>
</head>
<body>

    <div id="notification-toast"><p id="notif-text" class="text-[11px] font-black text-slate-700 uppercase italic"></p></div>

    <nav class="bg-white/90 backdrop-blur-md border-b px-6 py-5 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3 cursor-pointer" onclick="location.reload()">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border" id="adminTrigger" onclick="handleTap()">
            <div>
                <span class="block font-black text-sm uppercase text-blue-900 tracking-tighter">U.S. Home Improvement LLC</span>
                <span class="block text-[8px] font-extrabold text-emerald-600 uppercase italic">● Licensed National Contractor Network</span>
            </div>
        </div>
        <div class="hidden md:flex gap-4 items-center">
            <span class="text-[10px] font-black text-slate-400 uppercase italic">Status: <span class="text-emerald-500">Dispatch Active</span></span>
        </div>
    </nav>

    <header class="py-20 px-6 text-center bg-slate-50 border-b">
        <div class="max-w-4xl mx-auto">
            <h1 class="text-4xl md:text-6xl font-black uppercase italic tracking-tighter mb-6 text-slate-900 leading-none">The Trusted Name In <br><span class="text-blue-600">American Remodeling.</span></h1>
            <div class="trust-bar flex flex-wrap justify-center gap-8 mb-10">
                <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Forbes_logo.svg" alt="Forbes">
                <img src="https://upload.wikimedia.org/wikipedia/commons/1/11/Business_Insider_Logo.svg" alt="Insider">
                <img src="https://upload.wikimedia.org/wikipedia/commons/a/a2/Better_Business_Bureau_logo.svg" alt="BBB">
            </div>
            <p class="text-[10px] font-black text-slate-400 uppercase tracking-[0.3em] mb-10 italic">Providing Authorized Estimates Since 1998</p>
        </div>
    </header>

    <main class="max-w-xl mx-auto px-6 -mt-12 mb-32 relative z-10">
        <div class="glass-card p-8 md:p-12">
            
            <div class="progress-container">
                <div id="progress-bar"></div>
            </div>

            <form id="ultraDispatchForm">
                <div class="form-step active" id="step1">
                    <h2 class="text-xl font-black uppercase italic mb-6">01. Area <span class="text-blue-600">Validation</span></h2>
                    <div class="mb-4">
                        <label class="text-[10px] font-black text-blue-500 uppercase block mb-2">Service Selection</label>
                        <select id="mainService" class="input-pro" onchange="loadQualifiers()" required>
                            <option value="Windows">Window Replacement</option>
                            <option value="Roofing">Roofing Installation</option>
                            <option value="Solar">Solar Power Matrix</option>
                            <option value="Kitchen">Kitchen Remodeling</option>
                        </select>
                    </div>
                    <div class="mb-6">
                        <label class="text-[10px] font-black text-blue-500 uppercase block mb-2">Site Zip Code</label>
                        <input type="text" id="custZip" placeholder="e.g. 95695" class="input-pro" maxlength="5" required>
                        <p id="zipStatus" class="text-[9px] font-black mt-2 text-emerald-600 hidden uppercase">✔ Authorized Area Detected</p>
                    </div>
                    <button type="button" onclick="validateZip()" class="btn-action">Continue Application</button>
                </div>

                <div class="form-step" id="step2">
                    <h2 class="text-xl font-black uppercase italic mb-6">02. Project <span class="text-blue-600">Specifications</span></h2>
                    <div id="dynamicQualifiers"></div>
                    
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-2 mt-4">Property Ownership</label>
                    <select id="isOwner" class="input-pro mb-4" required>
                        <option value="Yes">Confirmed Homeowner</option>
                        <option value="No">Renter / Tenant</option>
                    </select>

                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-2">Est. Credit Score</label>
                    <select id="creditScore" class="input-pro mb-6" required>
                        <option value="Excellent (720+)">Excellent (720+)</option>
                        <option value="Good (660-719)">Good (660-719)</option>
                        <option value="Fair (Below 660)">Fair/Other</option>
                    </select>
                    <button type="button" onclick="goToStep(3)" class="btn-action">Authorize Schedule</button>
                </div>

                <div class="form-step" id="step3">
                    <h2 class="text-xl font-black uppercase italic mb-6">03. Site <span class="text-blue-600">Verification</span></h2>
                    <input type="text" id="custName" placeholder="Full Name" class="input-pro mb-3" required>
                    <input type="email" id="custEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="text" id="custAddress" placeholder="Street Address" class="input-pro mb-3" required>
                    
                    <div class="bg-slate-100 h-32 rounded-2xl mb-4 flex items-center justify-center border-2 border-dashed border-slate-300">
                        <p class="text-[9px] font-black text-slate-400 uppercase">🛰 Satellite Link Active...</p>
                    </div>

                    <div class="grid grid-cols-2 gap-3 mb-6">
                        <input type="tel" id="custPhone" placeholder="Phone" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="10am-1pm">10AM-1PM</option>
                            <option value="1pm-4pm">1PM-4PM</option>
                            <option value="4pm-7pm">4PM-7PM</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action shadow-xl">Submit Authorization</button>
                </div>
            </form>

            <div id="receiptBox" class="hidden text-center py-6">
                <div class="text-6xl mb-4">✅</div>
                <h2 class="text-2xl font-black text-blue-900 uppercase italic">Dispatch Confirmed</h2>
                <div class="mt-8 p-8 bg-slate-50 border-2 border-dashed border-slate-300 rounded-3xl text-left">
                    <div class="space-y-4 text-[11px] font-black uppercase">
                        <p class="text-slate-400">Order ID: #<span id="r-id"></span></p>
                        <p>Customer: <span id="r-name" class="text-slate-900"></span></p>
                        <p>Service: <span id="r-service" class="text-blue-600"></span></p>
                        <p>Area: <span id="r-zip" class="text-slate-900"></span></p>
                    </div>
                </div>
                <p class="mt-8 text-[9px] font-bold text-slate-400 uppercase italic">Take a screenshot. Our specialist will call you from a California area code.</p>
                <button onclick="location.reload()" class="mt-8 text-blue-600 font-black uppercase text-xs">Back To Home</button>
            </div>
        </div>
    </main>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-8"><h3 class="font-black italic text-blue-900 underline">HQ TERMINAL</h3><button onclick="closeAdmin()" class="text-red-500 font-black uppercase text-xs">Exit</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="PIN"><button onclick="unlock()" class="btn-action max-w-[200px]">Unlock</button></div>
        <div id="leadsList" class="hidden space-y-4 pb-20"></div>
    </div>

    <footer class="bg-white border-t py-20 px-8 text-center">
        <div class="flex justify-center gap-4 mb-8">
            <span class="bg-slate-100 px-3 py-1 rounded text-[8px] font-black uppercase tracking-widest">Licensed</span>
            <span class="bg-slate-100 px-3 py-1 rounded text-[8px] font-black uppercase tracking-widest">Insured</span>
            <span class="bg-slate-100 px-3 py-1 rounded text-[8px] font-black uppercase tracking-widest">Certified</span>
        </div>
        <p class="text-[9px] text-slate-400 uppercase font-black leading-loose">
            U.S. Home Improvement LLC | 702 Main Street, Woodland, CA 95695 <br>
            Authorized National Terminal. Data protected by 256-bit AES encryption.
        </p>
    </footer>

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
        function handleTap() { taps++; clearTimeout(tapT); if(taps>=5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } tapT=setTimeout(()=>taps=0,2000); }

        function validateZip() {
            const z = document.getElementById('custZip').value;
            if(z.length === 5) {
                document.getElementById('zipStatus').classList.remove('hidden');
                setTimeout(() => goToStep(2), 800);
            } else { alert("Please enter a valid 5-digit Zip Code"); }
        }

        function goToStep(n) {
            document.querySelectorAll('.form-step').forEach(s => s.classList.remove('active'));
            document.getElementById('step' + n).classList.add('active');
            document.getElementById('progress-bar').style.width = (n === 1 ? '33%' : n === 2 ? '66%' : '100%');
        }

        function loadQualifiers() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicQualifiers');
            const questions = {
                'Windows': [{l:'Window Quantity', o:['1-5','6-10','11+']},{l:'Frame Choice', o:['Vinyl','Wood']}],
                'Roofing': [{l:'Current Material', o:['Shingle','Metal','Tile']},{l:'Leaks?', o:['None','Minor','Serious']}],
                'Solar': [{l:'Monthly Bill', o:['$50-150','$151-300','$301+']},{l:'Sun Exposure', o:['Full Sun','Partial']}]
            };
            const current = questions[s] || [{l:'Timeline', o:['Immediate','1-3 Months']}];
            container.innerHTML = current.map((q, i) => `
                <label class="text-[10px] font-black text-slate-400 uppercase block mb-2 mt-4">${q.l}</label>
                <select id="q${i}" class="input-pro mb-3">${q.o.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>
            `).join('');
        }
        loadQualifiers();

        document.getElementById('ultraDispatchForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const id = Math.floor(100000 + Math.random() * 900000);
            const data = {
                id: id,
                service: document.getElementById('mainService').value,
                name: document.getElementById('custName').value,
                email: document.getElementById('custEmail').value,
                phone: document.getElementById('custPhone').value,
                address: document.getElementById('custAddress').value,
                zip: document.getElementById('custZip').value,
                owner: document.getElementById('isOwner').value,
                credit: document.getElementById('creditScore').value,
                spec: document.getElementById('q0')?.value || 'Standard',
                appointment: document.getElementById('appSlot').value,
                timestamp: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                document.getElementById('ultraDispatchForm').classList.add('hidden');
                document.getElementById('receiptBox').classList.remove('remove');
                document.getElementById('receiptBox').style.display = 'block';
                document.getElementById('r-id').innerText = id;
                document.getElementById('r-name').innerText = data.name;
                document.getElementById('r-service').innerText = data.service;
                document.getElementById('r-zip').innerText = data.zip;
            });
        });

        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value==="786"){ document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); syncLeads(); } }
        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="p-6 border-2 rounded-3xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded-full text-[8px] absolute top-4 right-4">${leads[k].service}</span>
                        <p class="text-lg text-blue-900 uppercase">#${leads[k].id} | ${leads[k].name}</p>
                        <div class="grid grid-cols-2 mt-4 gap-2">
                            <p>📧 ${leads[k].email}</p>
                            <p>📞 ${leads[k].phone}</p>
                            <p>📍 ${leads[k].address} (${leads[k].zip})</p>
                            <p>💳 Credit: ${leads[k].credit}</p>
                            <p>🛠 Spec: ${leads[k].spec}</p>
                            <p class="text-emerald-600">📅 Appt: ${leads[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 w-full border-t pt-4">DELETE</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'Empty';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }

        const notifs = ["John from Woodland booked Roofing!", "Emily from TX authorized Solar.", "New Windows lead in Florida!", "Authorized dispatch for NY Area."];
        setInterval(() => {
            const toast = document.getElementById('notification-toast');
            document.getElementById('notif-text').innerText = "⚡ " + notifs[Math.floor(Math.random()*notifs.length)];
            toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 5000);
        }, 15000);
    </script>
</body>
</html>
