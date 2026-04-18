<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Official National Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #05070a; color: white; scroll-behavior: smooth; }
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.08); }
        .step { display: none; }
        .step.active { display: block; animation: slideUp 0.5s ease; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .hero-bg { background: linear-gradient(rgba(5, 7, 10, 0.8), rgba(5, 7, 10, 0.8)), url('https://images.unsplash.com/photo-1513694203232-719a280e022f?auto=format&fit=crop&q=80&w=1600'); background-size: cover; background-position: center; }
        .service-img { height: 180px; width: 100%; object-fit: cover; border-radius: 12px; margin-bottom: 15px; }
        .btn-blue { background: linear-gradient(90deg, #2563eb, #3b82f6); transition: all 0.3s; }
        .btn-blue:hover { transform: translateY(-2px); box-shadow: 0 10px 20px rgba(37, 99, 235, 0.3); }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-50 glass px-6 py-4 flex justify-between items-center backdrop-blur-lg">
        <div class="text-xl font-extrabold tracking-tighter text-blue-500">U.S. HOME IMPROVEMENTS</div>
        <a href="#quote" class="bg-blue-600 px-5 py-2 rounded-full text-xs font-bold hover:bg-blue-500 transition uppercase tracking-widest">Get Free Quote</a>
    </nav>

    <section class="hero-bg py-24 px-4 text-center border-b border-white/5">
        <div class="inline-block px-4 py-1 border border-blue-500/30 rounded-full text-blue-400 text-[10px] font-bold mb-6 tracking-widest uppercase">Certified Contractor Network</div>
        <h1 class="text-5xl md:text-7xl font-extrabold mb-6 leading-tight">Better Homes,<br><span class="text-blue-500">Top-Rated Pros.</span></h1>
        <p class="text-gray-300 max-w-2xl mx-auto text-lg mb-10">We match American homeowners with licensed, local professionals for every home project.</p>
        <div class="flex justify-center gap-6 grayscale opacity-60">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Better_Business_Bureau_logo.svg/1200px-Better_Business_Bureau_logo.svg.png" class="h-8 invert" alt="BBB">
            <span class="font-bold border-l pl-6 border-gray-700">⭐ 4.9/5 Rating</span>
        </div>
    </section>

    <section id="quote" class="py-16 px-4">
        <div class="max-w-xl mx-auto glass p-8 md:p-12 rounded-[2.5rem] shadow-2xl relative">
            <div id="progress" class="absolute top-0 left-0 h-1 bg-blue-500 transition-all" style="width: 33%;"></div>
            
            <form id="proLeadForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-bold mb-6 italic text-blue-300">01. Select Project</h2>
                    <div class="grid grid-cols-1 gap-3">
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="p-4 glass rounded-xl border border-white/5 hover:border-blue-500 text-left transition">🏠 Roofing & Gutters</button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="p-4 glass rounded-xl border border-white/5 hover:border-blue-500 text-left transition">☀️ Solar Power Systems</button>
                        <button type="button" onclick="setVal('service', 'HVAC', 2)" class="p-4 glass rounded-xl border border-white/5 hover:border-blue-500 text-left transition">❄️ HVAC Installation/Repair</button>
                        <button type="button" onclick="setVal('service', 'Remodel', 2)" class="p-4 glass rounded-xl border border-white/5 hover:border-blue-500 text-left transition">🛁 Kitchen & Bath Remodeling</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-bold mb-6 italic text-blue-300">02. Location Details</h2>
                    <input type="text" id="zip" placeholder="Zip Code" class="w-full p-4 glass rounded-xl mb-4 outline-none focus:ring-1 ring-blue-500">
                    <select id="state" class="w-full p-4 glass rounded-xl mb-8 outline-none text-gray-400">
                        <option value="">Select State</option>
                        <option value="AL">Alabama</option><option value="CA">California</option><option value="FL">Florida</option>
                        <option value="TX">Texas</option><option value="NY">New York</option>
                    </select>
                    <button type="button" onclick="move(3)" class="w-full btn-blue p-4 rounded-xl font-bold">Next</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-bold mb-6 italic text-blue-300">03. Contact Info</h2>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-4 glass rounded-xl mb-4 outline-none">
                    <input type="tel" id="phone" placeholder="Phone Number" class="w-full p-4 glass rounded-xl mb-8 outline-none">
                    <button type="submit" class="w-full bg-green-600 p-4 rounded-xl font-bold hover:bg-green-500">Get Free Estimates</button>
                </div>
            </form>
        </div>
    </section>

    <section class="py-20 max-w-6xl mx-auto px-6" id="services">
        <h2 class="text-3xl font-bold mb-12 text-center">Our Featured Services</h2>
        <div class="grid md:grid-cols-3 gap-8">
            <div class="glass p-4 rounded-3xl">
                <img src="https://images.unsplash.com/photo-1632759145351-1d592919f522?auto=format&fit=crop&q=80&w=800" class="service-img" alt="Roofing">
                <h3 class="font-bold text-lg mb-2">Expert Roofing</h3>
                <p class="text-gray-500 text-sm">Full replacement and repairs with lifetime warranty.</p>
            </div>
            <div class="glass p-4 rounded-3xl">
                <img src="https://images.unsplash.com/photo-1508514177221-188b1cf16e9d?auto=format&fit=crop&q=80&w=800" class="service-img" alt="Solar">
                <h3 class="font-bold text-lg mb-2">Solar Energy</h3>
                <p class="text-gray-500 text-sm">Save up to 70% on your monthly electricity bills.</p>
            </div>
            <div class="glass p-4 rounded-3xl">
                <img src="https://images.unsplash.com/photo-1556911220-e150223bd797?auto=format&fit=crop&q=80&w=800" class="service-img" alt="Remodeling">
                <h3 class="font-bold text-lg mb-2">Modern Kitchens</h3>
                <p class="text-gray-500 text-sm">High-end kitchen and bathroom transformation.</p>
            </div>
        </div>
    </section>

    <footer class="mt-20 border-t border-white/5 py-12 px-6">
        <div class="max-w-6xl mx-auto flex flex-col md:flex-row justify-between items-center gap-8">
            <div class="text-center md:text-left">
                <p class="text-xl font-extrabold text-blue-500 mb-2 uppercase">U.S. Home Improvements</p>
                <a href="mailto:ushomeimprovement07@gmail.com" class="text-sm text-gray-400 hover:text-blue-400">✉️ ushomeimprovement07@gmail.com</a>
            </div>
            <div class="flex gap-6 text-[10px] font-bold text-gray-600 uppercase tracking-widest">
                <a href="#">Privacy</a><a href="#">Terms</a><a href="#">States</a>
            </div>
        </div>
        <p class="text-center text-[10px] text-gray-800 mt-10 tracking-[0.3em] font-bold uppercase">© 2026 National Contractor Network</p>
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

        document.getElementById('proLeadForm').addEventListener('submit', async (e) => {
            e.preventDefault();
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
                alert("Success! A pro will contact you.");
                location.reload();
            } catch(e) { alert("Error! Check Firebase Rules."); }
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
                document.getElementById('proLeadForm').appendChild(h);
            }
            document.getElementById('selectedService').value = v;
            move(n);
        }
    </script>
</body>
</html>
