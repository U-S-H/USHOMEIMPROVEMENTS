<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Official National Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --neon: #00f2ff; --premium-gold: #d4af37; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #020408; color: white; overflow-x: hidden; }
        
        .hero-section {
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.8)), url('https://images.pexels.com/photos/1396122/pexels-photo-1396122.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1');
            background-size: cover; background-position: center; min-h: 80vh;
        }

        .glass-box { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 2rem; }
        .neon-shadow { box-shadow: 0 0 20px rgba(0, 242, 255, 0.2); transition: 0.4s; }
        .neon-shadow:hover { box-shadow: 0 0 40px rgba(0, 242, 255, 0.5); border-color: var(--neon); }

        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.5s ease forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .service-img { width: 100%; height: 250px; object-fit: cover; border-radius: 1.5rem; border: 1px solid rgba(255,255,255,0.1); }
    </style>
</head>
<body>

    <nav class="p-4 sticky top-0 z-50">
        <div class="max-w-6xl mx-auto glass-box px-6 py-4 flex justify-between items-center neon-shadow">
            <div class="flex flex-col leading-none">
                <span class="text-xl font-black text-white tracking-tighter">U.S. HOME IMPROVEMENTS</span>
                <span class="text-[7px] text-cyan-400 font-bold uppercase tracking-[0.4em]">Official National Network</span>
            </div>
            <a href="#portal" class="bg-cyan-600 text-[10px] font-black px-4 py-2 rounded-full uppercase tracking-widest hover:bg-cyan-400 transition">Support</a>
        </div>
    </nav>

    <section class="hero-section flex items-center justify-center text-center px-6 py-20">
        <div class="max-w-3xl">
            <div class="inline-block border border-cyan-500/50 px-4 py-1 rounded-full text-[9px] font-bold text-cyan-400 uppercase tracking-widest mb-6">Verified Licensed Network</div>
            <h1 class="text-5xl md:text-8xl font-black mb-6 leading-none tracking-tighter">Your Dream.<br><span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-300 to-blue-600">Our Experts.</span></h1>
            <p class="text-gray-300 text-sm md:text-lg mb-10 max-w-xl mx-auto uppercase tracking-wide">Connecting USA homeowners with the top 1% of pre-vetted local professionals.</p>
        </div>
    </section>

    <section id="portal" class="max-w-xl mx-auto px-6 -mt-24 relative z-10 pb-20">
        <div class="glass-box p-10 neon-shadow border-t-2 border-cyan-500">
            <form id="proLeadForm">
                <div class="step active" id="step1">
                    <h3 class="text-2xl font-black mb-8 italic uppercase text-cyan-400">01. Project Type</h3>
                    <div class="space-y-3">
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="w-full p-6 glass-box text-left hover:bg-white/5 flex justify-between group">
                            <span class="font-bold uppercase tracking-widest">🏠 Roofing & Gutters</span> <span>→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="w-full p-6 glass-box text-left hover:bg-white/5 flex justify-between group">
                            <span class="font-bold uppercase tracking-widest">☀️ Solar Energy Matrix</span> <span>→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Remodel', 2)" class="w-full p-6 glass-box text-left hover:bg-white/5 flex justify-between group">
                            <span class="font-bold uppercase tracking-widest">🛁 Elite Remodeling</span> <span>→</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h3 class="text-2xl font-black mb-8 italic uppercase text-cyan-400">02. Your Area</h3>
                    <input type="text" id="zip" placeholder="Zip Code (e.g. 90210)" class="w-full p-5 glass-box outline-none focus:ring-1 ring-cyan-500 mb-4 bg-transparent">
                    <select id="state" class="w-full p-5 glass-box outline-none bg-black mb-8">
                        <option value="">Select State</option>
                        <option value="TX">Texas</option><option value="CA">California</option><option value="FL">Florida</option><option value="NY">New York</option>
                    </select>
                    <button type="button" onclick="move(3)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg shadow-cyan-900/50">Verify Location</button>
                </div>

                <div class="step" id="step3">
                    <h3 class="text-2xl font-black mb-8 italic text-cyan-400 uppercase tracking-tighter">03. Secure Quotes</h3>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-5 glass-box outline-none mb-4 bg-transparent">
                    <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 glass-box outline-none mb-10 bg-transparent">
                    <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg shadow-green-900/50">Get Estimates Now</button>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-6xl mx-auto px-6 py-20">
        <h2 class="text-3xl font-black mb-16 italic uppercase text-center tracking-tighter">Our Luxury Specializations</h2>
        <div class="grid md:grid-cols-3 gap-10">
            <div class="group">
                <img src="https://images.pexels.com/photos/209251/pexels-photo-209251.jpeg?auto=compress&cs=tinysrgb&w=600" class="service-img mb-6 shadow-2xl" alt="Roofing">
                <h4 class="text-xl font-bold uppercase tracking-tighter text-cyan-400">Premium Roofing</h4>
                <p class="text-gray-500 text-xs mt-2 uppercase font-bold tracking-widest">Certified Installation & Repair</p>
            </div>
            <div class="group">
                <img src="https://images.pexels.com/photos/356036/pexels-photo-356036.jpeg?auto=compress&cs=tinysrgb&w=600" class="service-img mb-6 shadow-2xl" alt="Solar">
                <h4 class="text-xl font-bold uppercase tracking-tighter text-cyan-400">Solar Grid Tech</h4>
                <p class="text-gray-500 text-xs mt-2 uppercase font-bold tracking-widest">High Efficiency Energy Systems</p>
            </div>
            <div class="group">
                <img src="https://images.pexels.com/photos/1080721/pexels-photo-1080721.jpeg?auto=compress&cs=tinysrgb&w=600" class="service-img mb-6 shadow-2xl" alt="Kitchen">
                <h4 class="text-xl font-bold uppercase tracking-tighter text-cyan-400">Luxury Kitchens</h4>
                <p class="text-gray-500 text-xs mt-2 uppercase font-bold tracking-widest">Bespoke Interior Engineering</p>
            </div>
        </div>
    </section>

    <footer class="py-20 border-t border-white/5 bg-[#010204] text-center px-6">
        <p class="text-2xl font-black text-cyan-500 italic mb-6">U.S. HOME IMPROVEMENTS</p>
        <div class="flex justify-center gap-8 mb-10 opacity-50 grayscale hover:grayscale-0 transition duration-500">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Better_Business_Bureau_logo.svg/1200px-Better_Business_Bureau_logo.svg.png" class="h-6 invert" alt="BBB">
            <span class="text-xs self-center font-bold tracking-[0.3em]">SSL SECURED</span>
        </div>
        <p class="text-gray-600 text-[9px] font-bold uppercase tracking-[0.3em] mb-4">ushomeimprovement07@gmail.com</p>
        <p class="text-[8px] text-gray-800 font-bold uppercase tracking-[0.5em]">© 2026 National Enterprise | License US-770821-B</p>
    </footer>

    <script>
        function move(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
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
