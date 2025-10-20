<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Happy Birthday — A Personal Journey</title>
<meta name="description" content="An immersive, modern, interactive birthday greeting — customize the message, follow the guided journey, and celebrate!" />
<style>
  :root{
    --bg-1: #0b0f14;
    --bg-2: #0f1720;
    --accent: #ff6bcb;
    --accent-2: #7be7ff;
    --glass: rgba(255,255,255,0.04);
    --muted: rgba(255,255,255,0.65);
    --card-radius: 18px;
    --glass-2: rgba(255,255,255,0.03);
    --shadow: 0 10px 30px rgba(2,6,23,0.6);
    --glow: 0 6px 30px rgba(127, 82, 255, 0.12);
    font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
  }

  *{box-sizing:border-box}
  html,body{height:100%}
  body{
    margin:0;
    background: radial-gradient(1200px 600px at 10% 10%, rgba(123,231,255,0.04), transparent 5%),
                radial-gradient(800px 400px at 90% 80%, rgba(255,107,203,0.03), transparent 5%),
                linear-gradient(180deg, var(--bg-1) 0%, var(--bg-2) 100%);
    color:#f5f7fb;
    -webkit-font-smoothing:antialiased;
    -moz-osx-font-smoothing:grayscale;
    padding:32px;
    display:flex;
    align-items:center;
    justify-content:center;
    overflow:hidden;
  }

  /* Container */
  .stage{
    width:min(980px, 96vw);
    max-width:1200px;
    min-height:640px;
    border-radius:22px;
    padding:28px;
    position:relative;
    overflow:hidden;
    box-shadow:var(--shadow);
    background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    backdrop-filter: blur(8px) saturate(120%);
    border:1px solid rgba(255,255,255,0.03);
    display:grid;
    grid-template-columns: 1fr 420px;
    gap:24px;
  }

  /* Left main */
  .main{
    padding:28px;
    display:flex;
    flex-direction:column;
    gap:18px;
  }

  .header{
    display:flex;
    gap:16px;
    align-items:center;
  }

  .portrait{
    width:84px;height:84px;border-radius:16px;
    background: linear-gradient(135deg, rgba(255,255,255,0.04), rgba(255,255,255,0.02));
    border:1px solid rgba(255,255,255,0.04);
    display:flex;align-items:center;justify-content:center;
    position:relative;
    overflow:hidden;
    box-shadow:var(--glow);
    flex-shrink:0;
  }

  .portrait svg{width:72px;height:72px;opacity:0.95;filter:drop-shadow(0 8px 26px rgba(0,0,0,0.4))}

  .title{
    display:flex;flex-direction:column;gap:6px;
  }

  .title h1{
    margin:0;font-size:20px;letter-spacing:-0.02em;
    font-weight:700;
  }

  .subtitle{
    font-size:13px;color:var(--muted);
  }

  /* Personalized message card */
  .card{
    background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));
    padding:20px;border-radius:14px;border:1px solid rgba(255,255,255,0.03);
    box-shadow: 0 6px 20px rgba(2,6,23,0.45);
  }

  .personal-message{
    display:flex;flex-direction:column;gap:12px;
  }

  .message-top{
    display:flex;gap:12px;align-items:center;
  }

  .name-display{
    font-size:28px;font-weight:800;
    letter-spacing:-0.01em;
    background: linear-gradient(90deg,var(--accent),var(--accent-2));
    -webkit-background-clip:text;background-clip:text;color:transparent;
    text-shadow: 0 2px 14px rgba(123,231,255,0.04);
  }

  .message-line{
    font-size:14px;color:var(--muted);max-width:70%;
  }

  .typewriter{
    font-family: "Courier New", monospace;
    font-size:15px;
    margin-top:6px;
    color: #ffecf8;
    opacity:0.95;
  }

  .controls{
    display:flex;gap:10px;align-items:center;margin-top:12px;
  }

  .input{
    display:flex;gap:10px;align-items:center;width:100%;
  }

  .input input[type="text"], .input input[type="search"]{
    flex:1;padding:10px 12px;border-radius:10px;background:var(--glass);
    border:1px solid rgba(255,255,255,0.03);color:inherit;font-size:14px;
    outline:none;
  }
  .btn{
    padding:10px 14px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);
    background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    cursor:pointer;font-weight:600;font-size:13px;
  }
  .btn:active{transform:translateY(1px)}

  .small{
    font-size:12px;color:var(--muted);
  }

  /* Journey area */
  .journey{
    margin-top:12px;display:flex;flex-direction:column;gap:12px;
  }

  .steps{
    display:flex;gap:10px;flex-wrap:wrap;
  }
  .step{
    flex:0 0 48%;
    background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));
    padding:14px;border-radius:12px;border:1px solid rgba(255,255,255,0.03);
    cursor:pointer;transition:transform .28s cubic-bezier(.2,.9,.2,1), box-shadow .28s;
    position:relative;overflow:hidden;
  }
  .step:not(.unlocked){opacity:0.5;filter:grayscale(0.1)}
  .step:hover{transform:translateY(-6px)}
  .step h3{margin:0;font-size:15px}
  .step p{margin:6px 0 0;font-size:13px;color:var(--muted)}

  .step .badge{
    position:absolute;top:12px;right:12px;padding:6px 8px;border-radius:999px;font-weight:700;
    font-size:12px;background:linear-gradient(90deg,var(--accent),var(--accent-2));
    color:#071223;box-shadow:0 8px 18px rgba(123,107,255,0.12)
  }

  /* Right column */
  .side{
    padding:22px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.015), rgba(255,255,255,0.007));
    border:1px solid rgba(255,255,255,0.03);display:flex;flex-direction:column;gap:14px;
  }

  .preview{
    height:260px;border-radius:12px;display:flex;flex-direction:column;align-items:center;justify-content:center;
    border:1px dashed rgba(255,255,255,0.03);
    position:relative;overflow:hidden;background:linear-gradient(180deg, rgba(123,231,255,0.02), rgba(255,107,203,0.02));
  }

  .preview .heart-emoji{font-size:42px;margin-bottom:8px}
  .preview h4{margin:0;font-size:16px}
  .preview p{margin:6px 18px 0;text-align:center;color:var(--muted);font-size:13px}

  .share{
    display:flex;gap:8px;align-items:center;flex-wrap:wrap;
  }

  .toggle{
    display:flex;gap:8px;align-items:center;
  }

  /* Footer actions */
  .actions{display:flex;gap:10px;align-items:center;flex-wrap:wrap}
  .download{
    padding:10px 12px;border-radius:12px;background:linear-gradient(90deg,#1b1e28,#12151a);border:1px solid rgba(255,255,255,0.02);
    font-weight:700;cursor:pointer;
  }

  /* Confetti / canvas overlay */
  canvas#hearts, canvas#confetti{
    position:absolute;inset:0;width:100%;height:100%;pointer-events:none;z-index:1;
  }

  /* Modal / final card */
  .overlay{
    position:absolute;inset:0;display:grid;place-items:center;z-index:40;pointer-events:none;
  }
  .surprise{
    pointer-events:auto;max-width:900px;width:min(92%,980px);border-radius:18px;padding:28px;background:linear-gradient(180deg, rgba(10,12,16,0.9), rgba(12,16,22,0.98));
    box-shadow:0 40px 120px rgba(2,6,23,0.8);border:1px solid rgba(255,255,255,0.03);transform:translateY(16px) scale(.98);
    opacity:0;transition:all .45s cubic-bezier(.2,.9,.2,1);
  }
  .surprise.show{opacity:1;transform:translateY(0) scale(1)}
  .surprise .hero{
    display:flex;gap:18px;align-items:center;
  }
  .surprise .hero .bigname{
    font-size:34px;font-weight:900;line-height:1;
    background:linear-gradient(90deg,var(--accent),var(--accent-2));
    -webkit-background-clip:text;background-clip:text;color:transparent;
  }
  .surprise p{color:var(--muted);margin-top:8px;font-size:15px}

  /* Responsive */
  @media (max-width:980px){
    .stage{grid-template-columns:1fr;min-height:720px}
    .side{order:-1}
  }

  /* micro-animations */
  .pulse{
    animation: pulse 3.6s ease-in-out infinite;
  }
  @keyframes pulse{
    0%{transform:scale(1);opacity:1}
    50%{transform:scale(1.015);opacity:0.98}
    100%{transform:scale(1);opacity:1}
  }

  /* tiny glass tags */
  .tag{
    display:inline-block;padding:6px 10px;border-radius:999px;background:var(--glass-2);border:1px solid rgba(255,255,255,0.02);
    font-size:12px;color:var(--muted)
  }

  /* subtle floating */
  .float{
    animation: floaty 8s ease-in-out infinite;
  }
  @keyframes floaty{
    0%{transform:translateY(0)}
    50%{transform:translateY(-8px)}
    100%{transform:translateY(0)}
  }

  /* small helper */
  .muted{color:var(--muted)}
  .center{text-align:center}

</style>
</head>
<body>
  <div class="stage" id="stage" role="application" aria-label="Interactive birthday greeting">
    <!-- draw hearts & confetti canvases -->
    <canvas id="hearts" aria-hidden="true"></canvas>
    <canvas id="confetti" aria-hidden="true"></canvas>

    <main class="main" aria-live="polite">
      <div class="header">
        <div class="portrait float" aria-hidden="true">
          <!-- soft artist svg heart -->
          <svg viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg" role="img" aria-hidden="true">
            <defs>
              <linearGradient id="g1" x1="0" x2="1">
                <stop offset="0" stop-color="#ff6bcb"/>
                <stop offset="1" stop-color="#7be7ff"/>
              </linearGradient>
            </defs>
            <rect x="0" y="0" width="64" height="64" rx="12" fill="url(#g1)" opacity="0.14"></rect>
            <path d="M32 46s-14.5-9.2-19-13.8C6 26 12 16 21.5 18 26 19.4 28.3 23.8 32 26c3.7-2.2 6-6.6 10.5-8 9.5-2 15.5 8 8.5 14.2C46.6 36.8 32 46 32 46z" fill="#fff" opacity="0.95"/>
          </svg>
        </div>
        <div class="title">
          <h1 id="greetingH">Happy Birthday, <span id="namePreview">[Name]</span> 🎉</h1>
          <div class="subtitle">A curated, heartfelt experience — tap each step and reveal a layer of the surprise.</div>
        </div>
      </div>

      <section class="card personal-message" aria-labelledby="personalHeading">
        <div class="message-top">
          <div style="flex:1">
            <div class="name-display" id="nameBig">[Name]</div>
            <div class="message-line" id="topLine">You are the light of my world — wishing you endless love and joy today!</div>
            <div class="typewriter" id="typewriter" aria-hidden="false"></div>
          </div>

          <div style="width:140px;display:flex;flex-direction:column;align-items:flex-end;gap:8px">
            <div class="tag">Dark mode • 2025 aesthetic</div>
            <div class="small muted center" style="max-width:140px">Tip: personalize the message and press <strong>Share</strong> to generate a link.</div>
          </div>
        </div>

        <div class="controls">
          <div class="input" role="form" aria-label="Customize message">
            <input id="nameInput" type="text" placeholder="Enter their name (e.g., Aisha)" aria-label="Recipient name" />
            <input id="messageInput" type="text" placeholder='Customize the top message (e.g., "You light up my life")' aria-label="Top message" />
            <button class="btn" id="applyBtn" title="Apply changes">Apply</button>
          </div>
        </div>

        <div class="journey" aria-hidden="false">
          <div class="small muted">Guided Journey — click each unlocked step to reveal the memory, note, or surprise.</div>
          <div class="steps" id="steps">
            <div class="step unlocked" data-step="1" tabindex="0" role="button" aria-pressed="false">
              <div class="badge">1</div>
              <h3>A Little Memory</h3>
              <p>Open to read one of the sweetest memories you share.</p>
            </div>

            <div class="step unlocked" data-step="2" tabindex="0" role="button" aria-pressed="false">
              <div class="badge">2</div>
              <h3>Compliment & Promise</h3>
              <p>A heartfelt compliment and a promise for tomorrow.</p>
            </div>

            <div class="step" data-step="3" tabindex="0" role="button" aria-pressed="false">
              <div class="badge">3</div>
              <h3>Secret Gift</h3>
              <p>Reveal a small surprise — click to unveil.</p>
            </div>

            <div class="step" data-step="4" tabindex="0" role="button" aria-pressed="false">
              <div class="badge">4</div>
              <h3>The Finale</h3>
              <p>Confetti, music, and a personalized closing embrace.</p>
            </div>
          </div>
        </div>

      </section>

      <!-- Right column -->
    </main>

    <aside class="side" aria-label="Controls and preview">
      <div class="preview center">
        <div class="heart-emoji" aria-hidden="true">💖</div>
        <h4 id="previewTitle">You're the reason I smile</h4>
        <p id="previewLine" class="muted">“🎂 Wishing you a day filled with love, laughter, and sweet memories 💖”</p>

        <!-- floating sparkles -->
        <svg style="position:absolute;right:8px;bottom:8px;opacity:0.08" width="160" height="120" viewBox="0 0 160 120" fill="none" aria-hidden="true">
          <circle cx="24" cy="22" r="12" fill="#ff6bcb"></circle>
          <circle cx="72" cy="72" r="18" fill="#7be7ff"></circle>
          <circle cx="132" cy="40" r="8" fill="#a78bfa"></circle>
        </svg>
      </div>

      <div>
        <div class="small muted" style="margin-bottom:8px">Share & Experience</div>
        <div class="share">
          <button class="btn" id="shareBtn" title="Share a link">Share (link)</button>
          <button class="btn" id="copyBtn" title="Copy message">Copy Message</button>
          <button class="btn" id="downloadBtn" title="Download card">Download Card</button>
        </div>

        <div style="height:12px"></div>

        <div class="small muted" style="margin-bottom:8px">Play ambient</div>
        <div class="actions">
          <button class="btn" id="playMusic">Play Music</button>
          <button class="btn" id="stopMusic">Stop</button>
          <button class="btn" id="toggleHearts">Toggle Hearts</button>
        </div>
      </div>

      <div style="margin-top:6px">
        <div class="small muted">Accessibility</div>
        <div style="display:flex;gap:8px;margin-top:8px">
          <button class="btn" id="prefersReduced" title="Reduce animations">Reduce Motion</button>
          <button class="btn" id="resetBtn" title="Reset to defaults">Reset</button>
        </div>
      </div>

      <div style="margin-top:auto" class="small muted center">Designed with care • 2025 modern UI • Dark aesthetic</div>
    </aside>

    <!-- Surprise overlay -->
    <div class="overlay" id="overlay" aria-hidden="true">
      <div class="surprise" role="dialog" aria-modal="true" aria-label="Surprise card" id="surpriseCard">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div class="tag">Surprise</div>
          <div style="display:flex;gap:8px">
            <button class="btn" id="closeSurprise">Close</button>
            <button class="btn" id="finalDownload">Save</button>
          </div>
        </div>

        <div class="hero" style="margin-top:14px">
          <div style="flex:1">
            <div class="bigname" id="surpriseName">[Name]</div>
            <p id="surpriseText">You make ordinary moments feel like magic. Thank you for being you. Let's make this year unforgettable — all my love, today and always.</p>
          </div>
          <div style="width:160px;text-align:right">
            <svg viewBox="0 0 120 120" width="120" height="120" aria-hidden="true">
              <defs><linearGradient id="sg" x1="0" x2="1"><stop offset="0" stop-color="#ff6bcb"/><stop offset="1" stop-color="#7be7ff"/></linearGradient></defs>
              <rect x="0" y="0" width="120" height="120" rx="20" fill="url(#sg)" opacity="0.08"></rect>
              <path d="M60 88s-20-12.8-26-19.8C18 48 28 34 42 36c6.9 1.5 9.4 6.9 18 9.6 8.6-2.7 11.1-8.1 18-9.6C92 34 102 48 86 68.2 80 75.2 60 88 60 88z" fill="#fff" opacity="0.95"/>
            </svg>
          </div>
        </div>

      </div>
    </div>

  </div>

<script>
/* ======================
   Interactive Birthday Site
   Single-file, modern 2025 aesthetic
   Features:
   - Personalization (name + message)
   - Typewriter line
   - Falling hearts canvas
   - Guided steps that unlock & show a modal
   - Confetti finale, downloadable card (PNG)
   - Shareable link via URL hash
   - Simple ambient music (user-play)
   ====================== */

(() => {
  // Helpers
  const $ = sel => document.querySelector(sel);
  const $$ = sel => Array.from(document.querySelectorAll(sel));
  const nameInput = $('#nameInput');
  const messageInput = $('#messageInput');
  const applyBtn = $('#applyBtn');
  const namePreview = $('#namePreview');
  const nameBig = $('#nameBig');
  const topLine = $('#topLine');
  const typewriterEl = $('#typewriter');
  const previewTitle = $('#previewTitle');
  const previewLine = $('#previewLine');

  const heartsCanvas = document.getElementById('hearts');
  const confettiCanvas = document.getElementById('confetti');
  const overlay = $('#overlay');
  const surpriseCard = $('#surpriseCard');
  const surpriseName = $('#surpriseName');
  const surpriseText = $('#surpriseText');

  // Default content
  const defaults = {
    name: 'Beloved',
    message: 'You are the light of my world — wishing you endless love and joy today!',
    typewriter: '🎂 Wishing you a day filled with love, laughter, and sweet memories 💖'
  };

  // Read name from URL hash if present
  function readFromHash() {
    try {
      const h = location.hash.slice(1);
      if(!h) return null;
      const parts = new URLSearchParams(h);
      return {
        name: parts.get('n') || null,
        message: parts.get('m') ? decodeURIComponent(parts.get('m')) : null
      };
    } catch(e) { return null; }
  }

  function applyValues({name, message} = {}) {
    if(!name) name = defaults.name;
    if(!message) message = defaults.message;
    namePreview.textContent = name;
    nameBig.textContent = name;
    topLine.textContent = message;
    previewTitle.textContent = message.split('—')[0] || message;
    previewLine.textContent = defaults.typewriter;
    surpriseName.textContent = name;
    // store current values on window for downloads & share
    window._greetingState = {name, message};
    // update typewriter (restart)
    startTypewriter(defaults.typewriter, typewriterEl);
  }

  // Build share link
  function buildShareLink() {
    const s = window._greetingState || defaults;
    const params = new URLSearchParams();
    if(s.name) params.set('n', s.name);
    if(s.message) params.set('m', encodeURIComponent(s.message));
    const url = `${location.origin}${location.pathname}#${params.toString()}`;
    return url;
  }

  // Typewriter effect (fade + write)
  let twTimer = null;
  function startTypewriter(text, el) {
    if(twTimer) { clearInterval(twTimer); twTimer = null; }
    el.textContent = '';
    el.style.opacity = '1';
    let i = 0;
    twTimer = setInterval(() => {
      i++;
      el.textContent = text.slice(0, i);
      if(i >= text.length) {
        clearInterval(twTimer);
        twTimer = null;
      }
    }, 28);
  }

  // Apply button handler
  applyBtn.addEventListener('click', () => {
    const name = (nameInput.value || '').trim() || defaults.name;
    const message = (messageInput.value || '').trim() || defaults.message;
    applyValues({name, message});
    // update hash for sharing convenience
    const params = new URLSearchParams();
    params.set('n', name);
    if(message) params.set('m', encodeURIComponent(message));
    history.replaceState(null,'', '#' + params.toString());
  });

  // Initialize from hash or defaults
  const fromHash = readFromHash();
  if(fromHash && (fromHash.name || fromHash.message)) {
    applyValues({name: fromHash.name || defaults.name, message: fromHash.message || defaults.message});
  } else {
    applyValues(defaults);
  }

  // Steps interaction
  const steps = $$('.step');
  function unlockStep(n) {
    const s = steps.find(st => st.dataset.step == n);
    if(!s) return;
    s.classList.add('unlocked'); s.style.opacity = '1';
  }

  // Pre-unlock step 1 and 2 already in markup. We'll unlock 3 after 2 clicked, 4 after 3 clicked.
  let highestUnlocked = 2;
  function handleStepClick(e) {
    const el = e.currentTarget;
    const step = parseInt(el.dataset.step, 10);
    if(step > highestUnlocked) {
      // show gentle shake to indicate locked
      el.animate([{transform:'translateY(0)'},{transform:'translateY(-6px)'},{transform:'translateY(3px)'},{transform:'translateY(0)'}], {duration:420, easing:'ease-out'});
      return;
    }
    openStep(step);
  }

  function openStep(step) {
    if(step === 1) {
      // show memory modal-like reveal (small)
      showMiniSurprise('Little Memory', `Remember the time we laughed until midnight? I still replay that night — you are my favorite memory.`);
      // unlock next if needed
      if(highestUnlocked < 3) { highestUnlocked = 3; unlockStep(3); }
    } else if(step === 2) {
      showMiniSurprise('Compliment & Promise', `You are kind, brilliant, and fiercely loving. I promise to be there for every sunrise and late-night talk.`);
      if(highestUnlocked < 3) { highestUnlocked = 3; unlockStep(3); }
    } else if(step === 3) {
      showMiniSurprise('Secret Gift', `A little surprise awaits — check your messages later ;)`, true);
      if(highestUnlocked < 4) { highestUnlocked = 4; unlockStep(4); }
    } else if(step === 4) {
      // final: show big overlay with confetti and music
      showFinalSurprise();
    }
  }

  // attach handlers
  steps.forEach(s => s.addEventListener('click', handleStepClick));
  steps.forEach(s => s.addEventListener('keydown', e => { if(e.key === 'Enter' || e.key === ' ') { e.preventDefault(); handleStepClick({currentTarget:s}); }}));

  // Mini surprise (small overlay)
  let miniTimer = null;
  function showMiniSurprise(title, text, triggerConfetti=false) {
    surpriseName.textContent = title;
    surpriseText.textContent = text;
    overlay.style.pointerEvents = 'auto';
    overlay.setAttribute('aria-hidden','false');
    surpriseCard.classList.add('show');
    // auto-hide after some seconds
    if(miniTimer) clearTimeout(miniTimer);
    miniTimer = setTimeout(() => {
      closeSurprise();
      if(triggerConfetti) triggerConfettiBurst();
    }, 4200);
  }

  function closeSurprise() {
    surpriseCard.classList.remove('show');
    overlay.style.pointerEvents = 'none';
    overlay.setAttribute('aria-hidden','true');
    if(miniTimer) { clearTimeout(miniTimer); miniTimer=null; }
  }

  $('#closeSurprise').addEventListener('click', closeSurprise);

  // Final surprise
  function showFinalSurprise() {
    surpriseName.textContent = window._greetingState?.name || defaults.name;
    surpriseText.textContent = `You make ordinary moments feel like magic. Thank you for being you. Let's make this year unforgettable — all my love, today and always.`;
    overlay.style.pointerEvents = 'auto';
    surpriseCard.classList.add('show');
    overlay.setAttribute('aria-hidden','false');
    // confetti + hearts
    triggerConfettiBurst();
    hearts.startBigPulse();
  }

  $('#finalDownload').addEventListener('click', () => {
    // generate PNG of the surprise card
    downloadCardImage();
  });

  // Share / copy / download
  $('#shareBtn').addEventListener('click', () => {
    const url = buildShareLink();
    prompt('Share this link with them:', url);
  });

  $('#copyBtn').addEventListener('click', async () => {
    const s = window._greetingState || defaults;
    const text = `Happy Birthday, ${s.name}!\n\n${s.message}\n\n${defaults.typewriter}\n\n— Sent with ❤️`;
    try {
      await navigator.clipboard.writeText(text);
      alert('Message copied to clipboard');
    } catch(e) {
      prompt('Copy this message:', text);
    }
  });

  // Download card as PNG (draw the surpriseCard area to canvas)
  async function downloadCardImage() {
    // We'll snapshot the surpriseCard element using foreignObject technique
    // Build an SVG containing the HTML via foreignObject
    const el = surpriseCard.cloneNode(true);
    // Remove interactive elements that might not render nicely
    const buttons = el.querySelectorAll('button'); buttons.forEach(b => b.remove());
    const width = 1200, height = 700;
    // Inline CSS style string: take computed styles of body to mimic theme
    const cssText = Array.from(document.styleSheets).reduce((acc, sheet) => {
      try {
        const rules = sheet.cssRules || sheet.rules;
        if(!rules) return acc;
        return acc + Array.from(rules).map(r => r.cssText).join(' ');
      } catch(e) { return acc; }
    }, '');
    const svg = `
      <svg xmlns="http://www.w3.org/2000/svg" width="${width}" height="${height}">
        <foreignObject width="100%" height="100%">
          <div xmlns="http://www.w3.org/1999/xhtml" style="width:${width}px;height:${height}px;display:flex;align-items:center;justify-content:center;">
            <div style="width:92%;height:84%;border-radius:20px;padding:28px;background:linear-gradient(180deg, rgba(10,12,16,0.96), rgba(12,16,22,0.98));color:#fff;font-family:Inter, sans-serif;">
              ${el.innerHTML}
            </div>
          </div>
        </foreignObject>
      </svg>`;
    const blob = new Blob([svg], {type:'image/svg+xml;charset=utf-8'});
    const url = URL.createObjectURL(blob);
    const img = new Image();
    img.onload = () => {
      const c = document.createElement('canvas'); c.width = width; c.height = height;
      const ctx = c.getContext('2d');
      // fill with bg
      ctx.fillStyle = '#07090b'; ctx.fillRect(0,0,width,height);
      ctx.drawImage(img, 0, 0);
      URL.revokeObjectURL(url);
      // Save
      const a = document.createElement('a');
      a.download = `birthday-${(window._greetingState?.name||'friend').replace(/\s+/g,'_')}.png`;
      a.href = c.toDataURL('image/png');
      a.click();
    };
    img.src = url;
  }

  $('#downloadBtn').addEventListener('click', downloadCardImage);

  // Music (simple ambient using WebAudio: a soft pad)
  let audioCtx = null, musicNodes = null;
  $('#playMusic').addEventListener('click', async () => {
    if(!audioCtx) {
      audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    }
    if(musicNodes) return; // already playing
    const ctx = audioCtx;
    const master = ctx.createGain(); master.gain.value = 0.12; master.connect(ctx.destination);

    // create two detuned oscillators with reverb-like effect using Delay + feedback
    const o1 = ctx.createOscillator(); o1.type = 'sine'; o1.frequency.value = 220; // A3
    const o2 = ctx.createOscillator(); o2.type = 'sine'; o2.frequency.value = 277.18; // C#4
    o1.detune.value = -12; o2.detune.value = 10;

    const g1 = ctx.createGain(); g1.gain.value = 0;
    o1.connect(g1); g1.connect(master);
    const g2 = ctx.createGain(); g2.gain.value = 0;
    o2.connect(g2); g2.connect(master);

    // slow attack
    g1.gain.linearRampToValueAtTime(0.08, ctx.currentTime + 3);
    g2.gain.linearRampToValueAtTime(0.08, ctx.currentTime + 3);

    o1.start(); o2.start();

    musicNodes = {ctx, o1, o2, g1, g2, master};
  });

  $('#stopMusic').addEventListener('click', () => {
    if(!musicNodes) return;
    try {
      musicNodes.o1.stop();
      musicNodes.o2.stop();
    } catch(e){}
    musicNodes = null;
  });

  // hearts canvas animation
  const hearts = (function(){
    const c = heartsCanvas;
    const ctx = c.getContext('2d');
    let width=0, height=0;
    const particles = [];
    let running = true;
    function resize() {
      width = c.width = c.clientWidth * devicePixelRatio;
      height = c.height = c.clientHeight * devicePixelRatio;
      ctx.scale(devicePixelRatio, devicePixelRatio);
    }
    window.addEventListener('resize', resize);
    // heart path generator (parametric)
    function heartPath(size=12){
      const path = new Path2D();
      // draw simple heart shape
      const s = size;
      path.moveTo(0, -s*0.2);
      path.bezierCurveTo(-s/1.6, -s/1.3, -s, s*0.2, 0, s);
      path.bezierCurveTo(s, s*0.2, s/1.6, -s/1.3, 0, -s*0.2);
      return path;
    }
    function newParticle(x,y,opts={}) {
      const size = (Math.random()*10)+8;
      return {
        x, y,
        vx:(Math.random()-0.5)*0.6,
        vy: -(Math.random()*1.2+0.6),
        life: Math.random()*200+120,
        age:0,
        size,
        rotation: Math.random()*Math.PI*2,
        color: opts.color || (`hsl(${Math.random()*40+320}deg,70%,65%)`),
      }
    }
    function step() {
      if(!running) return;
      ctx.clearRect(0,0,c.width,c.height);
      ctx.save();
      ctx.globalCompositeOperation = 'lighter';
      // adapt to CSS pixel size (we already scaled)
      particles.forEach(p => {
        p.age++;
        p.vy += 0.01;
        p.x += p.vx;
        p.y += p.vy;
        p.rotation += 0.01;
        const alpha = Math.max(0, 1 - p.age / p.life);
        ctx.save();
        ctx.translate(p.x, p.y);
        ctx.rotate(p.rotation);
        ctx.globalAlpha = alpha;
        ctx.fillStyle = p.color;
        const path = heartPath(p.size);
        ctx.fill(path);
        ctx.restore();
      });
      // remove dead
      for(let i=particles.length-1;i>=0;i--) if(particles[i].age > particles[i].life) particles.splice(i,1);
      ctx.restore();
      requestAnimationFrame(step);
    }

    // generate gentle background float
    function spawnRandom(count=1) {
      for(let i=0;i<count;i++){
        const x = Math.random() * (c.clientWidth - 40) + 20;
        const y = c.clientHeight + 12;
        particles.push(newParticle(x,y));
      }
    }

    // periodic spawn
    let spawnInterval = setInterval(() => spawnRandom(2), 700);
    // larger pulse
    function startBigPulse(){
      spawnRandom(60);
      setTimeout(()=>spawnRandom(30), 300);
    }

    // public API
    resize();
    requestAnimationFrame(step);
    return {
      stop(){ running=false; clearInterval(spawnInterval); },
      start(){ if(!running){ running=true; requestAnimationFrame(step); spawnInterval = setInterval(()=>spawnRandom(2),700);} },
      toggle(){ running = !running; if(running) this.start(); else this.stop(); },
      startBigPulse
    }
  })();

  $('#toggleHearts').addEventListener('click', () => hearts.toggle());

  // Confetti canvas (for bursts)
  const confetti = (function(){
    const c = confettiCanvas;
    const ctx = c.getContext('2d');
    let width=0, height=0;
    const pieces = [];
    function resize(){ width=c.width=c.clientWidth*devicePixelRatio; height=c.height=c.clientHeight*devicePixelRatio; ctx.scale(devicePixelRatio, devicePixelRatio); }
    window.addEventListener('resize', resize);
    function spawnBurst(x= null, y = null, count = 80){
      if(x===null) x = c.clientWidth/2;
      if(y===null) y = c.clientHeight*0.35;
      for(let i=0;i<count;i++){
        const angle = Math.random()*Math.PI*2;
        const speed = Math.random()*6 + 2;
        pieces.push({
          x,y,
          vx: Math.cos(angle)*speed,
          vy: Math.sin(angle)*speed - (Math.random()*2),
          life: Math.random()*60+80,
          age:0,
          size: Math.random()*8+6,
          rotation: Math.random()*Math.PI*2,
          vr: (Math.random()-0.5)*0.2,
          color: ['#ff6bcb','#7be7ff','#a78bfa','#ffd86b'][Math.floor(Math.random()*4)]
        });
      }
      // auto fade after some time
      setTimeout(()=>{ /* noop */ }, 1000);
    }
    function step(){
      ctx.clearRect(0,0,c.width,c.height);
      ctx.save(); ctx.globalCompositeOperation='source-over';
      for(let i=pieces.length-1;i>=0;i--){
        const p = pieces[i];
        p.age++;
        p.vy += 0.12;
        p.vx *= 0.999;
        p.x += p.vx;
        p.y += p.vy;
        p.rotation += p.vr;
        const alpha = Math.max(0, 1 - p.age/p.life);
        ctx.globalAlpha = alpha;
        ctx.fillStyle = p.color;
        ctx.save();
        ctx.translate(p.x, p.y);
        ctx.rotate(p.rotation);
        ctx.fillRect(-p.size/2, -p.size/2, p.size, p.size*0.6);
        ctx.restore();
        if(p.age > p.life) pieces.splice(i,1);
      }
      ctx.restore();
      requestAnimationFrame(step);
    }
    resize();
    requestAnimationFrame(step);
    return {
      burst(x,y,count){ spawnBurst(x,y,count); },
    }
  })();

  function triggerConfettiBurst(){
    const rect = confettiCanvas.getBoundingClientRect();
    confetti.burst(rect.width/2, rect.height/3, 140);
  }

  // pref reduced motion
  const prefersReduced = $('#prefersReduced');
  prefersReduced.addEventListener('click', () => {
    document.documentElement.style.setProperty('transition-duration','0.001s');
    hearts.stop();
    alert('Animations minimized. Refresh page to fully reset.');
  });

  $('#resetBtn').addEventListener('click', () => {
    nameInput.value = '';
    messageInput.value = '';
    applyValues(defaults);
    history.replaceState(null,'', location.pathname);
    alert('Reset to defaults');
  });

  // small startup effect
  setTimeout(()=> {
    document.querySelectorAll('.step.unlocked').forEach((el,i) => {
      el.animate([{transform:'translateY(0)'},{transform:'translateY(-6px)'},{transform:'translateY(0)'}], {duration:800, delay:i*140, easing:'cubic-bezier(.2,.9,.2,1)'});
    });
  }, 400);

  // keyboard: space -> open next unlocked
  let nextStepToOpen = 1;
  document.addEventListener('keydown', e => {
    if(e.key === 'n') {
      // open next
      const st = document.querySelector(`.step[data-step="${nextStepToOpen}"]`);
      if(st && st.classList.contains('unlocked')) {
        st.click();
        nextStepToOpen++;
      }
    }
  });

  // accessibility: announce name changes
  const observer = new MutationObserver(() => {});
  // done

})();
</script>
</body>
</html>
