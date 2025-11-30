# Alif25

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>ALIF – Campus Literary Arts Fest</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
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
        margin: 0;
        padding: 0;
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
    
    /* Sidebar */
    .sidebar {
        width: 260px;
        background: var(--bg-sidebar);
        border-right: 1px solid var(--border-color);
        display: flex;
        flex-direction: column;
        padding: 20px 15px;
        flex-shrink: 0;
    }
    
    .brand-area {
        display: flex;
        align-items: center;
        gap: 12px;
        padding: 0 10px 25px 10px;
        margin-bottom: 10px;
        border-bottom: 1px solid var(--border-color);
    }
    
    .logo-circle {
        width: 36px; height: 36px;
        background: var(--primary); color: #fff;
        border-radius: 10px;
        display: grid; place-items: center;
        font-weight: 700; font-size: 18px;
        object-fit: cover;
    }

    .nav-links { display: flex; flex-direction: column; gap: 4px; overflow-y: auto; flex: 1; }
    
    .nav-item {
        display: flex; align-items: center; gap: 12px;
        padding: 10px 12px;
        border-radius: var(--radius-sm);
        color: var(--text-secondary);
        text-decoration: none;
        font-weight: 500;
        cursor: pointer;
        transition: all 0.2s ease;
    }
    .nav-item:hover { background: var(--bg-hover); color: var(--text-main); }
    .nav-item.active { background: #fff; color: var(--primary); box-shadow: var(--shadow-sm); font-weight: 600; }

    /* Main Content */
    .main-content {
        flex: 1;
        display: flex;
        flex-direction: column;
        overflow: hidden;
        background: var(--bg-body);
    }

    .top-bar {
        height: 64px;
        border-bottom: 1px solid var(--border-color);
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 30px;
        background: rgba(255,255,255,0.8);
        backdrop-filter: blur(10px);
        z-index: 10;
    }

    .content-scroll {
        flex: 1;
        overflow-y: auto;
        padding: 30px;
        max-width: 1400px;
        margin: 0 auto;
        width: 100%;
    }

    /* --- UI Components --- */
    .card {
        background: #fff;
        border: 1px solid var(--border-color);
        border-radius: var(--radius-md);
        padding: 24px;
        margin-bottom: 24px;
        box-shadow: var(--shadow-sm);
    }

    .grid { display: grid; gap: 24px; }
    .cols-2 { grid-template-columns: repeat(2, 1fr); }
    .cols-3 { grid-template-columns: repeat(3, 1fr); }
    .row { display: flex; align-items: center; gap: 12px; flex-wrap: wrap; }
    
    .btn {
        display: inline-flex; align-items: center; justify-content: center; gap: 8px;
        padding: 9px 16px;
        border-radius: var(--radius-sm);
        font-weight: 600; font-size: 13px;
        cursor: pointer; transition: all 0.2s;
        border: 1px solid var(--border-color);
        background: #fff; color: var(--text-secondary);
    }
    .btn:hover { background: var(--bg-hover); color: var(--text-main); border-color: var(--text-secondary); }
    .btn.primary { background: var(--primary); color: #fff; border-color: var(--primary); }
    .btn.primary:hover { background: var(--primary-hover); border-color: var(--primary-hover); box-shadow: 0 2px 4px rgba(79, 70, 229, 0.3); }
    .btn.danger { background: #fee2e2; color: var(--danger); border-color: #fecaca; }
    .btn.danger:hover { background: var(--danger); color: #fff; }
    .btn.sm { padding: 6px 12px; font-size: 12px; }

    .input, select {
        width: 100%;
        padding: 10px 12px;
        border-radius: var(--radius-sm);
        border: 1px solid var(--border-color);
        background: #fff;
        font-family: var(--font-main);
        font-size: 14px;
        color: var(--text-main);
        transition: border-color 0.2s, box-shadow 0.2s;
    }
    .input:focus, select:focus {
        border-color: var(--primary);
        box-shadow: 0 0 0 3px var(--primary-soft);
    }

    /* Tags */
    .tag {
        padding: 4px 10px; border-radius: 20px;
        font-size: 11px; font-weight: 700;
        text-transform: uppercase; letter-spacing: 0.5px;
        display: inline-block;
    }
    .tag.blue { background: var(--primary-soft); color: var(--primary); }
    .tag.green { background: #d1fae5; color: var(--success); }
    .tag.gold { background: #fef3c7; color: #d97706; }
    .tag.gray { background: #f1f5f9; color: var(--text-secondary); }

    /* Tables */
    table { width: 100%; border-collapse: separate; border-spacing: 0; }
    th {
        text-align: left; padding: 12px 16px;
        border-bottom: 1px solid var(--border-color);
        color: var(--text-secondary); font-size: 12px; font-weight: 600; text-transform: uppercase;
        background: #fafafa;
    }
    td { padding: 14px 16px; border-bottom: 1px solid var(--border-color); color: var(--text-main); font-size: 14px; }
    tr:last-child td { border-bottom: none; }
    tbody tr:hover { background: #f8fafc; }

    /* Modal */
    .modal-overlay {
        position: fixed; top: 0; left: 0; width: 100%; height: 100%;
        background: rgba(0,0,0,0.4); backdrop-filter: blur(4px);
        z-index: 100; display: none; align-items: center; justify-content: center;
    }
    .modal-box {
        background: #fff; width: 500px; max-width: 90%;
        border-radius: var(--radius-lg); padding: 30px;
        box-shadow: var(--shadow-md);
        animation: slideUp 0.2s ease-out;
    }
    @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

    /* Login */
    .login-container {
        display: flex; align-items: center; justify-content: center;
        height: 100vh; background: #fff;
    }
    .login-box { width: 380px; text-align: center; border: none; box-shadow: none; }
    
    /* Print */
    @media print {
        .sidebar, .top-bar, .btn, .input, select, .no-print { display: none !important; }
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

<!-- Modal Template -->
<div id="modal-overlay" class="modal-overlay" onclick="if(event.target===this) App.closeModal()">
    <div id="modal-content" class="modal-box"></div>
</div>

<script>
"use strict";

/* --------------------------------------------------------------------------
   Data Store & Configuration
-------------------------------------------------------------------------- */
const Store = {
    key: "alif_median_v6",
    defaults: () => ({
        meta: { version: 6 },
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
        results: [], // { id, competitionId, entryId, rankLabel, pointsAwarded, attendance, codeLetter }
        logo: null,
        chestConfig: {
            widthCm: 9, heightCm: 13, bgColor: "#ffffff",
            elements: {
                qr: { x: 50, y: 35, size: 80, color: "#000000", bold: false, visible: true },
                name: { x: 50, y: 65, size: 16, color: "#000000", bold: true, visible: true },
                chest: { x: 50, y: 78, size: 28, color: "#4f46e5", bold: true, visible: true },
                team: { x: 50, y: 90, size: 12, color: "#64748b", bold: false, visible: true },
                fest: { x: 50, y: 10, size: 18, color: "#1e293b", bold: true, text:"ALIF Fest", visible: true }
            }
        }
    }),
    load() {
        const d = localStorage.getItem(this.key);
        return d ? JSON.parse(d) : this.defaults();
    },
    save(data) {
        localStorage.setItem(this.key, JSON.stringify(data));
    }
};

/* --------------------------------------------------------------------------
   Application Logic
-------------------------------------------------------------------------- */
const App = {
    data: Store.load(),
    state: { user: null, role: null, activeTab: 'setup' },

    init() {
        if(!localStorage.getItem(Store.key)) Store.save(this.data);
        this.renderLogin();
    },

    /* --- Auth --- */
    renderLogin() {
        document.getElementById("app").innerHTML = `
            <div class="login-container">
                <div class="card login-box">
                    <div style="margin-bottom:30px">
                        <div class="logo-circle" style="margin:0 auto 15px; width:50px; height:50px; font-size:24px; background:var(--primary)">A</div>
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
        const logoTxt = this.data.logo ? '' : 'A';
        const logoBg = this.data.logo ? 'transparent' : 'var(--primary)';
        
        const tabs = this.state.role === 'admin' 
            ? [
                {id:'setup', icon:'⚙️', lbl:'Setup & Settings'},
                {id:'comps', icon:'📋', lbl:'Competitions'},
                {id:'judge', icon:'⚖️', lbl:'Judge Panel'},
                {id:'scores', icon:'🏆', lbl:'Scoreboard'},
                {id:'students_rep', icon:'👥', lbl:'Student Report'},
                {id:'entries_rep', icon:'📝', lbl:'Entry Report'},
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
                        <div class="logo-circle" style="background:${logoBg}"><img src="${logoSrc}" alt="${logoTxt}" style="width:100%;height:100%;border-radius:10px;object-fit:cover"></div>
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
                            ${this.state.role==='admin' ? `<input class="input sm" style="width:240px" placeholder="Search Student / Comp..." oninput="App.globalSearch(this.value)">` : ''}
                            <div class="tag gray">${this.state.role==='admin' ? this.data.admin.username : this.state.user.name}</div>
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
        const tab = this.state.activeTab;
        
        if(this.state.role === 'admin') {
            if(tab==='setup') this.renderSetup(el);
            else if(tab==='comps') this.renderComps(el);
            else if(tab==='judge') this.renderJudge(el);
            else if(tab==='scores') this.renderScores(el);
            else if(tab==='students_rep') this.renderStudentRep(el);
            else if(tab==='entries_rep') this.renderEntryRep(el);
            else if(tab==='chest') this.renderChest(el);
        } else {
            if(tab==='students') this.renderTeamStudents(el);
            else if(tab==='enroll') this.renderTeamEnroll(el);
            else if(tab==='settings') this.renderTeamSettings(el);
        }
    },

    /* ----------------------------------------------------------------------
       ADMIN MODULES
       ---------------------------------------------------------------------- */
    
    /* 1. Setup */
    renderSetup(el) {
        el.innerHTML = `
            <div class="grid cols-2">
                <div class="card">
                    <h3>General Settings</h3>
                    <form onsubmit="App.saveSettings(event)">
                        <label>Admin Username</label><input class="input" id="adm-u" value="${this.data.admin.username}" style="margin-bottom:10px">
                        <label>Admin Password</label><input class="input" id="adm-p" value="${this.data.admin.password}" style="margin-bottom:10px">
                        <label>Max Programs per Student (Excl. General)</label>
                        <input class="input" type="number" id="adm-max" value="${this.data.admin.maxEventsPerStudent || 5}" style="margin-bottom:20px">
                        <button class="btn primary">Save Config</button>
                    </form>
                </div>
                <div class="card">
                    <h3>Teams Management</h3>
                    <div style="max-height:200px; overflow-y:auto; margin-bottom:15px">
                        ${this.data.teams.map(t => `<div class="row" style="padding:8px; border-bottom:1px solid #eee; justify-content:space-between">
                            <span><strong>${t.name}</strong> <span class="tag gray">${t.password}</span></span>
                            <button class="btn sm danger" onclick="App.deleteTeam('${t.id}')">Remove</button>
                        </div>`).join('')}
                    </div>
                    <button class="btn primary sm" onclick="App.addTeam()">+ Add Team</button>
                </div>
                <div class="card">
                    <h3>Data Control</h3>
                    <div class="row">
                        <button class="btn" onclick="App.downloadData()">⬇️ Backup JSON</button>
                        <label class="btn primary">⬆️ Restore JSON <input type="file" hidden onchange="App.uploadData(this)"></label>
                    </div>
                    <div style="margin-top:20px; padding-top:20px; border-top:1px solid #eee">
                        <button class="btn danger" onclick="App.wipeData()">⚠️ Wipe All Data</button>
                    </div>
                </div>
            </div>
        `;
    },
    saveSettings(e) {
        e.preventDefault();
        this.data.admin.username = document.getElementById("adm-u").value;
        this.data.admin.password = document.getElementById("adm-p").value;
        this.data.admin.maxEventsPerStudent = parseInt(document.getElementById("adm-max").value);
        Store.save(this.data); alert("Settings Saved");
    },
    addTeam() {
        const n = prompt("Team Name:"); if(!n) return;
        const p = prompt("Password:"); if(!p) return;
        this.data.teams.push({id:'t'+Date.now(), name:n.toUpperCase(), password:p}); Store.save(this.data); this.renderTab();
    },
    deleteTeam(id) {
        if(!confirm("Delete team?")) return;
        this.data.teams = this.data.teams.filter(t=>t.id!==id);
        this.data.students = this.data.students.filter(s=>s.teamId!==id);
        Store.save(this.data); this.renderTab();
    },
    downloadData() {
        const a = document.createElement("a");
        a.href = URL.createObjectURL(new Blob([JSON.stringify(this.data)], {type:"application/json"}));
        a.download = "ALIF_Backup.json"; a.click();
    },
    uploadData(input) {
        const r = new FileReader();
        r.onload = e => { this.data = JSON.parse(e.target.result); Store.save(this.data); location.reload(); };
        r.readAsText(input.files[0]);
    },
    wipeData() {
        if(confirm("WARNING: This will delete all students, competitions, and results. Admin login remains.") && prompt("Type DELETE to confirm")==="DELETE") {
            this.data.students=[]; this.data.entries=[]; this.data.results=[]; this.data.competitions=[];
            Store.save(this.data); location.reload();
        }
    },

    /* 2. Competitions */
    renderComps(el) {
        el.innerHTML = `
            <div class="card">
                <h3>Add Competition</h3>
                <form class="row" onsubmit="App.addComp(event)">
                    <input class="input" id="c-n" placeholder="Competition Name" required style="flex:2">
                    <select class="input" id="c-c" style="flex:1">${this.data.categories.map(c=>`<option>${c}</option>`).join('')}</select>
                    <div class="row" style="gap:15px; margin:0 10px;">
                        <label style="font-size:12px; display:flex; gap:5px"><input type="checkbox" id="c-s"> Stage Item?</label>
                    </div>
                    <button class="btn primary">Add</button>
                </form>
            </div>
            <div class="card">
                <table>
                    <thead><tr><th>Name</th><th>Category</th><th>Type</th><th>Entries</th><th>Action</th></tr></thead>
                    <tbody>
                        ${this.data.competitions.map(c => `
                        <tr>
                            <td>${c.name}</td>
                            <td><span class="tag ${c.category==='GENERAL'?'gray':'blue'}">${c.category}</span></td>
                            <td>${c.isStage ? 'Stage' : 'Off-Stage'}</td>
                            <td>${this.data.entries.filter(e=>e.competitionId===c.id).length}</td>
                            <td><button class="btn sm danger" onclick="App.delComp('${c.id}')">Delete</button></td>
                        </tr>`).join('')}
                    </tbody>
                </table>
            </div>
        `;
    },
    addComp(e) {
        e.preventDefault();
        this.data.competitions.push({
            id: Date.now().toString(),
            name: document.getElementById("c-n").value,
            category: document.getElementById("c-c").value,
            isStage: document.getElementById("c-s").checked
        });
        Store.save(this.data); this.renderTab();
    },
    delComp(id) {
        if(confirm("Delete competition?")) {
            this.data.competitions = this.data.competitions.filter(c=>c.id!==id);
            this.data.entries = this.data.entries.filter(e=>e.competitionId!==id);
            this.data.results = this.data.results.filter(r=>r.competitionId!==id);
            Store.save(this.data); this.renderTab();
        }
    },

    /* 3. Judge Panel (With Auto Code, Attendance, Search Buttons) */
    renderJudge(el) {
        el.innerHTML = `
            <div class="grid cols-3">
                ${this.data.competitions.map(c => `
                    <div class="card" style="cursor:pointer; transition:0.2s" onclick="App.openScoreSheet('${c.id}')">
                        <div class="row" style="justify-content:space-between">
                            <h3>${c.name}</h3>
                            <span class="tag blue">${c.category}</span>
                        </div>
                        <p style="margin:0; font-size:13px">${this.data.entries.filter(e=>e.competitionId===c.id).length} Entries</p>
                    </div>
                `).join('')}
            </div>
        `;
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
                <button class="btn primary" onclick="App.autoCode('${cid}')">⚡ Auto-Code</button>
            </div>
            <div class="card">
                <table id="j-table">
                    <thead>
                        <tr>
                            <th>Chest No</th>
                            <th>Code Letter</th>
                            <th>Details</th>
                            <th>Attended?</th>
                            <th>Rank / Grade</th>
                            <th>Points</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${ents.map(e => this.judgeRow(e)).join('')}
                    </tbody>
                </table>
            </div>
        `;
    },
    judgeRow(e) {
        const s = this.data.students.find(x=>x.id===e.memberStudentIds[0]);
        const t = this.data.teams.find(x=>x.id===s.teamId);
        const res = this.data.results.find(r=>r.entryId===e.id) || {};
        
        return `
            <tr>
                <td><span class="tag gold">#${s.chestNo}</span></td>
                <td><input class="input sm" style="width:60px;text-align:center;font-weight:bold;color:var(--primary)" value="${res.codeLetter||''}" id="cl-${e.id}" placeholder="-"></td>
                <td>
                    <strong>${s.name}</strong><br>
                    <span style="font-size:11px;color:var(--text-secondary)">${t.name}</span>
                </td>
                <td><input type="checkbox" id="att-${e.id}" ${res.attendance?'checked':''} style="transform:scale(1.3)"></td>
                <td><input class="input sm" id="rnk-${e.id}" value="${res.rankLabel||''}" placeholder="1, 2, 3 or A"></td>
                <td><input class="input sm" type="number" id="pts-${e.id}" value="${res.pointsAwarded||0}" style="width:60px"></td>
                <td><button class="btn sm primary" onclick="App.saveResult('${e.id}','${e.competitionId}')">Save</button></td>
            </tr>
        `;
    },
    saveResult(eid, cid) {
        const att = document.getElementById(`att-${eid}`).checked;
        const rnk = document.getElementById(`rnk-${eid}`).value;
        const pts = Number(document.getElementById(`pts-${eid}`).value);
        const cl = document.getElementById(`cl-${eid}`).value.toUpperCase();

        this.data.results = this.data.results.filter(r=>r.entryId!==eid);
        this.data.results.push({ id:Date.now().toString(), competitionId:cid, entryId:eid, rankLabel:rnk, pointsAwarded:pts, attendance:att, codeLetter:cl });
        Store.save(this.data);
        // Visual feedback
        const btn = event.target; btn.innerText="Saved"; btn.style.background="var(--success)";
        setTimeout(()=> { btn.innerText="Save"; btn.style.background="var(--primary)"; }, 1000);
    },
    autoCode(cid) {
        if(!confirm("Generate random Code Letters for all entries in this competition? Existing codes will be overwritten.")) return;
        const ents = this.data.entries.filter(e=>e.competitionId===cid);
        const codes = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split('').sort(() => 0.5 - Math.random());
        
        ents.forEach((e, idx) => {
            const code = codes[idx % codes.length] + (Math.floor(idx/26) || '');
            // Find existing result or create new
            let res = this.data.results.find(r=>r.entryId===e.id);
            if(res) res.codeLetter = code;
            else this.data.results.push({ id:Date.now().toString(), competitionId:cid, entryId:e.id, rankLabel:'', pointsAwarded:0, attendance:false, codeLetter:code });
        });
        Store.save(this.data);
        this.openScoreSheet(cid); // Refresh
    },

    /* 4. Scoreboard (Implemented Logic: General->Team Only, 3rd Grade->Student Only) */
    calcScores() {
        const tScores = {}; this.data.teams.forEach(t => tScores[t.id] = { name:t.name, total:0 });
        
        this.data.results.forEach(r => {
            const ent = this.data.entries.find(e=>e.id===r.entryId); if(!ent) return;
            const comp = this.data.competitions.find(c=>c.id===ent.competitionId); if(!comp) return;
            
            const points = r.pointsAwarded || 0;
            const isGeneral = comp.category === 'GENERAL';
            const isThirdGrade = r.rankLabel === '3'; // "3rd grade... point not add to team point" logic
            
            // Logic: 
            // 1. General -> Team YES, Student NO.
            // 2. 3rd Grade -> Team NO (per request), Student YES.
            // Conflict: What if General AND 3rd Grade? 
            // Combined: If General, Student NO. If 3rd Grade, Team NO.
            
            let addToTeam = true;
            if(isThirdGrade) addToTeam = false; 
            
            // Add to team
            if(addToTeam && tScores[ent.teamId]) {
                tScores[ent.teamId].total += points;
            }
        });
        
        return Object.values(tScores).sort((a,b)=>b.total - a.total);
    },
    renderScores(el) {
        const ranks = this.calcScores();
        el.innerHTML = `
            <div class="row" style="justify-content:center; margin-bottom:30px">
                ${ranks[0] ? `
                <div class="card" style="text-align:center; border-top:5px solid var(--accent-gold); transform:scale(1.1)">
                    <div style="font-size:40px">👑</div>
                    <h1 style="color:var(--accent-gold); font-size:32px">${ranks[0].name}</h1>
                    <p style="font-size:18px; font-weight:700">${ranks[0].total} Points</p>
                    <div class="tag gold">CHAMPION</div>
                </div>` : ''}
            </div>
            <div class="card">
                <h3>Full Standings</h3>
                <table>
                    <thead><tr><th>Rank</th><th>Team</th><th>Points</th></tr></thead>
                    <tbody>
                        ${ranks.map((t,i) => `<tr><td>#${i+1}</td><td><strong>${t.name}</strong></td><td>${t.total}</td></tr>`).join('')}
                    </tbody>
                </table>
                <p style="margin-top:20px; font-size:12px; color:var(--danger)">
                    * Note: Points for "General" items go to Team only. Points for "Rank 3/Grade 3" go to Students only (not Team).
                </p>
            </div>
        `;
    },

    /* 5. Global Search with Actions */
    globalSearch(q) {
        if(q.length < 2) { this.renderTab(); return; }
        q = q.toLowerCase();
        const el = document.getElementById("content-area");
        
        // Search Students
        const studRes = this.data.students.filter(s => s.name.toLowerCase().includes(q) || s.chestNo.includes(q));
        // Search Comps
        const compRes = this.data.competitions.filter(c => c.name.toLowerCase().includes(q));
        
        el.innerHTML = `
            <h3>Search Results for "${q}"</h3>
            <div class="grid cols-2">
                <div class="card">
                    <h4>Students (${studRes.length})</h4>
                    ${studRes.map(s => `
                        <div class="row" style="justify-content:space-between; padding:10px 0; border-bottom:1px solid #eee">
                            <div><strong>${s.name}</strong> (#${s.chestNo})</div>
                            <button class="btn sm primary" onclick="App.viewStudentPrograms('${s.id}')">See Programs</button>
                        </div>
                    `).join('')}
                </div>
                <div class="card">
                    <h4>Competitions (${compRes.length})</h4>
                    ${compRes.map(c => `
                        <div class="row" style="justify-content:space-between; padding:10px 0; border-bottom:1px solid #eee">
                            <div>${c.name}</div>
                            <button class="btn sm primary" onclick="App.openScoreSheet('${c.id}')">Judge Panel</button>
                        </div>
                    `).join('')}
                </div>
            </div>
        `;
    },
    viewStudentPrograms(sid) {
        const s = this.data.students.find(x=>x.id===sid);
        const enrollments = this.data.entries.filter(e => e.memberStudentIds.includes(sid));
        
        let html = `<h3>Programs for ${s.name} (#${s.chestNo})</h3><ul>`;
        enrollments.forEach(e => {
            const c = this.data.competitions.find(x=>x.id===e.competitionId);
            const r = this.data.results.find(x=>x.entryId===e.id);
            html += `<li><strong>${c.name}</strong> - ${r ? (r.rankLabel ? `Rank: ${r.rankLabel}` : 'Participated') : 'Enrolled'}</li>`;
        });
        html += `</ul>`;
        this.openModal(html);
    },

    /* --- TEAM MODULES --- */

    renderTeamStudents(el) {
        const myS = this.data.students.filter(s=>s.teamId===this.state.user.id);
        el.innerHTML = `
            <div class="card">
                <h3>Register Student</h3>
                <form class="row" onsubmit="App.addStudent(event)">
                    <input class="input" id="s-n" placeholder="Full Name" required style="flex:2">
                    <input class="input" id="s-cn" placeholder="Chest No" required style="flex:1">
                    <select class="input" id="s-c" style="flex:1">${this.data.categories.filter(c=>c!=='GENERAL').map(c=>`<option>${c}</option>`).join('')}</select>
                    <button class="btn primary">Add</button>
                </form>
            </div>
            <div class="card">
                <h3>My Students (${myS.length})</h3>
                <table>
                    <thead><tr><th>Chest</th><th>Name</th><th>Category</th><th>Programs</th><th>Action</th></tr></thead>
                    <tbody>
                        ${myS.map(s => {
                            const count = this.data.entries.filter(e=>e.memberStudentIds.includes(s.id)).length;
                            return `<tr>
                                <td><span class="tag gold">#${s.chestNo}</span></td>
                                <td>${s.name}</td>
                                <td><span class="tag blue">${s.category}</span></td>
                                <td>${count}</td>
                                <td><button class="btn sm danger" onclick="App.delStudent('${s.id}')">&times;</button></td>
                            </tr>`
                        }).join('')}
                    </tbody>
                </table>
            </div>
        `;
    },
    addStudent(e) {
        e.preventDefault();
        const chest = document.getElementById("s-cn").value;
        if(this.data.students.find(s=>s.chestNo===chest)) return alert("Chest No exists!");
        this.data.students.push({
            id:Date.now().toString(), teamId:this.state.user.id,
            name:document.getElementById("s-n").value,
            chestNo:chest,
            category:document.getElementById("s-c").value
        });
        Store.save(this.data); this.renderTab();
    },
    delStudent(id) {
        if(confirm("Remove student?")) {
            this.data.students = this.data.students.filter(s=>s.id!==id);
            this.data.entries = this.data.entries.filter(e=>!e.memberStudentIds.includes(id));
            Store.save(this.data); this.renderTab();
        }
    },

    /* Enrollment with Limits */
    renderTeamEnroll(el) {
        const myS = this.data.students.filter(s=>s.teamId===this.state.user.id);
        el.innerHTML = `
            <div class="grid cols-3">
            ${this.data.competitions.map(c => {
                const enrolled = this.data.entries.filter(e=>e.competitionId===c.id && e.teamId===this.state.user.id);
                // Filter eligible students: Category Match OR General
                const eligible = myS.filter(s => c.category==='GENERAL' || s.category===c.category);
                return `
                    <div class="card">
                        <div class="row" style="justify-content:space-between">
                            <strong>${c.name}</strong>
                            <span class="tag ${c.category==='GENERAL'?'gray':'blue'}">${c.category}</span>
                        </div>
                        <div style="margin:15px 0; min-height:30px">
                            ${enrolled.map(e => {
                                const st = this.data.students.find(x=>x.id===e.memberStudentIds[0]);
                                return `<span class="tag green" style="margin:2px">${st.name} <span onclick="App.unenroll('${e.id}')" style="cursor:pointer">&times;</span></span>`
                            }).join('')}
                        </div>
                        <form class="row" onsubmit="App.enroll(event, '${c.id}')">
                            <select class="input sm" id="enr-${c.id}">
                                ${eligible.map(s => `<option value="${s.id}">${s.name}</option>`).join('')}
                            </select>
                            <button class="btn sm primary">Enroll</button>
                        </form>
                    </div>
                `;
            }).join('')}
            </div>
        `;
    },
    enroll(e, cid) {
        e.preventDefault();
        const sid = document.getElementById(`enr-${cid}`).value;
        const comp = this.data.competitions.find(c=>c.id===cid);
        
        if(!sid) return;
        
        // check duplicate
        if(this.data.entries.find(e=>e.competitionId===cid && e.memberStudentIds.includes(sid))) return alert("Already enrolled!");
        
        // check limit (Skip if General)
        if(comp.category !== 'GENERAL') {
            const limit = this.data.admin.maxEventsPerStudent || 5;
            // Count non-general entries for this student
            const currentEntries = this.data.entries.filter(entry => {
                if(!entry.memberStudentIds.includes(sid)) return false;
                const c = this.data.competitions.find(x=>x.id===entry.competitionId);
                return c && c.category !== 'GENERAL';
            }).length;
            
            if(currentEntries >= limit) return alert(`Limit Reached! Student can only join ${limit} individual programs.`);
        }

        this.data.entries.push({ id:Date.now().toString(), competitionId:cid, teamId:this.state.user.id, memberStudentIds:[sid] });
        Store.save(this.data); this.renderTab();
    },
    unenroll(eid) {
        this.data.entries = this.data.entries.filter(e=>e.id!==eid);
        Store.save(this.data); this.renderTab();
    },

    /* Helpers */
    openModal(content) {
        document.getElementById("modal-content").innerHTML = content;
        document.getElementById("modal-overlay").style.display = "flex";
    },
    closeModal() {
        document.getElementById("modal-overlay").style.display = "none";
    },

    /* Admin Reports (Simplified) */
    renderStudentRep(el) {
        el.innerHTML = `<button class="btn primary" onclick="window.print()">Print Report</button><div class="card" style="margin-top:20px">
            ${this.data.teams.map(t => `<h3>${t.name}</h3><ul>${this.data.students.filter(s=>s.teamId===t.id).map(s=>`<li>${s.name} (${s.category}) - #${s.chestNo}</li>`).join('')}</ul>`).join('')}
        </div>`;
    },
    renderEntryRep(el) {
        el.innerHTML = `<button class="btn primary" onclick="window.print()">Print Report</button><div class="card" style="margin-top:20px">
            ${this.data.competitions.map(c => `<h3>${c.name}</h3><ul>${this.data.entries.filter(e=>e.competitionId===c.id).map(e=>{
                const s=this.data.students.find(x=>x.id===e.memberStudentIds[0]); return `<li>${s.name} (#${s.chestNo})</li>`;
            }).join('')}</ul>`).join('')}
        </div>`;
    },
    
    /* Chest Card (Minimal implementation) */
    renderChest(el) {
        el.innerHTML = `
            <div class="row"><button class="btn primary" onclick="App.printChest()">Print All Cards</button></div>
            <p>Preview first 5 students:</p>
            <div class="grid cols-3" id="cc-prev"></div>
        `;
        setTimeout(() => this.renderChestPreview(), 100);
    },
    renderChestPreview() {
        const box = document.getElementById("cc-prev");
        const cfg = this.data.chestConfig;
        box.innerHTML = this.data.students.slice(0,5).map(s => {
            const t = this.data.teams.find(x=>x.id===s.teamId);
            return `
                <div style="position:relative; width:${cfg.widthCm * 25}px; height:${cfg.heightCm * 25}px; background:${cfg.bgColor}; border:1px solid #ccc; margin:10px; overflow:hidden">
                    <div style="position:absolute; top:${cfg.elements.fest.y}%; left:${cfg.elements.fest.x}%; transform:translate(-50%,-50%); font-weight:bold; font-size:14px">${cfg.elements.fest.text}</div>
                    <div style="position:absolute; top:${cfg.elements.name.y}%; left:${cfg.elements.name.x}%; transform:translate(-50%,-50%); font-weight:bold;">${s.name}</div>
                    <div style="position:absolute; top:${cfg.elements.chest.y}%; left:${cfg.elements.chest.x}%; transform:translate(-50%,-50%); font-weight:bold; font-size:24px; color:${cfg.elements.chest.color}">${s.chestNo}</div>
                    <div style="position:absolute; top:${cfg.elements.team.y}%; left:${cfg.elements.team.x}%; transform:translate(-50%,-50%); color:#666; font-size:10px">${t.name}</div>
                </div>
            `;
        }).join('');
    },
    printChest() {
        const p = document.getElementById("print-area");
        const cfg = this.data.chestConfig;
        const style = `<style>@media print { .cc { border:1px solid #eee; page-break-inside:avoid; display:inline-block; margin:0.5cm; width:${cfg.widthCm}cm; height:${cfg.heightCm}cm; position:relative; } }</style>`;
        
        const cards = this.data.students.map(s => {
             const t = this.data.teams.find(x=>x.id===s.teamId);
             return `<div class="cc">
                <div style="position:absolute; top:${cfg.elements.fest.y}%; left:${cfg.elements.fest.x}%; transform:translate(-50%,-50%); font-weight:bold; font-size:12pt">${cfg.elements.fest.text}</div>
                <div style="position:absolute; top:${cfg.elements.name.y}%; left:${cfg.elements.name.x}%; transform:translate(-50%,-50%); font-weight:bold; font-size:10pt">${s.name}</div>
                <div style="position:absolute; top:${cfg.elements.chest.y}%; left:${cfg.elements.chest.x}%; transform:translate(-50%,-50%); font-weight:bold; font-size:24pt; color:${cfg.elements.chest.color}">${s.chestNo}</div>
                <div style="position:absolute; top:${cfg.elements.team.y}%; left:${cfg.elements.team.x}%; transform:translate(-50%,-50%); font-size:8pt">${t.name}</div>
                <div id="qr-${s.id}" style="position:absolute; top:${cfg.elements.qr.y}%; left:${cfg.elements.qr.x}%; transform:translate(-50%,-50%);"></div>
             </div>`;
        }).join('');
        
        p.innerHTML = style + cards;
        // Generate QRs
        this.data.students.forEach(s => {
            new QRCode(document.getElementById(`qr-${s.id}`), {text:`ALIF-${s.chestNo}`, width:60, height:60});
        });
        window.print();
    }
};

App.init();
</script>
</body>
</html>
