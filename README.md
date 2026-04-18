<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Premium Contractor Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --dark: #020408; }
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background: var(--dark); 
            color: white; 
            overflow-x: hidden; 
            scroll-behavior: smooth; 
        }
        
        /* Premium Background Blobs */
        .blob { position: absolute; width: 500px; height: 500px; background: rgba(0, 242, 255, 0.05); filter: blur(120px); border-radius: 50%; z-index: -1; }
        
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(30px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 2.5rem; }
        .neon-glow { border: 1px solid rgba(0, 242, 255, 0.2); transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1); }
        .neon-glow:hover { border-color: var(--neon); box-shadow: 0 0 40px rgba(0, 242, 255, 0.2); transform: translateY(-2px); }

        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.6s cubic-bezier(0.19, 1, 0.22, 1) forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        .btn-opt { 
            width: 100%; padding: 1.5rem; background: rgba(255,255,255,0.03); 
            border: 1px solid rgba(255,255,255,0.05); border-radius: 1.5rem; 
            text-align: left; transition: 0.3s; display: flex; justify-content: space-between; align-items: center; 
        }
        .btn-opt:hover { background: rgba(0, 242, 255, 0.1); border-color: var(--neon); transform: scale(1.02); }

        input, select { background: rgba(255,255,255,0.05) !important; border: 1px solid rgba(255,255,255,0.1) !important; color: white !important; outline: none; }
        input:focus { border-color: var(--neon) !important; box-shadow: 0 0 15px rgba(0, 242, 255, 0.1); }
        
        /* Custom Scrollbar for Admin */
        ::-webkit-scrollbar { width: 5px; }
        ::-webkit-scrollbar-thumb { background: var(--neon); border-radius: 10px; }
    </style>
</head>
<body class="pb-10">

    <div class="blob" style="top: -100px; left: -100px;"></div>
    <div class="blob" style="bottom: -100px; right: -100px; background: rgba(0, 97, 255, 0.05);"></div>

    <nav class="p-6">
        <div class="max-w-7xl mx-auto glass px-8 py-4 flex justify-between items-center neon-glow">
            <div class="leading-none">
                <span class="text-2xl font-black italic tracking-tighter">U.S. HOME IMPROVEMENTS</span>
                <p class="text-[7px] text-cyan-400 font-bold uppercase tracking-[0.5em] mt-1">Certified National Contractor Network</p>
            </div>
            <div class="hidden md:block text-[10px] font-black uppercase tracking-widest text-gray-500">Secure SSL Encrypted Portal</div>
        </div>
    </nav>

    <section id="portal" class="max-w-2xl mx-auto px-6 mt-10">
        <div class="glass p-10 md:p-14 neon-glow relative overflow-hidden">
            <div class="absolute top-0 left-0 w-full h-1 bg-gradient-to-r from-transparent via-cyan-500 to-transparent opacity-50"></div>
            
            <form id="masterForm">
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black mb-2 uppercase italic">01. Project Type</h2>
                    <p class="text-gray-500 text-xs mb-10 uppercase tracking-widest font-bold">Select the service you need</p>
                    <div class="space-y-4">
                        <button type="button" onclick="handleService('Windows')" class="btn-opt group">
                            <span class="font-bold">🪟 WINDOWS & DOORS</span> 
                            <span class="opacity-0 group-hover:opacity-100 transition text-cyan-400">SELECT →</span>
                        </button>
                        <button type="button" onclick="next(3, 'service', 'Roofing')" class="btn-opt group">
                            <span class="font-bold">🏠 ROOFING & GUTTERS</span> 
                            <span class="opacity-0 group-hover:opacity-100 transition text-cyan-400">SELECT →</span>
                        </button>
                        <button type="button" onclick="next(3, 'service', 'Solar')" class="btn-opt group">
                            <span class="font-bold">☀️ SOLAR ENERGY</span> 
                            <span class="opacity-0 group-hover:opacity-100 transition text-cyan-400">SELECT →</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step-windows">
                    <h2 class="text-3xl font-black mb-2 uppercase italic text-cyan-400">02. Quantity</h2>
                    <p class="text-gray-500 text-xs mb-10 uppercase tracking-widest font-bold">How many windows need replacement?</p>
                    <div class="grid grid-cols-2 gap-4">
                        <button type="button" onclick="next(3, 'units', '1-5')" class="btn-opt text-center justify-center">1-5 Units</button>
                        <button type="button" onclick="next(3, 'units', '6-10')" class="btn-opt text-center justify-center">6-10 Units</button>
                        <button type="button" onclick="next(3, 'units', '11-20')" class="btn-opt text-center justify-center">11-20 Units</button>
                        <button type="button" onclick="next(3, 'units', '20+')" class="btn-opt text-center justify-center">20+ Units</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black mb-2 uppercase italic text-cyan-400">03. Timeline</h2>
                    <p class="text-gray-500 text-xs mb-10 uppercase tracking-widest font-bold">When should we start?</p>
                    <div class="space-y-4">
                        <button type="button" onclick="next(4, 'time', 'ASAP / Urgent')" class="btn-opt"><span>🚀 ASAP (READY TO START)</span></button>
                        <button type="button" onclick="next(4, 'time', 'Within 30 Days')" class="btn-opt"><span>📅 WITHIN 30 DAYS</span></button>
                        <button type="button" onclick="next(4, 'time', 'Just Estimates')" class="btn-opt"><span>🔍 JUST GETTING ESTIMATES</span></button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-3xl font-black mb-2 uppercase italic text-cyan-400">04. Location</h2>
                    <p class="text-gray-500 text-xs mb-10 uppercase tracking-widest font-bold">Property address verification</p>
                    <input type="text" id="address" placeholder="Street Address" class="w-full p-6 rounded-2xl mb-4 font-bold">
                    <div class="grid grid-cols-2 gap-4 mb-10">
                        <input type="text" id="city" placeholder="City" class="p-6 rounded-2xl font-bold">
                        <input type="number" id="zip" placeholder="Zip Code" class="p-6 rounded-2xl font-bold">
                    </div>
                    <button type="button" onclick="next(5)" class="w-full bg-cyan-600 p-6 rounded-2xl font-black uppercase tracking-widest shadow-xl">Confirm Address</button>
                </div>

                <div class="step" id="step5">
                    <h2 class="text-3xl font-black mb-2 uppercase italic text-cyan-400">05. Ownership</h2>
                    <p class="text-gray-500 text-xs mb-10 uppercase tracking-widest font-bold">Final verification details</p>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" class="w-full p-6 rounded-2xl font-bold">
                        <input type="email" id="email" placeholder="Email Address" class="w-full p-6 rounded-2xl font-bold">
                        <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-6 rounded-2xl font-bold">
                        <button type="submit" class="w-full bg-green-600 p-6 rounded-2xl font-black uppercase text-xl mt-6 shadow-2xl shadow-green-900/40">Secure My Quotes</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 z-[500] bg-black/98 backdrop-blur-3xl p-6 hidden overflow-y-auto">
        <div class="max-w-6xl mx-auto pt-10 pb-20">
            <div class="flex justify-between items-center mb-16 border-b border-white/10 pb-8">
                <div>
                    <h2 class="text-5xl font-black italic tracking-tighter text-cyan-400">CENTRAL COMMAND</h2>
                    <p class="text-[10px] font-bold text-gray-500 uppercase tracking-[0.5em]">Global Lead Management System</p>
                </div>
                <button onclick="location.reload()" class="bg-white/5 border border-white/10 px-8 py-3 rounded-full font-black text-xs uppercase hover:bg-red-600 transition">Terminate Session</button>
            </div>
            
            <div id="loginBox" class="max-w-md mx-auto py-20">
                <p class="text-center text-gray-600 uppercase text-[10px] font-bold tracking-[0.3em] mb-6">Enter Authorization Key</p>
                <input type="password" id="adminKey" class="w-full p-8 rounded-3xl bg-white/5 border border-white/10 text-center text-4xl tracking-[0.5em] focus:border-cyan-500 mb-8 outline-none">
                <button onclick="unlock()" class="w-full bg-cyan-600 p-6 rounded-3xl font-black uppercase text-lg">Grant Access</button>
            </div>

            <div id="leadsDashboard" class="hidden">
                <div class="grid md:grid-cols-2 gap-6" id="leadsList">
                    </div>
            </div>
        </div>
    </div>

    <script>
        // FIREBASE INITIALIZATION
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

        let leadData = { units: "N/A" };

        function handleService(val) {
            leadData.service = val;
            if(val === 'Windows') {
                showStep('step-windows');
            } else {
                next(3);
            }
        }

        function showStep(id) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo(0, 0);
        }

        function next(s, k, v) {
            if(k) leadData[k] = v;
            showStep('step' + s);
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            leadData.name = document.getElementById('name').value;
            leadData.email = document.getElementById('email').value;
            leadData.phone = document.getElementById('phone').value;
            leadData.address = `${document.getElementById('address').value}, ${document.getElementById('city').value}`;
            leadData.zip = document.getElementById('zip').value;
            leadData.timestamp = new Date().toLocaleString();

            db.ref('leads').push(leadData).then(() => {
                alert("APPLICATION QUALIFIED! 🚀\nOur specialists will contact you shortly.");
                location.reload();
            });
        });

        // SECRET ADMIN TRIGGER (5 FAST CLICKS)
        let tap = 0, last = 0;
        document.addEventListener('click', () => {
            const now = Date.now();
            if(now - last < 400) tap++; else tap = 1;
            last = now;
            if(tap === 5) {
                document.getElementById('adminPortal').classList.remove('hidden');
                tap = 0;
            }
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('leadsDashboard').classList.remove('hidden');
                syncLeads();
            } else { alert("ACCESS DENIED"); }
        }

        function syncLeads() {
            db.ref('leads').on('value', (snap) => {
                const data = snap.val();
                let html = '';
                for(let id in data) {
                    html = `
                    <div class="glass p-8 border-t-4 border-cyan-500 relative group animate-pulse-once">
                        <div class="flex justify-between items-start mb-6">
                            <div>
                                <h4 class="text-3xl font-black italic tracking-tighter">${data[id].name}</h4>
                                <p class="text-cyan-400 font-black text-[10px] uppercase tracking-widest mt-1">${data[id].service} | ${data[id].time}</p>
                            </div>
                            <div class="flex gap-2">
                                <button onclick="copyLead('${id}')" class="bg-cyan-600/20 text-cyan-400 border border-cyan-500/30 px-4 py-2 rounded-xl text-[10px] font-black hover:bg-cyan-600 hover:text-white transition">COPY</button>
                                <button onclick="deleteLead('${id}')" class="bg-red-600/20 text-red-500 border border-red-500/30 px-4 py-2 rounded-xl text-[10px] font-black hover:bg-red-600 hover:text-white transition">DEL</button>
                            </div>
                        </div>
                        <div class="space-y-3 text-sm font-medium">
                            <p class="flex items-center gap-3 text-white/80"><span>📱</span> ${data[id].phone}</p>
                            <p class="flex items-center gap-3 text-white/80"><span>✉️</span> ${data[id].email}</p>
                            <p class="flex items-center gap-3 text-white/80 italic"><span>📍</span> ${data[id].address} (Zip: ${data[id].zip})</p>
                        </div>
                        <div class="mt-6 pt-6 border-t border-white/5 flex justify-between items-center">
                            <span class="text-[9px] text-gray-600 font-bold uppercase tracking-widest">${data[id].timestamp}</span>
                            ${data[id].units !== 'N/A' ? `<span class="bg-yellow-500/10 text-yellow-500 px-3 py-1 rounded-full text-[10px] font-black uppercase">${data[id].units} Windows</span>` : ''}
                        </div>
                        <textarea id="data-${id}" class="hidden">Lead Details:\nName: ${data[id].name}\nPhone: ${data[id].phone}\nEmail: ${data[id].email}\nAddress: ${data[id].address}\nService: ${data[id].service}\nUnits: ${data[id].units}\nTime: ${data[id].time}</textarea>
                    </div>` + html;
                }
                document.getElementById('leadsList').innerHTML = html || '<div class="col-span-2 text-center py-20 text-gray-700 font-black uppercase tracking-widest">Waiting for new leads...</div>';
            });
        }

        function copyLead(id) {
            const el = document.getElementById('data-' + id);
            el.classList.remove('hidden');
            el.select();
            document.execCommand('copy');
            el.classList.add('hidden');
            alert("Lead data successfully exported to clipboard!");
        }

        function deleteLead(id) {
            if(confirm("Permanent Delete? This action cannot be undone.")) {
                db.ref('leads/' + id).remove();
            }
        }
    </script>
</body>
</html>
