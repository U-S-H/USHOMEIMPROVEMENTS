<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise Terminal</title>
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
        .label-text { font-size: 10px; font-weight: 800; text-transform: uppercase; color: #94a3b8; margin-left: 8px; margin-bottom: 6px; display: block; letter-spacing: 0.5px; }
    </style>
</head>
<body>

    <section class="max-w-xl mx-auto px-4 py-12">
        <div id="main-container" class="bg-white p-8 md:p-12 rounded-[40px] shadow-2xl border border-slate-100">
            
            <div class="mb-10 text-center">
                <div class="flex justify-between text-[10px] font-black uppercase text-slate-400 mb-2 italic">
                    <span id="step-txt">Step 1 of 4</span>
                    <span id="perc-txt">25%</span>
                </div>
                <div class="h-1.5 w-full bg-slate-100 rounded-full overflow-hidden">
                    <div id="p-bar" class="progress-fill w-1/4"></div>
                </div>
                <p class="text-[9px] font-black text-blue-600 mt-3 uppercase tracking-[0.3em]">National Authorized Dispatch</p>
            </div>

            <form id="masterForm">
                <div class="step-node active" id="step1">
                    <h3 class="text-2xl font-black italic uppercase mb-8 tracking-tighter">Service <span class="text-blue-600">Selection</span></h3>
                    <div class="space-y-5">
                        <div>
                            <span class="label-text">Area Zip Code</span>
                            <input type="text" id="zip" placeholder="e.g. 90210" class="input-elite" required>
                        </div>
                        <div>
                            <span class="label-text">Project Category</span>
                            <select id="product" class="input-elite" onchange="toggleProductDetails()" required>
                                <option value="">Select Service (20+ Available)</option>
                                <option value="Roofing">Roofing</option>
                                <option value="Windows">Windows</option>
                                <option value="Solar">Solar Panels</option>
                                <option value="Siding">Siding</option>
                                <option value="Kitchen">Kitchen Remodel</option>
                                <option value="Bathroom">Bathroom Remodel</option>
                                <option value="HVAC">HVAC (AC/Heating)</option>
                                <option value="Gutters">Gutters</option>
                                <option value="Insulation">Insulation</option>
                                <option value="Flooring">Flooring</option>
                                <option value="Painting_In">Interior Painting</option>
                                <option value="Painting_Ex">Exterior Painting</option>
                                <option value="Deck">Deck & Patio</option>
                                <option value="Basement">Basement Finishing</option>
                                <option value="Garage">Garage Doors</option>
                                <option value="Fencing">Fencing</option>
                                <option value="Pool">Pools & Spas</option>
                                <option value="Landscaping">Landscaping</option>
                                <option value="Security">Home Security</option>
                                <option value="Plumbing">Plumbing</option>
                            </select>
                        </div>
                        <button type="button" onclick="go(2)" class="btn-next">Continue</button>
                    </div>
                </div>

                <div class="step-node" id="step2">
                    <h3 class="text-2xl font-black italic uppercase mb-8 tracking-tighter">Project <span class="text-blue-600">Details</span></h3>
                    
                    <div id="win-options" class="hidden space-y-5 mb-6">
                        <div>
                            <span class="label-text">Number of Windows</span>
                            <select id="win-count" class="input-elite">
                                <script>for(let i=1; i<=30; i++) document.write(`<option value="${i}">${i} Windows</option>`);</script>
                                <option value="30+">More than 30 Windows</option>
                            </select>
                        </div>
                        <div>
                            <span class="label-text">Window Style</span>
                            <select id="win-type" class="input-elite">
                                <option value="Sliding">Sliding</option><option value="Double-Hung">Double-Hung</option>
                                <option value="Casement">Casement</option><option value="Aluminum">Aluminum</option>
                                <option value="Vinyl">Vinyl</option><option value="Other">Other Type</option>
                            </select>
                        </div>
                    </div>

                    <div id="roof-options" class="hidden space-y-5 mb-6">
                        <div>
                            <span class="label-text">Roof Material Preference</span>
                            <select id="roof-type" class="input-elite">
                                <option value="Asphalt Shingles">Asphalt Shingles</option>
                                <option value="Metal">Metal</option><option value="Tile">Tile</option>
                                <option value="Flat">Flat Roof</option><option value="Other">Other Material</option>
                            </select>
                        </div>
                    </div>

                    <div class="mb-6">
                        <span class="label-text">Specific Requirements / Notes</span>
                        <textarea id="manual-note" placeholder="Tell us more about your project needs..." class="input-elite h-24 pt-4"></textarea>
                    </div>

                    <div class="flex gap-3">
                        <button type="button" onclick="go(1)" class="w-1/3 font-bold text-slate-300 uppercase text-[10px]">Back</button>
                        <button type="button" onclick="go(3)" class="btn-next">Next</button>
                    </div>
                </div>

                <div class="step-node" id="step3">
                    <h3 class="text-2xl font-black italic uppercase mb-8 tracking-tighter">Owner <span class="text-blue-600">Verification</span></h3>
                    <div class="space-y-5">
                        <div class="grid grid-cols-2 gap-4">
                            <select id="owner" class="input-elite" required>
                                <option value="">Owner?</option><option value="Yes">Yes</option><option value="No">No</option>
                            </select>
                            <select id="credit" class="input-elite" required>
                                <option value="">Credit Score</option>
                                <option value="Excellent">720+</option><option value="Good">660-719</option><option value="Fair">Below 660</option>
                            </select>
                        </div>
                        <input type="text" id="name" placeholder="Full Name" class="input-elite" required>
                        <input type="tel" id="phone" placeholder="Phone Number" class="input-elite" required>
                        <input type="email" id="email" placeholder="Email Address" class="input-elite" required>
                        <input type="text" id="addr" placeholder="Physical Property Address" class="input-elite" required>
                        
                        <div class="flex gap-3">
                            <button type="button" onclick="go(2)" class="w-1/3 font-bold text-slate-300 uppercase text-[10px]">Back</button>
                            <button type="button" onclick="go(4)" class="btn-next">Finalize</button>
                        </div>
                    </div>
                </div>

                <div class="step-node" id="step4">
                    <h3 class="text-2xl font-black italic uppercase mb-8 tracking-tighter">Set <span class="text-blue-600">Appointment</span></h3>
                    <div class="space-y-5">
                        <select id="timeline" class="input-elite" required>
                            <option value="">When do you want to start?</option>
                            <option value="Immediately">Immediately</option>
                            <option value="1-3 Months">1-3 Months</option>
                            <option value="Researching">Just Researching</option>
                        </select>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="date" id="date" class="input-elite" required>
                            <select id="time" class="input-elite" required>
                                <option value="10:00 AM">10:00 AM</option><option value="01:00 PM">01:00 PM</option><option value="04:00 PM">04:00 PM</option>
                            </select>
                        </div>
                        <div class="p-4 bg-blue-50 border border-blue-100 rounded-2xl">
                            <p class="text-[9px] font-bold text-blue-700 uppercase italic leading-relaxed">Legal: By submitting, you authorize U.S. Home Improvement to contact you regarding this appointment via phone/SMS.</p>
                        </div>
                        <div class="flex gap-3">
                            <button type="button" onclick="go(3)" class="w-1/3 font-bold text-slate-300 uppercase text-[10px]">Back</button>
                            <button type="submit" class="btn-next bg-blue-700 shadow-xl">Confirm Appointment</button>
                        </div>
                    </div>
                </div>
            </form>
        </div>

        <div id="receipt" class="hidden text-center bg-white p-12 rounded-[50px] shadow-3xl border-t-[10px] border-emerald-500">
            <h3 class="text-2xl font-black italic uppercase mb-6">Dispatch <span class="text-emerald-500">Ready</span></h3>
            <div id="receipt-data" class="text-left space-y-4 bg-slate-50 p-8 rounded-3xl font-bold text-[10px] uppercase italic mb-8"></div>
            <p class="text-[10px] text-slate-400 font-black uppercase mb-8 tracking-widest">Screenshot this for your session verification.</p>
            <button onclick="location.reload()" class="text-blue-600 font-black text-[10px] uppercase underline">Return Home</button>
        </div>
    </section>

    <script>
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
            window.scrollTo(0,0);
        }

        document.getElementById('masterForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-" + Math.floor(100000 + Math.random() * 899999);
            const p = document.getElementById('product').value;
            let spec = document.getElementById('manual-note').value || "Standard Request";
            if(p === 'Windows') spec = `${document.getElementById('win-count').value} x ${document.getElementById('win-type').value} | ${spec}`;
            if(p === 'Roofing') spec = `${document.getElementById('roof-type').value} | ${spec}`;
            
            const data = { tid, zip: document.getElementById('zip').value, product: p, spec, owner: document.getElementById('owner').value, credit: document.getElementById('credit').value, name: document.getElementById('name').value, phone: document.getElementById('phone').value, email: document.getElementById('email').value, address: document.getElementById('addr').value, timeline: document.getElementById('timeline').value, date: document.getElementById('date').value, time: document.getElementById('time').value, ts: new Date().toLocaleString() };

            db.ref('leads').push(data).then(() => {
                document.getElementById('main-container').classList.add('hidden');
                document.getElementById('receipt').classList.remove('hidden');
                document.getElementById('receipt-data').innerHTML = `
                    <p class="flex justify-between border-b pb-2"><span>Tracking ID:</span> <span class="text-blue-600">${tid}</span></p>
                    <p class="flex justify-between border-b pb-2"><span>Customer:</span> <span>${data.name}</span></p>
                    <p class="flex justify-between border-b pb-2"><span>Address:</span> <span>${data.address}</span></p>
                    <p class="flex justify-between border-b pb-2"><span>Service:</span> <span>${data.product}</span></p>
                    <p class="flex justify-between text-emerald-600"><span>Date:</span> <span>${data.date} @ ${data.time}</span></p>
                `;
            });
        });
    </script>
</body>
</html>
