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
        :root { --primary: #0f172a; --accent: #2563eb; --gold: #fbbf24; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #1e293b; scroll-behavior: smooth; }
        
        /* UI Enhancements */
        .glass-header { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(15px); border-bottom: 1px solid rgba(0,0,0,0.05); }
        .hero-premium { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.85)), url('https://images.unsplash.com/photo-1560518883-ce09059eeffa?q=80&w=1973&auto=format&fit=crop'); background-size: cover; background-position: center; }
        .input-premium { width: 100%; padding: 18px; border: 2px solid #e2e8f0; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: white; }
        .input-premium:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 22px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; transition: 0.4s; box-shadow: 0 15px 35px rgba(37, 99, 235, 0.25); border: none; cursor: pointer; }
        
        /* Specialized Chat System */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 380px; height: 600px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 25px; color: white; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #fdfdfd; display: flex; flex-direction: column; gap: 15px; }
        .bubble { padding: 14px 20px; border-radius: 22px; font-size: 13px; max-width: 85%; line-height: 1.5; font-weight: 500; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .chat-option { background: white; border: 2px solid #2563eb; color: #2563eb; padding: 10px 15px; border-radius: 50px; font-size: 11px; font-weight: 800; text-transform: uppercase; cursor: pointer; transition: 0.3s; text-align: center; }
        .chat-option:hover { background: #2563eb; color: white; }
    </style>
</head>
<body>

    <nav class="glass-header sticky top-0 z-[8000] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <div onclick="handleAdminTap()" class="h-14 w-14 bg-slate-900 rounded-2xl flex items-center justify-center text-white font-black cursor-pointer shadow-xl">US</div>
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase tracking-tighter">U.S. Home Improvement</h1>
                <div class="flex items-center gap-2">
                    <span class="h-2 w-2 bg-emerald-500 rounded-full animate-pulse"></span>
                    <span class="text-[9px] font-bold text-slate-400 uppercase italic">Registered LLC & BBB Accredited</span>
                </div>
            </div>
        </div>
        <div class="hidden lg:flex gap-10 text-[10px] font-black uppercase tracking-[0.2em] text-slate-500">
            <button onclick="showPage('home')">Welcome</button>
            <button onclick="showPage('benefits')">Benefits</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-4 rounded-2xl shadow-lg">Start Project</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="flex items-center gap-4">
                    <div class="w-12 h-12 bg-blue-600 rounded-2xl flex items-center justify-center text-xl shadow-inner">🛡️</div>
                    <div>
                        <h4 class="font-black text-[12px] uppercase">Corporate Concierge</h4>
                        <p class="text-[9px] text-blue-400 font-bold uppercase tracking-widest">Status: Agent-786 Monitoring</p>
                    </div>
                </div>
            </div>
            <div id="chat-feed">
                <div class="bubble bubble-admin">Welcome to U.S. Home Improvement. I am your automated assistant. How can we serve your property today?</div>
                <div class="flex flex-col gap-2 mt-2" id="chat-options">
                    <button class="chat-option" onclick="chatAction('Pricing Info')">Pricing & Estimates</button>
                    <button class="chat-option" onclick="chatAction('Service Areas')">Check Service States</button>
                    <button class="chat-option" onclick="transferToLive()" style="border-color: #ef4444; color: #ef4444;">🚨 Transfer to Live Agent</button>
                </div>
            </div>
            <div class="p-5 border-t bg-white flex gap-3">
                <input type="text" id="chat-input" placeholder="Type detailed inquiry..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-20 h-20 bg-slate-900 rounded-3xl shadow-3xl flex items-center justify-center text-2xl z-[8500] hover:scale-110 transition">💬</button>
    </div>

    <section id="home" class="page-section active">
        <div class="hero-premium py-40 px-8 text-center text-white">
            <div class="max-w-4xl mx-auto">
                <span class="bg-blue-600/30 border border-blue-500 px-6 py-2 rounded-full text-[10px] font-black uppercase tracking-[0.3em] mb-10 inline-block">Established National Network</span>
                <h1 class="text-5xl md:text-8xl font-black uppercase italic tracking-tighter mb-12">Building Trust, <br><span class="text-blue-500">America.</span></h1>
                <p class="text-slate-300 text-sm font-medium leading-relaxed max-w-2xl mx-auto mb-16 uppercase tracking-widest">U.S. Home Improvement is a registered LLC nationwide service provider, connecting homeowners with BBB-Accredited contractors for high-end property upgrades.</p>
                <div class="flex flex-wrap justify-center gap-6">
                    <button onclick="showPage('form')" class="btn-master px-12">Initialize Survey</button>
                    <button onclick="showPage('benefits')" class="bg-white/10 backdrop-blur text-white px-12 py-5 rounded-2xl font-black text-[10px] uppercase border border-white/20">Our Benefits</button>
                </div>
            </div>
        </div>
    </section>

    <section id="benefits" class="page-section py-32 px-8 bg-white">
        <div class="max-w-7xl mx-auto">
            <div class="text-center mb-24">
                <h2 class="text-4xl font-black uppercase italic tracking-tighter text-slate-900">Why Homeowners <span class="text-blue-600">Choose Us</span></h2>
                <div class="h-1.5 w-24 bg-blue-600 mx-auto mt-6 rounded-full"></div>
            </div>
            <div class="grid md:grid-cols-3 gap-12">
                <div class="p-10 bg-slate-50 rounded-[40px] border border-slate-100">
                    <div class="text-4xl mb-6">✅</div>
                    <h4 class="font-black uppercase italic mb-4">Certified LLC</h4>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-loose">We operate as a legally registered entity, ensuring every project follows national building codes and safety regulations.</p>
                </div>
                <div class="p-10 bg-slate-50 rounded-[40px] border border-slate-100">
                    <div class="text-4xl mb-6">⭐️</div>
                    <h4 class="font-black uppercase italic mb-4">BBB Accredited</h4>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-loose">Maintaining an A+ network standard, we only dispatch contractors who meet our elite quality and reliability criteria.</p>
                </div>
                <div class="p-10 bg-slate-50 rounded-[40px] border border-slate-100">
                    <div class="text-4xl mb-6">🛡️</div>
                    <h4 class="font-black uppercase italic mb-4">Privacy First</h4>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-loose">Your data is secured under the CCPA & GDPR guidelines. We never sell your info to unauthorized third parties.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="form" class="page-section py-32 bg-slate-50">
        <div class="max-w-3xl mx-auto px-8">
            <div class="bg-white p-12 md:p-20 rounded-[60px] shadow-3xl border border-slate-100 relative">
                <form id="masterForm">
                    <div class="mb-12">
                        <h3 class="text-3xl font-black uppercase italic mb-2 text-slate-900">Official Survey</h3>
                        <p class="text-[10px] font-bold text-slate-400 uppercase italic">Enterprise Dispatch Qualification Terminal</p>
                    </div>

                    <div class="space-y-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-400 mb-3 block">Primary Property Service</label>
                            <select id="vSvc" class="input-premium" required>
                                <option value="">Select Service Architecture</option>
                                <option value="Windows">Windows (National Replacement)</option>
                                <option value="Roofing">Roofing (Complete System)</option>
                                <option value="Solar">Solar Energy Matrix</option>
                                <option value="HVAC">HVAC (High-Efficiency Heating/Air)</option>
                                <option value="Kitchen">Interior: Kitchen Luxury Remodel</option>
                                <option value="Bathroom">Interior: Premium Bathroom Spa</option>
                                <option value="Siding">Exterior: High-End Vinyl/Fiber Siding</option>
                                <option value="Garage">Garage Door Systems</option>
                                <option value="Flooring">Flooring: Hardwood/Tile/Carpet</option>
                                <option value="Security">Home Automation & Security</option>
                            </select>
                        </div>

                        <div class="grid md:grid-cols-2 gap-8">
                            <div>
                                <label class="text-[10px] font-black uppercase text-slate-400 mb-3 block">Legal Full Name</label>
                                <input type="text" id="vName" class="input-premium" placeholder="John Doe" required>
                            </div>
                            <div>
                                <label class="text-[10px] font-black uppercase text-slate-400 mb-3 block">Contact Number</label>
                                <input type="tel" id="vPhone" class="input-premium" placeholder="(555) 000-0000" required>
                            </div>
                        </div>

                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-400 mb-3 block">Property Ownership Status</label>
                            <select id="vOwner" class="input-premium" required>
                                <option value="">Are you the legal owner?</option>
                                <option value="Yes">Yes, Primary Owner</option>
                                <option value="No">No, Tenant/Other</option>
                            </select>
                        </div>

                        <button type="submit" class="btn-master w-full py-6 mt-10">Transmit to Dispatch</button>
                    </div>
                </form>

                <div id="vReceipt" class="hidden text-center">
                    <div class="w-24 h-24 bg-emerald-50 text-emerald-500 rounded-full flex items-center justify-center mx-auto mb-10 text-4xl">✓</div>
                    <h3 class="text-3xl font-black uppercase italic mb-10">Verification <span class="text-emerald-500">Authorized</span></h3>
                    <div id="receipt-data" class="bg-slate-900 text-white p-10 rounded-[40px] text-left text-[11px] font-bold uppercase space-y-4"></div>
                    <p class="text-[10px] font-bold text-slate-400 mt-10 uppercase italic leading-relaxed">A certified agent will contact you shortly to confirm the site inspection.</p>
                </div>
            </div>
        </div>
    </section>

    <footer class="bg-slate-900 text-white py-32 px-8">
        <div class="max-w-7xl mx-auto grid md:grid-cols-3 gap-20">
            <div>
                <h4 class="text-xl font-black uppercase italic mb-8">U.S. Home <span class="text-blue-500">Improvement</span></h4>
                <p class="text-[10px] font-bold text-slate-500 uppercase leading-relaxed">We are a registered nationwide network providing authorized property survey solutions for American homeowners.</p>
            </div>
            <div>
                <h4 class="text-xs font-black uppercase tracking-widest mb-8 text-blue-500">Accreditations</h4>
                <div class="flex gap-4 opacity-50">
                    <div class="px-4 py-2 border border-white rounded-lg text-[9px] font-black uppercase">BBB A+</div>
                    <div class="px-4 py-2 border border-white rounded-lg text-[9px] font-black uppercase">LLC Reg</div>
                    <div class="px-4 py-2 border border-white rounded-lg text-[9px] font-black uppercase">EPA Cert</div>
                </div>
            </div>
            <div>
                <h4 class="text-xs font-black uppercase tracking-widest mb-8 text-blue-500">Legal & Privacy</h4>
                <ul class="text-[9px] font-black uppercase text-slate-500 space-y-4">
                    <li><a href="#" onclick="showPage('legal')">Privacy Policy</a></li>
                    <li><a href="#" onclick="showPage('legal')">Terms of Service</a></li>
                    <li><a href="#" onclick="showPage('legal')">CCPA Data Rights</a></li>
                </ul>
            </div>
        </div>
        <div class="mt-24 pt-8 border-t border-white/5 text-center">
            <p class="text-[9px] font-bold text-slate-600 uppercase tracking-widest">© 2026 U.S. HOME IMPROVEMENT LLC. ALL RIGHTS RESERVED.</p>
        </div>
    </footer>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center border-b pb-10 mb-12">
                <h3 class="text-4xl font-black italic uppercase">Enterprise <span class="text-blue-600">Admin</span></h3>
                <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-8 py-3 rounded-full font-black text-[10px] uppercase">Close Terminal</button>
            </div>
            <div id="authBox" class="text-center py-32">
                <input type="password" id="pin" class="input-premium max-w-[300px] text-center text-4xl mb-8" placeholder="••••">
                <br><button onclick="unlock()" class="btn-master max-w-[300px]">Authorize Access</button>
            </div>
            <div id="hubData" class="hidden grid lg:grid-cols-2 gap-12">
                <div id="adminLeads"></div>
                <div id="adminChats"></div>
            </div>
        </div>
    </div>

    <script>
        // FIREBASE INFRASTRUCTURE
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const userId = "CLIENT-" + Math.floor(100000 + Math.random() * 899999);

        // NAVIGATION ENGINE
        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo({top:0, behavior:'smooth'}); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        
        // HYBRID CHAT LOGIC
        function chatAction(action) {
            const feed = document.getElementById('chat-feed');
            feed.innerHTML += `<div class="bubble bubble-user">${action}</div>`;
            setTimeout(() => {
                let reply = "";
                if(action === 'Pricing Info') reply = "Estimates are provided after a site survey. Our services qualify for national tax credits in many states.";
                if(action === 'Service Areas') reply = "We operate in all 50 states. Simply complete the survey form to verify local contractor availability.";
                feed.innerHTML += `<div class="bubble bubble-admin">${reply}</div>`;
                feed.scrollTop = feed.scrollHeight;
            }, 800);
        }

        function transferToLive() {
            const feed = document.getElementById('chat-feed');
            feed.innerHTML += `<div class="bubble bubble-user">Requesting Live Agent...</div>`;
            db.ref('chats/' + userId).push({ text: "URGENT: USER REQUESTED LIVE AGENT", type: 'user' });
            setTimeout(() => {
                feed.innerHTML += `<div class="bubble bubble-admin" style="background: #fffbeb; border: 1px solid #fde68a;">Signal sent to Dispatch Agent-786. Please stay active; we will respond directly in this window.</div>`;
                feed.scrollTop = feed.scrollHeight;
            }, 1000);
        }

        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + userId).push({ text: txt, type: 'user' });
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
            const tid = "US-HUB-" + Math.floor(100000 + Math.random() * 900000);
            const data = { tid, name: document.getElementById('vName').value, svc: document.getElementById('vSvc').value, phone: document.getElementById('vPhone').value, ts: new Date().toLocaleString() };
            db.ref('leads').push(data).then(() => {
                document.getElementById('masterForm').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('receipt-data').innerHTML = `<p>Tracking: ${tid}</p><p>Customer: ${data.name}</p><p>Service: ${data.svc}</p>`;
            });
        });

        // ADMIN TERMINAL
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }
        
        function syncAdmin() {
            db.ref('leads').on('value', s => {
                let h = '<h4 class="font-black uppercase mb-6">Recent Leads</h4>';
                s.forEach(l => { const v = l.val(); h += `<div class="p-6 bg-slate-50 rounded-2xl mb-4 border"><p class="text-[10px] font-black text-blue-600">${v.tid}</p><h5 class="font-bold">${v.name}</h5><p class="text-[9px] uppercase">${v.svc} | ${v.phone}</p></div>`; });
                document.getElementById('adminLeads').innerHTML = h;
            });
        }
    </script>
</body>
</html>
