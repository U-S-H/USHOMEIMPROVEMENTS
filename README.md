<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Premium Contractor Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <script src="https://unpkg.com/@lottiefiles/lottie-player@latest/dist/lottie-player.js"></script>
    <style>
        :root { --accent: #3b82f6; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #030406; color: white; overflow-x: hidden; }
        
        /* Premium Background Animation */
        .blob { position: absolute; width: 400px; height: 400px; background: rgba(59, 130, 246, 0.15); filter: blur(100px); border-radius: 50%; z-index: -1; animation: move 20s infinite alternate; }
        @keyframes move { from { transform: translate(-10%, -10%); } to { transform: translate(20%, 20%); } }

        .glass { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.08); transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        .glass:hover { background: rgba(255, 255, 255, 0.06); border-color: var(--accent); transform: translateY(-5px); }
        
        .step { display: none; }
        .step.active { display: block; animation: slideIn 0.6s ease forwards; }
        @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }

        .premium-btn { background: linear-gradient(135deg, #2563eb 0%, #3b82f6 100%); position: relative; overflow: hidden; }
        .premium-btn::after { content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%; background: rgba(255,255,255,0.1); transform: rotate(45deg); transition: 0.5s; }
        .premium-btn:hover::after { left: 120%; }

        .stat-card { border-left: 2px solid var(--accent); }
    </style>
</head>
<body>

    <div class="blob" style="top: 0; left: 0;"></div>
    <div class="blob" style="bottom: 0; right: 0; background: rgba(37, 99, 235, 0.1);"></div>

    <div class="w-full py-2 bg-blue-600/10 border-b border-blue-500/20 text-center">
        <p class="text-[10px] font-bold tracking-[0.3em] text-blue-400 uppercase">Verified State Licensed & A+ BBB Accredited Network</p>
    </div>

    <nav class="sticky top-0 z-50 glass mx-4 my-4 rounded-2xl px-6 py-4 flex justify-between items-center">
        <div class="flex flex-col">
            <span class="text-xl font-extrabold tracking-tighter text-blue-500">U.S. HOME IMPROVEMENTS</span>
            <span class="text-[8px] text-gray-500 font-bold tracking-widest uppercase">Reg #US-770821-B</span>
        </div>
        <div class="hidden md:flex gap-8 text-[10px] font-bold uppercase tracking-widest text-gray-400">
            <a href="#quote" class="hover:text-white transition">Services</a>
            <a href="#trust" class="hover:text-white transition">Trust Centers</a>
            <a href="mailto:ushomeimprovement07@gmail.com" class="hover:text-white transition">Support</a>
        </div>
        <a href="#quote" class="premium-btn px-6 py-2.5 rounded-xl text-[10px] font-bold uppercase tracking-widest">Free Estimate</a>
    </nav>

    <section class="relative pt-20 pb-12 px-6 text-center">
        <div class="inline-block px-4 py-1.5 glass rounded-full text-blue-400 text-[9px] font-bold mb-8 tracking-widest uppercase border-blue-500/30">Built for American Homeowners</div>
        <h1 class="text-6xl md:text-8xl font-extrabold mb-8 tracking-tighter leading-none">Modern Homes.<br><span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600">Expert Hands.</span></h1>
        <p class="text-gray-400 max-w-2xl mx-auto text-lg mb-12 leading-relaxed">Connect with premium, licensed, and background-checked contractors for elite home transformations.</p>
        
        <div class="flex justify-center gap-4 md:gap-12 flex-wrap">
            <div class="stat-card px-6 py-2 text-left"><p class="text-2xl font-bold italic">45k+</p><p class="text-[9px] uppercase tracking-widest text-gray-500">Projects Done</p></div>
            <div class="stat-card px-6 py-2 text-left"><p class="text-2xl font-bold italic">A+ Rating</p><p class="text-[9px] uppercase tracking-widest text-gray-500">BBB Accredited</p></div>
            <div class="stat-card px-6 py-2 text-left"><p class="text-2xl font-bold italic">100%</p><p class="text-[9px] uppercase tracking-widest text-gray-500">Insured Pros</p></div>
        </div>
    </section>

    <section id="quote" class="py-20 px-6">
        <div class="max-w-xl mx-auto glass p-10 md:p-14 rounded-[3.5rem] shadow-3xl border-t-2 border-blue-500/50">
            <form id="premiumForm">
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-extrabold mb-2 italic">Select Project</h2>
                    <p class="text-gray-500 text-sm mb-10 tracking-wide">Select your primary category</p>
                    <div class="space-y-4">
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="w-full glass p-6 rounded-3xl text-left flex justify-between items-center group">
                            <span class="font-bold tracking-tight">🏠 Roofing & Exterior</span>
                            <span class="text-blue-500 group-hover:translate-x-2 transition">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="w-full glass p-6 rounded-3xl text-left flex justify-between items-center group">
                            <span class="font-bold tracking-tight">☀️ Solar & Energy</span>
                            <span class="text-blue-500 group-hover:translate-x-2 transition">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Kitchen', 2)" class="w-full glass p-6 rounded-3xl text-left flex justify-between items-center group">
                            <span class="font-bold tracking-tight">🛁 Premium Remodeling</span>
                            <span class="text-blue-500 group-hover:translate-x-2 transition">→</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-3xl font-extrabold mb-8 italic">Project Location</h2>
                    <div class="space-y-6">
                        <input type="text" id="zip" placeholder="Zip Code" class="w-full p-5 glass rounded-2xl outline-none focus:ring-2 ring-blue-500 transition">
                        <select id="state" class="w-full p-5 glass rounded-2xl outline-none bg-[#0a0c10]">
                            <option value="">Select State</option>
                            <option value="TX">Texas</option><option value="CA">California</option><option value="FL">Florida</option><option value="NY">New York</option>
                        </select>
                        <button type="button" onclick="move(3)" class="w-full premium-btn p-5 rounded-2xl font-bold uppercase tracking-widest">Verify Area</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-extrabold mb-2 italic">Final Security</h2>
                    <p class="text-gray-500 text-sm mb-10">Verification required for licensed quotes.</p>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" class="w-full p-5 glass rounded-2xl outline-none">
                        <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 glass rounded-2xl outline-none">
                        <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-bold uppercase tracking-widest hover:bg-green-500 transition">Secure Estimates</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section id="trust" class="py-24 max-w-6xl mx-auto px-6 grid md:grid-cols-2 gap-12">
        <div class="glass p-10 rounded-[3rem]">
            <h4 class="text-xl font-extrabold mb-4 italic text-blue-400 underline">Compliance Checked</h4>
            <p class="text-gray-500 text-sm leading-relaxed">Every professional in our network is audited for Active State Licenses and General Liability Insurance (Minimum $1M Coverage). We handle the verification so you don't have to.</p>
        </div>
        <div class="glass p-10 rounded-[3rem]">
            <h4 class="text-xl font-extrabold mb-4 italic text-blue-400 underline">Consumer Protection</h4>
            <p class="text-gray-500 text-sm leading-relaxed">Operating under National Business Standards, we ensure fair pricing through competitive quoting—allowing homeowners to save up to 40% on labor costs.</p>
        </div>
    </section>

    <footer class="py-20 border-t border-white/5 px-6">
        <div class="max-w-6xl mx-auto flex flex-col md:flex-row justify-between items-center gap-12">
            <div class="text-center md:text-left">
                <p class="text-2xl font-extrabold text-blue-500 tracking-tighter mb-4">U.S. HOME IMPROVEMENTS</p>
                <div class="flex gap-4 grayscale opacity-40 hover:opacity-100 transition justify-center md:justify-start">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Better_Business_Bureau_logo.svg/1200px-Better_Business_Bureau_logo.svg.png" class="h-6 invert" alt="BBB">
                </div>
            </div>
            <div class="flex flex-col md:items-end">
                <p class="text-[9px] font-bold uppercase tracking-[0.3em] text-gray-500 mb-2">Corporate Support</p>
                <a href="mailto:ushomeimprovement07@gmail.com" class="text-blue-400 text-lg font-bold hover:underline italic">ushomeimprovement07@gmail.com</a>
            </div>
        </div>
        <div class="mt-20 text-center">
            <p class="text-[8px] text-gray-700 font-bold uppercase tracking-[0.5em]">© 2026 U.S. HOME IMPROVEMENTS | NATIONAL LICENSE US-770821-B | 50 STATE COVERAGE</p>
        </div>
    </footer>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getFirestore, collection, addDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

        const firebaseConfig = {
          apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA",
          authDomain: "ushomes07.firebaseapp.com",
          projectId: "ushomes07",
          storageBucket: "ushomes07.firebasestorage.app",
          messagingSenderId: "24299478735",
          appId: "1:24299478735:web:14f41d56809beac56521ba"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        document.getElementById('premiumForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const btn = e.target.querySelector('button[type="submit"]');
            btn.innerText = "Securing Lead...";
            const data = {
                service: document.getElementById('selectedService').value,
                zip: document.getElementById('zip').value,
                state: document.getElementById('state').value,
                name: document.getElementById('name').value,
                phone: document.getElementById('phone').value,
                timestamp: new Date().toLocaleString()
            };
            try {
                await addDoc(collection(db, "leads"), data);
                alert("Verified! A licensed pro will contact you shortly.");
                location.reload();
            } catch(err) { alert("Security Error! Check connection."); }
        });
    </script>

    <script>
        function move(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }
        function setVal(t, v, n) {
            if(!document.getElementById('selectedService')) {
                const h = document.createElement("input"); h.type="hidden"; h.id="selectedService";
                document.getElementById('premiumForm').appendChild(h);
            }
            document.getElementById('selectedService').value = v;
            move(n);
        }
    </script>
</body>
</html>
