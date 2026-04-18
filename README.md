<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Premium Neon Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { 
            --neon-cyan: #00f2ff; 
            --neon-pink: #ff00e6; 
            --neon-purple: #9d00ff;
            --slate: #0f172a;
        }
        
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background: #ffffff; 
            color: var(--slate); 
            scroll-behavior: smooth; 
            overflow-x: hidden;
        }

        /* Animated Neon Gradient Header */
        .neon-slide-header {
            background: linear-gradient(-45deg, #00f2ff, #ff00e6, #9d00ff, #00f2ff);
            background-size: 400% 400%;
            animation: gradientSlide 10s ease infinite;
            position: relative;
            overflow: hidden;
        }
        @keyframes gradientSlide {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .hero-overlay {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(5px);
        }

        /* Glassmorphism Cards */
        .glass-panel {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 3rem;
            border: 2px solid var(--neon-cyan);
            box-shadow: 0 20px 50px rgba(0, 242, 255, 0.2);
        }

        .step { display: none; }
        .step.active { display: block; animation: neonPop 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        @keyframes neonPop { from { opacity: 0; scale: 0.9; } to { opacity: 1; scale: 1; } }

        /* Neon Inputs */
        .input-neon {
            width: 100%; padding: 1.3rem; border-radius: 1.5rem; border: 2px solid #f1f5f9;
            font-weight: 700; outline: none; transition: 0.4s;
        }
        .input-neon:focus { border-color: var(--neon-pink); box-shadow: 0 0 20px rgba(255, 0, 230, 0.15); }

        /* Premium Buttons */
        .btn-neon {
            background: var(--slate); color: white; padding: 1.3rem; border-radius: 1.5rem;
            font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; transition: 0.4s;
            position: relative; overflow: hidden; border: none;
        }
        .btn-neon:hover {
            background: var(--neon-cyan); color: var(--slate);
            box-shadow: 0 0 30px var(--neon-cyan); transform: translateY(-3px);
        }

        /* Service Cards */
        .service-card {
            background: white; border-radius: 2.5rem; border: 2px solid #f1f5f9;
            transition: 0.5s; overflow: hidden; cursor: pointer;
        }
        .service-card:hover { 
            border-color: var(--neon-purple); 
            transform: translateY(-15px) rotate(2deg);
            box-shadow: 0 25px 50px rgba(157, 0, 255, 0.15);
        }
        .service-card img { width: 100%; height: 220px; object-fit: cover; }

        /* Modal */
        .modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.8); z-index: 9999; align-items: center; justify-content: center; padding: 20px; }
        .modal-inner { background: white; border-radius: 2rem; padding: 40px; max-width: 600px; width: 100%; max-height: 80vh; overflow-y: auto; }
    </style>
</head>
<body>

    <header class="neon-slide-header h-[70vh] flex flex-col items-center justify-center text-center px-6 relative">
        <div class="hero-overlay absolute inset-0"></div>
        
        <div class="relative z-10 mb-10">
            <img src="./WA_1776550450872.jpeg" alt="Logo" class="h-20 rounded-full border-4 border-white shadow-2xl">
        </div>

        <h1 class="relative z-10 text-6xl md:text-9xl font-black italic text-white tracking-tighter uppercase leading-none drop-shadow-2xl">
            U.S. HOME<br><span class="text-slate-900">UPGRADES</span>
        </h1>
        <p class="relative z-10 text-white font-black tracking-[0.8em] text-xs mt-8 uppercase opacity-90">Nationwide Certified Matrix 2026</p>
    </header>

    <section id="portal" class="max-w-3xl mx-auto -mt-32 px-4 mb-32 relative z-20">
        <div class="glass-panel p-10 md:p-16">
            <form id="leadForm">
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black italic mb-8 uppercase text-slate-800">01. Service Path</h2>
                    <div class="space-y-6">
                        <select id="service" class="input-neon" required>
                            <option value="">Choose Upgrade Path</option>
                            <option value="Windows">Windows Matrix</option>
                            <option value="Doors">Security Doors</option>
                            <option value="Roofing">Roofing Systems</option>
                            <option value="Solar">Solar Matrix</option>
                            <option value="Kitchen">Kitchen Hub</option>
                            <option value="Bathroom">Bath Hub</option>
                            <option value="Deck">Outdoor Deck</option>
                            <option value="Garage">Garage Matrix</option>
                        </select>
                        <select id="owner" class="input-neon" required>
                            <option value="">Ownership Status?</option>
                            <option value="Owner">I am the Homeowner</option>
                            <option value="Renter">I am a Tenant</option>
                        </select>
                        <button type="button" onclick="goNext('step2')" class="btn-neon">Continue Next</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-3xl font-black italic mb-8 uppercase text-slate-800">02. Qualification</h2>
                    <div class="space-y-6">
                        <select id="credit" class="input-neon" required>
                            <option value="">Credit Score Range</option>
                            <option value="Excellent">720+ (Elite)</option>
                            <option value="Good">660-719 (Standard)</option>
                            <option value="Fair">Below 660 (Basic)</option>
                        </select>
                        <input type="text" id="cZip" placeholder="Enter Zip Code" class="input-neon" required>
                        <button type="button" onclick="goNext('step3')" class="btn-neon">Final Protocol</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black italic mb-8 uppercase text-slate-800">03. Deployment</h2>
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Legal Name" class="input-neon" required>
                        <input type="tel" id="cPhone" placeholder="Mobile Protocol" class="input-neon" required>
                        <input type="email" id="cEmail" placeholder="Email Address" class="input-neon" required>
                        <button type="submit" class="btn-neon bg-cyan-400 !text-slate-900">Confirm & Get Quote</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-7xl mx-auto px-6 mb-32">
        <div class="text-center mb-16">
            <h3 class="text-5xl font-black italic uppercase text-slate-900">The Service Matrix</h3>
            <div class="h-2 w-40 bg-gradient-to-r from-cyan-400 to-pink-500 mx-auto mt-4 rounded-full"></div>
        </div>
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-10">
            <div class="service-card"><img src="./WA_1776549555727.jpeg"><div class="p-6 font-black uppercase italic">Windows</div></div>
            <div class="service-card"><img src="./WA_1776549622236.jpeg"><div class="p-6 font-black uppercase italic">Doors</div></div>
            <div class="service-card"><img src="./WA_1776549716792.jpeg"><div class="p-6 font-black uppercase italic">Roofing</div></div>
            <div class="service-card"><img src="./WA_1776549781247.jpeg"><div class="p-6 font-black uppercase italic">Solar</div></div>
            <div class="service-card"><img src="./WA_1776549862258.jpeg"><div class="p-6 font-black uppercase italic">Kitchen</div></div>
            <div class="service-card"><img src="./WA_1776549917709.jpeg"><div class="p-6 font-black uppercase italic">Bathroom</div></div>
            <div class="service-card"><img src="./WA_1776549990293.jpeg"><div class="p-6 font-black uppercase italic">Decks</div></div>
            <div class="service-card"><img src="./WA_1776550066723.jpeg"><div class="p-6 font-black uppercase italic">Garage</div></div>
        </div>
    </section>

    <footer class="bg-slate-950 py-20 text-white">
        <div class="max-w-6xl mx-auto px-6 text-center">
            <img src="./WA_1776550450872.jpeg" class="h-12 mx-auto mb-8 rounded-full border-2 border-cyan-400 shadow-[0_0_20px_rgba(0,242,255,0.5)]">
            <div class="flex flex-wrap justify-center gap-10 mb-16 text-[10px] font-black uppercase tracking-widest text-white/60">
                <button onclick="openModal('privacy')" class="hover:text-cyan-400">Privacy Policy</button>
                <button onclick="openModal('terms')" class="hover:text-cyan-400">Terms of Service</button>
                <button onclick="openModal('about')" class="hover:text-cyan-400">Company Benefits</button>
            </div>
            <p class="text-[9px] font-bold tracking-[0.5em] text-white/20 uppercase">U.S. Home Improvements • National Enterprise • 2026</p>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[99999] p-6 hidden overflow-y-auto">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center mb-10">
                <h2 class="text-4xl font-black italic uppercase">HQ Admin Matrix</h2>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-6 py-2 rounded-full font-bold">Exit HQ</button>
            </div>
            <div id="authArea" class="text-center py-20">
                <input type="password" id="pin" class="input-neon max-w-xs text-center text-4xl mb-4" placeholder="PIN">
                <button onclick="checkPin()" class="btn-neon max-w-xs mx-auto">Access Matrix</button>
            </div>
            <div id="dataArea" class="hidden grid gap-4"></div>
        </div>
    </div>

    <div id="modal" class="modal" onclick="closeModal()">
        <div class="modal-inner" onclick="event.stopPropagation()">
            <div id="modalContent"></div>
            <button onclick="closeModal()" class="btn-neon mt-10">Close Matrix</button>
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

        document.getElementById('leadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                service: document.getElementById('service').value,
                zip: document.getElementById('cZip').value,
                credit: document.getElementById('credit').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                alert("SUCCESS! Matrix Authorized.");
                location.reload();
            });
        });

        // Modals
        const contents = {
            privacy: '<h3 class="text-3xl font-black mb-6">PRIVACY POLICY</h3><p class="font-bold uppercase text-xs leading-loose">We encrypt all project data. We do not sell info to 3rd party bots. Your data is used for qualification only.</p>',
            terms: '<h3 class="text-3xl font-black mb-6">TERMS</h3><p class="font-bold uppercase text-xs leading-loose">U.S. Home Improvements connects you with certified contractors. We are not responsible for direct labor disputes. All quotes are estimates.</p>',
            about: '<h3 class="text-3xl font-black mb-6">BENEFITS</h3><p class="font-bold uppercase text-xs leading-loose">1. Lifetime Warranty.<br>2. Energy Certified.<br>3. National Network.<br>4. Zero-Down Financing available.</p>'
        };
        function openModal(id) { document.getElementById('modalContent').innerHTML = contents[id]; document.getElementById('modal').style.display = 'flex'; }
        function closeModal() { document.getElementById('modal').style.display = 'none'; }

        // Admin
        let clicks = 0;
        document.querySelector('footer').addEventListener('click', () => {
            clicks++;
            if(clicks === 10) document.getElementById('adminPanel').classList.remove('hidden');
        });
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); clicks=0; }
        function checkPin() {
            if(document.getElementById('pin').value === "786") {
                document.getElementById('authArea').classList.add('hidden');
                document.getElementById('dataArea').classList.remove('hidden');
                loadData();
            }
        }
        function loadData() {
            db.ref('leads').on('value', snap => {
                const data = snap.val();
                let html = '';
                for(let k in data) {
                    html += `<div class="p-6 border-2 border-slate-100 rounded-3xl flex justify-between items-center">
                        <div>
                            <p class="font-black text-cyan-500 uppercase text-xs">${data[k].service}</p>
                            <h4 class="text-2xl font-black">${data[k].name}</h4>
                            <p class="font-bold text-slate-400 uppercase text-[10px] tracking-widest">${data[k].phone} | ZIP: ${data[k].zip} | ${data[k].timestamp}</p>
                        </div>
                        <button onclick="deleteLead('${k}')" class="bg-red-500 text-white px-6 py-2 rounded-full font-bold uppercase text-[10px]">Delete</button>
                    </div>`;
                }
                document.getElementById('dataArea').innerHTML = html || '<p class="text-center font-bold uppercase py-20">No Leads Found</p>';
            });
        }
        function deleteLead(id) { if(confirm('Delete Lead?')) db.ref('leads/'+id).remove(); }
    </script>
</body>
</html>
