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
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #0f172a; margin: 0; }
        .nav-pro { background: white; border-bottom: 1px solid #f1f5f9; position: sticky; top: 0; z-index: 1000; padding: 15px 20px; }
        .hero-banner { background: #1e3a8a; padding: 45px 20px; text-align: center; color: white; border-bottom: 5px solid #2563eb; }
        
        .form-card { background: white; border-radius: 20px; border: 1px solid #e2e8f0; box-shadow: 0 10px 25px rgba(0,0,0,0.05); padding: 25px; margin: -30px 15px 30px; }
        .input-box { width: 100%; padding: 12px; border: 1px solid #cbd5e1; border-radius: 10px; margin-bottom: 15px; font-weight: 600; outline-color: #1e3a8a; }
        .btn-matrix { background: #1e3a8a; color: white; padding: 16px; border-radius: 10px; font-weight: 800; width: 100%; text-transform: uppercase; cursor: pointer; border: none; }

        .service-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; padding: 0 15px 40px; }
        .card { background: white; border: 1px solid #f1f5f9; border-radius: 15px; overflow: hidden; text-align: center; padding-bottom: 12px; box-shadow: 0 4px 6px rgba(0,0,0,0.02); }
        .card img { width: 100%; height: 120px; object-fit: cover; }
        .card h4 { font-size: 10px; font-weight: 800; color: #1e3a8a; margin-top: 8px; text-transform: uppercase; }
    </style>
</head>
<body>

    <nav class="nav-pro flex justify-between items-center">
        <div class="flex items-center gap-2">
            <img src="./WA_1776550450872.jpeg" class="h-8 w-8 rounded-full border">
            <span onclick="handleAdminTap()" class="font-black text-xs uppercase cursor-pointer">U.S. Home Improvement</span>
        </div>
        <div class="text-[9px] font-bold text-blue-700 bg-blue-50 px-2 py-1 rounded">EST. 2026</div>
    </nav>

    <header class="hero-banner">
        <h1 class="text-2xl font-black uppercase italic tracking-tighter">Enterprise Upgrades</h1>
        <p class="text-[8px] font-bold uppercase tracking-[0.5em] text-blue-200">Certified National Matrix</p>
    </header>

    <main class="max-w-md mx-auto">
        <div class="form-card">
            <form id="matrixLeadForm">
                <select id="service" class="input-box" required>
                    <option value="Roofing">Roofing</option>
                    <option value="Solar">Solar Panels</option>
                    <option value="Windows">Windows</option>
                    <option value="Doors">Doors</option>
                    <option value="Kitchen">Kitchen Remodel</option>
                    <option value="Bathroom">Bathroom Remodel</option>
                    <option value="Garage">Garage</option>
                    <option value="Deck">Deck</option>
                </select>
                <input type="text" id="cName" placeholder="Full Name" class="input-box" required>
                <input type="tel" id="cPhone" placeholder="Phone Number" class="input-box" required>
                <button type="submit" class="btn-matrix">Authorize Project</button>
            </form>
        </div>

        <div class="service-grid">
            <div class="card"><img src="./WA_1776549716792.jpeg"><h4>Roofing</h4></div>
            <div class="card"><img src="./WA_1776549781247.jpeg"><h4>Solar Panels</h4></div>
            <div class="card"><img src="./WA_1776549555727.jpeg"><h4>Windows</h4></div>
            <div class="card"><img src="./WA_1776549622236.jpeg"><h4>Doors</h4></div>
            <div class="card"><img src="./WA_1776549862258.jpeg"><h4>Kitchen</h4></div>
            <div class="card"><img src="./WA_1776549917709.jpeg"><h4>Bathroom</h4></div>
            <div class="card"><img src="./WA_1776550133465.jpeg"><h4>Garage</h4></div>
            <div class="card"><img src="./WA_1776549990291.jpeg"><h4>Deck</h4></div>
        </div>
    </main>

    <footer class="bg-white border-t py-12 px-8 text-center">
        <p class="text-[9px] font-bold text-slate-400 uppercase tracking-widest mb-4">U.S. Home Improvement • National Enterprise</p>
        <div class="flex justify-center gap-6 text-[8px] font-black text-slate-300 uppercase">
            <span onclick="alert('Privacy Secured')">Privacy Policy</span>
            <span onclick="alert('Terms Verified')">Terms</span>
        </div>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[2000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-4 mb-6"><h3 class="font-black uppercase">Leads HQ</h3><button onclick="closeAdmin()" class="text-red-500 font-bold">EXIT</button></div>
        <div id="auth" class="text-center py-10">
            <input type="password" id="pin" class="input-box max-w-[200px] text-center" placeholder="PIN">
            <button onclick="unlock()" class="btn-matrix max-w-[200px] mt-2">Unlock</button>
        </div>
        <div id="leads" class="hidden"></div>
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

        document.getElementById('matrixLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('service').value,
                name: document.getElementById('cName').value,
                phone: document.getElementById('cPhone').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { alert("Success!"); location.reload(); });
        });

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
                    h += `<div class="p-4 border rounded-xl mb-3 relative bg-slate-50">
                        <span class="bg-blue-600 text-white px-2 py-0.5 rounded text-[8px] absolute top-3 right-3 uppercase font-black">${data[k].service}</span>
                        <h4 class="font-bold text-slate-900">${data[k].name}</h4>
                        <p class="text-[10px]">📞 ${data[k].phone}</p>
                        <button onclick="del('${k}')" class="text-red-500 font-bold text-[8px] mt-2 uppercase">Delete</button>
                    </div>`;
                }
                document.getElementById('leads').innerHTML = h || 'No Leads';
            });
        }
        function del(id) { if(confirm('Delete?')) db.ref('leads/'+id).remove(); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
    </script>
</body>
</html>
