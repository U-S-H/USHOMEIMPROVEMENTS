<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | National Enterprise Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fafafa; color: #1e293b; overflow-x: hidden; }
        
        .hero-bg { background: linear-gradient(rgba(15, 23, 42, 0.85), rgba(15, 23, 42, 0.85)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.3); }
        
        .input-pro { width: 100%; padding: 14px 18px; border: 2px solid #f1f5f9; border-radius: 12px; font-weight: 600; outline: none; transition: 0.3s; font-size: 14px; }
        .input-pro:focus { border-color: var(--accent); background: #f8faff; box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }
        
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 16px 32px; border-radius: 14px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; box-shadow: 0 10px 20px rgba(37, 99, 235, 0.2); cursor: pointer; border: none; }
        .btn-master:hover { transform: translateY(-3px); box-shadow: 0 15px 30px rgba(37, 99, 235, 0.3); }

        .page-section { display: none; }
        .page-section.active { display: block; animation: slideUp 0.6s ease; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        /* Real-Time Chat System */
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 340px; height: 500px; background: white; border-radius: 28px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.25); display: none; flex-direction: column; z-index: 5001; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #1e3a8a; padding: 20px; color: white; display: flex; justify-content: space-between; align-items: center; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; display: flex; flex-direction: column; gap: 10px; background: #f8fafc; }
        .bubble { padding: 12px 16px; border-radius: 18px; font-size: 13px; max-width: 85%; font-weight: 500; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .bubble-admin { background: #e2e8f0; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 4px; }

        #toast { position: fixed; bottom: 30px; left: 30px; background: white; padding: 12px 24px; border-radius: 50px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); display: none; z-index: 9999; border-left: 5px solid #2563eb; }
    </style>
</head>
<body>

    <div id="toast"><p id="toast-msg" class="text-[10px] font-black uppercase italic text-slate-600"></p></div>

    <nav class="glass sticky top-0 z-[5000] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <img src="logo.png" onclick="handleAdminTap()" class="h-12 w-12 bg-white rounded-xl shadow-sm border p-1 cursor-pointer" onerror="this.src='https://ui-avatars.com/api/?name=US&background=1e3a8a&color=fff'">
            <div>
                <h1 class="text-sm font-black text-blue-950 uppercase leading-none tracking-tight">U.S. Home Improvement</h1>
                <span class="text-[9px] font-bold text-emerald-600 uppercase italic">● Enterprise National Dispatch</span>
            </div>
        </div>
        <div class="hidden lg:flex gap-10 text-[10px] font-extrabold uppercase tracking-widest text-slate-400">
            <button onclick="showPage('home')" class="hover:text-blue-600 transition">Solutions</button>
            <button onclick="showPage('legal')" class="hover:text-blue-600 transition">Compliance</button>
            <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-full shadow-lg shadow-blue-100 hover:bg-blue-700 transition">Request Estimate</button>
        </div>
    </nav>

    <div id="chat-hub">
        <div id="chat-window">
            <div class="chat-header">
                <div><h4 class="font-black uppercase text-[10px]">Support Terminal</h4><p class="text-[8px] opacity-80 italic">Verified Live Connection</p></div>
                <button onclick="toggleChat()" class="text-xl">×</button>
            </div>
            <div id="chat-feed"></div>
            <div class="p-4 border-t flex gap-2">
                <input type="text" id="chat-input" placeholder="Ask a question..." class="w-full text-xs font-semibold outline-none">
                <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-blue-600 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[5000] hover:scale-110 transition">💬</button>
    </div>

    <section id="home" class="page-section active">
        <header class="hero-bg py-48 px-6 text-center text-white">
            <div class="max-w-5xl mx-auto">
                <span class="px-5 py-1.5 rounded-full border border-white/20 bg-white/10 text-[10px] font-black uppercase tracking-[0.3em] mb-10 inline-block">Authorized National Industry Leader</span>
                <h1 class="text-5xl md:text-8xl font-black uppercase italic leading-[0.85] tracking-tighter mb-12">American <br><span class="text-blue-500">Excellence</span> <br>Redefined.</h1>
                <p class="max-w-2xl mx-auto text-blue-100 font-bold text-xs uppercase tracking-[0.4em] mb-16 leading-loose">Premium Site Inspections & Certified Contractor Logistics Across 50 States.</p>
                <div class="flex flex-wrap justify-center gap-6">
                    <button onclick="showPage('form')" class="btn-master">Secure Site Survey</button>
                    <button onclick="showPage('legal')" class="bg-white/10 border border-white/20 px-10 py-4 rounded-14 font-black uppercase text-xs hover:bg-white/20 transition">Compliance Docs</button>
                </div>
            </div>
        </header>
    </section>

    <section id="form" class="page-section py-24 bg-white px-6">
        <div class="max-w-3xl mx-auto">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-black uppercase italic text-blue-950">Enterprise <span class="text-blue-600">Qualification</span></h2>
                <p class="text-[10px] font-bold text-slate-400 uppercase mt-3 tracking-widest">Complete all parameters for authorized dispatch</p>
            </div>
            <div class="bg-white p-12 rounded-[48px] shadow-2xl border border-slate-50">
                <form id="deepForm">
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <div>
                            <label class="text-[9px] font-black text-slate-400 uppercase mb-2 block">Full Legal Name</label>
                            <input type="text" id="f_name" class="input-pro" required>
                        </div>
                        <div>
                            <label class="text-[9px] font-black text-slate-400 uppercase mb-2 block">Email Address</label>
                            <input type="email" id="f_email" class="input-pro" required>
                        </div>
                    </div>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <div>
                            <label class="text-[9px] font-black text-slate-400 uppercase mb-2 block">Mobile Connection</label>
                            <input type="tel" id="f_phone" class="input-pro" required>
                        </div>
                        <div>
                            <label class="text-[9px] font-black text-slate-400 uppercase mb-2 block">Service Category</label>
                            <select id="f_svc" class="input-pro" required>
                                <option value="Roofing">Roofing Replacement</option>
                                <option value="Solar">Solar Power Matrix</option>
                                <option value="Windows">Energy Windows</option>
                                <option value="Kitchen">Kitchen Remodeling</option>
                                <option value="Bathroom">Bathroom Spa Upgrade</option>
                                <option value="HVAC">Climate Control (HVAC)</option>
                                <option value="Gutters">Seamless Gutters</option>
                            </select>
                        </div>
                    </div>

                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <div>
                            <label class="text-[9px] font-black text-slate-400 uppercase mb-2 block">Estimated Credit Score</label>
                            <select id="f_credit" class="input-pro" required>
                                <option value="Excellent (720+)">Excellent (720+)</option>
                                <option value="Good (660-719)">Good (660-719)</option>
                                <option value="Fair (620-659)">Fair (620-659)</option>
                                <option value="Building (Below 620)">Building (Below 620)</option>
                            </select>
                        </div>
                        <div>
                            <label class="text-[9px] font-black text-slate-400 uppercase mb-2 block">Project Timeline</label>
                            <select id="f_timeline" class="input-pro" required>
                                <option value="As Soon As Possible">As Soon As Possible</option>
                                <option value="Within 2-3 Months">Within 2-3 Months</option>
                                <option value="6 Months to 1 Year">6 Months to 1 Year</option>
                                <option value="Future Estimate Only">Future Estimate Only</option>
                            </select>
                        </div>
                    </div>

                    <div class="grid md:grid-cols-2 gap-6 mb-8">
                        <div>
                            <label class="text-[9px] font-black text-slate-400 uppercase mb-2 block">Appointment Date</label>
                            <input type="date" id="f_date" class="input-pro" required>
                        </div>
                        <div>
                            <label class="text-[9px] font-black text-slate-400 uppercase mb-2 block">Preferred Window</label>
                            <select id="f_time" class="input-pro" required>
                                <option value="Morning (8AM - 12PM)">Morning (8AM - 12PM)</option>
                                <option value="Afternoon (12PM - 4PM)">Afternoon (12PM - 4PM)</option>
                                <option value="Evening (4PM - 7PM)">Evening (4PM - 7PM)</option>
                            </select>
                        </div>
                    </div>

                    <input type="text" id="f_addr" placeholder="Site Address" class="input-pro mb-10" required>
                    <button type="submit" class="btn-master w-full">Submit Authorization Request</button>
                </form>
                <div id="formSuccess" class="hidden text-center py-16">
                    <div class="text-6xl mb-8">✅</div>
                    <h3 class="text-3xl font-black uppercase italic text-blue-950">Dispatch Confirmed</h3>
                    <p class="text-xs font-bold text-slate-400 mt-4 uppercase">Reference ID: #US-<span id="refId"></span></p>
                </div>
            </div>
        </div>
    </section>

    <section id="legal" class="page-section py-24 bg-slate-50 px-6">
        <div class="max-w-4xl mx-auto glass p-16 rounded-[40px]">
            <h2 class="text-3xl font-black uppercase italic text-blue-950 mb-12 border-b pb-6">Compliance <span class="text-blue-600">& Legal</span></h2>
            
            <div class="space-y-12">
                <div>
                    <h4 class="text-xs font-black uppercase text-blue-600 mb-4 tracking-widest">01. Privacy Protocol</h4>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">U.S. Home Improvement LLC values your data security. We utilize 256-bit AES encryption for all lead transmissions. By submitting your information, you authorize our network of certified contractors to contact you via phone, SMS, or email regarding your project estimate. We do not sell user data to third-party marketing firms outside our verified service network.</p>
                </div>
                <div>
                    <h4 class="text-xs font-black uppercase text-blue-600 mb-4 tracking-widest">02. Terms of Service</h4>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">Estimates provided through this terminal are preliminary based on user-provided data. Final pricing is subject to on-site inspection by a licensed technician. All site surveys are conducted by independent authorized contractors within our national dispatch framework.</p>
                </div>
                <div>
                    <h4 class="text-xs font-black uppercase text-blue-600 mb-4 tracking-widest">03. TCPA Compliance</h4>
                    <p class="text-[11px] font-bold text-slate-500 uppercase leading-relaxed">By clicking "Submit", you provide express written consent to be contacted by U.S. Home Improvement LLC and its partners at the number provided. Consent is not a condition of purchase.</p>
                </div>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[9999] hidden overflow-y-auto p-12">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-center mb-16 border-b pb-8">
                <h3 class="text-3xl font-black uppercase italic text-blue-950">Master Terminal <span class="text-blue-600">Control Hub</span></h3>
                <button onclick="closeAdmin()" class="bg-red-50 text-red-500 px-8 py-3 rounded-full font-black text-xs uppercase tracking-widest">Exit Terminal</button>
            </div>
            
            <div id="authBox" class="text-center py-24">
                <input type="password" id="adminPin" class="input-pro max-w-[280px] text-center text-2xl mb-6" placeholder="TERMINAL PIN">
                <br><button onclick="verifyAdmin()" class="btn-master">Authorize Access</button>
            </div>

            <div id="hubContent" class="hidden grid lg:grid-cols-3 gap-12">
                <div class="lg:col-span-2">
                    <h5 class="font-black uppercase text-xs mb-8 text-slate-400 italic tracking-widest">Authorized Dispatches</h5>
                    <div id="leadList" class="space-y-6"></div>
                </div>
                <div>
                    <h5 class="font-black uppercase text-xs mb-8 text-slate-400 italic tracking-widest">Live Terminal Chats</h5>
                    <div id="chatList" class="space-y-4"></div>
                    <div id="replyArea" class="hidden mt-10 bg-slate-50 p-8 rounded-[32px] border border-blue-100 shadow-inner">
                        <p class="text-[10px] font-black uppercase mb-6 text-blue-600">Dispatching Reply to: <span id="targetUser"></span></p>
                        <input type="text" id="adminReplyInput" placeholder="Enter secure message..." class="input-pro mb-6">
                        <button onclick="sendAdminReply()" class="btn-master w-full text-xs">Transmit Reply</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <footer class="bg-slate-950 text-white py-32 px-6 text-center">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-center gap-12 mb-20 opacity-30 grayscale">
                <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Forbes_logo.svg" class="h-5">
                <img src="https://upload.wikimedia.org/wikipedia/commons/a/a2/Better_Business_Bureau_logo.svg" class="h-5">
                <img src="https://upload.wikimedia.org/wikipedia/commons/c/c8/HomeAdvisor_logo.svg" class="h-5">
            </div>
            <p class="text-[10px] font-black uppercase tracking-[0.5em] text-blue-500 mb-6 italic">National Terminal Dispatch HQ</p>
            <p class="text-[10px] font-bold text-slate-500 uppercase max-w-lg mx-auto leading-relaxed">702 Main Street, Woodland, CA 95695 | (786) Authorized Access Only | Compliance ID: 786-US-HI</p>
            <p class="text-[8px] text-slate-700 font-bold uppercase mt-16 tracking-widest">© 2026 U.S. HOME IMPROVEMENT LLC. DATA PROTECTED BY MILITARY-GRADE ENCRYPTION.</p>
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
        const myId = "UID_" + Math.floor(Math.random() * 999999);

        // PAGE LOGIC
        function showPage(id) {
            document.querySelectorAll('.page-section').forEach(p => p.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo({top:0, behavior: 'smooth'});
        }

        // CHAT LOGIC
        function toggleChat() {
            const win = document.getElementById('chat-window');
            win.style.display = win.style.display === 'flex' ? 'none' : 'flex';
        }
        function sendMsg() {
            const input = document.getElementById('chat-input');
            if(!input.value) return;
            db.ref('chats/' + myId).push({ text: input.value, type: 'user', time: new Date().toLocaleTimeString() });
            input.value = '';
        }
        db.ref('chats/' + myId).on('value', snap => {
            const msgs = snap.val(); let h = '';
            for(let k in msgs) h += `<div class="bubble ${msgs[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${msgs[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // FORM SUBMISSION
        document.getElementById('deepForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const rid = Math.floor(1000 + Math.random() * 8999);
            const leadData = {
                id: rid,
                name: document.getElementById('f_name').value,
                email: document.getElementById('f_email').value,
                phone: document.getElementById('f_phone').value,
                svc: document.getElementById('f_svc').value,
                credit: document.getElementById('f_credit').value,
                timeline: document.getElementById('f_timeline').value,
                date: document.getElementById('f_date').value,
                time: document.getElementById('f_time').value,
                addr: document.getElementById('f_addr').value,
                timestamp: new Date().toLocaleString()
            };
            db.ref('leads').push(leadData).then(() => {
                document.getElementById('deepForm').classList.add('hidden');
                document.getElementById('refId').innerText = rid;
                document.getElementById('formSuccess').classList.remove('hidden');
            });
        });

        // ADMIN HUB LOGIC
        let taps = 0, tapT;
        function handleAdminTap() { taps++; if(taps>=5){ document.getElementById('adminPanel').classList.remove('hidden'); taps=0; } clearTimeout(tapT); tapT=setTimeout(()=>taps=0,2500); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }
        function verifyAdmin() {
            if(document.getElementById('adminPin').value === "786") {
                document.getElementById('authBox').classList.add('hidden');
                document.getElementById('hubContent').classList.remove('hidden');
                syncHub();
            }
        }

        let replyId = '';
        function syncHub() {
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) h += `<div class="p-8 bg-slate-50 border rounded-[32px] relative shadow-sm">
                    <span class="absolute top-6 right-6 bg-blue-600 text-white px-4 py-1 rounded-full text-[8px] font-black uppercase">${leads[k].svc}</span>
                    <h4 class="text-xl font-black text-blue-900 italic mb-2">${leads[k].name}</h4>
                    <div class="grid grid-cols-2 gap-y-2 text-[10px] font-bold text-slate-500 uppercase italic">
                        <p>📧 ${leads[k].email}</p><p>📞 ${leads[k].phone}</p>
                        <p>📍 ${leads[k].addr}</p><p>💳 Credit: ${leads[k].credit}</p>
                        <p>⏳ Timeline: ${leads[k].timeline}</p><p>📅 Appt: ${leads[k].date} (${leads[k].time})</p>
                    </div>
                    <button onclick="delItem('leads/${k}')" class="mt-6 text-red-500 font-black text-[9px] uppercase tracking-widest border-t pt-4 w-full text-center">Erase Dispatch</button>
                </div>`;
                document.getElementById('leadList').innerHTML = h || 'Terminal Clear.';
            });

            db.ref('chats').on('value', snap => {
                const chats = snap.val(); let h = '';
                for(let uid in chats) {
                    const last = Object.values(chats[uid]).pop();
                    h += `<div class="p-5 border rounded-2xl bg-white flex justify-between items-center mb-3 shadow-sm hover:border-blue-300 transition cursor-pointer" onclick="openReply('${uid}')">
                        <div><p class="text-[9px] font-black text-blue-600 uppercase">Terminal ID: ${uid}</p><p class="text-[11px] font-bold italic">"${last.text}"</p></div>
                        <button onclick="delItem('chats/${uid}')" class="text-red-200 hover:text-red-500">✕</button>
                    </div>`;
                }
                document.getElementById('chatList').innerHTML = h || 'No Active Signals.';
            });
        }

        function openReply(uid) {
            replyId = uid;
            document.getElementById('replyArea').classList.remove('hidden');
            document.getElementById('targetUser').innerText = uid;
        }

        function sendAdminReply() {
            const txt = document.getElementById('adminReplyInput').value;
            if(!txt || !replyId) return;
            db.ref('chats/' + replyId).push({ text: txt, type: 'admin', time: new Date().toLocaleTimeString() });
            document.getElementById('adminReplyInput').value = '';
            alert("Secure Reply Transmitted.");
        }

        function delItem(path) { if(confirm('Permanently erase data?')) db.ref(path).remove(); }

        // SOCIAL PROOF
        const userN = ["James", "Linda", "Robert", "Patricia", "Michael", "Sarah"];
        const cityN = ["Houston", "Miami", "Woodland", "Chicago", "Phoenix"];
        setInterval(() => {
            const t = document.getElementById('toast');
            document.getElementById('toast-msg').innerText = `⚡ ${userN[Math.floor(Math.random()*userN.length)]} from ${cityN[Math.floor(Math.random()*cityN.length)]} authorized a survey!`;
            t.style.display = 'flex';
            setTimeout(() => t.style.display = 'none', 6000);
        }, 18000);
    </script>
</body>
</html>
