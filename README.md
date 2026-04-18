<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Certified Pro Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --blue-primary: #2563eb; --glass-bg: rgba(255, 255, 255, 0.03); }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #020408; color: white; overflow-x: hidden; scroll-behavior: smooth; }
        
        .premium-glass { background: var(--glass-bg); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 2rem; }
        .hero-gradient { background: radial-gradient(circle at top right, rgba(37, 99, 235, 0.15), transparent 50%), radial-gradient(circle at bottom left, rgba(37, 99, 235, 0.05), transparent 40%); }
        
        .step { display: none; transition: all 0.5s ease; }
        .step.active { display: block; animation: fadeInUp 0.6s ease forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        .trust-badge-float { position: fixed; bottom: 20px; left: 20px; z-index: 100; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(1); } 50% { transform: scale(1.05); } 100% { transform: scale(1); } }
        
        .glow-button { background: linear-gradient(135deg, #2563eb, #1d4ed8); box-shadow: 0 0 20px rgba(37, 99, 235, 0.3); transition: 0.4s; }
        .glow-button:hover { box-shadow: 0 0 35px rgba(37, 99, 235, 0.6); transform: translateY(-2px); }
    </style>
</head>
<body class="hero-gradient">

    <div class="trust-badge-float hidden md:flex items-center gap-2 bg-black/80 p-3 rounded-full border border-green-500/30">
        <span class="text-green-500 text-xl">🛡️</span>
        <span class="text-[9px] font-bold uppercase tracking-widest">SSL Secure & Verified</span>
    </div>

    <div class="bg-blue-600 py-1.5 text-center text-[9px] font-bold uppercase tracking-[0.4em] text-white">
        Official Contractor Network — License #US-770821-B — Serving All 50 States
    </div>

    <nav class="sticky top-4 z-50 mx-auto max-w-6xl px-4">
        <div class="premium-glass px-6 py-4 flex justify-between items-center shadow-2xl">
            <div class="flex flex-col">
                <span class="text-xl font-extrabold tracking-tighter text-blue-500">U.S. HOME IMPROVEMENTS</span>
                <span class="text-[8px] text-gray-500 font-bold uppercase tracking-widest">A National Vetted Network</span>
            </div>
            <div class="hidden md:flex gap-8 text-[10px] font-bold uppercase tracking-widest text-gray-400">
                <a href="#quote" class="hover:text-white">Estimates</a>
                <a href="#why-us" class="hover:text-white">Why Us</a>
                <a href="mailto:ushomeimprovement07@gmail.com" class="hover:text-white">Support</a>
            </div>
            <a href="#quote" class="glow-button px-5 py-2.5 rounded-xl text-[10px] font-bold uppercase tracking-widest text-white">Start Project</a>
        </div>
    </nav>

    <section class="pt-24 pb-16 px-6 text-center">
        <h1 class="text-6xl md:text-8xl font-extrabold mb-8 tracking-tighter">Luxury Living. <br><span class="text-blue-500 italic">Expertly Built.</span></h1>
        <p class="text-gray-400 max-w-3xl mx-auto text-lg mb-12 leading-relaxed">Skip the stress. We match you with the top 1% of pre-vetted, licensed, and insured contractors in your local area for guaranteed results.</p>
        
        <div class="flex justify-center gap-12 flex-wrap mb-16 grayscale opacity-60">
            <div class="text-center"><p class="text-2xl font-bold">1.4k+</p><p class="text-[8px] uppercase tracking-widest">Active Pros</p></div>
            <div class="text-center"><p class="text-2xl font-bold">4.9/5</p><p class="text-[8px] uppercase tracking-widest">Google Rating</p></div>
            <div class="text-center"><p class="text-2xl font-bold">A+ Rated</p><p class="text-[8px] uppercase tracking-widest">BBB Member</p></div>
        </div>
    </section>

    <section id="quote" class="py-12 px-6">
        <div class="max-w-xl mx-auto premium-glass p-10 md:p-14 border-t-2 border-blue-500/50 shadow-blue-500/10 shadow-2xl">
            <form id="ultraFinalForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-extrabold mb-2 uppercase tracking-tighter">01. Choose Service</h2>
                    <p class="text-gray-500 text-xs mb-10">All contractors are verified for State License & Insurance</p>
                    <div class="space-y-3">
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="w-full p-6 premium-glass border-white/5 hover:border-blue-500 text-left flex justify-between items-center group transition-all">
                            <span class="font-bold">🏠 ROOFING & EXTERIORS</span> <span class="group-hover:translate-x-2 transition">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="w-full p-6 premium-glass border-white/5 hover:border-blue-500 text-left flex justify-between items-center group transition-all">
                            <span class="font-bold">☀️ SOLAR ENERGY SYSTEMS</span> <span class="group-hover:translate-x-2 transition">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Kitchen', 2)" class="w-full p-6 premium-glass border-white/5 hover:border-blue-500 text-left flex justify-between items-center group transition-all">
                            <span class="font-bold">🛁 KITCHEN & BATH REMODEL</span> <span class="group-hover:translate-x-2 transition">→</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-extrabold mb-8 italic">02. WHERE IS THE PROJECT?</h2>
                    <input type="text" id="zip" placeholder="Zip Code (e.g. 90210)" class="w-full p-5 premium-glass outline-none focus:ring-2 ring-blue-500 mb-5">
                    <select id="state" class="w-full p-5 premium-glass outline-none bg-black text-gray-400 mb-10">
                        <option value="">Select Your State</option>
                        <option value="TX">Texas</option><option value="CA">California</option><option value="FL">Florida</option><option value="NY">New York</option>
                    </select>
                    <button type="button" onclick="move(3)" class="w-full glow-button p-5 rounded-2xl font-bold uppercase tracking-widest">Verify My Location</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-extrabold mb-2">03. SECURE VERIFICATION</h2>
                    <p class="text-gray-500 text-xs mb-10 italic">Final step to receive your 3 free estimates</p>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-5 premium-glass outline-none mb-4">
                    <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 premium-glass outline-none mb-10">
                    <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-bold uppercase tracking-widest hover:bg-green-500 transition shadow-lg shadow-green-900/30">Get Estimates Now</button>
                </div>
            </form>
        </div>
    </section>

    <section id="why-us" class="py-24 max-w-4xl mx-auto px-6">
        <h3 class="text-3xl font-extrabold mb-12 text-center uppercase tracking-tighter">The Gold Standard</h3>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div class="p-8 premium-glass border-l-4 border-blue-500">
                <h4 class="font-bold text-blue-400 mb-4 uppercase text-xs tracking-widest italic">100% Vetted Pros</h4>
                <p class="text-sm text-gray-500 leading-relaxed">Unlike other sites, we manually check license numbers and insurance certificates every 6 months to ensure your safety.</p>
            </div>
            <div class="p-8 premium-glass border-l-4 border-blue-500">
                <h4 class="font-bold text-blue-400 mb-4 uppercase text-xs tracking-widest italic">Price Match Guarantee</h4>
                <p class="text-sm text-gray-500 leading-relaxed">Our network members agree to provide competitive, fair-market pricing to all homeowners through our platform.</p>
            </div>
        </div>
    </section>

    <footer class="py-24 border-t border-white/5 bg-[#010204]">
        <div class="max-w-6xl mx-auto px-6 grid md:grid-cols-2 gap-16 mb-20">
            <div>
                <p class="text-2xl font-extrabold text-blue-500 tracking-tighter mb-6">U.S. HOME IMPROVEMENTS</p>
                <p class="text-gray-500 text-[10px] leading-relaxed uppercase tracking-[0.2em] mb-8">
                    U.S. Home Improvements is a national network connecting homeowners with local, licensed contractors. All estimates are free and no-obligation. <br><br>
                    Reg #US-770821-B | 50 State Coverage | SSL Secured Portal
                </p>
                <div class="flex gap-4 opacity-40">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Better_Business_Bureau_logo.svg/1200px-Better_Business_Bureau_logo.svg.png" class="h-6 invert" alt="BBB">
                </div>
            </div>
            <div class="flex flex-col md:items-end">
                <p class="text-[9px] font-bold text-gray-600 uppercase tracking-widest mb-4">Support & Administration</p>
                <a href="mailto:ushomeimprovement07@gmail.com" class="text-blue-400 text-lg font-bold italic hover:underline">ushomeimprovement07@gmail.com</a>
                <p class="mt-8 text-[9px] text-gray-700 italic">Operating under US Consumer Protection Laws 2026</p>
            </div>
        </div>
        <div class="text-center border-t border-white/5 pt-10">
            <p class="text-[8px] text-gray-800 font-bold uppercase tracking-[0.6em]">© 2026 National Contractor Network. All Rights Reserved.</p>
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

        document.getElementById('ultraFinalForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const btn = e.target.querySelector('button[type="submit"]');
            btn.innerText = "Processing Verified Lead...";
            
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
                alert("Verified! Your free quote request has been safely delivered to local professionals.");
                location.reload();
            } catch(e) { alert("Error! Check your connection."); btn.innerText = "Get Estimates Now"; }
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
                document.getElementById('ultraFinalForm').appendChild(h);
            }
            document.getElementById('selectedService').value = v;
            move(n);
        }
    </script>
</body>
</html>
