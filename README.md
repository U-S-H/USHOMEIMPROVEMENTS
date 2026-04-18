<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Enterprise Matrix</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --slate: #0f172a; --slate-light: #1e293b; --accent: #334155; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--slate); scroll-behavior: smooth; margin: 0; overflow-x: hidden; }
        
        /* Premium Backgrounds */
        .hero-bg {
            background: linear-gradient(rgba(15, 23, 42, 0.90), rgba(15, 23, 42, 0.85)),
                        url('https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/hero-banner.jpg');
            background-size: cover; background-position: center;
        }

        /* Glassmorphism Card */
        .glass-panel {
            background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(20px);
            border-radius: 2.5rem; border: 1px solid white; box-shadow: 0 40px 100px rgba(0,0,0,0.08);
        }

        /* Form Steps Animation */
        .step { display: none; }
        .step.active { display: block; animation: slideFade 0.5s ease-out; }
        @keyframes slideFade { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        /* Modern Inputs */
        .input-matrix {
            width: 100%; padding: 1.25rem; border-radius: 1.25rem; border: 2px solid #f1f5f9;
            font-weight: 600; outline: none; transition: 0.3s; background: #fff; appearance: none;
        }
        .input-matrix:focus { border-color: var(--neon); box-shadow: 0 0 20px rgba(0, 242, 255, 0.1); }

        /* Buttons */
        .btn-elite {
            background: var(--slate); color: white; padding: 1.3rem; border-radius: 1.25rem;
            font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; transition: 0.4s;
            letter-spacing: 1px;
        }
        .btn-elite:hover { background: var(--neon); color: var(--slate); transform: translateY(-3px); }
        
        /* Service Cards */
        .feature-card {
            background: white; border-radius: 2rem; border: 1px solid #f1f5f9; transition: 0.4s; cursor: pointer;
            overflow: hidden;
        }
        .feature-card:hover { border-color: var(--neon); transform: translateY(-10px); box-shadow: 0 20px 40px rgba(0,0,0,0.05); }
        .feature-card img { width: 100%; h-48; object-cover; transition: 0.5s; }
        .feature-card:hover img { transform: scale(1.05); }
    </style>
</head>
<body>

    <header class="hero-bg h-[65vh] flex flex-col items-center justify-center text-center px-6 text-white relative">
        <div class="absolute top-8 left-8 flex items-center gap-3">
            <img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/logo.png" alt="Logo" class="h-10">
            <span class="text-[10px] font-black tracking-[0.3em] uppercase border-l-2 border-cyan-400 pl-4">National Enterprise</span>
        </div>
        <h1 class="text-5xl md:text-8xl font-black italic tracking-tighter uppercase leading-none mt-10">THE NATIONAL<br>STANDARD</h1>
        <p class="text-cyan-400 font-bold tracking-[0.6em] text-[10px] mt-8 uppercase">Nationwide Certified Contractor Matrix</p>
        <div class="mt-12">
            <a href="#portal" class="bg-white text-slate-900 px-10 py-4 rounded-full font-black text-xs uppercase hover:bg-cyan-400 transition shadow-2xl">Start Qualification</a>
        </div>
    </header>

    <section id="portal" class="max-w-3xl mx-auto -mt-24 px-4 mb-32 relative z-20">
        <div class="glass-panel p-10 md:p-16 border-t-[10px] border-slate-900 shadow-2xl">
            <form id="masterLeadForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">01. Project Criteria</h2>
                    <div class="space-y-6">
                        <select id="homeowner" class="input-matrix" required>
                            <option value="">Property Ownership Status?</option>
                            <option value="Yes">I am the Homeowner</option>
                            <option value="No">I am a Renter</option>
                        </select>
                        <select id="service" class="input-matrix" required onchange="handleServiceSelection()">
                            <option value="">Select Upgrade Service</option>
                            <option value="Windows">Replacement Windows</option>
                            <option value="Doors">Security Entry Doors</option>
                            <option value="Roofing">Architectural Roofing</option>
                            <option value="Solar">Residential Solar Matrix</option>
                            <option value="Build Home">Professional Build Service</option>
                            <option value="Kitchen">Kitchen Remodeling</option>
                            <option value="Bathroom">Bathroom Remodeling</option>
                            <option value="Deck">Deck Remodeling</option>
                            <option value="Garage">Garage Matrix</option>
                        </select>
                        <div id="winDiv" class="hidden animate-pulse">
                            <label class="text-[10px] font-black uppercase text-slate-400 ml-2 mb-2 block">Quantity of Units</label>
                            <select id="winCount" class="input-matrix">
                                <option value="">How many windows?</option>
                                <option value="1-5">1 - 5 Windows</option>
                                <option value="6-10">6 - 10 Windows</option>
                                <option value="11-20">11 - 20 Windows</option>
                                <option value="20+">20+ Units</option>
                            </select>
                        </div>
                        <button type="button" onclick="goNext('step2')" class="btn-elite">Continue</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">02. Timing & Eligibility</h2>
                    <div class="space-y-6">
                        <select id="ready" class="input-matrix" required>
                            <option value="">Project Timeline</option>
                            <option value="ASAP">As Soon As Possible</option>
                            <option value="2-Months">Within 2 Months</option>
                            <option value="3-Months">Within 3 Months</option>
                            <option value="6-Months">Within 6 Months</option>
                            <option value="1-Year">In a Year</option>
                        </select>
                        <select id="credit" class="input-matrix" required>
                            <option value="">Estimated Credit Rating</option>
                            <option value="Excellent (720+)">Excellent (720+)</option>
                            <option value="Good (660-719)">Good (660-719)</option>
                            <option value="Fair (600-659)">Fair (600-659)</option>
                            <option value="Building (Below 600)">Building Credit</option>
                        </select>
                        <button type="button" onclick="goNext('step3')" class="btn-elite">Schedule Visit</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">03. Deployment Window</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-400 ml-2 mb-2 block">Inspection Date</label>
                            <input type="date" id="appDate" class="input-matrix" required>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-400 ml-2 mb-2 block">Time Preference</label>
                            <select id="appTime" class="input-matrix">
                                <option>Morning (8AM-12PM)</option>
                                <option>Afternoon (12PM-4PM)</option>
                                <option>Evening (4PM-7PM)</option>
                            </select>
                        </div>
                    </div>
                    <button type="button" onclick="goNext('step4')" class="btn-elite">Final Details</button>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">04. Contact Protocol</h2>
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Legal Name" class="input-matrix" required>
                        <input type="number" id="cAge" placeholder="Age" class="input-matrix" required>
                        <input type="email" id="cEmail" placeholder="Email Address" class="input-matrix" required>
                        <input type="tel" id="cPhone" placeholder="Direct Contact Number" class="input-matrix" required>
                        <input type="text" id="cAddr" placeholder="Street Address" class="input-matrix" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="text" id="cState" placeholder="State" class="input-matrix" required>
                            <input type="number" id="cZip" placeholder="Zip" class="input-matrix" required>
                        </div>
                        <button type="submit" class="btn-elite bg-cyan-500 text-slate-900 shadow-xl shadow-cyan-100">Authorise & Get Quote</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section id="services" class="max-w-7xl mx-auto px-6 mb-32">
        <div class="text-center mb-16">
            <h3 class="text-4xl font-black italic uppercase">National Network Services</h3>
            <p class="text-slate-400 font-bold uppercase text-[10px] tracking-widest mt-2">Serving All 50 States Across the Continental U.S.</p>
        </div>
        <div class="grid md:grid-cols-3 lg:grid-cols-4 gap-8">
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <div class="h-48 overflow-hidden rounded-2xl mb-6"><img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/build-service.jpg" class="h-48 object-cover"></div>
                <h4 class="font-black uppercase text-xs italic">Professional Build Service</h4>
                <p class="text-[10px] text-slate-400 font-bold uppercase mt-2">Certified Corporate Structural Execution.</p>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <div class="h-48 overflow-hidden rounded-2xl mb-6"><img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/windows-service.jpg" class="h-48 object-cover"></div>
                <h4 class="font-black uppercase text-xs italic">Windows Matrix</h4>
                <p class="text-[10px] text-slate-400 font-bold uppercase mt-2">Energy-Star Rated Elite Glass.</p>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <div class="h-48 overflow-hidden rounded-2xl mb-6"><img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/doors-service.jpg" class="h-48 object-cover"></div>
                <h4 class="font-black uppercase text-xs italic">Security Entry Doors</h4>
                <p class="text-[10px] text-slate-400 font-bold uppercase mt-2">Maximum Security Reinforcement.</p>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <div class="h-48 overflow-hidden rounded-2xl mb-6"><img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/roofing-service.jpg" class="h-48 object-cover"></div>
                <h4 class="font-black uppercase text-xs italic">Roofing Elite Service</h4>
                <p class="text-[10px] text-slate-400 font-bold uppercase mt-2">Lifetime Structural Warranty.</p>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <div class="h-48 overflow-hidden rounded-2xl mb-6"><img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/solar-service.jpg" class="h-48 object-cover"></div>
                <h4 class="font-black uppercase text-xs italic">Residential Solar Matrix</h4>
                <p class="text-[10px] text-slate-400 font-bold uppercase mt-2">Net Zero Federal Rebates.</p>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <div class="h-48 overflow-hidden rounded-2xl mb-6"><img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/kitchen-service.jpg" class="h-48 object-cover"></div>
                <h4 class="font-black uppercase text-xs italic">Kitchen Remodeling</h4>
                <p class="text-[10px] text-slate-400 font-bold uppercase mt-2">Premium Structural Modernization.</p>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <div class="h-48 overflow-hidden rounded-2xl mb-6"><img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/bathroom-service.jpg" class="h-48 object-cover"></div>
                <h4 class="font-black uppercase text-xs italic">Bathroom Remodeling</h4>
                <p class="text-[10px] text-slate-400 font-bold uppercase mt-2">Elite Matrix Finishes.</p>
            </div>
            <div class="feature-card p-6" onclick="document.getElementById('portal').scrollIntoView()">
                <div class="h-48 overflow-hidden rounded-2xl mb-6"><img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/deck-service.jpg" class="h-48 object-cover"></div>
                <h4 class="font-black uppercase text-xs italic">Deck Remodeling</h4>
                <p class="text-[10px] text-slate-400 font-bold uppercase mt-2">Outdoor Modernization Systems.</p>
            </div>
            <div class="feature-card p-6 lg:col-span-1 lg:ml-auto" onclick="document.getElementById('portal').scrollIntoView()">
                <div class="h-48 overflow-hidden rounded-2xl mb-6"><img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/garage-service.jpg" class="h-48 object-cover"></div>
                <h4 class="font-black uppercase text-xs italic">Garage Matrix</h4>
                <p class="text-[10px] text-slate-400 font-bold uppercase mt-2">Organisation & EV Integration.</p>
            </div>
        </div>
    </section>

    <footer class="bg-slate-900 border-t border-white/5 pt-24 pb-12 text-white/70 px-6">
        <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-16 text-center md:text-left">
            <div>
                <img src="https://raw.githubusercontent.com/Anum786/Ushome/main/assets/img/logo.png" alt="Logo" class="h-10 mx-auto md:mx-0 mb-6">
                <p class="text-[11px] font-bold leading-relaxed uppercase">U.S. Home Improvements is a national modernization matrix, providing elite structural modernization, energy independence, and structural security for American homeowners.</p>
            </div>
            <div>
                <h5 class="font-black italic uppercase mb-6 text-sm tracking-widest text-white">National Privacy</h5>
                <p class="text-[11px] font-bold leading-relaxed uppercase">Data stream is end-to-end encrypted. Information provided in this qualification matrix is used solely for contractor matching across all 50 states.</p>
            </div>
            <div>
                <h5 class="font-black italic uppercase mb-6 text-sm tracking-widest text-white">Coverage Matrix</h5>
                <p class="text-[11px] font-bold leading-relaxed uppercase">Active network operations in California, Texas, Florida, New York, and all continental U.S. jurisdictions. Certified Elite Contractors only.</p>
            </div>
        </div>
        <div class="text-center mt-24 opacity-30 text-[9px] font-black uppercase tracking-[0.5em]">
            U.S. HOME IMPROVEMENTS • NATIONAL NETWORK ENTERPRISE • 2026
        </div>
    </footer>

    <div id="adminHQ" class="fixed inset-0 bg-slate-950 z-[5000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-7xl mx-auto py-10">
            <div class="flex justify-between items-center mb-16 border-b border-white/10 pb-8">
                <h2 class="text-3xl font-black italic text-cyan-400 uppercase tracking-tight">HQ Global Lead Matrix</h2>
                <button onclick="location.reload()" class="bg-red-500/20 text-red-500 border border-red-500/20 px-8 py-2 rounded-full text-[10px] font-black uppercase">DISCONNECT</button>
            </div>
            <div id="loginGate" class="max-w-xs mx-auto py-20 text-center">
                <input type="password" id="adminPin" class="w-full p-6 bg-white/5 border border-white/10 rounded-2xl text-center text-4xl mb-4 outline-none focus:border-cyan-400" placeholder="KEY">
                <button onclick="unlockHQ()" class="btn-elite bg-cyan-500 text-slate-900">VERIFY ID</button>
            </div>
            <div id="dash" class="hidden grid md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
        </div>
    </div>

    <script>
        // Firebase Configuration (STAY SECURE)
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

        // Step Navigation Logic
        function goNext(nextId) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(nextId).classList.add('active');
            window.scrollTo({ top: document.getElementById('portal').offsetTop - 50, behavior: 'smooth' });
        }

        // Window Count Toggle Logic
        function handleServiceSelection() {
            const svc = document.getElementById('service').value;
            document.getElementById('winDiv').classList.toggle('hidden', svc !== 'Windows');
        }

        // Form Submission Matrix
        document.getElementById('masterLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const leadData = {
                name: document.getElementById('cName').value,
                age: document.getElementById('cAge').value,
                phone: document.getElementById('cPhone').value,
                address: document.getElementById('cAddr').value,
                state: document.getElementById('cState').value,
                zip: document.getElementById('cZip').value,
                owner: document.getElementById('homeowner').value,
                service: document.getElementById('service').value,
                windows: document.getElementById('winCount').value || 'N/A',
                readiness: document.getElementById('ready').value,
                credit: document.getElementById('credit').value,
                date: document.getElementById('appDate').value,
                time: document.getElementById('appTime').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(leadData).then(() => {
                alert("QUALIFIED! Your application has been authorised.");
                location.reload();
            });
        });

        // HQ Access Logic (5 Taps)
        let taps = 0, last = 0;
        document.addEventListener('click', () => {
            const now = Date.now();
            if(now - last < 400) taps++; else taps = 1; last = now;
            if(taps === 5) document.getElementById('adminHQ').classList.remove('hidden');
        });

        function unlockHQ() {
            if(document.getElementById('adminPin').value === "ADMIN@786#") {
                document.getElementById('loginGate').classList.add('hidden');
                document.getElementById('dash').classList.remove('hidden');
                syncLeads();
            } else { alert("ACCESS DENIED"); }
        }

        // Sync Leads Data Matrix
        function syncLeads() {
            db.ref('leads').on('value', snap => {
                const data = snap.val();
                let h = '';
                for(let k in data) {
                    h = `<div class="bg-white/5 border-l-4 border-cyan-400 p-8 rounded-r-3xl relative group">
                        <div class="flex justify-between items-start mb-6">
                            <div>
                                <h4 class="font-black italic uppercase text-xl">${data[k].name} (${data[k].age})</h4>
                                <p class="text-cyan-400 text-[10px] font-black uppercase tracking-widest">${data[k].service} | Owner: ${data[k].owner}</p>
                            </div>
                            <span class="text-[9px] font-bold text-gray-500">${data[k].state}</span>
                        </div>
                        <div class="space-y-3 text-[11px] text-gray-400 font-bold italic uppercase">
                            <p>📞 Contact: ${data[k].phone}</p>
                            <p>🏠 Address: ${data[k].address} (Zip: ${data[k].zip})</p>
                            <div class="grid grid-cols-2 gap-4 mt-6">
                                <div class="bg-white/5 p-4 rounded-xl border border-white/5 text-white">
                                    <p class="text-[8px] opacity-50 mb-1">Credit Score</p>
                                    ${data[k].credit}
                                </div>
                                <div class="bg-white/5 p-4 rounded-xl border border-white/5 text-white">
                                    <p class="text-[8px] opacity-50 mb-1">Readiness</p>
                                    ${data[k].readiness}
                                </div>
                            </div>
                            <div class="bg-cyan-500/10 p-4 rounded-xl mt-4 border border-cyan-500/10 text-cyan-400">
                                <p class="text-[8px] opacity-50 mb-1">APPOINTMENT Matrix</p>
                                ${data[k].date} @ ${data[k].time}
                            </div>
                        </div>
                        <button onclick="db.ref('leads/${k}').remove()" class="absolute top-4 right-4 opacity-0 group-hover:opacity-100 text-[8px] text-red-500">DELETE</button>
                    </div>` + h;
                }
                document.getElementById('dash').innerHTML = h || 'No Leads Stream detected.';
            });
        }
    </script>
</body>
</html>
