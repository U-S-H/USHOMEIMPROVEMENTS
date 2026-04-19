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

        /* CHAT SYSTEM */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 30px; box-shadow: 0 30px 60px -12px rgba(0,0,0,0.25); display: none; flex-direction: column; z-index: 6000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 22px; color: white; display: flex; align-items: center; gap: 12px; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); }

        /* ADMIN CARDS */
        .lead-card { background: white; border: 2px solid #f1f5f9; border-radius: 35px; padding: 25px; position: relative; transition: 0.3s; }
        .info-label { font-size: 9px; font-weight: 800; color: #64748b; text-transform: uppercase; margin-bottom: 2px; }
        .info-val { font-size: 12px; font-weight: 700; color: #0f172a; }
        .reply-terminal { background: #0f172a; border-radius: 30px; padding: 25px; color: white; border: 3px solid #2563eb; }
    </style>
</head>
<body>

    <nav class="glass-blur sticky top-0 z-[5000] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <div onclick="handleAdminTap()" class="h-12 w-12 bg-slate-900 rounded-xl flex items-center justify-center text-white font-black cursor-pointer shadow-lg">US</div>
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
                <div class="w-2 h-2 bg-emerald-500 rounded-full"></div>
                <h4 class="font-black uppercase text-[10px]">Senior Dispatch Support</h4>
                <button onclick="toggleChat()" class="ml-auto text-xs opacity-50">✕</button>
            </div>
            <div id="chat-feed"></div>
            <div id="bot-persistent-options" class="p-4 bg-slate-50 flex flex-col gap-2 border-t">
                <div class="border-2 border-blue-600 text-blue-600 p-2 rounded-full text-[9px] font-black text-center cursor-pointer" onclick="botReply('price')">Free Estimate Cost?</div>
                <div class="border-2 border-red-500 text-red-500 p-2 rounded-full text-[9px] font-black text-center cursor-pointer" onclick="requestLiveAgent()">🚨 Talk to Live Agent</div>
            </div>
            <div class="p-4 border-t bg-white flex gap-2">
                <input type="text" id="chat-input" placeholder="Type here..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-[10px] uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-14 h-14 bg-slate-900 rounded-full shadow-2xl flex items-center justify-center text-white text-xl z-[5500]">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-v3 py-48 px-6 text-center text-white">
            <h1 class="text-6xl md:text-8xl font-black uppercase italic mb-8">The Elite <br><span class="text-blue-500">Standard</span>.</h1>
            <p class="max-w-xl mx-auto font-bold uppercase tracking-[0.4em] text-slate-300 text-[10px] mb-12">Authorized Property Evaluations & National Logistics.</p>
            <button onclick="showPage('form')" class="btn-elite max-w-[320px]">Initiate Project Survey</button>
        </header>
    </section>

    <section id="form" class="page-section py-20 bg-white px-6">
        <div class="max-w-3xl mx-auto bg-white p-12 rounded-[48px] shadow-2xl border">
            <form id="v3Form">
                <h3 class="text-2xl font-black uppercase italic text-slate-900 border-b pb-4 mb-10">Site Authorization</h3>
                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro" required>
                    <input type="tel" id="vPhone" placeholder="Primary Phone" class="input-pro" required>
                </div>
                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <select id="vSvc" class="input-pro" required>
                        <option value="">Select Service</option>
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
                        <option value="Morning">Morning (9AM-12PM)</option>
                        <option value="Afternoon">Afternoon (12PM-4PM)</option>
                        <option value="Evening">Evening (4PM-7PM)</option>
                    </select>
                </div>
                <button type="submit" class="btn-elite">Authorize & Transmit</button>
            </form>

            <div id="vReceipt" class="hidden text-center py-10 animate-pulse">
                <h3 class="text-4xl font-black text-blue-600 mb-4 uppercase italic">Authorized</h3>
                <p class="text-xs font-bold text-slate-500 uppercase">Case ID: <span id="displayTid" class="text-slate-900 font-black"></span></p>
                <div class="mt-8 p-6 bg-slate-50 rounded-2xl border-2 border-dashed border-slate-200">
                    <p class="text-[11px] font-bold text-slate-600">Verification Pending. Our Senior Dispatcher will call you shortly.</p>
                </div>
                <button onclick="location.reload()" class="underline text-[10px] font-black uppercase mt-12 block mx-auto">New Project Request</button>
            </div>

            <div class="flex justify-center gap-6 opacity-40 mt-12 border-t pt-8">
                <img src="https://img.icons8.com/color/48/google-logo.png" class="h-6">
                <img src="https://img.icons8.com/color/48/bbb.png" class="h-6">
                <p class="text-[9px] font-black self-center uppercase">Licensed National Network</p>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-8 md:p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-12 border-b-2 pb-8 gap-6">
                <div>
                    <h3 class="text-3xl font-black uppercase italic">Master <span class="text-blue-600">Terminal</span></h3>
                    <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mt-1">USA National Lead & Dispatch Center</p>
                </div>
                <div class="flex gap-4">
                    <button onclick="exportToExcel()" class="bg-emerald-600 text-white px-6 py-3 rounded-xl text-[10px] font-black">EXPORT EXCEL</button>
                    <button onclick="closeAdmin()" class="bg-red-500 text-white px-8 py-3 rounded-xl text-[10px] font-black">EXIT</button>
                </div>
            </div>
            
            <div id="authBox" class="text-center py-20">
                <input type="password" id="pin" class="input-pro max-w-[300px] text-center text-3xl mb-6 shadow-xl" placeholder="••••">
                <br><button onclick="unlock()" class="btn-elite max-w-[300px]">Access Secure Node</button>
            </div>
            
            <div id="hubData" class="hidden grid lg:grid-cols-3 gap-12">
                <div class="lg:col-span-2">
                    <div class="flex justify-between items-center mb-8">
                        <h5 class="font-black uppercase text-xs text-slate-400 italic">Dispatches Queue</h5>
                        <select onchange="filterAdmin(this.value)" class="text-[10px] border p-2 rounded-xl font-bold">
                            <option value="all">All Portfolio</option>
                            <option value="Windows">Windows</option>
                            <option value="Roofing">Roofing</option>
                            <option value="Solar">Solar</option>
                        </select>
                    </div>
                    <div id="adminLeads" class="space-y-6"></div>
                </div>
                
                <div>
                    <h5 class="font-black uppercase text-xs text-slate-400 mb-8 italic">Signal Monitor</h5>
                    <div id="adminChats" class="space-y-4"></div>
                    
                    <div id="replyArea" class="hidden mt-8 reply-terminal shadow-2xl">
                        <div class="flex justify-between items-center mb-4">
                            <p class="text-[9px] font-black text-blue-400 uppercase tracking-widest">Reply To: <span id="targetId" class="text-white"></span></p>
                            <button onclick="clearChatHistory()" class="text-red-400 font-black text-[9px] uppercase">Erase Signal</button>
                        </div>
                        <textarea id="adminReplyText" rows="3" class="w-full bg-slate-800 border-none p-4 rounded-2xl text-xs font-bold text-white mb-4 outline-none resize-none" placeholder="Enter transmission..."></textarea>
                        <button onclick="sendAdminReply()" class="btn-elite py-4 text-[10px]">Transmit Signal</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // CONFIG
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
        const cid = "SIG-" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }

        // LEAD SCORING LOGIC
        function getScoreBadge(credit, svc) {
            if (credit === "720+" && (svc === "Solar" || svc === "Roofing")) {
                return '<span class="bg-red-600 text-white px-3 py-1 rounded-full animate-pulse text-[8px] font-black uppercase">🔥 High Value</span>';
            }
            return '<span class="bg-blue-100 text-blue-600 px-3 py-1 rounded-full text-[8px] font-black uppercase">Standard</span>';
        }

        // CHATBOT
        function botReply(t) {
            const feed = document.getElementById('chat-feed');
            feed.innerHTML += `<div class="bubble bubble-user">${t} query</div>`;
            setTimeout(() => { 
                feed.innerHTML += `<div class="bubble bubble-admin">Site evaluations are 100% Free of charge nationwide.</div>`; 
                feed.scrollTop = feed.scrollHeight; 
            }, 500);
        }

        function requestLiveAgent() {
            db.ref('chats/' + cid).push({ text: "🚨 LIVE AGENT REQUESTED", type: 'user', time: new Date().toLocaleTimeString() });
            document.getElementById('bot-persistent-options').classList.add('hidden');
        }

        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + cid).push({ text: txt, type: 'user', time: new Date().toLocaleTimeString() });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + cid).on('value', snap => {
            let h = `<div class="bubble bubble-admin">System Ready. How can we serve you today?</div>`;
            snap.forEach(m => { const v = m.val(); h += `<div class="bubble ${v.type==='user'?'bubble-user':'bubble-admin'}">${v.text}</div>`; });
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // SURVEY SUBMISSION
        document.getElementById('v3Form').onsubmit = (e) => {
            e.preventDefault();
            const tid = "US-" + Math.floor(100000 + Math.random() * 900000);
            const data = {
                tid: tid, name: document.getElementById('vName').value, phone: document.getElementById('vPhone').value,
                svc: document.getElementById('vSvc').value, credit: document.getElementById('vCredit').value,
                addr: document.getElementById('vAddr').value, appt: document.getElementById('vDate').value + " | " + document.getElementById('vTime').value,
                ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('v3Form').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('displayTid').innerText = tid;
            });
        };

        // MASTER ADMIN HUB
        let taps = 0, activeId = '';
        function handleAdminTap() { taps++; if(taps>=5) document.getElementById('adminHub').classList.remove('hidden'); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                let h = '';
                snap.forEach(l => {
                    const v = l.val(); const k = l.key;
                    h += `<div class="lead-card border-l-8 ${v.credit === '720+' ? 'border-red-500' : 'border-blue-500'}" data-svc="${v.svc}">
                        <div class="flex justify-between mb-4">
                            ${getScoreBadge(v.credit, v.svc)}
                            <span class="text-[9px] font-bold text-slate-400">ID: ${v.tid}</span>
                        </div>
                        <h4 class="text-xl font-black italic uppercase text-slate-900">${v.name}</h4>
                        <div class="grid grid-cols-2 gap-x-6 gap-y-4 mt-6">
                            <div><p class="info-label">Portfolio</p><p class="info-val">${v.svc}</p></div>
                            <div><p class="info-label">Phone</p><p class="info-val">📞 ${v.phone}</p></div>
                            <div><p class="info-label">Credit Profile</p><p class="info-val">${v.credit}</p></div>
                            <div><p class="info-label">Window</p><p class="info-val text-emerald-600">${v.appt}</p></div>
                            <div class="col-span-2 border-t pt-2"><p class="info-label">Property Address</p><p class="info-val">${v.addr}</p></div>
                        </div>
                        <div class="flex gap-4 mt-6 border-t pt-4">
                            <button onclick="del('leads/${k}')" class="text-red-500 font-black text-[9px] uppercase hover:underline">Erase Dispatch</button>
                            <a href="https://www.google.com/maps/search/${encodeURIComponent(v.addr)}" target="_blank" class="text-blue-600 font-black text-[9px] uppercase ml-auto hover:underline">Satellite View</a>
                        </div>
                    </div>`;
                });
                document.getElementById('adminLeads').innerHTML = h || 'No leads in queue.';
            });

            db.ref('chats').on('value', snap => {
                let h = '';
                snap.forEach(c => {
                    const uid = c.key; const last = Object.values(c.val()).pop();
                    h += `<div onclick="openReply('${uid}')" class="p-4 bg-white border-2 border-slate-50 rounded-2xl cursor-pointer hover:border-blue-600 shadow-sm transition">
                        <p class="text-[8px] font-black text-blue-600 uppercase">${uid}</p>
                        <p class="text-[11px] font-bold italic truncate">"${last.text}"</p>
                    </div>`;
                });
                document.getElementById('adminChats').innerHTML = h || 'Quiet signals.';
            });
        }

        function openReply(uid) { activeId = uid; document.getElementById('replyArea').classList.remove('hidden'); document.getElementById('targetId').innerText = uid; }
        
        function sendAdminReply() {
            const txt = document.getElementById('adminReplyText').value; if(!txt || !activeId) return;
            db.ref('chats/' + activeId).push({ text: txt, type: 'admin', time: new Date().toLocaleTimeString() });
            document.getElementById('adminReplyText').value = '';
        }

        function clearChatHistory() { if(confirm('Clear entire thread?')) db.ref('chats/' + activeId).remove(); }
        function del(path) { if(confirm('Erase data permanently?')) db.ref(path).remove(); }
        
        function filterAdmin(svc) {
            document.querySelectorAll('.lead-card').forEach(c => {
                c.style.display = (svc === 'all' || c.getAttribute('data-svc') === svc) ? 'block' : 'none';
            });
        }

        function exportToExcel() {
            db.ref('leads').once('value', snap => {
                const data = Object.values(snap.val() || {});
                const ws = XLSX.utils.json_to_sheet(data);
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "Leads");
                XLSX.writeFile(wb, "US_Home_Improvements_Data.xlsx");
            });
        }
    </script>
</body>
</html>
