<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Elite Contractor Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --dark: #05070a; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; margin: 0; padding: 0; }
        
        /* Fixed Glass Card for Mobile */
        .glass-box { 
            background: rgba(255, 255, 255, 0.03); 
            backdrop-filter: blur(15px); 
            border: 1px solid rgba(255, 255, 255, 0.1); 
            border-radius: 1.5rem; 
            overflow: hidden;
            margin-bottom: 1.5rem;
        }

        .step { display: none; }
        .step.active { display: block; animation: fadeIn 0.4s ease-in; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .btn-choice { 
            width: 100%; padding: 1rem; background: rgba(255,255,255,0.05); 
            border-radius: 1rem; border: 1px solid rgba(255,255,255,0.1); 
            text-align: left; font-weight: 600; margin-bottom: 0.75rem;
        }
        .btn-choice:hover { border-color: var(--neon); background: rgba(0, 242, 255, 0.05); }

        /* Ensuring Images Always Show or Have Backup */
        .img-container { width: 100%; height: 200px; background: #111; position: relative; }
        .img-container img { width: 100%; height: 100%; object-fit: cover; }
    </style>
</head>
<body class="p-4">

    <nav class="max-w-xl mx-auto mb-8 mt-4 text-center">
        <h1 class="text-2xl font-black italic tracking-tighter leading-none">U.S. HOME IMPROVEMENTS</h1>
        <p class="text-[8px] text-cyan-400 font-bold uppercase tracking-[0.3em] mt-1">Certified Professional Network</p>
    </nav>

    <main class="max-w-xl mx-auto">
        <div class="glass-box p-6 border-t-2 border-cyan-500 shadow-2xl">
            <form id="masterForm">
                <div class="step active" id="step1">
                    <h2 class="text-xl font-black mb-4 uppercase italic">01. Select Service</h2>
                    <button type="button" onclick="handleService('Windows')" class="btn-choice">🪟 Windows & Doors</button>
                    <button type="button" onclick="next(3, 'service', 'Roofing')" class="btn-choice">🏠 Premium Roofing</button>
                    <button type="button" onclick="next(3, 'service', 'Solar')" class="btn-choice">☀️ Solar Power System</button>
                </div>

                <div class="step" id="step-windows">
                    <h2 class="text-xl font-black mb-4 uppercase italic">02. Window Units</h2>
                    <div class="grid grid-cols-2 gap-2">
                        <button type="button" onclick="next(3, 'units', '1-10')" class="btn-choice text-center">1-10</button>
                        <button type="button" onclick="next(3, 'units', '10+')" class="btn-choice text-center">10+</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-xl font-black mb-4 uppercase italic">03. Contact Info</h2>
                    <input type="text" id="name" placeholder="Full Name" class="w-full p-4 mb-3 bg-white/5 border border-white/10 rounded-xl" required>
                    <input type="tel" id="phone" placeholder="Phone Number" class="w-full p-4 mb-3 bg-white/5 border border-white/10 rounded-xl" required>
                    <input type="number" id="zip" placeholder="Zip Code" class="w-full p-4 mb-3 bg-white/5 border border-white/10 rounded-xl" required>
                    <button type="submit" class="w-full bg-cyan-600 p-4 rounded-xl font-black uppercase">Submit Application</button>
                </div>
            </form>
        </div>
    </main>

    <section class="max-w-xl mx-auto mt-10 space-y-6">
        <div class="glass-box">
            <div class="img-container">
                <img src="https://images.unsplash.com/photo-1513694490325-24b3dc52a21c?auto=format&fit=crop&w=600&q=80" alt="Solar">
            </div>
            <div class="p-6">
                <h3 class="text-lg font-black italic uppercase">Solar Systems</h3>
                <p class="text-xs text-gray-500 font-semibold uppercase mt-2">Government backed solar programs for qualifying homeowners.</p>
            </div>
        </div>

        <div class="glass-box">
            <div class="img-container">
                <img src="https://images.unsplash.com/photo-1632759162353-19c9a543fe79?auto=format&fit=crop&w=600&q=80" alt="Roofing">
            </div>
            <div class="p-6">
                <h3 class="text-lg font-black italic uppercase">Architectural Roofing</h3>
                <p class="text-xs text-gray-500 font-semibold uppercase mt-2">Lifetime-warranted asphalt and metal systems for protection.</p>
            </div>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 bg-black/95 z-[1000] p-6 hidden overflow-y-auto">
        <div class="max-w-md mx-auto">
            <h2 class="text-2xl font-black text-cyan-400 mb-8 italic">LEAD ACCESS</h2>
            <input type="password" id="adminKey" class="w-full p-4 bg-white/5 border border-white/10 rounded-xl mb-4 text-center" placeholder="ENTER KEY">
            <button onclick="unlock()" class="w-full bg-cyan-600 p-4 rounded-xl font-bold">AUTHORIZE</button>
            <div id="dashboard" class="mt-10 space-y-4 hidden"></div>
        </div>
    </nav>

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

        let lead = { units: 'N/A' };

        function handleService(v) {
            lead.service = v;
            if(v === 'Windows') show('step-windows'); else show('step3');
        }

        function show(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function next(s, k, v) {
            if(k) lead[k] = v;
            show('step' + s);
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            lead.name = document.getElementById('name').value;
            lead.phone = document.getElementById('phone').value;
            lead.zip = document.getElementById('zip').value;
            lead.time = new Date().toLocaleString();
            db.ref('leads').push(lead).then(() => { alert("Success!"); location.reload(); });
        });

        // Secret Admin (5 rapid taps)
        let t = 0, l = 0;
        document.addEventListener('click', () => {
            if(Date.now() - l < 400) t++; else t = 1; l = Date.now();
            if(t === 5) document.getElementById('adminPortal').classList.remove('hidden');
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('dashboard').classList.remove('hidden');
                sync();
            }
        }

        function sync() {
            db.ref('leads').on('value', (snap) => {
                const data = snap.val();
                let h = '';
                for(let id in data) {
                    h = `<div class="p-4 bg-white/5 border-l-4 border-cyan-500 rounded-r-xl">
                            <p class="font-bold">${data[id].name}</p>
                            <p class="text-xs text-gray-400">${data[id].phone} | ${data[id].service}</p>
                         </div>` + h;
                }
                document.getElementById('dashboard').innerHTML = h;
            });
        }
    </script>
</body>
</html>
