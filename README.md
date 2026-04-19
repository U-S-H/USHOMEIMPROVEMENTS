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
        
        .hero-v3 { background: linear-gradient(rgba(15, 23, 42, 0.92), rgba(15, 23, 42, 0.85)), url('https://images.unsplash.com/photo-1513584684374-8bdb7489feef?auto=format&fit=crop&w=2000'); background-size: cover; background-position: center; }
        .input-elite { width: 100%; padding: 18px; border: 2px solid #e2e8f0; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: white; color: #0f172a; font-size: 14px; }
        .input-elite:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 22px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; transition: 0.3s; box-shadow: 0 15px 30px rgba(37, 99, 235, 0.2); width: 100%; }

        /* CHAT SYSTEM */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #fdfdfd; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }

        /* ADMIN CARDS */
        .lead-card { background: white; border: 2px solid #f1f5f9; border-radius: 35px; padding: 25px; margin-bottom: 20px; position: relative; }
        .stat-box { background: #f8fafc; border: 1px solid #e2e8f0; border-radius: 20px; padding: 15px; text-align: center; }
        .reply-box { background: #0f172a; border-radius: 25px; padding: 20px; color: white; margin-top: 20px; border: 2px solid #2563eb; }
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

    <section id="home" class="page-section active hero-v3 py-48 text-center text-white">
        <h1 class="text-6xl md:text-8xl font-black uppercase italic mb-8 tracking-tighter">Elite <span class="text-blue-500">Service</span>.</h1>
        <p class="max-w-xl mx-auto font-bold uppercase tracking-[0.4em] text-slate-300 text-[10px] mb-12">Authorized Property Evaluations & National Logistics.</p>
        <button onclick="showPage('form')" class="btn-master max-w-[300px]">Start Free Survey</button>
    </section>

    <section id="form" class="page-section py-20 px-6">
        <div class="max-w-3xl mx-auto bg-white p-12 rounded-[50px] shadow-2xl border">
            <form id="v3Form" class="space-y-6">
                <h3 class="text-xl font-black uppercase italic text-slate-900 border-b pb-4 mb-6">Site Qualification</h3>
                <div class="grid md:grid-cols-2 gap-6">
                    <input type="text" id="vName" placeholder="Full Legal Name" class="input-elite" required>
                    <input type="tel" id="vPhone" placeholder="Phone Number" class="input-elite" required>
                </div>
                <div class="grid md:grid-cols-2 gap-6">
                    <select id="vSvc" class="input-elite" required>
                        <option value="">Select Service</option>
                        <option value="Windows">Windows</option>
                        <option value="Roofing">Roofing</option>
                        <option value="Solar">Solar</option>
                    </select>
                    <select id="vCredit" class="input-elite" required>
                        <option value="">Credit Score</option>
                        <option value="720+">720+</option>
                        <option value="660-719">660-719</option>
                        <option value="Below 660">Below 660</option>
                    </select>
                </div>
                <input type="text" id="vAddr" placeholder="Physical Address" class="input-elite" required>
                <div class="grid md:grid-cols-2 gap-6 mb-10">
                    <input type="date" id="vDate" class="input-elite" required>
                    <select id="vTime" class="input-elite" required>
                        <option value="Morning">Morning</option>
                        <option value="Afternoon">Afternoon</option>
                    </select>
                </div>
                <button type="submit" class="btn-master">Transmit To Dispatch</button>
            </form>
            <div id="vSuccess" class="hidden text-center py-10">
                <h2 class="text-3xl font-black text-blue-600 mb-4">AUTHORIZED!</h2>
                <button onclick="location.reload()" class="underline text-[10px] font-black uppercase">New Survey</button>
            </div>
        </div>
    </section>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header bg-slate-900 p-6 text-white flex justify-between">
                <span class="font-black text-[11px] uppercase">Senior Support</span>
                <button onclick="toggleChat()">✕</button>
            </div>
            <div id="chat-feed"></div>
            <div id="bot-persistent-options" class="p-4 bg-slate-50 flex flex-col gap-2">
                <div class="border-2 border-blue-600 text-blue-600 p-2 rounded-full text-[10px] font-black text-center cursor-pointer" onclick="botAsk('price')">Free Estimate?</div>
                <div class="border-2 border-red-500 text-red-500 p-2 rounded-full text-[10px] font-black text-center cursor-pointer" onclick="requestLive()">🚨 Live Agent</div>
            </div>
            <div class="p-5 border-t bg-white flex gap-3">
                <input type="text" id="chat-input" placeholder="Type..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[8500]">💬</button>
    </div>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b-2 pb-8">
                <div>
                    <h3 class="text-3xl font-black uppercase italic">Master <span class="text-blue-600">Terminal</span></h3>
                    <p class="text-[10px] font-bold text-slate-400 mt-1">USA NATIONAL LEAD GENERATION HUB</p>
                </div>
                <div class="flex gap-4">
                    <button onclick="exportExcel()" class="bg-emerald-500 text-white px-6 py-3 rounded-xl text-[10px] font-black">DOWNLOAD EXCEL</button>
                    <button onclick="closeAdmin()" class="bg-red-500 text-white px-8 py-3 rounded-xl text-[10px] font-black">EXIT</button>
                </div>
            </div>

            <div id="authBox" class="text-center py-32"><input type="password" id="pin" class="input-elite max-w-[300px] text-center text-3xl mb-6 shadow-xl" placeholder="••••"><br><button onclick="unlock()" class="btn-master max-w-[300px]">Authorize</button></div>
            
            <div id="hubData" class="hidden">
                <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-12">
                    <div class="stat-box">
                        <p class="text-[9px] font-black text-slate-400 uppercase">Total Dispatches</p>
                        <p id="totalLeads" class="text-3xl font-black text-blue-600">0</p>
                    </div>
                    <div class="stat-box">
                        <p class="text-[9px] font-black text-slate-400 uppercase">Filter Service</p>
                        <select onchange="filterLeads(this.value)" class="text-[10px] font-bold bg-transparent border-none outline-none text-center w-full">
                            <option value="all">All Services</option>
                            <option value="Windows">Windows</option>
                            <option value="Roofing">Roofing</option>
                            <option value="Solar">Solar</option>
                        </select>
                    </div>
                </div>

                <div class="grid lg:grid-cols-3 gap-12">
                    <div class="lg:col-span-2 space-y-6" id="adminLeads"></div>
                    <div>
                        <h5 class="font-black uppercase text-xs text-slate-400 mb-8 italic tracking-widest">Active Signals</h5>
                        <div id="adminChats" class="space-y-4"></div>
                        <div id="adminReplyArea" class="hidden reply-box shadow-2xl">
                            <p class="text-[9px] font-black text-blue-400 uppercase mb-4">Reply to: <span id="targetId" class="text-white"></span></p>
                            <input type="text" id="replyText" placeholder="Enter official response..." class="w-full bg-slate-800 border-none p-4 rounded-xl text-xs font-bold text-white mb-4 outline-none">
                            <button onclick="sendReply()" class="btn-master py-3 text-[10px]">Transmit Message</button>
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
        const cid = "US-USER-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const w = document.getElementById('chat-window'); w.style.display = w.style.display === 'flex' ? 'none' : 'flex'; }

        // CHAT LOGIC
        function botAsk(t) {
            const feed = document.getElementById('chat-feed');
            feed.innerHTML += `<div class="bubble bubble-user">${t} query</div>`;
            setTimeout(() => { feed.innerHTML += `<div class="bubble bubble-admin">All site evaluations are 100% Free.</div>`; feed.scrollTop = feed.scrollHeight; }, 500);
        }

        function requestLive() {
            db.ref('chats/' + cid).push({ text: "🚨 LIVE AGENT REQUESTED", type: 'user' });
            document.getElementById('bot-persistent-options').classList.add('hidden');
        }

        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + cid).push({ text: txt, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + cid).on('value', snap => {
            let h = `<div class="bubble bubble-admin">Welcome to U.S. Dispatch Hub. How can we help?</div>`;
            snap.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // FORM
        document.getElementById('v3Form').onsubmit = (e) => {
            e.preventDefault();
            const data = {
                name: document.getElementById('vName').value, phone: document.getElementById('vPhone').value,
                svc: document.getElementById('vSvc').value, credit: document.getElementById('vCredit').value,
                addr: document.getElementById('vAddr').value, appt: document.getElementById('vDate').value + " | " + document.getElementById('vTime').value,
                ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('v3Form').classList.add('hidden');
                document.getElementById('vSuccess').classList.remove('hidden');
            });
        };

        // ADMIN TERMINAL - ADVANCED
        let taps = 0, activeId = '';
        function handleAdminTap() { taps++; if(taps>=5) document.getElementById('adminHub').classList.remove('hidden'); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                let h = '', count = 0;
                snap.forEach(l => {
                    const v = l.val(); const k = l.key; count++;
                    h += `<div class="lead-card" data-svc="${v.svc}">
                        <div class="flex justify-between items-start border-b pb-4 mb-4">
                            <h4 class="text-xl font-black italic text-blue-600 uppercase">${v.name}</h4>
                            <span class="bg-blue-600 text-white text-[8px] px-3 py-1 rounded-full font-black">NEW DISPATCH</span>
                        </div>
                        <div class="grid grid-cols-2 gap-4 text-[10px] font-bold uppercase tracking-tighter">
                            <p class="text-slate-400">Service: <span class="text-slate-900">${v.svc}</span></p>
                            <p class="text-slate-400">Credit: <span class="text-slate-900">${v.credit}</span></p>
                            <p class="text-slate-400">Phone: <span class="text-slate-900">${v.phone}</span></p>
                            <p class="text-slate-400">Time: <span class="text-emerald-600">${v.appt}</span></p>
                            <p class="text-slate-400 col-span-2 border-t pt-2">Address: <span class="text-slate-900">${v.addr}</span></p>
                        </div>
                        <button onclick="del('${k}')" class="text-red-500 font-black text-[9px] uppercase mt-6 hover:underline">Permanently Erase Lead</button>
                    </div>`;
                });
                document.getElementById('adminLeads').innerHTML = h || 'No leads.';
                document.getElementById('totalLeads').innerText = count;
            });

            db.ref('chats').on('value', snap => {
                let h = '';
                snap.forEach(c => {
                    const uid = c.key; const last = Object.values(c.val()).pop();
                    h += `<div onclick="openReply('${uid}')" class="p-4 bg-white border-2 border-slate-50 rounded-2xl cursor-pointer hover:border-blue-500">
                        <p class="text-[8px] font-black text-blue-600 uppercase">${uid}</p>
                        <p class="text-[11px] font-bold italic truncate">"${last.text}"</p>
                    </div>`;
                });
                document.getElementById('adminChats').innerHTML = h || 'No signals.';
            });
        }

        function del(k) { if(confirm('Erase lead?')) db.ref('leads/' + k).remove(); }
        function openReply(id) { activeId = id; document.getElementById('adminReplyArea').classList.remove('hidden'); document.getElementById('targetId').innerText = id; }
        function sendReply() { const t = document.getElementById('replyText').value; if(!t) return; db.ref('chats/' + activeId).push({ text: t, type: 'admin' }); document.getElementById('replyText').value = ''; }
        
        function filterLeads(svc) {
            document.querySelectorAll('.lead-card').forEach(c => {
                c.style.display = (svc === 'all' || c.getAttribute('data-svc') === svc) ? 'block' : 'none';
            });
        }

        function exportExcel() {
            db.ref('leads').once('value', snap => {
                const data = Object.values(snap.val() || {});
                const ws = XLSX.utils.json_to_sheet(data);
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "Leads");
                XLSX.writeFile(wb, "US_Home_Improvements_Leads.xlsx");
            });
        }
    </script>
</body>
</html>
