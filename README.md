<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | National Enterprise Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; scroll-behavior: smooth; }
        
        .hero-section { background: linear-gradient(rgba(15, 23, 42, 0.85), rgba(15, 23, 42, 0.85)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
        .glass-nav { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(15px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        
        .input-pro { width: 100%; padding: 15px; border: 2px solid #f1f5f9; border-radius: 12px; font-weight: 600; outline: none; transition: 0.3s; font-size: 13px; }
        .input-pro:focus { border-color: var(--accent); background: #f8faff; }
        
        .btn-premium { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 16px 30px; border-radius: 14px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; cursor: pointer; transition: 0.4s; box-shadow: 0 10px 20px rgba(37, 99, 235, 0.2); border: none; }
        .btn-premium:hover { transform: translateY(-3px); box-shadow: 0 15px 30px rgba(37, 99, 235, 0.3); }

        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.5s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Chat UI 2.0 */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 350px; height: 500px; background: white; border-radius: 25px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.2); display: none; flex-direction: column; z-index: 5000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #1e3a8a; padding: 20px; color: white; display: flex; justify-content: space-between; align-items: center; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; display: flex; flex-direction: column; gap: 10px; background: #f8fafc; }
        .bubble { padding: 10px 14px; border-radius: 18px; font-size: 13px; max-width: 80%; line-height: 1.4; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .bubble-admin { background: #e2e8f0; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; font-weight: 600; }
        
        .logo-img { height: 42px; width: 42px; object-fit: contain; border-radius: 8px; background: white; cursor: pointer; border: 1px solid #eee; }
        #toast { position: fixed; bottom: 30px; left: 30px; background: white; padding: 12px 20px; border-radius: 50px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); display: none; z-index: 9999; border-left: 4px solid #2563eb; }
    </style>
</head>
<body>

    <div id="toast" class="flex items-center gap-3"><p id="toast-msg" class="text-[10px] font-black uppercase italic text-slate-600"></p></div>

    <nav class="glass-nav sticky top-0 z-[4000] px-6 py-4 flex justify-between items-center">
        <div class="flex items-center gap-3">
            <img src="logo.png" onclick="handleAdminTap()" class="logo-img" onerror="this.src='https://ui-avatars.com/api/?name=US&background=1e3a8a&color=fff'">
            <div>
                <h1 class="text-sm font-black text-blue-950 uppercase leading-none">U.S. Home Improvement</h1>
                <span class="text-[8px] font-bold text-emerald-600 uppercase italic">● Enterprise Dispatch Terminal</span>
            </div>
        </div>
        <div class="hidden lg:flex gap-8 text-[9px] font-black uppercase tracking-widest text-slate-400">
            <button onclick="showPage('home')" class="hover:text-blue-600">Solutions</button>
            <button onclick="showPage('services')" class="hover:text-blue-600">Full Portfolio</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-2 rounded-full shadow-lg">Get Estimate</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div><h4 class="font-black uppercase text-[10px]">Live Dispatch Support</h4><p class="text-[8px] opacity-80 italic">Verified Terminal Connection</p></div>
                <button onclick="toggleChat()">✕</button>
            </div>
            <div id="chat-feed"></div>
            <div class="p-4 border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="Ask a specialist..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-blue-600 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[4999] hover:scale-110 transition">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-section py-40 px-6 text-center text-white">
            <div class="max-w-5xl mx-auto">
                <span class="px-4 py-1 rounded-full border border-white/20 bg-white/10 text-[9px] font-black uppercase tracking-widest mb-8 inline-block">Authorized National Authority</span>
                <h1 class="text-5xl md:text-8xl font-black uppercase italic leading-[0.9] tracking-tighter mb-10">Premium <br><span class="text-blue-400">Home Improvement</span> <br>Network.</h1>
                <p class="max-w-xl mx-auto text-blue-100 font-bold text-[11px] uppercase tracking-[0.3em] mb-12">Certified Inspections & Professional Contractor Dispatch across 50 States.</p>
                <div class="flex flex-wrap justify-center gap-4">
                    <button onclick="showPage('form')" class="btn-premium">Start Site Survey</button>
                    <button onclick="showPage('services')" class="bg-white/10 px-8 py-4 rounded-14 font-black uppercase text-xs border border-white/20">Explore Services</button>
                </div>
            </div>
        </header>

        <div class="max-w-7xl mx-auto px-6 py-24 grid md:grid-cols-4 gap-6">
            <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm text-center" onclick="startSvc('Roofing')"><img src="WA_1776549716792.jpeg" class="w-full h-32 object-cover rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Roofing</h4></div>
            <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm text-center" onclick="startSvc('Solar')"><img src="WA_1776549781247.jpeg" class="w-full h-32 object-cover rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Solar</h4></div>
            <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm text-center" onclick="startSvc('Windows')"><img src="WA_1776549555727.jpeg" class="w-full h-32 object-cover rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Windows</h4></div>
            <div class="bg-white p-6 rounded-3xl border border-slate-100 shadow-sm text-center" onclick="startSvc('Kitchen')"><img src="WA_1776549917709.jpeg" class="w-full h-32 object-cover rounded-2xl mb-4"><h4 class="font-black uppercase text-xs">Interior</h4></div>
        </div>
    </section>

    <section id="services" class="page-section py-24 bg-slate-50">
        <div class="max-w-6xl mx-auto px-6">
            <h2 class="text-4xl font-black uppercase italic text-center mb-16 tracking-tighter">Full <span class="text-blue-600">Enterprise Portfolio</span></h2>
            <div class="grid md:grid-cols-3 gap-8">
                <div class="bg-white p-8 rounded-[32px] shadow-sm border border-slate-100">
                    <h3 class="font-black uppercase text-blue-900 mb-2 italic">Exterior Solutions</h3>
                    <ul class="text-[10px] font-bold text-slate-500 uppercase space-y-3">
                        <li class="flex justify-between border-b pb-2"><span>Roofing Replacement</span> <button onclick="startSvc('Roofing')" class="text-blue-600">Select</button></li>
                        <li class="flex justify-between border-b pb-2"><span>Gutter Systems</span> <button onclick="startSvc('Gutters')" class="text-blue-600">Select</button></li>
                        <li class="flex justify-between border-b pb-2"><span>Exterior Painting</span> <button onclick="startSvc('Painting')" class="text-blue-600">Select</button></li>
                        <li class="flex justify-between border-b pb-2"><span>Siding & Facade</span> <button onclick="startSvc('Siding')" class="text-blue-600">Select</button></li>
                    </ul>
                </div>
                <div class="bg-white p-8 rounded-[32px] shadow-sm border border-slate-100">
                    <h3 class="font-black uppercase text-blue-900 mb-2 italic">Energy & Systems</h3>
                    <ul class="text-[10px] font-bold text-slate-500 uppercase space-y-3">
                        <li class="flex justify-between border-b pb-2"><span>Solar Power Matrix</span> <button onclick="startSvc('Solar')" class="text-blue-600">Select</button></li>
                        <li class="flex justify-between border-b pb-2"><span>HVAC Optimization</span> <button onclick="startSvc('HVAC')" class="text-blue-600">Select</button></li>
                        <li class="flex justify-between border-b pb-2"><span>Insulation Shield</span> <button onclick="startSvc('Insulation')" class="text-blue-600">Select</button></li>
                        <li class="flex justify-between border-b pb-2"><span>Window Sealing</span> <button onclick="startSvc('Windows')" class="text-blue-600">Select</button></li>
                    </ul>
                </div>
                <div class="bg-white p-8 rounded-[32px] shadow-sm border border-slate-100">
                    <h3 class="font-black uppercase text-blue-900 mb-2 italic">Interior Design</h3>
                    <ul class="text-[10px] font-bold text-slate-500 uppercase space-y-3">
                        <li class="flex justify-between border-b pb-2"><span>Kitchen Remodeling</span> <button onclick="startSvc('Kitchen')" class="text-blue-600">Select</button></li>
                        <li class="flex justify-between border-b pb-2"><span>Bathroom Spas</span> <button onclick="startSvc('Bathroom')" class="text-blue-600">Select</button></li>
                        <li class="flex justify-between border-b pb-2"><span>Basement Refinish</span> <button onclick="startSvc('Basement')" class="text-blue-600">Select</button></li>
                        <li class="flex justify-between border-b pb-2"><span>Flooring Matrix</span> <button onclick="startSvc('Flooring')" class="text-blue-600">Select</button></li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-24 bg-white px-6">
        <div class="max-w-xl mx-auto">
            <div class="bg-white p-10 rounded-[40px] shadow-2xl border border-slate-50">
                <form id="mainLeadForm">
                    <h3 class="text-2xl font-black uppercase italic mb-8 border-l-8 border-blue-600 pl-4 text-blue-950">Dispatch Authorization</h3>
                    <div id="step-1">
                        <input type="text" id="custName" placeholder="Full Legal Name" class="input-pro mb-3" required>
                        <input type="tel" id="custPhone" placeholder="Mobile Number" class="input-pro mb-3" required>
                        <select id="custSvc" class="input-pro mb-3" onchange="updateQualifiers()" required>
                            <option value="Roofing">Roofing Installation</option>
                            <option value="Solar">Solar Power Matrix</option>
                            <option value="Windows">Energy Windows</option>
                            <option value="Kitchen">Kitchen Remodeling</option>
                            <option value="Bathroom">Bathroom Spas</option>
                            <option value="HVAC">HVAC Systems</option>
                            <option value="Painting">Exterior Painting</option>
                        </select>
                        <div id="qualifiers" class="mt-2"></div>
                        <input type="text" id="custAddr" placeholder="Site Address" class="input-pro mt-4 mb-8" required>
                        <button type="submit" class="btn-premium w-full">Request Site Survey</button>
                    </div>
                </form>
                <div id="formSuccess" class="hidden text-center py-10">
                    <div class="text-6xl mb-6">🚀</div>
                    <h2 class="text-2xl font-black uppercase italic text-blue-950">Authorization Sent</h2>
                    <p class="text-[10px] font-bold text-slate-400 mt-4 uppercase">Reference Code: #US-<span id="refCode"></span></p>
                    <button onclick="location.reload()" class="mt-8 text-blue-600 font-black text-[10px] uppercase">Submit New</button>
                </div>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9000] hidden overflow-y-auto p-8">
        <div class="flex justify-between items-center mb-12 border-b pb-6">
            <h3 class="text-2xl font-black uppercase italic text-blue-950">Master Terminal <span class="text-blue-600">Hub</span></h3>
            <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-6 py-2 rounded-full font-black text-[10px] uppercase">Exit Hub</button>
        </div>
        <div id="authBox" class="text-center py-20"><input type="password" id="pin" class="input-pro max-w-[200px] text-center text-xl mb-4" placeholder="ENTER PIN"><br><button onclick="unlock()" class="btn-premium max-w-[200px]">Access Hub</button></div>
        
        <div id="hubData" class="hidden grid lg:grid-cols-2 gap-10">
            <div><h5 class="font-black uppercase text-xs mb-6 text-slate-400 italic">Project Dispatches</h5><div id="adminLeads" class="space-y-4"></div></div>
            <div>
                <h5 class="font-black uppercase text-xs mb-6 text-slate-400 italic">Live Chat Terminal</h5>
                <div id="adminChats" class="space-y-4"></div>
                <div id="replyBox" class="hidden mt-6 bg-slate-50 p-6 rounded-3xl border">
                    <p class="text-[10px] font-black uppercase mb-4 text-blue-600">Replying to: <span id="replyTo"></span></p>
                    <input type="text" id="adminReplyText" placeholder="Type response..." class="input-pro mb-4">
                    <button onclick="sendAdminReply()" class="btn-premium w-full text-xs">Send Reply to User</button>
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
        const userId = "USER_" + Math.floor(Math.random() * 1000000);

        // NAVIGATION
        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo(0,0); }
        function startSvc(svc) { document.getElementById('custSvc').value = svc; updateQualifiers(); showPage('form'); }

        // QUALIFYING QUESTIONS SYSTEM
        function updateQualifiers() {
            const svc = document.getElementById('custSvc').value;
            const container = document.getElementById('qualifiers');
            const data = {
                'Roofing': [{l:'Roof Age', o:['1-10', '11-20', '20+']}, {l:'Material', o:['Shingle', 'Metal', 'Flat']}],
                'Solar': [{l:'Monthly Bill', o:['$100-200', '$200-400', '$400+']}, {l:'Credit Score', o:['650+', 'Below 650']}],
                'Kitchen': [{l:'Cabinet Status', o:['Reface', 'Replace']}, {l:'Budget', o:['$5k-15k', '$15k+']}]
            };
            const current = data[svc] || [{l:'Timeline', o:['Immediate', '1 Month+', 'Researching']}];
            container.innerHTML = current.map((q, i) => `
                <label class="text-[9px] font-black text-slate-400 uppercase tracking-widest mt-3 block italic">${q.l}</label>
                <select id="q_${i}" class="input-pro mb-2">${q.o.map(o=>`<option value="${o}">${o}</option>`).join('')}</select>
            `).join('');
        }
        updateQualifiers();

        // CHAT LOGIC (2-WAY)
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        function sendMsg() {
            const txt = document.getElementById('chat-input').value;
            if(!txt) return;
            const msgObj = { text: txt, sender: userId, time: new Date().toLocaleTimeString(), type: 'user' };
            db.ref('chats/' + userId).push(msgObj);
            document.getElementById('chat-input').value = '';
        }

        // LISTEN FOR REPLIES
        db.ref('chats/' + userId).on('value', snap => {
            const messages = snap.val();
            let h = '';
            for(let k in messages) {
                const m = messages[k];
                h += `<div class="bubble ${m.type === 'user' ? 'bubble-user' : 'bubble-admin'}">${m.text}</div>`;
            }
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // FORM SUBMISSION
        document.getElementById('mainLeadForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const rid = Math.floor(1000 + Math.random() * 9000);
            const lead = {
                id: rid, name: document.getElementById('custName').value,
                phone: document.getElementById('custPhone').value,
                svc: document.getElementById('custSvc').value,
                addr: document.getElementById('custAddr').value,
                q: document.getElementById('q_0')?.value || 'N/A',
                time: new Date().toLocaleString()
            };
            db.ref('leads').push(lead).then(() => {
                document.getElementById('mainLeadForm').classList.add('hidden');
                document.getElementById('refCode').innerText = rid;
                document.getElementById('formSuccess').classList.remove('hidden');
            });
        });

        // ADMIN TERMINAL LOGIC
        let taps = 0, tapT;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } clearTimeout(tapT); tapT=setTimeout(()=>taps=0,2000); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        let activeChatUser = '';
        function syncAdmin() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) h += `<div class="p-6 bg-slate-50 border rounded-3xl relative mb-4">
                    <span class="absolute top-4 right-4 bg-blue-600 text-white px-3 py-1 rounded-full text-[8px] font-black uppercase">${leads[k].svc}</span>
                    <h4 class="font-black text-blue-900 mb-1 italic">${leads[k].name}</h4>
                    <p class="text-[9px] font-bold text-slate-500 uppercase tracking-tighter">📞 ${leads[k].phone} | 📍 ${leads[k].addr} | 🛠 Q: ${leads[k].q}</p>
                    <button onclick="delItem('leads/${k}')" class="mt-4 text-red-500 font-black text-[9px] uppercase">Erase Lead</button>
                </div>`;
                document.getElementById('adminLeads').innerHTML = h || 'No Active Leads';
            });

            db.ref('chats').on('value', snap => {
                const chats = snap.val(); let h = '';
                for(let uid in chats) {
                    const lastMsg = Object.values(chats[uid]).pop();
                    h += `<div class="p-4 border rounded-2xl bg-white flex justify-between items-center mb-2 shadow-sm">
                        <div onclick="openReply('${uid}')" class="cursor-pointer">
                            <p class="text-[10px] font-black text-blue-600">ID: ${uid}</p>
                            <p class="text-[11px] font-bold text-slate-700 italic">"${lastMsg.text}"</p>
                        </div>
                        <button onclick="delItem('chats/${uid}')" class="text-red-300">✕</button>
                    </div>`;
                }
                document.getElementById('adminChats').innerHTML = h || 'No Messages';
            });
        }

        function openReply(uid) {
            activeChatUser = uid;
            document.getElementById('replyBox').classList.remove('hidden');
            document.getElementById('replyTo').innerText = uid;
        }

        function sendAdminReply() {
            const txt = document.getElementById('adminReplyText').value;
            if(!txt || !activeChatUser) return;
            db.ref('chats/' + activeChatUser).push({ text: txt, type: 'admin', time: new Date().toLocaleTimeString() });
            document.getElementById('adminReplyText').value = '';
            alert("Reply sent to user's screen!");
        }

        function delItem(path) { if(confirm('Delete record?')) db.ref(path).remove(); }

        // LIVE SOCIAL PROOF
        const nms = ["Robert", "Sarah", "Kevin", "Emily", "Jason", "Linda"];
        const cts = ["Miami", "Houston", "Phoenix", "Chicago", "Atlanta"];
        setInterval(() => {
            const t = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = "🔥 " + nms[Math.floor(Math.random()*nms.length)] + " from " + cts[Math.floor(Math.random()*cts.length)] + " authorized a survey!";
            t.style.display = 'flex';
            setTimeout(() => t.style.display = 'none', 6000);
        }, 15000);
    </script>
</body>
</html>
