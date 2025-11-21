<html lang="nl">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1.0"/>
  <title>Kerst Kraak’M — UFO Cockpit (15 moeilijke puzzels)</title>
  <style>
    :root{
      --bg:#0b1220; --panel:#121a2e; --accent:#00ffd1; --accent2:#ff2e76;
      --text:#e7f2ff; --muted:#9bb0cc; --gold:#ffda2e; --ok:#19f3c6; --fail:#ff488f;
    }
    *{box-sizing:border-box}
    body{margin:0; font-family:system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Cantarell,"Open Sans","Helvetica Neue",sans-serif;
      background:radial-gradient(1200px 800px at 70% -10%, #152347, var(--bg)); color:var(--text);}
    header{padding:24px; border-bottom:1px solid #1f2b49;
      background:radial-gradient(600px 250px at 10% -20%, rgba(0,255,209,.15), transparent),
                 radial-gradient(600px 250px at 90% -30%, rgba(255,46,118,.12), transparent);}
    h1{margin:0 0 8px; font-size:clamp(28px,5vw,40px); letter-spacing:.5px}
    .subtitle{color:var(--muted)}
    main{display:grid; grid-template-columns:320px 1fr; gap:20px; padding:20px}

    /* Sidebar */
    .sidebar{background:var(--panel); border:1px solid #1f2b49; border-radius:16px; padding:16px; position:sticky; top:16px; height:fit-content}
    .section-title{font-weight:700; margin:12px 0 8px; font-size:15px; color:var(--accent); text-transform:uppercase; letter-spacing:.7px}
    .status,.inventory,.log,.codes{background:#0f172a; border:1px solid #203154; border-radius:12px; padding:10px; margin-bottom:12px; max-height:220px; overflow:auto}
    .status-row{display:flex; justify-content:space-between; padding:6px 0; border-bottom:1px dashed #24406e; font-size:14px; color:#cfe6ff}
    .status-row:last-child{border-bottom:none}
    .chip{display:inline-block; border:1px dashed #3b4c78; border-radius:999px; padding:6px 10px; margin:6px 6px 0 0; font-size:13px; color:#cfe6ff; background:linear-gradient(180deg,#0d152a,#0a1224)}
    .log p{margin:8px 0; color:#cfe6ff; font-size:13px}
    .timer{font-size:18px; font-weight:bold; color:var(--gold); margin:10px 0}
    .score{font-size:16px; color:var(--ok); margin:10px 0}
    .btn{appearance:none; border:none; background:linear-gradient(180deg,#13e8c4,#04b89c); color:#032a2a; font-weight:700; padding:10px 14px; border-radius:10px; cursor:pointer; transition:transform .05s ease; box-shadow:0 8px 20px rgba(0,255,209,.15)}
    .btn:active{transform:scale(.98)}
    .btn.secondary{background:linear-gradient(180deg,#ff4f98,#e43783); color:#2a0016; box-shadow:0 8px 20px rgba(255,46,118,.18)}
    .btn.ghost{background:transparent; border:1px solid #32507f; color:#cfe6ff}
    .hint{font-size:13px; color:#9bb0cc; margin-top:6px}
    .ok{color:var(--ok)} .fail{color:var(--fail)}
    .hidden{display:none}

    /* Cockpit home */
    .cockpit{background:var(--panel); border:1px solid #1f2b49; border-radius:16px; overflow:hidden}
    .scene-header{padding:14px 16px; border-bottom:1px solid #1f2b49;
      background:radial-gradient(300px 120px at 20% 0%, rgba(0,255,209,.12), transparent),
                 radial-gradient(300px 120px at 80% 0%, rgba(255,46,118,.1), transparent);
      display:flex; align-items:center; justify-content:space-between}
    .scene-title{margin:0; font-size:18px; letter-spacing:.3px}
    .viewport{margin:16px 18px 0; border-radius:12px; overflow:hidden; border:1px solid #203154;
      background:radial-gradient(800px 300px at 70% -40%, rgba(255,220,80,.18), transparent),
                 radial-gradient(600px 220px at 10% -30%, rgba(0,255,209,.12), transparent),
                 linear-gradient(180deg,#0a1326,#0b1220); height:160px; position:relative}
    .planet{position:absolute; border-radius:50%; filter:blur(.2px) drop-shadow(0 0 8px rgba(255,255,255,.08))}
    .planet.yellow{width:80px; height:80px; right:24px; top:24px; background:#f2c94c}
    .ring{position:absolute; width:110px; height:30px; right:9px; top:58px; border:3px solid rgba(255,255,255,.35); border-radius:999px; transform:rotate(20deg)}
    .planet.blue{width:42px; height:42px; left:26px; top:38px; background:#56ccf2}
    .planet.red{width:32px; height:32px; left:120px; top:16px; background:#eb5757}
    .star{position:absolute; width:2px; height:2px; background:#fff; opacity:.8}
    .grid{padding:18px; display:grid; gap:12px; grid-template-columns:repeat(3, minmax(200px,1fr))}
    .tile{background:#0f172a; border:1px solid #203154; border-radius:12px; padding:12px}
    .tile h3{margin:0 0 8px; font-size:16px; color:#bdefff}
    .dot{display:inline-block; width:10px; height:10px; border-radius:50%; background:#4a5c84; margin-left:8px}
    .dot.ok{background:var(--ok)}

    /* Puzzle page */
    .page{background:var(--panel); border:1px solid #1f2b49; border-radius:16px; padding:18px}
    .question{background:#0f172a; border:1px solid #203154; border-radius:12px; padding:12px; margin-top:12px}
    input[type="text"], input[type="number"]{background:#0b1220; border:1px solid #2b3f69; border-radius:10px; padding:10px 12px; color:#e7f2ff; outline:none; min-width:240px}

    /* Overlay ending */
    .overlay{position:fixed; inset:0; background:rgba(5,10,20,.7); display:none; align-items:center; justify-content:center; z-index:99}
    .modal{background:#0f172a; border:1px solid #203154; border-radius:16px; padding:18px; max-width:720px; width:92%}
    .modal h2{margin:0 0 10px}
    .end-banner{border:1px solid #27e7c7; background:linear-gradient(180deg, rgba(19,232,196,.12), rgba(19,232,196,.05)); border-radius:12px; padding:12px; color:#cffff4; margin-top:10px}
    .santa{width:160px; height:160px; margin:8px auto 0; display:block; filter:drop-shadow(0 4px 10px rgba(255,255,255,.1))}
    .celebrate{animation:glow 1.4s ease-in-out infinite}
    @keyframes glow{0%{text-shadow:0 0 0 rgba(0,255,209,0)} 50%{text-shadow:0 0 12px rgba(0,255,209,.6)} 100%{text-shadow:0 0 0 rgba(0,255,209,0)}}

    footer{padding:16px 20px; color:#8fa9cf}
    @media (max-width:900px){main{grid-template-columns:1fr} .grid{grid-template-columns:1fr}}
  </style>
</head>
<body>
  <header>
    <h1>Kerst Kraak’M — UFO Cockpit</h1>
    <p class="subtitle">Steeds één puzzel-scherm. Geen weggevertjes. Kraakt 15 cryptische kerst-puzzels, typ je antwoorden, verzamel codecijfers.</p>
  </header>

  <main>
    <!-- Sidebar -->
    <aside class="sidebar" aria-label="Status en inventaris">
      <div class="status" id="statusBox">
        <div class="status-row"><span>Hoofddoel</span><strong>Bevrijd de Kerstman</strong></div>
        <div class="status-row"><span>Puzzels</span><strong id="subs">0/15 opgelost</strong></div>
        <div class="status-row"><span>Locatie</span><strong id="loc">UFO Cockpit</strong></div>
        <div class="status-row"><span>Toegang</span><strong id="access">Basis</strong></div>
      </div>

      <div class="timer" id="timer">Tijd: 30:00</div>
      <div class="score" id="score">Score: 0</div>

      <h2 class="section-title">Codecijfers</h2>
      <div class="codes" id="codesBox" aria-live="polite"></div>

      <h2 class="section-title">Inventaris</h2>
      <div class="inventory" id="inv" aria-live="polite">
        <span class="chip">Cockpit Badge</span>
      </div>

      <h2 class="section-title">Notities</h2>
      <div class="log" id="log" aria-live="polite">
        <p>— UFO boven Slagharen. Alleen jij & de cockpit.</p>
        <p>— Elk juist antwoord geeft een codecijfer. Verzamel ze allemaal.</p>
      </div>

      <div class="inline">
        <button class="btn" id="saveBtn">Opslaan</button>
        <button class="btn secondary" id="resetBtn">Reset</button>
      </div>
      <p class="hint">Opslaan gebruikt localStorage. Werkt offline.</p>
    </aside>

    <!-- Cockpit home -->
    <section id="home" class="cockpit">
      <div class="scene-header">
        <h2 class="scene-title">UFO Cockpit — 15 modules</h2>
        <span class="hint">Druk op een knop. Eén puzzel per scherm. Typ je antwoord exact.</span>
      </div>

      <div class="viewport">
        <div class="planet yellow"></div>
        <div class="ring"></div>
        <div class="planet blue"></div>
        <div class="planet red"></div>
        <div class="star" style="left:22px;top:18px"></div>
        <div class="star" style="left:88px;top:40px"></div>
        <div class="star" style="left:140px;top:80px"></div>
        <div class="star" style="left:200px;top:24px"></div>
        <div class="star" style="left:260px;top:100px"></div>
        <div class="star" style="left:320px;top:60px"></div>
      </div>

      <div class="grid" id="grid">
        <!-- Tiles generated by JS -->
      </div>

      <div class="scene-header">
        <h2 class="scene-title">Rescue — Eindcode</h2>
        <button class="btn secondary" id="rescueBtn" disabled onclick="openEnding()">Toon eindscherm</button>
      </div>
    </section>

    <!-- Puzzle page (single) -->
    <section id="page" class="page hidden" aria-live="polite">
      <div class="scene-header">
        <h2 class="scene-title" id="pageTitle">Puzzel</h2>
        <div class="inline">
          <button class="btn ghost" onclick="backToHome()">Terug naar cockpit</button>
        </div>
      </div>
      <div class="question" id="pageBody"></div>
    </section>
  </main>

  <!-- Overlay ending -->
  <div class="overlay" id="overlay">
    <div class="modal" id="modal"></div>
  </div>

  <footer>
    <p>Gemaakt voor Ravi — 15 moeilijke Kraak’M puzzels, één scherm tegelijk, 30 min timer, offline opslag. 🎄👽</p>
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

    // ---- Carol playback patterns (suggestief, geen spoil) ----
    function playJinglePattern(){
      const seq = [880, 880, 880, 880, 880, 880, 880, 1046, 784, 880]; let t=0;
      seq.forEach((f,i)=>{ setTimeout(()=>tone(f,120,'sine',0.16), t); t += (i%3===2)? 280 : 180; });
    }
    function playSilentNightPattern(){
      const seq = [659,587,523,587,659,659,659,587,587,587,659,784,784];
      let t=0; seq.forEach(f=>{ setTimeout(()=>tone(f,160,'sine',0.14), t); t+=220; });
    }
    function playWeWishPattern(){
      const seq = [659,659,740,659,587,523,523,587,659]; let t=0;
      seq.forEach(f=>{ setTimeout(()=>tone(f,140,'sine',0.16), t); t+=200; });
    }

    // ---- Puzzles definition (15) ----
    const
