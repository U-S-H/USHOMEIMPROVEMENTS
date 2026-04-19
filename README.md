<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | Official National Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #0f172a; scroll-behavior: smooth; }
        
        .glass-card { background: white; border: 1px solid #e2e8f0; border-radius: 24px; box-shadow: 0 20px 25px -5px rgba(0,0,0,0.05); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 12px; font-weight: 600; outline: none; transition: 0.3s; font-size: 14px; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px; border-radius: 12px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; transition: 0.3s; }
        .btn-action:hover { transform: translateY(-2px); box-shadow: 0 10px 15px rgba(30, 58, 138, 0.2); }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s ease; }
        .form-step { display: none; }
        .form-step.active { display: block; animation: slideUp 0.3s ease; }
        
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideUp { from { transform: translateY(10px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        #notif-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 12px 20px; border-radius: 50px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); border-left: 5px solid #059669; display: none; z-index: 9999; }
    </style>
</head>
<body>

    <div id="notif-toast"><p id="notif-text" class="text-[10px] font-black text-slate-700 uppercase italic"></p></div>

    <nav class="bg-white/90 backdrop-blur-md border-b px-6 py-4 flex justify-between items-center sticky top-0 z-[2000]">
        <div class="flex items-center gap-3 cursor-pointer" onclick="showPage('homePage')">
            <img src="Screenshot_2026-04-19-06-03-04-64.png" class="h-10 w-10 rounded-lg shadow-sm border" id="adminTrigger" onclick="handleTap()">
            <div>
                <span class="block font-black text-xs uppercase text-blue-900 tracking-tighter leading-none">U.S. Home Improvement LLC</span>
                <span class="block text-[7px] font-extrabold text-emerald-600 uppercase italic">● Licensed Dispatch Terminal</span>
            </div>
        </div>
        <div class="hidden md:flex gap-6 text-[9px] font-black text-slate-400 uppercase tracking-widest">
            <a href="#" onclick="showPage('homePage')" class="hover:text-blue-600">Home</a>
            <a href="#" onclick="showPage('servicesPage')" class="hover:text-blue-600">Services</a>
            <a href="#" onclick="showPage('privacyPage')" class="hover:text-blue-600">Compliance</a>
            <button onclick="showPage('formPage')" class="bg-blue-600 text-white px-4 py-2 rounded-lg">Get Quote</button>
        </div>
    </nav>

    <section id="homePage" class="page-section active">
        <header class="py-20 px-6 text-center bg-slate-50 border-b">
            <div class="max-w-4xl mx-auto">
                <span class="bg-blue-100 text-blue-700 px-4 py-1 rounded-full text-[8px] font-black uppercase tracking-widest mb-4 inline-block italic">Nationwide Inspection Authority</span>
                <h1 class="text-4xl md:text-6xl font-black uppercase italic tracking-tighter mb-6 text-slate-900 leading-none">Your Home, Our <span class="text-blue-600">Priority.</span></h1>
                <p class="text-slate-500 font-bold uppercase text-[9px] tracking-[0.3em] mb-10 italic">Providing Certified Site Estimates Across 50 States</p>
                <button onclick="showPage('formPage')" class="btn-action max-w-sm">Secure Your Free Estimate</button>
            </div>
        </header>

        <div class="max-w-6xl mx-auto px-6 py-16 grid md:grid-cols-3 gap-8">
            <div class="glass-card overflow-hidden cursor-pointer" onclick="startSvc('Windows')">
                <img src="Screenshot_2026-04-19-06-21-41-75.png" class="h-48 w-full object-cover">
                <div class="p-6"><h3 class="font-black text-blue-900 uppercase italic text-sm">Energy Windows</h3><p class="text-[9px] font-bold text-slate-400 mt-2 uppercase">Triple-pane high efficiency systems.</p></div>
            </div>
            <div class="glass-card overflow-hidden cursor-pointer" onclick="startSvc('Roofing')">
                <img src="Screenshot_2026-04-19-06-03-04-64.png" class="h-48 w-full object-cover">
                <div class="p-6"><h3 class="font-black text-blue-900 uppercase italic text-sm">Roofing Matrix</h3><p class="text-[9px] font-bold text-slate-400 mt-2 uppercase">Lifetime architectural protection.</p></div>
            </div>
            <div class="glass-card overflow-hidden cursor-pointer" onclick="startSvc('Solar')">
                <img src="Screenshot_2026-04-19-06-03-04-64.png" class="h-48 w-full object-cover"> <div class="p-6"><h3 class="font-black text-blue-900 uppercase italic text-sm">Solar Power</h3><p class="text-[9px] font-bold text-slate-400 mt-2 uppercase">Zero-down smart energy solutions.</p></div>
            </div>
        </div>
    </section>

    <section id="servicesPage" class="page-section py-20 bg-white">
        <div class="max-w-4xl mx-auto px-6">
            <h2 class="text-3xl font-black italic uppercase text-center mb-16">Certified <span class="text-blue-600">Home Services</span></h2>
            <div class="grid md:grid-cols-2 gap-6">
                <div class="p-8 bg-slate-50 rounded-3xl border border-slate-100">
                    <h4 class="font-black uppercase mb-4 text-blue-900 italic">Interior Remodeling</h4>
                    <ul class="text-[10px] font-bold text-slate-500 space-y-3 uppercase">
                        <li>● Kitchen Countertops & Cabinets</li>
                        <li>● Bathroom Spa Conversions</li>
                        <li>● Luxury Flooring Installation</li>
                    </ul>
                </div>
                <div class="p-8 bg-slate-50 rounded-3xl border border-slate-100">
                    <h4 class="font-black uppercase mb-4 text-blue-900 italic">Exterior Defense</h4>
                    <ul class="text-[10px] font-bold text-slate-500 space-y-3 uppercase">
                        <li>● Fiber Cement Siding</li>
                        <li>● High-Security Entry Doors</li>
                        <li>● Hurricane-Resistant Windows</li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <section id="privacyPage" class="page-section py-20 px-6">
        <div class="max-w-3xl mx-auto glass-card p-10">
            <h2 class="text-2xl font-black uppercase italic text-blue-900 mb-8">Privacy Policy & <span class="text-blue-600">Compliance</span></h2>
            <div class="text-[10px] font-bold text-slate-500 space-y-6 uppercase leading-relaxed">
                <p>U.S. Home Improvement LLC operates as a nationwide dispatch terminal for licensed contractors. By submitting your information, you authorize our network to contact you regarding home improvement services via phone, SMS, or email.</p>
                <p><strong>Data Protection:</strong> All consumer data is encrypted using 256-bit SSL technology. We do not sell or trade your personal information to third-party marketing firms outside our authorized contractor network.</p>
                <p><strong>Lead Authorization:</strong> Information collected (Name, Email, Phone, Credit Score, Ownership Status) is used solely for the purpose of generating a project estimate and scheduling a site survey.</p>
            </div>
        </div>
    </section>

    <section id="formPage" class="page-section py-16 bg-slate-100 min-h-screen px-6">
        <div class="max-w-xl mx-auto glass-card p-8 md:p-12 relative overflow-hidden">
            <div id="progress" class="h-1 bg-blue-600 absolute top-0 left-0 transition-all duration-500" style="width: 33%"></div>
            
            <form id="proMasterForm">
                <div class="form-step active" id="s1">
                    <h3 class="text-xl font-black italic uppercase mb-8">01. Service <span class="text-blue-600">Authorization</span></h3>
                    <select id="mainService" class="input-pro mb-4" onchange="loadQs()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                    </select>
                    <select id="isOwner" class="input-pro mb-8" required>
                        <option value="Yes">Confirmed Homeowner</option>
                        <option value="No">Tenant / Renter</option>
                    </select>
                    <button type="button" onclick="nextStep('s2', 66)" class="btn-action">Continue</button>
                </div>

                <div class="form-step" id="s2">
                    <h3 class="text-xl font-black italic uppercase mb-8">02. Project <span class="text-blue-600">Specs</span></h3>
                    <div id="dynamicQs"></div>
                    <label class="text-[9px] font-black text-slate-400 uppercase block mb-2 mt-4">Estimated Credit Health</label>
                    <select id="creditScore" class="input-pro mb-8" required>
                        <option value="Excellent (720+)">Excellent (720+)</option>
                        <option value="Good (660-719)">Good (660-719)</option>
                        <option value="Fair (Below 660)">Fair / Other</option>
                    </select>
                    <button type="button" onclick="nextStep('s3', 100)" class="btn-action">Final Step</button>
                </div>

                <div class="form-step" id="s3">
                    <h3 class="text-xl font-black italic uppercase mb-8">03. Dispatch <span class="text-blue-600">Details</span></h3>
                    <input type="text" id="cName" placeholder="Full Name" class="input-pro mb-3" required>
                    <input type="email" id="cEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="text" id="cAddress" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-4">
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-pro" maxlength="5" required>
                        <input type="tel" id="cPhone" placeholder="Mobile Number" class="input-pro" required>
                    </div>
                    <label class="text-[9px] font-black text-slate-400 uppercase block mb-2">Preferred Inspection Window</label>
                    <div class="grid grid-cols-2 gap-3 mb-8">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="10am-1pm">10AM-1PM</option>
                            <option value="1pm-4pm">1PM-4PM</option>
                            <option value="4pm-7pm">4PM-7PM</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action shadow-xl">Confirm Authorization</button>
                </div>
            </form>

            <div id="receiptBox" class="hidden text-center py-6">
                <div class="text-5xl mb-4">✅</div>
                <h2 class="text-2xl font-black text-blue-900 uppercase italic">Dispatch Authorized</h2>
                <div class="mt-8 p-6 bg-slate-50 border-2 border-dashed rounded-3xl text-left text-[10px] font-bold uppercase">
                    <p class="text-slate-400 mb-4">Ref ID: #<span id="r-id"></span></p>
                    <div class="space-y-3">
                        <p>Project: <span id="r-svc" class="text-blue-600"></span></p>
                        <p>Customer: <span id="r-name"></span></p>
                        <p>Schedule: <span id="r-date" class="text-emerald-600"></span></p>
                        <p>Location: <span id="r-addr"></span></p>
                    </div>
                </div>
                <p class="mt-8 text-[8px] font-bold text-slate-400 italic uppercase leading-relaxed">Save this receipt. A field specialist will contact you to verify site access.</p>
                <button onclick="location.reload()" class="mt-8 text-blue-600 font-black text-[9px] uppercase">Back To Home</button>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-8"><h3 class="font-black italic text-blue-900 uppercase">Master Dispatch Terminal</h3><button onclick="closeAdmin()" class="text-red-500 font-black uppercase text-xs">Exit</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="ENTER PIN"><button onclick="unlock()" class="btn-action max-w-[200px]">Access Hub</button></div>
        <div id="leadsList" class="hidden space-y-4 pb-20"></div>
    </div>

    <footer class="bg-white border-t py-16 px-6 text-center">
        <h4 class="font-black text-blue-900 uppercase text-xs mb-4 italic tracking-widest">U.S. Home Improvement LLC</h4>
        <p class="text-[8px] text-slate-400 font-black uppercase mb-6 italic">Support: ushomeimprovement07@gmail.com</p>
        <p class="text-[7px] text-slate-300 font-bold uppercase max-w-sm mx-auto leading-loose">
            702 Main Street, Woodland, CA 95695. <br>
            © 2026 National Dispatch Terminal. All Rights Reserved. Data Protected by Enterprise Encryption.
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

        // LOGO SECURITY
        let taps = 0, tapT;
        function handleTap() { taps++; clearTimeout(tapT); if(taps>=5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } tapT=setTimeout(()=>taps=0,2000); }

        function showPage(id) {
            document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo(0,0);
        }

        function startSvc(svc) {
            document.getElementById('mainService').value = svc;
            loadQs();
            showPage('formPage');
        }

        function nextStep(id, pct) {
            document.querySelectorAll('.form-step').forEach(s=>s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            document.getElementById('progress').style.width = pct + '%';
        }

        function loadQs() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicQs');
            const data = {
                'Windows': [{l:'Number of Windows', o:['1-5','6-10','11-20','21+']},{l:'Frame Type', o:['Vinyl','Fiberglass','Wood']}],
                'Roofing': [{l:'Roof Age', o:['1-10 years','11-20 years','20+ years']},{l:'Active Leaks?', o:['None','Minor','Emergency']}],
                'Solar': [{l:'Monthly Power Bill', o:['$50-150','$151-300','$301+']},{l:'Roof Direction', o:['South Facing','Other']}]
            };
            const current = data[s] || [{l:'Timeline', o:['Immediate','1-3 Months']}];
            container.innerHTML = current.map((q, i) => `
                <label class="text-[9px] font-black text-slate-400 uppercase block mb-2 mt-4">${q.l}</label>
                <select id="q${i}" class="input-pro mb-3">${q.o.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>
            `).join('');
        }
        loadQs();

        document.getElementById('proMasterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const id = Math.floor(100000 + Math.random() * 900000);
            const svc = document.getElementById('mainService').value;
            const name = document.getElementById('cName').value;
            const appt = `${document.getElementById('appDate').value} (${document.getElementById('appSlot').value})`;

            const data = {
                id: id,
                service: svc,
                owner: document.getElementById('isOwner').value,
                credit: document.getElementById('creditScore').value,
                name: name,
                email: document.getElementById('cEmail').value,
                phone: document.getElementById('cPhone').value,
                address: document.getElementById('cAddress').value,
                zip: document.getElementById('cZip').value,
                spec: document.getElementById('q0')?.value || 'Standard',
                appointment: appt,
                timestamp: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                document.getElementById('proMasterForm').classList.add('hidden');
                document.getElementById('receiptBox').classList.remove('hidden');
                document.getElementById('r-id').innerText = id;
                document.getElementById('r-svc').innerText = svc.toUpperCase();
                document.getElementById('r-name').innerText = name;
                document.getElementById('r-date').innerText = appt;
                document.getElementById('r-addr').innerText = data.address;
            });
        });

        // ADMIN TERMINAL
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value==="786"){ document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        function sync() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="p-6 border rounded-2xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] absolute top-4 right-4">${leads[k].service}</span>
                        <h4 class="text-xl font-black italic text-blue-900 mb-2">#${leads[k].id} | ${leads[k].name}</h4>
                        <div class="grid grid-cols-2 gap-4 uppercase">
                            <p>📧 Email: <span class="text-blue-600">${leads[k].email}</span></p>
                            <p>📞 Phone: ${leads[k].phone}</p>
                            <p>📍 Site: ${leads[k].address} (${leads[k].zip})</p>
                            <p>👤 Owner: ${leads[k].owner} | 💳 Credit: ${leads[k].credit}</p>
                            <p>🛠 Spec: ${leads[k].spec}</p>
                            <p class="text-emerald-600 col-span-2 border-t pt-2">📅 Appt: ${leads[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black w-full text-center border-t pt-2 text-[9px]">DELETE DISPATCH PERMANENTLY</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'Terminal Clear';
            });
        }
        function del(id) { if(confirm('Erase lead?')) db.ref('leads/'+id).remove(); }

        // FAKE NOTIFICATIONS
        const names = ["Sarah", "David", "Michael", "Linda", "John", "Jessica", "James", "Emily"];
        const cities = ["CA", "TX", "FL", "NY", "NV", "GA", "AZ", "WA"];
        setInterval(() => {
            const toast = document.getElementById('notif-toast');
            document.getElementById('notif-text').innerText = "⚡ " + names[Math.floor(Math.random()*names.length)] + " from " + cities[Math.floor(Math.random()*cities.length)] + " just authorized a project survey!";
            toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 5000);
        }, 12000);
    </script>
</body>
</html>
