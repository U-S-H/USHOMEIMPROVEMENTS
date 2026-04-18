<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Enterprise Lead Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --neon-blue: #00f2ff; --dark-bg: #010206; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark-bg); color: white; overflow-x: hidden; }
        
        .glass-panel { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 2.5rem; }
        .neon-shadow { transition: 0.5s; }
        .neon-shadow:hover { border-color: var(--neon-blue); box-shadow: 0 0 30px rgba(0, 242, 255, 0.2); }

        .step { display: none; }
        .step.active { display: block; animation: slideUp 0.6s cubic-bezier(0.19, 1, 0.22, 1) forwards; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(40px); } to { opacity: 1; transform: translateY(0); } }

        .progress-bar { height: 4px; background: rgba(255,255,255,0.1); border-radius: 10px; overflow: hidden; }
        .progress-fill { height: 100%; background: linear-gradient(90deg, #00f2ff, #0061ff); width: 20%; transition: 0.8s ease; }

        .option-btn { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.05); padding: 1.5rem; border-radius: 1.5rem; text-align: left; transition: 0.3s; width: 100%; display: flex; justify-content: space-between; align-items: center; }
        .option-btn:hover { background: rgba(0, 242, 255, 0.1); border-color: var(--neon-blue); transform: scale(1.02); }
    </style>
</head>
<body class="py-10 px-4">

    <div class="max-w-xl mx-auto mb-8 px-4">
        <div class="flex justify-between text-[10px] font-bold uppercase tracking-widest text-cyan-400 mb-2">
            <span>Project Qualification</span>
            <span id="progress-text">Step 1 of 5</span>
        </div>
        <div class="progress-bar"><div class="progress-fill" id="fill"></div></div>
    </div>

    <section class="max-w-xl mx-auto relative">
        <div class="glass-panel p-8 md:p-12 shadow-2xl border-t-2 border-cyan-500/50">
            <form id="qualifyForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black mb-2 uppercase italic tracking-tighter">01. Service</h2>
                    <p class="text-gray-500 text-xs mb-8">What are we building today?</p>
                    <div class="space-y-3">
                        <button type="button" onclick="nextStep(2, 'service', 'Windows')" class="option-btn group"><span class="font-bold">🪟 WINDOWS & DOORS</span><span class="opacity-0 group-hover:opacity-100 transition">→</span></button>
                        <button type="button" onclick="nextStep(2, 'service', 'Roofing')" class="option-btn group"><span class="font-bold">🏠 ROOFING SYSTEMS</span><span class="opacity-0 group-hover:opacity-100 transition">→</span></button>
                        <button type="button" onclick="nextStep(2, 'service', 'Solar')" class="option-btn group"><span class="font-bold">☀️ SOLAR ENERGY</span><span class="opacity-0 group-hover:opacity-100 transition">→</span></button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-3xl font-black mb-2 uppercase italic tracking-tighter">02. Timeframe</h2>
                    <p class="text-gray-500 text-xs mb-8">How soon do you want to start?</p>
                    <div class="space-y-3">
                        <button type="button" onclick="nextStep(3, 'time', 'Urgent')" class="option-btn group"><span class="font-bold">🚀 AS SOON AS POSSIBLE</span><span>→</span></button>
                        <button type="button" onclick="nextStep(3, 'time', '1-3 Months')" class="option-btn group"><span class="font-bold">📅 WITHIN 1-3 MONTHS</span><span>→</span></button>
                        <button type="button" onclick="nextStep(3, 'time', 'Planning')" class="option-btn group"><span class="font-bold">🔍 JUST PLANNING</span><span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black mb-2 uppercase italic tracking-tighter">03. Property</h2>
                    <p class="text-gray-500 text-xs mb-8">Do you own this property?</p>
                    <div class="space-y-3">
                        <button type="button" onclick="nextStep(4, 'ownership', 'Yes')" class="option-btn group"><span class="font-bold">✅ YES, I AM THE OWNER</span><span>→</span></button>
                        <button type="button" onclick="nextStep(4, 'ownership', 'No')" class="option-btn group"><span class="font-bold">❌ NO, I AM RENTING</span><span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-3xl font-black mb-8 italic uppercase text-cyan-400">04. Zip Code</h2>
                    <input type="number" id="zip" placeholder="Enter Zip Code" class="w-full p-6 bg-white/5 border border-white/10 rounded-2xl mb-8 outline-none focus:border-cyan-500 text-2xl font-bold tracking-widest">
                    <button type="button" onclick="nextStep(5)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg shadow-cyan-900/50">Verify Network Coverage</button>
                </div>

                <div class="step" id="step5">
                    <h2 class="text-3xl font-black mb-2 italic text-cyan-400 uppercase">Final Step</h2>
                    <p class="text-gray-500 text-[10px] mb-8 uppercase tracking-widest font-bold">Secure SSL Verification Enabled</p>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none">
                        <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none">
                        <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg shadow-green-900/40">Get Verified Estimates</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <footer class="mt-20 text-center">
        <p class="text-cyan-500 font-bold tracking-tighter text-xl italic mb-2 uppercase">U.S. Home Improvements</p>
        <p class="text-gray-600 text-[8px] uppercase tracking-[0.4em]">Official National HQ | License #US-770821-B</p>
    </footer>

    <script>
        let leadData = {};

        function nextStep(s, key, val) {
            if(key) leadData[key] = val;
            
            // Progress Bar Logic
            const percent = (s / 5) * 100;
            document.getElementById('fill').style.width = percent + '%';
            document.getElementById('progress-text').innerText = `Step ${s} of 5`;

            // Switch Steps
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }

        document.getElementById('qualifyForm').addEventListener('submit', function(e) {
            e.preventDefault();
            leadData.zip = document.getElementById('zip').value;
            leadData.name = document.getElementById('name').value;
            leadData.phone = document.getElementById('phone').value;
            
            console.log("Qualified Lead Data Captured:", leadData);
            alert("Congratulations sweetie! Your project has been qualified. Our experts will contact you shortly.");
            location.reload();
        });
    </script>
</body>
</html>
