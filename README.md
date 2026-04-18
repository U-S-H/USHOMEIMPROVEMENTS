<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Official National Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #080a10; color: white; }
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.08); }
        .step { display: none; }
        .step.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: scale(0.98); } to { opacity: 1; transform: scale(1); } }
        .service-card:hover { transform: translateY(-5px); border-color: #3b82f6; background: rgba(59, 130, 246, 0.1); }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-50 glass px-6 py-4 flex justify-between items-center">
        <div class="text-xl font-extrabold tracking-tighter text-blue-500">U.S. HOME IMPROVEMENTS</div>
        <a href="#quote" class="bg-blue-600 px-5 py-2 rounded-full text-sm font-bold hover:bg-blue-500 transition">Get Started</a>
    </nav>

    <section class="py-20 px-4 text-center">
        <div class="inline-block px-4 py-1 border border-blue-500/30 rounded-full text-blue-400 text-xs font-bold mb-6 tracking-widest uppercase">#1 Contractor Network in USA</div>
        <h1 class="text-5xl md:text-7xl font-extrabold mb-6 leading-tight">Better Homes,<br><span class="text-blue-500">Trusted Pros.</span></h1>
        <p class="text-gray-400 max-w-2xl mx-auto text-lg mb-10">Connect with pre-screened home improvement specialists for roofing, solar, HVAC, and more in your local area.</p>
        
        <div class="flex flex-wrap justify-center gap-8 opacity-60 grayscale hover:grayscale-0 transition duration-500">
            <span class="font-bold border-r pr-8 border-gray-700">⭐ 4.9/5 Rating</span>
            <span class="font-bold border-r pr-8 border-gray-700">✓ Licensed & Insured</span>
            <span class="font-bold">✓ BBB Accredited</span>
        </div>
    </section>

    <section id="quote" class="py-12 px-4">
        <div class="glass max-w-xl mx-auto p-8 rounded-[2rem] shadow-2xl relative">
            <div id="progress" class="absolute top-0 left-0 h-1 bg-blue-500 transition-all" style="width: 25%;"></div>
            
            <form id="mainLeadForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-bold mb-6 text-center">Select Your Project</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                        <button type="button" onclick="selectOption('service', 'Roofing', 2)" class="p-5 glass service-card rounded-2xl text-left transition">🏠 Roofing</button>
                        <button type="button" onclick="selectOption('service', 'Solar', 2)" class="p-5 glass service-card rounded-2xl text-left transition">☀️ Solar Energy</button>
                        <button type="button" onclick="selectOption('service', 'HVAC', 2)" class="p-5 glass service-card rounded-2xl text-left transition">❄️ HVAC Repair</button>
                        <button type="button" onclick="selectOption('service', 'Kitchen', 2)" class="p-5 glass service-card rounded-2xl text-left transition">🛁 Remodeling</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-bold mb-6 text-center">Project Location</h2>
                    <input type="text" id="zipCode" placeholder="Enter Zip Code" class="w-full p-4 glass rounded-xl mb-4 focus:border-blue-500 outline-none">
                    <button type="button" onclick="goToStep(3)" class="w-full bg-blue-600 p-4 rounded-xl font-bold">Next Step</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-bold mb-6 text-center">Your Details</h2>
                    <input type="text" id="userName" placeholder="Full Name" class="w-full p-4 glass rounded-xl mb-4 outline-none">
                    <input type="tel" id="userPhone" placeholder="Phone Number" class="w-full p-4 glass rounded-xl mb-6 outline-none">
                    <button type="submit" class="w-full bg-green-600 p-4 rounded-xl font-bold">Get My Free Quote</button>
                </div>
            </form>
        </div>
    </section>

    <section class="py-20 bg-[#0c0f17]">
        <div class="max-w-6xl mx-auto px-6 grid md:grid-cols-3 gap-10">
            <div class="p-8 glass rounded-3xl">
                <div class="text-blue-500 text-3xl mb-4 italic">01</div>
                <h4 class="text-xl font-bold mb-2 text-blue-300">Fast Match</h4>
                <p class="text-gray-400 text-sm">We find the best contractors near you within 24 hours.</p>
            </div>
            <div class="p-8 glass rounded-3xl">
                <div class="text-blue-500 text-3xl mb-4 italic">02</div>
                <h4 class="text-xl font-bold mb-2 text-blue-300">Verified Pros</h4>
                <p class="text-gray-400 text-sm">Every contractor is vetted for license and insurance.</p>
            </div>
            <div class="p-8 glass rounded-3xl">
                <div class="text-blue-500 text-3xl mb-4 italic">03</div>
                <h4 class="text-xl font-bold mb-2 text-blue-300">Best Price</h4>
                <p class="text-gray-400 text-sm">Compare multiple quotes to save up to 40% on your project.</p>
            </div>
        </div>
    </section>

    <section class="py-20 px-6 max-w-6xl mx-auto">
        <h2 class="text-3xl font-bold mb-10 text-center">Service Directory</h2>
        <div class="grid grid-cols-2 md:grid-cols-5 gap-4 text-gray-500 text-sm">
            <a href="#" class="hover:text-blue-400 transition">Alabama</a> <a href="#" class="hover:text-blue-400 transition">California</a>
            <a href="#" class="hover:text-blue-400 transition">Florida</a> <a href="#" class="hover:text-blue-400 transition">Texas</a>
            <a href="#" class="hover:text-blue-400 transition">New York</a> <a href="#" class="hover:text-blue-400 transition">Georgia</a>
            <a href="#" class="hover:text-blue-400 transition">Arizona</a> <a href="#" class="hover:text-blue-400 transition">Illinois</a>
            <a href="#" class="hover:text-blue-400 transition">Nevada</a> <a href="#" class="hover:text-blue-400 transition">Michigan</a>
        </div>
    </section>

    <footer class="py-10 border-t border-gray-900 text-center text-gray-600 text-sm">
        <p>&copy; 2026 U.S. HOME IMPROVEMENTS. All Rights Reserved.</p>
        <div class="mt-4 flex justify-center gap-6">
            <a href="#">Privacy Policy</a> <a href="#">Terms of Service</a> <a href="#">Contact Us</a>
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

        const form = document.getElementById('mainLeadForm');
        form.addEventListener('submit', async (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('selectedService').value,
                zip: document.getElementById('zipCode').value,
                name: document.getElementById('userName').value,
                phone: document.getElementById('userPhone').value,
                timestamp: new Date()
            };
            try {
                await addDoc(collection(db, "leads"), data);
                alert("Request Sent! A pro will call you soon.");
                location.reload();
            } catch (err) { alert("Error: " + err.message); }
        });
    </script>

    <script>
        let leadState = { service: "" };
        function goToStep(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
            document.getElementById('progress').style.width = (s * 33.3) + "%";
        }
        function selectOption(type, val, next) {
            if(type === 'service') {
                const hiddenInput = document.createElement("input");
                hiddenInput.type = "hidden"; hiddenInput.id = "selectedService";
                hiddenInput.value = val; document.getElementById('mainLeadForm').appendChild(hiddenInput);
            }
            goToStep(next);
        }
    </script>
</body>
</html>
