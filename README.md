# Alif25

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>ALIF – Campus Literary Arts Fest</title>
<!-- Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<!-- QR Code Generator -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<!-- QR Code Scanner -->
<script src="https://unpkg.com/html5-qrcode" type="text/javascript"></script>

<style>
    /* --- Design System: Median UI Aesthetic --- */
    :root {
        --bg-body: #ffffff;
        --bg-surface: #ffffff;
        --bg-sidebar: #f8f9fa;
        --bg-hover: #f1f5f9;
        --border-color: #e2e8f0;
        
        --primary: #4f46e5; /* Indigo */
        --primary-hover: #4338ca;
        --primary-soft: #eef2ff;
        
        --text-main: #0f172a;
        --text-secondary: #64748b;
        --text-muted: #94a3b8;
        
        --accent-gold: #f59e0b;
        --danger: #ef4444;
        --success: #10b981;
        
        --radius-sm: 8px;
        --radius-md: 12px;
        --radius-lg: 16px;
        
        --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
        --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        
        --font-main: 'Plus Jakarta Sans', sans-serif;
    }

    * { box-sizing: border-box; outline: none; -webkit-tap-highlight-color: transparent; }
    
    body {
        margin: 0; padding: 0;
        background-color: var(--bg-body);
        color: var(--text-main);
        font-family: var(--font-main);
        font-size: 14px;
        height: 100vh;
        display: flex;
        overflow: hidden;
    }

    /* --- Typography --- */
    h1, h2, h3, h4 { margin: 0; font-weight: 700; letter-spacing: -0.025em; color: var(--text-main); }
    h2 { font-size: 20px; margin-bottom: 1.5rem; }
    h3 { font-size: 16px; margin-bottom: 1rem; }
    p { color: var(--text-secondary); line-height: 1.6; margin-bottom: 1rem; }

    /* --- Layout --- */
    .app-wrapper { display: flex; width: 100%; height: 100%; }
    
    .sidebar {
        width: 260px; background: var(--bg-sidebar); border-right: 1px solid var(--border-color);
        display: flex; flex-direction: column; padding: 20px 15px; flex-shrink: 0;
    }
    
    .brand-area {
        display: flex; align-items: center; gap: 12px; padding: 0 10px 25px 10px;
        margin-bottom: 10px; border-bottom: 1px solid var(--border-color);
    }
    
    .logo-circle {
        width: 36px; height: 36px; background: var(--primary); color: #fff;
        border-radius: 10px; display: grid; place-items: center;
        font-weight: 700; font-size: 18px; object-fit: cover;
    }

    .nav-links { display: flex; flex-direction: column; gap: 4px; overflow-y: auto; flex: 1; }
    
    .nav-item {
        display: flex; align-items: center; gap: 12px; padding: 10px 12px;
        border-radius: var(--radius-sm); color: var(--text-secondary);
        text-decoration: none; font-weight: 500; cursor: pointer; transition: all 0.2s ease;
    }
    .nav-item:hover { background: var(--bg-hover); color: var(--text-main); }
    .nav-item.active { background: #fff; color: var(--primary); box-shadow: var(--shadow-sm); font-weight: 600; }

    .main-content { flex: 1; display: flex; flex-direction: column; overflow: hidden; background: var(--bg-body); }

    .top-bar {
        height: 64px; border-bottom: 1px solid var(--border-color);
        display: flex; align-items: center; justify-content: space-between;
        padding: 0 30px; background: rgba(255,255,255,0.9); backdrop-filter: blur(10px); z-index: 10;
    }

    .content-scroll { flex: 1; overflow-y: auto; padding: 30px; max-width: 1400px; margin: 0 auto; width: 100%; }

    /* --- UI Components --- */
    .card {
        background: #fff; border: 1px solid var(--border-color); border-radius: var(--radius-md);
        padding: 24px; margin-bottom: 24px; box-shadow: var(--shadow-sm);
    }

    .grid { display: grid; gap: 24px; }
    .cols-2 { grid-template-columns: repeat(2, 1fr); }
    .cols-3 { grid-template-columns: repeat(3, 1fr); }
    .row { display: flex; align-items: center; gap: 12px; flex-wrap: wrap; }
    
    .btn {
        display: inline-flex; align-items: center; justify-content: center; gap: 8px;
        padding: 9px 16px; border-radius: var(--radius-sm);
        font-weight: 600; font-size: 13px; cursor: pointer; transition: all 0.2s;
        border: 1px solid var(--border-color); background: #fff; color: var(--text-secondary);
    }
    .btn:hover { background: var(--bg-hover); color: var(--text-main); border-color: var(--text-secondary); }
    .btn.primary { background: var(--primary); color: #fff; border-color: var(--primary); }
    .btn.primary:hover { background: var(--primary-hover); border-color: var(--primary-hover); box-shadow: 0 2px 4px rgba(79, 70, 229, 0.3); }
    .btn.danger { background: #fee2e2; color: var(--danger); border-color: #fecaca; }
    .btn.danger:hover { background: var(--danger); color: #fff; }
    .btn.sm { padding: 6px 12px; font-size: 12px; }

    .input, select {
        width: 100%; padding: 10px 12px; border-radius: var(--radius-sm);
        border: 1px solid var(--border-color); background: #fff;
        font-family: var(--font-main); font-size: 14px; color: var(--text-main);
        transition: border-color 0.2s;
    }
    .input:focus, select:focus { border-color: var(--primary); box-shadow: 0 0 0 3px var(--primary-soft); }

    .tag {
        padding: 4px 10px; border-radius: 20px; font-size: 11px; font-weight: 700;
        text-transform: uppercase; letter-spacing: 0.5px; display: inline-block;
    }
    .tag.blue { background: var(--primary-soft); color: #4f46e5; }
    .tag.green { background: #d1fae5; color: var(--success); }
    .tag.gold { background: #fef3c7; color: #d97706; }
    .tag.gray { background: #f1f5f9; color: var(--text-secondary); }

    table { width: 100%; border-collapse: separate; border-spacing: 0; }
    th {
        text-align: left; padding: 12px 16px; border-bottom: 1px solid var(--border-color);
        color: var(--text-secondary); font-size: 12px; font-weight: 600; text-transform: uppercase; background: #fafafa;
    }
    td { padding: 14px 16px; border-bottom: 1px solid var(--border-color); color: var(--text-main); font-size: 14px; }
    tr:last-child td { border-bottom: none; }
    tbody tr:hover { background: #f8fafc; }

    /* Modal */
    .modal-overlay {
        position: fixed; top: 0; left: 0; width: 100%; height: 100%;
        background: rgba(0,0,0,0.4); backdrop-filter: blur(4px); z-index: 100;
        display: none; align-items: center; justify-content: center;
    }
    .modal-box {
        background: #fff; width: 600px; max-width: 90%; max-height: 90vh; overflow-y: auto;
        border-radius: var(--radius-lg); padding: 30px; box-shadow: var(--shadow-md);
        animation: slideUp 0.2s ease-out;
    }
    @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

    /* Login */
    .login-container { display: flex; align-items: center; justify-content: center; height: 100vh; background: #fff; }
    .login-box { width: 380px; text-align: center; border: none; box-shadow: none; }
    
    /* Chest Editor Helpers */
    .range-wrap { display: flex; align-items: center; gap: 10px; font-size: 12px; margin-bottom: 5px; }
    .range-wrap input[type=range] { flex: 1; }
    .color-inp { width: 30px; height: 30px; padding: 0; border: none; border-radius: 50%; cursor: pointer; }

    /* Scanner */
    #reader { width: 100%; border-radius: var(--radius-md); overflow: hidden; }

    /* Print */
    @media print {
        .sidebar, .top-bar, .btn, .input, select, .no-print, .range-wrap { display: none !important; }
        .app-wrapper { display: block; }
        .main-content { overflow: visible; }
        .content-scroll { padding: 0; max-width: 100%; }
        .card { border: none; box-shadow: none; padding: 0; margin-bottom: 20px; }
    }
</style>
</head>
<body>

<div id="app"></div>
<div id="print-area"></div>

<!-- Modals -->
<div id="modal-overlay" class="modal-overlay" onclick="if(event.target===this) App.closeModal()">
    <div id="modal-content" class="modal-box"></div>
</div>

<script>
"use strict";

/* --------------------------------------------------------------------------
   Data Store
-------------------------------------------------------------------------- */
const Store = {
    key: "alif_median_v8_final",
    defaults: () => ({
        meta: { version: 8 },
        admin: { username: 'admin', password: '123', maxEventsPerStudent: 5 },
        teams: [
            { id: 't1', name: 'ZARQAN', password: '123' },
            { id: 't2', name: 'ASQALAN', password: '123' },
            { id: 't3', name: 'ASBAHAN', password: '123' }
        ],
        categories: ['SUB JUNIOR', 'JUNIOR', 'SENIOR', 'GENERAL'],
        competitions: [],
        students: [],
        entries: [],
        results: [], 
        logo: null, // Site Logo
        chestConfig: {
            widthCm: 9, heightCm: 13, radius: 0, bgColor: "#ffffff", logo: null, // Chest Logo
            elements: {
                qr: { x: 50, y: 35, size: 80, color: "#000000", visible: true },
                name: { x: 50, y: 65, size: 16, color: "#000000", bold: true, visible: true },
                chest: { x: 50, y: 78, size: 28, color: "#4f46e5", bold: true, visible: true },
                team: { x: 50, y: 90, size: 12, color: "#64748b", bold: false, visible: true },
                fest: { x: 50, y: 10, size: 18, color: "#1e293b", bold: true, text:"ALIF Fest", visible: true },
                logo: { x: 50, y: 20, size: 40, visible: false } // Position for chest logo
            }
        }
    }),
    load() { const d = localStorage.getItem(this.key); return d ? JSON.parse(d) : this.defaults(); },
    save(data) { localStorage.setItem(this.key, JSON.stringify(data)); }
};

/* --------------------------------------------------------------------------
   App Logic
-------------------------------------------------------------------------- */
const App = {
    data: Store.load(),
    state: { user: null, role: null, activeTab: 'setup', html5QrcodeScanner: null },

    init() {
        if(!localStorage.getItem(Store.key)) Store.save(this.data);
        this.renderLogin();
    },

    /* --- Auth --- */
    renderLogin() {
        // Use configured logo if available
        const logoHtml = this.data.logo 
            ? `<img src="${this.data.logo}" style="width:60px; height:60px; border-radius:12px; margin-bottom:15px">`
            : `<div class="logo-circle" style="margin:0 auto 15px; width:50px; height:50px; font-size:24px; background:var(--primary)">A</div>`;

        document.getElementById("app").innerHTML = `
            <div class="login-container">
                <div class="card login-box">
                    <div style="margin-bottom:30px">
                        ${logoHtml}
                        <h1 style="font-size:24px; margin-bottom:5px">ALIF Fest</h1>
                        <p>Campus Literary Arts Festival</p>
                    </div>
                    <div class="grid cols-2" style="gap:10px; margin-bottom:20px">
                         <button class="btn ${this.state.role!=='team'?'primary':''}" onclick="document.getElementById('adm-f').style.display='block';document.getElementById('tm-f').style.display='none';">Crew Login</button>
                         <button class="btn ${this.state.role==='team'?'primary':''}" onclick="document.getElementById('adm-f').style.display='none';document.getElementById('tm-f').style.display='block';">Team Portal</button>
                    </div>
                    <form id="adm-f" onsubmit="App.loginAdmin(event)">
                        <input class="input" id="u" placeholder="Username" style="margin-bottom:10px" value="${this.data.admin.username}">
                        <input class="input" type="password" id="p" placeholder="Password" style="margin-bottom:20px" value="${this.data.admin.password}">
                        <button class="btn primary" style="width:100%">Login to Dashboard</button>
                    </form>
                    <form id="tm-f" style="display:none" onsubmit="App.loginTeam(event)">
                        <select class="input" id="t-sel" style="margin-bottom:10px">
                            <option value="">Select Team</option>
                            ${this.data.teams.map(t => `<option value="${t.id}">${t.name}</option>`).join('')}
                        </select>
                        <input class="input" type="password" id="tp" placeholder="Team Password" style="margin-bottom:20px">
                        <button class="btn primary" style="width:100%">Enter Portal</button>
                    </form>
                </div>
            </div>
        `;
    },

    loginAdmin(e) {
        e.preventDefault();
        if(document.getElementById('u').value === this.data.admin.username && document.getElementById('p').value === this.data.admin.password) {
            this.state.role = 'admin'; this.state.user = 'Administrator'; this.state.activeTab = 'setup'; this.loadLayout();
        } else alert("Invalid Admin Credentials");
    },
    loginTeam(e) {
        e.preventDefault();
        const t = this.data.teams.find(x => x.id === document.getElementById('t-sel').value);
        if(t && t.password === document.getElementById('tp').value) {
            this.state.role = 'team'; this.state.user = t; this.state.activeTab = 'students'; this.loadLayout();
        } else alert("Invalid Team Password");
    },
    logout() { this.state.role = null; this.state.user = null; this.renderLogin(); },

    /* --- Layout --- */
    loadLayout() {
        const logoSrc = this.data.logo || '';
        const logoBg = this.data.logo ? 'transparent' : 'var(--primary)';
        
        const tabs = this.state.role === 'admin' 
            ? [
                {id:'setup', icon:'⚙️', lbl:'Setup & Settings'},
                {id:'comps', icon:'📋', lbl:'Competitions'},
                {id:'judge', icon:'⚖️', lbl:'Judge Panel'},
                {id:'scores', icon:'🏆', lbl:'Scoreboard'},
                {id:'students_rep', icon:'👥', lbl:'Reports'},
                {id:'chest', icon:'🏷️', lbl:'Chest Cards'}
              ]
            : [
                {id:'students', icon:'🎓', lbl:'My Students'},
                {id:'enroll', icon:'✍️', lbl:'Enrollment'},
                {id:'settings', icon:'⚙️', lbl:'Team Settings'}
              ];

        document.getElementById("app").innerHTML = `
            <div class="app-wrapper">
                <aside class="sidebar">
                    <div class="brand-area">
                        <div class="logo-circle" style="background:${logoBg}"><img src="${logoSrc}" style="width:100%;height:100%;border-radius:10px;object-fit:cover"></div>
                        <div><h3 style="margin:0;font-size:15px">ALIF Fest</h3><span style="font-size:11px;color:var(--text-muted)">${this.state.role === 'admin' ? 'Event Crew' : 'Team Portal'}</span></div>
                    </div>
                    <div class="nav-links">
                        ${tabs.map(t => `<div class="nav-item ${this.state.activeTab===t.id?'active':''}" onclick="App.switchTab('${t.id}')"><span>${t.icon}</span> ${t.lbl}</div>`).join('')}
                    </div>
                    <div style="margin-top:auto; padding-top:15px; border-top:1px solid var(--border-color)">
                        <div class="nav-item" onclick="App.logout()"><span>🚪</span> Logout</div>
                    </div>
                </aside>
                <main class="main-content">
                    <header class="top-bar">
                        <h2 style="margin:0; font-size:18px; font-weight:600">${tabs.find(t=>t.id===this.state.activeTab).lbl}</h2>
                        <div class="row">
                            ${this.state.role==='admin' ? `<button class="btn sm primary" onclick="App.openGlobalScanner()">📷 Scan QR</button>` : ''}
                            ${this.state.role==='admin' ? `<input class="input sm" style="width:200px" placeholder="Search..." oninput="App.globalSearch(this.value)">` : ''}
                        </div>
                    </header>
                    <div class="content-scroll" id="content-area"></div>
                </main>
            </div>
        `;
        this.renderTab();
    },

    switchTab(id) { this.state.activeTab = id; this.loadLayout(); },

    renderTab() {
        const el = document.getElementById("content-area");
        const t = this.state.activeTab;
        if(this.state.role === 'admin') {
            if(t==='setup') this.renderSetup(el);
            else if(t==='comps') this.renderComps(el);
            else if(t==='judge') this.renderJudge(el);
            else if(t==='scores') this.renderScores(el);
            else if(t==='students_rep') this.renderStudentRep(el);
            else if(t==='chest') this.renderChest(el);
        } else {
            if(t==='students') this.renderTeamStudents(el);
            else if(t==='enroll') this.renderTeamEnroll(el);
            else if(t==='settings') this.renderTeamSettings(el);
        }
    },

    /* --- 1. Setup (Site Logo Upload) --- */
    renderSetup(el) {
        el.innerHTML = `
            <div class="grid cols-2">
                <div class="card">
                    <h3>Site Branding</h3>
                    <div class="row" style="margin-bottom:15px">
                        ${this.data.logo ? `<img src="${this.data.logo}" style="width:50px;height:50px;border-radius:8px">` : ''}
                        <div>
                            <p style="font-size:12px;margin:0">Upload Site Logo (Square, Small file)</p>
                            <input type="file" accept="image/*" onchange="App.uploadSiteLogo(this)">
                        </div>
                    </div>
                    <button class="btn sm danger" onclick="App.removeSiteLogo()">Remove Logo</button>
                </div>
                <div class="card">
                    <h3>Admin Config</h3>
                    <form onsubmit="App.saveSettings(event)">
                        <label>Username</label><input class="input" id="adm-u" value="${this.data.admin.username}" style="margin-bottom:5px">
                        <label>Password</label><input class="input" id="adm-p" value="${this.data.admin.password}" style="margin-bottom:5px">
                        <label>Max Events (Student)</label><input class="input" type="number" id="adm-max" value="${this.data.admin.maxEventsPerStudent}">
                        <button class="btn primary" style="margin-top:10px">Save</button>
                    </form>
                </div>
                <div class="card">
                    <h3>Teams Management</h3>
                     <div style="max-height:200px; overflow-y:auto; margin-bottom:15px">
                        ${this.data.teams.map(t => `<div class="row" style="padding:8px; border-bottom:1px solid #eee; justify-content:space-between">
                            <span><strong>${t.name}</strong> <span class="tag gray">${t.password}</span></span>
                            <div>
                                <button class="btn sm" onclick="App.editTeam('${t.id}')">Edit</button>
                                <button class="btn sm danger" onclick="App.deleteTeam('${t.id}')">Del</button>
                            </div>
                        </div>`).join('')}
                    </div>
                    <button class="btn primary sm" onclick="App.addTeam()">+ Add Team</button>
                </div>
                <div class="card">
                    <h3>Backup / Reset</h3>
                    <div class="row">
                        <button class="btn" onclick="App.downloadData()">Backup JSON</button>
                        <label class="btn primary">Restore JSON <input type="file" hidden onchange="App.uploadData(this)"></label>
                    </div>
                    <button class="btn danger" style="margin-top:15px" onclick="App.wipeData()">⚠️ Wipe Data</button>
                </div>
            </div>
        `;
    },
    uploadSiteLogo(input) {
        const r = new FileReader(); r.onload = e => { this.data.logo = e.target.result; Store.save(this.data); this.loadLayout(); };
        if(input.files[0]) r.readAsDataURL(input.files[0]);
    },
    removeSiteLogo() { this.data.logo = null; Store.save(this.data); this.loadLayout(); },
    saveSettings(e) {
        e.preventDefault();
        this.data.admin.username = document.getElementById("adm-u").value;
        this.data.admin.password = document.getElementById("adm-p").value;
        this.data.admin.maxEventsPerStudent = parseInt(document.getElementById("adm-max").value);
        Store.save(this.data); alert("Saved");
    },
    addTeam() {
        const n = prompt("Team Name:"); if(!n) return; const p = prompt("Password:");
        this.data.teams.push({id:'t'+Date.now(), name:n.toUpperCase(), password:p||'123'}); Store.save(this.data); this.renderTab();
    },
    editTeam(id) {
        const t = this.data.teams.find(x=>x.id===id);
        const n = prompt("Name:", t.name); if(n) t.name=n.toUpperCase();
        const p = prompt("Password:", t.password); if(p) t.password=p;
        Store.save(this.data); this.renderTab();
    },
    deleteTeam(id) {
        if(confirm("Delete Team?")) {
            this.data.teams = this.data.teams.filter(t=>t.id!==id);
            this.data.students = this.data.students.filter(s=>s.teamId!==id);
            Store.save(this.data); this.renderTab();
        }
    },
    downloadData() {
        const a = document.createElement("a");
        a.href = URL.createObjectURL(new Blob([JSON.stringify(this.data)], {type:"application/json"}));
        a.download = "ALIF_Data.json"; a.click();
    },
    uploadData(input) {
        const r = new FileReader(); r.onload = e => { this.data = JSON.parse(e.target.result); Store.save(this.data); location.reload(); };
        r.readAsText(input.files[0]);
    },
    wipeData() { if(confirm("Wipe all data?")) { this.data.students=[]; this.data.entries=[]; this.data.results=[]; Store.save(this.data); location.reload(); } },

    /* --- 2. Competitions --- */
    renderComps(el) {
        el.innerHTML = `
            <div class="card">
                <h3>Add Competition</h3>
                <form class="row" onsubmit="App.addComp(event)">
                    <input class="input" id="c-n" placeholder="Name" required style="flex:2">
                    <select class="input" id="c-c" style="flex:1">${this.data.categories.map(c=>`<option>${c}</option>`).join('')}</select>
                    <label style="font-size:12px"><input type="checkbox" id="c-s"> Stage</label>
                    <button class="btn primary">Add</button>
                </form>
            </div>
            <div class="card">
                <table>
                    <thead><tr><th>Name</th><th>Category</th><th>Type</th><th>Entries</th><th>Action</th></tr></thead>
                    <tbody>
                        ${this.data.competitions.map(c => `
                        <tr><td>${c.name}</td><td><span class="tag blue">${c.category}</span></td><td>${c.isStage?'Stage':'Off'}</td>
                        <td>${this.data.entries.filter(e=>e.competitionId===c.id).length}</td>
                        <td><button class="btn sm danger" onclick="App.delComp('${c.id}')">Del</button></td></tr>`).join('')}
                    </tbody>
                </table>
            </div>
        `;
    },
    addComp(e) {
        e.preventDefault();
        this.data.competitions.push({ id: Date.now().toString(), name: document.getElementById("c-n").value, category: document.getElementById("c-c").value, isStage: document.getElementById("c-s").checked });
        Store.save(this.data); this.renderTab();
    },
    delComp(id) {
        if(confirm("Delete?")) { this.data.competitions = this.data.competitions.filter(c=>c.id!==id); this.data.entries = this.data.entries.filter(e=>e.competitionId!==id); Store.save(this.data); this.renderTab(); }
    },

    /* --- 3. Judge Panel & QR Attendance --- */
    renderJudge(el) {
        el.innerHTML = `<div class="grid cols-3">${this.data.competitions.map(c => `
            <div class="card" style="cursor:pointer" onclick="App.openScoreSheet('${c.id}')">
                <div class="row" style="justify-content:space-between"><h3>${c.name}</h3><span class="tag blue">${c.category}</span></div>
                <p style="font-size:13px">${this.data.entries.filter(e=>e.competitionId===c.id).length} Entries</p>
            </div>`).join('')}</div>`;
    },
    openScoreSheet(cid) {
        const c = this.data.competitions.find(x=>x.id===cid);
        const ents = this.data.entries.filter(e=>e.competitionId===cid);
        const modal = document.getElementById("content-area");
        modal.innerHTML = `
            <div class="row" style="margin-bottom:20px">
                <button class="btn" onclick="App.switchTab('judge')">← Back</button>
                <h2>Judging: ${c.name}</h2>
                <div style="flex:1"></div>
                <button class="btn primary" onclick="App.scanAttendance('${cid}')">📷 Scan Attendance</button>
                <button class="btn" onclick="App.autoCode('${cid}')">⚡ Auto-Code</button>
            </div>
            <div class="card">
                <table>
                    <thead><tr><th>Chest</th><th>Code</th><th>Student</th><th>Attended?</th><th>Rank</th><th>Points</th><th>Act</th></tr></thead>
                    <tbody>
                        ${ents.map(e => this.judgeRow(e)).join('')}
                    </tbody>
                </table>
            </div>
        `;
    },
    judgeRow(e) {
        const s = this.data.students.find(x=>x.id===e.memberStudentIds[0]);
        const res = this.data.results.find(r=>r.entryId===e.id) || {};
        return `<tr>
            <td><span class="tag gold">#${s.chestNo}</span></td>
            <td><input class="input sm" style="width:50px;text-align:center;color:var(--primary);font-weight:bold" value="${res.codeLetter||''}" id="cl-${e.id}"></td>
            <td>${s.name}</td>
            <td><input type="checkbox" id="att-${e.id}" ${res.attendance?'checked':''} style="transform:scale(1.3)"></td>
            <td><input class="input sm" style="width:60px" id="rnk-${e.id}" value="${res.rankLabel||''}" placeholder="1,2.."></td>
            <td><input class="input sm" type="number" style="width:60px" id="pts-${e.id}" value="${res.pointsAwarded||0}"></td>
            <td><button class="btn sm primary" onclick="App.saveResult('${e.id}','${e.competitionId}')">Save</button></td>
        </tr>`;
    },
    saveResult(eid, cid) {
        const att = document.getElementById(`att-${eid}`).checked;
        const rnk = document.getElementById(`rnk-${eid}`).value;
        const pts = Number(document.getElementById(`pts-${eid}`).value);
        const cl = document.getElementById(`cl-${eid}`).value.toUpperCase();
        this.data.results = this.data.results.filter(r=>r.entryId!==eid);
        this.data.results.push({ id:Date.now().toString(), competitionId:cid, entryId:eid, rankLabel:rnk, pointsAwarded:pts, attendance:att, codeLetter:cl });
        Store.save(this.data);
        const btn = event.target; btn.innerText="Saved"; btn.style.background="var(--success)"; setTimeout(()=>{btn.innerText="Save";btn.style.background="var(--primary)"},1000);
    },
    autoCode(cid) {
        if(!confirm("Generate Codes?")) return;
        const ents = this.data.entries.filter(e=>e.competitionId===cid);
        const codes = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split('').sort(()=>0.5-Math.random());
        ents.forEach((e,i) => {
            let code = codes[i%codes.length] + (Math.floor(i/26)||'');
            let res = this.data.results.find(r=>r.entryId===e.id);
            if(res) res.codeLetter = code;
            else this.data.results.push({ id:Date.now().toString(), competitionId:cid, entryId:e.id, rankLabel:'', pointsAwarded:0, attendance:false, codeLetter:code });
        });
        Store.save(this.data); this.openScoreSheet(cid);
    },

    /* --- 4. Chest Card Designer --- */
    renderChest(el) {
        const cfg = this.data.chestConfig;
        el.innerHTML = `
            <div class="grid cols-2">
                <div class="card" style="max-height:85vh; overflow-y:auto">
                    <h3>🎨 Designer</h3>
                    <div class="row">
                        <label>Width (cm) <input class="input sm" type="number" value="${cfg.widthCm}" onchange="App.updChest('widthCm',this.value)"></label>
                        <label>Height (cm) <input class="input sm" type="number" value="${cfg.heightCm}" onchange="App.updChest('heightCm',this.value)"></label>
                        <label>Radius <input class="input sm" type="number" value="${cfg.radius}" onchange="App.updChest('radius',this.value)"></label>
                        <label>BgColor <input type="color" class="color-inp" value="${cfg.bgColor}" onchange="App.updChest('bgColor',this.value)"></label>
                    </div>
                    <hr style="margin:15px 0; border:0; border-top:1px solid #eee">
                    
                    <div style="margin-bottom:15px">
                        <p>Chest Card Logo</p>
                        <input type="file" accept="image/*" onchange="App.updChestLogo(this)">
                        ${cfg.logo ? `<button class="btn sm danger" onclick="App.remChestLogo()">Remove</button>` : ''}
                    </div>

                    ${['fest','name','chest','team','qr','logo'].map(k => `
                        <div style="background:#f9fafb; padding:10px; border-radius:8px; margin-bottom:10px;">
                            <div class="row" style="justify-content:space-between">
                                <strong style="text-transform:capitalize">${k}</strong>
                                <label><input type="checkbox" ${cfg.elements[k].visible?'checked':''} onchange="App.updChest('elements.${k}.visible',this.checked)"> Show</label>
                            </div>
                            ${cfg.elements[k].visible ? `
                            <div class="range-wrap"><span>X</span> <input type="range" min="0" max="100" value="${cfg.elements[k].x}" oninput="App.updChest('elements.${k}.x',this.value)"></div>
                            <div class="range-wrap"><span>Y</span> <input type="range" min="0" max="100" value="${cfg.elements[k].y}" oninput="App.updChest('elements.${k}.y',this.value)"></div>
                            <div class="range-wrap"><span>Size</span> <input type="range" min="5" max="150" value="${cfg.elements[k].size}" oninput="App.updChest('elements.${k}.size',this.value)"></div>
                            ${k!=='qr' && k!=='logo' ? `
                                <div class="row">
                                    <label>Color <input type="color" class="color-inp" value="${cfg.elements[k].color}" onchange="App.updChest('elements.${k}.color',this.value)"></label>
                                    <label><input type="checkbox" ${cfg.elements[k].bold?'checked':''} onchange="App.updChest('elements.${k}.bold',this.checked)"> Bold</label>
                                    ${k==='fest'?`<input class="input sm" value="${cfg.elements[k].text}" oninput="App.updChest('elements.${k}.text',this.value)">`:''}
                                </div>
                            `:''}
                            `:''}
                        </div>
                    `).join('')}
                </div>
                <div class="card" style="display:flex;flex-direction:column;align-items:center;justify-content:center;background:#eef2ff">
                    <div id="cc-prev"></div>
                    <button class="btn primary" style="margin-top:20px" onclick="App.printChest()">🖨️ Print All Cards</button>
                </div>
            </div>
        `;
        setTimeout(() => this.renderChestPreview(), 100);
    },
    updChest(path, val) {
        let obj = this.data.chestConfig; const keys = path.split('.');
        for(let i=0; i<keys.length-1; i++) obj = obj[keys[i]];
        obj[keys[keys.length-1]] = (path.includes('visible')||path.includes('bold')) ? val : (isNaN(val)||path.includes('color')||path.includes('text') ? val : Number(val));
        Store.save(this.data); this.renderChestPreview();
    },
    updChestLogo(inp) {
        const r = new FileReader(); r.onload = e => { this.data.chestConfig.logo = e.target.result; Store.save(this.data); this.renderChest(document.getElementById("content-area")); };
        if(inp.files[0]) r.readAsDataURL(inp.files[0]);
    },
    remChestLogo() { this.data.chestConfig.logo = null; Store.save(this.data); this.renderChest(document.getElementById("content-area")); },
    renderChestPreview() {
        const box = document.getElementById("cc-prev"); if(!box) return;
        const cfg = this.data.chestConfig;
        const scale = 3.78; // Approx px per mm
        const w = cfg.widthCm * 10 * scale; const h = cfg.heightCm * 10 * scale;
        
        // Use Dummy Data
        const s = {name: "John Doe", chest: "101", team: "ZARQAN"};
        
        box.innerHTML = `
            <div style="position:relative; width:${w}px; height:${h}px; background:${cfg.bgColor}; border-radius:${cfg.radius}px; overflow:hidden; box-shadow:0 4px 12px rgba(0,0,0,0.1);">
                ${this.ccEl('fest',cfg,s)} ${this.ccEl('name',cfg,s)} ${this.ccEl('chest',cfg,s)} 
                ${this.ccEl('team',cfg,s)} ${this.ccEl('logo',cfg,s)}
                <div id="qr-prev" style="position:absolute; top:${cfg.elements.qr.y}%; left:${cfg.elements.qr.x}%; transform:translate(-50%,-50%); display:${cfg.elements.qr.visible?'block':'none'}"></div>
            </div>
        `;
        new QRCode(document.getElementById("qr-prev"), {text:`ID:123`, width:cfg.elements.qr.size, height:cfg.elements.qr.size, colorDark:cfg.elements.qr.color, colorLight:"transparent"});
    },
    ccEl(k,cfg,s) {
        const el = cfg.elements[k]; if(!el.visible) return '';
        if(k==='logo') return `<img src="${cfg.logo}" style="position:absolute; top:${el.y}%; left:${el.x}%; width:${el.size}px; transform:translate(-50%,-50%)">`;
        const txt = k==='fest'?el.text : (k==='name'?s.name : (k==='chest'?s.chest : s.team));
        return `<div style="position:absolute; top:${el.y}%; left:${el.x}%; transform:translate(-50%,-50%); font-size:${el.size}px; color:${el.color}; font-weight:${el.bold?'bold':'normal'}; white-space:nowrap;">${txt}</div>`;
    },
    printChest() {
        const p = document.getElementById("print-area");
        const cfg = this.data.chestConfig;
        // CSS for Print: CM dimensions
        const style = `<style>@media print { .cc-wrap { width:${cfg.widthCm}cm; height:${cfg.heightCm}cm; position:relative; display:inline-block; margin:0.2cm; page-break-inside:avoid; background:${cfg.bgColor}; border-radius:${cfg.radius}px; overflow:hidden; border:1px dashed #ccc; } .cc-el { position:absolute; transform:translate(-50%,-50%); white-space:nowrap; text-align:center; } }</style>`;
        
        const cards = this.data.students.map(s => {
             const t = this.data.teams.find(x=>x.id===s.teamId);
             const dummyS = {name:s.name, chest:s.chestNo, team:t.name};
             return `<div class="cc-wrap">
                ${this.ccPrintEl('fest',cfg,dummyS)} ${this.ccPrintEl('name',cfg,dummyS)} ${this.ccPrintEl('chest',cfg,dummyS)}
                ${this.ccPrintEl('team',cfg,dummyS)} ${this.ccPrintEl('logo',cfg,dummyS)}
                <div class="cc-el" style="top:${cfg.elements.qr.y}%; left:${cfg.elements.qr.x}%; display:${cfg.elements.qr.visible?'block':'none'}">
                    <div id="qr-p-${s.id}"></div>
                </div>
             </div>`;
        }).join('');
        
        p.innerHTML = style + cards;
        this.data.students.forEach(s => {
            const el = document.getElementById(`qr-p-${s.id}`);
            if(el) new QRCode(el, {text:`ID:${s.id}`, width:cfg.elements.qr.size, height:cfg.elements.qr.size, colorDark:cfg.elements.qr.color, colorLight:"transparent"});
        });
        setTimeout(() => window.print(), 500); // Wait for QRs
    },
    ccPrintEl(k,cfg,s) {
        const el = cfg.elements[k]; if(!el.visible) return '';
        if(k==='logo') return `<img src="${cfg.logo}" class="cc-el" style="top:${el.y}%; left:${el.x}%; width:${el.size}px;">`;
        const txt = k==='fest'?el.text : (k==='name'?s.name : (k==='chest'?s.chest : s.team));
        // Scale font for print (approx conversion px to pt or maintain relative)
        return `<div class="cc-el" style="top:${el.y}%; left:${el.x}%; font-size:${el.size}px; color:${el.color}; font-weight:${el.bold?'bold':'normal'}">${txt}</div>`;
    },

    /* --- 5. Scanner Logic --- */
    openGlobalScanner() { this.startScanner(res => { this.closeModal(); this.viewStudentPrograms(res); }); },
    scanAttendance(cid) { this.startScanner(res => { this.closeModal(); this.markAttendanceByQR(res, cid); }); },
    
    startScanner(callback) {
        const html = `
            <h3>📷 QR Scanner</h3>
            <div id="reader"></div>
            <p style="text-align:center; font-size:12px; color:orange">Ensure you are on Localhost or HTTPS for camera access.</p>
            <button class="btn danger" style="width:100%" onclick="App.stopScanner()">Close</button>
        `;
        this.openModal(html);
        
        this.state.html5QrcodeScanner = new Html5QrcodeScanner("reader", { fps: 10, qrbox: 250 });
        this.state.html5QrcodeScanner.render((decodedText) => {
            // Parse "ID:123"
            if(decodedText.startsWith("ID:")) {
                const sid = decodedText.split(":")[1];
                const s = this.data.students.find(x=>x.id === sid);
                if(s) {
                    // Stop scanning
                    this.state.html5QrcodeScanner.clear();
                    callback(sid);
                } else {
                    alert("Student not found in database.");
                }
            }
        });
    },
    stopScanner() {
        if(this.state.html5QrcodeScanner) this.state.html5QrcodeScanner.clear();
        this.closeModal();
    },
    markAttendanceByQR(sid, cid) {
        const ent = this.data.entries.find(e => e.competitionId === cid && e.memberStudentIds[0] === sid);
        if(!ent) return alert("Student not enrolled in this competition.");
        
        // Find or Create Result
        let res = this.data.results.find(r => r.entryId === ent.id);
        if(!res) {
            this.data.results.push({ id:Date.now().toString(), competitionId:cid, entryId:ent.id, rankLabel:'', pointsAwarded:0, attendance:true, codeLetter:'' });
        } else {
            res.attendance = true;
        }
        Store.save(this.data);
        alert(`Marked Attendance: ${this.data.students.find(s=>s.id===sid).name}`);
        this.openScoreSheet(cid); // Refresh View
    },

    /* --- 6. Scoreboard & Reports --- */
    renderScores(el) {
        const ranks = this.calcTeamScores();
        const toppers = this.getTopStudents();
        const topCard = (t, list) => {
             if(!list.length) return `<div class="card" style="padding:10px;text-align:center;font-size:12px;color:#999">${t}: -</div>`;
             const s = list[0];
             return `<div class="card" style="border:1px solid var(--primary-soft);text-align:center;padding:15px">
                <div style="font-size:10px;text-transform:uppercase;color:var(--primary);font-weight:bold">${t}</div>
                <div style="font-weight:bold;font-size:16px;margin:5px 0">${s.name}</div>
                <div style="font-size:11px;color:#666">#${s.chest} | ${s.team}</div>
                <div class="tag gold" style="margin-top:5px">${s[t.toLowerCase().includes('non')?'nonStage':'stage']} Pts</div>
             </div>`;
        };
        
        el.innerHTML = `
            <div class="row" style="justify-content:center; margin-bottom:20px">
                 ${ranks[0] ? `<div class="card" style="text-align:center;border-top:5px solid gold;transform:scale(1.1)"><div style="font-size:40px">👑</div><h1>${ranks[0].name}</h1><h2>${ranks[0].total} Pts</h2></div>` : ''}
            </div>
            <h3>Toppers</h3>
            <div class="grid cols-3" style="margin-bottom:20px">
                ${Object.keys(toppers).map(c => `<div style="display:flex;flex-direction:column;gap:10px"><h4 style="text-align:center">${c}</h4>${topCard('Stage',toppers[c].stage)}${topCard('Non-Stage',toppers[c].nonStage)}</div>`).join('')}
            </div>
            <h3>Teams</h3>
            <div class="card"><table><thead><tr><th>Rank</th><th>Team</th><th>Pts</th></tr></thead><tbody>${ranks.map((t,i)=>`<tr><td>#${i+1}</td><td>${t.name}</td><td>${t.total}</td></tr>`).join('')}</tbody></table></div>
        `;
    },
    calcTeamScores() {
        const ts = {}; this.data.teams.forEach(t=>ts[t.id]={name:t.name,total:0});
        this.data.results.forEach(r => {
            const e=this.data.entries.find(x=>x.id===r.entryId); if(!e) return;
            if(r.rankLabel !== '3') ts[e.teamId].total += (r.pointsAwarded||0);
        });
        return Object.values(ts).sort((a,b)=>b.total-a.total);
    },
    getTopStudents() {
        const cats = this.data.categories.filter(c=>c!=='GENERAL');
        const map = {}; cats.forEach(c=>map[c]={stage:[],nonStage:[]});
        const sPts = {};
        this.data.results.forEach(r => {
            const e=this.data.entries.find(x=>x.id===r.entryId); if(!e) return;
            const c=this.data.competitions.find(x=>x.id===e.competitionId);
            if(!c || c.category==='GENERAL') return;
            const sid=e.memberStudentIds[0]; const s=this.data.students.find(x=>x.id===sid);
            if(!sPts[sid]) sPts[sid]={id:sid,stage:0,nonStage:0,cat:s.category,name:s.name,chest:s.chestNo,team:this.data.teams.find(t=>t.id===s.teamId).name};
            if(c.isStage) sPts[sid].stage+=(r.pointsAwarded||0); else sPts[sid].nonStage+=(r.pointsAwarded||0);
        });
        Object.values(sPts).forEach(p => { if(map[p.cat]) { if(p.stage>0)map[p.cat].stage.push(p); if(p.nonStage>0)map[p.cat].nonStage.push(p); } });
        cats.forEach(c => { map[c].stage.sort((a,b)=>b.stage-a.stage); map[c].nonStage.sort((a,b)=>b.nonStage-a.nonStage); });
        return map;
    },
    
    /* --- 7. Student Report --- */
    renderStudentRep(el) { el.innerHTML = `<button class="btn primary" onclick="window.print()">Print</button><div class="card" style="margin-top:10px">${this.data.teams.map(t=>`<h4>${t.name}</h4><ul>${this.data.students.filter(s=>s.teamId===t.id).map(s=>`<li>${s.name} (#${s.chestNo})</li>`).join('')}</ul>`).join('')}</div>`; },

    /* --- 8. Team Module --- */
    renderTeamStudents(el) {
        const myS = this.data.students.filter(s=>s.teamId===this.state.user.id);
        el.innerHTML = `<div class="card"><h3>Add Student</h3><form class="row" onsubmit="App.addStudent(event)"><input class="input" id="s-n" placeholder="Name" required style="flex:2"><input class="input" id="s-c" placeholder="Chest No" required><select class="input" id="s-cat">${this.data.categories.filter(c=>c!=='GENERAL').map(c=>`<option>${c}</option>`).join('')}</select><button class="btn primary">Add</button></form></div>
        <div class="card"><table><thead><tr><th>#</th><th>Name</th><th>Cat</th><th>Act</th></tr></thead><tbody>${myS.map(s=>`<tr><td>${s.chestNo}</td><td>${s.name}</td><td>${s.category}</td><td><button class="btn sm danger" onclick="App.delStudent('${s.id}')">X</button></td></tr>`).join('')}</tbody></table></div>`;
    },
    addStudent(e) { e.preventDefault(); const c=document.getElementById('s-c').value; if(this.data.students.find(s=>s.chestNo===c)) return alert("Chest Exists"); this.data.students.push({id:Date.now().toString(), teamId:this.state.user.id, name:document.getElementById('s-n').value, chestNo:c, category:document.getElementById('s-cat').value}); Store.save(this.data); this.renderTab(); },
    delStudent(id) { if(confirm("Del?")) { this.data.students=this.data.students.filter(s=>s.id!==id); this.data.entries=this.data.entries.filter(e=>!e.memberStudentIds.includes(id)); Store.save(this.data); this.renderTab(); } },
    renderTeamEnroll(el) {
        const myS = this.data.students.filter(s=>s.teamId===this.state.user.id);
        el.innerHTML = `<div class="grid cols-3">${this.data.competitions.map(c => {
            const enr = this.data.entries.filter(e=>e.competitionId===c.id && e.teamId===this.state.user.id);
            const eli = myS.filter(s=>c.category==='GENERAL'||s.category===c.category);
            return `<div class="card"><strong>${c.name}</strong> <span class="tag gray">${c.category}</span>
            <div style="margin:10px 0">${enr.map(e=>`<span class="tag green">${this.data.students.find(x=>x.id===e.memberStudentIds[0]).name} <b onclick="App.unenroll('${e.id}')" style="cursor:pointer">x</b></span>`).join(' ')}</div>
            <form class="row" onsubmit="App.enroll(event,'${c.id}')"><select class="input sm" id="e-${c.id}">${eli.map(s=>`<option value="${s.id}">${s.name}</option>`).join('')}</select><button class="btn sm primary">Enroll</button></form></div>`;
        }).join('')}</div>`;
    },
    enroll(e, cid) {
        e.preventDefault(); const sid = document.getElementById(`e-${cid}`).value; if(!sid) return;
        if(this.data.entries.find(e=>e.competitionId===cid && e.memberStudentIds.includes(sid))) return alert("Enrolled");
        const c = this.data.competitions.find(x=>x.id===cid);
        if(c.category!=='GENERAL') {
            const cnt = this.data.entries.filter(e=>e.memberStudentIds.includes(sid) && this.data.competitions.find(x=>x.id===e.competitionId).category!=='GENERAL').length;
            if(cnt >= this.data.admin.maxEventsPerStudent) return alert("Limit Reached");
        }
        this.data.entries.push({id:Date.now().toString(), competitionId:cid, teamId:this.state.user.id, memberStudentIds:[sid]}); Store.save(this.data); this.renderTab();
    },
    unenroll(eid) { this.data.entries=this.data.entries.filter(e=>e.id!==eid); Store.save(this.data); this.renderTab(); },
    renderTeamSettings(el) { el.innerHTML = `<div class="card">Contact Admin to change credentials.</div>`; },

    /* --- 9. Global Search & View --- */
    globalSearch(q) {
        const el = document.getElementById("content-area"); if(q.length<2) { this.renderTab(); return; }
        const sRes = this.data.students.filter(s=>s.name.toLowerCase().includes(q)||s.chestNo.includes(q));
        el.innerHTML = `<h3>Results</h3><div class="card">${sRes.map(s=>`<div class="row" style="padding:10px;border-bottom:1px solid #eee"><b>${s.name}</b> (#${s.chestNo}) <button class="btn sm primary" onclick="App.viewStudentPrograms('${s.id}')">View</button></div>`).join('')}</div>`;
    },
    viewStudentPrograms(sid) {
        const s = this.data.students.find(x=>x.id===sid); if(!s) return;
        const enr = this.data.entries.filter(e=>e.memberStudentIds.includes(sid));
        let h = `<h3>${s.name} (#${s.chestNo})</h3><p>${s.category} | ${this.data.teams.find(t=>t.id===s.teamId).name}</p><table style="width:100%">`;
        enr.forEach(e => {
            const c = this.data.competitions.find(x=>x.id===e.competitionId);
            const r = this.data.results.find(x=>x.entryId===e.id);
            h += `<tr><td>${c.name}</td><td><span class="tag ${r&&r.rankLabel?'gold':'gray'}">${r?r.rankLabel||'Participated':'Enrolled'}</span></td><td>${r?r.pointsAwarded+' pts':'-'}</td></tr>`;
        });
        h += `</table><button class="btn" style="margin-top:15px;width:100%" onclick="App.closeModal()">Close</button>`;
        this.openModal(h);
    },
    openModal(h) { document.getElementById("modal-content").innerHTML=h; document.getElementById("modal-overlay").style.display="flex"; },
    closeModal() { document.getElementById("modal-overlay").style.display="none"; if(this.state.html5QrcodeScanner) this.state.html5QrcodeScanner.clear(); }
};

App.init();
</script>
</body>
</html>
