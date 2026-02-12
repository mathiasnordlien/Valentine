<!doctype html>
<html lang="no">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>💗</title>

  <style>
    :root{
      --p50:#fff0f6; --p100:#ffe0ee; --p200:#ffc2dd; --p300:#ff9ac7;
      --p400:#ff6cab; --p500:#ff3d93; --p600:#e81d7b; --p700:#b90f5f;
      --ink:#3a0b22;
      --card: rgba(255,240,246,.82);
      --shadow: 0 22px 70px rgba(232,29,123,.22);
      --shadow2: 0 14px 28px rgba(58,11,34,.12);
    }

    *{box-sizing:border-box}
    body{
      margin:0; min-height:100vh; display:grid; place-items:center;
      font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;
      color:var(--ink);
      background:
        radial-gradient(900px 500px at 15% 10%, rgba(255,240,246,.95), transparent 60%),
        radial-gradient(700px 420px at 85% 25%, rgba(255,154,199,.55), transparent 60%),
        radial-gradient(800px 520px at 50% 95%, rgba(255,61,147,.22), transparent 65%),
        linear-gradient(135deg, var(--p100), var(--p400));
      overflow:hidden;
    }

    .card{
      width:min(620px,92vw);
      border-radius:26px;
      padding:26px;
      background:var(--card);
      backdrop-filter:blur(10px);
      box-shadow:var(--shadow);
      border:1px solid rgba(255,61,147,.18);
      position:relative;
      overflow:hidden;
    }

    .sparkles{
      position:absolute; inset:-60px; pointer-events:none; opacity:.45;
      background:
        radial-gradient(circle at 12% 22%, rgba(255,61,147,.35) 0 6px, transparent 7px),
        radial-gradient(circle at 72% 18%, rgba(255,61,147,.28) 0 4px, transparent 5px),
        radial-gradient(circle at 86% 52%, rgba(255,61,147,.22) 0 7px, transparent 8px),
        radial-gradient(circle at 22% 78%, rgba(255,61,147,.25) 0 5px, transparent 6px);
    }

    .question{
      margin: 6px 0 14px;
      text-align:center;
      font-size:clamp(26px,4vw,40px);
      font-weight:900;
      letter-spacing:.2px;
    }

    .sub{
      margin:0 0 18px;
      text-align:center;
      opacity:.9;
      font-weight:650;
    }

    .stage{
      position:relative;
      height:160px;
      border-radius:20px;
      background:linear-gradient(135deg, rgba(255,255,255,.55), rgba(255,224,238,.55));
      border:1px solid rgba(255,61,147,.15);
      box-shadow:var(--shadow2);
      overflow:hidden;
    }

    .buttons{ position:relative; width:100%; height:100%; }

    button{
      border:0;
      border-radius:999px;
      padding:14px 24px;
      font-size:18px;
      font-weight:900;
      cursor:pointer;
      user-select:none;
      transition:transform .12s ease, filter .12s ease;
      box-shadow:0 14px 30px rgba(232,29,123,.25);
      white-space:nowrap;
    }
    button:hover{ filter:brightness(1.03); }
    button:active{ transform:scale(.98); }

    #yesBtn{
      position:absolute;
      left:50%; top:50%;
      transform:translate(-50%,-50%);
      color:#fff;
      background:linear-gradient(135deg, var(--p500), var(--p700));
      z-index:2;
    }

    /* NEI: konstant bevegelse + umulig å trykke */
    #noBtn{
      position:absolute;
      left:10px; top:10px;
      color:#fff;
      background:linear-gradient(135deg, var(--p300), var(--p600));
      z-index:1;
      pointer-events:none; /* <- gjør den i praksis umulig å klikke */
    }

    /* Modal base */
    .overlay{
      position:fixed; inset:0;
      background:rgba(58,11,34,.55);
      display:none;
      place-items:center;
      padding:18px;
      z-index:50;
    }
    .overlay.show{ display:grid; }

    .modal{
      width:min(560px,94vw);
      background:rgba(255,240,246,.92);
      border:1px solid rgba(255,61,147,.18);
      border-radius:26px;
      overflow:hidden;
      box-shadow:var(--shadow);
      transform:translateY(8px);
      animation: pop .18s ease-out forwards;
    }
    @keyframes pop{ to{ transform:translateY(0) } }

    .modal img{
      width:100%;
      height:320px;
      object-fit:cover;
      display:block;
      filter:saturate(1.05) contrast(1.02);
    }

    .content{ padding:18px 18px 22px; text-align:center; }
    .content h2{ margin:8px 0 10px; font-size:28px; }
    .content p{ margin:0 0 16px; line-height:1.5; opacity:.95; }

    .row{
      display:flex;
      justify-content:center;
      gap:10px;
      flex-wrap:wrap;
    }

    .ghost{
      background:linear-gradient(135deg, rgba(255,255,255,.9), rgba(255,224,238,.9));
      color:var(--ink);
      border:2px solid rgba(255,61,147,.18);
      box-shadow:none;
      font-weight:900;
    }

    .primary{
      color:#fff;
      background:linear-gradient(135deg, var(--p500), var(--p700));
    }
  </style>
</head>

<body>
  <div class="card">
    <div class="sparkles"></div>

    <div class="question">Vil du være min Valentine?💘</div>
    <div class="sub">Velg rolig. “Nei” er ikke et reelt alternativ. 😈</div>

    <div class="stage" id="stage">
      <div class="buttons">
        <button id="yesBtn">JA</button>
        <button id="noBtn">Nei</button>
      </div>
    </div>
  </div>

  <!-- Modal 1 (etter JA) -->
  <div class="overlay" id="overlay1" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true" aria-label="Svar">
      <img src="bilde1.jpg" alt="Bilde av dere" />
      <div class="content">
        <h2>Ok, deal! 🥹💞</h2>
        <p>Du trykket JA. Og jeg tar det som et livslangt ja. 🌹</p>
        <div class="row">
          <button class="primary" id="aboutBtn">Om din valentine</button>
          <button class="ghost" id="close1">Lukk</button>
        </div>
      </div>
    </div>
  </div>

  <!-- Modal 2 (Om din valentine) -->
  <div class="overlay" id="overlay2" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true" aria-label="Om din valentine">
      <img src="bilde2.jpg" alt="Bilde av dere" />
      <div class="content">
        <h2>Om din valentine 💗</h2>
        <p>
          Mathias møtte Emilie på videregående – og helt ærlig: han har vært sykt heldig
          med valentiner i åtte år nå. Han er skikkelig forelska i deg, og det største ønsket hans
          er å få dele selve valentinsdagen med deg.
          <br><br>
          Når han ser på deg, tenker han at han har funnet drømmedama. Han er utrolig glad
          for den du er – og han er stolt av deg, på ekte.
          <br><br>
          Og så går det rykter… om at en liten baby er på vei 👀 Mathias klarer uansett ikke å vente.
          Han mener barnet kommer til å bli det fineste mennesket i verden – spesielt når det kommer fra deg. 💞
        </p>
        <div class="row">
          <button class="ghost" id="backBtn">Tilbake</button>
          <button class="ghost" id="close2">Lukk</button>
        </div>
      </div>
    </div>
  </div>

  <script>
    const stage = document.getElementById('stage');
    const noBtn = document.getElementById('noBtn');
    const yesBtn = document.getElementById('yesBtn');

    const overlay1 = document.getElementById('overlay1');
    const overlay2 = document.getElementById('overlay2');

    const close1 = document.getElementById('close1');
    const close2 = document.getElementById('close2');
    const aboutBtn = document.getElementById('aboutBtn');
    const backBtn = document.getElementById('backBtn');

    // ---- NEI: konstant bevegelse (bouncer rundt) + dodger musepeker ----
    let x = 10, y = 10;
    let vx = 2.6, vy = 2.1;
    let mouseX = 9999, mouseY = 9999;

    stage.addEventListener('mousemove', (e) => {
      const r = stage.getBoundingClientRect();
      mouseX = e.clientX - r.left;
      mouseY = e.clientY - r.top;
    });

    function tickNoBtn(){
      const s = stage.getBoundingClientRect();
      const b = noBtn.getBoundingClientRect();

      const w = s.width;
      const h = s.height;
      const bw = b.width;
      const bh = b.height;

      // flytt
      x += vx;
      y += vy;

      // bounce i kantene
      if (x <= 6) { x = 6; vx *= -1; }
      if (y <= 6) { y = 6; vy *= -1; }
      if (x >= w - bw - 6) { x = w - bw - 6; vx *= -1; }
      if (y >= h - bh - 6) { y = h - bh - 6; vy *= -1; }

      // dodge musepekeren: hvis du kommer nær, så skifter den retning
      const cx = x + bw/2;
      const cy = y + bh/2;
      const dx = cx - mouseX;
      const dy = cy - mouseY;
      const dist = Math.hypot(dx, dy);

      if (dist < 110) {
        // push bort fra cursor
        const push = 0.9;
        vx += (dx / (dist || 1)) * push;
        vy += (dy / (dist || 1)) * push;

        // cap fart så den ikke blir helt kaos
        const maxV = 5.2;
        vx = Math.max(-maxV, Math.min(maxV, vx));
        vy = Math.max(-maxV, Math.min(maxV, vy));
      }

      noBtn.style.left = `${x}px`;
      noBtn.style.top = `${y}px`;

      requestAnimationFrame(tickNoBtn);
    }
    requestAnimationFrame(tickNoBtn);

    // ---- Modaler ----
    yesBtn.addEventListener('click', () => {
      overlay1.classList.add('show');
      overlay1.setAttribute('aria-hidden', 'false');
      confettiHearts();
    });

    close1.addEventListener('click', () => {
      overlay1.classList.remove('show');
      overlay1.setAttribute('aria-hidden', 'true');
    });

    aboutBtn.addEventListener('click', () => {
      overlay1.classList.remove('show');
      overlay1.setAttribute('aria-hidden', 'true');

      overlay2.classList.add('show');
      overlay2.setAttribute('aria-hidden', 'false');
    });

    backBtn.addEventListener('click', () => {
      overlay2.classList.remove('show');
      overlay2.setAttribute('aria-hidden', 'true');

      overlay1.classList.add('show');
      overlay1.setAttribute('aria-hidden', 'false');
    });

    close2.addEventListener('click', () => {
      overlay2.classList.remove('show');
      overlay2.setAttribute('aria-hidden', 'true');
    });

    // klikk utenfor modal lukker
    overlay1.addEventListener('click', (e) => { if (e.target === overlay1) close1.click(); });
    overlay2.addEventListener('click', (e) => { if (e.target === overlay2) close2.click(); });

    function confettiHearts() {
      const amount = 26;
      for (let i = 0; i < amount; i++) {
        const el = document.createElement('div');
        el.textContent = Math.random() > 0.5 ? "💖" : "💗";
        el.style.position = "fixed";
        el.style.left = Math.random() * 100 + "vw";
        el.style.top = "-10vh";
        el.style.fontSize = (16 + Math.random() * 18) + "px";
        el.style.transform = `rotate(${Math.random() * 80 - 40}deg)`;
        el.style.zIndex = 60;
        el.style.transition = "transform 1.6s linear, top 1.6s linear, opacity 1.6s linear";
        document.body.appendChild(el);

        requestAnimationFrame(() => {
          el.style.top = (80 + Math.random() * 30) + "vh";
          el.style.opacity = "0";
          el.style.transform += ` translateX(${(Math.random() * 120 - 60)}px)`;
        });

        setTimeout(() => el.remove(), 1700);
      }
    }
  </script>
</body>
</html>
