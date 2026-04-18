<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Professional Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --slate: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--slate); scroll-behavior: smooth; }
        
        .hero-bg {
            background: linear-gradient(rgba(15, 23, 42, 0.85), rgba(15, 23, 42, 0.80)),
                        url('./WA_1776549402527.jpeg');
            background-size: cover; background-position: center;
        }

        .glass-panel {
            background: rgba(255, 255, 255, 0.98); backdrop-filter: blur(20px);
            border-radius: 2.5rem; border: 1px solid white; box-shadow: 0 40px 100px rgba(0,0,0,0.08);
        }

        .step { display: none; }
        .step.active { display: block; animation: slideFade 0.5s ease-out; }
        @keyframes slideFade { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .input-matrix {
            width: 100%; padding: 1.25rem; border-radius: 1.25rem; border: 2px solid #f1f5f9;
            font-weight: 600; outline: none; transition: 0.3s;
        }
        .input-matrix:focus { border-color: var(--neon); box-shadow: 0 0 15px rgba(0, 242, 255, 0.1); }

        .btn-elite {
            background: var(--slate); color: white; padding: 1.3rem; border-radius: 1.25rem;
            font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; transition: 0.4s;
        }
        .btn-elite:hover { background: var(--neon); color: var(--slate); transform: translateY(-3px); }
        
        .feature-card {
            background: white; border-radius: 2rem; border: 1px solid #f1f5f9; transition: 0.4s; overflow: hidden;
        }
        .feature-card:hover { transform: translateY(-10px); border-color: var(--neon); }

        /* Modal Style */
        .modal { display: none; position: fixed; inset: 0; background: rgba(15, 23, 42, 0.9); z-index: 1000; padding: 2rem; }
        .modal-content { background: white; max-width: 800px; margin: auto; border-radius: 2rem; padding: 3rem; max-height: 80vh; overflow-y: auto; }
    </style>
</head>
<body>

    <header class="hero-bg h-[75vh] flex flex-col items-center justify-center text-center px-6 text-white relative">
        <div class="absolute top-8 left-8 flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" alt="Logo" class="h-12">
            <span class="text-[10px] font-black tracking-[0.3em] uppercase border-l-2 border-cyan-400 pl-4">National Enterprise</span>
        </div>
        <h1 class="text-5xl md:text-8xl font-black italic tracking-tighter uppercase leading-none mt-10">UPGRADE YOUR<br>LIFESTYLE</h1>
        <p class="text-cyan-400 font-bold tracking-[0.5em] text-[11px] mt-8 uppercase">Nationwide Certified Home Improvement Network</p>
        <div class="mt-12 flex gap-4">
            <a href="#portal" class="bg-white text-slate-900 px-10 py-4 rounded-full font-black text-xs uppercase hover:bg-cyan-400 transition shadow-2xl">Get Free Quote</a>
            <a href="#benefits" class="border-2 border-white/20 px-10 py-4 rounded-full font-black text-xs uppercase hover:bg-white/10 transition">Our Benefits</a>
        </div>
    </header>

    <section id="benefits" class="py-24 bg-white">
        <div class="max-w-6xl mx-auto px-6">
            <div class="grid md:grid-cols-3 gap-12 text-center">
                <div class="p-8">
                    <div class="text-4xl mb-4">🛡️</div>
                    <h4 class="font-black uppercase text-sm mb-3">Lifetime Warranty</h4>
                    <p class="text-xs text-slate-400 leading-relaxed">Our materials and labor come with a nationwide lifetime guarantee for your peace of mind.</p>
                </div>
                <div class="p-8">
                    <div class="text-4xl mb-4">⚡</div>
                    <h4 class="font-black uppercase text-sm mb-3">Energy Efficiency</h4>
                    <p class="text-xs text-slate-400 leading-relaxed">Save up to 40% on your monthly utility bills with our premium energy-rated installations.</p>
                </div>
                <div class="p-8">
                    <div class="text-4xl mb-4">👷</div>
                    <h4 class="font-black uppercase text-sm mb-3">Certified Experts</h4>
                    <p class="text-xs text-slate-400 leading-relaxed">Every technician in our network is licensed, bonded, and fully insured for structural work.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="portal" class="max-w-3xl mx-auto -mt-32 px-4 mb-32 relative z-20">
        <div class="glass-panel p-10 md:p-16 border-t-[12px] border-slate-900 shadow-2xl">
            <form id="masterLeadForm">
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">01. Service Type</h2>
                    <div class="space-y-6">
                        <select id="homeowner" class="input-matrix" required>
                            <option value="">Do you own this home?</option>
                            <option value="Yes">Yes, I am the owner</option>
                            <option value="No">No, I am a tenant</option>
                        </select>
                        <select id="service" class="input-matrix" required>
                            <option value="">What is your project?</option>
                            <option value="Windows">Replacement Windows</option>
                            <option value="Doors">Exterior Doors</option>
                            <option value="Roofing">Full Roofing</option>
                            <option value="Solar">Solar Panels</option>
                            <option value="Remodel">Interior Remodeling</option>
                        </select>
                        <button type="button" onclick="goNext('step2')" class="btn-elite">Next Step</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">02. Eligibility</h2>
                    <div class="space-y-6">
                        <select id="credit" class="input-matrix" required>
                            <option value="">Estimated Credit Score</option>
                            <option value="720+">720+ (Excellent)</option>
                            <option value="660-719">660-719 (Good)</option>
                            <option value="Below 660">Below 660 (Fair)</option>
                        </select>
                        <select id="ready" class="input-matrix" required>
                            <option value="">Start Timeline</option>
                            <option value="ASAP">Immediately</option>
                            <option value="1-3-Months">1-3 Months</option>
                        </select>
                        <button type="button" onclick="goNext('step3')" class="btn-elite">Verify Identity</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black italic mb-8 uppercase tracking-tight">03. Deployment</h2>
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Name" class="input-matrix" required>
                        <input type="tel" id="cPhone" placeholder="Mobile Number" class="input-matrix" required>
                        <input type="email" id="cEmail" placeholder="Email Address" class="input-matrix" required>
                        <input type="text" id="cZip" placeholder="Zip Code" class="input-matrix" required>
                        <p class="text-[9px] text-slate-400 font-bold uppercase text-center mt-4">By clicking below, you agree to our Privacy Policy and Terms.</p>
                        <button type="submit" class="btn-elite bg-cyan-500 text-slate-900">Confirm Qualification</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 mb-32">
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
            <div class="feature-card p-6">
                <img src="./WA_1776549555727.jpeg" class="rounded-2xl mb-6 shadow-lg">
                <h4 class="font-black uppercase text-xs">Windows Elite</h4>
                <p class="text-[10px] text-slate-400 mt-2 uppercase font-bold">Premium Glass Matrix</p>
            </div>
            <div class="feature-card p-6">
                <img src="./WA_1776549622236.jpeg" class="rounded-2xl mb-6 shadow-lg">
                <h4 class="font-black uppercase text-xs">Security Doors</h4>
                <p class="text-[10px] text-slate-400 mt-2 uppercase font-bold">Maximum Reinforcement</p>
            </div>
            <div class="feature-card p-6">
                <img src="./WA_1776549716792.jpeg" class="rounded-2xl mb-6 shadow-lg">
                <h4 class="font-black uppercase text-xs">Roofing Systems</h4>
                <p class="text-[10px] text-slate-400 mt-2 uppercase font-bold">Lifetime Structure</p>
            </div>
            <div class="feature-card p-6">
                <img src="./WA_1776549781247.jpeg" class="rounded-2xl mb-6 shadow-lg">
                <h4 class="font-black uppercase text-xs">Solar Matrix</h4>
                <p class="text-[10px] text-slate-400 mt-2 uppercase font-bold">Energy Independence</p>
            </div>
        </div>
    </section>

    <footer class="bg-slate-900 pt-20 pb-10 text-white px-6">
        <div class="max-w-6xl mx-auto">
            <div class="grid md:grid-cols-4 gap-12 mb-16 border-b border-white/10 pb-16">
                <div class="col-span-1 md:col-span-2">
                    <img src="./WA_1776550450872.jpeg" class="h-10 mb-6 grayscale brightness-200">
                    <p class="text-[11px] font-bold text-white/50 leading-relaxed uppercase pr-10">
                        U.S. HOME IMPROVEMENTS is a national leader in structural residential modernization. We connect homeowners with certified, top-tier contractors to ensure every project meets the national standard for quality and safety.
                    </p>
                </div>
                <div>
                    <h5 class="font-black uppercase text-xs mb-6 text-cyan-400">Navigation</h5>
                    <ul class="text-[10px] font-bold uppercase space-y-4 text-white/70">
                        <li><a href="#" class="hover:text-cyan-400">Home</a></li>
                        <li><a href="#benefits" class="hover:text-cyan-400">Benefits</a></li>
                        <li><a href="#portal" class="hover:text-cyan-400">Quotes</a></li>
                    </ul>
                </div>
                <div>
                    <h5 class="font-black uppercase text-xs mb-6 text-cyan-400">Legal Matrix</h5>
                    <ul class="text-[10px] font-bold uppercase space-y-4 text-white/70">
                        <li><button onclick="toggleModal('privacyModal')" class="hover:text-cyan-400">Privacy Policy</button></li>
                        <li><button onclick="toggleModal('termsModal')" class="hover:text-cyan-400">Terms of Service</button></li>
                        <li><button onclick="toggleModal('detailsModal')" class="hover:text-cyan-400">Company Details</button></li>
                    </ul>
                </div>
            </div>
            <p class="text-center text-[9px] font-black uppercase tracking-[0.6em] text-white/30">U.S. HOME IMPROVEMENTS • EST 2026 • ALL RIGHTS RESERVED</p>
        </div>
    </footer>

    <div id="privacyModal" class="modal">
        <div class="modal-content">
            <h2 class="text-3xl font-black uppercase mb-6">Privacy Policy</h2>
            <div class="text-xs text-slate-600 leading-relaxed space-y-4 uppercase font-bold">
                <p>1. Data Collection: We collect only the information necessary to provide accurate home improvement quotes.</p>
                <p>2. Data Security: Your information is encrypted and never sold to third-party telemarketers.</p>
                <p>3. Opt-Out: You can request to delete your data from our matrix at any time.</p>
            </div>
            <button onclick="toggleModal('privacyModal')" class="mt-10 btn-elite">Close</button>
        </div>
    </div>

    <div id="detailsModal" class="modal">
        <div class="modal-content">
            <h2 class="text-3xl font-black uppercase mb-6">Company Details</h2>
            <div class="text-xs text-slate-600 leading-relaxed space-y-4 uppercase font-bold">
                <p>Network: National Home Improvement Alliance</p>
                <p>Coverage: 50 States Continental USA</p>
                <p>Headquarters: Corporate Enterprise Division</p>
                <p>Certification: Class-A Nationwide Network</p>
            </div>
            <button onclick="toggleModal('detailsModal')" class="mt-10 btn-elite">Close</button>
        </div>
    </div>

    <script>
        const firebaseConfig = {
            apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA",
            authDomain: "ushomes07.firebaseapp.com",
            databaseURL: "https://ushomes07-default-rtdb.firebaseio.com",
            projectId: "ushomes07",
            storageBucket: "ushomes07.firebasestorage.app",
            messagingSenderId: "24299478735",
            appId: "1:24299478735:web:5ec1ac023ef15e186521ba"
        };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();

        function goNext(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function toggleModal(id) {
            const m = document.getElementById(id);
            m.style.display = m.style.display === 'flex' ? 'none' : 'flex';
        }

        document.getElementById('masterLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                service: document.getElementById('service').value,
                zip: document.getElementById('cZip').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                alert("APPLICATION SUBMITTED SUCCESSFULLY!");
                location.reload();
            });
        });
    </script>
</body>
</html>
