<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; --success: #10b981; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; scroll-behavior: smooth; }
        .hero-v3 { background: linear-gradient(rgba(15, 23, 42, 0.92), rgba(15, 23, 42, 0.85)), url('https://images.unsplash.com/photo-1513584684374-8bdb7489feef?q=80&w=2070&auto=format&fit=crop') center/cover no-repeat fixed; }
        .glass-blur { background: rgba(255, 255, 255, 0.85); backdrop-filter: blur(20px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; outline: none; transition: 0.4s; font-size: 14px; background: #fff; }
        .input-pro:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px 32px; border-radius: 16px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; border: none; transition: 0.4s; box-shadow: 0 12px 24px rgba(37, 99, 235, 0.25); width: 100%; }
        .btn-elite:hover { transform: translateY(-4px); box-shadow: 0 18px 36px rgba(37, 99, 235, 0.35); }
        .page-section { display: none; }
        .page-section.active { display: block; animation: contentFade 0.7s ease-out; }
        @keyframes contentFade { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 30px; box-shadow: 0 30px 60px -12px rgba(0,0,0,0.25); display: none; flex-direction: column; z-index: 6000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 22px; color: white; display: flex; align-items: center; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); }
    </style>
</head>
<body>

    <nav class="glass-blur sticky top-0 z-[5000] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <div onclick="handleAdminTap()" class="h-12 w-12 bg-slate-900 rounded-2xl flex items-center justify-center text-white font-black cursor-pointer">US</div>
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase tracking-tight">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic">Enterprise National Authority</span>
            </div>
        </div>
        <div class="hidden lg:flex gap-10 text-[10px] font-black uppercase tracking-[0.2em] text-slate-400">
            <button onclick="showPage('home')">Home</button>
            <button onclick="showPage('faq')">FAQ</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-full">Get Quote</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="w-3 h-3 bg-emerald-500 rounded-full border-2 border-slate-900"></div>
                <div><p class="text-[9px] font-black text-blue-400 uppercase">Agent Connection: Verified</p><h4 class="font-black text-[11px] uppercase">Senior Dispatch Support</h4></div>
                <button onclick="toggleChat()" class="ml-auto">✕</button>
            </div>
            <div id="chat-feed" class="flex-1 p-5 overflow-y-auto bg-slate-50 flex flex-col gap-3">
                <div class="bubble bubble-admin">Welcome to U.S. Home Improvement Support. I am Agent-786. How may I assist you with your property survey today?</div>
            </div>
            <div class="p-5 border-t bg-white flex gap-3">
                <input type="text" id="chat-input" placeholder="Type here..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full shadow-2xl flex items-center justify-center text-white z-[5500]">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-v3 py-48 px-6 text-center text-white">
            <h1 class="text-6xl md:text-8xl font-black uppercase italic mb-12">The Elite <span class="text-blue-500">Standard</span>.</h1>
            <p class="text-xs font-bold uppercase tracking-[0.5em] mb-16">Certified Site Inspections & National Logistics.</p>
            <button onclick="showPage('form')" class="btn-elite max-w-[320px]">Initiate Survey</button>
        </header>
    </section>

    <section id="form" class="page-section py-20 bg-white">
        <div class="max-w-3xl mx-auto px-6">
            <div class="bg-white p-12 rounded-[48px] shadow-2xl border border-slate-50">
                <form id="finalForm">
                    <h3 class="text-2xl font-black uppercase italic mb-10">Site Authorization Terminal</h3>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro" required>
                        <input type="email" id="vEmail" placeholder="Email Address" class="input-pro" required>
                    </div>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="tel" id="vPhone" placeholder="Primary Phone" class="input-pro" required>
                        <select id="vSvc" class="input-pro" required>
                            <option value="">Select Service Portfolio</option>
                            <option value="Windows">Windows Replacement</option>
                            <option value="Roofing">Roofing Installation</option>
                            <option value="Solar">Solar Power Matrix</option>
                            <option value="Siding">Siding Repair/Replacement</option>
                            <option value="Kitchen">Kitchen Remodeling</option>
                            <option value="Bathroom">Bathroom Remodeling</option>
                            <option value="HVAC">HVAC (Heating & Air)</option>
                            <option value="Flooring">Flooring (Wood/Tile)</option>
                            <option value="Painting">Interior/Exterior Painting</option>
                            <option value="Garage">Garage Door Systems</option>
                        </select>
                    </div>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="text" id="vZip" placeholder="Zip Code" class="input-pro" required>
                        <select id="vCredit" class="input-pro" required>
                            <option value="">Credit Score</option>
                            <option value="Excellent">720+</option>
                            <option value="Good">660-719</option>
                            <option value="Fair">Below 660</option>
                        </select>
                    </div>
                    <input type="text" id="vAddr" placeholder="Physical Site Address" class="input-pro mb-10" required>
                    <button type="submit" class="btn-elite">Authorize & Transmit</button>
                </form>

                <div id="vReceipt" class="hidden text-center py-10">
                    <h3 class="text-3xl font-black uppercase italic text-emerald-600">Transmission Success</h3>
                    <div id="receipt-data" class="bg-slate-900 text-white p-8 rounded-[35px] my-10 text-left text-xs uppercase font-bold space-y-3">
                        </div>
                    <button onclick="location.reload()" class="text-blue-600 font-black text-[10px] uppercase underline">Return Home</button>
                </div>
            </div>
        </div>
    </section>

    <script>
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const userId = "SIG-" + Math.floor(100000 + Math.random() * 899999);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo({top:0, behavior:'smooth'}); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + userId).push({ text: txt, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + userId).on('value', snap => {
            let h = ''; const msgs = snap.val();
            for(let k in msgs) h += `<div class="bubble ${msgs[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${msgs[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        document.getElementById('finalForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-" + Math.floor(100000 + Math.random() * 900000);
            const data = { tid, name: document.getElementById('vName').value, svc: document.getElementById('vSvc').value, addr: document.getElementById('vAddr').value, ts: new Date().toLocaleString() };
            db.ref('leads').push(data).then(() => {
                document.getElementById('finalForm').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('receipt-data').innerHTML = `<p>ID: ${tid}</p><p>Name: ${data.name}</p><p>Service: ${data.svc}</p><p>Address: ${data.addr}</p>`;
            });
        });

        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5) { alert('Admin Hub Triggered (PIN 786)'); taps=0; } }
    </script>
</body>
</html>
