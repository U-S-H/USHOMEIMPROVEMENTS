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
        .hero-premium { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.85)), url('https://images.unsplash.com/photo-1560518883-ce09059eeffa?q=80&w=1973&auto=format&fit=crop') center/cover; }
        .input-premium { width: 100%; padding: 16px; border: 2px solid #e2e8f0; border-radius: 18px; font-weight: 600; outline: none; transition: 0.4s; background: white; font-size: 14px; }
        .input-premium:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 20px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; transition: 0.4s; border: none; cursor: pointer; }
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeUp 0.6s ease-out; }
        @keyframes fadeUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        
        /* Advanced Chat UI */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 380px; height: 620px; background: white; border-radius: 35px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.3); display: none; flex-direction: column; z-index: 9000; overflow: hidden; border: 1px solid #f1f5f9; }
        .bubble { padding: 14px 20px; border-radius: 22px; font-size: 13px; max-width: 85%; line-height: 1.5; font-weight: 500; }
        .bubble-admin { background: #f1f5f9; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .chat-option { background: white; border: 2px solid #2563eb; color: #2563eb; padding: 12px; border-radius: 50px; font-size: 11px; font-weight: 800; text-transform: uppercase; cursor: pointer; margin-bottom: 8px; transition: 0.3s; }
        .chat-option:hover { background: #2563eb; color: white; }
    </style>
</head>
<body>

    <nav class="bg-white/90 backdrop-blur sticky top-0 z-[8000] px-8 py-5 flex justify-between items-center border-b">
        <div class="flex items-center gap-4">
            <div onclick="handleAdminTap()" class="h-12 w-12 bg-slate-900 rounded-2xl flex items-center justify-center text-white font-black cursor-pointer shadow-xl">US</div>
            <div>
                <h1 class="text-xs font-black text-slate-900 uppercase tracking-tighter">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-blue-600 uppercase italic">Registered LLC | BBB Accredited</span>
            </div>
        </div>
        <button onclick="showPage('form')" class="bg-blue-600 text-white px-6 py-3 rounded-xl font-black text-[10px] uppercase shadow-lg">Free Quote</button>
    </nav>

    <section id="home" class="page-section active">
        <header class="hero-premium py-40 px-8 text-center text-white">
            <span class="bg-blue-600/40 border border-blue-500 px-6 py-2 rounded-full text-[10px] font-black uppercase tracking-[0.3em] mb-10 inline-block">100% No-Cost Estimates</span>
            <h1 class="text-5xl md:text-8xl font-black uppercase italic mb-8">Building <span class="text-blue-500">Better</span>.</h1>
            <p class="text-slate-300 text-sm font-bold max-w-2xl mx-auto mb-16 uppercase tracking-widest leading-relaxed">Connecting homeowners with verified, BBB-Accredited professionals for a lifetime of property excellence.</p>
            <button onclick="showPage('form')" class="btn-master px-16">Start Free Survey</button>
        </header>
    </section>

    <section id="form" class="page-section py-24 bg-slate-50">
        <div class="max-w-4xl mx-auto px-8">
            <div class="bg-white p-12 md:p-20 rounded-[60px] shadow-3xl border border-slate-100">
                <form id="masterForm" class="space-y-10">
                    <div>
                        <h3 class="text-3xl font-black uppercase italic mb-2">Project Authorization</h3>
                        <p class="text-[10px] font-bold text-slate-400 uppercase italic">Every quote is 100% Free - No Commitment Required</p>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Primary Service</label>
                            <select id="vSvc" class="input-premium" required onchange="toggleWindowsCount()">
                                <option value="">Select Service Architecture</option>
                                <option value="Windows">Windows (Full Replacement)</option>
                                <option value="Roofing">Roofing (Repair/Install)</option>
                                <option value="Solar">Solar Energy Matrix</option>
                                <option value="HVAC">HVAC: Heating & Air</option>
                                <option value="Siding">Siding: Vinyl/Fiber</option>
                                <option value="Kitchen">Kitchen Luxury Remodel</option>
                                <option value="Bathroom">Bathroom Spa Refit</option>
                                <option value="Gutters">Gutters & Drainage</option>
                            </select>
                        </div>
                        <div id="windowCountBox" class="hidden">
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Total Window Units</label>
                            <input type="number" id="vWinCount" class="input-premium" placeholder="e.g. 12">
                        </div>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Home Ownership Status</label>
                            <select id="vOwner" class="input-premium" required>
                                <option value="Yes">Yes, I am the Homeowner</option>
                                <option value="No">No, I am a Tenant/Renter</option>
                            </select>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Project Timeline</label>
                            <select id="vTimeframe" class="input-premium" required>
                                <option value="Immediate">Immediate / Emergency</option>
                                <option value="Within 1 Month">Within 1 Month</option>
                                <option value="1-3 Months">1-3 Months</option>
                                <option value="Planning Only">Just Researching</option>
                            </select>
                        </div>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Credit Standing</label>
                            <select id="vCredit" class="input-premium" required>
                                <option value="Excellent (720+)">Excellent (720+)</option>
                                <option value="Good (660-719)">Good (660-719)</option>
                                <option value="Fair (Below 660)">Fair (Below 660)</option>
                            </select>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Zip Code</label>
                            <input type="text" id="vZip" class="input-premium" placeholder="e.g. 90210" required>
                        </div>
                    </div>

                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Full Physical Address</label>
                        <input type="text" id="vAddr" class="input-premium" placeholder="Street, City, State" required>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Full Legal Name</label>
                            <input type="text" id="vName" class="input-premium" placeholder="First & Last Name" required>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Phone Number</label>
                            <input type="tel" id="vPhone" class="input-premium" placeholder="(555) 000-0000" required>
                        </div>
                    </div>

                    <div>
                        <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Email Address</label>
                        <input type="email" id="vEmail" class="input-premium" placeholder="johndoe@email.com" required>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Preferred Appointment Date</label>
                            <input type="date" id="vApptDate" class="input-premium" required>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-slate-500 mb-3 block">Preferred Time Slot (9 AM - 7 PM)</label>
                            <select id="vApptTime" class="input-premium" required>
                                <option value="09:00 AM">09:00 AM</option>
                                <option value="11:00 AM">11:00 AM</option>
                                <option value="01:00 PM">01:00 PM</option>
                                <option value="03:00 PM">03:00 PM</option>
                                <option value="05:00 PM">05:00 PM</option>
                                <option value="07:00 PM">07:00 PM</option>
                            </select>
                        </div>
                    </div>

                    <p class="text-[9px] font-bold text-slate-400 uppercase italic">Legal Disclaimer: By clicking 'Authorize', you agree to receive estimates from our BBB-Accredited network. This is a no-cost, no-obligation service.</p>
                    <button type="submit" class="btn-master w-full py-6 mt-10">Authorize & Transmit Request</button>
                </form>

                <div id="vReceipt" class="hidden text-center py-10">
                    <div class="w-24 h-24 bg-blue-50 text-blue-600 rounded-full flex items-center justify-center mx-auto mb-10 text-4xl">🛡️</div>
                    <h3 class="text-3xl font-black uppercase italic mb-8">Securely Transmitted</h3>
                    <div id="receipt-data" class="bg-slate-900 text-white p-12 rounded-[40px] text-left text-[11px] font-bold uppercase space-y-4 border-4 border-blue-500 shadow-2xl"></div>
                    <button onclick="location.reload()" class="mt-12 text-blue-600 font-black text-[10px] uppercase underline">Return to Dashboard</button>
                </div>
            </div>
        </div>
    </section>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header text-white">
                <div class="flex items-center gap-4">
                    <div class="w-12 h-12 bg-blue-600 rounded-2xl flex items-center justify-center text-xl shadow-inner">👤</div>
                    <div>
                        <h4 class="font-black text-[12px] uppercase">Agent Dispatch Terminal</h4>
                        <p class="text-[9px] text-blue-400 font-bold uppercase tracking-widest">ID: Agent-786 Monitoring</p>
                    </div>
                </div>
            </div>
            <div id="chat-feed" class="flex-1 p-5 overflow-y-auto bg-slate-50 flex flex-col gap-4">
                <div class="bubble bubble-admin">Welcome to U.S. Home Improvement. How can we assist with your free estimate today?</div>
                <div class="flex flex-col gap-2" id="chat-options">
                    <button class="chat-option" onclick="chatAction('Pricing')">General Pricing Info</button>
                    <button class="chat-option" onclick="chatAction('States')">Serviceable States</button>
                    <button class="chat-option" onclick="transferToLive()" style="border-color:#ef4444; color:#ef4444;">🚨 Connect to Live Agent</button>
                </div>
            </div>
            <div class="p-5 border-t bg-white flex gap-3">
                <input type="text" id="chat-input" placeholder="Type here..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-20 h-20 bg-slate-900 rounded-full shadow-3xl flex items-center justify-center text-2xl z-[8500]">💬</button>
    </div>

    <div id="adminHub" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center border-b pb-10 mb-12">
                <h3 class="text-4xl font-black italic uppercase">Master Dispatch Terminal</h3>
                <div class="flex gap-4">
                    <button onclick="exportToExcel()" class="bg-emerald-50 text-emerald-600 px-8 py-3 rounded-full font-black text-[10px] uppercase">Export Leads</button>
                    <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-8 py-3 rounded-full font-black text-[10px] uppercase italic">Close</button>
                </div>
            </div>
            <div id="authBox" class="text-center py-32">
                <input type="password" id="pin" class="input-premium max-w-[300px] text-center text-4xl mb-8" placeholder="••••">
                <br><button onclick="unlock()" class="btn-master px-12">Authorize Access</button>
            </div>
            <div id="hubData" class="hidden grid lg:grid-cols-2 gap-16">
                <div id="adminLeads" class="space-y-6"></div>
                <div id="adminChats" class="space-y-4"></div>
            </div>
        </div>
    </div>

    <script>
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const userId = "USER-" + Math.floor(100000 + Math.random() * 899999);

        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo({top:0, behavior:'smooth'}); }
        function toggleChat() { const win = document.getElementById('chat-window'); win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; }
        function toggleWindowsCount() { const svc = document.getElementById('vSvc').value; document.getElementById('windowCountBox').classList.toggle('hidden', svc !== 'Windows'); }

        // CHAT LOGIC
        function chatAction(type) {
            const feed = document.getElementById('chat-feed');
            let resp = type === 'Pricing' ? "All our estimates are 100% Free at no cost to the homeowner. Our contractors provide technical site quotes." : "We cover all 50 states via our authorized partner network.";
            feed.innerHTML += `<div class="bubble bubble-user">${type} Info Request</div>`;
            setTimeout(() => { feed.innerHTML += `<div class="bubble bubble-admin">${resp}</div>`; feed.scrollTop = feed.scrollHeight; }, 600);
        }

        function transferToLive() {
            db.ref('chats/' + userId).push({ text: "🚨 URGENT: USER REQUESTED LIVE AGENT", type: 'user' });
            document.getElementById('chat-feed').innerHTML += `<div class="bubble bubble-admin" style="background:#fffbeb; border:1px solid #fde68a;">Connecting to Senior Dispatcher Agent-786... Please stand by.</div>`;
        }

        function sendMsg() {
            const txt = document.getElementById('chat-input').value; if(!txt) return;
            db.ref('chats/' + userId).push({ text: txt, type: 'user', ts: new Date().toLocaleTimeString() });
            document.getElementById('chat-input').value = '';
        }

        db.ref('chats/' + userId).on('value', snap => {
            const msgs = snap.val(); let h = '';
            for(let k in msgs) h += `<div class="bubble ${msgs[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${msgs[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // FORM TRANSIT
        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-APP-" + Math.floor(100000 + Math.random() * 900000);
            const data = { 
                tid, name: document.getElementById('vName').value, email: document.getElementById('vEmail').value,
                phone: document.getElementById('vPhone').value, addr: document.getElementById('vAddr').value, 
                zip: document.getElementById('vZip').value, svc: document.getElementById('vSvc').value,
                owner: document.getElementById('vOwner').value, timeframe: document.getElementById('vTimeframe').value,
                credit: document.getElementById('vCredit').value, appt: document.getElementById('vApptDate').value + " @ " + document.getElementById('vApptTime').value,
                win: document.getElementById('vWinCount').value || "N/A", ts: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('masterForm').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('receipt-data').innerHTML = `
                    <p>Track ID: <span class="text-blue-400">${tid}</span></p>
                    <p>Client: ${data.name}</p>
                    <p>Service: ${data.svc} (${data.win} units)</p>
                    <p>Location: ${data.addr}, ${data.zip}</p>
                    <p>Ownership: Verified Homeowner</p>
                    <p>Appointment: ${data.appt}</p>
                `;
            });
        });

        // ADMIN TERMINAL
        let taps = 0;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminHub').classList.remove('hidden'); taps=0; } }
        function closeAdmin() { document.getElementById('adminHub').classList.add('hidden'); }
        function unlock() { if(document.getElementById('pin').value === "786") { document.getElementById('authBox').classList.add('hidden'); document.getElementById('hubData').classList.remove('hidden'); syncAdmin(); } }

        function syncAdmin() {
            db.ref('leads').on('value', s => {
                let h = '<h4 class="font-black uppercase mb-8 text-blue-600">Active High-Quality Leads</h4>';
                s.forEach(l => { 
                    const v = l.val(); 
                    h += `<div class="p-8 bg-slate-50 border-2 rounded-[30px] mb-6 relative"><span class="absolute top-6 right-6 bg-slate-900 text-white px-3 py-1 rounded-full text-[8px] font-black">${v.tid}</span><h5 class="text-xl font-black italic">${v.name}</h5><p class="text-[10px] font-bold text-slate-500 uppercase mt-2">📍 ${v.addr} | 📞 ${v.phone}</p><p class="text-[10px] font-bold text-blue-600 mt-2 uppercase">Service: ${v.svc} | Windows: ${v.win} | Credit: ${v.credit}</p><p class="text-[10px] font-bold text-emerald-600 mt-1 uppercase italic underline">Appt: ${v.appt}</p></div>`;
                });
                document.getElementById('adminLeads').innerHTML = h;
            });
            db.ref('chats').on('value', snap => {
                let h = '<h4 class="font-black uppercase mb-8">Secure Chat Signals</h4>';
                snap.forEach(c => {
                    const uid = c.key; const last = Object.values(c.val()).pop();
                    h += `<div class="p-5 bg-white border-2 rounded-2xl mb-4 hover:border-blue-500 cursor-pointer" onclick="alert('Reply to ${uid} via standard terminal')"><div><p class="text-[9px] font-black text-blue-600">${uid}</p><p class="text-[11px] font-bold italic">"${last.text}"</p></div></div>`;
                });
                document.getElementById('adminChats').innerHTML = h;
            });
        }
    </script>
</body>
</html>
