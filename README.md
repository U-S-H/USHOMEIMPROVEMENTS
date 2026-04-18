<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Elite National Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --neon-blue: #00f2ff; --dark-bg: #03050a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark-bg); color: white; overflow-x: hidden; }
        
        /* Premium Blur Backgrounds */
        .blob { position: absolute; width: 500px; height: 500px; background: rgba(0, 242, 255, 0.1); filter: blur(120px); border-radius: 50%; z-index: -1; }
        
        .glass-nav { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(20px); border-bottom: 1px solid rgba(255, 255, 255, 0.08); }
        .hero-gradient { background: linear-gradient(rgba(3,5,10,0.6), rgba(3,5,10,0.9)), url('https://images.pexels.com/photos/1396122/pexels-photo-1396122.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1'); background-size: cover; background-position: center; }

        .service-card { background: rgba(255, 255, 255, 0.02); border: 1px solid rgba(255, 255, 255, 0.05); transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); border-radius: 2rem; overflow: hidden; }
        .service-card:hover { border-color: var(--neon-blue); transform: translateY(-10px); background: rgba(255, 255, 255, 0.05); }

        .step { display: none; }
        .step.active { display: block; animation: fadeIn 0.6s ease forwards; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        .neon-btn { background: linear-gradient(135deg, #00f2ff 0%, #0061ff 100%); color: white; transition: 0.3s; box-shadow: 0 4px 15px rgba(0, 242, 255, 0.3); }
        .neon-btn:hover { box-shadow: 0 8px 25px rgba(0, 242, 255, 0.5); transform: scale(1.02); }
    </style>
</head>
<body>

    <div class="blob" style="top: -100px; right: -100px;"></div>
    <div class="blob" style="bottom: -100px; left: -100px; background: rgba(0, 97, 255, 0.1);"></div>

    <nav class="sticky top-0 z-50 glass-nav px-6 py-4">
        <div class="max-w-7xl mx-auto flex justify-between items-center">
            <div class="flex flex-col">
                <span class="text-xl font-extrabold tracking-tighter text-white">U.S. HOME IMPROVEMENTS</span>
                <span class="text-[8px] text-cyan-400 font-bold uppercase tracking-[0.4em]">Verified National Network</span>
            </div>
            <a href="#quote" class="neon-btn px-6 py-2 rounded-full text-[10px] font-black uppercase tracking-widest">Free Estimate</a>
        </div>
    </nav>

    <section class="hero-gradient min-h-[70vh] flex items-center justify-center text-center px-6 border-b border-white/5">
        <div class="max-w-4xl">
            <div class="inline-block px-4 py-1.5 border border-cyan-500/30 rounded-full text-[9px] font-black text-cyan-400 uppercase tracking-[0.3em] mb-8">Serving All 50 States</div>
            <h1 class="text-5xl md:text-8xl font-black mb-8 tracking-tighter leading-none">Modern Homes.<br><span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-500 italic">Masterfully Built.</span></h1>
            <p class="text-gray-400 text-lg max-w-2xl mx-auto mb-10">Compare free quotes from top-rated, licensed professionals for your next home transformation.</p>
        </div>
    </section>

    <section id="quote" class="py-20 px-6 -mt-24">
        <div class="max-w-xl mx-auto service-card p-10 md:p-14 bg-black/60 backdrop-blur-3xl shadow-2xl">
            <form id="finalForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black mb-2 uppercase italic">Select Service</h2>
                    <p class="text-gray-500 text-xs mb-10">Vetted pros for every project</p>
                    <div class="space-y-4">
                        <button type="button" onclick="setVal('service', 'Windows', 2)" class="w-full p-6 service-card text-left flex justify-between group">
                            <span class="font-bold tracking-widest uppercase text-sm">🪟 Windows & Doors</span> <span>→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="w-full p-6 service-card text-left flex justify-between group">
                            <span class="font-bold tracking-widest uppercase text-sm">🏠 Roofing & Gutters</span> <span>→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="w-full p-6 service-card text-left flex justify-between group">
                            <span class="font-bold tracking-widest uppercase text-sm">☀️ Solar Energy Matrix</span> <span>→</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black mb-8 italic text-cyan-400 uppercase">Project Location</h2>
                    <input type="text" id="zip" placeholder="Zip Code" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl mb-4 outline-none focus:border-cyan-500 transition">
                    <select id="state" class="w-full p-5 bg-[#0a0c12] border border-white/10 rounded-2xl mb-10 outline-none">
                        <option value="">Select State</option>
                        <option value="TX">Texas</option><option value="CA">California</option><option value="FL">Florida</option><option value="NY">New York</option>
                    </select>
                    <button type="button" onclick="move(3)" class="w-full neon-btn p-5 rounded-2xl font-black uppercase tracking-widest">Verify Area</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black mb-2 italic text-cyan-400 uppercase">Secure Quotes</h2>
                    <p class="text-gray-500 text-[10px] mb-10 uppercase tracking-widest">Identity protection enabled</p>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl mb-4 outline-none">
                    <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl mb-10 outline-none">
                    <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg shadow-green-900/40">Submit Request</button>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 py-20 grid md:grid-cols-3 gap-8">
        <div class="service-card group">
            <img src="https://images.pexels.com/photos/277559/pexels-photo-277559.jpeg?auto=compress&cs=tinysrgb&w=600" class="w-full h-64 object-cover opacity-80 group-hover:opacity-100 transition" alt="Windows">
            <div class="p-8">
                <h4 class="text-xl font-bold uppercase tracking-tighter mb-2">Windows & Doors</h4>
                <p class="text-gray-500 text-xs">Energy-efficient solutions for modern security.</p>
            </div>
        </div>
        <div class="service-card group">
            <img src="https://images.pexels.com/photos/1080721/pexels-photo-1080721.jpeg?auto=compress&cs=tinysrgb&w=600" class="w-full h-64 object-cover opacity-80 group-hover:opacity-100 transition" alt="Kitchen">
            <div class="p-8">
                <h4 class="text-xl font-bold uppercase tracking-tighter mb-2">Kitchen Remodel</h4>
                <p class="text-gray-500 text-xs">Custom designs for the heart of your home.</p>
            </div>
        </div>
        <div class="service-card group">
            <img src="https://images.pexels.com/photos/356036/pexels-photo-356036.jpeg?auto=compress&cs=tinysrgb&w=600" class="w-full h-64 object-cover opacity-80 group-hover:opacity-100 transition" alt="Solar">
            <div class="p-8">
                <h4 class="text-xl font-bold uppercase tracking-tighter mb-2">Solar Solutions</h4>
                <p class="text-gray-500 text-xs">Harness the sun and slash your energy bills.</p>
            </div>
        </div>
    </section>

    <footer class="py-24 border-t border-white/5 bg-[#010204] text-center px-6">
        <p class="text-2xl font-black italic tracking-tighter text-blue-500 mb-6">U.S. HOME IMPROVEMENTS</p>
        <div class="flex justify-center gap-10 opacity-40 mb-10">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Better_Business_Bureau_logo.svg/1200px-Better_Business_Bureau_logo.svg.png" class="h-6 invert" alt="BBB">
        </div>
        <p class="text-gray-600 text-[10px] font-bold uppercase tracking-widest mb-4">ushomeimprovement07@gmail.com</p>
        <p class="text-[8px] text-gray-800 font-bold uppercase tracking-[0.5em]">License #US-770821-B | © 2026 National Network</p>
    </footer>

    <script>
        function move(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }
        function setVal(t, v, n) {
            if(!document.getElementById('selectedService')) {
                const h = document.createElement("input"); h.type="hidden"; h.id="selectedService";
                document.getElementById('finalForm').appendChild(h);
            }
            document.getElementById('selectedService').value = v;
            move(n);
        }
    </script>
</body>
</html>
