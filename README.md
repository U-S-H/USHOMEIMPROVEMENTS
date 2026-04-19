<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | Contractor-Grade Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>

    <style>
        :root { --accent: #2563eb; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fdfdfd; color: #0f172a; }
        .step-node { display: none; }
        .step-node.active { display: block; animation: slideIn 0.4s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .input-elite { width: 100%; padding: 16px; border: 2px solid #f1f5f9; border-radius: 16px; font-weight: 600; outline: none; transition: 0.3s; background: #fff; font-size: 14px; }
        .input-elite:focus { border-color: var(--accent); box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }
        .btn-next { background: #2563eb; color: white; padding: 18px; border-radius: 18px; font-weight: 800; width: 100%; transition: 0.3s; text-transform: uppercase; letter-spacing: 1px; }
        .progress-fill { height: 100%; background: #2563eb; transition: 0.5s; }
        .label-text { font-[10px]; font-weight: 800; text-transform: uppercase; color: #94a3b8; margin-left: 8px; margin-bottom: 6px; display: block; letter-spacing: 0.5px; }
    </style>
</head>
<body>

    <section class="max-w-xl mx-auto px-4 py-12">
        <div id="main-container" class="bg-white p-8 md:p-12 rounded-[40px] shadow-2xl border border-slate-100">
            
            <div class="mb-10">
                <div class="flex justify-between text-[10px] font-black uppercase text-slate-400 mb-2 italic">
                    <span id="step-txt">Step 1 of 4</span>
                    <span id="perc-txt">25%</span>
                </div>
                <div class="h-1.5 w-full bg-slate-100 rounded-full overflow-hidden">
                    <div id="p-bar" class="progress-fill w-1/4"></div>
                </div>
            </div>

            <form id="masterForm">
                <div class="step-node active" id="step1">
                    <h3 class="text-2xl font-black italic uppercase mb-8 tracking-tighter">Initial <span class="text-blue-600">Scan</span></h3>
                    <div class="space-y-5">
                        <div>
                            <span class="label-text">Zip Code</span>
                            <input type="text" id="zip" placeholder="e.g. 90210" class="input-elite" required>
                        </div>
                        <div>
                            <span class="label-text">Select Service</span>
                            <select id="product" class="input-elite" onchange="toggleProductDetails()" required>
                                <option value="">What do you need?</option>
                                <option value="Roofing">Roofing (Replacement/Repair)</option>
                                <option value="Windows">Windows (Installation)</option>
                                <option value="Solar">Solar Panels</option>
                                <option value="Siding">Exterior Siding</option>
                            </select>
                        </div>
                        <button type="button" onclick="go(2)" class="btn-next">Next Step</button>
                    </div>
                </div>

                <div class="step-node" id="step2">
                    <h3 class="text-2xl font-black italic uppercase mb-8 tracking-tighter">Project <span class="text-blue-600">Specs</span></h3>
                    
                    <div id="win-options" class="hidden space-y-5 mb-6">
                        <div>
                            <span class="label-text">Number of Windows</span>
                            <select id="win-count" class="input-elite">
                                <script>
                                    for(let i=1; i<=30; i++) document.write(`<option value="${i}">${i} Windows</option>`);
                                </script>
                                <option value="30+">More than 30 Windows</option>
                            </select>
                        </div>
                        <div>
                            <span class="label-text">Window Type</span>
                            <select id="win-type" class="input-elite">
                                <option value="Sliding">Sliding</option>
                                <option value="Double-Hung">Double-Hung</option>
                                <option value="Casement">Casement</option>
                                <option value="Aluminum">Aluminum Frame</option>
                                <option value="Vinyl">Vinyl Frame</option>
                                <option value="Other">Other / Not Sure</option>
                            </select>
                        </div>
                    </div>

                    <div id="roof-options" class="hidden space-y-5 mb-6">
                        <div>
                            <span class="label-text">Roof Material Type</span>
                            <select id="roof-type" class="input-elite">
                                <option value="Asphalt Shingles">Asphalt Shingles</option>
                                <option value="Metal">Metal Roofing</option>
                                <option value="Tile">Clay / Concrete Tile</option>
                                <option value="Flat Roof">Flat / Rubber Roof</option>
                                <option value="Wood Shake">Wood Shake</option>
                                <option value="Other">Other Material</option>
                            </select>
                        </div>
                    </div>

                    <div class="mb-6">
                        <span class="label-text">Additional Details (Optional)</span>
                        <textarea id="manual-note" placeholder="Any specific requirements or 'Other' types..." class="input-elite h-24 pt-4"></textarea>
                    </div>

                    <div class="flex gap-3">
                        <button type="button" onclick="go(1)" class="w-1/3 font-bold text-slate-300 uppercase text-[10px]">Back</button>
                        <button type="button" onclick="go(3)" class="btn-next">Continue</button>
                    </div>
                </div>

                <div class="step-node" id="step3">
                    <h3 class="text-2xl font-black italic uppercase mb-8 tracking-tighter">Ownership <span class="text-blue-600">& Contact</span></h3>
                    <div class="space-y-5">
                        <div class="grid grid-cols-2 gap-4">
                            <select id="owner" class="input-elite" required>
                                <option value="">Home Owner?</option>
                                <option value="Yes">Yes</option><option value="No">No</option>
                            </select>
                            <select id="credit" class="input-elite" required>
                                <option value="">Credit Score</option>
                                <option value="Excellent">720+</option><option value="Good">660-719</option><option value="Building">Below 660</option>
                            </select>
                        </div>
                        <input type="text" id="name" placeholder="Full Name" class="input-elite" required>
                        <input type="tel" id="phone" placeholder="Phone Number" class="input-elite" required>
                        <input type="email" id="email" placeholder="Email Address" class="input-elite" required>
                        <input type="text" id="addr" placeholder="Full Physical Address (Street, City, State)" class="input-elite" required>
                        
                        <div class="flex gap-3">
                            <button type="button" onclick="go(2)" class="w-1/3 font-bold text-slate-300 uppercase text-[10px]">Back</button>
                            <button type="button" onclick="go(4)" class="btn-next">Last Step</button>
                        </div>
                    </div>
                </div>

                <div class="step-node" id="step4">
                    <h3 class="text-2xl font-black italic uppercase mb-8 tracking-tighter">Final <span class="text-blue-600">Booking</span></h3>
                    <div class="space-y-5">
                        <select id="timeline" class="input-elite" required>
                            <option value="">Planning to start?</option>
                            <option value="Immediately">Immediately</option>
                            <option value="1-3 Months">Within 1-3 Months</option>
                            <option value="Researching">Just Researching</option>
                        </select>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="date" id="date" class="input-elite" required>
                            <select id="time" class="input-elite" required>
                                <option value="10:00 AM">10:00 AM</option>
                                <option value="01:00 PM">01:00 PM</option>
                                <option value="04:00 PM">04:00 PM</option>
                            </select>
                        </div>
                        <div class="p-4 bg-slate-50 rounded-2xl">
                            <p class="text-[9px] font-bold text-slate-400 uppercase italic leading-relaxed">By submitting, you agree to a professional site assessment. A specialist will call to verify your details.</p>
                        </div>
                        <div class="flex gap-3">
                            <button type="button" onclick="go(3)" class="w-1/3 font-bold text-slate-300 uppercase text-[10px]">Back</button>
                            <button type="submit" class="btn-next bg-emerald-600">Confirm & Transmit</button>
                        </div>
                    </div>
                </div>
            </form>
        </div>

        <div id="receipt" class="hidden animate-bounce-in">
            <div class="bg-white p-10 rounded-[50px] shadow-2xl border-t-[10px] border-blue-600">
                <div class="text-center mb-8">
                    <div class="text-4xl mb-4">🛡️</div>
                    <h3 class="text-2xl font-black uppercase italic">Dispatch Authorized</h3>
                    <p class="text-[9px] font-black text-blue-500 uppercase tracking-widest mt-1 italic">Save for your records</p>
                </div>
                <div class="space-y-4 bg-slate-50 p-6 rounded-3xl font-bold text-[10px] uppercase italic">
                    <p class="flex justify-between border-b pb-2"><span>Ref ID:</span> <span id="r-tid" class="text-blue-600"></span></p>
                    <p class="flex justify-between border-b pb-2"><span>Client:</span> <span id="r-name"></span></p>
                    <p class="flex justify-between border-b pb-2"><span>Project:</span> <span id="r-svc"></span></p>
                    <p class="flex justify-between border-b pb-2"><span>Spec:</span> <span id="r-spec"></span></p>
                    <p class="flex justify-between text-emerald-600"><span>Schedule:</span> <span id="r-dt"></span></p>
                </div>
                <button onclick="location.reload()" class="w-full mt-8 text-slate-400 font-black text-[9px] uppercase underline">Return to Start</button>
            </div>
        </div>
    </section>

    <script>
        // Firebase Config (Keep as is)
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();

        function toggleProductDetails() {
            const p = document.getElementById('product').value;
            document.getElementById('win-options').classList.add('hidden');
            document.getElementById('roof-options').classList.add('hidden');
            if(p === 'Windows') document.getElementById('win-options').classList.remove('hidden');
            if(p === 'Roofing') document.getElementById('roof-options').classList.remove('hidden');
        }

        function go(s) {
            document.querySelectorAll('.step-node').forEach(n => n.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
            document.getElementById('p-bar').style.width = (s/4)*100 + '%';
            document.getElementById('step-txt').innerText = `Step ${s} of 4`;
            document.getElementById('perc-txt').innerText = (s/4)*100 + '%';
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-HUB-" + Math.floor(100000 + Math.random() * 899999);
            const p = document.getElementById('product').value;
            let spec = "";
            if(p === 'Windows') spec = `${document.getElementById('win-count').value} x ${document.getElementById('win-type').value}`;
            else if(p === 'Roofing') spec = document.getElementById('roof-type').value;
            
            const data = {
                tid: tid,
                zip: document.getElementById('zip').value,
                product: p,
                specification: spec,
                manual_note: document.getElementById('manual-note').value,
                owner: document.getElementById('owner').value,
                credit: document.getElementById('credit').value,
                name: document.getElementById('name').value,
                phone: document.getElementById('phone').value,
                email: document.getElementById('email').value,
                address: document.getElementById('addr').value,
                timeline: document.getElementById('timeline').value,
                date: document.getElementById('date').value,
                time: document.getElementById('time').value,
                ts: new Date().toLocaleString()
            };

            db.ref('leads').push(data).then(() => {
                document.getElementById('main-container').classList.add('hidden');
                document.getElementById('receipt').classList.remove('hidden');
                document.getElementById('r-tid').innerText = tid;
                document.getElementById('r-name').innerText = data.name;
                document.getElementById('r-svc').innerText = data.product;
                document.getElementById('r-spec').innerText = spec || "Standard";
                document.getElementById('r-dt').innerText = data.date + " @ " + data.time;
            });
        });
    </script>
</body>
</html>
