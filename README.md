<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | Enterprise Lead Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --dark: #020408; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; overflow-x: hidden; scroll-behavior: smooth; }
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 2rem; }
        .neon-border { border: 1px solid rgba(0, 242, 255, 0.2); transition: 0.5s; }
        .neon-border:hover { border-color: var(--neon); box-shadow: 0 0 30px rgba(0, 242, 255, 0.2); }
        .step { display: none; }
        .step.active { display: block; animation: fadeInUp 0.5s ease forwards; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .btn-opt { width: 100%; padding: 1.25rem; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.05); border-radius: 1.5rem; text-align: left; transition: 0.3s; display: flex; justify-content: space-between; align-items: center; }
        .btn-opt:hover { background: rgba(0, 242, 255, 0.1); border-color: var(--neon); transform: scale(1.02); }
        input, select { background: rgba(255,255,255,0.05) !important; border: 1px solid rgba(255,255,255,0.1) !important; color: white !important; outline: none; transition: 0.3s; }
        input:focus { border-color: var(--neon) !important; box-shadow: 0 0 15px rgba(0, 242, 255, 0.1); }
    </style>
</head>
<body class="pb-20">

    <nav class="p-6">
        <div class="max-w-7xl mx-auto glass px-8 py-4 flex justify-between items-center neon-border">
            <div class="leading-none"><span class="text-2xl font-black italic tracking-tighter">U.S. HOME IMPROVEMENTS</span><br><span class="text-[7px] text-cyan-400 font-bold uppercase tracking-[0.5em]">Licensed Contractor Network</span></div>
        </div>
    </nav>

    <section id="portal" class="max-w-2xl mx-auto px-6 mt-10">
        <div class="glass p-8 md:p-12 neon-border">
            <form id="masterForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black mb-6 uppercase italic text-cyan-400">Project Type</h2>
                    <div class="space-y-3">
                        <button type="button" onclick="handleService('Windows')" class="btn-opt"><span>🪟 Windows & Doors</span> <span>→</span></button>
                        <button type="button" onclick="next(2, 'service', 'Roofing')" class="btn-opt"><span>🏠 Roofing & Gutters</span> <span>→</span></button>
                        <button type="button" onclick="next(2, 'service', 'Solar')" class="btn-opt"><span>☀️ Solar Energy</span> <span>→</span></button>
                    </div>
                </div>

                <div class="step" id="step-windows">
                    <h2 class="text-3xl font-black mb-6 uppercase italic text-cyan-400">Window Count</h2>
                    <p class="text-gray-500 text-xs mb-6">How many units do you need replaced?</p>
                    <div class="grid grid-cols-2 gap-4">
                        <button type="button" onclick="next(3, 'units', '1-5')" class="btn-opt"><span>1-5 Units</span></button>
                        <button type="button" onclick="next(3, 'units', '6-10')" class="btn-opt"><span>6-10 Units</span></button>
                        <button type="button" onclick="next(3, 'units', '11-20')" class="btn-opt"><span>11-20 Units</span></button>
                        <button type="button" onclick="next(3, 'units', '20+')" class="btn-opt"><span>20+ Units</span></button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black mb-6 uppercase italic text-cyan-400">Timeline</h2>
                    <div class="space-y-3">
                        <button type="button" onclick="next(4, 'time', 'ASAP / Urgent')" class="btn-opt"><span>🚀 ASAP (Ready to Start)</span></button>
                        <button type="button" onclick="next(4, 'time', 'Within 1 Month')" class="btn-opt"><span>📅 Within 30 Days</span></button>
                        <button type="button" onclick="next(4, 'time', 'Just Estimates')" class="btn-opt"><span>🔍 Getting Estimates</span></button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-3xl font-black mb-6 uppercase italic text-cyan-400">Property Details</h2>
                    <input type="text" id="address" placeholder="Street Address" class="w-full p-5 rounded-2xl mb-4">
                    <div class="grid grid-cols-2 gap-4 mb-8">
                        <input type="text" id="city" placeholder="City" class="p-5 rounded-2xl">
                        <input type="number" id="zip" placeholder="Zip Code" class="p-5 rounded-2xl">
                    </div>
                    <button type="button" onclick="next(5)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase shadow-lg shadow-cyan-900/40">Verify Address</button>
                </div>

                <div class="step" id="step5">
                    <h2 class="text-3xl font-black mb-6 uppercase italic text-cyan-400">Owner Identity</h2>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Name" class="w-full p-5 rounded-2xl">
                        <input type="email" id="email" placeholder="Email Address" class="w-full p-5 rounded-2xl">
                        <input type="tel" id="phone" placeholder="Mobile Number" class="w-full p-5 rounded-2xl">
                        <button type="submit" class="w-full bg-green-600 p-6 rounded-2xl font-black uppercase text-xl mt-4">Submit Application</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 z-[200] bg-black/98 backdrop-blur-3xl p-6 hidden overflow-y-auto">
        <div class="max-w-5xl mx-auto pt-10">
            <div class="flex justify-between items-center mb-10">
                <h2 class="text-4xl font-black italic text-cyan-400 tracking-tighter">LEAD CONTROL CENTER</h2>
                <button onclick="location.reload()" class="bg-white/10 px-6 py-2 rounded-full font-bold">CLOSE</button>
            </div>
            
            <div id="loginBox" class="max-w-md mx-auto text-center">
                <input type="password" id="adminKey" placeholder="Secret Key" class="w-full p-6 rounded-2xl text-center text-3xl tracking-[0.5em] mb-6">
                <button onclick="unlock()" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase">Authorize Access</button>
            </div>

            <div id="leadsDashboard" class="hidden grid gap-6" id="leadsList">
                </div>
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

        let leadData = {};

        function handleService(val) {
            leadData.service = val;
            if(val === 'Windows') {
                showStep('step-windows');
            } else {
                next(3);
            }
        }

        function showStep(id) {
            document.querySelectorAll('.step').forEach(el => el.classList.remove('active'));
            document.getElementById(id).classList.add('active');
        }

        function next(s, k, v) {
            if(k) leadData[k] = v;
            showStep('step' + s);
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            leadData.name = document.getElementById('name').value;
            leadData.email = document.getElementById('email').value;
            leadData.phone = document.getElementById('phone').value;
            leadData.address = `${document.getElementById('address').value}, ${document.getElementById('city').value}`;
            leadData.zip = document.getElementById('zip').value;
            leadData.timestamp = new Date().toLocaleString();

            db.ref('leads').push(leadData).then(() => {
                alert("Application Submitted Sweetie! 🚀");
                location.reload();
            });
        });

        // ADMIN LOGIC
        let clicks = 0;
        document.addEventListener('click', () => {
            clicks++;
            setTimeout(() => clicks = 0, 2000);
            if(clicks === 5) document.getElementById('adminPortal').classList.remove('hidden');
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('leadsDashboard').classList.remove('hidden');
                loadLeads();
            } else { alert("WRONG KEY!"); }
        }

        function loadLeads() {
            db.ref('leads').on('value', (snap) => {
                const data = snap.val();
                let html = '';
                for(let id in data) {
                    html = `
                    <div class="glass p-6 border-l-4 border-cyan-500 relative group">
                        <div class="flex justify-between mb-4">
                            <div>
                                <p class="text-2xl font-black italic">${data[id].name}</p>
                                <p class="text-cyan-400 font-bold uppercase text-xs">${data[id].service} | ${data[id].time}</p>
                            </div>
                            <div class="flex gap-2">
                                <button onclick="copyLead('${id}')" class="bg-blue-600 px-3 py-1 rounded text-[10px] font-bold">COPY</button>
                                <button onclick="deleteLead('${id}')" class="bg-red-600 px-3 py-1 rounded text-[10px] font-bold">DELETE</button>
                            </div>
                        </div>
                        <div class="grid md:grid-cols-2 gap-2 text-sm text-gray-400">
                            <p>📞 ${data[id].phone}</p>
                            <p>📧 ${data[id].email}</p>
                            <p class="col-span-2">📍 ${data[id].address} (Zip: ${data[id].zip})</p>
                        </div>
                        ${data[id].units ? `<p class="mt-2 text-xs text-yellow-500 font-bold">Windows: ${data[id].units} Units</p>` : ''}
                        <p class="mt-4 text-[9px] text-gray-600 uppercase tracking-widest">${data[id].timestamp}</p>
                        <textarea id="copy-${id}" class="hidden">Name: ${data[id].name}\nPhone: ${data[id].phone}\nEmail: ${data[id].email}\nAddress: ${data[id].address}\nService: ${data[id].service}\nTime: ${data[id].time}</textarea>
                    </div>` + html;
                }
                document.getElementById('leadsDashboard').innerHTML = html || '<p class="text-center text-gray-600">No leads found.</p>';
            });
        }

        function copyLead(id) {
            const text = document.getElementById('copy-' + id);
            text.classList.remove('hidden');
            text.select();
            document.execCommand('copy');
            text.classList.add('hidden');
            alert("Lead Data Copied to Clipboard!");
        }

        function deleteLead(id) {
            if(confirm("Are you sure you want to delete this lead?")) {
                db.ref('leads/' + id).remove();
            }
        }
    </script>
</body>
</html>
