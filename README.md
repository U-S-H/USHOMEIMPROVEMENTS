<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Matrix Dispatch</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon-blue: #2563eb; --neon-cyan: #06b6d4; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #1e293b; }
        .glass-card { background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(10px); border-radius: 32px; border: 1px solid #e2e8f0; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.1); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #e2e8f0; border-radius: 14px; font-weight: 600; transition: 0.3s; margin-bottom: 12px; font-size: 14px; appearance: none; background: #fff; }
        .input-pro:focus { border-color: var(--neon-blue); outline: none; box-shadow: 0 0 10px rgba(37, 99, 235, 0.1); }
        .btn-action { background: linear-gradient(135deg, var(--neon-blue), var(--neon-cyan)); color: white; padding: 18px; border-radius: 14px; font-weight: 800; width: 100%; cursor: pointer; border: none; text-transform: uppercase; margin-top: 10px; }
        .step-form { display: none; }
        .step-form.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .matrix-card { background: white; border-radius: 20px; overflow: hidden; border: 1px solid #f1f5f9; text-align: center; }
        .matrix-card img { width: 100%; height: 130px; object-fit: cover; }
        .matrix-card h4 { font-size: 11px; font-weight: 800; padding: 12px; text-transform: uppercase; color: #1e3a8a; }
    </style>
</head>
<body>

    <nav class="bg-white border-b px-6 py-4 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-sm border">
            <div>
                <span onclick="toggleAdmin()" class="block font-black text-sm uppercase tracking-tighter cursor-pointer text-blue-800">U.S. Home Improvement</span>
                <span class="block text-[8px] font-bold text-emerald-600 uppercase italic">● Licensed Nationwide Hub</span>
            </div>
        </div>
        <div class="hidden md:block text-[10px] font-black text-slate-400 uppercase italic">Dispatch Center: Woodland, CA</div>
    </nav>

    <header class="py-12 px-6 text-center">
        <h1 class="text-3xl md:text-5xl font-black uppercase italic tracking-tighter text-slate-900">Get Your <span class="text-blue-600">Free Quotes</span></h1>
        <p class="text-slate-500 font-bold uppercase text-[9px] tracking-[0.4em] mt-2">Connecting You to Authorized Local Crews</p>
    </header>

    <main class="max-w-xl mx-auto px-6 mb-32">
        <div class="glass-card p-8 md:p-10">
            <form id="proMatrixForm">
                <div class="step-form active" id="step1">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-3">01. Project Selection</label>
                    <select id="mainService" class="input-pro" onchange="loadServiceOptions()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Siding">Exterior Siding</option>
                        <option value="Solar">Solar Energy Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                        <option value="Garage">Garage Door Systems</option>
                        <option value="Deck">Custom Decking</option>
                    </select>
                    <select id="isOwner" class="input-pro" required>
                        <option value="Yes">Yes, I am the Homeowner</option>
                        <option value="No">No, I am a Tenant</option>
                    </select>
                    <button type="button" onclick="goStep('step2')" class="btn-action">Continue</button>
                </div>

                <div class="step-form" id="step2">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-3">02. Specific Requirements</label>
                    <div id="dynamicQuestions"></div>
                    <button type="button" onclick="goStep('step3')" class="btn-action">Confirm Details</button>
                </div>

                <div class="step-form" id="step3">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-3">03. Local Dispatch Info</label>
                    <input type="text" id="custName" placeholder="Full Name" class="input-pro" required>
                    <input type="text" id="custAddress" placeholder="Street Address" class="input-pro" required>
                    <div class="grid grid-cols-2 gap-3">
                        <input type="text" id="custZip" placeholder="Zip" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Phone Number" class="input-pro" required>
                    </div>
                    <input type="email" id="custEmail" placeholder="Email Address" class="input-pro" required>
                    <div class="grid grid-cols-2 gap-3">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appTime" class="input-pro" required>
                            <option value="Morning">Morning Window</option>
                            <option value="Afternoon">Afternoon Window</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Request Dispatch</button>
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

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-6"><h3 class="font-black">ADMIN LEADS HQ</h3><button onclick="toggleAdmin()" class="text-red-500 font-bold">CLOSE</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="PIN"><button onclick="unlock()" class="btn-action max-w-[200px]">Access</button></div>
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

        function loadServiceOptions() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicQuestions');
            let h = '';

            const options = {
                'Windows': [
                    { label: 'How many windows?', options: ['1-5','6-10','11-15','16-20','21-30','31+'] },
                    { label: 'Window Material?', options: ['Vinyl','Wood','Aluminum','Fiberglass','Composite'] }
                ],
                'Roofing': [
                    { label: 'Material Interest?', options: ['Shingles','Metal','Tile','Slate','Flat Roof'] },
                    { label: 'Approx Square Footage?', options: ['<1500','1500-2500','2500-4000','4000+'] }
                ],
                'Siding': [
                    { label: 'Type of Siding?', options: ['Vinyl','Wood','Fiber Cement','Aluminum','Brick/Stone'] },
                    { label: 'Project Goal?', options: ['Full Replacement','Partial Repair','New Installation'] }
                ],
                'Solar': [
                    { label: 'Monthly Power Bill?', options: ['$50-$100','$101-$200','$201-$300','$301+'] },
                    { label: 'Roof Age?', options: ['New','1-5 Years','5-15 Years','15+ Years'] }
                ],
                'Kitchen': [
                    { label: 'Remodel Scope?', options: ['Full Renovation','Cabinets/Counters Only','Appliance Upgrade'] },
                    { label: 'Kitchen Size?', options: ['Small','Standard','Gourmet/Large'] }
                ],
                'Bathroom': [
                    { label: 'Scope of Work?', options: ['Tub to Shower','Full Remodel','Vanity Only','New Suite'] },
                    { label: 'Number of Baths?', options: ['1','2','3+'] }
                ],
                'Garage': [
                    { label: 'System Type?', options: ['Single Door','Double Door','Modern Glass','Insulated Steel'] }
                ],
                'Deck': [
                    { label: 'Material?', options: ['Pressure Treated Wood','Composite','Cedar','Vinyl/PVC'] }
                ]
            };

            const data = options[s] || [];
            data.forEach((item, i) => {
                h += `<p class="text-[10px] font-black uppercase text-slate-400 mb-1">${item.label}</p>
                      <select id="q${i}" class="input-pro" onchange="toggleM(${i})">
                        ${item.options.map(opt => `<option value="${opt}">${opt}</option>`).join('')}
                        <option value="Manual">Manual / Other...</option>
                      </select>
                      <input type="text" id="m${i}" placeholder="Type exact details here" class="input-pro hidden">`;
            });
            container.innerHTML = h;
        }
        loadServiceOptions();

        function toggleM(idx) {
            const s = document.getElementById(`q${idx}`);
            const m = document.getElementById(`m${idx}`);
            if(s.value === 'Manual') m.classList.remove('hidden'); else m.classList.add('hidden');
        }

        document.getElementById('proMatrixForm').addEventListener('submit', (e) => {
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
                appointment: `${document.getElementById('appDate').value} (${document.getElementById('appTime').value})`,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { 
                alert("Success! Your Local State Contractor will call you soon."); 
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
                        <h4 class="text-xl font-black uppercase italic">${data[k].name}</h4>
                        <p>📍 ${data[k].address} (${data[k].zip})</p>
                        <div class="mt-4 grid grid-cols-2 gap-4 border-t pt-4 text-blue-800 uppercase text-[9px]">
                            <p>📞: ${data[k].phone}</p>
                            <p>✉️: ${data[k].email}</p>
                            <p>👤 Owner: ${data[k].owner}</p>
                            <p>🛠 Specs: ${data[k].spec1 || 'N/A'} | ${data[k].spec2 || 'N/A'}</p>
                        </div>
                        <div class="mt-4 bg-white p-3 rounded-lg border flex justify-between items-center text-[10px]">
                            <span>📅 Appointment: ${data[k].appointment}</span>
                            <button onclick="del('${k}')" class="text-red-500 font-black">DELETE</button>
                        </div>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Leads';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
