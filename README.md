<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENTS | National Enterprise Matrix</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --neon: #00f2ff; --dark: #010204; --card: rgba(255, 255, 255, 0.03); }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--dark); color: white; overflow-x: hidden; scroll-behavior: smooth; }
        
        /* Animated Background */
        .glow-bg { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; background: radial-gradient(circle at 50% -20%, #004d4d 0%, var(--dark) 80%); }
        
        .glass-panel { background: var(--card); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 2.5rem; }
        .neon-glow:hover { border-color: var(--neon); box-shadow: 0 0 40px rgba(0, 242, 255, 0.15); transform: translateY(-5px); transition: 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); }

        .step { display: none; }
        .step.active { display: block; animation: slideUp 0.6s ease forwards; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(40px); } to { opacity: 1; transform: translateY(0); } }

        input, select, textarea { background: rgba(255,255,255,0.05) !important; border: 1px solid rgba(255,255,255,0.1) !important; color: white !important; padding: 1.25rem; border-radius: 1.25rem; width: 100%; outline: none; }
        input:focus { border-color: var(--neon) !important; box-shadow: 0 0 15px rgba(0, 242, 255, 0.1); }

        .btn-choice { width: 100%; padding: 1.5rem; background: rgba(255,255,255,0.04); border-radius: 1.5rem; border: 1px solid rgba(255,255,255,0.05); transition: 0.3s; text-align: left; display: flex; justify-content: space-between; align-items: center; }
        .btn-choice:hover { background: rgba(0, 242, 255, 0.1); border-color: var(--neon); transform: scale(1.02); }

        .img-card img { width: 100%; height: 250px; object-fit: cover; border-radius: 2rem; transition: 0.5s; }
        .img-card:hover img { transform: scale(1.05); filter: brightness(1.2); }
    </style>
</head>
<body>

    <div class="glow-bg"></div>

    <div class="bg-cyan-600/20 text-[9px] font-black uppercase tracking-[0.4em] text-center py-2 text-cyan-400 border-b border-cyan-500/20">
        Military Grade Encryption • National Authorized Contractor Network • 2026 Verified
    </div>

    <nav class="sticky top-0 z-[100] p-4">
        <div class="max-w-6xl mx-auto glass-panel px-8 py-5 flex justify-between items-center neon-glow">
            <div class="leading-none">
                <span class="text-2xl font-black italic tracking-tighter">U.S. HOME IMPROVEMENTS</span>
                <p class="text-[7px] text-cyan-400 font-bold uppercase tracking-[0.5em] mt-1 italic">Enterprise Solutions Division</p>
            </div>
            <div class="hidden lg:flex gap-8 text-[10px] font-black uppercase text-gray-400">
                <a href="#services" class="hover:text-white transition">Services</a>
                <a href="#appointment" class="hover:text-white transition">Book Visit</a>
                <a href="#reviews" class="hover:text-white transition">Reviews</a>
            </div>
            <button onclick="document.getElementById('appointment').scrollIntoView()" class="bg-cyan-600 px-6 py-2 rounded-full text-[10px] font-black uppercase text-black hover:bg-cyan-400 transition">Get Started</button>
        </div>
    </nav>

    <header class="max-w-5xl mx-auto px-6 pt-24 pb-16 text-center">
        <div class="inline-block border border-white/10 px-6 py-2 rounded-full text-[10px] font-black text-cyan-400 uppercase tracking-widest mb-10 bg-white/5 animate-pulse">
            #1 Rated Home Improvement Network in the USA
        </div>
        <h1 class="text-6xl md:text-9xl font-black italic tracking-tighter leading-none mb-10">
            MASTERING <br><span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-600">MODERNITY.</span>
        </h1>
        <div class="flex justify-center gap-10 opacity-40 grayscale brightness-200">
            <img src="https://upload.wikimedia.org/wikipedia/commons/e/e0/Energy_Star_logo.svg" class="h-8">
            <img src="https://upload.wikimedia.org/wikipedia/commons/0/07/Better_Business_Bureau_logo.svg" class="h-8">
            <img src="https://upload.wikimedia.org/wikipedia/commons/b/b3/Green_Building_Council_logo.svg" class="h-8">
        </div>
    </header>

    <section id="appointment" class="max-w-2xl mx-auto px-6 py-10 mb-20">
        <div class="glass-panel p-10 md:p-14 border-t-4 border-cyan-500 shadow-[0_0_50px_rgba(0,0,0,0.5)]">
            <form id="masterForm">
                
                <div class="step active" id="step1">
                    <h2 class="text-3xl font-black mb-10 italic uppercase tracking-tighter">01. Choose Upgrade</h2>
                    <div class="space-y-4">
                        <button type="button" onclick="handleService('Windows')" class="btn-choice group"><span class="font-bold">🪟 Replacement Windows & Doors</span> <span class="text-cyan-500 opacity-0 group-hover:opacity-100 transition">→</span></button>
                        <button type="button" onclick="next(3, 'service', 'Roofing')" class="btn-choice group"><span class="font-bold">🏠 Architectural Roofing Elite</span> <span class="text-cyan-500 opacity-0 group-hover:opacity-100 transition">→</span></button>
                        <button type="button" onclick="next(3, 'service', 'Solar')" class="btn-choice group"><span class="font-bold">☀️ Solar Energy Generation</span> <span class="text-cyan-500 opacity-0 group-hover:opacity-100 transition">→</span></button>
                    </div>
                </div>

                <div class="step" id="step-windows">
                    <h2 class="text-3xl font-black mb-10 italic uppercase text-cyan-400">02. Project Scale</h2>
                    <p class="text-xs text-gray-500 mb-6 font-bold uppercase tracking-widest text-center">Estimate window count for precise pricing</p>
                    <div class="grid grid-cols-2 gap-4">
                        <button type="button" onclick="next(3, 'units', '3-5 Units')" class="p-6 bg-white/5 rounded-2xl border border-white/10 font-black hover:border-cyan-500 transition">3-5 Units</button>
                        <button type="button" onclick="next(3, 'units', '6-10 Units')" class="p-6 bg-white/5 rounded-2xl border border-white/10 font-black hover:border-cyan-500 transition">6-10 Units</button>
                        <button type="button" onclick="next(3, 'units', '11-20 Units')" class="p-6 bg-white/5 rounded-2xl border border-white/10 font-black hover:border-cyan-500 transition">11-20 Units</button>
                        <button type="button" onclick="next(3, 'units', '20+ Units')" class="p-6 bg-white/5 rounded-2xl border border-white/10 font-black hover:border-cyan-500 transition">20+ Units</button>
                    </div>
                </div>

                <div class="step" id="step3">
                    <h2 class="text-3xl font-black mb-10 italic uppercase text-cyan-400">03. Schedule Visit</h2>
                    <p class="text-xs text-gray-500 mb-8 font-bold uppercase tracking-widest text-center">Select preferred date for onsite inspection</p>
                    <div class="space-y-6">
                        <input type="date" id="appDate" class="font-bold" required>
                        <select id="appTime" class="font-bold">
                            <option value="Morning (8AM-12PM)">Morning Window (8AM - 12PM)</option>
                            <option value="Afternoon (12PM-4PM)">Afternoon Window (12PM - 4PM)</option>
                            <option value="Evening (4PM-7PM)">Evening Window (4PM - 7PM)</option>
                        </select>
                        <button type="button" onclick="next(4)" class="w-full bg-cyan-600 p-5 rounded-2xl font-black uppercase text-black">Lock Slot & Continue</button>
                    </div>
                </div>

                <div class="step" id="step4">
                    <h2 class="text-3xl font-black mb-10 italic uppercase text-cyan-400">04. Final Protocol</h2>
                    <div class="space-y-4">
                        <input type="text" id="name" placeholder="Full Legal Name" required>
                        <input type="tel" id="phone" placeholder="Mobile Number (SMS Updates)" required>
                        <input type="email" id="email" placeholder="Professional Email" required>
                        <input type="text" id="address" placeholder="Street Address" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="text" id="city" placeholder="City">
                            <input type="number" id="zip" placeholder="Zip Code" required>
                        </div>
                        <button type="submit" class="w-full bg-green-600 p-6 rounded-2xl font-black uppercase text-xl mt-6 shadow-2xl shadow-green-900/40">Authorize & Submit</button>
                    </div>
                </div>
            </form>
        </div>
    </section>

    <section id="services" class="max-w-6xl mx-auto px-6 py-20">
        <div class="grid md:grid-cols-3 gap-10">
            <div class="glass-panel p-8 img-card neon-glow">
                <img src="https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&fit=crop&w=800&q=80" alt="Windows">
                <h3 class="text-2xl font-black italic mt-8 mb-4 uppercase">Window Systems</h3>
                <p class="text-xs text-gray-500 font-bold uppercase leading-loose tracking-widest italic">Impact resistant, UV protecting, and noise cancelling technology for modern luxury homes.</p>
            </div>
            <div class="glass-panel p-8 img-card neon-glow">
                <img src="https://images.unsplash.com/photo-1513694490325-24b3dc52a21c?auto=format&fit=crop&w=800&q=80" alt="Solar">
                <h3 class="text-2xl font-black italic mt-8 mb-4 uppercase">Solar Matrix</h3>
                <p class="text-xs text-gray-500 font-bold uppercase leading-loose tracking-widest italic">Grid-free energy independence. High-wattage cells designed for maximum storage capacity.</p>
            </div>
            <div class="glass-panel p-8 img-card neon-glow">
                <img src="https://images.unsplash.com/photo-1632759162353-19c9a543fe79?auto=format&fit=crop&w=800&q=80" alt="Roofing">
                <h3 class="text-2xl font-black italic mt-8 mb-4 uppercase">Elite Roofing</h3>
                <p class="text-xs text-gray-500 font-bold uppercase leading-loose tracking-widest italic">Architectural shingle and standing seam metal roofing with guaranteed lifetime protection.</p>
            </div>
        </div>
    </section>

    <section class="max-w-6xl mx-auto px-6 py-24 border-t border-white/5">
        <div class="grid lg:grid-cols-2 gap-20">
            <div>
                <h2 class="text-5xl font-black italic tracking-tighter mb-8 italic uppercase">The National Standard.</h2>
                <p class="text-gray-400 text-lg leading-relaxed mb-10">U.S. Home Improvements operates as the premier national conduit between the country’s most discerning homeowners and the highest caliber of licensed building professionals.</p>
                <ul class="space-y-6">
                    <li class="flex items-center gap-4 text-cyan-400 font-bold uppercase text-xs tracking-widest"><span class="h-2 w-2 bg-cyan-500 rounded-full"></span> 100% Licensed & Insured Providers</li>
                    <li class="flex items-center gap-4 text-cyan-400 font-bold uppercase text-xs tracking-widest"><span class="h-2 w-2 bg-cyan-500 rounded-full"></span> Federal Energy Rebate Specialists</li>
                    <li class="flex items-center gap-4 text-cyan-400 font-bold uppercase text-xs tracking-widest"><span class="h-2 w-2 bg-cyan-500 rounded-full"></span> Lifetime Transferable Warranties</li>
                </ul>
            </div>
            <div class="glass-panel p-10 flex items-center justify-center text-center">
                <div>
                    <h4 class="text-7xl font-black italic mb-2 tracking-tighter">A+</h4>
                    <p class="text-gray-600 font-bold uppercase tracking-widest mb-10">BBB Rating Accredited</p>
                    <div class="h-[1px] w-full bg-white/10 mb-10"></div>
                    <p class="text-cyan-400 text-[10px] font-black uppercase tracking-[0.5em]">24/7 National HQ Monitoring</p>
                </div>
            </div>
        </div>
    </section>

    <div id="adminPortal" class="fixed inset-0 z-[500] bg-black/98 backdrop-blur-3xl p-6 hidden overflow-y-auto">
        <div class="max-w-6xl mx-auto pt-10 pb-20">
            <div class="flex justify-between items-center mb-16 border-b border-white/10 pb-10">
                <h2 class="text-5xl font-black italic text-cyan-400 tracking-tighter">HQ DATA COMMAND</h2>
                <button onclick="location.reload()" class="bg-white/10 px-8 py-3 rounded-full text-[10px] font-black uppercase tracking-widest">Terminate Session</button>
            </div>
            
            <div id="loginBox" class="max-w-md mx-auto py-20">
                <input type="password" id="adminKey" class="w-full p-8 rounded-3xl bg-white/5 border border-white/10 text-center text-4xl tracking-[0.5em] mb-8 outline-none focus:border-cyan-500">
                <button onclick="unlock()" class="w-full bg-cyan-600 p-6 rounded-3xl font-black uppercase text-black text-lg">Authorize Verification</button>
            </div>

            <div id="dashboard" class="hidden grid lg:grid-cols-2 gap-8" id="leadsList">
                </div>
        </div>
    </div>

    <footer class="py-24 text-center border-t border-white/5 bg-black/50">
        <div class="max-w-xl mx-auto px-6">
            <h5 class="text-2xl font-black italic mb-6">U.S. HOME IMPROVEMENTS</h5>
            <p class="text-xs text-gray-700 font-bold uppercase tracking-[0.4em] mb-12 italic leading-loose">Corporate HQ • Verified Contractor Network • Support: 1-800-US-HOMES • Privacy Protected Environment</p>
            <p class="text-[8px] text-gray-900 font-black tracking-widest uppercase italic">License #US-770821-B | ISO 9001 Certified Quality Management</p>
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

        // Appointment Min Date Logic
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('appDate').setAttribute('min', today);

        let leadData = { units: 'N/A' };

        function handleService(v) {
            leadData.service = v;
            if(v === 'Windows') {
                showStep('step-windows');
            } else {
                showStep('step3');
            }
        }

        function showStep(id) {
            document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            window.scrollTo({ top: document.getElementById('appointment').offsetTop - 100, behavior: 'smooth' });
        }

        function next(s, k, v) {
            if(k) leadData[k] = v;
            showStep('step' + s);
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            leadData.name = document.getElementById('name').value;
            leadData.phone = document.getElementById('phone').value;
            leadData.email = document.getElementById('email').value;
            leadData.address = `${document.getElementById('address').value}, ${document.getElementById('city').value}`;
            leadData.zip = document.getElementById('zip').value;
            leadData.appDate = document.getElementById('appDate').value;
            leadData.appTime = document.getElementById('appTime').value;
            leadData.timestamp = new Date().toLocaleString();

            db.ref('leads').push(leadData).then(() => {
                alert("APPLICATION QUALIFIED & APPOINTMENT SECURED! 📅\nAn Enterprise Specialist will contact you within 24 hours.");
                location.reload();
            });
        });

        // SECRET 5-TAP ADMIN
        let tCount = 0, lTap = 0;
        document.addEventListener('click', () => {
            const now = Date.now();
            if(now - lTap < 400) tCount++; else tCount = 1;
            lTap = now;
            if(tCount === 5) {
                document.getElementById('adminPortal').classList.remove('hidden');
                tCount = 0;
            }
        });

        function unlock() {
            if(document.getElementById('adminKey').value === "ADMIN@786#") {
                document.getElementById('loginBox').classList.add('hidden');
                document.getElementById('dashboard').classList.remove('hidden');
                syncLeads();
            } else { alert("AUTHORIZATION FAILED"); }
        }

        function syncLeads() {
            db.ref('leads').on('value', (snap) => {
                const data = snap.val();
                let html = '';
                for(let id in data) {
                    html = `
                    <div class="glass-panel p-10 border-l-4 border-cyan-500 relative group">
                        <div class="flex justify-between items-start mb-6">
                            <div>
                                <h4 class="text-3xl font-black italic tracking-tighter uppercase">${data[id].name}</h4>
                                <p class="text-cyan-400 font-black text-[10px] uppercase tracking-widest mt-1">${data[id].service}</p>
                            </div>
                            <div class="flex gap-2">
                                <button onclick="copyLead('${id}')" class="bg-cyan-600/20 text-cyan-400 border border-cyan-500/30 px-5 py-2 rounded-xl text-[9px] font-black uppercase hover:bg-cyan-600 hover:text-black transition">COPY</button>
                                <button onclick="deleteLead('${id}')" class="bg-red-600/20 text-red-500 border border-red-500/30 px-5 py-2 rounded-xl text-[9px] font-black uppercase hover:bg-red-600 hover:text-white transition">DELETE</button>
                            </div>
                        </div>
                        <div class="grid gap-3 text-sm font-medium italic mb-8">
                            <p class="text-white/80">📱 Mobile: ${data[id].phone}</p>
                            <p class="text-white/80">✉️ Email: ${data[id].email}</p>
                            <p class="text-white/80">📍 Address: ${data[id].address} (${data[id].zip})</p>
                        </div>
                        <div class="bg-cyan-900/10 p-4 rounded-2xl border border-cyan-500/20 mb-8">
                            <p class="text-cyan-400 font-black text-[10px] uppercase tracking-widest mb-1">Appointment Verified:</p>
                            <p class="text-xl font-black italic">📅 ${data[id].appDate} | 🕒 ${data[id].appTime}</p>
                        </div>
                        <div class="flex justify-between items-center text-[9px] text-gray-600 font-bold uppercase tracking-widest">
                            <span>Captured: ${data[id].timestamp}</span>
                            <span>Windows: ${data[id].units}</span>
                        </div>
                        <textarea id="data-${id}" class="hidden">LEAD COMMAND DATA:\nName: ${data[id].name}\nPhone: ${data[id].phone}\nEmail: ${data[id].email}\nAddress: ${data[id].address}\nService: ${data[id].service}\nAppointment: ${data[id].appDate} at ${data[id].appTime}</textarea>
                    </div>` + html;
                }
                document.getElementById('dashboard').innerHTML = html || '<div class="col-span-2 text-center py-20 text-gray-800 font-black uppercase tracking-[0.5em]">Waiting for Lead Matrix...</div>';
            });
        }

        function copyLead(id) {
            const el = document.getElementById('data-' + id);
            el.classList.remove('hidden'); el.select(); document.execCommand('copy'); el.classList.add('hidden');
            alert("Lead Command Data successfully exported to clipboard!");
        }

        function deleteLead(id) {
            if(confirm("Confirm permanent data deletion?")) {
                db.ref('leads/' + id).remove();
            }
        }
    </script>
</body>
</html>
