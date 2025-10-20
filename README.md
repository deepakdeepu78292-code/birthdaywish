<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>JAPPY BIRTHDAY MY LOVE — IMPU</title>
<style>
  :root{
    --bg:#06050a;
    --panel: rgba(255,255,255,0.04);
    --accent:#ff4db8;
    --accent-2:#ff83cf;
    --glass: rgba(255,255,255,0.03);
    --neon: 0 0 20px rgba(255,77,184,0.25), 0 0 40px rgba(255,131,207,0.12);
    --text:#f8f7fb;
    --muted: rgba(248,247,251,0.6);
    font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
  }

  html,body{height:100%;margin:0;background:linear-gradient(180deg,#05040a 0%, #0b0710 100%);color:var(--text);-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;}
  .stage{
    height:100vh;
    width:100%;
    position:relative;
    overflow:hidden;
    display:flex;
    align-items:center;
    justify-content:center;
  }

  /* Shared card */
  .card {
    width:min(980px,94%);
    max-width:1100px;
    border-radius:18px;
    background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    box-shadow: 0 10px 40px rgba(2,2,6,0.7);
    backdrop-filter: blur(10px) saturate(120%);
    padding:36px;
    position:relative;
    overflow:hidden;
    min-height:560px;
    display:flex;
    flex-direction:column;
    gap:18px;
  }

  /* Top title */
  .title {
    text-align:center;
    margin-top:8px;
    margin-bottom:6px;
  }
  .title h1{
    margin:0;
    font-size: clamp(28px, 4.6vw, 56px);
    letter-spacing:1px;
    line-height:1;
    font-weight:700;
    color:var(--text);
    text-shadow: 0 6px 24px rgba(0,0,0,0.7), var(--neon);
  }
  .subtitle{
    color:var(--muted);
    font-size:clamp(13px,1.6vw,16px);
    margin-top:8px;
  }

  /* name badge */
  .name-badge{
    display:inline-flex;
    gap:8px;
    align-items:center;
    margin-top:12px;
    justify-content:center;
  }
  .name {
    font-weight:800;
    color:var(--text);
    font-size: clamp(18px,2.5vw,22px);
    display:inline-flex;
    gap:8px;
    align-items:center;
    padding:8px 14px;
    border-radius:999px;
    background: linear-gradient(90deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    box-shadow: 0 6px 20px rgba(0,0,0,0.6);
  }
  .name .heart {
    width:20px;height:20px;border-radius:4px;
    display:inline-block;
    transform:translateY(1px);
    filter: drop-shadow(0 6px 20px rgba(255,77,184,0.15));
  }
  .name .star{
    font-size:14px;
    margin-left:4px;
    color: #ffd86b;
    text-shadow: 0 6px 20px rgba(255,216,107,0.08);
  }

  /* canvas layers fill */
  canvas{
    position:absolute;
    inset:0;
    width:100%;
    height:100%;
    display:block;
    pointer-events:none;
  }

  /* bottom prompt */
  .footer{
    margin-top:auto;
    display:flex;
    justify-content:center;
    align-items:center;
    gap:12px;
  }
  .btn {
    --pad:14px 26px;
    background: linear-gradient(90deg, rgba(255,77,184,0.14), rgba(255,131,207,0.08));
    border:1px solid rgba(255,255,255,0.06);
    color:var(--text);
    padding:var(--pad);
    border-radius:999px;
    font-weight:700;
    letter-spacing:0.6px;
    cursor:pointer;
    box-shadow: var(--neon), 0 6px 18px rgba(0,0,0,0.5);
    transition: transform .28s cubic-bezier(.2,.9,.3,1), opacity .22s;
    backdrop-filter: blur(6px);
  }
  .btn:active{ transform:translateY(2px) scale(.996); }
  .hint { color:var(--muted); font-size:13px; text-align:center; margin-top:6px; }

  /* page flip animation */
  .page {
    position:absolute;
    inset:18px;
    border-radius:14px;
    overflow:hidden;
    display:flex;
    flex-direction:column;
    background:transparent;
    transition: transform .9s cubic-bezier(.2,.9,.3,1), opacity .45s ease;
    transform-origin:center right;
    pointer-events:auto;
  }
  .page.hidden{ opacity:0; transform: perspective(900px) rotateY(20deg) translateX(40px) scale(.98); pointer-events:none; }

  /* second page visuals */
  .secondContent{
    padding:44px;
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    gap:18px;
    text-align:center;
    height:100%;
    color:var(--text);
  }
  .stars-back{
    position:absolute;
    inset:0;
    z-index:0;
    pointer-events:none;
  }

  /* message area */
  .message {
    z-index:2;
    max-width:860px;
    backdrop-filter: blur(6px);
    padding:28px 24px;
    border-radius:14px;
    background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    box-shadow: 0 8px 40px rgba(1,1,6,0.6);
    display:flex;
    flex-direction:column;
    gap:8px;
    align-items:center;
  }
  .message p{
    margin:0;
    font-size: clamp(16px,2.2vw,22px);
    line-height:1.45;
    color:var(--text);
    white-space:pre-wrap;
    font-weight:600;
    text-shadow: 0 6px 20px rgba(0,0,0,0.6);
  }

  /* animated effect for lines */
  .message .line{
    display:inline-block;
    opacity:0;
    transform:translateY(10px) scale(.995);
    animation:appear .9s forwards cubic-bezier(.2,.9,.3,1);
  }
  .message .line:nth-child(1){ animation-delay:.35s; }
  .message .line:nth-child(2){ animation-delay:.9s; transform-origin:center; }
  .message .line:nth-child(3){ animation-delay:1.4s; }
  .message .line:nth-child(4){ animation-delay:1.9s; }
  .message .line:nth-child(5){ animation-delay:2.45s; }
  @keyframes appear{
    from{ opacity:0; transform:translateY(14px) scale(.99) rotateX(6deg); filter:blur(6px); }
    to{ opacity:1; transform:translateY(0) scale(1) rotateX(0); filter:blur(0); }
  }

  /* pulsing heart */
  .big-heart{
    width:120px;height:120px;
    display:inline-block;
    transform-origin:center;
    animation:pulse 2.6s infinite cubic-bezier(.25,.9,.3,1);
    filter: drop-shadow(0 12px 35px rgba(255,77,184,0.12));
  }
  @keyframes pulse{
    0%{ transform:scale(.96) rotate(-6deg); }
    50%{ transform:scale(1.02) rotate(6deg); }
    100%{ transform:scale(.96) rotate(-6deg); }
  }

  /* small helpers */
  .controls{ display:flex; gap:12px; align-items:center; justify-content:center; margin-top:8px; z-index:3; }
  .ghost {
    font-size:13px;
    color:var(--muted);
  }

  /* responsive */
  @media (max-width:720px){
    .card{ padding:20px; min-height:640px; border-radius:14px; }
    .message p{ font-size:16px; }
    .big-heart{ width:92px;height:92px; }
  }
</style>
</head>
<body>
  <div class="stage" id="stage">
    <div class="card" role="main" aria-label="Birthday greeting card">
      <!-- Layer canvases -->
      <canvas id="heartsCanvas"></canvas>
      <canvas id="particlesCanvas"></canvas>

      <!-- FRONT PAGE (page1) -->
      <section class="page" id="page1" aria-hidden="false" style="position:relative; z-index:2;">
        <div class="title" style="margin-top:10px;">
          <h1>JAPPY BIRTHDAY MY LOVE</h1>
          <div class="name-badge" aria-hidden="false">
            <div class="name" title="IMPU">
              <span style="color:var(--accent); font-size:20px;">IMPU</span>
              <!-- Pink sparkle heart -->
              <svg class="heart" viewBox="0 0 24 24" aria-hidden="true">
                <defs>
                  <linearGradient id="g1" x1="0" y1="0" x2="1" y2="1">
                    <stop offset="0%" stop-color="#ff4db8"/>
                    <stop offset="100%" stop-color="#ff83cf"/>
                  </linearGradient>
                </defs>
                <path d="M12 21s-7-4.6-9.2-7.4C-1.6 8.7 4.2 3 8.4 5.2 10 6.2 12 8 12 8s2-.8 3.6-2.8C19.8 3 25.6 8.7 21.2 13.6 19 16.4 12 21 12 21z" fill="url(#g1)"/>
              </svg>
              <span class="star" aria-hidden="true">★</span>
            </div>
          </div>
          <div class="subtitle">You are my light — every little thing reminds me of you ✨</div>
        </div>

        <div style="text-align:center;margin-top:18px;">
          <svg class="big-heart" viewBox="0 0 24 24" aria-hidden="true">
            <defs>
              <linearGradient id="g2" x1="0" y1="0" x2="1" y2="1">
                <stop offset="0%" stop-color="#ff8ac9"/>
                <stop offset="100%" stop-color="#ff3fa0"/>
              </linearGradient>
            </defs>
            <path d="M12 21s-7-4.8-9-7.8C1 9.4 6.5 4.6 9.1 6.4 10.6 7.6 12 9.2 12 9.2s1.4-1.6 2.9-2.8C17.5 4.6 23 9.4 21 13.2 19 16.2 12 21 12 21z" fill="url(#g2)"/>
          </svg>
        </div>

        <p class="hint" style="margin-top:8px;">(Welcome — watch the little 3D hearts fall. When you're ready, click to continue.)</p>

        <div class="footer">
          <button class="btn" id="nextBtn" aria-label="Click to go to next page">Click to go to the next page — Make a wish ✨</button>
        </div>
      </section>

      <!-- SECOND PAGE (page2) -->
      <section class="page hidden" id="page2" aria-hidden="true" style="z-index:3;">
        <div class="stars-back" id="starsBack"></div>

        <div class="secondContent" role="article">
          <div class="message" id="messageBox" aria-live="polite">
            <!-- Animated message lines (we will fill using JS for exact formatting & timing) -->
            <p class="line" id="l1"></p>
            <p class="line" id="l2"></p>
            <p class="line" id="l3"></p>
            <p class="line" id="l4"></p>
            <p class="line" id="l5"></p>
          </div>

          <div class="controls">
            <button class="btn" id="replayBtn" aria-label="Replay animation">Replay</button>
            <div class="ghost">Tap the hearts or press space to replay the blast ✨</div>
          </div>
        </div>
      </section>

    </div>
  </div>

<script>
/* ===============================================================
   Friendly, self-contained interactive birthday greeting
   - Canvas hearts falling (3D-ish)
   - Click to produce blast particle effect and transition page
   - Second page: stars background and animated message
   - All in a single HTML file, no external libraries
   =============================================================== */

(() => {
  /* Utility */
  const $ = sel => document.querySelector(sel);

  /* Canvas setup: heartsCanvas (background falling hearts) and particlesCanvas (blast) */
  const heartsCanvas = $('#heartsCanvas');
  const particlesCanvas = $('#particlesCanvas');
  const stage = $('#stage');
  const card = document.querySelector('.card');

  function fitCanvas(canvas){
    const rect = card.getBoundingClientRect();
    const dpr = Math.max(1, window.devicePixelRatio || 1);
    canvas.width = Math.round(rect.width * dpr);
    canvas.height = Math.round(rect.height * dpr);
    canvas.style.width = rect.width + 'px';
    canvas.style.height = rect.height + 'px';
    canvas.getContext('2d').scale(dpr, dpr);
  }

  function resizeAll(){
    fitCanvas(heartsCanvas);
    fitCanvas(particlesCanvas);
    starField && starField.reset();
  }
  window.addEventListener('resize', resizeAll);

  /* Hearts falling */
  const H = heartsCanvas.getContext('2d');
  let hearts = [];
  const maxHearts = 20;

  function rand(min,max){ return Math.random()*(max-min)+min; }

  function makeHeartShape(ctx,x,y,s,angle,fillStyle,shadowColor){
    ctx.save();
    ctx.translate(x,y);
    ctx.rotate(angle);
    ctx.scale(s,s);
    // draw heart path (centered)
    ctx.beginPath();
    ctx.moveTo(0,-6);
    ctx.bezierCurveTo(0,-9,6,-12,8,-6);
    ctx.bezierCurveTo(10,-1,6,4,0,10);
    ctx.bezierCurveTo(-6,4,-10,-1,-8,-6);
    ctx.bezierCurveTo(-6,-12,0,-9,0,-6);
    ctx.closePath();
    // shading gradient
    const g = ctx.createLinearGradient(-12,-12,12,16);
    g.addColorStop(0, fillStyle);
    g.addColorStop(1, 'rgba(255,255,255,0.06)');
    ctx.fillStyle = g;
    ctx.shadowColor = shadowColor || 'rgba(0,0,0,0.35)';
    ctx.shadowBlur = 8;
    ctx.fill();
    // glossy highlight
    ctx.beginPath();
    ctx.ellipse(2,-3,3,5, -0.5, 0, Math.PI*2);
    ctx.fillStyle = 'rgba(255,255,255,0.18)';
    ctx.globalCompositeOperation = 'lighter';
    ctx.fill();
    ctx.globalCompositeOperation = 'source-over';
    ctx.restore();
  }

  class Heart {
    constructor(w,h){
      this.reset(w,h,true);
    }
    reset(w,h,fromTop=false){
      this.x = rand(36, w-36);
      this.y = fromTop ? rand(-80, -20) : rand(-120, h+60);
      this.s = rand(.9,1.6);
      this.vy = rand(30, 90) * (0.6 + Math.random()*0.8);
      this.vx = rand(-20,20);
      this.spin = rand(-1.2,1.2);
      this.alpha = rand(.85,1);
      this.color = Math.random()<0.5 ? 'rgba(255,77,184,0.95)' : 'rgba(255,131,207,0.95)';
      this.shadow = 'rgba(200,20,90,0.12)';
      this.angle = rand(-0.5,0.5);
    }
    step(dt, w, h){
      this.y += this.vy * dt;
      this.x += this.vx * dt;
      this.angle += this.spin * 0.01;
      // remove if beyond bottom
      if(this.y - 40 > h) {
        this.reset(w,h,true);
      }
    }
    draw(ctx){
      ctx.save();
      ctx.globalAlpha = this.alpha;
      makeHeartShape(ctx, this.x, this.y, this.s, this.angle, this.color, this.shadow);
      ctx.restore();
    }
  }

  function initHearts(){
    hearts = [];
    const rect = card.getBoundingClientRect();
    for(let i=0;i<maxHearts;i++){
      hearts.push(new Heart(rect.width, rect.height));
    }
  }

  /* Particles for blast effect */
  const P = particlesCanvas.getContext('2d');
  let particles = [];

  class Particle {
    constructor(x,y,dx,dy,life,scale,color){
      this.x = x; this.y = y; this.vx = dx; this.vy = dy;
      this.life = life; this.age = 0; this.scale = scale; this.color = color;
      this.spin = rand(-3,3);
      this.angle = rand(0,Math.PI*2);
    }
    step(dt){
      this.age += dt;
      this.x += this.vx * dt;
      this.y += this.vy * dt;
      // gravity-ish
      this.vy += 30 * dt;
      this.angle += this.spin * 0.04;
    }
    draw(ctx){
      const t = Math.max(0, 1 - this.age/this.life);
      ctx.save();
      ctx.globalAlpha = t * 0.98;
      ctx.translate(this.x, this.y);
      ctx.rotate(this.angle);
      ctx.scale(this.scale * t, this.scale * t);
      // draw small heart-ish particle
      ctx.beginPath();
      ctx.moveTo(0,-4);
      ctx.bezierCurveTo(0,-6,3,-7,4,-4);
      ctx.bezierCurveTo(5,-1,3,2,0,4);
      ctx.bezierCurveTo(-3,2,-5,-1,-4,-4);
      ctx.bezierCurveTo(-3,-7,0,-6,0,-4);
      ctx.closePath();
      const g = ctx.createLinearGradient(-6,-6,6,8);
      g.addColorStop(0,this.color);
      g.addColorStop(1,'rgba(255,255,255,0.05)');
      ctx.fillStyle = g;
      ctx.fill();
      ctx.restore();
    }
    get done(){ return this.age >= this.life; }
  }

  function blast(x,y,strength=1){
    const rect = card.getBoundingClientRect();
    const count = Math.round(28 * strength + Math.random()*18);
    for(let i=0;i<count;i++){
      const ang = Math.random()*Math.PI*2;
      const speed = rand(80,420) * (0.6 + Math.random()*0.8) * strength;
      const dx = Math.cos(ang)*speed;
      const dy = Math.sin(ang)*speed - Math.random()*120;
      const life = rand(.9,1.8);
      const s = rand(.6,1.4);
      const col = Math.random()<0.5 ? 'rgba(255,77,184,0.95)' : 'rgba(255,131,207,0.95)';
      particles.push(new Particle(x, y, dx, dy, life, s, col));
    }
  }

  /* Star field for second page */
  const starsBackEl = $('#starsBack');
  let starCanvas, starCtx, starField;

  function ensureStarCanvas(){
    if(!starCanvas){
      starCanvas = document.createElement('canvas');
      starCanvas.style.position = 'absolute';
      starCanvas.style.inset = '0';
      starCanvas.style.width = '100%';
      starCanvas.style.height = '100%';
      starCanvas.style.zIndex = '0';
      starCanvas.id = 'starCanvas';
      starsBackEl.appendChild(starCanvas);
      starCtx = starCanvas.getContext('2d');
    }
    fitCanvas(starCanvas);
  }

  class StarField {
    constructor(){
      this.stars = [];
      this.t = 0;
      this.init();
    }
    init(){
      ensureStarCanvas();
      const rect = card.getBoundingClientRect();
      const w = rect.width;
      const h = rect.height;
      const count = Math.round((w*h)/4000);
      this.stars = [];
      for(let i=0;i<count;i++){
        this.stars.push({
          x: Math.random()*w,
          y: Math.random()*h,
          r: Math.random()*1.8 + 0.3,
          flick: Math.random()*1,
          phase: Math.random()*Math.PI*2,
          hue: 220 + Math.random()*40,
          speed: Math.random()*0.04 + 0.01
        });
      }
      this.reset = () => this.init();
    }
    step(dt){
      this.t += dt;
      const rect = card.getBoundingClientRect();
      starCtx.clearRect(0,0,rect.width,rect.height);
      for(const s of this.stars){
        s.phase += s.speed * dt * 50;
        const alpha = 0.4 + Math.abs(Math.sin(s.phase))*0.6;
        starCtx.beginPath();
        starCtx.fillStyle = `rgba(255,255,255,${alpha*0.85})`;
        starCtx.arc(s.x, s.y, s.r, 0, Math.PI*2);
        starCtx.fill();
      }
    }
  }

  /* Animation loop */
  let last = performance.now()/1000;
  let raf;
  function loop(now){
    const t = now/1000;
    const dt = Math.min(0.05, t - last);
    last = t;
    // hearts
    const rect = card.getBoundingClientRect();
    H.clearRect(0,0,rect.width,rect.height);
    for(const h of hearts){
      h.step(dt, rect.width, rect.height);
      h.draw(H);
    }
    // particles
    P.clearRect(0,0,rect.width,rect.height);
    for(let i=particles.length-1;i>=0;i--){
      const p = particles[i];
      p.step(dt);
      p.draw(P);
      if(p.done) particles.splice(i,1);
    }

    // stars
    if(starField) starField.step(dt);

    raf = requestAnimationFrame(loop);
  }

  /* Page transition and UI behavior */
  const page1 = $('#page1'), page2 = $('#page2');
  const nextBtn = $('#nextBtn');
  const replayBtn = $('#replayBtn');

  function transitionToPage2(){
    // make blast at center
    const rect = card.getBoundingClientRect();
    const cx = rect.width/2;
    const cy = rect.height/2;
    blast(cx, cy, 1.1);
    // subtle short delay then flip
    setTimeout(()=>{
      page1.classList.add('hidden');
      page1.setAttribute('aria-hidden','true');
      page2.classList.remove('hidden');
      page2.setAttribute('aria-hidden','false');
      // ensure star field active
      if(!starField) starField = new StarField();
      // start animated lines
      playMessageLines();
    }, 420);
  }

  nextBtn.addEventListener('click', (e)=>{
    // produce a more dramatic blast near the button's location
    const btnRect = nextBtn.getBoundingClientRect();
    const cardRect = card.getBoundingClientRect();
    const x = btnRect.left - cardRect.left + btnRect.width/2;
    const y = btnRect.top - cardRect.top + btnRect.height/2;
    blast(x,y,1.5);
    // small camera-like shake
    card.animate([
      { transform: 'translateY(0px)'},
      { transform: 'translateY(-6px)'},
      { transform: 'translateY(0px)'}
    ], { duration:380, easing: 'cubic-bezier(.2,.9,.3,1)' });
    setTimeout(transitionToPage2, 260);
  });

  // allow whole card click to produce a small blast on second page
  card.addEventListener('click', (e)=>{
    // only on second page produce small heart burst
    if(!page2.classList.contains('hidden')){
      const rect = card.getBoundingClientRect();
      const x = (e.clientX - rect.left);
      const y = (e.clientY - rect.top);
      blast(x,y,0.9);
    }
  });

  // keyboard control
  window.addEventListener('keydown',(e)=>{
    if(e.code === 'Space'){
      e.preventDefault();
      if(page2.classList.contains('hidden')){
        nextBtn.click();
      } else {
        // replay small burst center
        const rect = card.getBoundingClientRect();
        blast(rect.width/2, rect.height/2, 0.9);
        playMessageLines(true);
      }
    }
  });

  replayBtn.addEventListener('click', ()=>{
    // big blast
    const rect = card.getBoundingClientRect();
    blast(rect.width/2, rect.height/2, 1.0);
    playMessageLines(true);
  });

  /* MESSAGE LINES: exact content as requested, with animated effect */
  const lines = [
    "I MISS YOU MY LOVE.",
    "THERE WAS NOTHING BEFORE YOU, AND THERE IS NOTHING AFTER YOU.",
    "I'M WAITING TO HUG YOU",
    "I LOVE YOU",
    "My story begins with your smile, and it ends in your eyes"
  ];
  const lEls = [$('#l1'), $('#l2'), $('#l3'), $('#l4'), $('#l5')];

  let typingControllers = [];

  function clearTyping(){
    // remove any scheduled timeouts
    typingControllers.forEach(id=>clearTimeout(id));
    typingControllers = [];
  }

  function playMessageLines(restart=false){
    clearTyping();
    // reset content & styles
    lEls.forEach((el,i)=>{
      el.textContent = '';
      el.style.opacity = 0;
      el.style.transform = 'translateY(12px) scale(.995)';
    });

    // sequential typewriter-ish reveal (but keep the lines heavy and present as requested)
    let baseDelay = 250;
    lines.forEach((txt,i) => {
      const start = baseDelay + i*650;
      const el = lEls[i];
      // delay then animate fade/slide + do a fast typewriter for effect
      const fadeId = setTimeout(()=>{
        // fade in container
        el.style.transition = 'opacity .65s cubic-bezier(.2,.9,.3,1), transform .65s';
        el.style.opacity = 1;
        el.style.transform = 'translateY(0) scale(1)';
        // now type text char by char:
        let idx = 0;
        const speed = Math.max(12, 28 - i*2); // slightly faster for later lines
        const typeInterval = setInterval(()=>{
          el.textContent = txt.slice(0, idx+1);
          idx++;
          if(idx >= txt.length){
            clearInterval(typeInterval);
          }
        }, speed);
        typingControllers.push(typeInterval);
      }, start);
      typingControllers.push(fadeId);
    });

    // small heart pulse effect each time
    const bigHeart = document.querySelector('.big-heart');
    if(bigHeart){
      bigHeart.animate([
        { transform: 'scale(1) rotate(-6deg)' },
        { transform: 'scale(1.06) rotate(6deg)' },
        { transform: 'scale(1) rotate(-6deg)' }
      ], { duration: 1100, easing:'cubic-bezier(.2,.9,.3,1)' })
    }
  }

  /* Initialize */
  function start(){
    resizeAll();
    initHearts();
    // populate first page - small welcome burst on load
    setTimeout(()=>{
      const rect = card.getBoundingClientRect();
      const cx = rect.width * 0.5;
      const cy = rect.height * 0.25;
      blast(cx, cy, 0.9);
    }, 350);
    // initial loop
    last = performance.now()/1000;
    cancelAnimationFrame(raf);
    raf = requestAnimationFrame(loop);
    // show a few drifting hearts already
  }

  // star field must be created only when transitioning to page2; but ensure canvas fits.
  ensureStarCanvas();
  starField = null;

  start();

  // Accessibility: focus management
  nextBtn.focus();

  // Small decorative: gentle parallax for card based on mouse
  let mouseX = 0, mouseY = 0;
  card.addEventListener('mousemove', (e)=>{
    const rect = card.getBoundingClientRect();
    const cx = rect.left + rect.width/2;
    const cy = rect.top + rect.height/2;
    const dx = (e.clientX - cx)/rect.width;
    const dy = (e.clientY - cy)/rect.height;
    card.style.transform = `translate3d(${dx*6}px, ${dy*6}px, 0)`;
  });
  card.addEventListener('mouseleave', ()=>{
    card.style.transform = '';
  });

  // Done.
})();
</script>
</body>
</html>

