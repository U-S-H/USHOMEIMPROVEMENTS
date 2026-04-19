<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | Verified National Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #0f172a; overflow-x: hidden; }
        
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 32px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.06); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; font-size: 14px; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); outline: none; }
        
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 16px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; }

        /* Fake Notification Pop-up */
        #notification-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 12px 20px; border-radius: 15px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); border-left: 5px solid #059669; display: none; z-index: 9999; animation: slideIn 0.5s ease; }
        @keyframes slideIn { from { transform: translateX(-100%); opacity: 0; } to { transform: translateX(0); opacity: 1; } }

        .matrix-card { background: white; border-radius: 28px; overflow: hidden; box-shadow: 0 10px 20px rgba(0,0,0,0.03); border: 1px solid #f8fafc; text-align: center; cursor: pointer; }
        .matrix-card img { width: 100%; height: 200px; object-fit: cover; transition: 0.5s; }
        .matrix-card:hover img { transform: scale(1.05); }
        .matrix-card h4 { font-size: 13px; font-weight: 800; color: #1e3a8a; padding: 15px 0; text-transform: uppercase; }

        .step-form { display: none; }
        .step-form.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .trust-badge { display: inline-flex; align-items: center; gap: 5px; background: #f0fdf4; color: #166534; padding: 4px 10px; border-radius: 50px; font-size: 10px; font-weight: 800; }
    </style>
</head>
<body>

    <div id="notification-toast">
        <p id="notif-text" class="text-[11px] font-bold text-slate-700"></p>
    </div>

    <nav class="bg-white border-b px-6 py-5 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3" id="secureTrigger" onclick="handleTap()">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border">
            <div>
                <span class="block font-black text-sm uppercase text-blue-900 italic">U.S. Home Improvement</span>
                <div class="trust-badge uppercase italic">● 50-State Licensed Network</div>
            </div>
        </div>
        <div class="hidden md:flex items-center gap-4 text-[10px] font-black text-slate-400">
            <span class="text-blue-600">A+ RATING</span>
            <span>WOODLAND, CA HUB</span>
        </div>
    </nav>

    <header class="py-16 px-6 text-center bg-slate-50">
        <h1 class="text-4xl md:text-6xl font-black uppercase italic tracking-tighter mb-4 text-slate-900 leading-none">
            Authorized <span class="text-blue-600">National</span> Hub
        </h1>
        <div class="flex justify-center gap-2 mb-6">
            <span class="text-yellow-400 text-xl">★★★★★</span>
            <span class="text-[10px] font-black self-center text-slate-500 uppercase">4.9/5 Based on 12,400+ Reviews</span>
        </div>
    </header>

    <main class="max-w-xl mx-auto px-6 -mt-10 mb-32 relative z-10">
        <div class="glass-card p-8 md:p-12">
            <form id="masterForm">
                <div class="step-form active" id="step1">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4">01. Choose Your Project</label>
                    <select id="mainService" class="input-pro mb-4" onchange="updateOptions()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Siding">Exterior Siding</option>
                        <option value="Doors">Custom Doors</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                    </select>
                    <select id="isOwner" class="input-pro" required>
                        <option value="Yes">Yes, I am the Homeowner</option>
                        <option value="No">No, I am a Tenant</option>
                    </select>
                    <button type="button" onclick="goStep('step2')" class="btn-action mt-6">Get Guaranteed Quote</button>
                </div>

                <div class="step-form" id="step2">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4">02. Project Details</label>
                    <div id="dynamicFields"></div>
                    <button type="button" onclick="goStep('step3')" class="btn-action">Authorize Appointment</button>
                </div>

                <div class="step-form" id="step3">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4">03. Site Authorization</label>
                    <input type="text" id="custName" placeholder="Full Legal Name" class="input-pro mb-3" required>
                    <input type="text" id="custAddress" placeholder="Site Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-3">
                        <input type="text" id="custZip" placeholder="Zip Code" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Mobile Number" class="input-pro" required>
                    </div>
                    <div class="grid grid-cols-2 gap-3 mb-4">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="">Choose Time</option>
                            <option value="10am-1pm">Morning (10am - 1pm)</option>
                            <option value="1pm-4pm">Afternoon (1pm - 4pm)</option>
                            <option value="4pm-7pm">Evening (4pm - 7pm)</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Submit to Local Dispatch</button>
                    <p class="text-[8px] text-slate-400 mt-4 text-center font-bold uppercase tracking-widest">A local licensed contractor will reach out within 24 hours.</p>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-5xl mx-auto px-6 mb-32 grid grid-cols-1 md:grid-cols-2 gap-10">
        <div class="matrix-card"><img src="./WA_1776549716792.jpeg"><h4>Roofing Excellence</h4></div>
        <div class="matrix-card"><img src="./WA_1776549781247.jpeg"><h4>Solar Efficiency</h4></div>
        <div class="matrix-card"><img src="./WA_1776549555727.jpeg"><h4>Premium Windows</h4></div>
        <div class="matrix-card"><img src="./WA_1776549622236.jpeg"><h4>Custom Doors</h4></div>
        <div class="matrix-card"><img src="./WA_1776549862258.jpeg"><h4>Bathroom Luxury</h4></div>
        <div class="matrix-card"><img src="./WA_1776549917709.jpeg"><h4>Designer Kitchens</h4></div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-6"><h3 class="font-black">ADMIN LEADS TERMINAL</h3><button onclick="closeAdmin()" class="text-red-500 font-bold uppercase text-xs">Exit</button></div>
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

        // 5-TAP SECURITY
        let taps = 0, tapT;
        function handleTap() {
            taps++; clearTimeout(tapT);
            if(taps >= 5) { document.getElementById('adminPanel').classList.remove('hidden'); taps = 0; }
            tapT = setTimeout(() => taps = 0, 2000);
        }

        // FAKE NOTIFICATION ENGINE (20+ Notifications)
        const fakeNotifs = [
            "Sarah M. from California just booked a Roofing estimate!",
            "David L. from Texas requested Solar pricing.",
            "New Window installation booked in Florida!",
            "Mike from New York just verified his appointment.",
            "Authorized Siding crew dispatched to Chicago.",
            "Kitchen remodel inquiry received from Ohio.",
            "Bathroom site survey booked in Georgia!",
            "Jennifer from Arizona just saved 20% on Windows.",
            "Contractor dispatched for Roofing in Nevada.",
            "New inquiry for Solar in Colorado!",
            "Robert from Seattle requested a Doors quote.",
            "Garage door system booked in New Jersey.",
            "Local contractor reaching out to Lisa in Utah.",
            "Authorized survey scheduled for Deck in Oregon.",
            "Homeowner in Michigan just authorized a Roofing dispatch.",
            "Solar estimate requested in Pennsylvania.",
            "Window replacement booking confirmed in North Carolina.",
            "Siding estimate authorized for Kevin in Virginia.",
            "Kitchen survey dispatched in Massachusetts.",
            "New Bathroom remodel inquiry from Tennessee."
        ];

        setInterval(() => {
            const toast = document.getElementById('notification-toast');
            const txt = document.getElementById('notif-text');
            txt.innerText = "✨ " + fakeNotifs[Math.floor(Math.random() * fakeNotifs.length)];
            toast.style.display = 'block';
            setTimeout(() => toast.style.display = 'none', 5000);
        }, 12000);

        function goStep(id) {
            document.querySelectorAll('.step-form').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function updateOptions() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicFields');
            let h = '';
            const opts = {
                'Windows': [{ l: 'Window Count?', o: ['1-5','6-10','11-15','16-20','21-30','31+'] }, { l: 'Material?', o: ['Premium Vinyl','Natural Wood','Fiberglass'] }],
                'Roofing': [{ l: 'Roof Material?', o: ['Asphalt Shingles','Architectural Metal','Tile','Slate'] }],
                'Siding': [{ l: 'Siding Type?', o: ['Vinyl','Wood','Fiber Cement','Aluminum'] }],
                'Solar': [{ l: 'Monthly Bill?', o: ['$50-$100','$101-$200','$201-$300','$301+'] }]
            };
            const items = opts[s] || [{ l: 'Detail', o: ['Standard','Premium','Luxury'] }];
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
        updateOptions();

        function toggleM(idx) {
            const s = document.getElementById(`q${idx}`);
            const m = document.getElementById(`m${idx}`);
            if(s.value === 'Manual') m.classList.remove('hidden'); else m.classList.add('hidden');
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('mainService').value,
                owner: document.getElementById('isOwner').value,
                spec: document.getElementById('q0')?.value === 'Manual' ? document.getElementById('m0').value : document.getElementById('q0')?.value,
                name: document.getElementById('custName').value,
                phone: document.getElementById('custPhone').value,
                address: document.getElementById('custAddress').value,
                zip: document.getElementById('custZip').value,
                appointment: `${document.getElementById('appDate').value} (${document.getElementById('appSlot').value})`,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { 
                alert("Success! Your Local Dispatch Authorization ID is #" + Math.floor(Math.random()*9999) + ". A local contractor will call you shortly."); 
                location.reload(); 
            });
        });

        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-6 border rounded-2xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] absolute top-4 right-4 font-black">${data[k].service}</span>
                        <h4 class="text-xl font-black uppercase italic text-blue-900">${data[k].name}</h4>
                        <p>📍 ${data[k].address} (${data[k].zip})</p>
                        <div class="mt-4 border-t pt-4 grid grid-cols-2 gap-4">
                            <p>📞: ${data[k].phone}</p>
                            <p>👤 Owner: ${data[k].owner}</p>
                            <p class="col-span-2 text-emerald-600">📅 Appt: ${data[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black">DELETE LEAD</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Leads';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
