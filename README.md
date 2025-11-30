
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
    .modal-box { background: var(--bg-surface); width: 600px; max-width: 90%; max-height: 90vh; overflow-y: auto; padding: 2rem; border-radius: var(--radius); box-shadow: var(--shadow); }

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
    key: "alif_fest_v15_final",
    defaults: () => ({
        meta: { version: 15 },
        theme: 'light',
        admin: { username: 'admin', password: '123' },
        teams: [ { id: 't1', name: 'ZARQAN', password: '123' }, { id: 't2', name: 'ASQALAN', password: '123' }, { id: 't3', name: 'ASBAHAN', password: '123' } ],
        categories: ['SUB JUNIOR', 'JUNIOR', 'SENIOR', 'GENERAL'],
        competitions: [], // {id, name, category, isStage, type:'INDIVIDUAL'|'GROUP', teamLimit: 2}
        students: [], entries: [], results: [], 
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
                    <td><input class="input sm" style="width:50px" id="rnk-${tid}" value="${r.rankLabel||''}"></td>
                    <td><input class="input sm" type="number" style="width:50px" id="pts-${tid}" value="${r.pointsAwarded||0}"></td>
                    <td><button class="btn sm primary" onclick="App.svGroupRes('${tid}','${cid}')">Save</button></td>
                </tr>`;
            }).join('');
        } else {
            rows = ents.map(e=>{
                const s = this.data.students.find(x=>x.id===e.memberStudentIds[0]);
                const r = this.data.results.find(x=>x.entryId===e.id)||{};
                return `<tr>
                    <td><span class="tag gold">#${s.chestNo}</span></td>
                    <td><input class="input sm" style="width:50px" value="${r.codeLetter||''}" id="cl-${e.id}"></td>
                    <td>${s.name}</td>
                    <td><input type="checkbox" id="att-${e.id}" ${r.attendance?'checked':''}></td>
                    <td><input class="input sm" style="width:50px" id="rnk-${e.id}" value="${r.rankLabel||''}"></td>
                    <td><input class="input sm" type="number" style="width:50px" id="pts-${e.id}" value="${r.pointsAwarded||0}"></td>
                    <td><button class="btn sm primary" onclick="App.svRes('${e.id}','${cid}')">Save</button></td>
                </tr>`;
            }).join('');
        }

        const modal = document.getElementById("content");
        modal.innerHTML = `
            <div class="row" style="margin-bottom:20px"><button class="btn" onclick="App.switchTab('judge')">Back</button><h2>${c.name}</h2><div style="flex:1"></div><button class="btn primary" onclick="App.scanAtt('${cid}')">📷 Scan Attendance</button><button class="btn" onclick="App.autoCode('${cid}')">⚡ Codes</button></div>
            <div class="card"><table><thead><tr><th>ID</th><th>Code</th><th>Participant</th><th>Att</th><th>Rank</th><th>Pts</th><th>Save</th></tr></thead>
            <tbody>${rows}</tbody></table></div>`;
    },
    svRes(eid,cid){
        const att=document.getElementById(`att-${eid}`).checked; const rnk=document.getElementById(`rnk-${eid}`).value; const pts=Number(document.getElementById(`pts-${eid}`).value); const cl=document.getElementById(`cl-${eid}`).value.toUpperCase();
        this.data.results=this.data.results.filter(r=>r.entryId!==eid); this.data.results.push({id:Date.now().toString(),competitionId:cid,entryId:eid,rankLabel:rnk,pointsAwarded:pts,attendance:att,codeLetter:cl}); Store.save(this.data);
    },
    svGroupRes(tid, cid){
        const teamEnts = this.data.entries.filter(e => e.competitionId === cid && e.teamId === tid);
        const att = document.getElementById(`att-${tid}`).checked; const rnk = document.getElementById(`rnk-${tid}`).value; const pts = Number(document.getElementById(`pts-${tid}`).value); const cl = document.getElementById(`cl-${tid}`).value.toUpperCase();
        teamEnts.forEach(ent => {
            this.data.results = this.data.results.filter(r => r.entryId !== ent.id);
            this.data.results.push({ id: Date.now().toString()+Math.random(), competitionId: cid, entryId: ent.id, rankLabel: rnk, pointsAwarded: pts, attendance: att, codeLetter: cl });
        });
        Store.save(this.data); alert("Group Result Saved!");
    },
    autoCode(cid){ if(confirm("Generate?")){const es=this.data.entries.filter(e=>e.competitionId===cid); const cs="ABCDEFGHIJKLMNOPQRSTUVWXYZ".split('').sort(()=>0.5-Math.random()); es.forEach((e,i)=>{let r=this.data.results.find(x=>x.entryId===e.id); if(r)r.codeLetter=cs[i%26]; else this.data.results.push({id:Date.now(),competitionId:cid,entryId:e.id,rankLabel:'',pointsAwarded:0,attendance:false,codeLetter:cs[i%26]})}); Store.save(this.data); this.openJudge(cid); } },

    /* Scores: Team Points & Toppers */
    renderScores(el) {
        const d = this.calcScores(); const tops = this.getToppers();
        const topCard = (t, l) => { if(!l.length) return `<div class="card" style="padding:10px;text-align:center;font-size:12px;color:#999">${t}: -</div>`; const s=l[0]; return `<div class="card" style="border:1px solid var(--primary-soft);text-align:center;padding:10px"><div style="font-size:10px;text-transform:uppercase;color:var(--primary);font-weight:bold">${t}</div><div style="font-weight:bold;font-size:14px;margin:4px 0">${s.name}</div><div style="font-size:11px;color:#666">#${s.chest} | ${s.team}</div><div class="tag gold" style="margin-top:5px">${s[t.toLowerCase().includes('non')?'nst':'st']} Pts</div></div>`; };
        el.innerHTML = `
            <div class="row" style="justify-content:center;margin-bottom:20px">${d[0]?`<div class="card" style="text-align:center;border-top:5px solid gold;transform:scale(1.1)"><h1>${d[0].name}</h1><h2>${d[0].total} Pts</h2><div class="tag gold">CHAMPION</div></div>`:''}</div>
            <h3>🏆 Category Toppers</h3>
            <div class="grid cols-3" style="margin-bottom:20px">${Object.keys(tops).map(c => `<div style="display:flex;flex-direction:column;gap:10px"><h4 style="text-align:center">${c}</h4>${topCard('Stage',tops[c].st)}${topCard('Non-Stage',tops[c].nst)}</div>`).join('')}</div>
            <h3>📊 Team Standings</h3>
            <div class="card" style="overflow-x:auto"><table><thead><tr><th>Rank</th><th>Team</th><th>Total</th><th>Stage</th><th>Off-Stage</th>${this.data.categories.map(c=>`<th>${c}</th>`).join('')}</tr></thead>
            <tbody>${d.map((t,i)=>`<tr><td>#${i+1}</td><td>${t.name}</td><td><b>${t.total}</b></td><td>${t.st}</td><td>${t.nst}</td>${this.data.categories.map(c=>`<td>${t.cats[c]||0}</td>`).join('')}</tr>`).join('')}</tbody></table></div>`;
    },
    calcScores() {
        const ts={}; this.data.teams.forEach(t=>ts[t.id]={name:t.name,total:0,st:0,nst:0,cats:{}});
        this.data.results.forEach(r=>{
            const e=this.data.entries.find(x=>x.id===r.entryId); if(!e)return; const c=this.data.competitions.find(x=>x.id===e.competitionId);
            // Team Points: Add everything EXCEPT 3rd Grade. (Group & General OK for teams)
            if(c && r.rankLabel!=='3') { const p=r.pointsAwarded||0; ts[e.teamId].total+=p; if(c.isStage)ts[e.teamId].st+=p; else ts[e.teamId].nst+=p; if(!ts[e.teamId].cats[c.category])ts[e.teamId].cats[c.category]=0; ts[e.teamId].cats[c.category]+=p; }
        }); return Object.values(ts).sort((a,b)=>b.total-a.total);
    },
    getToppers() {
        const map={}; this.data.categories.filter(c=>c!=='GENERAL').forEach(c=>map[c]={st:[],nst:[]}); const sPts={};
        this.data.results.forEach(r=>{
            const e=this.data.entries.find(x=>x.id===r.entryId); if(!e)return; const c=this.data.competitions.find(x=>x.id===e.competitionId);
            // Individual Points: NO General, NO Group. (3rd Grade OK for indiv)
            if(c && c.category!=='GENERAL' && c.type!=='GROUP') { 
                const sid=e.memberStudentIds[0]; 
                if(!sPts[sid]){const s=this.data.students.find(x=>x.id===sid);sPts[sid]={id:sid,st:0,nst:0,cat:s.category,name:s.name,chest:s.chestNo,team:this.data.teams.find(t=>t.id===s.teamId).name}}; 
                if(c.isStage)sPts[sid].st+=r.pointsAwarded||0; else sPts[sid].nst+=r.pointsAwarded||0; 
            }
        });
        Object.values(sPts).forEach(p=>{if(map[p.cat]){if(p.st>0)map[p.cat].st.push(p);if(p.nst>0)map[p.cat].nst.push(p)}});
        Object.keys(map).forEach(c=>{map[c].st.sort((a,b)=>b.st-a.st);map[c].nst.sort((a,b)=>b.nst-a.nst)}); return map;
    },

    /* Chest Card Designer */
    renderChest(el) {
        const cfg = this.data.chestConfig;
        el.innerHTML = `
            <div class="grid cols-2">
                <div class="card" style="max-height:85vh; overflow-y:auto"><h3>🎨 Designer</h3>
                    <div class="row"><label>Width(cm)<input class="input sm" type="number" value="${cfg.widthCm}" onchange="App.updChest('widthCm',this.value)"></label><label>Height(cm)<input class="input sm" type="number" value="${cfg.heightCm}" onchange="App.updChest('heightCm',this.value)"></label><label>Radius<input class="input sm" type="number" value="${cfg.radius}" onchange="App.updChest('radius',this.value)"></label><label>Bg<input type="color" class="color-inp" value="${cfg.bgColor}" onchange="App.updChest('bgColor',this.value)"></label></div>
                    <div style="margin:15px 0"><p>Chest Logo</p><input type="file" onchange="App.updChestLogo(this)">${cfg.logo?`<button class="btn sm danger" onclick="App.remChestLogo()">Rm</button>`:''}</div>
                    ${['fest','name','chest','team','qr','logo'].map(k=>`<div style="background:var(--bg-body);padding:10px;border-radius:8px;margin-bottom:10px"><div class="row" style="justify-content:space-between"><strong style="text-transform:capitalize">${k}</strong><label><input type="checkbox" ${cfg.elements[k].visible?'checked':''} onchange="App.updChest('elements.${k}.visible',this.checked)"> Show</label></div>${cfg.elements[k].visible?`<div class="range-wrap"><span>X</span><input type="range" min="0" max="100" value="${cfg.elements[k].x}" oninput="App.updChest('elements.${k}.x',this.value)"></div><div class="range-wrap"><span>Y</span><input type="range" min="0" max="100" value="${cfg.elements[k].y}" oninput="App.updChest('elements.${k}.y',this.value)"></div><div class="range-wrap"><span>Size</span><input type="range" min="5" max="150" value="${cfg.elements[k].size}" oninput="App.updChest('elements.${k}.size',this.value)"></div>${k!=='qr'&&k!=='logo'?`<div class="row"><label>Color <input type="color" class="color-inp" value="${cfg.elements[k].color}" onchange="App.updChest('elements.${k}.color',this.value)"></label><label><input type="checkbox" ${cfg.elements[k].bold?'checked':''} onchange="App.updChest('elements.${k}.bold',this.checked)"> Bold</label>${k==='fest'?`<input class="input sm" value="${cfg.elements[k].text}" oninput="App.updChest('elements.${k}.text',this.value)">`:''}</div>`:''} `:''}</div>`).join('')}
                </div>
                <div class="card" style="display:flex;flex-direction:column;align-items:center;justify-content:center;background:var(--bg-body)"><div id="cc-prev"></div><button class="btn primary" style="margin-top:20px" onclick="App.printChest()">🖨️ Print All</button></div>
            </div>`; setTimeout(()=>this.renderChestPreview(),100);
    },
    updChest(p,v){let o=this.data.chestConfig;const k=p.split('.');for(let i=0;i<k.length-1;i++)o=o[k[i]];o[k[k.length-1]]=(p.includes('visible')||p.includes('bold'))?v:(isNaN(v)||p.includes('color')||p.includes('text')?v:Number(v));Store.save(this.data);this.renderChestPreview()},
    updChestLogo(i){const r=new FileReader();r.onload=e=>{this.data.chestConfig.logo=e.target.result;Store.save(this.data);this.renderChest(document.getElementById("content"))};if(i.files[0])r.readAsDataURL(i.files[0])},
    remChestLogo(){this.data.chestConfig.logo=null;Store.save(this.data);this.renderChest(document.getElementById("content"))},
    renderChestPreview(){
        const b=document.getElementById("cc-prev");if(!b)return; const c=this.data.chestConfig; const s=3.78; const w=c.widthCm*10*s; const h=c.heightCm*10*s;
        const d={name:"Student Name",chest:"101",team:"ZARQAN"};
        b.innerHTML=`<div style="position:relative;width:${w}px;height:${h}px;background:${c.bgColor};border-radius:${c.radius}px;overflow:hidden;box-shadow:0 4px 12px rgba(0,0,0,0.1)">${this.ccEl('fest',c,d)}${this.ccEl('name',c,d)}${this.ccEl('chest',c,d)}${this.ccEl('team',c,d)}${this.ccEl('logo',c,d)}<div id="qr-prev" style="position:absolute;top:${c.elements.qr.y}%;left:${c.elements.qr.x}%;transform:translate(-50%,-50%);display:${c.elements.qr.visible?'block':'none'}"></div></div>`;
        new QRCode(document.getElementById("qr-prev"),{text:"ID:123",width:c.elements.qr.size,height:c.elements.qr.size,colorDark:c.elements.qr.color,colorLight:"transparent"});
    },
    ccEl(k,c,d){const e=c.elements[k];if(!e.visible)return'';if(k==='logo')return`<img src="${c.logo}" style="position:absolute;top:${e.y}%;left:${e.x}%;width:${e.size}px;transform:translate(-50%,-50%)">`;const t=k==='fest'?e.text:(k==='name'?d.name:(k==='chest'?d.chest:d.team));return`<div style="position:absolute;top:${e.y}%;left:${e.x}%;transform:translate(-50%,-50%);font-size:${e.size}px;color:${e.color};font-weight:${e.bold?'bold':'normal'};white-space:nowrap">${t}</div>`},
    printChest(){
        const p=document.getElementById("print-area"); const c=this.data.chestConfig;
        const s=`<style>@media print { .cc-wrap { width:${c.widthCm}cm; height:${c.heightCm}cm; position:relative; display:inline-block; margin:0.2cm; page-break-inside:avoid; background:${c.bgColor}; border-radius:${c.radius}px; overflow:hidden; border:1px dashed #ccc; } .cc-el { position:absolute; transform:translate(-50%,-50%); white-space:nowrap; text-align:center; } }</style>`;
        const cds=this.data.students.map(st=>{const t=this.data.teams.find(x=>x.id===st.teamId); const d={name:st.name,chest:st.chestNo,team:t.name}; return `<div class="cc-wrap">${this.ccPrintEl('fest',c,d)}${this.ccPrintEl('name',c,d)}${this.ccPrintEl('chest',c,d)}${this.ccPrintEl('team',c,d)}${this.ccPrintEl('logo',c,d)}<div class="cc-el" style="top:${c.elements.qr.y}%;left:${c.elements.qr.x}%;display:${c.elements.qr.visible?'block':'none'}"><div id="q-${st.id}"></div></div></div>`}).join('');
        p.innerHTML=s+cds; this.data.students.forEach(st=>{const e=document.getElementById(`q-${st.id}`);if(e)new QRCode(e,{text:`ID:${st.id}`,width:c.elements.qr.size,height:c.elements.qr.size,colorDark:c.elements.qr.color,colorLight:"transparent"})}); setTimeout(()=>window.print(),500);
    },
    ccPrintEl(k,c,d){const e=c.elements[k];if(!e.visible)return'';if(k==='logo')return`<img src="${c.logo}" class="cc-el" style="top:${e.y}%;left:${e.x}%;width:${e.size}px">`;const t=k==='fest'?e.text:(k==='name'?d.name:(k==='chest'?d.chest:d.team));return`<div class="cc-el" style="top:${e.y}%;left:${e.x}%;font-size:${e.size}px;color:${e.color};font-weight:${e.bold?'bold':'normal'}">${t}</div>`},

    /* Search & Modals - Updated for Groups & Team Search */
    renderStudentPoints(el) { el.innerHTML = `<div class="row" style="margin-bottom:20px"><h2>Student Points Portal</h2><input class="input" style="width:300px" placeholder="Search Student or Team..." oninput="App.searchPoints(this.value)"></div><div class="card" id="pts-res"><p>Start typing...</p></div>`; },
    searchPoints(q) {
        if(q.length<2) return; const ql = q.toLowerCase();
        const res = this.data.students.filter(s => {
            const tName = this.data.teams.find(t=>t.id===s.teamId).name.toLowerCase();
            return s.name.toLowerCase().includes(ql) || s.chestNo.includes(q) || tName.includes(ql);
        });
        const calcs = res.map(s => {
            let st=0, nst=0, tot=0; this.data.entries.filter(e=>e.memberStudentIds.includes(s.id)).forEach(e=>{
                const c=this.data.competitions.find(x=>x.id===e.competitionId);const r=this.data.results.find(x=>x.entryId===e.id);
                // Logic: Not General, Not Group
                if(c && c.category!=='GENERAL' && c.type!=='GROUP' && r){if(c.isStage)st+=(r.pointsAwarded||0);else nst+=(r.pointsAwarded||0);tot+=(r.pointsAwarded||0)}
            }); return {s, st, nst, tot};
        });
        document.getElementById('pts-res').innerHTML = `<table><thead><tr><th>Chest</th><th>Name</th><th>Team</th><th>Stage Pts</th><th>Off-Stage Pts</th><th>Total</th></tr></thead><tbody>${calcs.map(x=>`<tr><td>#${x.s.chestNo}</td><td>${x.s.name}</td><td>${this.data.teams.find(t=>t.id===x.s.teamId).name}</td><td>${x.st}</td><td>${x.nst}</td><td><strong>${x.tot}</strong></td></tr>`).join('')}</tbody></table>`;
    },
    renderTeamProgs(el) { el.innerHTML = `<div class="row" style="margin-bottom:20px"><h2>Team Programs</h2><select class="input" style="width:200px" onchange="App.loadTeamList(this.value)"><option value="">Select Team</option>${this.data.teams.map(t=>`<option value="${t.id}">${t.name}</option>`).join('')}</select><button class="btn primary" onclick="window.print()">🖨️ Print</button></div><div id="team-list-view" class="card"><p>Select a team...</p></div>`; },
    loadTeamList(tid) {
        if(!tid) return; const t = this.data.teams.find(x=>x.id===tid); const studs = this.data.students.filter(s=>s.teamId===tid);
        let html = `<div class="print-section"><h3>${t.name} - Programs</h3><table style="margin-top:15px"><thead><tr><th>Chest</th><th>Student</th><th>Category</th><th>Programs</th></tr></thead><tbody>`;
        studs.forEach(s => { const enr = this.data.entries.filter(e=>e.memberStudentIds.includes(s.id)); if(enr.length > 0) html += `<tr><td>#${s.chestNo}</td><td>${s.name}</td><td>${s.category}</td><td>${enr.map(e => this.data.competitions.find(c=>c.id===e.competitionId).name).join(', ')}</td></tr>`; });
        document.getElementById('team-list-view').innerHTML = html + `</tbody></table></div>`;
    },
    globalSearch(q) {
        const el = document.getElementById('content'); if(q.length<2){this.renderTab();return;}
        const sRes = this.data.students.filter(s=>s.name.toLowerCase().includes(q)||s.chestNo.includes(q)); const cRes = this.data.competitions.filter(c=>c.name.toLowerCase().includes(q));
        el.innerHTML = `<div class="grid cols-2"><div class="card"><h3>Students</h3>${sRes.map(s=>`<div class="row" style="justify-content:space-between;border-bottom:1px solid var(--border);padding:5px"><span><b>${s.name}</b> (#${s.chestNo})</span> <button class="btn sm" onclick="App.viewStud('${s.id}')">View</button></div>`).join('')}</div><div class="card"><h3>Competitions</h3>${cRes.map(c=>`<div class="row" style="justify-content:space-between;border-bottom:1px solid var(--border);padding:5px"><span>${c.name}</span><button class="btn sm primary" onclick="App.openJudge('${c.id}')">Judge</button></div>`).join('')}</div></div>`;
    },
    viewStud(sid) {
        const s=this.data.students.find(x=>x.id===sid); const enr=this.data.entries.filter(e=>e.memberStudentIds.includes(sid));
        let st=0,nst=0,tot=0; enr.forEach(e=>{const c=this.data.competitions.find(x=>x.id===e.competitionId);const r=this.data.results.find(x=>x.entryId===e.id);if(c&&c.category!=='GENERAL'&&c.type!=='GROUP'&&r){if(c.isStage)st+=(r.pointsAwarded||0);else nst+=(r.pointsAwarded||0);tot+=(r.pointsAwarded||0)}});
        const h = `<h3>${s.name} (#${s.chestNo})</h3><div class="row" style="margin:10px 0;gap:10px"><div class="tag gold">Total: ${tot}</div><div class="tag blue">Stage: ${st}</div><div class="tag green">Non-Stage: ${nst}</div></div><table><thead><tr><th>Comp</th><th>Result</th><th>Pts</th></tr></thead><tbody>${enr.map(e=>{const c=this.data.competitions.find(x=>x.id===e.competitionId);const r=this.data.results.find(x=>x.entryId===e.id);return `<tr><td>${c.name} (${c.isStage?'S':'NS'})</td><td>${r?r.rankLabel||'-':'-'}</td><td>${r?r.pointsAwarded:0}</td></tr>`}).join('')}</tbody></table><button class="btn" style="margin-top:10px;width:100%" onclick="App.closeModal()">Close</button>`;
        this.openModal(h);
    },

    /* Team Portal Logic */
    renderTeamStudents(el) {
        const my = this.data.students.filter(s=>s.teamId===this.state.user.id);
        el.innerHTML = `<div class="card"><form class="row" onsubmit="App.addStud(event)"><input id="sn" placeholder="Name" required><input id="sc" placeholder="Chest No" required><select id="sct">${this.data.categories.filter(c=>c!=='GENERAL').map(c=>`<option>${c}</option>`).join('')}</select><button class="btn primary">Add</button></form></div><div class="card"><table><thead><tr><th>#</th><th>Name</th><th>Cat</th><th>Act</th></tr></thead><tbody>${my.map(s=>`<tr><td>${s.chestNo}</td><td>${s.name}</td><td>${s.category}</td><td><button class="btn sm danger" onclick="App.delStud('${s.id}')">X</button></td></tr>`).join('')}</tbody></table></div>`;
    },
    addStud(e){e.preventDefault();const c=document.getElementById('sc').value;if(this.data.students.find(s=>s.chestNo===c))return alert("Chest Exists");this.data.students.push({id:Date.now().toString(),teamId:this.state.user.id,name:document.getElementById('sn').value,chestNo:c,category:document.getElementById('sct').value});Store.save(this.data);this.renderTab()},
    delStud(id){if(confirm("Del?")){this.data.students=this.data.students.filter(s=>s.id!==id);Store.save(this.data);this.renderTab()}},
    renderTeamEnroll(el) {
        const my = this.data.students.filter(s=>s.teamId===this.state.user.id);
        el.innerHTML = `<div class="grid cols-3">${this.data.competitions.map(c=>{
            const enr = this.data.entries.filter(e=>e.competitionId===c.id && e.teamId===this.state.user.id); const eli = my.filter(s=>c.category==='GENERAL' || s.category===c.category);
            return `<div class="card"><b>${c.name}</b> <span class="tag blue">${c.category}</span><br><span class="tag gray">${c.type}</span> <span class="tag ${c.isStage?'gold':'green'}">${c.isStage?'Stage':'Off'}</span>
            <div style="margin:10px 0;font-size:0.8rem">${enr.length} / ${c.teamLimit} Slots</div>
            <div style="margin-bottom:10px">${enr.map(e=>`<span class="tag green">${this.data.students.find(x=>x.id===e.memberStudentIds[0]).name} <b style="cursor:pointer" onclick="App.unenroll('${e.id}')">x</b></span>`).join(' ')}</div>
            <form class="row" onsubmit="App.enroll(event,'${c.id}')"><select class="input sm" id="e-${c.id}">${eli.map(s=>`<option value="${s.id}">${s.name}</option>`).join('')}</select><button class="btn sm primary">Join</button></form></div>`;
        }).join('')}</div>`;
    },
    enroll(e, cid) {
        e.preventDefault(); const sid = document.getElementById(`e-${cid}`).value; if(!sid) return;
        const c = this.data.competitions.find(x=>x.id===cid); 
        const teamCur = this.data.entries.filter(x => x.competitionId === cid && x.teamId === this.state.user.id).length;
        
        if(teamCur >= c.teamLimit) return alert("Team Limit Reached!");
        if(this.data.entries.find(x=>x.competitionId===cid && x.memberStudentIds.includes(sid))) return alert("Already Joined");

        const sEnr = this.data.entries.filter(x=>x.memberStudentIds.includes(sid));
        if (c.category === 'GENERAL') { if (c.type === 'INDIVIDUAL') { if (sEnr.filter(ent => { const comp = this.data.competitions.find(x=>x.id===ent.competitionId); return comp.category === 'GENERAL' && comp.type === 'INDIVIDUAL'; }).length >= 3) return alert("Limit: 3 General Indiv Events."); } } 
        else { if (c.isStage) { if (sEnr.filter(ent => { const comp = this.data.competitions.find(x=>x.id===ent.competitionId); return comp.category !== 'GENERAL' && comp.isStage; }).length >= 3) return alert("Limit: 3 Stage Events."); } }
        this.data.entries.push({id:Date.now().toString(),competitionId:cid,teamId:this.state.user.id,memberStudentIds:[sid]}); Store.save(this.data); this.renderTab();
    },
    unenroll(eid) { this.data.entries=this.data.entries.filter(e=>e.id!==eid); Store.save(this.data); this.renderTab(); },

    /* Scanners */
    openGlobalScanner(){this.startScan(id=>{this.closeModal();this.viewStud(id)})},
    scanAtt(cid){this.startScan(id=>{this.closeModal();this.markAtt(id,cid)})},
    startScan(cb){
        this.openModal(`<h3>Scanner</h3><div id="rdr"></div><button class="btn danger" style="width:100%" onclick="App.stopScan()">Close</button>`);
        this.state.scanner=new Html5QrcodeScanner("rdr",{fps:10,qrbox:250}); this.state.scanner.render(txt=>{if(txt.startsWith("ID:")){const id=txt.split(":")[1];if(this.data.students.find(x=>x.id===id)){this.state.scanner.clear();cb(id)}else alert("Not Found")}});
    },
    stopScan(){if(this.state.scanner)this.state.scanner.clear();this.closeModal()},
    markAtt(sid,cid){
        const ent=this.data.entries.find(e=>e.competitionId===cid && e.memberStudentIds.includes(sid)); if(!ent)return alert("Not Enrolled");
        let res=this.data.results.find(r=>r.entryId===ent.id); if(!res)this.data.results.push({id:Date.now(),competitionId:cid,entryId:ent.id,rankLabel:'',pointsAwarded:0,attendance:true,codeLetter:''}); else res.attendance=true; Store.save(this.data); this.openJudge(cid);
    },
    openModal(h){document.getElementById('modal-content').innerHTML=h;document.getElementById('modal-overlay').style.display='grid'},
    closeModal(){document.getElementById('modal-overlay').style.display='none';if(this.state.scanner)this.state.scanner.clear()}
};
App.init();
</script>
</body>
</html>
