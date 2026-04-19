<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | National Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fafafa; color: #1e293b; overflow-x: hidden; }
        .hero-section { background: linear-gradient(rgba(15, 23, 42, 0.9), rgba(15, 23, 42, 0.9)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
        .glass-nav { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(15px); border-bottom: 1px solid #f1f5f9; }
        
        .input-pro { width: 100%; padding: 15px; border: 2px solid #f1f5f9; border-radius: 12px; font-weight: 600; outline: none; transition: 0.3s; font-size: 13px; }
        .input-pro:focus { border-color: var(--accent); background: #f8faff; box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }
        
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 16px 32px; border-radius: 14px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; cursor: pointer; border: none; width: 100%; }
        .btn-master:hover { transform: translateY(-3px); box-shadow: 0 15px 30px rgba(37, 99, 235, 0.3); }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeInUp 0.5s ease; }
        @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        /* Professional Chat UI */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 350px; height: 500px; background: white; border-radius: 28px; box-shadow: 0 25px 50px rgba(0,0,0,0.15); display: none; flex-direction: column; z-index: 5000; overflow: hidden; border: 1px solid #e2e8f0; }
        .chat-header { background: #1e3a8a; padding: 20px; color: white; display: flex; align-items: center; gap: 12px; }
        .online-dot { width: 10px; height: 10px; background: #10b981; border-radius: 50%; border: 2px solid white; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 10px; }
        .bubble { padding: 12px 16px; border-radius: 18px; font-size: 12px; max-width: 80%; font-weight: 500; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .bubble-admin { background: #e2e8f0; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; }
    </style>
</head>
<body>

    <nav class="glass-nav sticky top-0 z-[4000] px-6 py-4 flex justify-between items-center">
        <div class="flex items-center gap-3">
            <img src="logo.png" onclick="handleAdminTap()" class="h-10 w-10 bg-white border rounded-xl cursor-pointer" onerror="this.src='https://ui-avatars.com/api/?name=US&background=1e3a8a&color=fff'">
            <div>
                <h1 class="text-xs font-black text-blue-950 uppercase leading-none">U.S. Home Improvement</h1>
                <span class="text-[8px] font-bold text-emerald-600 uppercase italic tracking-tighter">● National Enterprise Hub</span>
            </div>
        </div>
        <div class="hidden lg:flex gap-8 text-[9px] font-black uppercase tracking-widest text-slate-400">
            <button onclick="showPage('home')" class="hover:text-blue-600">Home</button>
            <button onclick="showPage('legal')" class="hover:text-blue-600">Compliance</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-5 py-2.5 rounded-full shadow-lg">New Estimate</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="online-dot"></div>
                <div><h4 class="font-black uppercase text-[10px] leading-tight">Live Agent: Agent-786</h4><p class="text-[8px] opacity-70 italic">Verified Support Line</p></div>
                <button onclick="toggleChat()" class="ml-auto text-xl">✕</button>
            </div>
            <div id="chat-feed">
                <div class="bubble bubble-admin">Hello! Welcome to U.S. Home Improvement. How can we assist you with your project today? Our agents are online.</div>
            </div>
            <div class="p-4 border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="Type message..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-blue-600 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[4999] hover:scale-110 transition">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-section py-40 px-6 text-center text-white">
            <div class="max-w-4xl mx-auto">
                <span class="px-4 py-1.5 rounded-full border border-white/20 bg-white/10 text-[9px] font-black uppercase tracking-[0.3em] mb-8 inline-block">Authorized National Industry Leader</span>
                <h1 class="text-5xl md:text-8xl font-black uppercase italic leading-[0.85] tracking-tighter mb-10">Premium <br><span class="text-blue-500">Home Services</span> <br>Network.</h1>
                <p class="text-blue-100 font-bold text-[10px] uppercase tracking-[0.4em] mb-12">Certified Site Inspections & Logistics Across 50 States.</p>
                <div class="flex flex-wrap justify-center gap-4">
                    <button onclick="showPage('form')" class="btn-master max-w-[250px]">Start Dispatch</button>
                    <button onclick="showPage('legal')" class="bg-white/10 border border-white/20 px-8 py-4 rounded-14 font-black uppercase text-xs">View Legal</button>
                </div>
            </div>
        </header>
    </section>

    <section id="form" class="page-section py-20 px-6 bg-white">
        <div class="max-w-2xl mx-auto bg-white p-10 rounded-[40px] shadow-2xl border border-slate-50">
            <form id="masterForm">
                <h3 class="text-xl font-black uppercase italic text-blue-950 mb-8 border-l-8 border-blue-600 pl-4">Authorization Terminal</h3>
                
                <div class="grid md:grid-cols-2 gap-4 mb-4">
                    <input type="text" id="fName" placeholder="Full Legal Name" class="input-pro" required>
                    <input type="email" id="fEmail" placeholder="Email Address" class="input-pro" required>
                </div>

                <div class="grid md:grid-cols-2 gap-4 mb-4">
                    <input type="tel" id="fPhone" placeholder="Direct Mobile" class="input-pro" required>
                    <select id="fSvc" class="input-pro" required>
                        <option value="">Select Service</option>
                        <option value="Windows">Windows Replacement</option>
                        <option value="Roofing">Roofing Installation</option>
                        <option value="Solar">Solar Power Matrix</option>
                        <option value="Kitchen">Kitchen Remodeling</option>
                        <option value="Gutters">Seamless Gutters</option>
                        <option value="HVAC">Climate Control (HVAC)</option>
                    </select>
                </div>

                <div class="grid md:grid-cols-2 gap-4 mb-4">
                    <input type="number" id="fCount" placeholder="Count (e.g. 10 Windows)" class="input-pro">
                    <select id="fCredit" class="input-pro" required>
                        <option value="">Credit Score Range</option>
                        <option value="720+">Excellent (720+)</option>
                        <option value="660-719">Good (660-719)</option>
                        <option value="Below 660">Building (Below 660)</option>
                    </select>
                </div>

                <div class="grid md:grid-cols-2 gap-4 mb-4">
                    <input type="date" id="fDate" class="input-pro" required>
                    <select id="fTime" class="input-pro" required>
                        <option value="">Appt Time (10AM - 7PM)</option>
                        <option value="10:00 AM">10:00 AM</option>
                        <option value="12:00 PM">12:00 PM</option>
                        <option value="03:00 PM">03:00 PM</option>
                        <option value="05:00 PM">05:00 PM</option>
                        <option value="07:00 PM">07:00 PM</option>
                    </select>
                </div>

                <select id="fTimeline" class="input-pro mb-4" required>
                    <option value="">Project Timeline</option>
                    <option value="ASAP">As Soon As Possible</option>
                    <option value="2-3 Months">Within 2-3 Months</option>
                    <option value="Future">Future Estimate Only</option>
                </select>

                <input type="text" id="fAddr" placeholder="Property Address" class="input-pro mb-8" required>

                <div class="bg-blue-50 p-5 rounded-2xl border border-blue-100 mb-8">
                    <p class="text-[9px] font-black text-blue-900 uppercase italic">⚠️ Important Notice</p>
                    <p class="text-[8px] font-bold text-blue-700 uppercase leading-relaxed mt-1">A local certified contractor will contact you within 24 hours to confirm site access. Your appointment is pending final confirmation via phone call.</p>
                </div>

                <button type="submit" class="btn-master">Authorize Dispatch</button>
            </form>

            <div id="receipt" class="hidden text-center py-6">
                <div class="text-6xl mb-6">✅</div>
                <h3 class="text-2xl font-black uppercase italic text-blue-950">Dispatch Authorized</h3>
                <div class="bg-slate-50 p-8 rounded-3xl border my-8 text-left">
                    <p class="text-[9px] font-black text-blue-600 uppercase mb-4 tracking-widest text-center">--- Official Service Receipt ---</p>
                    <div class="space-y-3 text-[10px] font-bold uppercase text-slate-700">
                        <div class="flex justify-between border-b pb-2"><span>Tracking ID:</span> <span id="rId" class="text-blue-700 font-black"></span></div>
                        <div class="flex justify-between border-b pb-2"><span>Customer:</span> <span id="rName"></span></div>
                        <div class="flex justify-between border-b pb-2"><span>Service:</span> <span id="rSvc"></span></div>
                        <div class="flex justify-between border-b pb-2"><span>Appt:</span> <span id="rTime"></span></div>
                        <div class="flex justify-between border-b pb-2"><span>Address:</span> <span id="rAddr" class="text-right max-w-[150px]"></span></div>
                        <div class="flex justify-between border-b pb-2"><span>Details:</span> <span>Count: <span id="rCount"></span> | Credit: <span id="rCredit"></span></span></div>
                    </div>
                </div>
                <p class="text-[9px] font-black text-slate-400 uppercase italic">Screenshot this screen for your records.</p>
                <button onclick="location.reload()" class="mt-10 text-blue-600 font-black text-[10px] uppercase underline">Return to Terminal</button>
            </div>
        </div>
    </section>

    <section id="legal" class="page-section py-20 px-6 bg-slate-50">
        <div class="max-w-4xl mx-auto bg-white p-12 rounded-[40px] border shadow-sm">
            <h3 class="text-2xl font-black uppercase italic text-blue-950 mb-10 border-b pb-4">Compliance <span class="text-blue-600">& Legal</span></h3>
            <div class="space-y-10">
                <div>
                    <h5 class="text-[10px] font-black uppercase text-blue-600 mb-3 tracking-widest">Privacy Protocol</h5>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">U.S. Home Improvement LLC values your security. All data is protected by 256-bit AES encryption. By submitting, you authorize our network to contact you via phone/SMS. We do not sell data to third parties.</p>
                </div>
                <div>
                    <h5 class="text-[10px] font-black uppercase text-blue-600 mb-3 tracking-widest">Appointment Terms</h5>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Appointments are subject to availability and final confirmation by a local licensed contractor. Estimates are preliminary until an on-site inspection is performed.</p>
                </div>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-10">
        <div class="flex justify-between items-center mb-12 border-b pb-6">
            <h3 class="text-2xl font-black uppercase italic text-blue-950">Master Terminal <span class="text-blue-600">Hub</span></h3>
            <button onclick="closeAdmin()" class="text-red-500 font-black text-[10px] uppercase">Exit Hub</button>
        </div>
        <div id="authBox" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center mb-4" placeholder="HUB PIN"><br><button onclick="unlock()" class="btn-master max-w-[200px]">Unlock</button></div>
        
        <div id="hubContent" class="hidden grid lg:grid-cols-2 gap-12">
            <div>
                <h5 class="font-black uppercase text-xs text-slate-400 mb-8 italic">Verified Lead Dispatches</h5>
                <div id="leadContainer" class="space-y-4"></div>
            </div>
            <div>
                <h5 class="font-black uppercase text-xs text-slate-400 mb-8 italic">Agent Chat Terminal</h5>
                <div id="chatContainer" class="space-y-4"></div>
                <div id="replyArea" class="hidden mt-8 bg-blue-50 p-8 rounded-3xl border">
                    <p class="text-[10px] font-black uppercase text-blue-600 mb-4">Replying to: <span id="targetId"></span></p>
                    <input type="text" id="adminReplyText" class="input-pro mb-4" placeholder="Type secure reply...">
                    <button onclick="sendAdminReply()" class="btn-master text-xs">Transmit Reply</button>
                </div>
            </div>
        </div>
    </div>

    <footer class="bg-slate-950 text-white py-24 px-6 text-center">
        <p class="text-[10px] font-black uppercase text-blue-500 mb-8 italic tracking-[0.4em]">Official Enterprise National Dispatch</p>
        <div class="flex justify-center gap-10 opacity-30 grayscale mb-16">
            <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Forbes_logo.svg" class="h-4">
            <img src="https://upload.wikimedia.org/wikipedia/commons/a/a2/Better_Business_Bureau_logo.svg" class="h-4">
        </div>
        <p class="text-[8px] font-bold text-slate-600 uppercase max-w-lg mx-auto leading-relaxed">702 Main Street, Woodland, CA 95695 | (786) Authorized Access | © 2026 U.S. HOME IMPROVEMENT LLC.</p>
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
        const userId = "USER_" + Math.floor(1000 + Math.random() * 9000);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo(0,0); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        // CHAT SYNC (2-Way)
        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + userId).push({ text: txt, type: 'user', time: new Date().toLocaleTimeString() });
            document.getElementById('chat-input').value = '';
        }
        db.ref('chats/' + userId).on('value', snap => {
            const msgs = snap.val(); let h = '';
            for(let k in msgs) h += `<div class="bubble ${msgs[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${msgs[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // FORM SUBMISSION
        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-" + Math.floor(100000 + Math.random() * 899999);
            const data = {
                tid: tid, name: document.getElementById('fName').value, email: document.getElementById('fEmail').value,
                phone: document.getElementById('fPhone').value, svc: document.getElementById('fSvc').value,
                count: document.getElementById('fCount').value || '1', credit: document.getElementById('fCredit').value,
                date: document.getElementById('fDate').value, time: document.getElementById('fTime').value,
                timeline: document.getElementById('fTimeline').value, addr: document.getElementById('fAddr').value,
                ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('masterForm').classList.add('hidden');
                document.getElementById('receipt').classList.remove('hidden');
                document.getElementById('rId').innerText = tid;
                document.getElementById('rName').innerText = data.name;
                document.getElementById('rSvc').innerText = data.svc;
                document.getElementById('rTime').innerText = data.date + " @ " + data.time;
                document.getElementById('rAddr').innerText = data.addr;
                document.getElementById('rCount').innerText = data.count;
                document.getElementById('rCredit').innerText = data.credit;
            });
        });

        // ADMIN LOGIC
        let taps = 0, tapT;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } clearTimeout(tapT); tapT=setTimeout(()=>taps=0,2000); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubContent').classList.remove('hidden'); syncAdmin(); } }

        let replyId = '';
        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) h += `<div class="p-6 bg-slate-50 border rounded-3xl relative mb-4">
                    <span class="absolute top-4 right-4 bg-blue-600 text-white px-3 py-1 rounded-full text-[8px] font-black uppercase">Tracking: ${leads[k].tid}</span>
                    <h4 class="font-black text-blue-900 mb-1 italic">${leads[k].name} (${leads[k].svc})</h4>
                    <p class="text-[9px] font-bold text-slate-500 uppercase italic">📞 ${leads[k].phone} | 📍 ${leads[k].addr}</p>
                    <p class="text-[8px] font-black text-blue-600 mt-2 uppercase">Appt: ${leads[k].date} @ ${leads[k].time} | Credit: ${leads[k].credit} | Timeline: ${leads[k].timeline}</p>
                    <button onclick="del('leads/${k}')" class="mt-4 text-red-400 font-black text-[8px] uppercase">Erase Lead</button>
                </div>`;
                document.getElementById('leadContainer').innerHTML = h || 'Terminal Empty.';
            });
            db.ref('chats').on('value', snap => {
                const chats = snap.val(); let h = '';
                for(let uid in chats) {
                    const last = Object.values(chats[uid]).pop();
                    h += `<div class="p-4 bg-white border rounded-xl flex justify-between items-center mb-2 shadow-sm cursor-pointer" onclick="openReply('${uid}')">
                        <div><p class="text-[9px] font-black text-blue-600 uppercase">Signal ID: ${uid}</p><p class="text-[10px] font-bold italic">"${last.text}"</p></div>
                    </div>`;
                }
                document.getElementById('chatContainer').innerHTML = h || 'No Active Signals.';
            });
        }
        function openReply(uid) { replyId = uid; document.getElementById('replyArea').classList.remove('hidden'); document.getElementById('targetId').innerText = uid; }
        function sendAdminReply() {
            const txt = document.getElementById('adminReplyText').value; if(!txt || !replyId) return;
            db.ref('chats/' + replyId).push({ text: txt, type: 'admin', time: new Date().toLocaleTimeString() });
            document.getElementById('adminReplyText').value = ''; alert("Reply Transmitted!");
        }
        function del(path) { if(confirm('Erase Record?')) db.ref(path).remove(); }
    </script>
</body>
</html>
