<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Authorized Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <style>
        :root { --brand: #0f172a; --accent: #2563eb; --safety: #10b981; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #1e293b; overflow-x: hidden; }
        .hero-matrix { background: linear-gradient(rgba(15, 23, 42, 0.98), rgba(15, 23, 42, 0.94)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
        .glass-ui { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(25px); border-bottom: 1px solid #f1f5f9; }
        .input-pro { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 24px; font-weight: 600; outline: none; transition: 0.4s; background: #fff; }
        .input-pro:focus { border-color: var(--accent); box-shadow: 0 0 0 6px rgba(37, 99, 235, 0.1); }
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 22px; border-radius: 24px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; transition: 0.4s; width: 100%; box-shadow: 0 12px 30px rgba(37, 99, 235, 0.25); }
        .btn-elite:hover { transform: translateY(-4px); box-shadow: 0 20px 45px rgba(37, 99, 235, 0.35); }
        .page-node { display: none; }
        .page-node.active { display: block; animation: nodeAppear 0.8s cubic-bezier(0.2, 1, 0.2, 1); }
        @keyframes nodeAppear { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        .secret-control { display: none; } /* HIDDEN BY DEFAULT */
        #chat-terminal { position: fixed; bottom: 100px; right: 30px; width: 370px; height: 580px; background: white; border-radius: 35px; box-shadow: 0 40px 80px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 6000; border: 1px solid #f1f5f9; }
        .scroll-hide::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-[5000] glass-ui px-10 py-6 flex justify-between items-center">
        <div class="flex items-center gap-5">
            <img src="logo.png" onclick="verifyAdminTap()" class="h-14 w-14 bg-white border rounded-2xl cursor-pointer shadow-sm hover:scale-105 transition" onerror="this.src='https://ui-avatars.com/api/?name=US&background=0f172a&color=fff'">
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase leading-none tracking-tight">U.S. Home Improvement LLC</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic tracking-tighter">● National Infrastructure Matrix</span>
            </div>
        </div>
        <div class="hidden lg:flex gap-12 text-[10px] font-black uppercase tracking-[0.2em] text-slate-400">
            <button onclick="showNode('home')" class="hover:text-blue-600">Home</button>
            <button onclick="showNode('services')" class="hover:text-blue-600">Portfolio</button>
            <button onclick="showNode('compliance')" class="hover:text-blue-600">Compliance</button>
            <button onclick="showNode('form')" class="bg-blue-600 text-white px-10 py-4 rounded-full shadow-2xl shadow-blue-200">Get Quote</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-terminal">
            <div class="bg-slate-900 p-7 text-white flex items-center gap-4">
                <div class="w-2 h-2 bg-emerald-500 rounded-full animate-pulse"></div>
                <div><h4 class="text-[11px] font-black uppercase tracking-widest leading-none">Agent ID: 786-Dispatch</h4><p class="text-[9px] opacity-60 mt-1 italic">Authorized Signal Link</p></div>
                <button onclick="toggleChat()" class="ml-auto text-xl">✕</button>
            </div>
            <div id="chat-feed" class="flex-1 p-7 overflow-y-auto bg-slate-50 flex flex-col gap-4 scroll-hide"></div>
            <div class="p-6 bg-white border-t flex gap-3">
                <input type="text" id="chat-in" placeholder="Transmit secure message..." class="flex-1 text-xs font-bold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-[11px] uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-10 right-10 w-16 h-16 bg-slate-950 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[5500] hover:rotate-12 transition">💬</button>
    </div>

    <section id="home" class="page-node active">
        <header class="hero-matrix py-64 px-8 text-center text-white">
            <div class="max-w-6xl mx-auto">
                <span class="inline-block px-6 py-2 rounded-full border border-blue-500/30 bg-blue-600/10 text-[11px] font-black uppercase tracking-[0.4em] text-blue-400 mb-10 italic">Certified National Infrastructure Partner</span>
                <h1 class="text-7xl md:text-[10rem] font-black uppercase italic leading-[0.85] tracking-tighter mb-16">The <span class="text-blue-500">Gold</span> <br>Standard.</h1>
                <p class="max-w-2xl mx-auto text-blue-100 font-bold text-xs uppercase tracking-[0.5em] mb-20 leading-loose opacity-70">U.S. Wide Site Assessments & Elite Remodeling Logistics Since 2012.</p>
                <div class="flex flex-wrap justify-center gap-8">
                    <button onclick="showNode('form')" class="btn-elite max-w-[360px]">Initiate Authorization</button>
                    <button onclick="showNode('services')" class="bg-white/10 border border-white/20 px-12 py-5 rounded-2xl font-black uppercase text-xs backdrop-blur hover:bg-white/20 transition">View Capabilities</button>
                </div>
            </div>
        </header>
    </section>

    <section id="services" class="page-node py-24 bg-slate-50 px-10">
        <div class="max-w-7xl mx-auto">
            <h2 class="text-5xl font-black uppercase italic text-center mb-20 tracking-tighter text-slate-900">National <span class="text-blue-600">Enterprise Feed</span></h2>
            <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
                <script>
                    const services = ["Roofing Systems", "Windows Matrix", "Solar Integration", "Kitchen Design", "Bath Sanctuary", "HVAC Climate", "Siding Shields", "Insulation Flow", "Security Grid", "Smart Tech", "Luxury Decks", "Hardscapes", "Basement Hub", "Garage Systems", "Fence Barriers", "Flooring Matrix", "Interior Paint", "Stone Craft", "Gutter Flow", "Poolscapes"];
                    services.forEach(s => document.write(`
                        <div onclick="showNode('form')" class="bg-white p-10 rounded-[40px] border border-slate-100 shadow-sm hover:shadow-2xl transition cursor-pointer group">
                            <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center mb-6 text-lg font-black group-hover:bg-blue-600 group-hover:text-white transition">★</div>
                            <h4 class="font-black text-slate-900 uppercase italic text-[13px] mb-2">${s}</h4>
                            <p class="text-[9px] font-bold text-slate-400 uppercase tracking-widest">Authorized Dispatch</p>
                        </div>
                    `));
                </script>
            </div>
        </div>
    </section>

    <section id="form" class="page-node py-24 bg-white px-8">
        <div class="max-w-3xl mx-auto bg-white p-16 rounded-[60px] shadow-2xl border-2 border-slate-50 relative">
            <form id="secureTerminal">
                <h3 class="text-3xl font-black uppercase italic mb-12 border-l-[12px] border-blue-600 pl-8 tracking-tighter">Site Assessment <br><span class="text-blue-600 text-xl tracking-widest">Terminal-A1</span></h3>
                
                <div class="grid md:grid-cols-2 gap-8 mb-8">
                    <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro" required>
                    <input type="email" id="vEmail" placeholder="Secure Email Address" class="input-pro" required>
                </div>
                <div class="grid md:grid-cols-2 gap-8 mb-8">
                    <input type="tel" id="vPhone" placeholder="Direct Mobile Signal" class="input-pro" required>
                    <select id="vSvc" class="input-pro" required>
                        <option value="">Select Service Node</option>
                        <script>services.forEach(s => document.write(`<option value="${s}">${s}</option>`));</script>
                    </select>
                </div>
                <div class="grid md:grid-cols-2 gap-8 mb-8">
                    <select id="vOwn" class="input-pro" required>
                        <option value="">Property Ownership?</option>
                        <option value="Yes">Yes, Primary Owner</option>
                        <option value="No">No, Tenant/Renter</option>
                    </select>
                    <select id="vCredit" class="input-pro" required>
                        <option value="">Est. Credit Health</option>
                        <option value="Excellent">Excellent (720+)</option>
                        <option value="Good">Good (660-719)</option>
                        <option value="Building">Building (Below 660)</option>
                    </select>
                </div>
                <input type="text" id="vAddr" placeholder="Physical Property Address" class="input-pro mb-12" required>
                
                <div class="bg-blue-50 p-8 rounded-[35px] border border-blue-100 mb-12">
                    <p class="text-[10px] font-black text-blue-900 uppercase mb-3">● Legal Transmission Disclosure</p>
                    <p class="text-[10px] font-bold text-blue-700 uppercase leading-relaxed italic">By submitting, you authorize U.S. Home Improvement to coordinate with a local licensed contractor. A mandatory verification call is required to finalize site access.</p>
                </div>

                <button type="submit" class="btn-elite">Transmit Data</button>
            </form>

            <div id="successNode" class="hidden text-center py-16">
                <div class="text-8xl mb-10">🛡️</div>
                <h3 class="text-4xl font-black uppercase italic text-slate-900 mb-8">Authorization Transmitted</h3>
                <div class="bg-slate-950 text-white p-12 rounded-[50px] my-12 text-left border-t-[10px] border-blue-600 shadow-3xl">
                    <p class="text-[10px] font-black text-blue-500 uppercase mb-8 text-center tracking-[0.4em]">-- OFFICIAL TERMINAL RECEIPT --</p>
                    <div class="space-y-4 text-[11px] font-bold uppercase italic">
                        <p class="flex justify-between border-b border-white/10 pb-3"><span>Tracking ID:</span> <span id="rTid" class="text-emerald-400 font-black"></span></p>
                        <p class="flex justify-between border-b border-white/10 pb-3"><span>Asset:</span> <span id="rName"></span></p>
                        <p class="flex justify-between border-b border-white/10 pb-3"><span>Capability:</span> <span id="rSvc"></span></p>
                    </div>
                </div>
                <button onclick="location.reload()" class="text-blue-600 font-black text-[11px] uppercase underline tracking-widest">Return to Home</button>
            </div>
        </div>
    </section>

    <section id="compliance" class="page-node py-24 px-10 bg-slate-900 text-white">
        <div class="max-w-5xl mx-auto grid lg:grid-cols-2 gap-20 items-center">
            <div>
                <h3 class="text-4xl font-black uppercase italic mb-10 tracking-tighter">Security <br><span class="text-blue-600">& Privacy Matrix</span></h3>
                <p class="text-[12px] font-bold text-slate-400 uppercase leading-loose mb-8">We utilize AES-256 military grade encryption for all data transmissions. U.S. Home Improvement LLC is fully compliant with TCPA, CCPA, and GDPR data security frameworks.</p>
                <div class="flex gap-6 opacity-40">
                    <div class="px-6 py-2 border rounded-full text-[9px] font-black uppercase">SSL-SECURE</div>
                    <div class="px-6 py-2 border rounded-full text-[9px] font-black uppercase">TRUST-PASS</div>
                </div>
            </div>
            <div class="bg-slate-950 p-12 rounded-[50px] border border-white/5">
                <h5 class="text-blue-500 font-black uppercase text-xs mb-6 italic">Privacy Policy</h5>
                <p class="text-[10px] text-slate-500 uppercase font-bold leading-relaxed mb-8">Your data is never sold to third-party marketing firms. It is exclusively used to connect your property with a verified contractor in the National Infrastructure Hub.</p>
                <p class="text-[10px] text-slate-500 uppercase font-bold leading-relaxed">By providing your phone number, you consent to receive SMS/Call signals regarding your project status.</p>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-16 border-b-2 pb-12">
                <div>
                    <h3 class="text-4xl font-black uppercase italic text-slate-900">National <span class="text-blue-600">Master Hub</span></h3>
                    <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mt-2 italic">Enterprise Dispatch Matrix 2.0</p>
                </div>
                <div class="flex gap-4">
                    <button id="exBtn" onclick="exportExcel()" class="secret-control bg-emerald-50 text-emerald-600 px-10 py-4 rounded-full font-black text-[10px] uppercase border border-emerald-100">Export All Data</button>
                    <button onclick="exitAdmin()" class="bg-red-50 text-red-500 px-10 py-4 rounded-full font-black text-[10px] uppercase">Kill Session</button>
                </div>
            </div>

            <div id="authBox" class="text-center py-48">
                <input type="password" id="pin" class="input-pro max-w-[320px] text-center text-5xl mb-12 shadow-3xl" placeholder="••••">
                <br><button onclick="authorize()" class="btn-elite max-w-[320px]">Establish Connection</button>
            </div>

            <div id="hubView" class="hidden">
                <div class="grid md:grid-cols-3 gap-10 mb-20 text-center">
                    <div class="bg-slate-900 text-white p-12 rounded-[50px] shadow-2xl"><h3 id="statL" class="text-6xl font-black italic">0</h3><p class="text-[10px] uppercase font-black opacity-50 tracking-widest">Total Dispatches</p></div>
                    <div class="bg-blue-600 text-white p-12 rounded-[50px] shadow-2xl"><h3 id="statC" class="text-6xl font-black italic">0</h3><p class="text-[10px] uppercase font-black opacity-50 tracking-widest">Active Signals</p></div>
                    <div class="bg-emerald-500 text-white p-12 rounded-[50px] shadow-2xl"><h3 class="text-5xl font-black italic">ONLINE</h3><p class="text-[10px] uppercase font-black opacity-50 tracking-widest">System Link</p></div>
                </div>

                <div class="grid lg:grid-cols-2 gap-20">
                    <div id="adminLeads" class="space-y-6"></div>
                    <div>
                        <div id="adminChats" class="space-y-5"></div>
                        <div id="repHub" class="hidden mt-12 bg-slate-50 p-12 rounded-[55px] border shadow-inner">
                            <div class="flex justify-between items-center mb-8">
                                <p class="text-[11px] font-black text-blue-600 uppercase">Target Signal: <span id="targetId"></span></p>
                                <button id="wipeBtn" onclick="wipeChat()" class="secret-control text-red-500 font-black text-[9px] uppercase border-b border-red-200">Wipe History</button>
                            </div>
                            <input type="text" id="adminRep" class="input-pro mb-6" placeholder="Transmit reply...">
                            <button onclick="sendAdminRep()" class="btn-elite text-[12px]">Push Signal</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <footer class="bg-slate-950 text-white py-32 px-10 text-center border-t border-white/5">
        <img src="logo.png" class="h-14 mx-auto mb-12 opacity-40 grayscale hover:grayscale-0 transition duration-700" onerror="this.src='https://ui-avatars.com/api/?name=US&background=333&color=fff'">
        <p class="text-[13px] font-black uppercase tracking-[0.5em] text-blue-500 mb-8 italic">National Infrastructure Headquarters</p>
        <p class="text-[10px] font-bold text-slate-500 uppercase max-w-2xl mx-auto leading-loose mb-16 tracking-[0.2em]">702 Main Street, Woodland, CA 95695 | Authorized Terminal Access | Data Encrypted via SSL-256 AES | Licensed & Bonded Network Coordination</p>
        <div class="flex flex-wrap justify-center gap-12 text-[9px] font-black text-slate-800 uppercase tracking-widest">
            <span>© 2026 U.S. HOME IMPROVEMENT LLC</span><span>●</span><span>TCPA COMPLIANT</span><span>●</span><span>GDPR SECURED</span>
        </div>
    </footer>

    <script>
        // FIREBASE MASTER CONFIG
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
        const nodeUid = "TX-" + Math.floor(100000 + Math.random() * 899999);

        // UI NAVIGATION
        function showNode(id) { document.querySelectorAll('.page-node').forEach(n=>n.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo({top:0, behavior:'smooth'}); }
        function toggleChat() { const w = document.getElementById('chat-terminal'); w.style.display = (w.style.display==='flex'?'none':'flex'); }

        // LIVE CHAT LOGIC
        function sendMsg() {
            const t = document.getElementById('chat-in').value; if(!t) return;
            db.ref('chats/'+nodeUid).push({ text: t, type: 'user', time: new Date().toLocaleTimeString() });
            document.getElementById('chat-in').value = '';
        }
        db.ref('chats/'+nodeUid).on('value', s => {
            const m = s.val(); let h = '';
            for(let k in m) h += `<div class="p-4 rounded-2xl text-[12px] font-bold ${m[k].type==='user'?'bg-blue-600 text-white self-end':'bg-white border self-start shadow-sm'}">${m[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = 99999;
        });

        // DATA SUBMISSION
        document.getElementById('secureTerminal').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-NAT-" + Math.floor(1000000 + Math.random() * 8999999);
            const d = { tid: tid, name: document.getElementById('vName').value, email: document.getElementById('vEmail').value, phone: document.getElementById('vPhone').value, svc: document.getElementById('vSvc').value, own: document.getElementById('vOwn').value, credit: document.getElementById('vCredit').value, addr: document.getElementById('vAddr').value, ts: new Date().toLocaleString() };
            db.ref('leads').push(d).then(() => {
                document.getElementById('secureTerminal').classList.add('hidden');
                document.getElementById('successNode').classList.remove('hidden');
                document.getElementById('rTid').innerText = tid;
                document.getElementById('rName').innerText = d.name;
                document.getElementById('rSvc').innerText = d.svc;
            });
        });

        // ADMIN TERMINAL LOGIC (SECURE)
        let taps = 0, tapT;
        function verifyAdminTap() { taps++; if(taps>=5) { document.getElementById('adminHub').classList.remove('hidden'); taps=0; } clearTimeout(tapT); tapT=setTimeout(()=>taps=0,2000); }
        function exitAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function authorize() { 
            if(document.getElementById('pin').value === "786") { 
                document.getElementById('authBox').classList.add('hidden'); 
                document.getElementById('hubView').classList.remove('hidden');
                document.querySelectorAll('.secret-control').forEach(el => el.style.display = 'block'); // SHOW HIDDEN CONTROLS
                syncMaster(); 
            } else { alert('ACCESS DENIED'); }
        }

        let targetSignal = '';
        function syncMaster() {
            db.ref('leads').on('value', s => {
                const l = s.val(); let h = '';
                document.getElementById('statL').innerText = Object.keys(l||{}).length;
                for(let k in l) h += `<div class="p-10 bg-slate-50 border rounded-[40px] relative hover:border-blue-400 transition shadow-sm"><span class="absolute top-6 right-6 text-[9px] font-black text-blue-600 uppercase">${l[k].tid}</span><h4 class="text-2xl font-black italic text-slate-900 mb-3">${l[k].name}</h4><div class="grid md:grid-cols-2 gap-4 text-[10px] font-bold text-slate-500 uppercase italic"><p>📞 ${l[k].phone}</p><p>📧 ${l[k].email}</p><p>📍 ${l[k].addr}</p><p>🛠 ${l[k].svc} | ${l[k].credit}</p></div><button onclick="del('leads/${k}')" class="mt-8 text-red-500 font-black text-[9px] uppercase border-t pt-4 w-full">Delete Record</button></div>`;
                document.getElementById('adminLeads').innerHTML = h || 'Terminal Clear.';
            });
            db.ref('chats').on('value', s => {
                const c = s.val(); let h = '';
                document.getElementById('statC').innerText = Object.keys(c||{}).length;
                for(let u in c) h += `<div onclick="openSignal('${u}')" class="p-6 bg-white border rounded-[30px] flex justify-between items-center cursor-pointer hover:border-blue-500 shadow-sm"><p class="text-[10px] font-black text-blue-600">${u}</p><span class="w-2 h-2 bg-emerald-500 rounded-full animate-pulse"></span></div>`;
                document.getElementById('adminChats').innerHTML = h || 'No Active Signals.';
            });
        }
        function openSignal(u) { targetSignal = u; document.getElementById('repHub').classList.remove('hidden'); document.getElementById('targetId').innerText = u; }
        function sendAdminRep() {
            const t = document.getElementById('adminRep').value; if(!t) return;
            db.ref('chats/'+targetSignal).push({ text: t, type: 'admin', time: new Date().toLocaleTimeString() });
            document.getElementById('adminRep').value = '';
        }
        function wipeChat() { if(confirm('Erase entire signal history?')) db.ref('chats/'+targetSignal).remove(); }
        function del(p) { if(confirm('Delete permanently?')) db.ref(p).remove(); }
        function exportExcel() {
            db.ref('leads').once('value', s => {
                const ws = XLSX.utils.json_to_sheet(Object.values(s.val()||{}));
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "MasterLeads");
                XLSX.writeFile(wb, "US_Home_Enterprise_Data.xlsx");
            });
        }
    </script>
</body>
</html>
