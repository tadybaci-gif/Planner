# index.html
<!DOCTYPE html>

<html lang="cs">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>🐱 Můj Planner</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #1a1118;
  --surface: #251a22;
  --surface2: #2e2029;
  --border: #3d2e3a;
  --border2: #5a3f55;
  --text: #f5ece8;
  --muted: #9a7f93;
  --pink: #e8628a;
  --pink-soft: #c4506d;
  --rose: #f0a0b8;
  --gold: #d4a76a;
  --sage: #7ab89a;
  --lavender: #b09ad4;
  --cream: #f5e6d8;
}

- { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
font-family: ‘DM Sans’, sans-serif;
background: var(–bg);
color: var(–text);
min-height: 100vh;
overflow-x: hidden;
}

/* ── BG decoration ── */
body::before {
content: ‘’;
position: fixed;
inset: 0;
background:
radial-gradient(ellipse 60% 50% at 80% 10%, rgba(232,98,138,0.12) 0%, transparent 60%),
radial-gradient(ellipse 50% 40% at 10% 80%, rgba(176,154,212,0.1) 0%, transparent 60%);
pointer-events: none;
z-index: 0;
}

/* ── NAV ── */
nav {
position: sticky;
top: 0;
z-index: 100;
background: rgba(26,17,24,0.85);
backdrop-filter: blur(16px);
border-bottom: 1px solid var(–border);
display: flex;
align-items: center;
justify-content: space-between;
padding: 0.8rem 1.5rem;
gap: 1rem;
}

.nav-brand {
font-family: ‘Playfair Display’, serif;
font-size: 1.15rem;
color: var(–rose);
font-style: italic;
display: flex;
align-items: center;
gap: 0.5rem;
white-space: nowrap;
}

.nav-tabs {
display: flex;
gap: 0.3rem;
background: var(–surface);
border-radius: 12px;
padding: 0.3rem;
border: 1px solid var(–border);
overflow-x: auto;
scrollbar-width: none;
}
.nav-tabs::-webkit-scrollbar { display: none; }

.nav-tab {
padding: 0.4rem 0.9rem;
border-radius: 9px;
border: none;
background: transparent;
color: var(–muted);
font-family: ‘DM Sans’, sans-serif;
font-size: 0.82rem;
font-weight: 500;
cursor: pointer;
transition: all 0.2s;
white-space: nowrap;
}
.nav-tab.active {
background: var(–pink);
color: white;
box-shadow: 0 2px 10px rgba(232,98,138,0.35);
}
.nav-tab:hover:not(.active) { color: var(–text); background: var(–surface2); }

/* ── MAIN ── */
main {
position: relative;
z-index: 1;
max-width: 840px;
margin: 0 auto;
padding: 1.5rem 1rem 5rem;
}

/* ── SECTION ── */
.section { display: none; }
.section.active { display: block; animation: fadeUp 0.3s ease; }
@keyframes fadeUp { from{opacity:0;transform:translateY(12px)} to{opacity:1;transform:translateY(0)} }

/* ── HEADER CARD ── */
.hero {
background: linear-gradient(135deg, rgba(232,98,138,0.18), rgba(176,154,212,0.12));
border: 1px solid rgba(232,98,138,0.25);
border-radius: 24px;
padding: 2rem;
text-align: center;
margin-bottom: 1.5rem;
position: relative;
overflow: hidden;
}
.hero::before {
content: ‘’;
position: absolute;
top: -30px; right: -30px;
width: 150px; height: 150px;
background: radial-gradient(circle, rgba(232,98,138,0.2), transparent 70%);
border-radius: 50%;
}
.hero-cat {
font-size: 3rem;
display: block;
animation: floatCat 3s ease-in-out infinite;
margin-bottom: 0.5rem;
}
@keyframes floatCat { 0%,100%{transform:translateY(0) rotate(-3deg)} 50%{transform:translateY(-10px) rotate(3deg)} }

.hero h1 {
font-family: ‘Playfair Display’, serif;
font-size: 2rem;
font-weight: 700;
line-height: 1.2;
}
.hero h1 em { color: var(–rose); }
.hero p { color: var(–muted); font-size: 0.9rem; margin-top: 0.4rem; }

/* Deadline strip inside hero */
.deadline-strip {
display: flex;
align-items: center;
justify-content: center;
gap: 1.5rem;
flex-wrap: wrap;
margin-top: 1.2rem;
padding-top: 1.2rem;
border-top: 1px solid var(–border);
}
.dl-input-wrap { display: flex; flex-direction: column; align-items: center; gap: 0.2rem; }
.dl-label { font-size: 0.72rem; color: var(–muted); text-transform: uppercase; letter-spacing: 1px; }
.dl-input {
background: var(–surface);
border: 1px solid var(–border2);
border-radius: 10px;
color: var(–text);
font-family: ‘DM Sans’, sans-serif;
font-size: 0.9rem;
padding: 0.4rem 0.8rem;
cursor: pointer;
}
.dl-input::-webkit-calendar-picker-indicator { filter: invert(0.7); }

.countdown-wrap { display: flex; gap: 0.8rem; }
.count-box {
background: rgba(232,98,138,0.15);
border: 1px solid rgba(232,98,138,0.3);
border-radius: 12px;
padding: 0.5rem 1rem;
text-align: center;
}
.count-num {
font-family: ‘Playfair Display’, serif;
font-size: 1.8rem;
font-weight: 700;
color: var(–rose);
display: block;
line-height: 1;
}
.count-lbl { font-size: 0.65rem; color: var(–muted); text-transform: uppercase; letter-spacing: 0.5px; }

/* ── PROGRESS GRID ── */
.prog-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px,1fr)); gap: 0.8rem; margin-bottom: 1.5rem; }
.prog-card {
background: var(–surface);
border: 1px solid var(–border);
border-radius: 16px;
padding: 1rem;
transition: border-color 0.2s, transform 0.2s;
}
.prog-card:hover { border-color: var(–border2); transform: translateY(-2px); }
.prog-lbl { font-size: 0.72rem; color: var(–muted); text-transform: uppercase; letter-spacing: 0.8px; }
.prog-val { font-family: ‘Playfair Display’, serif; font-size: 1.6rem; color: var(–pink); margin: 0.2rem 0; }
.prog-bar-bg { height: 4px; background: var(–border); border-radius: 99px; overflow: hidden; }
.prog-bar-fg { height: 100%; background: linear-gradient(90deg, var(–pink-soft), var(–rose)); border-radius: 99px; transition: width 0.5s ease; }
.prog-slider { width: 100%; margin-top: 0.6rem; accent-color: var(–pink); }

/* ── PANELS ── */
.panel {
background: var(–surface);
border: 1px solid var(–border);
border-radius: 20px;
padding: 1.3rem;
margin-bottom: 1rem;
}
.panel-title {
font-family: ‘Playfair Display’, serif;
font-size: 1.05rem;
margin-bottom: 1rem;
display: flex;
align-items: center;
gap: 0.5rem;
color: var(–text);
}

/* ── ADD ROW ── */
.add-row { display: flex; gap: 0.5rem; margin-bottom: 0.9rem; flex-wrap: wrap; }
.inp {
font-family: ‘DM Sans’, sans-serif;
font-size: 0.88rem;
background: var(–surface2);
border: 1px solid var(–border);
border-radius: 10px;
color: var(–text);
padding: 0.5rem 0.8rem;
outline: none;
transition: border-color 0.2s;
}
.inp:focus { border-color: var(–pink); }
.inp::placeholder { color: var(–muted); }
.inp-grow { flex: 1; min-width: 120px; }

.btn-add {
background: var(–pink);
color: white;
border: none;
border-radius: 10px;
padding: 0.5rem 1.1rem;
font-family: ‘DM Sans’, sans-serif;
font-size: 0.88rem;
font-weight: 500;
cursor: pointer;
transition: all 0.2s;
box-shadow: 0 3px 12px rgba(232,98,138,0.3);
flex-shrink: 0;
}
.btn-add:hover { background: var(–pink-soft); transform: translateY(-1px); }

/* ── LIST ── */
.scroll-list { display: flex; flex-direction: column; gap: 0.45rem; max-height: 300px; overflow-y: auto; padding-right: 4px; }
.scroll-list::-webkit-scrollbar { width: 3px; }
.scroll-list::-webkit-scrollbar-track { background: transparent; }
.scroll-list::-webkit-scrollbar-thumb { background: var(–border2); border-radius: 99px; }

.item {
display: flex;
align-items: center;
gap: 0.6rem;
padding: 0.6rem 0.8rem;
background: var(–surface2);
border: 1px solid transparent;
border-radius: 12px;
transition: all 0.2s;
animation: slideIn 0.25s ease;
}
@keyframes slideIn { from{opacity:0;transform:translateX(-8px)} to{opacity:1;transform:translateX(0)} }
.item:hover { border-color: var(–border2); }
.item.done { opacity: 0.45; }
.item.done .item-text { text-decoration: line-through; }

.check {
width: 20px; height: 20px;
border: 2px solid var(–border2);
border-radius: 6px;
cursor: pointer;
display: flex; align-items: center; justify-content: center;
flex-shrink: 0;
transition: all 0.2s;
}
.check.on { background: var(–pink); border-color: var(–pink); }
.check.on::after { content: ‘✓’; color: white; font-size: 11px; font-weight: 700; }

.item-text { flex: 1; font-size: 0.87rem; line-height: 1.4; }

.tag {
font-size: 0.68rem;
padding: 0.15rem 0.5rem;
border-radius: 99px;
font-weight: 500;
flex-shrink: 0;
}
.tag-prace    { background: rgba(232,98,138,0.2); color: var(–rose); }
.tag-skola    { background: rgba(212,167,106,0.2); color: var(–gold); }
.tag-osobni   { background: rgba(122,184,154,0.2); color: var(–sage); }
.tag-kreativa { background: rgba(176,154,212,0.2); color: var(–lavender); }

.del-btn {
background: none; border: none; color: var(–muted);
cursor: pointer; font-size: 0.85rem; opacity: 0;
transition: opacity 0.2s, color 0.2s;
padding: 0.1rem 0.2rem; flex-shrink: 0;
}
.item:hover .del-btn { opacity: 1; }
.del-btn:hover { color: var(–pink); }

.empty { text-align: center; color: var(–muted); font-size: 0.85rem; padding: 1.5rem; font-style: italic; }

/* ── MILESTONE ── */
.ms-item {
display: flex;
align-items: flex-start;
gap: 0.7rem;
padding: 0.7rem 0.8rem;
background: var(–surface2);
border: 1px solid transparent;
border-radius: 12px;
transition: all 0.2s;
animation: slideIn 0.25s ease;
}
.ms-item:hover { border-color: var(–border2); }
.ms-item.done { opacity: 0.45; }
.ms-item.done .ms-name { text-decoration: line-through; }

.ms-dot {
width: 14px; height: 14px;
border-radius: 50%;
border: 2px solid var(–sage);
flex-shrink: 0; margin-top: 3px;
cursor: pointer; transition: all 0.2s;
}
.ms-dot.on { background: var(–sage); }
.ms-info { flex: 1; }
.ms-name { font-size: 0.87rem; font-weight: 500; }
.ms-date { font-size: 0.73rem; color: var(–muted); margin-top: 0.15rem; }
.ms-date.overdue { color: var(–pink); font-weight: 500; }

/* ── NOTES ── */
.note-tabs { display: flex; gap: 0.4rem; margin-bottom: 0.8rem; }
.note-tab-btn {
padding: 0.35rem 0.9rem;
border-radius: 99px;
border: 1px solid var(–border);
background: transparent;
color: var(–muted);
font-family: ‘DM Sans’, sans-serif;
font-size: 0.8rem;
cursor: pointer; transition: all 0.2s;
}
.note-tab-btn.active { background: var(–pink); color: white; border-color: var(–pink); }

.textarea {
width: 100%; min-height: 180px;
font-family: ‘DM Sans’, sans-serif; font-size: 0.9rem;
background: var(–surface2); border: 1px solid var(–border);
border-radius: 12px; color: var(–text);
padding: 0.9rem; resize: vertical; outline: none; line-height: 1.7;
transition: border-color 0.2s;
}
.textarea:focus { border-color: var(–pink); }
.textarea::placeholder { color: var(–muted); }

/* ── MOODBOARD ── */
.mood-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(120px,1fr)); gap: 0.7rem; margin-bottom: 1rem; }
.mood-card {
background: var(–surface2);
border: 1px solid var(–border);
border-radius: 14px;
padding: 0.6rem;
text-align: center;
position: relative;
transition: all 0.2s;
animation: slideIn 0.25s ease;
}
.mood-card:hover { border-color: var(–border2); transform: translateY(-2px); }
.mood-emoji { font-size: 2.2rem; display: block; margin-bottom: 0.3rem; }
.mood-label { font-size: 0.75rem; color: var(–muted); }
.mood-del {
position: absolute; top: 0.3rem; right: 0.4rem;
background: none; border: none; color: var(–muted);
cursor: pointer; font-size: 0.8rem; opacity: 0; transition: opacity 0.2s;
}
.mood-card:hover .mood-del { opacity: 1; }

.color-swatch {
width: 100%; height: 80px;
border-radius: 10px; margin-bottom: 0.4rem;
position: relative;
cursor: pointer;
}
.swatch-del {
position: absolute; top: 0.3rem; right: 0.3rem;
background: rgba(0,0,0,0.5); border: none; color: white;
border-radius: 50%; width: 18px; height: 18px;
font-size: 0.65rem; cursor: pointer; display: none;
align-items: center; justify-content: center;
}
.mood-card:hover .swatch-del { display: flex; }

.mood-add-row { display: flex; gap: 0.5rem; flex-wrap: wrap; align-items: center; }
.mood-emoji-inp { font-size: 1.2rem; width: 55px; text-align: center; }

/* keyword chips */
.chips-wrap { display: flex; flex-wrap: wrap; gap: 0.4rem; margin-top: 0.7rem; }
.chip {
background: rgba(176,154,212,0.15);
border: 1px solid rgba(176,154,212,0.3);
color: var(–lavender);
border-radius: 99px;
padding: 0.25rem 0.7rem;
font-size: 0.78rem;
display: flex; align-items: center; gap: 0.4rem;
animation: slideIn 0.2s ease;
}
.chip-del { background: none; border: none; color: var(–lavender); cursor: pointer; font-size: 0.75rem; line-height: 1; }

/* ── CAT ── */
.cat-widget {
text-align: center;
background: linear-gradient(135deg, rgba(232,98,138,0.12), rgba(176,154,212,0.1));
border: 1px solid rgba(232,98,138,0.2);
border-radius: 20px;
padding: 1.5rem;
}
.cat-big { font-size: 3.5rem; display: block; animation: floatCat 2.5s ease-in-out infinite; margin-bottom: 0.5rem; }
.cat-quote { font-size: 0.92rem; color: var(–muted); font-style: italic; line-height: 1.5; max-width: 340px; margin: 0 auto; }
.cat-quote strong { color: var(–rose); font-style: normal; }
.btn-cat {
margin-top: 1rem;
background: rgba(232,98,138,0.2);
border: 1px solid rgba(232,98,138,0.35);
color: var(–rose);
font-family: ‘DM Sans’, sans-serif;
font-size: 0.82rem;
font-weight: 500;
border-radius: 99px;
padding: 0.4rem 1.1rem;
cursor: pointer;
transition: all 0.2s;
}
.btn-cat:hover { background: rgba(232,98,138,0.3); }

/* ── STATS ── */
.stats-row { display: flex; flex-wrap: wrap; gap: 0.8rem; margin-bottom: 1.5rem; }
.stat-pill {
background: var(–surface2);
border: 1px solid var(–border);
border-radius: 99px;
padding: 0.45rem 1rem;
font-size: 0.82rem;
color: var(–muted);
}
.stat-pill strong { color: var(–text); }

/* ── RESPONSIVE ── */
@media (max-width: 480px) {
nav { padding: 0.7rem 1rem; }
.hero h1 { font-size: 1.5rem; }
.count-num { font-size: 1.4rem; }
}
</style>

</head>
<body>

<nav>
  <div class="nav-brand">🐱 Planner</div>
  <div class="nav-tabs">
    <button class="nav-tab active" onclick="showSection('home',this)">🏠 Domů</button>
    <button class="nav-tab" onclick="showSection('todo',this)">📌 Úkoly</button>
    <button class="nav-tab" onclick="showSection('plan',this)">🗓️ Plán</button>
    <button class="nav-tab" onclick="showSection('notes',this)">💭 Poznámky</button>
    <button class="nav-tab" onclick="showSection('mood',this)">🎨 Moodboard</button>
  </div>
</nav>

<main>

<!-- ══════════ HOME ══════════ -->

<div class="section active" id="sec-home">
  <div class="hero">
    <span class="hero-cat" id="heroCat">🐱</span>
    <h1>Tvůj kreativní<br><em>Planner</em></h1>
    <p>Pro umělkyni, studentku & snílek ✨</p>

```
<div class="deadline-strip">
  <div class="dl-input-wrap">
    <span class="dl-label">📅 Deadline</span>
    <input type="date" class="dl-input" id="deadlineInput">
  </div>
  <div class="countdown-wrap">
    <div class="count-box">
      <span class="count-num" id="cDays">—</span>
      <span class="count-lbl">dní</span>
    </div>
    <div class="count-box">
      <span class="count-num" id="cWeeks">—</span>
      <span class="count-lbl">týdnů</span>
    </div>
  </div>
</div>
```

  </div>

  <!-- Progress -->

  <div class="prog-grid" id="progGrid">
    <div class="prog-card">
      <div class="prog-lbl">📝 Psaní</div>
      <div class="prog-val" id="pv0">0%</div>
      <div class="prog-bar-bg"><div class="prog-bar-fg" id="pb0" style="width:0%"></div></div>
      <input type="range" class="prog-slider" id="ps0" min="0" max="100" value="0">
    </div>
    <div class="prog-card">
      <div class="prog-lbl">🎨 Tvorba</div>
      <div class="prog-val" id="pv1">0%</div>
      <div class="prog-bar-bg"><div class="prog-bar-fg" id="pb1" style="width:0%"></div></div>
      <input type="range" class="prog-slider" id="ps1" min="0" max="100" value="0">
    </div>
    <div class="prog-card">
      <div class="prog-lbl">🔍 Výzkum</div>
      <div class="prog-val" id="pv2">0%</div>
      <div class="prog-bar-bg"><div class="prog-bar-fg" id="pb2" style="width:0%"></div></div>
      <input type="range" class="prog-slider" id="ps2" min="0" max="100" value="0">
    </div>
    <div class="prog-card">
      <div class="prog-lbl">✅ Úkoly</div>
      <div class="prog-val" id="pv3">0/0</div>
      <div class="prog-bar-bg"><div class="prog-bar-fg" id="pb3" style="width:0%"></div></div>
    </div>
  </div>

  <!-- Cat widget -->

  <div class="cat-widget">
    <span class="cat-big" id="catEmoji">😸</span>
    <p class="cat-quote" id="catMsg">Každý den trochu — a nakonec vznikne něco <strong>krásného</strong>. 🐾</p>
    <button class="btn-cat" onclick="newCat()">Nová zpráva ✨</button>
  </div>
</div>

<!-- ══════════ TODO ══════════ -->

<div class="section" id="sec-todo">
  <div class="panel">
    <div class="panel-title">📌 Úkoly</div>
    <div class="add-row">
      <input type="text" class="inp inp-grow" id="todoTxt" placeholder="Co je potřeba udělat..." maxlength="120">
      <select class="inp" id="todoTag">
        <option value="prace">💼 Práce</option>
        <option value="skola">📚 Škola</option>
        <option value="kreativa">🎨 Tvorba</option>
        <option value="osobni">🌿 Osobní</option>
      </select>
      <button class="btn-add" onclick="addTodo()">+ Přidat</button>
    </div>
    <div class="scroll-list" id="todoList" style="max-height:420px"></div>
  </div>

  <!-- Quick stats -->

  <div class="stats-row" id="todoStats"></div>
</div>

<!-- ══════════ PLAN ══════════ -->

<div class="section" id="sec-plan">
  <div class="panel">
    <div class="panel-title">🗓️ Harmonogram & milníky</div>
    <div class="add-row">
      <input type="text" class="inp inp-grow" id="msTxt" placeholder="Milník nebo termín..." maxlength="100">
      <input type="date" class="inp" id="msDate">
      <button class="btn-add" onclick="addMs()">+ Přidat</button>
    </div>
    <div class="scroll-list" id="msList" style="max-height:420px"></div>
  </div>
</div>

<!-- ══════════ NOTES ══════════ -->

<div class="section" id="sec-notes">
  <div class="panel">
    <div class="panel-title">💭 Poznámky & nápady</div>
    <div class="note-tabs">
      <button class="note-tab-btn active" onclick="switchNote('main',this)">📓 Hlavní</button>
      <button class="note-tab-btn" onclick="switchNote('ideas',this)">💡 Nápady</button>
      <button class="note-tab-btn" onclick="switchNote('inspo',this)">🌸 Inspirace</button>
      <button class="note-tab-btn" onclick="switchNote('todo_notes',this)">📋 Rychlé poznámky</button>
    </div>
    <textarea class="textarea" id="noteArea" placeholder="Sem si piš cokoliv... ✨"></textarea>
    <div style="font-size:0.75rem;color:var(--muted);margin-top:0.5rem;text-align:right;" id="noteCount">0 znaků</div>
  </div>
</div>

<!-- ══════════ MOODBOARD ══════════ -->

<div class="section" id="sec-mood">
  <div class="panel">
    <div class="panel-title">🎨 Moodboard</div>

```
<!-- Emoji / symboly -->
<div style="margin-bottom:1rem;">
  <div style="font-size:0.78rem;color:var(--muted);margin-bottom:0.5rem;text-transform:uppercase;letter-spacing:0.8px;">Vizuální prvky & symboly</div>
  <div class="mood-grid" id="emojiGrid"></div>
  <div class="mood-add-row">
    <input type="text" class="inp mood-emoji-inp" id="emojiInp" placeholder="🌸" maxlength="4">
    <input type="text" class="inp" style="flex:1" id="emojiLbl" placeholder="Popis (volitelné)" maxlength="30">
    <button class="btn-add" onclick="addEmoji()">+ Symbol</button>
  </div>
</div>

<!-- Barvy -->
<div style="margin-bottom:1rem;">
  <div style="font-size:0.78rem;color:var(--muted);margin-bottom:0.5rem;text-transform:uppercase;letter-spacing:0.8px;">Barevná paleta</div>
  <div class="mood-grid" id="colorGrid"></div>
  <div class="mood-add-row">
    <input type="color" class="inp" id="colorPick" style="width:55px;height:40px;padding:0.2rem;cursor:pointer;" value="#e8628a">
    <input type="text" class="inp" style="flex:1" id="colorLbl" placeholder="Název barvy (např. růžová jiskra)" maxlength="30">
    <button class="btn-add" onclick="addColor()">+ Barva</button>
  </div>
</div>

<!-- Klíčová slova -->
<div>
  <div style="font-size:0.78rem;color:var(--muted);margin-bottom:0.5rem;text-transform:uppercase;letter-spacing:0.8px;">Klíčová slova & nálady</div>
  <div class="chips-wrap" id="chipWrap"></div>
  <div class="mood-add-row" style="margin-top:0.6rem;">
    <input type="text" class="inp inp-grow" id="chipInp" placeholder="Přidej slovo nebo náladu..." maxlength="30">
    <button class="btn-add" onclick="addChip()">+ Slovo</button>
  </div>
</div>
```

  </div>
</div>

</main>

<script>
// ═══════ STORAGE ═══════
const LS = 'artplanner_v1';
let D = {
  deadline: '',
  progress: [0,0,0],
  todos: [],
  milestones: [],
  notes: { main:'', ideas:'', inspo:'', todo_notes:'' },
  mood: { emojis: [], colors: [], chips: [] }
};
function load() {
  try { const s = localStorage.getItem(LS); if(s) D = {...D,...JSON.parse(s)}; } catch(e){}
}
function save() {
  try { localStorage.setItem(LS, JSON.stringify(D)); } catch(e){}
}

// ═══════ SECTIONS ═══════
function showSection(id, btn) {
  document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(b=>b.classList.remove('active'));
  document.getElementById('sec-'+id).classList.add('active');
  btn.classList.add('active');
}

// ═══════ DEADLINE ═══════
const dlInp = document.getElementById('deadlineInput');
dlInp.value = D.deadline;
dlInp.addEventListener('change', () => { D.deadline = dlInp.value; save(); updateCountdown(); });

function updateCountdown() {
  if (!D.deadline) { document.getElementById('cDays').textContent='—'; document.getElementById('cWeeks').textContent='—'; return; }
  const now = new Date(); now.setHours(0,0,0,0);
  const dl = new Date(D.deadline);
  const diff = Math.ceil((dl-now)/86400000);
  document.getElementById('cDays').textContent = Math.max(0,diff);
  document.getElementById('cWeeks').textContent = Math.max(0,Math.ceil(diff/7));
}

// ═══════ PROGRESS ═══════
[0,1,2].forEach(i => {
  const sl = document.getElementById('ps'+i);
  sl.value = D.progress[i]||0;
  updateProg(i);
  sl.addEventListener('input', () => {
    D.progress[i] = parseInt(sl.value);
    updateProg(i);
    save();
  });
});
function updateProg(i) {
  const v = D.progress[i]||0;
  document.getElementById('pv'+i).textContent = v+'%';
  document.getElementById('pb'+i).style.width = v+'%';
}
function updateTodoProg() {
  const tot = D.todos.length, done = D.todos.filter(t=>t.done).length;
  document.getElementById('pv3').textContent = tot ? `${done}/${tot}` : '0/0';
  document.getElementById('pb3').style.width = tot ? Math.round(done/tot*100)+'%' : '0%';
}

// ═══════ TODOS ═══════
const tagMeta = {
  prace:    {label:'💼 Práce',    cls:'tag-prace'},
  skola:    {label:'📚 Škola',    cls:'tag-skola'},
  kreativa: {label:'🎨 Tvorba',   cls:'tag-kreativa'},
  osobni:   {label:'🌿 Osobní',   cls:'tag-osobni'},
};

function renderTodos() {
  const list = document.getElementById('todoList');
  list.innerHTML = '';
  if (!D.todos.length) { list.innerHTML = '<div class="empty">Žádné úkoly zatím 🐾<br>Přidej první!</div>'; updateTodoProg(); updateTodoStats(); return; }
  D.todos.forEach((t,i) => {
    const m = tagMeta[t.tag]||tagMeta.osobni;
    const div = document.createElement('div');
    div.className = 'item'+(t.done?' done':'');
    div.innerHTML = `
      <div class="check ${t.done?'on':''}" onclick="toggleTodo(${i})"></div>
      <span class="item-text">${esc(t.text)}</span>
      <span class="tag ${m.cls}">${m.label}</span>
      <button class="del-btn" onclick="delTodo(${i})">✕</button>
    `;
    list.appendChild(div);
  });
  updateTodoProg();
  updateTodoStats();
}

function addTodo() {
  const txt = document.getElementById('todoTxt').value.trim();
  if (!txt) return;
  D.todos.push({ text: txt, tag: document.getElementById('todoTag').value, done: false, id: Date.now() });
  document.getElementById('todoTxt').value = '';
  save(); renderTodos();
}

function toggleTodo(i) { D.todos[i].done = !D.todos[i].done; save(); renderTodos(); }
function delTodo(i) { D.todos.splice(i,1); save(); renderTodos(); }

function updateTodoStats() {
  const tot = D.todos.length, done = D.todos.filter(t=>t.done).length;
  const el = document.getElementById('todoStats');
  if (!tot) { el.innerHTML=''; return; }
  const byTag = {};
  D.todos.forEach(t=>{ if(!t.done) byTag[t.tag]=(byTag[t.tag]||0)+1; });
  let html = `<div class="stat-pill">Celkem: <strong>${tot}</strong></div><div class="stat-pill">Hotovo: <strong>${done}</strong></div>`;
  Object.entries(byTag).forEach(([tag,n]) => {
    const m = tagMeta[tag];
    html += `<div class="stat-pill">${m.label}: <strong>${n}</strong></div>`;
  });
  el.innerHTML = html;
}

document.getElementById('todoTxt').addEventListener('keydown', e => { if(e.key==='Enter') addTodo(); });

// ═══════ MILESTONES ═══════
function renderMs() {
  const list = document.getElementById('msList');
  list.innerHTML = '';
  if (!D.milestones.length) { list.innerHTML = '<div class="empty">Přidej první milník nebo deadline 🗓️</div>'; return; }
  const now = new Date(); now.setHours(0,0,0,0);
  const sorted = [...D.milestones].sort((a,b)=>new Date(a.date||'9999')-new Date(b.date||'9999'));
  sorted.forEach(m => {
    const idx = D.milestones.findIndex(x=>x.id===m.id);
    const div = document.createElement('div');
    div.className = 'ms-item'+(m.done?' done':'');
    const dl = m.date ? new Date(m.date) : null;
    const overdue = dl && dl < now && !m.done;
    const dateStr = dl ? dl.toLocaleDateString('cs-CZ',{day:'numeric',month:'long'}) : '';
    div.innerHTML = `
      <div class="ms-dot ${m.done?'on':''}" onclick="toggleMs(${idx})"></div>
      <div class="ms-info">
        <div class="ms-name">${esc(m.name)}</div>
        ${dateStr?`<div class="ms-date ${overdue?'overdue':''}">${overdue?'⚠️ Prošlý: ':'📅 '}${dateStr}</div>`:''}
      </div>
      <button class="del-btn" onclick="delMs(${idx})">✕</button>
    `;
    list.appendChild(div);
  });
}

function addMs() {
  const txt = document.getElementById('msTxt').value.trim();
  if (!txt) return;
  D.milestones.push({ id: Date.now(), name: txt, date: document.getElementById('msDate').value, done: false });
  document.getElementById('msTxt').value = '';
  document.getElementById('msDate').value = '';
  save(); renderMs();
}
function toggleMs(i) { D.milestones[i].done=!D.milestones[i].done; save(); renderMs(); }
function delMs(i) { D.milestones.splice(i,1); save(); renderMs(); }
document.getElementById('msTxt').addEventListener('keydown', e => { if(e.key==='Enter') addMs(); });

// ═══════ NOTES ═══════
let currentNote = 'main';
const notePlaceholders = {
  main: 'Hlavní poznámky, myšlenky, plány... ✨',
  ideas: 'Nápady — žádný nápad není špatný! 💡',
  inspo: 'Inspirace, reference, co tě zaujalo... 🌸',
  todo_notes: 'Rychlé poznámky a to-do věci... 📋',
};

const noteArea = document.getElementById('noteArea');
noteArea.value = D.notes['main']||'';
noteArea.addEventListener('input', () => {
  D.notes[currentNote] = noteArea.value;
  document.getElementById('noteCount').textContent = noteArea.value.length+' znaků';
  save();
});

function switchNote(key, btn) {
  currentNote = key;
  document.querySelectorAll('.note-tab-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  noteArea.value = D.notes[key]||'';
  noteArea.placeholder = notePlaceholders[key];
  document.getElementById('noteCount').textContent = noteArea.value.length+' znaků';
}

// ═══════ MOODBOARD ═══════
function renderEmojis() {
  const g = document.getElementById('emojiGrid');
  g.innerHTML = '';
  D.mood.emojis.forEach((e,i) => {
    const d = document.createElement('div');
    d.className = 'mood-card';
    d.innerHTML = `<span class="mood-emoji">${e.emoji}</span><div class="mood-label">${esc(e.label||'')}</div><button class="mood-del" onclick="delEmoji(${i})">✕</button>`;
    g.appendChild(d);
  });
  if (!D.mood.emojis.length) g.innerHTML = '<div class="empty" style="grid-column:1/-1;padding:0.8rem">Přidej symboly a motivy své tvorby 🌸</div>';
}

function addEmoji() {
  const e = document.getElementById('emojiInp').value.trim();
  if (!e) return;
  D.mood.emojis.push({ emoji: e, label: document.getElementById('emojiLbl').value.trim() });
  document.getElementById('emojiInp').value='';
  document.getElementById('emojiLbl').value='';
  save(); renderEmojis();
}
function delEmoji(i) { D.mood.emojis.splice(i,1); save(); renderEmojis(); }

function renderColors() {
  const g = document.getElementById('colorGrid');
  g.innerHTML = '';
  D.mood.colors.forEach((c,i) => {
    const d = document.createElement('div');
    d.className = 'mood-card';
    d.innerHTML = `
      <div class="color-swatch" style="background:${c.hex}">
        <button class="swatch-del" onclick="delColor(${i})">✕</button>
      </div>
      <div class="mood-label">${esc(c.label||c.hex)}</div>`;
    g.appendChild(d);
  });
  if (!D.mood.colors.length) g.innerHTML = '<div class="empty" style="grid-column:1/-1;padding:0.8rem">Přidej barvy své palety 🎨</div>';
}

function addColor() {
  const hex = document.getElementById('colorPick').value;
  D.mood.colors.push({ hex, label: document.getElementById('colorLbl').value.trim() });
  document.getElementById('colorLbl').value='';
  save(); renderColors();
}
function delColor(i) { D.mood.colors.splice(i,1); save(); renderColors(); }

function renderChips() {
  const w = document.getElementById('chipWrap');
  w.innerHTML = '';
  D.mood.chips.forEach((c,i) => {
    const s = document.createElement('span');
    s.className = 'chip';
    s.innerHTML = `${esc(c)}<button class="chip-del" onclick="delChip(${i})">✕</button>`;
    w.appendChild(s);
  });
  if (!D.mood.chips.length) w.innerHTML = '<span style="font-size:0.82rem;color:var(--muted);font-style:italic;">Zatím žádná slova...</span>';
}

function addChip() {
  const v = document.getElementById('chipInp').value.trim();
  if (!v) return;
  D.mood.chips.push(v);
  document.getElementById('chipInp').value='';
  save(); renderChips();
}
function delChip(i) { D.mood.chips.splice(i,1); save(); renderChips(); }
document.getElementById('chipInp').addEventListener('keydown', e => { if(e.key==='Enter') addChip(); });

// ═══════ CAT ═══════
const catData = [
  {e:'😸', m:'Každý den trochu — a nakonec vznikne něco <strong>krásného</strong>. 🐾'},
  {e:'🐱', m:'Tvoje kreativita je <strong>dar</strong>. Dnes ji použij aspoň trochu! ✨'},
  {e:'😺', m:'I kočky potřebují přestávku. Dej si čaj a pak zpátky do tvorby ☕'},
  {e:'😻', m:'Ty <strong>zvládneš</strong> všechno co sis naplánovala! Věřím ti 🌸'},
  {e:'🙀', m:'Deadline se blíží — ale ty <strong>jsi připravena</strong>! 💪'},
  {e:'🐈', m:'Umění se nedá unáhlit — ty víš kdy je to <strong>správně</strong> 🎨'},
  {e:'😽', m:'Nejlepší nápady přicházejí když si <strong>dovolíš snít</strong> 💭'},
  {e:'🐾', m:'Každý odškrtnutý úkol = <strong>malé vítězství</strong>. Gratuluju! 🎉'},
  {e:'😸', m:'Jsi umělkyně. Chaos je součástí procesu — <strong>neboj se ho</strong> 🌀'},
  {e:'🐱', m:'Tvoje bakalářka bude <strong>jedinečná</strong> jako ty 💕'},
];
let lastCat = -1;
function newCat() {
  let i; do { i = Math.floor(Math.random()*catData.length); } while(i===lastCat);
  lastCat = i;
  const c = catData[i];
  const e = document.getElementById('catEmoji');
  e.style.transform='scale(1.5) rotate(15deg)';
  setTimeout(()=>{e.style.transform='';},350);
  e.textContent = c.e;
  document.getElementById('catMsg').innerHTML = c.m;
}

// ═══════ UTILS ═══════
function esc(s) { return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

// ═══════ BOOT ═══════
load();
dlInp.value = D.deadline;
updateCountdown();
[0,1,2].forEach(i => { document.getElementById('ps'+i).value=D.progress[i]||0; updateProg(i); });
renderTodos();
renderMs();
noteArea.value = D.notes.main||'';
document.getElementById('noteCount').textContent = (D.notes.main||'').length+' znaků';
renderEmojis();
renderColors();
renderChips();
</script>

</body>
</html>
