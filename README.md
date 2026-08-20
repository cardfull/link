<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
  <meta name="theme-color" content="#050b16" />
  <title>Central de Downloads</title>
  <style>
    :root {
      color-scheme: dark;
      --bg: #050b16;
      --bg-2: #081426;
      --panel: rgba(12, 28, 49, 0.94);
      --panel-2: rgba(14, 34, 57, 0.94);
      --line: #274560;
      --line-strong: #47789f;
      --text: #f4f7fb;
      --muted: #9bb3cb;
      --blue: #2f7df6;
      --violet: #6f46f6;
      --cyan: #2ed5c4;
      --green: #4de0a7;
      --orange: #ff8a3d;
      --focus: #7b61ff;
      --radius: 18px;
      --shadow: 0 18px 45px rgba(0, 0, 0, .28);
    }

    * { box-sizing: border-box; }

    html { scroll-behavior: smooth; }

    body {
      margin: 0;
      min-height: 100vh;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Arial, sans-serif;
      color: var(--text);
      background:
        radial-gradient(circle at 15% 0%, rgba(111, 70, 246, .16), transparent 28rem),
        radial-gradient(circle at 90% 10%, rgba(47, 125, 246, .14), transparent 30rem),
        linear-gradient(160deg, #030811 0%, var(--bg) 52%, #061326 100%);
      -webkit-tap-highlight-color: transparent;
      overscroll-behavior-y: none;
    }

    button, a { font: inherit; }

    button {
      border: 0;
      color: inherit;
    }

    .shell {
      width: min(1180px, calc(100% - 32px));
      margin: 0 auto;
      padding: 30px 0 42px;
    }

    .hero {
      display: flex;
      align-items: center;
      gap: 20px;
      padding: 24px 6px 28px;
    }

    .hero-icon {
      width: 82px;
      height: 82px;
      flex: 0 0 82px;
      border-radius: 22px;
      display: grid;
      place-items: center;
      color: #9d7dff;
      background: linear-gradient(145deg, rgba(18, 35, 58, .98), rgba(6, 16, 31, .98));
      border: 1px solid #334d68;
      box-shadow: inset 0 0 30px rgba(111, 70, 246, .08), var(--shadow);
    }

    .hero-icon svg { width: 48px; height: 48px; }

    .hero h1 {
      margin: 0;
      font-size: clamp(2rem, 4vw, 3.2rem);
      line-height: 1.05;
      letter-spacing: -.035em;
    }

    .hero p {
      margin: 10px 0 0;
      color: var(--muted);
      font-size: clamp(1rem, 2vw, 1.18rem);
    }

    .hint {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      margin-top: 14px;
      color: #7894ae;
      font-size: .9rem;
    }

    .hint span {
      display: inline-flex;
      align-items: center;
      min-height: 30px;
      padding: 5px 9px;
      border: 1px solid #203d57;
      border-radius: 9px;
      background: rgba(12, 28, 49, .62);
    }

    .servers {
      display: grid;
      gap: 14px;
    }

    .server {
      overflow: hidden;
      border: 1px solid var(--line);
      border-radius: var(--radius);
      background: rgba(5, 16, 30, .64);
      box-shadow: 0 12px 38px rgba(0,0,0,.16);
    }

    .server.open {
      border-color: #3d5f7c;
      box-shadow: 0 16px 48px rgba(0,0,0,.24), inset 0 0 0 1px rgba(93, 121, 159, .08);
    }

    .server-toggle {
      width: 100%;
      min-height: 82px;
      padding: 14px 20px;
      display: flex;
      align-items: center;
      gap: 16px;
      text-align: left;
      cursor: pointer;
      background: linear-gradient(90deg, rgba(15, 35, 58, .98), rgba(10, 25, 44, .96));
      transition: background .18s ease, transform .12s ease, box-shadow .18s ease;
    }

    .server.open .server-toggle {
      background: linear-gradient(105deg, rgba(19, 63, 142, .90), rgba(50, 28, 126, .93));
    }

    .server-toggle:hover {
      background: linear-gradient(90deg, rgba(21, 47, 77, .98), rgba(12, 31, 52, .98));
    }

    .server.open .server-toggle:hover {
      background: linear-gradient(105deg, rgba(24, 73, 158, .95), rgba(61, 34, 145, .96));
    }

    .server-number {
      width: 54px;
      height: 54px;
      flex: 0 0 54px;
      display: grid;
      place-items: center;
      border-radius: 14px;
      font-size: 1.55rem;
      font-weight: 800;
      background: linear-gradient(145deg, rgba(44, 112, 229, .55), rgba(73, 58, 209, .55));
      border: 1px solid rgba(110, 151, 255, .7);
      box-shadow: inset 0 0 20px rgba(42, 109, 255, .16);
    }

    .server-title {
      min-width: 0;
      flex: 1;
      font-size: clamp(1.15rem, 2.3vw, 1.55rem);
      font-weight: 800;
      letter-spacing: -.015em;
    }

    .chevron {
      width: 19px;
      height: 19px;
      flex: 0 0 19px;
      border-right: 3px solid #9eb2cf;
      border-bottom: 3px solid #9eb2cf;
      transform: rotate(45deg);
      transition: transform .2s ease;
      margin-right: 5px;
    }

    .server.open .chevron { transform: rotate(225deg); }

    .server-content {
      display: none;
      padding: 16px;
      background: linear-gradient(180deg, rgba(6, 16, 29, .97), rgba(7, 18, 33, .97));
      border-top: 1px solid rgba(74, 111, 143, .44);
    }

    .server.open .server-content { display: block; }

    .apps-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 16px;
    }

    .app-card {
      min-width: 0;
      padding: 18px;
      display: grid;
      grid-template-columns: 84px minmax(0, 1fr);
      gap: 16px;
      align-items: center;
      border: 1px solid #294b67;
      border-radius: 16px;
      background:
        radial-gradient(circle at 100% 0%, rgba(49, 116, 255, .08), transparent 45%),
        linear-gradient(145deg, rgba(14, 33, 55, .98), rgba(8, 22, 39, .98));
      box-shadow: inset 0 1px 0 rgba(255,255,255,.025);
    }

    .app-icon {
      width: 84px;
      aspect-ratio: 1;
      display: grid;
      place-items: center;
      border-radius: 16px;
      font-weight: 900;
      line-height: 1;
      text-align: center;
      overflow: hidden;
      border: 1px solid rgba(255,255,255,.2);
      box-shadow: 0 12px 28px rgba(0,0,0,.24);
      user-select: none;
    }

    .app-icon small {
      display: block;
      margin-top: 4px;
      font-size: .52rem;
      font-weight: 800;
      letter-spacing: .04em;
    }

    .pink { background: linear-gradient(145deg, #9d2cef, #ff6476); font-size: 1.2rem; }
    .blue { background: linear-gradient(145deg, #093c8e, #0c71d7); font-size: 1.25rem; }
    .black { background: linear-gradient(145deg, #171717, #050505); font-size: 1.2rem; }
    .purple { background: linear-gradient(145deg, #2b0e4d, #8a25da); font-size: 1.15rem; }
    .indigo { background: linear-gradient(145deg, #1d245e, #5e48d8); font-size: 1.15rem; }
    .teal { background: linear-gradient(145deg, #0a5361, #10a8a1); font-size: 1.15rem; }
    .orange { background: linear-gradient(145deg, #743514, #e3742d); font-size: 1.15rem; }
    .slate { background: linear-gradient(145deg, #1d3348, #496780); font-size: 1.15rem; }

    .app-info { min-width: 0; }

    .app-title {
      margin: 0;
      font-size: clamp(1.05rem, 2vw, 1.3rem);
      line-height: 1.25;
      letter-spacing: -.01em;
    }

    .app-code {
      color: #adc1da;
      font-weight: 600;
      margin-right: 5px;
    }

    .app-desc {
      margin: 8px 0 12px;
      color: #c1d0df;
      line-height: 1.5;
      font-size: .96rem;
    }

    .meta-row {
      display: flex;
      align-items: center;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 13px;
    }

    .platform,
    .downloader-copy {
      min-height: 38px;
      display: inline-flex;
      align-items: center;
      gap: 7px;
      border-radius: 9px;
      border: 1px solid #2f516d;
      background: rgba(9, 25, 43, .8);
      color: #c3d2e3;
      padding: 7px 10px;
      font-size: .92rem;
    }

    .downloader-copy {
      cursor: pointer;
      transition: border-color .15s ease, background .15s ease, transform .1s ease;
    }

    .downloader-copy strong {
      color: var(--green);
      font-size: 1rem;
      letter-spacing: .025em;
    }

    .downloader-copy:hover { border-color: #4f7da2; background: rgba(17, 39, 64, .9); }

    .download-button {
      width: 100%;
      min-height: 56px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      padding: 13px 18px;
      border-radius: 12px;
      text-decoration: none;
      font-weight: 800;
      color: #fff;
      cursor: pointer;
      background: linear-gradient(100deg, var(--violet), var(--blue));
      border: 1px solid rgba(146, 148, 255, .68);
      box-shadow: 0 10px 24px rgba(47, 87, 246, .18), inset 0 1px 0 rgba(255,255,255,.18);
      transition: transform .12s ease, filter .15s ease, box-shadow .15s ease;
      user-select: none;
    }

    .download-button:hover {
      filter: brightness(1.08);
      transform: translateY(-1px);
    }

    .download-button svg { width: 22px; height: 22px; flex: 0 0 22px; }

    .download-state {
      display: none;
      margin-top: 10px;
      padding: 10px 12px;
      border-radius: 10px;
      background: rgba(5, 16, 30, .72);
      border: 1px solid #294c68;
    }

    .app-card.preparing .download-state { display: block; }
    .app-card.preparing .download-button { opacity: .68; pointer-events: none; }

    .download-status {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      color: #b5cae1;
      font-size: .86rem;
      margin-bottom: 8px;
    }

    .progress-track {
      height: 8px;
      overflow: hidden;
      border-radius: 999px;
      background: #1b3650;
    }

    .progress-bar {
      width: 38%;
      height: 100%;
      border-radius: inherit;
      background: linear-gradient(90deg, var(--cyan), #8d68ff);
      animation: prepare 1s ease-in-out infinite alternate;
    }

    @keyframes prepare {
      from { transform: translateX(-65%); }
      to { transform: translateX(185%); }
    }

    .toast {
      position: fixed;
      left: 50%;
      bottom: max(18px, env(safe-area-inset-bottom));
      transform: translate(-50%, 18px);
      z-index: 100;
      min-width: min(340px, calc(100% - 28px));
      max-width: calc(100% - 28px);
      padding: 12px 16px;
      border: 1px solid #3a6486;
      border-radius: 12px;
      background: rgba(9, 24, 41, .97);
      box-shadow: 0 14px 40px rgba(0,0,0,.38);
      color: #e9f3ff;
      text-align: center;
      opacity: 0;
      pointer-events: none;
      transition: opacity .2s ease, transform .2s ease;
    }

    .toast.show { opacity: 1; transform: translate(-50%, 0); }

    .footer {
      margin-top: 18px;
      padding: 16px 18px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 9px;
      color: #7f9ab4;
      font-size: .92rem;
      border: 1px solid #213e58;
      border-radius: 14px;
      background: rgba(10, 24, 41, .68);
    }

    .footer svg { width: 20px; height: 20px; color: var(--green); }

    /* TV Box / teclado / acessibilidade: foco grande e muito visível */
    .focusable:focus { outline: none; }

    .focusable:focus-visible,
    .remote-focus {
      position: relative;
      z-index: 2;
      outline: 4px solid rgba(126, 96, 255, .94) !important;
      outline-offset: 4px;
      box-shadow: 0 0 0 8px rgba(72, 131, 255, .18), 0 0 34px rgba(115, 78, 255, .55) !important;
    }

    @media (max-width: 760px) {
      .shell {
        width: min(100% - 20px, 680px);
        padding: 14px 0 28px;
      }

      .hero {
        align-items: flex-start;
        gap: 14px;
        padding: 18px 4px 22px;
      }

      .hero-icon {
        width: 62px;
        height: 62px;
        flex-basis: 62px;
        border-radius: 17px;
      }

      .hero-icon svg { width: 36px; height: 36px; }

      .hint { display: none; }

      .server-toggle {
        min-height: 72px;
        padding: 10px 13px;
      }

      .server-number {
        width: 48px;
        height: 48px;
        flex-basis: 48px;
        border-radius: 12px;
        font-size: 1.35rem;
      }

      .server-content { padding: 10px; }
      .apps-grid { grid-template-columns: 1fr; gap: 10px; }

      .app-card {
        grid-template-columns: 66px minmax(0, 1fr);
        gap: 12px;
        padding: 14px;
      }

      .app-icon { width: 66px; border-radius: 14px; }

      .app-desc {
        grid-column: 1 / -1;
        font-size: .93rem;
      }

      .download-button { min-height: 58px; font-size: 1rem; }
      .downloader-copy, .platform { min-height: 42px; }
    }

    @media (max-width: 420px) {
      .hero h1 { font-size: 1.75rem; }
      .hero p { font-size: .93rem; }
      .server-title { font-size: 1.08rem; }
      .app-title { font-size: 1rem; }
      .app-card { grid-template-columns: 58px minmax(0, 1fr); padding: 12px; }
      .app-icon { width: 58px; }
      .meta-row { grid-column: 1 / -1; margin-top: 2px; }
      .download-button, .download-state { grid-column: 1 / -1; }
    }

    @media (min-width: 1200px) {
      .shell { width: min(1280px, calc(100% - 60px)); }
      .app-card { min-height: 238px; }
    }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        scroll-behavior: auto !important;
        animation-duration: .01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: .01ms !important;
      }
    }
  </style>
</head>
<body>
  <main class="shell">
    <header class="hero">
      <div class="hero-icon" aria-hidden="true">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
          <path d="M7 18a5 5 0 0 1-.6-9.96A6.5 6.5 0 0 1 18.8 9.5 4.25 4.25 0 0 1 18 18h-2"/>
          <path d="M12 11v9m0 0-3-3m3 3 3-3"/>
        </svg>
      </div>
      <div>
        <h1>Central de Downloads</h1>
        <p>Escolha o servidor e baixe seu aplicativo.</p>
        <div class="hint" aria-hidden="true">
          <span>📱 Toque no celular</span>
          <span>⌨️ ↑ ↓ no controle/teclado</span>
          <span>OK / Enter para selecionar</span>
        </div>
      </div>
    </header>

    <section class="servers" id="servers" aria-label="Servidores e aplicativos">

      <!-- 1 - CLASSIC SERVER -->
      <article class="server" data-server="1">
        <button class="server-toggle focusable" type="button" aria-expanded="false" aria-controls="server-1-content">
          <span class="server-number">1</span>
          <span class="server-title">Classic Server</span>
          <span class="chevron" aria-hidden="true"></span>
        </button>
        <div class="server-content" id="server-1-content">
          <div class="apps-grid">

            <article class="app-card">
              <div class="app-icon pink" aria-hidden="true">IPTV<small>SMARTERS</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">1-1</span> Smarters <span style="color:#9fb2cc;font-weight:500">(Painel Rosa)</span></h2>
                <p class="app-desc">Este aplicativo só precisa colocar seu login e senha, sem necessidade do cliente por DNS.</p>
                <div class="meta-row">
                  <span class="platform">Android</span>
                  <button class="downloader-copy focusable" type="button" data-copy="972242" aria-label="Copiar código Downloader 972242">
                    Downloader: <strong>972242</strong>
                  </button>
                </div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=1YvQBrRm63RTrrwuXmj3muBQOui6CpFpz" data-download>
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>
                  Baixar aplicativo
                </a>
                <div class="download-state" aria-live="polite">
                  <div class="download-status"><span>Preparando download...</span><span>aguarde</span></div>
                  <div class="progress-track"><div class="progress-bar"></div></div>
                </div>
              </div>
            </article>

            <article class="app-card">
              <div class="app-icon blue" aria-hidden="true">XC<small>PAINEL AZUL</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">1-2</span> Ottrun XC <span style="color:#9fb2cc;font-weight:500">(Painel Azul)</span></h2>
                <div class="meta-row">
                  <span class="platform">Android</span>
                  <button class="downloader-copy focusable" type="button" data-copy="886987" aria-label="Copiar código Downloader 886987">Downloader: <strong>886987</strong></button>
                </div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=1zwnF10ZolECr-9akWZBM4x7w_jadcD9X" data-download>
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>
                  Baixar aplicativo
                </a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>

            <article class="app-card">
              <div class="app-icon black" aria-hidden="true">CM+<small>CINE MAGIC</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">1-3</span> Cine Magic Plus</h2>
                <div class="meta-row">
                  <span class="platform">Android</span>
                  <button class="downloader-copy focusable" type="button" data-copy="8142851" aria-label="Copiar código Downloader 8142851">Downloader: <strong>8142851</strong></button>
                </div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=14r3xQZRu7jD1LF6VSfhxueHQI311o5rP" data-download>
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>
                  Baixar aplicativo
                </a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>

            <article class="app-card">
              <div class="app-icon purple" aria-hidden="true">TV+<small>UNIVERSAL</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">1-4</span> TV Universal</h2>
                <div class="meta-row">
                  <span class="platform">Android</span>
                  <button class="downloader-copy focusable" type="button" data-copy="2041040" aria-label="Copiar código Downloader 2041040">Downloader: <strong>2041040</strong></button>
                </div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=16O9jl7zqdsJO3ZUtejuK6CvJRaqzFxc5" data-download>
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>
                  Baixar aplicativo
                </a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>

          </div>
        </div>
      </article>

      <!-- 2 - P2SERVER -->
      <article class="server" data-server="2">
        <button class="server-toggle focusable" type="button" aria-expanded="false" aria-controls="server-2-content">
          <span class="server-number">2</span><span class="server-title">P2Server Server</span><span class="chevron" aria-hidden="true"></span>
        </button>
        <div class="server-content" id="server-2-content">
          <div class="apps-grid">
            <article class="app-card">
              <div class="app-icon indigo" aria-hidden="true">P2<small>PRO</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">2-1</span> P2 Pro</h2>
                <div class="meta-row"><span class="platform">Android</span><button class="downloader-copy focusable" type="button" data-copy="7333254">Downloader: <strong>7333254</strong></button></div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=1LY9Q7gcifSrZQN6t4_PpbxgM6mrFjaGD" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar aplicativo</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>

            <article class="app-card">
              <div class="app-icon blue" aria-hidden="true">P2<small>OFICIAL</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">2-2</span> P2 Oficial</h2>
                <div class="meta-row"><span class="platform">Android</span><button class="downloader-copy focusable" type="button" data-copy="8538401">Downloader: <strong>8538401</strong></button></div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=1Zb4LJjFhQqh9h8nVVXkio0-fdA6KKHxM" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar aplicativo</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>

            <article class="app-card">
              <div class="app-icon slate" aria-hidden="true">XC<small>P2SERVER</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">2-3</span> XCIPTV P2Server</h2>
                <div class="meta-row"><span class="platform">Android</span><button class="downloader-copy focusable" type="button" data-copy="9238100">Downloader: <strong>9238100</strong></button></div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=1lyDCtp42bk2uaoOmCiRKJWZJUNZqKJIo" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar aplicativo</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>
          </div>
        </div>
      </article>

      <!-- 3 - UNIPLAY -->
      <article class="server" data-server="3">
        <button class="server-toggle focusable" type="button" aria-expanded="false" aria-controls="server-3-content">
          <span class="server-number">3</span><span class="server-title">UniPlay</span><span class="chevron" aria-hidden="true"></span>
        </button>
        <div class="server-content" id="server-3-content">
          <div class="apps-grid">
            <article class="app-card">
              <div class="app-icon purple" aria-hidden="true">UNI<small>IPTV</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">3-1</span> IPTV UniPlay</h2>
                <div class="meta-row"><span class="platform">Android</span><button class="downloader-copy focusable" type="button" data-copy="1603568">Downloader: <strong>1603568</strong></button></div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=10y86to_kfZmd-kAmyEjdfR7B7dmuVD7H" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar aplicativo</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>

            <article class="app-card">
              <div class="app-icon indigo" aria-hidden="true">UNI<small>P2P</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">3-2</span> P2P UniPlay</h2>
                <div class="meta-row"><span class="platform">Android</span><button class="downloader-copy focusable" type="button" data-copy="4211099">Downloader: <strong>4211099</strong></button></div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=15dFn2Qjjuvro8p5NcSfR0Uc7al5VWhNW" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar aplicativo</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>
          </div>
        </div>
      </article>

      <!-- 4 - CLUB MEXICANO -->
      <article class="server" data-server="4">
        <button class="server-toggle focusable" type="button" aria-expanded="false" aria-controls="server-4-content">
          <span class="server-number">4</span><span class="server-title">Club Mexicano</span><span class="chevron" aria-hidden="true"></span>
        </button>
        <div class="server-content" id="server-4-content">
          <div class="apps-grid">
            <article class="app-card">
              <div class="app-icon teal" aria-hidden="true">CP<small>LITE</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">4-1</span> CPlayer Lite</h2>
                <div class="meta-row"><span class="platform">Android</span><button class="downloader-copy focusable" type="button" data-copy="6199512">Downloader: <strong>6199512</strong></button></div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=1gZjk7gT2SbjAj_O8Tk1FWKwKVgzzY4uN" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar aplicativo</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>
          </div>
        </div>
      </article>

      <!-- 5 - APPS DIVERSOS -->
      <article class="server" data-server="5">
        <button class="server-toggle focusable" type="button" aria-expanded="false" aria-controls="server-5-content">
          <span class="server-number">5</span><span class="server-title">Apps Diversos</span><span class="chevron" aria-hidden="true"></span>
        </button>
        <div class="server-content" id="server-5-content">
          <div class="apps-grid">
            <article class="app-card">
              <div class="app-icon blue" aria-hidden="true">SP<small>WINDOWS</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">5-1</span> Smarters Pro para Windows</h2>
                <div class="meta-row"><span class="platform">Windows</span></div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=17Nan4ZeCMWw31Imbn7X__Eg1qIEJszCi" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar para Windows</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>

            <article class="app-card">
              <div class="app-icon pink" aria-hidden="true">SP<small>ANDROID</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">5-2</span> Smarters Pro para Android</h2>
                <div class="meta-row"><span class="platform">Android</span><button class="downloader-copy focusable" type="button" data-copy="8943618">Downloader: <strong>8943618</strong></button></div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=1Midxxpti1y1m4LrKnuV7bSKjqozBPX3Q" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar aplicativo</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>

            <article class="app-card">
              <div class="app-icon slate" aria-hidden="true">DNS<small>CHANGER</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">5-3</span> DNS Changer</h2>
                <div class="meta-row"><span class="platform">Android</span><button class="downloader-copy focusable" type="button" data-copy="7743711">Downloader: <strong>7743711</strong></button></div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=138qm-a6WoalvrMLff3GhYV5BlESVHaYn" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar aplicativo</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>

            <article class="app-card">
              <div class="app-icon orange" aria-hidden="true">VPN<small>GRÁTIS</small></div>
              <div class="app-info">
                <h2 class="app-title"><span class="app-code">5-4</span> VPN Grátis</h2>
                <div class="meta-row"><span class="platform">Android</span><button class="downloader-copy focusable" type="button" data-copy="1955500">Downloader: <strong>1955500</strong></button></div>
                <a class="download-button focusable" href="https://drive.usercontent.google.com/download?id=1NCInAchyvYLdJ8W4gYRhhCY53B0dXxcS&amp;export=download&amp;authuser=0" data-download><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3v12m0 0 4-4m-4 4-4-4M5 21h14"/></svg>Baixar aplicativo</a>
                <div class="download-state" aria-live="polite"><div class="download-status"><span>Preparando download...</span><span>aguarde</span></div><div class="progress-track"><div class="progress-bar"></div></div></div>
              </div>
            </article>
          </div>
        </div>
      </article>
    </section>

    <footer class="footer">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10Z"/><path d="m9 12 2 2 4-4"/></svg>
      Central de Downloads • compatível com celular, computador e TV Box
    </footer>
  </main>

  <div class="toast" id="toast" role="status" aria-live="polite"></div>

  <script>
    (() => {
      const servers = [...document.querySelectorAll('.server')];
      const toast = document.getElementById('toast');
      let toastTimer;

      function visibleFocusable() {
        return [...document.querySelectorAll('.focusable')].filter((el) => {
          if (el.disabled) return false;
          if (el.offsetParent === null) return false;
          return true;
        });
      }

      function showToast(message) {
        clearTimeout(toastTimer);
        toast.textContent = message;
        toast.classList.add('show');
        toastTimer = setTimeout(() => toast.classList.remove('show'), 1800);
      }

      function closeServer(server) {
        server.classList.remove('open');
        const button = server.querySelector('.server-toggle');
        button.setAttribute('aria-expanded', 'false');
      }

      function openServer(server, focusFirstInside = false) {
        servers.forEach((item) => {
          if (item !== server) closeServer(item);
        });
        server.classList.add('open');
        const button = server.querySelector('.server-toggle');
        button.setAttribute('aria-expanded', 'true');

        if (focusFirstInside) {
          requestAnimationFrame(() => {
            const first = server.querySelector('.server-content .focusable');
            if (first) focusElement(first);
          });
        }
      }

      function toggleServer(server) {
        if (server.classList.contains('open')) {
          closeServer(server);
          localStorage.removeItem('centralDownloadsOpenServer');
        } else {
          openServer(server);
        }
      }

      function focusElement(el) {
        if (!el) return;
        document.querySelectorAll('.remote-focus').forEach((item) => item.classList.remove('remote-focus'));
        el.classList.add('remote-focus');
        el.focus({ preventScroll: true });
        el.scrollIntoView({ behavior: 'smooth', block: 'center', inline: 'nearest' });
      }

      // Accordion: abre um servidor e fecha todos os outros.
      servers.forEach((server) => {
        const toggle = server.querySelector('.server-toggle');
        toggle.addEventListener('click', () => toggleServer(server));
      });

      // Copiar código Downloader com toque, mouse ou OK/Enter.
      document.querySelectorAll('[data-copy]').forEach((button) => {
        button.addEventListener('click', async () => {
          const code = button.dataset.copy;
          try {
            await navigator.clipboard.writeText(code);
            showToast(`Código ${code} copiado.`);
          } catch {
            const input = document.createElement('textarea');
            input.value = code;
            input.style.position = 'fixed';
            input.style.opacity = '0';
            document.body.appendChild(input);
            input.select();
            document.execCommand('copy');
            input.remove();
            showToast(`Código ${code} copiado.`);
          }
        });
      });

      // Barra de preparação honesta: não simula percentual/MB do Google Drive.
      document.querySelectorAll('[data-download]').forEach((link) => {
        link.addEventListener('click', (event) => {
          if (event.ctrlKey || event.metaKey || event.shiftKey || event.altKey) return;
          event.preventDefault();
          const card = link.closest('.app-card');
          const url = link.href;
          card.classList.add('preparing');
          showToast('Preparando o download...');
          setTimeout(() => {
            window.location.href = url;
          }, 850);
        });
      });

      // Navegação para controles de TV Box e teclado.
      document.addEventListener('keydown', (event) => {
        const key = event.key;
        const active = document.activeElement;
        const focusables = visibleFocusable();
        let index = focusables.indexOf(active);

        if (['ArrowDown', 'ArrowUp'].includes(key)) {
          event.preventDefault();
          if (!focusables.length) return;
          if (index < 0) index = 0;
          else index = key === 'ArrowDown'
            ? (index + 1) % focusables.length
            : (index - 1 + focusables.length) % focusables.length;
          focusElement(focusables[index]);
          return;
        }

        if (key === 'ArrowRight') {
          const toggle = active.closest?.('.server-toggle');
          if (toggle) {
            event.preventDefault();
            const server = toggle.closest('.server');
            if (!server.classList.contains('open')) openServer(server, true);
            else {
              const first = server.querySelector('.server-content .focusable');
              if (first) focusElement(first);
            }
          }
          return;
        }

        if (key === 'ArrowLeft') {
          const server = active.closest?.('.server');
          if (server && server.classList.contains('open')) {
            const toggle = server.querySelector('.server-toggle');
            if (active !== toggle) {
              event.preventDefault();
              focusElement(toggle);
            } else {
              event.preventDefault();
              closeServer(server);
              localStorage.removeItem('centralDownloadsOpenServer');
            }
          }
          return;
        }

        // Alguns controles enviam Backspace como botão voltar.
        if (key === 'Escape' || key === 'Backspace' || key === 'BrowserBack') {
          const open = document.querySelector('.server.open');
          if (open) {
            event.preventDefault();
            closeServer(open);
            localStorage.removeItem('centralDownloadsOpenServer');
            focusElement(open.querySelector('.server-toggle'));
          }
        }
      });

      document.addEventListener('focusin', (event) => {
        if (event.target.classList?.contains('focusable')) {
          document.querySelectorAll('.remote-focus').forEach((item) => {
            if (item !== event.target) item.classList.remove('remote-focus');
          });
          event.target.classList.add('remote-focus');
        }
      });

      document.addEventListener('pointerdown', () => {
        document.querySelectorAll('.remote-focus').forEach((item) => item.classList.remove('remote-focus'));
      }, { passive: true });

      // A página sempre inicia com todos os servidores fechados.
    })();
  </script>
</body>
</html>
