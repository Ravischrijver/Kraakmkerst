<!DOCTYPE html>
<html lang="nl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kerst Kraak’M — UFO Cockpit (Kerstpuzzels)</title>
  <style>
    :root{
      --bg:#0b1220; --panel:#121a2e; --accent:#00ffd1; --accent2:#ff2e76;
      --text:#e7f2ff; --muted:#9bb0cc; --gold:#ffda2e; --ok:#19f3c6; --fail:#ff488f;
    }
    *{box-sizing:border-box}
    body{
      margin:0; font-family: system-ui, -apple-system, Segoe UI, Roboto, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
      background: radial-gradient(1200px 800px at 70% -10%, #152347, var(--bg)); color:var(--text);
    }
    header{
      padding:24px; border-bottom:1px solid #1f2b49;
      background: radial-gradient(600px 250px at 10% -20%, rgba(0,255,209,.15), transparent),
                  radial-gradient(600px 250px at 90% -30%, rgba(255,46,118,.12), transparent);
    }
    h1{ margin:0 0 8px; font-size: clamp(28px, 5vw, 40px); letter-spacing:.5px; }
    .subtitle{ color:var(--muted); }

    main{ display:grid; grid-template-columns: 320px 1fr; gap:20px; padding:20px; }

    /* Sidebar */
    .sidebar{
      background:var(--panel); border:1px solid #1f2b49; border-radius:16px; padding:16px; position:sticky; top:16px; height: fit-content;
    }
    .section-title{ font-weight:700; margin:12px 0 8px; font-size:15px; color:var(--accent); text-transform:uppercase; letter-spacing:.7px; }
    .inventory, .log, .status{
      background:#0f172a; border:1px solid #203154; border-radius:12px; padding:10px; margin-bottom:12px; max-height:220px; overflow:auto;
    }
    .chip{ display:inline-block; border:1px dashed #3b4c78; border-radius:999px; padding:6px 10px; margin:6px 6px 0 0; font-size:13px; color:#cfe6ff; background:linear-gradient(180deg,#0d152a,#0a1224); }
    .log p{ margin:8px 0; color:#cfe6ff; font-size:13px; }
    .status-row{ display:flex; justify-content:space-between; padding:6px 0; border-bottom:1px dashed #24406e; font-size:14px; color:#cfe6ff; }
    .status-row:last-child{border-bottom:none}
    .btn{
      appearance:none; border:none; background:linear-gradient(180deg, #13e8c4, #04b89c); color:#032a2a; font-weight:700;
      padding:10px 14px; border-radius:10px; cursor:pointer; transition:transform .05s ease; box-shadow:0 8px 20px rgba(0,255,209,.15);
    }
    .btn:active{transform:scale(.98)}
    .btn.secondary{ background:linear-gradient(180deg, #ff4f98, #e43783); color:#2a0016; box-shadow:0 8px 20px rgba(255,46,118,.18); }
    .btn.ghost{ background:transparent; border:1px solid #32507f; color:#cfe6ff; }
    .timer { font-size:18px; font-weight:bold; color:var(--gold); margin:10px 0; }
    .score { font-size:16px; color:var(--ok); margin:10px 0; }

    /* Cockpit */
    .cockpit{
      background:var(--panel); border:1px solid #1f2b49; border-radius:16px; overflow:hidden;
    }
    .scene-header{
      padding:14px 16px; border-bottom:1px solid #1f2b49;
      background: radial-gradient(300px 120px at 20% 0%, rgba(0,255,209,.12), transparent),
                  radial-gradient(300px 120px at 80% 0%, rgba(255,46,118,.1), transparent);
      display:flex; align-items:center; justify-content:space-between;
    }
    .scene-title{ margin:0; font-size:18px; letter-spacing:.3px; }
    .dashboard{ padding:18px; display:grid; gap:18px; grid-template-columns: repeat(2, minmax(260px,1fr)); }
    .panel{
      background:#0f172a; border:1px solid #203154; border-radius:12px; padding:12px; position:relative;
    }
    .panel h3{ margin:0 0 6px; font-size:16px; color:#bdefff; }
    .status-dot{ position:absolute; top:12px; right:12px; width:10px; height:10px; border-radius:50%; background:#4a5c84; box-shadow:0 0 0 2px #203154 inset; }
    .status-dot.ok{ background:var(--ok); }
    .status-dot.pending{ background:#4a5c84; }
    .inline{ display:flex; gap:10px; align-items:center; flex-wrap:wrap; margin-top:8px; }
    input[type="text"], select{
      background:#0b1220; border:1px solid #2b3f69; border-radius:10px; padding:10px 12px; color:#e7f2ff; outline:none; min-width:180px;
    }
    .hint{ font-size:13px; color:#9bb0cc; margin-top:6px; }
    .ok{ color:var(--ok) } .fail{ color:var(--fail) }
    .hidden{ display:none }

    /* Overlay & Ending */
    .overlay{ position:fixed; inset:0; background:rgba(5,10,20,.7); display:none; align-items:center; justify-content:center; z-index:99; }
    .modal{ background:#0f172a; border:1px solid #203154; border-radius:16px; padding:18px; max-width:720px; width:92%; }
    .modal h2{ margin:0 0 10px; }
    .end-banner{ border:1px solid #27e7c7; background:linear-gradient(180deg, rgba(19,232,196,.12), rgba(19,232,196,.05)); border-radius:12px; padding:12px; color:#cffff4; margin-top:10px; }
    .santa{ width:160px; height:160px; margin:8px auto 0; display:block; filter:drop-shadow(0 4px 10px rgba(255,255,255,.1)); }
    .celebrate{ animation: glow 1.4s ease-in-out infinite; }
    @keyframes glow{
      0%{text-shadow:0 0 0 rgba(0,255,209,0)}
      50%{text-shadow:0 0 12px rgba(0,255,209,.6)}
      100%{text-shadow:0 0 0 rgba(0,255,209,0)}
    }
    footer{ padding:16px 20px; color:#8fa9cf; }

    @media (max-width:900px){
      main{grid-template-columns:1fr} .inventory,.log,.status{max-height:none} .dashboard{grid-template-columns:1fr}
    }

    /* Small cockpit window visual */
    .viewport{
      margin:16px 18px 0; border-radius:12px; overflow:hidden; border:1px solid #203154;
      background: radial-gradient(800px 300px at 70% -40%, rgba(255,220,80,.18), transparent),
                  radial-gradient(600px 220px at 10% -30%, rgba(0,255,209,.12), transparent),
                  linear-gradient(180deg, #0a1326, #0b1220);
      height:160px; position:relative;
    }
    .planet{ position:absolute; border-radius:50%; filter:blur(.2px) drop-shadow(0 0 8px rgba(255,255,255,.08)); }
    .planet.yellow{ width:80px; height:80px; right:24px; top:24px; background:#f2c94c; }
    .ring{
      position:absolute; width:110px; height:30px; right:9px; top:58px; border:3px solid rgba(255,255,255,.35);
      border-radius:999px; transform:rotate(20deg);
    }
    .planet.blue{ width:42px; height:42px; left:26px; top:38px; background:#56ccf2; }
    .planet.red{ width:32px; height:32px; left:120px; top:16px; background:#eb5757; }
    .star{ position:absolute; width:2px; height:2px; background:#fff; opacity:.8; }
  </style>
</head>
<body>
  <header>
    <h1>Kerst Kraak’M — UFO Cockpit</h1>
    <p class="subtitle">Je zit in een UFO boven Slagharen. Druk op cockpit-knoppen om kerstpuzzels te kraken. Geen spoilers — gewoon spelen.</p>
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
        <p>— De cockpit zoemt zacht. Buiten fonkelen sterren.</p>
        <p>— Vier modules knipperen: Muziek, Cadeau, Winter, Boom.</p>
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
        <h2 class="scene-title">UFO Cockpit — Activeer alle kerstmodules</h2>
        <span class="hint">Druk op een knop om de puzzel te openen. Speels, visueel en auditief.</span>
      </div>

      <!-- Viewport (ruimtezicht) -->
      <div class="viewport">
        <div class="planet yellow"></div>
        <div class="ring"></div>
        <div class="planet blue"></div>
        <div class="planet red"></div>
        <!-- sterren -->
        <div class="star" style="left:22px;top:18px"></div>
        <div class="star" style="left:88px;top:40px"></div>
        <div class="star" style="left:140px;top:80px"></div>
        <div class="star" style="left:200px;top:24px"></div>
        <div class="star" style="left:260px;top:100px"></div>
        <div class="star" style="left:320px;top:60px"></div>
      </div>

      <div class="dashboard">
        <!-- MUZIEKMODULE -->
        <div class="panel" id="panel-music">
          <span class="status-dot pending" id="dot-music"></span>
          <h3>🎶 Muziekmodule — Raad het kerstlied</h3>
          <p>Druk op “Speel beltoon”. Kies daarna de titel van het lied.</p>
          <div class="inline">
            <button class="btn" onclick="playCarol()">Speel beltoon</button>
            <button class="btn ghost" onclick="openPuzzle('music')">Open keuze</button>
          </div>
          <div class="hidden" id="puzzle-music">
            <div class="inline">
              <select id="select-music">
                <option value="">Kies een lied...</option>
                <option>JINGLE BELLS</option>
                <option>STILLE NACHT</option>
                <option>WE WISH YOU A MERRY CHRISTMAS</option>
                <option>LAST CHRISTMAS</option>
              </select>
              <button class="btn" onclick="checkMusic()">Valideer</button>
              <span id="status-music" class="hint"></span>
            </div>
          </div>
        </div>

        <!-- CADEAU-MODULE -->
        <div class="panel" id="panel-gift">
          <span class="status-dot pending" id="dot-gift"></span>
          <h3>🎁 Cadeau-module — Wat zit er in de doos?</h3>
          <p>Bekijk het cadeautje en kies wat erin zit.</p>
          <div class="inline">
            <button class="btn ghost" onclick="openPuzzle('gift')">Open puzzel</button>
          </div>
          <div class="hidden" id="puzzle-gift">
            <!-- Inline SVG cadeau -->
            <svg viewBox="0 0 160 120" width="220" height="160" aria-label="Cadeau">
              <rect x="20" y="40" width="120" height="70" rx="8" fill="#d14b4b" stroke="#8c2e2e" />
              <rect x="70" y="40" width="20" height="70" fill="#ffd24d"/>
              <rect x="20" y="70" width="120" height="10" fill="#ffd24d"/>
              <circle cx="80" cy="35" r="16" fill="#ffd24d"/>
              <path d="M70 30 Q60 20 50 30 Q60 35 70 34 Z" fill="#ffd24d"/>
              <path d="M90 30 Q100 20 110 30 Q100 35 90 34 Z" fill="#ffd24d"/>
            </svg>
            <div class="inline">
              <select id="select-gift">
                <option value="">Kies inhoud...</option>
                <option>SJAAL</option>
                <option>SNEEUWPOP</option>
                <option>SLEE</option>
                <option>KERSTBAL</option>
              </select>
              <button class="btn" onclick="checkGift()">Valideer</button>
              <span id="status-gift" class="hint"></span>
            </div>
          </div>
        </div>

        <!-- WINTER-MODULE -->
        <div class="panel" id="panel-winter">
          <span class="status-dot pending" id="dot-winter"></span>
          <h3>🧤 Wintermodule — Kies het juiste woord</h3>
          <p>Kijk naar het plaatje en kies het woord dat erbij hoort.</p>
          <div class="inline">
            <button class="btn ghost" onclick="openPuzzle('winter')">Open puzzel</button>
          </div>
          <div class="hidden" id="puzzle-winter">
            <!-- Sneeuwpop SVG -->
            <svg viewBox="0 0 160 140" width="220" height="160" aria-label="Sneeuwpop">
              <circle cx="80" cy="50" r="24" fill="#ffffff" stroke="#cfe6ff"/>
              <circle cx="80" cy="100" r="34" fill="#ffffff" stroke="#cfe6ff"/>
              <circle cx="74" cy="48" r="3" fill="#2b2b2b"/>
              <circle cx="86" cy="48" r="3" fill="#2b2b2b"/>
              <polygon points="80,54 88,58 80,60" fill="#ff7f2a"/>
              <rect x="62" y="26" width="36" height="12" fill="#2b2b2b"/>
              <rect x="66" y="18" width="28" height="10" fill="#2b2b2b"/>
              <line x1="46" y1="90" x2="12" y2="78" stroke="#8c4a2e" stroke-width="3"/>
              <line x1="114" y1="90" x2="148" y2="78" stroke="#8c4a2e" stroke-width="3"/>
            </svg>
            <div class="inline">
              <select id="select-winter">
                <option value="">Kies woord...</option>
                <option>SJAAL</option>
                <option>SNEEUWPOP</option>
                <option>SLEE</option>
                <option>KERSTSTER</option>
              </select>
              <button class="btn" onclick="checkWinter()">Valideer</button>
              <span id="status-winter" class="hint"></span>
            </div>
          </div>
        </div>

        <!-- BOOM-MODULE -->
        <div class="panel" id="panel-tree">
          <span class="status-dot pending" id="dot-tree"></span>
          <h3>🎄 Boom-module — Wat ontbreekt?</h3>
          <p>Bekijk de versierde boom. Kies welk item er ontbreekt.</p>
          <div class="inline">
            <button class="btn ghost" onclick="openPuzzle('tree')">Open puzzel</button>
          </div>
          <div class="hidden" id="puzzle-tree">
            <!-- Kerstboom SVG -->
            <svg viewBox="0 0 160 180" width="220" height="180" aria-label="Kerstboom">
              <polygon points="80,20 110,70 50,70" fill="#2ecc71"/>
              <polygon points="80,50 120,110 40,110" fill="#27ae60"/>
              <polygon points="80,90 130,150 30,150" fill="#1e8449"/>
              <rect x="72" y="150" width="16" height="20" fill="#8c4a2e"/>
              <!-- Decor: kerstballen -->
              <circle cx="90" cy="80" r="5" fill="#ff4f98"/>
              <circle cx="65" cy="100" r="5" fill="#ffd24d"/>
              <circle cx="100" cy="120" r="5" fill="#56ccf2"/>
              <!-- Let op: geen ster bovenop -->
            </svg>
            <div class="inline">
              <select id="select-tree">
                <option value="">Kies ontbrekend item...</option>
                <option>KERSTBAL</option>
                <option>SLINGER</option>
                <option>STER</option>
                <option>CADEAU</option>
              </select>
              <button class="btn" onclick="checkTree()">Valideer</button>
              <span id="status-tree" class="hint"></span>
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

  <!-- Overlay: Ending / Game Over -->
  <div class="overlay" id="overlay">
    <div class="modal" id="modal"></div>
  </div>

  <footer>
    <p>Speels, kerstachtig, offline. Direct plakbaar voor GitHub Pages. 🎄👽</p>
  </footer>

  <script>
    // ---- Minimal Audio (WebAudio, geen externe bestanden) ----
    let audioCtx;
    function initAudio(){
      if(!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    }
    function tone(f=660, d=160, type='sine', vol=0.18){
      initAudio();
      const ctx = audioCtx, osc = ctx.createOscillator(), gain = ctx.createGain();
      osc.type = type; osc.frequency.value = f; gain.gain.value = vol;
      osc.connect(gain).connect(ctx.destination); osc.start();
      setTimeout(()=>osc.stop(), d);
    }
    function successSound(){ tone(880,140,'sine',0.2); setTimeout(()=>tone(1320,120,'sine',0.16),150); }
    function failSound(){ tone(220,180,'triangle',0.2); setTimeout(()=>tone(180,160,'triangle',0.14),190); }
    function bellSound(){ tone(1046,200,'sine',0.24); setTimeout(()=>tone(1318,160,'sine',0.2),210); setTimeout(()=>tone(1567,180,'sine',0.18),380); }

    // ---- Carol playback (Muziekmodule) ----
    // Simpele beltoon voor "JINGLE BELLS" patroon
    function playCarol(){
      initAudio();
      const seq = [880, 880, 880, 880, 880, 880, 880, 1046, 784, 880]; // suggestief
      let t = 0;
      seq.forEach((f,i)=>{
        setTimeout(()=>tone(f,120,'sine',0.16), t);
        t += (i%3===2) ? 280 : 180;
      });
    }

    // ---- State & Persistence ----
    const state = {
      music:false, gift:false, winter:false, tree:false,
      inv:["Cockpit Badge"], loc:"UFO Cockpit", accessLevel:"Basis", score:0
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
      const solved = ['music','gift','winter','tree'].filter(k => state[k]).length;
      subsEl.textContent = `${solved}/4 geactiveerd`;
      if(solved === 4){ rescueBtn.disabled = false; log("Alle kerstmodules actief. Hyperlift klaar."); }
      saveState();
    }
    function updateScore(points){
      state.score += points; if(state.score < 0) state.score = 0;
      scoreEl.textContent = "Score: " + state.score; saveState();
    }
    function setDot(id, ok){ const el = document.getElementById(id); el.classList.toggle('ok', !!ok); el.classList.toggle('pending', !ok); }
    function show(id){ document.getElementById(id).classList.remove('hidden'); }
    function ok(el, msg){ el.textContent = msg; el.className = 'hint ok'; }
    function fail(el, msg){ el.textContent = msg; el.className = 'hint fail'; }

    // ---- Open puzzles ----
    function openPuzzle(which){
      const ids = { music:'puzzle-music', gift:'puzzle-gift', winter:'puzzle-winter', tree:'puzzle-tree' };
      show(ids[which]);
      log("Puzzel geopend: " + which);
    }

    // ---- Checks (kerstpuzzels, geen rekenraadsels) ----
    function checkMusic(){
      const sel = document.getElementById('select-music');
      const status = document.getElementById('status-music');
      const choice = (sel.value || "").toUpperCase();
      // Correct: JINGLE BELLS
      if(choice === "JINGLE BELLS"){
        ok(status, "Yes! Dat is 'Jingle Bells'. Muziekmodule actief.");
        state.music = true; setDot('dot-music', true); updateSubs(); updateScore(25); successSound();
      } else if(choice){
        fail(status, "Nee, die is het niet. Luister nog eens naar de beltoon.");
        updateScore(-5); failSound();
      } else {
        fail(status, "Kies een lied.");
        failSound();
      }
    }

    function checkGift(){
      const sel = document.getElementById('select-gift');
      const status = document.getElementById('status-gift');
      const choice = (sel.value || "").toUpperCase();
      // Correct: SJAAL (warm cadeau)
      if(choice === "SJAAL"){
        ok(status, "Warm! Een sjaal zit in de doos. Cadeau-module actief.");
        if(!state.inv.includes("Sjaal")) state.inv.push("Sjaal");
        renderInv();
        state.gift = true; setDot('dot-gift', true); updateSubs(); updateScore(25); successSound();
      } else if(choice){
        fail(status, "Nope. Denk aan iets warms voor de winter.");
        updateScore(-5); failSound();
      } else {
        fail(status, "Maak een keuze.");
        failSound();
      }
    }

    function checkWinter(){
      const sel = document.getElementById('select-winter');
      const status = document.getElementById('status-winter');
      const choice = (sel.value || "").toUpperCase();
      // Correct: SNEEUWPOP (plaatje toont sneeuwpop)
      if(choice === "SNEEUWPOP"){
        ok(status, "Koud en vrolijk! Dat is een sneeuwpop. Wintermodule actief.");
        state.winter = true; setDot('dot-winter', true); updateSubs(); updateScore(25); successSound();
      } else if(choice){
        fail(status, "Niet goed. Kijk goed naar het plaatje.");
        updateScore(-5); failSound();
      } else {
        fail(status, "Maak een keuze.");
        failSound();
      }
    }

    function checkTree(){
      const sel = document.getElementById('select-tree');
      const status = document.getElementById('status-tree');
      const choice = (sel.value || "").toUpperCase();
      // Correct: STER (boom mist een ster bovenop)
      if(choice === "STER"){
        ok(status, "Precies! De ster ontbreekt. Boom-module actief.");
        state.tree = true; setDot('dot-tree', true); updateSubs(); updateScore(25); successSound();
      } else if(choice){
        fail(status, "Niet juist. Wat staat normaal bovenop?");
        updateScore(-5); failSound();
      } else {
        fail(status, "Maak een keuze.");
        failSound();
      }
    }

    // ---- Rescue flow ----
    function openRescue(){
      if(!state.music || !state.gift || !state.winter || !state.tree){
        alert("Activeer alle kerstmodules eerst."); return;
      }
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
          <p>“Ho Ho Ho! Fantastisch gedaan — kerst is gered!”</p>
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
      log("Eindscène: Kerstman lacht breed. Score: "+state.score+" | Tijd: "+mm+":"+ss);
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
        <p>De tijd is op. Probeer het opnieuw!</p>
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
        localStorage.setItem('ufo-kerst-escape-v2', JSON.stringify(snapshot));
      }catch(e){}
    }
    function restoreState(){
      const raw = localStorage.getItem('ufo-kerst-escape-v2'); if(!raw) return false;
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
      setDot('dot-music', state.music); setDot('dot-gift', state.gift); setDot('dot-winter', state.winter); setDot('dot-tree', state.tree);
      updateSubs();
      if(state.music && state.gift && state.winter && state.tree){ rescueBtn.disabled = false; }
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
      localStorage.removeItem('ufo-kerst-escape-v2'); location.reload();
    });

    function newGamePlus(){
      const history = JSON.parse(localStorage.getItem('ufo-kerst-escape-history') || '[]');
      history.push({ score: state.score, date: new Date().toISOString() });
      localStorage.setItem('ufo-kerst-escape-history', JSON.stringify(history));
      alert("New Game+! Vorige score opgeslagen.");
      localStorage.removeItem('ufo-kerst-escape-v2'); location.reload();
    }

    // ---- Init ----
    (function init(){
      const had = restoreState();
      restoreUI();
      startTimer();
      document.body.addEventListener('click', initAudio, { once:true });
      if(had){ log("Voortgang hersteld."); } else { log("Nieuw spel: activeer alle kerstmodules binnen 30 minuten."); }
    })();
  </script>
</body>
</html>
