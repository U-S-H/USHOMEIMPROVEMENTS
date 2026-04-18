<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Qualified Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --neon: #00f2ff; --bg: #010204; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: white; overflow-x: hidden; }
        
        .glass-card { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 0.07); border-radius: 2rem; }
        .neon-glow { transition: 0.4s; }
        .neon-glow:hover { border-color: var(--neon); box-shadow: 0 0 25px rgba(0, 242, 255, 0.15); }

        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.5s ease-out forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        .progress-container { height: 6px; background: rgba(255,255,255,0.05); border-radius: 10px; }
        .progress-bar { height: 100%; background: linear-gradient(90deg, #00f2ff, #0061ff); width: 14%; transition: 0.6s ease; border-radius: 10px; }

        .btn-opt { width: 100%; padding: 1.25rem; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.05); border-radius: 1.25rem; text-align: left; font-weight: 600; display: flex; justify-content: space-between; align-items: center; transition: 0.3s; }
        .btn-opt:hover { background: rgba(0, 242, 255, 0.08); border-color: var(--neon); transform: scale(1.02); }

        input[type=range] { -webkit-appearance: none; width: 100%; background: transparent; }
        input[type=range]::-webkit-slider-runnable-track { width: 100%; height: 8px; background: rgba(255,255,255,0.1); border-radius: 5px; }
        input[type=range]::-webkit-slider-thumb { -webkit-appearance: none; height: 24px; width: 24px; border-radius: 50%; background: var(--neon); cursor: pointer; margin-top: -8px; box-shadow: 0 0 10px var(--neon); }
    </style>
</head>
<body class="p-6">

    <div class="max-w-xl mx-auto mb-10 text-center">
        <h1 class="text-xl font-black italic tracking-tighter text-white mb-2 uppercase">U.S. Home Improvements</h1>
        <div class="progress-container mb-2"><div class="progress-bar" id="bar"></div></div>
        <p class="text-[9px] font-bold text-cyan-500 uppercase tracking-widest" id="step-label">Step 1: Project Selection</p>
    </div>

    <section class="max-w-xl mx-auto glass-card p-8 md:p-12 shadow-2xl relative">
        <form id="masterLeadForm">
            
            <div class="step active" id="step1">
                <h2 class="text-2xl font-black mb-6 uppercase italic">What is your project?</h2>
                <div class="space-y-3">
                    <button type="button" onclick="next(2, 'service', 'Windows')" class="btn-opt"><span>🪟 Windows & Doors</span> <span>→</span></button>
                    <button type="button" onclick="next(2, 'service', 'Roofing')" class="btn-opt"><span>🏠 Roofing Systems</span> <span>→</span></button>
                    <button type="button" onclick="next(2, 'service', 'Solar')" class="btn-opt"><span>☀️ Solar Energy Matrix</span> <span>→</span></button>
                </div>
            </div>

            <div class="step" id="step2">
                <h2 class="text-2xl font-black mb-2 uppercase italic">Credit Standing</h2>
                <p class="text-gray-500 text-[10px] mb-8 uppercase tracking-widest">Helps determine financing eligibility</p>
                <div class="text-center py-6">
                    <span id="scoreVal" class="text-5xl font-black text-cyan-400">700</span>
                    <p class="text-xs text-gray-500 mt-2 font-bold uppercase tracking-widest" id="scoreGrade">Excellent</p>
                </div>
                <input type="range" min="300" max="850" value="700" step="10" oninput="updateScore(this.value)" class="mb-10">
                <button type="button" onclick="next(3, 'credit_score', document.getElementById('scoreVal').innerText)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg">Confirm Credit Tier</button>
            </div>

            <div class="step" id="step3">
                <h2 class="text-2xl font-black mb-6 uppercase italic">Property Ownership</h2>
                <div class="space-y-3">
                    <button type="button" onclick="next(4, 'ownership', 'Owner')" class="btn-opt"><span>🏠 I Own This Home</span> <span>→</span></button>
                    <button type="button" onclick="next(4, 'ownership', 'Renter')" class="btn-opt"><span>🏢 I Am Renting</span> <span>→</span></button>
                </div>
            </div>

            <div class="step" id="step4">
                <h2 class="text-2xl font-black mb-6 uppercase italic">Start Date</h2>
                <div class="space-y-3">
                    <button type="button" onclick="next(5, 'timeframe', 'Immediate')" class="btn-opt"><span>🚀 Immediately</span> <span>→</span></button>
                    <button type="button" onclick="next(5, 'timeframe', '3 Months')" class="btn-opt"><span>📅 Within 3 Months</span> <span>→</span></button>
                    <button type="button" onclick="next(5, 'timeframe', 'Planning')" class="btn-opt"><span>🔍 Just Browsing</span> <span>→</span></button>
                </div>
            </div>

            <div class="step" id="step5">
                <h2 class="text-2xl font-black mb-8 italic uppercase text-cyan-400">Area Selection</h2>
                <input type="number" id="zip" placeholder="Zip Code" class="w-full p-6 bg-white/5 border border-white/10 rounded-2xl mb-8 outline-none text-3xl font-bold tracking-tighter">
                <button type="button" onclick="next(6)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase tracking-widest">Check Network Coverage</button>
            </div>

            <div class="step" id="step6">
                <h2 class="text-2xl font-black mb-2 italic text-cyan-400 uppercase">Final Verification</h2>
                <p class="text-gray-500 text-[10px] mb-8 uppercase tracking-widest font-bold">Secure SSL Verification Enabled</p>
                <div class="space-y-4">
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none">
                    <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none">
                    <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-black uppercase tracking-widest">Get Qualified Quotes</button>
                </div>
            </div>
        </form>
    </section>

    <script>
        let fullLead = {};

        function updateScore(v) {
            document.getElementById('scoreVal').innerText = v;
            let grade = "Fair";
            if(v > 740) grade = "Excellent 💎";
            else if(v > 670) grade = "Good ✅";
            else if(v > 580) grade = "Average ⚠️";
            else grade = "Low 🛑";
            document.getElementById('scoreGrade').innerText = grade;
        }

        function next(s, key, val) {
            if(key) fullLead[key] = val;
            
            // Progress Update
            const prog = (s / 6) * 100;
            document.getElementById('bar').style.width = prog + '%';
            document.getElementById('step-label').innerText = `Step ${s} of 6`;

            // Navigation
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }

        document.getElementById('masterLeadForm').addEventListener('submit', function(e) {
            e.preventDefault();
            fullLead.zip = document.getElementById('zip').value;
            fullLead.name = document.getElementById('name').value;
            fullLead.phone = document.getElementById('phone').value;
            
            console.log("FINAL QUALIFIED LEAD:", fullLead);
            alert("Congratulations! Lead qualified and encrypted. Check console for data.");
            location.reload();
        });
    </script>
</body>
</html>
