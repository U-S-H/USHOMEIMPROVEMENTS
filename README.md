<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Enterprise</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --neon: #00f2ff; --dark: #020408; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; overflow-x: hidden; scroll-behavior: smooth; }
        
        /* Premium Background Animation */
        .blob { position: absolute; width: 400px; height: 400px; background: rgba(0, 242, 255, 0.07); filter: blur(100px); border-radius: 50%; z-index: -1; animation: move 20s infinite alternate; }
        @keyframes move { from { transform: translate(-10%, -10%); } to { transform: translate(20%, 20%); } }

        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 2rem; }
        .neon-glow { border: 1px solid rgba(0, 242, 255, 0.2); transition: 0.5s; }
        .neon-glow:hover { border-color: var(--neon); box-shadow: 0 0 30px rgba(0, 242, 255, 0.2); }

        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.6s ease forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        .progress-bar { height: 6px; background: rgba(255,255,255,0.05); border-radius: 10px; overflow: hidden; }
        .progress-fill { height: 100%; background: linear-gradient(90deg, #00f2ff, #0061ff); width: 15%; transition: 0.8s ease; }

        .btn-opt { width: 100%; padding: 1.5rem; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.05); border-radius: 1.5rem; text-align: left; transition: 0.3s; display: flex; justify-content: space-between; align-items: center; }
        .btn-opt:hover { background: rgba(0, 242, 255, 0.1); border-color: var(--neon); transform: scale(1.02); }

        input[type=range] { -webkit-appearance: none; width: 100%; background: transparent; }
        input[type=range]::-webkit-slider-runnable-track { height: 8px; background: rgba(255,255,255,0.1); border-radius: 5px; }
        input[type=range]::-webkit-slider-thumb { -webkit-appearance: none; height: 24px; width: 24px; border-radius: 50%; background: var(--neon); cursor: pointer; margin-top: -8px; box-shadow: 0 0 15px var(--neon); }
    </style>
</head>
<body>

    <div class="blob" style="top: 0; left: 0;"></div>
    <div class="blob" style="bottom: 0; right: 0; background: rgba(0, 97, 255, 0.05);"></div>

    <nav class="sticky top-0 z-50 p-6">
        <div class="max-w-7xl mx-auto glass px-8 py-4 flex justify-between items-center neon-glow" id="headerLogo">
            <div class="flex flex-col">
                <span class="text-2xl font-black tracking-tighter italic">U.S. HOME IMPROVEMENTS</span>
                <span class="text-[8px] text-cyan-400 font-bold uppercase tracking-[0.4em]">Official Enterprise Portal</span>
            </div>
            <a href="#portal" class="bg-cyan-600 px-6 py-2 rounded-full text-[10px] font-black uppercase tracking-widest hover:bg-cyan-400 transition">Get Estimate</a>
        </div>
    </nav>

    <section class="py-20 text-center px-6">
        <div class="inline-block px-4 py-1.5 border border-cyan-500/30 rounded-full text-[9px] font-black text-cyan-400 uppercase tracking-widest mb-8">Serving All 50 States</div>
        <h1 class="text-6xl md:text-9xl font-black mb-8 tracking-tighter leading-none italic">Quality.<br><span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-600">Reimagined.</span></h1>
    </section>

    <section id="portal" class="max-w-xl mx-auto px-6 pb-20">
        <div class="mb-8">
            <div class="flex justify-between text-[10px] font-bold text-cyan-500 uppercase tracking-widest mb-2">
                <span id="stepLabel">Project Selection</span>
                <span id="stepCount">Step 1 of 6</span>
            </div>
            <div class="progress-bar"><div class="progress-fill" id="fillBar"></div></div>
        </div>

        <div class="glass p-10 neon-glow">
            <form id="masterForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black mb-8 uppercase italic">01. Service Type</h2>
                    <div class="space-y-3">
                        <button type="button" onclick="next(2, 'service', 'Windows')" class="btn-opt"><span>🪟 Windows & Doors</span> <span>→</span></button>
                        <button type="button" onclick="next(2, 'service', 'Roofing')" class="btn-opt"><span>🏠 Roofing & Gutters</span> <span>→</span></button>
                        <button type="button" onclick="next(2, 'service', 'Solar')" class="btn-opt"><span>☀️ Solar Energy</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black mb-2 uppercase italic">02. Credit Standing</h2>
                    <p class="text-gray-500 text-[10px] mb-10 tracking-widest uppercase font-bold text-center">Eligibility Verification</p>
                    <div class="text-center py-6">
                        <span id="scoreVal" class="text-6xl font-black text-cyan-400">700</span>
                        <p class="text-xs text-gray-500 mt-4 font-bold uppercase tracking-widest" id="scoreGrade">Excellent</p>
                    </div>
                    <input type="range" min="300" max="850" value="700" step="10" oninput="updateScore(this.value)" class="mb-10">
                    <button type="button" onclick="next(3, 'credit', document.getElementById('scoreVal').innerText)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase tracking-widest">Confirm Score</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black mb-8 uppercase italic">03. Ownership</h2>
                    <div class="space-y-3">
                        <button type="button" onclick="next(4, 'ownership', 'Owner')" class="btn-opt"><span>🏠 I Own This Home</span> <span>→</span></button>
                        <button type="button" onclick="next(4, 'ownership', 'Renter')" class="btn-opt"><span>🏢 I Am Renting</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-2xl font-black mb-8 uppercase italic">04. Timeframe</h2>
                    <div class="space-y-3">
                        <button type="button" onclick="next(5, 'time', 'Urgent')" class="btn-opt"><span>🚀 Immediately</span> <span>→</span></button>
                        <button type="button" onclick="next(5, 'time', '1-3 Months')" class="btn-opt"><span>📅 1-3 Months</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step5">
                    <h2 class="text-2xl font-black mb-8 italic uppercase text-cyan-400">05. Area Code</h2>
                    <input type="number" id="zip" placeholder="Zip Code" class="w-full p-6 bg-white/5 border border-white/10 rounded-2xl mb-8 outline-none text-3xl font-bold tracking-tighter">
                    <button type="button" onclick="next(6)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase tracking-widest">Verify Coverage</button>
                </div>

                <div class="step" id="step6">
                    <h2 class="text-2xl font-black mb-2 italic text-cyan-400 uppercase">06. Verification</h2>
                    <p class="text-gray-500 text-[9px] mb-10 tracking-[0.3em] font-bold uppercase text-center">Secure Data Encrypted</p>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none">
                        <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none">
                        <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg shadow-green-900/40">Get My Quotes</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 py-20 grid md:grid-cols-3 gap-10">
        <div class="glass overflow-hidden neon-glow group">
            <img src="https://images.pexels.com/photos/277559/pexels-photo-277559.jpeg?auto=compress&cs=tinysrgb&w=600" class="w-full h-64 object-cover" alt="Windows">
            <div class="p-8"><h3 class="font-bold uppercase italic">Elite Windows</h3><p class="text-xs text-gray-500 mt-2 uppercase tracking-widest">Energy Efficient Matrix</p></div>
        </div>
        <div class="glass overflow-hidden neon-glow group">
            <img src="https://images.pexels.com/photos/1080721/pexels-photo-1080721.jpeg?auto=compress&cs=tinysrgb&w=600" class="w-full h-64 object-cover" alt="Kitchen">
            <div class="p-8"><h3 class="font-bold uppercase italic">Luxury Remodels</h3><p class="text-xs text-gray-500 mt-2 uppercase tracking-widest">High-End Engineering</p></div>
        </div>
        <div class="glass overflow-hidden neon-glow group">
            <img src="https://images.pexels.com/photos/356036/pexels-photo-356036.jpeg?auto=compress&cs=tinysrgb&w=600" class="w-full h-64 object-cover" alt="Solar">
            <div class="p-8"><h3 class="font-bold uppercase italic">Solar Systems</h3><p class="text-xs text-gray-500 mt-2 uppercase tracking-widest">Grid-Free Solutions</p></div>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 z-[200] bg-black/98 backdrop-blur-2xl p-6 hidden">
        <div class="max-w-2xl mx-auto mt-20">
            <h2 class="text-4xl font-black italic text-cyan-400 mb-10 uppercase tracking-tighter">Mission Control</h2>
            <div id="keyBox">
                <input type="password" id="adminKey" placeholder="Access Key" class="w-full p-6 bg-white/5 border border-white/10 rounded-2xl outline-none text-center text-3xl tracking-[0.5em] mb-6">
                <button onclick="unlock()" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase">Authorize Access</button>
            </div>
            <div id="leadsList" class="hidden space-y-4">
                <p class="text-cyan-500 font-bold animate-pulse">Scanning leads...</p>
            </div>
            <button onclick="document.getElementById('adminPortal').classList.add('hidden')" class="mt-10 text-gray-600 font-bold uppercase text-[10px] tracking-widest">Close System</button>
        </div>
    </div>

    <footer class="py-20 text-center opacity-40">
        <p class="text-xl font-black italic mb-4">U.S. HOME IMPROVEMENTS</p>
        <p class="text-[8px] uppercase tracking-[0.5em]">License #US-770821-B | ushomeimprovement07@gmail.com</p>
    </footer>

    <script>
        let leadData = {};
        
        // Qualification System Logic
        function updateScore(v) {
            document.getElementById('scoreVal').innerText = v;
            document.getElementById('scoreGrade').innerText = v > 740 ? "Excellent 💎" : v > 670 ? "Good ✅" : "Fair ⚠️";
        }

        function next(s, k, v) {
            if(k) leadData[k] = v;
            const labels = ["Service", "Credit", "Ownership", "Timeframe", "Zip", "Verify"];
            document.getElementById('fillBar').style.width = (s/6)*100 + '%';
            document.getElementById('stepCount').innerText = `Step ${s} of 6`;
            document.getElementById('stepLabel').innerText = labels[s-1];
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }

        // Tap-Tap Secret Admin (5 fast clicks anywhere)
        let t = 0, l = 0;
        document.addEventListener('click', () => {
            const n = Date.now();
            if(n - l < 400) t++; else t = 1;
            l = n;
            if(t === 5) { document.getElementById('adminPortal').classList.remove('hidden'); t = 0; }
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('keyBox').classList.add('hidden');
                document.getElementById('leadsList').classList.remove('hidden');
                document.getElementById('leadsList').innerHTML = `<div class="glass p-6 border-l-4 border-cyan-500"><p class="font-bold">LIVE LEAD CAPTURE ACTIVE</p><p class="text-xs text-gray-500">Wait for customer entries...</p></div>`;
            } else { alert("ACCESS DENIED!"); }
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            alert("Congratulations Sweetie! Your project is qualified. 🚀");
            location.reload();
        });
    </script>
</body>
</html>
