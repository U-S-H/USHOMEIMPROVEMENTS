<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | National Dispatch Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fafbfc; color: #0f172a; scroll-behavior: smooth; }
        
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 32px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.06); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; font-size: 14px; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px; border-radius: 16px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.5s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .form-step { display: none; }
        .form-step.active { display: block; animation: slideUp 0.4s ease; }
        @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        #notification-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 12px 20px; border-radius: 50px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); border-left: 5px solid #059669; display: none; z-index: 9999; }
        .matrix-card { background: white; border-radius: 24px; overflow: hidden; border: 1px solid #f1f5f9; cursor: pointer; transition: 0.3s; }
        .matrix-card:hover { transform: translateY(-8px); box-shadow: 0 15px 30px rgba(0,0,0,0.08); }
    </style>
</head>
<body>

    <div id="notification-toast"><p id="notif-text" class="text-[10px] font-bold text-slate-700 uppercase tracking-tighter"></p></div>

    <nav class="bg-white/90 backdrop-blur-md border-b px-6 py-4 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3 cursor-pointer" onclick="showPage('homePage')">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border" id="adminTrigger" onclick="handleTap()">
            <div>
                <span class="block font-black text-sm uppercase text-blue-900 tracking-tighter">U.S. Home Improvement LLC</span>
                <span class="block text-[8px] font-extrabold text-emerald-600 uppercase italic">● Authorized National Dispatch Terminal</span>
            </div>
        </div>
        <div class="hidden md:flex gap-8 text-[10px] font-black text-slate-400 uppercase tracking-widest">
            <a href="#" onclick="showPage('homePage')" class="hover:text-blue-600">Home</a>
            <a href="#" onclick="showPage('servicesPage')" class="hover:text-blue-600">Services</a>
            <a href="#" onclick="showPage('formPage')" class="text-blue-600 px-4 py-2 bg-blue-50 rounded-lg">Get Free Quote</a>
        </div>
    </nav>

    <section id="homePage" class="page-section active">
        <header class="py-24 px-6 text-center bg-gradient-to-b from-slate-50 to-white">
            <div class="inline-block bg-blue-100 text-blue-700 px-4 py-1 rounded-full text-[9px] font-black uppercase mb-6 tracking-widest">Licensed & Insured Across 50 States</div>
            <h1 class="text-5xl md:text-7xl font-black uppercase italic tracking-tighter mb-6 text-slate-900 leading-none">Your Dream Home,<br><span class="text-blue-600">Nationwide Care.</span></h1>
            <p class="text-slate-500 font-bold uppercase text-[10px] tracking-[0.4em] mb-12 max-w-2xl mx-auto leading-relaxed">The authorized hub for professional home inspections and remodeling estimates.</p>
            <button onclick="showPage('formPage')" class="btn-action max-w-sm shadow-xl shadow-blue-200">Start Free Inspection</button>
            <div class="mt-12 flex justify-center gap-3">
                <span class="text-yellow-400 text-xl">★★★★★</span>
                <span class="text-[11px] font-black self-center text-slate-700 uppercase">4.9/5 RATING | 12.4K+ VERIFIED REVIEWS</span>
            </div>
        </header>

        <div class="max-w-6xl mx-auto px-6 py-20 grid md:grid-cols-2 lg:grid-cols-3 gap-8">
            <div class="matrix-card" onclick="startWith('Windows')"><img src="./WA_1776549555727.jpeg" class="h-56 w-full object-cover"><div class="p-6"><h4 class="font-black text-blue-900 text-xs mb-2">ENERGY WINDOWS</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Save up to 30% on energy bills with our thermal-sealed windows.</p></div></div>
            <div class="matrix-card" onclick="startWith('Roofing')"><img src="./WA_1776549716792.jpeg" class="h-56 w-full object-cover"><div class="p-6"><h4 class="font-black text-blue-900 text-xs mb-2">LIFETIME ROOFING</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Architectural shingles and metal roofing with lifetime warranties.</p></div></div>
            <div class="matrix-card" onclick="startWith('Solar')"><img src="./WA_1776549781247.jpeg" class="h-56 w-full object-cover"><div class="p-6"><h4 class="font-black text-blue-900 text-xs mb-2">SMART SOLAR</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Zero-down solar installation with federal tax credit eligibility.</p></div></div>
        </div>
    </section>

    <section id="servicesPage" class="page-section bg-white py-24">
        <div class="max-w-6xl mx-auto px-6">
            <h2 class="text-4xl font-black italic text-center uppercase mb-16 tracking-tighter">Premium <span class="text-blue-600">Home Solutions</span></h2>
            <div class="grid md:grid-cols-2 gap-10">
                <div class="p-10 border-2 border-slate-50 rounded-3xl bg-slate-50/50">
                    <h3 class="text-xl font-black mb-6 uppercase italic text-blue-900">Interior Luxury</h3>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-loose">Kitchen remodeling with custom cabinetry, quartz countertops, and smart islands. Bathroom spas with tub-to-shower conversion and lifetime waterproofing.</p>
                </div>
                <div class="p-10 border-2 border-slate-50 rounded-3xl bg-slate-50/50">
                    <h3 class="text-xl font-black mb-6 uppercase italic text-blue-900">Exterior Shield</h3>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-loose">Fiber-cement siding, premium insulated garage doors, and custom composite decking designed for the harsh American climate.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="formPage" class="page-section py-20 px-6 min-h-screen">
        <div class="max-w-xl mx-auto glass-card p-8 md:p-12 relative overflow-hidden" id="formFrame">
            <form id="proDispatchForm">
                <div class="form-step active" id="s1">
                    <h3 class="text-2xl font-black italic uppercase text-blue-900 mb-8 leading-none">Project <span class="text-blue-600">Type</span></h3>
                    <select id="mainService" class="input-pro mb-4" onchange="updateQualifiers()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                    </select>
                    <select id="isOwner" class="input-pro mb-8" required>
                        <option value="Yes">Yes, I am the Homeowner</option>
                        <option value="No">No, I am a Tenant</option>
                    </select>
                    <button type="button" onclick="moveStep('s2')" class="btn-action shadow-lg">Next: Requirements</button>
                </div>

                <div class="form-step" id="s2">
                    <h3 class="text-2xl font-black italic uppercase text-blue-900 mb-8 leading-none">Project <span class="text-blue-600">Details</span></h3>
                    <div id="qualifierFields"></div>
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-2 mt-6">Estimated Credit Score</label>
                    <select id="creditScore" class="input-pro mb-8" required>
                        <option value="Excellent (720+)">Excellent (720+)</option>
                        <option value="Good (660-719)">Good (660-719)</option>
                        <option value="Fair (600-659)">Fair (600-659)</option>
                        <option value="Poor (Below 600)">Poor (Below 600)</option>
                    </select>
                    <button type="button" onclick="moveStep('s3')" class="btn-action shadow-lg">Next: Site Info</button>
                </div>

                <div class="form-step" id="s3">
                    <h3 class="text-2xl font-black italic uppercase text-blue-900 mb-8 leading-none">Site <span class="text-blue-600">Authorization</span></h3>
                    <input type="text" id="custName" placeholder="Full Legal Name" class="input-pro mb-3" required>
                    <input type="email" id="custEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="text" id="custAddr" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-4">
                        <input type="text" id="custZip" placeholder="Zip" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Mobile Phone #" class="input-pro" required>
                    </div>
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-2">Preferred Inspection Schedule</label>
                    <div class="grid grid-cols-2 gap-3 mb-8">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="10am-1pm">Morning (10-1)</option>
                            <option value="1pm-4pm">Afternoon (1-4)</option>
                            <option value="4pm-7pm">Evening (4-7)</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action shadow-xl">Confirm Dispatch</button>
                </div>
            </form>

            <div id="receiptBox" class="hidden text-center py-6">
                <div class="bg-emerald-100 text-emerald-600 h-20 w-20 rounded-full flex items-center justify-center text-3xl mx-auto mb-6">✔</div>
                <h2 class="text-3xl font-black text-blue-900 uppercase italic">Appointment Set</h2>
                <p class="text-[10px] font-bold text-slate-400 uppercase mt-2 italic">Please save this for your site inspector.</p>
                <div class="mt-8 p-8 bg-slate-50 border-2 border-dashed border-slate-200 rounded-3xl text-left">
                    <div class="space-y-4">
                        <div><p class="text-[9px] font-black text-slate-400 uppercase">Service</p><p id="r-service" class="font-black text-blue-900"></p></div>
                        <div><p class="text-[9px] font-black text-slate-400 uppercase">Customer</p><p id="r-name" class="font-black text-slate-700"></p></div>
                        <div><p class="text-[9px] font-black text-slate-400 uppercase">Confirmed Slot</p><p id="r-date" class="font-black text-emerald-600"></p></div>
                        <div><p class="text-[9px] font-black text-slate-400 uppercase">Site Location</p><p id="r-addr" class="font-black text-slate-700"></p></div>
                    </div>
                </div>
                <button onclick="location.reload()" class="mt-10 text-blue-600 font-black text-xs uppercase underline">Back to Home</button>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-8"><h3 class="font-black italic text-blue-900">ADMIN TERMINAL (786)</h3><button onclick="closeAdmin()" class="text-red-500 font-black uppercase text-xs">Exit</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="PIN"><button onclick="unlock()" class="btn-action max-w-[200px]">Access</button></div>
        <div id="leadsList" class="hidden space-y-6 pb-20"></div>
    </div>

    <footer class="bg-white border-t py-20 px-6 text-center">
        <h4 class="font-black text-blue-900 uppercase text-xs mb-6 italic tracking-widest">U.S. Home Improvement LLC</h4>
        <p class="text-[9px] text-slate-400 uppercase max-w-lg mx-auto leading-loose font-bold">
            Headquarters: 702 Main Street, Woodland, CA 95695. <br>
            Authorized National Dispatch Hub. Privacy Policy & Terms of Service Active. All inspectors are state-licensed and insured.
        </p>
    </footer>

    <script>
        // CONFIG
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
        function handleTap() { taps++; clearTimeout(tapT); if(taps>=5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } tapT=setTimeout(()=>taps=0,2000); }

        // NAVIGATION
        function showPage(id) {
            document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo(0,0);
        }
        function startWith(svc) {
            document.getElementById('mainService').value = svc;
            updateQualifiers();
            showPage('formPage');
        }
        function moveStep(id) {
            document.querySelectorAll('.form-step').forEach(s=>s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        // DYNAMIC FIELDS
        function updateQualifiers() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('qualifierFields');
            const data = {
                'Windows': [{l:'Window Count', o:['1-5','6-10','11-20','21+']},{l:'Preferred Material', o:['Vinyl','Wood','Fiberglass']}],
                'Roofing': [{l:'Roof Age', o:['1-10 years','11-20 years','20+ years']},{l:'Active Leaks?', o:['No','Yes, Minor','Yes, Emergency']}],
                'Solar': [{l:'Avg Power Bill', o:['$50-150','$151-300','$301+']},{l:'Roof Type', o:['Shingle','Metal','Flat']}]
            };
            const current = data[s] || [{l:'Project Timeline', o:['Immediate','1-3 Months','Just Estimating']}];
            container.innerHTML = current.map((q, i) => `
                <label class="text-[10px] font-black text-slate-400 uppercase block mb-2 mt-4">${q.l}</label>
                <select id="q${i}" class="input-pro mb-2">${q.o.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>
            `).join('');
        }
        updateQualifiers();

        // SUBMISSION
        document.getElementById('proDispatchForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const service = document.getElementById('mainService').value;
            const name = document.getElementById('custName').value;
            const addr = document.getElementById('custAddr').value;
            const appt = `${document.getElementById('appDate').value} @ ${document.getElementById('appSlot').value}`;

            const data = {
                service: service,
                owner: document.getElementById('isOwner').value,
                credit: document.getElementById('creditScore').value,
                name: name,
                email: document.getElementById('custEmail').value,
                phone: document.getElementById('custPhone').value,
                address: addr,
                zip: document.getElementById('custZip').value,
                spec: document.getElementById('q0')?.value || 'Standard',
                appointment: appt,
                timestamp: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                document.getElementById('proDispatchForm').classList.add('hidden');
                document.getElementById('receiptBox').classList.remove('hidden');
                document.getElementById('r-service').innerText = service.toUpperCase();
                document.getElementById('r-name').innerText = name;
                document.getElementById('r-date').innerText = appt;
                document.getElementById('r-addr').innerText = addr;
            });
        });

        // ADMIN HUB
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value==="786"){ document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); syncLeads(); } }
        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="p-8 border-2 border-slate-100 rounded-3xl bg-white relative mb-4 text-[11px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded-full text-[8px] absolute top-4 right-4 uppercase font-black">${leads[k].service}</span>
                        <h4 class="text-xl font-black italic text-blue-900 mb-4">${leads[k].name}</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-slate-600">
                            <p>📧 Email: <span class="text-blue-600">${leads[k].email}</span></p>
                            <p>📞 Phone: ${leads[k].phone}</p>
                            <p>📍 Site: ${leads[k].address} (${leads[k].zip})</p>
                            <p>👤 Owner: ${leads[k].owner} | 💳 Credit: ${leads[k].credit}</p>
                            <p>🛠 Spec: ${leads[k].spec}</p>
                            <p class="text-emerald-600 col-span-full border-t pt-4 font-black">📅 APPOINTMENT: ${leads[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-6 text-red-500 font-black border-t w-full pt-4 text-center text-[10px]">DELETE DISPATCH PERMANENTLY</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'Terminal Empty';
            });
        }
        function del(id) { if(confirm('Remove Lead?')) db.ref('leads/'+id).remove(); }

        // FAKE SOCIAL PROOF
        const notifs = ["Sarah from California authorized Roofing!", "David from TX requested Windows.", "New Solar survey booked in Florida!", "Bathroom dispatch sent to Georgia.", "Kitchen estimate requested in NY."];
        setInterval(() => {
            const toast = document.getElementById('notification-toast');
            document.getElementById('notif-text').innerText = "✨ " + notifs[Math.floor(Math.random()*notifs.length)];
            toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 5000);
        }, 15000);
    </script>
</body>
</html>
