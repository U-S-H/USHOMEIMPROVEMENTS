<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Certified Enterprise</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --accent: #00f2ff; --bg: #03050a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background-color: var(--bg); color: white; scroll-behavior: smooth; overflow-x: hidden; }
        
        /* Animated Moving Background */
        .hero-visual {
            position: relative;
            background: linear-gradient(rgba(3, 5, 10, 0.7), rgba(3, 5, 10, 0.8)), 
                        url('https://images.unsplash.com/photo-1600585154340-be6161a56a0c?auto=format&fit=crop&q=80&w=1600');
            background-size: cover; background-attachment: fixed; background-position: center;
        }

        .neon-border { border: 1px solid rgba(0, 242, 255, 0.2); transition: 0.5s; }
        .neon-border:hover { border-color: var(--accent); box-shadow: 0 0 20px rgba(0, 242, 255, 0.3); }

        .glass-panel { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(25px); border-radius: 2rem; }
        
        .step { display: none; transition: 0.5s; }
        .step.active { display: block; animation: slideIn 0.8s cubic-bezier(0.2, 1, 0.3, 1); }
        @keyframes slideIn { from { opacity: 0; transform: scale(0.95); } to { opacity: 1; transform: scale(1); } }

        .service-card img { transition: 0.7s ease; }
        .service-card:hover img { transform: scale(1.1); filter: brightness(1.1); }
        
        .floating-badge { animation: float 3s infinite ease-in-out; }
        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-[100] px-6 py-4">
        <div class="max-w-7xl mx-auto glass-panel px-8 py-4 flex justify-between items-center neon-border">
            <div class="flex flex-col">
                <span class="text-2xl font-black tracking-tighter text-transparent bg-clip-text bg-gradient-to-r from-white to-cyan-400">U.S. HOME IMPROVEMENTS</span>
                <span class="text-[8px] font-bold text-cyan-500 uppercase tracking-[0.4em]">Official National HQ</span>
            </div>
            <div class="hidden md:flex gap-10 text-[10px] font-bold uppercase tracking-[0.2em] text-gray-400">
                <a href="#quote" class="hover:text-cyan-400 transition">Get Estimates</a>
                <a href="#services" class="hover:text-cyan-400 transition">Services</a>
                <a href="#trust" class="hover:text-cyan-400 transition">Verification</a>
            </div>
            <a href="mailto:ushomeimprovement07@gmail.com" class="text-[10px] bg-cyan-600 px-5 py-2 rounded-full font-bold uppercase tracking-widest hover:bg-cyan-500 transition">Support</a>
        </div>
    </nav>

    <section class="hero-visual min-h-[90vh] flex items-center justify-center text-center px-6">
        <div class="max-w-4xl">
            <div class="floating-badge inline-block px-5 py-2 glass-panel border border-cyan-500/30 text-cyan-400 text-[10px] font-black mb-8 uppercase tracking-[0.4em]">
                Licensed & Bonded Professionals Only
            </div>
            <h1 class="text-6xl md:text-9xl font-black mb-8 leading-none tracking-tighter">Your Dream.<br><span class="text-cyan-400">Our Experts.</span></h1>
            <p class="text-gray-300 text-lg md:text-xl max-w-2xl mx-auto mb-12">The most trusted network for high-end home upgrades across the United States. Fast, free, and reliable.</p>
            
            <div class="flex justify-center gap-10 opacity-60">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Better_Business_Bureau_logo.svg/1200px-Better_Business_Bureau_logo.svg.png" class="h-8 invert" alt="BBB">
                <span class="h-8 w-[1px] bg-white/20"></span>
                <span class="text-xl font-bold italic tracking-widest self-center">SSL SECURED</span>
            </div>
        </div>
    </section>

    <section id="quote" class="py-24 px-6 -mt-32 relative z-10">
        <div class="max-w-xl mx-auto glass-panel p-10 md:p-16 shadow-[0_0_100px_rgba(0,0,0,0.5)] border-t-2 border-cyan-500/50">
            <form id="proForm">
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black mb-10 italic uppercase tracking-tighter border-b border-cyan-500/20 pb-4">01. Select Project</h2>
                    <div class="grid gap-4">
                        <button type="button" onclick="setVal('service', 'Roofing', 2)" class="w-full p-6 glass-panel neon-border text-left group flex justify-between">
                            <span class="font-bold tracking-widest uppercase">🏠 Roofing & Gutters</span> <span class="group-hover:translate-x-3 transition">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Solar', 2)" class="w-full p-6 glass-panel neon-border text-left group flex justify-between">
                            <span class="font-bold tracking-widest uppercase">☀️ Solar Grid Matrix</span> <span class="group-hover:translate-x-3 transition">→</span>
                        </button>
                        <button type="button" onclick="setVal('service', 'Kitchen', 2)" class="w-full p-6 glass-panel neon-border text-left group flex justify-between">
                            <span class="font-bold tracking-widest uppercase">🛁 Elite Kitchen Remodel</span> <span class="group-hover:translate-x-3 transition">→</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-3xl font-black mb-10 italic uppercase text-cyan-400">02. Geo-Location</h2>
                    <input type="text" id="zip" placeholder="Zip Code (e.g. 90210)" class="w-full p-5 glass-panel outline-none focus:ring-2 ring-cyan-500 mb-6 bg-transparent">
                    <select id="state" class="w-full p-5 glass-panel outline-none bg-[#0a0c12] mb-10">
                        <option value="">Select State</option>
                        <option value="TX">Texas</option><option value="CA">California</option><option value="FL">Florida</option><option value="NY">New York</option>
                    </select>
                    <button type="button" onclick="move(3)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg shadow-cyan-900/50">Verify Identity</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black mb-4 italic text-cyan-400">03. Secure Contact</h2>
                    <p class="text-gray-500 text-xs mb-10 uppercase tracking-widest font-bold">Encrypted Data Transfer</p>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-5 glass-panel outline-none mb-4 bg-transparent">
                    <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 glass-panel outline-none mb-10 bg-transparent">
                    <button type="submit" class="w-full bg-green-600 p-5 rounded-2xl font-black uppercase tracking-widest shadow-lg shadow-green-900/50">Get Estimates</button>
                </div>
            </form>
        </div>
    </section>

    <section id="services" class="py-32 max-w-7xl mx-auto px-6">
        <div class="flex flex-col md:flex-row justify-between items-end mb-20 gap-6">
            <h3 class="text-5xl font-black italic tracking-tighter uppercase leading-none">Our National<br><span class="text-cyan-400">Service Grid</span></h3>
            <p class="text-gray-500 text-sm max-w-md uppercase font-bold tracking-widest">Only the top 1% of contractors pass our 15-point verification check.</p>
        </div>
        <div class="grid md:grid-cols-3 gap-10">
            <div class="service-card group cursor-pointer">
                <div class="overflow-hidden rounded-[2.5rem] mb-6 neon-border">
                    <img src="https://images.unsplash.com/photo-1632759145351-1d592919f522?auto=format&fit=crop&q=80&w=800" class="w-full h-[300px] object-cover" alt="Roofing">
                </div>
                <h4 class="text-xl font-bold mb-2 uppercase tracking-tighter">Premium Roofing</h4>
                <p class="text-gray-500 text-sm">Engineered for durability. Guaranteed for life.</p>
            </div>
            <div class="service-card group cursor-pointer">
                <div class="overflow-hidden rounded-[2.5rem] mb-6 neon-border">
                    <img src="https://images.unsplash.com/photo-1508514177221-188b1cf16e9d?auto=format&fit=crop&q=80&w=800" class="w-full h-[300px] object-cover" alt="Solar">
                </div>
                <h4 class="text-xl font-bold mb-2 uppercase tracking-tighter">Solar Energy</h4>
                <p class="text-gray-500 text-sm">Save up to 80% on grid costs with Tier-1 tech.</p>
            </div>
            <div class="service-card group cursor-pointer">
                <div class="overflow-hidden rounded-[2.5rem] mb-6 neon-border">
                    <img src="https://images.unsplash.com/photo-1556911220-e150223bd797?auto=format&fit=crop&q=80&w=800" class="w-full h-[300px] object-cover" alt="Kitchen">
                </div>
                <h4 class="text-xl font-bold mb-2 uppercase tracking-tighter">Luxury Kitchens</h4>
                <p class="text-gray-500 text-sm">Transform the heart of your home with elite designers.</p>
            </div>
        </div>
    </section>

    <section id="trust" class="py-24 bg-white/5 border-y border-white/5">
        <div class="max-w-6xl mx-auto px-6 grid md:grid-cols-2 gap-20 items-center">
            <div>
                <h3 class="text-4xl font-black mb-8 italic uppercase tracking-tighter">Why Homeowners<br><span class="text-cyan-400">Choose USH</span></h3>
                <ul class="space-y-6">
                    <li class="flex gap-4">
                        <span class="text-cyan-400 font-black">✓</span>
                        <p class="text-sm text-gray-400 font-bold uppercase tracking-widest">Active State License Verification</p>
                    </li>
                    <li class="flex gap-4">
                        <span class="text-cyan-400 font-black">✓</span>
                        <p class="text-sm text-gray-400 font-bold uppercase tracking-widest">Minimum $1,000,000 Liability Bond</p>
                    </li>
                    <li class="flex gap-4">
                        <span class="text-cyan-400 font-black">✓</span>
                        <p class="text-sm text-gray-400 font-bold uppercase tracking-widest">Background Checked Labor Teams</p>
                    </li>
                </ul>
            </div>
            <div class="glass-panel p-10 neon-border text-center">
                <p class="text-cyan-400 text-5xl font-black mb-2 italic">A+ Rating</p>
                <p class="text-gray-500 text-xs font-bold uppercase tracking-[0.3em]">Official BBB Accredited Member</p>
                <div class="mt-8 border-t border-white/10 pt-8 flex justify-center">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Better_Business_Bureau_logo.svg/1200px-Better_Business_Bureau_logo.svg.png" class="h-10 invert opacity-40" alt="BBB">
                </div>
            </div>
        </div>
    </section>

    <footer class="py-24 px-6">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-start gap-16">
            <div>
                <p class="text-3xl font-black italic tracking-tighter mb-4">U.S. HOME IMPROVEMENTS</p>
                <p class="text-gray-600 text-[10px] font-bold uppercase tracking-[0.2em] max-w-sm">
                    Connecting USA homeowners with licensed professionals for nearly a decade. 50-state coverage. All rights reserved.
                </p>
            </div>
            <div class="flex flex-col md:items-end">
                <p class="text-cyan-500 font-bold uppercase text-[9px] tracking-widest mb-4">Network Administration</p>
                <a href="mailto:ushomeimprovement07@gmail.com" class="text-white text-2xl font-black italic hover:text-cyan-400 transition">ushomeimprovement07@gmail.com</a>
                <p class="mt-10 text-[8px] text-gray-800 font-bold uppercase tracking-[0.5em]">Reg #US-770821-B | NATIONAL PORTAL</p>
            </div>
        </div>
    </footer>

    <script>
        function move(s) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
        }
        function setVal(t, v, n) {
            if(!document.getElementById('selectedService')) {
                const h = document.createElement("input"); h.type="hidden"; h.id="selectedService";
                document.getElementById('proForm').appendChild(h);
            }
            document.getElementById('selectedService').value = v;
            move(n);
        }
    </script>
</body>
</html>
