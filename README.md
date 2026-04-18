<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Enterprise Lead Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --dark: #020408; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; overflow-x: hidden; scroll-behavior: smooth; }
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 2rem; }
        .neon-glow { border: 1px solid rgba(0, 242, 255, 0.2); transition: 0.5s; }
        .neon-glow:hover { border-color: var(--neon); box-shadow: 0 0 30px rgba(0, 242, 255, 0.2); }
        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.6s ease forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        .progress-fill { height: 100%; background: linear-gradient(90deg, #00f2ff, #0061ff); width: 15%; transition: 0.8s ease; }
        .btn-opt { width: 100%; padding: 1.25rem; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.05); border-radius: 1.5rem; text-align: left; transition: 0.3s; display: flex; justify-content: space-between; align-items: center; }
        .btn-opt:hover { background: rgba(0, 242, 255, 0.1); border-color: var(--neon); transform: scale(1.02); }
        input[type=range] { -webkit-appearance: none; width: 100%; background: transparent; }
        input[type=range]::-webkit-slider-runnable-track { height: 8px; background: rgba(255,255,255,0.1); border-radius: 5px; }
        input[type=range]::-webkit-slider-thumb { -webkit-appearance: none; height: 24px; width: 24px; border-radius: 50%; background: var(--neon); cursor: pointer; margin-top: -8px; box-shadow: 0 0 15px var(--neon); }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-50 p-6">
        <div class="max-w-7xl mx-auto glass px-8 py-4 flex justify-between items-center neon-glow">
            <div class="flex flex-col">
                <span class="text-2xl font-black tracking-tighter italic">U.S. HOME IMPROVEMENTS</span>
                <span class="text-[8px] text-cyan-400 font-bold uppercase tracking-[0.4em]">National Qualified Network</span>
            </div>
            <a href="#portal" class="bg-cyan-600 px-6 py-2 rounded-full text-[10px] font-black uppercase tracking-widest">Get Free Quotes</a>
        </div>
    </nav>

    <section id="portal" class="max-w-xl mx-auto px-6 py-10">
        <div class="mb-8">
            <div class="flex justify-between text-[10px] font-bold text-cyan-500 uppercase tracking-widest mb-2">
                <span id="stepLabel">Project Selection</span>
                <span id="stepCount">Step 1 of 6</span>
            </div>
            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="progress-fill" id="fillBar"></div></div>
        </div>

        <div class="glass p-8 md:p-10 neon-glow">
            <form id="masterForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black mb-6 uppercase italic">01. What is your project?</h2>
                    <div class="space-y-3">
                        <button type="button" onclick="next(2, 'service', 'Windows')" class="btn-opt"><span>🪟 Windows & Doors</span> <span>→</span></button>
                        <button type="button" onclick="next(2, 'service', 'Roofing')" class="btn-opt"><span>🏠 Roofing & Gutters</span> <span>→</span></button>
                        <button type="button" onclick="next(2, 'service', 'Solar')" class="btn-opt"><span>☀️ Solar Energy</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black mb-2 uppercase italic text-center">02. Credit Score</h2>
                    <div class="text-center py-6">
                        <span id="scoreVal" class="text-6xl font-black text-cyan-400">700</span>
                        <p class="text-xs text-gray-500 mt-4 font-bold uppercase tracking-widest" id="scoreGrade">Excellent</p>
                    </div>
                    <input type="range" min="300" max="850" value="700" step="10" oninput="updateScore(this.value)" class="mb-10">
                    <button type="button" onclick="next(3, 'credit', document.getElementById('scoreVal').innerText)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase">Next Step</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black mb-8 uppercase italic">03. Property Owner?</h2>
                    <div class="space-y-3">
                        <button type="button" onclick="next(4, 'ownership', 'Owner')" class="btn-opt"><span>🏠 Yes, I am the owner</span> <span>→</span></button>
                        <button type="button" onclick="next(4, 'ownership', 'Renter')" class="btn-opt"><span>🏢 No, I am renting</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-2xl font-black mb-8 uppercase italic">04. Timeframe</h2>
                    <div class="space-y-3">
                        <button type="button" onclick="next(5, 'time', 'Immediately')" class="btn-opt"><span>🚀 Immediately</span> <span>→</span></button>
                        <button type="button" onclick="next(5, 'time', '1-3 Months')" class="btn-opt"><span>📅 1-3 Months</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step5">
                    <h2 class="text-2xl font-black mb-6 italic uppercase text-cyan-400">05. Zip Code</h2>
                    <input type="number" id="zip" placeholder="Zip Code" class="w-full p-6 bg-white/5 border border-white/10 rounded-2xl mb-8 outline-none text-2xl font-bold">
                    <button type="button" onclick="next(6)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase">Check Coverage</button>
                </div>

                <div class="step" id="step6">
                    <h2 class="text-2xl font-black mb-6 italic text-cyan-400 uppercase">06. Final Verification</h2>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none mb-4">
                    <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none mb-10">
                    <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-black uppercase">Get My Free Quotes</button>
                </div>
            </form>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 z-[200] bg-black/95 backdrop-blur-xl p-6 hidden overflow-y-auto">
        <div class="max-w-3xl mx-auto pt-10">
            <div class="flex justify-between items-center mb-10">
                <h2 class="text-3xl font-black italic text-cyan-400">ADMIN DASHBOARD</h2>
                <button onclick="location.reload()" class="text-gray-500 font-bold uppercase text-xs">Exit</button>
            </div>
            <div id="loginBox">
                <input type="password" id="adminKey" placeholder="Secret Key" class="w-full p-6 bg-white/5 border border-white/10 rounded-2xl outline-none text-center text-2xl tracking-[0.5em] mb-6">
                <button onclick="unlock()" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase">Unlock Leads</button>
            </div>
            <div id="leadsContainer" class="hidden space-y-4">
                <p class="text-cyan-500 animate-pulse font-bold uppercase tracking-widest text-xs">Syncing Live Leads...</p>
                <div id="leadsList"></div>
            </div>
        </div>
    </div>

    <script>
        // FIREBASE CONFIG
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

        let leadData = {};

        function updateScore(v) {
            document.getElementById('scoreVal').innerText = v;
            document.getElementById('scoreGrade').innerText = v > 740 ? "Excellent 💎" : v > 670 ? "Good ✅" : "Fair ⚠️";
        }

        function next(s, k, v) {
            if(k) leadData[k] = v;
            document.getElementById('fillBar').style.width = (s/6)*100 + '%';
            document.getElementById('stepCount').innerText = `Step ${s} of 6`;
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            leadData.name = document.getElementById('name').value;
            leadData.phone = document.getElementById('phone').value;
            leadData.zip = document.getElementById('zip').value;
            leadData.timestamp = new Date().toLocaleString();

            db.ref('leads').push(leadData).then(() => {
                alert("Success sweetie! Your request is submitted. 🚀");
                location.reload();
            });
        });

        // Tap-Tap Admin Secret (5 fast clicks)
        let t = 0, l = 0;
        document.addEventListener('click', () => {
            if(Date.now() - l < 400) t++; else t = 1;
            l = Date.now();
            if(t === 5) { document.getElementById('adminPortal').classList.remove('hidden'); t = 0; }
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('leadsContainer').classList.remove('hidden');
                
                db.ref('leads').on('value', (snap) => {
                    const data = snap.val();
                    let html = '';
                    for(let id in data) {
                        html = `
                        <div class="glass p-6 border-l-4 border-cyan-500 mb-4">
                            <div class="flex justify-between items-start mb-2">
                                <p class="font-black text-xl italic">${data[id].name}</p>
                                <span class="text-[10px] bg-cyan-900/50 px-3 py-1 rounded-full text-cyan-400 font-bold">${data[id].service}</span>
                            </div>
                            <p class="text-sm text-gray-400">📞 ${data[id].phone} | 📍 ${data[id].zip}</p>
                            <div class="mt-4 flex gap-4 text-[9px] uppercase font-bold text-gray-500 tracking-widest">
                                <span>Credit: ${data[id].credit}</span>
                                <span>Owner: ${data[id].ownership}</span>
                                <span>Time: ${data[id].time}</span>
                            </div>
                        </div>` + html;
                    }
                    document.getElementById('leadsList').innerHTML = html || '<p class="text-gray-600">No leads yet, sweetie.</p>';
                });
            } else { alert("ACCESS DENIED!"); }
        }
    </script>
</body>
</html>
