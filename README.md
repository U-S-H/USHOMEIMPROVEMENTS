<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Enterprise Solutions</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --dark: #020408; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 2rem; }
        .neon-glow:hover { border-color: var(--neon); box-shadow: 0 0 30px rgba(0, 242, 255, 0.15); transform: translateY(-5px); }
        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.5s ease forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        input { background: rgba(255,255,255,0.05) !important; border: 1px solid rgba(255,255,255,0.1) !important; color: white !important; padding: 1.25rem; border-radius: 1rem; width: 100%; outline: none; transition: 0.3s; }
        input:focus { border-color: var(--neon) !important; }
        .badge-glow { filter: grayscale(1) invert(1) brightness(2); opacity: 0.5; transition: 0.3s; }
        .badge-glow:hover { filter: none; opacity: 1; }
    </style>
</head>
<body class="pb-10">

    <div class="bg-cyan-600 text-[10px] font-black uppercase tracking-[0.3em] text-center py-2 text-black">
        National Licensed Contractor Network • Accredited A+ Rated System
    </div>

    <nav class="p-6">
        <div class="max-w-6xl mx-auto glass px-8 py-4 flex justify-between items-center neon-glow">
            <div class="leading-none">
                <span class="text-2xl font-black italic tracking-tighter">U.S. HOME IMPROVEMENTS</span>
                <p class="text-[7px] text-cyan-400 font-bold uppercase tracking-[0.4em] mt-1">Official Corporate Matrix</p>
            </div>
            <div class="hidden md:flex gap-6 text-[10px] font-black uppercase text-gray-400">
                <a href="#services" class="hover:text-cyan-400">Services</a>
                <a href="#faqs" class="hover:text-cyan-400">FAQ</a>
                <a href="#portal" class="text-cyan-400 underline underline-offset-8">Get Quote</a>
            </div>
        </div>
    </nav>

    <header class="max-w-5xl mx-auto px-6 pt-20 pb-10 text-center">
        <div class="inline-block bg-white/5 border border-white/10 px-4 py-1 rounded-full text-[10px] font-bold uppercase text-cyan-400 mb-6">
            Trusted by 50,000+ Homeowners
        </div>
        <h1 class="text-5xl md:text-8xl font-black italic tracking-tighter leading-none mb-8">
            ELITE HOME <br><span class="text-cyan-400 underline decoration-white/10">UPGRADES.</span>
        </h1>
        
        <div class="flex justify-center gap-8 md:gap-16 mt-12 mb-20 flex-wrap">
            <img src="https://upload.wikimedia.org/wikipedia/commons/e/e0/Energy_Star_logo.svg" class="h-8 badge-glow" alt="Energy Star">
            <img src="https://upload.wikimedia.org/wikipedia/commons/0/07/Better_Business_Bureau_logo.svg" class="h-8 badge-glow" alt="BBB">
            <div class="text-left"><p class="text-[10px] font-bold text-gray-500 uppercase">Google Rating</p><p class="text-lg font-black italic">4.9 ⭐⭐⭐⭐⭐</p></div>
        </div>
    </header>

    <section id="portal" class="max-w-2xl mx-auto px-6 py-10">
        <div class="glass p-10 md:p-14 border-t-4 border-cyan-500 relative shadow-2xl">
            <form id="masterForm">
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black mb-10 italic uppercase">01. Choose Upgrade</h2>
                    <div class="grid gap-4">
                        <button type="button" onclick="handleService('Windows')" class="p-6 bg-white/5 border border-white/10 rounded-2xl flex justify-between items-center hover:border-cyan-500 transition font-bold uppercase tracking-widest text-sm"><span>🪟 Windows Replacement</span> <span>→</span></button>
                        <button type="button" onclick="next(3, 'service', 'Roofing')" class="p-6 bg-white/5 border border-white/10 rounded-2xl flex justify-between items-center hover:border-cyan-500 transition font-bold uppercase tracking-widest text-sm"><span>🏠 Elite Roofing</span> <span>→</span></button>
                        <button type="button" onclick="next(3, 'service', 'Solar')" class="p-6 bg-white/5 border border-white/10 rounded-2xl flex justify-between items-center hover:border-cyan-500 transition font-bold uppercase tracking-widest text-sm"><span>☀️ Solar Matrix</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step-windows">
                    <h2 class="text-3xl font-black mb-10 italic uppercase text-cyan-400">02. Quantity</h2>
                    <div class="grid grid-cols-2 gap-4">
                        <button type="button" onclick="next(3, 'units', '1-5')" class="p-5 bg-white/5 rounded-2xl hover:border-cyan-400 border border-transparent font-bold">1-5 Units</button>
                        <button type="button" onclick="next(3, 'units', '6-10')" class="p-5 bg-white/5 rounded-2xl hover:border-cyan-400 border border-transparent font-bold">6-10 Units</button>
                        <button type="button" onclick="next(3, 'units', '11-20')" class="p-5 bg-white/5 rounded-2xl hover:border-cyan-400 border border-transparent font-bold">11-20 Units</button>
                        <button type="button" onclick="next(3, 'units', '20+')" class="p-5 bg-white/5 rounded-2xl hover:border-cyan-400 border border-transparent font-bold">20+ Units</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black mb-10 italic uppercase text-cyan-400">03. Timeline</h2>
                    <div class="space-y-4">
                        <button type="button" onclick="next(4, 'time', 'ASAP')" class="w-full p-6 bg-cyan-600/10 border border-cyan-500/50 rounded-2xl text-left font-black">🚀 ASAP (READY TO START)</button>
                        <button type="button" onclick="next(4, 'time', '1-3 Months')" class="w-full p-6 bg-white/5 rounded-2xl text-left font-bold">📅 WITHIN 90 DAYS</button>
                        <button type="button" onclick="next(4, 'time', 'Just Estimate')" class="w-full p-6 bg-white/5 rounded-2xl text-left font-bold">🔍 GATHERING ESTIMATES</button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-3xl font-black mb-10 italic uppercase text-cyan-400">04. Qualification</h2>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" required>
                        <input type="tel" id="phone" placeholder="Mobile Phone" required>
                        <input type="email" id="email" placeholder="Email Address" required>
                        <input type="text" id="address" placeholder="Street Address" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="text" id="city" placeholder="City">
                            <input type="number" id="zip" placeholder="Zip Code" required>
                        </div>
                        <button type="submit" class="w-full p-6 bg-cyan-600 rounded-2xl font-black uppercase text-xl mt-6 text-black tracking-widest shadow-xl shadow-cyan-500/20">Authorize & Submit</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section id="services" class="max-w-6xl mx-auto px-6 py-24 grid md:grid-cols-3 gap-8">
        <div class="glass p-8 neon-glow">
            <img src="https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&fit=crop&w=600" class="w-full h-48 object-cover rounded-2xl mb-6">
            <h3 class="text-xl font-black italic uppercase mb-2">Impact Windows</h3>
            <p class="text-xs text-gray-500 font-bold uppercase leading-relaxed">High-performance insulated glass units for maximum thermal efficiency.</p>
        </div>
        <div class="glass p-8 neon-glow">
            <img src="https://images.unsplash.com/photo-1632759162353-19c9a543fe79?auto=format&fit=crop&w=600" class="w-full h-48 object-cover rounded-2xl mb-6">
            <h3 class="text-xl font-black italic uppercase mb-2">Architectural Roofing</h3>
            <p class="text-xs text-gray-500 font-bold uppercase leading-relaxed">Lifetime-warranted asphalt and metal systems for total property protection.</p>
        </div>
        <div class="glass p-8 neon-glow">
            <img src="https://images.unsplash.com/photo-1513694490325-24b3dc52a21c?auto=format&fit=crop&w=600" class="w-full h-48 object-cover rounded-2xl mb-6">
            <h3 class="text-xl font-black italic uppercase mb-2">Solar Generation</h3>
            <p class="text-xs text-gray-500 font-bold uppercase leading-relaxed">Net-zero energy solutions designed to eliminate your monthly utility costs.</p>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 z-[1000] bg-black/98 backdrop-blur-3xl p-6 hidden overflow-y-auto">
        <div class="max-w-5xl mx-auto pt-10 pb-20">
            <div class="flex justify-between items-center mb-16 border-b border-white/10 pb-8">
                <h2 class="text-5xl font-black italic text-cyan-400">GLOBAL LEAD COMMAND</h2>
                <button onclick="location.reload()" class="bg-red-600 px-8 py-3 rounded-full text-[10px] font-black uppercase">Terminate</button>
            </div>
            <div id="loginBox" class="max-w-md mx-auto py-20">
                <input type="password" id="adminKey" class="text-center text-4xl tracking-[0.5em] mb-8" placeholder="****">
                <button onclick="unlock()" class="w-full bg-cyan-600 p-6 rounded-2xl font-black uppercase text-black">Authorize Session</button>
            </div>
            <div id="leadsDashboard" class="hidden grid gap-6" id="leadsList"></div>
        </div>
    </div>

    <footer class="max-w-6xl mx-auto px-6 py-20 border-t border-white/5 text-center md:text-left grid md:grid-cols-4 gap-12">
        <div class="col-span-2">
            <h2 class="text-2xl font-black italic tracking-tighter mb-4">U.S. HOME IMPROVEMENTS</h2>
            <p class="text-xs text-gray-600 font-bold uppercase leading-relaxed max-w-sm">The national leader in home modernization. We connect homeowners with certified, top-tier contractors to ensure every project is built to perfection.</p>
        </div>
        <div>
            <p class="text-[10px] font-black uppercase text-cyan-400 mb-4">Verification</p>
            <p class="text-xs text-gray-500 font-bold uppercase mb-2">License #US-99201-HI</p>
            <p class="text-xs text-gray-500 font-bold uppercase mb-2">Fully Bonded & Insured</p>
        </div>
        <div>
            <p class="text-[10px] font-black uppercase text-cyan-400 mb-4">Contact HQ</p>
            <p class="text-xs text-gray-500 font-bold uppercase mb-2">Support: 1-800-US-HOMES</p>
            <p class="text-xs text-gray-500 font-bold uppercase mb-2">hq@ushomeimprovements.com</p>
        </div>
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

        let leadData = { units: 'N/A' };

        function handleService(v) {
            leadData.service = v;
            if(v === 'Windows') showStep('step-windows'); else next(3);
        }

        function showStep(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo({ top: document.getElementById('portal').offsetTop - 80, behavior: 'smooth' });
        }

        function next(s, k, v) {
            if(k) leadData[k] = v;
            showStep('step' + s);
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            leadData.name = document.getElementById('name').value;
            leadData.phone = document.getElementById('phone').value;
            leadData.email = document.getElementById('email').value;
            leadData.address = `${document.getElementById('address').value}, ${document.getElementById('city').value}`;
            leadData.zip = document.getElementById('zip').value;
            leadData.timestamp = new Date().toLocaleString();

            db.ref('leads').push(leadData).then(() => {
                alert("APPLICATION QUALIFIED! 🚀\nA National Specialist will contact you within 24 hours.");
                location.reload();
            });
        });

        // GHOST ADMIN TRIGGER
        let taps = 0, lastTap = 0;
        document.addEventListener('click', () => {
            if(Date.now() - lastTap < 400) taps++; else taps = 1;
            lastTap = Date.now();
            if(taps === 5) { document.getElementById('adminPortal').classList.remove('hidden'); taps = 0; }
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('leadsDashboard').classList.remove('hidden');
                sync();
            } else { alert("ACCESS DENIED"); }
        }

        function sync() {
            db.ref('leads').on('value', (snap) => {
                const data = snap.val();
                let html = '';
                for(let id in data) {
                    html = `
                    <div class="glass p-8 border-l-4 border-cyan-500 relative group">
                        <div class="flex justify-between mb-4">
                            <div><h3 class="text-2xl font-black italic tracking-tighter">${data[id].name}</h3><p class="text-cyan-400 font-bold text-[10px] uppercase">${data[id].service}</p></div>
                            <div class="flex gap-2">
                                <button onclick="copyLead('${id}')" class="bg-cyan-600/10 text-cyan-400 border border-cyan-500/20 px-4 py-2 rounded-xl text-[9px] font-black uppercase">Copy</button>
                                <button onclick="deleteLead('${id}')" class="bg-red-600/10 text-red-400 border border-red-500/20 px-4 py-2 rounded-xl text-[9px] font-black uppercase">Delete</button>
                            </div>
                        </div>
                        <div class="grid md:grid-cols-2 gap-4 text-sm text-gray-500 font-medium italic">
                            <p>📞 ${data[id].phone}</p><p>📧 ${data[id].email}</p><p class="col-span-2">📍 ${data[id].address} (ZIP: ${data[id].zip})</p>
                        </div>
                        <div class="mt-6 flex justify-between text-[9px] text-gray-700 font-black uppercase tracking-widest">
                            <span>Time: ${data[id].time}</span><span>Units: ${data[id].units}</span><span>Captured: ${data[id].timestamp}</span>
                        </div>
                        <textarea id="copy-${id}" class="hidden">Lead Details:\nName: ${data[id].name}\nPhone: ${data[id].phone}\nEmail: ${data[id].email}\nAddress: ${data[id].address}\nService: ${data[id].service}\nTime: ${data[id].time}</textarea>
                    </div>` + html;
                }
                document.getElementById('leadsDashboard').innerHTML = html || '<p class="text-center py-20 text-gray-700 font-black uppercase tracking-widest">Waiting for leads...</p>';
            });
        }

        function copyLead(id) {
            const el = document.getElementById('copy-' + id);
            el.classList.remove('hidden'); el.select(); document.execCommand('copy'); el.classList.add('hidden');
            alert("Lead data exported to clipboard!");
        }

        function deleteLead(id) {
            if(confirm("Confirm deletion?")) db.ref('leads/' + id).remove();
        }
    </script>
</body>
</html>
