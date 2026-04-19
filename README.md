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
        
        .hero-v3 { background: linear-gradient(rgba(15, 23, 42, 0.92), rgba(15, 23, 42, 0.85)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
        .glass-blur { background: rgba(255, 255, 255, 0.85); backdrop-filter: blur(20px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; outline: none; transition: 0.4s; font-size: 14px; background: #fff; }
        .input-pro:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px 32px; border-radius: 16px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; border: none; transition: 0.4s; box-shadow: 0 12px 24px rgba(37, 99, 235, 0.25); width: 100%; }

        .page-section { display: none; }
        .page-section.active { display: block; animation: contentFade 0.7s ease-out; }
        @keyframes contentFade { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        /* PERSISTENT CHAT SYSTEM */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 30px; box-shadow: 0 30px 60px -12px rgba(0,0,0,0.25); display: none; flex-direction: column; z-index: 6000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 22px; color: white; display: flex; align-items: center; gap: 12px; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); }
        .bot-opt { border: 2px solid #2563eb; color: #2563eb; padding: 8px; border-radius: 50px; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; background: white; transition: 0.3s; }
        .bot-opt:hover { background: #2563eb; color: white; }

        /* ADMIN LEAD CARDS - FULL DETAILS */
        .lead-card { background: #f8fafc; border: 2px solid #e2e8f0; border-radius: 35px; padding: 30px; position: relative; transition: 0.3s; }
        .lead-card:hover { border-color: #2563eb; transform: translateY(-5px); }
        .info-grid { display: grid; grid-cols: 2; gap: 10px; margin-top: 15px; border-top: 1px solid #e2e8f0; pt-15; }
        .info-item { font-size: 10px; font-weight: 700; color: #64748b; text-transform: uppercase; }
        .info-val { color: #0f172a; font-weight: 800; display: block; }
    </style>
</head>
<body>

    <nav class="glass-blur sticky top-0 z-[5000] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <img src="logo.png" onclick="handleAdminTap()" class="h-12 w-12 bg-white border-2 border-slate-50 rounded-2xl shadow-sm cursor-pointer" onerror="this.src='https://ui-avatars.com/api/?name=US&background=0f172a&color=fff'">
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic">Enterprise National Hub</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-full text-[10px] font-black uppercase">Get Quote</button>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="w-3 h-3 bg-emerald-500 rounded-full border-2 border-slate-900"></div>
                <h4 class="font-black uppercase text-[11px]">Senior Dispatch Support</h4>
                <button onclick="toggleChat()" class="ml-auto">✕</button>
            </div>
            <div id="chat-feed"></div>
            <div id="bot-persistent-options" class="p-4 bg-slate-50 flex flex-col gap-2 border-t">
                <div class="bot-opt" onclick="botReply('price')">Free Estimate Cost?</div>
                <div class="bot-opt" onclick="botReply('area')">Service Areas?</div>
                <div class="bot-opt" onclick="requestLiveAgent()" style="border-color:#ef4444; color:#ef4444;">🚨 Talk to Live Agent</div>
            </div>
            <div class="p-5 border-t bg-white flex gap-3">
                <input type="text" id="chat-input" placeholder="Type here..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[5500]">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-v3 py-48 px-6 text-center text-white">
            <h1 class="text-7xl font-black uppercase italic mb-8">The Elite <br><span class="text-blue-500">Standard</span>.</h1>
            <button onclick="showPage('form')" class="btn-elite max-w-[320px]">Initiate Project Survey</button>
        </header>
    </section>

    <section id="form" class="page-section py-20 bg-white px-6">
        <div class="max-w-3xl mx-auto bg-white p-12 rounded-[48px] shadow-2xl border">
            <form id="v3Form">
                <h3 class="text-2xl font-black uppercase italic text-slate-900 mb-10">Site Authorization</h3>
                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <input type="text" id="vName" placeholder="Full Name" class="input-pro" required>
                    <input type="tel" id="vPhone" placeholder="Primary Phone" class="input-pro" required>
                </div>
                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <select id="vSvc" class="input-pro" required>
                        <option value="">Portfolio</option>
                        <option value="Windows">Windows</option>
                        <option value="Roofing">Roofing</option>
                        <option value="Solar">Solar</option>
                    </select>
                    <select id="vCredit" class="input-pro" required>
                        <option value="">Credit Score</option>
                        <option value="720+">720+</option>
                        <option value="660-719">660-719</option>
                        <option value="Below 660">Below 660</option>
                    </select>
                </div>
                <input type="text" id="vAddr" placeholder="Physical Address" class="input-pro mb-6" required>
                <div class="grid md:grid-cols-2 gap-6 mb-10">
                    <input type="date" id="vDate" class="input-pro" required>
                    <select id="vTime" class="input-pro" required>
                        <option value="Morning">Morning</option>
                        <option value="Afternoon">Afternoon</option>
                    </select>
                </div>
                <button type="submit" class="btn-elite">Authorize & Transmit</button>
            </form>
            <div id="vReceipt" class="hidden text-center py-10">
                <h3 class="text-3xl font-black text-blue-600">SUBMITTED!</h3>
                <button onclick="location.reload()" class="underline text-[10px] font-black uppercase mt-4">New Lead</button>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b-2 pb-8">
                <h3 class="text-3xl font-black uppercase italic">Master <span class="text-blue-600">Terminal</span></h3>
                <button onclick="closeAdmin()" class="bg-red-500 text-white px-8 py-3 rounded-full text-[10px] font-black">EXIT</button>
            </div>
            
            <div id="authBox" class="text-center py-32"><input type="password" id="pin" class="input-pro max-w-[300px] text-center text-3xl mb-6 shadow-xl" placeholder="••••"><br><button onclick="unlock()" class="btn-elite max-w-[300px]">Authorize</button></div>
            
            <div id="hubData" class="hidden grid lg:grid-cols-3 gap-16">
                <div class="lg:col-span-2">
                    <h5 class="font-black uppercase text-xs text-slate-400 mb-8 italic tracking-widest">Authorized Dispatches</h5>
                    <div id="adminLeads" class="space-y-6"></div>
                </div>
                <div>
                    <h5 class="font-black uppercase text-xs text-slate-400 mb-8 italic tracking-widest">Active Chats</h5>
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

        // CHAT LOGIC
        function botReply(t) {
            let m = t === 'price' ? "All site assessments are 100% Free." : "We serve all 50 states nationwide.";
            const feed = document.getElementById('chat-feed');
            feed.innerHTML += `<div class="bubble bubble-user">${t} info request</div>`;
            setTimeout(() => { feed.innerHTML += `<div class="bubble bubble-admin">${m}</div>`; feed.scrollTop = feed.scrollHeight; }, 500);
        }

        function requestLiveAgent() {
            db.ref('chats/' + userId).push({ text: "🚨 LIVE AGENT REQUESTED", type: 'user' });
            document.getElementById('bot-persistent-options').style.display = 'none';
        }

        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + userId).push({ text: txt, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + userId).on('value', snap => {
            const msgs = snap.val(); let h = `<div class="bubble bubble-admin">Welcome! How can I help you today?</div>`;
            for(let k in msgs) h += `<div class="bubble ${msgs[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${msgs[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // FORM SUBMISSION
        document.getElementById('v3Form').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                tid: "US-" + Math.floor(100000 + Math.random() * 900000),
                name: document.getElementById('vName').value, phone: document.getElementById('vPhone').value,
                svc: document.getElementById('vSvc').value, credit: document.getElementById('vCredit').value,
                addr: document.getElementById('vAddr').value, appt: document.getElementById('vDate').value + " @ " + document.getElementById('vTime').value
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('v3Form').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
            });
        });

        // ADMIN TERMINAL - FULL DETAILS
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) {
                    const l = leads[k];
                    h += `<div class="lead-card">
                        <span class="absolute top-4 right-4 text-[8px] font-black bg-slate-900 text-white px-3 py-1 rounded-full">${l.tid}</span>
                        <h4 class="text-xl font-black italic text-blue-600">${l.name}</h4>
                        <div class="info-grid mt-4 grid grid-cols-2 gap-y-4">
                            <div><span class="info-item">Phone:</span><span class="info-val">${l.phone}</span></div>
                            <div><span class="info-item">Service:</span><span class="info-val">${l.svc}</span></div>
                            <div><span class="info-item">Credit:</span><span class="info-val">${l.credit}</span></div>
                            <div><span class="info-item">Appointment:</span><span class="info-val text-emerald-600">${l.appt}</span></div>
                            <div class="col-span-2"><span class="info-item">Full Address:</span><span class="info-val">${l.addr}</span></div>
                        </div>
                        <button onclick="delLead('${k}')" class="mt-6 w-full text-[9px] font-black text-red-500 uppercase border-t pt-4">Permanently Delete Lead</button>
                    </div>`;
                }
                document.getElementById('adminLeads').innerHTML = h || 'No dispatches found.';
            });

            db.ref('chats').on('value', snap => {
                const chats = snap.val(); let h = '';
                for(let uid in chats) {
                    const last = Object.values(chats[uid]).pop();
                    h += `<div class="p-4 bg-white border rounded-2xl shadow-sm"><p class="text-[8px] font-black text-blue-600">${uid}</p><p class="text-[11px] font-bold italic">"${last.text}"</p></div>`;
                }
                document.getElementById('adminChats').innerHTML = h || 'No active chats.';
            });
        }

        function delLead(k) { if(confirm('Erase this lead permanently?')) db.ref('leads/' + k).remove(); }
    </script>
</body>
</html>
