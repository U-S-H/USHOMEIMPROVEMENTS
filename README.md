<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Matrix</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --main: #1e3a8a; --light: #f8fafc; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; margin: 0; padding: 0; }
        
        .sticky-nav { background: white; border-bottom: 1px solid #f1f5f9; position: sticky; top: 0; z-index: 1000; padding: 15px 20px; }
        
        /* Compact corporate header */
        .hero-banner { background: var(--main); padding: 40px 20px; text-align: center; color: white; position: relative; }
        .hero-banner::after { content: ''; position: absolute; bottom: 0; left: 0; width: 100%; height: 6px; background: #2563eb; }

        .form-panel { background: white; border-radius: 16px; border: 1px solid #e2e8f0; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.05); padding: 25px; margin: -25px 15px 30px; }
        .input-pro { width: 100%; padding: 12px; border: 1px solid #cbd5e1; border-radius: 8px; margin-bottom: 12px; font-weight: 600; outline-color: #2563eb; font-size: 15px; }
        .btn-matrix { background: var(--main); color: white; padding: 15px; border-radius: 8px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; width: 100%; border: none; cursor: pointer; transition: 0.2s; }
        .btn-matrix:hover { background: #1e40af; }

        /* Trusted 11-Image Service Matrix */
        .service-matrix { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; padding: 0 15px 40px; }
        .matrix-item { background: white; border: 1px solid #f1f5f9; border-radius: 12px; overflow: hidden; text-align: center; padding-bottom: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.02); }
        .matrix-item:hover { border-color: #2563eb; }
        .matrix-item img { width: 100%; height: 120px; object-fit: cover; background: #f1f5f9; }
        .matrix-item h4 { font-size: 10px; font-weight: 800; color: #1e3a8a; margin-top: 8px; text-transform: uppercase; }
    </style>
</head>
<body>

    <nav class="sticky-nav flex justify-between items-center">
        <div class="flex items-center gap-2">
            <img src="./WA_1776550450872.jpeg" class="h-8 w-8 rounded-full border shadow-sm">
            <span onclick="handleAdminTap()" class="font-black text-xs uppercase cursor-pointer select-none">U.S. Home Improvement</span>
        </div>
        <div class="text-[9px] font-bold text-blue-700 bg-blue-50 px-2 py-1 rounded">EST. 2026</div>
    </nav>

    <header class="hero-banner">
        <h1 class="text-2xl font-black uppercase italic tracking-tighter">Enterprise Solutions</h1>
        <p class="text-[8px] font-bold uppercase tracking-[0.5em] text-blue-200">Certified National Matrix</p>
    </header>

    <main class="max-w-md mx-auto">
        <div class="form-panel">
            <form id="finalInventoryForm">
                <select id="service" class="input-pro" required>
                    <option value="Windows">Replacement Windows</option>
                    <option value="Roofing">Architectural Roofing</option>
                    <option value="Doors">Exterior Doors</option>
                    <option value="Solar">Solar Energy Hub</option>
                    <option value="Kitchen">Kitchen Luxury Remodel</option>
                </select>
                <input type="text" id="cName" placeholder="Full Legal Name" class="input-pro" required>
                <input type="tel" id="cPhone" placeholder="Direct Contact Number" class="input-pro" required>
                <button type="submit" class="btn-matrix">Authorize Project</button>
            </form>
        </div>

        <h3 class="text-center font-bold uppercase text-[11px] mb-8 tracking-widest text-slate-400">Authorized Services Matrix</h3>
        <div class="service-matrix">
            <div class="matrix-item"><img src="./WA_1776549402525.jpeg"><h4>Exterior Solutions</h4></div>
            <div class="matrix-item"><img src="./WA_1776549555727.jpeg"><h4>Energy Windows</h4></div>
            <div class="matrix-item"><img src="./WA_1776549622236.jpeg"><h4>Entry Doors</h4></div>
            <div class="matrix-item"><img src="./WA_1776549716792.jpeg"><h4>Roofing Matrix</h4></div>
            <div class="matrix-item"><img src="./WA_1776549781247.jpeg"><h4>Solar Power Hub</h4></div>
            <div class="matrix-item"><img src="./WA_1776549862258.jpeg"><h4>Kitchen Luxury</h4></div>
            <div class="matrix-item"><img src="./WA_1776549917709.jpeg"><h4>Master Bath Remodel</h4></div>
            <div class="matrix-item"><img src="./WA_1776549990291.jpeg"><h4>Interior Concepts</h4></div>
            <div class="matrix-item"><img src="./WA_1776550066723.jpeg"><h4>Smart Home Matrix</h4></div>
            <div class="matrix-item"><img src="./WA_1776550133465.jpeg"><h4>Exterior Siding</h4></div>
            <div class="matrix-item"><img src="./WA_1776550199723.jpeg"><h4>Gutters & Drainage</h4></div>
        </div>
    </main>

    <footer class="bg-slate-900 py-16 text-center text-white/30 px-6 border-t border-white/5">
        <p class="text-[9px] font-black uppercase tracking-[0.5em] mb-4">U.S. Home Improvement • Nationwide Network</p>
        <div class="flex justify-center gap-6 text-[8px] font-bold uppercase tracking-widest">
            <span onclick="alert('Privacy Secured')">Privacy Policy</span>
            <span onclick="alert('Terms of Service Verified')">Terms</span>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[2000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-6">
            <h3 class="font-black italic uppercase">Matrix Leads HQ</h3>
            <button onclick="closeAdmin()" class="text-red-500 font-bold text-xs">EXIT terminal</button>
        </div>
        <div id="auth" class="text-center py-10">
            <input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="****">
            <button onclick="unlock()" class="btn-matrix max-w-[200px]">Unlock Terminal</button>
        </div>
        <div id="leads" class="hidden space-y-4 pb-20"></div>
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

        document.getElementById('finalInventoryForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('service').value,
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                alert("LEAD AUTHORIZED SUCCESSFULLY!");
                location.reload();
            });
        });

        // Secret Admin protocol
        let taps = 0, timer;
        function handleAdminTap() {
            taps++; clearTimeout(timer);
            if(taps === 4) { document.getElementById('adminPanel').classList.remove('hidden'); taps=0; }
            timer = setTimeout(() => taps = 0, 1500);
        }
        function unlock() {
            if(document.getElementById('pin').value === "786") {
                document.getElementById('auth').classList.add('hidden');
                document.getElementById('leads').classList.remove('hidden');
                sync();
            }
        }
        function sync() {
            db.ref('leads').on('value', snap => {
                const data = snap.val(); let h = '';
                for(let k in data) {
                    h += `<div class="p-4 border rounded-xl bg-slate-50 relative text-[11px] font-bold">
                        <span class="bg-blue-600 text-white px-2 py-0.5 rounded text-[8px] absolute top-3 right-3 uppercase font-black">${data[k].service}</span>
                        <h4 class="font-black text-slate-900">${data[k].name}</h4>
                        <p>📞 Phone: ${data[k].phone}</p>
                        <p class="text-[10px] text-slate-400 mt-1 uppercase">Time: ${data[k].timestamp}</p>
                        <button onclick="del('${k}')" class="text-red-500 font-black text-[9px] mt-2 uppercase border-b border-red-100">Delete Record</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = h || 'NO LEADS HQ';
            });
        }
        function del(id) { if(confirm('Permanent Delete?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
    </script>
</body>
</html>
