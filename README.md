<html lang="nl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Kerst Kraak’M: Ontvoerd door aliens — Complete versie</title>
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
    .subtitle{
      color:var(--muted);
    }
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
    .log p{
      margin:8px 0;
      color:#cfe6ff;
      font-size:13px;
    }
    .status-row{
      display:flex;
      justify-content:space-between;
      padding:6px 0;
      border-bottom:1px dashed #24406e;
      font-size:14px;
      color:#cfe6ff;
    }
    .status-row:last-child{border-bottom:none}
    .btn{
      appearance:none;
      border:none;
      background:linear-gradient(180deg, #13e8c4, #04b89c);
      color:#032a2a;
      font-weight:700;
      padding:10px 14px;
      border-radius:10px;
      cursor:pointer;
      transition:transform .05s ease;
      box-shadow:0 8px 20px rgba(0,255,209,.15);
    }
    .btn:active{transform:scale(.98)}
    .btn.secondary{
      background:linear-gradient(180deg, #ff4f98, #e43783);
      color:#2a0016;
      box-shadow:0 8px 20px rgba(255,46,118,.18);
    }
    /* Game area */
    .scene{
      background:var(--panel);
      border:1px solid #1f2b49;
      border-radius:16px;
      overflow:hidden;
    }
    .scene-header{
      padding:14px 16px;
      border-bottom:1px solid #1f2b49;
      background:
        radial-gradient(300px 120px at 20% 0%, rgba(0,255,209,.12), transparent),
        radial-gradient(300px 120px at 80% 0%, rgba(255,46,118,.1), transparent);
      display:flex;
      align-items:center;
      justify-content:space-between;
    }
    .scene-title{
      margin:0;
      font-size:18px;
      letter-spacing:.3px;
    }
    .scene-body{
      padding:18px;
      display:grid;
      gap:18px;
      grid-template-columns: 1fr;
    }
    .card{
      background:#0f172a;
      border:1px solid #203154;
      border-radius:12px;
      padding:12px;
    }
    .card h3{
      margin:0 0 6px;
      font-size:16px;
      color:#bdefff;
    }
    .inline{
      display:flex;
      gap:10px;
      align-items:center;
      flex-wrap:wrap;
      margin-top:8px;
    }
    input[type="text"], input[type="number"], input[type="password"]{
      background:#0b1220;
      border:1px solid #2b3f69;
      border-radius:10px;
      padding:10px 12px;
      color:#e7f2ff;
      outline:none;
      min-width:180px;
    }
    .hint{
      font-size:13px;
      color:#9bb0cc;
      margin-top:6px;
    }
    .ok{color:var(--ok)}
    .fail{color:var(--fail)}
    .gate{
      border-left:4px solid var(--accent2);
      padding-left:12px;
      margin:8px 0;
    }
    .pulse{
      animation: glow 1.4s ease-in-out infinite;
    }
    @keyframes glow{
      0%{text-shadow:0 0 0 rgba(0,255,209,0)}
      50%{text-shadow:0 0 12px rgba(0,255,209,.6)}
      100%{text-shadow:0 0 0 rgba(0,255,209,0)}
    }
    footer{
      padding:16px 20px;
      color:#8fa9cf;
    }
    .end-banner{
      border:1px solid #27e7c7;
      background:linear-gradient(180deg, rgba(19,232,196,.12), rgba(19,232,196,.05));
      border-radius:12px;
      padding:12px;
      color:#cffff4;
      display:none;
      margin-top:10px;
    }
    .hidden{display:none}
    .timer {
      font-size:18px;
      font-weight:bold;
      color:var(--gold);
      margin:10px 0;
    }
    .score {
      font-size:16px;
      color:var(--ok);
      margin:10px 0;
    }
    @media (max-width:900px){
      main{grid-template-columns:1fr}
      .inventory,.log,.status{max-height:none}
    }
  </style>
</head>
<body>
  <header>
    <h1>Kerst Kraak’M: Ontvoerd door aliens</h1>
    <p class="subtitle">Het is kerstavond in Slagharen. De slee is klaar. De man in rood? Weg. Jij kraakt het mysterie.</p>
  </header>

  <main>
    <!-- Sidebar -->
    <aside class="sidebar" aria-label="Spelerstatus en inventaris">
      <div class="status" id="statusBox">
        <div class="status-row"><span>Hoofddoel</span><strong>Vind en bevrijd de Kerstman</strong></div>
        <div class="status-row"><span>Subdoelen</span><strong id="subs">0/4 opgelost</strong></div>
        <div class="status-row"><span>Locatie</span><strong id="loc">Kerstwerkplaats</strong></div>
        <div class="status-row"><span>Toegang</span><strong id="access">Basis</strong></div>
      </div>

      <div class="timer" id="timer">Tijd: 30:00</div>
      <div class="score" id="score">Score: 0</div>

      <h2 class="section-title">Inventaris</h2>
      <div class="inventory" id="inv" aria-live="polite"><span class="chip">Sneeuwvlok-sleutel</span></div>

      <h2 class="section-title">Notities</h2>
      <div class="log" id="log" aria-live="polite">
        <p>— De slee staat warm te draaien maar de rode jas hangt nog aan de kapstok.</p>
        <p>— Een vaag groen licht boven de dennen…</p>
      </div>

      <div class="inline">
        <button class="btn" id="saveBtn">Opslaan</button>
        <button class="btn secondary" id="resetBtn">Reset</button>
      </div>
      <p class="hint">Opslaan gebruikt localStorage. Werkt offline.</p>
    </aside>

    <!-- Game area -->
    <section class="scene">
      <div class="scene-header">
        <h2 class="scene-title">Act 1 — Werkplaats: De ijskoude aanwijzing</h2>
        <span class="hint">Los 4 puzzels op om de UFO-hangar te openen.</span>
      </div>
      <div class="scene-body">
        <!-- Puzzle 1: Kerstcode -->
        <div class="card" id="p1">
          <h3>Kerstcode: Het liedje met de sleutel</h3>
          <p>Op het werkbankje ligt een muziekdoos met acht noten: J, I, N, G, L, E, B, E. De doos vraagt om een acht-letter code.</p>
          <p class="hint">Hint: Denk aan een klassieker die begint met “Jingle…”.</p>
          <div class="inline">
            <input type="text" id="codeP1" placeholder="Voer code in (8 letters)" aria-label="Kerstcode invoer"/>
            <button class="btn" onclick="checkP1()">Valideer</button>
            <span id="statusP1" class="hint"></span>
          </div>
          <div class="gate hidden" id="gateP1">
            <p class="ok">Ontgrendeld: Je vindt een <strong>UFO-kwaliteitscertificaat</strong> met stempel “Aurora Sector”.</p>
          </div>
        </div>

        <!-- Puzzle 2: Sneeuwvlok slot -->
        <div class="card" id="p2">
          <h3>Sneeuwvlok-slot: Zes armen, één patroon</h3>
          <p>Een cryo-kist met een sneeuwvlok-slot toont zes cijfers die samen een symmetrisch patroon vormen.</p>
          <p class="hint">Hint: Palindroom met kerstgetal. Probeer 122221.</p>
          <div class="inline">
            <input type="number" id="codeP2" placeholder="6 cijfers" aria-label="Sneeuwvlok code"/>
            <button class="btn" onclick="checkP2()">Ontgrendel</button>
            <span id="statusP2" class="hint"></span>
          </div>
          <div class="gate hidden" id="gateP2">
            <p class="ok">Ontgrendeld: Je vindt een <strong>Cosmische bel</strong> die zacht zoemt bij groen licht.</p>
          </div>
        </div>

        <!-- Puzzle 3: Rendier coördinaten -->
        <div class="card" id="p3">
          <h3>Rendier-coördinaten: Polaris oriëntatie</h3>
          <p>Op een kaart staat: “Volg Polaris. Tel de letters van ‘NOORDPOOL’, vermenigvuldig met 2 en voeg 1 toe.”</p>
          <p class="hint">NOORDPOOL heeft 9 letters: 9×2+1 = 19. Voer 19 in.</p>
          <div class="inline">
            <input type="number" id="codeP3" placeholder="Resultaat" aria-label="Coördinaat getal"/>
            <button class="btn" onclick="checkP3()">Bevestig</button>
            <span id="statusP3" class="hint"></span>
          </div>
          <div class="gate hidden" id="gateP3">
            <p class="ok">Geactiveerd: Het kompas wijst naar een <strong>bosaal</strong> met vreemd footstep-licht.</p>
          </div>
        </div>

        <!-- Puzzle 4: Alien dialoog (woordslot) -->
        <div class="card" id="p4">
          <h3>Alien-woordslot: “GLÆ-EN”</h3>
          <p>Op de muur: “Wij namen de man in rood. Spreek de vreugde in onze tong.” De tekens lijken op het woord ‘VREUGDE’ zonder ‘V’.</p>
          <p class="hint">Zoek het Nederlandse woord voor joy. Probeer “VREUGDE”.</p>
          <div class="inline">
            <input type="text" id="codeP4" placeholder="Woord" aria-label="Alien woordslot"/>
            <button class="btn" onclick="checkP4()">Open</button>
            <span id="statusP4" class="hint"></span>
          </div>
          <div class="gate hidden" id="gateP4">
            <p class="ok">De deur schuift open: Een <strong>hangar</strong> met UFO-afdrukken en vallend stardust.</p>
          </div>
        </div>

        <!-- Act 2: Hangar -->
        <div class="card hidden" id="act2">
          <h3>Act 2 — UFO-hangar: Frequenties van het Noorderlicht</h3>
          <p>Een controlepaneel vraagt drie inputs: frequentie, patroon en toegangscode.</p>

          <div class="card" style="margin-top:10px;">
            <h3>Frequentie — Aurora beltoon</h3>
            <p>Luister naar de kosmische bel. Het pulst in groepen van 5. Vul 5.</p>
            <div class="inline">
              <input type="number" id="freq" placeholder="Frequentie" />
              <button class="btn" onclick="checkFreq()">Set</button>
              <span id="statusFreq" class="hint"></span>
            </div>
          </div>

          <div class="card" style="margin-top:10px;">
            <h3>Patroon — Sneeuwspoor</h3>
            <p>Het licht knippert in volgorde: Rood, Groen, Groen, Rood. Voer “RGGR”.</p>
            <div class="inline">
              <input type="text" id="pattern" placeholder="Patroon" />
              <button class="btn" onclick="checkPattern()">Set</button>
              <span id="statusPattern" class="hint"></span>
            </div>
          </div>

          <div class="card" style="margin-top:10px;">
            <h3>Toegang — Kerstman ID</h3>
            <p>De badge toont: “SANTA-1225”. Vul SANTA-1225.</p>
            <div class="inline">
              <input type="text" id="accessCode" placeholder="Toegangscode" />
              <button class="btn" onclick="checkAccess()">Set</button>
              <span id="statusAccess" class="hint"></span>
            </div>
          </div>

          <div class="gate hidden" id="hangarGate" style="margin-top:12px;">
            <p class="ok pulse">Hyperlift actief! Je hoort sleebelletjes en een diepe stem: “Ho ho… bedankt!”</p>
            <div class="end-banner" id="endBanner">
              <strong>Eindscène:</strong> De Kerstman verschijnt, nog wat duizelig.
              “Aliens wilden een betere beltoon. Jij stemde het Noorderlicht. Kerst is gered.”
              <p id="finalScore"></p>
              <p id="finalTime"></p>
            </div>
            <div class="inline" style="margin-top:10px;">
              <button class="btn" onclick="showEnding()">Toon eindscène</button>
              <button class="btn secondary" onclick="newGamePlus()">New Game+</button>
            </div>
          </div>
        </div>

      </div>
    </section>
  </main>

  <footer>
    <p>Made met sneeuw, sterrenstof en een snufje Slagharen. Speelbaar offline, opslaan via localStorage.</p>
  </footer>

  <script>
    // ---- Minimalistische audio (geen externe bestanden) ----
    let audioCtx;
    function initAudio(){
      if(!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    }
    function beep(frequency=660, duration=140, type='sine', volume=0.15){
      initAudio();
      const ctx = audioCtx;
      const osc = ctx.createOscillator();
      const gain = ctx.createGain();
      osc.type = type;
      osc.frequency.value = frequency;
      gain.gain.value = volume;
      osc.connect(gain).connect(ctx.destination);
      osc.start();
      setTimeout(()=>osc.stop(), duration);
    }
    function successSound(){
      beep(880,120,'sine',0.18);
      setTimeout(()=>beep(1320,120,'sine',0.15),130);
    }
    function failSound(){
      beep(220,160,'triangle',0.18);
      setTimeout(()=>beep(180,160,'triangle',0.14),170);
    }
    function bellSound(){
      beep(1046,180,'sine',0.22);
      setTimeout(()=>beep(1318,140,'sine',0.18),180);
      setTimeout(()=>beep(1567,160,'sine',0.16),330);
    }

    // ---- State & persistence ----
    const state = {
      p1:false, p2:false, p3:false, p4:false,
      freq:false, pattern:false, access:false,
      inv:["Sneeuwvlok-sleutel"],
      loc:"Kerstwerkplaats",
      accessLevel:"Basis",
      score:0
    };

    const invEl = document.getElementById('inv');
    const logEl = document.getElementById('log');
    const subsEl = document.getElementById('subs');
    const locEl = document.getElementById('loc');
    const accessEl = document.getElementById('access');
    const scoreEl = document.getElementById('score');
    const timerEl = document.getElementById('timer');

    function renderInv(){
      invEl.innerHTML = state.inv.map(i => `<span class="chip">${i}</span>`).join('');
    }
    function log(msg){
      const p = document.createElement('p');
      p.textContent = "— " + msg;
      logEl.appendChild(p);
      logEl.scrollTop = logEl.scrollHeight;
    }
    function updateSubs(){
      const solved = ['p1','p2','p3','p4'].filter(k => state[k]).length;
      subsEl.textContent = `${solved}/4 opgelost`;
      if(solved === 4){
        document.getElementById('act2').classList.remove('hidden');
        state.loc = "UFO-hangar";
        locEl.textContent = state.loc;
        log("De hangar opent. Koude ruimte-lucht stroomt naar binnen.");
      }
      saveState();
    }
    function updateScore(points){
      state.score += points;
      if(state.score < 0) state.score = 0;
      scoreEl.textContent = "Score: " + state.score;
      saveState();
    }

    // ---- Puzzle feedback ----
    function ok(el, msg){
      el.textContent = msg;
      el.className = 'hint ok';
    }
    function fail(el, msg){
      el.textContent = msg;
      el.className = 'hint fail';
    }

    // ---- Puzzle checks ----
    function checkP1(){
      const v = (document.getElementById('codeP1').value || "").trim().toUpperCase();
      const status = document.getElementById('statusP1');
      if(v === "JINGLEBELLS"){
        ok(status, "Correct. De muziekdoos speelt en onthult een document.");
        document.getElementById('gateP1').classList.remove('hidden');
        if(!state.inv.includes("UFO-certificaat")) state.inv.push("UFO-certificaat");
        state.p1 = true;
        renderInv(); updateSubs();
        updateScore(25);
        successSound();
        log("P1: JINGLEBELLS — Certificaat gevonden: Aurora Sector.");
      } else if(v){
        fail(status, "Niet goed. Luister naar het liedje…");
        updateScore(-5);
        failSound();
      } else {
        fail(status, "Vul een code in.");
        failSound();
      }
    }

    function checkP2(){
      const v = (document.getElementById('codeP2').value || "").trim();
      const status = document.getElementById('statusP2');
      if(v === "122221"){
        ok(status, "Slot open. De cryo-kist schuift langzaam omhoog.");
        document.getElementById('gateP2').classList.remove('hidden');
        if(!state.inv.includes("Cosmische bel")) state.inv.push("Cosmische bel");
        state.p2 = true;
        renderInv(); updateSubs();
        updateScore(25);
        successSound();
        log("P2: Sneeuwvlok patroon 122221 — Bel verkregen.");
      } else if(v){
        fail(status, "Probeer een palindroom dat past bij symmetrie.");
        updateScore(-5);
        failSound();
      } else {
        fail(status, "Voer 6 cijfers in.");
        failSound();
      }
    }

    function checkP3(){
      const raw = document.getElementById('codeP3').value;
      const v = Number(raw);
      const status = document.getElementById('statusP3');
      if(v === 19){
        ok(status, "Coördinaten bevestigd. Het kompas licht op.");
        document.getElementById('gateP3').classList.remove('hidden');
        if(!state.inv.includes("Bosaal-coördinaat")) state.inv.push("Bosaal-coördinaat");
        state.p3 = true;
        renderInv(); updateSubs();
        updateScore(25);
        successSound();
        log("P3: Polaris berekening 19 — Bosaal pad ontgrendeld.");
      } else if(raw !== ""){
        fail(status, "Check: letters in NOORDPOOL ×2 +1.");
        updateScore(-5);
        failSound();
      } else {
        fail(status, "Voer een getal in.");
        failSound();
      }
    }

    function checkP4(){
      const v = (document.getElementById('codeP4').value || "").trim().toUpperCase();
      const status = document.getElementById('statusP4');
      if(v === "VREUGDE"){
        ok(status, "Woord herkend. De deur schuift open.");
        document.getElementById('gateP4').classList.remove('hidden');
        state.p4 = true;
        renderInv(); updateSubs();
        updateScore(25);
        successSound();
        log("P4: VREUGDE — Hangar toegankelijk.");
      } else if(v){
        fail(status, "Spreek de vreugde: het Nederlandse woord voor joy.");
        updateScore(-5);
        failSound();
      } else {
        fail(status, "Voer het woord in.");
        failSound();
      }
    }

    // ---- Act 2 checks ----
    function checkFreq(){
      const raw = document.getElementById('freq').value;
      const v = Number(raw);
      const el = document.getElementById('statusFreq');
      if(v === 5){
        ok(el, "Frequentie gesynchroniseerd.");
        state.freq = true; maybeOpenHangar();
        updateScore(10);
        successSound();
        log("Aurora frequentie ingesteld op 5.");
      } else if(raw !== ""){
        fail(el, "Luister: pulsen in groepen van 5.");
        updateScore(-3);
        failSound();
      } else {
        fail(el, "Voer een getal in.");
        failSound();
      }
    }

    function checkPattern(){
      const v = (document.getElementById('pattern').value || "").trim().toUpperCase();
      const el = document.getElementById('statusPattern');
      if(v === "RGGR"){
        ok(el, "Patroon bevestigd.");
        state.pattern = true; maybeOpenHangar();
        updateScore(10);
        successSound();
        log("Patroon RGGR ingevoerd.");
      } else if(v){
        fail(el, "Let op de volgorde: Rood, Groen, Groen, Rood.");
        updateScore(-3);
        failSound();
      } else {
        fail(el, "Voer een patroon in.");
        failSound();
      }
    }

    function checkAccess(){
      const v = (document.getElementById('accessCode').value || "").trim().toUpperCase();
      const el = document.getElementById('statusAccess');
      if(v === "SANTA-1225"){
        ok(el, "Toegang verleend.");
        state.access = true; state.accessLevel = "Hangar";
        accessEl.textContent = state.accessLevel;
        updateScore(10);
        successSound();
        maybeOpenHangar();
        log("Toegang geverifieerd: SANTA-1225.");
      } else if(v){
        fail(el, "Bekijk de badge: SANTA-1225.");
        updateScore(-3);
        failSound();
      } else {
        fail(el, "Voer de toegangscode in.");
        failSound();
      }
    }

    function maybeOpenHangar(){
      if(state.freq && state.pattern && state.access){
        document.getElementById('hangarGate').classList.remove('hidden');
        bellSound();
      }
      saveState();
    }

    function showEnding(){
      document.getElementById('endBanner').style.display = 'block';
      const used = totalSeconds - timeLeft;
      const mm = String(Math.floor(used/60)).padStart(2,'0');
      const ss = String(used%60).padStart(2,'0');
      document.getElementById('finalScore').textContent = "Eindscore: " + state.score + " punten";
      document.getElementById('finalTime').textContent = "Tijd gebruikt: " + mm + ":" + ss;
      log("Eindscène getoond: Kerstman gered. Score: "+state.score+" | Tijd: "+mm+":"+ss);
      bellSound();
      clearInterval(timerInterval);
      saveState();
    }

    function newGamePlus(){
      // Houdt score-geschiedenis bij in localStorage
      const history = JSON.parse(localStorage.getItem('kerst-escape-history') || '[]');
      history.push({
        score: state.score,
        date: new Date().toISOString()
      });
      localStorage.setItem('kerst-escape-history', JSON.stringify(history));
      alert("New Game+ start! Vorige score opgeslagen.");
      localStorage.removeItem('kerst-escape');
      location.reload();
    }

    // ---- Timer (30 minuten) ----
    const totalSeconds = 1800; // 30 minuten
    let timeLeft = totalSeconds;
    let timerInterval;

    function startTimer(){
      timerInterval = setInterval(()=>{
        if(timeLeft <= 0){
          clearInterval(timerInterval);
          timerEl.textContent = "Tijd: 00:00";
          log("Tijd voorbij! De aliens vertrekken met de Kerstman...");
          failSound();
          alert("Game Over! Je was te laat.");
        } else {
          timeLeft--;
          const m = String(Math.floor(timeLeft/60)).padStart(2,'0');
          const s = String(timeLeft%60).padStart(2,'0');
          timerEl.textContent = `Tijd: ${m}:${s}`;
          // lichte spanning-klik elke 60s
          if(timeLeft % 60 === 0) beep(520,70,'square',0.07);
        }
      },1000);
    }

    // ---- Persistence helpers ----
    function saveState(){
      try{
        const snapshot = {
          ...state,
          timeLeft
        };
        localStorage.setItem('kerst-escape', JSON.stringify(snapshot));
      }catch(e){
        // stil
      }
    }
    function restoreState(){
      const raw = localStorage.getItem('kerst-escape');
      if(!raw) return false;
      try{
        const s = JSON.parse(raw);
        Object.assign(state, s);
        // tijd herstellen (niet onder 0)
        if(typeof s.timeLeft === 'number' && s.timeLeft > 0 && s.timeLeft <= totalSeconds){
          timeLeft = s.timeLeft;
        }
        return true;
      }catch(e){
        return false;
      }
    }

    // ---- UI restore ----
    function restoreUI(){
      renderInv();
      scoreEl.textContent = "Score: " + state.score;
      locEl.textContent = state.loc;
      accessEl.textContent = state.accessLevel;

      if(state.p1){document.getElementById('gateP1').classList.remove('hidden')}
      if(state.p2){document.getElementById('gateP2').classList.remove('hidden')}
      if(state.p3){document.getElementById('gateP3').classList.remove('hidden')}
      if(state.p4){document.getElementById('gateP4').classList.remove('hidden')}
      updateSubs();
      if(state.loc === "UFO-hangar"){document.getElementById('act2').classList.remove('hidden')}
      if(state.freq && state.pattern && state.access){
        document.getElementById('hangarGate').classList.remove('hidden');
      }
      const m = String(Math.floor(timeLeft/60)).padStart(2,'0');
      const s = String(timeLeft%60).padStart(2,'0');
      timerEl.textContent = `Tijd: ${m}:${s}`;
    }

    // ---- Buttons ----
    const saveBtn = document.getElementById('saveBtn');
    const resetBtn = document.getElementById('resetBtn');

    saveBtn.addEventListener('click', () => {
      saveState();
      log("Voortgang opgeslagen.");
      successSound();
    });

    resetBtn.addEventListener('click', () => {
      if(!confirm("Reset spel en geheugen?")) return;
      localStorage.removeItem('kerst-escape');
      location.reload();
    });

    // ---- Init ----
    (function init(){
      const had = restoreState();
      restoreUI();
      startTimer();
      if(had){
        log("Voortgang hersteld.");
      }else{
        log("Nieuw spel gestart. Je hebt 30 minuten.");
      }
      // resume AudioContext on first interaction (mobile policy)
      document.body.addEventListener('click', initAudio, { once:true });
    })();
  </script>
</body>
</html>
