<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Pro Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; background: #0b0f1a; color: white; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .step { display: none; }
        .step.active { display: block; animation: slideIn 0.4s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }
        .btn-gradient { background: linear-gradient(90deg, #2563eb, #3b82f6); transition: all 0.3s ease; }
        .btn-gradient:hover { transform: translateY(-2px); box-shadow: 0 10px 20px rgba(37, 99, 235, 0.3); }
    </style>
</head>
<body class="min-h-screen flex flex-col items-center py-10 px-4">

    <nav class="w-full max-w-6xl flex justify-between items-center mb-16">
        <div class="text-2xl font-extrabold tracking-tighter text-blue-500">U.S. HOME IMPROVEMENTS</div>
        <div class="hidden md:block text-sm text-gray-400 uppercase tracking-widest">Premium Service Network</div>
    </nav>

    <div class="text-center mb-12">
        <h1 class="text-5xl md:text-6xl font-extrabold mb-4 leading-tight">Upgrade Your Home <br><span class="text-blue-500 text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600">The Smart Way.</span></h1>
        <p class="text-gray-400 max-w-xl mx-auto">Get matched with top-rated local contractors in minutes. Professional service, guaranteed quality.</p>
    </div>

    <div class="glass w-full max-w-lg p-8 rounded-3xl shadow-2xl relative overflow-hidden">
        <div class="absolute top-0 left-0 w-full h-1 bg-gray-800">
            <div id="progress" class="h-full bg-blue-500 transition-all duration-500" style="width: 25%;"></div>
        </div>

        <form id="mainLeadForm">
            <div class="step active" id="step1">
                <h3 class="text-xl font-bold mb-6 italic text-blue-300 underline">01. Choose Service</h3>
                <div class="grid grid-cols-1 gap-3 mb-8 text-left">
                    <button type="button" onclick="selectOption('service', 'Roofing', 2)" class="p-4 rounded-xl border border-gray-700 bg-gray-800/50 hover:border-blue-500 hover:bg-blue-500/10 transition text-left">🏠 Roofing Services</button>
                    <button type="button" onclick="selectOption('service', 'HVAC', 2)" class="p-4 rounded-xl border border-gray-700 bg-gray-800/50 hover:border-blue-500 hover:bg-blue-500/10 transition text-left">❄️ HVAC Installation</button>
                    <button type="button" onclick="selectOption('service', 'Solar', 2)" class="p-4 rounded-xl border border-gray-700 bg-gray-800/50 hover:border-blue-500 hover:bg-blue-500/10 transition text-left">☀️ Solar Energy Solutions</button>
                    <button type="button" onclick="selectOption('service', 'Remodeling', 2)" class="p-4 rounded-xl border border-gray-700 bg-gray-800/50 hover:border-blue-500 hover:bg-blue-500/10 transition text-left">🛁 Kitchen & Bath Remodel</button>
                </div>
                <input type="hidden" id="selectedService">
            </div>

            <div class="step" id="step2">
                <h3 class="text-xl font-bold mb-6 italic text-blue-300 underline">02. Project Location</h3>
                <input type="text" id="zipCode" placeholder="Enter ZIP Code" class="w-full bg-gray-900 border border-gray-700 p-4 rounded-xl mb-4 focus:border-blue-500 outline-none">
                <select id="state" class="w-full bg-gray-900 border border-gray-700 p-4 rounded-xl mb-6 outline-none focus:border-blue-500 text-gray-400">
                    <option value="">Select Your State</option>
                    <option value="AL">Alabama</option><option value="CA">California</option><option value="FL">Florida</option>
                    <option value="NY">New York</option><option value="TX">Texas</option>
                    </select>
                <button type="button" onclick="goToStep(3)" class="w-full btn-gradient py-4 rounded-xl font-bold">Continue</button>
            </div>

            <div class="step" id="step3">
                <h3 class="text-xl font-bold mb-6 italic text-blue-300 underline">03. Verification</h3>
                <div class="space-y-4 mb-6">
                    <p class="text-sm text-gray-400 text-center">Do you own the property?</p>
                    <div class="flex gap-4">
                        <button type="button" onclick="selectOption('owner', 'Yes', 4)" class="flex-1 p-4 rounded-xl border border-gray-700 bg-gray-800/50 hover:border-blue-500 transition">Yes</button>
                        <button type="button" onclick="selectOption('owner', 'No', 4)" class="flex-1 p-4 rounded-xl border border-gray-700 bg-gray-800/50 hover:border-blue-500 transition">No</button>
                    </div>
                </div>
                <input type="hidden" id="isOwner">
            </div>

            <div class="step" id="step4">
                <h3 class="text-xl font-bold mb-6 italic text-blue-300 underline">04. Contact Details</h3>
                <div class="space-y-4 mb-6">
                    <input type="text" id="userName" placeholder="Full Name" class="w-full bg-gray-900 border border-gray-700 p-4 rounded-xl focus:border-blue-500 outline-none">
                    <input type="tel" id="userPhone" placeholder="Phone Number" class="w-full bg-gray-900 border border-gray-700 p-4 rounded-xl focus:border-blue-500 outline-none">
                </div>
                <button type="submit" class="w-full bg-green-600 hover:bg-green-500 py-4 rounded-xl font-bold transition shadow-lg">Submit Request</button>
            </div>
        </form>
    </div>

    <footer class="mt-20 text-gray-600 text-xs text-center">
        &copy; 2026 U.S. HOME IMPROVEMENTS. All Rights Reserved. <br>
        Licensed & Insured Across 50 States.
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

        // Form Submit
        document.getElementById('mainLeadForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const btn = e.target.querySelector('button[type="submit"]');
            btn.innerText = "Processing...";
            
            const leadData = {
                service: document.getElementById('selectedService').value,
                zip: document.getElementById('zipCode').value,
                state: document.getElementById('state').value,
                owner: document.getElementById('isOwner').value,
                name: document.getElementById('userName').value,
                phone: document.getElementById('userPhone').value,
                date: new Date().toLocaleString()
            };

            try {
                await addDoc(collection(db, "leads"), leadData);
                alert("Success! We've received your request.");
                window.location.reload();
            } catch (err) {
                alert("Error saving lead. Check Firebase Rules!");
                btn.innerText = "Submit Request";
            }
        });
    </script>

    <script>
        function goToStep(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
            document.getElementById('progress').style.width = (s * 25) + "%";
        }

        function selectOption(type, val, next) {
            if(type === 'service') document.getElementById('selectedService').value = val;
            if(type === 'owner') document.getElementById('isOwner').value = val;
            goToStep(next);
        }
    </script>
</body>
</html>
