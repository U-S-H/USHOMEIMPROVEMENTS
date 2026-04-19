<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Dispatch Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; --success: #059669; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; }
        
        .glass-card { background: white; border: 1px solid #e2e8f0; border-radius: 24px; box-shadow: 0 20px 25px -5px rgba(0,0,0,0.1); }
        .input-pro { width: 100%; padding: 14px; border: 2px solid #f1f5f9; border-radius: 12px; font-weight: 600; font-size: 14px; outline: none; background: #fff; appearance: none; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px; border-radius: 12px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; transition: 0.3s; }
        .btn-action:hover { transform: translateY(-2px); box-shadow: 0 10px 15px -3px rgba(37, 99, 235, 0.3); }

        .step-form { display: none; }
        .step-form.active { display: block; animation: slideUp 0.4s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .matrix-card { background: white; border-radius: 20px; overflow: hidden; border: 1px solid #f1f5f9; transition: 0.3s; text-align: center; }
        .matrix-card img { width: 100%; height: 130px; object-fit: cover; }
        .matrix-card h4 { font-size: 11px; font-weight: 800; color: var(--primary); text-transform: uppercase; padding: 12px 0; }
        
        .badge-live { display: inline-flex; align-items: center; gap: 6px; background: #ecfdf5; color: #059669; padding: 4px 12px; border-radius: 50px; font-size: 10px; font-weight: 800; }
    </style>
</head>
<body>

    <nav class="bg-white border-b px-6 py-4 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-sm border">
            <div>
                <span onclick="toggleAdmin()" class="block font-black text-sm uppercase tracking-tighter cursor-pointer text-blue-900">U.S. Home Improvement</span>
                <div class="badge-live uppercase italic">● Licensed National Dispatch</div>
            </div>
        </div>
        <div class="hidden md:block text-[10px] font-black text-slate-400 uppercase tracking-widest italic">Woodland, California HQ</div>
    </nav>

    <header class="py-12 px-6 text-center">
        <h1 class="text-3xl md:text-5xl font-black uppercase italic tracking-tighter mb-4">Authorized <span class="text-blue-600">Upgrade</span> Matrix</h1>
        <p class="text-slate-500 font-bold uppercase text-[9px] tracking-[0.4em]">Get Professional Site Estimates Nationwide</p>
    </header>

    <main class="max-w-xl mx-auto px-6 mb-32">
        <div class="glass-card p-8 md:p-10">
            <form id="proDispatchForm">
                <div class="step-form active" id="step1">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-3">01. Select Improvement</label>
                    <select id="mainService" class="input-pro mb-4" onchange="loadOptions()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Siding">Exterior Siding</option>
                        <option value="Solar">Solar Power System</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                        <option value="Garage">Garage Door Systems</option>
                        <option value="Deck">Custom Decking</option>
                    </select>
                    <select id="isOwner" class="input-pro" required>
                        <option value="Yes">Yes, I am the Homeowner</option>
                        <option value="No">No, I am a Tenant</option>
                    </select>
                    <button type="button" onclick="goStep('step2')" class="btn-action mt-6">Next Step</button>
                </div>

                <div class="step-form" id="step2">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-3">02. Specific Requirements</label>
                    <div id="dynamicContainer"></div>
                    <button type="button" onclick="goStep('step3')" class="btn-action">Finalize Appointment</button>
                </div>

                <div class="step-form" id="step3">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-3">03. Site Dispatch & Timing</label>
                    <input type="text" id="custName" placeholder="Full Name" class="input-pro mb-3" required>
                    <input type="text" id="custAddress" placeholder="Site Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-3">
                        <input type="text" id="custZip" placeholder="Zip" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Mobile Number" class="input-pro" required>
                    </div>
                    
                    <div class="grid grid-cols-2 gap-3 mb-3">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="">Select Time Slot</option>
                            <optgroup label="Morning">
                                <option value="10:00 AM">10:00 AM</option>
                                <option value="11:00 AM">11:00 AM</option>
                                <option value="12:00 PM">12:00 PM</option>
                            </optgroup>
                            <optgroup label="Afternoon">
                                <option value="01:00 PM">01:00 PM</option>
                                <option value="02:00 PM">02:00 PM</option>
                                <option value="03:00 PM">03:00 PM</option>
                                <option value="04:00 PM">04:00 PM</option>
                            </optgroup>
                            <optgroup label="Evening">
                                <option value="05:00 PM">05:00 PM</option>
                                <option value="06:00 PM">06:00 PM</option>
                                <option value="07:00 PM">07:00 PM</option>
                            </optgroup>
                        </select>
                    </div>
                    
                    <input type="email" id="custEmail" placeholder="Email Address" class="input-pro mb-4" required>
                    <button type="submit" class="btn-action">Authorize Dispatch</button>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-5xl mx-auto px-6 mb-32 grid grid-cols-2 md:grid-cols-4 gap-6">
        <div class="matrix-card"><img src="./WA_1776549716792.jpeg"><h4>Roofing</h4></div>
        <div class="matrix-card"><img src="./WA_1776549781247.jpeg"><h4>Solar</h4></div>
        <div class="matrix-card"><img src="./WA_1776549555727.jpeg"><h4>Windows</h4></div>
        <div class="matrix-card"><img src="./WA_1776549622236.jpeg"><h4>Doors</h4></div>
        <div class="matrix-card"><img src="./WA_1776549862258.jpeg"><h4>Kitchen</h4></div>
        <div class="matrix-card"><img src="./WA_1776549917709.jpeg"><h4>Bathroom</h4></div>
        <div class="matrix-card"><img src="./WA_1776550066723.jpeg"><h4>Garage</h4></div>
        <div class="matrix-card"><img src="./WA_1776549990293.jpeg"><h4>Deck</h4></div>
    </section>

    <footer class="bg-slate-900 py-16 px-8 text-white">
        <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-12 text-center md:text-left">
            <div>
                <h4 class="text-blue-400 font-black uppercase text-xs mb-4">Corporate HQ</h4>
                <p class="text-slate-400 text-sm font-bold">702 Main Street<br>Woodland, California 95695</p>
                <p class="text-blue-300 text-[10px] mt-2 lowercase">ushomeimprovement07@gmail.com</p>
            </div>
            <div>
                <h4 class="text-blue-400 font-black uppercase text-xs mb-4">Network Info</h4>
                <p class="text-slate-500 text-[10px] font-bold uppercase leading-relaxed">
                    Nationwide Authorized Hub. Upon appointment authorization, a local state-licensed contractor will be dispatched for a site technical survey.
                </p>
            </div>
            <div>
                <h4 class="text-blue-400 font-black uppercase text-xs mb-4">Legal Portal</h4>
                <div class="flex flex-col gap-2 text-[9px] font-black uppercase text-slate-500">
                    <span>Privacy & Data Shield</span>
                    <span>Terms & Conditions</span>
                    <span class="mt-4">© 2026 National Hub</span>
                </div>
            </div>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-6"><h3 class="font-black">ADMIN DISPATCH HQ</h3><button onclick="toggleAdmin()" class="text-red-500 font-bold">EXIT</button></div>
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

        function goStep(id) {
            document.querySelectorAll('.step-form').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function loadOptions() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicContainer');
            let h = '';

            const dataMap = {
                'Windows': [
                    { label: 'Window Count?', opt: ['1-4','5-9','10-15','16-25','26+'] },
                    { label: 'Material?', opt: ['Vinyl','Wood','Aluminum','Fiberglass'] }
                ],
                'Roofing': [
                    { label: 'Roof Material?', opt: ['Shingles','Metal','Tile','Slate'] },
                    { label: 'Approx Sq Footage?', opt: ['<1500','1500-2500','2500-4000','4000+'] }
                ],
                'Siding': [
                    { label: 'Siding Type?', opt: ['Vinyl','Wood','Fiber Cement','Metal'] }
                ],
                'Solar': [
                    { label: 'Electric Bill?', opt: ['$50-100','$100-200','$200-300','$300+'] }
                ],
                'Kitchen': [{ label: 'Style?', opt: ['Modern','Classic','Rustic'] }],
                'Bathroom': [{ label: 'Scope?', opt: ['Full Remodel','Tub to Shower'] }],
                'Garage': [{ label: 'Door Type?', opt: ['Single','Double','Insulated'] }],
                'Deck': [{ label: 'Material?', opt: ['Composite','Cedar','Vinyl'] }]
            };

            const items = dataMap[s] || [];
            items.forEach((item, i) => {
                h += `<p class="text-[10px] font-black text-slate-400 uppercase mb-2">${item.label}</p>
                      <select id="q${i}" class="input-pro mb-3" onchange="toggleM(${i})">
                        ${item.opt.map(o => `<option value="${o}">${o}</option>`).join('')}
                        <option value="Manual">Manual Entry / Other...</option>
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
                spec2: document.getElementById('q1')?.value === 'Manual' ? document.getElementById('m1').value : document.getElementById('q1')?.value,
                name: document.getElementById('custName').value,
                address: document.getElementById('custAddress').value,
                zip: document.getElementById('custZip').value,
                phone: document.getElementById('custPhone').value,
                email: document.getElementById('custEmail').value,
                appointment: `${document.getElementById('appDate').value} @ ${document.getElementById('appSlot').value}`,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { 
                alert("Authorization Successful! Local dispatch crew will call you."); 
                location.reload(); 
            });
        });

        function toggleAdmin() { document.getElementById('adminPanel').classList.toggle('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-6 border rounded-2xl bg-slate-50 relative mb-4 text-[11px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] font-black absolute top-4 right-4 uppercase italic">${data[k].service}</span>
                        <h4 class="text-lg font-black uppercase italic">${data[k].name}</h4>
                        <p>📍 ${data[k].address} (${data[k].zip})</p>
                        <div class="mt-4 grid grid-cols-2 gap-4 border-t pt-4 text-blue-900 uppercase text-[9px]">
                            <p>📞: ${data[k].phone}</p>
                            <p>👤 Owner: ${data[k].owner}</p>
                            <p class="col-span-2">🛠 Specs: ${data[k].spec1 || 'N/A'} | ${data[k].spec2 || 'N/A'}</p>
                        </div>
                        <div class="mt-4 bg-white p-3 rounded-lg border flex justify-between items-center text-[10px]">
                            <span class="text-emerald-700">📅 Dispatch Slot: ${data[k].appointment}</span>
                            <button onclick="del('${k}')" class="text-red-500 font-black">DELETE</button>
                        </div>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Active Dispatches';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
