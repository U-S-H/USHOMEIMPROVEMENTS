<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Authority Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; --emerald: #10b981; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #1e293b; scroll-behavior: smooth; }
        .hero-v4 { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.9)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
        .glass-nav { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(25px); border-bottom: 1px solid #f1f5f9; }
        
        .input-pro { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; font-size: 14px; background: #fff; }
        .input-pro:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        
        .btn-elite { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px 36px; border-radius: 20px; font-weight: 800; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; border: none; transition: 0.4s; box-shadow: 0 15px 35px rgba(37, 99, 235, 0.25); width: 100%; }
        .btn-elite:hover { transform: translateY(-4px); box-shadow: 0 20px 45px rgba(37, 99, 235, 0.35); }

        .page-section { display: none; }
        .page-section.active { display: block; animation: contentReveal 0.8s cubic-bezier(0.2, 1, 0.2, 1); }
        @keyframes contentReveal { from { opacity: 0; transform: scale(0.98) translateY(20px); } to { opacity: 1; transform: scale(1) translateY(0); } }

        /* Multi-Step Wizard */
        .step-container { display: none; }
        .step-container.active { display: block; animation: fadeIn 0.4s ease; }
        .progress-dot { width: 12px; height: 12px; border-radius: 50%; background: #e2e8f0; transition: 0.4s; }
        .progress-dot.active { background: var(--accent); transform: scale(1.3); box-shadow: 0 0 15px rgba(37, 99, 235, 0.4); }

        /* Chat Terminal UI */
        #chat-window { position: fixed; bottom: 110px; right: 30px; width: 380px; height: 580px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 6000; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 25px; color: white; display: flex; align-items: center; gap: 15px; }
        #chat-feed { flex: 1; padding: 25px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 14px 20px; border-radius: 22px; font-size: 13px; max-width: 85%; font-weight: 600; line-height: 1.5; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; box-shadow: 0 5px 15px rgba(0,0,0,0.05); }

        .project-card { background: white; border: 1px solid #f1f5f9; padding: 30px; border-radius: 35px; transition: 0.4s; cursor: pointer; text-align: center; }
        .project-card:hover { transform: translateY(-10px); border-color: var(--accent); box-shadow: 0 25px 50px -12px rgba(0,0,0,0.08); }
    </style>
</head>
<body>

    <nav class="glass-nav sticky top-0 z-[5000] px-10 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <img src="logo.png" onclick="handleAdminTap()" class="h-14 w-14 bg-white border-2 rounded-2xl shadow-sm cursor-pointer" onerror="this.src='https://ui-avatars.com/api/?name=US&background=0f172a&color=fff'">
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase leading-none tracking-tight">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic tracking-tighter">● National Enterprise Dispatch</span>
            </div>
        </div>
        <div class="hidden lg:flex gap-10 text-[10px] font-black uppercase tracking-[0.2em] text-slate-400">
            <button onclick="showPage('home')" class="hover:text-blue-600">Home</button>
            <button onclick="showPage('projects')" class="hover:text-blue-600">Projects</button>
            <button onclick="showPage('faq')" class="hover:text-blue-600">FAQ</button>
            <button onclick="showStep(1); showPage('form')" class="bg-blue-600 text-white px-8 py-3.5 rounded-full shadow-xl shadow-blue-100">Start Estimate</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="w-3 h-3 bg-emerald-500 rounded-full animate-pulse shadow-[0_0_10px_#10b981]"></div>
                <div><h4 class="font-black uppercase text-[11px] tracking-widest">Master Agent: Dispatch-786</h4><p class="text-[9px] opacity-70 italic">Secure Signal Established</p></div>
                <button onclick="toggleChat()" class="ml-auto text-xl">✕</button>
            </div>
            <div id="chat-feed">
                <div class="bubble bubble-admin">Welcome to U.S. Home Improvement. <br><br>I am Agent-786. How can I assist you with your property assessment today?</div>
            </div>
            <div class="p-6 border-t bg-white flex gap-3">
                <input type="text" id="chat-input" placeholder="Type secure message..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-10 right-10 w-16 h-16 bg-slate-950 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[5500] hover:scale-110 transition ring-8 ring-white/5">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-v4 py-64 px-6 text-center text-white">
            <div class="max-w-6xl mx-auto">
                <span class="inline-block px-6 py-2 rounded-full border border-blue-500/30 bg-blue-600/10 text-[11px] font-black uppercase tracking-[0.4em] text-blue-400 mb-10 italic">Certified National Infrastructure Partner</span>
                <h1 class="text-7xl md:text-[10rem] font-black uppercase italic leading-[0.8] tracking-tighter mb-16">Build <br><span class="text-blue-500">Greater</span>.</h1>
                <p class="max-w-xl mx-auto text-blue-100 font-bold text-xs uppercase tracking-[0.5em] mb-20 leading-loose opacity-80">Elite Site Assessments & National Contractor Coordination Across 50 States.</p>
                <div class="flex flex-wrap justify-center gap-8">
                    <button onclick="showStep(1); showPage('form')" class="btn-elite max-w-[350px]">Initiate Authorization</button>
                    <button onclick="showPage('projects')" class="bg-white/5 border border-white/20 px-12 py-5 rounded-2xl font-black uppercase text-xs hover:bg-white/10 transition backdrop-blur-md">View All Projects</button>
                </div>
            </div>
        </header>

        <div class="bg-white py-24 border-b">
            <div class="max-w-7xl mx-auto px-8 flex flex-wrap justify-center gap-20 opacity-40 grayscale hover:grayscale-0 transition-all duration-700">
                <img src="https://upload.wikimedia.org/wikipedia/commons/a/a2/Better_Business_Bureau_logo.svg" class="h-10">
                <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Forbes_logo.svg" class="h-10">
                <img src="https://upload.wikimedia.org/wikipedia/commons/3/39/Bloomberg_Logo.svg" class="h-10">
            </div>
        </div>
    </section>

    <section id="projects" class="page-section py-24 bg-slate-50 px-8">
        <div class="max-w-7xl mx-auto">
            <div class="text-center mb-20">
                <h2 class="text-5xl font-black uppercase italic text-slate-900 tracking-tighter mb-4">Enterprise <span class="text-blue-600">Portfolio</span></h2>
                <p class="text-[10px] font-black uppercase text-slate-400 tracking-[0.3em]">Authorized Service Capabilities</p>
            </div>
            <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-10">
                <script>
                    const projects = ["Windows Upgrade", "Roofing Systems", "Solar Power", "Luxury Kitchens", "Modern Bathrooms", "Seamless Gutters", "HVAC Systems", "Home Insulation", "Premium Siding", "Custom Pools", "Decks & Patios", "Smart Home Tech", "Garage Systems", "Security Matrix", "Interior Paint", "Premium Flooring", "Basement Finish", "Landscaping", "Fence Install", "Stone Work"];
                    projects.forEach(p => {
                        document.write(`<div class="project-card" onclick="showStep(1); showPage('form')">
                            <div class="w-14 h-14 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center mx-auto mb-6 text-xl font-black">★</div>
                            <h4 class="font-black text-slate-900 uppercase italic text-[13px] mb-2">${p}</h4>
                            <p class="text-[9px] font-bold text-slate-400 uppercase tracking-widest">Certified Dispatch</p>
                        </div>`);
                    });
                </script>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-24 bg-white">
        <div class="max-w-3xl mx-auto px-6">
            <div class="bg-white p-14 rounded-[50px] shadow-2xl border-2 border-slate-50 relative">
                
                <div class="flex justify-center gap-4 mb-14">
                    <div class="progress-dot" id="dot-1"></div>
                    <div class="progress-dot" id="dot-2"></div>
                    <div class="progress-dot" id="dot-3"></div>
                </div>

                <form id="ultimateForm">
                    <div class="step-container active" id="step-1">
                        <h3 class="text-3xl font-black uppercase italic text-slate-900 mb-8 tracking-tighter">Step 1: Project <span class="text-blue-600">Selection</span></h3>
                        <div class="space-y-6">
                            <select id="vSvc" class="input-pro" required>
                                <option value="">Select Service Portfolio</option>
                                <script>projects.forEach(p => document.write(`<option value="${p}">${p}</option>`));</script>
                            </select>
                            <select id="vOwn" class="input-pro" required>
                                <option value="">Do you own the property?</option>
                                <option value="Yes">Yes, I am the owner</option>
                                <option value="No">No, I am a tenant</option>
                            </select>
                            <select id="vProp" class="input-pro" required>
                                <option value="">Property Classification</option>
                                <option value="Single Family">Single Family Home</option>
                                <option value="Commercial">Commercial Property</option>
                                <option value="Multi-Unit">Multi-Unit Complex</option>
                            </select>
                            <button type="button" onclick="showStep(2)" class="btn-elite mt-6">Next Phase</button>
                        </div>
                    </div>

                    <div class="step-container" id="step-2">
                        <h3 class="text-3xl font-black uppercase italic text-slate-900 mb-8 tracking-tighter">Step 2: Legal <span class="text-blue-600">Identification</span></h3>
                        <div class="space-y-6">
                            <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro" required>
                            <input type="tel" id="vPhone" placeholder="Primary Mobile" class="input-pro" required>
                            <input type="email" id="vEmail" placeholder="Email Address" class="input-pro" required>
                            <div class="flex gap-4">
                                <button type="button" onclick="showStep(1)" class="w-1/3 bg-slate-100 py-5 rounded-20 font-black uppercase text-[10px]">Back</button>
                                <button type="button" onclick="showStep(3)" class="w-2/3 btn-elite">Next Phase</button>
                            </div>
                        </div>
                    </div>

                    <div class="step-container" id="step-3">
                        <h3 class="text-3xl font-black uppercase italic text-slate-900 mb-8 tracking-tighter">Step 3: Site <span class="text-blue-600">Logistics</span></h3>
                        <div class="space-y-6">
                            <input type="text" id="vAddr" placeholder="Physical Property Address" class="input-pro" required>
                            <div class="grid grid-cols-2 gap-4">
                                <input type="date" id="vDate" class="input-pro" required>
                                <select id="vTime" class="input-pro" required>
                                    <option value="">Preferred Time</option>
                                    <option value="10:00 AM">10:00 AM</option>
                                    <option value="02:00 PM">02:00 PM</option>
                                    <option value="06:00 PM">06:00 PM</option>
                                </select>
                            </div>
                            <select id="vCredit" class="input-pro" required>
                                <option value="">Estimated Credit Score</option>
                                <option value="720+">Excellent (720+)</option>
                                <option value="660-719">Good (660-719)</option>
                                <option value="Below 660">Building Credit</option>
                            </select>
                            <div class="flex gap-4">
                                <button type="button" onclick="showStep(2)" class="w-1/3 bg-slate-100 py-5 rounded-20 font-black uppercase text-[10px]">Back</button>
                                <button type="submit" class="w-2/3 btn-elite">Authorize & Transmit</button>
                            </div>
                        </div>
                    </div>
                </form>

                <div id="successScreen" class="hidden text-center py-10">
                    <div class="text-8xl mb-8">🎖️</div>
                    <h3 class="text-3xl font-black uppercase italic text-slate-900">Authorization Transmitted</h3>
                    <div class="bg-slate-950 text-white p-10 rounded-[45px] my-10 text-left border-4 border-blue-600 shadow-2xl">
                        <p class="text-[10px] font-black text-blue-500 uppercase mb-8 tracking-widest text-center">--- Official Terminal Receipt ---</p>
                        <div class="space-y-4 text-[11px] font-bold uppercase">
                            <p class="flex justify-between border-b border-white/10 pb-2"><span>Tracking ID:</span> <span id="rTid" class="text-emerald-400"></span></p>
                            <p class="flex justify-between border-b border-white/10 pb-2"><span>Customer:</span> <span id="rName"></span></p>
                            <p class="flex justify-between border-b border-white/10 pb-2"><span>Project:</span> <span id="rSvc"></span></p>
                            <p class="flex justify-between border-b border-white/10 pb-2"><span>Site:</span> <span id="rLoc" class="text-right max-w-[150px]"></span></p>
                        </div>
                    </div>
                    <p class="text-[10px] font-black text-slate-400 uppercase italic mb-10">Please screenshot this official document for your records.</p>
                    <button onclick="location.reload()" class="text-blue-600 font-black text-[11px] uppercase underline tracking-widest">Return Home</button>
                </div>
            </div>
        </div>
    </section>

    <section id="faq" class="page-section py-24 bg-slate-50 px-8">
        <div class="max-w-4xl mx-auto">
            <h2 class="text-4xl font-black uppercase italic text-center mb-20 tracking-tighter">Security & <span class="text-blue-600">Compliance</span></h2>
            <div class="grid gap-6">
                <div class="bg-white p-10 rounded-3xl border border-slate-100">
                    <h4 class="font-black text-xs text-blue-600 uppercase mb-4 italic tracking-widest">How does the National Hub work?</h4>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-loose">We coordinate between your property data and our network of local, licensed, and bonded contractors. Once authorized, a specialist will call you for final confirmation.</p>
                </div>
                <div class="bg-white p-10 rounded-3xl border border-slate-100">
                    <h4 class="font-black text-xs text-blue-600 uppercase mb-4 italic tracking-widest">Is my data encrypted?</h4>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-loose">Yes. All transmissions utilize AES 256-bit military-grade encryption. We are fully compliant with National Data Privacy standards.</p>
                </div>
            </div>
        </div>
    </section>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-16 border-b-2 pb-10">
                <div>
                    <h3 class="text-3xl font-black uppercase italic text-slate-900">National <span class="text-blue-600">Master</span> Terminal</h3>
                    <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mt-2">Enterprise Analytics & Dispatch Matrix</p>
                </div>
                <div class="flex gap-4">
                    <button onclick="exportToExcel()" class="bg-emerald-50 text-emerald-600 px-8 py-4 rounded-full font-black text-[10px] uppercase border border-emerald-200">Export All Leads</button>
                    <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-8 py-4 rounded-full font-black text-[10px] uppercase">Exit Hub</button>
                </div>
            </div>
            
            <div id="authBox" class="text-center py-40">
                <input type="password" id="pin" class="input-pro max-w-[300px] text-center text-5xl mb-10 shadow-2xl" placeholder="••••">
                <br>
                <button onclick="unlock()" class="btn-elite max-w-[300px]">Authorize Access</button>
            </div>
            
            <div id="hubData" class="hidden">
                <div class="grid md:grid-cols-3 gap-10 mb-16 text-center">
                    <div class="bg-slate-900 text-white p-10 rounded-[40px] shadow-xl"><h3 id="statLeads" class="text-5xl font-black italic mb-2">0</h3><p class="text-[9px] font-black uppercase tracking-widest opacity-60">Total Dispatches</p></div>
                    <div class="bg-blue-600 text-white p-10 rounded-[40px] shadow-xl"><h3 id="statChats" class="text-5xl font-black italic mb-2">0</h3><p class="text-[9px] font-black uppercase tracking-widest opacity-60">Active Signals</p></div>
                    <div class="bg-emerald-500 text-white p-10 rounded-[40px] shadow-xl"><h3 class="text-5xl font-black italic mb-2">Active</h3><p class="text-[9px] font-black uppercase tracking-widest opacity-60">System Status</p></div>
                </div>

                <div class="grid lg:grid-cols-3 gap-16">
                    <div class="lg:col-span-2"><h5 class="font-black uppercase text-xs text-slate-400 mb-10 italic">Dispatch Feed</h5><div id="adminLeads" class="space-y-6"></div></div>
                    <div>
                        <h5 class="font-black uppercase text-xs text-slate-400 mb-10 italic">Signal Stream</h5>
                        <div id="adminChats" class="space-y-4"></div>
                        <div id="replyArea" class="hidden mt-10 bg-slate-50 p-10 rounded-[45px] border border-slate-200 shadow-inner">
                            <div class="flex justify-between items-center mb-6">
                                <p class="text-[10px] font-black text-blue-600 uppercase">Signal: <span id="targetId"></span></p>
                                <button onclick="clearUserChat()" class="text-red-500 font-black text-[9px] uppercase hover:underline">Clear Entire Chat</button>
                            </div>
                            <input type="text" id="adminReplyText" class="input-pro mb-4" placeholder="Type transmission...">
                            <button onclick="sendAdminReply()" class="btn-elite text-[10px]">Transmit Signal</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <footer class="bg-slate-950 text-white py-32 px-8 text-center border-t border-white/5">
        <img src="logo.png" class="h-14 mx-auto mb-12 opacity-50 grayscale hover:grayscale-0 transition duration-700" onerror="this.src='https://ui-avatars.com/api/?name=US&background=333&color=fff'">
        <p class="text-[13px] font-black uppercase tracking-[0.5em] text-blue-500 mb-10 italic">National Enterprise HQ</p>
        <p class="text-[10px] font-bold text-slate-600 uppercase max-w-2xl mx-auto leading-loose mb-16 tracking-widest">702 Main Street, Woodland, CA 95695 | Authorized Terminal | Data Encrypted via SSL-256 AES Encryption | CCPA & TCPA Compliant Network</p>
        <div class="flex justify-center gap-12 text-[10px] font-black text-slate-800 uppercase tracking-widest">
            <span>© 2026 U.S. Home Improvement</span><span>●</span><span>Authorized Access Only</span>
        </div>
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
        const userId = "SIG-TX-" + Math.floor(100000 + Math.random() * 899999);

        // UI Logic
        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo({top:0, behavior:'smooth'}); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        function showStep(s) {
            document.querySelectorAll('.step-container').forEach(c => c.classList.remove('active'));
            document.querySelectorAll('.progress-dot').forEach(d => d.classList.remove('active'));
            document.getElementById('step-' + s).classList.add('active');
            for(let i=1; i<=s; i++) document.getElementById('dot-' + i).classList.add('active');
        }

        // Chat Engine
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

        // Form Submission
        document.getElementById('ultimateForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-NAT-" + Math.floor(1000000 + Math.random() * 8999999);
            const data = {
                tid: tid, name: document.getElementById('vName').value, email: document.getElementById('vEmail').value,
                phone: document.getElementById('vPhone').value, svc: document.getElementById('vSvc').value,
                addr: document.getElementById('vAddr').value, prop: document.getElementById('vProp').value,
                own: document.getElementById('vOwn').value, credit: document.getElementById('vCredit').value,
                date: document.getElementById('vDate').value, time: document.getElementById('vTime').value,
                ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('ultimateForm').classList.add('hidden');
                document.getElementById('successScreen').classList.remove('hidden');
                document.getElementById('rTid').innerText = tid;
                document.getElementById('rName').innerText = data.name;
                document.getElementById('rSvc').innerText = data.svc;
                document.getElementById('rLoc').innerText = data.addr;
            });
        });

        // Master Admin Hub
        let taps = 0, tapT;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } clearTimeout(tapT); tapT=setTimeout(()=>taps=0,2000); }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncMasterHub(); } }

        let activeId = '';
        function syncMasterHub() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val() || {}; 
                document.getElementById('statLeads').innerText = Object.keys(leads).length;
                let h = '';
                for(let k in leads) h += `<div class="p-10 bg-slate-50 border-2 rounded-[40px] relative hover:border-blue-400 transition">
                    <span class="absolute top-8 right-8 bg-blue-600 text-white px-5 py-1.5 rounded-full text-[10px] font-black">${leads[k].tid}</span>
                    <h4 class="text-3xl font-black italic text-slate-900 mb-4">${leads[k].name}</h4>
                    <div class="grid md:grid-cols-2 gap-6 text-[11px] font-bold text-slate-500 uppercase italic">
                        <p>📞 ${leads[k].phone}</p><p>📧 ${leads[k].email}</p>
                        <p>📍 ${leads[k].addr}</p><p>🛠 ${leads[k].svc}</p>
                        <p>🏠 ${leads[k].prop} (Owner: ${leads[k].own})</p><p>📅 ${leads[k].date} @ ${leads[k].time}</p>
                    </div>
                    <button onclick="del('leads/${k}')" class="mt-8 text-red-500 font-black text-[10px] uppercase border-t pt-6 w-full text-center">Delete Dispatch Record</button>
                </div>`;
                document.getElementById('adminLeads').innerHTML = h || 'No Active Records.';
            });
            db.ref('chats').on('value', snap => {
                const chats = snap.val() || {};
                document.getElementById('statChats').innerText = Object.keys(chats).length;
                let h = '';
                for(let uid in chats) {
                    const last = Object.values(chats[uid]).pop();
                    h += `<div class="p-8 bg-white border rounded-[30px] flex justify-between items-center mb-4 shadow-sm cursor-pointer hover:border-blue-500" onclick="openReply('${uid}')">
                        <div><p class="text-[10px] font-black text-blue-600 uppercase tracking-widest">${uid}</p><p class="text-[13px] font-bold italic mt-1">"${last.text}"</p></div>
                    </div>`;
                }
                document.getElementById('adminChats').innerHTML = h || 'No Signals.';
            });
        }

        function openReply(uid) { activeId = uid; document.getElementById('replyArea').classList.remove('hidden'); document.getElementById('targetId').innerText = uid; }
        function sendAdminReply() {
            const txt = document.getElementById('adminReplyText').value; if(!txt || !activeId) return;
            db.ref('chats/' + activeId).push({ text: txt, type: 'admin', time: new Date().toLocaleTimeString() });
            document.getElementById('adminReplyText').value = '';
        }
        function clearUserChat() { if(confirm('Erase entire signal history?')) db.ref('chats/' + activeId).remove(); }
        function del(path) { if(confirm('Erase record permanently?')) db.ref(path).remove(); }
        function exportToExcel() {
            db.ref('leads').once('value', snap => {
                const data = Object.values(snap.val() || {});
                const ws = XLSX.utils.json_to_sheet(data);
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "Dispatches");
                XLSX.writeFile(wb, "US_Home_Improvements_Master_Leads.xlsx");
            });
        }
    </script>
</body>
</html>
