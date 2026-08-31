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

    .app-icon img { width: 100%; height: 100%; object-fit: cover; display: block; }

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

    /* TV Box / teclado / acessibilidade: foco grande e muito visível.
       Regras separadas para funcionar também em Chromes/WebViews antigos. */
    .focusable:focus {
      position: relative;
      z-index: 2;
      outline: 4px solid rgba(126, 96, 255, .94) !important;
      outline-offset: 4px;
      box-shadow: 0 0 0 8px rgba(72, 131, 255, .18), 0 0 34px rgba(115, 78, 255, .55) !important;
    }

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
        <button class="server-toggle focusable" type="button" onclick="return centralToggleServer(this);" aria-expanded="false" aria-controls="server-1-content">
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

            <article class="app-card">
              <div class="app-icon black" aria-hidden="true"><img src="data:image/jpeg;base64,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" alt=""></div>
              <div class="app-info">
                <div style="color:#4de0a7;font-size:.78rem;font-weight:800;letter-spacing:.025em;margin-bottom:7px;">APLICATIVO OFICIAL</div>
                <h2 class="app-title"><span class="app-code">1-5</span> New Painel</h2>
                <p class="app-desc">Aplicativo IPTV mais moderno do mercado.</p>
                <div class="meta-row">
                  <span class="platform">Android</span>
                  <button class="downloader-copy focusable" type="button" data-copy="2077595" aria-label="Copiar código Downloader 2077595">
                    Downloader: <strong>2077595</strong>
                  </button>
                  <span class="platform">Versão 0.9.120</span>
                  <span class="platform">2.1 MB</span>
                </div>
                <a class="download-button focusable" href="https://drive.google.com/uc?export=download&id=1Q6u4MVhG2_Yu43K_n62xp5kEMSAsOWJw" data-download>
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
        <button class="server-toggle focusable" type="button" onclick="return centralToggleServer(this);" aria-expanded="false" aria-controls="server-2-content">
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
        <button class="server-toggle focusable" type="button" onclick="return centralToggleServer(this);" aria-expanded="false" aria-controls="server-3-content">
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
        <button class="server-toggle focusable" type="button" onclick="return centralToggleServer(this);" aria-expanded="false" aria-controls="server-4-content">
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
        <button class="server-toggle focusable" type="button" onclick="return centralToggleServer(this);" aria-expanded="false" aria-controls="server-5-content">
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
    /*
      Compatibilidade TV Box:
      - JavaScript ES5 (sem optional chaining, async/await, arrow function, spread etc.)
      - suporte a keyCode de controles Android/TV (DPAD 19/20/21/22/23 e Enter 66)
      - clique normal continua funcionando em mouse e touch
    */

    var centralServers = [];
    var centralToast = null;
    var centralToastTimer = null;

    function centralHasClass(el, name) {
      if (!el) return false;
      if (el.classList) return el.classList.contains(name);
      return new RegExp('(^|\\s)' + name + '(\\s|$)').test(el.className || '');
    }

    function centralAddClass(el, name) {
      if (!el || centralHasClass(el, name)) return;
      if (el.classList) el.classList.add(name);
      else el.className = (el.className ? el.className + ' ' : '') + name;
    }

    function centralRemoveClass(el, name) {
      if (!el) return;
      if (el.classList) el.classList.remove(name);
      else el.className = (el.className || '').replace(new RegExp('(^|\\s)' + name + '(?=\\s|$)', 'g'), ' ').replace(/^\\s+|\\s+$/g, '');
    }

    function centralClosestByClass(el, className) {
      while (el && el !== document) {
        if (centralHasClass(el, className)) return el;
        el = el.parentNode;
      }
      return null;
    }

    function centralAddEvent(el, type, handler) {
      if (!el) return;
      if (el.addEventListener) el.addEventListener(type, handler, false);
      else if (el.attachEvent) el.attachEvent('on' + type, handler);
    }

    function centralShowToast(message) {
      if (!centralToast) return;
      if (centralToastTimer) window.clearTimeout(centralToastTimer);
      centralToast.innerHTML = message;
      centralAddClass(centralToast, 'show');
      centralToastTimer = window.setTimeout(function () {
        centralRemoveClass(centralToast, 'show');
      }, 1800);
    }

    function centralCloseServer(server) {
      if (!server) return;
      centralRemoveClass(server, 'open');
      var button = server.querySelector ? server.querySelector('.server-toggle') : null;
      if (button) button.setAttribute('aria-expanded', 'false');
    }

    function centralOpenServer(server, focusFirstInside) {
      if (!server) return;
      var i;
      for (i = 0; i < centralServers.length; i++) {
        if (centralServers[i] !== server) centralCloseServer(centralServers[i]);
      }
      centralAddClass(server, 'open');
      var button = server.querySelector ? server.querySelector('.server-toggle') : null;
      if (button) button.setAttribute('aria-expanded', 'true');

      if (focusFirstInside) {
        window.setTimeout(function () {
          var first = server.querySelector ? server.querySelector('.server-content .focusable') : null;
          if (first) centralFocusElement(first);
        }, 30);
      }
    }

    function centralToggleServer(button) {
      var server = centralClosestByClass(button, 'server');
      if (!server) return false;
      if (centralHasClass(server, 'open')) centralCloseServer(server);
      else centralOpenServer(server, false);
      return false;
    }

    function centralIsVisible(el) {
      if (!el || el.disabled) return false;
      if (el.offsetWidth === 0 && el.offsetHeight === 0) return false;
      return true;
    }

    function centralVisibleFocusable() {
      var nodes = document.querySelectorAll ? document.querySelectorAll('.focusable') : [];
      var result = [];
      var i;
      for (i = 0; i < nodes.length; i++) {
        if (centralIsVisible(nodes[i])) result.push(nodes[i]);
      }
      return result;
    }

    function centralClearRemoteFocus(except) {
      var nodes = document.querySelectorAll ? document.querySelectorAll('.remote-focus') : [];
      var i;
      for (i = 0; i < nodes.length; i++) {
        if (nodes[i] !== except) centralRemoveClass(nodes[i], 'remote-focus');
      }
    }

    function centralFocusElement(el) {
      if (!el) return;
      centralClearRemoteFocus(el);
      centralAddClass(el, 'remote-focus');
      try { el.focus(); } catch (e) {}
      try { el.scrollIntoView(false); } catch (e2) {}
    }

    function centralCopyText(code) {
      var ok = false;
      var input = document.createElement('textarea');
      input.value = code;
      input.setAttribute('readonly', 'readonly');
      input.style.position = 'fixed';
      input.style.left = '-9999px';
      input.style.top = '0';
      document.body.appendChild(input);
      try {
        input.focus();
        input.select();
        ok = document.execCommand ? document.execCommand('copy') : false;
      } catch (e) {}
      document.body.removeChild(input);
      centralShowToast(ok ? ('Código ' + code + ' copiado.') : ('Código: ' + code));
    }

    function centralPrepareDownload(link, event) {
      if (!link) return false;
      if (event && (event.ctrlKey || event.metaKey || event.shiftKey || event.altKey)) return true;
      if (event && event.preventDefault) event.preventDefault();
      var card = centralClosestByClass(link, 'app-card');
      var url = link.getAttribute('href');
      if (card) centralAddClass(card, 'preparing');
      centralShowToast('Preparando o download...');
      window.setTimeout(function () {
        window.location.href = url;
      }, 650);
      return false;
    }

    function centralKeyInfo(event) {
      var e = event || window.event;
      var code = e.keyCode || e.which || 0;
      var key = e.key || '';
      return { e: e, code: code, key: key };
    }

    function centralPrevent(e) {
      if (!e) return;
      if (e.preventDefault) e.preventDefault();
      e.returnValue = false;
    }

    function centralHandleKeydown(event) {
      var info = centralKeyInfo(event);
      var e = info.e;
      var code = info.code;
      var key = info.key;
      var active = document.activeElement;
      var focusables;
      var index;
      var i;

      var isUp = key === 'ArrowUp' || code === 38 || code === 19;
      var isDown = key === 'ArrowDown' || code === 40 || code === 20;
      var isLeft = key === 'ArrowLeft' || code === 37 || code === 21;
      var isRight = key === 'ArrowRight' || code === 39 || code === 22;
      var isOk = key === 'Enter' || key === ' ' || key === 'Spacebar' || code === 13 || code === 23 || code === 66 || code === 32;
      var isBack = key === 'Escape' || key === 'Backspace' || key === 'BrowserBack' || code === 27 || code === 8 || code === 4;

      if (isUp || isDown) {
        centralPrevent(e);
        focusables = centralVisibleFocusable();
        if (!focusables.length) return false;
        index = -1;
        for (i = 0; i < focusables.length; i++) {
          if (focusables[i] === active) { index = i; break; }
        }
        if (index < 0) index = isDown ? -1 : 0;
        index = isDown ? (index + 1) % focusables.length : (index - 1 + focusables.length) % focusables.length;
        centralFocusElement(focusables[index]);
        return false;
      }

      if (isOk) {
        if (active && centralHasClass(active, 'focusable')) {
          centralPrevent(e);
          try { active.click(); } catch (clickError) {
            if (centralHasClass(active, 'server-toggle')) centralToggleServer(active);
          }
          return false;
        }
      }

      if (isRight) {
        var toggle = centralClosestByClass(active, 'server-toggle');
        if (toggle) {
          centralPrevent(e);
          var server = centralClosestByClass(toggle, 'server');
          if (!centralHasClass(server, 'open')) centralOpenServer(server, true);
          else {
            var first = server.querySelector ? server.querySelector('.server-content .focusable') : null;
            if (first) centralFocusElement(first);
          }
          return false;
        }
      }

      if (isLeft) {
        var currentServer = centralClosestByClass(active, 'server');
        if (currentServer && centralHasClass(currentServer, 'open')) {
          centralPrevent(e);
          var currentToggle = currentServer.querySelector ? currentServer.querySelector('.server-toggle') : null;
          if (active !== currentToggle) centralFocusElement(currentToggle);
          else centralCloseServer(currentServer);
          return false;
        }
      }

      if (isBack) {
        var openServer = document.querySelector ? document.querySelector('.server.open') : null;
        if (openServer) {
          centralPrevent(e);
          var openToggle = openServer.querySelector ? openServer.querySelector('.server-toggle') : null;
          centralCloseServer(openServer);
          if (openToggle) centralFocusElement(openToggle);
          return false;
        }
      }
      return true;
    }

    function centralInit() {
      var serverNodes = document.querySelectorAll ? document.querySelectorAll('.server') : [];
      var i;
      centralServers = [];
      for (i = 0; i < serverNodes.length; i++) {
        centralServers.push(serverNodes[i]);
        centralCloseServer(serverNodes[i]);
      }

      centralToast = document.getElementById('toast');

      var copyButtons = document.querySelectorAll ? document.querySelectorAll('[data-copy]') : [];
      for (i = 0; i < copyButtons.length; i++) {
        (function (button) {
          centralAddEvent(button, 'click', function () {
            centralCopyText(button.getAttribute('data-copy'));
          });
        })(copyButtons[i]);
      }

      var links = document.querySelectorAll ? document.querySelectorAll('[data-download]') : [];
      for (i = 0; i < links.length; i++) {
        (function (link) {
          centralAddEvent(link, 'click', function (ev) {
            return centralPrepareDownload(link, ev || window.event);
          });
        })(links[i]);
      }

      centralAddEvent(document, 'keydown', centralHandleKeydown);

      centralAddEvent(document, 'focusin', function (ev) {
        var e = ev || window.event;
        var target = e.target || e.srcElement;
        if (target && centralHasClass(target, 'focusable')) {
          centralClearRemoteFocus(target);
          centralAddClass(target, 'remote-focus');
        }
      });

      // Em aparelhos que não suportam Pointer Events, mousedown/touchstart continuam funcionando.
      centralAddEvent(document, 'mousedown', function () { centralClearRemoteFocus(null); });
      centralAddEvent(document, 'touchstart', function () { centralClearRemoteFocus(null); });

      // Inicia com tudo fechado e com foco no primeiro servidor no TV Box/teclado.
      window.setTimeout(function () {
        var firstToggle = document.querySelector ? document.querySelector('.server-toggle') : null;
        if (firstToggle && !('ontouchstart' in window)) centralFocusElement(firstToggle);
      }, 100);
    }

    if (document.readyState === 'loading') centralAddEvent(document, 'DOMContentLoaded', centralInit);
    else centralInit();

    centralAddEvent(window, 'pageshow', function () {
      var i;
      for (i = 0; i < centralServers.length; i++) centralCloseServer(centralServers[i]);
    });
  </script>
</body>
</html>
