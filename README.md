<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | Multi-Step Appointment Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fdfdfd; }
        .step-node { display: none; }
        .step-node.active { display: block; animation: slideIn 0.5s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }
        .input-elite { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 20px; font-weight: 600; outline: none; transition: 0.3s; background: #fff; }
        .input-elite:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-next { background: #2563eb; color: white; padding: 20px; border-radius: 20px; font-weight: 800; width: 100%; transition: 0.3s; }
        .progress-bar { height: 6px; background: #f1f5f9; border-radius: 10px; overflow: hidden; }
        .progress-fill { height: 100%; background: #2563eb; width: 25%; transition: 0.5s; }
    </style>
</head>
<body>

    <section class="max-w-xl mx-auto px-6 py-20">
        
        <div id="booking-container" class="bg-white p-10 rounded-[40px] shadow-2xl border border-slate-50">
            <div class="mb-10">
                <div class="flex justify-between text-[10px] font-black uppercase text-slate-400 mb-3 italic">
                    <span id="step-label">Step 1 of 4</span>
                    <span id="percent-label">25% Complete</span>
                </div>
                <div class="progress-bar"><div id="p-fill" class="progress-fill"></div></div>
            </div>

            <form id="multiStepForm">
                <div class="step-node active" id="step1">
                    <h3 class="text-2xl font-black italic uppercase mb-8">Project <span class="text-blue-600">Start</span></h3>
                    <div class="space-y-6">
                        <input type="text" id="zip" placeholder="Zip Code (e.g. 90210)" class="input-elite" required>
                        <select id="product" class="input-elite" required>
                            <option value="">Select Service Needed</option>
                            <option value="Roofing">Roofing</option><option value="Solar">Solar</option>
                            <option value="Windows">Windows</option><option value="Siding">Siding</option>
                        </select>
                        <button type="button" onclick="nextStep(2)" class="btn-next">Continue</button>
                    </div>
                </div>

                <div class="step-node" id="step2">
                    <h3 class="text-2xl font-black italic uppercase mb-8">Property <span class="text-blue-600">Details</span></h3>
                    <div class="space-y-6">
                        <select id="owner" class="input-elite" required>
                            <option value="">Do you own the home?</option>
                            <option value="Yes">Yes, I am the owner</option>
                            <option value="No">No, I am a tenant</option>
                        </select>
                        <select id="credit" class="input-elite" required>
                            <option value="">Est. Credit Score</option>
                            <option value="720+">Excellent (720+)</option>
                            <option value="660-719">Good (660-719)</option>
                            <option value="Below 660">Fair/Poor</option>
                        </select>
                        <div class="flex gap-4">
                            <button type="button" onclick="nextStep(1)" class="w-1/3 text-slate-400 font-bold uppercase text-[10px]">Back</button>
                            <button type="button" onclick="nextStep(3)" class="btn-next">Continue</button>
                        </div>
                    </div>
                </div>

                <div class="step-node" id="step3">
                    <h3 class="text-2xl font-black italic uppercase mb-8">Personal <span class="text-blue-600">Info</span></h3>
                    <div class="space-y-6">
                        <input type="text" id="name" placeholder="Full Legal Name" class="input-elite" required>
                        <input type="tel" id="phone" placeholder="Phone Number" class="input-elite" required>
                        <input type="email" id="email" placeholder="Email Address" class="input-elite" required>
                        <input type="text" id="addr" placeholder="Physical Home Address" class="input-elite" required>
                        <div class="flex gap-4">
                            <button type="button" onclick="nextStep(2)" class="w-1/3 text-slate-400 font-bold uppercase text-[10px]">Back</button>
                            <button type="button" onclick="nextStep(4)" class="btn-next">Final Step</button>
                        </div>
                    </div>
                </div>

                <div class="step-node" id="step4">
                    <h3 class="text-2xl font-black italic uppercase mb-8">Schedule <span class="text-blue-600">Visit</span></h3>
                    <div class="space-y-6">
                        <select id="timeline" class="input-elite" required>
                            <option value="">Project Timeline</option>
                            <option value="Immediately">Immediately</option>
                            <option value="1-3 Months">1-3 Months</option>
                        </select>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="date" id="date" class="input-elite" required>
                            <select id="time" class="input-elite" required>
                                <option value="10:00 AM">10:00 AM</option>
                                <option value="01:00 PM">01:00 PM</option>
                                <option value="04:00 PM">04:00 PM</option>
                            </select>
                        </div>
                        <p class="text-[9px] text-slate-400 font-bold uppercase text-center italic">** You are booking a direct site assessment visit.</p>
                        <div class="flex gap-4">
                            <button type="button" onclick="nextStep(3)" class="w-1/3 text-slate-400 font-bold uppercase text-[10px]">Back</button>
                            <button type="submit" class="btn-next bg-emerald-600">Confirm Booking</button>
                        </div>
                    </div>
                </div>
            </form>
        </div>

        <div id="success-ui" class="hidden text-center bg-white p-12 rounded-[50px] shadow-2xl border-t-[10px] border-blue-600">
            <h3 class="text-3xl font-black italic uppercase mb-6">Booking <span class="text-blue-600">Success</span></h3>
            <div class="space-y-4 text-left bg-slate-50 p-8 rounded-3xl mb-8 font-bold text-[11px] uppercase italic">
                <p class="flex justify-between border-b pb-3"><span>ID:</span> <span id="r-tid" class="text-blue-600"></span></p>
                <p class="flex justify-between border-b pb-3"><span>Name:</span> <span id="r-name"></span></p>
                <p class="flex justify-between border-b pb-3"><span>Address:</span> <span id="r-addr"></span></p>
                <p class="flex justify-between text-emerald-600"><span>Appointment:</span> <span id="r-dt"></span></p>
            </div>
            <p class="text-[10px] font-black text-slate-400 mb-8 uppercase">Save this screenshot for your records.</p>
            <button onclick="location.reload()" class="text-blue-600 font-black text-[10px] uppercase underline">Return Home</button>
        </div>
    </section>

    <script>
        // Firebase Init (Same as before)
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();

        function nextStep(step) {
            document.querySelectorAll('.step-node').forEach(n => n.classList.remove('active'));
            document.getElementById('step' + step).classList.add('active');
            
            // Update Progress
            const prog = (step / 4) * 100;
            document.getElementById('p-fill').style.width = prog + '%';
            document.getElementById('step-label').innerText = `Step ${step} of 4`;
            document.getElementById('percent-label').innerText = `${prog}% Complete`;
        }

        document.getElementById('multiStepForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "APT-" + Math.floor(100000 + Math.random() * 899999);
            const data = { tid: tid, zip: document.getElementById('zip').value, product: document.getElementById('product').value, owner: document.getElementById('owner').value, credit: document.getElementById('credit').value, name: document.getElementById('name').value, phone: document.getElementById('phone').value, email: document.getElementById('email').value, addr: document.getElementById('addr').value, timeline: document.getElementById('timeline').value, date: document.getElementById('date').value, time: document.getElementById('time').value, ts: new Date().toLocaleString() };

            db.ref('appointments').push(data).then(() => {
                document.getElementById('booking-container').classList.add('hidden');
                document.getElementById('success-ui').classList.remove('hidden');
                document.getElementById('r-tid').innerText = tid;
                document.getElementById('r-name').innerText = data.name;
                document.getElementById('r-addr').innerText = data.addr;
                document.getElementById('r-dt').innerText = data.date + ' @ ' + data.time;
            });
        });
    </script>
</body>
</html>
