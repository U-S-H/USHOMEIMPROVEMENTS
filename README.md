<!DOCTYPE html>
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
        .step-fill { height: 100%; background: var(--accent); width: 0%; transition: 0.6s; }
        #chat-window { position: fixed; bottom: 100px; right: 30px; width: 360px; height: 550px; background: white; border-radius: 30px; box-shadow: 0 30px 60px -12px rgba(0,0,0,0.25); display: none; flex-direction: column; z-index: 6000; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #0f172a; padding: 22px; color: white; display: flex; align-items: center; gap: 12px; }
        #chat-feed { flex: 1; padding: 20px; overflow-y: auto; background: #f8fafc; display: flex; flex-direction: column; gap: 12px; }
        .bubble { padding: 12px 18px; border-radius: 20px; font-size: 13px; max-width: 85%; font-weight: 500; }
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
                <span id="nav-subtitle" class="text-[9px] font-bold text-blue-600 uppercase italic">Enterprise National Authority</span>
            </div>
        </div>
        <div class="flex items-center gap-6">
            <button onclick="toggleLanguage()" id="langBtn" class="text-[10px] font-black border-2 border-blue-600 px-4 py-1 rounded-full text-blue-600 hover:bg-blue-600 hover:text-white transition">ESP</button>
            <div class="hidden lg:flex gap-10 text-[10px] font-black uppercase tracking-[0.2em] text-slate-400">
                <button onclick="showPage('home')" class="hover:text-blue-600">Home</button>
                <button onclick="showPage('faq')" class="hover:text-blue-600">FAQ</button>
                <button onclick="showPage('form')" class="bg-blue-600 text-white px-8 py-3 rounded-full shadow-lg">Get Quote</button>
            </div>
        </div>
    </nav>

    <section id="form" class="page-section py-20 bg-white">
        <div class="max-w-3xl mx-auto px-6">
            <div class="mb-12">
                <div class="flex justify-between text-[10px] font-black uppercase text-slate-400 mb-4 italic"><span>Survey Progress</span> <span id="pcent">0%</span></div>
                <div class="step-pill"><div id="pBar" class="step-fill" style="width: 0%;"></div></div>
            </div>

            <div class="bg-white p-12 rounded-[48px] shadow-2xl border border-slate-50">
                <form id="v3Form">
                    <h3 id="form-title" class="text-2xl font-black uppercase italic text-slate-900 mb-10">Site Authorization Terminal</h3>
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
                    <input type="text" id="vAddr" placeholder="Physical Site Address" class="input-pro mb-10" required>
                    <button type="submit" id="submitBtn" class="btn-elite">Authorize & Transmit</button>
                </form>
                </div>
        </div>
    </section>

    <script>
        // Initialization and Config
        const firebaseConfig = { /* Your Config */ };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const storage = firebase.storage();
        
        // Multi-Language System
        let currentLang = 'EN';
        const langData = {
            EN: { nav: "Enterprise National Authority", title: "Site Authorization Terminal", btn: "Authorize & Transmit" },
            ES: { nav: "Autoridad Nacional de Empresas", title: "Terminal de Autorización de Sitio", btn: "Autorizar y Transmitir" }
        };

        function toggleLanguage() {
            currentLang = currentLang === 'EN' ? 'ES' : 'EN';
            document.getElementById('langBtn').innerText = currentLang === 'EN' ? 'ESP' : 'ENG';
            document.getElementById('nav-subtitle').innerText = langData[currentLang].nav;
            document.getElementById('form-title').innerText = langData[currentLang].title;
            document.getElementById('submitBtn').innerText = langData[currentLang].btn;
        }

        // Form Logic with Image Upload & Zip Check
        document.getElementById('v3Form').addEventListener('submit', async (e) => {
            e.preventDefault();
            const zip = document.getElementById('vZip').value;
            
            // AI/Logic Check: Only allow certain Zip formats
            if(!/^\d{5}$/.test(zip)) {
                alert("Please enter a valid 5-digit US Zip Code.");
                return;
            }

            const btn = document.getElementById('submitBtn');
            btn.innerText = "Processing...";
            btn.disabled = true;

            let imageUrl = null;
            const file = document.getElementById('vFile').files[0];
            
            if(file) {
                const storageRef = storage.ref('site_photos/' + Date.now() + "_" + file.name);
                await storageRef.put(file);
                imageUrl = await storageRef.getDownloadURL();
            }

            const tid = "US-DISPATCH-" + Math.floor(100000 + Math.random() * 900000);
            const data = {
                tid: tid,
                name: document.getElementById('vName').value,
                zip: zip,
                photo: imageUrl || 'No Photo',
                ts: new Date().toLocaleString()
                // ... rest of your fields
            };

            db.ref('leads').push(data).then(() => {
                // Show Success Receipt
                alert("Transmission Success! Tracking ID: " + tid);
                location.reload(); 
            });
        });

        // AI Chat Simulation (Simple Response)
        function autoReply(userMsg) {
            const msg = userMsg.toLowerCase();
            let reply = "I am connecting you with a Senior Dispatcher. Please wait.";
            if(msg.includes("cost") || msg.includes("price")) reply = "Site assessments are 100% free. A local contractor will provide the final quote.";
            if(msg.includes("time")) reply = "Standard dispatch takes 24-48 hours.";
            
            setTimeout(() => {
                db.ref('chats/' + userId).push({ text: reply, type: 'admin', time: new Date().toLocaleTimeString() });
            }, 1500);
        }

        // Add handleAdminTap and other original functions here...
    </script>
</body>
</html>
