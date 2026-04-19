<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Dispatch Authority</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #1e293b; }
        
        .hero-premium { background: linear-gradient(rgba(15, 23, 42, 0.94), rgba(15, 23, 42, 0.88)), url('https://images.unsplash.com/photo-1513584684374-8bdb7489feef?auto=format&fit=crop&w=2000'); background-size: cover; background-position: center; }
        .input-elite { width: 100%; padding: 18px; border: 2px solid #e2e8f0; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: white; color: #0f172a; font-size: 14px; }
        .input-elite:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 22px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; transition: 0.3s; box-shadow: 0 15px 30px rgba(37, 99, 235, 0.2); width: 100%; }
        
        /* CHAT BOX STYLING */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 22px; color: white; display: flex; align-items: center; gap: 12px; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #fdfdfd; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .bot-persistent-btn { border: 2px solid #2563eb; color: #2563eb; padding: 10px; border-radius: 50px; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; background: white; transition: 0.3s; margin-bottom: 5px; }

        /* ADMIN CARDS */
        .lead-card { background: white; border: 2px solid #f1f5f9; border-radius: 35px; padding: 25px; margin-bottom: 20px; transition: 0.3s; }
        .status-badge { font-size: 8px; font-weight: 900; padding: 4px 12px; border-radius: 50px; text-transform: uppercase; margin-bottom: 10px; display: inline-block; }
        .status-pending { background: #fffbeb; color: #92400e; }
        .detail-item { font-size: 10px; font-weight: 800; color: #64748b; text-transform: uppercase; letter-spacing: 0.5px; }
        .detail-val { color: #0f172a; font-weight: 700; font-size: 11px; }
    </style>
</head>
<body>

    <nav class="bg-white/95 backdrop-blur sticky top-0 z-[8000] px-8 py-5 flex justify-between items-center border-b">
        <div class="flex items-center gap-4" onclick="handleAdminTap()">
            <div class="h-10 w-10 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer shadow-lg">US</div>
            <div>
                <h1 class="text-xs font-black text-slate-900 uppercase leading-none">U.S. Home Improvement</h1>
                <span class="text-[8px] font-bold text-blue-600 uppercase italic tracking-widest">National Dispatch Authority</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-2 rounded-xl font-black text-[9px] uppercase shadow-lg">Get Free Quote</button>
    </nav>

    <section id="home" class="page-section active hero-premium py-40 text-center text-white">
        <span class="bg-blue-600/20 text-blue-400 px-4 py-1 rounded-full text-[9px] font-black uppercase mb-8 inline-block border border-blue-500/30">50-State Certified Network</span>
        <h1 class="text-6xl md:text-8xl font-black uppercase italic mb-8 tracking-tighter">Elite <span class="text-blue-500">Service</span>.</h1>
        <p class="max-w-xl mx-auto font-bold uppercase tracking-[0.4em] text-slate-300 text-[10px] mb-12">Authorized Property Evaluations & National Logistics.</p>
        <button onclick="showPage('form')" class="btn-master max-w-[300px]">Start Free Survey</button>
    </section>

    <section id="form" class="page-section py-20 px-6">
        <div class="max-w-3xl mx-auto bg-white p-12 rounded-[50px] shadow-2xl border">
            <form id="masterForm" class="space-y-6">
                <div class="flex justify-between items-center border-b pb-4 mb-6">
                    <h3 class="text-xl font-black uppercase italic text-slate-900">Site Qualification</h3>
                    <img src="https://img.icons8.com/ios-filled/50/2563eb/guarantee.png" class="h-6 opacity-50">
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="text" id="vName" placeholder="Full Legal Name" class="input-elite" required>
                    <input type="tel" id="vPhone" placeholder="Primary Phone Number" class="input-elite" required>
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                    <select id="vSvc" class="input-elite" required>
                        <option value="">Portfolio Service</option>
                        <option value="Windows">Window Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                    </select>
                    <select id="vCredit" class="input-elite" required>
                        <option value="">Estimated Credit Score</option>
                        <option value="Excellent (720+)">720+</option>
                        <option value="Good (660-719)">660-719</option>
                        <option value="Fair (Below 660)">Below 660</option>
                    </select>
                </div>
                <input type="text" id="vAddr" placeholder="Physical Property Address" class="input-elite" required>
                <div class="grid md:grid-cols-2 gap-6 mb-10">
                    <input type="date" id="vDate" class="input-elite" required>
                    <select id="vTime" class="input-elite" required>
                        <option value="Morning (9AM-12PM)">Morning</option>
                        <option value="Afternoon (12PM-4PM)">Afternoon</option>
                        <option value="Evening (4PM-7PM)">Evening</option>
                    </select>
                </div>
                <button type="submit" class="btn-master">Transmit To Dispatch</button>
                <p class="text-[9px] text-center text-slate-400 font-bold uppercase italic mt-4">256-Bit SSL Encrypted Secure Transmission</p>
            </form>
            <div id="vSuccess" class="hidden text-center py-10">
                <div class="text-5xl mb-6">🎖️</div>
                <h2 class="text-3xl font-black text-blue-600 mb-4">AUTHORIZED!</h2>
                <p class="text-xs font-bold text-slate-500 uppercase italic">A Senior Dispatcher will call shortly.</p>
                <button onclick="location.reload()" class="underline text-[10px] font-black uppercase mt-8 block mx-auto">New Survey</button>
            </div>
        </div>
    </section>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="w-3 h-3 bg-emerald-500 rounded-full border-2 border-slate-900"></div>
                <h4 class="font-black uppercase text-[11px]">Senior Dispatch Support</h4>
                <button onclick="toggleChat()" class="ml-auto">✕</button>
            </div>
            <div id="chat-feed"></div>
            <div id="bot-persistent-options" class="p-4 bg-slate-50 flex flex-col gap-2 border-t">
                <div class="bot-persistent-btn" onclick="botAsk('cost')">How much is the estimate?</div>
                <div class="bot-persistent-btn" onclick="botAsk('states')">Are you in my state?</div>
                <div class="bot-persistent-btn" onclick="requestLive()" style="border-color:#ef4444; color:#ef4444;">🚨 Speak to Live Agent</div>
            </div>
            <div class="p-5 border-t bg-white flex gap-3">
                <input type="text" id="chat-input" placeholder="Enter message..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[8500]">💬</button>
    </div>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b-2 pb-8">
                <div>
                    <h3 class="text-3xl font-black uppercase italic">Master <span class="text-blue-600">Dispatch</span> Terminal</h3>
                    <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mt-1">USA National Lead Management Hub</p>
                </div>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-8 py-3 rounded-xl text-[10px] font-black">EXIT TERMINAL</button>
            </div>
            
            <div id="authBox" class="text-center py-32"><input type="password" id="pin" class="input-elite max-w-[300px] text-center text-3xl mb-6 shadow-xl" placeholder="••••"><br><button onclick="unlock()" class="btn-master max-w-[300px]">Authorize</button></div>
            
            <div id="hubData" class="hidden grid lg:grid-cols-3 gap-16">
                <div class="lg:col-span-2">
                    <div class="flex justify-between items-center mb-8">
                        <h5 class="font-black uppercase text-xs text-slate-400 italic tracking-widest">Authorized Dispatches</h5>
                        <input type="text" id="leadSearch" placeholder="Search by name..." class="text-[10px] border p-2 rounded-lg" onkeyup="searchLeads()">
                    </div>
                    <div id="adminLeads" class="space-y-6"></div>
                </div>
                <div>
                    <h5 class="font-black uppercase text-xs text-slate-400 mb-8 italic tracking-widest">Active Signals</h5>
                    <div id="adminChats" class="space-y-4"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const userId = "SIG-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }

        // CHATBOT USA VERSION
        function botAsk(t) {
            let m = t === 'cost' ? "All site evaluations and estimates are 100% Free of charge." : "We operate nationwide across all 50 states.";
            const feed = document.getElementById('chat-feed');
            feed.innerHTML += `<div class="bubble bubble-user">${t} query</div>`;
            setTimeout(() => { feed.innerHTML += `<div class="bubble bubble-admin">${m}</div>`; feed.scrollTop = feed.scrollHeight; }, 500);
        }

        function requestLive() {
            db.ref('chats/' + userId).push({ text: "🚨 CUSTOMER REQUESTING LIVE AGENT", type: 'user' });
            document.getElementById('bot-persistent-options').classList.add('hidden');
        }

        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + userId).push({ text: txt, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + userId).on('value', snap => {
            let h = `<div class="bubble bubble-admin">Welcome to U.S. Dispatch. How can we serve you today?</div>`;
            snap.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // SUBMISSION
        document.getElementById('masterForm').onsubmit = (e) => {
            e.preventDefault();
            const data = {
                tid: "US-DIS-" + Math.floor(100000 + Math.random() * 900000),
                name: document.getElementById('vName').value, phone: document.getElementById('vPhone').value,
                svc: document.getElementById('vSvc').value, credit: document.getElementById('vCredit').value,
                addr: document.getElementById('vAddr').value, appt: document.getElementById('vDate').value + " | " + document.getElementById('vTime').value,
                ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('masterForm').classList.add('hidden');
                document.getElementById('vSuccess').classList.remove('hidden');
            });
        };

        // MASTER ADMIN HUB
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncHub(); } }

        function syncHub() {
            db.ref('leads').on('value', snap => {
                let h = '';
                snap.forEach(l => {
                    const v = l.val(); const k = l.key;
                    h += `<div class="lead-card" data-name="${v.name.toLowerCase()}">
                        <div class="status-badge status-pending">● Dispatch Pending</div>
                        <h4 class="text-xl font-black italic text-blue-600 mb-4">${v.name}</h4>
                        <div class="grid grid-cols-2 gap-4">
                            <div><p class="detail-item">Service Portfolio</p><p class="detail-val">${v.svc}</p></div>
                            <div><p class="detail-item">Credit Profile</p><p class="detail-val text-blue-500">${v.credit}</p></div>
                            <div><p class="detail-item">Phone Number</p><p class="detail-val">📞 ${v.phone}</p></div>
                            <div><p class="detail-item">Appointment</p><p class="detail-val text-emerald-600">📅 ${v.appt}</p></div>
                            <div class="col-span-2"><p class="detail-item">Property Location</p><p class="detail-val">📍 ${v.addr}</p></div>
                        </div>
                        <div class="flex gap-4 mt-6 pt-4 border-t">
                             <button onclick="del('${k}')" class="text-red-500 font-black text-[9px] uppercase hover:underline">Erase Dispatch</button>
                             <button class="text-blue-600 font-black text-[9px] uppercase hover:underline ml-auto">Mark Contacted</button>
                        </div>
                    </div>`;
                });
                document.getElementById('adminLeads').innerHTML = h || 'No dispatches found.';
            });

            db.ref('chats').on('value', snap => {
                let h = '';
                snap.forEach(c => {
                    const uid = c.key; const last = Object.values(c.val()).pop();
                    h += `<div class="p-4 bg-white border-2 border-slate-50 rounded-2xl shadow-sm"><p class="text-[8px] font-black text-blue-600 uppercase">${uid}</p><p class="text-[11px] font-bold italic">"${last.text}"</p></div>`;
                });
                document.getElementById('adminChats').innerHTML = h || 'No active signals.';
            });
        }

        function del(k) { if(confirm('Permanently erase this lead data?')) db.ref('leads/' + k).remove(); }
        function searchLeads() {
            const val = document.getElementById('leadSearch').value.toLowerCase();
            document.querySelectorAll('.lead-card').forEach(c => {
                c.style.display = c.getAttribute('data-name').includes(val) ? 'block' : 'none';
            });
        }
    </script>
</body>
</html>
