<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | America's #1 Contractor Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #05070a; color: white; scroll-behavior: smooth; }
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.08); }
        .step { display: none; }
        .step.active { display: block; animation: slideUp 0.5s ease; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .gradient-text { background: linear-gradient(90deg, #60a5fa, #2563eb); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .service-btn:hover { background: rgba(37, 99, 235, 0.2); border-color: #3b82f6; transform: scale(1.02); }
    </style>
</head>
<body>

    <div class="fixed bottom-6 right-6 z-[100]">
        <a href="#quote" class="bg-blue-600 p-4 rounded-full shadow-2xl flex items-center justify-center hover:bg-blue-500 transition-all scale-110">
            <span class="text-white font-bold text-xs uppercase tracking-widest px-2">Free Quote</span>
        </a>
    </div>

    <nav class="sticky top-0 z-50 glass px-6 py-4 flex justify-between items-center backdrop-blur-md">
        <div class="text-xl font-extrabold tracking-tighter text-blue-500">U.S. HOME IMPROVEMENTS</div>
        <div class="hidden md:flex gap-6 text-sm font-medium text-gray-400">
            <a href="#features" class="hover:text-white">Features</a>
            <a href="#services" class="hover:text-white">Services</a>
            <a href="#states" class="hover:text-white">States</a>
        </div>
        <a href="#quote" class="bg-blue-600 px-6 py-2 rounded-full text-xs font-bold hover:bg-blue-500 transition">Get Started</a>
    </nav>

    <section class="pt-24 pb-12 px-4 text-center">
        <h1 class="text-5xl md:text-7xl font-extrabold mb-6 leading-tight">National Network of <br><span class="gradient-text text-blue-500">Certified Contractors.</span></h1>
        <p class="text-gray-400 max-w-2xl mx-auto text-lg mb-12">The easiest way for US homeowners to find top-rated local pros for any home project.</p>
        
        <div class="flex flex-wrap justify-center gap-12 text-center mb-16">
            <div><p class="text-3xl font-bold">50k+</p><p class="text-xs text-gray-500 uppercase tracking-widest">Leads Delivered</p></div>
            <div><p class="text-3xl font-bold">4.8/5</p><p class="text-xs text-gray-500 uppercase tracking-widest">Google Rating</p></div>
            <div><p class="text-3xl font-bold">50</p><p class="text-xs text-gray-500 uppercase tracking-widest">States Covered</p></div>
        </div>
    </section>

    <section id="quote" class="py-12 px-4 relative">
        <div class="max-w-xl mx-auto glass p-10 rounded-[2.5rem] shadow-3xl relative overflow-hidden border-blue-500/20">
            <div id="progress" class="absolute top-0 left-0 h-1.5 bg-blue-500 transition-all duration-700" style="width: 25%;"></div>
            
            <form id="proLeadForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-bold mb-2">What are you planning?</h2>
                    <p class="text-gray-400 text-sm mb-8 italic text-blue-400">Select a category to begin</p>
                    <div class="grid grid-cols-1 gap-3">
                        <button type="button" onclick="selectOption('service', 'Roofing', 2)" class="service-btn p-5 glass rounded-2xl text-left border border-white/5 transition-all">🏠 New Roof / Repair</button>
                        <button type="button" onclick="selectOption('service', 'Solar', 2)" class="service-btn p-5 glass rounded-2xl text-left border border-white/5 transition-all">☀️ Solar Installation</button>
                        <button type="button" onclick="selectOption('service', 'HVAC', 2)" class="service-btn p-5 glass rounded-2xl text-left border border-white/5 transition-all">❄️ HVAC & Cooling</button>
                        <button type="button" onclick="selectOption('service', 'Remodeling', 2)" class="service-btn p-5 glass rounded-2xl text-left border border-white/5 transition-all">🛁 Kitchen & Bath</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-bold mb-6">Where is your project?</h2>
                    <input type="text" id="zipCode" placeholder="Enter Zip Code (e.g. 90210)" class="w-full p-5 glass rounded-2xl mb-4 border-none outline-none focus:ring-2 ring-blue-500 transition-all">
                    <select id="state" class="w-full p-5 glass rounded-2xl mb-8 border-none outline-none focus:ring-2 ring-blue-500 text-gray-400">
                        <option value="">Select State</option>
                        <option value="AL">Alabama</option><option value="AK">Alaska</option><option value="AZ">Arizona</option>
                        <option value="CA">California</option><option value="FL">Florida</option><option value="TX">Texas</option>
                        <option value="NY">New York</option>
                        </select>
                    <button type="button" onclick="goToStep(3)" class="w-full bg-blue-600 p-5 rounded-2xl font-bold shadow-lg shadow-blue-500/20">Next: Contact Info</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-bold mb-6">Final Step</h2>
                    <p class="text-sm text-gray-400 mb-6">A local specialist from <span class="text-blue-400 font-bold">U.S. Home Improvements</span> will contact you with free estimates.</p>
                    <input type="text" id="userName" placeholder="First & Last Name" class="w-full p-5 glass rounded-2xl mb-4 border-none outline-none focus:ring-2 ring-blue-500">
                    <input type="tel" id="userPhone" placeholder="Mobile Number" class="w-full p-5 glass rounded-2xl mb-8 border-none outline-none focus:ring-2 ring-blue-500">
                    <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-bold hover:bg-green-500 transition-all">Get Free Estimates</button>
                </div>
            </form>
        </div>
    </section>

    <section id="features" class="py-24 max-w-6xl mx-auto px-6 grid md:grid-cols-3 gap-12">
        <div class="text-center p-8">
            <div class="text-4xl mb-4">🛡️</div>
            <h4 class="text-xl font-bold mb-2">Verified Pros</h4>
            <p class="text-gray-500 text-sm">We only work with licensed, insured, and background-checked contractors.</p>
        </div>
        <div class="text-center p-8">
            <div class="text-4xl mb-4">💰</div>
            <h4 class="text-xl font-bold mb-2">Cost Savings</h4>
            <p class="text-gray-500 text-sm">Compare multiple quotes and save up to 35% on total project costs.</p>
        </div>
        <div class="text-center p-8">
            <div class="text-4xl mb-4">⏱️</div>
            <h4 class="text-xl font-bold mb-2">Fast Results</h4>
            <p class="text-gray-500 text-sm">Get matched with up to 3 local professionals in under 24 hours.</p>
        </div>
    </section>

    <section id="states" class="py-20 bg-[#080a10] border-t border-white/5">
        <div class="max-w-6xl mx-auto px-6">
            <h3 class="text-gray-400 text-xs font-bold uppercase tracking-[0.3em] mb-12 text-center">Serviceable States</h3>
            <div class="grid grid-cols-2 md:grid-cols-5 gap-y-4 gap-x-8 text-sm text-gray-600">
                <a href="#" class="hover:text-blue-500">California</a><a href="#" class="hover:text-blue-500">Texas</a>
                <a href="#" class="hover:text-blue-500">Florida</a><a href="#" class="hover:text-blue-500">New York</a>
                <a href="#" class="hover:text-blue-500">Pennsylvania</a><a href="#" class="hover:text-blue-500">Illinois</a>
                <a href="#" class="hover:text-blue-500">Ohio</a><a href="#" class="hover:text-blue-500">Georgia</a>
                <a href="#" class="hover:text-blue-500">North Carolina</a><a href="#" class="hover:text-blue-500">Michigan</a>
            </div>
        </div>
    </section>

    <footer class="py-12 glass border-t border-white/5">
        <div class="max-w-6xl mx-auto px-6 flex flex-col md:flex-row justify-between items-center gap-8">
            <div class="text-center md:text-left">
                <p class="text-lg font-bold text-white mb-2">U.S. HOME IMPROVEMENTS</p>
                <p class="text-gray-500 text-xs tracking-wider uppercase font-medium">&copy; 2026 National Contractor Network</p>
            </div>
            <div class="flex gap-8 text-gray-500 text-xs font-bold uppercase tracking-widest">
                <a href="#" class="hover:text-white transition-colors">Privacy</a>
                <a href="#" class="hover:text-white transition-colors">Terms</a>
                <a href="#" class="hover:text-white transition-colors">Contact</a>
            </div>
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

        const form = document.getElementById('proLeadForm');
        form.addEventListener('submit', async (e) => {
            e.preventDefault();
            const btn = e.target.querySelector('button[type="submit"]');
            btn.innerText = "Submitting Lead...";
            
            const data = {
                service: document.getElementById('selectedService').value,
                zip: document.getElementById('zipCode').value,
                state: document.getElementById('state').value,
                name: document.getElementById('userName').value,
                phone: document.getElementById('userPhone').value,
                timestamp: new Date()
            };

            try {
                await addDoc(collection(db, "leads"), data);
                alert("Success! Your request is being matched with local pros.");
                location.reload();
            } catch (err) {
                alert("Error: " + err.message);
                btn.innerText = "Get Free Estimates";
            }
        });
    </script>

    <script>
        function goToStep(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
            document.getElementById('progress').style.width = (s * 33.3) + "%";
        }
        function selectOption(type, val, next) {
            if(type === 'service') {
                if(!document.getElementById('selectedService')) {
                    const hidden = document.createElement("input");
                    hidden.type = "hidden"; hidden.id = "selectedService";
                    document.getElementById('proLeadForm').appendChild(hidden);
                }
                document.getElementById('selectedService').value = val;
            }
            goToStep(next);
        }
    </script>
</body>
</html>
