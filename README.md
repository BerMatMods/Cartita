
<html lang="es">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>💌 Carta Especial</title>

<!-- Fuentes -->
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&family=Share+Tech+Mono&family=Dancing+Script:wght@700&display=swap" rel="stylesheet">

<style>
  :root{
    --matrix-green: #00ff66;
    --accent-red: #ff3b3b;
    --bg-pink-start: #ffedf2;
    --bg-pink-end: #ffd7e8;
    --glow-pink: #ff7aa8;
  }
  html,body{height:100%;margin:0;background:linear-gradient(180deg,var(--bg-pink-start),var(--bg-pink-end));font-family:Georgia,serif;overflow:hidden; position: relative;}

  /* ---------- Cover mejorado ---------- */
  #cover{
    height:100vh;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:14px;
    animation: fadeIn 1.5s ease-in;
    position: relative;
    z-index: 2;
  }
  @keyframes fadeIn{0%{opacity:0}100%{opacity:1}}

  .coverHeart{
    position: absolute; font-size: 24px; opacity: 0.7; pointer-events: none;
    animation: floatHeart 8s infinite ease-in-out;
  }
  @keyframes floatHeart{
    0%,100%{ transform: translateY(0) rotate(0deg); }
    50%{ transform: translateY(-40px) rotate(20deg); }
  }

  .card{
    width:90%;max-width:760px;background:rgba(255,255,255,0.95);border-radius:18px;padding:30px;box-shadow:0 30px 80px rgba(0,0,0,0.08);text-align:left;
    transform: scale(0.95); animation: popIn 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards, glow 2s infinite alternate;
    position: relative; overflow: hidden;
  }
  @keyframes popIn{0%{transform:scale(0.9)}100%{transform:scale(1)}}
  @keyframes glow{
    0%{ box-shadow: 0 30px 80px rgba(0,0,0,0.08); }
    100%{ box-shadow: 0 30px 80px rgba(255,122,168,0.25); }
  }
  .card::before{
    content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%;
    background: radial-gradient(circle, rgba(255,122,168,0.1) 0%, transparent 70%);
    animation: pulse 3s infinite;
    z-index: -1;
  }
  @keyframes pulse{
    0%{ transform: scale(0.8); opacity: 0.3; }
    50%{ transform: scale(1.2); opacity: 0.6; }
    100%{ transform: scale(0.8); opacity: 0.3; }
  }

  .card h1{font-family:'Georgia',serif;font-size:34px;margin:0;color:#d4377a; text-shadow: 2px 2px 4px rgba(0,0,0,0.1)}
  .card p{color:#6b4a56;font-size:17px;line-height:1.6}
  .openBtn{
    margin-top:18px;padding:12px 22px;border-radius:12px;border:0;background:linear-gradient(90deg,#ff7aa8,#ff4d8a);color:white;font-weight:700;cursor:pointer;font-family: 'Orbitron', sans-serif;
    box-shadow:0 12px 30px rgba(255,77,138,0.14); transition: all 0.3s ease; transform: translateY(0);
    animation: pulseBtn 1.8s infinite;
  }
  @keyframes pulseBtn{
    0%{ box-shadow: 0 12px 30px rgba(255,77,138,0.14); }
    50%{ box-shadow: 0 12px 40px rgba(255,77,138,0.35); }
    100%{ box-shadow: 0 12px 30px rgba(255,77,138,0.14); }
  }
  .openBtn:hover{ transform: translateY(-3px); box-shadow: 0 18px 40px rgba(255,77,138,0.25); background: linear-gradient(90deg, #ff4d8a, #ff7aa8); }

  /* ---------- BerMatMods (HACKEO REAL) ---------- */
  #sim{display:none;position:fixed;inset:0;background:#000;color:var(--matrix-green);font-family:'Share Tech Mono', monospace;overflow:hidden}
  canvas#matrix{position:absolute;inset:0;z-index:0}
  #overlayUI{position:absolute;inset:0;z-index:4;pointer-events:none}
  #console{position:absolute;left:22px;top:18px;z-index:6;max-width:56%;font-size:13px;line-height:1.45}
  .console-line{margin-bottom:8px; opacity:0; animation: fadeInLine 0.5s forwards; }
  @keyframes fadeInLine{0%{opacity:0}100%{opacity:1}}
  .banner{
    position:fixed;left:0;right:0;top:0;background:linear-gradient(90deg, rgba(255,0,0,0.95), rgba(200,0,0,0.85));color:#fff;padding:8px 12px;font-family:'Orbitron',sans-serif;font-weight:700;text-align:center;z-index:8;animation:flashBanner 900ms infinite;
  }
  @keyframes flashBanner{0%{opacity:1}50%{opacity:0.2}100%{opacity:1}}

  .errBox{
    position:fixed;width:300px;height:130px;background:#001100;border:2px solid var(--matrix-green);color:var(--matrix-green);padding:10px;z-index:7;box-shadow:0 20px 60px rgba(0,255,102,0.06);
    font-size:13px;animation:flicker .25s infinite, floatMove 4s linear infinite; cursor: pointer; transition: transform 0.2s;
  }
  .errBox:hover{ transform: scale(1.03); }
  @keyframes flicker{0%{opacity:1}50%{opacity:.5}100%{opacity:1}}
  @keyframes floatMove{0%{transform:translate(0,0)}50%{transform:translate(18px,-12px)}100%{transform:translate(0,0)}}

  .sysDialog{position:fixed;left:50%;top:50%;transform:translate(-50%,-50%);width:520px;background:#050505;border:3px solid #0f0;padding:16px;color:var(--matrix-green);z-index:9;box-shadow:0 50px 120px rgba(0,255,102,0.08);font-size:14px; opacity:0; animation: dialogPop 0.6s forwards 0.3s;}
  @keyframes dialogPop{0%{opacity:0; transform: translate(-50%,-50%) scale(0.8);}100%{opacity:1; transform: translate(-50%,-50%) scale(1);}}
  .sysDialog h3{margin:0 0 8px 0;font-family:'Orbitron',sans-serif;color:#fff}
  .progressBar{height:14px;background:rgba(255,255,255,0.03);border-radius:10px;overflow:hidden;margin-top:8px}
  .progressBar > i{display:block;height:100%;width:0;background:linear-gradient(90deg,var(--matrix-green), #7affb7);box-shadow:0 8px 40px rgba(0,255,102,0.08);transition:width 350ms linear}

  #glitch{position:fixed;inset:0;z-index:10;pointer-events:none;mix-blend-mode:screen;opacity:0}
  .stripe{position:absolute;left:0;right:0;height:6px;background:linear-gradient(90deg, rgba(0,255,102,0.06), rgba(0,255,102,0.02));animation:glitch 700ms infinite}
  @keyframes glitch{0%{transform:translateX(0)}50%{transform:translateX(14px)}100%{transform:translateX(0)}}

  .critical{position:fixed;right:18px;bottom:18px;background:rgba(255,59,59,0.95);color:#fff;padding:10px 14px;border-radius:10px;font-weight:700;z-index:11;animation:pulse 900ms infinite}
  @keyframes pulse{0%{transform:scale(1)}50%{transform:scale(1.05)}100%{transform:scale(1)}}

  .hcurs{display:inline-block;width:10px;height:18px;background:var(--matrix-green);margin-left:6px;vertical-align:middle;animation:blink 1s steps(2) infinite}
  @keyframes blink{50%{opacity:0}}

  /* ---------- Final card ---------- */
  #final{display:none;position:fixed;inset:0;background:linear-gradient(135deg,#ffecf2,#ffd7e8);z-index:30;overflow:auto;padding:40px; animation: fadeIn 1.5s ease-in; background-attachment: fixed;}
  #final::before{
    content:'';position:absolute;inset:0;background:radial-gradient(circle at 30% 30%, rgba(255,255,255,0.3), transparent 70%);
    animation: twinkle 4s infinite; z-index: -1; pointer-events: none;
  }
  @keyframes twinkle{
    0%,100%{ opacity: 0.2; }
    50%{ opacity: 0.6; }
  }

  .finalWrap{
    max-width:780px;margin:40px auto;background:rgba(255,255,255,0.95);border-radius:18px;padding:28px;border:2px solid rgba(255,105,180,0.12);box-shadow:0 30px 80px rgba(255,105,180,0.08);font-family:Georgia,serif;color:#6b2341; 
    transform: scale(0.9); animation: finalPop 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards 0.3s, floating 6s ease-in-out infinite;
    position: relative; overflow: hidden;
  }
  @keyframes finalPop{0%{transform:scale(0.8)}100%{transform:scale(1)}}
  @keyframes floating{
    0%,100%{ transform: scale(1) translateY(0); }
    50%{ transform: scale(1.01) translateY(-10px); }
  }

  .finalTitle{
    font-size:28px;margin:0 0 12px 0;color:#db2f6b; font-family: 'Dancing Script', cursive; 
    text-shadow: 2px 2px 4px rgba(255,105,180,0.3); 
    animation: glowTitle 2s infinite alternate, bounce 2s infinite;
    display: inline-block;
  }
  @keyframes glowTitle{
    0%{text-shadow: 2px 2px 4px rgba(255,105,180,0.3);}
    100%{text-shadow: 2px 2px 12px rgba(255,105,180,0.6);}
  }
  @keyframes bounce{
    0%,100%{ transform: translateY(0); }
    50%{ transform: translateY(-8px); }
  }

  .finalText{
    font-size:18px;line-height:1.6;white-space:pre-wrap; opacity:0; animation: fadeInText 2s forwards 0.5s;
    position: relative;
  }

  @keyframes fadeInText{0%{opacity:0}100%{opacity:1}}

  .hearts{position:absolute;inset:0;pointer-events:none;z-index:29}
  .heart{
    position:absolute;font-size:34px;opacity:0.9;animation:rise 4200ms linear infinite;
    filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.1));
  }
  @keyframes rise{0%{transform:translateY(0) scale(.8);opacity:0}50%{opacity:1}100%{transform:translateY(-900px) scale(1.3);opacity:0}}

  .particle{
    position:absolute;pointer-events:none;opacity:0.8;animation:floatParticle 6s infinite ease-in-out;z-index:28;
    text-shadow: 0 0 8px rgba(255,122,168,0.8);
  }
  @keyframes floatParticle{
    0%{transform:translate(0,0) rotate(0deg);}
    50%{transform:translate(20px,-50px) rotate(180deg);}
    100%{transform:translate(0,-100px) rotate(360deg);}
  }

  .finalBtns{margin-top:18px;display:flex;gap:12px;justify-content:center}
  .btn{padding:10px 14px;border-radius:12px;border:0;background:#ff4d84;color:#fff;font-weight:700;cursor:pointer; transition: all 0.3s; box-shadow: 0 4px 10px rgba(255,77,132,0.3);}
  .btn:hover{ background: #ff3366; transform: translateY(-2px); box-shadow: 0 8px 20px rgba(255,77,132,0.4); }
  .btn:active{ transform: translateY(1px); }
  .btnAlt{background:transparent;border:1px solid #ff4d84;color:#ff4d84; transition: all 0.3s;}
  .btnAlt:hover{ background: rgba(255,77,132,0.1); transform: translateY(-2px); }

  .confetti{
    position:fixed;width:10px;height:10px;pointer-events:none;z-index:50;opacity:0;
    border-radius: 50%;
    transform-origin: center;
  }

  .star{
    position: absolute; background: white; border-radius: 50%; pointer-events: none;
    animation: twinkleStar 3s infinite;
  }
  @keyframes twinkleStar{
    0%,100%{ opacity: 0.3; transform: scale(1); }
    50%{ opacity: 1; transform: scale(1.2); }
  }

  .loveBurst{
    position: fixed; inset: 0; z-index: 40; pointer-events: none; display: flex; justify-content: center; align-items: center;
    opacity: 0;
  }
  .loveBurst.show{
    animation: burstIn 1s forwards 0.5s;
  }
  @keyframes burstIn{
    0%{ opacity: 0; transform: scale(0.5); }
    100%{ opacity: 0.8; transform: scale(1.5); }
  }
  .loveBurst div{
    font-size: 80px; animation: spinDrop 3s infinite;
    text-shadow: 0 0 20px var(--glow-pink);
  }
  @keyframes spinDrop{
    0%{ transform: translateY(-100px) rotate(0deg); opacity: 0; }
    20%{ opacity: 1; }
    100%{ transform: translateY(100vh) rotate(720deg); opacity: 0; }
  }

  @media (max-width:820px){ 
    .sysDialog{width:88%} 
    .errBox{width:240px;height:110px} 
    .finalWrap{margin:20px;padding:18px} 
    .finalTitle{font-size:24px}
  }
</style>
</head>
<body>

<!-- Cover -->
<section id="cover">
  <div class="coverHeart" style="top:20%; left:10%; animation-delay:0s;">💖</div>
  <div class="coverHeart" style="top:40%; left:80%; animation-delay:1s;">❤️</div>
  <div class="coverHeart" style="top:70%; left:20%; animation-delay:2s;">💞</div>
  <div class="coverHeart" style="top:30%; left:70%; animation-delay:3s;">💗</div>
  <div class="coverHeart" style="top:60%; left:40%; animation-delay:4s;">💕</div>

  <div class="card" role="region" aria-label="Carta">
    <h1>💌 Una carta especial para ti</h1>
    <p>He preparado algo sorpresa. Cuando estés listo(a), pulsa <strong>Abrir carta</strong>. (BerMatMods.)</p>
    <button class="openBtn" id="openBtn" aria-label="Abrir carta">Abrir carta 💌</button>
  </div>
</section>

<!-- BerMatMods HACKEO REAL -->
<section id="sim" aria-hidden="true">
  <canvas id="matrix"></canvas>
  <div class="banner" id="banner" style="display:none">¡CRÍTICO! PROCESOS NO AUTORIZADOS DETECTADOS</div>
  <div id="console" aria-live="polite" role="status"></div>
  <div class="sysDialog" id="sysDialog" style="display:none">
    <h3>DETECCIÓN: PROCESO SOSPECHOSO</h3>
    <div id="sysMsg">Analizando integridad...</div>
    <div class="progressBar" aria-hidden="true"><i id="progBar"></i></div>
  </div>
  <div id="glitch"></div>
  <div class="critical" id="critical" style="display:none">ACCESO REMOTO EN CURSO</div>

  <!-- AUDIO (todos pre-cargados) -->
  <audio id="alarm" loop preload="auto" src="https://actions.google.com/sounds/v1/alarms/alarm_clock.ogg"></audio>
  <audio id="beep" preload="auto" src="https://actions.google.com/sounds/v1/alarms/beep_short.ogg"></audio>
  <audio id="siren" loop preload="auto" src="https://actions.google.com/sounds/v1/alarms/siren.ogg"></audio>
  <audio id="typewriter" preload="auto" src="https://actions.google.com/sounds/v1/office/typewriter_key_press.ogg"></audio>
  <audio id="glitchSound" preload="auto" src="https://actions.google.com/sounds/v1/technology/glitch_down.ogg"></audio>
  <audio id="systemBeep" preload="auto" src="https://actions.google.com/sounds/v1/technology/system_notification_01.ogg"></audio>
  <audio id="romantic" preload="auto" src="https://actions.google.com/sounds/v1/alarms/gentle_wake_up_tone.ogg"></audio>
  <audio id="chime" preload="auto" src="https://actions.google.com/sounds/v1/alarms/medieval_fanfare.ogg"></audio>
</section>

<!-- Final Card -->
<section id="final" aria-hidden="true">
  <div class="hearts" id="hearts"></div>
  <div id="particles" class="hearts"></div>
  <div id="confettiContainer"></div>
  <div id="starsContainer"></div>
  <div id="loveBurst" class="loveBurst"></div>

  <div class="finalWrap" role="dialog" aria-modal="true" aria-label="Carta romántica">
    <h2 class="finalTitle">💚 TE AMO MUCHÍSIMO MI REINA 💚</h2>
    <div class="finalText" id="finalText"></div>

    <div class="finalBtns">
      <button class="btn" id="replay">Volver a empezar</button>
      <button class="btnAlt" id="close">Cerrar</button>
    </div>
  </div>
</section>

<script>
/* CONFIG */
const REVEAL_SECONDS = 22; // 22 segundos de hackeo intenso
const ERROR_INTERVAL_MS = 380; // más frecuente = más caos
const ERROR_LIFE_MS = 7000;

/* ELEMENTS */
const openBtn = document.getElementById('openBtn');
const sim = document.getElementById('sim');
const cover = document.getElementById('cover');
const consoleEl = document.getElementById('console');
const matrixCanvas = document.getElementById('matrix');
const banner = document.getElementById('banner');
const sysDialog = document.getElementById('sysDialog');
const sysMsg = document.getElementById('sysMsg');
const progBar = document.getElementById('progBar');
const glitch = document.getElementById('glitch');
const critical = document.getElementById('critical');
const alarm = document.getElementById('alarm');
const beep = document.getElementById('beep');
const siren = document.getElementById('siren');
const typewriter = document.getElementById('typewriter');
const glitchSound = document.getElementById('glitchSound');
const systemBeep = document.getElementById('systemBeep');
const romantic = document.getElementById('romantic');
const chime = document.getElementById('chime');
const finalSec = document.getElementById('final');
const finalText = document.getElementById('finalText');
const heartsWrap = document.getElementById('hearts');
const particlesWrap = document.getElementById('particles');
const confettiContainer = document.getElementById('confettiContainer');
const starsContainer = document.getElementById('starsContainer');
const loveBurst = document.getElementById('loveBurst');
const replay = document.getElementById('replay');
const closeBtn = document.getElementById('close');

let errInterval, progInterval, revealTimeout, matrixTimer, typeInterval;
let progValue = 0;
let running = false;

/* Utilities */
function rand(a,b){ return Math.floor(Math.random()*(b-a+1))+a; }
function timeStamp(){ const d=new Date(); return d.toTimeString().slice(0,8); }
function randomChoice(arr){ return arr[Math.floor(Math.random()*arr.length)]; }

/* Iniciar al hacer clic */
openBtn.addEventListener('click', () => {
  cover.style.display = 'none';
  sim.style.display = 'block';
  sim.setAttribute('aria-hidden','false');
  startBerMatMods();
});

/* MATRIX */
(function startMatrix(){
  const canvas = matrixCanvas;
  const ctx = canvas.getContext('2d');
  function resize(){ canvas.width = window.innerWidth; canvas.height = window.innerHeight; init(); }
  let cols, drops, letters, fontSize=14;
  function init(){
    letters = "01➪𝐁𝐞𝐫𝐌𝐚𝐭_𝐌𝐨𝐝𝐬𖤍ABCDEFGHIJKLMNOPQRSTUVWXYZ!@#$%&*".split("");
    cols = Math.floor(canvas.width / fontSize) + 1;
    drops = Array(cols).fill(0).map(()=>Math.random()*1000);
  }
  function draw(){
    ctx.fillStyle = "rgba(0,0,0,0.08)";
    ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle = "#00ff66";
    ctx.font = fontSize + "px Share Tech Mono, monospace";
    for(let i=0;i<drops.length;i++){
      const t = letters[Math.floor(Math.random()*letters.length)];
      ctx.fillText(t, i*fontSize, drops[i]*fontSize);
      drops[i] += 1 + Math.random()*1.6;
      if(drops[i]*fontSize > canvas.height && Math.random() > 0.975) drops[i]=0;
    }
  }
  window.addEventListener('resize', resize);
  resize();
  matrixTimer = setInterval(draw, 35);
})();

/* ¡MENSAJES DE HACKEO REALISTA! */
const consoleLines = [
  `[${timeStamp()}] INICIANDO SECUENCIA DE INTRUSIÓN...`,
  `[${timeStamp()}] OBTENIENDO PERMISOS ROOT... ✔`,
  `[${timeStamp()}] DESACTIVANDO FIREWALL... ✔`,
  `[${timeStamp()}] ACCEDIENDO A CUENTA DE GOOGLE... ✔`,
  `[${timeStamp()}] EXTRAYENDO TOKEN DE SESIÓN... ✔`,
  `[${timeStamp()}] CONECTANDO A SERVIDOR C2 (BerMatMods )... ✔`,
  `[${timeStamp()}] DESCARGANDO MÓDULO: PHOTO-EXTRACTOR-V3...`,
  `[${timeStamp()}] ESCANEANDO ALMACENAMIENTO... 12,487 ARCHIVOS ENCONTRADOS`,
  `[${timeStamp()}] FILTRANDO: FOTOS_OCULTAS/, VIDEOS_PRIVADOS/, BACKUPS/`,
  `[${timeStamp()}] DESCARGANDO: IMG_20240517_OCULTA.jpg (3.2MB)`,
  `[${timeStamp()}] DESCARGANDO: VIDEO_PRIVADO_ANNIV.mp4 (28.7MB)`,
  `[${timeStamp()}] ACCEDIENDO A WHATSAPP DATABASE... ✔`,
  `[${timeStamp()}] RECUPERANDO MENSAJES BORRADOS (ÚLTIMOS 30 DÍAS)...`,
  `[${timeStamp()}] CLAVE OBTENIDA: "Enviada al servidor"`,
  `[${timeStamp()}] OBTENIENDO UBICACIÓN GPS EN TIEMPO REAL... LAT: 19.4326, LNG: -99.1332`,
  `[${timeStamp()}] SUBIENDO DATOS A NUBE ENCRIPTADA (BerMatMods )...`,
  `[${timeStamp()}] PROGRESO: 87%... ESPERANDO CONFIRMACIÓN DE RECEPCIÓN...`
];

const errorMessages = [
  "⚠️ ¡FOTOS OCULTAS EXTRAÍDAS!\nRuta: /storage/emulated/0/.secret_album/",
  "⚠️ ¡CONTRASEÑA CLONADA!\nCuenta:Enviada Al Servidor",
  "⚠️ ¡UBICACIÓN EN TIEMPO REAL!\nÚltima posición:IP Rastreado",
  "⚠️ ¡MENSAJES BORRADOS RECUPERADOS!\nTotal: 847 mensajes privados",
  "⚠️ ¡BACKUP DE ICLOUD COMPROMETIDO!\nDescargando Keychain...",
  "⚠️ ¡ACCESO  OBTENIDO!\nSesión activa hasta: 2025",
  "⚠️ ¡CLONACIÓN DE WHATSAPP COMPLETA!\nDispositivo esclavo conectado",
  "⚠️ ¡VIDEOS OCULTOS DESCARGADOS!\nCarpeta: /Movies/.private/"
];

/* Efectos de sonido al escribir */
function addConsoleLine(txt){
  const d = document.createElement('div');
  d.className = 'console-line';
  d.textContent = txt;
  consoleEl.appendChild(d);
  consoleEl.scrollTop = consoleEl.scrollHeight;

  // Sonido de tecleo por cada línea
  if(typewriter) {
    typewriter.currentTime = 0;
    typewriter.volume = 0.12;
    typewriter.play().catch(()=>{});
  }

  // Si es mensaje crítico, shake + beep
  if(txt.includes("OCULTA") || txt.includes("ROBADA") || txt.includes("CLONACIÓN")){
    document.body.style.filter = 'contrast(1.05) saturate(1.1)';
    setTimeout(()=>document.body.style.filter = '', 700);
    if(systemBeep) {
      systemBeep.currentTime = 0;
      systemBeep.volume = 0.3;
      systemBeep.play().catch(()=>{});
    }
  }
}

/* Crear ventanas de error con sonido */
function createErrBox(){
  const box = document.createElement('div');
  box.className = 'errBox';
  box.style.top = (Math.random()*(window.innerHeight-140))+'px';
  box.style.left = (Math.random()*(window.innerWidth-320))+'px';
  box.innerText = randomChoice(errorMessages);
  document.body.appendChild(box);
  box.style.transform = `rotate(${rand(-3,3)}deg)`;

  if(Math.random()>0.8) box.animate([{transform:'translateY(0)'}, {transform:'translateY(-8px)'}, {transform:'translateY(0)'}], {duration:800,iterations:1});

  box.addEventListener('click', () => {
    if(glitchSound) {
      glitchSound.currentTime = 0;
      glitchSound.volume = 0.4;
      glitchSound.play().catch(()=>{});
    }
    spawnGlitchExplosion(box.getBoundingClientRect());
    box.remove();
  });

  if(Math.random() > 0.82){
    showSysDialog("DESENCRIPTANDO METADATOS DE FOTOS...");
  }
  if(navigator.vibrate) try{ navigator.vibrate([140,60,120]); }catch(e){}
  setTimeout(()=>{ if(box && box.parentNode) box.remove(); }, ERROR_LIFE_MS);
}

function spawnGlitchExplosion(rect){
  for(let i=0; i<12; i++){
    const stripe = document.createElement('div');
    stripe.className = 'stripe';
    stripe.style.top = rect.top + rand(-20, rect.height + 20) + 'px';
    stripe.style.left = rect.left + rand(-30, rect.width + 30) + 'px';
    stripe.style.width = '80px';
    stripe.style.height = '4px';
    stripe.style.opacity = 0.7;
    stripe.style.animation = 'glitch 300ms forwards';
    glitch.appendChild(stripe);
    setTimeout(() => stripe.remove(), 500);
  }
}

function showSysDialog(msg){
  sysMsg.textContent = msg;
  sysDialog.style.display = 'block';
  progValue = 0;
  progBar.style.width = '0%';
  if(typeof progInterval !== 'undefined') clearInterval(progInterval);
  progInterval = setInterval(()=> {
    progValue += rand(4,10);
    if(progValue > 98) progValue = 98;
    progBar.style.width = progValue + '%';
  }, 600);
  setTimeout(()=>{ sysDialog.style.display = 'none'; clearInterval(progInterval); }, rand(3000,7000));
}

function spawnGlitch(){
  const s = document.createElement('div');
  s.className='stripe';
  s.style.top = rand(0, window.innerHeight) + 'px';
  glitch.appendChild(s);
  glitch.style.opacity = 1;
  setTimeout(()=>{ s.remove(); if(!glitch.hasChildNodes()) glitch.style.opacity = 0; }, 1400 + rand(0,900));
}

function flashCritical(){
  critical.style.display = 'block';
  setTimeout(()=> critical.style.display='none', 2400);
}

/* ¡INICIAR HACKEO REAL! */
function startBerMatMods(){
  if(running) return;
  running = true;

  // Mostrar banner de alerta
  banner.style.display='block';
  setTimeout(()=> banner.style.display='none', 5000);

  // ¡SONIDOS CAÓTICOS EN LOOP!
  if(alarm) {
    alarm.volume = 0.35;
    alarm.play().catch(()=>{});
  }
  if(siren) {
    siren.volume = 0.25;
    siren.play().catch(()=>{});
  }

  // Líneas de consola con pausas dramáticas
  let li = 0;
  typeInterval = setInterval(()=> {
    if(li < consoleLines.length) {
      addConsoleLine(consoleLines[li++]);
    } else {
      // Mensajes aleatorios de "mantenimiento de hackeo"
      const extras = [
        `[${timeStamp()}] MANTENIENDO SESIÓN ACTIVA...`,
        `[${timeStamp()}] BORRANDO LOGS DE ACCESO...`,
        `[${timeStamp()}] CAMUFLANDO TRÁFICO COMO ACTUALIZACIÓN DE SISTEMA...`,
        `[${timeStamp()}] ESPERANDO RESPUESTA DEL SERVIDOR C2...`,
        `[${timeStamp()}] CIFRANDO DATOS EXTRAÍDOS...`,
        `[${timeStamp()}] PREPARANDO PAQUETE FINAL PARA ENTREGA...`
      ];
      addConsoleLine(randomChoice(extras));
    }
  }, 1100);

  // Errores, glitches, críticos — ¡CAOS TOTAL!
  errInterval = setInterval(()=> {
    createErrBox();
    if(Math.random() > 0.5) createErrBox(); // ¡Doble error!
    if(Math.random() > 0.7) spawnGlitch();
    if(Math.random() > 0.8) flashCritical();
    if(Math.random() > 0.9) {
      // ¡Mensaje aleatorio adicional en consola!
      const randMsgs = [
        `[${timeStamp()}] ¡ALERTA! DISPOSITIVO BLOQUEADO POR 5s (falso)`,
        `[${timeStamp()}] ¡ÉXITO! FOTOS DEL 14-F DESCARGADAS`,
        `[${timeStamp()}] ¡ATENCIÓN! UBICACIÓN ACTUALIZADA: CAFETERÍA FAVORITA`,
        `[${timeStamp()}] ¡COMPLETADO! VIDEOS DE ANIVERSARIO EXTRAÍDOS`
      ];
      addConsoleLine(randomChoice(randMsgs));
    }
  }, ERROR_INTERVAL_MS);

  // Diálogos de sistema estratégicos
  setTimeout(()=> showSysDialog("EXTRAYENDO METADATOS DE FOTOS..."), 4000);
  setTimeout(()=> showSysDialog("DESCIFRANDO CLAVES DE CIFRADO..."), 10000);
  setTimeout(()=> showSysDialog("PREPARANDO ENTREGA DEL PAQUETE DE AMOR..."), 16000);

  // ¡Revelar carta después de 22 segundos!
  revealTimeout = setTimeout(()=> {
    stopBerMatModsAndReveal();
    clearInterval(typeInterval);
  }, REVEAL_SECONDS * 1000);
}

/* ¡DETENER TODO EL HACKEO DE GOLPE! */
function stopBerMatModsAndReveal(){
  running = false;

  // Detener todos los intervalos
  clearInterval(errInterval);
  clearInterval(matrixTimer);
  clearInterval(progInterval);
  clearInterval(typeInterval);
  clearTimeout(revealTimeout);

  // ¡DETENER TODOS LOS SONIDOS DE HACKEO!
  [alarm, siren, beep, glitchSound, systemBeep].forEach(a => {
    if(a) {
      a.pause();
      a.currentTime = 0;
    }
  });

  // Detener vibración
  if(navigator.vibrate) try{ navigator.vibrate(0); }catch(e){}

  // Limpiar interfaz
  document.querySelectorAll('.errBox').forEach(n=>n.remove());
  sysDialog.style.display='none';
  glitch.innerHTML = '';
  banner.style.display='none';
  critical.style.display='none';
  consoleEl.innerHTML = '';

  // Ocultar simulación
  sim.style.display = 'none';
  sim.setAttribute('aria-hidden','true');

  // ¡Mostrar carta romántica con transición suave!
  showFinalCard();
}

/* Carta final con efectos mágicos */
function showFinalCard(){
  finalSec.style.display = 'block';
  finalSec.setAttribute('aria-hidden','false');

  // Estrellas de fondo
  for(let i=0; i<50; i++){
    const star = document.createElement('div');
    star.className = 'star';
    star.style.width = star.style.height = rand(2,6) + 'px';
    star.style.left = rand(0,100) + '%';
    star.style.top = rand(0,100) + '%';
    star.style.animationDelay = Math.random() * 5 + 's';
    starsContainer.appendChild(star);
  }

  const text = `Mi Amor💖,

Sé que te asusté con la broma, pero lo que sí es real es lo que siento por ti.

Eres lo más valioso que tengo, mi reina hermosa. 
Siempre voy a estar a tu lado en las buenas y en las malas.

Con todo mi cariño,
➪𝐁𝐞𝐫𝐌𝐚𝐭_𝐌𝐨𝐝𝐬𖤍 (Anth'Zz)`;

  let idx = 0;
  finalText.textContent = '';

  (function escribe(){
    if(idx < text.length){
      finalText.textContent += text[idx++];
      if(text[idx-1] !== ' ' && text[idx-1] !== '\n'){
        if(typewriter) {
          typewriter.currentTime = 0;
          typewriter.volume = 0.15;
          typewriter.play().catch(()=>{});
        }
      }
      setTimeout(escribe, 50);
    } else {
      // ¡Campanitas mágicas y música romántica!
      if(chime) {
        chime.currentTime = 0;
        chime.volume = 0.4;
        chime.play().catch(()=>{});
      }

      if(romantic) {
        romantic.volume = 0.25;
        romantic.loop = true;
        romantic.play().catch(()=>{});
      }

      // ¡CONFETI, CORAZONES, PARTÍCULAS!
      launchConfetti();
      spawnParticles(35);
      spawnHearts(25);

      // ¡Explosión final de amor!
      setTimeout(() => {
        loveBurst.classList.add('show');
        for(let i=0; i<18; i++){
          const heart = document.createElement('div');
          heart.textContent = randomChoice(['💖','❤️','💘','💝','💗','✨','🌹']);
          heart.style.animationDelay = i * 0.08 + 's';
          loveBurst.appendChild(heart);
        }
        setTimeout(() => {
          loveBurst.classList.remove('show');
          loveBurst.innerHTML = '';
        }, 4000);
      }, 1200);
    }
  })();
}

/* Funciones de decoración (corazones, partículas, confeti) */
function spawnHearts(n){
  const emojis = ['❤️','💖','💞','😍','💗','💓','💘','💝','💕','🫀','🫶'];
  for(let i=0;i<n;i++){
    const el = document.createElement('div');
    el.className='heart';
    el.style.left = (10 + Math.random()*80) + '%';
    el.style.fontSize = (18 + Math.random()*40) + 'px';
    el.style.animationDuration = (3800 + Math.random()*3000) + 'ms';
    el.style.opacity = (0.6 + Math.random()*0.5);
    el.textContent = randomChoice(emojis);
    heartsWrap.appendChild(el);
    setTimeout(()=> el.remove(), 9000 + Math.random()*3000);
  }
}

function spawnParticles(n){
  const emojis = ['✨','🌟','💫','🌸','🌹','💕','💗','💖','💮','🪷','🦋','🕊️','🫧','🪩'];
  for(let i=0; i<n; i++){
    const p = document.createElement('div');
    p.className = 'particle';
    p.textContent = randomChoice(emojis);
    p.style.left = rand(5,95) + '%';
    p.style.top = rand(10,90) + '%';
    p.style.fontSize = rand(16,36) + 'px';
    p.style.animationDuration = (4 + Math.random()*7) + 's';
    p.style.animationDelay = Math.random()*4 + 's';
    particlesWrap.appendChild(p);
    setTimeout(()=> p.remove(), 12000);
  }
}

function launchConfetti(){
  const colors = ['#ff4d84', '#ff7aa8', '#ffd7e8', '#ff9a9e', '#a8edea', '#fecfef', '#ffcc00', '#ff66cc', '#66ccff', '#ff3366', '#cc66ff'];
  for(let i=0; i<300; i++){
    const c = document.createElement('div');
    c.className = 'confetti';
    c.style.backgroundColor = randomChoice(colors);
    c.style.left = rand(0, window.innerWidth) + 'px';
    c.style.top = window.innerHeight + 'px';
    c.style.width = rand(6,18) + 'px';
    c.style.height = rand(6,18) + 'px';
    c.style.transform = `rotate(${rand(0,360)}deg)`;
    c.style.opacity = Math.random() * 0.8 + 0.2;
    c.style.borderRadius = Math.random() > 0.5 ? '50%' : (Math.random() > 0.5 ? '10%' : '0');
    confettiContainer.appendChild(c);

    c.animate([
      { transform: `translateY(0) rotate(0deg)`, opacity: 1 },
      { transform: `translateY(-${window.innerHeight + 300}px) rotate(${rand(360,1440)}deg)`, opacity: 0 }
    ], {
      duration: rand(4000,9000),
      easing: 'cubic-bezier(0.2, 0.8, 0.6, 1)',
      fill: 'forwards'
    });

    c.addEventListener('animationend', () => c.remove());
  }
}

/* Botones */
replay.addEventListener('click', ()=> {
  [romantic, chime].forEach(a => { if(a) { a.pause(); a.currentTime = 0; } });
  location.reload();
});

closeBtn.addEventListener('click', ()=> {
  [romantic, chime].forEach(a => { if(a) { a.pause(); a.currentTime = 0; } });
  finalSec.style.display='none';
  cover.style.display='block';
});

window.startBerMatMods = startBerMatMods;
</script>

</body>
</html>
