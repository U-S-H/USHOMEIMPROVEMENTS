<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Professional Neon Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { 
            --neon: #00f2ff; 
            --bg-light: #f0f4f8; /* Soft Steel Light Background */
            --accent: #1e293b; 
        }
        
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background: linear-gradient(135deg, #e0e7ff 0%, #f1f5f9 100%); 
            color: #1e293b; 
            margin: 0; 
        }

        /* Glass Cards with Neon Border */
        .neon-card { 
            background: rgba(255, 255, 255, 0.7); 
            backdrop-filter: blur(10px); 
            border: 2px solid white; 
            border-radius: 2rem; 
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.05), inset 0 0 15px rgba(0, 242, 255, 0.1);
            transition: 0.3s;
        }
        .neon-card:hover { 
            border-color: var(--neon); 
            transform: translateY(-5px); 
            box-shadow: 0 20px 40px rgba(0, 242, 255, 0.2);
        }

        /* Neon Buttons */
        .btn-neon {
            background: #1e293b;
            color: white;
            padding: 1rem 2rem;
            border-radius: 1rem;
            font-weight: 800;
            text-transform: uppercase;
            box-shadow: 0 10px 20px rgba(0, 242, 255, 0.2);
            transition: 0.3s;
        }
        .btn-neon:hover {
            background: var(--neon);
            color: #1e293b;
        }

        .step { display: none; }
        .step.active { display: block; animation: slideIn 0.5s ease; }
        @keyframes slideIn { from { opacity: 0; transform: scale(0.95); } to { opacity: 1; transform: scale(1); } }

        /* Image Handling */
        .img-wrap { width: 100%; height: 220px; overflow: hidden; border-radius: 1.5rem; background: #ddd; }
        .img-wrap img { width: 100%; height: 100%; object-fit: cover; }
    </style>
</head>
<body class="p-4 md:p-8">

    <nav class="max-w-4xl mx-auto mb-10 text-center">
        <div class="inline-block px-6 py-2 bg-white/50 backdrop-blur rounded-full border border-white mb-4">
            <span class="text-[10px] font-black text-blue-600 uppercase tracking-widest">Official National Network</span>
        </div>
        <h1 class="text-4xl font-black italic tracking-tighter text-slate-900">U.S. HOME IMPROVEMENTS</h1>
    </nav>

    <section id="portal" class="max-w-xl mx-auto mb-20">
        <div class="neon-card p-8 md:p-12 relative overflow-hidden">
            <form id="masterForm">
                <div class="step active" id="step1">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">Select Upgrade</h2>
                    <div class="space-y-4">
                        <button type="button" onclick="handleService('Windows')" class="w-full p-6 bg-white border-2 border-slate-100 rounded-2xl text-left font-bold flex justify-between hover:border-cyan-400 group">
                            Windows & Doors <span class="group-hover:translate-x-2 transition">→</span>
                        </button>
                        <button type="button" onclick="next(2, 'service', 'Roofing')" class="w-full p-6 bg-white border-2 border-slate-100 rounded-2xl text-left font-bold flex justify-between hover:border-cyan-400 group">
                            Elite Roofing <span class="group-hover:translate-x-2 transition">→</span>
                        </button>
                        <button type="button" onclick="next(2, 'service', 'Solar')" class="w-full p-6 bg-white border-2 border-slate-100 rounded-2xl text-left font-bold flex justify-between hover:border-cyan-400 group">
                            Solar Energy <span class="group-hover:translate-x-2 transition">→</span>
                        </button>
                    </div>
                </div>

                <div class="step" id="step2">
                    <h2 class="text-2xl font-black mb-8 italic uppercase">Schedule Visit</h2>
                    <input type="date" id="appDate" class="w-full p-4 mb-4 border-2 border-slate-100 rounded-xl outline-none" required>
                    <select id="appTime" class="w-full p-4 mb-6 border-2 border-slate-100 rounded-xl outline-none font-bold">
                        <option>Morning (8AM - 12PM)</option>
                        <option>Afternoon (12PM - 4PM)</option>
                        <option>Evening (4PM - 7PM)</option>
                    </select>
                    <button type="button" onclick="showStep('step3')" class="btn-neon w-full">Set Appointment</button>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-2xl font-black mb-8 italic uppercase text-cyan-500">Your Details</h2>
                    <div class="space-y-3">
                        <input type="text" id="name" placeholder="Full Name" class="w-full p-4 border-2 border-slate-100 rounded-xl" required>
                        <input type="tel" id="phone" placeholder="Phone Number" class="w-full p-4 border-2 border-slate-100 rounded-xl" required>
                        <input type="text" id="address" placeholder="Address" class="w-full p-4 border-2 border-slate-100 rounded-xl" required>
                        <button type="submit" class="btn-neon w-full mt-4">Confirm & Submit</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section class="max-w-4xl mx-auto grid md:grid-cols-3 gap-6 mb-20">
        <div class="neon-card p-4">
            <div class="img-wrap">
                <img src="https://images.unsplash.com/photo-1512917774080-9991f1c4c750?w=600" alt="Windows">
            </div>
            <h3 class="font-black italic mt-4 uppercase">Windows</h3>
            <p class="text-[10px] font-bold text-slate-500 uppercase mt-2">Certified impact & energy saving glass.</p>
        </div>
        <div class="neon-card p-4">
            <div class="img-wrap">
                <img src="https://images.unsplash.com/photo-1625938140722-234d9671897d?w=600" alt="Solar">
            </div>
            <h3 class="font-black italic mt-4 uppercase">Solar Matrix</h3>
            <p class="text-[10px] font-bold text-slate-500 uppercase mt-2">Zero-down solar installation programs.</p>
        </div>
        <div class="neon-card p-4">
            <div class="img-wrap">
                <img src="https://images.unsplash.com/photo-1632759162353-19c9a543fe79?w=600" alt="Roofing">
            </div>
            <h3 class="font-black italic mt-4 uppercase">Elite Roofing</h3>
            <p class="text-[10px] font-bold text-slate-500 uppercase mt-2">Lifetime warranted architectural shingles.</p>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 bg-slate-900/95 backdrop-blur-xl z-[1000] p-6 hidden overflow-y-auto text-white">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-between items-center mb-10 border-b border-white/10 pb-4">
                <h2 class="text-3xl font-black italic text-cyan-400">HQ DATA COMMAND</h2>
                <button onclick="location.reload()" class="bg-red-500 px-4 py-1 rounded text-[10px] font-bold">CLOSE</button>
            </div>
            <div id="loginBox" class="max-w-xs mx-auto py-20 text-center">
                <input type="password" id="adminKey" class="w-full p-4 bg-white/10 rounded-xl mb-4 text-center text-2xl" placeholder="KEY">
                <button onclick="unlock()" class="btn-neon w-full">AUTHORIZE</button>
            </div>
            <div id="dashboard" class="hidden grid gap-4"></div>
        </div>
    </div>

    <footer class="text-center py-10 opacity-50">
        <p class="text-[9px] font-black uppercase tracking-[0.4em]">© 2026 U.S. Home Improvements Enterprise</p>
    </footer>

    <script>
        // Firebase Config
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

        let lead = {};

        function showStep(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function next(s, k, v) {
            if(k) lead[k] = v;
            showStep('step' + s);
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            lead.name = document.getElementById('name').value;
            lead.phone = document.getElementById('phone').value;
            lead.address = document.getElementById('address').value;
            lead.date = document.getElementById('appDate').value;
            lead.time = document.getElementById('appTime').value;
            lead.timestamp = new Date().toLocaleString();

            db.ref('leads').push(lead).then(() => {
                alert("APPLICATION SECURED! 📅");
                location.reload();
            });
        });

        // Admin Secret (5 taps)
        let t = 0, l = 0;
        document.addEventListener('click', () => {
            if(Date.now() - l < 400) t++; else t = 1; l = Date.now();
            if(t === 5) document.getElementById('adminPortal').classList.remove('hidden');
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('dashboard').classList.remove('hidden');
                sync();
            }
        }

        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val();
                let html = '';
                for(let id in data) {
                    html = `
                    <div class="bg-white/5 border-l-4 border-cyan-400 p-6 rounded-r-2xl mb-4">
                        <div class="flex justify-between">
                            <h4 class="font-black italic">${data[id].name}</h4>
                            <span class="text-cyan-400 text-[10px] font-bold">${data[id].service}</span>
                        </div>
                        <p class="text-xs text-gray-400 mt-1">📞 ${data[id].phone} | 📅 ${data[id].date}</p>
                    </div>` + html;
                }
                document.getElementById('dashboard').innerHTML = html || 'No leads yet.';
            });
        }
    </script>
</body>
</html>
