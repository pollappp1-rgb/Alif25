
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
    key: "alif_median_v9_final",
    defaults: () => ({
        meta: { version: 9 },
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
                logo: { x: 50, y: 20, size: 40, visible: false }
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

    /* --- 1. Setup --- */
    renderSetup(el) {
        el.innerHTML = `
            <div class="grid cols-2">
                <div class="card">
                    <h3>Site Branding</h3>
                    <div class="row" style="margin-bottom:15px">
                        ${this.data.logo ? `<img src="${this.data.logo}" style="width:50px;height:50px;border-radius:8px">` : ''}
                        <div>
                            <p style="font-size:12px;margin:0">Upload Site Logo</p>
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
                            <div><button class="btn sm" onclick="App.editTeam('${t.id}')">Edit</button><button class="btn sm danger" onclick="App.deleteTeam('${t.id}')">Del</button></div>
                        </div>`).join('')}
                    </div>
                    <button class="btn primary sm" onclick="App.addTeam()">+ Add Team</button>
                </div>
                <div class="card">
                    <h3>Backup / Reset</h3>
                    <div class="row"><button class="btn" onclick="App.downloadData()">Backup JSON</button><label class="btn primary">Restore JSON <input type="file" hidden onchange="App.uploadData(this)"></label></div>
                    <button class
