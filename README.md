<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. Home Improvement | National Service Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        body { font-family: 'Inter', sans-serif; background-color: #fcfcfc; color: #1a1a1a; margin: 0; }
        
        /* Corporate Header Styling */
        .nav-bar { background: white; border-bottom: 1px solid #eee; padding: 15px 20px; display: flex; align-items: center; justify-content: space-between; position: sticky; top: 0; z-index: 100; }
        
        /* Clean Matrix Form */
        .step-panel { display: none; }
        .step-panel.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .form-container { background: white; border: 1px solid #e5e7eb; border-radius: 12px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1); }
        
        .input-box { width: 100%; padding: 12px; border: 1px solid #d1d5db; border-radius: 6px; font-size: 15px; margin-top: 5px; outline-color: #2563eb; }
        
        .btn-primary { background: #1e3a8a; color: white; padding: 14px; border-radius: 6px; font-weight: 700; width: 100%; cursor: pointer; transition: 0.2s; border: none; }
        .btn-primary:hover { background: #1e40af; }

        /* Trusted Grid Fix */
        .service-grid { display: grid; grid-cols: 2; gap: 15px; padding: 20px; }
        .service-item { background: white; border: 1px solid #efefef; border-radius: 10px; text-align: center; padding-bottom: 15px; overflow: hidden; }
        .service-item img { width: 100%; height: 120px; object-fit: cover; }
        .service-item h4 { font-size: 11px; font-weight: 800; color: #374151; margin-top: 10px; text-transform: uppercase; letter-spacing: 0.5px; }
    </style>
</head>
<body>

    <nav class="nav-bar">
        <div class="flex items-center gap-2">
            <img src="./WA_1776550450872.jpeg" class="h-8 w-8 rounded-full border shadow-sm">
            <span onclick="handleAdminTap()" class="font-bold text-sm tracking-tight cursor-pointer uppercase">U.S. Home Improvement</span>
        </div>
        <div class="text-[9px] font-bold text-blue-700 bg-blue-50 px-2 py-1 rounded">EST. 2026</div>
    </nav>

    <div class="bg-slate-50 py-10 px-4">
        <div class="max-w-md mx-auto">
            <div class="text-center mb-6">
                <h2 class="text-2xl font-extrabold text-slate-900">National Quote Matrix</h2>
                <p class="text-slate-500 text-xs mt-1">Authorized Contractor Appointment System</p>
            </div>

            <div class="form-container p-6">
                <form id="proForm">
                    <div class="step-panel active" id="s1">
                        <label class="text-xs font-bold text-slate-600">Select Project Type</label>
                        <select id="service" class="input-box mb-4" required>
                            <option value="Windows">Replacement Windows</option>
                            <option value="Roofing">Architectural Roofing</option>
                            <option value="Solar">Solar Energy Hub</option>
                            <option value="Kitchen">Kitchen Remodeling</option>
                        </select>
                        <input type="text" id="cName" placeholder="Full Legal Name" class="input-box mb-4" required>
                        <button type="button" onclick="goNext('s2')" class="btn-primary mt-2">Continue</button>
                    </div>

                    <div class="step-panel" id="s2">
                        <input type="text" id="address" placeholder="Street Address" class="input-box mb-4" required>
                        <div class="flex gap-4 mb-4">
                            <input type="text" id="cZip" placeholder="Zip Code" class="input-box" required>
                            <select id="owner" class="input-box" required>
                                <option value="Homeowner">Homeowner</option>
                                <option value="Tenant">Tenant</option>
                            </select>
                        </div>
                        <button type="button" onclick="goNext('s3')" class="btn-primary">Next Step</button>
                    </div>

                    <div class="step-panel" id="s3">
                        <div class="flex gap-4 mb-4">
                            <input type="date" id="appDate" class="input-box" required>
                            <select id="appTime" class="input-box" required>
                                <option value="Morning">Morning</option>
                                <option value="Afternoon">Afternoon</option>
                            </select>
                        </div>
                        <input type="tel" id="cPhone" placeholder="Mobile Contact Number" class="input-box mb-4" required>
                        <button type="submit" class="btn-primary">Finalize Booking</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <div class="grid grid-cols-2 gap-4 px-4 py-8 max-w-md mx-auto">
        <div class="service-item"><img src="./WA_1776549555727.jpeg"><h4>Windows</h4></div>
        <div class="service-item"><img src="./WA_1776549716792.jpeg"><h4>Roofing</h4></div>
        <div class="service-item"><img src="./WA_1776549781247.jpeg"><h4>Solar Hub</h4></div>
        <div class="service-item"><img src="./WA_1776549862258.jpeg"><h4>Kitchen</h4></div>
    </div>

    <footer class="bg-white border-t py-10 text-center text-slate-400">
        <p class="text-[9px] font-bold tracking-widest uppercase mb-1">U.S. Home Improvement • Nationwide Network</p>
        <p class="text-[8px] uppercase">Official Certified Contractor Portal © 2026</p>
    </footer>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[200] p-6 hidden overflow-y-auto">
        <div class="flex justify-between border-b pb-4 mb-6">
            <h3 class="font-bold uppercase italic">Admin Terminal</h3>
            <button onclick="closeAdmin()" class="text-red-500 font-bold text-xs">EXIT</button>
        </div>
        <div id="auth" class="text-center py-10">
            <input type="password" id="pin" class="input-box max-w-[200px] text-center mb-4" placeholder="PIN">
            <button onclick="unlock()" class="btn-primary max-w-[200px]">Unlock</button>
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

        function goNext(id) {
            document.querySelectorAll('.step-panel').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        document.getElementById('proForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                service: document.getElementById('service').value,
                name: document.getElementById('cName').value,
                address: document.getElementById('address').value,
                zip: document.getElementById('cZip').value,
                owner: document.getElementById('owner').value,
                appDate: document.getElementById('appDate').value,
                appTime: document.getElementById('appTime').value,
                phone: document.getElementById('cPhone').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                alert("Appointment Scheduled Successfully!");
                location.reload();
            });
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
                    h += `<div class="p-4 border rounded-lg bg-slate-50 mb-4 text-[11px] font-bold">
                        <p class="text-blue-600 uppercase mb-2">${data[k].service}</p>
                        <p>NAME: ${data[k].name}</p>
                        <p>PHONE: ${data[k].phone}</p>
                        <p>ADDR: ${data[k].address}, ${data[k].zip}</p>
                        <p>APPT: ${data[k].appDate} (${data[k].appTime})</p>
                        <button onclick="del('${k}')" class="text-red-500 mt-2 uppercase">Delete</button>
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
