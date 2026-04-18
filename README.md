<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>US Home Improvements | National Pro Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Poppins', sans-serif; background: #0f172a; color: white; }
        .glass-card { 
            background: rgba(255, 255, 255, 0.05); 
            backdrop-filter: blur(10px); 
            border: 1px solid rgba(255, 255, 255, 0.1); 
            border-radius: 20px; 
        }
        .step { display: none; }
        .step.active { display: block; animation: fadeIn 0.5s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body class="min-h-screen flex flex-col items-center justify-center p-4">

    <div class="text-center mb-8">
        <h1 class="text-4xl md:text-5xl font-bold text-blue-400 mb-2">U.S. HOME IMPROVEMENTS</h1>
        <p class="text-gray-400 text-lg">Trusted by Homeowners Across 50 States</p>
    </div>

    <div class="glass-card w-full max-w-lg p-8 shadow-2xl">
        <form id="leadForm">
            
            <div class="step active" id="step1">
                <h2 class="text-2xl font-semibold mb-6">What service do you need?</h2>
                <select id="service" class="w-full bg-slate-800 p-4 rounded-xl border border-slate-700 mb-6 outline-none">
                    <option value="Roofing">🏠 Roofing</option>
                    <option value="HVAC">❄️ HVAC (Heating & Cooling)</option>
                    <option value="Kitchen-Bath">🛁 Kitchen & Bath Remodel</option>
                    <option value="Windows">🪟 Windows & Doors</option>
                    <option value="Solar">☀️ Solar Panels</option>
                </select>
                <button type="button" onclick="nextStep(2)" class="w-full bg-blue-600 hover:bg-blue-500 py-4 rounded-xl font-bold transition">Next Step</button>
            </div>

            <div class="step" id="step2">
                <h2 class="text-2xl font-semibold mb-6">Property Details</h2>
                <input type="text" id="zipCode" placeholder="Enter ZIP Code (e.g. 90210)" class="w-full bg-slate-800 p-4 rounded-xl border border-slate-700 mb-4 outline-none">
                <select id="isHomeowner" class="w-full bg-slate-800 p-4 rounded-xl border border-slate-700 mb-6 outline-none">
                    <option value="">Are you the homeowner?</option>
                    <option value="Yes">Yes, I am the owner</option>
                    <option value="No">No, I am a renter</option>
                </select>
                <button type="button" onclick="nextStep(3)" class="w-full bg-blue-600 hover:bg-blue-500 py-4 rounded-xl font-bold transition">Almost There</button>
            </div>

            <div class="step" id="step3">
                <h2 class="text-2xl font-semibold mb-6">Estimated Credit Score</h2>
                <p class="text-sm text-gray-400 mb-4">Contractors use this to check for financing options.</p>
                <div class="grid grid-cols-2 gap-3 mb-6">
                    <button type="button" onclick="setCredit('Excellent (720+)')" class="bg-slate-800 p-3 rounded-lg border border-slate-700 hover:bg-blue-900 transition text-sm">Excellent (720+)</button>
                    <button type="button" onclick="setCredit('Good (660-719)')" class="bg-slate-800 p-3 rounded-lg border border-slate-700 hover:bg-blue-900 transition text-sm">Good (660-719)</button>
                    <button type="button" onclick="setCredit('Fair (620-659)')" class="bg-slate-800 p-3 rounded-lg border border-slate-700 hover:bg-blue-900 transition text-sm">Fair (620-659)</button>
                    <button type="button" onclick="setCredit('Poor (Below 620)')" class="bg-slate-800 p-3 rounded-lg border border-slate-700 hover:bg-blue-900 transition text-sm">Poor (Below 620)</button>
                </div>
                <input type="hidden" id="creditScore">
                <button type="button" onclick="nextStep(4)" class="w-full bg-blue-600 hover:bg-blue-500 py-4 rounded-xl font-bold transition">Next</button>
            </div>

            <div class="step" id="step4">
                <h2 class="text-2xl font-semibold mb-4">Contact Details</h2>
                <input type="text" id="fullName" placeholder="Full Name" class="w-full bg-slate-800 p-4 rounded-xl border border-slate-700 mb-3 outline-none">
                <input type="email" id="email" placeholder="Email Address" class="w-full bg-slate-800 p-4 rounded-xl border border-slate-700 mb-3 outline-none">
                <input type="tel" id="phone" placeholder="Phone Number" class="w-full bg-slate-800 p-4 rounded-xl border border-slate-700 mb-6 outline-none">
                <button type="submit" class="w-full bg-green-600 hover:bg-green-500 py-4 rounded-xl font-bold transition">Get My Free Quote</button>
            </div>
        </form>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getFirestore, collection, addDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

        // Paste your config here
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

        // Form Submission Logic
        document.getElementById('leadForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const leadData = {
                service: document.getElementById('service').value,
                zipCode: document.getElementById('zipCode').value,
                isHomeowner: document.getElementById('isHomeowner').value,
                creditScore: document.getElementById('creditScore').value,
                fullName: document.getElementById('fullName').value,
                email: document.getElementById('email').value,
                phone: document.getElementById('phone').value,
                timestamp: new Date()
            };

            try {
                await addDoc(collection(db, "leads"), leadData);
                alert("Thank you! A local specialist will contact you shortly.");
                location.reload();
            } catch (error) {
                console.error("Error adding document: ", error);
            }
        });
    </script>

    <script>
        function nextStep(step) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById('step' + step).classList.add('active');
        }
        function setCredit(val) {
            document.getElementById('creditScore').value = val;
            alert("Credit Selected: " + val);
        }
    </script>
</body>
</html>
