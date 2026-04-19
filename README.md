<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Authorized Matrix</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; --gold: #f59e0b; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fdfdfd; color: var(--primary); }
        
        .hero-section { background: linear-gradient(rgba(15, 23, 42, 0.9), rgba(15, 23, 42, 0.9)), url('https://images.unsplash.com/photo-1513694203232-719a280e022f?q=80&w=2069&auto=format&fit=crop'); background-size: cover; background-position: center; color: white; padding: 100px 20px; text-align: center; }
        
        .glass-form { background: white; border-radius: 30px; border: 1px solid #e2e8f0; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.1); padding: 40px; margin-top: -60px; position: relative; z-index: 10; }
        
        .step-content { display: none; }
        .step-content.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .input-premium { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 15px; font-weight: 600; margin-bottom: 20px; outline: none; transition: 0.3s; background: #f8fafc; }
        .input-premium:focus { border-color: var(--accent); background: white; box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }
        
        .btn-premium { background: var(--accent); color: white; padding: 20px; border-radius: 15px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; }
        .btn-premium:hover { background: #1d4ed8; transform: translateY(-2px); box-shadow: 0 10px 15px -3px rgba(37, 99, 235, 0.3); }

        .service-card { border-radius: 20px; overflow: hidden; border: 1px solid #f1f5f9; background: white; transition: 0.3s; }
        .service-card:hover { transform: translateY(-5px); box-shadow: 0 20px 25px -5px rgba(0,0,0,0.05); }
        .service-card img { width: 100%; height: 160px; object-fit: cover; }
        .service-card h4 { font-weight: 800; text-transform: uppercase; font-size: 12px; padding: 15px; color: var(--primary); }

        .trust-badge { display: flex; align-items: center; gap: 10px; background: rgba(255,255,255,0.1); padding: 8px 16px; border-radius: 50px; font-size: 10px; font-weight: 700; border: 1px solid rgba(255,255,255,0.2); }
    </style>
</head>
<body>

    <nav class="bg-white border-b px-8 py-5 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-4">
            <img src="./WA_1776550450872.jpeg" class="h-12 w-12 rounded-xl shadow-md border">
            <div>
                <span onclick="toggleAdmin()" class="block font-black text-sm uppercase tracking-tighter cursor-pointer">U.S. Home Improvement</span>
                <span class="block text-[9px] font-bold text-emerald-600 uppercase">● Licensed National Enterprise</span>
            </div>
        </div>
        <div class="hidden md:flex gap-6 text-[11px] font-black uppercase text-slate-400">
            <span>California HQ</span>
            <span>Est. 2026</span>
            <span class="text-blue-600">Nationwide Coverage</span>
        </div>
    </nav>

    <header class="hero-section">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-center mb-6"><div class="trust-badge uppercase">National Matrix Hub • Verified Network</div></div>
            <h1 class="text-4xl md:text-6xl font-black uppercase italic tracking-tighter mb-6">Upgrade Your Home <br> With Zero Hassle</h1>
            <p class="text-slate-300 font-medium text-lg max-w-2xl mx-auto">Authorized national network connecting you with licensed professionals for premium roofing, solar, and remodeling.</p>
        </div>
    </header>

    <main class="max-w-xl mx-auto px-6 mb-24">
        <div class="glass-form">
            <form id="proLeadForm">
                <div class="step-content active" id="step1">
                    <h3 class="text-xl font-extrabold mb-6 uppercase italic text-blue-600">01. Choose Service</h3>
                    <select id="mainService" class="input-premium" onchange="updateDynamicInputs()" required>
                        <option value="Roofing">Roofing Solutions</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Doors">Entry & Patio Doors</option>
                        <option value="Garage">Garage System</option>
                        <option value="Deck">Custom Decking</option>
                        <option value="Kitchen">Kitchen Remodel</option>
                        <option value="Bathroom">Bathroom Remodel</option>
                        <option value="Siding">Exterior Siding</option>
                    </select>
                    <select id="isOwner" class="input-premium" required>
                        <option value="">Are you the home owner?</option>
                        <option value="Yes">Yes, I am the owner</option>
                        <option value="No">No, I am a tenant</option>
                    </select>
                    <button type="button" onclick="nextStep('step2')" class="btn-premium">Continue to Qualify</button>
                </div>

                <div class="step-content" id="step2">
                    <h3 class="text-xl font-extrabold mb-6 uppercase italic text-blue-600">02. Qualification</h3>
                    <div id="dynamicInputs">
                        </div>
                    <select id="creditScore" class="input-premium" required>
                        <option value="">Estimated Credit Score?</option>
                        <option value="720+">720+ (Excellent)</option>
                        <option value="660-719">660-719 (Good)</option>
                        <option value="600-659">600-659 (Fair)</option>
                        <option value="Manual">Enter Manually...</option>
                    </select>
                    <input type="text" id="manualCredit" placeholder="If manual, enter credit score" class="input-premium hidden">
                    
                    <button type="button" onclick="nextStep('step3')" class="btn-premium">Set Appointment</button>
                </div>

                <div class="step-content" id="step3">
                    <h3 class="text-xl font-extrabold mb-6 uppercase italic text-blue-600">03. Final Authorization</h3>
                    <input type="text" id="custAddress" placeholder="Street Address" class="input-premium" required>
                    <div class="grid grid-cols-2 gap-4">
                        <input type="text" id="custZip" placeholder="Zip Code" class="input-premium" required>
                        <input type="text" id="custName" placeholder="Full Name" class="input-premium" required>
                    </div>
                    <input type="email" id="custEmail" placeholder="Email Address" class="input-premium" required>
                    <input type="tel" id="custPhone" placeholder="Direct Phone Number" class="input-premium" required>
                    
                    <div class="grid grid-cols-2 gap-4">
                        <input type="date" id="appDate" class="input-premium" required>
                        <select id="appTime" class="input-premium" required>
                            <option value="Morning (9AM-12PM)">Morning</option>
                            <option value="Afternoon (1PM-5PM)">Afternoon</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-premium">Confirm Appointment</button>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-5xl mx-auto px-8 mb-32">
        <div class="text-center mb-16">
            <h2 class="text-3xl font-black uppercase italic tracking-tighter">Enterprise Solutions</h2>
            <p class="text-slate-400 font-bold uppercase text-[10px] tracking-[0.4em] mt-2">Licensed Nationwide Specialists</p>
        </div>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
            <div class="service-card"><img src="./WA_1776549716792.jpeg"><h4>Roofing</h4></div>
            <div class="service-card"><img src="./WA_1776549781247.jpeg"><h4>Solar Panels</h4></div>
            <div class="service-card"><img src="./WA_1776549555727.jpeg"><h4>Windows</h4></div>
            <div class="service-card"><img src="./WA_1776549622236.jpeg"><h4>Doors</h4></div>
            <div class="service-card"><img src="./WA_1776549862258.jpeg"><h4>Kitchen</h4></div>
            <div class="service-card"><img src="./WA_1776549917709.jpeg"><h4>Bathroom</h4></div>
            <div class="service-card"><img src="./WA_1776550066723.jpeg"><h4>Garage</h4></div>
            <div class="service-card"><img src="./WA_1776549990293.jpeg"><h4>Deck</h4></div>
        </div>
    </section>

    <footer class="bg-slate-950 py-24 px-8 text-white">
        <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-16">
            <div>
                <h4 class="text-blue-500 font-black uppercase text-xs mb-6 tracking-widest">National Headquarters</h4>
                <p class="text-slate-400 font-bold text-sm leading-relaxed">
                    702 Main Street<br>
                    Woodland, California 95695<br>
                    United States
                </p>
                <p class="text-blue-300 mt-4 text-xs font-black lowercase">ushomeimprovement07@gmail.com</p>
            </div>
            <div>
                <h4 class="text-blue-500 font-black uppercase text-xs mb-6 tracking-widest">Our Promise</h4>
                <ul class="text-slate-400 font-bold text-xs space-y-3 uppercase">
                    <li>✓ 50-State Licensing Network</li>
                    <li>✓ Lifetime Matrix Warranty</li>
                    <li>✓ Licensed & Bonded Crews</li>
                    <li>✓ Zero-Down Financing Plans</li>
                </ul>
            </div>
            <div>
                <h4 class="text-blue-500 font-black uppercase text-xs mb-6 tracking-widest">Legal Portal</h4>
                <div class="flex flex-col gap-4 text-[10px] font-black uppercase text-slate-500">
                    <span class="hover:text-white cursor-pointer" onclick="alert('Privacy Encrypted')">Privacy Policy</span>
                    <span class="hover:text-white cursor-pointer" onclick="alert('Terms Verified')">Terms & Conditions</span>
                    <span class="mt-4 text-slate-700">© 2026 U.S. Home Improvement Enterprise</span>
                </div>
            </div>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-6 mb-8">
            <h2 class="text-2xl font-black uppercase italic">Leads Control Terminal</h2>
            <button onclick="toggleAdmin()" class="bg-red-50 text-red-600 px-6 py-2 rounded-full font-black text-xs uppercase">Exit</button>
        </div>
        <div id="authSection" class="text-center py-20">
            <p class="font-bold text-slate-400 uppercase text-xs mb-4">Enter Authorization PIN</p>
            <input type="password" id="pin" class="input-premium max-w-[240px] text-center text-2xl tracking-[10px]" placeholder="****">
            <button onclick="unlockTerminal()" class="btn-premium max-w-[240px] mt-4">Access Terminal</button>
        </div>
        <div id="leadsContainer" class="hidden space-y-6 pb-20"></div>
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

        function nextStep(id) {
            document.querySelectorAll('.step-content').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function updateDynamicInputs() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicInputs');
            let h = '';

            if(s === 'Windows') {
                h = `<select id="q1" class="input-premium" onchange="toggleManual('q1','m1')">
                        <option value="">How many windows?</option>
                        <option value="3-5">3-5 Windows</option>
                        <option value="6-10">6-10 Windows</option>
                        <option value="Manual">Enter Manual Amount...</option>
                    </select>
                    <input type="text" id="m1" placeholder="Type exact amount of windows" class="input-premium hidden">
                    <select id="q2" class="input-premium"><option value="">Type of windows?</option><option value="Vinyl">Premium Vinyl</option><option value="Wood">Classic Wood</option></select>`;
            } else if(s === 'Roofing') {
                h = `<select id="q1" class="input-premium"><option value="">Current Roof Type?</option><option value="Shingles">Asphalt Shingles</option><option value="Metal">Metal Sheet</option></select>`;
            } else {
                h = `<p class="text-xs font-bold text-blue-600 mb-6 uppercase italic">Standard nationwide qualifying applied for ${s}.</p>`;
            }
            container.innerHTML = h;
        }
        updateDynamicInputs();

        function toggleManual(selectId, manualId) {
            const s = document.getElementById(selectId);
            const m = document.getElementById(manualId);
            if(s.value === 'Manual') m.classList.remove('hidden'); else m.classList.add('hidden');
        }

        document.getElementById('creditScore').addEventListener('change', function() {
            const m = document.getElementById('manualCredit');
            if(this.value === 'Manual') m.classList.remove('hidden'); else m.classList.add('hidden');
        });

        document.getElementById('proLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('mainService').value,
                isOwner: document.getElementById('isOwner').value,
                credit: document.getElementById('creditScore').value === 'Manual' ? document.getElementById('manualCredit').value : document.getElementById('creditScore').value,
                details: (document.getElementById('q1')?.value === 'Manual' ? document.getElementById('m1').value : document.getElementById('q1')?.value) || 'Standard',
                name: document.getElementById('custName').value,
                address: document.getElementById('custAddress').value,
                zip: document.getElementById('custZip').value,
                email: document.getElementById('custEmail').value,
                phone: document.getElementById('custPhone').value,
                appointment: `${document.getElementById('appDate').value} (${document.getElementById('appTime').value})`,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { alert("Authorization Successful! An agent will call you."); location.reload(); });
        });

        function toggleAdmin() { document.getElementById('adminPanel').classList.toggle('hidden'); }
        function unlockTerminal() {
            if(document.getElementById('pin').value === "786") {
                document.getElementById('authSection').classList.add('hidden');
                document.getElementById('leadsContainer').classList.remove('hidden');
                syncLeads();
            }
        }

        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-8 border rounded-3xl bg-slate-50 relative mb-6 shadow-sm border-slate-200">
                        <span class="bg-blue-600 text-white px-4 py-1.5 rounded-full text-[10px] font-black absolute top-6 right-8 uppercase tracking-widest">${data[k].service}</span>
                        <h4 class="text-2xl font-black mb-1 uppercase italic">${data[k].name}</h4>
                        <p class="text-slate-500 font-bold mb-6">📍 ${data[k].address} (${data[k].zip})</p>
                        <div class="grid grid-cols-2 gap-8 py-6 border-t border-slate-200">
                            <div>
                                <p class="text-[9px] font-black text-slate-400 uppercase mb-2">Contact Details</p>
                                <p class="text-sm font-bold">📞 ${data[k].phone}</p>
                                <p class="text-sm font-bold">✉️ ${data[k].email}</p>
                            </div>
                            <div>
                                <p class="text-[9px] font-black text-slate-400 uppercase mb-2">Qualifying Matrix</p>
                                <p class="text-sm font-bold uppercase">Owner: ${data[k].isOwner} | Credit: ${data[k].credit}</p>
                                <p class="text-sm font-bold uppercase text-blue-600">Specs: ${data[k].details}</p>
                            </div>
                        </div>
                        <div class="bg-blue-50 p-4 rounded-xl flex justify-between items-center mt-2">
                            <span class="text-[10px] font-black uppercase text-blue-800 tracking-tighter">📅 Appointment: ${data[k].appointment}</span>
                            <button onclick="deleteLead('${k}')" class="text-red-500 font-black text-[10px] uppercase">Remove</button>
                        </div>
                    </div>`;
                }
                document.getElementById('leadsContainer').innerHTML = h || '<p class="text-center py-20 font-bold text-slate-300 uppercase">Terminal Clear - No Leads</p>';
            });
        }
        function deleteLead(id) { if(confirm('Permanently Delete Lead?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
