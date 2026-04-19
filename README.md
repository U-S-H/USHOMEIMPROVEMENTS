<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | National Enterprise Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; --emerald: #10b981; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #1e293b; overflow-x: hidden; }
        .hero-final { background: linear-gradient(rgba(15, 23, 42, 0.96), rgba(15, 23, 42, 0.9)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
        .glass-nav { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(20px); border-bottom: 1px solid #f1f5f9; }
        .input-elite { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; font-size: 14px; }
        .input-elite:focus { border-color: var(--accent); background: #f8faff; box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.08); }
        .btn-glow { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px 32px; border-radius: 20px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; transition: 0.4s; box-shadow: 0 15px 30px rgba(37, 99, 235, 0.2); border: none; }
        .btn-glow:hover { transform: translateY(-4px); box-shadow: 0 20px 40px rgba(37, 99, 235, 0.3); }
        .page-section { display: none; }
        .page-section.active { display: block; animation: contentFade 0.7s ease-out; }
        @keyframes contentFade { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 30px; box-shadow: 0 30px 60px rgba(0,0,0,0.2); display: none; flex-direction: column; z-index: 6000; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 22px; color: white; display: flex; align-items: center; gap: 12px; }
        #chat-feed { flex: 1; padding: 25px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 600; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); }
        .admin-secret-btn { display: none; } /* HIDDEN FOR SECURITY */
    </style>
</head>
<body>

    <nav class="glass-nav sticky top-0 z-[5000] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <img src="logo.png" onclick="handleAdminTap()" class="h-12 w-12 bg-white border-2 rounded-2xl shadow-sm cursor-pointer" onerror="this.src='https://ui-avatars.com/api/?name=US&background=0f172a&color=fff'">
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase leading-none tracking-tight">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic tracking-tighter">Enterprise National Terminal</span>
            </div>
        </div>
        <div class="hidden lg:flex gap-10 text-[10px] font-black uppercase tracking-widest text-slate-400">
            <button onclick="showPage('home')" class="hover:text-blue-600">Home</button>
            <button onclick="showPage('projects')" class="hover:text-blue-600">Projects</button>
            <button onclick="showPage('legal')" class="hover:text-blue-600">Compliance</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-full shadow-lg">Free Estimate</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="w-3 h-3 bg-emerald-500 rounded-full animate-pulse shadow-[0_0_10px_#10b981]"></div>
                <div><h4 class="font-black uppercase text-[11px] tracking-widest">Agent ID: Dispatch-786</h4><p class="text-[9px] opacity-70 italic">Secure Support Online</p></div>
                <button onclick="toggleChat()" class="ml-auto text-xl">✕</button>
            </div>
            <div id="chat-feed">
                <div class="bubble bubble-admin">Welcome to U.S. Home Improvement. I am Agent-786. How can I help you today?</div>
            </div>
            <div class="p-5 border-t bg-white flex gap-3">
                <input type="text" id="chat-input" placeholder="Type message..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-950 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[5500] hover:scale-110 transition">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-final py-64 px-6 text-center text-white">
            <div class="max-w-5xl mx-auto">
                <span class="inline-block px-5 py-2 rounded-full border border-blue-500/30 bg-blue-600/10 text-[11px] font-black uppercase tracking-[0.4em] text-blue-400 mb-10 italic">Certified National Infrastructure Partner</span>
                <h1 class="text-6xl md:text-[9rem] font-black uppercase italic leading-[0.8] tracking-tighter mb-12">The <span class="text-blue-500">Master</span> <br>Network.</h1>
                <p class="max-w-2xl mx-auto text-blue-100 font-bold text-xs uppercase tracking-[0.5em] mb-16 leading-relaxed opacity-80">National Site Assessments & Elite Contractor Logistics Across All 50 States.</p>
                <div class="flex flex-wrap justify-center gap-6">
                    <button onclick="showPage('form')" class="btn-glow max-w-[320px]">Initiate Authorization</button>
                    <button onclick="showPage('projects')" class="bg-white/10 border border-white/20 px-10 py-5 rounded-20 font-black uppercase text-xs hover:bg-white/20 transition">View Portfolio</button>
                </div>
            </div>
        </header>
    </section>

    <section id="projects" class="page-section py-24 bg-slate-50 px-8">
        <div class="max-w-7xl mx-auto">
            <h2 class="text-4xl font-black uppercase italic text-center mb-16 tracking-tighter">Enterprise <span class="text-blue-600">Project Feed</span></h2>
            <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
                <script>
                    const pList = ["Roofing Replacement", "Windows Upgrade", "Solar Power", "Kitchen Remodel", "Bath Spa Refit", "Gutters & Siding", "HVAC Systems", "Insulation Sealing", "Luxury Pools", "Hardscapes", "Home Security", "Interior Paint", "Flooring Matrix", "Basement Finish", "Smart Home Tech", "Garage Systems", "Decks & Patios", "Landscaping", "Fence Installation", "Concrete Work"];
                    pList.forEach(p => {
                        document.write(`<div class="bg-white p-8 rounded-[35px] border border-slate-100 shadow-sm hover:shadow-xl transition cursor-pointer" onclick="showPage('form')">
                            <h4 class="font-black text-slate-900 uppercase italic text-xs mb-3">${p}</h4>
                            <p class="text-[9px] font-bold text-slate-400 uppercase tracking-widest">Authorized Dispatch</p>
                        </div>`);
                    });
                </script>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-20 bg-white px-6">
        <div class="max-w-3xl mx-auto bg-white p-12 rounded-[50px] shadow-2xl border-2 border-slate-50">
            <form id="vMasterForm">
                <h3 class="text-2xl font-black uppercase italic text-slate-900 mb-10 border-l-8 border-blue-600 pl-6">Site Authorization Terminal</h3>
                
                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <input type="text" id="vName" placeholder="Full Legal Name" class="input-elite" required>
                    <input type="email" id="vEmail" placeholder="Email Address" class="input-elite" required>
                </div>

                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <input type="tel" id="vPhone" placeholder="Direct Mobile" class="input-elite" required>
                    <select id="vSvc" class="input-elite" required>
                        <option value="">Select Portfolio</option>
                        <script>pList.forEach(p => document.write(`<option value="${p}">${p}</option>`));</script>
                    </select>
                </div>

                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <select id="vOwn" class="input-elite" required>
                        <option value="">Do you own the property?</option>
                        <option value="Yes">Yes, I am the owner</option>
                        <option value="No">No, I am a tenant</option>
                    </select>
                    <input type="number" id="vCount" placeholder="Est. Quantity (e.g. 15)" class="input-elite">
                </div>

                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <select id="vCredit" class="input-elite" required>
                        <option value="">Estimated Credit Score</option>
                        <option value="720+">Excellent (720+)</option>
                        <option value="660-719">Good (660-719)</option>
                        <option value="Below 660">Building Credit</option>
                    </select>
                    <select id="vTimeline" class="input-elite" required>
                        <option value="">Project Timeline</option>
                        <option value="ASAP">As Soon As Possible</option>
                        <option value="1-3 Months">Within 1-3 Months</option>
                        <option value="Future">Future Estimate Only</option>
                    </select>
                </div>

                <div class="grid md:grid-cols-2 gap-6 mb-10">
                    <input type="date" id="vDate" class="input-elite" required>
                    <select id="vTime" class="input-elite" required>
                        <option value="">Appt Time (10AM - 7PM)</option>
                        <option value="10:00 AM">10:00 AM</option>
                        <option value="01:00 PM">01:00 PM</option>
                        <option value="04:00 PM">04:00 PM</option>
                        <option value="07:00 PM">07:00 PM</option>
                    </select>
                </div>

                <input type="text" id="vAddr" placeholder="Property Site Address" class="input-elite mb-10" required>

                <div class="bg-blue-50 p-6 rounded-3xl border border-blue-100 mb-10">
                    <p class="text-[9px] font-black text-blue-900 uppercase mb-2">● Dispatch Security Protocol</p>
                    <p class="text-[10px] font-bold text-blue-700 uppercase leading-relaxed italic">By submitting, you agree that a local certified contractor will call to finalize site access. Your visit is pending this mandatory call.</p>
                </div>

                <button type="submit" class="btn-glow">Authorize Dispatch</button>
            </form>

            <div id="vReceipt" class="hidden text-center py-12">
                <div class="text-7xl mb-10">✅</div>
                <h3 class="text-3xl font-black uppercase italic text-slate-900 mb-6">Dispatch Authorized</h3>
                <div class="bg-slate-950 text-white p-10 rounded-[45px] my-12 text-left border-4 border-blue-600 shadow-3xl">
                    <p class="text-[10px] font-black text-blue-400 uppercase mb-8 tracking-widest text-center">--- OFFICIAL SERVICE RECEIPT ---</p>
                    <div class="space-y-4 text-[11px] font-bold uppercase">
                        <p class="flex justify-between border-b border-white/10 pb-2"><span>Tracking ID:</span> <span id="rTid" class="text-emerald-400 font-black"></span></p>
                        <p class="flex justify-between border-b border-white/10 pb-2"><span>Customer:</span> <span id="rName"></span></p>
                        <p class="flex justify-between border-b border-white/10 pb-2"><span>Service:</span> <span id="rSvc"></span></p>
                        <p class="flex justify-between border-b border-white/10 pb-2"><span>Appt:</span> <span id="rAppt"></span></p>
                        <p class="flex justify-between border-b border-white/10 pb-2"><span>Location:</span> <span id="rLoc" class="text-right max-w-[150px]"></span></p>
                    </div>
                </div>
                <p class="text-[11px] font-black text-slate-400 uppercase italic mb-10">Screenshot this page for your authorized entry.</p>
                <button onclick="location.reload()" class="text-blue-600 font-black text-[11px] uppercase underline">Return Home</button>
            </div>
        </div>
    </section>

    <section id="legal" class="page-section py-24 px-8 bg-slate-900 text-white">
        <div class="max-w-4xl mx-auto border-t-8 border-blue-600 p-16 bg-slate-950 rounded-[48px]">
            <h3 class="text-3xl font-black uppercase italic mb-12">Security <span class="text-blue-500">& Privacy</span></h3>
            <p class="text-[12px] font-bold text-slate-400 uppercase leading-loose mb-10">U.S. Home Improvement LLC operates under strict National Data Standards. All transmissions utilize AES 256-bit military-grade encryption. Information is only shared with verified licensed contractors within our network.</p>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-16 border-b-2 pb-10">
                <div><h3 class="text-3xl font-black uppercase italic text-slate-900">National <span class="text-blue-600">Master</span> Terminal</h3></div>
                <div class="flex gap-4">
                    <button id="exportBtn" onclick="exportData()" class="admin-secret-btn bg-emerald-50 text-emerald-600 px-8 py-4 rounded-full font-black text-[10px] uppercase border border-emerald-200">Export All Leads</button>
                    <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-8 py-4 rounded-full font-black text-[10px] uppercase">Exit Terminal</button>
                </div>
            </div>
            
            <div id="authBox" class="text-center py-40">
                <input type="password" id="pin" class="input-elite max-w-[300px] text-center text-5xl mb-10 shadow-2xl" placeholder="••••">
                <br><button onclick="unlock()" class="btn-glow max-w-[300px]">Authorize Access</button>
            </div>
            
            <div id="hubContent" class="hidden grid lg:grid-cols-3 gap-20">
                <div class="lg:col-span-2"><h5 class="font-black uppercase text-xs text-slate-400 mb-10 italic">Dispatch Records</h5><div id="adminLeads" class="space-y-6"></div></div>
                <div>
                    <h5 class="font-black uppercase text-xs text-slate-400 mb-10 italic">Signal Feed</h5>
                    <div id="adminChats" class="space-y-4"></div>
                    <div id="replyArea" class="hidden mt-10 bg-slate-50 p-10 rounded-[45px] border shadow-inner">
                        <div class="flex justify-between mb-6">
                            <p class="text-[10px] font-black text-blue-600">Signal: <span id="targetId"></span></p>
                            <button id="clearChatBtn" onclick="clearUserChat()" class="admin-secret-btn text-red-500 font-black text-[9px] uppercase">Clear Entire Chat</button>
                        </div>
                        <input type="text" id="adminReplyText" class="input-elite mb-4" placeholder="Type transmission...">
                        <button onclick="sendAdminReply()" class="btn-glow text-[11px]">Transmit Signal</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <footer class="bg-slate-950 text-white py-32 px-8 text-center border-t border-white/5">
        <img src="logo.png" class="h-14 mx-auto mb-10 opacity-50 grayscale hover:grayscale-0 transition" onerror="this.src='https://ui-avatars.com/api/?name=US&background=333&color=fff'">
        <p class="text-[12px] font-black uppercase tracking-[0.5em] text-blue-500 mb-8 italic">National Enterprise HQ</p>
        <p class="text-[10px] font-bold text-slate-600 uppercase mb-16">702 Main Street, Woodland, CA 95695 | Authorized Service Portal</p>
        <p class="text-[9px] font-black text-slate-800 uppercase tracking-widest">© 2026 U.S. HOME IMPROVEMENT LLC. DATA SECURED BY AES-256.</p>
    </footer>

    <script>
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
        const myUid = "SIG-US-" + Math.floor(100000 + Math.random() * 899999);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo({top:0, behavior:'smooth'}); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        // CHAT ENGINE
        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + myUid).push({ text: txt, type: 'user', time: new Date().toLocaleTimeString() });
            document.getElementById('chat-input').value = '';
        }
        db.ref('chats/' + myUid).on('value', snap => {
            const msgs = snap.val(); let h = '';
            for(let k in msgs) h += `<div class="bubble ${msgs[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${msgs[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // SUBMISSION
        document.getElementById('vMasterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-DIS-" + Math.floor(1000000 + Math.random() * 8999999);
            const data = {
                tid: tid, name: document.getElementById('vName').value, email: document.getElementById('vEmail').value,
                phone: document.getElementById('vPhone').value, svc: document.getElementById('vSvc').value,
                count: document.getElementById('vCount').value || '1', credit: document.getElementById('vCredit').value,
                date: document.getElementById('vDate').value, time: document.getElementById('vTime').value,
                timeline: document.getElementById('vTimeline').value, addr: document.getElementById('vAddr').value,
                ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('vMasterForm').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('rTid').innerText = tid;
                document.getElementById('rName').innerText = data.name;
                document.getElementById('rSvc').innerText = data.svc;
                document.getElementById('rAppt').innerText = data.date + " @ " + data.time;
                document.getElementById('rLoc').innerText = data.addr;
            });
        });

        // ADMIN HUB
        let taps = 0, tapT;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } clearTimeout(tapT); tapT=setTimeout(()=>taps=0,2000); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { 
            if(document.getElementById('pin').value === "786") { 
                document.getElementById('authBox').classList.add('hidden'); 
                document.getElementById('hubContent').classList.remove('hidden'); 
                document.getElementById('exportBtn').style.display = 'block'; // SHOW SECRET BUTTONS
                document.getElementById('clearChatBtn').style.display = 'block'; 
                syncData(); 
            } 
        }

        let activeId = '';
        function syncData() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) h += `<div class="p-10 bg-slate-50 border-2 rounded-[40px] relative">
                    <span class="absolute top-6 right-6 bg-blue-600 text-white px-4 py-1 rounded-full text-[9px] font-black">${leads[k].tid}</span>
                    <h4 class="text-2xl font-black italic text-slate-900 mb-2">${leads[k].name}</h4>
                    <div class="grid md:grid-cols-2 gap-4 text-[10px] font-bold text-slate-500 uppercase italic">
                        <p>📞 ${leads[k].phone}</p><p>📧 ${leads[k].email}</p>
                        <p>📍 ${leads[k].addr}</p><p>🛠 ${leads[k].svc} (${leads[k].count})</p>
                        <p>💳 Credit: ${leads[k].credit}</p><p>📅 ${leads[k].date} (${leads[k].time})</p>
                    </div>
                    <button onclick="del('leads/${k}')" class="mt-8 text-red-500 font-black text-[9px] uppercase border-t pt-4 w-full text-center">Delete Dispatch Data</button>
                </div>`;
                document.getElementById('adminLeads').innerHTML = h || 'Terminal Clear.';
            });
            db.ref('chats').on('value', snap => {
                const chats = snap.val(); let h = '';
                for(let uid in chats) {
                    const last = Object.values(chats[uid]).pop();
                    h += `<div class="p-6 bg-white border rounded-3xl flex justify-between items-center mb-4 shadow-sm cursor-pointer hover:border-blue-500" onclick="openReply('${uid}')">
                        <div><p class="text-[9px] font-black text-blue-600 uppercase">${uid}</p><p class="text-[12px] font-bold italic">"${last.text}"</p></div>
                    </div>`;
                }
                document.getElementById('adminChats').innerHTML = h || 'No Active Signals.';
            });
        }
        function openReply(uid) { activeId = uid; document.getElementById('replyArea').classList.remove('hidden'); document.getElementById('targetId').innerText = uid; }
        function sendAdminReply() {
            const txt = document.getElementById('adminReplyText').value; if(!txt || !activeId) return;
            db.ref('chats/' + activeId).push({ text: txt, type: 'admin', time: new Date().toLocaleTimeString() });
            document.getElementById('adminReplyText').value = '';
        }
        function clearUserChat() { if(confirm('Permanently clear entire chat history?')) db.ref('chats/' + activeId).remove(); }
        function del(path) { if(confirm('Erase permanently?')) db.ref(path).remove(); }
        function exportData() {
            db.ref('leads').once('value', snap => {
                const ws = XLSX.utils.json_to_sheet(Object.values(snap.val() || {}));
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "Leads");
                XLSX.writeFile(wb, "US_Home_Enterprise_Leads.xlsx");
            });
        }
    </script>
</body>
</html>
