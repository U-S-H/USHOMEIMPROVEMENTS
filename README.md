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
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfd; color: #0f172a; scroll-behavior: smooth; }
        
        /* Layout & UI */
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 32px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.08); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; font-size: 14px; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 16px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; }

        /* Multi-Page Logic */
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Toast & Matrix */
        #notification-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 15px 25px; border-radius: 50px; box-shadow: 0 15px 35px rgba(0,0,0,0.1); border-left: 6px solid #059669; display: none; z-index: 9999; }
        .matrix-card { background: white; border-radius: 28px; overflow: hidden; border: 1px solid #f1f5f9; transition: 0.3s; cursor: pointer; }
        .matrix-card:hover { transform: translateY(-5px); box-shadow: 0 10px 20px rgba(0,0,0,0.05); }

        .form-step { display: none; }
        .form-step.active { display: block; animation: slideUp 0.3s ease; }
        @keyframes slideUp { from { transform: translateY(10px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
    </style>
</head>
<body>

    <div id="notification-toast"><p id="notif-text" class="text-[11px] font-bold text-slate-700"></p></div>

    <nav class="bg-white/90 backdrop-blur-md border-b px-6 py-5 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3 cursor-pointer" onclick="showPage('homePage')">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border" id="adminTrigger" onclick="handleTap()">
            <div>
                <span class="block font-black text-sm uppercase text-blue-900 italic">U.S. Home Improvement LLC</span>
                <span class="block text-[8px] font-extrabold text-emerald-600 uppercase italic">● Licensed National Dispatch Terminal</span>
            </div>
        </div>
        <div class="hidden md:flex gap-6 text-[10px] font-black text-slate-400 uppercase tracking-widest">
            <a href="#" onclick="showPage('homePage')" class="hover:text-blue-600">Home</a>
            <a href="#" onclick="showPage('servicesPage')" class="hover:text-blue-600">Services</a>
            <a href="#" onclick="showPage('formPage')" class="text-blue-600">Get Quote</a>
        </div>
    </nav>

    <section id="homePage" class="page-section active">
        <header class="py-20 px-6 text-center bg-slate-50">
            <h1 class="text-4xl md:text-6xl font-black uppercase italic tracking-tighter mb-4 text-slate-900">National <span class="text-blue-600">Dispatch</span> Center</h1>
            <p class="text-slate-500 font-bold uppercase text-[10px] tracking-[0.4em] mb-10">Authorized For Professional Site Estimates In 50 States</p>
            <button onclick="showPage('formPage')" class="btn-action max-w-sm">Get Started Today</button>
            <div class="mt-8 flex justify-center gap-2">
                <span class="text-yellow-400 text-xl">★★★★★</span>
                <span class="text-[11px] font-black self-center text-slate-700 uppercase">4.9/5 RATING | 12K+ VERIFIED REVIEWS</span>
            </div>
        </header>

        <section class="max-w-6xl mx-auto px-6 py-20 grid md:grid-cols-2 lg:grid-cols-3 gap-8">
            <div class="matrix-card" onclick="startForm('Roofing')"><img src="./WA_1776549716792.jpeg"><div class="p-6"><h4 class="font-black text-blue-900 text-xs mb-2">ROOFING SYSTEMS</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Lifetime architectural shingles and heavy-duty metal roofing.</p></div></div>
            <div class="matrix-card" onclick="startForm('Windows')"><img src="./WA_1776549555727.jpeg"><div class="p-6"><h4 class="font-black text-blue-900 text-xs mb-2">ENERGY WINDOWS</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">High-efficiency vinyl and wood replacements with thermal sealing.</p></div></div>
            <div class="matrix-card" onclick="startForm('Solar')"><img src="./WA_1776549781247.jpeg"><div class="p-6"><h4 class="font-black text-blue-900 text-xs mb-2">SOLAR POWER</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Tier-1 solar panels and home energy management systems.</p></div></div>
        </section>
    </section>

    <section id="servicesPage" class="page-section">
        <div class="max-w-6xl mx-auto px-6 py-20">
            <h2 class="text-3xl font-black italic text-center uppercase mb-12">Our <span class="text-blue-600">Solutions</span></h2>
            <div class="grid md:grid-cols-2 gap-12">
                <div class="p-8 bg-white border rounded-3xl">
                    <h3 class="font-black text-xl mb-4">Interior Remodeling</h3>
                    <ul class="text-[11px] font-black text-slate-500 space-y-3 uppercase">
                        <li>● Custom Kitchen Cabinetry & Islands</li>
                        <li>● Luxury Bathroom Tub-to-Shower Conversion</li>
                        <li>● Modern Lighting & Flooring Integration</li>
                    </ul>
                </div>
                <div class="p-8 bg-white border rounded-3xl">
                    <h3 class="font-black text-xl mb-4">Exterior Protection</h3>
                    <ul class="text-[11px] font-black text-slate-500 space-y-3 uppercase">
                        <li>● Fiber-Cement & Vinyl Siding</li>
                        <li>● Insulated Custom Entry Doors</li>
                        <li>● High-Durability Decking & Patios</li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <section id="formPage" class="page-section bg-slate-100 py-16 px-6 min-h-screen">
        <div class="max-w-xl mx-auto glass-card p-8 md:p-12" id="formContainer">
            <form id="proMatrixForm">
                <div class="form-step active" id="s1">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-2">Project Type</label>
                    <select id="mainService" class="input-pro mb-4" onchange="loadQualifiers()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                    </select>
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-2">Are You the Homeowner?</label>
                    <select id="isOwner" class="input-pro mb-6" required>
                        <option value="Yes">Yes, I am the Legal Owner</option>
                        <option value="No">No, I am a Tenant</option>
                    </select>
                    <button type="button" onclick="nextStep('s2')" class="btn-action">Continue</button>
                </div>

                <div class="form-step" id="s2">
                    <div id="dynamicQualifiers"></div>
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-2 mt-4">Estimated Credit Score</label>
                    <select id="creditScore" class="input-pro mb-6" required>
                        <option value="Excellent (720+)">Excellent (720+)</option>
                        <option value="Good (660-719)">Good (660-719)</option>
                        <option value="Fair (600-659)">Fair (600-659)</option>
                        <option value="Poor (Below 600)">Poor (Below 600)</option>
                    </select>
                    <button type="button" onclick="nextStep('s3')" class="btn-action">Final Step</button>
                </div>

                <div class="form-step" id="s3">
                    <input type="text" id="cName" placeholder="Full Legal Name" class="input-pro mb-3" required>
                    <input type="email" id="cEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="text" id="cAddress" placeholder="Site Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-4">
                        <input type="text" id="cZip" placeholder="Zip" class="input-pro" required>
                        <input type="tel" id="cPhone" placeholder="Mobile #" class="input-pro" required>
                    </div>
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-2">Preferred Appointment</label>
                    <div class="grid grid-cols-2 gap-3 mb-6">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="10am-1pm">10AM - 1PM</option>
                            <option value="1pm-4pm">1PM - 4PM</option>
                            <option value="4pm-7pm">4PM - 7PM</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Authorize Dispatch</button>
                </div>
            </form>

            <div id="receiptBox" class="hidden text-center">
                <div class="text-5xl mb-4">✅</div>
                <h2 class="text-2xl font-black text-blue-900 uppercase italic">Appointment Authorized</h2>
                <div class="mt-8 p-6 bg-slate-50 border-2 border-dashed rounded-3xl text-left">
                    <p class="text-[9px] font-black text-slate-400 uppercase">Confirmation Receipt</p>
                    <div class="mt-4 space-y-4 text-[11px] font-black uppercase">
                        <p>Project: <span id="r-service" class="text-blue-600"></span></p>
                        <p>Customer: <span id="r-name"></span></p>
                        <p>Schedule: <span id="r-date" class="text-emerald-600"></span></p>
                        <p>Site: <span id="r-addr"></span></p>
                    </div>
                </div>
                <p class="mt-6 text-[9px] font-bold text-slate-400 uppercase italic">A verification specialist will call you shortly.</p>
                <button onclick="location.reload()" class="mt-8 text-blue-600 font-black text-xs">Home</button>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-4 mb-6"><h3 class="font-black">ADMIN LEADS HUB</h3><button onclick="closeAdmin()" class="text-red-500 font-black">EXIT</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="PIN"><button onclick="unlock()" class="btn-action max-w-[200px]">Unlock</button></div>
        <div id="leadsList" class="hidden space-y-4 pb-20"></div>
    </div>

    <footer class="bg-white border-t py-12 px-6 text-center">
        <h4 class="font-black text-blue-900 uppercase text-xs mb-4 italic">U.S. Home Improvement LLC</h4>
        <p class="text-[9px] text-slate-400 uppercase max-w-lg mx-auto leading-loose">
            702 Main Street, Woodland, CA 95695. Authorized National Dispatch Hub. <br>
            Privacy Policy: All site data is encrypted. We do not sell consumer information.
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

        // 5-TAP SECURITY
        let taps = 0, tapT;
        function handleTap() { taps++; clearTimeout(tapT); if(taps>=5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } tapT=setTimeout(()=>taps=0,2000); }

        // NAVIGATION
        function showPage(id) {
            document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo(0,0);
        }

        function startForm(service) {
            document.getElementById('mainService').value = service;
            loadQualifiers();
            showPage('formPage');
        }

        function nextStep(id) {
            document.querySelectorAll('.form-step').forEach(s=>s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        // QUALIFIERS ENGINE
        function loadQualifiers() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicQualifiers');
            const questions = {
                'Windows': [{l:'Number of Windows', o:['1-5','6-10','11-20','21+']},{l:'Frame Material', o:['Vinyl','Wood','Fiberglass']}],
                'Roofing': [{l:'Any Active Leaks?', o:['No','Small Leak','Major Leak']},{l:'Roof Age', o:['1-10 years','11-20 years','20+ years']}],
                'Solar': [{l:'Monthly Power Bill', o:['$50-150','$151-300','$301+']},{l:'Roof Direction', o:['South Facing','East/West','North/Other']}]
            };
            const current = questions[s] || [{l:'Project Timeline', o:['Immediate','1-3 Months','Just Estimating']}];
            container.innerHTML = current.map((q, i) => `
                <label class="text-[10px] font-black text-blue-500 uppercase block mb-2 mt-4">${q.l}</label>
                <select id="q${i}" class="input-pro mb-2">${q.o.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>
            `).join('');
        }
        loadQualifiers();

        // SUBMISSION
        document.getElementById('proMatrixForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const service = document.getElementById('mainService').value;
            const name = document.getElementById('cName').value;
            const addr = document.getElementById('cAddress').value;
            const appt = `${document.getElementById('appDate').value} (${document.getElementById('appSlot').value})`;

            const data = {
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
                document.getElementById('proMatrixForm').classList.add('hidden');
                document.getElementById('receiptBox').classList.remove('hidden');
                document.getElementById('r-service').innerText = service;
                document.getElementById('r-name').innerText = name;
                document.getElementById('r-date').innerText = appt;
                document.getElementById('r-addr').innerText = addr;
            });
        });

        // ADMIN FUNCTIONS
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value==="786"){ document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); syncLeads(); } }
        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="p-6 border rounded-3xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] absolute top-4 right-4 uppercase">${leads[k].service}</span>
                        <h4 class="text-xl font-black italic text-blue-900 mb-2">${leads[k].name}</h4>
                        <div class="grid grid-cols-2 gap-4">
                            <p>📧 ${leads[k].email}</p>
                            <p>📞 ${leads[k].phone}</p>
                            <p>📍 ${leads[k].address} (${leads[k].zip})</p>
                            <p>💳 Credit: ${leads[k].credit}</p>
                            <p>🛠 Spec: ${leads[k].spec}</p>
                            <p class="text-emerald-600 col-span-2">📅 Appt: ${leads[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black w-full border-t pt-4">DELETE LEAD</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Leads Available';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }

        // FAKE NOTIFS
        const notifs = ["Sarah from CA booked Roofing!", "David from TX authorized Solar.", "New Windows lead in FL!", "Contractor dispatched to NV.", "Kitchen survey booked in AZ."];
        setInterval(() => {
            const toast = document.getElementById('notification-toast');
            document.getElementById('notif-text').innerText = "⚡ " + notifs[Math.floor(Math.random()*notifs.length)];
            toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 5000);
        }, 15000);
    </script>
</body>
</html>
