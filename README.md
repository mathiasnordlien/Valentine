<!doctype html>
<html lang="no">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Valentine? 💗</title>

  <style>
    :root{
      --pink-50:  #fff0f6;
      --pink-100: #ffe0ee;
      --pink-200: #ffc2dd;
      --pink-300: #ff9ac7;
      --pink-400: #ff6cab;
      --pink-500: #ff3d93;
      --pink-600: #e81d7b;
      --pink-700: #c41266;

      --ink: #3a0b22;
      --card: rgba(255, 240, 246, .82);
      --glass: rgba(255, 255, 255, .45);

      --shadow: 0 22px 70px rgba(232, 29, 123, .22);
      --shadow-2: 0 14px 28px rgba(58, 11, 34, .12);
    }

    * { box-sizing: border-box; }
    body{
      margin: 0;
      min-height: 100vh;
      display: grid;
      place-items: center;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      color: var(--ink);

      /* rosa gradient stack */
      background:
        radial-gradient(900px 500px at 15% 10%, rgba(255, 240, 246, .95), transparent 60%),
        radial-gradient(700px 420px at 85% 25%, rgba(255, 154, 199, .55), transparent 60%),
        radial-gradient(800px 520px at 50% 95%, rgba(255, 61, 147, .22), transparent 65%),
        linear-gradient(135deg, var(--pink-100), var(--pink-400));
      overflow-x: hidden;
    }

    .card{
      width: min(600px, 92vw);
      border-radius: 26px;
      padding: 28px;
      background: var(--card);
      backdrop-filter: blur(10px);
      box-shadow: var(--shadow);
      position: relative;
      overflow: hidden;
      border: 1px solid rgba(255, 61, 147, .18);
    }

    .sparkles{
      position: absolute;
      inset: -60px;
      pointer-events: none;
      opacity: .45;
      background:
        radial-gradient(circle at 12% 22%, rgba(255, 61, 147, .35) 0 6px, transparent 7px),
        radial-gradient(circle at 72% 18%, rgba(255, 61, 147, .28) 0 4px, transparent 5px),
        radial-gradient(circle at 86% 52%, rgba(255, 61, 147, .22) 0 7px, transparent 8px),
        radial-gradient(circle at 22% 78%, rgba(255, 61, 147, .25) 0 5px, transparent 6px);
      filter: blur(.2px);
    }

    h1{
      margin: 0 0 10px;
      font-size: clamp(28px, 4vw, 44px);
      letter-spacing: .2px;
      text-align: center;
    }

    .sub{
      margin: 0 0 18px;
      text-align: center;
      opacity: .9;
    }

    .stage{
      position: relative;
      height: 150px;
      margin-top: 14px;
      border-radius: 20px;
      background: linear-gradient(135deg, rgba(255,255,255,.55), rgba(255, 224, 238, .55));
      border: 1px solid rgba(255, 61, 147, .15);
      box-shadow: var(--shadow-2);
      overflow: hidden;
    }

    .stage::before{
      content:"";
      position:absolute;
      inset:-80px;
      background:
        radial-gradient(circle at 20% 30%, rgba(255, 61, 147, .18), transparent 55%),
        radial-gradient(circle at 75% 70%, rgba(255, 61, 147, .12), transparent 55%);
      pointer-events:none;
    }

    .buttons{
      position: relative;
      width: 100%;
      height: 100%;
    }

    button{
      border: 0;
      border-radius: 999px;
      padding: 14px 24px;
      font-size: 18px;
      font-weight: 800;
      cursor: pointer;
      user-select: none;
      transition: transform .12s ease, filter .12s ease;
      box-shadow: 0 14px 30px rgba(232, 29, 123, .25);
    }
    button:hover{ filter: brightness(1.03); }
    button:active{ transform: scale(.98); }

    /* JA */
    #yesBtn{
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-120%, -50%);
      color: #fff;
      background: linear-gradient(135deg, var(--pink-500), var(--pink-700));
    }

    /* NEI (rosa, men “feil” rosa 😈) */
    #noBtn{
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(20%, -50%);
      color: #fff;
      background: linear-gradient(135deg, var(--pink-300), var(--pink-600));
    }

    /* Modal */
    .overlay{
      position: fixed;
      inset: 0;
      background: rgba(58, 11, 34, .55);
      display: none;
      place-items: center;
      padding: 18px;
      z-index: 50;
    }
    .overlay.show{ display: grid; }

    .modal{
      width: min(540px, 94vw);
      background: rgba(255, 240, 246, .92);
      border: 1px solid rgba(255, 61, 147, .18);
      border-radius: 26px;
      overflow: hidden;
      box-shadow: var(--shadow);
      transform: translateY(8px);
      animation: pop .18s ease-out forwards;
    }

    @keyframes pop{ to { transform: translateY(0); } }

    .modal img{
      width: 100%;
      height: 300px;
      object-fit: cover;
      display: block;
      filter: saturate(1.05) contrast(1.02);
    }

    .modal .content{
      padding: 18px 18px 22px;
      text-align: center;
    }

    .modal h2{
      margin: 8px 0 10px;
      font-size: 28px;
    }

    .modal p{
      margin: 0 0 16px;
      line-height: 1.45;
      opacity: .95;
    }

    .modal .closeRow{
      display: flex;
      justify-content: center;
      gap: 10px;
    }

    #closeBtn{
      background: linear-gradient(135deg, rgba(255,255,255,.9), rgba(255, 224, 238, .9));
      color: var(--ink);
      border: 2px solid rgba(255, 61, 147, .18);
      box-shadow: none;
      font-weight: 900;
    }

    /* Litt ekstra “cute” */
    .badge{
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 8px 12px;
      border-radius: 999px;
      background: rgba(255, 224, 238, .7);
      border: 1px solid rgba(255, 61, 147, .18);
      box-shadow: 0 10px 22px rgba(232, 29, 123, .10);
      font-weight: 800;
      margin: 0 auto 12px;
    }

    .rowCenter{ display:flex; justify-content:center; }
  </style>
</head>

<body>
  <div class="card">
    <div class="sparkles"></div>

    <div class="rowCenter">
      <div class="badge">💗 Rosa modus: ON</div>
    </div>

    <h1>Vil du være min Valentine? 💘</h1>
    <p class="sub">Velg smart. Jeg ser alt. 😇</p>

    <div class="stage" id="stage">
      <div class="buttons">
        <button id="yesBtn">JA</button>
        <button id="noBtn">Nei</button>
      </div>
    </div>
  </div>

  <div class="overlay" id="overlay" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true" aria-label="Valentine svar">
      <!-- Bytt dette til et eget bilde hvis du vil -->
      <img id="resultImg"
        src="https://images.unsplash.com/photo-1518199266791-5375a83190b7?auto=format&fit=crop&w=1400&q=80"
        alt="Valentine bilde" />
      <div class="content">
        <h2>Yesss! 🥹💞</h2>
        <p id="resultText">Ok, da er det offisielt: du er min Valentine. Jeg elsker deg. 🌹</p>
        <div class="closeRow">
          <button id="closeBtn">Lukk</button>
        </div>
      </div>
    </div>
  </div>

  <script>
    const stage = document.getElementById('stage');
    const noBtn = document.getElementById('noBtn');
    const yesBtn = document.getElementById('yesBtn');
    const overlay = document.getElementById('overlay');
    const closeBtn = document.getElementById('closeBtn');

    function moveNoButton() {
      const s = stage.getBoundingClientRect();
      const b = noBtn.getBoundingClientRect();

      const padding = 10;
      const maxX = s.width - b.width - padding;
      const maxY = s.height - b.height - padding;

      const x = Math.random() * maxX + padding;
      const y = Math.random() * maxY + padding;

      noBtn.style.left = `${x}px`;
      noBtn.style.top = `${y}px`;
      noBtn.style.transform = `translate(0,0)`;
    }

    noBtn.addEventListener('mouseenter', moveNoButton);

    // mobil: også rømme på touch
    noBtn.addEventListener('touchstart', (e) => {
      e.preventDefault();
      moveNoButton();
    }, { passive: false });

    yesBtn.addEventListener('click', () => {
      overlay.classList.add('show');
      overlay.setAttribute('aria-hidden', 'false');
      confettiHearts();
    });

    closeBtn.addEventListener('click', () => {
      overlay.classList.remove('show');
      overlay.setAttribute('aria-hidden', 'true');
    });

    overlay.addEventListener('click', (e) => {
      if (e.target === overlay) closeBtn.click();
    });

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
