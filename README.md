<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | Master Dispatch Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #1e293b; scroll-behavior: smooth; }
        
        .hero-v6 { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.85)), url('https://images.unsplash.com/photo-1513584684374-8bdb7489feef?q=80&w=2070&auto=format&fit=crop'); background-size: cover; background-position: center; }
        .input-elite { width: 100%; padding: 18px; border: 2px solid #e2e8f0; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: white; font-size: 14px; color: #0f172a; }
        .input-elite:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 22px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; box-shadow: 0 15px 30px rgba(37, 99, 235, 0.2); transition: 0.3s; }
        .btn-master:hover { transform: translateY(-3px); box-shadow: 0 20px 40px rgba(37, 99, 235, 0.3); }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        /* ADVANCED CHAT SYSTEM */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 380px; height: 600px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 25px; color: white; display: flex; justify-content: space-between; align-items: center; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #fdfdfd; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 14px 18px; border-radius: 22px; font-size: 13px; max-width: 85%; font-weight: 500; line-height: 1.5; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        
        /* ADMIN PANEL UI - HIGH VISIBILITY */
        .admin-card { background: white; border: 2px solid #f1f5f9; border-radius: 30px; padding: 25px; transition: 0.3s; position: relative; }
        .admin-card:hover { border-color: #2563eb; box-shadow: 0 10px 30px rgba(0,0,0,0.05); }
        .reply-box { background: #0f172a; border-radius: 30px; padding: 30px; border: 3px solid #2563eb; color: white; }
        .reply-input { width: 100%; background: #1e293b; border: 1px solid #334155; border-radius: 15px; padding: 15px; color: white; font-weight: 600; outline: none; margin-bottom: 15px; }
    </style>
</head>
<body>

    <nav class="bg-white/95 backdrop-blur sticky top-0 z-[8000] px-8 py-5 flex justify-between items-center border-b">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-12 w-12 bg-slate-900 rounded-2xl flex items-center justify-center text-white font-black cursor-pointer shadow-xl">US</div>
            <div>
                <h1 class="text-xs font-black text-slate-900 uppercase tracking-tighter">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic">Enterprise National Hub</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-2xl font-black text-[10px] uppercase shadow-lg">Free Quote</button>
    </nav>

    <section id="home" class="page-section active hero-v6 py-48 text-center text-white">
        <h1 class="text-6xl md:text-8xl font-black uppercase italic mb-8 tracking-tighter">Professional <span class="text-blue-500">Excellence.</span></h1>
        <p class="max-w-xl mx-auto font-bold uppercase tracking-[0.3em] text-slate-300 text-xs mb-12">Authorized Nationwide Contractor Network.</p>
        <button onclick="showPage('form')" class="btn-master px-16">Get Free Estimate</button>
    </section>

    <section id="form" class="page-section py-24 px-8 bg-slate-50">
        <div class="max-w-4xl mx-auto bg-white p-12 md:p-20 rounded-[60px] shadow-2xl border">
            <form id="masterForm" class="space-y-8">
                <div class="border-b pb-6">
                    <h3 class="text-3xl font-black uppercase italic">Project Authorization</h3>
                    <p class="text-[10px] font-bold text-slate-400 uppercase">Qualify for 100% Free Site Inspection</p>
                </div>
                
                <div class="grid md:grid-cols-2 gap-8">
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400 mb-3 block">Service Portfolio</label>
                        <select id="vSvc" class="input-elite" required onchange="toggleWin()">
                            <option value="">Select Portfolio</option>
                            <option value="Windows">Windows Replacement</option>
                            <option value="Roofing">Roofing Installation</option>
                            <option value="Solar">Solar Energy Matrix</option>
                            <option value="HVAC">Heating & Cooling</option>
                            <option value="Kitchen">Interior Remodel</option>
                        </select>
                    </div>
                    <div id="winBox" class="hidden">
                        <label class="text-[10px] font-black uppercase text-slate-400 mb-3 block">Total Units</label>
                        <input type="number" id="vUnits" class="input-elite" placeholder="e.g. 12">
                    </div>
                </div>

                <div class="grid md:grid-cols-2 gap-8">
                    <select id="vOwner" class="input-elite" required><option value="Yes">Homeowner: Yes</option><option value="No">No</option></select>
                    <select id="vCredit" class="input-elite" required><option value="Excellent (720+)">720+ Credit</option><option value="Good (660-719)">660-719</option><option value="Fair (Below 660)">Below 660</option></select>
                </div>

                <input type="text" id="vAddr" class="input-elite" placeholder="Physical Address" required>
                <div class="grid md:grid-cols-2 gap-8">
                    <input type="text" id="vZip" class="input-elite" placeholder="Zip Code" required>
                    <input type="text" id="vName" class="input-elite" placeholder="Full Legal Name" required>
                </div>

                <div class="grid md:grid-cols-2 gap-8">
                    <input type="tel" id="vPhone" class="input-elite" placeholder="Primary Phone" required>
                    <input type="email" id="vEmail" class="input-elite" placeholder="Email Address" required>
                </div>

                <div class="grid md:grid-cols-2 gap-8">
                    <input type="date" id="vDate" class="input-elite" required>
                    <select id="vTime" class="input-elite" required>
                        <option value="09:00 AM">09:00 AM</option>
                        <option value="12:00 PM">12:00 PM</option>
                        <option value="03:00 PM">03:00 PM</option>
                        <option value="06:00 PM">06:00 PM</option>
                    </select>
                </div>

                <button type="submit" class="btn-master w-full">Transmit Request</button>
            </form>
            <div id="vSuccess" class="hidden text-center py-10">
                <div class="w-20 h-20 bg-emerald-50 text-emerald-500 rounded-full flex items-center justify-center mx-auto mb-6 text-3xl">✓</div>
                <h2 class="text-3xl font-black uppercase italic mb-4">Transmission Success</h2>
                <p id="vTid" class="text-xs font-bold text-blue-600 uppercase tracking-widest"></p>
                <button onclick="location.reload()" class="mt-10 underline text-[10px] font-black uppercase">New Authorization</button>
            </div>
        </div>
    </section>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center text-xl">👤</div>
                    <div><p class="text-[10px] font-black uppercase">Live Terminal</p><p class="text-[8px] text-blue-400 font-bold uppercase tracking-tighter">Agent-786 Status: Online</p></div>
                </div>
                <button onclick="toggleChat()" class="text-white/50">✕</button>
            </div>
            <div id="chat-feed">
                <div class="bubble bubble-admin">Welcome. I am the U.S. Home Improvement Bot. How can I help you?</div>
                <div id="bot-options" class="flex flex-col gap-2">
                    <button class="border-2 border-blue-600 text-blue-600 p-2 rounded-full text-[10px] font-black" onclick="botResp('price')">Estimate Pricing?</button>
                    <button class="border-2 border-red-500 text-red-500 p-2 rounded-full text-[10px] font-black" onclick="requestLive()">Connect Live Agent</button>
                </div>
            </div>
            <div class="p-4 border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="Type message..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full text-white shadow-2xl z-[8500] flex items-center justify-center text-2xl">💬</button>
    </div>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center border-b pb-8 mb-12">
                <div><h3 class="text-4xl font-black uppercase italic tracking-tighter">Dispatch <span class="text-blue-600">Terminal</span></h3><p class="text-[10px] font-bold text-slate-400 uppercase tracking-[0.3em]">Master Control Hub</p></div>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-8 py-3 rounded-2xl text-[10px] font-black uppercase">Exit Hub</button>
            </div>

            <div id="authBox" class="text-center py-20">
                <input type="password" id="pin" class="input-elite max-w-xs text-center text-3xl mb-6 shadow-xl" placeholder="••••">
                <br><button onclick="unlock()" class="btn-master max-w-xs">Authorize</button>
            </div>

            <div id="hubData" class="hidden grid lg:grid-cols-2 gap-12">
                <div id="adminLeads" class="space-y-6"></div>
                <div>
                    <h4 class="font-black uppercase mb-8 text-slate-400 tracking-widest text-xs">Live Chat Signals</h4>
                    <div id="adminChats" class="space-y-4"></div>
                    
                    <div id="replyInterface" class="hidden mt-10 reply-box shadow-2xl">
                        <div class="flex justify-between items-center mb-6">
                            <p class="text-[10px] font-black text-blue-400 uppercase">Replying To: <span id="targetUser" class="text-white"></span></p>
                            <button onclick="clearChat()" class="text-red-400 font-black text-[9px] uppercase underline">Clear History</button>
                        </div>
                        <input type="text" id="replyText" class="reply-input" placeholder="Type your official message here...">
                        <button onclick="sendReply()" class="btn-master w-full text-xs">Transmit Message</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const cid = "SIG-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const w = document.getElementById('chat-window'); w.style.display = w.style.display === 'flex' ? 'none' : 'flex'; }
        function toggleWin() { document.getElementById('winBox').classList.toggle('hidden', document.getElementById('vSvc').value !== 'Windows'); }

        // CHAT ENGINE
        function botResp(t) {
            const f = document.getElementById('chat-feed');
            f.innerHTML += `<div class="bubble bubble-user">Price Request</div>`;
            setTimeout(() => { f.innerHTML += `<div class="bubble bubble-admin">Estimates are 100% Free. No cost to the owner.</div>`; f.scrollTop = f.scrollHeight; }, 500);
        }

        function requestLive() {
            db.ref('chats/' + cid).push({ text: "🚨 LIVE AGENT REQUESTED", type: 'user' });
            document.getElementById('bot-options').classList.add('hidden');
            document.getElementById('chat-feed').innerHTML += `<div class="bubble bubble-admin" style="background:#fffbeb; color:#92400e;">Connecting to Agent-786...</div>`;
        }

        function sendMsg() {
            const t = document.getElementById('chat-input').value; if(!t) return;
            db.ref('chats/' + cid).push({ text: t, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + cid).on('value', s => {
            let h = `<div class="bubble bubble-admin">Welcome. I am the U.S. Home Improvement Bot. How can I help you?</div>`;
            s.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // FORM SUBMIT
        document.getElementById('masterForm').onsubmit = (e) => {
            e.preventDefault(); const tid = "US-HUB-" + Math.floor(100000 + Math.random() * 900000);
            const data = { tid, name: document.getElementById('vName').value, email: document.getElementById('vEmail').value, phone: document.getElementById('vPhone').value, addr: document.getElementById('vAddr').value, svc: document.getElementById('vSvc').value, credit: document.getElementById('vCredit').value, appt: document.getElementById('vDate').value + " @ " + document.getElementById('vTime').value, ts: new Date().toLocaleString() };
            db.ref('leads').push(data).then(() => { document.getElementById('masterForm').classList.add('hidden'); document.getElementById('vSuccess').classList.remove('hidden'); document.getElementById('vTid').innerText = "TRACKING ID: " + tid; });
        };

        // ADMIN LOGIC
        let taps = 0, activeChat = '';
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncHub(); } }

        function syncHub() {
            db.ref('leads').on('value', s => {
                let h = '<h4 class="font-black uppercase mb-10 text-slate-400 tracking-widest text-xs italic">Qualified Dispatches</h4>';
                s.forEach(l => { const v = l.val(); h += `<div class="admin-card"><span class="absolute top-4 right-6 bg-slate-900 text-white px-3 py-1 rounded-full text-[8px] font-black">${v.tid}</span><h5 class="text-xl font-black italic">${v.name}</h5><p class="text-[10px] font-bold text-blue-600 mt-2">📍 ${v.addr} | 📞 ${v.phone}</p><p class="text-[9px] font-bold text-slate-400 mt-3 uppercase">${v.svc} | Credit: ${v.credit} | Appt: ${v.appt}</p></div>`; });
                document.getElementById('adminLeads').innerHTML = h;
            });
            db.ref('chats').on('value', s => {
                let h = '';
                s.forEach(c => { const uid = c.key; const last = Object.values(c.val()).pop(); h += `<div onclick="openReply('${uid}')" class="p-5 bg-white border-2 rounded-2xl cursor-pointer hover:border-blue-500 shadow-sm"><p class="text-[9px] font-black text-blue-600 uppercase mb-2">${uid}</p><p class="text-[12px] font-bold italic truncate">"${last.text}"</p></div>`; });
                document.getElementById('adminChats').innerHTML = h || '<p class="text-[10px] font-black text-slate-300">No signals.</p>';
            });
        }

        function openReply(u) { activeChat = u; document.getElementById('replyInterface').classList.remove('hidden'); document.getElementById('targetUser').innerText = u; }
        function sendReply() { const t = document.getElementById('replyText').value; if(!t) return; db.ref('chats/' + activeChat).push({ text: t, type: 'admin' }); document.getElementById('replyText').value = ''; }
        function clearChat() { if(confirm('Delete history?')) { db.ref('chats/' + activeChat).remove(); document.getElementById('replyInterface').classList.add('hidden'); } }
    </script>
</body>
</html>
