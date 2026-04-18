<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Official National Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@200;400;600;800&display=swap" rel="stylesheet">
    
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --dark: #010204; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; scroll-behavior: smooth; }
        
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.08); }
        .neon-glow { border: 1px solid rgba(0, 242, 255, 0.15); transition: 0.5s; }
        .neon-glow:hover { border-color: var(--neon); box-shadow: 0 0 40px rgba(0, 242, 255, 0.2); }

        .step { display: none; }
        .step.active { display: block; animation: slideUp 0.6s cubic-bezier(0.19, 1, 0.22, 1) forwards; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(40px); } to { opacity: 1; transform: translateY(0); } }

        .btn-opt { width: 100%; padding: 1.25rem; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.05); border-radius: 1.25rem; transition: 0.3s; display: flex; justify-content: space-between; align-items: center; }
        .btn-opt:hover { background: rgba(0, 242, 255, 0.1); border-color: var(--neon); transform: scale(1.02); }

        .feature-card img { transition: 0.8s ease; }
        .feature-card:hover img { transform: scale(1.1); }

        input { background: rgba(255,255,255,0.05) !important; border: 1px solid rgba(255,255,255,0.1) !important; color: white !important; outline: none; padding: 1.2rem; border-radius: 1rem; }
        input:focus { border-color: var(--neon) !important; }
    </style>
</head>
<body class="overflow-x-hidden">

    <nav class="fixed top-0 w-full z-[100] p-4">
        <div class="max-w-7xl mx-auto glass rounded-3xl px-8 py-4 flex justify-between items-center neon-glow">
            <div>
                <span class="text-2xl font-black italic tracking-tighter">U.S. HOME IMPROVEMENTS</span>
                <p class="text-[7px] text-cyan-400 font-bold uppercase tracking-[0.4em]">Official Contractor Matrix</p>
            </div>
            <a href="#portal" class="hidden md:block bg-cyan-600 px-6 py-2 rounded-full text-[10px] font-black uppercase hover:bg-cyan-400 transition">Get Started</a>
        </div>
    </nav>

    <header class="pt-40 pb-20 text-center px-6">
        <div class="max-w-4xl mx-auto">
            <h1 class="text-6xl md:text-8xl font-black mb-6 tracking-tighter leading-none italic">WE BUILD THE<br><span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-600">FUTURE OF HOMES.</span></h1>
            <p class="text-gray-500 text-lg uppercase tracking-widest font-light">Windows • Roofing • Solar • Remodeling</p>
        </div>
    </header>

    <section id="portal" class="max-w-2xl mx-auto px-6 py-10 mb-20">
        <div class="glass p-10 md:p-14 rounded-[3rem] neon-glow relative">
            <div class="absolute -top-4 -left-4 bg-cyan-600 px-4 py-1 rounded-lg text-[10px] font-black italic uppercase">Qualified Enrollment</div>
            <form id="masterForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black mb-8 italic">Choose Your Service</h2>
                    <div class="space-y-4">
                        <button type="button" onclick="handleService('Windows')" class="btn-opt font-bold"><span>🪟 Replacement Windows</span> <span>→</span></button>
                        <button type="button" onclick="next(3, 'service', 'Roofing')" class="btn-opt font-bold"><span>🏠 Premium Roofing</span> <span>→</span></button>
                        <button type="button" onclick="next(3, 'service', 'Solar')" class="btn-opt font-bold"><span>☀️ Solar Energy Matrix</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step-windows">
                    <h2 class="text-3xl font-black mb-8 italic">Project Scale</h2>
                    <p class="text-gray-500 text-xs mb-6 uppercase tracking-widest">How many windows?</p>
                    <div class="grid grid-cols-2 gap-4">
                        <button type="button" onclick="next(3, 'units', '3-5 Units')" class="btn-opt justify-center">3-5 Units</button>
                        <button type="button" onclick="next(3, 'units', '6-10 Units')" class="btn-opt justify-center">6-10 Units</button>
                        <button type="button" onclick="next(3, 'units', '11-20 Units')" class="btn-opt justify-center">11-20 Units</button>
                        <button type="button" onclick="next(3, 'units', '20+ Units')" class="btn-opt justify-center">20+ Units</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black mb-8 italic">Timeframe</h2>
                    <div class="space-y-4">
                        <button type="button" onclick="next(4, 'time', 'Urgent / ASAP')" class="btn-opt font-bold text-cyan-400"><span>🚀 ASAP (Ready to Start)</span></button>
                        <button type="button" onclick="next(4, 'time', '1-3 Months')" class="btn-opt font-bold"><span>📅 Within 3 Months</span></button>
                        <button type="button" onclick="next(4, 'time', 'Just Estimates')" class="btn-opt font-bold"><span>🔍 Getting Estimates</span></button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-3xl font-black mb-8 italic">Verification</h2>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" class="w-full font-bold">
                        <input type="tel" id="phone" placeholder="Phone Number" class="w-full font-bold">
                        <input type="email" id="email" placeholder="Email Address" class="w-full font-bold">
                        <input type="text" id="address" placeholder="Street Address" class="w-full font-bold">
                        <div class="grid grid-cols-2 gap-4">
                            <input type="text" id="city" placeholder="City" class="font-bold">
                            <input type="number" id="zip" placeholder="Zip" class="font-bold">
                        </div>
                        <button type="submit" class="w-full bg-green-600 p-6 rounded-2xl font-black uppercase text-xl shadow-2xl shadow-green-900/40 mt-4">Submit for Approval</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 py-20">
        <div class="grid md:grid-cols-3 gap-8">
            <div class="glass rounded-[2rem] overflow-hidden feature-card neon-glow">
                <img src="https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&fit=crop&w=600&q=80" class="w-full h-64 object-cover">
                <div class="p-8">
                    <h3 class="text-xl font-black italic mb-2 uppercase">Windows & Doors</h3>
                    <p class="text-xs text-gray-500 font-bold uppercase tracking-widest leading-loose">Energy efficient vinyl & wood solutions designed for the American climate.</p>
                </div>
            </div>
            <div class="glass rounded-[2rem] overflow-hidden feature-card neon-glow">
                <img src="https://images.unsplash.com/photo-1513694490325-24b3dc52a21c?auto=format&fit=crop&w=600&q=80" class="w-full h-64 object-cover">
                <div class="p-8">
                    <h3 class="text-xl font-black italic mb-2 uppercase">Solar Systems</h3>
                    <p class="text-xs text-gray-500 font-bold uppercase tracking-widest leading-loose">Reduce your bill to zero. Government backed solar programs for owners.</p>
                </div>
            </div>
            <div class="glass rounded-[2rem] overflow-hidden feature-card neon-glow">
                <img src="https://images.unsplash.com/photo-1632759162353-19c9a543fe79?auto=format&fit=crop&w=600&q=80" class="w-full h-64 object-cover">
                <div class="p-8">
                    <h3 class="text-xl font-black italic mb-2 uppercase">Roofing Elite</h3>
                    <p class="text-xs text-gray-500 font-bold uppercase tracking-widest leading-loose">Lifetime warranty architectural shingles and metal roofing systems.</p>
                </div>
            </div>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 z-[500] bg-black/98 backdrop-blur-3xl p-6 hidden overflow-y-auto">
        <div class="max-w-6xl mx-auto pt-10">
            <div class="flex justify-between items-center mb-10 border-b border-white/10 pb-8">
                <h2 class="text-4xl font-black italic text-cyan-400">LEAD CONTROL CENTER</h2>
                <button onclick="location.reload()" class="bg-red-600 px-4 py-2 rounded-xl text-[10px] font-bold">LOGOUT</button>
            </div>
            
            <div id="loginBox" class="max-w-md mx-auto py-20">
                <input type="password" id="adminKey" placeholder="Access Key" class="w-full p-6 bg-white/5 border border-white/10 rounded-2xl text-center text-4xl tracking-[0.4em] mb-6">
                <button onclick="unlock()" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase tracking-widest">Authorize Access</button>
            </div>

            <div id="dashboard" class="hidden grid gap-6" id="leadsList">
                </div>
        </div>
    </div>

    <footer class="py-20 text-center border-t border-white/5 mt-20">
        <p class="text-2xl font-black italic mb-4">U.S. HOME IMPROVEMENTS</p>
        <p class="text-[8px] text-gray-600 uppercase tracking-[0.5em] mb-8 font-bold">Licensed • Bonded • Insured | © 2026 National HQ</p>
    </footer>

    <script>
        // FIREBASE SETUP
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

        // Form Logic
        function handleService(val) {
            leadData.service = val;
            if(val === 'Windows') {
                document.getElementById('step1').classList.remove('active');
                document.getElementById('step-windows').classList.add('active');
            } else {
                next(3);
            }
        }

        function next(s, k, v) {
            if(k) leadData[k] = v;
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            leadData.name = document.getElementById('name').value;
            leadData.phone = document.getElementById('phone').value;
            leadData.email = document.getElementById('email').value;
            leadData.address = document.getElementById('address').value + ", " + document.getElementById('city').value;
            leadData.zip = document.getElementById('zip').value;
            leadData.timestamp = new Date().toLocaleString();

            db.ref('leads').push(leadData).then(() => {
                alert("Qualified Sweetie! Data sent to HQ. 🚀");
                location.reload();
            });
        });

        // ADMIN ACCESS (5 Taps)
        let t = 0, l = 0;
        document.addEventListener('click', () => {
            if(Date.now() - l < 400) t++; else t = 1;
            l = Date.now();
            if(t === 5) { document.getElementById('adminPortal').classList.remove('hidden'); t = 0; }
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('dashboard').classList.remove('hidden');
                sync();
            } else { alert("ACCESS DENIED!"); }
        }

        function sync() {
            db.ref('leads').on('value', (snap) => {
                const data = snap.val();
                let html = '';
                for(let id in data) {
                    html = `
                    <div class="glass p-8 rounded-3xl border-l-4 border-cyan-500">
                        <div class="flex justify-between mb-4">
                            <div><h3 class="text-2xl font-black italic">${data[id].name}</h3><p class="text-cyan-400 font-bold text-xs uppercase">${data[id].service}</p></div>
                            <div class="flex gap-2"><button onclick="copy('${id}')" class="bg-cyan-600 px-3 py-1 rounded text-[10px] font-bold">COPY</button><button onclick="del('${id}')" class="bg-red-600 px-3 py-1 rounded text-[10px] font-bold">DEL</button></div>
                        </div>
                        <div class="grid grid-cols-2 gap-4 text-sm text-gray-500 mb-4">
                            <p>📞 ${data[id].phone}</p><p>📧 ${data[id].email}</p><p class="col-span-2">📍 ${data[id].address} (${data[id].zip})</p>
                        </div>
                        <div class="flex justify-between text-[10px] font-bold uppercase tracking-widest text-gray-700">
                            <span>Time: ${data[id].time}</span><span>Windows: ${data[id].units}</span>
                        </div>
                        <textarea id="copy-${id}" class="hidden">Lead Details:\nName: ${data[id].name}\nPhone: ${data[id].phone}\nEmail: ${data[id].email}\nAddress: ${data[id].address}\nService: ${data[id].service}\nUnits: ${data[id].units}\nTime: ${data[id].time}</textarea>
                    </div>` + html;
                }
                document.getElementById('dashboard').innerHTML = html;
            });
        }

        function copy(id) {
            const el = document.getElementById('copy-' + id);
            el.classList.remove('hidden'); el.select(); document.execCommand('copy'); el.classList.add('hidden');
            alert("Lead data copied!");
        }

        function del(id) { if(confirm("Delete lead?")) db.ref('leads/' + id).remove(); }
    </script>
</body>
</html>
