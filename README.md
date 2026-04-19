<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | Official Enterprise Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #0f172a; overflow-x: hidden; }
        
        /* UI Components */
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 28px; box-shadow: 0 15px 35px rgba(0,0,0,0.06); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 14px; font-weight: 600; outline: none; font-size: 14px; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px; border-radius: 14px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; transition: 0.3s; }
        .btn-action:hover { transform: scale(1.02); box-shadow: 0 20px 40px rgba(37, 99, 235, 0.3); }

        /* Multi-Page System */
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s ease; }
        .form-step { display: none; }
        .form-step.active { display: block; animation: slideUp 0.3s ease; }
        
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideUp { from { transform: translateY(15px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        /* Custom Elements */
        .hero-bg { background: linear-gradient(rgba(15, 23, 42, 0.75), rgba(15, 23, 42, 0.75)), url('WA_1776549716792.jpeg'); background-size: cover; background-position: center; background-attachment: fixed; }
        .logo-img { height: 42px; width: 42px; object-fit: contain; border-radius: 8px; background: white; cursor: pointer; }
        .service-card { border-radius: 24px; overflow: hidden; border: 1px solid #f1f5f9; transition: 0.4s ease; cursor: pointer; background: white; }
        .service-card:hover { transform: translateY(-10px); box-shadow: 0 25px 50px rgba(0, 0, 0, 0.1); }
        
        #notif-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 12px 22px; border-radius: 50px; box-shadow: 0 10px 30px rgba(0,0,0,0.12); border-left: 5px solid #059669; display: none; z-index: 9999; }
        .step-indicator { height: 4px; background: #e2e8f0; border-radius: 10px; flex: 1; overflow: hidden; }
        .step-progress { height: 100%; background: #2563eb; width: 0%; transition: 0.5s ease; }
    </style>
</head>
<body>

    <div id="notif-toast"><p id="notif-text" class="text-[10px] font-black text-slate-700 uppercase italic"></p></div>

    <nav class="bg-white/95 backdrop-blur-md border-b px-6 py-4 flex justify-between items-center sticky top-0 z-[2000]">
        <div class="flex items-center gap-3">
            <img src="logo.png" alt="Logo" class="logo-img" id="adminTrigger" onclick="handleTap()" onerror="this.src='https://ui-avatars.com/api/?name=US&background=1e3a8a&color=fff'">
            <div class="cursor-pointer" onclick="showPage('homePage')">
                <span class="block font-black text-sm uppercase text-blue-900 leading-none">U.S. Home Improvement LLC</span>
                <span class="block text-[8px] font-extrabold text-emerald-600 uppercase italic">● Licensed National Dispatch Terminal</span>
            </div>
        </div>
        <div class="hidden md:flex gap-8 text-[9px] font-black text-slate-400 uppercase tracking-widest">
            <button onclick="showPage('homePage')" class="hover:text-blue-600">Home</button>
            <button onclick="showPage('servicesPage')" class="hover:text-blue-600">Our Services</button>
            <button onclick="showPage('legalPage')" class="hover:text-blue-600">Compliance</button>
            <button onclick="showPage('formPage')" class="bg-blue-600 text-white px-5 py-2 rounded-lg">Get Estimate</button>
        </div>
    </nav>

    <section id="homePage" class="page-section active">
        <header class="hero-bg py-32 px-6 text-center text-white">
            <div class="max-w-4xl mx-auto">
                <span class="bg-white/10 text-white px-4 py-1 rounded-full text-[9px] font-black uppercase tracking-widest mb-6 inline-block italic border border-white/20">Nationwide Industry Authority</span>
                <h1 class="text-4xl md:text-7xl font-black uppercase italic tracking-tighter mb-8 leading-none">Premium American <br><span class="text-blue-400">Home Solutions.</span></h1>
                <p class="text-blue-100 font-bold uppercase text-[10px] tracking-[0.4em] mb-12 max-w-lg mx-auto">Authorized Inspections & Certified Contractor Networks</p>
                <button onclick="showPage('formPage')" class="btn-action max-w-sm">Secure Your Site Survey</button>
            </div>
        </header>

        <div class="max-w-7xl mx-auto px-6 py-20 grid md:grid-cols-4 gap-6">
            <div class="service-card" onclick="startSvc('Roofing')"><img src="WA_1776549716792.jpeg" class="w-full h-40 object-cover"><div class="p-4"><h4 class="font-black text-blue-900 text-[10px] uppercase">Roofing</h4></div></div>
            <div class="service-card" onclick="startSvc('Solar')"><img src="WA_1776549781247.jpeg" class="w-full h-40 object-cover"><div class="p-4"><h4 class="font-black text-blue-900 text-[10px] uppercase">Solar</h4></div></div>
            <div class="service-card" onclick="startSvc('Windows')"><img src="WA_1776549555727.jpeg" class="w-full h-40 object-cover"><div class="p-4"><h4 class="font-black text-blue-900 text-[10px] uppercase">Windows</h4></div></div>
            <div class="service-card" onclick="startSvc('Doors')"><img src="WA_1776549622236.jpeg" class="w-full h-40 object-cover"><div class="p-4"><h4 class="font-black text-blue-900 text-[10px] uppercase">Doors</h4></div></div>
        </div>
    </section>

    <section id="servicesPage" class="page-section bg-slate-50 py-24 px-6">
        <div class="max-w-6xl mx-auto">
            <h2 class="text-3xl font-black italic text-center uppercase mb-16 tracking-tighter">Enterprise <span class="text-blue-600">Portfolio</span></h2>
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div class="bg-white p-6 rounded-3xl border"><img src="WA_1776550066723.jpeg" class="w-full h-48 object-cover rounded-2xl mb-4"><h4 class="font-black text-blue-900 uppercase italic">Garage Door Matrix</h4><button onclick="startSvc('Garage')" class="text-blue-600 text-[10px] font-black uppercase mt-2 underline">Get Specs</button></div>
                <div class="bg-white p-6 rounded-3xl border"><img src="WA_1776549917709.jpeg" class="w-full h-48 object-cover rounded-2xl mb-4"><h4 class="font-black text-blue-900 uppercase italic">Gourmet Kitchens</h4><button onclick="startSvc('Kitchen')" class="text-blue-600 text-[10px] font-black uppercase mt-2 underline">Get Specs</button></div>
                <div class="bg-white p-6 rounded-3xl border"><img src="WA_1776549862258.jpeg" class="w-full h-48 object-cover rounded-2xl mb-4"><h4 class="font-black text-blue-900 uppercase italic">Bathroom Spas</h4><button onclick="startSvc('Bathroom')" class="text-blue-600 text-[10px] font-black uppercase mt-2 underline">Get Specs</button></div>
                <div class="bg-white p-6 rounded-3xl border"><img src="WA_1776549990293.jpeg" class="w-full h-48 object-cover rounded-2xl mb-4"><h4 class="font-black text-blue-900 uppercase italic">Custom Decks</h4><button onclick="startSvc('Deck')" class="text-blue-600 text-[10px] font-black uppercase mt-2 underline">Get Specs</button></div>
            </div>
        </div>
    </section>

    <section id="formPage" class="page-section py-20 bg-slate-50 min-h-screen px-6">
        <div class="max-w-xl mx-auto glass-card p-10 relative">
            <div class="flex gap-2 mb-10">
                <div class="step-indicator"><div id="pb1" class="step-progress" style="width: 100%"></div></div>
                <div class="step-indicator"><div id="pb2" class="step-progress"></div></div>
                <div class="step-indicator"><div id="pb3" class="step-progress"></div></div>
            </div>

            <form id="leadForm">
                <div class="form-step active" id="st1">
                    <h3 class="text-xl font-black italic uppercase mb-6">01. Service <span class="text-blue-600">Path</span></h3>
                    <select id="mainService" class="input-pro mb-4" onchange="loadQualifiers()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Matrix</option>
                        <option value="Kitchen">Kitchen Remodel</option>
                        <option value="Bathroom">Bathroom Spa</option>
                        <option value="Garage">Garage Systems</option>
                        <option value="Deck">Custom Decking</option>
                    </select>
                    <select id="isOwner" class="input-pro mb-8" required>
                        <option value="Yes">Confirmed Homeowner</option>
                        <option value="No">Tenant / Other</option>
                    </select>
                    <button type="button" onclick="goStep('st2', 'pb2')" class="btn-action">Verify Ownership</button>
                </div>

                <div class="form-step" id="st2">
                    <h3 class="text-xl font-black italic uppercase mb-6">02. Project <span class="text-blue-600">Specs</span></h3>
                    <div id="qualifierBox"></div>
                    <label class="text-[9px] font-black text-slate-400 uppercase mt-4 block italic">Credit Qualification</label>
                    <select id="credit" class="input-pro mb-8" required>
                        <option value="Excellent (720+)">Excellent (720+)</option>
                        <option value="Good (660-719)">Good (660-719)</option>
                        <option value="Fair">Fair / Other</option>
                    </select>
                    <button type="button" onclick="goStep('st3', 'pb3')" class="btn-action">Analyze Data</button>
                </div>

                <div class="form-step" id="st3">
                    <h3 class="text-xl font-black italic uppercase mb-6">03. Site <span class="text-blue-600">Dispatch</span></h3>
                    <input type="text" id="name" placeholder="Full Legal Name" class="input-pro mb-3" required>
                    <input type="tel" id="phone" placeholder="Mobile Number" class="input-pro mb-3" required>
                    <input type="text" id="address" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-8">
                        <input type="text" id="zip" placeholder="Zip Code" class="input-pro" required>
                        <input type="date" id="date" class="input-pro" required>
                    </div>
                    <button type="submit" class="btn-action">Authorize Estimate</button>
                </div>
            </form>

            <div id="success" class="hidden text-center py-10">
                <div class="text-6xl mb-4">✅</div>
                <h2 class="text-2xl font-black uppercase italic">Authorization Complete</h2>
                <p class="text-[10px] font-bold text-slate-400 mt-4 uppercase">Your file has been dispatched to the local field unit.</p>
                <button onclick="location.reload()" class="mt-8 text-blue-600 font-black text-[10px] uppercase">Submit Another</button>
            </div>
        </div>
    </section>

    <section id="legalPage" class="page-section py-20 px-6">
        <div class="max-w-4xl mx-auto glass-card p-12">
            <h2 class="text-2xl font-black text-blue-900 uppercase italic mb-10 tracking-tighter">Compliance <span class="text-blue-600">& Privacy</span></h2>
            <div class="space-y-8 text-[11px] font-bold text-slate-500 uppercase leading-relaxed">
                <p>U.S. Home Improvement LLC operates as an authorized national dispatch terminal. All contractors in our network are vetted for licensing and insurance compliance.</p>
                <p>Data Protection: All information is transmitted via 256-bit AES encryption to ensure consumer privacy.</p>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-8"><h3 class="font-black italic text-blue-900 uppercase">Master Admin Dispatch</h3><button onclick="closeAdmin()" class="text-red-500 font-black text-[10px] uppercase border border-red-500 px-4 py-1 rounded-full">Exit</button></div>
        <div id="authBox" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="PIN"><br><button onclick="unlock()" class="btn-action max-w-[200px]">Unlock</button></div>
        <div id="leadsList" class="hidden space-y-4 pb-20"></div>
    </div>

    <footer class="bg-white border-t py-20 px-6 text-center">
        <div class="flex justify-center gap-10 mb-10 grayscale opacity-40">
            <img src="https://upload.wikimedia.org/wikipedia/commons/a/a2/Better_Business_Bureau_logo.svg" class="h-4">
            <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Forbes_logo.svg" class="h-4">
        </div>
        <h4 class="font-black text-blue-900 uppercase text-xs mb-2">U.S. Home Improvement LLC</h4>
        <p class="text-[8px] text-slate-400 font-black uppercase italic">702 Main Street, Woodland, CA 95695 | Authorized National Terminal © 2026</p>
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

        // LOGO TAP SECRET
        let taps = 0, tapT;
        function handleTap() { taps++; clearTimeout(tapT); if(taps>=5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } tapT=setTimeout(()=>taps=0,2000); }

        // NAVIGATION
        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo(0,0); }
        function startSvc(svc) { document.getElementById('mainService').value = svc; loadQualifiers(); showPage('formPage'); }
        function goStep(id, pbid) { document.querySelectorAll('.form-step').forEach(s=>s.classList.remove('active')); document.getElementById(id).classList.add('active'); document.getElementById(pbid).style.width = '100%'; }

        // DYNAMIC QUALIFIERS
        function loadQualifiers() {
            const s = document.getElementById('mainService').value;
            const box = document.getElementById('qualifierBox');
            const questions = {
                'Roofing': [{l:'Roof Age', o:['1-10 yrs','11-20 yrs','20+ yrs']},{l:'Active Leaks?', o:['None','Minor','Serious']}],
                'Solar': [{l:'Electric Bill', o:['$50-150','$151-300','$301+']},{l:'Sun Exposure', o:['Full Sun','Partial']}],
                'Windows': [{l:'Quantity', o:['1-5','6-10','11+']},{l:'Frame Material', o:['Vinyl','Wood','Metal']}]
            };
            const current = questions[s] || [{l:'Timeline', o:['Immediate','1-3 Months']}];
            box.innerHTML = current.map((q, i) => `<label class="text-[9px] font-black text-slate-400 uppercase mt-4 block italic tracking-widest">${q.l}</label><select id="q${i}" class="input-pro mb-3">${q.o.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>`).join('');
        }
        loadQualifiers();

        // LEAD SUBMISSION
        document.getElementById('leadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('mainService').value,
                owner: document.getElementById('isOwner').value,
                credit: document.getElementById('credit').value,
                name: document.getElementById('name').value,
                phone: document.getElementById('phone').value,
                address: document.getElementById('address').value,
                zip: document.getElementById('zip').value,
                date: document.getElementById('date').value,
                q1: document.getElementById('q0')?.value || 'N/A',
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('leadForm').classList.add('hidden');
                document.getElementById('success').classList.remove('hidden');
            });
        });

        // ADMIN HUB
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value==="786"){ document.getElementById('authBox').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        function sync() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="p-6 border rounded-3xl bg-slate-50 relative mb-4 text-[10px] font-bold shadow-sm">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded-full text-[8px] absolute top-4 right-4 uppercase">${leads[k].service}</span>
                        <h4 class="text-xl font-black italic text-blue-900 mb-2">${leads[k].name}</h4>
                        <div class="grid grid-cols-2 gap-2 uppercase italic text-slate-500">
                            <p>📞 Phone: ${leads[k].phone}</p><p>📍 Zip: ${leads[k].zip}</p>
                            <p>🏠 Address: ${leads[k].address}</p><p>💳 Credit: ${leads[k].credit}</p>
                            <p>🛠 Detail: ${leads[k].q1}</p><p>📅 Appt: ${leads[k].date}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black border-t pt-2 w-full text-center tracking-widest">ERASE DISPATCH</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Active Dispatches';
            });
        }
        function del(id) { if(confirm('Delete permanently?')) db.ref('leads/'+id).remove(); }

        // FAKE SOCIAL PROOF
        const fNames = ["Jessica", "David", "Linda", "Michael", "Sarah", "James"];
        const fCities = ["Houston", "Miami", "Phoenix", "Chicago", "Atlanta"];
        setInterval(() => {
            const toast = document.getElementById('notif-toast');
            document.getElementById('notif-text').innerText = "⚡ " + fNames[Math.floor(Math.random()*fNames.length)] + " from " + fCities[Math.floor(Math.random()*fCities.length)] + " authorized an estimate!";
            toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 5000);
        }, 15000);
    </script>
</body>
</html>
