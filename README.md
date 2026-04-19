<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | National Enterprise Dispatch</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfd; color: #0f172a; scroll-behavior: smooth; }
        
        /* UI Elements */
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 32px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.08); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; font-size: 14px; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 16px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; }

        /* Multi-Page & Steps */
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s ease; }
        .form-step { display: none; }
        .form-step.active { display: block; animation: slideUp 0.3s ease; }
        
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideUp { from { transform: translateY(10px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        /* Progress Bar */
        .progress-line { height: 6px; background: #f1f5f9; border-radius: 10px; overflow: hidden; margin-bottom: 30px; }
        #progress-fill { height: 100%; width: 33%; background: #2563eb; transition: 0.4s; }

        /* Badges */
        .trust-badge { filter: grayscale(100%); opacity: 0.5; transition: 0.3s; }
        .trust-badge:hover { filter: grayscale(0%); opacity: 1; }
    </style>
</head>
<body>

    <div id="notif-toast" class="fixed bottom-6 left-6 bg-white p-4 rounded-3xl shadow-2xl border-l-4 border-emerald-500 z-[9999] hidden">
        <p id="notif-text" class="text-[10px] font-black text-slate-700 uppercase italic"></p>
    </div>

    <nav class="bg-white/90 backdrop-blur-md border-b px-6 py-4 flex justify-between items-center sticky top-0 z-[2000]">
        <div class="flex items-center gap-3 cursor-pointer" onclick="showPage('homePage')">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border" id="adminTrigger" onclick="handleTap()">
            <div>
                <span class="block font-black text-sm uppercase text-blue-900 italic">U.S. Home Improvement LLC</span>
                <span class="block text-[8px] font-extrabold text-emerald-600 uppercase italic">● National Dispatch Center</span>
            </div>
        </div>
        <div class="hidden md:flex gap-6 text-[10px] font-black text-slate-400 uppercase">
            <a href="#" onclick="showPage('homePage')" class="hover:text-blue-600">Home</a>
            <a href="#" onclick="showPage('servicesPage')" class="hover:text-blue-600">Our Services</a>
            <a href="#" onclick="showPage('formPage')" class="text-blue-600 font-black">Get Free Estimate</a>
        </div>
    </nav>

    <section id="homePage" class="page-section active">
        <header class="py-20 px-6 text-center bg-slate-50">
            <h1 class="text-5xl md:text-7xl font-black uppercase italic tracking-tighter mb-6 text-slate-900 leading-none">Protect Your <span class="text-blue-600">Investment.</span></h1>
            <p class="text-slate-500 font-bold uppercase text-[10px] tracking-[0.3em] mb-12">Authorized Site Surveys & Professional Estimates</p>
            <div class="flex justify-center gap-8 mb-16 trust-badge-container">
                <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Forbes_logo.svg" class="trust-badge h-4">
                <img src="https://upload.wikimedia.org/wikipedia/commons/a/a2/Better_Business_Bureau_logo.svg" class="trust-badge h-4">
                <img src="https://upload.wikimedia.org/wikipedia/commons/c/c8/HomeAdvisor_logo.svg" class="trust-badge h-4">
            </div>
            <button onclick="showPage('formPage')" class="btn-action max-w-sm shadow-xl shadow-blue-100">Start Application</button>
        </header>

        <div class="max-w-6xl mx-auto px-6 py-20 grid md:grid-cols-3 gap-8">
            <div class="matrix-card glass-card p-2 cursor-pointer" onclick="startSvc('Roofing')">
                <img src="./WA_1776549716792.jpeg" class="rounded-2xl h-48 w-full object-cover mb-4">
                <div class="p-4"><h3 class="font-black text-blue-900 uppercase italic">Roofing Systems</h3><p class="text-[10px] font-bold text-slate-400 mt-2 uppercase">Lifetime Protection & Insulation</p></div>
            </div>
            <div class="matrix-card glass-card p-2 cursor-pointer" onclick="startSvc('Windows')">
                <img src="./WA_1776549555727.jpeg" class="rounded-2xl h-48 w-full object-cover mb-4">
                <div class="p-4"><h3 class="font-black text-blue-900 uppercase italic">Energy Windows</h3><p class="text-[10px] font-bold text-slate-400 mt-2 uppercase">Triple-Pane Efficiency</p></div>
            </div>
            <div class="matrix-card glass-card p-2 cursor-pointer" onclick="startSvc('Solar')">
                <img src="./WA_1776549781247.jpeg" class="rounded-2xl h-48 w-full object-cover mb-4">
                <div class="p-4"><h3 class="font-black text-blue-900 uppercase italic">Smart Solar</h3><p class="text-[10px] font-bold text-slate-400 mt-2 uppercase">Grid-Independent Power</p></div>
            </div>
        </div>
    </section>

    <section id="servicesPage" class="page-section py-20 bg-white">
        <div class="max-w-4xl mx-auto px-6">
            <h2 class="text-3xl font-black italic uppercase text-center mb-16">Full <span class="text-blue-600">Remodeling</span> Catalog</h2>
            <div class="space-y-6">
                <div class="p-8 border-2 border-slate-50 rounded-3xl bg-slate-50 flex justify-between items-center">
                    <div><h4 class="font-black text-xl mb-2">Kitchen & Bath Luxe</h4><p class="text-[10px] font-bold text-slate-500 uppercase">Custom counters, plumbing, and design layout.</p></div>
                    <button onclick="showPage('formPage')" class="text-blue-600 font-black text-xs uppercase underline">Get Info</button>
                </div>
                <div class="p-8 border-2 border-slate-50 rounded-3xl bg-slate-50 flex justify-between items-center">
                    <div><h4 class="font-black text-xl mb-2">Exterior Siding & Doors</h4><p class="text-[10px] font-bold text-slate-500 uppercase">Fiber cement siding and high-security doors.</p></div>
                    <button onclick="showPage('formPage')" class="text-blue-600 font-black text-xs uppercase underline">Get Info</button>
                </div>
            </div>
        </div>
    </section>

    <section id="formPage" class="page-section py-16 bg-slate-100 min-h-screen">
        <div class="max-w-xl mx-auto glass-card p-8 md:p-12">
            <div class="progress-line"><div id="progress-fill"></div></div>
            
            <form id="masterDispatchForm">
                <div class="form-step active" id="s1">
                    <h3 class="text-xl font-black italic uppercase mb-6">01. Service <span class="text-blue-600">Verification</span></h3>
                    <select id="mainService" class="input-pro mb-4" onchange="loadQs()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                    </select>
                    <select id="isOwner" class="input-pro mb-8" required>
                        <option value="Yes">I am the Legal Homeowner</option>
                        <option value="No">I am a Tenant / Renter</option>
                    </select>
                    <button type="button" onclick="goNext('s2', 66)" class="btn-action">Continue</button>
                </div>

                <div class="form-step" id="s2">
                    <h3 class="text-xl font-black italic uppercase mb-6">02. Site <span class="text-blue-600">Qualifications</span></h3>
                    <div id="dynamicQs"></div>
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-2 mt-4">Estimated Credit Score</label>
                    <select id="creditScore" class="input-pro mb-8" required>
                        <option value="Excellent (720+)">Excellent (720+)</option>
                        <option value="Good (660-719)">Good (660-719)</option>
                        <option value="Fair (Below 660)">Fair / Other</option>
                    </select>
                    <button type="button" onclick="goNext('s3', 100)" class="btn-action">Final Step</button>
                </div>

                <div class="form-step" id="s3">
                    <h3 class="text-xl font-black italic uppercase mb-6">03. Authorized <span class="text-blue-600">Dispatch</span></h3>
                    <input type="text" id="cName" placeholder="Full Name" class="input-pro mb-3" required>
                    <input type="email" id="cEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="text" id="cAddress" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-4">
                        <input type="text" id="cZip" placeholder="Zip" class="input-pro" required>
                        <input type="tel" id="cPhone" placeholder="Mobile #" class="input-pro" required>
                    </div>
                    <label class="text-[10px] font-black text-slate-400 uppercase block mb-2">Preferred Inspection Slot</label>
                    <div class="grid grid-cols-2 gap-3 mb-8">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="10am-1pm">10AM - 1PM</option>
                            <option value="1pm-4pm">1PM - 4PM</option>
                            <option value="4pm-7pm">4PM - 7PM</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action shadow-xl">Confirm Dispatch</button>
                </div>
            </form>

            <div id="receiptBox" class="hidden text-center">
                <div class="text-5xl mb-4">📋</div>
                <h2 class="text-2xl font-black text-blue-900 uppercase italic">Appointment Confirmed</h2>
                <div class="mt-8 p-6 bg-slate-50 border-2 border-dashed rounded-3xl text-left text-[11px] font-bold uppercase">
                    <p class="text-slate-400 mb-4">Tracking ID: #<span id="r-id"></span></p>
                    <div class="space-y-3">
                        <p>Project: <span id="r-svc" class="text-blue-600"></span></p>
                        <p>Name: <span id="r-name"></span></p>
                        <p>Schedule: <span id="r-date" class="text-emerald-600"></span></p>
                        <p>Location: <span id="r-addr"></span></p>
                    </div>
                </div>
                <p class="mt-8 text-[9px] font-bold text-slate-400 italic">Please save this screen. Our office will call you shortly.</p>
                <button onclick="location.reload()" class="mt-8 text-blue-600 font-black text-xs uppercase">Home</button>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-8"><h3 class="font-black italic text-blue-900 uppercase">Admin Leads Hub</h3><button onclick="closeAdmin()" class="text-red-500 font-black uppercase text-xs">Exit</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="ENTER PIN"><button onclick="unlock()" class="btn-action max-w-[200px]">Unlock</button></div>
        <div id="leadsList" class="hidden space-y-4 pb-20"></div>
    </div>

    <footer class="bg-white border-t py-16 px-6 text-center">
        <h4 class="font-black text-blue-900 uppercase text-xs mb-4 italic tracking-widest">U.S. Home Improvement LLC</h4>
        <p class="text-[9px] text-slate-400 font-black uppercase mb-6 italic">Support: ushomeimprovement07@gmail.com</p>
        <p class="text-[8px] text-slate-300 font-bold uppercase max-w-sm mx-auto leading-loose">
            Authorized National Dispatch Center. 702 Main Street, Woodland, CA 95695. Licensed, Insured, & Bonded.
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

        // LOGO TAP SECURITY
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

        function goNext(id, pct) {
            document.querySelectorAll('.form-step').forEach(s=>s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            document.getElementById('progress-fill').style.width = pct + '%';
        }

        function loadQs() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicQs');
            const data = {
                'Windows': [{l:'Number of Windows', o:['1-5','6-10','11+']},{l:'Frame Type', o:['Vinyl','Wood']}],
                'Roofing': [{l:'Roof Age', o:['1-10 years','11-20 years','20+ years']},{l:'Active Leaks?', o:['None','Minor','Major']}],
                'Solar': [{l:'Monthly Bill', o:['$50-150','$151-300','$301+']},{l:'Sun Exposure', o:['Full Sun','Partial']}]
            };
            const current = data[s] || [{l:'Timeline', o:['Immediate','1-3 Months']}];
            container.innerHTML = current.map((q, i) => `
                <label class="text-[10px] font-black text-slate-400 uppercase block mb-2 mt-4">${q.l}</label>
                <select id="q${i}" class="input-pro mb-3">${q.o.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>
            `).join('');
        }
        loadQs();

        document.getElementById('masterDispatchForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const id = Math.floor(100000 + Math.random() * 900000);
            const service = document.getElementById('mainService').value;
            const name = document.getElementById('cName').value;
            const appt = `${document.getElementById('appDate').value} (${document.getElementById('appSlot').value})`;
            const addr = document.getElementById('cAddress').value;

            const data = {
                id: id,
                service: service,
                owner: document.getElementById('isOwner').value,
                credit: document.getElementById('creditScore').value,
                name: name,
                email: document.getElementById('cEmail').value,
                phone: document.getElementById('cPhone').value,
                address: addr,
                zip: document.getElementById('cZip').value,
                spec: document.getElementById('q0')?.value || 'Standard',
                appointment: appt,
                timestamp: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                document.getElementById('masterDispatchForm').classList.add('hidden');
                document.getElementById('receiptBox').classList.remove('hidden');
                document.getElementById('r-id').innerText = id;
                document.getElementById('r-svc').innerText = service.toUpperCase();
                document.getElementById('r-name').innerText = name;
                document.getElementById('r-date').innerText = appt;
                document.getElementById('r-addr').innerText = addr;
            });
        });

        // ADMIN HUB
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value==="786"){ document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        function sync() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="p-6 border rounded-3xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] absolute top-4 right-4">${leads[k].service}</span>
                        <h4 class="text-xl font-black italic text-blue-900 mb-2">#${leads[k].id} | ${leads[k].name}</h4>
                        <div class="grid grid-cols-2 gap-4">
                            <p>📧 ${leads[k].email}</p>
                            <p>📞 ${leads[k].phone}</p>
                            <p>📍 ${leads[k].address} (${leads[k].zip})</p>
                            <p>💳 Credit: ${leads[k].credit}</p>
                            <p class="text-emerald-600 col-span-2 border-t pt-2">📅 Appt: ${leads[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black w-full text-center border-t pt-2">DELETE PERMANENTLY</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Active Leads';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }

        const notifs = ["John from Woodland authorized Roofing!", "David from TX requested Windows.", "New Solar survey booked in Florida!", "Contractor dispatched to Nevada."];
        setInterval(() => {
            const toast = document.getElementById('notif-toast');
            document.getElementById('notif-text').innerText = "⚡ " + notifs[Math.floor(Math.random()*notifs.length)];
            toast.style.display = 'block';
            setTimeout(() => toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 5000);
        }, 15000);
    </script>
</body>
</html>
