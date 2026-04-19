<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; scroll-behavior: smooth; }
        
        .hero-v5 { background: linear-gradient(rgba(15, 23, 42, 0.9), rgba(15, 23, 42, 0.8)), url('https://images.unsplash.com/photo-1513584684374-8bdb7489feef?q=80&w=2070&auto=format&fit=crop'); background-size: cover; background-position: center; }
        .input-premium { width: 100%; padding: 16px; border: 2px solid #e2e8f0; border-radius: 18px; font-weight: 600; outline: none; transition: 0.4s; background: white; font-size: 14px; }
        .input-premium:focus { border-color: var(--accent); box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px; border-radius: 20px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; box-shadow: 0 15px 30px rgba(37, 99, 235, 0.2); }
        .page-section { display: none; }
        .page-section.active { display: block; }

        /* FIXED CHAT ENGINE */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 580px; background: white; border-radius: 30px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 20px; color: white; display: flex; justify-content: space-between; align-items: center; }
        #chat-feed { flex: 1; padding: 15px; overflow-y: auto; background: #fdfdfd; display: flex; flex-direction: column; gap: 10px; }
        .bubble { padding: 12px 16px; border-radius: 18px; font-size: 13px; max-width: 80%; line-height: 1.4; font-weight: 500; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .bot-opt { border: 2px solid #2563eb; color: #2563eb; padding: 8px; border-radius: 50px; font-size: 11px; font-weight: 800; text-align: center; cursor: pointer; transition: 0.3s; margin-top: 5px; }
        .bot-opt:hover { background: #2563eb; color: white; }
    </style>
</head>
<body>

    <nav class="bg-white/95 backdrop-blur sticky top-0 z-[8000] px-8 py-4 flex justify-between items-center border-b">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-10 w-10 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer shadow-lg">US</div>
            <div>
                <h1 class="text-[11px] font-black text-slate-900 uppercase">U.S. Home Improvement</h1>
                <span class="text-[8px] font-bold text-blue-600 uppercase italic">LLC Registered | BBB A+</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-2 rounded-xl font-black text-[9px] uppercase shadow-lg">Free Quote</button>
    </nav>

    <section id="home" class="page-section active hero-v5 py-40 text-center text-white">
        <h1 class="text-6xl font-black uppercase italic mb-6">Elite <span class="text-blue-500">Service</span>.</h1>
        <p class="max-w-xl mx-auto font-bold uppercase tracking-widest text-slate-300 text-xs mb-10">100% Free Nationwide Site Estimates.</p>
        <button onclick="showPage('form')" class="btn-master px-12">Start Free Survey</button>
    </section>

    <section id="form" class="page-section py-20 px-6">
        <div class="max-w-3xl mx-auto bg-white p-12 rounded-[50px] shadow-2xl border">
            <form id="masterForm" class="space-y-6">
                <h3 class="text-2xl font-black uppercase italic border-b pb-4">Project Details</h3>
                <div class="grid md:grid-cols-2 gap-6">
                    <select id="vSvc" class="input-premium" required onchange="checkWin()"><option value="">Service Type</option><option value="Windows">Windows</option><option value="Roofing">Roofing</option><option value="Solar">Solar</option></select>
                    <input type="number" id="vWin" class="input-premium hidden" placeholder="How many windows?">
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                    <select id="vOwner" class="input-premium" required><option value="Yes">Homeowner (Yes)</option><option value="No">No</option></select>
                    <select id="vCredit" class="input-premium" required><option value="720+">720+ Credit</option><option value="660-719">660-719</option><option value="Below 660">Below 660</option></select>
                </div>
                <input type="text" id="vAddr" class="input-premium" placeholder="Full Address" required>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="text" id="vZip" class="input-premium" placeholder="Zip Code" required>
                    <input type="text" id="vName" class="input-premium" placeholder="Full Name" required>
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="tel" id="vPhone" class="input-premium" placeholder="Phone Number" required>
                    <input type="email" id="vEmail" class="input-premium" placeholder="Email Address" required>
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="date" id="vDate" class="input-premium" required>
                    <select id="vTime" class="input-premium" required><option value="09 AM - 12 PM">09 AM - 12 PM</option><option value="12 PM - 03 PM">12 PM - 03 PM</option><option value="03 PM - 07 PM">03 PM - 07 PM</option></select>
                </div>
                <button type="submit" class="btn-master w-full">Submit Authorization</button>
            </form>
            <div id="vSuccess" class="hidden text-center py-10">
                <h2 class="text-3xl font-black text-blue-600 mb-4">SUBMITTED!</h2>
                <p id="vTid" class="text-xs font-bold uppercase"></p>
                <button onclick="location.reload()" class="mt-6 underline text-[10px] font-black">BACK</button>
            </div>
        </div>
    </section>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="flex items-center gap-3"><div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center">👤</div><div><p class="text-[10px] font-black uppercase">Live Support</p><p class="text-[8px] text-blue-400 font-bold">Agent-786</p></div></div>
                <button onclick="toggleChat()">✕</button>
            </div>
            <div id="chat-feed"></div>
            <div id="bot-panel" class="p-4 bg-slate-50 border-t flex flex-col gap-2">
                <div class="bot-opt" onclick="botResp('pricing')">Free Estimate Pricing?</div>
                <div class="bot-opt" onclick="botResp('areas')">Serviceable Areas?</div>
                <div class="bot-opt" onclick="requestLive()" style="border-color:#ef4444; color:#ef4444;">🚨 Talk to Live Agent</div>
            </div>
            <div class="p-4 border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="Type..." class="w-full text-xs outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full text-white shadow-2xl z-[8500]">💬</button>
    </div>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center border-b pb-6 mb-10">
                <h3 class="text-3xl font-black italic">DISPATCH HUB</h3>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-6 py-2 rounded-xl text-[10px] font-bold">EXIT</button>
            </div>
            <div id="authBox" class="text-center py-20">
                <input type="password" id="pin" class="input-premium max-w-xs text-center text-2xl mb-6" placeholder="PIN">
                <br><button onclick="unlock()" class="btn-master max-w-xs">LOGIN</button>
            </div>
            <div id="hubData" class="hidden grid lg:grid-cols-2 gap-10">
                <div id="adminLeads"></div>
                <div>
                    <h4 class="font-black uppercase mb-6 text-blue-600">Live Chats</h4>
                    <div id="adminChats" class="space-y-4"></div>
                    <div id="adminReplyArea" class="hidden mt-8 p-8 bg-slate-900 rounded-[30px] text-white">
                        <p class="text-[10px] font-black text-blue-400 mb-4">REPLYING TO: <span id="targetUser"></span></p>
                        <input type="text" id="replyText" class="input-premium bg-slate-800 border-slate-700 text-white mb-4" placeholder="Message...">
                        <div class="flex gap-4">
                            <button onclick="sendReply()" class="btn-master flex-1 text-xs">Send</button>
                            <button onclick="clearChat()" class="bg-red-600 px-6 rounded-xl font-bold text-[10px]">CLEAR</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const cid = "USER-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const w = document.getElementById('chat-window'); w.style.display = w.style.display === 'flex' ? 'none' : 'flex'; }
        function checkWin() { document.getElementById('vWin').classList.toggle('hidden', document.getElementById('vSvc').value !== 'Windows'); }

        // CHAT LOGIC
        const feed = document.getElementById('chat-feed');
        window.onload = () => { feed.innerHTML += `<div class="bubble bubble-admin">Welcome! How can we assist you with your free quote today?</div>`; };

        function botResp(t) {
            let m = t === 'pricing' ? "Our estimates are 100% Free - no obligation." : "We serve all 50 US States.";
            feed.innerHTML += `<div class="bubble bubble-user">${t} info</div>`;
            setTimeout(() => { feed.innerHTML += `<div class="bubble bubble-admin">${m}</div>`; feed.scrollTop = feed.scrollHeight; }, 500);
        }

        function requestLive() {
            db.ref('chats/' + cid).push({ text: "🚨 LIVE AGENT REQUESTED", type: 'user' });
            document.getElementById('bot-panel').classList.add('hidden');
            feed.innerHTML += `<div class="bubble bubble-admin" style="background:#fffbeb">Connecting to Agent-786...</div>`;
        }

        function sendMsg() {
            const t = document.getElementById('chat-input').value; if(!t) return;
            db.ref('chats/' + cid).push({ text: t, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        // Real-time Chat Sync
        db.ref('chats/' + cid).on('value', s => {
            let h = `<div class="bubble bubble-admin">Welcome! How can we assist you with your free quote today?</div>`;
            s.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            feed.innerHTML = h; feed.scrollTop = feed.scrollHeight;
        });

        // FORM
        document.getElementById('masterForm').onsubmit = (e) => {
            e.preventDefault(); const tid = "US-" + Math.floor(100000 + Math.random() * 900000);
            const d = { tid, name: document.getElementById('vName').value, phone: document.getElementById('vPhone').value, addr: document.getElementById('vAddr').value, svc: document.getElementById('vSvc').value, credit: document.getElementById('vCredit').value, appt: document.getElementById('vDate').value + " " + document.getElementById('vTime').value };
            db.ref('leads').push(d).then(() => { document.getElementById('masterForm').classList.add('hidden'); document.getElementById('vSuccess').classList.remove('hidden'); document.getElementById('vTid').innerText = "TRACKING ID: " + tid; });
        };

        // ADMIN
        let activeChat = '';
        function handleAdminTap() { if(!window.taps) window.taps=0; window.taps++; if(window.taps>=5) document.getElementById('adminHub').classList.remove('hidden'); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); window.taps=0; }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        function syncAdmin() {
            db.ref('leads').on('value', s => {
                let h = '<h4 class="font-black uppercase mb-6">Leads</h4>';
                s.forEach(l => { const v = l.val(); h += `<div class="p-6 bg-slate-50 rounded-2xl mb-4 border"><p class="text-[10px] font-black">${v.tid}</p><h5 class="font-black">${v.name}</h5><p class="text-[9px] uppercase">${v.svc} | ${v.phone} | ${v.addr}</p><p class="text-[9px] text-blue-600 font-bold uppercase">${v.appt}</p></div>`; });
                document.getElementById('adminLeads').innerHTML = h;
            });
            db.ref('chats').on('value', s => {
                let h = '';
                s.forEach(c => { const uid = c.key; const last = Object.values(c.val()).pop(); h += `<div onclick="openReply('${uid}')" class="p-4 bg-white border-2 rounded-xl cursor-pointer hover:border-blue-500"><p class="text-[8px] font-black">${uid}</p><p class="text-[11px] font-bold truncate">"${last.text}"</p></div>`; });
                document.getElementById('adminChats').innerHTML = h;
            });
        }

        function openReply(u) { activeChat = u; document.getElementById('adminReplyArea').classList.remove('hidden'); document.getElementById('targetUser').innerText = u; }
        function sendReply() { const t = document.getElementById('replyText').value; if(!t) return; db.ref('chats/' + activeChat).push({ text: t, type: 'admin' }); document.getElementById('replyText').value = ''; }
        function clearChat() { if(confirm('Delete?')) { db.ref('chats/' + activeChat).remove(); document.getElementById('adminReplyArea').classList.add('hidden'); } }
    </script>
</body>
</html>
