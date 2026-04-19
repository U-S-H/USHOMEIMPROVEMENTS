<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | Master Dispatch</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #1e293b; }
        
        .hero-v7 { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.85)), url('https://images.unsplash.com/photo-1513584684374-8bdb7489feef?auto=format&fit=crop&w=2000'); background-size: cover; background-position: center; }
        .input-elite { width: 100%; padding: 18px; border: 2px solid #e2e8f0; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: white; color: #0f172a; font-size: 14px; }
        .input-elite:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 22px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; transition: 0.3s; box-shadow: 0 15px 30px rgba(37, 99, 235, 0.2); }
        
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        /* CHAT SYSTEM */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 580px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 20px; color: white; display: flex; justify-content: space-between; align-items: center; }
        #chat-feed { flex: 1; padding: 15px; overflow-y: auto; background: #fdfdfd; display: flex; flex-direction: column; gap: 10px; }
        .bubble { padding: 12px 16px; border-radius: 20px; font-size: 13px; max-width: 80%; font-weight: 500; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        
        /* ADMIN HUB - FULL DETAILS VIEW */
        .lead-card { background: white; border: 2px solid #f1f5f9; border-radius: 30px; padding: 25px; margin-bottom: 20px; transition: 0.3s; }
        .lead-card:hover { border-color: #2563eb; box-shadow: 0 10px 30px rgba(0,0,0,0.05); }
        .detail-row { display: flex; justify-content: space-between; border-bottom: 1px solid #f8fafc; padding: 8px 0; font-size: 11px; }
        .detail-label { font-weight: 800; color: #64748b; text-transform: uppercase; }
        .detail-value { font-weight: 700; color: #0f172a; text-align: right; }
        
        .reply-terminal { background: #0f172a; border-radius: 30px; padding: 25px; color: white; border: 3px solid #2563eb; }
        .reply-field { width: 100%; background: #1e293b; border: 1px solid #334155; border-radius: 15px; padding: 15px; color: white; font-weight: 600; outline: none; margin-bottom: 10px; }
        .del-action { background: #fee2e2; color: #ef4444; width: 100%; padding: 12px; border-radius: 15px; font-size: 11px; font-weight: 800; text-transform: uppercase; margin-top: 15px; }
    </style>
</head>
<body>

    <nav class="bg-white/95 backdrop-blur sticky top-0 z-[8000] px-8 py-4 flex justify-between items-center border-b">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-10 w-10 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer">US</div>
            <div>
                <h1 class="text-[11px] font-black text-slate-900 uppercase">U.S. Home Improvement</h1>
                <span class="text-[8px] font-bold text-blue-600 uppercase italic tracking-widest">Enterprise Terminal</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-2 rounded-xl font-black text-[9px] uppercase shadow-lg">Free Quote</button>
    </nav>

    <section id="home" class="page-section active hero-v7 py-40 text-center text-white">
        <h1 class="text-6xl font-black uppercase italic mb-6">Master <span class="text-blue-500">Logistics</span>.</h1>
        <p class="max-w-xl mx-auto font-bold uppercase tracking-[0.3em] text-slate-300 text-xs mb-10">Authorized Property Site Evaluations.</p>
        <button onclick="showPage('form')" class="btn-master px-16">Start Survey</button>
    </section>

    <section id="form" class="page-section py-20 px-6">
        <div class="max-w-3xl mx-auto bg-white p-12 rounded-[50px] shadow-2xl border">
            <form id="masterForm" class="space-y-6">
                <h3 class="text-2xl font-black uppercase italic border-b pb-4">Property Qualification</h3>
                <div class="grid md:grid-cols-2 gap-6">
                    <select id="vSvc" class="input-elite" required><option value="">Select Service</option><option value="Windows">Windows</option><option value="Roofing">Roofing</option><option value="Solar">Solar</option></select>
                    <select id="vCredit" class="input-elite" required><option value="Excellent (720+)">720+ Credit</option><option value="Good (660-719)">660-719</option><option value="Fair (Below 660)">Below 660</option></select>
                </div>
                <input type="text" id="vAddr" class="input-elite" placeholder="Physical Address" required>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="text" id="vZip" class="input-elite" placeholder="Zip Code" required>
                    <input type="text" id="vName" class="input-elite" placeholder="Full Name" required>
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="tel" id="vPhone" class="input-elite" placeholder="Phone Number" required>
                    <input type="email" id="vEmail" class="input-elite" placeholder="Email Address" required>
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="date" id="vDate" class="input-elite" required>
                    <select id="vTime" class="input-elite" required><option value="Morning (9AM-12PM)">Morning</option><option value="Afternoon (12PM-4PM)">Afternoon</option><option value="Evening (4PM-7PM)">Evening</option></select>
                </div>
                <button type="submit" class="btn-master w-full">Transmit To Dispatch</button>
            </form>
            <div id="vSuccess" class="hidden text-center py-10">
                <h2 class="text-3xl font-black text-blue-600 mb-4">AUTHORIZED!</h2>
                <button onclick="location.reload()" class="underline text-[10px] font-black uppercase">New Lead</button>
            </div>
        </div>
    </section>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="flex items-center gap-3"><div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center">👤</div><div><p class="text-[10px] font-black uppercase">Live Terminal</p><p class="text-[8px] text-blue-400 font-bold uppercase">Agent-786</p></div></div>
                <button onclick="toggleChat()">✕</button>
            </div>
            <div id="chat-feed"></div>
            <div id="bot-opts" class="p-4 bg-slate-50 border-t flex flex-col gap-2">
                <button class="border-2 border-blue-600 text-blue-600 p-2 rounded-full text-[10px] font-black" onclick="botAsk('price')">Free Estimate Cost?</button>
                <button class="border-2 border-red-500 text-red-500 p-2 rounded-full text-[10px] font-black" onclick="requestLive()">🚨 Connect Live Agent</button>
            </div>
            <div class="p-4 border-t flex gap-2 bg-white">
                <input type="text" id="chat-input" placeholder="Type here..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full text-white shadow-2xl flex items-center justify-center text-2xl z-[8500]">💬</button>
    </div>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center border-b pb-6 mb-10">
                <h3 class="text-3xl font-black italic tracking-tighter uppercase">Dispatch <span class="text-blue-600">Master</span></h3>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-8 py-2 rounded-xl text-[10px] font-bold">CLOSE HUB</button>
            </div>
            <div id="authBox" class="text-center py-20">
                <input type="password" id="pin" class="input-elite max-w-xs text-center text-2xl mb-6 shadow-xl" placeholder="••••">
                <br><button onclick="unlock()" class="btn-master max-w-xs">LOGIN</button>
            </div>
            <div id="hubData" class="hidden grid lg:grid-cols-2 gap-12">
                <div id="adminLeads"></div>
                <div>
                    <h4 class="font-black uppercase mb-6 text-blue-600 text-xs tracking-widest italic">Live Signals</h4>
                    <div id="adminChats" class="space-y-4"></div>
                    <div id="replyArea" class="hidden mt-8 reply-terminal shadow-2xl">
                        <div class="flex justify-between items-center mb-4">
                            <p class="text-[10px] font-black text-blue-400 uppercase">Target: <span id="targetId" class="text-white"></span></p>
                            <button onclick="clearChat()" class="text-red-400 font-black text-[9px] uppercase underline">Clear Chat</button>
                        </div>
                        <input type="text" id="replyText" class="reply-field" placeholder="Type message clearly...">
                        <button onclick="sendReply()" class="btn-master w-full text-xs">Transmit</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const cid = "CID-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const w = document.getElementById('chat-window'); w.style.display = w.style.display === 'flex' ? 'none' : 'flex'; }

        // CHAT LOGIC
        const feed = document.getElementById('chat-feed');
        window.onload = () => { feed.innerHTML = `<div class="bubble bubble-admin">Welcome to U.S. Home Improvement. How can we serve you today?</div>`; };

        function botAsk(t) {
            feed.innerHTML += `<div class="bubble bubble-user">Requesting ${t} info</div>`;
            setTimeout(() => { feed.innerHTML += `<div class="bubble bubble-admin">All property evaluations and estimates are 100% Free at no cost.</div>`; feed.scrollTop = feed.scrollHeight; }, 500);
        }

        function requestLive() {
            db.ref('chats/' + cid).push({ text: "🚨 LIVE AGENT REQUESTED", type: 'user' });
            document.getElementById('bot-opts').classList.add('hidden');
            feed.innerHTML += `<div class="bubble bubble-admin" style="background:#fffbeb; color:#92400e;">Connecting to Senior Dispatcher Agent-786...</div>`;
        }

        function sendMsg() {
            const t = document.getElementById('chat-input').value; if(!t) return;
            db.ref('chats/' + cid).push({ text: t, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + cid).on('value', s => {
            let h = `<div class="bubble bubble-admin">Welcome to U.S. Home Improvement. How can we serve you today?</div>`;
            s.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            feed.innerHTML = h; feed.scrollTop = feed.scrollHeight;
        });

        // FORM
        document.getElementById('masterForm').onsubmit = (e) => {
            e.preventDefault();
            const data = {
                name: document.getElementById('vName').value, phone: document.getElementById('vPhone').value,
                email: document.getElementById('vEmail').value, addr: document.getElementById('vAddr').value,
                zip: document.getElementById('vZip').value, svc: document.getElementById('vSvc').value,
                credit: document.getElementById('vCredit').value, appt: document.getElementById('vDate').value + " | " + document.getElementById('vTime').value,
                ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => { document.getElementById('masterForm').classList.add('hidden'); document.getElementById('vSuccess').classList.remove('hidden'); });
        };

        // ADMIN TERMINAL - FULL DETAILS
        let taps = 0, activeChat = '';
        function handleAdminTap() { taps++; if(taps>=5) document.getElementById('adminHub').classList.remove('hidden'); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); taps=0; }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncHub(); } }

        function syncHub() {
            db.ref('leads').on('value', s => {
                let h = '<h4 class="font-black uppercase mb-6 text-xs text-slate-400 tracking-[0.2em]">Qualified Dispatch Leads</h4>';
                s.forEach(l => { 
                    const v = l.val(); const key = l.key;
                    h += `<div class="lead-card">
                        <h5 class="text-xl font-black italic uppercase text-blue-600 mb-4">${v.name}</h5>
                        <div class="detail-row"><span class="detail-label">Service:</span><span class="detail-value">${v.svc}</span></div>
                        <div class="detail-row"><span class="detail-label">Phone:</span><span class="detail-value">${v.phone}</span></div>
                        <div class="detail-row"><span class="detail-label">Credit:</span><span class="detail-value">${v.credit}</span></div>
                        <div class="detail-row"><span class="detail-label">Zip Code:</span><span class="detail-value">${v.zip}</span></div>
                        <div class="detail-row"><span class="detail-label">Address:</span><span class="detail-value text-[9px]">${v.addr}</span></div>
                        <div class="detail-row"><span class="detail-label">Appointment:</span><span class="detail-value text-emerald-600">${v.appt}</span></div>
                        <div class="detail-row"><span class="detail-label">Timestamp:</span><span class="detail-value">${v.ts}</span></div>
                        <button onclick="delLead('${key}')" class="del-action">Permanently Delete Lead</button>
                    </div>`; 
                });
                document.getElementById('adminLeads').innerHTML = h || 'No leads in system.';
            });
            db.ref('chats').on('value', s => {
                let h = '';
                s.forEach(c => { const uid = c.key; const last = Object.values(c.val()).pop(); h += `<div onclick="openReply('${uid}')" class="p-4 bg-white border rounded-2xl cursor-pointer hover:border-blue-500 shadow-sm"><p class="text-[8px] font-black text-blue-600">${uid}</p><p class="text-[11px] font-bold truncate italic">"${last.text}"</p></div>`; });
                document.getElementById('adminChats').innerHTML = h;
            });
        }

        function delLead(k) { if(confirm('Delete this qualified lead?')) db.ref('leads/' + k).remove(); }
        function openReply(u) { activeChat = u; document.getElementById('replyArea').classList.remove('hidden'); document.getElementById('targetId').innerText = u; }
        function sendReply() { const t = document.getElementById('replyText').value; if(!t) return; db.ref('chats/' + activeChat).push({ text: t, type: 'admin' }); document.getElementById('replyText').value = ''; }
        function clearChat() { if(confirm('Erase history?')) { db.ref('chats/' + activeChat).remove(); document.getElementById('replyArea').classList.add('hidden'); } }
    </script>
</body>
</html>
