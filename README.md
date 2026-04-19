<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | Authorized National Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; --gold: #f59e0b; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #0f172a; }
        
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 32px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.08); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; font-size: 14px; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); outline: none; background: #f8fafc; }
        
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 16px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; transition: 0.3s; }
        .btn-action:hover { transform: scale(1.02); box-shadow: 0 10px 20px rgba(37, 99, 235, 0.2); }

        .matrix-card { background: white; border-radius: 28px; overflow: hidden; border: 1px solid #f1f5f9; transition: 0.4s; }
        .matrix-card:hover { transform: translateY(-10px); box-shadow: 0 20px 30px rgba(0,0,0,0.05); }
        .matrix-card img { width: 100%; height: 240px; object-fit: cover; }
        
        .step-form { display: none; }
        .step-form.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        #notification-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 15px 25px; border-radius: 50px; box-shadow: 0 15px 35px rgba(0,0,0,0.1); border-left: 6px solid #059669; display: none; z-index: 9999; animation: slideIn 0.5s ease; }
        @keyframes slideIn { from { transform: translateX(-100%); } to { transform: translateX(0); } }

        .legal-link { cursor: pointer; color: #64748b; font-size: 10px; font-weight: 800; text-transform: uppercase; }
        .legal-link:hover { color: var(--accent); }
    </style>
</head>
<body>

    <div id="notification-toast"><p id="notif-text" class="text-[11px] font-bold text-slate-700"></p></div>

    <nav class="bg-white/80 backdrop-blur-md border-b px-6 py-5 flex justify-between items-center sticky top-0 z-[1000]">
        <div class="flex items-center gap-3" id="adminTrigger" onclick="handleTap()">
            <img src="./WA_1776550450872.jpeg" class="h-10 w-10 rounded-xl shadow-md border">
            <div>
                <span class="block font-black text-sm uppercase tracking-tighter text-blue-900">U.S. Home Improvement LLC</span>
                <span class="block text-[9px] font-extrabold text-emerald-600 uppercase italic">● Verified National Contractor Network</span>
            </div>
        </div>
        <div class="hidden lg:block">
            <span class="text-[10px] font-black text-slate-400 uppercase italic">Headquarters: Woodland, CA 95695</span>
        </div>
    </nav>

    <header class="py-20 px-6 text-center bg-gradient-to-b from-slate-50 to-white">
        <div class="inline-flex items-center gap-2 bg-blue-50 text-blue-700 px-4 py-1 rounded-full text-[10px] font-black uppercase mb-6">
            🛡️ $1M Liability Insured & Licensed
        </div>
        <h1 class="text-4xl md:text-6xl font-black uppercase italic tracking-tighter mb-4 text-slate-900 leading-none">
            Your Home, <span class="text-blue-600">Our Mission.</span>
        </h1>
        <p class="text-slate-500 font-bold uppercase text-[10px] tracking-[0.4em] mb-8">Authorized National Dispatch For Site Estimations</p>
        <div class="flex justify-center gap-2 mb-4">
            <span class="text-yellow-400 text-xl">★★★★★</span>
            <span class="text-[11px] font-black self-center text-slate-700 uppercase">4.9/5 RATING | 12,400+ HAPPY HOMEOWNERS</span>
        </div>
    </header>

    <main class="max-w-xl mx-auto px-6 -mt-12 mb-32 relative z-10">
        <div class="glass-card p-8 md:p-12">
            <form id="proDispatchForm">
                <div class="step-form active" id="step1">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4 tracking-widest">Select Category</label>
                    <select id="mainService" class="input-pro mb-4" onchange="loadServiceMeta()" required>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Siding">Exterior Siding</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Bathroom">Bathroom Remodeling</option>
                        <option value="Garage">Garage Door Systems</option>
                        <option value="Deck">Custom Decking</option>
                    </select>
                    <select id="isOwner" class="input-pro" required>
                        <option value="Yes">Yes, I am the Homeowner</option>
                        <option value="No">No, I am a Tenant</option>
                    </select>
                    <button type="button" onclick="goStep('step2')" class="btn-action mt-6">Continue To Options</button>
                </div>

                <div class="step-form" id="step2">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4 tracking-widest">Project Requirements</label>
                    <div id="dynamicContainer"></div>
                    <button type="button" onclick="goStep('step3')" class="btn-action">Proceed To Schedule</button>
                </div>

                <div class="step-form" id="step3">
                    <label class="text-[10px] font-black text-blue-500 uppercase block mb-4 tracking-widest">Contact & Appointment</label>
                    <input type="text" id="custName" placeholder="Full Name" class="input-pro mb-3" required>
                    <input type="text" id="custAddress" placeholder="Site Address" class="input-pro mb-3" required>
                    <div class="grid grid-cols-2 gap-3 mb-3">
                        <input type="text" id="custZip" placeholder="Zip Code" class="input-pro" required>
                        <input type="tel" id="custPhone" placeholder="Mobile Number" class="input-pro" required>
                    </div>
                    <div class="grid grid-cols-2 gap-3 mb-6">
                        <input type="date" id="appDate" class="input-pro" required>
                        <select id="appSlot" class="input-pro" required>
                            <option value="">Select Slot</option>
                            <option value="10am-1pm">Morning (10AM - 1PM)</option>
                            <option value="1pm-4pm">Afternoon (1PM - 4PM)</option>
                            <option value="4pm-7pm">Evening (4PM - 7PM)</option>
                        </select>
                    </div>
                    <button type="submit" class="btn-action">Request Verified Dispatch</button>
                    <p class="text-[8px] text-center mt-4 text-slate-400 font-bold uppercase">By clicking, you agree to our Privacy Policy & Terms.</p>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-6xl mx-auto px-6 mb-32 grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div class="matrix-card">
            <img src="./WA_1776549716792.jpeg">
            <div class="p-6">
                <h4 class="font-black text-blue-900 uppercase text-xs mb-2">Lifetime Roofing</h4>
                <p class="text-[10px] font-bold text-slate-500 leading-relaxed uppercase">High-impact shingles & metal roofing systems. 50-year warranty included on all national installs.</p>
            </div>
        </div>
        <div class="matrix-card">
            <img src="./WA_1776549555727.jpeg">
            <div class="p-6">
                <h4 class="font-black text-blue-900 uppercase text-xs mb-2">Energy-Star Windows</h4>
                <p class="text-[10px] font-bold text-slate-500 leading-relaxed uppercase">Triple-pane vinyl and wood options. Reduce your energy bills by up to 35% with our sealed technology.</p>
            </div>
        </div>
        <div class="matrix-card">
            <img src="./WA_1776549781247.jpeg">
            <div class="p-6">
                <h4 class="font-black text-blue-900 uppercase text-xs mb-2">Smart Solar Matrix</h4>
                <p class="text-[10px] font-bold text-slate-500 leading-relaxed uppercase">Tier-1 solar panels with battery backup. Take control of your power grid with $0 down financing.</p>
            </div>
        </div>
        <div class="matrix-card">
            <img src="./WA_1776549917709.jpeg">
            <div class="p-6">
                <h4 class="font-black text-blue-900 uppercase text-xs mb-2">Gourmet Kitchens</h4>
                <p class="text-[10px] font-bold text-slate-500 leading-relaxed uppercase">Custom cabinets, quartz countertops, and modern islands. Full renovation in under 14 days.</p>
            </div>
        </div>
        <div class="matrix-card">
            <img src="./WA_1776549862258.jpeg">
            <div class="p-6">
                <h4 class="font-black text-blue-900 uppercase text-xs mb-2">Bathroom Spas</h4>
                <p class="text-[10px] font-bold text-slate-500 leading-relaxed uppercase">Tub-to-shower conversions and luxury tiling. Waterproof lifetime guarantee on all wet areas.</p>
            </div>
        </div>
        <div class="matrix-card">
            <img src="./WA_1776550066723.jpeg">
            <div class="p-6">
                <h4 class="font-black text-blue-900 uppercase text-xs mb-2">Garage & Decks</h4>
                <p class="text-[10px] font-bold text-slate-500 leading-relaxed uppercase">Smart insulated garage doors and composite decking. Built for durability and curb appeal.</p>
            </div>
        </div>
    </section>

    <section class="bg-slate-900 py-20 px-6 text-white text-center">
        <h2 class="text-2xl font-black uppercase italic mb-12">The U.S. Home Improvement Advantage</h2>
        <div class="max-w-5xl mx-auto grid md:grid-cols-3 gap-10">
            <div>
                <div class="text-3xl mb-4">📍</div>
                <h5 class="font-black uppercase text-xs mb-2 text-blue-400">Local Experts</h5>
                <p class="text-[10px] font-bold text-slate-400 uppercase">We only dispatch state-licensed crews within 30 miles of your zip code.</p>
            </div>
            <div>
                <div class="text-3xl mb-4">💰</div>
                <h5 class="font-black uppercase text-xs mb-2 text-blue-400">Fixed Rates</h5>
                <p class="text-[10px] font-bold text-slate-400 uppercase">National wholesale pricing ensures you get the best rates on materials and labor.</p>
            </div>
            <div>
                <div class="text-3xl mb-4">🛡️</div>
                <h5 class="font-black uppercase text-xs mb-2 text-blue-400">Full Shield</h5>
                <p class="text-[10px] font-bold text-slate-400 uppercase">Every project is backed by our $1,000,000 service guarantee and LLC protection.</p>
            </div>
        </div>
    </section>

    <footer class="bg-white border-t py-16 px-8">
        <div class="max-w-6xl mx-auto grid md:grid-cols-4 gap-12">
            <div class="col-span-1 md:col-span-2">
                <h3 class="font-black uppercase text-sm mb-4 text-blue-900 italic">U.S. Home Improvement LLC</h3>
                <p class="text-[10px] font-bold text-slate-500 leading-relaxed uppercase max-w-sm">
                    U.S. Home Improvement is a registered LLC operating as a national service provider network. We connect homeowners with authorized, licensed, and insured local contractors. All site estimates are provided by local state professionals.
                </p>
            </div>
            <div>
                <h4 class="font-black uppercase text-[10px] mb-4 text-slate-400">Corporate HQ</h4>
                <p class="text-[10px] font-black text-slate-700 uppercase">702 Main Street<br>Woodland, California 95695<br>United States</p>
            </div>
            <div>
                <h4 class="font-black uppercase text-[10px] mb-4 text-slate-400">Legal Portal</h4>
                <div class="flex flex-col gap-3">
                    <span class="legal-link" onclick="alert('Privacy Shield Active: We do not sell your data to 3rd party marketers.')">Privacy Policy</span>
                    <span class="legal-link" onclick="alert('Terms of Use: Dispatch depends on local crew availability.')">Terms of Service</span>
                    <span class="legal-link">Licensing Info</span>
                </div>
            </div>
        </div>
        <div class="mt-16 border-t pt-8 text-center">
            <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest">© 2026 U.S. Home Improvement LLC. All Rights Reserved.</p>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-6"><h3 class="font-black">ADMIN DISPATCH TERMINAL</h3><button onclick="closeAdmin()" class="text-red-500 font-bold uppercase text-xs">Close</button></div>
        <div id="authPanel" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="****"><button onclick="unlock()" class="btn-action max-w-[200px]">Access</button></div>
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

        let taps = 0, tapT;
        function handleTap() { taps++; clearTimeout(tapT); if(taps >= 5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } tapT = setTimeout(()=>taps=0,2000); }

        const notifs = ["Sarah from CA booked Roofing!", "David from TX requested Solar.", "New Window lead in Florida!", "Bathroom survey booked in AZ.", "Kitchen remodel dispatch in NY."];
        setInterval(() => {
            const toast = document.getElementById('notification-toast');
            document.getElementById('notif-text').innerText = "⚡ " + notifs[Math.floor(Math.random()*notifs.length)];
            toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 5000);
        }, 15000);

        function goStep(id) { document.querySelectorAll('.step-form').forEach(s=>s.classList.remove('active')); document.getElementById(id).classList.add('active'); }

        function loadServiceMeta() {
            const s = document.getElementById('mainService').value;
            const container = document.getElementById('dynamicContainer');
            let h = '';
            const opts = {
                'Windows': [{l:'Window Count', o:['1-5','6-10','11-20','21+']},{l:'Frame Material', o:['Premium Vinyl','Natural Wood','Fiberglass']}],
                'Roofing': [{l:'Roof Type', o:['Asphalt','Metal','Tile','Flat']}],
                'Solar': [{l:'Electric Bill', o:['$50-150','$151-300','$301+']}]
            };
            const items = opts[s] || [{l:'Project Scope', o:['Standard','Premium','Luxury']}];
            items.forEach((item, i) => {
                h += `<p class="text-[9px] font-black text-slate-400 uppercase mb-2">${item.l}</p>
                      <select id="q${i}" class="input-pro mb-3" onchange="toggleM(${i})">
                        ${item.o.map(o => `<option value="${o}">${o}</option>`).join('')}
                        <option value="Manual">Manual Specifications...</option>
                      </select>
                      <input type="text" id="m${i}" placeholder="Enter specific details" class="input-pro hidden mb-3">`;
            });
            container.innerHTML = h;
        }
        loadServiceMeta();

        function toggleM(idx) { const s = document.getElementById(`q${idx}`); const m = document.getElementById(`m${idx}`); if(s.value==='Manual') m.classList.remove('hidden'); else m.classList.add('hidden'); }

        document.getElementById('proDispatchForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('mainService').value,
                owner: document.getElementById('isOwner').value,
                spec: document.getElementById('q0')?.value === 'Manual' ? document.getElementById('m0').value : document.getElementById('q0')?.value,
                name: document.getElementById('custName').value,
                address: document.getElementById('custAddress').value,
                phone: document.getElementById('custPhone').value,
                appointment: `${document.getElementById('appDate').value} (${document.getElementById('appSlot').value})`,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { alert("Authorization Success! ID #" + Math.floor(Math.random()*10000)); location.reload(); });
        });

        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authPanel').classList.add('hidden'); document.getElementById('leadsList').classList.remove('hidden'); sync(); } }
        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-6 border rounded-2xl bg-slate-50 relative mb-4 text-[10px] font-bold">
                        <span class="bg-blue-600 text-white px-3 py-1 rounded text-[8px] absolute top-4 right-4 uppercase">${data[k].service}</span>
                        <h4 class="text-xl font-black uppercase italic text-blue-900">${data[k].name}</h4>
                        <p>📍 ${data[k].address}</p>
                        <div class="mt-4 border-t pt-4 grid grid-cols-2 gap-4">
                            <p>📞: ${data[k].phone}</p>
                            <p class="col-span-2 text-emerald-600">📅 Appt: ${data[k].appointment}</p>
                        </div>
                        <button onclick="del('${k}')" class="mt-4 text-red-500 font-black">DELETE</button>
                    </div>`;
                }
                document.getElementById('leadsList').innerHTML = h || 'No Leads';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
