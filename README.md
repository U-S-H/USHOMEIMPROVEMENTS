<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Contractor Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --dark: #020408; --glass-bg: rgba(255, 255, 255, 0.03); }
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background-color: var(--dark); 
            color: white; 
            overflow-x: hidden;
            background-image: radial-gradient(circle at 50% -20%, #1a3a4a 0%, var(--dark) 80%);
        }
        
        .glass-card { 
            background: var(--glass-bg); 
            backdrop-filter: blur(20px); 
            border: 1px solid rgba(255, 255, 255, 0.08); 
            border-radius: 2rem;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
        }

        .neon-glow:hover { 
            border-color: var(--neon); 
            box-shadow: 0 0 30px rgba(0, 242, 255, 0.1); 
            transform: translateY(-5px);
            transition: all 0.4s ease;
        }

        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.6s cubic-bezier(0.23, 1, 0.32, 1) forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        input, select { 
            background: rgba(255, 255, 255, 0.05) !important; 
            border: 1px solid rgba(255, 255, 255, 0.1) !important; 
            color: white !important;
            padding: 1.25rem !important;
            border-radius: 1rem !important;
            width: 100%;
            outline: none;
        }
        input:focus { border-color: var(--neon) !important; box-shadow: 0 0 15px rgba(0, 242, 255, 0.1); }

        .btn-action {
            background: linear-gradient(135deg, #00f2ff 0%, #0061ff 100%);
            color: black;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: 0.3s;
        }
        .btn-action:hover { filter: brightness(1.1); transform: scale(1.02); }
        
        .service-img { width: 100%; height: 220px; object-fit: cover; border-radius: 1.5rem; }
    </style>
</head>
<body class="pb-20">

    <nav class="sticky top-0 z-50 p-4">
        <div class="max-w-5xl mx-auto glass-card px-8 py-4 flex justify-between items-center neon-glow">
            <div>
                <span class="text-xl font-black italic tracking-tighter">U.S. HOME IMPROVEMENTS</span>
                <p class="text-[7px] text-cyan-400 font-bold uppercase tracking-[0.4em] mt-1">Certified National HQ</p>
            </div>
            <div class="flex items-center gap-4">
                <span class="hidden md:block text-[9px] font-bold text-gray-500 uppercase tracking-widest">🛡️ Bonded & Insured</span>
                <div class="h-8 w-[1px] bg-white/10 hidden md:block"></div>
                <button onclick="document.getElementById('portal').scrollIntoView()" class="text-[10px] font-black uppercase text-cyan-400">Start Project</button>
            </div>
        </div>
    </nav>

    <header class="max-w-5xl mx-auto px-6 pt-16 pb-10 text-center">
        <h2 class="text-5xl md:text-7xl font-black italic tracking-tighter leading-none mb-6">
            TRANSFORMING <br><span class="text-cyan-400">AMERICAN HOMES.</span>
        </h2>
        <p class="text-gray-400 max-w-2xl mx-auto text-sm md:text-base leading-relaxed">
            The most trusted network for high-end home upgrades across the United States. 
            Fast, free, and reliable contractor matching.
        </p>
    </header>

    <section id="portal" class="max-w-2xl mx-auto px-6 py-10">
        <div class="glass-card p-8 md:p-12 relative overflow-hidden border-t-2 border-cyan-500/30">
            <form id="masterForm">
                
                <div class="step active" id="step1">
                    <div class="flex justify-between items-center mb-8">
                        <h3 class="text-2xl font-black italic uppercase">01. Service</h3>
                        <span class="text-[10px] font-bold text-cyan-500 bg-cyan-500/10 px-3 py-1 rounded-full uppercase">Step 1/4</span>
                    </div>
                    <div class="grid grid-cols-1 gap-4">
                        <button type="button" onclick="handleService('Windows')" class="p-6 bg-white/5 border border-white/10 rounded-2xl flex justify-between items-center hover:bg-cyan-500/10 hover:border-cyan-500/50 transition group">
                            <span class="font-bold">Replacement Windows</span>
                            <span class="text-cyan-500 opacity-0 group-hover:opacity-100 transition">→</span>
                        </button>
                        <button type="button" onclick="next(3, 'service', 'Roofing')" class="p-6 bg-white/5 border border-white/10 rounded-2xl flex justify-between items-center hover:bg-cyan-500/10 hover:border-cyan-500/50 transition group">
                            <span class="font-bold">Premium Roofing</span>
                            <span class="text-cyan-500 opacity-0 group-hover:opacity-100 transition">→</span>
                        </button>
                        <button type="button" onclick="next(3, 'service', 'Solar')" class="p-6 bg-white/5 border border-white/10 rounded-2xl flex justify-between items-center hover:bg-cyan-500/10 hover:border-cyan-500/50 transition group">
                            <span class="font-bold">Solar Power Matrix</span>
                            <span class="text-cyan-500 opacity-0 group-hover:opacity-100 transition">→</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step-windows">
                    <h3 class="text-2xl font-black italic uppercase mb-8">02. Window Units</h3>
                    <div class="grid grid-cols-2 gap-4">
                        <button type="button" onclick="next(3, 'units', '1-5')" class="p-4 bg-white/5 border border-white/10 rounded-xl font-bold hover:border-cyan-500">1-5 Units</button>
                        <button type="button" onclick="next(3, 'units', '6-10')" class="p-4 bg-white/5 border border-white/10 rounded-xl font-bold hover:border-cyan-500">6-10 Units</button>
                        <button type="button" onclick="next(3, 'units', '11-20')" class="p-4 bg-white/5 border border-white/10 rounded-xl font-bold hover:border-cyan-500">11-20 Units</button>
                        <button type="button" onclick="next(3, 'units', '20+')" class="p-4 bg-white/5 border border-white/10 rounded-xl font-bold hover:border-cyan-500">20+ Units</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h3 class="text-2xl font-black italic uppercase mb-8">03. Project Timeline</h3>
                    <div class="space-y-4">
                        <button type="button" onclick="next(4, 'time', 'Urgent / ASAP')" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl text-left font-bold hover:border-cyan-500">🚀 ASAP (Ready to Start)</button>
                        <button type="button" onclick="next(4, 'time', '1-3 Months')" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl text-left font-bold hover:border-cyan-500">📅 Within 90 Days</button>
                        <button type="button" onclick="next(4, 'time', 'Estimates Only')" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl text-left font-bold hover:border-cyan-500">🔍 Getting Quotes Only</button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h3 class="text-2xl font-black italic uppercase mb-8">04. Final Verification</h3>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" required>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <input type="tel" id="phone" placeholder="Mobile Number" required>
                            <input type="email" id="email" placeholder="Email Address" required>
                        </div>
                        <input type="text" id="address" placeholder="Street Address" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="text" id="city" placeholder="City">
                            <input type="number" id="zip" placeholder="Zip Code" required>
                        </div>
                        <button type="submit" class="w-full p-5 rounded-2xl btn-action text-xl mt-4">Confirm Lead Details</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-5xl mx-auto px-6 py-20 grid md:grid-cols-2 gap-8">
        <div class="glass-card p-6 neon-glow">
            <img src="https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&fit=crop&w=800" class="service-img mb-6" alt="Windows">
            <h4 class="text-xl font-black italic uppercase mb-2">Architectural Windows</h4>
            <p class="text-xs text-gray-500 font-bold uppercase tracking-widest leading-loose">Energy-star rated vinyl and wood window replacements for maximum efficiency.</p>
        </div>
        <div class="glass-card p-6 neon-glow">
            <img src="https://images.unsplash.com/photo-1513694490325-24b3dc52a21c?auto=format&fit=crop&w=800" class="service-img mb-6" alt="Solar">
            <h4 class="text-xl font-black italic uppercase mb-2">Solar Solutions</h4>
            <p class="text-xs text-gray-500 font-bold uppercase tracking-widest leading-loose">Join the green revolution. Reduce electric bills to zero with zero-down solar programs.</p>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 z-[1000] bg-black/95 backdrop-blur-3xl p-6 hidden overflow-y-auto">
        <div class="max-w-5xl mx-auto pt-10">
            <div class="flex justify-between items-center mb-10 border-b border-white/10 pb-8">
                <h2 class="text-4xl font-black italic text-cyan-400">HQ DATA COMMAND</h2>
                <button onclick="location.reload()" class="bg-red-600 px-6 py-2 rounded-xl text-[10px] font-black uppercase">Close Access</button>
            </div>
            
            <div id="loginBox" class="max-w-md mx-auto py-20">
                <input type="password" id="adminKey" placeholder="Access Key" class="w-full p-8 text-center text-5xl tracking-[0.5em] mb-8">
                <button onclick="unlock()" class="w-full bg-cyan-600 p-6 rounded-2xl font-black uppercase tracking-widest">Verify Authorization</button>
            </div>

            <div id="dashboard" class="hidden space-y-6" id="leadsList">
                </div>
        </div>
    </div>

    <footer class="text-center py-20 border-t border-white/5">
        <span class="text-2xl font-black italic">U.S. HOME IMPROVEMENTS</span>
        <p class="text-[8px] text-gray-600 uppercase tracking-[0.6em] mt-4 font-bold italic">© 2026 National Contractor Matrix | Authorized Providers Only</p>
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
            if(v === 'Windows') {
                showStep('step-windows');
            } else {
                next(3);
            }
        }

        function showStep(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo({ top: document.getElementById('portal').offsetTop - 100, behavior: 'smooth' });
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
                alert("Data Securely Transmitted! 🚀\nA specialist will verify your eligibility.");
                location.reload();
            });
        });

        // ADMIN TRIGGER (5 TAPS)
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
            } else { alert("ACCESS DENIED"); }
        }

        function sync() {
            db.ref('leads').on('value', (snap) => {
                const data = snap.val();
                let html = '';
                for(let id in data) {
                    html = `
                    <div class="glass-card p-8 border-l-4 border-cyan-500 relative">
                        <div class="flex justify-between items-start mb-6">
                            <div>
                                <h4 class="text-3xl font-black italic tracking-tighter">${data[id].name}</h4>
                                <p class="text-cyan-400 font-black text-[10px] uppercase tracking-widest">${data[id].service}</p>
                            </div>
                            <div class="flex gap-2">
                                <button onclick="copyLead('${id}')" class="bg-cyan-600/20 text-cyan-400 border border-cyan-500/30 px-4 py-2 rounded-xl text-[10px] font-black hover:bg-cyan-600 hover:text-white transition">COPY</button>
                                <button onclick="deleteLead('${id}')" class="bg-red-600/20 text-red-500 border border-red-500/30 px-4 py-2 rounded-xl text-[10px] font-black hover:bg-red-600 hover:text-white transition">DELETE</button>
                            </div>
                        </div>
                        <div class="grid md:grid-cols-2 gap-4 text-sm text-gray-400">
                            <p>📞 ${data[id].phone}</p>
                            <p>📧 ${data[id].email}</p>
                            <p class="col-span-2">📍 ${data[id].address} (Zip: ${data[id].zip})</p>
                        </div>
                        <div class="mt-6 pt-6 border-t border-white/5 flex justify-between text-[9px] text-gray-600 font-bold uppercase tracking-widest">
                            <span>Time: ${data[id].time}</span>
                            <span>Windows: ${data[id].units}</span>
                            <span>Date: ${data[id].timestamp}</span>
                        </div>
                        <textarea id="copy-${id}" class="hidden">Lead Details:\nName: ${data[id].name}\nPhone: ${data[id].phone}\nService: ${data[id].service}\nAddress: ${data[id].address}</textarea>
                    </div>` + html;
                }
                document.getElementById('dashboard').innerHTML = html || '<p class="text-center py-20 text-gray-600">No leads captured yet.</p>';
            });
        }

        function copyLead(id) {
            const el = document.getElementById('copy-' + id);
            el.classList.remove('hidden'); el.select(); document.execCommand('copy'); el.classList.add('hidden');
            alert("Lead Data Copied!");
        }

        function deleteLead(id) {
            if(confirm("Permanent Delete?")) db.ref('leads/' + id).remove();
        }
    </script>
</body>
</html>
