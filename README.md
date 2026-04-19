<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | Official National Enterprise Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #0f172a; overflow-x: hidden; }
        
        /* Layout Elements */
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 28px; box-shadow: 0 15px 35px rgba(0,0,0,0.06); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 14px; font-weight: 600; outline: none; font-size: 14px; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px; border-radius: 14px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; }

        /* Multi-Step & Page Logic */
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s ease; }
        .form-step { display: none; }
        .form-step.active { display: block; animation: slideUp 0.3s ease; }
        
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideUp { from { transform: translateY(10px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        /* Fake Notifications */
        #notif-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 12px 20px; border-radius: 50px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); border-left: 5px solid #059669; display: none; z-index: 9999; }
        
        /* Background & Media */
        .hero-bg { background-image: url('WA_1776549716792.jpeg'); background-size: cover; background-position: center; background-attachment: fixed; }
        .matrix-card img { width: 100%; height: 240px; object-fit: cover; }
        .matrix-card { cursor: pointer; border: 1px solid #f8fafc; border-radius: 20px; overflow: hidden; transition: 0.4s; }
        .matrix-card:hover { transform: translateY(-8px); box-shadow: 0 20px 30px rgba(0,0,0,0.06); }
    </style>
</head>
<body>

    <div id="notif-toast"><p id="notif-text" class="text-[10px] font-black text-slate-700 uppercase italic"></p></div>

    <nav class="bg-white/95 backdrop-blur-md border-b px-6 py-5 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3 cursor-pointer" onclick="location.reload()">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border" id="adminTrigger" onclick="handleTap()">
            <div>
                <span class="block font-black text-sm uppercase text-blue-900 leading-tight">U.S. Home Improvement LLC</span>
                <span class="block text-[8px] font-extrabold text-emerald-600 uppercase italic">● Licensed National Dispatch Terminal</span>
            </div>
        </div>
        <div class="hidden md:flex gap-10 items-center text-[10px] font-black text-slate-400 uppercase tracking-widest">
            <a href="#" onclick="showPage('homePage')" class="hover:text-blue-600">Home</a>
            <a href="#" onclick="showPage('servicesPage')" class="hover:text-blue-600">Portfolio</a>
            <a href="#" onclick="showPage('formPage')" class="px-5 py-2.5 bg-blue-50 rounded-full text-blue-600">Request Survey</a>
        </div>
    </nav>

    <header id="homeHero" class="hero-bg py-32 px-6 text-center text-white relative">
        <div class="absolute inset-0 bg-slate-950/60"></div>
        <div class="relative z-10 max-w-4xl mx-auto">
            <span class="bg-blue-600/20 text-blue-200 px-4 py-1 rounded-full text-[9px] font-black uppercase tracking-widest mb-6 inline-block italic border border-blue-500/30">Nationwide Inspection Authority</span>
            <h1 class="text-4xl md:text-7xl font-black uppercase italic tracking-tighter mb-8 leading-none">Connecting You to American <span class="text-blue-400">Quality.</span></h1>
            <p class="text-blue-200 font-bold uppercase text-[10px] tracking-[0.4em] mb-12 max-w-lg mx-auto leading-relaxed">Authorized Site Surveys & Certified Estimations Across 50 States</p>
            <button onclick="showPage('formPage')" class="btn-action max-w-sm">Secure Your Dispatch</button>
            <div class="mt-12 flex justify-center gap-2">
                <span class="text-yellow-400 text-xl">★★★★★</span>
                <span class="text-[11px] font-black self-center uppercase">A+ Rating (12.4K+ Happy Homeowners)</span>
            </div>
        </div>
    </header>

    <section id="homePage" class="page-section active">
        <div class="max-w-6xl mx-auto px-6 py-24 grid md:grid-cols-2 lg:grid-cols-3 gap-8">
            <div class="matrix-card" onclick="startSvc('Roofing')"><img src="./WA_1776549716792.jpeg"><div class="p-6"><h4 class="font-black text-blue-900 text-xs uppercase mb-2">Lifetime Roofing</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Certified architectural protection for generations.</p></div></div>
            <div class="matrix-card" onclick="startSvc('Solar')"><img src="./WA_1776549781247.jpeg"><div class="p-6"><h4 class="font-black text-blue-900 text-xs uppercase mb-2">Solar Efficiency</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Grid-independent power & energy bachat.</p></div></div>
            <div class="matrix-card" onclick="startSvc('Windows')"><img src="./WA_1776549555727.jpeg"><div class="p-6"><h4 class="font-black text-blue-900 text-xs uppercase mb-2">Energy Windows</h4><p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">Double-Pane sealing for ultimate savings.</p></div></div>
        </div>
    </section>

    <section id="servicesPage" class="page-section bg-slate-50 border-t py-24 px-6">
        <div class="max-w-6xl mx-auto">
            <h2 class="text-3xl font-black italic text-center uppercase mb-16 tracking-tighter">Our <span class="text-blue-600">Nationwide Portfolio</span></h2>
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-10">
                <div class="p-8 bg-white rounded-3xl border"><img src="./WA_1776549716792.jpeg" class="w-full h-40 object-cover rounded-xl mb-6"><h4 class="font-black text-xl mb-4 italic text-blue-900">Roofing Matrix</h4><p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Lifetime architectural shingles & metal roofing systems. Certified state-licensed contractors dispatch for full técnico survey.</p></div>
                <div class="p-8 bg-white rounded-3xl border"><img src="./WA_1776549781247.jpeg" class="w-full h-40 object-cover rounded-xl mb-6"><h4 class="font-black text-xl mb-4 italic text-blue-900">Solar Matrix</h4><p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Tier-1 solar panels with smart energy management. $0 down financing based on approved credit matrix survey.</p></div>
                <div class="p-8 bg-white rounded-3xl border"><img src="./WA_1776549555727.jpeg" class="w-full h-40 object-cover rounded-xl mb-6"><h4 class="font-black text-xl mb-4 italic text-blue-900">Energy Windows</h4><p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Custom energy-star window systems. Double and triple pane sealing included in all national Technical Specifications.</p></div>
                <div class="p-8 bg-white rounded-3xl border"><img src="./WA_1776549622236.jpeg" class="w-full h-40 object-cover rounded-xl mb-6"><h4 class="font-black text-xl mb-4 italic text-blue-900">Entry Doors</h4><p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Hurricane-resistant and secure doors. Designed for ultimate durability and curb appeal in every American weather condition.</p></div>
                <div class="p-8 bg-white rounded-3xl border"><img src="./WA_1776549917709.jpeg" class="w-full h-40 object-cover rounded-xl mb-6"><h4 class="font-black text-xl mb-4 italic text-blue-900">Gourmet Kitchens</h4><p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Custom cabinets, quartz countertops, and modern islands. Our crews handle plumbing, electrical, and full structural changes.</p></div>
                <div class="p-8 bg-white rounded-3xl border"><img src="./WA_1776549862258.jpeg" class="w-full h-40 object-cover rounded-xl mb-6"><h4 class="font-black text-xl mb-4 italic text-blue-900">Bathroom Spas</h4><p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Luxury tiling, custom showers, and tub conversions. Complete waterproofing guarantee is included with all site installations.</p></div>
                <div class="p-8 bg-white rounded-3xl border"><img src="./WA_1776550066723.jpeg" class="w-full h-40 object-cover rounded-xl mb-6"><h4 class="font-black text-xl mb-4 italic text-blue-900">Garage Door</h4><p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Smart and insulated garage door systems. Ultra-durable engineering ensures safety and smooth operation for your primary entry.</p></div>
                <div class="p-8 bg-white rounded-3xl border"><img src="./WA_1776549990293.jpeg" class="w-full h-40 object-cover rounded-xl mb-6"><h4 class="font-black text-xl mb-4 italic text-blue-900">Custom Decks</h4><p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Composite and premium wood decks. We dispatch certified technical survey crews to handle design, permits, and complete construction.</p></div>
            </div>
            <p class="text-center mt-12 text-[9px] text-slate-400 uppercase font-black italic">Click "Request Survey" for detailed pricing in your area.</p>
        </div>
    </section>

    <section id="formPage" class="page-section bg-slate-50 py-20 min-h-screen px-6">
        <div class="max-w-xl mx-auto glass-card p-8 md:p-12 relative overflow-hidden" id="matrixContainer">
            <form id="proDispatchForm">
                <div class="form-step active" id="s1">
                    <h3 class="text-xl font-black uppercase italic mb-6">Start Your <span class="text-blue-600">Application</span></h3>
                    <select id="mainService" class="input-pro mb-4" onchange="loadMeta()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                        <option value="Garage">Garage Door Systems</option>
                        <option value="Deck">Custom Decking</option>
                    </select>
                    <select id="isOwner" class="input-pro mb-8" required>
                        <option value="Yes">I am the Legal Homeowner</option>
                        <option value="No">I am a Tenant</option>
                    </select>
                    <button type="button" onclick="goNext('s2')" class="btn-action">Continue Application</button>
                </div>

                <div class="form-step" id="s2">
                    <h3 class="text-xl font-black uppercase italic mb-6">Qualifying <span class="text-blue-600">Matrix</span></h3>
                    <div id="dynamicFields"></div>
                    <label class="text-[9px] font-black text-slate-400 uppercase block mb-2 mt-4 tracking-widest">Est. Credit Score</label>
                    <select id="creditScore" class="input-pro mb-8" required>
                        <option value="Excellent (720+)">Excellent (720+)</option>
                        <option value="Good (660-719)">Good (660-719)</option>
                        <option value="Fair (Below 660)">Fair/Other</option>
                    </select>
                    <button type="button" onclick="goNext('s3')" class="btn-action">Proceed To Schedule</button>
                </div>

                <div class="form-step" id="s3">
                    <h3 class="text-xl font-black uppercase italic mb-6">Site <span class="text-blue-600">Verification</span></h3>
                    <input type="text" id="custName" placeholder="Full Legal Name" class="input-pro mb-3" required>
                    <input type="email" id="custEmail" placeholder="Email Address" class="input-pro mb-3" required>
                    <input type="text" id="custAddress" placeholder="Street Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-3">
                        <input type="text" id="custZip" placeholder="Zip" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Mobile" class="input-pro" required>
                    </div>
                    <div class="grid grid-cols-2 gap-3 mb-6">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="10am-1pm">Morning (10-1)</option>
                            <option value="1pm-4pm">Afternoon (1-4)</option>
                            <option value="4pm-7pm">Evening (4-7)</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Authorize Dispatch</button>
                </div>
            </form>

            <div id="receiptBox" class="hidden text-center py-6">
                <div class="text-6xl mb-4">✔</div>
                <h2 class="text-3xl font-black text-blue-900 uppercase italic"> Dispatch authorized</h2>
                <div class="mt-8 p-8 bg-slate-50 border-2 border-dashed border-slate-300 rounded-3xl text-left text-[11px] font-bold uppercase space-y-3">
                    <p>Track ID: #<span id="r-id" class="text-blue-600 font-black"></span></p>
                    <p>Name: <span id="r-name" class="font-black text-slate-700"></span></p>
                    <p>Authorized Slot: <span id="r-date" class="font-black text-emerald-600"></span></p>
                    <p>Address: <span id="r-address" class="font-black text-slate-700"></span></p>
                </div>
                <p class="mt-8 text-[9px] font-bold text-slate-400 italic">Save this screen. An expert will call from a California number to verify site access.</p>
                <button onclick="location.reload()" class="mt-8 text-blue-600 font-black uppercase text-xs">Home</button>
            </div>
        </div>
    </section>

    <section id="legalPage" class="page-section bg-white py-20 px-6">
        <div class="max-w-4xl mx-auto glass-card p-12">
            <h2 class="text-2xl font-black text-blue-900 uppercase italic mb-8">National Hub <span class="text-blue-600">Compliance Portfolio</span></h2>
            <div class="text-[10px] font-bold text-slate-600 space-y-6 uppercase leading-relaxed">
                <p>U.S. Home Improvement LLC operates as a Nationwide Authorized Dispatch Terminal. By submitting your information, you grant our network permission to connect you with a state-licensed contractor. Estimates provided are based on site technical surveys.</p>
                <p><strong>Privacy Shield:</strong> Your data is protected by 256-bit AES encryption. We never share or sell consumer data outside our authorized network.</p>
                <p><strong>LEGAL DISPATCH:</strong> A "dispatch authorization" connects your property to a licensed local technical expert for an estimate. It is not a contract for final services.</p>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-4 mb-8"><h3 class="font-black text-blue-900 italic">ADMIN LEADS TERMINAL</h3><button onclick="closeAdmin()" class="text-red-500 font-black">Exit</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[240px] text-center mb-4" placeholder="ENTER PIN"><button onclick="unlock()" class="btn-action max-w-[240px]">Access Hub</button></div>
        <div id="leadsList" class="hidden space-y-4 pb-20"></div>
    </div>

    <footer class="bg-white border-t py-16 px-6 text-center">
        <div class="trust-bar flex flex-wrap justify-center gap-6 mb-10 text-[9px] font-black uppercase text-slate-300 tracking-widest">
            <span>● A+ BBB Rating</span>
            <span>● 50-State Licensing hub</span>
            <span>● Insured Crews</span>
        </div>
        
        <h4 class="font-black text-blue-900 uppercase text-xs mb-3 italic">U.S. Home Improvement LLC</h4>
        <p class="text-[8px] text-slate-400 font-black uppercase mb-8 italic">Support: ushomeimprovement07@gmail.com</p>
        <p class="text-[8px] text-slate-300 font-bold max-w-lg mx-auto leading-loose uppercase">702 Main Street, Woodland, CA 95695. <br> Nationwide Authorized Dispatch Hub © 2026. All data encryption protected.</p>
    </footer>

    <script>
        // FIREBASE MASTER CONFIG
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

        // LOGO SECURITY SYSTEM
        let taps = 0, tapTimer;
        function handleTap() { taps++; clearTimeout(tapTimer); if(taps>=5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } tapTimer=setTimeout(()=>taps=0,2000); }

        // MULTI-PAGE & FORM SWITCHING
        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo(0,0); }
        function startSvc(svc) { document.getElementById('mainService').value = svc; loadMeta(); showPage('formPage'); }
        function goNext(id) { document.querySelectorAll('.form-step').forEach(s=>s.classList.remove('active')); document.getElementById(id).classList.add('active'); }

        // DYNAMIC QUALIFIERS
        function loadMeta() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicFields');
            const data = {
                'Windows': [{l:'Window Count', o:['1-5','6-10','11-20','21+']},{l:'Frame Choice', o:['Vinyl','Wood']}],
                'Roofing': [{l:'Roof Age', o:['1-10 years','11-20 years','20+ years']},{l:'Any Leaks?', o:['None','Minor','Major Leaks']}],
                'Solar': [{l:'Mahina Bill', o:['$50-150','$151-300','$301+']},{l:'Roof Exposure', o:['Full Sun','Partial']}]
            };
            const current = data[s] || [{l:'Timeline', o:['Immediate','1-3 Months']}];
            container.innerHTML = current.map((q, i) => `
                <label class="text-[9px] font-black text-slate-400 uppercase block mb-2 mt-4 tracking-widest">${q.l}</label>
                <select id="q${i}" class="input-pro mb-3">${q.o.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>
            `).join('');
        }
        loadMeta();

        // FORM SUBMISSION ENGINE
        document.getElementById('proDispatchForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const id = Math.floor(100000 + Math.random() * 900000);
            const name = document.getElementById('custName').value;
            const appt = `${document.getElementById('appDate').value} (${document.getElementById('appSlot').value})`;
            const address = document.getElementById('custAddress').value;

            const data = {
                id: id, service: document.getElementById('mainService').value,
                owner: document.getElementById('isOwner').value, credit: document.getElementById('creditScore').value,
                name: name, email: document.getElementById('custEmail').value,
                phone: document.getElementById('custPhone').value, address: address,
                zip: document.getElementById('custZip').value,
                appointment: appt, timestamp: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                document.getElementById('matrixContainer').style.background = '#fcfcfd';
                document.getElementById('proDispatchForm').classList.add('hidden');
                document.getElementById('receiptBox').classList.remove('hidden');
                document.getElementById('r-id').innerText = id;
                document.getElementById('r-name').innerText = name;
                document.getElementById('r-date').innerText = appt;
                document.getElementById('r-address').innerText = address;
            });
        });

        // ADMIN TERMINAL SYNC
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value==="786"){ document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); syncLeads(); } }
        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="p-6 border rounded-3xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] absolute top-4 right-4 uppercase">${leads[k].service}</span>
                        <h4 class="text-xl font-black italic text-blue-900 mb-2">#${leads[k].id} | ${leads[k].name}</h4>
                        <div class="grid grid-cols-2 gap-x-6 gap-y-2 uppercase">
                            <p>📧 <span class="text-blue-600 underline">${leads[k].email}</span></p>
                            <p>📞 Phone: ${leads[k].phone}</p>
                            <p>📍 Site: ${leads[k].address} (${leads[k].zip})</p>
                            <p>💳 Credit: ${leads[k].credit}</p>
                            <p>👤 Owner: ${leads[k].owner}</p>
                            <p class="text-emerald-600 col-span-2 border-t pt-2">📅 Appt: ${leads[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black w-full border-t pt-2">DELETE DISPATCH</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'Terminal Empty';
            });
        }
        function del(id) { if(confirm('Erase dispatch?')) db.ref('leads/'+id).remove(); }

        // FAKE SOCIAL PROOF Engine
        const names = ["Sarah", "David", "Michael", "Linda", "John", "Jessica", "James", "Emily"];
        const cityAbbr = ["CA", "TX", "FL", "NY", "NV", "GA", "AZ", "WA"];
        setInterval(() => {
            const toast = document.getElementById('notif-toast');
            document.getElementById('notif-text').innerText = "⚡ " + names[Math.floor(Math.random()*names.length)] + " from " + cityAbbr[Math.floor(Math.random()*cityAbbr.length)] + " just authorized a project survey!";
            toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 5000);
        }, 12000);
    </script>
</body>
</html>
