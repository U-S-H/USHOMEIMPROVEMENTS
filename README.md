<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | NEON FUTURE</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;700;800&display=swap" rel="stylesheet">
    <style>
        :root { --neon-blue: #00f2ff; --neon-purple: #bc13fe; --neon-pink: #ff00ff; }
        
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background: linear-gradient(45deg, #0f0c29, #302b63, #24243e);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            color: white;
            overflow-x: hidden;
        }

        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .neon-glass {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border: 2px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.8), inset 0 0 15px rgba(255, 255, 255, 0.05);
            border-radius: 30px;
            transition: all 0.4s ease;
        }

        .neon-glass:hover {
            border-color: var(--neon-blue);
            box-shadow: 0 0 25px var(--neon-blue);
            transform: scale(1.02);
        }

        .neon-text {
            color: #fff;
            text-shadow: 0 0 7px #fff, 0 0 10px #fff, 0 0 21px var(--neon-blue), 0 0 42px var(--neon-blue);
        }

        .step { display: none; }
        .step.active { display: block; animation: neonSlide 0.7s cubic-bezier(0.175, 0.885, 0.32, 1.275); }

        @keyframes neonSlide {
            from { opacity: 0; transform: translateY(50px) rotate(-2deg); }
            to { opacity: 1; transform: translateY(0) rotate(0deg); }
        }

        .btn-neon {
            background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple));
            border: none;
            color: white;
            font-weight: 800;
            text-transform: uppercase;
            letter-spacing: 2px;
            box-shadow: 0 0 15px var(--neon-purple);
            transition: 0.3s;
        }

        .btn-neon:hover {
            box-shadow: 0 0 30px var(--neon-pink);
            transform: translateY(-3px);
        }

        .floating { animation: floating 3s ease-in-out infinite; }
        @keyframes floating {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-15px); }
            100% { transform: translateY(0px); }
        }

        input, select {
            background: rgba(255, 255, 255, 0.05) !important;
            border: 1px solid var(--neon-blue) !important;
            color: white !important;
            border-radius: 15px !important;
        }
    </style>
</head>
<body class="min-h-screen">

    <nav class="p-6">
        <div class="max-w-6xl mx-auto neon-glass px-8 py-4 flex justify-between items-center">
            <div class="flex flex-col">
                <h1 class="text-2xl font-extrabold tracking-tighter neon-text">U.S. HOME IMPROVEMENTS</h1>
                <span class="text-[9px] font-bold text-cyan-400 tracking-[0.3em] uppercase">Hyper-Modern National Network</span>
            </div>
            <div class="hidden md:flex gap-6 items-center">
                <span class="px-3 py-1 bg-white/10 rounded-full text-[10px] font-bold border border-cyan-500/50">⚡ ONLINE</span>
                <button class="btn-neon px-6 py-2 rounded-full text-[10px]">Portal Access</button>
            </div>
        </div>
    </nav>

    <header class="text-center py-16 px-6">
        <div class="floating inline-block mb-6">
            <span class="bg-gradient-to-r from-cyan-400 to-purple-500 p-1 rounded-full px-6 py-2 font-bold text-[10px] uppercase tracking-widest shadow-lg shadow-cyan-500/50">Industry Leaders 2026</span>
        </div>
        <h2 class="text-6xl md:text-8xl font-extrabold mb-6 tracking-tighter italic">Transforming <br><span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-300 via-purple-400 to-pink-500">The Future.</span></h2>
        <p class="text-cyan-100/70 max-w-2xl mx-auto text-lg mb-12">The world's first AI-integrated hyper-modern home improvement network.</p>
    </header>

    <section class="max-w-xl mx-auto px-6 mb-24">
        <div class="neon-glass p-10 md:p-14 relative overflow-hidden">
            <div class="absolute -top-10 -right-10 w-40 h-40 bg-purple-600/30 blur-[80px]"></div>
            
            <form id="neonLeadForm">
                <div class="step active" id="step1">
                    <h3 class="text-3xl font-black mb-8 italic uppercase tracking-tighter neon-text">Select Category</h3>
                    <div class="grid gap-4">
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="p-6 neon-glass border-white/5 text-left group flex justify-between">
                            <span class="font-bold tracking-widest uppercase">Roofing Systems</span>
                            <span class="group-hover:translate-x-3 transition duration-500">🛸</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="p-6 neon-glass border-white/5 text-left group flex justify-between">
                            <span class="font-bold tracking-widest uppercase">Solar Matrix</span>
                            <span class="group-hover:translate-x-3 transition duration-500">💎</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Kitchen', 2)" class="p-6 neon-glass border-white/5 text-left group flex justify-between">
                            <span class="font-bold tracking-widest uppercase">Elite Remodel</span>
                            <span class="group-hover:translate-x-3 transition duration-500">🌠</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h3 class="text-3xl font-black mb-8 italic neon-text uppercase">Geo-Location</h3>
                    <div class="space-y-6">
                        <input type="text" id="zip" placeholder="Zip Code" class="w-full p-5 outline-none focus:scale-105 transition shadow-2xl">
                        <select id="state" class="w-full p-5 outline-none">
                            <option value="">Choose State</option>
                            <option value="TX">Texas</option><option value="CA">California</option>
                        </select>
                        <button type="button" onclick="move(3)" class="w-full btn-neon p-5 rounded-2xl">Initialize Verification</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h3 class="text-3xl font-black mb-8 italic neon-text uppercase">Secure Contact</h3>
                    <div class="space-y-6">
                        <input type="text" id="name" placeholder="Full Name" class="w-full p-5 outline-none">
                        <input type="tel" id="phone" placeholder="Phone Number" class="w-full p-5 outline-none">
                        <button type="submit" class="w-full btn-neon p-5 rounded-2xl shadow-[0_0_20px_#bc13fe]">Get Estimates Now</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-6xl mx-auto px-6 grid md:grid-cols-3 gap-8 pb-24 text-center">
        <div class="neon-glass p-8">
            <h4 class="text-cyan-400 font-bold mb-2">VERIFIED</h4>
            <p class="text-xs text-gray-400">Licensed & Bonded Pros Only</p>
        </div>
        <div class="neon-glass p-8">
            <h4 class="text-purple-400 font-bold mb-2">A+ RATED</h4>
            <p class="text-xs text-gray-400">Better Business Bureau Member</p>
        </div>
        <div class="neon-glass p-8">
            <h4 class="text-pink-400 font-bold mb-2">SECURE</h4>
            <p class="text-xs text-gray-400">256-Bit SSL Encrypted Lead Portal</p>
        </div>
    </section>

    <footer class="p-10 border-t border-white/10 text-center">
        <p class="neon-text font-black text-xl mb-4 italic">U.S. HOME IMPROVEMENTS</p>
        <p class="text-cyan-300/50 text-[10px] tracking-[0.5em] mb-4 uppercase">ushomeimprovement07@gmail.com</p>
        <div class="flex justify-center gap-6 grayscale opacity-50 mb-8">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Better_Business_Bureau_logo.svg/1200px-Better_Business_Bureau_logo.svg.png" class="h-6 invert" alt="BBB">
        </div>
        <p class="text-[8px] text-gray-600 font-bold uppercase tracking-widest">© 2026 Official National Network | Reg #US-770821-B</p>
    </footer>

    <script>
        function move(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }
        function setVal(t, v, n) {
            if(!document.getElementById('selectedService')) {
                const h = document.createElement("input"); h.type="hidden"; h.id="selectedService";
                document.getElementById('neonLeadForm').appendChild(h);
            }
            document.getElementById('selectedService').value = v;
            move(n);
        }
    </script>
</body>
</html>
