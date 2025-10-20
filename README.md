<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>JAPPY BIRTHDAY MY LOVE — IMPU</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;900&family=Great+Vibes&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#070417;
    --glass: rgba(255,255,255,0.04);
    --accent:#ff69b4;
    --accent-2:#ffb3d9;
    --muted: rgba(255,255,255,0.15);
    --glass-2: rgba(255,255,255,0.03);
  }
  html,body{height:100%;margin:0;background:radial-gradient(1200px 600px at 10% 10%, rgba(255,0,150,0.04), transparent), radial-gradient(900px 400px at 90% 90%, rgba(0,150,255,0.02), transparent), var(--bg); color:#fff; font-family:'Plus Jakarta Sans',system-ui,Segoe UI,Roboto,Helvetica,Arial,sans-serif; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;}
  .app{
    height:100vh; width:100vw; display:grid; place-items:center; position:relative; overflow:hidden;
  }

  /* GLOBAL GLASS CARD */
  .card{
    width:min(980px,94vw); max-height:92vh; border-radius:20px; padding:28px; box-sizing:border-box;
    background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    border: 1px solid rgba(255,255,255,0.04); box-shadow: 0 12px 40px rgba(0,0,0,0.6);
    backdrop-filter: blur(8px) saturate(120%); -webkit-backdrop-filter: blur(8px) saturate(120%);
    display:flex; flex-direction:column; gap:16px; align-items:center; justify-content:center;
  }

  /* Hero text */
  .title{
    text-align:center; letter-spacing:1px;
  }
  .title h1{
    margin:0; font-size:clamp(28px,6vw,56px); font-weight:900; line-height:0.9; font-family:'Great Vibes', cursive;
    color:linear-gradient(#fff,#fff); transform:translateZ(0);
    text-shadow: 0 6px 24px rgba(255,105,180,0.12), 0 2px 8px rgba(0,0,0,0.6);
  }

  .subtitle{
    font-weight:500; font-size:clamp(13px,2vw,18px); color:var(--muted); margin-top:8px;
  }

  /* IMPU name style with heart & star */
  .name{
    margin-top:12px; display:flex; gap:8px; align-items:center; justify-content:center;
    transform-style:preserve-3d;
  }
  .name .badge{
    font-weight:800; font-size:28px; letter-spacing:2px; padding:10px 18px; border-radius:14px;
    background: linear-gradient(135deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01));
    border:1px solid rgba(255,255,255,0.04);
  }
  .spark-heart{
    display:inline-flex; align-items:center; justify-content:center; width:56px; height:56px;
    border-radius:50%; background: linear-gradient(135deg, rgba(255,105,180,0.18), rgba(255,180,210,0.08));
    box-shadow: 0 8px 30px rgba(255,105,180,0.14), inset 0 1px 0 rgba(255,255,255,0.06);
    position:relative; transform:translateZ(40px) rotate(-8deg);
  }
  .spark-heart::after{
    content:"";
    position:absolute; inset:6px; border-radius:50%;
    background: radial-gradient(circle at 35% 30%, rgba(255,255,255,0.7), rgba(255,255,255,0.05) 20%, transparent 25%);
    mix-blend-mode:screen; filter:blur(2px);
  }
  .spark-heart svg{ width:32px; height:32px; filter:drop-shadow(0 6px 18px rgba(255,105,180,0.18)); }

  /* falling hearts container (behind card) */
  .hearts-layer{ position:absolute; inset:0; pointer-events:none; overflow:hidden; z-index:1; transform-style:preserve-3d; }

  /* bottom prompt */
  .prompt{
    margin-top:18px; display:flex; gap:12px; align-items:center;
  }
  .btn{
    appearance:none; border:0; outline:0; cursor:pointer; padding:12px 18px; border-radius:12px; background:linear-gradient(90deg,var(--accent),var(--accent-2));
    color:#111; font-weight:700; box-shadow: 0 8px 30px rgba(255,105,180,0.15), 0 2px 6px rgba(0,0,0,0.6);
    transform:translateZ(40px); transition:transform .18s ease, box-shadow .18s ease;
  }
  .btn:active{ transform:translateY(2px) scale(.995); }
  .mutebtn{ background:transparent; border:1px solid rgba(255,255,255,0.06); color:var(--muted); padding:8px 12px; border-radius:10px; font-weight:600; }

  /* small sparkle animation near title */
  .sparkles{ display:inline-block; vertical-align:middle; width:26px; height:26px; margin-left:8px; transform:translateY(-4px); }
  .sparkles svg{ filter:drop-shadow(0 8px 18px rgba(255,105,180,0.12)); }

  /* second page (hidden by default) */
  .stage-two{ position:absolute; inset:0; display:flex; align-items:center; justify-content:center; background:linear-gradient(180deg, rgba(0,0,0,0.45), rgba(0,0,0,0.6)); z-index:5; opacity:0; pointer-events:none; transition:opacity .8s cubic-bezier(.2,.9,.24,1); }
  .stage-two.show{ opacity:1; pointer-events:auto; }
  .stars-canvas{ position:absolute; inset:0; z-index:1; }
  .two-content{ z-index:2; color:#fff; max-width:980px; padding:36px; text-align:center; border-radius:18px; background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border:1px solid rgba(255,255,255,0.03); box-shadow: 0 12px 40px rgba(0,0,0,0.6); backdrop-filter: blur(6px); }

  .two-content .message{ font-size:clamp(18px,2.6vw,28px); line-height:1.4; white-space:pre-line; font-weight:600; letter-spacing:0.4px; font-family:'Plus Jakarta Sans'; margin-bottom:18px; opacity:0; transform:translateY(14px) scale(.995); transition:all .9s cubic-bezier(.2,.9,.24,1); }
  .two-content .message.show{ opacity:1; transform:translateY(0) scale(1); }

  .two-content .love-line{ font-family:'Great Vibes',cursive; font-size:44px; margin-top:10px; letter-spacing:0; transform:translateZ(0); text-shadow: 0 10px 40px rgba(255,105,180,0.12); }

  .pulse{
    display:inline-block; padding:10px 18px; border-radius:12px; margin-top:18px; font-weight:800;
    background: linear-gradient(90deg, rgba(255,105,180,0.1), rgba(255,105,180,0.06));
    border: 1px solid rgba(255,105,180,0.06);
    transform-origin:center; animation:beat 1.25s infinite;
  }
  @keyframes beat{
    0%{ transform:scale(1); box-shadow: 0 8px 30px rgba(255,105,180,0.06); }
    50%{ transform:scale(1.05); box-shadow: 0 18px 40px rgba(255,105,180,0.12); }
    100%{ transform:scale(1); }
  }

  /* small footer controls */
  .footer-row{ display:flex; gap:12px; justify-content:center; align-items:center; margin-top:12px; }

  /* Responsive */
  @media (max-width:640px){
    .card{ padding:18px; border-radius:14px; }
    .spark-heart{ width:48px; height:48px; }
  }

  /* decorative star twinkle (for title) */
  .twinkle{
    display:inline-block; margin-left:10px; transform-origin:center; animation:twink 2.2s infinite;
  }
  @keyframes twink {
    0%,100%{ transform:scale(.9) rotate(0); opacity:0.7; }
    50%{ transform:scale(1.15) rotate(12deg); opacity:1; }
  }

  /* animated type effect fallback */
  .typed { display:inline-block; border-right:2px solid rgba(255,255,255,0.15); padding-right:6px; }

  /* particle blast canvas */
  #blastCanvas{ position:absolute; inset:0; z-index:6; pointer-events:none; }

</style>
</head>
<body>
<div class="app" id="app">
  <div class="hearts-layer" id="heartsLayer" aria-hidden="true"></div>

  <div class="card" id="card">
    <div class="title">
      <h1>JAPPY BIRTHDAY MY LOVE</h1>
      <div class="subtitle">pink sparkle heart <span class="sparkles" aria-hidden="true">
        <!-- small sparkle svg -->
        <svg viewBox="0 0 24 24" width="26" height="26" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M12 2l1.8 3.8L18 7l-4.2 2L12 12l-1.8-2L6 7l4.2-1.2L12 2z" fill="#fff" opacity=".95"/>
          <path d="M5 16l.9 1.9L8 18l-1.1 1.1L6 21l-.9-1.9L4 18l1.1-1.1L5 16z" fill="#ff7ab6" opacity=".95"/>
        </svg>
      </span></div>
    </div>

    <div class="name" aria-hidden="false">
      <div class="badge" aria-label="Name badge">IMPU</div>
      <div class="spark-heart" title="heart">
        <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <path d="M12 21s-7-4.35-9.04-7.04C.9 10.87 3 6 7 6c2.2 0 3.2 1.45 5 3.11C14.8 7.45 15.8 6 18 6c4 0 6.1 4.87 4.04 7.96C19 16.65 12 21 12 21z" fill="#ff6aa6"/>
        </svg>
      </div>
      <div style="display:flex;align-items:center; gap:8px; color:var(--muted); font-weight:700;">
        <span class="twinkle" aria-hidden="true">★</span>
      </div>
    </div>

    <div style="margin-top:18px; text-align:center; color:var(--muted); max-width:70ch;">
      <div class="subtitle">Welcome — open your heart and click to continue the surprise</div>
    </div>

    <div class="prompt" role="group" aria-label="Continue">
      <button class="btn" id="nextBtn">Click to next page →</button>
      <button class="mutebtn" id="openSpotify" title="Open track in Spotify">Open track in Spotify</button>
    </div>

    <div style="font-size:12px; color:rgba(255,255,255,0.12); margin-top:8px; text-align:center;">(Tip: clicking "next" will trigger the effect and open Spotify in a new tab — this lets it play.)</div>
  </div>

  <!-- Stage two (hidden initially) -->
  <div class="stage-two" id="stageTwo" role="dialog" aria-modal="true" aria-hidden="true">
    <canvas class="stars-canvas" id="starsCanvas"></canvas>
    <div class="two-content" id="twoContent" role="document" aria-label="Birthday message">
      <div class="message" id="messageText" aria-live="polite">
I MISS YOU MY LOVE.
TEHERE WAS NOTHING BEFORE YOU,AND THERE IS NOTHING AFTER YOU.
 IM WAITING TO HUG YOU 
I LOVE YOU With animated effect
My story begins with your smile, and it ends in your eyes
      </div>

      <div class="love-line">💫 IMPU — my everything</div>

      <div class="footer-row">
        <div class="pulse">HUG ME</div>
      </div>

      <div style="margin-top:16px;">
        <!-- Spotify embed (user-provided track) -->
        <iframe id="spotifyEmbed" src="https://open.spotify.com/embed/track/2xFUCXedvkdCj0AUPN2QvC?utm_source=generator" width="100%" height="80" frameborder="0" allowtransparency="true" allow="encrypted-media; clipboard-write" title="Spotify Embed"></iframe>
      </div>
    </div>
  </div>

  <!-- blast canvas overlay -->
  <canvas id="blastCanvas"></canvas>
</div>

<script>
  /* Utility: random helpers */
  function rand(min, max){ return Math.random()*(max-min)+min; }
  function choice(arr){ return arr[Math.floor(Math.random()*arr.length)]; }

  /* HEARTS: spawn falling 3D hearts */
  const heartsLayer = document.getElementById('heartsLayer');
  const colors = ["#ff6aa6","#ff7ab6","#ff9cc9","#ffb3d9"];
  let heartsRunning = true;

  function createHeart(x, scale, speed, rotate, color){
    const el = document.createElement('div');
    el.className = 'heart';
    el.style.position = 'absolute';
    el.style.left = (x*100) + 'vw';
    el.style.top = '-8vh';
    el.style.width = (48*scale)+'px';
    el.style.height = (48*scale)+'px';
    el.style.pointerEvents = 'none';
    el.style.zIndex = 0;
    el.style.transform = 'translateZ('+ (rand(-200,400)) +'px) rotate('+rotate+'deg)';
    el.innerHTML = `
      <svg viewBox="0 0 24 24" width="${48*scale}" height="${48*scale}" style="display:block;filter:drop-shadow(0 6px 24px rgba(255,105,180,0.12));">
        <path d="M12 21s-7-4.35-9.04-7.04C.9 10.87 3 6 7 6c2.2 0 3.2 1.45 5 3.11C14.8 7.45 15.8 6 18 6c4 0 6.1 4.87 4.04 7.96C19 16.65 12 21 12 21z" fill="${color}"/>
      </svg>
    `;
    heartsLayer.appendChild(el);

    // animate fall
    const duration = rand(5500,9500) / (speed||1);
    el.animate([
      { transform: el.style.transform + ' translateY(0vh)'},
      { transform: el.style.transform + ' translateY(120vh)'}
    ], {duration: duration, easing: 'cubic-bezier(.2,.8,.2,1)'});
    setTimeout(()=> el.remove(), duration+120);
  }

  // initial wave of hearts
  function startHearts(){
    let spawn = setInterval(()=> {
      if(!heartsRunning) { clearInterval(spawn); return; }
      createHeart(Math.random()*0.9 + 0.05, rand(0.75,1.3), rand(0.8,1.2), rand(-45,20), choice(colors));
      // occasionally spawn a big one
      if(Math.random()<0.12) createHeart(Math.random()*0.9 + 0.05, rand(1.6,2.1), rand(0.7,1.0), rand(-20,40), "#ff2d95");
    }, 380);
  }
  startHearts();

  /* BLAST: particle explosion on click - canvas */
  const blastCanvas = document.getElementById('blastCanvas');
  const bc = blastCanvas.getContext('2d');
  function resizeBlast(){ blastCanvas.width = innerWidth; blastCanvas.height = innerHeight; }
  resizeBlast(); window.addEventListener('resize', resizeBlast);

  function blastAt(x,y){
    const particles = [];
    const count = 90;
    for(let i=0;i<count;i++){
      particles.push({
        x, y,
        vx: rand(-8,8),
        vy: rand(-8,8),
        r: rand(2,7),
        life: rand(800,1700),
        t:0,
        fill: choice(colors.concat(["#fff","#ffd6ea","#ffdeef"]))
      });
    }
    const start = performance.now();
    function step(now){
      bc.clearRect(0,0,blastCanvas.width, blastCanvas.height);
      let alive = 0;
      for(const p of particles){
        p.t = now - start;
        if(p.t < p.life){
          p.x += p.vx * (1 + p.t/1200);
          p.y += p.vy * (1 + p.t/1200) + 0.5*(p.t/1200);
          const alpha = 1 - (p.t/p.life);
          bc.beginPath();
          bc.globalAlpha = alpha;
          bc.fillStyle = p.fill;
          bc.arc(p.x, p.y, p.r * (1 + p.t/2000), 0, Math.PI*2);
          bc.fill();
          alive++;
        }
      }
      bc.globalAlpha = 1;
      if(alive>0) requestAnimationFrame(step);
      else bc.clearRect(0,0,blastCanvas.width, blastCanvas.height);
    }
    requestAnimationFrame(step);
  }

  /* Transition to stage two */
  const nextBtn = document.getElementById('nextBtn');
  const stageTwo = document.getElementById('stageTwo');
  const messageText = document.getElementById('messageText');
  const twoContent = document.getElementById('twoContent');
  const spotifyOpenBtn = document.getElementById('openSpotify');

  // open Spotify track in new tab (user provided link)
  spotifyOpenBtn.addEventListener('click', ()=> {
    window.open("https://open.spotify.com/track/2xFUCXedvkdCj0AUPN2QvC?si=DSEgokChT62dbKDBzdRUuA", "_blank");
  });

  nextBtn.addEventListener('click', (e)=>{
    // blast center near button
    const r = nextBtn.getBoundingClientRect();
    const cx = r.left + r.width/2 + rand(-120,120);
    const cy = r.top + r.height/2 + rand(-50,50);
    heartsRunning = false; // stop new hearts
    blastAt(cx, cy);

    // small camera shake and card hide
    document.getElementById('card').animate([
      { transform: 'translateY(0)'},
      { transform: 'translateY(-12px) rotateZ(-1deg)'}
    ], { duration: 280, easing: 'cubic-bezier(.2,.9,.24,1)' });

    setTimeout(()=> {
      // fade in stage two
      stageTwo.classList.add('show');
      stageTwo.setAttribute('aria-hidden','false');
      // spawn a few slow hearts to drift
      for(let i=0;i<18;i++){ setTimeout(()=> createHeart(Math.random()*0.95, rand(.9,1.4), rand(.98,1.2), rand(-30,30), choice(colors)), i*120); }
      // animate message
      setTimeout(()=> messageText.classList.add('show'), 680);
      // attempt to open Spotify in new tab (user gesture continues)
      try{ window.open("https://open.spotify.com/track/2xFUCXedvkdCj0AUPN2QvC?si=DSEgokChT62dbKDBzdRUuA", "_blank"); }catch(err){}
    }, 420);
  });

  /* STARFIELD canvas for stage two */
  const canvas = document.getElementById('starsCanvas');
  const ctx = canvas.getContext('2d');
  function resizeStars(){ canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
  resizeStars(); window.addEventListener('resize', resizeStars);

  const stars = [];
  for(let i=0;i<220;i++){
    stars.push({
      x: Math.random()*window.innerWidth,
      y: Math.random()*window.innerHeight,
      r: Math.random()*1.8 + 0.3,
      alpha: Math.random()*0.9 + 0.1,
      dx: (Math.random()-0.5)*0.02,
      dy: (Math.random()-0.5)*0.02,
    });
  }

  function drawStars(){
    ctx.clearRect(0,0,canvas.width, canvas.height);
    for(const s of stars){
      s.x += s.dx; s.y += s.dy;
      if(s.x < 0) s.x = canvas.width;
      if(s.x > canvas.width) s.x = 0;
      if(s.y < 0) s.y = canvas.height;
      if(s.y > canvas.height) s.y = 0;
      ctx.beginPath();
      const g = ctx.createRadialGradient(s.x, s.y, 0, s.x, s.y, s.r*6);
      g.addColorStop(0, 'rgba(255,255,255,' + (s.alpha) + ')');
      g.addColorStop(0.3, 'rgba(255,255,255,' + (s.alpha*0.4) + ')');
      g.addColorStop(1, 'rgba(255,255,255,0)');
      ctx.fillStyle = g;
      ctx.arc(s.x, s.y, s.r*6, 0, Math.PI*2);
      ctx.fill();
    }
    requestAnimationFrame(drawStars);
  }
  drawStars();

  /* nice gentle glow pulse for the message text after appear */
  setInterval(()=> {
    const el = document.querySelector('.love-line');
    if(el) el.animate([{ transform:'scale(1)'},{ transform:'scale(1.02)'},{ transform:'scale(1)' }], { duration:2600, easing:'ease-in-out' });
  }, 2600);

  /* Accessibility: keyboard allow Enter to go next */
  document.addEventListener('keydown', (e)=>{
    if(e.key === 'Enter' && !stageTwo.classList.contains('show')) nextBtn.click();
  });

  /* small pre-warm: when user first clicks anywhere, spawn a few hearts */
  document.addEventListener('pointerdown', function warm(){
    for(let i=0;i<6;i++) createHeart(Math.random()*0.9 + 0.05, rand(.9,1.6), rand(0.9,1.1), rand(-40,40), choice(colors));
    document.removeEventListener('pointerdown', warm);
  });

  // Ensure canvases match DPR for crispness
  function fixCanvasDPR(){
    [blastCanvas, canvas].forEach(c=>{
      const ratio = window.devicePixelRatio || 1;
      const w = window.innerWidth; const h = window.innerHeight;
      c.width = Math.floor(w*ratio);
      c.height = Math.floor(h*ratio);
      c.style.width = w+'px'; c.style.height = h+'px';
      const ctx = c.getContext('2d');
      if(ctx) ctx.setTransform(ratio,0,0,ratio,0,0);
    });
  }
  fixCanvasDPR(); window.addEventListener('resize', fixCanvasDPR);

  // Small 'falling 3D' extra: add CSS animations for subtle parallax (done via JS spawn)
  // the rest is handled above.

  /* Helpful note for the user who will open the file:
     - Because of browser autoplay policies, audio in the Spotify embed won't start until the user interacts.
     - We open the Spotify track in a new tab on the user's click so playback can begin there.
  */
</script>
</body>
</html>
