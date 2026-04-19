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
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; scroll-behavior: smooth; overflow-x: hidden; }
        
        .hero-premium { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.85)), url('https://images.unsplash.com/photo-1513584684374-8bdb7489feef?q=80&w=2070&auto=format&fit=crop'); background-size: cover; background-position: center; }
        .input-premium { width: 100%; padding: 18px; border: 2px solid #e2e8f0; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: white; font-size: 14px; }
        .input-premium:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 22px; border-radius: 24px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; transition: 0.4s; border: none; cursor: pointer; box-shadow: 0 20px 40px rgba(37, 99, 235, 0.25); }
        .page-section { display: none; }
        .page-section.active { display: block; animation: slideUp 0.6s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        /* ADVANCED CHAT SYSTEM */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 380px; height: 620px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 25px; color: white; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #fdfdfd; display: flex; flex-direction: column; gap: 15px; }
        .bubble { padding: 14px 20px; border-radius: 22px; font-size: 13px; max-width: 85%; line-height: 1.5; font-weight: 500; position: relative; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .chat-bot-option { background: white; border: 2px solid #2563eb; color: #2563eb; padding: 12px; border-radius: 50px; font-size: 11px; font-weight: 800; cursor: pointer; text-align: center; transition: 0.3s; }
        .chat-bot-option:hover { background: #2563eb; color: white; }
    </style>
</head>
<body>

    <nav class="bg-white/95 backdrop-blur sticky top-0 z-[8000] px-8 py-5 flex justify-between items-center border-b">
        <div class="flex items-center gap-4">
            <div onclick="handleAdminTap()" class="h-12 w-12 bg-slate-900 rounded-2xl flex items-center justify-center text-white font-black cursor-pointer shadow-xl">US</div>
            <div>
                <h1 class="text-xs font-black text-slate-900 uppercase tracking-tighter">U.S. Home Improvement</h1>
                <div class="flex items-center gap-2">
                    <span class="h-2 w-2 bg-emerald-500 rounded-full animate-pulse"></span>
                    <span class="text-[9px] font-bold text-blue-600 uppercase italic">Licensed LLC & BBB Accredited</span>
                </div>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-2xl font-black text-[10px] uppercase shadow-lg hover:scale-105 transition">Free Quote</button>
    </nav>

    <section id="home" class="page-section active">
        <header class="hero-premium py-48 px-8 text-center text-white">
            <span class="bg-blue-600/40 border border-blue-500 px-6 py-2 rounded-full text-[10px] font-black uppercase tracking-[0.3em] mb-10 inline-block">National Coverage | $0 Down Financing</span>
            <h1 class="text-5xl md:text-8xl font-black uppercase italic tracking-tighter mb-10 leading-none">The Trusted <br><span class="text-blue-500">Choice.</span></h1>
            <p class="text-slate-300 text-sm font-bold max-w-2xl mx-auto mb-16 uppercase tracking-widest leading-relaxed">No-cost estimates for premium home upgrades. Authorized by nationwide building standards.</p>
            <div class="flex flex-wrap justify-center gap-6">
                <button onclick="showPage('form')" class="btn-master px-16">Start Free Survey</button>
                <button onclick="showPage('about')" class="bg-white/10 backdrop-blur text-white px-10 py-5 rounded-2xl font-black text-[10px] uppercase border border-white/20">Learn More</button>
            </div>
        </header>
    </section>

    <section id="form" class="page-section py-24 bg-slate-50">
        <div class="max-w-4xl mx-auto px-8">
            <div class="bg-white p-12 md:p-20 rounded-[60px] shadow-3xl border border-slate-100">
                <form id="masterForm" class="space-y-10">
                    <div class="border-b pb-8">
                        <h3 class="text-3xl font-black uppercase italic mb-2">Project Authorization</h3>
                        <p class="text-[10px] font-bold text-slate-400 uppercase italic">Detailed qualification for 100% Free estimates</p>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Property Service Needed</label>
                            <select id="vSvc" class="input-premium" required onchange="toggleExtraOptions()">
                                <option value="">Select Service Type</option>
                                <option value="Windows">Windows (National Replacement)</option>
                                <option value="Roofing">Roofing (Complete System)</option>
                                <option value="Solar">Solar Energy Matrix</option>
                                <option value="HVAC">Heating & Air Efficiency</option>
                                <option value="Siding">Siding & Exterior Wall</option>
                                <option value="Kitchen">Luxury Kitchen Remodel</option>
                                <option value="Bathroom">Premium Bathroom Spa</option>
                            </select>
                        </div>
                        <div id="extraOptions" class="hidden">
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Total Units/Windows</label>
                            <input type="number" id="vUnits" class="input-premium" placeholder="e.g. 10">
                        </div>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Homeownership Verified?</label>
                            <select id="vOwner" class="input-premium" required>
                                <option value="Yes">Yes, Legal Owner</option>
                                <option value="No">No, Tenant/Renter</option>
                            </select>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Ready for Installation?</label>
                            <select id="vReady" class="input-premium" required>
                                <option value="Emergency">Emergency / Immediate</option>
                                <option value="Within 30 Days">Within 30 Days</option>
                                <option value="1-3 Months">1-3 Months</option>
                                <option value="Planning Only">Just Researching</option>
                            </select>
                        </div>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Estimated Credit Range</label>
                            <select id="vCredit" class="input-premium" required>
                                <option value="Excellent (720+)">Excellent (720+)</option>
                                <option value="Good (660-719)">Good (660-719)</option>
                                <option value="Fair (Below 660)">Fair (Below 660)</option>
                            </select>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Property Zip Code</label>
                            <input type="text" id="vZip" class="input-premium" placeholder="e.g. 90210" required>
                        </div>
                    </div>

                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Full Physical Property Address</label>
                        <input type="text" id="vAddr" class="input-premium" placeholder="Street, City, State" required>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Full Legal Name</label>
                            <input type="text" id="vName" class="input-premium" placeholder="John Doe" required>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Contact Phone Number</label>
                            <input type="tel" id="vPhone" class="input-premium" placeholder="(555) 000-0000" required>
                        </div>
                    </div>

                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Official Email Address</label>
                        <input type="email" id="vEmail" class="input-premium" placeholder="email@domain.com" required>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Preferred Appointment Date</label>
                            <input type="date" id="vDate" class="input-premium" required>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Preferred Time Slot (9 AM - 7 PM)</label>
                            <select id="vTime" class="input-premium" required>
                                <option value="09:00 AM">09:00 AM</option>
                                <option value="11:00 AM">11:00 AM</option>
                                <option value="01:00 PM">01:00 PM</option>
                                <option value="03:00 PM">03:00 PM</option>
                                <option value="05:00 PM">05:00 PM</option>
                                <option value="07:00 PM">07:00 PM</option>
                            </select>
                        </div>
                    </div>

                    <p class="text-[9px] font-bold text-slate-400 uppercase italic">By clicking authorize, you agree to our privacy policy. Your data is protected by enterprise-grade encryption.</p>
                    <button type="submit" class="btn-master w-full">Transmit Authorization Request</button>
                </form>

                <div id="vSuccess" class="hidden text-center py-12">
                    <div class="w-24 h-24 bg-blue-50 text-blue-600 rounded-full flex items-center justify-center mx-auto mb-10 text-4xl">✓</div>
                    <h3 class="text-3xl font-black uppercase mb-6">Request Authorized</h3>
                    <div id="vReceipt" class="bg-slate-900 text-white p-10 rounded-[40px] text-left text-[11px] font-bold uppercase space-y-4 border-l-8 border-blue-500"></div>
                    <button onclick="location.reload()" class="mt-12 text-blue-600 font-black text-[10px] uppercase underline">New Project Authorization</button>
                </div>
            </div>
        </div>
    </section>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div class="flex justify-between items-center">
                    <div class="flex items-center gap-3">
                        <div class="w-10 h-10 bg-blue-600 rounded-2xl flex items-center justify-center text-xl">👤</div>
                        <div>
                            <h4 class="font-black text-[11px] uppercase tracking-tighter">Corporate Dispatch</h4>
                            <p class="text-[8px] text-blue-400 font-black uppercase">Agent-786 Monitoring</p>
                        </div>
                    </div>
                    <button onclick="toggleChat()" class="text-white opacity-50">✕</button>
                </div>
            </div>
            <div id="chat-feed">
                <div class="bubble bubble-admin">Welcome to U.S. Home Improvement. I am your automated assistant. How can we serve your property today?</div>
                <div id="bot-options" class="flex flex-col gap-2">
                    <button class="chat-bot-option" onclick="botHelp('pricing')">Estimate Pricing Info</button>
                    <button class="chat-bot-option" onclick="botHelp('areas')">Check Service Areas</button>
                    <button class="chat-bot-option" onclick="requestLiveAgent()" style="border-color: #ef4444; color: #ef4444;">🚨 Connect to Live Agent</button>
                </div>
            </div>
            <div class="p-5 border-t bg-white flex gap-3">
                <input type="text" id="chat-input" placeholder="Type detailed inquiry..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-20 h-20 bg-slate-900 rounded-full shadow-3xl flex items-center justify-center text-3xl z-[8500] hover:scale-110 transition">💬</button>
    </div>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center border-b pb-10 mb-12">
                <h3 class="text-4xl font-black italic uppercase tracking-tighter">Enterprise <span class="text-blue-600">Dispatch Hub</span></h3>
                <div class="flex gap-4">
                    <button onclick="exportData()" class="bg-emerald-50 text-emerald-600 px-8 py-3 rounded-full font-black text-[10px] uppercase">Export Leads</button>
                    <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-8 py-3 rounded-full font-black text-[10px] uppercase">Exit Terminal</button>
                </div>
            </div>
            <div id="authBox" class="text-center py-24">
                <input type="password" id="pin" class="input-premium max-w-[320px] text-center text-4xl mb-8" placeholder="••••">
                <br><button onclick="unlock()" class="btn-master max-w-[320px]">Authorize Access</button>
            </div>
            <div id="hubData" class="hidden grid lg:grid-cols-2 gap-16">
                <div id="adminLeads"></div>
                <div>
                    <h4 class="font-black uppercase mb-10 text-slate-400 tracking-[0.2em]">Live Signals</h4>
                    <div id="adminChats" class="space-y-4"></div>
                    <div id="replyInterface" class="hidden mt-12 p-10 bg-slate-900 rounded-[50px] border-4 border-blue-500 shadow-2xl">
                        <p class="text-[10px] font-black text-blue-400 mb-6 uppercase">Target ID: <span id="targetUser" class="text-white"></span></p>
                        <input type="text" id="adminReplyText" class="input-premium mb-6 bg-slate-800 border-slate-700 text-white" placeholder="Type official response...">
                        <div class="flex gap-4">
                            <button onclick="sendAdminReply()" class="btn-master flex-1 text-xs">Send Response</button>
                            <button onclick="clearCurrentChat()" class="bg-red-500 text-white px-8 rounded-3xl font-black text-[10px] uppercase">Clear Chat History</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // FIREBASE ARCHITECTURE
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const userId = "CID-" + Math.floor(1000 + Math.random() * 9000);

        // NAVIGATION ENGINE
        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo({top:0, behavior:'smooth'}); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        function toggleExtraOptions() { document.getElementById('extraOptions').classList.toggle('hidden', document.getElementById('vSvc').value !== 'Windows'); }

        // HYBRID CHAT LOGIC
        function botHelp(type) {
            const f = document.getElementById('chat-feed');
            let resp = type === 'pricing' ? "All site inspections and estimates are 100% Free at no cost to the owner." : "We operate nationwide across all 50 states through authorized partners.";
            f.innerHTML += `<div class="bubble bubble-user">${type} Info Request</div>`;
            setTimeout(() => { f.innerHTML += `<div class="bubble bubble-admin">${resp}</div>`; f.scrollTop = f.scrollHeight; }, 600);
        }

        function requestLiveAgent() {
            db.ref('chats/' + userId).push({ text: "🚨 URGENT: USER REQUESTED LIVE AGENT", type: 'user' });
            document.getElementById('bot-options').classList.add('hidden');
            document.getElementById('chat-feed').innerHTML += `<div class="bubble bubble-admin" style="background:#fffbeb; border:1px solid #fde68a;">Connecting to Dispatch Senior Agent-786... Please stand by.</div>`;
        }

        function sendMsg() {
            const t = document.getElementById('chat-input').value; if(!t) return;
            db.ref('chats/' + userId).push({ text: t, type: 'user' });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + userId).on('value', snap => {
            const msgs = snap.val(); let h = '';
            for(let k in msgs) h += `<div class="bubble ${msgs[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${msgs[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // SURVEY TRANSIT
        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-HUB-" + Math.floor(100000 + Math.random() * 900000);
            const data = { 
                tid, name: document.getElementById('vName').value, email: document.getElementById('vEmail').value,
                phone: document.getElementById('vPhone').value, addr: document.getElementById('vAddr').value, 
                zip: document.getElementById('vZip').value, svc: document.getElementById('vSvc').value,
                owner: document.getElementById('vOwner').value, ready: document.getElementById('vReady').value,
                credit: document.getElementById('vCredit').value, appt: document.getElementById('vDate').value + " @ " + document.getElementById('vTime').value,
                units: document.getElementById('vUnits').value || "N/A", ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('masterForm').classList.add('hidden');
                document.getElementById('vSuccess').classList.remove('hidden');
                document.getElementById('vReceipt').innerHTML = `
                    <p>TRACKING ID: <span class="text-blue-400">${tid}</span></p>
                    <p>CUSTOMER: ${data.name}</p>
                    <p>SERVICE: ${data.svc} (${data.units} Units)</p>
                    <p>PROPERTY: ${data.addr}, ${data.zip}</p>
                    <p>CREDIT RATING: ${data.credit}</p>
                    <p>APPOINTMENT: ${data.appt}</p>
                `;
            });
        });

        // ADMIN TERMINAL ENGINE
        let taps = 0;
        let activeAdminChat = '';
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        function syncAdmin() {
            db.ref('leads').on('value', s => {
                let h = '<h4 class="font-black uppercase mb-10 text-slate-400 tracking-[0.2em]">Authorized Leads</h4>';
                s.forEach(l => { const v = l.val(); h += `<div class="p-8 bg-slate-50 border-2 rounded-[40px] mb-6 relative hover:border-blue-500 transition shadow-sm"><span class="absolute top-6 right-8 bg-slate-900 text-white text-[8px] font-black px-3 py-1 rounded-full">${v.tid}</span><h5 class="text-xl font-black italic uppercase">${v.name}</h5><p class="text-[10px] font-bold text-blue-600 mt-2">📍 ${v.addr} | 📞 ${v.phone}</p><p class="text-[9px] font-bold text-slate-400 mt-3 uppercase">${v.svc} | ${v.ready} | Credit: ${v.credit}</p><p class="text-[10px] font-black text-emerald-600 mt-2 uppercase italic underline">Appt: ${v.appt}</p></div>`; });
                document.getElementById('adminLeads').innerHTML = h;
            });
            db.ref('chats').on('value', s => {
                let h = '';
                s.forEach(c => { 
                    const uid = c.key; const last = Object.values(c.val()).pop();
                    h += `<div onclick="openAdminReply('${uid}')" class="p-6 bg-white border-2 rounded-3xl mb-4 cursor-pointer hover:border-blue-600 shadow-sm"><p class="text-[10px] font-black text-blue-600 mb-2 uppercase tracking-tighter">${uid}</p><p class="text-[11px] font-bold italic truncate">"${last.text}"</p></div>`;
                });
                document.getElementById('adminChats').innerHTML = h || '<p class="text-[10px] font-black uppercase text-slate-300">No Active Signals.</p>';
            });
        }

        function openAdminReply(uid) { activeAdminChat = uid; document.getElementById('replyInterface').classList.remove('hidden'); document.getElementById('targetUser').innerText = uid; }
        function sendAdminReply() {
            const t = document.getElementById('adminReplyText').value; if(!t) return;
            db.ref('chats/' + activeAdminChat).push({ text: t, type: 'admin' });
            document.getElementById('adminReplyText').value = '';
        }
        function clearCurrentChat() { if(confirm('Erase entire history for this user?')) { db.ref('chats/' + activeAdminChat).remove(); document.getElementById('replyInterface').classList.add('hidden'); } }
    </script>
</body>
</html>
