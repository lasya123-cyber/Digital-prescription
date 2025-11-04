<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Digital Prescription Manager 💊 - Demo</title>

<style>
  :root{
    --primary:#0d6efd;
    --accent:#0b5ed7;
    --bg:#f4f7fb;
    --card:#ffffff;
    --muted:#6c757d;
    --danger:#dc3545;
    --success:#198754;
    --glass: rgba(255,255,255,0.9);
    font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
  }
  body,html{height:100%;margin:0;background:linear-gradient(180deg,#eef5ff 0%, #f7fbff 100%);}
  /* SPLASH */
  .splash {
    position:fixed;inset:0;display:flex;align-items:center;justify-content:center;flex-direction:column;
    background:linear-gradient(180deg,#eaf2ff, #f8fbff);z-index:1000;
  }
  .app-icon{
    width:110px;height:110px;border-radius:26px;background:linear-gradient(135deg,var(--primary),var(--accent));
    display:flex;align-items:center;justify-content:center;color:#fff;font-size:48px;box-shadow:0 12px 30px rgba(11,92,203,.18);
    animation:bounceIn 1.1s cubic-bezier(.36,.07,.19,.97) both;
  }
  @keyframes bounceIn{
    0%{transform:translateY(-120px) scale(.6);opacity:0}
    60%{transform:translateY(12px) scale(1.06);opacity:1}
    80%{transform:translateY(-6px) scale(.98)}
    100%{transform:translateY(0) scale(1)}
  }
  .app-name{margin-top:12px;font-weight:700;color:var(--primary);font-size:18px}
  /* LAYOUT */
  .app {
    max-width:980px;margin:32px auto;padding:20px;background:var(--card);border-radius:14px;box-shadow:0 6px 30px rgba(22,35,70,.06);
    min-height:560px;position:relative;overflow:hidden;
  }
  header{display:flex;align-items:center;gap:12px}
  .logo{display:flex;align-items:center;gap:10px}
  .logo .icon{width:48px;height:48px;border-radius:10px;background:linear-gradient(135deg,var(--primary),var(--accent));display:flex;align-items:center;justify-content:center;color:#fff;font-size:22px}
  h1{margin:0;font-size:20px;color:#07203b}
  .sub{color:var(--muted);font-size:13px}
  /* hamburger */
  .hamburger{margin-left:auto;cursor:pointer;padding:8px;border-radius:8px}
  .hamburger:hover{background:rgba(0,0,0,0.03)}
  /* main */
  .main{display:flex;gap:20px;margin-top:20px}
  .left-col{width:320px}
  .card{background:var(--glass);padding:18px;border-radius:12px;margin-bottom:16px;box-shadow:inset 0 1px 0 rgba(255,255,255,0.6)}
  .profile-photo{width:68px;height:68px;border-radius:12px;background:#fff;display:flex;align-items:center;justify-content:center;font-size:28px;color:var(--primary);font-weight:700}
  .info-row{display:flex;gap:12px;align-items:center}
  .small{font-size:13px;color:var(--muted)}
  .btn{display:inline-block;padding:8px 12px;border-radius:10px;background:var(--primary);color:#fff;text-decoration:none;font-size:13px}
  .btn.ghost{background:transparent;color:var(--primary);border:1px solid rgba(13,110,253,.12)}
  /* prescriptions list */
  .right-col{flex:1}
  .pres-list{display:flex;flex-direction:column;gap:10px}
  .pres-item{background:linear-gradient(180deg,#fff,#fbfdff);padding:12px;border-radius:10px;border:1px solid rgba(11,92,203,.06);display:flex;justify-content:space-between;align-items:center}
  .pres-left{display:flex;gap:12px;align-items:center;min-width:0}
  .pill{width:48px;height:48px;border-radius:10px;background:linear-gradient(135deg,#ffdcb1,#ffb4a2);display:flex;align-items:center;justify-content:center;font-weight:700;color:#6b2b00}
  .pres-meta{min-width:0}
  .pres-meta b{display:block;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
  .pres-meta .muted{font-size:12px;color:var(--muted)}
  .pres-right{display:flex;gap:8px;align-items:center}
  .tag{font-size:12px;padding:6px 8px;border-radius:8px;background:#f1f7ff;color:var(--primary)}
  .danger{background:#fff0f0;color:var(--danger);border:1px solid rgba(220,53,69,.06)}
  .success{background:#ecfbef;color:var(--success);border:1px solid rgba(25,135,84,.06)}
  /* modal */
  .modal-backdrop{position:fixed;inset:0;background:rgba(2,10,23,.45);display:none;align-items:center;justify-content:center;z-index:999}
  .modal{background:#fff;padding:18px;border-radius:12px;min-width:320px;max-width:720px;box-shadow:0 18px 40px rgba(2,10,23,.3)}
  .modal h3{margin-top:0}
  .form-row{display:flex;gap:8px;margin-bottom:10px}
  .form-row input,.form-row textarea, select{flex:1;padding:8px;border-radius:8px;border:1px solid #e6eefc;background:#fbfdff}
  .list-inline{display:flex;gap:8px;flex-wrap:wrap}
  .menu-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
  .empty{color:var(--muted);text-align:center;padding:30px}
  /* responsive */
  @media(max-width:860px){
    .app{margin:16px;border-radius:0}
    .left-col{display:none}
  }
</style>
</head>
<body>

<!-- SPLASH SCREEN -->
<div id="splash" class="splash">
  <div class="app-icon" title="Digital Prescription Manager">💊</div>
  <div class="app-name">Digital Prescription Manager</div>
</div>

<!-- APP -->
<div id="root" style="display:none;">
  <div class="app" role="application">
    <header>
      <div class="logo">
        <div class="icon">💊</div>
        <div>
          <h1>Digital Prescription Manager</h1>
          <div class="sub">Smart prescriptions • reminders • expiry tracker</div>
        </div>
      </div>

      <div id="user-area" style="margin-left:auto;">
        <!-- login area -->
      </div>

      <div class="hamburger" id="hambtn" title="Open menu">
        <svg width="26" height="26" viewBox="0 0 24 24"><path fill="#05243a" d="M3 6h18v2H3zM3 11h18v2H3zM3 16h18v2H3z"/></svg>
      </div>
    </header>

    <div class="main">
      <div class="left-col">
        <div class="card" id="profile-card">
          <!-- profile -->
        </div>

        <div class="card">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div><b>Quick Actions</b><div class="small">Use these shortcuts</div></div>
            <div><a href="#" class="btn" id="addPrescriptionBtn">+ New</a></div>
          </div>

          <div style="margin-top:12px" id="quick-actions">
            <div class="list-inline">
              <a class="btn ghost" id="btnSchedule">Tablets Schedule</a>
              <a class="btn ghost" id="btnExpiry">Expiry Alerts</a>
              <a class="btn ghost" id="btnAlternatives">Alternatives</a>
            </div>
          </div>
        </div>

      </div>

      <div class="right-col">
        <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">
          <div><b>Prescriptions</b><div class="small">Recent prescriptions (one-line view)</div></div>
          <div><a id="logoutBtn" class="btn ghost">Logout</a></div>
        </div>

        <div id="presList" class="pres-list"></div>
        <div id="emptyMsg" class="empty" style="display:none">No prescriptions yet. Add one using "+ New".</div>
      </div>
    </div>
  </div>
</div>

<!-- MODALS -->
<div id="backdrop" class="modal-backdrop">
  <div class="modal" id="modalContent"></div>
</div>

<script>
/* ---------- Demo data & helpers ---------- */

const demoUsers = {
  doctor: { role: 'doctor', username: 'doctor', password: '1234', name: 'Dr. Kavya', phone: '9876543210', email: 'dr.kavya@example.com' },
  patient: { role: 'patient', username: 'patient', password: '1234', name: 'Asha R', phone: '9988776655', email: 'asha.r@example.com', bill: 450.00 }
};

// localStorage keys
const LS_USER = 'dpm_demo_user';
const LS_PRES = 'dpm_demo_prescriptions';

/* ---------- Splash and init ---------- */
function hideSplash() {
  document.getElementById('splash').style.display='none';
  document.getElementById('root').style.display='block';
  renderUserArea();
}
setTimeout(hideSplash, 1200); // show splash for 1.2s

/* ---------- Utility functions ---------- */
function uid(){ return Math.random().toString(36).slice(2,9); }
function savePresList(list){ localStorage.setItem(LS_PRES, JSON.stringify(list)); }
function loadPresList(){ return JSON.parse(localStorage.getItem(LS_PRES) || '[]'); }
function saveUser(u){ localStorage.setItem(LS_USER, JSON.stringify(u)); }
function loadUser(){ return JSON.parse(localStorage.getItem(LS_USER) || 'null'); }
function clearUser(){ localStorage.removeItem(LS_USER); }

/* ---------- AUTH / Login UI ---------- */
function renderUserArea(){
  const area = document.getElementById('user-area');
  const user = loadUser();
  if(user){
    area.innerHTML = `<div style="display:flex;align-items:center;gap:8px">
      <div style="font-weight:700;color:#07203b">${user.name}</div>
      <div class="small" style="color:var(--muted);">${user.role.toUpperCase()}</div>
    </div>`;
    renderProfileCard(user);
    renderPrescriptions();
  } else {
    area.innerHTML = `<a class="btn" id="openLogin">Login</a>`;
    document.getElementById('openLogin').onclick = openLoginModal;
    document.getElementById('profile-card').innerHTML = `<div style="text-align:center"><b>Welcome</b><div class="small">Please login to continue</div></div>`;
    document.getElementById('presList').innerHTML = '';
    document.getElementById('emptyMsg').style.display = 'block';
  }
}

/* ---------- Profile Card ---------- */
function renderProfileCard(user){
  const card = document.getElementById('profile-card');
  card.innerHTML = `
    <div style="display:flex;gap:12px;align-items:center">
      <div class="profile-photo">${(user.name||'U').split(' ').map(n=>n[0]).slice(0,2).join('')}</div>
      <div>
        <div style="font-weight:700">${user.name}</div>
        <div class="small">${user.email}</div>
        <div class="small">Phone: ${user.phone}</div>
      </div>
    </div>
    <div style="margin-top:12px" class="small">
      Role: <b>${user.role}</b><br/>
      ${user.role==='patient'? `Bill Amount: <b>₹${(user.bill||0).toFixed(2)}</b>` : 'Doctor Dashboard'}
    </div>
  `;
}

/* ---------- LOGIN MODAL ---------- */
function openLoginModal(){
  showModal(`
    <h3>Login</h3>
    <div class="form-row">
      <input id="l_user" placeholder="username (doctor / patient)" />
      <input id="l_pass" type="password" placeholder="password (1234)" />
    </div>
    <div style="display:flex;gap:8px;justify-content:flex-end">
      <button class="btn ghost" onclick="closeModal()">Cancel</button>
      <button class="btn" id="doLoginBtn">Login</button>
    </div>
    <div class="small" style="margin-top:8px;color:var(--muted)">Demo creds: doctor/1234  patient/1234</div>
  `);
  document.getElementById('doLoginBtn').onclick = doLogin;
}

function doLogin(){
  const u = document.getElementById('l_user').value.trim();
  const p = document.getElementById('l_pass').value.trim();
  // demo check
  if(u==='doctor' && p===demoUsers.doctor.password){
    saveUser(demoUsers.doctor);
    closeModal();
    renderUserArea();
    return;
  }
  if(u==='patient' && p===demoUsers.patient.password){
    saveUser(demoUsers.patient);
    closeModal();
    renderUserArea();
    return;
  }
  alert('Invalid credentials (demo). Try doctor/1234 or patient/1234');
}

/* ---------- LOGOUT ---------- */
document.addEventListener('click', e=>{
  if(e.target && e.target.id==='logoutBtn'){ clearUser(); renderUserArea(); }
});

/* ---------- MODAL HELPERS ---------- */
function showModal(html){
  document.getElementById('modalContent').innerHTML = html;
  const b = document.getElementById('backdrop');
  b.style.display='flex';
}
function closeModal(){ document.getElementById('backdrop').style.display='none'; }

/* ---------- PRESCRIPTIONS RENDER ---------- */
function renderPrescriptions(){
  const user = loadUser();
  if(!user){ document.getElementById('presList').innerHTML=''; document.getElementById('emptyMsg').style.display='block'; return; }
  const all = loadPresList();
  // For doctor show all patient prescriptions; for patient show only their own (owner in demo by patientId)
  const items = user.role==='doctor' ? all : all.filter(i=>i.patientUsername===user.username);
  const list = document.getElementById('presList');
  list.innerHTML = '';
  if(items.length===0){ document.getElementById('emptyMsg').style.display='block'; return; } else document.getElementById('emptyMsg').style.display='none';

  items.forEach(p=>{
    const container = document.createElement('div');
    container.className='pres-item';
    // make one-line: PatientName — Medicine (dosage) • Exp: date • Alt: generic1,generic2 • Schedule
    const left = document.createElement('div'); left.className='pres-left';
    left.innerHTML = `
      <div class="pill">P</div>
      <div class="pres-meta">
        <b>${p.patientName} — ${p.medicineName}</b>
        <div class="muted">${p.dosage} • Exp: ${p.expiryDate || '—'} • Alt: ${p.alternatives.join(', ') || '—'}</div>
      </div>
    `;
    const right = document.createElement('div'); right.className='pres-right';
    // if expiring soon, show danger
    const expBadge = document.createElement('div');
    const today = new Date().toISOString().slice(0,10);
    let expClass = 'tag';
    if(p.expiryDate){
      if(p.expiryDate <= today) expClass = 'tag danger';
      else {
        const d1 = new Date(p.expiryDate), d0 = new Date();
        const diff = (d1 - d0)/(1000*60*60*24);
        if(diff <= 7) expClass = 'tag danger';
      }
    }
    const viewBtn = document.createElement('a'); viewBtn.className='btn ghost'; viewBtn.textContent='View';
    viewBtn.onclick = ()=>openViewPrescription(p.id);
    const editBtn = document.createElement('a'); editBtn.className='btn'; editBtn.textContent='Edit';
    editBtn.onclick = ()=>openEditPrescription(p.id);
    right.appendChild(viewBtn);
    // only doctor sees edit
    if(user.role==='doctor'){ right.appendChild(editBtn); }
    container.appendChild(left);
    container.appendChild(right);
    list.appendChild(container);
  });
}

/* ---------- OPEN VIEW ---------- */
function openViewPrescription(id){
  const list = loadPresList();
  const p = list.find(x=>x.id===id);
  if(!p) return alert('Not found');
  showModal(`
    <h3>Prescription — ${p.medicineName}</h3>
    <div class="small">Patient: <b>${p.patientName}</b> • Prescribed by: <b>${p.doctorName}</b></div>
    <hr/>
    <div><b>Dosage:</b> ${p.dosage}</div>
    <div><b>Schedule:</b> ${p.schedule}</div>
    <div><b>Expiry:</b> ${p.expiryDate || '—'}</div>
    <div><b>Alternatives:</b> ${p.alternatives.join(', ') || '—'}</div>
    <div style="margin-top:10px"><b>Description:</b><div style="padding:10px;background:#fbfdff;border-radius:8px;margin-top:6px">${p.description || '—'}</div></div>
    <div style="display:flex;gap:8px;justify-content:flex-end;margin-top:12px">
      <button class="btn ghost" onclick="closeModal()">Close</button>
    </div>
  `);
}

/* ---------- EDIT OR ADD PRESCRIPTION ---------- */
document.getElementById('addPrescriptionBtn').addEventListener('click', ()=> openAddEditModal());

function openAddEditModal(id){
  const user = loadUser();
  if(!user){ openLoginModal(); return; }
  const isEdit = Boolean(id);
  const list = loadPresList();
  const pObj = isEdit ? list.find(x=>x.id===id) : {
    id: uid(),
    doctorUsername: user.role==='doctor' ? user.username : 'doctor',
    doctorName: user.role==='doctor' ? user.name : 'Dr. Demo',
    patientUsername: user.role==='patient' ? user.username : 'patient',
    patientName: user.role==='patient' ? user.name : 'Patient Demo',
    medicineName:'Amoxicillin 500mg',
    dosage:'1 tablet twice daily',
    schedule:'08:00,20:00',
    expiryDate:'',
    alternatives:['Amoxicillin (generic)'],
    description:'',
  };

  showModal(`
    <h3>${isEdit? 'Edit' : 'Add New'} Prescription</h3>
    <div class="form-row"><input id="f_med" value="${escapeHtml(pObj.medicineName)}" placeholder="Medicine name"/></div>
    <div class="form-row"><input id="f_dos" value="${escapeHtml(pObj.dosage)}" placeholder="Dosage"/></div>
    <div class="form-row"><input id="f_schedule" value="${escapeHtml(pObj.schedule)}" placeholder="Schedule (comma separated times)"/></div>
    <div class="form-row"><input id="f_exp" type="date" value="${pObj.expiryDate || ''}" /></div>
    <div class="form-row"><input id="f_alt" value="${escapeHtml(pObj.alternatives.join(', '))}" placeholder="Alternatives (comma)"/></div>
    <div class="form-row"><textarea id="f_desc" placeholder="Description">${escapeHtml(pObj.description)}</textarea></div>
    <div style="display:flex;gap:8px;justify-content:flex-end">
      <button class="btn ghost" onclick="closeModal()">Cancel</button>
      <button class="btn" id="savePresBtn">${isEdit? 'Save' : 'Add'}</button>
    </div>
  `);

  document.getElementById('savePresBtn').onclick = ()=>{
    const med = document.getElementById('f_med').value.trim();
    if(!med) return alert('Enter medicine name');
    const newObj = {
      id: pObj.id,
      doctorUsername: pObj.doctorUsername,
      doctorName: pObj.doctorName,
      patientUsername: document.getElementById('f_med') && (user.role==='patient' ? user.username : document.getElementById('f_med').value) ? pObj.patientUsername : pObj.patientUsername,
      patientName: pObj.patientName,
      medicineName: med,
      dosage: document.getElementById('f_dos').value.trim(),
      schedule: document.getElementById('f_schedule').value.trim(),
      expiryDate: document.getElementById('f_exp').value || '',
      alternatives: document.getElementById('f_alt').value.split(',').map(s=>s.trim()).filter(Boolean),
      description: document.getElementById('f_desc').value.trim()
    };
    // save
    let arr = loadPresList();
    const idx = arr.findIndex(x=>x.id===newObj.id);
    if(idx>=0) arr[idx]=newObj; else arr.unshift(newObj);
    savePresList(arr);
    closeModal();
    renderPrescriptions();
  };
}

/* open edit for doctors */
function openEditPrescription(id){
  openAddEditModal(id);
}

/* ---------- MENU (hamburger) ---------- */
document.getElementById('hambtn').addEventListener('click', ()=>{
  const user = loadUser();
  if(!user){ openLoginModal(); return; }
  // show menu modal
  showModal(`
    <h3>Menu</h3>
    <div class="menu-grid" style="margin-top:8px">
      <a class="btn ghost" onclick="openModalAction('profile')">Profile</a>
      <a class="btn ghost" onclick="openModalAction('prescriptions')">View Prescriptions</a>
      <a class="btn ghost" onclick="openModalAction('add')">Add Prescription</a>
      <a class="btn ghost" onclick="openModalAction('schedule')">Tablets Schedule</a>
      <a class="btn ghost" onclick="openModalAction('expiry')">Expiry Alerts</a>
      <a class="btn ghost" onclick="openModalAction('alternatives')">Alternatives</a>
      <a class="btn ghost" onclick="openModalAction('bill')">Bill</a>
      <a class="btn ghost" onclick="closeModal()">Close</a>
    </div>
  `);
});

function openModalAction(name){
  closeModal();
  const user = loadUser();
  if(!user) return openLoginModal();
  if(name==='profile'){
    showModal(`<h3>Profile</h3>
      <div><b>${user.name}</b></div>
      <div class="small">${user.email}</div>
      <div class="small">Phone: ${user.phone}</div>
      <div style="margin-top:12px;display:flex;gap:8px;justify-content:flex-end">
        <button class="btn ghost" onclick="closeModal()">Close</button>
      </div>
    `);
  } else if(name==='prescriptions'){
    closeModal();
    renderPrescriptions();
  } else if(name==='add'){
    openAddEditModal();
  } else if(name==='schedule'){
    // show schedule for all prescriptions belonging to user
    const arr = loadPresList().filter(i=> i.patientUsername===user.username || user.role==='doctor');
    let inner = `<h3>Tablets Schedule</h3><div class="small">Times shown per prescription</div><div style="margin-top:10px">`;
    if(arr.length===0) inner += `<div class="empty">No schedules</div>`; else {
      arr.forEach(p=> inner += `<div style="padding:8px;border-radius:8px;margin-bottom:8px;background:#fbfdff"><b>${p.medicineName}</b><div class="small">${p.schedule || '—'}</div></div>`);
    }
    inner += `<div style="display:flex;justify-content:flex-end"><button class="btn ghost" onclick="closeModal()">Close</button></div></div>`;
    showModal(inner);
  } else if(name==='expiry'){
    const arr = loadPresList().filter(i=> i.patientUsername===user.username || user.role==='doctor');
    const today = new Date().toISOString().slice(0,10);
    const soon = arr.filter(p=>p.expiryDate && p.expiryDate <= today || (p.expiryDate && (new Date(p.expiryDate) - new Date())/(1000*60*60*24) <= 7 ));
    let inner = `<h3>Expiry Alerts</h3>`;
    if(soon.length===0) inner += `<div class="empty">No expiring medicines in next 7 days.</div>`; else {
      soon.forEach(p=> inner += `<div style="padding:8px;border-radius:8px;margin-bottom:8px;background:#fff7f7"><b>${p.medicineName}</b> for <b>${p.patientName}</b> expires on ${p.expiryDate}</div>`);
    }
    inner += `<div style="display:flex;justify-content:flex-end"><button class="btn ghost" onclick="closeModal()">Close</button></div>`;
    showModal(inner);
  } else if(name==='alternatives'){
    const arr = loadPresList().filter(i=> i.patientUsername===user.username || user.role==='doctor');
    let inner = `<h3>Alternatives</h3>`;
    if(arr.length===0) inner += `<div class="empty">No prescriptions</div>`; else {
      arr.forEach(p=> inner += `<div style="padding:8px;border-radius:8px;margin-bottom:8px;background:#fbfdff"><b>${p.medicineName}</b> — ${p.alternatives.join(', ') || '—'}</div>`);
    }
    inner += `<div style="display:flex;justify-content:flex-end"><button class="btn ghost" onclick="closeModal()">Close</button></div>`;
    showModal(inner);
  } else if(name==='bill'){
    if(user.role!=='patient'){ showModal(`<h3>Bill</h3><div class="empty">Bill view is only for patients.</div><div style="display:flex;justify-content:flex-end"><button class="btn ghost" onclick="closeModal()">Close</button></div>`); return; }
    showModal(`<h3>Bill</h3><div style="padding:10px;background:#fbfdff;border-radius:8px">Patient: <b>${user.name}</b><div class="small">Amount Due: <b>₹${(user.bill||0).toFixed(2)}</b></div></div><div style="display:flex;justify-content:flex-end;margin-top:12px"><button class="btn ghost" onclick="closeModal()">Close</button></div>`);
  }
}

/* ---------- Demo initialize sample data if none ---------- */
(function seedDemo(){
  if(!localStorage.getItem(LS_PRES)){
    const sample = [
      { id: uid(), doctorUsername:'doctor', doctorName:'Dr. Kavya', patientUsername:'patient', patientName:'Asha R', medicineName:'Azithromycin 500mg', dosage:'500mg once daily', schedule:'09:00', expiryDate:'2026-05-01', alternatives:['Azithro(generic)'], description:'Use after food'},
      { id: uid(), doctorUsername:'doctor', doctorName:'Dr. Kavya', patientUsername:'patient', patientName:'Asha R', medicineName:'Paracetamol 500mg', dosage:'500mg every 8 hours', schedule:'08:00,16:00,00:00', expiryDate:'2026-12-01', alternatives:['Paracetamol (generic)'], description:'For fever and pain'},
    ];
    savePresList(sample);
  }
})();

/* ---------- Small helpers ---------- */
function escapeHtml(s){ return (s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

/* ---------- initial render ---------- */
document.addEventListener('DOMContentLoaded', ()=>{
  // wire logout (already delegated)
  // open login if no user & button exists
  renderUserArea();
  // wire quick action buttons
  document.getElementById('btnSchedule').addEventListener('click', ()=> openModalAction('schedule'));
  document.getElementById('btnExpiry').addEventListener('click', ()=> openModalAction('expiry'));
  document.getElementById('btnAlternatives').addEventListener('click', ()=> openModalAction('alternatives'));
});

</script>

</body>
</html>
