<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | America's Trusted Contractor Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #05070a; color: white; scroll-behavior: smooth; }
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.08); }
        .step { display: none; }
        .step.active { display: block; animation: slideUp 0.5s ease; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        .btn-blue { background: linear-gradient(135deg, #2563eb, #1d4ed8); transition: all 0.3s ease; }
        .btn-blue:hover { transform: translateY(-2px); box-shadow: 0 10px 25px rgba(37, 99, 235, 0.4); }
        .service-card:hover { border-color: #3b82f6; background: rgba(59, 130, 246, 0.05); cursor: pointer; }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-50 glass px-6 py-4 flex justify-between items-center">
        <div class="text-2xl font-extrabold tracking-tighter text-blue-500">U.S. HOME IMPROVEMENTS</div>
        <div class="hidden md:flex gap-8 text-sm font-semibold text-gray-400">
            <a href="#services" class="hover:text-blue-400 transition">Services</a>
            <a href="#quote" class="hover:text-blue-400 transition">Get Estimates</a>
            <a href="mailto:Ushomeimprovement07@gmail.com" class="hover:text-blue-400 transition">Support</a>
        </div>
        <a href="#quote" class="bg-blue-600 px-6 py-2 rounded-full text-xs font-bold uppercase tracking-widest hover:bg-blue-500 transition">Free Quote</a>
    </nav>

    <section class="py-24 px-4 text-center">
        <div class="inline-block px-4 py-1 border border-blue-500/30 rounded-full text-blue-400 text-[10px] font-bold mb-8 tracking-[0.2em] uppercase">National Pro Network</div>
        <h1 class="text-5xl md:text-7xl font-extrabold mb-6 leading-tight">Upgrade Your Home <br><span class="text-blue-500">With Local Experts.</span></h1>
        <p class="text-gray-400 max-w-2xl mx-auto text-lg mb-12">Connect with the top 3% of licensed contractors in your area. Fast, free, and no obligation.</p>
        
        <div class="flex flex-wrap justify-center gap-10 opacity-70 mb-10">
            <div class="text-center"><p class="text-2xl font-bold">4.9/5</p><p class="text-[10px] text-gray-500 uppercase font-bold tracking-widest">Customer Rating</p></div>
            <div class="text-center"><p class="text-2xl font-bold">24hr</p><p class="text-[10px] text-gray-500 uppercase font-bold tracking-widest">Response Time</p></div>
            <div class="text-center"><p class="text-2xl font-bold">100%</p><p class="text-[10px] text-gray-500 uppercase font-bold tracking-widest">Vetted Pros</p></div>
        </div>
    </section>

    <section id="quote" class="py-12 px-4 relative">
        <div class="max-w-xl mx-auto glass p-10 rounded-[3rem] shadow-3xl relative overflow-hidden border-blue-500/20">
            <div class="absolute top-0 left-0 w-full h-1.5 bg-gray-900">
                <div id="progress" class="h-full bg-blue-600 transition-all duration-700" style="width: 33.3%;"></div>
            </div>

            <form id="ultraLeadForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-bold mb-8">What project are you starting?</h2>
                    <div class="grid grid-cols-1 gap-3">
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="service-card p-5 glass rounded-2xl text-left border border-white/5 transition-all">🏠 Roofing (New/Repair)</button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="service-card p-5 glass rounded-2xl text-left border border-white/5 transition-all">☀️ Solar Energy Panels</button>
                        <button type="button" onclick="setVal('service', 'HVAC', 2)" class="service-card p-5 glass rounded-2xl text-left border border-white/5 transition-all">❄️ HVAC & Cooling</button>
                        <button type="button" onclick="setVal('service', 'Windows', 2)" class="service-card p-5 glass rounded-2xl text-left border border-white/5 transition-all">🪟 Windows & Doors</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-bold mb-6">Where is the property?</h2>
                    <input type="text" id="zip" placeholder="Zip Code (e.g. 90210)" class="w-full p-5 glass rounded-2xl mb-4 outline-none focus:ring-2 ring-blue-500">
                    <select id="state" class="w-full p-5 glass rounded-2xl mb-8 outline-none focus:ring-2 ring-blue-500 text-gray-400">
                        <option value="">Select State</option>
                        <option value="AL">Alabama</option><option value="CA">California</option><option value="FL">Florida</option>
                        <option value="TX">Texas</option><option value="NY">New York</option>
                        </select>
                    <button type="button" onclick="move(3)" class="w-full btn-blue p-5 rounded-2xl font-bold">Continue</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-bold mb-6">Contact Information</h2>
                    <p class="text-gray-400 text-sm mb-6">Almost done! Enter your details to receive your free quotes.</p>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-5 glass rounded-2xl mb-4 outline-none focus:ring-2 ring-blue-500">
                    <input type="tel" id="phone" placeholder="Phone Number" class="w-full p-5 glass rounded-2xl mb-8 outline-none focus:ring-2 ring-blue-500">
                    <button type="submit" class="w-full bg-green-600 hover:bg-green-500 p-5 rounded-2xl font-bold shadow-lg shadow-green-500/20 transition-all">Submit My Request</button>
                </div>
            </form>
        </div>
    </section>

    <footer class="mt-32 border-t border-white/5 bg-[#030508] py-16 px-6">
        <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-12 mb-12">
            <div>
                <h4 class="text-xl font-bold text-blue-500 mb-4">U.S. HOME IMPROVEMENTS</h4>
                <p class="text-gray-500 text-sm leading-relaxed">Connecting American homeowners with quality contractors. Licensed, insured, and verified pros across all 50 states.</p>
            </div>
            <div>
                <h4 class="text-white font-bold mb-4 uppercase text-xs tracking-widest">Contact Us</h4>
                <a href="mailto:Ushomeimprovement07@gmail.com" class="text-blue-400 text-sm hover:underline">✉️ Ushomeimprovement07@gmail.com</a>
                <p class="text-gray-500 text-xs mt-4">Support available 24/7 for homeowners and partners.</p>
            </div>
            <div>
                <h4 class="text-white font-bold mb-4 uppercase text-xs tracking-widest">States We Cover</h4>
                <div class="grid grid-cols-2 gap-2 text-xs text-gray-600">
                    <span>Texas</span><span>California</span><span>Florida</span><span>New York</span>
                </div>
            </div>
        </div>
        <div class="max-w-6xl mx-auto text-center border-t border-white/5 pt-8">
            <p class="text-[10px] text-gray-700 uppercase tracking-widest">&copy; 2026 U.S. Home Improvements | All Rights Reserved</p>
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

        const form = document.getElementById('ultraLeadForm');
        form.addEventListener('submit', async (e) => {
            e.preventDefault();
            const btn = e.target.querySelector('button[type="submit"]');
            btn.innerText = "Processing Your Quote...";
            
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
                alert("Thank you! Your request has been sent to local professionals.");
                window.location.reload();
            } catch (err) {
                alert("Database Error! Make sure Firestore Rules are set to Public.");
                btn.innerText = "Submit My Request";
            }
        });
    </script>

    <script>
        function move(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
            document.getElementById('progress').style.width = (s * 33.3) + "%";
        }
        function setVal(type, val, next) {
            if(type === 'service') {
                if(!document.getElementById('selectedService')) {
                    const h = document.createElement("input");
                    h.type = "hidden"; h.id = "selectedService";
                    document.getElementById('ultraLeadForm').appendChild(h);
                }
                document.getElementById('selectedService').value = val;
            }
            move(next);
        }
    </script>
</body>
</html>
