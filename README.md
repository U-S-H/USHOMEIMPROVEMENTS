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
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px; border-radius: 14px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; }

        /* Multi-Page Animation */
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s ease; }
        .form-step { display: none; }
        .form-step.active { display: block; animation: slideUp 0.3s ease; }
        
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideUp { from { transform: translateY(10px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        /* Backgrounds & Hover Effects */
        .hero-bg { background: linear-gradient(rgba(15, 23, 42, 0.7), rgba(15, 23, 42, 0.7)), url('WA_1776549716792.jpeg'); background-size: cover; background-position: center; background-attachment: fixed; }
        .service-card { border-radius: 24px; overflow: hidden; border: 1px solid #f1f5f9; transition: 0.4s ease; cursor: pointer; background: white; }
        .service-card:hover { transform: translateY(-10px); box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.1); }
        .service-card img { width: 100%; height: 220px; object-fit: cover; }

        /* Fake Notifications Toast */
        #notif-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 12px 22px; border-radius: 50px; box-shadow: 0 10px 30px rgba(0,0,0,0.12); border-left: 5px solid #059669; display: none; z-index: 9999; }
    </style>
</head>
<body>

    <div id="notif-toast"><p id="notif-text" class="text-[10px] font-black text-slate-700 uppercase italic"></p></div>

    <nav class="bg-white/95 backdrop-blur-md border-b px-6 py-4 flex justify-between items-center sticky top-0 z-[2000]">
        <div class="flex items-center gap-3 cursor-pointer" onclick="showPage('homePage')">
            <img src="Screenshot_2026-04-19-06-03-04-64.png" class="h-10 w-10 rounded-xl shadow-md border" id="adminTrigger" onclick="handleTap()">
            <div>
                <span class="block font-black text-sm uppercase text-blue-900 leading-none">U.S. Home Improvement LLC</span>
                <span class="block text-[8px] font-extrabold text-emerald-600 uppercase italic">● Licensed National Dispatch Terminal</span>
            </div>
        </div>
        <div class="hidden md:flex gap-8 text-[9px] font-black text-slate-400 uppercase tracking-widest">
            <a href="#" onclick="showPage('homePage')" class="hover:text-blue-600">Home</a>
            <a href="#" onclick="showPage('servicesPage')" class="hover:text-blue-600">Services</a>
            <a href="#" onclick="showPage('legalPage')" class="hover:text-blue-600">Compliance</a>
            <button onclick="showPage('formPage')" class="bg-blue-600 text-white px-5 py-2 rounded-lg hover:bg-blue-700 transition">Get Estimate</button>
        </div>
    </nav>

    <section id="homePage" class="page-section active">
        <header class="hero-bg py-32 px-6 text-center text-white border-b">
            <div class="max-w-4xl mx-auto">
                <span class="bg-white/10 text-white px-4 py-1 rounded-full text-[9px] font-black uppercase tracking-widest mb-6 inline-block italic border border-white/20">Nationwide Authorized Authority</span>
                <h1 class="text-4xl md:text-7xl font-black uppercase italic tracking-tighter mb-8 leading-none">Premium American <br><span class="text-blue-400">Home Remodeling.</span></h1>
                <p class="text-blue-100 font-bold uppercase text-[10px] tracking-[0.4em] mb-12 max-w-lg mx-auto leading-relaxed">Connecting Homeowners to Certified Contractor Networks in All 50 States</p>
                <button onclick="showPage('formPage')" class="btn-action max-w-sm shadow-2xl shadow-blue-900/40">Secure Your Site Survey</button>
            </div>
        </header>

        <div class="max-w-7xl mx-auto px-6 py-24 grid md:grid-cols-2 lg:grid-cols-4 gap-8">
            <div class="service-card" onclick="startSvc('Roofing')">
                <img src="WA_1776549716792.jpeg">
                <div class="p-6"><h4 class="font-black text-blue-900 text-xs uppercase mb-2">Lifetime Roofing</h4><p class="text-[9px] font-bold text-slate-400 uppercase leading-relaxed italic">Architectural protection for your primary investment.</p></div>
            </div>
            <div class="service-card" onclick="startSvc('Solar')">
                <img src="WA_1776549781247.jpeg">
                <div class="p-6"><h4 class="font-black text-blue-900 text-xs uppercase mb-2">Solar Efficiency</h4><p class="text-[9px] font-bold text-slate-400 uppercase leading-relaxed italic">Grid-independent power & smart bachat solutions.</p></div>
            </div>
            <div class="service-card" onclick="startSvc('Windows')">
                <img src="WA_1776549555727.jpeg">
                <div class="p-6"><h4 class="font-black text-blue-900 text-xs uppercase mb-2">Energy Windows</h4><p class="text-[9px] font-bold text-slate-400 uppercase leading-relaxed italic">Triple-Pane sealing for ultimate energy bachat.</p></div>
            </div>
            <div class="service-card" onclick="startSvc('Doors')">
                <img src="WA_1776549622236.jpeg">
                <div class="p-6"><h4 class="font-black text-blue-900 text-xs uppercase mb-2">Security Doors</h4><p class="text-[9px] font-bold text-slate-400 uppercase leading-relaxed italic">Hurricane-rated and high-security entry systems.</p></div>
            </div>
        </div>
    </section>

    <section id="servicesPage" class="page-section bg-slate-50 py-24 px-6 border-t">
        <div class="max-w-6xl mx-auto">
            <h2 class="text-3xl font-black italic text-center uppercase mb-16 tracking-tighter">Full <span class="text-blue-600">Enterprise Portfolio</span></h2>
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-10">
                <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm">
                    <img src="WA_1776550066723.jpeg" class="w-full h-44 object-cover rounded-2xl mb-6">
                    <h4 class="font-black text-blue-900 uppercase italic mb-3">Garage Door Matrix</h4>
                    <p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed mb-4">Smart-integrated insulated doors for safety and extreme weather protection.</p>
                    <button onclick="startSvc('Garage')" class="text-blue-600 font-black text-[9px] uppercase underline">Request Specs</button>
                </div>
                <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm">
                    <img src="WA_1776549917709.jpeg" class="w-full h-44 object-cover rounded-2xl mb-6">
                    <h4 class="font-black text-blue-900 uppercase italic mb-3">Gourmet Kitchens</h4>
                    <p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed mb-4">Custom cabinetry and quartz island installations. Full electrical & plumbing rework.</p>
                    <button onclick="startSvc('Kitchen')" class="text-blue-600 font-black text-[9px] uppercase underline">Request Specs</button>
                </div>
                <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm">
                    <img src="WA_1776549862258.jpeg" class="w-full h-44 object-cover rounded-2xl mb-6">
                    <h4 class="font-black text-blue-900 uppercase italic mb-3">Bathroom Spas</h4>
                    <p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed mb-4">Modern tiling and walk-in shower conversions. Authorized waterproofing technology.</p>
                    <button onclick="startSvc('Bathroom')" class="text-blue-600 font-black text-[9px] uppercase underline">Request Specs</button>
                </div>
                <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm">
                    <img src="WA_1776549990293.jpeg" class="w-full h-44 object-cover rounded-2xl mb-6">
                    <h4 class="font-black text-blue-900 uppercase italic mb-3">Custom Decks</h4>
                    <p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed mb-4">Composite and premium wood deck construction. Permit handling and site survey included.</p>
                    <button onclick="startSvc('Deck')" class="text-blue-600 font-black text-[9px] uppercase underline">Request Specs</button>
                </div>
                <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm flex items-center justify-center text-center">
                    <div>
                        <h4 class="font-black text-blue-900 uppercase italic mb-2">More Services</h4>
                        <p class="text-[9px] font-bold text-slate-400 uppercase italic">Gutters, Paint, & Insulation</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="formPage" class="page-section bg-slate-50 py-20 min-h-screen px-6">
        <div class="max-w-xl mx-auto glass-card p-10 relative overflow-hidden">
            <div id="p-bar" class="h-1.5 bg-blue-600 absolute top-0 left-0 transition-all duration-500" style="width: 33%"></div>
            
            <form id="proMasterForm">
                <div class="form-step active" id="s1">
                    <h3 class="text-xl font-black italic uppercase mb-8">01. Area <span class="text-blue-600">Verification</span></h3>
                    <select id="mainService" class="input-pro mb-4" onchange="loadSpecs()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Spas</option>
                        <option value="Garage">Garage Systems</option>
                        <option value="Deck">Custom Decking</option>
                    </select>
                    <select id="isOwner" class="input-pro mb-8" required>
                        <option value="Yes">Confirmed Homeowner</option>
                        <option value="No">Tenant / Other</option>
                    </select>
                    <button type="button" onclick="nextStep('s2', 66)" class="btn-action">Proceed To Specs</button>
                </div>

                <div class="form-step" id="s2">
                    <h3 class="text-xl font-black italic uppercase mb-8">02. Project <span class="text-blue-600">Qualifications</span></h3>
                    <div id="dynamicSpecs"></div>
                    <label class="text-[9px] font-black text-slate-400 uppercase block mb-2 mt-4 italic">Est. Credit Health</label>
                    <select id="creditScore" class="input-pro mb-8" required>
                        <option value="Excellent (720+)">Excellent (720+)</option>
                        <option value="Good (660-719)">Good (660-719)</option>
                        <option value="Fair (Below 660)">Fair / Other</option>
                    </select>
                    <button type="button" onclick="nextStep('s3', 100)" class="btn-action">Authorize Dispatch</button>
                </div>

                <div class="form-step" id="s3">
                    <h3 class="text-xl font-black italic uppercase mb-8">03. Site <span class="text-blue-600">Authorization</span></h3>
                    <input type="text" id="cName" placeholder="Full Legal Name" class="input-pro mb-3" required>
                    <input type="email" id="cEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="text" id="cAddress" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-4">
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-pro" maxlength="5" required>
                        <input type="tel" id="cPhone" placeholder="Mobile Number" class="input-pro" required>
                    </div>
                    <label class="text-[9px] font-black text-slate-400 uppercase block mb-2 italic">Inspection Appointment Slot</label>
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
                <div class="text-6xl mb-6">✅</div>
                <h2 class="text-2xl font-black text-blue-900 uppercase italic">Application Authorized</h2>
                <div class="mt-8 p-6 bg-slate-50 border-2 border-dashed rounded-3xl text-left text-[11px] font-bold uppercase space-y-4">
                    <p class="text-slate-400">Ref ID: #<span id="r-id"></span></p>
                    <p>Service: <span id="r-svc" class="text-blue-600"></span></p>
                    <p>Customer: <span id="r-name"></span></p>
                    <p>Slot: <span id="r-date" class="text-emerald-600"></span></p>
                </div>
                <p class="mt-10 text-[8px] font-bold text-slate-400 italic uppercase">Save this receipt. A field specialist will contact you shortly to verify site access.</p>
                <button onclick="location.reload()" class="mt-8 text-blue-600 font-black text-[10px] uppercase">Back To Home</button>
            </div>
        </div>
    </section>

    <section id="legalPage" class="page-section py-20 px-6">
        <div class="max-w-4xl mx-auto glass-card p-12">
            <h2 class="text-2xl font-black text-blue-900 uppercase italic mb-10">Compliance & <span class="text-blue-600">Privacy Portfolio</span></h2>
            <div class="text-[11px] font-bold text-slate-500 space-y-8 uppercase leading-relaxed tracking-wide">
                <div><h4 class="text-blue-900 mb-2 font-black italic">01. Professional Dispatch</h4><p>U.S. Home Improvement LLC operates as a National Enterprise Terminal. We connect homeowners with state-licensed contractors for site technical surveys and certified estimates.</p></div>
                <div><h4 class="text-blue-900 mb-2 font-black italic">02. Data Protection (GDPR/CCPA)</h4><p>All consumer data (Name, Phone, Site Specs) is protected by 256-bit AES encryption. We never sell data to unauthorized 3rd parties outside our direct inspection network.</p></div>
                <div><h4 class="text-blue-900 mb-2 font-black italic">03. BBB Compliance</h4><p>We maintain an A+ equivalent trust standard. Our contractors are vetted for valid licensing, insurance, and professional background authorization.</p></div>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-8"><h3 class="font-black italic text-blue-900 uppercase">Master Dispatch Terminal</h3><button onclick="closeAdmin()" class="text-red-500 font-black text-xs uppercase">Exit Terminal</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="ENTER PIN"><button onclick="unlock()" class="btn-action max-w-[200px]">Access Hub</button></div>
        <div id="leadsList" class="hidden space-y-4 pb-20"></div>
    </div>

    <footer class="bg-white border-t py-20 px-6 text-center">
        <div class="flex justify-center gap-10 mb-12 grayscale opacity-40">
            <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Forbes_logo.svg" class="h-4">
            <img src="https://upload.wikimedia.org/wikipedia/commons/a/a2/Better_Business_Bureau_logo.svg" class="h-4">
            <img src="https://upload.wikimedia.org/wikipedia/commons/c/c8/HomeAdvisor_logo.svg" class="h-4">
        </div>
        
        <h4 class="font-black text-blue-900 uppercase text-xs mb-4 italic tracking-widest">U.S. Home Improvement LLC</h4>
        <p class="text-[8px] text-slate-400 font-black uppercase mb-6 italic">Dispatch: ushomeimprovement07@gmail.com</p>
        <p class="text-[8px] text-slate-300 font-bold uppercase max-w-sm mx-auto leading-loose">
            702 Main Street, Woodland, CA 95695. <br>
            Nationwide Authorized Terminal © 2026. All Data Encrypted.
        </p>
    </footer>

    <script>
        // FIREBASE CONNECT
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

        // ADMIN LOGO 5-TAP TRICK
        let taps = 0, tapT;
        function handleTap() { taps++; clearTimeout(tapT); if(taps>=5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } tapT=setTimeout(()=>taps=0,2000); }

        // NAVIGATION LOGIC
        function showPage(id) {
            document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo(0,0);
        }

        function startSvc(svc) {
            document.getElementById('mainService').value = svc;
            loadSpecs();
            showPage('formPage');
        }

        function nextStep(id, pct) {
            document.querySelectorAll('.form-step').forEach(s=>s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            document.getElementById('p-bar').style.width = pct + '%';
        }

        // DYNAMIC SPEC QUESTIONS
        function loadSpecs() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicSpecs');
            const data = {
                'Windows': [{l:'Window Quantity', o:['1-5','6-10','11-20','21+']},{l:'Frame Type', o:['Vinyl','Fiberglass','Wood']}],
                'Roofing': [{l:'Current Age', o:['1-10 yrs','11-20 yrs','20+ yrs']},{l:'Active Leaks?', o:['None','Minor','Serious']}],
                'Solar': [{l:'Electric Bill', o:['$50-150','$151-300','$301+']},{l:'Sun Exposure', o:['Direct Sun','Partial']}]
            };
            const current = data[s] || [{l:'Project Timeline', o:['Immediate','1-3 Months']}];
            container.innerHTML = current.map((q, i) => `
                <label class="text-[9px] font-black text-slate-400 uppercase block mb-2 mt-4 italic tracking-widest">${q.l}</label>
                <select id="q${i}" class="input-pro mb-3">${q.o.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>
            `).join('');
        }
        loadSpecs();

        // DISPATCH SUBMISSION
        document.getElementById('proMasterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const id = Math.floor(100000 + Math.random() * 900000);
            const svc = document.getElementById('mainService').value;
            const name = document.getElementById('cName').value;
            const appt = `${document.getElementById('appDate').value} (${document.getElementById('appSlot').value})`;

            const data = {
                id: id, service: svc, owner: document.getElementById('isOwner').value,
                credit: document.getElementById('creditScore').value, name: name,
                email: document.getElementById('cEmail').value, phone: document.getElementById('cPhone').value,
                address: document.getElementById('cAddress').value, zip: document.getElementById('cZip').value,
                spec: document.getElementById('q0')?.value || 'Standard', appointment: appt,
                timestamp: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                document.getElementById('proMasterForm').classList.add('hidden');
                document.getElementById('receiptBox').classList.remove('hidden');
                document.getElementById('r-id').innerText = id;
                document.getElementById('r-svc').innerText = svc.toUpperCase();
                document.getElementById('r-name').innerText = name;
                document.getElementById('r-date').innerText = appt;
            });
        });

        // ADMIN TERMINAL ENGINE
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value==="786"){ document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); syncLeads(); } }
        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="p-6 border rounded-3xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] absolute top-4 right-4 uppercase">${leads[k].service}</span>
                        <h4 class="text-xl font-black italic text-blue-900 mb-2">#${leads[k].id} | ${leads[k].name}</h4>
                        <div class="grid grid-cols-2 gap-4 uppercase italic">
                            <p>📧 <span class="text-blue-600 underline">${leads[k].email}</span></p>
                            <p>📞 Cell: ${leads[k].phone}</p>
                            <p>📍 Site: ${leads[k].address} (${leads[k].zip})</p>
                            <p>💳 Credit: ${leads[k].credit}</p>
                            <p>👤 Owner: ${leads[k].owner} | 🛠 Spec: ${leads[k].spec}</p>
                            <p class="text-emerald-600 col-span-2 border-t pt-2">📅 Appt: ${leads[k].appointment}</p>
                        </div>
                        <button onclick="delLead('${k}')" class="mt-4 text-red-500 font-black w-full border-t pt-2 text-[9px] uppercase">Erase Authorized Dispatch</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Active Dispatch Files';
            });
        }
        function delLead(id) { if(confirm('Delete permanently?')) db.ref('leads/'+id).remove(); }

        // FAKE SOCIAL PROOF (Names & Cities)
        const fakeN = ["Jessica", "Marcus", "Brian", "Ashley", "Robert", "Kimberly", "Thomas", "Nicole"];
        const fakeC = ["California", "Texas", "Florida", "New York", "Arizona", "Georgia", "Nevada"];
        setInterval(() => {
            const toast = document.getElementById('notif-toast');
            document.getElementById('notif-text').innerText = "⚡ " + fakeN[Math.floor(Math.random()*fakeN.length)] + " from " + fakeC[Math.floor(Math.random()*fakeC.length)] + " authorized a site survey!";
            toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 5000);
        }, 15000);
    </script>
</body>
</html>
