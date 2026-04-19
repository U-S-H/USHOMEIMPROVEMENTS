<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT LLC | Enterprise Master Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --primary: #1e3a8a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; color: #0f172a; overflow-x: hidden; }
        
        .glass-card { background: white; border: 1px solid #f1f5f9; border-radius: 28px; box-shadow: 0 15px 35px rgba(0,0,0,0.06); }
        .input-pro { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 14px; font-weight: 600; outline: none; font-size: 14px; transition: 0.3s; }
        .input-pro:focus { border-color: var(--accent); background: #f0f7ff; }
        .btn-action { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 18px; border-radius: 14px; font-weight: 800; text-transform: uppercase; width: 100%; cursor: pointer; border: none; letter-spacing: 1px; transition: 0.3s; }
        
        .page-section { display: none; }
        .page-section.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .logo-img { height: 45px; width: 45px; object-fit: contain; border-radius: 10px; background: white; cursor: pointer; border: 1px solid #e2e8f0; }
        
        /* Floating Chat Widget */
        #chat-widget { position: fixed; bottom: 30px; right: 30px; z-index: 9999; }
        .chat-box { width: 320px; height: 450px; background: white; border-radius: 24px; box-shadow: 0 20px 50px rgba(0,0,0,0.15); display: none; flex-direction: column; overflow: hidden; border: 1px solid #f1f5f9; }
        .chat-header { background: #1e3a8a; color: white; padding: 15px; font-weight: 800; font-size: 12px; text-transform: uppercase; }
        #chat-messages { flex: 1; padding: 15px; overflow-y: auto; font-size: 12px; display: flex; flex-direction: column; gap: 8px; }
        .msg-user { background: #f1f5f9; padding: 8px 12px; border-radius: 12px; align-self: flex-start; max-width: 80%; font-weight: 600; }
        .msg-admin { background: #dbeafe; color: #1e3a8a; padding: 8px 12px; border-radius: 12px; align-self: flex-end; max-width: 80%; font-weight: 600; }

        #notif-toast { position: fixed; bottom: 20px; left: 20px; background: white; padding: 12px 22px; border-radius: 50px; box-shadow: 0 10px 30px rgba(0,0,0,0.12); border-left: 5px solid #059669; display: none; z-index: 9999; }
    </style>
</head>
<body>

    <div id="notif-toast"><p id="notif-text" class="text-[10px] font-black text-slate-700 uppercase italic"></p></div>

    <nav class="bg-white/95 backdrop-blur-md border-b px-6 py-4 flex justify-between items-center sticky top-0 z-[2000]">
        <div class="flex items-center gap-3">
            <img src="logo.png" alt="Logo" class="logo-img" id="adminTrigger" onclick="handleTap()" onerror="this.src='https://ui-avatars.com/api/?name=US&background=1e3a8a&color=fff'">
            <div class="cursor-pointer" onclick="showPage('homePage')">
                <span class="block font-black text-sm uppercase text-blue-900 leading-none">U.S. Home Improvement LLC</span>
                <span class="block text-[8px] font-extrabold text-emerald-600 uppercase italic">● Enterprise Dispatch Terminal</span>
            </div>
        </div>
        <div class="hidden md:flex gap-8 text-[9px] font-black text-slate-400 uppercase tracking-widest">
            <button onclick="showPage('homePage')" class="hover:text-blue-600">Home</button>
            <button onclick="showPage('galleryPage')" class="hover:text-blue-600">Portfolio</button>
            <button onclick="showPage('formPage')" class="bg-blue-600 text-white px-5 py-2 rounded-lg">Get Estimate</button>
        </div>
    </nav>

    <div id="chat-widget">
        <div class="chat-box" id="chatBox">
            <div class="chat-header flex justify-between items-center">
                <span>Live Support Terminal</span>
                <button onclick="toggleChat()">✕</button>
            </div>
            <div id="chat-messages">
                <div class="msg-admin">Hello! How can we help with your home project today?</div>
            </div>
            <div class="p-3 border-t flex gap-2">
                <input type="text" id="chatInput" placeholder="Type message..." class="w-full text-xs p-2 outline-none">
                <button onclick="sendChat()" class="text-blue-600 font-black text-[10px] uppercase">Send</button>
            </div>
        </div>
        <button onclick="toggleChat()" class="bg-blue-600 text-white w-14 h-14 rounded-full shadow-2xl flex items-center justify-center text-2xl">💬</button>
    </div>

    <section id="homePage" class="page-section active">
        <header class="py-32 px-6 text-center bg-slate-900 text-white" style="background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), url('WA_1776549716792.jpeg') center/cover;">
            <h1 class="text-5xl md:text-7xl font-black uppercase italic mb-6">American <br>Quality <span class="text-blue-400">Restored.</span></h1>
            <button onclick="showPage('formPage')" class="btn-action max-w-xs mt-8">Start Site Survey</button>
        </header>
    </section>

    <section id="galleryPage" class="page-section py-20 bg-slate-50">
        <div class="max-w-6xl mx-auto px-6 text-center">
            <h2 class="text-3xl font-black uppercase italic mb-12">Recent <span class="text-blue-600">Transformations</span></h2>
            <div class="grid md:grid-cols-2 gap-8">
                <div class="glass-card overflow-hidden">
                    <img src="WA_1776549917709.jpeg" class="w-full h-64 object-cover">
                    <div class="p-6"><h4 class="font-black uppercase text-xs">Kitchen Remodel - Houston, TX</h4></div>
                </div>
                <div class="glass-card overflow-hidden">
                    <img src="WA_1776549862258.jpeg" class="w-full h-64 object-cover">
                    <div class="p-6"><h4 class="font-black uppercase text-xs">Bath Spa - Miami, FL</h4></div>
                </div>
            </div>
        </div>
    </section>

    <section id="formPage" class="page-section py-20 bg-slate-100 min-h-screen">
        <div class="max-w-xl mx-auto glass-card p-10">
            <form id="masterForm">
                <h3 class="text-xl font-black italic uppercase mb-8 border-l-4 border-blue-600 pl-4">Application Terminal</h3>
                <input type="text" id="custName" placeholder="Full Legal Name" class="input-pro mb-3" required>
                <input type="tel" id="custPhone" placeholder="Phone Number" class="input-pro mb-3" required>
                <select id="custService" class="input-pro mb-3" required>
                    <option value="Roofing">Roofing</option>
                    <option value="Solar">Solar</option>
                    <option value="Windows">Windows</option>
                </select>
                <input type="text" id="custAddr" placeholder="Property Address" class="input-pro mb-8" required>
                <button type="submit" class="btn-action">Authorize Dispatch</button>
            </form>
            <div id="successMsg" class="hidden text-center py-10">
                <h2 class="text-2xl font-black uppercase text-blue-900 italic">✅ Sent Successfully</h2>
                <p class="text-xs font-bold text-slate-400 mt-2">A specialist will contact you for site access.</p>
            </div>
        </div>
    </section>

    <div id="adminPanel" class="fixed inset-0 bg-white z-[5000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center border-b pb-4 mb-8">
            <h3 class="font-black italic text-blue-900 uppercase">Enterprise Dispatch Hub</h3>
            <button onclick="closeAdmin()" class="text-red-500 font-black text-xs uppercase">Close</button>
        </div>
        <div id="leadsList" class="space-y-4">
            <div class="grid md:grid-cols-2 gap-6">
                <div class="bg-blue-50 p-6 rounded-3xl">
                    <h4 class="font-black text-xs uppercase mb-4">Live Chat Messages</h4>
                    <div id="adminChatList" class="space-y-2"></div>
                </div>
                <div class="bg-slate-50 p-6 rounded-3xl">
                    <h4 class="font-black text-xs uppercase mb-4">Project Leads</h4>
                    <div id="adminLeadsList" class="space-y-2"></div>
                </div>
            </div>
        </div>
    </div>

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

        // Page Navigation
        function showPage(id) { document.querySelectorAll('.page-section').forEach(p=>p.classList.remove('active')); document.getElementById(id).classList.add('active'); window.scrollTo(0,0); }

        // Live Chat Logic
        function toggleChat() { const c = document.getElementById('chatBox'); c.style.display = (c.style.display === 'flex') ? 'none' : 'flex'; }
        
        function sendChat() {
            const msg = document.getElementById('chatInput').value;
            if(!msg) return;
            const chatData = { text: msg, time: new Date().toLocaleTimeString(), type: 'user' };
            db.ref('chats').push(chatData);
            appendMsg(msg, 'user');
            document.getElementById('chatInput').value = '';
        }

        function appendMsg(text, type) {
            const div = document.createElement('div');
            div.className = type === 'user' ? 'msg-user' : 'msg-admin';
            div.innerText = text;
            document.getElementById('chat-messages').appendChild(div);
        }

        // Form Submission
        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const data = {
                name: document.getElementById('custName').value,
                phone: document.getElementById('custPhone').value,
                service: document.getElementById('custService').value,
                address: document.getElementById('custAddr').value,
                time: new Date().toLocaleString()
            };
            db.ref('leads').push(data).then(() => {
                document.getElementById('masterForm').classList.add('hidden');
                document.getElementById('successMsg').classList.remove('hidden');
            });
        });

        // Admin Panel Logic
        let taps = 0, tapT;
        function handleTap() { taps++; clearTimeout(tapT); if(taps>=5){ document.getElementById('adminPanel').classList.remove('hidden'); syncAdmin(); taps=0; } tapT=setTimeout(()=>taps=0,2000); }
        function closeAdmin() { document.getElementById('adminPanel').classList.add('hidden'); }

        function syncAdmin() {
            // Sync Leads
            db.ref('leads').on('value', snap => {
                const leads = snap.val(); let h = '';
                for(let k in leads) h += `<div class="p-4 bg-white border rounded-2xl text-[10px] font-bold uppercase mb-2">
                    <p class="text-blue-600">${leads[k].service}</p>
                    <p>${leads[k].name} - ${leads[k].phone}</p>
                    <p class="text-slate-400 italic">${leads[k].address}</p>
                </div>`;
                document.getElementById('adminLeadsList').innerHTML = h || 'No leads yet.';
            });

            // Sync Chats
            db.ref('chats').on('value', snap => {
                const chats = snap.val(); let h = '';
                for(let k in chats) h += `<div class="p-3 bg-white border rounded-xl text-[10px] mb-1">
                    <span class="text-blue-900 font-black">${chats[k].type.toUpperCase()}:</span> ${chats[k].text}
                </div>`;
                document.getElementById('adminChatList').innerHTML = h || 'No messages.';
            });
        }

        // Fake Notifications
        setInterval(() => {
            const names = ["Robert", "Sarah", "Kevin", "Emily"];
            const toast = document.getElementById('notif-toast');
            document.getElementById('notif-text').innerText = "⭐ " + names[Math.floor(Math.random()*names.length)] + " just requested a quote!";
            toast.style.display = 'block';
            setTimeout(() => toast.style.display='none', 4000);
        }, 20000);
    </script>
</body>
</html>
