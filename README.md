<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | Secure National Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; }
        .admin-btn { display: none; } /* Hidden by default for security */
        .glass-panel { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(20px); border: 1px solid #f1f5f9; }
        .input-elite { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 20px; outline: none; transition: 0.3s; }
        .input-elite:focus { border-color: var(--accent); }
        .btn-glow { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; transition: 0.4s; box-shadow: 0 10px 20px rgba(37, 99, 235, 0.2); }
        .btn-glow:hover { transform: translateY(-3px); box-shadow: 0 15px 30px rgba(37, 99, 235, 0.3); }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-[5000] glass-panel px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <img src="logo.png" onclick="handleAdminTap()" class="h-12 w-12 cursor-pointer rounded-xl shadow-sm" onerror="this.src='https://ui-avatars.com/api/?name=US&background=0f172a&color=fff'">
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic">Authorized National Dispatch</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-3 rounded-full text-[10px] font-black uppercase">Get Quote</button>
    </nav>

    <section id="home" class="py-32 px-6 text-center">
        <h2 class="text-5xl md:text-8xl font-black uppercase italic tracking-tighter mb-8">Premium <br><span class="text-blue-600">Remodeling.</span></h2>
        <p class="text-[10px] font-black uppercase text-slate-400 tracking-[0.4em] mb-12">Authorized Site Surveys in All 50 States</p>
        <button onclick="showPage('form')" class="btn-glow px-12 py-5 rounded-2xl font-black uppercase text-xs">Start Project Survey</button>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden p-10 overflow-y-auto">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center mb-10 border-b pb-6">
                <h3 class="text-2xl font-black uppercase italic">National Master <span class="text-blue-600">Terminal</span></h3>
                <div class="flex gap-4">
                    <button id="exportBtn" onclick="exportData()" class="admin-btn bg-emerald-50 text-emerald-600 px-6 py-3 rounded-full text-[10px] font-black uppercase border border-emerald-100">Export All Leads</button>
                    <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-6 py-3 rounded-full text-[10px] font-black uppercase">Exit Hub</button>
                </div>
            </div>

            <div id="pinArea" class="text-center py-20">
                <input type="password" id="adminPin" class="input-elite max-w-[300px] text-center text-4xl mb-6" placeholder="••••">
                <br>
                <button onclick="verifyPin()" class="btn-glow px-10 py-4 rounded-xl font-black uppercase text-xs">Authorize Access</button>
            </div>

            <div id="secureContent" class="hidden">
                <div class="grid md:grid-cols-2 gap-10">
                    <div><h4 class="font-black uppercase text-xs text-slate-400 mb-6 italic">Dispatch Leads</h4><div id="leadsList" class="space-y-4"></div></div>
                    <div><h4 class="font-black uppercase text-xs text-slate-400 mb-6 italic">Secure Signals</h4><div id="chatsList" class="space-y-4"></div></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // FIREBASE CONFIG (Aapki wahi purani)
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

        let taps = 0;
        function handleAdminTap() {
            taps++;
            if(taps >= 5) {
                document.getElementById('adminHub').classList.remove('hidden');
                taps = 0;
            }
            setTimeout(() => taps = 0, 2000);
        }

        function verifyPin() {
            const pin = document.getElementById('adminPin').value;
            if(pin === "786") {
                document.getElementById('pinArea').classList.add('hidden');
                document.getElementById('secureContent').classList.remove('hidden');
                document.getElementById('exportBtn').style.display = 'block'; // Export button ab show hoga
                loadMasterData();
            } else {
                alert("Unauthorized Access!");
            }
        }

        function loadMasterData() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) h += `<div class="p-6 bg-slate-50 rounded-2xl border">
                    <p class="text-[10px] font-black text-blue-600 uppercase">${data[k].tid}</p>
                    <h5 class="font-black text-slate-900">${data[k].name}</h5>
                    <p class="text-[9px] font-bold text-slate-500 uppercase">${data[k].phone} | ${data[k].svc}</p>
                </div>`;
                document.getElementById('leadsList').innerHTML = h || 'No Leads.';
            });
        }

        function exportData() {
            db.ref('leads').once('value', snap => {
                const ws = XLSX.utils.json_to_sheet(Object.values(snap.val() || {}));
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "Leads");
                XLSX.writeFile(wb, "US_Home_Improvements_Data.xlsx");
            });
        }

        function closeAdmin() { 
            document.getElementById('adminHub').classList.add('hidden'); 
            document.getElementById('pinArea').classList.remove('hidden');
            document.getElementById('secureContent').classList.add('hidden');
            document.getElementById('exportBtn').style.display = 'none';
        }
    </script>
</body>
</html>
