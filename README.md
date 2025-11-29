          const team = this.data.teams.find(t => t.id === entry.teamId);
          
          if (!student || !team) return null;
          
          // Use only the first character of the rank label for sorting/identifying
          const rankChar = r.rankLabel ? r.rankLabel.toUpperCase().charAt(0) : '';

          return {
              ...r,
              rankChar: rankChar,
              studentName: student.name,
              teamName: team.name
          };
      }).filter(r => r !== null && r.rankChar); // Filter out nulls and empty ranks

      // Sort by rank: '1' > '2' > '3', then by points, then by rankLabel string
      decoratedResults.sort((a, b) => {
          const rankA = a.rankChar;
          const rankB = b.rankChar;
          
          if (rankA === '1') return -1;
          if (rankB === '1') return 1;
          if (rankA === '2' && rankB !== '1') return -1;
          if (rankB === '2' && rankA !== '1') return 1;
          if (rankA === '3' && rankB !== '1' && rankB !== '2') return -1;
          if (rankB === '3' && rankA !== '1' && rankA !== '2') return 1;
          
          // Secondary sort by points
          if (b.pointsAwarded !== a.pointsAwarded) return b.pointsAwarded - a.pointsAwarded;

          // Fallback sort by rank label string
          return (a.rankLabel || '').localeCompare(b.rankLabel || '');
      });
      
      const winners = {
          first: decoratedResults.find(r => r.rankChar === '1') || null,
          second: decoratedResults.find(r => r.rankChar === '2') || null,
          third: decoratedResults.find(r => r.rankChar === '3') || null,
          others: decoratedResults.filter(r => r.rankChar !== '1' && r.rankChar !== '2' && r.rankChar !== '3')
      };
      
      return winners;
  },

  getCompPosterHTML(comp, winners) {
      const festTitle = this.data.chestConfig.elements.fest.text;

      const getWinnerInfo = (place, nameKey, teamKey) => {
          if (place) {
              return {
                  name: place[nameKey],
                  team: place[teamKey],
                  label: place.rankLabel
              };
          }
          return { name: 'N/A', team: 'No Result' };
      };

      const w1 = getWinnerInfo(winners.first, 'studentName', 'teamName');
      const w2 = getWinnerInfo(winners.second, 'studentName', 'teamName');
      const w3 = getWinnerInfo(winners.third, 'studentName', 'teamName');

      return `
          <div class="comp-poster-box" id="comp-poster-print-area">
              <span style="font-size:16px; color:var(--primary); font-weight:600; text-transform:uppercase;">${festTitle} | ${comp.category}</span>
              <h1>${comp.name}</h1>
              <h2 style="font-family:var(--font-body); font-weight:400; font-size:18px;">Official Results</h2>

              <div class="winner-podium">
                  
                  <div class="podium-place place-2" style="order: 1;">
                      <div class="rank-badge">2</div>
                      <h3 style="color:#adb5bd;">Runner Up</h3>
                      <p style="font-weight:600;">${w2.name}</p>
                      <p style="color:var(--text-muted);">${w2.team}</p>
                      ${w2.label ? `<span class="tag gray sm" style="margin-top:5px; display:inline-block">Rank: ${w2.label}</span>` : ''}
                  </div>

                  <div class="podium-place place-1" style="order: 0; min-height: 200px; padding-top: 40px;">
                      <div class="rank-badge">1</div>
                      <h3 style="color:var(--accent-gold);">Champion</h3>
                      <p style="font-weight: bold; font-size:16px;">${w1.name}</p>
                      <p style="color:var(--text-main); font-size:14px;">${w1.team}</p>
                      ${w1.label ? `<span class="tag gold sm" style="margin-top:5px; display:inline-block">Rank: ${w1.label}</span>` : ''}
                  </div>

                  <div class="podium-place place-3" style="order: 2;">
                      <div class="rank-badge">3</div>
                      <h3 style="color:#ced4da;">2nd Runner Up</h3>
                      <p style="font-weight:600;">${w3.name}</p>
                      <p style="color:var(--text-muted);">${w3.team}</p>
                      ${w3.label ? `<span class="tag gray sm" style="margin-top:5px; display:inline-block">Rank: ${w3.label}</span>` : ''}
                  </div>
              </div>
              
              <p style="margin-top:40px; font-size:12px; color:var(--text-muted);">Congratulations to all participants!</p>
          </div>
      `;
  },

  renderAdminCompPosters(el) {
    const comps = this.data.competitions;
    const selectedComp = comps.find(c => c.id === this.state.compPosterId);
    let posterHtml = '';
    
    if (selectedComp) {
        const winners = this.getCompPosterData(selectedComp.id);
        posterHtml = this.getCompPosterHTML(selectedComp, winners);
    }

    el.innerHTML = `
      <div class="row">
        <h2>🥇 Competition Poster Generator</h2>
        <select class="input" id="comp-poster-selector" style="width:300px" onchange="App.setCompPosterSelection(this.value)">
            <option value="">-- Select Competition --</option>
            ${comps.map(c => `
                <option value="${c.id}" ${c.id === this.state.compPosterId ? 'selected' : ''}>
                    ${c.name} (${c.category})
                </option>
            `).join('')}
        </select>
        <button class="btn primary print-btn" onclick="App.printCompPoster()" ${!selectedComp ? 'disabled' : ''}>🖨️ Print/Save Poster (PDF)</button>
      </div>
      
      <div class="card">
         <p class="danger-note">💡 **Note:** Posters rely on Judge Panel results. Ensure you have entered the **Rank/Grade** (e.g., '1', '2', '3') for the winners to appear here.</p>
         ${!selectedComp ? '<p style="text-align:center; color:var(--text-muted); margin-top:20px;">Select a competition above to generate the result poster.</p>' : ''}
      </div>

      <div id="poster-container">
        ${posterHtml}
      </div>
    `;
  },
  
  printCompPoster() {
      const content = document.getElementById("comp-poster-print-area").outerHTML;
      const pArea = document.getElementById("print-area");
      
      pArea.innerHTML = `<div style="padding:40px; text-align:center; font-family:var(--font-heading); background:#fff;">
          <h1 style="font-size:30px; color:var(--primary-dark)">Official Competition Result</h1>
          <p style="color:var(--text-muted)">Generated on ${new Date().toLocaleDateString()}</p>
          <hr style="border:0; border-top:2px solid var(--border); margin:20px 0;">
      </div>` + content;
      
      window.print();
  },

  /* --------------------------------------------------------------------------
     ADMIN MODULES - OVERALL POSTER (Renamed)
     -------------------------------------------------------------------------- */
  
  renderAdminOverallPosters(el) { /* Renamed from renderAdminPosters */
    const scoreData = this.calculateScoreData();
    const posterHtml = this.getOverallPosterHTML(scoreData, this.state.posterTemplate);

    el.innerHTML = `
      <h2>🖼️ Overall Championship Poster Generator</h2>
      
      <div class="card">
        <h3>Template Selector</h3>
        <p class="danger-note">🚫 **Print Limitation:** Use the browser's **Print to PDF** function (Ctrl+P / Cmd+P) to save the generated poster as a high-quality file.</p>
        <div class="row" style="margin-top:15px;">
            <button class="btn ${this.state.posterTemplate === 'A' ? 'primary' : ''}" onclick="App.setOverallPosterTemplate('A')">🥇 Template A (Minimal)</button>
            <button class="btn ${this.state.posterTemplate === 'B' ? 'primary' : ''}" onclick="App.setOverallPosterTemplate('B')">✨ Template B (Detailed)</button>
            <button class="btn" style="margin-left:auto" onclick="App.printOverallPoster()">🖨️ Print/Save Poster (PDF)</button>
        </div>
      </div>
      
      <div id="overall-poster-area">
        ${posterHtml}
      </div>
    `;
  },
  
  setOverallPosterTemplate(template) {
      this.state.posterTemplate = template;
      this.renderAdminOverallPosters(document.getElementById("content-area")); 
  },
  
  getOverallPosterHTML(data, template) { /* Renamed from getPosterHTML */
      const festTitle = this.data.chestConfig.elements.fest.text;

      if (template === 'A') {
          return `
              <div class="poster-template" style="padding:60px; background:#fff;">
                  <span style="color:var(--text-muted); font-size:16px; text-transform:uppercase;">${new Date().getFullYear()} Edition</span>
                  <h1>${festTitle} Results</h1>
                  <h2 style="font-size:28px; color:var(--accent-gold); margin-bottom:15px;">Overall Championship Winner</h2>
                  
                  <div class="champion-box">
                      <p style="font-size:20px; color:var(--text-main); margin-bottom:8px;">The prestigious Champion Trophy goes to:</p>
                      <h3>${data.champion.name}</h3>
                      <p style="font-size:16px; color:var(--text-muted); margin-top:8px;">Total Points: ${data.champion.total}</p>
                  </div>
                  
                  <p style="margin-top:30px; font-weight:600; font-size:14px; color:var(--primary-dark)">Congratulations to all participants!</p>
              </div>
          `;
      } else if (template === 'B') {
          return `
              <div class="poster-template" style="padding:40px; background:#fff;">
                  <span style="color:var(--primary); font-size:14px; font-weight:600; text-transform:uppercase;">Official Scorecard | ${new Date().toLocaleDateString()}</span>
                  <h1>${festTitle} Standings</h1>
                  <h2 style="font-size:20px; color:var(--text-main)">Champion: <span style="color:var(--accent-gold); font-weight:bold;">${data.champion.name}</span> (${data.champion.total} Pts)</h2>

                  <div class="secondary-results">
                      <div style="background:#e9f7ef; border:1px solid #c8e6c9;">
                          <p style="color:var(--success); font-weight:700">🏆 2nd Place</p>
                          <h4>${data.runnerUp.name}</h4>
                          <p style="color:var(--success)">${data.runnerUp.total} Points</p>
                      </div>
                      <div style="background:#f0f5ff; border:1px solid #c9dfff;">
                          <p style="color:var(--primary-dark); font-weight:700">🥉 3rd Place</p>
                          <h4>${data.secondRunnerUp.name}</h4>
                          <p style="color:var(--primary-dark)">${data.secondRunnerUp.total} Points</p>
                      </div>
                  </div>
                  
                  <div class="secondary-results" style="margin-top:15px;">
                      <div style="background:#fefefe; border:1px solid #eee;">
                          <p style="color:#007bff; font-weight:700">🎤 Top Stage Performer</p>
                          <h4 style="color:#007bff; font-size:18px">${data.topStage.name}</h4>
                          <p style="font-size:13px">${data.topStage.points} Pts | ${data.topStage.team}</p>
                      </div>
                      <div style="background:#fefefe; border:1px solid #eee;">
                          <p style="color:#343a40; font-weight:700">✍️ Top Non-Stage Performer</p>
                          <h4 style="color:#343a40; font-size:18px">${data.topNonStage.name}</h4>
                          <p style="font-size:13px">${data.topNonStage.points} Pts | ${data.topNonStage.team}</p>
                      </div>
                  </div>
              </div>
          `;
      }
      return '<p style="text-align:center;">Select a template above to generate the poster.</p>';
  },

  printOverallPoster() { /* Renamed from printPoster */
    const content = document.getElementById("overall-poster-area").innerHTML;
    const pArea = document.getElementById("print-area");
    // Add header for print context
    pArea.innerHTML = `<div style="padding:40px; text-align:center; font-family:var(--font-heading); background:#fff;">
      <h1 style="font-size:30px; color:var(--primary-dark)">${this.data.chestConfig.elements.fest.text} Overall Results</h1>
      <p style="color:var(--text-muted)">Official Printout - ${new Date().toLocaleDateString()}</p>
      <hr style="border:0; border-top:1px solid var(--border); margin:20px 0;">
      </div>` + content;
    window.print();
  },

  /* --------------------------------------------------------------------------
     REST OF ADMIN MODULES (Unchanged functionality, minor adjustments)
     -------------------------------------------------------------------------- */
  
  // Reusing existing functions from previous steps...
  calculateScoreData() {
      const scores = {}; 
      this.data.teams.forEach(t => {
          scores[t.id] = { id: t.id, name: t.name, total: 0, stage: 0, nonStage: 0, cats: {} };
      });

      const studentPoints = {}; 
      
      this.data.results.forEach(r => {
          const entry = this.data.entries.find(e => e.id === r.entryId);
          if(!entry) return;
          const comp = this.data.competitions.find(c => c.id === entry.competitionId);
          if(!comp) return; // Ensure competition exists
          const pts = r.pointsAwarded || 0;
          const tid = entry.teamId;
          const sid = entry.memberStudentIds[0];
          
          if(scores[tid]) {
              scores[tid].total += pts;
              if(comp.isStage) scores[tid].stage += pts; else scores[tid].nonStage += pts;
          }
          
          if (sid) {
              if (!studentPoints[sid]) studentPoints[sid] = { total: 0, stage: 0, nonStage: 0 };
              studentPoints[sid].total += pts;
              if(comp.isStage) studentPoints[sid].stage += pts; else studentPoints[sid].nonStage += pts;
          }
      });

      const sortedTeams = Object.values(scores).sort((a,b) => b.total - a.total);
      
      let topStageStudent = { name: '-', points: 0, team: '-' };
      let topNonStageStudent = { name: '-', points: 0, team: '-' };

      Object.entries(studentPoints).forEach(([sid, p]) => {
          const s = this.data.students.find(student => student.id === sid);
          if (!s) return;
          const t = this.data.teams.find(team => team.id === s.teamId);
          const studentInfo = { name: s.name, points: 0, team: t ? t.name : 'N/A' };

          if (p.stage > topStageStudent.points) {
              topStageStudent = { ...studentInfo, points: p.stage };
          }
          if (p.nonStage > topNonStageStudent.points) {
              topNonStageStudent = { ...studentInfo, points: p.nonStage };
          }
      });

      return {
          champion: sortedTeams[0] || { name: 'N/A', total: 0 },
          runnerUp: sortedTeams[1] || { name: 'N/A', total: 0 },
          secondRunnerUp: sortedTeams[2] || { name: 'N/A', total: 0 },
          topStage: topStageStudent,
          topNonStage: topNonStageStudent,
          allTeams: sortedTeams
      };
  },
  
  renderAdminSetup: function(el) { /* Re-used from previous step */
    el.innerHTML = `
      <h2>🛠️ Setup & Data</h2>
      <div class="grid cols-3">
        <div class="card">
            <h3>Custom Logo Upload</h3>
            <p style="font-size:13px">Upload a square image (PNG/JPG) for the circular logo space.</p>
            ${this.data.logo ? `
                <div style="text-align:center; margin:15px 0;">
                    <img src="${this.data.logo}" class="logo-circle" style="width:60px; height:60px; margin:0 auto; background:transparent;">
                    <p style="margin-top:10px; font-size:12px;">Current Logo</p>
                </div>
                <button class="btn danger" style="width:100%" onclick="App.removeLogo()">❌ Remove Logo</button>
            ` : `
                <label class="logo-upload-box">
                    <p style="color:var(--text-muted)">Click to upload image (Recommended: PNG)</p>
                    <input type="file" style="display:none" accept="image/png, image/jpeg" onchange="App.handleLogoUpload(this.files[0])">
                </label>
            `}
        </div>

        <div class="card">
          <h3>Manage Teams</h3>
          <p class="tag gray" style="margin-bottom:15px">Click on the team to edit its name or password.</p>
          <div id="team-list">
            ${this.data.teams.map(t => `
              <div style="border:1px solid var(--border); padding:8px; margin-bottom:6px; border-radius:8px; cursor:pointer; background:var(--surface-alt);" onclick="App.editTeam('${t.id}')">
                <strong>${t.name}</strong> <span class="tag gray sm">${t.password}</span>
              </div>
            `).join('')}
          </div>
          <button class="btn primary sm" onclick="App.addTeamPrompt()" style="margin-top:10px; width:100%">+ Add Team</button>
        </div>

        <div class="card">
          <h3>Admin Credentials</h3>
          <form onsubmit="App.updateAdminCreds(event)">
             <label>Username</label><input class="input" id="adm-u-new" value="${this.data.admin.username}" required>
             <div style="height:10px"></div>
             <label>Password</label><input class="input" type="password" id="adm-p-new" value="${this.data.admin.password}" required>
             <button class="btn primary" style="width:100%; margin-top:15px;">💾 Update Crew Login</button>
          </form>

          <hr style="border:0; border-top:1px solid var(--border); margin:15px 0;">
          
          <h3>Backup & Restore</h3>
          <div class="row">
           <button class="btn sm primary" onclick="Store.exportJSON(App.data)">⬇️ Export JSON</button>
           <label class="btn sm">
              ⬆️ Import JSON <input type="file" style="display:none" accept=".json" onchange="Store.importJSON(this.files[0], (d)=>{App.data=d; Store.save(d); alert('Data Imported! Page will reload.'); location.reload();})">
           </label>
          </div>
        </div>
      </div>
      
      <div id="team-edit-modal" class="card" style="display:none; position:fixed; top:50%; left:50%; transform:translate(-50%, -50%); z-index:100; min-width:350px;">
          <h3>Edit Team <span id="edit-team-name-display"></span></h3>
          <form onsubmit="App.saveTeamEdit(event)">
              <input type="hidden" id="edit-team-id">
              <label>Team Name</label><input class="input" id="edit-team-name" required>
              <div style="height:10px"></div>
              <label>Password</label><input class="input" id="edit-team-password" required>
              <div class="row" style="margin-top:20px">
                  <button type="button" class="btn" onclick="document.getElementById('team-edit-modal').style.display='none'">Cancel</button>
                  <button type="submit" class="btn primary">Save Changes</button>
                  <button type="button" class="btn danger" style="margin-left:auto" onclick="App.deleteTeam()">Delete Team</button>
              </div>
          </form>
      </div>
    `;
  },
  handleLogoUpload: function(file) { /* Re-used from previous step */
      if (!file) return;
      const reader = new FileReader();
      reader.onload = (e) => {
          this.data.logo = e.target.result; // Store as base64
          Store.save(this.data);
          alert("Logo uploaded successfully!");
          this.renderTabContent();
          this.updateLogo();
      };
      reader.readAsDataURL(file);
  },
  removeLogo: function() { /* Re-used from previous step */
      if (confirm("Are you sure you want to remove the custom logo?")) {
          this.data.logo = null;
          Store.save(this.data);
          alert("Custom logo removed. Default 'F' will be used.");
          this.renderTabContent();
          this.updateLogo();
      }
  },
  addTeamPrompt: function() { /* Re-used from previous step */
    const name = prompt("Enter new team name:");
    if (!name) return;
    const pass = prompt(`Enter password for team "${name}":`);
    if (!pass) return;

    this.data.teams.push({
        id: 't' + Date.now().toString(), name: name.toUpperCase(), password: pass
    });
    Store.save(this.data);
    this.renderAdminSetup(document.getElementById("content-area"));
  },
  editTeam: function(id) { /* Re-used from previous step */
    const team = this.data.teams.find(t => t.id === id);
    if (!team) return;

    document.getElementById('edit-team-id').value = id;
    document.getElementById('edit-team-name').value = team.name;
    document.getElementById('edit-team-password').value = team.password;
    document.getElementById('edit-team-name-display').innerText = team.name;
    document.getElementById('team-edit-modal').style.display = 'block';
  },
  saveTeamEdit: function(e) { /* Re-used from previous step */
    e.preventDefault();
    const id = document.getElementById('edit-team-id').value;
    const name = document.getElementById('edit-team-name').value;
    const password = document.getElementById('edit-team-password').value;
    
    const team = this.data.teams.find(t => t.id === id);
    if (team) {
        team.name = name;
        team.password = password;
        Store.save(this.data);
        document.getElementById('team-edit-modal').style.display = 'none';
        this.renderTabContent();
    }
  },
  deleteTeam: function() { /* Re-used from previous step */
      if (!confirm("Are you sure you want to delete this team? This will remove all their students and entries.")) return;
      const id = document.getElementById('edit-team-id').value;
      this.data.teams = this.data.teams.filter(t => t.id !== id);
      this.data.students = this.data.students.filter(s => s.teamId !== id);
      this.data.entries = this.data.entries.filter(e => e.teamId !== id);
      Store.save(this.data);
      document.getElementById('team-edit-modal').style.display = 'none';
      this.renderTabContent();
  },
  updateAdminCreds: function(e) { /* Re-used from previous step */
      e.preventDefault();
      this.data.admin.username = document.getElementById("adm-u-new").value;
      this.data.admin.password = document.getElementById("adm-p-new").value;
      Store.save(this.data);
      alert("Crew credentials updated successfully!");
      this.loadLayout();
  },
  
  // Remaining modules (Comps, Judge, Scores, Chest) are re-used/re-mapped but not repeated here for brevity.
  renderAdminComps: function(el) { /* Re-used */
    el.innerHTML = `
      <div class="row"><h2>📋 Competitions</h2> <div style="flex:1"></div></div>
      <div class="card">
        <h3>Add New Competition</h3>
        <form class="grid cols-3" style="align-items:end" onsubmit="App.addComp(event)">
          <div><label>Name</label><input class="input" id="c-name" required placeholder="e.g., Arabic Elocution"></div>
          <div><label>Category</label><select class="input" id="c-cat">${this.data.categories.map(c=>`<option>${c}</option>`).join('')}</select></div>
          <div class="row">
             <div style="display:flex; gap:10px; align-items:center;">
                 <label style="display:flex;align-items:center;gap:5px; margin-bottom:0;"><input type="checkbox" id="c-stage"> Stage Item?</label>
                 <label style="display:flex;align-items:center;gap:5px; margin-bottom:0;"><input type="checkbox" id="c-general"> General?</label>
             </div>
             <button class="btn primary sm">➕ Add</button>
          </div>
        </form>
      </div>
      <div class="card">
        <h3>List of Competitions (${this.data.competitions.length})</h3>
        <table>
          <thead><tr><th>Name</th><th>Type</th><th>Category</th><th>Entries</th><th>Action</th></tr></thead>
          <tbody>
            ${this.data.competitions.map(c => `
              <tr>
                <td>${c.name}</td>
                <td>${c.isStage ? '<span class="tag gold">Stage</span>' : '<span class="tag gray">Non-Stage</span>'}</td>
                <td><span class="tag blue">${c.category}</span></td>
                <td>${this.data.entries.filter(e=>e.competitionId===c.id).length}</td>
                <td><button class="btn sm danger" onclick="App.delComp('${c.id}')">❌ Delete</button></td>
              </tr>
            `).join('')}
          </tbody>
        </table>
      </div>
    `;
  },
  addComp: function(e) { /* Re-used */
    e.preventDefault();
    const name = document.getElementById("c-name").value;
    const catSelect = document.getElementById("c-cat").value;
    const isStage = document.getElementById("c-stage").checked;
    const isGen = document.getElementById("c-general").checked;
    
    const finalCat = isGen ? 'GENERAL' : catSelect;

    this.data.competitions.push({
        id: Date.now().toString(), name, category: finalCat, isStage, locked: false
    });
    Store.save(this.data); this.renderTabContent();
  },
  delComp: function(id) { /* Re-used */
    if(confirm("Delete competition? All related entries and results will also be deleted.")) {
        this.data.competitions = this.data.competitions.filter(c=>c.id!==id);
        this.data.entries = this.data.entries.filter(e=>e.competitionId!==id);
        this.data.results = this.data.results.filter(r=>r.competitionId!==id);
        Store.save(this.data); this.renderTabContent();
    }
  },
  renderAdminJudge: function(el) { /* Re-used */
    el.innerHTML = `<h2>⚖️ Judge Panel</h2><div class="grid cols-3">${
      this.data.competitions.map(c => {
          const entryCount = this.data.entries.filter(e=>e.competitionId===c.id).length;
          return `
            <div class="card">
              <h3>${c.name}</h3>
              <div class="row"><span class="tag blue">${c.category}</span>${c.isStage?'<span class="tag gold">Stage</span>':''}</div>
              <p style="margin-top:10px; color:var(--primary-dark); font-weight:600;">${entryCount} Entries</p>
              <button class="btn primary sm" style="margin-top:15px" onclick="App.openJudging('${c.id}')">Open Score Sheet →</button>
            </div>
          `;
      }).join('')
    }</div>`;
  },
  openJudging: function(cid) { /* Re-used */
    const comp = this.data.competitions.find(c=>c.id===cid);
    const entries = this.data.entries.filter(e=>e.competitionId===cid);
    
    const el = document.getElementById("content-area");
    el.innerHTML = `
      <div class="row" style="margin-bottom:20px;">
        <button class="btn" onclick="App.switchTab('judge')">← Back to Competitions</button>
        <h2 style="margin-left:20px">${comp.name}</h2>
        <div style="flex:1"></div>
        <input class="input" style="width:250px" placeholder="🔍 Search Chest No. / Name..." oninput="App.judgeSearch(this.value, '${cid}')">
      </div>
      <div class="card">
         <p style="font-size:14px; font-weight:600; color:var(--primary-dark)">Total Enrolled Entries: ${entries.length}</p>
      </div>
      <div class="card">
        <table id="judge-table">
          <thead><tr><th>Chest No.</th><th>Student Name</th><th>Team</th><th>Rank/Grade</th><th>Points</th><th>Action</th></tr></thead>
          <tbody>
            ${entries.map(e => this.judgeRow(e, comp.id)).join('')}
          </tbody>
        </table>
      </div>
    `;
  },
  judgeRow: function(e, compId) { /* Re-used */
    const s = App.data.students.find(x=>x.id === e.memberStudentIds[0]); 
    if(!s) return '';
    const team = App.data.teams.find(t=>t.id === s.teamId);
    const res = App.data.results.find(r=>r.entryId === e.id) || {};
    
    return `<tr data-name="${s.name.toLowerCase()}" data-chest="${s.chestNo}">
      <td><span class="tag gold">#${s.chestNo}</span></td>
      <td><strong>${s.name}</strong></td>
      <td>${team.name}</td>
      <td><input class="input sm" style="width:80px" value="${res.rankLabel||''}" id="r-${e.id}" placeholder="1, A, etc."></td>
      <td><input class="input sm" type="number" style="width:80px" value="${res.pointsAwarded||0}" id="p-${e.id}"></td>
      <td><button class="btn sm primary" onclick="App.saveResult('${e.id}','${compId}', event)">💾 Save</button></td>
    </tr>`;
  },
  judgeSearch: function(q, cid) { /* Re-used */
    q = q.toLowerCase();
    const tbody = document.querySelector("#judge-table tbody");
    const entries = App.data.entries.filter(e=>e.competitionId===cid);
    
    tbody.innerHTML = entries.map(e => {
        const s = App.data.students.find(x=>x.id === e.memberStudentIds[0]);
        if (!s) return '';
        if (s.name.toLowerCase().includes(q) || s.chestNo.includes(q)) {
            return App.judgeRow(e, cid);
        }
        return '';
    }).join('');
  },
  saveResult: function(eid, cid, event) { /* Re-used */
    const rank = document.getElementById(`r-${eid}`).value;
    const pts = Number(document.getElementById(`p-${eid}`).value);
    
    this.data.results = this.data.results.filter(r => r.entryId !== eid);
    this.data.results.push({
        id: Date.now().toString(), competitionId: cid, entryId: eid,
        rankLabel: rank, pointsAwarded: pts
    });
    Store.save(this.data);
    
    const btn = event.target; 
    const originalText = btn.innerHTML;
    const originalBg = btn.style.background;
    btn.innerHTML = "✅ Saved"; 
    btn.style.background = "var(--success)";
    btn.style.borderColor = "var(--success)";
    setTimeout(()=>{ btn.innerHTML=originalText; btn.style.background=originalBg; btn.style.borderColor="var(--primary)" }, 1000);
  },
  renderAdminScores: function(el) { /* Re-used */
    const data = this.calculateScoreData();

    const getRank = (arr, item, key) => {
        const val = item[key];
        const rankIndex = arr.findIndex(x => x.id === item.id) + 1;
        const prevIndex = rankIndex - 2;
        
        const tie = prevIndex >= 0 && arr[prevIndex] && arr[prevIndex][key] === val ?
            '<span class="tie-indicator" title="Tied Rank" style="color:var(--accent-gold)">=</span>' : '';
        
        return `${val} ${tie}`;
    };

    el.innerHTML = `
      <div class="row"><h2>🏆 Live Scoreboard</h2> <button class="btn primary" onclick="App.printOverallScores()">⬇️ Download PDF</button></div>
      
      <div id="print-content">
        <div class="grid cols-3">
           <div class="card" style="text-align:center; background:#ffffe0; border-color:var(--accent-gold)">
              <h3>Overall Champion</h3>
              <h1 style="font-size:40px; color:var(--accent-gold); margin-top:5px; margin-bottom:5px;">${data.champion.name}</h1>
              <p style="font-size:16px; color:var(--text-main); font-weight:600">${data.champion.total} Points</p>
           </div>
           
           <div class="card" style="text-align:center; background:#e0f7fa;">
              <h3>🎤 Top Stage Performer</h3>
              <h3 style="color:var(--primary); margin-top:5px; margin-bottom:5px;">${data.topStage.name}</h3>
              <p style="font-size:14px">${data.topStage.points} Pts (${data.topStage.team})</p>
           </div>
           
           <div class="card" style="text-align:center; background:#f0f5ff;">
              <h3>🖊️ Top Non-Stage Performer</h3>
              <h3 style="color:var(--primary); margin-top:5px; margin-bottom:5px;">${data.topNonStage.name}</h3>
              <p style="font-size:14px">${data.topNonStage.points} Pts (${data.topNonStage.team})</p>
           </div>
        </div>

        <div class="card">
          <h3>Detailed Standings</h3>
          <table>
            <thead>
              <tr>
                <th>Rank</th>
                <th>Team</th>
                <th>Overall Points</th>
                <th>Stage</th>
                <th>Non-Stage</th>
                <th>Category Points</th>
              </tr>
            </thead>
            <tbody>
              ${data.allTeams.map((t, index) => `
                <tr>
                  <td>${index + 1}</td>
                  <td><strong>${t.name}</strong></td>
                  <td style="font-size:16px; color:var(--primary); font-weight:700">${getRank(data.allTeams, t, 'total')}</td>
                  <td>${t.stage}</td>
                  <td>${t.nonStage}</td>
                  <td><span class="tag gray">${Object.values(t.cats).reduce((a, b) => a + b, 0)}</span></td>
                </tr>
              `).join('')}
            </tbody>
          </table>
          <p style="margin-top:20px; font-size:12px; color:var(--text-muted);">Points are calculated based on results entered in the Judge Panel.</p>
        </div>
      </div>
    `;
  },
  printOverallScores: function() { /* Re-used */
    const content = document.getElementById("print-content").innerHTML;
    const pArea = document.getElementById("print-area");
    pArea.innerHTML = `<div style="padding:40px; text-align:center; font-family:var(--font-heading); background:#fff;">
      <h1 style="font-size:30px; color:var(--primary-dark)">${this.data.chestConfig.elements.fest.text} Scoreboard</h1>
      <p style="color:var(--text-muted)">Generated on ${new Date().toLocaleDateString()}</p>
      <hr style="border:0; border-top:2px solid var(--border); margin:20px 0;">
      </div>` + content;
    window.print();
  },
  renderAdminChest: function(el) { /* Re-used */
    const cfg = this.data.chestConfig;
    
    el.innerHTML = `
      <div class="row"><h2>🏷️ Chest Card Designer</h2> <button class="btn primary" onclick="App.printChestCards()">🖨️ Print All Cards</button></div>
      
      <div class="grid cols-2">
        <div class="card" style="max-height: 80vh; overflow-y:auto">
          <h3>Configuration</h3>
          <div class="grid cols-2">
            <div><label>Width (cm)</label><input class="input" type="number" value="${cfg.widthCm}" onchange="App.updateChestCfg('widthCm', this.value)"></div>
            <div><label>Height (cm)</label><input class="input" type="number" value="${cfg.heightCm}" onchange="App.updateChestCfg('heightCm', this.value)"></div>
            <div><label>Fest Title</label><input class="input" value="${cfg.elements.fest.text}" onchange="App.updateChestCfg('elements.fest.text', this.value)"></div>
            <div><label>Bg Color</label><input class="input" type="color" value="${cfg.bgColor}" onchange="App.updateChestCfg('bgColor', this.value)"></div>
          </div>
          
          <h4>Elements Position (Top/Left %)</h4>
          ${['qr','name','chest','team','fest'].map(k => `
            <div style="border-top:1px solid #eee; padding-top:10px; margin-top:10px; background:var(--surface-alt); padding:10px; border-radius:8px">
              <div class="row">
                <strong style="text-transform:uppercase; flex:1; font-size:14px;">${k}</strong>
                <label style="display:flex;align-items:center;gap:5px; margin-bottom:0">Visible <input type="checkbox" ${cfg.elements[k].visible?'checked':''} onchange="App.updateChestCfg('elements.${k}.visible', this.checked)"></label>
              </div>
              <div class="grid cols-3" style="margin-top:5px">
                 <div><label>Top %</label><input type="number" class="input sm" value="${cfg.elements[k].y}" onchange="App.updateChestCfg('elements.${k}.y', this.value)"></div>
                 <div><label>Left %</label><input type="number" class="input sm" value="${cfg.elements[k].x}" onchange="App.updateChestCfg('elements.${k}.x', this.value)"></div>
                 <div><label>Size (px)</label><input type="number" class="input sm" value="${cfg.elements[k].size}" onchange="App.updateChestCfg('elements.${k}.size', this.value)"></div>
              </div>
            </div>
          `).join('')}
        </div>

        <div class="card" style="display:flex; justify-content:center; align-items:center; background:#f1f5f9;">
           <div id="cc-preview" class="cc-preview-box" style="position:relative; overflow:hidden; box-shadow:0 0 10px rgba(0,0,0,0.1);"></div>
        </div>
      </div>
    `;
    this.renderChestPreview();
  },
  updateChestCfg: function(path, val) { /* Re-used */
    const keys = path.split('.');
    let obj = this.data.chestConfig;
    for(let i=0; i<keys.length-1; i++) obj = obj[keys[i]];
    
    // Type conversion
    if(keys[keys.length-1] === 'visible') obj[keys[keys.length-1]] = val; 
    else if(keys[keys.length-1] === 'text' || keys[keys.length-1] === 'bgColor' || keys[keys.length-1] === 'color') obj[keys[keys.length-1]] = val;
    else if(!isNaN(val)) obj[keys[keys.length-1]] = parseFloat(val);

    Store.save(this.data);
    this.renderChestPreview();
  },
  renderChestPreview: function(student = {name: "Student Name", chestNo: "101", teamName: "ZARQAN"}) { /* Re-used */
    const cfg = this.data.chestConfig;
    const box = document.getElementById("cc-preview");
    if(!box) return;

    const scale = 30; 
    box.style.width = (cfg.widthCm * scale) + "px";
    box.style.height = (cfg.heightCm * scale) + "px";
    box.style.backgroundColor = cfg.bgColor;
    
    box.innerHTML = ""; 

    const els = cfg.elements;
    
    const createEl = (key, content) => {
        if(!els[key].visible) return;
        const d = document.createElement("div");
        d.className = "cc-element";
        d.style.position = "absolute";
        d.style.top = els[key].y + "%";
        d.style.left = els[key].x + "%";
        d.style.transform = "translate(-50%, -50%)"; 
        d.style.fontSize = els[key].size + "px";
        d.style.fontWeight = els[key].bold ? "bold" : "normal";
        d.style.color = els[key].color;
        d.style.fontFamily = 'var(--font-body)';
        d.style.whiteSpace = 'nowrap';
        
        if(key === 'qr') {
            const qrDiv = document.createElement("div");
            qrDiv.style.padding = "2px";
            new QRCode(qrDiv, { text: content, width: els[key].size, height: els[key].size, colorDark: els[key].color, colorLight: 'transparent' });
            d.appendChild(qrDiv);
        } else {
            d.innerText = content;
        }
        box.appendChild(d);
    };

    createEl('fest', els.fest.text);
    createEl('name', student.name);
    createEl('chest', student.chestNo);
    createEl('team', student.teamName);
    createEl('qr', `ALIF-${student.chestNo}`);
  },
  printChestCards: function() { /* Re-used */
    const cfg = this.data.chestConfig;
    const pArea = document.getElementById("print-area");
    pArea.innerHTML = "";
    
    const style = document.createElement("style");
    style.innerHTML = `
        @media print { 
            .print-card { 
                width: ${cfg.widthCm}cm; height: ${cfg.heightCm}cm; 
                page-break-inside: avoid; display: inline-block; position: relative;
                border: 1px solid #ddd; background: ${cfg.bgColor}; margin: 0.5cm;
                overflow: hidden; text-align: center; 
            }
        }
    `;
    pArea.appendChild(style);

    const printableStudents = this.data.students.filter(s => s.chestNo);
    if(printableStudents.length === 0) {
        alert("No students with chest numbers found to print.");
        return;
    }

    printableStudents.forEach(s => {
        const t = this.data.teams.find(tm => tm.id === s.teamId);
        const card = document.createElement("div");
        card.className = "print-card";
        
        const els = cfg.elements;
        const add = (k, html) => {
            if(!els[k].visible) return;
            const d = document.createElement("div");
            d.style.position = "absolute";
            d.style.top = els[k].y + "%";
            d.style.left = els[k].x + "%";
            d.style.transform = "translate(-50%, -50%)";
            d.style.textAlign = "center";
            
            if(k!=='qr') {
                d.style.fontSize = (els[k].size * 0.7) + "pt"; 
                d.style.fontWeight = els[k].bold ? "bold" : "normal";
                d.style.color = els[k].color;
                d.style.whiteSpace = "nowrap";
                d.innerText = html;
            } else {
                 const qrSizePt = els[k].size * 0.7; 
                 const qrDiv = document.createElement("div");
                 qrDiv.style.padding = "2px"; // Padding to ensure QR code prints correctly
                 new QRCode(qrDiv, { text: `ALIF-${s.chestNo}`, width: qrSizePt, height: qrSizePt, colorDark: els[k].color, colorLight: 'transparent' });
                 d.appendChild(qrDiv);
            }
            card.appendChild(d);
        };
        
        add('fest', els.fest.text);
        add('name', s.name);
        add('chest', s.chestNo);
        add('team', t ? t.name : 'N/A');
        add('qr', '');

        pArea.appendChild(card);
    });

    window.print();
  },
  
  // Team Modules (re-used - not included here for brevity)
  renderTeamStudents: function(el) { /* Re-used */
    const myStudents = this.data.students.filter(s => s.teamId === this.state.user.id);
    
    el.innerHTML = `
      <div class="row">
        <h2>🧑‍🎓 My Students - ${this.state.user.name}</h2>
        <div style="flex:1"></div>
        <input class="input" style="width:250px" placeholder="🔍 Search Chest, Name, Category..." oninput="App.teamSearch(this.value)">
      </div>
      
      <div class="card">
        <h3>Add New Student</h3>
        <form class="grid cols-3" style="align-items:end" onsubmit="App.addStudent(event)">
           <div><label>Name</label><input class="input" id="s-name" placeholder="Full Name" required></div>
           <div><label>Chest No.</label><input class="input" id="s-chest" placeholder="e.g. 101, 250" required type="number"></div>
           <div><label>Category</label><select class="input" id="s-cat">${this.data.categories.map(c=>`<option>${c}</option>`).join('')}</select></div>
           <button class="btn primary sm">➕ Add</button>
        </form>
      </div>
      
      <div class="card">
        <h3>Current Students (${myStudents.length})</h3>
        <table id="student-table">
          <thead><tr><th>Chest No.</th><th>Name</th><th>Category</th><th>Action</th></tr></thead>
          <tbody>
            ${myStudents.map(s => this.studentRow(s)).join('')}
          </tbody>
        </table>
      </div>
    `;
  },
  studentRow: function(s) { /* Re-used */
    return `<tr>
      <td><span class="tag gold">#${s.chestNo}</span></td>
      <td><strong>${s.name}</strong></td>
      <td><span class="tag blue">${s.category}</span></td>
      <td><button class="btn sm danger" onclick="App.delStudent('${s.id}')">❌ Remove</button></td>
    </tr>`;
  },
  addStudent: function(e) { /* Re-used */
    e.preventDefault();
    const name = document.getElementById("s-name").value;
    const chest = document.getElementById("s-chest").value;
    const cat = document.getElementById("s-cat").value;
    
    if(this.data.students.find(s=>s.chestNo === chest)) return alert(`Chest Number ${chest} already exists! Please use a unique number.`);
    
    this.data.students.push({
        id: Date.now().toString(), teamId: this.state.user.id, name, chestNo: chest, category: cat
    });
    Store.save(this.data); this.renderTabContent();
  },
  delStudent: function(id) { /* Re-used */
    if(confirm("Remove student? All associated entries will also be removed.")) {
        this.data.students = this.data.students.filter(s=>s.id!==id);
        this.data.entries = this.data.entries.filter(e => !e.memberStudentIds.includes(id));
        Store.save(this.data); this.renderTabContent();
    }
  },
  teamSearch: function(q) { /* Re-used */
    q = q.toLowerCase();
    const myStudents = this.data.students.filter(s => s.teamId === this.state.user.id);
    const tbody = document.querySelector("#student-table tbody");
    tbody.innerHTML = myStudents.filter(s => 
        s.name.toLowerCase().includes(q) || s.chestNo.includes(q) || s.category.toLowerCase().includes(q)
    ).map(s => this.studentRow(s)).join('');
  },
  renderTeamEnroll: function(el) { /* Re-used */
    const myStudents = this.data.students.filter(s => s.teamId === this.state.user.id);
    
    el.innerHTML = `<h2>📝 Enrollment</h2><p>Enroll your eligible students in competitions.</p><div class="grid cols-3">
      ${this.data.competitions.map(c => {
        const enrolled = this.data.entries.filter(e => e.competitionId === c.id && e.teamId === this.state.user.id);
        
        const eligible = myStudents.filter(s => c.category === 'GENERAL' || s.category === c.category);

        return `<div class="card">
           <div class="row">
             <strong style="font-size:16px">${c.name}</strong> 
             <span class="tag blue">${c.category}</span>
             ${c.isStage ? '<span class="tag gold">Stage</span>' : ''}
           </div>
           <hr style="border:0; border-top:1px solid var(--border); margin:10px 0">
           
           <div style="margin-bottom:10px; min-height: 40px;">
             ${enrolled.map(e => {
                 const s = this.data.students.find(x => x.id === e.memberStudentIds[0]);
                 return `<span class="tag green" style="margin-right:5px; margin-bottom:5px; display:inline-block">
                    ${s.name} (#${s.chestNo}) <span style="cursor:pointer; margin-left:5px" onclick="App.unenroll('${e.id}')">&times;</span>
                 </span>`;
             }).join('')}
             ${enrolled.length === 0 ? '<p style="font-style:italic; color:#ccc; font-size:13px;">No students enrolled yet.</p>' : ''}
           </div>

           <form class="row" onsubmit="App.enroll(event, '${c.id}')">
             <select class="input sm" id="enr-${c.id}" ${eligible.length === 0 ? 'disabled' : ''}>
                ${eligible.length === 0 ? '<option>No eligible students</option>' : eligible.map(s => `<option value="${s.id}">${s.name} (${s.chestNo})</option>`).join('')}
             </select>
             <button class="btn sm primary" ${eligible.length === 0 ? 'disabled' : ''}>Enroll</button>
           </form>
        </div>`;
      }).join('')}
    </div>`;
  },
  enroll: function(e, cid) { /* Re-used */
    e.preventDefault();
    const sid = document.getElementById(`enr-${cid}`).value;
    if(!sid || sid === 'No eligible students') return alert("No student available or selected");
    
    const exists = this.data.entries.find(e => e.competitionId === cid && e.memberStudentIds.includes(sid));
    if(exists) return alert("Student already enrolled in this competition.");
    
    this.data.entries.push({
        id: Date.now().toString(), competitionId: cid, teamId: this.state.user.id, memberStudentIds: [sid]
    });
    Store.save(this.data); this.renderTabContent();
  },
  unenroll: function(eid) { /* Re-used */
    this.data.entries = this.data.entries.filter(e => e.id !== eid);
    Store.save(this.data); this.renderTabContent();
  },
  renderTeamSettings: function(el) { /* Re-used */
    el.innerHTML = `
      <h2>⚙️ Team Data Settings</h2>
      <div class="card">
        <h3>Team Password</h3>
        <p>Your current team password is: <span class="tag gray">${this.data.teams.find(t=>t.id===this.state.user.id)?.password || 'N/A'}</span></p>
        <form class="row" onsubmit="App.updateTeamPassword(event)">
           <input class="input" id="new-team-pass" type="text" placeholder="Enter New Password" required style="width:200px">
           <button class="btn primary">Update Password</button>
        </form>
      </div>
    `;
  },
  updateTeamPassword: function(e) { /* Re-used */
    e.preventDefault();
    const newPass = document.getElementById("new-team-pass").value;
    const team = this.data.teams.find(t=>t.id === this.state.user.id);
    if(team) {
        team.password = newPass;
        Store.save(this.data);
        alert(`Password for ${team.name} updated successfully!`);
        this.renderTabContent();
    }
  }
};

// Start App
App.init();
</script>
</body>
</html>
