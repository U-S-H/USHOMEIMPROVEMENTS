<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | Official National Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; --success: #059669; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fafafa; color: #1e293b; }
        
        .hero-gradient { background: linear-gradient(rgba(15, 23, 42, 0.8), rgba(15, 23, 42, 0.8)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
        .glass-nav { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(12px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        .card-pro { background: white; border: 1px solid #f1f5f9; border-radius: 24px; transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        .card-pro:hover { transform: translateY(-8px); box-shadow: 0 20px 40px rgba(0,0,0,0.08); }
        
        .input-pro { width: 100%; padding: 14px 18px; border: 2px solid #f1f5f9; border-radius: 12px; font-weight: 600; transition: 0.3s; font-size: 14px; outline: none; }
        .input-pro:focus { border-color: var(--accent); background: #f8faff; box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }
        
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 16px 32px; border-radius: 14px; font-weight: 800; text-transform: uppercase; letter-spacing: 0.5px; transition: 0.3s; box-shadow: 0 10px 20px rgba(37, 99, 235, 0.2); }
        .btn-master:hover { transform: scale(1.02); box-shadow: 0 15px 30px rgba(37, 99, 235, 0.3); }

        .page-section { display: none; }
        .page-section.active { display: block; animation: slideUp 0.5s ease; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        /* Floating Chat System */
        #chat-trigger { position: fixed; bottom: 30px; right: 30px; z-index: 1000; transition: 0.3s; }
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 340px; height: 500px; background: white; border-radius: 24px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.25); display: none; flex-direction: column; overflow: hidden; z-index: 1001; border: 1px solid #f1f5f9; }
        .chat-header { background: #1e3a8a; padding: 20px; color: white; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 10px; }
        .bubble { padding: 10px 14px; border-radius: 15px; font-size: 13px; max-width: 80%; font-weight: 500; }
        .bubble-admin { background: #e2e8f0; align-self: flex-start; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; }

        #toast { position: fixed; bottom: 30px; left: 30px; background: white; padding: 12px 20px; border-radius: 16px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); display: none; z-index: 2000; border-left: 4px solid var(--accent); }
    </style>
</head>
<body>

    <div id="toast" class="flex items-center gap-3">
        <div class="w-2 h-2 rounded-full bg-blue-600 animate-ping"></div>
        <p id="toast-msg" class="text-[10px] font-bold uppercase tracking-wider text-slate-600 italic"></p>
    </div>

    <nav class="glass-nav sticky top-0 z-[1500] px-6 py-4 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <img src="logo.png" onclick="handleAdminTap()" class="h-11 w-11 object-contain bg-white rounded-xl shadow-sm border border-slate-100 cursor-pointer" onerror="this.src='https://ui-avatars.com/api/?name=US&background=1e3a8a&color=fff'">
            <div>
                <h1 class="text-sm font-black text-blue-950 uppercase leading-none tracking-tight">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-emerald-600 uppercase italic">● Licensed National Terminal</span>
            </div>
        </div>
        <div class="hidden lg:flex gap-10 text-[10px] font-extrabold uppercase tracking-widest text-slate-400">
            <button onclick="showPage('home')" class="hover:text-blue-600 transition">Solutions</button>
            <button onclick="showPage('portfolio')" class="hover:text-blue-600 transition">Transformations</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-2.5 rounded-full hover:bg-blue-700 shadow-lg shadow-blue-200 transition">Get Quote</button>
        </div>
    </nav>

    <div id="chat-trigger">
        <button onclick="toggleChat()" class="w-16 h-16 bg-blue-600 rounded-full shadow-2xl flex items-center justify-center text-2xl text-white hover:scale-110 transition">💬</button>
    </div>
    <div id="chat-window">
        <div class="chat-header">
            <h4 class="font-black uppercase text-xs">Live Support Hub</h4>
            <p class="text-[9px] opacity-70">Typically replies in under 5 mins</p>
        </div>
        <div id="chat-feed">
            <div class="bubble bubble-admin">Welcome! How can we assist with your property today?</div>
        </div>
        <div class="p-4 bg-white border-t flex gap-2">
            <input type="text" id="chat-input" placeholder="Ask anything..." class="w-full text-xs font-semibold outline-none">
            <button onclick="sendChatMessage()" class="text-blue-600 font-black text-xs uppercase">Send</button>
        </div>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-gradient py-32 px-6 text-center text-white">
            <div class="max-w-5xl mx-auto">
                <span class="inline-block px-4 py-1 rounded-full border border-white/30 bg-white/10 text-[10px] font-black uppercase tracking-[0.2em] mb-8">America's Trusted Authority</span>
                <h1 class="text-5xl md:text-8xl font-black uppercase italic leading-[0.9] tracking-tighter mb-10">Premium <br><span class="text-blue-500">Remodeling</span> <br>Network.</h1>
                <p class="max-w-xl mx-auto text-blue-100 font-bold text-xs uppercase tracking-widest mb-12 leading-loose">Providing Certified Site Inspections and Advanced Contractor Dispatch Across 50 States.</p>
                <div class="flex flex-wrap justify-center gap-4">
                    <button onclick="showPage('form')" class="btn-master">Secure Site Survey</button>
                    <button onclick="showPage('portfolio')" class="bg-white/10 backdrop-blur-md border border-white/20 px-8 py-4 rounded-14 font-black uppercase text-xs hover:bg-white/20 transition">View Projects</button>
                </div>
            </div>
        </header>

        <div class="max-w-7xl mx-auto px-6 py-24">
            <div class="grid md:grid-cols-3 gap-8">
                <div class="card-pro p-8" onclick="startSvc('Roofing')">
                    <img src="WA_1776549716792.jpeg" class="w-full h-56 object-cover rounded-2xl mb-6">
                    <h3 class="font-black text-blue-900 uppercase italic mb-3">Elite Roofing</h3>
                    <p class="text-[11px] font-bold text-slate-400 uppercase leading-relaxed">Lifetime protection systems for residential assets.</p>
                </div>
                <div class="card-pro p-8" onclick="startSvc('Solar')">
                    <img src="WA_1776549781247.jpeg" class="w-full h-56 object-cover rounded-2xl mb-6">
                    <h3 class="font-black text-blue-900 uppercase italic mb-3">Solar Matrix</h3>
                    <p class="text-[11px] font-bold text-slate-400 uppercase leading-relaxed">Energy independence with tier-1 technology.</p>
                </div>
                <div class="card-pro p-8" onclick="startSvc('Interior')">
                    <img src="WA_1776549917709.jpeg" class="w-full h-56 object-cover rounded-2xl mb-6">
                    <h3 class="font-black text-blue-900 uppercase italic mb-3">Kitchen/Bath Spas</h3>
                    <p class="text-[11px] font-bold text-slate-400 uppercase leading-relaxed">Gourmet transformations and luxury upgrades.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="portfolio" class="page-section py-24 px-6 bg-slate-50">
        <div class="max-w-6xl mx-auto">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-black uppercase italic text-blue-950 mb-4">The <span class="text-blue-600">Standard</span></h2>
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest">Recent Authorized Site Transformations</p>
            </div>
            <div class="grid md:grid-cols-2 gap-10">
                <div class="card-pro overflow-hidden">
                    <div class="bg-blue-600 text-white text-[9px] font-black uppercase py-2 px-4 italic">Texas Division | Kitchens</div>
                    <img src="WA_1776549917709.jpeg" class="w-full h-72 object-cover">
                </div>
                <div class="card-pro overflow-hidden">
                    <div class="bg-blue-600 text-white text-[9px] font-black uppercase py-2 px-4 italic">Florida Division | Roofing</div>
                    <img src="WA_1776549716792.jpeg" class="w-full h-72 object-cover">
                </div>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-24 bg-white px-6">
        <div class="max-w-2xl mx-auto">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-black uppercase italic text-blue-950">Secure <span class="text-blue-600">Estimate</span></h2>
                <p class="text-[10px] font-bold text-slate-400 uppercase mt-2">Professional Dispatch Terminal V.3</p>
            </div>
            <div class="card-pro p-10 border-2">
                <form id="proForm">
                    <div class="grid md:grid-cols-2 gap-4 mb-4">
                        <input type="text" id="pName" placeholder="Full Legal Name" class="input-pro" required>
                        <input type="tel" id="pPhone" placeholder="Direct Mobile" class="input-pro" required>
                    </div>
                    <select id="pSvc" class="input-pro mb-4" required>
                        <option value="Windows">Windows Systems</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Interior">Kitchen/Bathroom Remodel</option>
                    </select>
                    <input type="text" id="pAddr" placeholder="Property Address (Full)" class="input-pro mb-8" required>
                    <button type="submit" class="btn-master w-full">Authorize Dispatch</button>
                </form>
                <div id="formSuccess" class="hidden text-center py-12">
                    <div class="text-5xl mb-6">✅</div>
                    <h4 class="text-2xl font-black uppercase italic text-blue-950">Application Dispatched</h4>
                    <p class="text-xs font-bold text-slate-400 mt-4 uppercase">Reference ID: #US-<span id="refId"></span></p>
                </div>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-8">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b pb-6">
                <h3 class="text-2xl font-black uppercase italic text-blue-950">Master Hub <span class="text-blue-600">Terminal</span></h3>
                <button onclick="closeAdmin()" class="bg-red-50 text-red-500 font-black px-6 py-2 rounded-full uppercase text-xs">Exit</button>
            </div>
            
            <div id="authBox" class="text-center py-20">
                <input type="password" id="adminPin" class="input-pro max-w-[240px] text-center text-xl mb-4" placeholder="HUB PIN">
                <br><button onclick="verifyAdmin()" class="btn-master">Unlock Hub</button>
            </div>

            <div id="hubContent" class="hidden grid lg:grid-cols-3 gap-10">
                <div class="lg:col-span-2">
                    <h5 class="font-black uppercase text-xs mb-6 text-slate-400">Recent Dispatches</h5>
                    <div id="leadContainer" class="space-y-4"></div>
                </div>
                <div>
                    <h5 class="font-black uppercase text-xs mb-6 text-slate-400">Live Interactions</h5>
                    <div id="chatContainer" class="space-y-4"></div>
                </div>
            </div>
        </div>
    </div>

    <footer class="bg-slate-950 text-white py-24 px-6 text-center">
        <div class="max-w-4xl mx-auto">
            <img src="logo.png" class="h-12 mx-auto mb-10 opacity-60 grayscale" onerror="this.style.display='none'">
            <div class="grid grid-cols-2 md:grid-cols-4 gap-10 mb-16 opacity-40 grayscale">
                <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Forbes_logo.svg" class="h-4 mx-auto">
                <img src="https://upload.wikimedia.org/wikipedia/commons/a/a2/Better_Business_Bureau_logo.svg" class="h-4 mx-auto">
                <img src="https://upload.wikimedia.org/wikipedia/commons/c/c8/HomeAdvisor_logo.svg" class="h-4 mx-auto">
                <span class="text-[10px] font-black uppercase self-center">USA Certified</span>
            </div>
            <p class="text-[9px] font-bold uppercase tracking-[0.4em] text-slate-500 italic mb-4">Official Enterprise Dispatch Terminal</p>
            <p class="text-[9px] font-bold text-slate-600 uppercase">702 Main Street, Woodland, CA 95695 | (786) Admin Access Only</p>
            <p class="text-[8px] text-slate-700 font-bold uppercase mt-10">© 2026 U.S. Home Improvement LLC. All Data Encrypted.</p>
        </div>
    </footer>

    <script>
        // FIREBASE SETUP
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

        // PAGE LOGIC
        function showPage(id) {
            document.querySelectorAll('.page-section').forEach(p => p.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo({top: 0, behavior: 'smooth'});
        }
        function startSvc(svc) {
            document.getElementById('pSvc').value = svc;
            showPage('form');
        }

        // CHAT LOGIC
        function toggleChat() {
            const win = document.getElementById('chat-window');
            win.style.display = win.style.display === 'flex' ? 'none' : 'flex';
        }
        function sendChatMessage() {
            const input = document.getElementById('chat-input');
            const msg = input.value;
            if(!msg) return;
            const chatData = { text: msg, type: 'user', time: new Date().toLocaleTimeString() };
            db.ref('chats').push(chatData);
            renderBubble(msg, 'user');
            input.value = '';
        }
        function renderBubble(txt, type) {
            const feed = document.getElementById('chat-feed');
            const b = document.createElement('div');
            b.className = `bubble bubble-${type}`;
            b.innerText = txt;
            feed.appendChild(b);
            feed.scrollTop = feed.scrollHeight;
        }

        // FORM SUBMISSION
        document.getElementById('proForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const rid = Math.floor(1000 + Math.random() * 9000);
            const data = {
                id: rid,
                name: document.getElementById('pName').value,
                phone: document.getElementById('pPhone').value,
                service: document.getElementById('pSvc').value,
                address: document.getElementById('pAddr').value,
                time: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('proForm').classList.add('hidden');
                document.getElementById('refId').innerText = rid;
                document.getElementById('formSuccess').classList.remove('hidden');
            });
        });

        // ADMIN TERMINAL
        let tapCount = 0;
        function handleAdminTap() {
            tapCount++;
            if(tapCount >= 5) {
                document.getElementById('adminPanel').classList.remove('hidden');
                tapCount = 0;
            }
            setTimeout(() => tapCount = 0, 3000);
        }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function verifyAdmin() {
            if(document.getElementById('adminPin').value === "786") {
                document.getElementById('authBox').classList.add('hidden');
                document.getElementById('hubContent').classList.remove('hidden');
                startHubSync();
            }
        }
        function startHubSync() {
            // Sync Leads
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    h += `<div class="bg-slate-50 p-6 rounded-2xl border flex justify-between items-center">
                        <div>
                            <p class="text-[10px] font-black text-blue-600 uppercase mb-1">${leads[k].service}</p>
                            <h4 class="font-black text-blue-900">${leads[k].name}</h4>
                            <p class="text-[9px] font-bold text-slate-400 mt-1">📞 ${leads[k].phone} | 📍 ${leads[k].address}</p>
                        </div>
                        <button onclick="delItem('leads/${k}')" class="text-red-500 font-black text-[9px] uppercase">Erase</button>
                    </div>`;
                }
                document.getElementById('leadContainer').innerHTML = h || 'Terminal Clear.';
            });
            // Sync Chats
            db.ref('chats').on('value', snap => {
                const chats = snap.val(); let h = '';
                for(let k in chats) {
                    h += `<div class="p-3 border-b text-[10px] font-bold">
                        <span class="${chats[k].type === 'user' ? 'text-blue-600' : 'text-slate-400'} uppercase">${chats[k].type}:</span> ${chats[k].text}
                        <button onclick="delItem('chats/${k}')" class="ml-2 text-red-300">×</button>
                    </div>`;
                }
                document.getElementById('chatContainer').innerHTML = h || 'No Active Chats.';
            });
        }
        function delItem(path) { if(confirm('Erase Record?')) db.ref(path).remove(); }

        // LIVE TOASTS
        const names = ["Robert", "Linda", "Michael", "Sarah", "Kevin", "Emily", "Jason"];
        const products = ["Roofing", "Solar", "Windows", "Kitchens"];
        setInterval(() => {
            const t = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = `⚡ ${names[Math.floor(Math.random()*names.length)]} authorized a ${products[Math.floor(Math.random()*products.length)]} survey!`;
            t.style.display = 'flex';
            setTimeout(() => t.style.display = 'none', 6000);
        }, 20000);
    </script>
</body>
</html>
