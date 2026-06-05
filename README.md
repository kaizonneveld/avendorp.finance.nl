# avendorp.finance.nl
Flessen registratie
[index (4).html](https://github.com/user-attachments/files/28639003/index.4.html)
<!DOCTYPE html>
<html lang="nl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Wijnverdeling Overzicht</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg:        #0e1a12;
    --surface:   #162119;
    --surface2:  #1c2b20;
    --border:    #2a3d2e;
    --green:     #4ade80;
    --green-dim: #2d6a4f;
    --gold:      #d4a853;
    --gold-dim:  #7c5c1e;
    --text:      #e8f5e9;
    --muted:     #7a9b80;
    --red:       #f87171;
    --radius:    12px;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    line-height: 1.6;
    min-height: 100vh;
  }

  /* subtle noise overlay */
  body::before {
    content: '';
    position: fixed; inset: 0; pointer-events: none; z-index: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    opacity: .4;
  }

  .wrap { max-width: 1100px; margin: 0 auto; padding: 40px 24px 80px; position: relative; z-index: 1; }

  /* HEADER */
  header { margin-bottom: 48px; }
  .header-inner { display: flex; align-items: flex-end; justify-content: space-between; flex-wrap: wrap; gap: 16px; }
  .title-block {}
  .eyebrow {
    font-size: 11px; font-weight: 600; letter-spacing: .18em;
    text-transform: uppercase; color: var(--green); margin-bottom: 8px;
  }
  h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 5vw, 3.2rem);
    font-weight: 900; line-height: 1.1;
    background: linear-gradient(135deg, var(--text) 30%, var(--green));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .subtitle {
    margin-top: 10px; font-size: 13px; color: var(--muted);
    font-style: italic; max-width: 520px;
  }

  .last-updated {
    font-size: 12px; color: var(--muted);
    background: var(--surface); border: 1px solid var(--border);
    padding: 6px 14px; border-radius: 20px;
    display: flex; align-items: center; gap: 6px;
    white-space: nowrap;
  }
  .dot { width: 7px; height: 7px; border-radius: 50%; background: var(--green);
    box-shadow: 0 0 8px var(--green); animation: pulse 2s infinite; }
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.4} }

  /* EDIT TOGGLE */
  .toolbar {
    display: flex; align-items: center; gap: 12px;
    margin-bottom: 32px; flex-wrap: wrap;
  }
  .btn {
    padding: 9px 20px; border-radius: 8px; border: none; cursor: pointer;
    font-family: 'DM Sans', sans-serif; font-size: 13px; font-weight: 600;
    transition: all .2s;
  }
  .btn-edit {
    background: var(--green-dim); color: var(--green); border: 1px solid var(--green-dim);
  }
  .btn-edit:hover { background: var(--green); color: var(--bg); }
  .btn-edit.active { background: var(--green); color: var(--bg); }
  .btn-save { background: var(--gold-dim); color: var(--gold); border: 1px solid var(--gold-dim); display: none; }
  .btn-save:hover { background: var(--gold); color: var(--bg); }
  .edit-hint { font-size: 12px; color: var(--muted); display: none; }

  /* STAT CARDS */
  .stats-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 16px; margin-bottom: 40px;
  }
  .stat-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: var(--radius); padding: 20px 22px;
    transition: border-color .2s;
  }
  .stat-card:hover { border-color: var(--green-dim); }
  .stat-label { font-size: 11px; font-weight: 600; letter-spacing: .1em; text-transform: uppercase; color: var(--muted); margin-bottom: 6px; }
  .stat-value { font-family: 'Playfair Display', serif; font-size: 2rem; font-weight: 700; color: var(--green); }
  .stat-value.gold { color: var(--gold); }
  .stat-sub { font-size: 12px; color: var(--muted); margin-top: 2px; }

  /* SECTION */
  .section { margin-bottom: 36px; }
  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.1rem; font-weight: 700;
    color: var(--green); margin-bottom: 14px;
    display: flex; align-items: center; gap: 10px;
  }
  .section-title::after { content: ''; flex: 1; height: 1px; background: var(--border); }

  /* TABLES */
  .table-wrap { overflow-x: auto; border-radius: var(--radius); border: 1px solid var(--border); }
  table { width: 100%; border-collapse: collapse; }
  thead th {
    background: var(--surface2); padding: 12px 16px;
    font-size: 11px; font-weight: 600; letter-spacing: .1em;
    text-transform: uppercase; color: var(--muted); text-align: right;
    white-space: nowrap;
  }
  thead th:first-child { text-align: left; }
  tbody tr { border-top: 1px solid var(--border); transition: background .15s; }
  tbody tr:hover { background: var(--surface2); }
  tbody td { padding: 12px 16px; text-align: right; font-size: 14px; color: var(--text); }
  tbody td:first-child { text-align: left; font-weight: 500; }

  .wijn-badge {
    display: inline-flex; align-items: center; gap: 7px;
    font-weight: 600;
  }
  .wijn-dot { width: 9px; height: 9px; border-radius: 50%; flex-shrink: 0; }
  .parel-dot    { background: #93c5fd; }
  .joha-dot     { background: #86efac; }
  .barrique-dot { background: #d4a853; }

  tfoot td {
    padding: 13px 16px; font-weight: 700; font-size: 14px;
    background: var(--surface2); border-top: 2px solid var(--green-dim);
    color: var(--green); text-align: right;
  }
  tfoot td:first-child { text-align: left; }

  .calc { color: var(--green); font-weight: 600; }
  .cost { color: var(--red); }

  /* Editable inputs */
  .editable { display: none; }
  body.edit-mode .editable { display: inline-block; }
  body.edit-mode .readonly { display: none; }
  .readonly { display: inline-block; }

  input.num-input {
    background: transparent; border: none; border-bottom: 1px solid var(--green-dim);
    color: var(--text); font-family: 'DM Sans', sans-serif; font-size: 14px;
    font-weight: 500; text-align: right; width: 80px; padding: 2px 4px;
    outline: none; transition: border-color .2s;
  }
  input.num-input:focus { border-bottom-color: var(--green); }

  /* VERKOOP DETAIL */
  .verkoop-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; }
  .vk-card {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: var(--radius); overflow: hidden;
  }
  .vk-card-header {
    padding: 14px 18px; display: flex; align-items: center; gap: 10px;
    border-bottom: 1px solid var(--border); background: var(--surface2);
  }
  .vk-card-title { font-weight: 700; font-size: 15px; }
  .vk-card-body { padding: 0; }
  .vk-row {
    display: flex; justify-content: space-between; align-items: center;
    padding: 10px 18px; border-bottom: 1px solid var(--border); font-size: 14px;
    transition: background .15s;
  }
  .vk-row:last-child { border-bottom: none; }
  .vk-row:hover { background: var(--surface2); }
  .vk-row.total {
    background: var(--surface2); font-weight: 700;
    border-top: 2px solid var(--green-dim);
  }
  .vk-label { color: var(--muted); font-size: 13px; }
  .vk-nums { display: flex; gap: 24px; text-align: right; }
  .vk-fl { min-width: 44px; color: var(--text); }
  .vk-eu { min-width: 80px; }
  .vk-eu.pos { color: var(--green); }
  .vk-eu.neg { color: var(--red); }
  .vk-col-hdr { font-size: 11px; font-weight: 600; text-transform: uppercase; letter-spacing: .08em; color: var(--muted); }

  /* FOOTER */
  footer { text-align: center; margin-top: 60px; font-size: 12px; color: var(--muted); }

  /* ANIMATIONS */
  .fade-in { opacity: 0; transform: translateY(16px); animation: fadeUp .5s ease forwards; }
  @keyframes fadeUp { to { opacity: 1; transform: none; } }
  .fade-in:nth-child(1){animation-delay:.05s}
  .fade-in:nth-child(2){animation-delay:.1s}
  .fade-in:nth-child(3){animation-delay:.15s}
  .fade-in:nth-child(4){animation-delay:.2s}
  .fade-in:nth-child(5){animation-delay:.25s}

  @media(max-width:600px){
    .stats-grid{grid-template-columns:1fr 1fr}
    .verkoop-grid{grid-template-columns:1fr}
    h1{font-size:1.8rem}
  }
</style>
</head>
<body>
<div class="wrap">

  <!-- HEADER -->
  <header class="fade-in">
    <div class="header-inner">
      <div class="title-block">
        <div class="eyebrow">🍷 Wijncoöperatie &mdash; Seizoen 2024</div>
        <h1>Wijnverdeling<br>Overzicht</h1>
        <p class="subtitle">20% Geert: 725 L / 967 flessen = 193 flessen &mdash; zie app contact 7 december</p>
      </div>
      <div class="last-updated">
        <span class="dot"></span>
        Live &mdash; <span id="ts"></span>
      </div>
    </div>
  </header>

  <!-- TOOLBAR -->
  <div class="toolbar fade-in">
    <button class="btn btn-edit" id="editBtn" onclick="toggleEdit()">✏️ Bewerken</button>
    <button class="btn btn-save" id="saveBtn" onclick="saveData()">💾 Opslaan & Delen</button>
    <span class="edit-hint" id="editHint">Pas getallen aan — berekeningen updaten live</span>
  </div>

  <!-- KPI CARDS -->
  <div class="stats-grid fade-in" id="kpiGrid"></div>

  <!-- KOSTPRIJS -->
  <div class="section fade-in">
    <div class="section-title">Kostprijs per Fles</div>
    <div class="table-wrap">
      <table id="kostprijsTable">
        <thead>
          <tr>
            <th>Wijn</th>
            <th>Flessen</th>
            <th>Prijs p/fles</th>
            <th>Extra</th>
            <th>Accijns + Transport</th>
            <th>Etiket</th>
            <th>Wax</th>
            <th>Totaal incl. btw</th>
          </tr>
        </thead>
        <tbody id="kostprijsBody"></tbody>
      </table>
    </div>
  </div>

  <!-- VERKOOPVERDELING -->
  <div class="section fade-in">
    <div class="section-title">Verkoopverdeling</div>
    <div class="table-wrap">
      <table id="verdelingTable">
        <thead>
          <tr>
            <th>Wijn</th>
            <th>Totaal flessen</th>
            <th>Geert</th>
            <th>Wijngenoten</th>
            <th>Voor verkoop</th>
            <th>Prijs p/fles</th>
            <th>Verwachte omzet</th>
          </tr>
        </thead>
        <tbody id="verdelingBody"></tbody>
        <tfoot id="verdelingFoot"></tfoot>
      </table>
    </div>
  </div>

  <!-- VERKOOP DETAIL -->
  <div class="section fade-in">
    <div class="section-title">Verkoop Detail per Wijn</div>
    <div class="verkoop-grid" id="verkoopDetail"></div>
  </div>

  <footer>
    Wijnverdeling Dashboard &mdash; automatisch berekend op basis van ingevoerde gegevens
  </footer>
</div>

<script>
// ─── DATA MODEL ───────────────────────────────────────────────────────────────
const defaultData = {
  wines: [
    { id:'parel',      name:'Parel',      flessen:1330, prijs:4.64,  extra:0,    accijns:0.819, etiket:1.382, wax:0.5,  geert:30,  wijngenoten:267,
      verkoop:[
        {label:'Totaal flessen', cat:'totaal'},
        {label:'Geert',          cat:'geert'},
        {label:'Wijngenoten',    cat:'wijngenoten'},
        {label:'STIEL gasten',   fl:110,  prijs_override:null},
        {label:'STIEL verkoop',  fl:308,  prijs_override:27.5},
        {label:'Sponsoring Fels',fl:24,   prijs_override:null},
      ]
    },
    { id:'johanniter', name:'Johanniter', flessen:660,  prijs:4.13,  extra:0,    accijns:0,     etiket:0,     wax:0,    geert:112, wijngenoten:337,
      verkoop:[
        {label:'Totaal flessen', cat:'totaal'},
        {label:'Geert',          cat:'geert'},
        {label:'Wijngenoten',    cat:'wijngenoten'},
        {label:'STIEL verkoop',  fl:0,    prijs_override:27.5},
      ]
    },
    { id:'barrique',   name:'Barrique',   flessen:300,  prijs:6.03,  extra:0,    accijns:0,     etiket:0,     wax:0,    geert:51,  wijngenoten:0,
      verkoop:[
        {label:'Totaal flessen', cat:'totaal'},
        {label:'Geert',          cat:'geert'},
        {label:'Wijngenoten',    cat:'wijngenoten'},
      ]
    },
  ]
};

const COLORS = { parel:'#93c5fd', johanniter:'#86efac', barrique:'#d4a853' };
const BTW = 1.21;

// Load from localStorage or use defaults
let data = JSON.parse(localStorage.getItem('wijndata') || 'null') || defaultData;

// ─── CALCULATIONS ─────────────────────────────────────────────────────────────
function calcTotaalPrijs(w) {
  return (w.prijs + (w.extra||0) + (w.accijns||0) + (w.etiket||0) + (w.wax||0)) * BTW;
}

function calcVoorVerkoop(w) {
  return w.flessen - w.geert - w.wijngenoten;
}

function calcOmzet(w) {
  return calcVoorVerkoop(w) * w.verkoopprijs;
}

function calcVerkoopRows(w) {
  const totaalPrijs = calcTotaalPrijs(w);
  const rows = [];
  for (const v of w.verkoop) {
    if (v.cat === 'totaal') {
      rows.push({ label: v.label, fl: w.flessen, euro: -w.flessen * totaalPrijs });
    } else if (v.cat === 'geert') {
      rows.push({ label: v.label, fl: w.geert, euro: 0 });
    } else if (v.cat === 'wijngenoten') {
      rows.push({ label: v.label, fl: w.wijngenoten, euro: 0 });
    } else {
      const p = v.prijs_override !== null ? v.prijs_override : totaalPrijs;
      rows.push({ label: v.label, fl: v.fl, euro: v.fl * p });
    }
  }
  return rows;
}

// ─── RENDER ───────────────────────────────────────────────────────────────────
function eur(n) {
  if (n === '' || n === null || n === undefined) return '—';
  return new Intl.NumberFormat('nl-NL', {style:'currency', currency:'EUR'}).format(n);
}
function num(n) {
  if (n === '' || n === null || n === undefined) return '—';
  return new Intl.NumberFormat('nl-NL').format(n);
}

function editableNum(val, path, fmt='eur') {
  return `<span class="readonly">${fmt==='eur'?eur(val):num(val)}</span>`
       + `<input class="num-input editable" value="${val}" data-path="${path}" data-fmt="${fmt}" oninput="updateValue(this)">`;
}

function renderAll() {
  renderKPIs();
  renderKostprijs();
  renderVerdeling();
  renderVerkoopDetail();
  document.getElementById('ts').textContent = new Date().toLocaleString('nl-NL', {day:'2-digit',month:'short',hour:'2-digit',minute:'2-digit'});
}

function renderKPIs() {
  const totalFlessen = data.wines.reduce((s,w)=>s+w.flessen, 0);
  const totalGeert   = data.wines.reduce((s,w)=>s+w.geert, 0);
  const totalWg      = data.wines.reduce((s,w)=>s+w.wijngenoten, 0);
  const totalVk      = data.wines.reduce((s,w)=>s+calcVoorVerkoop(w), 0);
  const totalOmzet   = data.wines.reduce((s,w)=>{
    const vk = calcVerkoopRows(w);
    return s + vk.filter(r=>r.euro>0).reduce((a,r)=>a+r.euro,0);
  }, 0);

  document.getElementById('kpiGrid').innerHTML = [
    {label:'Totaal flessen', value:num(totalFlessen), sub:'alle wijnen', gold:false},
    {label:'Geert',          value:num(totalGeert),   sub:'20% aandeel', gold:false},
    {label:'Wijngenoten',    value:num(totalWg),      sub:'leden verdeling', gold:false},
    {label:'Voor verkoop',   value:num(totalVk),      sub:'beschikbaar', gold:false},
    {label:'Verwachte omzet',value:eur(totalOmzet),   sub:'excl. kosten', gold:true},
  ].map(k=>`
    <div class="stat-card">
      <div class="stat-label">${k.label}</div>
      <div class="stat-value ${k.gold?'gold':''}">${k.value}</div>
      <div class="stat-sub">${k.sub}</div>
    </div>
  `).join('');
}

function renderKostprijs() {
  const tbody = document.getElementById('kostprijsBody');
  tbody.innerHTML = data.wines.map((w,wi)=>{
    const tp = calcTotaalPrijs(w);
    return `<tr>
      <td><span class="wijn-badge"><span class="wijn-dot" style="background:${COLORS[w.id]}"></span>${w.name}</span></td>
      <td>${editableNum(w.flessen, `wines.${wi}.flessen`, 'int')}</td>
      <td>${editableNum(w.prijs,   `wines.${wi}.prijs`)}</td>
      <td>${editableNum(w.extra||0,`wines.${wi}.extra`)}</td>
      <td>${editableNum(w.accijns||0,`wines.${wi}.accijns`)}</td>
      <td>${editableNum(w.etiket||0,`wines.${wi}.etiket`)}</td>
      <td>${editableNum(w.wax||0,  `wines.${wi}.wax`)}</td>
      <td class="calc">${eur(tp)}</td>
    </tr>`;
  }).join('');
}

function renderVerdeling() {
  const tbody = document.getElementById('verdelingBody');
  const tfoot = document.getElementById('verdelingFoot');

  tbody.innerHTML = data.wines.map((w,wi)=>{
    const vvk = calcVoorVerkoop(w);
    const vp  = w.verkoopprijs || 0;
    const omz = vvk * vp;
    return `<tr>
      <td><span class="wijn-badge"><span class="wijn-dot" style="background:${COLORS[w.id]}"></span>${w.name}</span></td>
      <td>${num(w.flessen)}</td>
      <td>${editableNum(w.geert,`wines.${wi}.geert`,'int')}</td>
      <td>${editableNum(w.wijngenoten,`wines.${wi}.wijngenoten`,'int')}</td>
      <td class="calc">${num(vvk)}</td>
      <td>${editableNum(vp,`wines.${wi}.verkoopprijs`)}</td>
      <td class="calc">${eur(omz)}</td>
    </tr>`;
  }).join('');

  const tF=data.wines.reduce((s,w)=>s+w.flessen,0);
  const tG=data.wines.reduce((s,w)=>s+w.geert,0);
  const tW=data.wines.reduce((s,w)=>s+w.wijngenoten,0);
  const tV=data.wines.reduce((s,w)=>s+calcVoorVerkoop(w),0);
  const tO=data.wines.reduce((s,w)=>s+(calcVoorVerkoop(w)*(w.verkoopprijs||0)),0);

  tfoot.innerHTML = `<tr>
    <td>TOTAAL</td>
    <td>${num(tF)}</td>
    <td>${num(tG)}</td>
    <td>${num(tW)}</td>
    <td>${num(tV)}</td>
    <td>—</td>
    <td>${eur(tO)}</td>
  </tr>`;
}

function renderVerkoopDetail() {
  const container = document.getElementById('verkoopDetail');
  container.innerHTML = data.wines.map(w=>{
    const rows = calcVerkoopRows(w);
    const totFlessen = rows.reduce((s,r)=> r.label==='Totaal flessen'?s:s+r.fl, 0);
    // actually sum non-totaal
    const verkFlessen = rows.filter(r=>r.label!=='Totaal flessen').reduce((s,r)=>s+r.fl,0);
    const totEuro = rows.reduce((s,r)=>s+r.euro,0);

    const rowsHtml = rows.map(r=>{
      const isTotal = r.label==='Totaal flessen';
      const euClass = r.euro<0?'neg':r.euro>0?'pos':'';
      return `<div class="vk-row${isTotal?' total':''}">
        <span class="vk-label">${r.label}</span>
        <div class="vk-nums">
          <span class="vk-fl">${num(r.fl)}</span>
          <span class="vk-eu ${euClass}">${eur(r.euro)}</span>
        </div>
      </div>`;
    }).join('');

    const totClass = totEuro >= 0 ? 'pos' : 'neg';
    return `
      <div class="vk-card">
        <div class="vk-card-header">
          <span class="wijn-dot" style="background:${COLORS[w.id]}; width:12px; height:12px; border-radius:50%; display:inline-block;"></span>
          <span class="vk-card-title">${w.name}</span>
        </div>
        <div class="vk-card-body">
          <div class="vk-row" style="background:var(--surface2); border-bottom:1px solid var(--border)">
            <span class="vk-label vk-col-hdr">Categorie</span>
            <div class="vk-nums">
              <span class="vk-fl vk-col-hdr">Fl.</span>
              <span class="vk-eu vk-col-hdr">Euro</span>
            </div>
          </div>
          ${rowsHtml}
          <div class="vk-row total">
            <span style="color:var(--green)">SALDO</span>
            <div class="vk-nums">
              <span class="vk-fl">${num(w.flessen - verkFlessen)}</span>
              <span class="vk-eu ${totClass}">${eur(totEuro)}</span>
            </div>
          </div>
        </div>
      </div>`;
  }).join('');
}

// ─── EDIT MODE ────────────────────────────────────────────────────────────────
let editMode = false;

function toggleEdit() {
  editMode = !editMode;
  document.body.classList.toggle('edit-mode', editMode);
  document.getElementById('editBtn').classList.toggle('active', editMode);
  document.getElementById('editBtn').textContent = editMode ? '👁 Bekijken' : '✏️ Bewerken';
  document.getElementById('saveBtn').style.display = editMode ? 'inline-block' : 'none';
  document.getElementById('editHint').style.display = editMode ? 'inline' : 'none';
}

function updateValue(input) {
  const path = input.dataset.path.split('.');
  const val = parseFloat(input.value) || 0;
  let obj = data;
  for (let i = 0; i < path.length - 1; i++) {
    obj = isNaN(path[i]) ? obj[path[i]] : obj[parseInt(path[i])];
  }
  const last = path[path.length-1];
  obj[isNaN(last) ? last : parseInt(last)] = val;
  renderAll();
  // re-attach inputs so they stay in sync
  // restore focus
  setTimeout(()=>{
    const inputs = document.querySelectorAll(`[data-path="${input.dataset.path}"]`);
    inputs.forEach(el => { if(el.tagName==='INPUT') el.focus(); });
  }, 10);
}

function saveData() {
  localStorage.setItem('wijndata', JSON.stringify(data));
  const btn = document.getElementById('saveBtn');
  btn.textContent = '✅ Opgeslagen!';
  setTimeout(()=>btn.textContent='💾 Opslaan & Delen', 2000);
}

// ─── INIT ─────────────────────────────────────────────────────────────────────

// Set default verkoopprijs if not set
data.wines.forEach((w, i) => {
  if (!w.verkoopprijs) {
    w.verkoopprijs = [27.5, 35, 35][i] || 0;
  }
});

renderAll();

// Auto-refresh timestamp every minute
setInterval(()=>{
  document.getElementById('ts').textContent = new Date().toLocaleString('nl-NL', {day:'2-digit',month:'short',hour:'2-digit',minute:'2-digit'});
}, 60000);
</script>
</body>
</html>
