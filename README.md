<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Official National Contractor Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #05070a; color: white; scroll-behavior: smooth; }
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.08); }
        .step { display: none; }
        .step.active { display: block; animation: slideUp 0.5s ease; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .hero-bg { 
            background: linear-gradient(rgba(5, 7, 10, 0.85), rgba(5, 7, 10, 0.85)), 
            url('https://images.unsplash.com/photo-1513694203232-719a280e022f?auto=format&fit=crop&q=80&w=1600'); 
            background-size: cover; background-position: center; 
        }
        .service-img { height: 200px; width: 100%; object-fit: cover; border-radius: 20px; transition: transform 0.5s; }
        .glass-card:hover .service-img { transform: scale(1.05); }
        .btn-blue { background: linear-gradient(90deg, #2563eb, #3b82f6); transition: all 0.3s; }
        .btn-blue:hover { transform: translateY(-2px); box-shadow: 0 10px 25px rgba(37, 99, 235, 0.4); }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-50 glass px-6 py-4 flex justify-between items-center backdrop-blur-xl">
        <div class="text-xl font-extrabold tracking-tighter text-blue-500">U.S. HOME IMPROVEMENTS</div>
        <div class="hidden md:flex gap-8 text-[10px] font-bold uppercase tracking-widest text-gray-400">
            <a href="#services" class="hover:text-blue-400 transition">Services</a>
            <a href="#directory" class="hover:text-blue-400 transition">Locations</a>
            <a href="mailto:ushomeimprovement07@gmail.com" class="hover:text-blue-400 transition">Contact</a>
        </div>
        <a href="#quote" class="bg-blue-600 px-6 py-2 rounded-full text-[10px] font-bold uppercase tracking-widest hover:bg-blue-500 transition">Get Started</a>
    </nav>

    <section class="hero-bg py-32 px-4 text-center border-b border-white/5">
        <div class="inline-block px-4 py-1 border border-blue-500/30 rounded-full text-blue-400 text-[9px] font-bold mb-8 tracking-[0.3em] uppercase">Trusted Across 50 States</div>
        <h1 class="text-5xl md:text-8xl font-extrabold mb-8 leading-tight tracking-tighter">Your Home. <br><span class="text-blue-500">Perfected.</span></h1>
        <p class="text-gray-400 max-w-2xl mx-auto text-lg mb-12">The most reliable way to find pre-vetted, licensed, and local home improvement professionals in the United States.</p>
        
        <div class="flex flex-wrap justify-center gap-12 opacity-50 grayscale hover:grayscale-0 transition duration-700">
            <div class="flex flex-col items-center">
                <span class="text-2xl font-bold italic">⭐ 4.9/5</span>
                <span class="text-[9px] uppercase font-bold tracking-widest">Trust Rating</span>
            </div>
            <div class="flex flex-col items-center">
                <span class="text-2xl font-bold italic">500k+</span>
                <span class="text-[9px] uppercase font-bold tracking-widest">Happy Clients</span>
            </div>
        </div>
    </section>

    <section id="quote" class="py-20 px-4 bg-[#080a10]">
        <div class="max-w-xl mx-auto glass p-8 md:p-12 rounded-[3rem] shadow-2xl relative border-blue-500/10">
            <div id="progress" class="absolute top-0 left-0 h-1 bg-blue-500 transition-all duration-700" style="width: 33.3%;"></div>
            
            <form id="finalLeadForm">
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-bold mb-2">Select Service</h2>
                    <p class="text-gray-500 text-sm mb-8 italic">Choose your project to begin</p>
                    <div class="grid grid-cols-1 gap-3">
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="p-5 glass rounded-2xl border border-white/5 hover:border-blue-500 text-left transition flex justify-between items-center">
                            <span>🏠 Roofing (New/Repair)</span> <span class="text-blue-500">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="p-5 glass rounded-2xl border border-white/5 hover:border-blue-500 text-left transition flex justify-between items-center">
                            <span>☀️ Solar Energy Panels</span> <span class="text-blue-500">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'HVAC', 2)" class="p-5 glass rounded-2xl border border-white/5 hover:border-blue-500 text-left transition flex justify-between items-center">
                            <span>❄️ HVAC & AC Systems</span> <span class="text-blue-500">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Kitchen', 2)" class="p-5 glass rounded-2xl border border-white/5 hover:border-blue-500 text-left transition flex justify-between items-center">
                            <span>🛁 Kitchen & Bath Remodel</span> <span class="text-blue-500">→</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-3xl font-bold mb-8 text-blue-400 underline italic">02. Location</h2>
                    <input type="text" id="zip" placeholder="Zip Code (e.g. 90210)" class="w-full p-5 glass rounded-2xl mb-4 outline-none focus:ring-1 ring-blue-500">
                    <select id="state" class="w-full p-5 glass rounded-2xl mb-8 outline-none text-gray-400 bg-[#0c0f17]">
                        <option value="">Select Your State</option>
                        <option value="AL">Alabama</option><option value="AZ">Arizona</option><option value="CA">California</option>
                        <option value="FL">Florida</option><option value="GA">Georgia</option><option value="IL">Illinois</option>
                        <option value="MI">Michigan</option><option value="NY">New York</option><option value="TX">Texas</option>
                        <option value="WA">Washington</option>
                    </select>
                    <button type="button" onclick="move(3)" class="w-full btn-blue p-5 rounded-2xl font-bold text-lg">Next Step</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-bold mb-4">Contact</h2>
                    <p class="text-gray-500 text-sm mb-8">Receive up to 3 free estimates within 24 hours.</p>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-5 glass rounded-2xl mb-4 outline-none">
                    <input type="tel" id="phone" placeholder="Phone Number" class="w-full p-5 glass rounded-2xl mb-8 outline-none">
                    <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-bold text-lg hover:bg-green-500 transition-all shadow-xl shadow-green-900/20">Submit Free Request</button>
                </div>
            </form>
        </div>
    </section>

    <section id="services" class="py-32 max-w-7xl mx-auto px-6">
        <div class="text-center mb-16">
            <h2 class="text-4xl font-extrabold mb-4">Top Professional Services</h2>
            <div class="h-1 w-20 bg-blue-500 mx-auto"></div>
        </div>
        <div class="grid md:grid-cols-3 gap-10">
            <div class="glass-card group">
                <img src="https://images.unsplash.com/photo-1632759145351-1d592919f522?auto=format&fit=crop&q=80&w=800" class="service-img" alt="Roof">
                <h3 class="text-xl font-bold mt-6 mb-2">Roofing Solutions</h3>
                <p class="text-gray-500 text-sm">From repairs to full replacements, our pros ensure a lifetime of protection.</p>
            </div>
            <div class="glass-card group">
                <img src="https://images.unsplash.com/photo-1508514177221-188b1cf16e9d?auto=format&fit=crop&q=80&w=800" class="service-img" alt="Solar">
                <h3 class="text-xl font-bold mt-6 mb-2">Sustainable Solar</h3>
                <p class="text-gray-500 text-sm">Join the energy revolution and lower your bills with top-tier panel installation.</p>
            </div>
            <div class="glass-card group">
                <img src="https://images.unsplash.com/photo-1556911220-e150223bd797?auto=format&fit=crop&q=80&w=800" class="service-img" alt="Kitchen">
                <h3 class="text-xl font-bold mt-6 mb-2">Premium Remodeling</h3>
                <p class="text-gray-500 text-sm">Transform your kitchen or bathroom with award-winning local designers.</p>
            </div>
        </div>
    </section>

    <section id="directory" class="py-24 bg-[#030508] border-t border-white/5">
        <div class="max-w-6xl mx-auto px-6">
            <h3 class="text-xs font-bold text-blue-500 uppercase tracking-[0.4em] mb-12 text-center italic">National Service Directory</h3>
            <div class="grid grid-cols-2 md:grid-cols-5 gap-y-6 gap-x-12 text-xs text-gray-600 font-bold uppercase tracking-widest">
                <a href="#" class="hover:text-white transition">Alabama</a> <a href="#" class="hover:text-white transition">Alaska</a>
                <a href="#" class="hover:text-white transition">California</a> <a href="#" class="hover:text-white transition">Florida</a>
                <a href="#" class="hover:text-white transition">Texas</a> <a href="#" class="hover:text-white transition">Georgia</a>
                <a href="#" class="hover:text-white transition">New York</a> <a href="#" class="hover:text-white transition">Arizona</a>
                <a href="#" class="hover:text-white transition">Colorado</a> <a href="#" class="hover:text-white transition">Nevada</a>
                <a href="#" class="hover:text-white transition">Virginia</a> <a href="#" class="hover:text-white transition">Ohio</a>
                <a href="#" class="hover:text-white transition">Michigan</a> <a href="#" class="hover:text-white transition">Illinois</a>
                <a href="#" class="hover:text-white transition">Washington</a>
            </div>
        </div>
    </section>

    <footer class="py-20 px-6 border-t border-white/5">
        <div class="max-w-6xl mx-auto grid md:grid-cols-2 gap-16 mb-16">
            <div>
                <p class="text-2xl font-extrabold text-blue-500 mb-4">U.S. HOME IMPROVEMENTS</p>
                <p class="text-gray-500 text-sm max-w-md leading-relaxed">
                    Connecting homeowners with local pros. We provide a seamless platform for high-quality home transformations across the USA.
                </p>
            </div>
            <div class="flex flex-col md:items-end">
                <p class="text-xs font-bold uppercase tracking-widest text-white mb-4 italic">Contact Support</p>
                <a href="mailto:ushomeimprovement07@gmail.com" class="text-blue-400 text-lg font-bold hover:underline tracking-tight italic">
                    ushomeimprovement07@gmail.com
                </a>
            </div>
        </div>
        <div class="text-center pt-10 border-t border-white/5">
            <p class="text-[9px] text-gray-700 font-bold uppercase tracking-[0.5em]">© 2026 National Contractor Network | Licensed & Insured</p>
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

        document.getElementById('finalLeadForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const btn = e.target.querySelector('button[submit]');
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
                alert("Success! Your free estimate request has been sent.");
                location.reload();
            } catch(e) { alert("Error! Check Firebase Firestore Rules."); }
        });
    </script>

    <script>
        function move(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
            document.getElementById('progress').style.width = (s * 33.3) + "%";
        }
        function setVal(t, v, n) {
            if(!document.getElementById('selectedService')) {
                const h = document.createElement("input"); h.type="hidden"; h.id="selectedService";
                document.getElementById('finalLeadForm').appendChild(h);
            }
            document.getElementById('selectedService').value = v;
            move(n);
        }
    </script>
</body>
</html>
