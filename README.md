<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Licensed Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: #05070a; color: white; }
        .glass-card { background: rgba(255, 255, 255, 0.05); backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 24px; }
        .step { display: none; }
        .step.active { display: block; }
        input, select { background: rgba(255,255,255,0.1) !important; color: white !important; border: 1px solid rgba(255,255,255,0.2) !important; }
        ::placeholder { color: rgba(255,255,255,0.5); }
    </style>
</head>
<body class="p-4 md:p-10">

    <header class="max-w-4xl mx-auto glass-card p-6 mb-10 flex justify-between items-center shadow-2xl">
        <div>
            <h1 class="text-xl font-extrabold text-blue-500 tracking-tighter uppercase">U.S. Home Improvements</h1>
            <p class="text-[10px] text-gray-400 font-bold uppercase tracking-widest">National Vetted Network</p>
        </div>
        <a href="#quote" class="bg-blue-600 text-white px-5 py-2 rounded-xl text-xs font-bold uppercase tracking-widest hover:bg-blue-500">Start Project</a>
    </header>

    <main class="max-w-xl mx-auto text-center">
        <h2 class="text-4xl font-extrabold mb-6 leading-tight">Upgrade Your Home With <span class="text-blue-500">Certified Pros.</span></h2>
        
        <div id="quote" class="glass-card p-8 md:p-12 shadow-2xl border-t-4 border-blue-500">
            <form id="leadForm">
                <div class="step active" id="step1">
                    <h3 class="text-2xl font-bold mb-2">01. Choose Service</h3>
                    <p class="text-gray-400 text-sm mb-8">All pros are verified & insured</p>
                    <div class="grid gap-3">
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="w-full p-5 glass-card hover:bg-blue-600/20 text-left flex justify-between items-center transition">
                            <span>🏠 Roofing & Exteriors</span> <span class="text-blue-500">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="w-full p-5 glass-card hover:bg-blue-600/20 text-left flex justify-between items-center transition">
                            <span>☀️ Solar Energy</span> <span class="text-blue-500">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Kitchen', 2)" class="w-full p-5 glass-card hover:bg-blue-600/20 text-left flex justify-between items-center transition">
                            <span>🛁 Kitchen Remodel</span> <span class="text-blue-500">→</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h3 class="text-2xl font-bold mb-8 italic text-blue-400">02. Project Location</h3>
                    <input type="text" id="zip" placeholder="Zip Code" class="w-full p-4 rounded-xl mb-4 outline-none">
                    <select id="state" class="w-full p-4 rounded-xl mb-8 outline-none">
                        <option value="">Select State</option>
                        <option value="TX">Texas</option><option value="CA">California</option><option value="FL">Florida</option><option value="NY">New York</option>
                    </select>
                    <button type="button" onclick="move(3)" class="w-full bg-blue-600 p-4 rounded-xl font-bold uppercase tracking-widest">Next Step</button>
                </div>

                <div class="step" id="step3">
                    <h3 class="text-2xl font-bold mb-8 italic text-blue-400">03. Contact Verification</h3>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-4 rounded-xl mb-4 outline-none">
                    <input type="tel" id="phone" placeholder="Phone Number" class="w-full p-4 rounded-xl mb-8 outline-none">
                    <button type="submit" class="w-full bg-green-600 p-4 rounded-xl font-bold uppercase tracking-widest">Get Free Quotes</button>
                </div>
            </form>
        </div>
    </main>

    <footer class="mt-20 py-10 text-center border-t border-white/10">
        <p class="text-blue-500 font-bold mb-2">U.S. HOME IMPROVEMENTS</p>
        <a href="mailto:ushomeimprovement07@gmail.com" class="text-gray-400 text-sm hover:underline">ushomeimprovement07@gmail.com</a>
        <p class="text-[9px] text-gray-600 mt-6 tracking-widest uppercase">© 2026 National License #US-770821-B</p>
    </footer>

    <script>
        function move(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }
        function setVal(t, v, n) {
            if(!document.getElementById('selectedService')) {
                const h = document.createElement("input"); h.type="hidden"; h.id="selectedService";
                document.getElementById('leadForm').appendChild(h);
            }
            document.getElementById('selectedService').value = v;
            move(n);
        }
    </script>
</body>
</html>
