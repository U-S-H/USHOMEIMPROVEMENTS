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
        .step-pill { width: 100%; height: 6px; background: #e2e8f0; border-radius: 10px; position: relative; overflow: hidden; }
        .step-fill { height: 100%; background: var(--accent); width: 0%; transition: 0.6s cubic-bezier(0.22, 1, 0.36, 1); }
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 30px; box-shadow: 0 30px 60px -12px rgba(0,0,0,0.25); display: none; flex-direction: column; z-index: 6000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 22px; color: white; display: flex; align-items: center; gap: 12px; }
        .agent-id { font-size: 9px; font-weight: 800; color: #3b82f6; text-transform: uppercase; letter-spacing: 1px; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; line-height: 1.5; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); }
        .badge-premium { background: #eff6ff; color: #2563eb; padding: 4px 12px; border-radius: 50px; font-size: 9px; font-weight: 800; text-transform: uppercase; border: 1px solid #dbeafe; }
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
            <button onclick="showPage('legal')">Security</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-full shadow-lg shadow-blue-100">Get Quote</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="w-3 h-3 bg-emerald-500 rounded-full border-2 border-slate-900"></div>
                <div><p class="agent-id">Agent Connection: Verified</p><h4 class="font-black uppercase text-[11px]">Senior Dispatch Support</h4></div>
                <button onclick="toggleChat()" class="ml-auto">✕</button>
            </div>
            <div id="chat-feed">
                <div class="bubble bubble-admin">Welcome to U.S. Home Improvement Support. <br><br>I am Agent-786. How may I assist you with your property survey today?</div>
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
            <span class="badge-premium mb-8 inline-block">Authorized 50-State Network</span>
            <h1 class="text-6xl md:text-9xl font-black uppercase italic tracking-tighter mb-12">The Elite <br><span class="text-blue-500">Standard</span>.</h1>
            <p class="max-w-xl mx-auto text-blue-100 font-bold text-xs uppercase tracking-[0.5em] mb-16">Certified Site Inspections & National Logistics.</p>
            <button onclick="showPage('form')" class="btn-elite max-w-[320px]">Initiate Project Survey</button>
        </header>
        <div class="max-w-7xl mx-auto px-8 py-32 grid md:grid-cols-3 gap-16 text-center font-black uppercase tracking-widest text-slate-400 text-[10px]">
            <div><h3 class="text-4xl text-blue-900 mb-4 italic">50+</h3> States Covered</div>
            <div><h3 class="text-4xl text-blue-900 mb-4 italic">A+</h3> BBB Rated Network</div>
            <div><h3 class="text-4xl text-blue-900 mb-4 italic">100%</h3> Secure Dispatch</div>
        </div>
    </section>

    <section id="form" class="page-section py-20 bg-white">
        <div class="max-w-3xl mx-auto px-6">
            <div class="mb-12">
                <div class="flex justify-between text-[10px] font-black uppercase text-slate-400 mb-4 italic"><span>Survey Progress</span> <span id="pcent">0%</span></div>
                <div class="step-pill"><div id="pBar" class="step-fill"></div></div>
            </div>
            <div class="bg-white p-12 rounded-[48px] shadow-2xl border border-slate-50 relative overflow-hidden">
                <form id="masterForm">
                    <h3 class="text-2xl font-black uppercase italic text-slate-900 mb-10">Site Authorization Terminal</h3>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro" required>
                        <input type="email" id="vEmail" placeholder="Email Address" class="input-pro" required>
                    </div>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="tel" id="vPhone" placeholder="Primary Phone" class="input-pro" required>
                        <select id="vSvc" class="input-pro" required>
                            <option value="">Select Service Portfolio</option>
                            <option value="Garage">Garage Door Systems</option>
                            <option value="Windows">Windows Replacement</option>
                            <option value="Roofing">Roofing Installation</option>
                            <option value="Solar">Solar Power Matrix</option>
                            <option value="Siding">Siding Repair/Replacement</option>
                            <option value="Kitchen">Kitchen Remodeling</option>
                            <option value="Bathroom">Bathroom Remodeling</option>
                            <option value="HVAC">HVAC (Heating & Air)</option>
                            <option value="Gutters">Seamless Gutter System</option>
                            <option value="Flooring">Flooring (Hardwood/Tile)</option>
                            <option value="Painting">Painting (In/Ext)</option>
                            <option value="Plumbing">Main Line Plumbing</option>
                        </select>
                    </div>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="number" id="vCount" placeholder="Est. Quantity (e.g. 10 windows)" class="input-pro">
                        <select id="vCredit" class="input-pro" required>
                            <option value="">Estimated Credit Score</option>
                            <option value="Excellent (720+)">Excellent (720+)</option>
                            <option value="Good (660-719)">Good (660-719)</option>
                            <option value="Fair (Below 660)">Below 660 (Fair)</option>
                        </select>
                    </div>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="date" id="vDate" class="input-pro" required>
                        <select id="vTime" class="input-pro" required>
                            <option value="">Preferred Time Slot</option>
                            <option value="10:00 AM">10:00 AM</option>
                            <option value="12:00 PM">12:00 PM</option>
                            <option value="03:00 PM">03:00 PM</option>
                            <option value="05:00 PM">05:00 PM</option>
                        </select>
                    </div>
                    <input type="text" id="vAddr" placeholder="Physical Property Address" class="input-pro mb-10" required>
                    <button type="submit" class="btn-elite">Authorize & Transmit</button>
                </form>
                <div id="vReceipt" class="hidden text-center py-10">
                    <h3 class="text-3xl font-black uppercase italic text-slate-900 mb-8">Transmission Success</h3>
                    <div id="receipt-data" class="bg-slate-950 text-white p-10 rounded-[35px] text-left text-[11px] font-bold uppercase space-y-4 border-4 border-blue-600 shadow-2xl">
                        </div>
                    <button onclick="location.reload()" class="mt-8 text-blue-600 font-black text-[10px] uppercase underline italic">Initiate New Survey</button>
                </div>
            </div>
        </div>
    </section>

    <section id="faq" class="page-section py-24 bg-slate-50 px-8">
        <div class="max-w-4xl mx-auto text-center">
            <h2 class="text-4xl font-black uppercase italic mb-16">Service Intelligence</h2>
            <div class="space-y-6 text-left">
                <div class="bg-white p-8 rounded-3xl border shadow-sm">
                    <h4 class="font-black uppercase text-xs mb-3 text-blue-600 italic">How is the estimate calculated?</h4>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Our hub transmits your data to a local certified inspector who provides a technical quote after a site visit.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="legal" class="page-section py-24 px-8">
        <div class="max-w-4xl mx-auto bg-slate-900 text-white p-16 rounded-[48px] border-t-8 border-blue-600">
            <h3 class="text-3xl font-black uppercase italic mb-8">Security Compliance</h3>
            <p class="text-[10px] font-bold text-slate-400 uppercase leading-loose">All transmissions are encrypted via 256-bit SSL protocol. We adhere to national data protection standards for home improvement logistics.</p>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-12 border-b pb-8">
                <div><h3 class="text-3xl font-black uppercase italic">Master Terminal</h3><p class="text-[9px] font-black text-slate-400 uppercase">Enterprise Dispatch Management</p></div>
                <div class="flex gap-4">
                    <button onclick="exportToExcel()" class="bg-emerald-50 text-emerald-600 px-8 py-3 rounded-full font-black text-[10px] uppercase">Export Leads</button>
                    <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-8 py-3 rounded-full font-black text-[10px] uppercase">Exit</button>
                </div>
            </div>
            <div id="authBox" class="text-center py-32">
                <input type="password" id="pin" class="input-pro max-w-[300px] text-center text-3xl mb-6 shadow-xl" placeholder="••••">
                <br><button onclick="unlock()" class="btn-elite max-w-[300px]">Authorize Access</button>
            </div>
            <div id="hubData" class="hidden grid lg:grid-cols-3 gap-16">
                <div class="lg:col-span-2 space-y-6" id="adminLeads"></div>
                <div class="space-y-4">
                    <div id="adminChats"></div>
                    <div id="replyArea" class="hidden p-8 bg-slate-50 rounded-[30px] border shadow-inner">
                        <p class="text-[10px] font-black uppercase text-blue-600 mb-4">Reply to ID: <span id="targetId"></span></p>
                        <input type="text" id="adminReplyText" class="input-pro mb-4" placeholder="Type secure message...">
                        <button onclick="sendAdminReply()" class="btn-elite text-[10px]">Transmit Response</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <footer class="bg-slate-950 text-white py-32 px-8 text-center">
        <p class="text-[11px] font-black uppercase tracking-[0.5em] text-blue-500 mb-8 italic">National Enterprise Dispatch HQ</p>
        <p class="text-[9px] font-bold text-slate-600 uppercase max-w-lg mx-auto leading-loose mb-16">702 Main Street, Woodland, CA 95695 | Authorized Service Portal</p>
    </footer>

    <script>
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const userId = "SIG-" + Math.floor(100000 + Math.random() * 899999);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo({top:0, behavior:'smooth'}); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        document.querySelectorAll('.input-pro').forEach(inp => {
            inp.addEventListener('change', () => {
                const filled = Array.from(document.querySelectorAll('#masterForm .input-pro')).filter(i => i.value).length;
                const p = Math.floor((filled / 9) * 100);
                document.getElementById('pBar').style.width = p + "%";
                document.getElementById('pcent').innerText = p + "%";
            });
        });

        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + userId).push({ text: txt, type: 'user', time: new Date().toLocaleTimeString() });
            document.getElementById('chat-input').value = '';
        }
        db.ref('chats/' + userId).on('value', snap => {
            let h = ''; const msgs = snap.val();
            for(let k in msgs) h += `<div class="bubble ${msgs[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${msgs[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-DISPATCH-" + Math.floor(100000 + Math.random() * 900000);
            const data = { tid, name: document.getElementById('vName').value, email: document.getElementById('vEmail').value, phone: document.getElementById('vPhone').value, svc: document.getElementById('vSvc').value, addr: document.getElementById('vAddr').value, ts: new Date().toLocaleString() };
            db.ref('leads').push(data).then(() => {
                document.getElementById('masterForm').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('receipt-data').innerHTML = `<p class="flex justify-between border-b border-white/10 pb-2"><span>ID:</span> <span class="text-blue-400">${tid}</span></p><p class="flex justify-between border-b border-white/10 pb-2"><span>Customer:</span> <span>${data.name}</span></p><p class="flex justify-between border-b border-white/10 pb-2"><span>Service:</span> <span>${data.svc}</span></p><p class="flex justify-between border-b border-white/10 pb-2"><span>Location:</span> <span>${data.addr}</span></p>`;
            });
        });

        let taps = 0, tapT;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } clearTimeout(tapT); tapT=setTimeout(()=>taps=0,2000); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) h += `<div class="p-8 bg-slate-50 border rounded-[35px] relative group"><span class="absolute top-6 right-6 bg-slate-900 text-white px-4 py-1 rounded-full text-[8px] font-black uppercase">${leads[k].tid}</span><h4 class="text-xl font-black italic mb-2">${leads[k].name}</h4><p class="text-[10px] font-bold text-slate-500 italic uppercase">📞 ${leads[k].phone} | 🏠 ${leads[k].addr}</p><button onclick="del('leads/${k}')" class="mt-4 text-red-500 font-black text-[9px] uppercase">Erase Lead</button></div>`;
                document.getElementById('adminLeads').innerHTML = h || 'Terminal Clear.';
            });
            db.ref('chats').on('value', snap => {
                const chats = snap.val(); let h = '';
                for(let uid in chats) {
                    const last = Object.values(chats[uid]).pop();
                    h += `<div class="p-4 bg-white border rounded-xl flex justify-between items-center mb-4 cursor-pointer hover:border-blue-400" onclick="openReply('${uid}')"><div><p class="text-[9px] font-black text-blue-600">${uid}</p><p class="text-[11px] font-bold italic">"${last.text}"</p></div></div>`;
                }
                document.getElementById('adminChats').innerHTML = h || 'No Active Signals.';
            });
        }
        let activeId = '';
        function openReply(uid) { activeId = uid; document.getElementById('replyArea').classList.remove('hidden'); document.getElementById('targetId').innerText = uid; }
        function sendAdminReply() {
            const txt = document.getElementById('adminReplyText').value; if(!txt || !activeId) return;
            db.ref('chats/' + activeId).push({ text: txt, type: 'admin' });
            document.getElementById('adminReplyText').value = '';
        }
        function del(p) { if(confirm('Erase data permanently?')) db.ref(p).remove(); }
        function exportToExcel() { db.ref('leads').once('value', s => { const d = Object.values(s.val()||{}); const ws = XLSX.utils.json_to_sheet(d); const wb = XLSX.utils.book_new(); XLSX.utils.book_append_sheet(wb, ws, "Leads"); XLSX.writeFile(wb, "National_Leads_Export.xlsx"); }); }
    </script>
</body>
</html>
