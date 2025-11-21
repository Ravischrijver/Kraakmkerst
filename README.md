<html lang="nl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kerst Kraak’M — UFO Cockpit Editie</title>
  <style>
    :root{
      --bg:#0b1220;
      --panel:#121a2e;
      --accent:#00ffd1;
      --accent2:#ff2e76;
      --text:#e7f2ff;
      --muted:#9bb0cc;
      --gold:#ffda2e;
      --ok:#19f3c6;
      --fail:#ff488f;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
      background: radial-gradient(1200px 800px at 70% -10%, #152347, var(--bg));
      color:var(--text);
    }
    header{
      padding:24px;
      border-bottom:1px solid #1f2b49;
      background:
        radial-gradient(600px 250px at 10% -20%, rgba(0,255,209,.15), transparent),
        radial-gradient(600px 250px at 90% -30%, rgba(255,46,118,.12), transparent);
    }
    h1{
      margin:0 0 8px;
      font-size: clamp(28px, 5vw, 40px);
      letter-spacing:.5px;
    }
    .subtitle{ color:var(--muted); }
    main{
      display:grid;
      grid-template-columns: 320px 1fr;
      gap:20px;
      padding:20px;
    }
    /* Sidebar */
    .sidebar{
      background:var(--panel);
      border:1px solid #1f2b49;
      border-radius:16px;
      padding:16px;
      position:sticky;
      top:16px;
      height: fit-content;
    }
    .section-title{
      font-weight:700;
      margin:12px 0 8px;
      font-size:15px;
      color:var(--accent);
      text-transform:uppercase;
      letter-spacing:.7px;
    }
    .inventory, .log, .status{
      background:#0f172a;
      border:1px solid #203154;
      border-radius:12px;
      padding:10px;
      margin-bottom:12px;
      max-height:220px;
      overflow:auto;
    }
    .chip{
      display:inline-block;
      border:1px dashed #3b4c78;
      border-radius:999px;
      padding:6px 10px;
      margin:6px 6px 0 0;
      font-size:13px;
      color:#cfe6ff;
      background:linear-gradient(180deg,#0d152a,#0a1224);
    }
    .log p{ margin:8px 0; color:#cfe6ff; font-size:13px; }
    .status-row{
      display:flex; justify-content:space-between;
      padding:6px 0; border-bottom:1px dashed #24406e;
      font-size:14px; color:#cfe6ff;
    }
    .status-row:last-child{border-bottom:none}
    .btn{
      appearance:none; border:none;
      background:linear-gradient(180deg, #13e8c4, #04b89c);
      color:#032a2a; font-weight:700;
      padding:10px 14px; border-radius:10px; cursor:pointer;
      transition:transform .05s ease; box-shadow:0 8px 20px rgba(0,255,209,.15);
    }
    .btn:active{transform:scale(.98)}
    .btn.secondary{
      background:linear-gradient(180deg, #ff4f98, #e43783);
      color:#2a0016; box-shadow:0 8px 20px rgba(255,46,118,.18);
    }
    .btn.ghost{
      background:transparent; border:1px solid #32507f; color:#cfe6ff;
    }
    .timer { font-size:18px; font-weight:bold; color:var(--gold); margin:10px 0; }
    .score { font-size:16px; color:var(--ok); margin:10px 0; }

    /* Cockpit */
    .cockpit{
      background:var(--panel);
      border:1px solid #1f2b49;
      border-radius:16px; overflow:hidden;
    }
    .scene-header{
      padding:14px 16px; border-bottom:1px solid #1f2b49;
      background:
        radial-gradient(300px 120px at 20% 0%, rgba(0,255,209,.12), transparent),
        radial-gradient(300px 120px at 80% 0%, rgba(255,46,118,.1), transparent);
      display:flex; align-items:center; justify-content:space-between;
    }
    .scene-title{ margin:0; font-size:18px; letter-spacing:.3px; }
    .dashboard{
      padding:18px;
      display:grid; gap:18px;
      grid-template-columns: repeat(2, minmax(220px,1fr));
    }
    .panel{
      background:#0f172a; border:1px solid #203154; border-radius:12px;
      padding:12px; position:relative;
    }
    .panel h3{ margin:0 0 6px; font-size:16px; color:#bdefff; }
    .status-dot{
      position:absolute; top:12px; right:12px;
      width:10px; height:10px; border-radius:50%;
      background:#4a5c84; box-shadow:0 0 0 2px #203154 inset;
    }
    .status-dot.ok{ background:var(--ok); }
    .status-dot.pending{ background:#4a5c84; }
    .inline{ display:flex; gap:10px; align-items:center; flex-wrap:wrap; margin-top:8px; }
    input[type="text"], input[type="number"]{
      background:#0b1220; border:1px solid #2b3f69; border-radius:10px;
      padding:10px 12px; color:#e7f2ff; outline:none; min-width:180px;
    }
    .hint{ font-size:13px; color:#9bb0cc; margin-top:6px; }
    .ok{ color:var(--ok) } .fail{ color:var(--fail) }
    .hidden{ display:none }

    /* Overlay & Ending */
    .overlay{
      position:fixed; inset:0; background:rgba(5,10,20,.7);
      display:none; align-items:center; justify-content:center; z-index:99;
    }
    .modal{
      background:#0f172a; border:1px solid #203154; border-radius:16px;
      padding:18px; max-width:720px; width:92%;
    }
    .modal h2{ margin:0 0 10px; }
    .end-banner{
      border:1px solid #27e7c7;
      background:linear-gradient(180deg, rgba(19,232,196,.12), rgba(19,232,196,.05));
      border-radius:12px; padding:12px; color:#cffff4; margin-top:10px;
    }
    .santa{
      width:160px; height:160px; margin:8px auto 0; display:block;
      filter:drop-shadow(0 4px 10px rgba(255,255,255,.1));
    }
    .celebrate{ animation: glow 1.4s ease-in-out infinite; }
    @keyframes glow{
      0%{text-shadow:0 0 0 rgba(0,255,209,0)}
      50%{text-shadow:0 0 12px rgba(0,255,209,.6)}
      100%{text-shadow:0 0 0 rgba(0,255,209,0)}
    }
    footer{ padding:16px 20px; color:#8fa9cf; }

    @media (max-width:900px){
      main{grid-template-columns:1fr}
      .inventory,.log,.status{max-height:none}
      .dashboard{grid-template-columns:1fr}
    }
  </style>
</head>
<body>
  <header>
    <h1>Kerst Kraak’M — UFO Cockpit</h1>
    <p class="subtitle">Je wordt wakker in een UFO boven Slagharen. De Kerstman is nergens. Jij bedient de cockpit en kraakt het mysterie.</p>
  </header>

  <main>
    <!-- Sidebar -->
    <aside class="sidebar" aria-label="Status en inventaris">
      <div class="status" id="statusBox">
        <div class="status-row"><span>Hoofddoel</span><strong>Bevrijd de Kerstman</strong></div>
        <div class="status-row"><span>Modules</span><strong id="subs">0/4 geactiveerd</strong></div>
        <div class="status-row"><span>Locatie</span><strong id="loc">UFO Cockpit</strong></div>
        <div class="status-row"><span>Toegang</span><strong id="access">Basis</strong></div>
      </div>

      <div class="timer" id="timer">Tijd: 30:00</div>
      <div class="score" id="score">Score: 0</div>

      <h2 class="section-title">Inventaris</h2>
      <div class="inventory" id="inv" aria-live="polite">
        <span class="chip">Cockpit Badge</span>
      </div>

      <h2 class="section-title">Notities</h2>
      <div class="log" id="log" aria-live="polite">
        <p>— De cockpit zoemt zacht. Buiten danst groen licht.</p>
        <p>— Vier modules knipperen: Navigatie, Communicatie, Cryo, Muziek.</p>
      </div>

      <div class="inline">
        <button class="btn" id="saveBtn">Opslaan</button>
        <button class="btn secondary" id="resetBtn">Reset</button>
      </div>
      <p class="hint">Opslaan gebruikt localStorage. Werkt offline.</p>
    </aside>

    <!-- Cockpit -->
    <section class="cockpit">
      <div class="scene-header">
        <h2 class="scene-title">UFO Cockpit — Activeer alle modules</h2>
        <span class="hint">Elke knop opent een puzzel. Geen directe antwoorden. Observeer, denk, los op.</span>
      </div>

      <div class="dashboard">
        <!-- NAVIGATIE -->
        <div class="panel" id="panel-nav">
          <span class="status-dot pending" id="dot-nav"></span>
          <h3>Navigatie — Polaris kalibratie</h3>
          <p>Het kompas wil een getal gebaseerd op wat je ‘ziet’ aan de noordkant.</p>
          <p class="hint">Aanwijzing: Gebruik een eenvoudig rekenrecept op een woord dat bij de noordelijke regio hoort.</p>
          <div class="inline">
            <button class="btn" onclick="openPuzzle('nav')">Open puzzel</button>
          </div>
          <div class="hidden" id="puzzle-nav">
            <div class="inline">
              <input type="number" id="input-nav" placeholder="Voer getal in"/>
              <button class="btn ghost" onclick="checkNav()">Valideer</button>
              <span id="status-nav" class="hint"></span>
            </div>
          </div>
        </div>

        <!-- COMMUNICATIE -->
        <div class="panel" id="panel-com">
          <span class="status-dot pending" id="dot-com"></span>
          <h3>Communicatie — Vreemde tong</h3>
          <p>De muur vraagt om één Nederlands woord dat pure blijdschap betekent.</p>
          <p class="hint">Aanwijzing: Spreek het uit in je eigen taal, helder en volledig.</p>
          <div class="inline">
            <button class="btn" onclick="openPuzzle('com')">Open puzzel</button>
          </div>
          <div class="hidden" id="puzzle-com">
            <div class="inline">
              <input type="text" id="input-com" placeholder="Voer woord in"/>
              <button class="btn ghost" onclick="checkCom()">Valideer</button>
              <span id="status-com" class="hint"></span>
            </div>
          </div>
        </div>

        <!-- CRYO LOCK -->
        <div class="panel" id="panel-cryo">
          <span class="status-dot pending" id="dot-cryo"></span>
          <h3>Cryo-slot — Sneeuwvlok symmetrie</h3>
          <p>Een kist vraagt om een code van zes cijfers die in perfecte spiegeling staat.</p>
          <p class="hint">Aanwijzing: Denk aan een palindroom dat past bij zes armen.</p>
          <div class="inline">
            <button class="btn" onclick="openPuzzle('cryo')">Open puzzel</button>
          </div>
          <div class="hidden" id="puzzle-cryo">
            <div class="inline">
              <input type="number" id="input-cryo" placeholder="6 cijfers"/>
              <button class="btn ghost" onclick="checkCryo()">Valideer</button>
              <span id="status-cryo" class="hint"></span>
            </div>
          </div>
        </div>

        <!-- MUZIEKMODULE -->
        <div class="panel" id="panel-music">
          <span class="status-dot pending" id="dot-music"></span>
          <h3>Muziekmodule — Beltoon frase</h3>
          <p>Een muziekdoos speelt een klassieker. Geef de volledige frase, in hoofdletters en zonder spaties.</p>
          <p class="hint">Aanwijzing: Het is hét kerstlied dat vaak als eerste wordt gezongen.</p>
          <div class="inline">
            <button class="btn" onclick="openPuzzle('music')">Open puzzel</button>
          </div>
          <div class="hidden" id="puzzle-music">
            <div class="inline">
              <input type="text" id="input-music" placeholder="Frase (letters)"/>
              <button class="btn ghost" onclick="checkMusic()">Valideer</button>
              <span id="status-music" class="hint"></span>
            </div>
          </div>
        </div>
      </div>

      <div class="scene-header">
        <h2 class="scene-title">Rescue — Hyperlift naar de Kerstman</h2>
        <button class="btn secondary" id="rescueBtn" disabled onclick="openRescue()">Start redding</button>
      </div>
    </section>
  </main>

  <!-- Overlay: Game Over / Ending -->
  <div class="overlay" id="overlay">
    <div class="modal" id="modal">
      <!-- Content dynamically injected -->
    </div>
  </div>

  <footer>
    <p>Gemaakt voor Ravi: UFO-cockpit puzzel, 30min timer, offline opslag, zonder weggevertjes. 🎄👽</p>
  </footer>

  <script>
    // ---- Minimal Audio (WebAudio, geen externe bestanden) ----
    let audioCtx;
    function initAudio(){
      if(!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    }
    function tone(f=660, d=140, type='sine', vol=0.15){
      initAudio();
      const ctx = audioCtx, osc = ctx.createOscillator(), gain = ctx.createGain();
      osc.type = type; osc.frequency.value = f; gain.gain.value = vol;
      osc.connect(gain).connect(ctx.destination); osc.start();
      setTimeout(()=>osc.stop(), d);
    }
    function successSound(){ tone(880,120,'sine',0.18); setTimeout(()=>tone(1320,120,'sine',0.15),130); }
    function failSound(){ tone(220,160,'triangle',0.18); setTimeout(()=>tone(180,160,'triangle',0.14),170); }
    function bellSound(){ tone(1046,180,'sine',0.22); setTimeout(()=>tone(1318,140,'sine',0.18),180); setTimeout(()=>tone(1567,160,'sine',0.16),330); }

    // ---- State & Persistence ----
    const state = {
      nav:false, com:false, cryo:false, music:false,
      inv:["Cockpit Badge"],
      loc:"UFO Cockpit",
      accessLevel:"Basis",
      score:0
    };
    const totalSeconds = 1800; // 30 minuten
    let timeLeft = totalSeconds;
    let timerInterval;

    // ---- UI refs ----
    const invEl = document.getElementById('inv');
    const logEl = document.getElementById('log');
    const subsEl = document.getElementById('subs');
    const locEl = document.getElementById('loc');
    const accessEl = document.getElementById('access');
    const scoreEl = document.getElementById('score');
    const timerEl = document.getElementById('timer');
    const rescueBtn = document.getElementById('rescueBtn');
    const overlay = document.getElementById('overlay');
    const modal = document.getElementById('modal');

    // ---- Helpers ----
    function renderInv(){ invEl.innerHTML = state.inv.map(i => `<span class="chip">${i}</span>`).join(''); }
    function log(msg){ const p = document.createElement('p'); p.textContent = "— " + msg; logEl.appendChild(p); logEl.scrollTop = logEl.scrollHeight; }
    function updateSubs(){
      const solved = ['nav','com','cryo','music'].filter(k => state[k]).length;
      subsEl.textContent = `${solved}/4 geactiveerd`;
      if(solved === 4){ rescueBtn.disabled = false; log("Alle modules actief. Hyperlift klaar voor redding."); }
      saveState();
    }
    function updateScore(points){
      state.score += points; if(state.score < 0) state.score = 0;
      scoreEl.textContent = "Score: " + state.score; saveState();
    }
    function setDot(id, ok){ const el = document.getElementById(id); el.classList.toggle('ok', !!ok); el.classList.toggle('pending', !ok); }
    function show(el){ el.classList.remove('hidden'); } function hide(el){ el.classList.add('hidden'); }
    function ok(el, msg){ el.textContent = msg; el.className = 'hint ok'; }
    function fail(el, msg){ el.textContent = msg; el.className = 'hint fail'; }

    // ---- Open puzzles ----
    function openPuzzle(which){
      // open inline puzzle area
      const ids = { nav:'puzzle-nav', com:'puzzle-com', cryo:'puzzle-cryo', music:'puzzle-music' };
      show(document.getElementById(ids[which]));
      log("Module geopend: " + which);
    }

    // ---- Checks (zonder weggevertjes in UI) ----
    function checkNav(){
      const raw = document.getElementById('input-nav').value;
      const v = Number(raw);
      const status = document.getElementById('status-nav');
      // Oplossing: 19 (afgeleid van NOORDPOOL met een eenvoudig recept)
      if(v === 19){
        ok(status, "Kalibratie bevestigd. Kompas vergrendeld.");
        state.nav = true; setDot('dot-nav', true); updateSubs(); updateScore(25); successSound();
        log("Navigatie geactiveerd.");
      } else if(raw !== ""){
        fail(status, "Niet juist. Herhaal jouw recept en controleer het getal.");
        updateScore(-5); failSound();
      } else {
        fail(status, "Voer een getal in.");
        failSound();
      }
    }

    function checkCom(){
      const v = (document.getElementById('input-com').value || "").trim().toUpperCase();
      const status = document.getElementById('status-com');
      // Oplossing: VREUGDE
      if(v === "VREUGDE"){
        ok(status, "Signaal ontvangen. De muur gloeit warm.");
        state.com = true; setDot('dot-com', true); updateSubs(); updateScore(25); successSound();
        log("Communicatie geactiveerd.");
      } else if(v){
        fail(status, "Niet herkend. Spreek het heldere woord voor blijdschap.");
        updateScore(-5); failSound();
      } else {
        fail(status, "Voer een woord in.");
        failSound();
      }
    }

    function checkCryo(){
      const raw = (document.getElementById('input-cryo').value || "").trim();
      const status = document.getElementById('status-cryo');
      // Oplossing: 122221 (palindroom, 6 cijfers)
      if(raw === "122221"){
        ok(status, "Cryo-kist ontgrendeld. Koele damp ontsnapt.");
        if(!state.inv.includes("Sneeuwvlok-sleutel")) state.inv.push("Sneeuwvlok-sleutel");
        renderInv();
        state.cryo = true; setDot('dot-cryo', true); updateSubs(); updateScore(25); successSound();
        log("Cryo-slot geactiveerd.");
      } else if(raw){
        fail(status, "Niet juist. Denk aan perfecte spiegeling.");
        updateScore(-5); failSound();
      } else {
        fail(status, "Voer 6 cijfers in.");
        failSound();
      }
    }

    function checkMusic(){
      const v = (document.getElementById('input-music').value || "").trim().toUpperCase().replace(/\s+/g,'');
      const status = document.getElementById('status-music');
      // Oplossing: JINGLEBELLS
      if(v === "JINGLEBELLS"){
        ok(status, "Beltoon ingesteld. De kamer resoneert feestelijk.");
        state.music = true; setDot('dot-music', true); updateSubs(); updateScore(25); successSound();
        log("Muziekmodule geactiveerd.");
      } else if(v){
        fail(status, "Niet juist. Geef de volledige frase, strak en zonder spaties.");
        updateScore(-5); failSound();
      } else {
        fail(status, "Voer een frase in.");
        failSound();
      }
    }

    // ---- Rescue flow ----
    function openRescue(){
      if(!state.nav || !state.com || !state.cryo || !state.music){
        alert("Activeer alle modules eerst."); return;
      }
      // Eindscène: blije Kerstman (SVG), score & tijd
      overlay.style.display = 'flex';
      modal.innerHTML = `
        <h2 class="celebrate">Hyperlift actief — De Kerstman verschijnt!</h2>
        <svg class="santa" viewBox="0 0 120 120" xmlns="http://www.w3.org/2000/svg" aria-label="Blije Kerstman">
          <circle cx="60" cy="60" r="50" fill="#fff3e0"/>
          <path d="M15 40 Q60 10 105 40 L105 55 Q60 35 15 55 Z" fill="#ff2e76"/>
          <circle cx="42" cy="62" r="6" fill="#2b2b2b"/>
          <circle cx="78" cy="62" r="6" fill="#2b2b2b"/>
          <path d="M40 82 Q60 95 80 82" stroke="#e43783" stroke-width="4" fill="none"/>
          <circle cx="60" cy="28" r="8" fill="#fff"/>
          <rect x="25" y="90" width="70" height="16" rx="8" fill="#fff"/>
        </svg>
        <div class="end-banner">
          <p>“Ho Ho Ho! Jij hebt de juiste modules afgestemd. Kerst is gered!”</p>
          <p id="finalScore"></p>
          <p id="finalTime"></p>
          <div class="inline">
            <button class="btn" onclick="closeOverlay()">Sluit</button>
            <button class="btn secondary" onclick="newGamePlus()">New Game+</button>
          </div>
        </div>
      `;
      const used = totalSeconds - timeLeft;
      const mm = String(Math.floor(used/60)).padStart(2,'0');
      const ss = String(used%60).padStart(2,'0');
      document.getElementById('finalScore').textContent = "Eindscore: " + state.score + " punten";
      document.getElementById('finalTime').textContent = "Tijd gebruikt: " + mm + ":" + ss;
      bellSound();
      clearInterval(timerInterval);
      saveState();
      log("Eindscène getoond: Kerstman lacht breed. Score: "+state.score+" | Tijd: "+mm+":"+ss);
    }
    function closeOverlay(){ overlay.style.display = 'none'; }

    // ---- Timer ----
    function startTimer(){
      timerInterval = setInterval(()=>{
        if(timeLeft <= 0){
          clearInterval(timerInterval);
          timerEl.textContent = "Tijd: 00:00";
          gameOver();
        } else {
          timeLeft--;
          const m = String(Math.floor(timeLeft/60)).padStart(2,'0');
          const s = String(timeLeft%60).padStart(2,'0');
          timerEl.textContent = `Tijd: ${m}:${s}`;
          if(timeLeft % 60 === 0) tone(520,70,'square',0.07);
        }
      },1000);
    }
    function gameOver(){
      overlay.style.display = 'flex';
      modal.innerHTML = `
        <h2>Game Over</h2>
        <p>De tijd is op. De aliens vertrekken… maar je kunt het opnieuw proberen.</p>
        <div class="inline">
          <button class="btn" onclick="closeOverlay()">Sluit</button>
          <button class="btn secondary" onclick="newGamePlus()">Opnieuw</button>
        </div>
      `;
      failSound();
      log("Tijd voorbij! Probeer opnieuw.");
    }

    // ---- Persistence ----
    function saveState(){
      try{
        const snapshot = { ...state, timeLeft };
        localStorage.setItem('ufo-kerst-escape', JSON.stringify(snapshot));
      }catch(e){}
    }
    function restoreState(){
      const raw = localStorage.getItem('ufo-kerst-escape'); if(!raw) return false;
      try{
        const s = JSON.parse(raw);
        Object.assign(state, s);
        if(typeof s.timeLeft === 'number' && s.timeLeft > 0 && s.timeLeft <= totalSeconds){
          timeLeft = s.timeLeft;
        }
        return true;
      }catch(e){ return false; }
    }

    // ---- UI restore ----
    function restoreUI(){
      renderInv();
      scoreEl.textContent = "Score: " + state.score;
      locEl.textContent = state.loc;
      accessEl.textContent = state.accessLevel;
      setDot('dot-nav', state.nav); setDot('dot-com', state.com); setDot('dot-cryo', state.cryo); setDot('dot-music', state.music);
      updateSubs();
      if(state.nav && state.com && state.cryo && state.music){ rescueBtn.disabled = false; }
      const m = String(Math.floor(timeLeft/60)).padStart(2,'0');
      const s = String(timeLeft%60).padStart(2,'0');
      timerEl.textContent = `Tijd: ${m}:${s}`;
    }

    // ---- Buttons ----
    document.getElementById('saveBtn').addEventListener('click', () => {
      saveState(); log("Voortgang opgeslagen."); successSound();
    });
    document.getElementById('resetBtn').addEventListener('click', () => {
      if(!confirm("Reset spel en geheugen?")) return;
      localStorage.removeItem('ufo-kerst-escape'); location.reload();
    });

    function newGamePlus(){
      const history = JSON.parse(localStorage.getItem('ufo-kerst-escape-history') || '[]');
      history.push({ score: state.score, date: new Date().toISOString() });
      localStorage.setItem('ufo-kerst-escape-history', JSON.stringify(history));
      alert("New Game+! Vorige score opgeslagen.");
      localStorage.removeItem('ufo-kerst-escape'); location.reload();
    }

    // ---- Init ----
    (function init(){
      const had = restoreState();
      restoreUI();
      startTimer();
      document.body.addEventListener('click', initAudio, { once:true });
      if(had){ log("Voortgang hersteld."); } else { log("Nieuw spel: activeer alle modules binnen 30 minuten."); }
    })();
  </script>
</body>
</html>
