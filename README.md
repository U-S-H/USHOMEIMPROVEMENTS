<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Enterprise Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --bg: #f1f5f9; }
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background: linear-gradient(135deg, #e2e8f0 0%, #f8fafc 100%); 
            color: #0f172a; 
            min-height: 100vh;
        }
        .glass-ui { 
            background: rgba(255, 255, 255, 0.7); 
            backdrop-filter: blur(15px); 
            border: 1px solid white; 
            border-radius: 2.5rem; 
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.08); 
        }
        .neon-btn {
            transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border: 2px solid transparent;
        }
        .neon-btn:hover {
            border-color: var(--neon);
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 242, 255, 0.15);
        }
        .step { display: none; }
        .step.active { display: block; animation: scaleUp 0.4s ease-out; }
        @keyframes scaleUp { from { opacity: 0; transform: scale(0.98); } to { opacity: 1; transform: scale(1); } }
        
        .service-img { width: 100%; height: 180px; object-fit: cover; border-radius: 1.5rem; background: #cbd5e1; }
        
        /* Custom Scrollbar for Admin */
        ::-webkit-scrollbar { width: 5px; }
        ::-webkit-scrollbar-thumb { background: var(--neon); border-radius: 10px; }
    </style>
</head>
<body class="p-4 md:p-10">

    <div class="max-w-6xl mx-auto mb-8 flex flex-col md:flex-row justify-between items-center gap-4 px-4">
        <div class="flex items-center gap-3">
            <span class="flex h-3 w-3"><span class="animate-ping absolute inline-flex h-3 w-3 rounded-full bg-cyan-400 opacity-75"></span><span class="relative inline-flex rounded-full h-3 w-3 bg-cyan-500"></span></span>
            <span class="text-[10px] font-extrabold uppercase tracking-[0.2em] text-slate-500">Live Network: All 50 U.S. States Active</span>
        </div>
        <div class="flex gap-6 items-center">
            <img src="https://upload.wikimedia.org/wikipedia/commons/0/07/Better_Business_Bureau_logo.svg" class="h-4 opacity-50">
            <span class="text-[10px] font-black text-blue-600 uppercase border-l pl-6 border-slate-300">ISO 9001 Certified</span>
        </div>
    </div>

    <header class="text-center mb-12">
        <h1 class="text-4xl md:text-5xl font-black italic tracking-tighter text-slate-900">U.S. HOME IMPROVEMENTS</h1>
        <p class="text-[10px] font-bold text-cyan-600 uppercase tracking-[0.5em] mt-3">National Contractor Matrix & Licensing Division</p>
    </header>

    <main class="max-w-2xl mx-auto mb-24">
        <div class="glass-ui p-8 md:p-14 border-t-8 border-cyan-500">
            <form id="matrixForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black mb-8 italic uppercase tracking-tight">01. Select Specific Project</h2>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <button type="button" onclick="next(2, 'service', 'High-Impact Windows')" class="neon-btn p-6 bg-white rounded-3xl text-left font-bold shadow-sm">🪟 Replacement Windows</button>
                        <button type="button" onclick="next(2, 'service', 'Security Entry Doors')" class="neon-btn p-6 bg-white rounded-3xl text-left font-bold shadow-sm">🚪 Professional Doors</button>
                        <button type="button" onclick="next(2, 'service', 'Architectural Roofing')" class="neon-btn p-6 bg-white rounded-3xl text-left font-bold shadow-sm">🏠 Roofing Systems</button>
                        <button type="button" onclick="next(2, 'service', 'Solar Power Matrix')" class="neon-btn p-6 bg-white rounded-3xl text-left font-bold shadow-sm">☀️ Solar Energy</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">02. Regional Assignment</h2>
                    <p class="text-xs font-bold text-slate-400 mb-6 uppercase">Select your state to match with local licensed contractors</p>
                    <select id="userState" class="w-full p-5 bg-white border-2 border-slate-100 rounded-2xl font-bold outline-none mb-6 appearance-none shadow-sm">
                        <option value="">Choose Your State...</option>
                        <option value="AL">Alabama</option><option value="AK">Alaska</option><option value="AZ">Arizona</option><option value="AR">Arkansas</option><option value="CA">California</option><option value="CO">Colorado</option><option value="CT">Connecticut</option><option value="DE">Delaware</option><option value="FL">Florida</option><option value="GA">Georgia</option><option value="HI">Hawaii</option><option value="ID">Idaho</option><option value="IL">Illinois</option><option value="IN">Indiana</option><option value="IA">Iowa</option><option value="KS">Kansas</option><option value="KY">Kentucky</option><option value="LA">Louisiana</option><option value="ME">Maine</option><option value="MD">Maryland</option><option value="MA">Massachusetts</option><option value="MI">Michigan</option><option value="MN">Minnesota</option><option value="MS">Mississippi</option><option value="MO">Missouri</option><option value="MT">Montana</option><option value="NE">Nebraska</option><option value="NV">Nevada</option><option value="NH">New Hampshire</option><option value="NJ">New Jersey</option><option value="NM">New Mexico</option><option value="NY">New York</option><option value="NC">North Carolina</option><option value="ND">North Dakota</option><option value="OH">Ohio</option><option value="OK">Oklahoma</option><option value="OR">Oregon</option><option value="PA">Pennsylvania</option><option value="RI">Rhode Island</option><option value="SC">South Carolina</option><option value="SD">South Dakota</option><option value="TN">Tennessee</option><option value="TX">Texas</option><option value="UT">Utah</option><option value="VT">Vermont</option><option value="VA">Virginia</option><option value="WA">Washington</option><option value="WV">West Virginia</option><option value="WI">Wisconsin</option><option value="WY">Wyoming</option>
                    </select>
                    <button type="button" onclick="validateState()" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase tracking-widest">Verify Coverage</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">03. On-Site Inspection</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                        <div class="space-y-2">
                            <label class="text-[10px] font-black uppercase text-slate-400 ml-2">Preferred Date</label>
                            <input type="date" id="appDate" class="w-full p-4 bg-white border border-slate-100 rounded-xl outline-none font-bold">
                        </div>
                        <div class="space-y-2">
                            <label class="text-[10px] font-black uppercase text-slate-400 ml-2">Time Window</label>
                            <select id="appTime" class="w-full p-4 bg-white border border-slate-100 rounded-xl outline-none font-bold">
                                <option>Morning (8AM-12PM)</option>
                                <option>Afternoon (12PM-4PM)</option>
                                <option>Evening (4PM-7PM)</option>
                            </select>
                        </div>
                    </div>
                    <button type="button" onclick="showStep('step4')" class="w-full bg-slate-900 text-white p-5 rounded-2xl font-black uppercase tracking-widest">Confirm Schedule</button>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">04. Final Submission</h2>
                    <div class="space-y-4">
                        <input type="text" id="userName" placeholder="Full Legal Name" class="w-full p-5 bg-white border border-slate-100 rounded-2xl outline-none font-bold shadow-sm" required>
                        <input type="tel" id="userPhone" placeholder="Mobile Number" class="w-full p-5 bg-white border border-slate-100 rounded-2xl outline-none font-bold shadow-sm" required>
                        <input type="text" id="userAddr" placeholder="Street Address" class="w-full p-5 bg-white border border-slate-100 rounded-2xl outline-none font-bold shadow-sm" required>
                        <button type="submit" class="w-full bg-cyan-500 text-slate-900 p-6 rounded-3xl font-black uppercase text-lg shadow-2xl shadow-cyan-200 mt-4">Confirm Appointment</button>
                    </div>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-6xl mx-auto grid md:grid-cols-4 gap-6 mb-24">
        <div class="glass-ui p-6 neon-btn">
            <img src="https://images.unsplash.com/photo-1512917774080-9991f1c4c750?w=500" class="service-img mb-4">
            <h3 class="font-black italic uppercase text-sm">Window Matrix</h3>
            <p class="text-[9px] font-bold text-slate-500 uppercase mt-2 leading-relaxed">Impact-rated glass with 99.9% UV protection. Energy Star certified.</p>
        </div>
        <div class="glass-ui p-6 neon-btn">
            <img src="https://images.unsplash.com/photo-1513694490325-24b3dc52a21c?w=500" class="service-img mb-4">
            <h3 class="font-black italic uppercase text-sm">Solar Generation</h3>
            <p class="text-[9px] font-bold text-slate-500 uppercase mt-2 leading-relaxed">High-efficiency Tier 1 panels with 25-year production guarantees.</p>
        </div>
        <div class="glass-ui p-6 neon-btn">
            <img src="https://images.unsplash.com/photo-1632759162353-19c9a543fe79?w=500" class="service-img mb-4">
            <h3 class="font-black italic uppercase text-sm">Roofing Elite</h3>
            <p class="text-[9px] font-bold text-slate-500 uppercase mt-2 leading-relaxed">Lifetime architectural shingles with professional weather sealing.</p>
        </div>
        <div class="glass-ui p-6 neon-btn">
            <img src="https://images.unsplash.com/photo-1517581177682-a085bb7ffb15?w=500" class="service-img mb-4">
            <h3 class="font-black italic uppercase text-sm">Entry Systems</h3>
            <p class="text-[9px] font-bold text-slate-500 uppercase mt-2 leading-relaxed">Custom steel & fiberglass doors with multi-point lock security.</p>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 bg-slate-900/98 backdrop-blur-3xl z-[5000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-6xl mx-auto pt-10 pb-20">
            <div class="flex justify-between items-center mb-16 border-b border-white/10 pb-8">
                <div>
                    <h2 class="text-4xl font-black italic text-cyan-400 tracking-tighter">NATIONAL HQ COMMAND</h2>
                    <p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest mt-1 italic">Authorized Data Stream Only</p>
                </div>
                <button onclick="location.reload()" class="bg-red-500/10 text-red-500 border border-red-500/20 px-8 py-3 rounded-full text-[10px] font-black uppercase tracking-widest hover:bg-red-500 hover:text-white transition">Terminate</button>
            </div>

            <div id="loginBox" class="max-w-md mx-auto py-20 text-center">
                <input type="password" id="adminKey" class="w-full p-8 rounded-3xl bg-white/5 border border-white/10 text-center text-4xl mb-8 outline-none focus:border-cyan-500" placeholder="KEY">
                <button onclick="unlock()" class="w-full bg-cyan-600 p-6 rounded-3xl font-black uppercase text-black text-lg shadow-2xl shadow-cyan-500/20">Authorize</button>
            </div>

            <div id="dashboard" class="hidden grid md:grid-cols-2 lg:grid-cols-3 gap-6">
                </div>
        </div>
    </div>

    <footer class="text-center py-16 opacity-30 border-t border-slate-200 mt-20">
        <p class="text-[9px] font-black uppercase tracking-[0.6em]">U.S. Home Improvements Enterprise • 2026 National Licensing Matrix</p>
    </footer>

    <script>
        // Firebase Official Config
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

        // Appointment Date Protection
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('appDate').setAttribute('min', today);

        let lead = { state: 'N/A' };

        function showStep(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function next(s, k, v) {
            if(k) lead[k] = v;
            showStep('step' + s);
        }

        function validateState() {
            const s = document.getElementById('userState').value;
            if(!s) return alert("Please select a state to proceed.");
            lead.state = s;
            showStep('step3');
        }

        document.getElementById('matrixForm').addEventListener('submit', (e) => {
            e.preventDefault();
            lead.name = document.getElementById('userName').value;
            lead.phone = document.getElementById('userPhone').value;
            lead.address = document.getElementById('userAddr').value;
            lead.date = document.getElementById('appDate').value;
            lead.time = document.getElementById('appTime').value;
            lead.timestamp = new Date().toLocaleString();

            db.ref('leads').push(lead).then(() => {
                alert("APPLICATION AUTHORIZED! 🚀\nA National Specialist will contact you to verify your visit on " + lead.date);
                location.reload();
            });
        });

        // HQ SECRET ACCESS (5 Rapid Taps)
        let tCount = 0, lTap = 0;
        document.addEventListener('click', () => {
            const now = Date.now();
            if(now - lTap < 400) tCount++; else tCount = 1;
            lTap = now;
            if(tCount === 5) { document.getElementById('adminPortal').classList.remove('hidden'); tCount = 0; }
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('dashboard').classList.remove('hidden');
                syncMatrix();
            } else { alert("ACCESS DENIED: INVALID KEY"); }
        }

        function syncMatrix() {
            db.ref('leads').on('value', snap => {
                const data = snap.val();
                let html = '';
                for(let id in data) {
                    html = `
                    <div class="bg-white/5 border-l-4 border-cyan-500 p-6 rounded-r-2xl relative group">
                        <div class="flex justify-between items-start mb-4">
                            <div>
                                <h4 class="font-black italic uppercase text-lg leading-tight">${data[id].name}</h4>
                                <p class="text-cyan-400 text-[9px] font-black uppercase tracking-widest mt-1">${data[id].service}</p>
                            </div>
                            <span class="bg-cyan-500 text-slate-900 px-2 py-1 rounded text-[10px] font-black">${data[id].state}</span>
                        </div>
                        <div class="space-y-2 text-[11px] font-bold text-gray-400 italic">
                            <p>📞 Phone: ${data[id].phone}</p>
                            <p>📍 Address: ${data[id].address}</p>
                            <div class="bg-white/5 p-3 rounded-xl mt-4 border border-white/5">
                                <p class="text-white">📅 Visit: ${data[id].date}</p>
                                <p class="text-white">🕒 Slot: ${data[id].time}</p>
                            </div>
                        </div>
                        <button onclick="db.ref('leads/${id}').remove()" class="absolute top-2 right-2 opacity-0 group-hover:opacity-100 text-[8px] bg-red-500/20 text-red-500 px-2 py-1 rounded transition">DELETE</button>
                    </div>` + html;
                }
                document.getElementById('dashboard').innerHTML = html || '<div class="col-span-full text-center py-20 text-gray-700 font-black uppercase tracking-widest">No Incoming Data Stream</div>';
            });
        }
    </script>
</body>
</html>
