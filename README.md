<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Official Site</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --slate: #0f172a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: var(--slate); scroll-behavior: smooth; }
        
        /* Direct Path Links - Make sure images are in the same folder as index.html */
        .hero-bg {
            background: linear-gradient(rgba(15, 23, 42, 0.90), rgba(15, 23, 42, 0.85)),
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
            width: 100%; padding: 1.2rem; border-radius: 1rem; border: 2px solid #f1f5f9;
            font-weight: 600; outline: none; transition: 0.3s;
        }
        .input-matrix:focus { border-color: var(--neon); }

        .btn-elite {
            background: var(--slate); color: white; padding: 1.2rem; border-radius: 1rem;
            font-weight: 800; width: 100%; cursor: pointer; transition: 0.4s;
        }
        .btn-elite:hover { background: var(--neon); color: var(--slate); transform: translateY(-2px); }
        
        .feature-card {
            background: white; border-radius: 1.5rem; border: 1px solid #f1f5f9; transition: 0.4s; overflow: hidden;
        }
        .feature-card img { width: 100%; height: 200px; object-fit: cover; }
    </style>
</head>
<body>

    <header class="hero-bg h-[60vh] flex flex-col items-center justify-center text-center px-6 text-white relative">
        <div class="absolute top-8 left-8 flex items-center gap-3">
            <img src="./WA_1776550450872.jpeg" alt="Company Logo" class="h-10">
            <span class="text-[10px] font-black tracking-widest uppercase border-l border-cyan-400 pl-4">U.S. Improvement Co.</span>
        </div>
        <h1 class="text-5xl md:text-7xl font-black italic uppercase leading-none">THE NATIONAL<br>STANDARD</h1>
        <p class="text-cyan-400 font-bold tracking-widest text-xs mt-6 uppercase">Quality Home Improvements Across America</p>
    </header>

    <section id="portal" class="max-w-2xl mx-auto -mt-20 px-4 mb-24 relative z-20">
        <div class="glass-panel p-8 md:p-12 shadow-2xl">
            <form id="masterLeadForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black italic mb-6 uppercase">Select Service</h2>
                    <div class="space-y-4">
                        <select id="service" class="input-matrix" required onchange="handleServiceSelection()">
                            <option value="">What do you need?</option>
                            <option value="Windows">Windows</option>
                            <option value="Doors">Doors</option>
                            <option value="Roofing">Roofing</option>
                            <option value="Solar">Solar</option>
                            <option value="Kitchen">Kitchen</option>
                            <option value="Bathroom">Bathroom</option>
                            <option value="Deck">Deck</option>
                            <option value="Garage">Garage</option>
                        </select>
                        <button type="button" onclick="goNext('step2')" class="btn-elite">Continue</button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black italic mb-6 uppercase">Contact Details</h2>
                    <div class="space-y-4">
                        <input type="text" id="cName" placeholder="Full Name" class="input-matrix" required>
                        <input type="tel" id="cPhone" placeholder="Phone" class="input-matrix" required>
                        <button type="submit" class="btn-elite bg-cyan-500 text-slate-900">Get My Quote</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-6xl mx-auto px-6 mb-20">
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
            <div class="feature-card"><img src="./WA_1776549555727.jpeg" alt="Windows"> <div class="p-4 font-bold text-center">WINDOWS</div></div>
            <div class="feature-card"><img src="./WA_1776549622236.jpeg" alt="Doors"> <div class="p-4 font-bold text-center">DOORS</div></div>
            <div class="feature-card"><img src="./WA_1776549716792.jpeg" alt="Roofing"> <div class="p-4 font-bold text-center">ROOFING</div></div>
            <div class="feature-card"><img src="./WA_1776549781247.jpeg" alt="Solar"> <div class="p-4 font-bold text-center">SOLAR</div></div>
        </div>
    </section>

    <footer class="bg-slate-900 py-10 text-white/50 text-center">
        <img src="./WA_1776550450872.jpeg" alt="Logo" class="h-8 mx-auto mb-4 grayscale brightness-200">
        <p class="text-[9px] font-black uppercase tracking-widest">U.S. HOME IMPROVEMENTS • 2026</p>
    </footer>

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

        function goNext(nextId) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(nextId).classList.add('active');
        }

        document.getElementById('masterLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            db.ref('leads').push({
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                service: document.getElementById('service').value,
                company: "US Home Improvement",
                timestamp: new Date().toLocaleString()
            }).then(() => {
                alert("Quote Requested Successfully!");
                location.reload();
            });
        });
    </script>
</body>
</html>
