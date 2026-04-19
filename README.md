<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>U.S. HOME IMPROVEMENT | National Enterprise Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <style>
        :root { --primary: #0f172a; --accent: #2563eb; --success: #10b981; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fafafa; color: #1e293b; overflow-x: hidden; }
        
        /* UI Elements */
        .glass-card { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(10px); border: 1px solid rgba(0,0,0,0.05); }
        .input-premium { width: 100%; padding: 18px; border: 2px solid #f1f5f9; border-radius: 20px; font-weight: 600; outline: none; transition: 0.4s; background: white; font-size: 15px; }
        .input-premium:focus { border-color: var(--accent); box-shadow: 0 0 0 5px rgba(37, 99, 235, 0.1); }
        .btn-master { background: linear-gradient(135deg, #1e3a8a, #2563eb); color: white; padding: 22px; border-radius: 22px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; transition: 0.4s; box-shadow: 0 12px 30px rgba(37, 99, 235, 0.2); width: 100%; cursor: pointer; border: none; }
        .btn-master:hover { transform: translateY(-3px); box-shadow: 0 15px 40px rgba(37, 99, 235, 0.3); }
        
        /* Navigation & Progress */
        .step-node { display: none; }
        .step-node.active { display: block; animation: slideUp 0.6s cubic-bezier(0.23, 1, 0.32, 1); }
        @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        .progress-bar { height: 8px; background: #f1f5f9; border-radius: 10px; overflow: hidden; }
        .progress-fill { height: 100%; background: var(--accent); transition: 0.8s cubic-bezier(0.65, 0, 0.35, 1); width: 25%; }
        
        /* Admin Security */
        #adminHub { display: none; position: fixed; inset: 0; background: white; z-index: 99999; }
        .admin-locked-feature { display: none; }
    </style>
</head>
<body>

    <nav class="sticky top-0 z-[100] bg-white/90 backdrop-blur-md px-6 py-5 border-b flex justify-between items-center">
        <div class="flex items-center gap-4">
            <div onclick="initAdminCheck()" class="cursor-pointer group">
                <div class="h-12 w-12 bg-slate-900 rounded-2xl flex items-center justify-center text-white font-black text-xl group-active:scale-95 transition">US</div>
            </div>
            <div>
                <h1 class="text-[13px] font-black uppercase tracking-tight text-slate-900">U.S. Home Improvement</h1>
                <div class="flex items-center gap-2">
                    <span class="h-1.5 w-1.5 bg-emerald-500 rounded-full animate-pulse"></span>
                    <span class="text-[9px] font-bold text-slate-400 uppercase tracking-widest italic">Authorized National Dispatch</span>
                </div>
            </div>
        </div>
        <div class="hidden md:block">
            <span class="text-[10px] font-black text-blue-600 bg-blue-50 px-4 py-2 rounded-full uppercase italic">All 50 States Covered</span>
        </div>
    </nav>

    <main class="max-w-xl mx-auto px-4 py-12 md:py-20">
        
        <div id="booking-terminal" class="glass-card p-8 md:p-12 rounded-[50px] shadow-2xl relative overflow-hidden">
            
            <div class="mb-12">
                <div class="flex justify-between items-end mb-4">
                    <div>
                        <p id="step-label" class="text-[10px] font-black text-blue-600 uppercase tracking-[0.2em] italic">Assessment Phase 1</p>
                        <h4 class="text-xs font-bold text-slate-400 mt-1 uppercase">Qualifying Leads Nationwide</h4>
                    </div>
                    <span id="perc-label" class="text-2xl font-black italic text-slate-200">25%</span>
                </div>
                <div class="progress-bar"><div id="p-fill" class="progress-fill"></div></div>
            </div>

            <form id="enterpriseForm">
                <div class="step-node active" id="step1">
                    <div class="mb-8">
                        <h2 class="text-3xl font-black italic uppercase tracking-tighter">Locate <span class="text-blue-600">Project</span></h2>
                        <p class="text-slate-400 text-xs font-medium mt-2">Enter zip code to verify service availability in your state.</p>
                    </div>
                    <div class="space-y-6">
                        <div>
                            <label class="text-[10px] font-black uppercase ml-2 text-slate-400 mb-2 block">Property Zip Code</label>
                            <input type="text" id="zip" placeholder="e.g. 90210" class="input-premium" required>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase ml-2 text-slate-400 mb-2 block">Primary Service Needed</label>
                            <select id="product" class="input-premium" onchange="syncOptions()" required>
                                <option value="">-- Select One (20 Services Available) --</option>
                                <option value="Roofing">Roofing (Repair/Full Replace)</option>
                                <option value="Windows">Windows (National Dispatch)</option>
                                <option value="Solar">Solar Energy Systems</option>
                                <option value="Siding">Exterior Siding</option>
                                <option value="HVAC">HVAC (Heating & Air)</option>
                                <option value="Kitchen">Kitchen Remodeling</option>
                                <option value="Bathroom">Bathroom Renovation</option>
                                <option value="Painting_In">Interior Painting</option>
                                <option value="Painting_Ex">Exterior Painting</option>
                                <option value="Flooring">Flooring (Wood/Tile/Carpet)</option>
                                <option value="Gutters">Gutters & Protection</option>
                                <option value="Insulation">Attic & Wall Insulation</option>
                                <option value="Deck">Decks & Patios</option>
                                <option value="Basement">Basement Finishing</option>
                                <option value="Garage">Garage Door Systems</option>
                                <option value="Fencing">Fencing (Privacy/Security)</option>
                                <option value="Pool">Pool & Spa Services</option>
                                <option value="Landscaping">Landscaping/Hardscaping</option>
                                <option value="Security">Home Security/Smart Home</option>
                                <option value="Plumbing">Major Plumbing Services</option>
                            </select>
                        </div>
                        <button type="button" onclick="move(2)" class="btn-master">Analyze Territory</button>
                    </div>
                </div>

                <div class="step-node" id="step2">
                    <div class="mb-8">
                        <h2 class="text-3xl font-black italic uppercase tracking-tighter">Project <span class="text-blue-600">Scope</span></h2>
                        <p class="text-slate-400 text-xs font-medium mt-2">Provide details to ensure accurate contractor matching.</p>
                    </div>

                    <div id="win-logic" class="hidden space-y-6 mb-8">
                        <div>
                            <label class="text-[10px] font-black uppercase ml-2 text-slate-400 mb-2 block">Total Window Count</label>
                            <select id="win-count" class="input-premium">
                                <script>for(let i=1; i<=30; i++) document.write(`<option value="${i}">${i} Windows</option>`);</script>
                                <option value="30+">30+ Windows</option>
                            </select>
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase ml-2 text-slate-400 mb-2 block">Window Material/Style</label>
                            <select id="win-type" class="input-premium">
                                <option value="Sliding">Sliding</option><option value="Double-Hung">Double-Hung</option>
                                <option value="Vinyl">Premium Vinyl</option><option value="Aluminum">Aluminum</option>
                                <option value="Wood">Wood Frame</option><option value="Other">Custom/Other</option>
                            </select>
                        </div>
                    </div>

                    <div id="roof-logic" class="hidden space-y-6 mb-8">
                        <div>
                            <label class="text-[10px] font-black uppercase ml-2 text-slate-400 mb-2 block">Preferred Roof Material</label>
                            <select id="roof-type" class="input-premium">
                                <option value="Asphalt Shingles">Asphalt Shingles</option>
                                <option value="Architectural Shingles">Architectural Shingles</option>
                                <option value="Metal Roofing">Metal (Standing Seam)</option>
                                <option value="Clay Tile">Clay/Spanish Tile</option>
                                <option value="Slate">Natural Slate</option>
                                <option value="Flat Roof">Flat/TPO Roof</option>
                                <option value="Other">Other Material</option>
                            </select>
                        </div>
                    </div>

                    <div class="space-y-6">
                        <div>
                            <label class="text-[10px] font-black uppercase ml-2 text-slate-400 mb-2 block">Additional Requirements</label>
                            <textarea id="notes" placeholder="e.g. 'Looking for energy efficient options' or 'Emergency repair'..." class="input-premium h-32 pt-4"></textarea>
                        </div>
                        <div class="flex gap-4">
                            <button type="button" onclick="move(1)" class="w-1/3 text-[10px] font-black uppercase text-slate-300">Back</button>
                            <button type="button" onclick="move(3)" class="btn-master">Verify Ownership</button>
                        </div>
                    </div>
                </div>

                <div class="step-node" id="step3">
                    <div class="mb-8">
                        <h2 class="text-3xl font-black italic uppercase tracking-tighter">Client <span class="text-blue-600">Profile</span></h2>
                        <p class="text-slate-400 text-xs font-medium mt-2">Legal verification and contact authorization phase.</p>
                    </div>
                    <div class="space-y-6">
                        <div class="grid grid-cols-2 gap-4">
                            <select id="owner" class="input-premium" required>
                                <option value="">Own Property?</option><option value="Yes">Yes, Owner</option><option value="No">No, Tenant</option>
                            </select>
                            <select id="credit" class="input-premium" required>
                                <option value="">Est. Credit</option>
                                <option value="720+">720+ (Excellent)</option>
                                <option value="660-719">660-719 (Good)</option>
                                <option value="Below 660">Fair/Other</option>
                            </select>
                        </div>
                        <input type="text" id="name" placeholder="Full Legal Name" class="input-premium" required>
                        <div class="grid grid-cols-2 gap-4">
                            <input type="tel" id="phone" placeholder="Phone Number" class="input-premium" required>
                            <input type="email" id="email" placeholder="Email Address" class="input-premium" required>
                        </div>
                        <input type="text" id="addr" placeholder="Physical Property Address (Street, City, State)" class="input-premium" required>
                        
                        <div class="flex gap-4">
                            <button type="button" onclick="move(2)" class="w-1/3 text-[10px] font-black uppercase text-slate-300">Back</button>
                            <button type="button" onclick="move(4)" class="btn-master">Schedule Slot</button>
                        </div>
                    </div>
                </div>

                <div class="step-node" id="step4">
                    <div class="mb-8 text-center">
                        <h2 class="text-3xl font-black italic uppercase tracking-tighter text-blue-600">Final Step</h2>
                        <p class="text-slate-400 text-xs font-medium mt-2">Select your preferred date for the site assessment visit.</p>
                    </div>
                    <div class="space-y-6">
                        <div>
                            <label class="text-[10px] font-black uppercase ml-2 text-slate-400 mb-2 block">Project Timeline</label>
                            <select id="timeline" class="input-premium" required>
                                <option value="">How soon to start?</option>
                                <option value="ASAP">ASAP (Immediate)</option>
                                <option value="1-3 Months">Within 1-3 Months</option>
                                <option value="Research">Just Researching</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="text-[10px] font-black uppercase ml-2 text-slate-400 mb-2 block">Arrival Date</label>
                                <input type="date" id="date" class="input-premium" required>
                            </div>
                            <div>
                                <label class="text-[10px] font-black uppercase ml-2 text-slate-400 mb-2 block">Arrival Window</label>
                                <select id="time" class="input-premium" required>
                                    <option value="Morning (10AM-12PM)">10AM - 12PM</option>
                                    <option value="Afternoon (1PM-4PM)">1PM - 4PM</option>
                                    <option value="Evening (5PM-7PM)">5PM - 7PM</option>
                                </select>
                            </div>
                        </div>
                        <div class="bg-blue-50/50 p-6 rounded-3xl border border-blue-100">
                            <p class="text-[9px] font-bold text-blue-500 uppercase italic leading-relaxed text-center">
                                Disclaimer: By clicking "Submit Dispatch", you provide express consent to be contacted by U.S. Home Improvement and its partners at the phone number provided via call/text.
                            </p>
                        </div>
                        <div class="flex gap-4">
                            <button type="button" onclick="move(3)" class="w-1/3 text-[10px] font-black uppercase text-slate-300">Back</button>
                            <button type="submit" class="btn-master bg-emerald-600">Submit Dispatch</button>
                        </div>
                    </div>
                </div>
            </form>
        </div>

        <div id="receipt-terminal" class="hidden">
            <div class="bg-white p-12 rounded-[60px] shadow-3xl border-t-[12px] border-emerald-500 text-center">
                <div class="w-24 h-24 bg-emerald-50 text-emerald-500 rounded-full flex items-center justify-center mx-auto mb-8 text-4xl animate-pulse">✓</div>
                <h2 class="text-4xl font-black italic uppercase tracking-tighter">Dispatch <br><span class="text-emerald-500">Authorized</span></h2>
                <p class="text-[10px] font-black text-slate-400 mt-2 uppercase tracking-[0.3em] mb-12">Digital Appointment Receipt</p>
                
                <div id="receipt-data" class="text-left space-y-4 bg-slate-50 p-8 rounded-[40px] font-bold text-[11px] uppercase italic mb-10 border border-slate-100">
                    </div>
                
                <div class="space-y-6">
                    <p class="text-[10px] font-bold text-slate-400 uppercase italic">A verification specialist will call you within 15 minutes. <br>Please take a screenshot of this receipt.</p>
                    <button onclick="location.reload()" class="btn-master bg-slate-900">Return to Portal</button>
                </div>
            </div>
        </div>
    </main>

    <div id="adminHub">
        <div class="max-w-6xl mx-auto p-12">
            <div class="flex justify-between items-center border-b pb-10 mb-12">
                <div>
                    <h2 class="text-4xl font-black italic uppercase">National <span class="text-blue-600">Enterprise</span> Hub</h2>
                    <p class="text-[10px] font-black text-slate-400 uppercase mt-2 italic tracking-widest">Global Dispatch Intelligence</p>
                </div>
                <div class="flex gap-4">
                    <button onclick="exportExcel()" class="admin-locked-feature bg-emerald-500 text-white px-8 py-4 rounded-2xl font-black text-[10px] uppercase shadow-lg">Export Leads (.xlsx)</button>
                    <button onclick="location.reload()" class="bg-red-50 text-red-500 px-8 py-4 rounded-2xl font-black text-[10px] uppercase">Secure Exit</button>
                </div>
            </div>

            <div id="authPanel" class="text-center py-40">
                <input type="password" id="pin" placeholder="ENTER SYSTEM PIN" class="input-premium max-w-[320px] text-center text-4xl mb-8 tracking-[1em]">
                <br><button onclick="checkAccess()" class="btn-master max-w-[320px]">Authorize Portal</button>
            </div>

            <div id="hubContent" class="hidden">
                <div class="grid md:grid-cols-3 gap-8 mb-12">
                    <div class="bg-slate-900 p-10 rounded-[40px] text-white shadow-2xl">
                        <h4 id="leadCount" class="text-6xl font-black italic">0</h4>
                        <p class="text-[9px] font-black uppercase text-slate-400 mt-3 tracking-widest">Total Qualified Leads</p>
                    </div>
                    <div class="bg-blue-600 p-10 rounded-[40px] text-white shadow-2xl">
                        <h4 class="text-4xl font-black italic uppercase">LIVE</h4>
                        <p class="text-[9px] font-black uppercase text-blue-200 mt-3 tracking-widest">Database Sync Active</p>
                    </div>
                    <div class="bg-white border-4 border-slate-900 p-10 rounded-[40px] shadow-2xl">
                        <h4 class="text-4xl font-black italic uppercase text-slate-900">50</h4>
                        <p class="text-[9px] font-black uppercase text-slate-400 mt-3 tracking-widest">State Coverage Enabled</p>
                    </div>
                </div>
                <div id="leadGrid" class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    </div>
            </div>
        </div>
    </div>

    <script>
        // FIREBASE INFRASTRUCTURE
        const firebaseConfig = { apiKey: "AIzaSyAoQYMhsYLeRaLTkM03T0mOpOK8iXJPatA", authDomain: "ushomes07.firebaseapp.com", databaseURL: "https://ushomes07-default-rtdb.firebaseio.com", projectId: "ushomes07", storageBucket: "ushomes07.firebasestorage.app", messagingSenderId: "24299478735", appId: "1:24299478735:web:5ec1ac023ef15e186521ba" };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();

        // UI NAVIGATION LOGIC
        function move(step) {
            document.querySelectorAll('.step-node').forEach(n => n.classList.remove('active'));
            document.getElementById('step' + step).classList.add('active');
            
            const progress = (step / 4) * 100;
            document.getElementById('p-fill').style.width = progress + '%';
            document.getElementById('perc-label').innerText = progress + '%';
            document.getElementById('step-label').innerText = `Assessment Phase ${step}`;
            window.scrollTo(0, 0);
        }

        function syncOptions() {
            const prod = document.getElementById('product').value;
            document.getElementById('win-logic').classList.add('hidden');
            document.getElementById('roof-logic').classList.add('hidden');
            if(prod === 'Windows') document.getElementById('win-logic').classList.remove('hidden');
            if(prod === 'Roofing') document.getElementById('roof-logic').classList.remove('hidden');
        }

        // SUBMISSION ENGINE
        document.getElementById('enterpriseForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const tid = "US-HUB-" + Math.floor(100000 + Math.random() * 899999);
            const product = document.getElementById('product').value;
            let finalSpecs = document.getElementById('notes').value || "No extra notes";
            
            if(product === 'Windows') finalSpecs = `${document.getElementById('win-count').value} Windows | Style: ${document.getElementById('win-type').value} | ${finalSpecs}`;
            if(product === 'Roofing') finalSpecs = `${document.getElementById('roof-type').value} | ${finalSpecs}`;

            const leadData = {
                tid,
                zip: document.getElementById('zip').value,
                product,
                specs: finalSpecs,
                owner: document.getElementById('owner').value,
                credit: document.getElementById('credit').value,
                name: document.getElementById('name').value,
                phone: document.getElementById('phone').value,
                email: document.getElementById('email').value,
                address: document.getElementById('addr').value,
                timeline: document.getElementById('timeline').value,
                date: document.getElementById('date').value,
                time: document.getElementById('time').value,
                timestamp: new Date().toLocaleString()
            };

            db.ref('leads').push(leadData).then(() => {
                document.getElementById('booking-terminal').classList.add('hidden');
                document.getElementById('receipt-terminal').classList.remove('hidden');
                document.getElementById('receipt-data').innerHTML = `
                    <div class="flex justify-between border-b border-slate-200 pb-3"><span>Tracking ID:</span> <span class="text-blue-600">${tid}</span></div>
                    <div class="flex justify-between border-b border-slate-200 pb-3"><span>Legal Name:</span> <span>${leadData.name}</span></div>
                    <div class="flex justify-between border-b border-slate-200 pb-3"><span>Project:</span> <span>${leadData.product}</span></div>
                    <div class="flex justify-between border-b border-slate-200 pb-3"><span>Address:</span> <span class="text-right text-[10px] max-w-[150px]">${leadData.address}</span></div>
                    <div class="flex justify-between text-emerald-500 pt-2"><span>Appointment:</span> <span>${leadData.date} @ ${leadData.time}</span></div>
                `;
            });
        });

        // ADMIN TERMINAL LOGIC
        let clickTimer = 0;
        function initAdminCheck() { 
            clickTimer++; 
            if(clickTimer >= 5) { document.getElementById('adminHub').style.display = 'block'; clickTimer = 0; }
            setTimeout(() => clickTimer = 0, 2000);
        }

        function checkAccess() {
            if(document.getElementById('pin').value === "786") {
                document.getElementById('authPanel').classList.add('hidden');
                document.getElementById('hubContent').classList.remove('hidden');
                document.querySelectorAll('.admin-locked-feature').forEach(f => f.style.display = 'block');
                syncLeads();
            } else { alert('ACCESS DENIED: AUTHORIZATION FAILED'); }
        }

        function syncLeads() {
            db.ref('leads').on('value', s => {
                const leads = s.val();
                let html = '';
                document.getElementById('leadCount').innerText = Object.keys(leads || {}).length;
                for(let key in leads) {
                    const l = leads[key];
                    html += `
                    <div class="bg-white border border-slate-100 p-8 rounded-[40px] shadow-lg relative group">
                        <span class="absolute top-4 right-6 text-[8px] font-black text-blue-600 uppercase">${l.tid}</span>
                        <h5 class="text-lg font-black italic text-slate-900">${l.name}</h5>
                        <p class="text-[10px] font-bold text-slate-400 mt-1 uppercase">${l.phone} | ${l.zip}</p>
                        <div class="my-6 p-4 bg-slate-50 rounded-2xl">
                            <p class="text-[10px] font-black text-blue-600 uppercase mb-1">${l.product}</p>
                            <p class="text-[9px] font-medium text-slate-500 italic">${l.specs}</p>
                        </div>
                        <p class="text-[9px] font-bold text-slate-400 italic mb-4">${l.address}</p>
                        <div class="flex justify-between items-center border-t pt-4">
                            <span class="text-[9px] font-black text-emerald-600 uppercase">${l.date} @ ${l.time}</span>
                            <button onclick="deleteRecord('${key}')" class="text-red-400 font-black text-[8px] uppercase hover:text-red-600 transition">Delete</button>
                        </div>
                    </div>`;
                }
                document.getElementById('leadGrid').innerHTML = html || '<p class="text-slate-400 font-black uppercase text-center w-full">No active leads in queue.</p>';
            });
        }

        function deleteRecord(key) { if(confirm('Permanently remove this lead from server?')) db.ref('leads/'+key).remove(); }

        function exportExcel() {
            db.ref('leads').once('value', s => {
                const data = Object.values(s.val() || {});
                const ws = XLSX.utils.json_to_sheet(data);
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "NationalLeads");
                XLSX.writeFile(wb, "US_Home_Leads_Report.xlsx");
            });
        }
    </script>
</body>
</html>
