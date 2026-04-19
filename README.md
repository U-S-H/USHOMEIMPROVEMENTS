<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-storage-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; --success: #10b981; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fcfcfc; color: #1e293b; scroll-behavior: smooth; }
        .hero-v3 { background: linear-gradient(rgba(15, 23, 42, 0.92), rgba(15, 23, 42, 0.85)), url('WA_1776549716792.jpeg') center/cover no-repeat fixed; }
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
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; line-height: 1.5; }
        .bubble-user { background: #2563eb; color: white; align-self: flex-end; border-bottom-right-radius: 5px; }
        .bubble-admin { background: white; color: #1e293b; align-self: flex-start; border-bottom-left-radius: 5px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); }
    </style>
</head>
<body>

    <nav class="glass-blur sticky top-0 z-[5000] px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-4">
            <img src="logo.png" onclick="handleAdminTap()" class="h-12 w-12 bg-white border-2 border-slate-50 rounded-2xl shadow-sm cursor-pointer" onerror="this.src='https://ui-avatars.com/api/?name=US&background=0f172a&color=fff'">
            <div>
                <h1 class="text-sm font-black text-slate-900 uppercase leading-none tracking-tight">U.S. Home Improvement</h1>
                <span id="navSubtitle" class="text-[9px] font-bold text-blue-600 uppercase italic">Enterprise National Authority</span>
            </div>
        </div>
        <div class="flex items-center gap-6">
            <button onclick="toggleLang()" id="langBtn" class="text-[10px] font-black border-2 border-blue-600 px-4 py-1 rounded-full text-blue-600 hover:bg-blue-600 hover:text-white transition uppercase">ESP</button>
            <div class="hidden lg:flex gap-10 text-[10px] font-black uppercase tracking-[0.2em] text-slate-400">
                <button onclick="showPage('home')" class="hover:text-blue-600">Home</button>
                <button onclick="showPage('faq')" class="hover:text-blue-600">FAQ</button>
                <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-full shadow-lg">Get Quote</button>
            </div>
        </div>
    </nav>

    <div id="chat-window">
        <div class="chat-header">
            <div class="relative"><div class="w-3 h-3 bg-emerald-500 rounded-full border-2 border-slate-900"></div></div>
            <div><p class="agent-id">Agent Connection: Verified</p><h4 class="font-black uppercase text-[11px]">Senior Dispatch Support</h4></div>
            <button onclick="toggleChat()" class="ml-auto text-xl">✕</button>
        </div>
        <div id="chat-feed">
            <div class="bubble bubble-admin">Welcome to U.S. Home Improvement. How may I assist you with your property survey?</div>
        </div>
        <div class="p-5 border-t bg-white flex gap-3">
            <input type="text" id="chat-input" placeholder="Type your question..." class="w-full text-xs font-semibold outline-none">
            <button onclick="sendMsg()" class="text-blue-600 font-black text-xs uppercase">Send</button>
        </div>
    </div>
    <button onclick="toggleChat()" class="fixed bottom-8 right-8 w-16 h-16 bg-slate-900 rounded-full shadow-2xl flex items-center justify-center text-white text-2xl z-[5500] hover:scale-110 transition ring-4 ring-white/10">💬</button>

    <section id="home" class="page-section active">
        <header class="hero-v3 py-48 px-6 text-center text-white">
            <span class="badge-premium mb-8 inline-block bg-blue-600 px-4 py-1 rounded-full text-[10px] font-bold uppercase">Authorized 50-State Network</span>
            <h1 class="text-6xl md:text-9xl font-black uppercase italic leading-[0.8] mb-12">The Elite <br><span class="text-blue-500">Standard</span>.</h1>
            <button onclick="showPage('form')" class="btn-elite max-w-[320px]">Initiate Project Survey</button>
        </header>
    </section>

    <section id="form" class="page-section py-20 bg-white">
        <div class="max-w-3xl mx-auto px-6">
            <div class="mb-12">
                <div class="flex justify-between text-[10px] font-black uppercase text-slate-400 mb-4 italic"><span>Survey Progress</span> <span id="pcent">0%</span></div>
                <div class="step-pill"><div id="pBar" class="step-fill" style="width: 0%;"></div></div>
            </div>

            <div class="bg-white p-12 rounded-[48px] shadow-2xl border border-slate-50 relative">
                <form id="v3Form">
                    <h3 id="formHeader" class="text-2xl font-black uppercase italic text-slate-900 mb-10">Site Authorization Terminal</h3>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="text" id="vName" placeholder="Full Legal Name" class="input-pro" required>
                        <input type="email" id="vEmail" placeholder="Email Address" class="input-pro" required>
                    </div>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <input type="tel" id="vPhone" placeholder="Primary Phone" class="input-pro" required>
                        <input type="text" id="vZip" placeholder="Zip Code (5 Digits)" class="input-pro" maxlength="5" required>
                    </div>
                    <div class="mb-6">
                        <label class="text-[10px] font-black uppercase text-blue-600 mb-2 block">Upload Site Photos (Optional)</label>
                        <input type="file" id="vFile" class="input-pro" accept="image/*">
                    </div>
                    <div class="grid md:grid-cols-2 gap-6 mb-6">
                        <select id="vSvc" class="input-pro" required>
                            <option value="">Select Service Portfolio</option>
                            <option value="Garage">Garage (Door, Roof, etc)</option>
                            <option value="Windows">Windows Replacement</option>
                            <option value="Roofing">Roofing Installation</option>
                            <option value="Solar">Solar Power Matrix</option>
                            <option value="Kitchen">Interior Remodeling</option>
                        </select>
                        <select id="vCredit" class="input-pro" required>
                            <option value="">Estimated Credit Score</option>
                            <option value="720+">Excellent (720+)</option>
                            <option value="660-719">Good (660-719)</option>
                            <option value="Below 660">Building (Below 660)</option>
                        </select>
                    </div>
                    <input type="text" id="vAddr" placeholder="Physical Site Address" class="input-pro mb-10" required>
                    <button type="submit" id="submitBtn" class="btn-elite">Authorize & Transmit</button>
                </form>

                <div id="vReceipt" class="hidden text-center py-10">
                    <div class="text-6xl mb-8">🎖️</div>
                    <h3 class="text-3xl font-black uppercase italic text-slate-900">Transmission Success</h3>
                    <p class="mt-4 font-bold text-slate-500 uppercase">Tracking ID: <span id="rTid" class="text-blue-600"></span></p>
                    <button onclick="location.reload()" class="mt-8 text-blue-600 font-black uppercase underline">Return to Main</button>
                </div>
            </div>
        </div>
    </section>

    <script>
        // Configuration
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
        const storage = firebase.storage();
        const userId = "SIG-" + Math.floor(100000 + Math.random() * 899999);

        // Language Toggle
        let currentLang = 'EN';
        const content = {
            EN: { subtitle: "Enterprise National Authority", header: "Site Authorization Terminal", btn: "Authorize & Transmit", zipErr: "Please enter a valid 5-digit Zip." },
            ES: { subtitle: "Autoridad Nacional de Empresas", header: "Terminal de Autorización de Sitio", btn: "Autorizar y Transmitir", zipErr: "Ingrese un código postal de 5 dígitos." }
        };

        function toggleLang() {
            currentLang = (currentLang === 'EN') ? 'ES' : 'EN';
            document.getElementById('langBtn').innerText = (currentLang === 'EN') ? 'ESP' : 'ENG';
            document.getElementById('navSubtitle').innerText = content[currentLang].subtitle;
            document.getElementById('formHeader').innerText = content[currentLang].header;
            document.getElementById('submitBtn').innerText = content[currentLang].btn;
        }

        // UI Logic
        function showPage(id) { 
            document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); 
            document.getElementById(id).classList.add('active'); 
            window.scrollTo({top:0, behavior:'smooth'}); 
        }
        function toggleChat() { 
            const win = document.getElementById('chat-window'); 
            win.style.display = (win.style.display === 'flex') ? 'none' : 'flex'; 
        }

        // Progress Bar
        document.querySelectorAll('.input-pro').forEach(inp => {
            inp.addEventListener('input', () => {
                const filled = Array.from(document.querySelectorAll('#v3Form .input-pro')).filter(i => i.value).length;
                const p = Math.floor((filled / 8) * 100);
                document.getElementById('pBar').style.width = p + "%";
                document.getElementById('pcent').innerText = p + "%";
            });
        });

        // Smart Chatbot
        function sendMsg() {
            const input = document.getElementById('chat-input');
            const txt = input.value; if(!txt) return;
            db.ref('chats/' + userId).push({ text: txt, type: 'user' });
            input.value = '';

            const lowTxt = txt.toLowerCase();
            let reply = "I'm connecting you to a senior agent. One moment.";
            if(lowTxt.includes("cost") || lowTxt.includes("price")) reply = "Site surveys are 100% free of charge. Your local contractor will provide a detailed quote after inspection.";
            if(lowTxt.includes("time") || lowTxt.includes("when")) reply = "Dispatches are usually finalized within 24-48 hours.";

            setTimeout(() => {
                db.ref('chats/' + userId).push({ text: reply, type: 'admin' });
            }, 1000);
        }

        db.ref('chats/' + userId).on('value', snap => {
            const msgs = snap.val(); let h = '';
            for(let k in msgs) h += `<div class="bubble ${msgs[k].type === 'user' ? 'bubble-user' : 'bubble-admin'}">${msgs[k].text}</div>`;
            document.getElementById('chat-feed').innerHTML = h;
            document.getElementById('chat-feed').scrollTop = document.getElementById('chat-feed').scrollHeight;
        });

        // Submission with Image Upload
        document.getElementById('v3Form').addEventListener('submit', async (e) => {
            e.preventDefault();
            const zip = document.getElementById('vZip').value;
            if(!/^\d{5}$/.test(zip)) return alert(content[currentLang].zipErr);

            const btn = document.getElementById('submitBtn');
            btn.innerText = "Transmitting...";
            btn.disabled = true;

            let imgUrl = "No Photo";
            const file = document.getElementById('vFile').files[0];
            if(file) {
                const ref = storage.ref('inspections/' + Date.now() + "_" + file.name);
                await ref.put(file);
                imgUrl = await ref.getDownloadURL();
            }

            const tid = "US-DISPATCH-" + Math.floor(100000 + Math.random() * 900000);
            const data = {
                tid, name: document.getElementById('vName').value, email: document.getElementById('vEmail').value,
                phone: document.getElementById('vPhone').value, zip, svc: document.getElementById('vSvc').value,
                addr: document.getElementById('vAddr').value, photo: imgUrl, ts: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                document.getElementById('v3Form').classList.add('hidden');
                document.getElementById('vReceipt').classList.remove('hidden');
                document.getElementById('rTid').innerText = tid;
            });
        });

        // Admin Secret
        let taps = 0, tapT;
        function handleAdminTap() { taps++; if(taps>=5) alert("Terminal Access: Use PIN 786 in Admin Hub"); clearTimeout(tapT); tapT=setTimeout(()=>taps=0,2000); }
    </script>
</body>
</html>
