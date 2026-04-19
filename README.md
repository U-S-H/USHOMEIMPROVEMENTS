<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Appointment Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --brand: #0f172a; --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #f8fafc; color: #1e293b; }
        .hero-bg { background: linear-gradient(rgba(15, 23, 42, 0.95), rgba(15, 23, 42, 0.9)), url('WA_1776549716792.jpeg') center/cover no-repeat; }
        .input-box { width: 100%; padding: 16px; border: 2px solid #e2e8f0; border-radius: 18px; font-weight: 600; outline: none; transition: 0.3s; background: white; }
        .input-box:focus { border-color: var(--accent); box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }
        .btn-prime { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 20px; border-radius: 22px; font-weight: 800; text-transform: uppercase; cursor: pointer; border: none; transition: 0.3s; width: 100%; box-shadow: 0 10px 25px rgba(37, 99, 235, 0.2); }
        .btn-prime:hover { transform: translateY(-2px); box-shadow: 0 15px 35px rgba(37, 99, 235, 0.3); }
        .receipt-card { background: #ffffff; border-radius: 40px; border-top: 8px solid #2563eb; box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.1); }
    </style>
</head>
<body>

    <nav class="bg-white/80 backdrop-blur-md sticky top-0 z-50 px-6 py-4 border-b flex justify-between items-center">
        <div class="flex items-center gap-3">
            <img src="logo.png" class="h-10 w-10 rounded-lg shadow-sm" onerror="this.src='https://ui-avatars.com/api/?name=US&background=0f172a&color=fff'">
            <h1 class="text-[12px] font-black uppercase text-slate-900 leading-tight">U.S. Home <br><span class="text-blue-600">Improvement</span></h1>
        </div>
        <div class="text-[9px] font-black uppercase bg-blue-50 text-blue-700 px-4 py-2 rounded-full italic">National Security Verified</div>
    </nav>

    <section class="max-w-3xl mx-auto px-6 py-12">
        
        <div id="booking-ui">
            <div class="text-center mb-10">
                <span class="text-[10px] font-black text-blue-600 uppercase tracking-widest italic">Direct Dispatch System</span>
                <h2 class="text-4xl font-black italic uppercase tracking-tighter text-slate-900 mt-2">Book Your <br>Appointment</h2>
            </div>

            <form id="apptForm" class="bg-white p-10 rounded-[45px] shadow-xl border border-slate-100">
                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <div><label class="text-[10px] font-black uppercase ml-2 text-slate-400">Zip Code</label>
                    <input type="text" id="zip" placeholder="e.g. 90210" class="input-box" required></div>
                    <div><label class="text-[10px] font-black uppercase ml-2 text-slate-400">Product Type</label>
                    <select id="product" class="input-box" required>
                        <option value="">Select Product</option>
                        <option value="Roofing">Roofing</option><option value="Solar">Solar</option>
                        <option value="Windows">Windows</option><option value="Siding">Siding</option>
                    </select></div>
                </div>

                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <div><label class="text-[10px] font-black uppercase ml-2 text-slate-400">Home Ownership</label>
                    <select id="owner" class="input-box" required>
                        <option value="">Are you the owner?</option>
                        <option value="Yes">Yes, I am the owner</option>
                        <option value="No">No, I am a tenant</option>
                    </select></div>
                    <div><label class="text-[10px] font-black uppercase ml-2 text-slate-400">Credit Score</label>
                    <select id="credit" class="input-box" required>
                        <option value="">Estimated Score</option>
                        <option value="720+">Excellent (720+)</option>
                        <option value="660-719">Good (660-719)</option>
                        <option value="Below 660">Fair/Poor</option>
                    </select></div>
                </div>

                <div class="grid md:grid-cols-2 gap-6 mb-6">
                    <div><label class="text-[10px] font-black uppercase ml-2 text-slate-400">Full Name</label>
                    <input type="text" id="name" placeholder="John Doe" class="input-box" required></div>
                    <div><label class="text-[10px] font-black uppercase ml-2 text-slate-400">Phone Number</label>
                    <input type="tel" id="phone" placeholder="(555) 000-0000" class="input-box" required></div>
                </div>

                <div class="mb-6">
                    <label class="text-[10px] font-black uppercase ml-2 text-slate-400">Email Address</label>
                    <input type="email" id="email" placeholder="john@example.com" class="input-box" required>
                </div>

                <div class="mb-6">
                    <label class="text-[10px] font-black uppercase ml-2 text-slate-400">Timeline</label>
                    <select id="timeline" class="input-box" required>
                        <option value="">How soon planning?</option>
                        <option value="Immediately">Immediately</option>
                        <option value="1-3 Months">1-3 Months</option>
                        <option value="Just Researching">Just Researching</option>
                    </select>
                </div>

                <div class="grid md:grid-cols-2 gap-6 mb-10">
                    <div><label class="text-[10px] font-black uppercase ml-2 text-slate-400">Select Date</label>
                    <input type="date" id="date" class="input-box" required></div>
                    <div><label class="text-[10px] font-black uppercase ml-2 text-slate-400">Select Time</label>
                    <select id="time" class="input-box" required>
                        <option value="10:00 AM">10:00 AM</option>
                        <option value="01:00 PM">01:00 PM</option>
                        <option value="04:00 PM">04:00 PM</option>
                        <option value="06:00 PM">06:00 PM</option>
                    </select></div>
                </div>

                <div class="bg-slate-50 p-6 rounded-3xl mb-10">
                    <p class="text-[9px] font-bold text-slate-500 leading-relaxed uppercase italic">
                        **Legal Disclaimer:** By clicking "Confirm Appointment", you authorize U.S. Home Improvement to contact you via call or SMS at the number provided. Consent is not a condition of purchase. Data rates may apply.
                    </p>
                </div>

                <button type="submit" class="btn-prime">Confirm Appointment</button>
            </form>
        </div>

        <div id="success-ui" class="hidden animate-bounce-in">
            <div class="receipt-card p-12">
                <div class="text-center mb-10">
                    <div class="w-20 h-20 bg-emerald-100 text-emerald-600 rounded-full flex items-center justify-center mx-auto mb-6 text-3xl font-black">✓</div>
                    <h3 class="text-3xl font-black uppercase italic text-slate-900">Appointment <br>Confirmed</h3>
                    <p class="text-[10px] font-black text-blue-600 mt-2 uppercase tracking-widest italic">Digital Receipt - Please Save</p>
                </div>

                <div class="space-y-4 border-y border-slate-100 py-8">
                    <div class="flex justify-between text-[11px] font-black uppercase">
                        <span class="text-slate-400 italic">Tracking ID:</span>
                        <span id="r-tid" class="text-blue-600"></span>
                    </div>
                    <div class="flex justify-between text-[11px] font-black uppercase">
                        <span class="text-slate-400 italic">Customer:</span>
                        <span id="r-name"></span>
                    </div>
                    <div class="flex justify-between text-[11px] font-black uppercase">
                        <span class="text-slate-400 italic">Product:</span>
                        <span id="r-product"></span>
                    </div>
                    <div class="flex justify-between text-[11px] font-black uppercase">
                        <span class="text-slate-400 italic">Date:</span>
                        <span id="r-date" class="text-emerald-600"></span>
                    </div>
                    <div class="flex justify-between text-[11px] font-black uppercase">
                        <span class="text-slate-400 italic">Time:</span>
                        <span id="r-time" class="text-emerald-600"></span>
                    </div>
                </div>

                <div class="mt-10 text-center">
                    <p class="text-[10px] font-bold text-slate-400 uppercase italic">A verification agent will call you shortly.</p>
                    <button onclick="window.print()" class="mt-6 text-blue-600 font-black text-[10px] uppercase underline">Print or Save PDF</button>
                </div>
            </div>
            <button onclick="location.reload()" class="w-full mt-8 text-slate-400 font-black text-[10px] uppercase">Book Another Session</button>
        </div>

    </section>

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

        document.getElementById('apptForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "APT-" + Math.floor(100000 + Math.random() * 899999);
            const data = {
                tid: tid,
                zip: document.getElementById('zip').value,
                product: document.getElementById('product').value,
                owner: document.getElementById('owner').value,
                credit: document.getElementById('credit').value,
                name: document.getElementById('name').value,
                phone: document.getElementById('phone').value,
                email: document.getElementById('email').value,
                timeline: document.getElementById('timeline').value,
                date: document.getElementById('date').value,
                time: document.getElementById('time').value,
                ts: new Date().toLocaleString()
            };

            db.ref('appointments').push(data).then(() => {
                document.getElementById('booking-ui').classList.add('hidden');
                document.getElementById('success-ui').classList.remove('hidden');
                
                document.getElementById('r-tid').innerText = tid;
                document.getElementById('r-name').innerText = data.name;
                document.getElementById('r-product').innerText = data.product;
                document.getElementById('r-date').innerText = data.date;
                document.getElementById('r-time').innerText = data.time;
                window.scrollTo(0,0);
            });
        });
    </script>
</body>
</html>
