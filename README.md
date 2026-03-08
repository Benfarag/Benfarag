<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>BENFARAG — GitHub Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #04040f;
    --deep: #08082a;
    --cyan: #00cfff;
    --cyan2: #00ffe7;
    --purple: #7b5ea7;
    --dim: #3a3a6a;
    --text: #aaaadd;
    --white: #e8e8ff;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Share Tech Mono', monospace;
    overflow-x: hidden;
    cursor: crosshair;
  }

  /* ── STARFIELD ── */
  #stars-canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    pointer-events: none;
  }

  .content { position: relative; z-index: 1; max-width: 860px; margin: 0 auto; padding: 0 24px 80px; }

  /* ── HERO ── */
  .hero {
    text-align: center;
    padding: 80px 0 40px;
    animation: fadeDown .9s ease both;
  }

  .hero-name {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(2.8rem, 8vw, 5.5rem);
    font-weight: 900;
    letter-spacing: .18em;
    background: linear-gradient(135deg, var(--cyan), var(--cyan2), var(--purple));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    filter: drop-shadow(0 0 18px #00cfff88);
    animation: glowPulse 3s ease-in-out infinite;
  }

  .hero-sub {
    margin-top: 12px;
    font-size: .85rem;
    letter-spacing: .35em;
    color: var(--dim);
    text-transform: uppercase;
    animation: fadeDown .9s .3s ease both;
  }

  /* ── TYPING ── */
  .typing-wrap {
    margin: 28px auto 0;
    height: 28px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .typing-text {
    font-size: 1rem;
    color: var(--cyan);
    border-right: 2px solid var(--cyan);
    white-space: nowrap;
    overflow: hidden;
    animation: blink .7s step-end infinite;
  }

  /* ── STATUS BADGES ── */
  .badges {
    display: flex;
    justify-content: center;
    gap: 10px;
    flex-wrap: wrap;
    margin: 32px 0;
    animation: fadeUp .8s .5s ease both;
  }
  .badge {
    background: #0a0a2a;
    border: 1px solid var(--dim);
    color: var(--cyan);
    font-size: .7rem;
    letter-spacing: .15em;
    padding: 6px 14px;
    border-radius: 4px;
    transition: all .3s;
  }
  .badge:hover {
    border-color: var(--cyan);
    box-shadow: 0 0 12px #00cfff55;
    transform: translateY(-2px);
  }

  /* ── SECTION TITLE ── */
  .section-title {
    font-family: 'Orbitron', sans-serif;
    font-size: .8rem;
    letter-spacing: .3em;
    color: var(--cyan);
    text-align: center;
    margin: 56px 0 24px;
    position: relative;
  }
  .section-title::before,
  .section-title::after {
    content: '';
    position: absolute;
    top: 50%;
    width: 28%;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--dim));
  }
  .section-title::before { right: 54%; }
  .section-title::after  { left: 54%; transform: scaleX(-1); }

  /* ── MISSION TABLE ── */
  .mission-table {
    width: 100%;
    border-collapse: collapse;
    animation: fadeUp .8s .2s ease both;
  }
  .mission-table th {
    font-family: 'Orbitron', sans-serif;
    font-size: .65rem;
    letter-spacing: .25em;
    color: var(--dim);
    padding: 8px 16px;
    text-align: center;
    border-bottom: 1px solid #1a1a3a;
  }
  .mission-table td {
    padding: 12px 16px;
    text-align: center;
    border-bottom: 1px solid #0e0e28;
    transition: background .3s;
    font-size: .85rem;
  }
  .mission-table tr:hover td { background: #0d0d2e; }

  .pill {
    display: inline-block;
    padding: 4px 12px;
    border-radius: 20px;
    font-size: .72rem;
    font-weight: bold;
    letter-spacing: .1em;
  }
  .pill-mobile   { background:#02569B22; color:#4da8ff; border:1px solid #02569B88; }
  .pill-web      { background:#E34F2622; color:#ff8c5a; border:1px solid #E34F2688; }
  .pill-sys      { background:#00599C22; color:#5aaaff; border:1px solid #00599C88; }
  .pill-art      { background:#7D929E22; color:#b0c4cc; border:1px solid #7D929E88; }
  .pill-nav      { background:#F0503222; color:#ff9977; border:1px solid #F0503288; }
  .pill-intel    { background:#02262B22; color:#44ddcc; border:1px solid #02262B88; }

  .status { font-size: .8rem; }

  /* ── SKILL BARS ── */
  .skill-bars { display: flex; flex-direction: column; gap: 14px; animation: fadeUp .8s .2s ease both; }
  .skill-row  { display: flex; align-items: center; gap: 12px; }
  .skill-label { width: 160px; font-size: .78rem; color: var(--text); flex-shrink: 0; }
  .bar-track {
    flex: 1; height: 6px;
    background: #0e0e28;
    border-radius: 4px;
    overflow: hidden;
    border: 1px solid #1a1a3a;
  }
  .bar-fill {
    height: 100%;
    border-radius: 4px;
    background: linear-gradient(90deg, var(--cyan), var(--cyan2));
    box-shadow: 0 0 8px var(--cyan);
    width: 0;
    transition: width 1.5s cubic-bezier(.4,0,.2,1);
  }
  .bar-pct { width: 36px; font-size: .75rem; color: var(--cyan); text-align: right; flex-shrink: 0; }

  /* ── LOG PANEL ── */
  .log-panel {
    background: #06061a;
    border: 1px solid var(--dim);
    border-radius: 6px;
    padding: 24px 28px;
    font-size: .82rem;
    line-height: 1.9;
    animation: fadeUp .8s .2s ease both;
    position: relative;
    overflow: hidden;
  }
  .log-panel::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--cyan), transparent);
    animation: scanLine 3s linear infinite;
  }
  .log-key   { color: var(--cyan); }
  .log-val   { color: var(--white); }
  .log-comment { color: var(--dim); }

  /* ── CLASSIFIED ── */
  .classified {
    border: 1px solid #ff334488;
    background: #1a00044a;
    border-radius: 6px;
    padding: 24px 28px;
    font-size: .82rem;
    line-height: 1.9;
    animation: fadeUp .8s .2s ease both;
    position: relative;
  }
  .classified-header {
    font-family: 'Orbitron', sans-serif;
    font-size: .75rem;
    color: #ff4455;
    letter-spacing: .3em;
    margin-bottom: 14px;
    animation: blink 1.2s step-end infinite;
  }
  .classified span { color: var(--cyan2); }
  .threat { color: #ff4455; font-weight: bold; }

  /* ── CONNECT ── */
  .connect-links {
    display: flex;
    justify-content: center;
    gap: 16px;
    flex-wrap: wrap;
    animation: fadeUp .8s .2s ease both;
  }
  .connect-btn {
    background: #08082a;
    border: 1px solid var(--dim);
    color: var(--cyan);
    text-decoration: none;
    font-family: 'Orbitron', sans-serif;
    font-size: .65rem;
    letter-spacing: .2em;
    padding: 12px 22px;
    border-radius: 4px;
    transition: all .3s;
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .connect-btn:hover {
    border-color: var(--cyan);
    background: #0d0d3a;
    box-shadow: 0 0 20px #00cfff33;
    transform: translateY(-3px);
  }

  /* ── FOOTER ── */
  .footer {
    text-align: center;
    margin-top: 60px;
    padding: 28px;
    border-top: 1px solid #1a1a3a;
    font-size: .72rem;
    color: var(--dim);
    letter-spacing: .15em;
  }
  .footer span { color: var(--cyan); }

  /* ── SCAN LINE OVERLAY ── */
  body::after {
    content: '';
    position: fixed;
    top: -100%; left: 0;
    width: 100%; height: 4px;
    background: linear-gradient(transparent, #00cfff18, transparent);
    animation: globalScan 6s linear infinite;
    pointer-events: none;
    z-index: 999;
  }

  /* ── KEYFRAMES ── */
  @keyframes fadeDown { from { opacity:0; transform:translateY(-24px); } to { opacity:1; transform:none; } }
  @keyframes fadeUp   { from { opacity:0; transform:translateY(24px);  } to { opacity:1; transform:none; } }
  @keyframes glowPulse { 0%,100% { filter:drop-shadow(0 0 18px #00cfff88); } 50% { filter:drop-shadow(0 0 34px #00cfffcc); } }
  @keyframes blink    { 0%,100% { border-color: var(--cyan); } 50% { border-color: transparent; } }
  @keyframes scanLine { 0% { left:-100%; } 100% { left:100%; } }
  @keyframes globalScan { 0% { top:-2%; } 100% { top:102%; } }
  @keyframes float    { 0%,100% { transform:translateY(0); } 50% { transform:translateY(-6px); } }
  @keyframes orbit    {
    0%   { transform: rotate(0deg)   translateX(140px) rotate(0deg); }
    100% { transform: rotate(360deg) translateX(140px) rotate(-360deg); }
  }
  @keyframes orbit2   {
    0%   { transform: rotate(120deg)  translateX(200px) rotate(-120deg); }
    100% { transform: rotate(480deg)  translateX(200px) rotate(-480deg); }
  }

  /* ── PLANET WIDGET ── */
  .planet-wrap {
    display: flex;
    justify-content: center;
    margin: 40px 0 10px;
    animation: fadeUp .8s ease both;
  }
  .planet-scene {
    position: relative;
    width: 300px;
    height: 300px;
  }
  .planet {
    position: absolute;
    top: 50%; left: 50%;
    width: 80px; height: 80px;
    transform: translate(-50%,-50%);
    background: radial-gradient(circle at 35% 35%, #1a4a7a, #04091a);
    border-radius: 50%;
    box-shadow: 0 0 30px #00cfff55, inset -10px -10px 20px #00000088;
    animation: float 4s ease-in-out infinite;
  }
  .planet::after {
    content: '';
    position: absolute;
    top: 50%; left: 50%;
    width: 120px; height: 22px;
    transform: translate(-50%,-50%) rotateX(70deg);
    background: transparent;
    border-radius: 50%;
    border: 2px solid #00cfff44;
    box-shadow: 0 0 12px #00cfff33;
  }
  .orbit-dot {
    position: absolute;
    top: 50%; left: 50%;
    width: 10px; height: 10px;
    margin: -5px;
    background: var(--cyan2);
    border-radius: 50%;
    box-shadow: 0 0 10px var(--cyan2);
    animation: orbit 5s linear infinite;
  }
  .orbit-dot2 {
    position: absolute;
    top: 50%; left: 50%;
    width: 7px; height: 7px;
    margin: -3.5px;
    background: var(--purple);
    border-radius: 50%;
    box-shadow: 0 0 10px var(--purple);
    animation: orbit2 8s linear infinite;
  }
</style>
</head>
<body>

<canvas id="stars-canvas"></canvas>

<div class="content">

  <!-- HERO -->
  <div class="hero">
    <div class="hero-name">BENFARAG</div>
    <div class="hero-sub">Mobile · Web · Systems · Pixel Art · Linux</div>

    <div class="typing-wrap">
      <div class="typing-text" id="typing"></div>
    </div>

    <div class="badges">
      <div class="badge">📍 LOW EARTH ORBIT</div>
      <div class="badge">🟢 STATUS: ONLINE</div>
      <div class="badge">🛸 MISSION: ACTIVE</div>
    </div>
  </div>

  <!-- PLANET -->
  <div class="planet-wrap">
    <div class="planet-scene">
      <div class="planet"></div>
      <div class="orbit-dot"></div>
      <div class="orbit-dot2"></div>
    </div>
  </div>

  <!-- MISSION LOADOUT -->
  <div class="section-title">🛸 MISSION LOADOUT</div>
  <table class="mission-table">
    <tr>
      <th>SYSTEM</th><th>MODULE</th><th>STATUS</th>
    </tr>
    <tr>
      <td>📱 Mobile Core</td>
      <td>
        <span class="pill pill-mobile">Flutter</span>
        <span class="pill pill-mobile">Dart</span>
      </td>
      <td class="status">🟢 ACTIVE</td>
    </tr>
    <tr>
      <td>🌐 Web Interface</td>
      <td>
        <span class="pill pill-web">HTML5</span>
        <span class="pill pill-web">CSS3</span>
      </td>
      <td class="status">🟢 ACTIVE</td>
    </tr>
    <tr>
      <td>⚙️ Systems Core</td>
      <td><span class="pill pill-sys">C Language</span></td>
      <td class="status">🟡 TRAINING</td>
    </tr>
    <tr>
      <td>🎨 Art Engine</td>
      <td><span class="pill pill-art">Aseprite</span></td>
      <td class="status">🟢 ACTIVE</td>
    </tr>
    <tr>
      <td>🔧 Navigation</td>
      <td>
        <span class="pill pill-nav">Git</span>
        <span class="pill pill-art">Linux</span>
        <span class="pill pill-mobile">Fedora</span>
      </td>
      <td class="status">🟢 ACTIVE</td>
    </tr>
    <tr>
      <td>📡 Intel Feed</td>
      <td><span class="pill pill-intel">edX</span></td>
      <td class="status">🔵 SCANNING</td>
    </tr>
  </table>

  <!-- SKILL MATRIX -->
  <div class="section-title">📡 SKILL MATRIX</div>
  <div class="skill-bars" id="skill-bars">
    <div class="skill-row"><div class="skill-label">📱 Flutter + Dart</div><div class="bar-track"><div class="bar-fill" data-pct="80"></div></div><div class="bar-pct">80%</div></div>
    <div class="skill-row"><div class="skill-label">🌐 HTML + CSS</div><div class="bar-track"><div class="bar-fill" data-pct="70"></div></div><div class="bar-pct">70%</div></div>
    <div class="skill-row"><div class="skill-label">💻 C Language</div><div class="bar-track"><div class="bar-fill" data-pct="60"></div></div><div class="bar-pct">60%</div></div>
    <div class="skill-row"><div class="skill-label">🎨 Aseprite</div><div class="bar-track"><div class="bar-fill" data-pct="55"></div></div><div class="bar-pct">55%</div></div>
    <div class="skill-row"><div class="skill-label">🔧 Git</div><div class="bar-track"><div class="bar-fill" data-pct="80"></div></div><div class="bar-pct">80%</div></div>
    <div class="skill-row"><div class="skill-label">🐧 Linux / Fedora</div><div class="bar-track"><div class="bar-fill" data-pct="90"></div></div><div class="bar-pct">90%</div></div>
  </div>

  <!-- CAPTAIN'S LOG -->
  <div class="section-title">🌌 CAPTAIN'S LOG</div>
  <div class="log-panel">
    <div><span class="log-key">STARDATE</span>  <span class="log-val">2025</span>  <span class="log-comment">// mission initiated</span></div>
    <div><span class="log-key">MISSION  </span>  <span class="log-val">Build. Learn. Ship.</span></div>
    <div>&nbsp;</div>
    <div><span class="log-key">&gt; Flutter + Dart</span>  <span class="log-comment">// deploying apps across all platforms</span></div>
    <div><span class="log-key">&gt; C Language   </span>  <span class="log-comment">// speaking to the machine at metal level</span></div>
    <div><span class="log-key">&gt; Aseprite     </span>  <span class="log-comment">// drawing every pixel by hand</span></div>
    <div><span class="log-key">&gt; Linux/Fedora </span>  <span class="log-comment">// living in the terminal, not just using it</span></div>
    <div><span class="log-key">&gt; Git          </span>  <span class="log-comment">// every commit tells a story</span></div>
    <div>&nbsp;</div>
    <div><span class="log-key">CREW SIZE</span>  <span class="log-val">1</span>  <span class="log-comment">// solo dev. full stack. full art. full control.</span></div>
  </div>

  <!-- CLASSIFIED -->
  <div class="section-title">☄️ CLASSIFIED INTEL</div>
  <div class="classified">
    <div class="classified-header">⚠️  SIGNAL INTERCEPTED — LEVEL 5 CLEARANCE  ⚠️</div>
    <div>Subject: <span>BENFARAG</span></div>
    <div>Analyst Report:</div>
    <div>&nbsp;</div>
    <div>Subject possesses a <span>rare multi-domain stack</span> —</div>
    <div>&nbsp;&nbsp;Mobile Dev  +  Systems Programmer  +  Pixel Artist</div>
    <div>&nbsp;</div>
    <div>This combination maps directly to:</div>
    <div>&nbsp;&nbsp;<span>→ Indie Game Developer</span> (solo capable)</div>
    <div>&nbsp;&nbsp;<span>→ Cross-platform App Creator</span></div>
    <div>&nbsp;&nbsp;<span>→ Full creative + technical ownership</span></div>
    <div>&nbsp;</div>
    <div>Missing coordinate: <span>Godot Engine</span></div>
    <div>Once acquired → mission becomes <span>COMPLETE</span>.</div>
    <div>&nbsp;</div>
    <div>Threat Level to competitors: <span class="threat">SEVERE 🔴</span></div>
  </div>

  <!-- CONNECT -->
  <div class="section-title">🛰️ OPEN CHANNEL</div>
  <div class="connect-links">
    <a class="connect-btn" href="#">⟁ LINKEDIN</a>
    <a class="connect-btn" href="#">⟁ GITHUB</a>
    <a class="connect-btn" href="#">⟁ GMAIL</a>
  </div>

  <div class="footer">
    <div>⭐ <span>STAR A REPO</span> — FUEL THE MISSION ⭐</div>
    <div style="margin-top:8px;">© BENFARAG · ALL SYSTEMS OPERATIONAL</div>
  </div>

</div>

<script>
// ── STARFIELD ──
const canvas = document.getElementById('stars-canvas');
const ctx = canvas.getContext('2d');
let stars = [];

function resize() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

for (let i = 0; i < 220; i++) {
  stars.push({
    x: Math.random(),
    y: Math.random(),
    r: Math.random() * 1.4 + .2,
    speed: Math.random() * .0003 + .00005,
    alpha: Math.random() * .7 + .3,
    twinkle: Math.random() * Math.PI * 2,
    twinkleSpeed: Math.random() * .03 + .01
  });
}

function drawStars(t) {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  stars.forEach(s => {
    s.twinkle += s.twinkleSpeed;
    s.y += s.speed;
    if (s.y > 1) { s.y = 0; s.x = Math.random(); }
    const alpha = s.alpha * (.6 + .4 * Math.sin(s.twinkle));
    ctx.beginPath();
    ctx.arc(s.x * canvas.width, s.y * canvas.height, s.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(180,210,255,${alpha})`;
    ctx.fill();
  });
  requestAnimationFrame(drawStars);
}
drawStars();

// ── TYPING ANIMATION ──
const lines = [
  'Flutter & Dart Developer 💙',
  'Pixel Artist with Aseprite 🎨',
  'C Programmer — close to metal 🖥️',
  'Linux / Fedora Power User 🐧',
  'Building cross-platform experiences 🚀',
];
let li = 0, ci = 0, deleting = false;
const el = document.getElementById('typing');

function type() {
  const line = lines[li];
  if (!deleting) {
    el.textContent = line.slice(0, ++ci);
    if (ci === line.length) { deleting = true; setTimeout(type, 2000); return; }
    setTimeout(type, 60);
  } else {
    el.textContent = line.slice(0, --ci);
    if (ci === 0) { deleting = false; li = (li + 1) % lines.length; setTimeout(type, 400); return; }
    setTimeout(type, 30);
  }
}
setTimeout(type, 800);

// ── SKILL BARS ──
function animateBars() {
  document.querySelectorAll('.bar-fill').forEach(bar => {
    bar.style.width = bar.dataset.pct + '%';
  });
}
setTimeout(animateBars, 600);
</script>
</body>
</html>
