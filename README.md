<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Happy Birthday — A Story for You</title>
<meta name="description" content="An immersive, interactive birthday greeting — dark, modern, animated. Single-file HTML." />
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;500;700;900&family=Great+Vibes&display=swap" rel="stylesheet">
<style>
:root{
  --bg-1:#0b0f17; --bg-2:#0f1724; --accent:#ff6b9a; --accent-2:#7ee7c4; --glass:rgba(255,255,255,0.04);
  --card-w:820px; --transition:550ms cubic-bezier(.2,.9,.25,1);
}
*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0; font-family:Montserrat,system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial; color:#e6eef8; background:linear-gradient(180deg,var(--bg-1),var(--bg-2));
  -webkit-font-smoothing:antialiased;text-rendering:optimizeLegibility; overflow:hidden;
}
.scene{
  position:fixed; inset:0; display:grid; place-items:center; padding:40px; gap:24px;
}
.container{
  width:min(100%,1160px); max-width:1200px; display:grid; grid-template-columns:1fr 420px; gap:32px; align-items:center;
}
@media (max-width:980px){.container{grid-template-columns:1fr; padding:0 20px}}
.card{
  width:100%; background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border-radius:20px; padding:34px; position:relative; overflow:visible; box-shadow:0 10px 30px rgba(2,6,23,0.6); border:1px solid rgba(255,255,255,0.03);
}
.header{display:flex; align-items:center; gap:18px}
.logo{
  width:72px;height:72px;border-radius:14px; display:grid; place-items:center; background:linear-gradient(135deg,var(--accent),var(--accent-2)); box-shadow:0 6px 30px rgba(126,231,196,0.08); font-weight:900; font-size:22px; color:#061018; transform:rotate(-8deg);
}
.title h1{margin:0;font-size:26px;letter-spacing:-0.6px}
.title p{margin:4px 0 0 0; opacity:0.8; font-size:13px}
.stage{margin-top:22px; display:grid; gap:18px}
.story{
  min-height:340px; display:grid; align-content:center; justify-items:center; text-align:center; padding:28px; border-radius:14px; background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00)); border:1px solid rgba(255,255,255,0.02);
}
.story h2{font-family:'Great Vibes', cursive; font-size:48px; margin:6px 0 12px 0; letter-spacing:0.6px}
.story p{max-width:780px;margin:0 auto;font-size:18px;line-height:1.5;color:rgba(230,238,248,0.95)}
.controls{display:flex; gap:12px; justify-content:center; margin-top:18px}
.button{background:linear-gradient(90deg,var(--accent),var(--accent-2)); padding:12px 18px; border-radius:12px; cursor:pointer; border:none; color:#041018; font-weight:700; transition:transform 220ms ease, box-shadow 220ms ease}
.button:active{transform:translateY(2px)}
.secondary{background:transparent; border:1px solid rgba(255,255,255,0.06); color:rgba(230,238,248,0.9); padding:10px 14px}
.side{
  position:relative; height:100%; display:flex; flex-direction:column; gap:18px; align-items:stretch; justify-content:flex-start;
}
.panel{
  padding:18px; border-radius:14px; background:linear-gradient(180deg, rgba(255,255,255,0.015), rgba(255,255,255,0.01)); border:1px solid rgba(255,255,255,0.03);
}
.panel h3{margin:0 0 6px 0}
.preview{display:grid; gap:10px}
.revealCard{
  position:relative; height:220px; border-radius:12px; overflow:hidden; transform-style:preserve-3d; perspective:1400px; display:flex; align-items:center; justify-content:center;
  background:linear-gradient(120deg, rgba(14,20,30,0.6), rgba(2,6,23,0.5)); border:1px solid rgba(255,255,255,0.02);
}
.revealInner{padding:26px; text-align:center; transform:translateZ(40px);}
.revealInner h4{margin:0;font-size:20px}
.revealInner p{opacity:0.95;margin-top:10px}
.layers{display:flex; gap:10px; margin-top:10px; flex-wrap:wrap}
.layer{padding:8px 10px; border-radius:10px; background:rgba(255,255,255,0.02); font-size:13px; cursor:pointer; border:1px solid rgba(255,255,255,0.02)}
.layer.active{background:linear-gradient(90deg,var(--accent),var(--accent-2)); color:#041018; border-color:rgba(255,255,255,0.04);}
.footerNote{opacity:0.7;font-size:12px;margin-top:8px}
/* hearts */
.hearts{position:absolute; inset:0; pointer-events:none;}
.heart{position:absolute; width:14px;height:14px; transform:translate(-50%,-50%); opacity:0.9}
/* typewriter */
.typewriter{display:inline-block; border-right:2px solid rgba(255,255,255,0.12); padding-right:6px; white-space:nowrap; overflow:hidden}
/* guided steps */
.step{opacity:0; transform:translateY(18px) scale(.99); transition:var(--transition)}
.step.active{opacity:1; transform:none}
/* confetti canvas on top */
#effects{position:fixed; inset:0; pointer-events:none; z-index:40}
/* small details */
.small{font-size:13px; opacity:0.85}
.credit{position:fixed; left:18px; bottom:18px; font-size:12px; opacity:0.6}

/* tasteful animations */
@keyframes floaty{0%{transform:translateY(0)}50%{transform:translateY(-10px)}100%{transform:translateY(0)}}
.decor-dot{width:8px;height:8px;border-radius:50%;background:linear-gradient(180deg,var(--accent),var(--accent-2)); box-shadow:0 8px 20px rgba(126,231,196,0.06); animation:floaty 4s ease-in-out infinite}
</style>
</head>
<body>
<div class="scene">
  <canvas id="bgCanvas" style="position:fixed;inset:0;z-index:0"></canvas>
  <div class="container" style="z-index:2">
    <main class="card" role="main" aria-labelledby="main-title">
      <div class="header">
        <div class="logo">❤</div>
        <div class="title">
          <h1 id="main-title">Happy Birthday — A Little Story</h1>
          <p class="small">A guided, intimate journey — click each layer to reveal the next.</p>
        </div>
      </div>

      <section class="stage">
        <div class="story">
          <h2 id="hero-name">For Someone Very Special</h2>
          <p id="hero-sub" class="typewriter">"I Just miss you. TEHERE WAS NOTHING BEFORE YOU,AND THERE IS NOTHING AFTER YOU.My story begins with your smile, and it ends in your eyes."</p>
        </div>

        <div class="controls">
          <button class="button" id="startBtn">Begin the Journey</button>
          <button class="secondary" id="muteBtn">🔊 Mute</button>
        </div>

        <div style="display:flex; justify-content:center; margin-top:6px">
          <div class="footerNote">Pro tip: click the layers on the right — each click reveals an intimate message and visual surprise.</div>
        </div>

      </section>
    </main>

    <aside class="side">
      <div class="panel preview">
        <h3>Layers</h3>
        <div class="revealCard" id="revealCard">
          <div class="revealInner" id="revealInner">
            <h4>Tap to reveal</h4>
            <p class="small">Each layer peels back a memory or feeling — click the chips to the right to explore.</p>
          </div>
        </div>

        <div class="layers" id="layers">
          <div class="layer" data-idx="0">1 — The Beginning</div>
          <div class="layer" data-idx="1">2 — The Smile</div>
          <div class="layer" data-idx="2">3 — First Memory</div>
          <div class="layer" data-idx="3">4 — Little Things</div>
          <div class="layer" data-idx="4">5 — The Promise</div>
        </div>
        <div class="credit">Made with care • Personalize easily</div>
      </div>

      <div class="panel" style="margin-top:12px">
        <h3>Customize</h3>
        <label class="small">Name</label>
        <input id="nameInput" placeholder="Her name" style="width:100%;margin-top:8px;padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.03);background:transparent;color:inherit" />
        <label class="small" style="margin-top:10px">Main message</label>
        <textarea id="msgInput" rows="3" style="width:100%;margin-top:8px;padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.03);background:transparent;color:inherit">I Just miss you. TEHERE WAS NOTHING BEFORE YOU,AND THERE IS NOTHING AFTER YOU.My story begins with your smile, and it ends in your eyes.</textarea>
        <div style="display:flex;gap:8px;margin-top:10px">
          <button class="button" id="applyBtn">Apply</button>
          <button class="secondary" id="resetBtn">Reset</button>
        </div>
      </div>

    </aside>
  </div>

  <div class="hearts" id="hearts"></div>
  <canvas id="effects"></canvas>
  <div class="small credit" style="right:18px; bottom:18px; position:fixed;">Tip: Press ⬇ to download as HTML (Save page as...)</div>
</div>

<script>
// ---------- Config & small helpers ----------
const layersData = [
  {title:'The Beginning', text:'I still remember the first day I noticed you — the world felt brighter.'},
  {title:'The Smile', text:'Your smile rewires my whole day. Everything else fades.'},
  {title:'First Memory', text:'Holding your hand for the first time — warm, a little clumsy, unforgettable.'},
  {title:'Little Things', text:'Your laugh, the way you tuck your hair, the quiet strength you carry.'},
  {title:'The Promise', text:'No matter where life leads, my story begins and ends with you.'}
];

// Elements
const layers = document.getElementById('layers');
const revealInner = document.getElementById('revealInner');
const revealCard = document.getElementById('revealCard');
const startBtn = document.getElementById('startBtn');
const muteBtn = document.getElementById('muteBtn');
const nameInput = document.getElementById('nameInput');
const msgInput = document.getElementById('msgInput');
const applyBtn = document.getElementById('applyBtn');
const resetBtn = document.getElementById('resetBtn');
const heroName = document.getElementById('hero-name');
const heroSub = document.getElementById('hero-sub');

// Insert layers chips
[...layers.children].forEach(chip=>{
  chip.addEventListener('click', ()=>{
    const idx = Number(chip.dataset.idx);
    activateLayer(idx);
    [...layers.children].forEach(c=>c.classList.remove('active'));
    chip.classList.add('active');
  });
});

function activateLayer(i){
  const data = layersData[i] || {title:'',text:''};
  revealInner.innerHTML = `\n    <h4>${data.title}</h4>\n    <p class="small">${data.text}</p>\n    <div style=\"margin-top:12px;display:flex;gap:8px;justify-content:center\">\n      <button class=\"button\" onclick=\"surprise(${i})\">Surprise</button>\n      <button class=\"secondary\" onclick=\"shareIt()\">Share</button>\n    </div>`;
  tiltPulse();
  spawnHearts(6+i*4);
}

function surprise(i){
  // mild confetti + a special modal text
  confettiBurst(80 + i*15);
  showMoment(layersData[i].text);
}

function shareIt(){
  navigator.share?.({title:'A message for you', text:revealInner.innerText})
}

function tiltPulse(){
  revealCard.animate([{transform:'rotateX(6deg) rotateY(-6deg) translateZ(0)'},{transform:'rotateX(0) rotateY(0)'}],{duration:700, easing:'cubic-bezier(.2,.9,.25,1)'});
}

// ---------- Typewriter appearance for the hero line ----------
function typeWrite(el){
  const text = el.getAttribute('data-full') || el.textContent;
  el.textContent = '';
  el.style.borderRight = '2px solid rgba(255,255,255,0.12)';
  let i=0; const speed=28;
  function step(){
    if(i<=text.length){ el.textContent = text.slice(0,i); i++; setTimeout(step, speed); }
    else el.style.borderRight='none';
  }
  step();
}

heroSub.setAttribute('data-full', heroSub.textContent.trim());

// ---------- Background particle painter (subtle) ----------
const bg = document.getElementById('bgCanvas');
const ctx = bg.getContext('2d');
function resizeBg(){ bg.width = innerWidth; bg.height = innerHeight; }
resizeBg(); window.addEventListener('resize', resizeBg);
const particles = [];
for(let i=0;i<80;i++) particles.push({x:Math.random()*innerWidth, y:Math.random()*innerHeight, r:Math.random()*1.6+0.6, vx:(Math.random()-0.5)*0.2, vy:(Math.random()-0.5)*0.4, hue:200+Math.random()*60});
function drawBg(){ ctx.clearRect(0,0,bg.width,bg.height);
  const g = ctx.createLinearGradient(0,0,bg.width,bg.height);
  g.addColorStop(0,'rgba(7,10,16,0.6)'); g.addColorStop(1,'rgba(6,14,25,0.45)');
  ctx.fillStyle=g; ctx.fillRect(0,0,bg.width,bg.height);
  particles.forEach(p=>{ p.x+=p.vx; p.y+=p.vy; if(p.x<0)p.x=bg.width; if(p.x>bg.width)p.x=0; if(p.y<0)p.y=bg.height; if(p.y>bg.height)p.y=0; ctx.beginPath(); ctx.globalAlpha=0.28; ctx.fillStyle='hsl('+p.hue+',80%,'+(30+Math.random()*10)+'%)'; ctx.arc(p.x,p.y,p.r,0,Math.PI*2); ctx.fill(); });
  requestAnimationFrame(drawBg);
}
requestAnimationFrame(drawBg);

// ---------- Hearts spawner (floating hearts) ----------
const heartsLayer = document.getElementById('hearts');
function spawnHearts(num=8){
  for(let i=0;i<num;i++){
    const h = document.createElement('div'); h.className='heart';
    const size = Math.random()*24+8; h.style.width = size+'px'; h.style.height = size+'px';
    const left = Math.random()*100; h.style.left = left+'%'; h.style.top = (80 + Math.random()*20) + '%';
    h.innerHTML = `<svg viewBox="0 0 24 24" width="${size}" height="${size}" aria-hidden="true"><path fill="url(#g)" d="M12 21s-7.5-4.35-10-7.05C-1 10.5 2.2 6 6 6c2.3 0 3.6 1.4 4 2.2.4-.8 1.7-2.2 4-2.2 3.8 0 7 4.5 4 7.95C19.5 16.65 12 21 12 21z"/></svg>`;
    heartsLayer.appendChild(h);
    const rise = 3000 + Math.random()*4000;
    h.animate([{transform:'translateY(0) scale(0.8)', opacity:1},{transform:'translateY(-220px) scale(1.05)', opacity:0}],{duration:rise, easing:'cubic-bezier(.2,.8,.2,1)'}).onfinish=()=>h.remove();
  }
}

// ---------- Confetti (canvas) ----------
const ef = document.getElementById('effects'); const efCtx = ef.getContext('2d');
function fitEffects(){ ef.width = innerWidth; ef.height = innerHeight; }
fitEffects(); window.addEventListener('resize', fitEffects);
let confettiPieces = [];
function confettiBurst(count=80){
  for(let i=0;i<count;i++){ confettiPieces.push({x:innerWidth/2 + (Math.random()-0.5)*300, y:innerHeight/2 + (Math.random()-0.5)*200, vx:(Math.random()-0.5)*8, vy:(Math.random()*-7)-2, r:Math.random()*6+4, c: ['#ff6b9a','#7ee7c4','#ffd166','#6ec9ff'][Math.floor(Math.random()*4)], rot:Math.random()*360, vr:(Math.random()-0.5)*12}); }
}
function drawConfetti(){ efCtx.clearRect(0,0,ef.width,ef.height); confettiPieces.forEach((p,i)=>{ p.vy += 0.2; p.x += p.vx; p.y += p.vy; p.rot += p.vr; efCtx.save(); efCtx.translate(p.x,p.y); efCtx.rotate(p.rot*Math.PI/180); efCtx.fillStyle=p.c; efCtx.fillRect(-p.r/2,-p.r/2,p.r,p.r*1.8); efCtx.restore(); if(p.y>ef.height+40){ confettiPieces.splice(i,1); } }); requestAnimationFrame(drawConfetti); }
requestAnimationFrame(drawConfetti);

// Modal-like moment text
function showMoment(text){
  const el = document.createElement('div'); el.style.position='fixed'; el.style.left='50%'; el.style.top='50%'; el.style.transform='translate(-50%,-50%) scale(0.96)'; el.style.zIndex=80; el.style.padding='26px 28px'; el.style.borderRadius='16px'; el.style.background='linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01))'; el.style.border='1px solid rgba(255,255,255,0.04)'; el.style.boxShadow='0 12px 40px rgba(2,6,23,0.7)'; el.innerHTML = `<div style="font-size:18px;font-weight:700;margin-bottom:8px">A Moment</div><div style="font-size:15px;opacity:0.95">${text}</div><div style="display:flex;gap:8px;justify-content:flex-end;margin-top:12px"><button class="secondary" onclick="this.parentElement.parentElement.remove()">Close</button></div>`;
  document.body.appendChild(el);
  el.animate([{opacity:0, transform:'translate(-50%,-50%) scale(0.96)'},{opacity:1, transform:'translate(-50%,-50%) scale(1)'}],{duration:420,easing:'cubic-bezier(.2,.9,.25,1)'});
}

// ---------- Quick interactions ----------
startBtn.addEventListener('click', ()=>{
  startBtn.textContent='Continue'; startBtn.classList.add('active');
  document.querySelectorAll('.step').forEach(s=>s.classList.remove('active'));
  typeWrite(heroSub);
  spawnHearts(12);
  confettiBurst(40);
});

applyBtn.addEventListener('click', ()=>{
  const name = nameInput.value.trim(); const msg = msgInput.value.trim(); if(name) heroName.textContent = name; heroSub.setAttribute('data-full', msg || heroSub.getAttribute('data-full'));
  typeWrite(heroSub);
});
resetBtn.addEventListener('click', ()=>{ nameInput.value=''; msgInput.value='I Just miss you. TEHERE WAS NOTHING BEFORE YOU,AND THERE IS NOTHING AFTER YOU.My story begins with your smile, and it ends in your eyes.'; heroName.textContent='For Someone Very Special'; heroSub.setAttribute('data-full', msgInput.value); typeWrite(heroSub); });

muteBtn.addEventListener('click', ()=>{ if(muteBtn.textContent.includes('Mute')) muteBtn.textContent='🔇 Muted'; else muteBtn.textContent='🔊 Mute'; });

// initial typewriter after small delay
setTimeout(()=>typeWrite(heroSub),700);

// keyboard confetti shortcut
window.addEventListener('keydown', e=>{ if(e.key === 'c' || e.key === 'C'){ confettiBurst(120); spawnHearts(20); } });

// tiny tilt effect on mousemove for revealCard
revealCard.addEventListener('mousemove',(ev)=>{
  const r = revealCard.getBoundingClientRect(); const dx = (ev.clientX - (r.left + r.width/2))/r.width; const dy = (ev.clientY - (r.top + r.height/2))/r.height;
  revealCard.style.transform = `perspective(900px) rotateY(${dx*8}deg) rotateX(${ -dy*6 }deg)`;
});
revealCard.addEventListener('mouseleave', ()=>{ revealCard.style.transform='none'; });

// simple auto-demo: cycle layers slowly (stops after interactions)
let demoIndex=0; let demoRunning=true;
const demoInterval = setInterval(()=>{ if(!demoRunning) return; activateLayer(demoIndex%layersData.length); [...layers.children].forEach(c=>c.classList.remove('active')); layers.children[demoIndex%layersData.length].classList.add('active'); demoIndex++; if(demoIndex>6){ demoRunning=false; clearInterval(demoInterval); } },2200);

// when user clicks anywhere in layers, stop demo
layers.addEventListener('click', ()=> demoRunning=false);

// ---------- tiny accessibility: focus states ----------
[...document.querySelectorAll('button,input,textarea')].forEach(el=>el.addEventListener('focus', ()=>el.style.outline='2px solid rgba(126,231,196,0.12)'));

</script>
</body>
</html>
