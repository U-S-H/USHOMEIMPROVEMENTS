<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. MASTER TERMINAL | Elite Authorization</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #1e293b; overflow-x: hidden; }
        
        .hero-premium { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.85)), url('https://images.unsplash.com/photo-1513584684374-8bdb7489feef?auto=format&fit=crop&w=2000'); background-size: cover; background-position: center; }
        .input-elite { width: 100%; padding: 18px; border: 2px solid #e2e8f0; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: white; color: #0f172a; }
        .input-elite:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 22px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; transition: 0.3s; box-shadow: 0 15px 30px rgba(37, 99, 235, 0.2); }
        
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        /* FIXED CHAT INTERFACE */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 580px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 20px; color: white; display: flex; justify-content: space-between; align-items: center; }
        #chat-feed { flex: 1; padding: 15px; overflow-y: auto; background: #fdfdfd; display: flex; flex-direction: column; gap: 10px; }
        .bubble { padding: 12px 16px; border-radius: 20px; font-size: 13px; max-width: 80%; font-weight: 500; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .bot-option-btn { border: 2px solid #2563eb; color: #2563eb; padding: 10px; border-radius: 50px; font-size: 11px; font-weight: 800; cursor: pointer; text-align: center; transition: 0.3s; margin-bottom: 5px; background: white; }
        .bot-option-btn:hover { background: #2563eb; color: white; }

        /* ADMIN TERMINAL - VISIBILITY FIX */
        .admin-card { background: white; border: 1px solid #e2e8f0; border-radius: 25px; padding: 25px; margin-bottom: 20px; position: relative; transition: 0.3s; }
        .admin-card:hover { border-color: #2563eb; box-shadow: 0 10px 30px rgba(0,0,0,0.05); }
        .reply-terminal { background: #0f172a; border-radius: 30px; padding: 25px; color: white; border: 3px solid #2563eb; }
        .reply-field { width: 100%; background: #1e293b; border: 1px solid #334155; border-radius: 15px; padding: 15px; color: white; font-weight: 600; outline: none; margin-bottom: 10px; }
        .del-btn { background: #fee2e2; color: #ef4444; padding: 8px 15px; border-radius: 12px; font-size: 10px; font-weight: 800; text-transform: uppercase; cursor: pointer; transition: 0.3s; }
        .del-btn:hover { background: #ef4444; color: white; }
    </style>
</head>
<body>

    <nav class="bg-white/95 backdrop-blur sticky top-0 z-[8000] px-8 py-4 flex justify-between items-center border-b">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-10 w-10 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer shadow-lg">US</div>
            <div>
                <h1 class="text-[11px] font-black text-slate-900 uppercase">U.S. Home Improvement</h1>
                <span class="text-[8px] font-bold text-blue-600 uppercase italic">Enterprise Authorized Hub</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-2 rounded-xl font-black text-[9px] uppercase shadow-lg">Free Quote</button>
    </nav>

    <section id="home" class="page-section active hero-premium py-40 text-center text-white">
        <h1 class="text-6xl font-black uppercase italic mb-6">Elite <span class="text-blue-500">Service</span>.</h1>
        <p class="max-w-xl mx-auto font-bold uppercase tracking-widest text-slate-300 text-xs mb-10">Nationwide Licensed Contractor Logistics.</p>
        <button onclick="showPage('form')" class="btn-master px-12">Start Free Survey</button>
    </section>

    <section id="form" class="page-section py-20 px-6">
        <div class="max-w-3xl mx-auto bg-white p-12 rounded-[50px] shadow-2xl border">
            <form id="masterForm" class="space-y-6">
                <h3 class="text-2xl font-black uppercase italic border-b pb-4">Project Authorization</h3>
                <div class="grid md:grid-cols-2 gap-6">
                    <select id="vSvc" class="input-elite" required><option value="">Select Service</option><option value="Windows">Windows</option><option value="Roofing">Roofing</option><option value="Solar">Solar</option></select>
                    <select id="vCredit" class="input-elite" required><option value="720+">720+ Credit</option><option value="660-719">660-719</option><option value="Below 660">Below 660</option></select>
                </div>
                <input type="text" id="vAddr" class="input-elite" placeholder="Full Address" required>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="text" id="vName" class="input-elite" placeholder="Full Name" required>
                    <input type="tel" id="vPhone" class="input-elite" placeholder="Phone Number" required>
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="date" id="vDate" class="input-elite" required>
                    <select id="vTime" class="input-elite" required><option value="Morning">Morning</option><option value="Afternoon">Afternoon</option><option value="Evening">Evening</option></select>
                </div>
                <button type="submit" class="btn-master w-full">Transmit Authorization</button>
            </form>
            <div id="vSuccess" class="hidden text-center py-10">
                <h2 class="text-3xl font-black text-blue-600 mb-4">SUBMITTED!</h2>
                <button onclick="location.reload()" class="underline text-[10px] font-black">NEW REQUEST</button>
            </div>
        </div>
    </section>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="flex items-center gap-3"><div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center">👤</div><div><p class="text-[10px] font-black uppercase">Live Support</p><p class="text-[8px] text-blue-400 font-bold tracking-widest">AGENT-786</p></div></div>
                <button onclick="toggleChat()">✕</button>
            </div>
            <div id="chat-feed"></div>
            <div id="bot-options-container" class="p-4 bg-slate-50 border-t flex flex-col gap-2">
                <div class="bot-option-btn" onclick="botResp('pricing')">Free Estimate Cost?</div>
                <div class="bot-option-btn" onclick="botResp('areas')">Are you in my city?</div>
                <div class="bot-option-btn" onclick="requestLive()" style="border-color:#ef4444; color:#ef4444;">🚨 Talk to Live Agent</div>
            </div>
            <div class="p-4 border-t flex gap-2 bg-white">
                <input type="text" id="chat-input" placeholder="Type message..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full text-white shadow-2xl flex items-center justify-center text-2xl z-[8500]">💬</button>
    </div>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center border-b pb-6 mb-10">
                <h3 class="text-3xl font-black italic">DISPATCH CONTROL</h3>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-6 py-2 rounded-xl text-[10px] font-bold">CLOSE</button>
            </div>
            <div id="authBox" class="text-center py-20">
                <input type="password" id="pin" class="input-elite max-w-xs text-center text-2xl mb-6 shadow-xl" placeholder="PIN">
                <br><button onclick="unlock()" class="btn-master max-w-xs">AUTHORIZE</button>
            </div>
            <div id="hubData" class="hidden grid lg:grid-cols-2 gap-12">
                <div id="adminLeads"></div>
                <div>
                    <h4 class="font-black uppercase mb-6 text-blue-600 tracking-widest text-xs">Active Chat Signals</h4>
                    <div id="adminChats" class="space-y-4"></div>
                    <div id="adminReplyArea" class="hidden mt-8 reply-terminal shadow-2xl">
                        <div class="flex justify-between items-center mb-4">
                            <p class="text-[10px] font-black text-blue-400 uppercase tracking-tighter">Target: <span id="targetUser" class="text-white"></span></p>
                            <button onclick="clearChat()" class="text-red-400 font-black text-[9px] uppercase hover:underline">Clear History</button>
                        </div>
                        <input type="text" id="replyText" class="reply-field" placeholder="Type official response...">
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
        const cid = "USER-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const w = document.getElementById('chat-window'); w.style.display = w.style.display === 'flex' ? 'none' : 'flex'; }

        // CHAT BOT FIXED
        const feed = document.getElementById('chat-feed');
        window.onload = () => { feed.innerHTML = `<div class="bubble bubble-admin">Hello! I am your automated assistant. How can I help you?</div>`; };

        function botResp(t) {
            let m = t === 'pricing' ? "All estimates are 100% Free." : "We serve all 50 states nationwide.";
            feed.innerHTML += `<div class="bubble bubble-user">${t} info</div>`;
            setTimeout(() => { feed.innerHTML += `<div class="bubble bubble-admin">${m}</div>`; feed.scrollTop = feed.scrollHeight; }, 500);
        }

        function requestLive() {
            db.ref('chats/' + cid).push({ text: "🚨 LIVE AGENT REQUESTED", type: 'user' });
            document.getElementById('bot-options-container').classList.add('hidden');
            feed.innerHTML += `<div class="bubble bubble-admin" style="background:#fffbeb; color:#92400e;">Connecting to Agent-786...</div>`;
        }

        function sendMsg() {
            const t = document.getElementById('chat-input').value; if(!t) return;
            db.ref('chats/' + cid).push({ text: t, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + cid).on('value', s => {
            let h = `<div class="bubble bubble-admin">Hello! I am your automated assistant. How can I help you?</div>`;
            s.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            feed.innerHTML = h; feed.scrollTop = feed.scrollHeight;
        });

        // FORM SUBMIT
        document.getElementById('masterForm').onsubmit = (e) => {
            e.preventDefault();
            const d = { name: document.getElementById('vName').value, phone: document.getElementById('vPhone').value, addr: document.getElementById('vAddr').value, svc: document.getElementById('vSvc').value, credit: document.getElementById('vCredit').value, appt: document.getElementById('vDate').value + " " + document.getElementById('vTime').value };
            db.ref('leads').push(d).then(() => { document.getElementById('masterForm').classList.add('hidden'); document.getElementById('vSuccess').classList.remove('hidden'); });
        };

        // ADMIN TERMINAL WITH DELETE LEAD
        let taps = 0, activeChat = '';
        function handleAdminTap() { taps++; if(taps>=5) document.getElementById('adminHub').classList.remove('hidden'); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); taps=0; }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        function syncAdmin() {
            db.ref('leads').on('value', s => {
                let h = '<h4 class="font-black uppercase mb-6 text-xs text-slate-400">Manage Appointments</h4>';
                s.forEach(l => { 
                    const v = l.val(); const key = l.key;
                    h += `<div class="admin-card"><h5 class="font-black italic">${v.name}</h5><p class="text-[10px] font-bold text-blue-600">📞 ${v.phone} | 📍 ${v.addr}</p><p class="text-[9px] text-slate-400 uppercase mt-2">${v.svc} | ${v.appt}</p><button onclick="deleteLead('${key}')" class="del-btn mt-4">Delete Appointment</button></div>`; 
                });
                document.getElementById('adminLeads').innerHTML = h || 'No leads available.';
            });
            db.ref('chats').on('value', s => {
                let h = '';
                s.forEach(c => { const uid = c.key; const last = Object.values(c.val()).pop(); h += `<div onclick="openReply('${uid}')" class="p-4 bg-white border rounded-2xl cursor-pointer hover:border-blue-500 shadow-sm"><p class="text-[8px] font-black text-blue-600">${uid}</p><p class="text-[11px] font-bold italic truncate">"${last.text}"</p></div>`; });
                document.getElementById('adminChats').innerHTML = h;
            });
        }

        function deleteLead(key) { if(confirm('Delete this appointment permanently?')) db.ref('leads/' + key).remove(); }
        function openReply(u) { activeChat = u; document.getElementById('adminReplyArea').classList.remove('hidden'); document.getElementById('targetUser').innerText = u; }
        function sendReply() { const t = document.getElementById('replyText').value; if(!t) return; db.ref('chats/' + activeChat).push({ text: t, type: 'admin' }); document.getElementById('replyText').value = ''; }
        function clearChat() { if(confirm('Clear history?')) { db.ref('chats/' + activeChat).remove(); document.getElementById('adminReplyArea').classList.add('hidden'); } }
    </script>
</body>
</html>
