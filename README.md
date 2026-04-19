<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise Authority</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #1e293b; }
        .hero-v4 { background: linear-gradient(rgba(15, 23, 42, 0.9), rgba(15, 23, 42, 0.8)), url('https://images.unsplash.com/photo-1513584684374-8bdb7489feef?q=80&w=2070&auto=format&fit=crop'); background-size: cover; }
        .input-elite { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: white; }
        .input-elite:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 20px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; width: 100%; box-shadow: 0 15px 30px rgba(37, 99, 235, 0.2); }
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.5s ease-in; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* ADVANCED CHAT SYSTEM */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 380px; height: 600px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #fdfdfd; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .chat-bot-option { background: white; border: 2px solid #2563eb; color: #2563eb; padding: 10px; border-radius: 50px; font-size: 11px; font-weight: 800; text-align: center; cursor: pointer; margin-top: 5px; }
    </style>
</head>
<body>

    <nav class="bg-white/90 backdrop-blur sticky top-0 z-[8000] px-8 py-5 flex justify-between items-center border-b">
        <div class="flex items-center gap-4">
            <div onclick="handleAdminTap()" class="h-12 w-12 bg-slate-900 rounded-2xl flex items-center justify-center text-white font-black cursor-pointer shadow-xl">US</div>
            <div>
                <h1 class="text-xs font-black text-slate-900 uppercase">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic">LLC Registered | BBB A+ Accredited</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-3 rounded-xl font-black text-[10px] uppercase">Free Quote</button>
    </nav>

    <section id="home" class="page-section active hero-v4 py-48 text-center text-white">
        <h1 class="text-6xl md:text-8xl font-black uppercase italic mb-8 tracking-tighter">Elite <span class="text-blue-500">Service</span>.</h1>
        <p class="max-w-2xl mx-auto font-bold uppercase tracking-widest text-slate-300 text-sm mb-12">100% Free Quotes & Site Inspections Nationwide.</p>
        <button onclick="showPage('form')" class="btn-elite max-w-sm">Get Free Estimate</button>
    </section>

    <section id="form" class="page-section py-24 px-8">
        <div class="max-w-3xl mx-auto bg-white p-12 md:p-20 rounded-[60px] shadow-3xl border">
            <form id="masterForm" class="space-y-8">
                <h3 class="text-3xl font-black uppercase italic">Project Survey</h3>
                
                <div class="grid md:grid-cols-2 gap-6">
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400 mb-2 block">Service Type</label>
                        <select id="vSvc" class="input-elite" required onchange="checkWindows()">
                            <option value="">Select Service</option>
                            <option value="Windows">Windows Replacement</option>
                            <option value="Roofing">Roofing System</option>
                            <option value="Solar">Solar Panels</option>
                            <option value="HVAC">Heating & Air</option>
                            <option value="Kitchen">Kitchen Remodel</option>
                        </select>
                    </div>
                    <div id="winBox" class="hidden">
                        <label class="text-[10px] font-black uppercase text-slate-400 mb-2 block">Number of Windows</label>
                        <input type="number" id="vWinCount" class="input-elite" placeholder="Total units">
                    </div>
                </div>

                <div class="grid md:grid-cols-2 gap-6">
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400 mb-2 block">Homeowner?</label>
                        <select id="vOwner" class="input-elite" required><option value="Yes">Yes</option><option value="No">No</option></select>
                    </div>
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400 mb-2 block">Ready to Start?</label>
                        <select id="vReady" class="input-elite" required>
                            <option value="Immediately">Immediately</option>
                            <option value="1-3 Months">1-3 Months</option>
                            <option value="Planning">Just Planning</option>
                        </select>
                    </div>
                </div>

                <div class="grid md:grid-cols-2 gap-6">
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400 mb-2 block">Credit Score</label>
                        <select id="vCredit" class="input-elite" required>
                            <option value="Excellent">720+ (Excellent)</option>
                            <option value="Good">660-719 (Good)</option>
                            <option value="Fair">Below 660 (Fair)</option>
                        </select>
                    </div>
                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-400 mb-2 block">Zip Code</label>
                        <input type="text" id="vZip" class="input-elite" placeholder="Zip Code" required>
                    </div>
                </div>

                <input type="text" id="vAddr" class="input-elite" placeholder="Full Physical Address" required>
                <input type="text" id="vName" class="input-elite" placeholder="Full Legal Name" required>
                
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="tel" id="vPhone" class="input-elite" placeholder="Phone Number" required>
                    <input type="email" id="vEmail" class="input-elite" placeholder="Email Address" required>
                </div>

                <div class="grid md:grid-cols-2 gap-6">
                    <input type="date" id="vDate" class="input-elite" required>
                    <select id="vTime" class="input-elite" required>
                        <option value="09:00 AM">09:00 AM</option>
                        <option value="12:00 PM">12:00 PM</option>
                        <option value="03:00 PM">03:00 PM</option>
                        <option value="06:00 PM">06:00 PM</option>
                    </select>
                </div>

                <button type="submit" class="btn-elite">Submit for Free Quote</button>
            </form>
            <div id="vSuccess" class="hidden text-center py-10">
                <h2 class="text-3xl font-black text-emerald-500 mb-4">TRANSIMITTED!</h2>
                <p class="font-bold uppercase text-xs">Your Tracking ID: <span id="vTid" class="text-blue-600"></span></p>
                <button onclick="location.reload()" class="mt-8 underline text-[10px] font-black">NEW REQUEST</button>
            </div>
        </div>
    </section>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="bg-slate-950 p-6 text-white flex justify-between items-center">
                <div><h4 class="font-black text-xs uppercase">Corporate Chat</h4><p class="text-[9px] text-blue-400 font-bold">Agent-786 Status: Online</p></div>
                <button onclick="toggleChat()">✕</button>
            </div>
            <div id="chat-feed">
                <div class="bubble bubble-admin">Welcome! 👋 I am the U.S. Home Improvement Bot. How can I help you today?</div>
                <div id="bot-options" class="flex flex-col gap-2">
                    <div class="chat-bot-option" onclick="botHelp('pricing')">Estimate Pricing?</div>
                    <div class="chat-bot-option" onclick="botHelp('areas')">Service Areas?</div>
                    <div class="chat-bot-option" onclick="requestLive()" style="border-color: red; color: red;">Connect to Live Agent</div>
                </div>
            </div>
            <div class="p-4 border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="Type message..." class="w-full text-xs outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full text-white shadow-2xl z-[8500]">💬</button>
    </div>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center border-b pb-8 mb-12">
                <h3 class="text-3xl font-black italic uppercase">Master Dispatch Hub</h3>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-6 py-2 rounded-full text-[10px] font-bold">CLOSE</button>
            </div>
            
            <div id="authBox" class="text-center py-20">
                <input type="password" id="pin" class="input-elite max-w-xs text-center text-2xl mb-6" placeholder="PIN">
                <br><button onclick="unlock()" class="btn-elite max-w-xs">LOGIN</button>
            </div>

            <div id="hubData" class="hidden grid lg:grid-cols-2 gap-12">
                <div id="adminLeads" class="space-y-6"></div>
                <div>
                    <h4 class="font-black uppercase mb-6">Live Chat Signals</h4>
                    <div id="adminChats" class="space-y-4"></div>
                    <div id="adminReplyArea" class="hidden mt-8 p-6 bg-slate-50 rounded-3xl border">
                        <p class="text-[10px] font-black text-blue-600 mb-4">REPLYING TO: <span id="targetUser"></span></p>
                        <input type="text" id="replyText" class="input-elite mb-4" placeholder="Type reply...">
                        <div class="flex gap-4">
                            <button onclick="sendReply()" class="btn-elite text-xs">Send Reply</button>
                            <button onclick="clearChat()" class="bg-red-500 text-white px-6 rounded-2xl text-[10px] font-bold">CLEAR CHAT</button>
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
        const userId = "CID-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const w = document.getElementById('chat-window'); w.style.display = w.style.display === 'flex' ? 'none' : 'flex'; }
        function checkWindows() { document.getElementById('winBox').classList.toggle('hidden', document.getElementById('vSvc').value !== 'Windows'); }

        // CHAT BOT & LIVE SYSTEM
        function botHelp(type) {
            const f = document.getElementById('chat-feed');
            let msg = type === 'pricing' ? "Our estimates are 100% Free at no cost." : "We serve all 50 US states.";
            f.innerHTML += `<div class="bubble bubble-user">${type === 'pricing' ? 'Price Info' : 'Area Info'}</div>`;
            setTimeout(() => { f.innerHTML += `<div class="bubble bubble-admin">${msg}</div>`; f.scrollTop = f.scrollHeight; }, 500);
        }

        function requestLive() {
            db.ref('chats/' + userId).push({ text: "🚨 LIVE AGENT REQUESTED", type: 'user' });
            document.getElementById('bot-options').classList.add('hidden');
            document.getElementById('chat-feed').innerHTML += `<div class="bubble bubble-admin" style="background:#fffbeb">Connecting to Agent-786...</div>`;
        }

        function sendMsg() {
            const t = document.getElementById('chat-input').value; if(!t) return;
            db.ref('chats/' + userId).push({ text: t, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + userId).on('value', snap => {
            const m = snap.val(); let h = '';
            for(let k in m) h += `<div class="bubble ${m[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${m[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // FORM SUBMISSION
        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-HUB-" + Math.floor(100000 + Math.random() * 900000);
            const data = { 
                tid, name: document.getElementById('vName').value, email: document.getElementById('vEmail').value,
                phone: document.getElementById('vPhone').value, addr: document.getElementById('vAddr').value,
                svc: document.getElementById('vSvc').value, win: document.getElementById('vWinCount').value || 'N/A',
                owner: document.getElementById('vOwner').value, ready: document.getElementById('vReady').value,
                zip: document.getElementById('vZip').value, credit: document.getElementById('vCredit').value,
                appt: document.getElementById('vDate').value + " @ " + document.getElementById('vTime').value
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('masterForm').classList.add('hidden');
                document.getElementById('vSuccess').classList.remove('hidden');
                document.getElementById('vTid').innerText = tid;
            });
        });

        // ADMIN HUB LOGIC
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        let activeAdminChat = '';
        function syncAdmin() {
            db.ref('leads').on('value', s => {
                let h = '<h4 class="font-black uppercase mb-6">New Qualified Leads</h4>';
                s.forEach(l => { const v = l.val(); h += `<div class="p-6 bg-slate-50 border rounded-3xl mb-4 relative"><span class="absolute top-4 right-4 bg-slate-900 text-white text-[8px] p-1 rounded">${v.tid}</span><h5 class="font-black">${v.name}</h5><p class="text-[10px] font-bold text-blue-600">${v.svc} | ${v.addr}</p><p class="text-[9px] uppercase mt-2">📞 ${v.phone} | Credit: ${v.credit} | Appt: ${v.appt}</p></div>`; });
                document.getElementById('adminLeads').innerHTML = h;
            });
            db.ref('chats').on('value', s => {
                let h = '';
                s.forEach(c => { 
                    const uid = c.key; const last = Object.values(c.val()).pop().text;
                    h += `<div onclick="openAdminReply('${uid}')" class="p-4 bg-white border-2 rounded-2xl cursor-pointer hover:border-blue-500"><p class="text-[9px] font-black">${uid}</p><p class="text-[11px] font-bold truncate">"${last}"</p></div>`;
                });
                document.getElementById('adminChats').innerHTML = h;
            });
        }

        function openAdminReply(uid) { activeAdminChat = uid; document.getElementById('adminReplyArea').classList.remove('hidden'); document.getElementById('targetUser').innerText = uid; }
        function sendReply() {
            const t = document.getElementById('replyText').value; if(!t) return;
            db.ref('chats/' + activeAdminChat).push({ text: t, type: 'admin' });
            document.getElementById('replyText').value = '';
        }
        function clearChat() { if(confirm('Erase chat history?')) { db.ref('chats/' + activeAdminChat).remove(); document.getElementById('adminReplyArea').classList.add('hidden'); } }
    </script>
</body>
</html>
