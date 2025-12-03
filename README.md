
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>ALIF – Campus Literary Arts Fest</title>
<!-- Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<!-- Libraries -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<script src="https://unpkg.com/html5-qrcode" type="text/javascript"></script>

<style>
    /* --- Median UI Theme (Light/Dark) --- */
    :root {
        --bg-body: #f8f9fa; --bg-surface: #ffffff; --bg-sidebar: #ffffff;
        --border: #e2e8f0; --text-main: #0f172a; --text-muted: #64748b;
        --primary: #4f46e5; --primary-soft: #eef2ff;
        --danger: #ef4444; --success: #10b981; --gold: #f59e0b;
        --shadow: 0 1px 3px 0 rgba(0,0,0,0.1), 0 1px 2px -1px rgba(0,0,0,0.1);
        --radius: 12px; --font: 'Plus Jakarta Sans', sans-serif;
    }
    [data-theme="dark"] {
        --bg-body: #0f172a; --bg-surface: #1e293b; --bg-sidebar: #1e293b;
        --border: #334155; --text-main: #f8fafc; --text-muted: #94a3b8;
        --primary: #6366f1; --primary-soft: #312e81; --shadow: 0 4px 6px -1px rgba(0,0,0,0.5);
    }

    * { box-sizing: border-box; outline: none; -webkit-tap-highlight-color: transparent; }
    body { margin: 0; background: var(--bg-body); color: var(--text-main); font-family: var(--font); height: 100vh; display: flex; overflow: hidden; transition: background 0.3s; }
    
    /* Layout */
    .app-wrap { display: flex; width: 100%; height: 100%; }
    .sidebar { width: 260px; background: var(--bg-sidebar); border-right: 1px solid var(--border); display: flex; flex-direction: column; padding: 1.5rem; flex-shrink: 0; }
    .main { flex: 1; display: flex; flex-direction: column; background: var(--bg-body); overflow: hidden; position: relative; }
    .top-bar { height: 64px; background: var(--bg-surface); border-bottom: 1px solid var(--border); display: flex; align-items: center; justify-content: space-between; padding: 0 2rem; z-index: 10; }
    .content { flex: 1; overflow-y: auto; padding: 2rem; max-width: 1400px; margin: 0 auto; width: 100%; }

    /* Components */
    .card { background: var(--bg-surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 1.5rem; margin-bottom: 1.5rem; box-shadow: var(--shadow); }
    .grid { display: grid; gap: 1.5rem; } .cols-2 { grid-template-columns: 1fr 1fr; } .cols-3 { grid-template-columns: repeat(3, 1fr); }
    .row { display: flex; align-items: center; gap: 0.75rem; flex-wrap: wrap; }
    
    .btn { display: inline-flex; align-items: center; justify-content: center; padding: 0.5rem 1rem; border-radius: 8px; font-weight: 600; cursor: pointer; border: 1px solid var(--border); background: var(--bg-surface); color: var(--text-muted); transition: 0.2s; gap: 6px; font-size: 0.875rem; }
    .btn:hover { background: var(--bg-body); color: var(--text-main); }
    .btn.primary { background: var(--primary); color: #fff; border-color: var(--primary); }
    .btn.danger { background: #fee2e2; color: var(--danger); border-color: #fecaca; } [data-theme="dark"] .btn.danger { background: #451a1a; border-color: #7f1d1d; }
    .btn.sm { padding: 0.25rem 0.75rem; font-size: 0.75rem; }

    .input, select { width: 100%; padding: 0.6rem; border-radius: 8px; border: 1px solid var(--border); background: var(--bg-surface); color: var(--text-main); font-family: var(--font); }
    .tag { padding: 2px 8px; border-radius: 4px; font-size: 0.7rem; font-weight: 700; text-transform: uppercase; }
    .tag.blue { background: var(--primary-soft); color: var(--primary); }
    .tag.gold { background: #fef3c7; color: #b45309; } [data-theme="dark"] .tag.gold { background: #451a03; color: #fbbf24; }
    .tag.green { background: #dcfce7; color: #15803d; } [data-theme="dark"] .tag.green { background: #052e16; color: #4ade80; }

    table { width: 100%; border-collapse: collapse; font-size: 0.9rem; }
    th { text-align: left; padding: 0.75rem; border-bottom: 1px solid var(--border); color: var(--text-muted); font-size: 0.75rem; text-transform: uppercase; }
    td { padding: 0.75rem; border-bottom: 1px solid var(--border); color: var(--text-main); }

    /* Nav & Modal */
    .nav-item { padding: 0.75rem; border-radius: 8px; color: var(--text-muted); cursor: pointer; font-weight: 500; margin-bottom: 4px; transition: 0.2s; }
    .nav-item:hover { background: var(--bg-body); color: var(--text-main); } .nav-item.active { background: var(--primary-soft); color: var(--primary); }
    .modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.5); backdrop-filter: blur(2px); z-index: 100; display: none; place-items: center; }
    .modal-box { background: var(--bg-surface); width: 750px; max-width: 90%; max-height: 90vh; overflow-y: auto; padding: 2rem; border-radius: var(--radius); box-shadow: var(--shadow); }

    /* Utils */
    .progress-bar { width: 100%; height: 6px; background: var(--bg-body); border-radius: 3px; overflow: hidden; margin-top: 5px; border: 1px solid var(--border); }
    .progress-fill { height: 100%; background: var(--primary); width: 0%; } .progress-fill.full { background: var(--danger); }
    .range-wrap { display: flex; align-items: center; gap: 10px; font-size: 12px; margin-bottom: 5px; } .range-wrap input[type=range]{flex:1}
    .color-inp { width: 30px; height: 30px; padding: 0; border: none; border-radius: 50%; cursor: pointer; }

    @media print {
        .sidebar, .top-bar, .btn, .input, select, .no-print { display: none !important; }
        .app-wrap { display: block; } .content { padding: 0; overflow: visible; } .card { border: none; box-shadow: none; padding: 0; }
        body, .main, .card { background: #fff !important; color: #000 !important; }
        .print-section { page-break-inside: avoid; }
    }
</style>
</head>
<body>

<div id="app"></div>
<div id="print-area"></div>
<div id="modal-overlay" class="modal-overlay" onclick="if(event.target===this) App.closeModal()"><div id="modal-content" class="modal-box"></div></div>

<script>
"use strict";

const Store = {
    key: "alif_fest_v20_final",
    defaults: () => ({
        meta: { version: 20 },
        theme: 'light',
        admin: { username: 'admin', password: '123' },
        teams: [ { id: 't1', name: 'ZARQAN', password: '123' }, { id: 't2', name: 'ASQALAN', password: '123' }, { id: 't3', name: 'ASBAHAN', password: '123' } ],
        categories: ['SUB JUNIOR', 'JUNIOR', 'SENIOR', 'GENERAL'],
        competitions: [], // {id, name, category, isStage, type:'INDIVIDUAL'|'GROUP', teamLimit: 2}
        students: [], entries: [], results: [], // result: {..., rankLabel, grade, pointsAwarded}
        logo: null,
        chestConfig: { widthCm: 9, heightCm: 13, radius: 0, bgColor: "#ffffff", logo: null, elements: { qr: { x: 50, y: 35, size: 80, color: "#000000", visible: true }, name: { x: 50, y: 65, size: 16, color: "#000000", bold: true, visible: true }, chest: { x: 50, y: 78, size: 28, color: "#4f46e5", bold: true, visible: true }, team: { x: 50, y: 90, size: 12, color: "#64748b", bold: false, visible: true }, fest: { x: 50, y: 10, size: 18, color: "#1e293b", bold: true, text:"ALIF Fest", visible: true }, logo: { x: 50, y: 20, size: 40, visible: false } } }
    }),
    load() { const d = localStorage.getItem(this.key); return d ? JSON.parse(d) : this.defaults(); },
    save(data) { localStorage.setItem(this.key, JSON.stringify(data)); }
};

const App = {
    data: Store.load(),
    state: { user: null, role: null, activeTab: 'setup', scanner: null },

    init() {
        if(!localStorage.getItem(Store.key)) Store.save(this.data);
        this.applyTheme();
        this.renderLogin();
    },

    toggleTheme() { this.data.theme = this.data.theme === 'light' ? 'dark' : 'light'; Store.save(this.data); this.applyTheme(); },
    applyTheme() { document.documentElement.setAttribute('data-theme', this.data.theme); },
    
    renderLogin() {
        const logoHtml = this.data.logo ? `<img src="${this.data.logo}" style="width:60px;height:60px;border-radius:12px;margin-bottom:15px">` : `<div style="width:50px;height:50px;background:var(--primary);color:#fff;border-radius:10px;display:grid;place-items:center;font-weight:bold;font-size:24px;margin:0 auto 15px">A</div>`;
        document.getElementById("app").innerHTML = `
            <div style="display:flex;align-items:center;justify-content:center;height:100vh;background:var(--bg-body)">
                <div class="card" style="width:380px;text-align:center">
                    ${logoHtml}<h1>ALIF Fest</h1><p>Campus Literary Arts Festival</p>
                    <div class="grid cols-2" style="margin:20px 0"><button class="btn ${this.state.role!=='team'?'primary':''}" onclick="document.getElementById('af').style.display='block';document.getElementById('tf').style.display='none'">Crew</button><button class="btn ${this.state.role==='team'?'primary':''}" onclick="document.getElementById('af').style.display='none';document.getElementById('tf').style.display='block'">Team</button></div>
                    <form id="af" onsubmit="App.loginAdmin(event)"><input class="input" id="u" placeholder="User" style="margin-bottom:10px"><input class="input" type="password" id="p" placeholder="Pass" style="margin-bottom:20px"><button class="btn primary" style="width:100%">Login</button></form>
                    <form id="tf" style="display:none" onsubmit="App.loginTeam(event)"><select class="input" id="ts" style="margin-bottom:10px"><option value="">Team</option>${this.data.teams.map(t=>`<option value="${t.id}">${t.name}</option>`).join('')}</select><input class="input" type="password" id="tp" placeholder="Pass" style="margin-bottom:20px"><button class="btn primary" style="width:100%">Login</button></form>
                </div>
            </div>`;
    },
    loginAdmin(e) { e.preventDefault(); if(document.getElementById('u').value===this.data.admin.username && document.getElementById('p').value===this.data.admin.password) { this.state.role='admin'; this.state.activeTab='setup'; this.loadLayout(); } else alert("Invalid"); },
    loginTeam(e) { e.preventDefault(); const t=this.data.teams.find(x=>x.id===document.getElementById('ts').value); if(t&&t.password===document.getElementById('tp').value) { this.state.role='team'; this.state.user=t; this.state.activeTab='students'; this.loadLayout(); } else alert("Invalid"); },
    logout() { this.state.role=null; this.state.user=null; this.renderLogin(); },

    loadLayout() {
        const tabs = this.state.role === 'admin' 
            ? [ {id:'setup',l:'Setup'}, {id:'comps',l:'Competitions'}, {id:'judge',l:'Judge Panel'}, {id:'scores',l:'Scoreboard'}, {id:'student_pts',l:'Student Points'}, {id:'team_progs',l:'Team Programs'}, {id:'chest',l:'Chest Cards'} ]
            : [ {id:'students',l:'My Students'}, {id:'enroll',l:'Enrollment'}, {id:'settings',l:'Settings'} ];
        
        document.getElementById("app").innerHTML = `
            <div class="app-wrap">
                <aside class="sidebar">
                    <div style="display:flex;gap:10px;align-items:center;margin-bottom:30px">${this.data.logo ? `<img src="${this.data.logo}" style="width:32px;height:32px;border-radius:6px">` : `<div style="width:32px;height:32px;background:var(--primary);border-radius:6px"></div>`}<div><h3 style="margin:0">ALIF Fest</h3><span style="font-size:0.7rem;color:var(--text-muted)">${this.state.role}</span></div></div>
                    <div class="nav-links">${tabs.map(t=>`<div class="nav-item ${this.state.activeTab===t.id?'active':''}" onclick="App.switchTab('${t.id}')">${t.l}</div>`).join('')}</div>
                    <div class="nav-item" onclick="App.logout()" style="margin-top:auto">🚪 Logout</div>
                </aside>
                <main class="main">
                    <header class="top-bar"><h2>${tabs.find(t=>t.id===this.state.activeTab).l}</h2><div class="row"><button class="btn sm" onclick="App.toggleTheme()">${this.data.theme==='light'?'🌙':'☀️'}</button>${this.state.role==='admin' ? `<button class="btn sm primary" onclick="App.openGlobalScanner()">📷 Scan</button><input class="input sm" style="width:250px" placeholder="Search Student/Chest/Comp..." oninput="App.globalSearch(this.value)">` : ''}</div></header>
                    <div class="content" id="content"></div>
                </main>
            </div>`;
        this.renderTab();
    },
    switchTab(id) { this.state.activeTab = id; this.loadLayout(); },

    renderTab() {
        const el = document.getElementById("content"); const t = this.state.activeTab;
        if(this.state.role === 'admin') {
            if(t==='setup') this.renderSetup(el);
            if(t==='comps') this.renderComps(el);
            if(t==='judge') this.renderJudge(el);
            if(t==='scores') this.renderScores(el);
            if(t==='student_pts') this.renderStudentPoints(el);
            if(t==='team_progs') this.renderTeamProgs(el);
            if(t==='chest') this.renderChest(el);
        } else {
            if(t==='students') this.renderTeamStudents(el);
            if(t==='enroll') this.renderTeamEnroll(el);
            if(t==='settings') el.innerHTML = `<div class="card">Contact Admin to change password.</div>`;
        }
    },

    /* --- ADMIN MODULES --- */
    renderSetup(el) {
        el.innerHTML = `
            <div class="grid cols-2">
                <div class="card"><h3>Site Branding</h3><div class="row" style="margin-top:10px"><input type="file" onchange="App.upLogo(this)">${this.data.logo?`<button class="btn sm danger" onclick="App.rmLogo()">Remove</button>`:''}</div></div>
                <div class="card"><h3>Admin Credentials</h3><form class="row" onsubmit="App.saveAdm(event)"><input class="input" id="au" value="${this.data.admin.username}"><input class="input" id="ap" value="${this.data.admin.password}"><button class="btn primary">Save</button></form></div>
                <div class="card"><h3>Teams</h3><div style="max-height:150px;overflow-y:auto;margin-bottom:10px">${this.data.teams.map(t=>`<div class="row" style="justify-content:space-between;padding:5px;border-bottom:1px solid var(--border)"><b>${t.name}</b> <div><button class="btn sm" onclick="App.editTeam('${t.id}')">Edit</button> <button class="btn sm danger" onclick="App.delTeam('${t.id}')">Del</button></div></div>`).join('')}</div><button class="btn primary sm" onclick="App.addTeam()">+ Add Team</button></div>
                <div class="card"><h3>Data Management</h3><div class="row"><button class="btn" onclick="App.dlData()">Backup</button><label class="btn primary">Restore <input type="file" hidden onchange="App.ulData(this)"></label><button class="btn danger" onclick="App.wipe()">Wipe</button></div></div>
            </div>`;
    },
    upLogo(i){const r=new FileReader();r.onload=e=>{this.data.logo=e.target.result;Store.save(this.data);this.loadLayout()};if(i.files[0])r.readAsDataURL(i.files[0])},
    rmLogo(){this.data.logo=null;Store.save(this.data);this.loadLayout()},
    saveAdm(e){e.preventDefault();this.data.admin.username=document.getElementById('au').value;this.data.admin.password=document.getElementById('ap').value;Store.save(this.data);alert('Saved')},
    addTeam(){const n=prompt("Name");const p=prompt("Pass");if(n){this.data.teams.push({id:'t'+Date.now(),name:n.toUpperCase(),password:p||'123'});Store.save(this.data);this.renderTab()}},
    editTeam(id){const t=this.data.teams.find(x=>x.id===id);const n=prompt("Name",t.name);const p=prompt("Pass",t.password);if(n){t.name=n;t.password=p;Store.save(this.data);this.renderTab()}},
    delTeam(id){if(confirm("Del?")){this.data.teams=this.data.teams.filter(t=>t.id!==id);Store.save(this.data);this.renderTab()}},
    dlData(){const a=document.createElement('a');a.href=URL.createObjectURL(new Blob([JSON.stringify(this.data)],{type:'application/json'}));a.download='ALIF.json';a.click()},
    ulData(i){const r=new FileReader();r.onload=e=>{this.data=JSON.parse(e.target.result);Store.save(this.data);location.reload()};r.readAsText(i.files[0])},
    wipe(){if(confirm("Wipe Data?")){this.data.students=[];this.data.entries=[];this.data.results=[];Store.save(this.data);location.reload()}},

    /* COMPETITIONS */
    renderComps(el) {
        el.innerHTML = `
            <div class="card"><h3>Create Competition</h3>
            <form class="row" onsubmit="App.addComp(event)">
                <input class="input" id="cn" placeholder="Name" required style="flex:2">
                <select class="input" id="cc" style="flex:1">${this.data.categories.map(c=>`<option>${c}</option>`).join('')}</select>
                <select class="input" id="ct" style="flex:1"><option value="INDIVIDUAL">Individual</option><option value="GROUP">Group</option></select>
                <input class="input" type="number" id="ctl" placeholder="Team Limit" style="width:100px" value="2" required title="Limit per Team">
                <label><input type="checkbox" id="cs"> Stage</label>
                <button class="btn primary">Add</button>
            </form></div>
            <div class="card"><table><thead><tr><th>Name</th><th>Cat</th><th>Type</th><th>Entries</th><th>Action</th></tr></thead><tbody>${this.data.competitions.map(c => {
                const cnt = this.data.entries.filter(e=>e.competitionId===c.id).length;
                return `<tr><td>${c.name}</td><td><span class="tag blue">${c.category}</span></td><td>${c.isStage?'Stage':'Off'} / ${c.type}</td>
                <td><div style="font-size:11px">${cnt} Enrolled (Max ${c.teamLimit}/Team)</div></td>
                <td><button class="btn sm danger" onclick="App.delComp('${c.id}')">Del</button></td></tr>`;
            }).join('')}</tbody></table></div>`;
    },
    addComp(e){
        e.preventDefault();
        this.data.competitions.push({
            id:Date.now().toString(),
            name:document.getElementById('cn').value,
            category:document.getElementById('cc').value,
            type:document.getElementById('ct').value,
            teamLimit:Number(document.getElementById('ctl').value),
            isStage:document.getElementById('cs').checked
        });
        Store.save(this.data); this.renderTab();
    },
    delComp(id){if(confirm("Del?")){this.data.competitions=this.data.competitions.filter(c=>c.id!==id);this.data.entries=this.data.entries.filter(e=>e.competitionId!==id);Store.save(this.data);this.renderTab()}},

    /* JUDGE PANEL */
    renderJudge(el) { el.innerHTML=`<div class="grid cols-3">${this.data.competitions.map(c=>`<div class="card" style="cursor:pointer" onclick="App.openJudge('${c.id}')"><h3>${c.name}</h3><span class="tag blue">${c.category}</span></div>`).join('')}</div>`; },
    openJudge(cid) {
        const c = this.data.competitions.find(x=>x.id===cid);
        const ents = this.data.entries.filter(e=>e.competitionId===cid);
        
        let rows = '';
        if(c.type === 'GROUP') {
            const teamsInvolved = [...new Set(ents.map(e=>e.teamId))];
            rows = teamsInvolved.map(tid => {
                const t = this.data.teams.find(x=>x.id===tid);
                const firstEnt = ents.find(e=>e.teamId===tid);
                const r = this.data.results.find(x=>x.entryId===firstEnt.id) || {};
                return `<tr>
                    <td><span class="tag gold">GROUP</span></td>
                    <td><input class="input sm" style="width:50px" value="${r.codeLetter||''}" id="cl-${tid}"></td>
                    <td><strong>${t.name}</strong> (${ents.filter(e=>e.teamId===tid).length} members)</td>
                    <td><input type="checkbox" id="att-${tid}" ${r.attendance?'checked':''}></td>
                    <td><input class="input sm" style="width:50px" id="rnk-${tid}" value="${r.rankLabel||''}" placeholder="1,2,3" oninput="App.autoCalc('${tid}','GROUP')"></td>
                    
