<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EcoRecicla</title>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --verde: #2d6a4f;
      --verde-medio: #40916c;
      --verde-claro: #74c69d;
      --verde-palido: #d8f3dc;
      --amarelo: #f9c74f;
      --laranja: #f77f00;
      --azul: #4361ee;
      --vermelho: #e63946;
      --branco: #ffffff;
      --cinza: #f8f9fa;
      --texto: #1b2d27;
      --sombra: 0 8px 32px rgba(45,106,79,0.15);
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: 'Nunito', sans-serif;
      background: var(--verde-palido);
      min-height: 100vh;
      color: var(--texto);
      overflow-x: hidden;
    }

    /* ===== SPLASH SCREEN ===== */
    #splash {
      position: fixed;
      inset: 0;
      background: linear-gradient(160deg, #1b4332 0%, #2d6a4f 45%, #40916c 80%, #74c69d 100%);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 9999;
      text-align: center;
      padding: 32px 24px;
      transition: opacity 0.7s ease, transform 0.7s ease;
    }

    #splash.hiding {
      opacity: 0;
      transform: scale(1.04);
      pointer-events: none;
    }

    .splash-leaves {
      position: absolute;
      inset: 0;
      overflow: hidden;
      pointer-events: none;
    }

    .splash-leaf {
      position: absolute;
      font-size: 2.5rem;
      opacity: 0.08;
      animation: floatLeaf linear infinite;
    }

    @keyframes floatLeaf {
      0%   { transform: translateY(110vh) rotate(0deg); }
      100% { transform: translateY(-20vh) rotate(360deg); }
    }

    .splash-logo {
      font-family: 'Fredoka One', cursive;
      font-size: clamp(3rem, 10vw, 5rem);
      color: #fff;
      letter-spacing: 2px;
      line-height: 1;
      margin-bottom: 6px;
      animation: splashPop 0.8s cubic-bezier(0.34,1.56,0.64,1) both;
    }

    .splash-logo span { color: var(--amarelo); }

    .splash-tagline {
      font-size: clamp(1rem, 3vw, 1.25rem);
      color: rgba(255,255,255,0.82);
      margin-bottom: 48px;
      font-weight: 600;
      animation: splashFade 0.8s 0.2s ease both;
    }

    @keyframes splashPop {
      from { opacity: 0; transform: scale(0.6) translateY(20px); }
      to   { opacity: 1; transform: scale(1) translateY(0); }
    }

    @keyframes splashFade {
      from { opacity: 0; transform: translateY(12px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .splash-features {
      display: flex;
      gap: 16px;
      flex-wrap: wrap;
      justify-content: center;
      margin-bottom: 52px;
      animation: splashFade 0.8s 0.35s ease both;
    }

    .splash-feat {
      background: rgba(255,255,255,0.12);
      border: 1px solid rgba(255,255,255,0.22);
      border-radius: 14px;
      padding: 14px 20px;
      color: #fff;
      min-width: 130px;
      max-width: 160px;
    }

    .splash-feat .sf-icon { font-size: 2rem; margin-bottom: 6px; display: block; }
    .splash-feat .sf-label { font-size: 0.82rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.5px; opacity: 0.85; }

    .btn-start {
      padding: 18px 52px;
      background: var(--amarelo);
      color: var(--verde);
      border: none;
      border-radius: 50px;
      font-family: 'Fredoka One', cursive;
      font-size: 1.4rem;
      letter-spacing: 1px;
      cursor: pointer;
      box-shadow: 0 8px 32px rgba(249,199,79,0.45);
      transition: all 0.2s;
      animation: splashFade 0.8s 0.5s ease both;
      position: relative;
    }

    .btn-start:hover {
      transform: translateY(-4px) scale(1.04);
      box-shadow: 0 16px 48px rgba(249,199,79,0.6);
    }

    .btn-start:active { transform: scale(0.97); }

    .btn-start::after {
      content: '→';
      margin-left: 10px;
      transition: transform 0.2s;
      display: inline-block;
    }

    .btn-start:hover::after { transform: translateX(4px); }

    .splash-footer {
      position: absolute;
      bottom: 20px;
      font-size: 0.78rem;
      color: rgba(255,255,255,0.4);
      animation: splashFade 1s 0.8s ease both;
    }

    /* hide app shell while splash is shown */
    #app-shell { display: none; }

    /* ===== NAV ===== */
    nav {
      background: var(--verde);
      padding: 0 24px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 4px 20px rgba(0,0,0,0.2);
    }

    .nav-logo {
      font-family: 'Fredoka One', cursive;
      color: var(--branco);
      font-size: 1.6rem;
      padding: 14px 0;
      letter-spacing: 1px;
    }

    .nav-logo span { color: var(--amarelo); }

    .nav-links {
      display: flex;
      gap: 4px;
      flex-wrap: wrap;
    }

    .nav-btn {
      background: none;
      border: none;
      color: rgba(255,255,255,0.75);
      font-family: 'Nunito', sans-serif;
      font-size: 0.95rem;
      font-weight: 700;
      padding: 10px 16px;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.2s;
    }

    .nav-btn:hover, .nav-btn.active {
      background: rgba(255,255,255,0.15);
      color: var(--branco);
    }

    .nav-pontos {
      background: var(--amarelo);
      color: var(--verde);
      font-weight: 800;
      font-size: 0.9rem;
      padding: 8px 16px;
      border-radius: 20px;
      white-space: nowrap;
    }

    /* ===== PAGES ===== */
    .page { display: none; padding: 28px 20px; max-width: 920px; margin: 0 auto; }
    .page.active { display: block; animation: fadeIn 0.4s ease; }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(16px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ===== CARDS ===== */
    .card {
      background: var(--branco);
      border-radius: 20px;
      padding: 28px;
      box-shadow: var(--sombra);
      margin-bottom: 20px;
    }

    /* ===== HOME PAGE ===== */
    .hero {
      background: linear-gradient(135deg, var(--verde) 0%, var(--verde-medio) 60%, var(--verde-claro) 100%);
      border-radius: 24px;
      padding: 40px 32px;
      color: var(--branco);
      margin-bottom: 24px;
      position: relative;
      overflow: hidden;
    }

    .hero::after {
      content: '🌍';
      position: absolute;
      right: 30px;
      top: 50%;
      transform: translateY(-50%);
      font-size: 7rem;
      opacity: 0.25;
    }

    .hero h2 {
      font-family: 'Fredoka One', cursive;
      font-size: 2.2rem;
      margin-bottom: 8px;
    }

    .hero p { font-size: 1.1rem; opacity: 0.9; max-width: 420px; }

    .form-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
      margin-bottom: 14px;
    }

    label {
      font-weight: 700;
      font-size: 0.85rem;
      color: var(--verde);
      display: block;
      margin-bottom: 6px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    select, input[type="number"] {
      width: 100%;
      padding: 12px 16px;
      border: 2px solid #e0e0e0;
      border-radius: 12px;
      font-family: 'Nunito', sans-serif;
      font-size: 1rem;
      color: var(--texto);
      background: var(--cinza);
      transition: border 0.2s;
      appearance: none;
      outline: none;
    }

    select:focus, input:focus { border-color: var(--verde-claro); background: #fff; }

    .btn-primary {
      width: 100%;
      padding: 14px;
      background: linear-gradient(135deg, var(--verde-medio), var(--verde));
      color: var(--branco);
      border: none;
      border-radius: 14px;
      font-family: 'Fredoka One', cursive;
      font-size: 1.2rem;
      cursor: pointer;
      letter-spacing: 1px;
      transition: all 0.2s;
      box-shadow: 0 4px 15px rgba(64,145,108,0.4);
    }

    .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 25px rgba(64,145,108,0.5); }
    .btn-primary:active { transform: translateY(0); }

    .points-display {
      text-align: center;
      background: linear-gradient(135deg, #1b2d27, #2d6a4f);
      border-radius: 20px;
      padding: 24px;
      color: var(--branco);
      margin-bottom: 20px;
    }

    .points-display .pts-num {
      font-family: 'Fredoka One', cursive;
      font-size: 3.5rem;
      color: var(--amarelo);
      line-height: 1;
      display: block;
      transition: all 0.3s;
    }

    .points-display .pts-label { font-size: 0.95rem; opacity: 0.7; margin-top: 4px; }

    .nivel-badge {
      display: inline-block;
      background: var(--amarelo);
      color: var(--verde);
      font-weight: 800;
      font-size: 0.85rem;
      padding: 4px 14px;
      border-radius: 20px;
      margin-top: 8px;
    }

    .history-item {
      display: flex;
      align-items: center;
      gap: 14px;
      padding: 14px 16px;
      background: var(--cinza);
      border-radius: 12px;
      margin-bottom: 10px;
      transition: transform 0.2s;
      animation: slideIn 0.3s ease;
    }

    .history-item:hover { transform: translateX(4px); }

    @keyframes slideIn {
      from { opacity: 0; transform: translateX(-20px); }
      to   { opacity: 1; transform: translateX(0); }
    }

    .history-icon {
      width: 44px; height: 44px;
      border-radius: 12px;
      display: flex; align-items: center; justify-content: center;
      font-size: 1.4rem;
      flex-shrink: 0;
    }

    .history-info { flex: 1; }
    .history-info strong { display: block; font-size: 1rem; }
    .history-info span { font-size: 0.85rem; color: #888; }
    .history-pts { font-family: 'Fredoka One', cursive; font-size: 1.2rem; color: var(--verde); }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 14px;
      margin-bottom: 20px;
    }

    .stat-card {
      background: var(--branco);
      border-radius: 16px;
      padding: 18px 14px;
      text-align: center;
      box-shadow: var(--sombra);
    }

    .stat-card .stat-icon { font-size: 2rem; margin-bottom: 6px; }
    .stat-card .stat-num { font-family: 'Fredoka One', cursive; font-size: 1.6rem; color: var(--verde); }
    .stat-card .stat-lbl { font-size: 0.75rem; color: #888; font-weight: 700; text-transform: uppercase; }

    /* ===== NEWS PAGE ===== */
    .page-title {
      font-family: 'Fredoka One', cursive;
      font-size: 2rem;
      color: var(--verde);
      margin-bottom: 6px;
    }

    .page-subtitle { color: #666; font-size: 1rem; margin-bottom: 24px; }

    .news-card {
      background: var(--branco);
      border-radius: 20px;
      overflow: hidden;
      box-shadow: var(--sombra);
      margin-bottom: 20px;
      display: flex;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .news-card:hover { transform: translateY(-4px); box-shadow: 0 16px 40px rgba(45,106,79,0.2); }

    .news-accent { width: 8px; flex-shrink: 0; }
    .news-body { padding: 22px 24px; flex: 1; }

    .news-tag {
      display: inline-block;
      font-size: 0.75rem;
      font-weight: 800;
      text-transform: uppercase;
      letter-spacing: 1px;
      padding: 3px 10px;
      border-radius: 20px;
      margin-bottom: 10px;
    }

    .news-body h3 { font-size: 1.15rem; margin-bottom: 8px; line-height: 1.4; }
    .news-body p  { font-size: 0.9rem; color: #666; line-height: 1.6; }

    .news-meta {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-top: 14px;
      font-size: 0.82rem;
      color: #aaa;
      font-weight: 600;
    }

    .news-stat {
      background: var(--verde-palido);
      border-left: 4px solid var(--verde-medio);
      padding: 14px 18px;
      border-radius: 0 12px 12px 0;
      margin: 12px 0;
      font-weight: 700;
      color: var(--verde);
      font-size: 1rem;
    }

    .fact-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
      margin-bottom: 20px;
    }

    .fact-card {
      background: var(--branco);
      border-radius: 16px;
      padding: 20px;
      box-shadow: var(--sombra);
      border-top: 4px solid;
      text-align: center;
    }

    .fact-card .fact-num { font-family: 'Fredoka One', cursive; font-size: 2rem; }
    .fact-card .fact-txt { font-size: 0.85rem; color: #666; margin-top: 6px; }

    /* ===== MINI GAME ===== */
    .game-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: var(--branco);
      border-radius: 16px;
      padding: 16px 22px;
      box-shadow: var(--sombra);
      margin-bottom: 20px;
    }

    .game-stat { text-align: center; }
    .game-stat .g-num { font-family: 'Fredoka One', cursive; font-size: 1.6rem; color: var(--verde); }
    .game-stat .g-lbl { font-size: 0.75rem; color: #aaa; text-transform: uppercase; font-weight: 700; }

    .lixeiras {
      display: flex;
      justify-content: center;
      gap: 12px;
      margin-bottom: 28px;
      flex-wrap: wrap;
    }

    .lixeira {
      width: 100px;
      padding: 16px 10px 12px;
      border-radius: 16px;
      cursor: pointer;
      transition: all 0.2s;
      border: 3px solid transparent;
      text-align: center;
      user-select: none;
    }

    .lixeira:hover { transform: translateY(-6px) scale(1.05); }
    .lixeira.correct { animation: bounce 0.4s ease; border-color: #00e676 !important; }
    .lixeira.wrong   { animation: shake 0.4s ease; border-color: var(--vermelho) !important; }

    @keyframes bounce {
      0%,100% { transform: translateY(0); }
      40%      { transform: translateY(-14px); }
      70%      { transform: translateY(-6px); }
    }

    @keyframes shake {
      0%,100% { transform: translateX(0); }
      25%      { transform: translateX(-8px); }
      75%      { transform: translateX(8px); }
    }

    .lixeira .lid { font-size: 2.8rem; display: block; }
    .lixeira .lxname { font-weight: 800; font-size: 0.75rem; margin-top: 8px; text-transform: uppercase; letter-spacing: 0.5px; }

    .item-area {
      min-height: 160px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 20px;
    }

    .item-card {
      background: var(--branco);
      border-radius: 20px;
      padding: 32px 48px;
      box-shadow: 0 12px 40px rgba(45,106,79,0.2);
      text-align: center;
      animation: popIn 0.4s cubic-bezier(0.34,1.56,0.64,1);
    }

    @keyframes popIn {
      from { opacity: 0; transform: scale(0.5); }
      to   { opacity: 1; transform: scale(1); }
    }

    .item-card .item-emoji { font-size: 4rem; display: block; margin-bottom: 10px; }
    .item-card .item-name  { font-family: 'Fredoka One', cursive; font-size: 1.5rem; color: var(--verde); }
    .item-card .item-hint  { font-size: 0.85rem; color: #aaa; margin-top: 6px; }

    .timer-bar-wrap {
      background: #e0e0e0;
      border-radius: 8px;
      height: 10px;
      overflow: hidden;
      margin-bottom: 20px;
    }

    .timer-bar {
      height: 100%;
      border-radius: 8px;
      transition: width 0.1s linear, background 0.3s;
      background: var(--verde-claro);
    }

    .game-feedback {
      font-family: 'Fredoka One', cursive;
      font-size: 1.4rem;
      min-height: 36px;
      transition: all 0.3s;
    }

    .game-feedback.certo  { color: var(--verde-medio); }
    .game-feedback.errado { color: var(--vermelho); }

    .game-over-screen {
      display: none;
      text-align: center;
      padding: 32px;
    }

    .game-over-screen .go-emoji { font-size: 5rem; display: block; margin-bottom: 12px; }
    .game-over-screen h2 { font-family: 'Fredoka One', cursive; font-size: 2.2rem; color: var(--verde); margin-bottom: 8px; }
    .game-over-screen p { color: #666; margin-bottom: 24px; }

    .btn-secondary {
      padding: 14px 36px;
      background: var(--amarelo);
      color: var(--verde);
      border: none;
      border-radius: 14px;
      font-family: 'Fredoka One', cursive;
      font-size: 1.1rem;
      cursor: pointer;
      transition: all 0.2s;
      box-shadow: 0 4px 15px rgba(249,199,79,0.5);
    }

    .btn-secondary:hover { transform: translateY(-2px); box-shadow: 0 8px 25px rgba(249,199,79,0.6); }

    .xp-bar-wrap { background: #e0e0e0; border-radius: 8px; height: 12px; overflow: hidden; margin: 8px 0 4px; }
    .xp-bar { height: 100%; border-radius: 8px; background: linear-gradient(90deg, var(--verde-claro), var(--verde-medio)); transition: width 0.6s ease; }

    /* ===== DESCARTE PAGE ===== */
    .page-hero {
      background: linear-gradient(135deg, #1b4332 0%, var(--verde) 55%, var(--verde-medio) 100%);
      border-radius: 26px;
      padding: 42px 36px;
      color: #fff;
      margin-bottom: 32px;
      position: relative;
      overflow: hidden;
    }

    .page-hero .leaf-deco {
      position: absolute; right: 28px; top: 50%; transform: translateY(-50%);
      font-size: 8rem; opacity: 0.12; pointer-events: none;
    }

    .page-hero h1 {
      font-family: 'Fredoka One', cursive;
      font-size: 2.2rem; margin-bottom: 10px;
    }

    .page-hero p { font-size: 1.05rem; opacity: 0.88; max-width: 460px; }

    .progress-section {
      background: #fff;
      border-radius: 20px;
      padding: 22px 26px;
      box-shadow: var(--sombra);
      margin-bottom: 24px;
    }

    .progress-top {
      display: flex; justify-content: space-between; align-items: center;
      margin-bottom: 10px; flex-wrap: wrap; gap: 8px;
    }

    .progress-top h3 {
      font-family: 'Fredoka One', cursive;
      color: var(--verde); font-size: 1.1rem;
    }

    .progress-top .pts-badge {
      background: var(--amarelo); color: var(--verde);
      font-weight: 800; font-size: 0.85rem;
      padding: 4px 14px; border-radius: 20px;
    }

    .prog-bar-wrap {
      background: #e9ecef; border-radius: 10px;
      height: 16px; overflow: hidden; margin-bottom: 6px;
    }

    .prog-bar {
      height: 100%; border-radius: 10px;
      background: linear-gradient(90deg, var(--verde-claro), var(--verde-medio));
      transition: width 0.8s cubic-bezier(0.34,1.2,0.64,1);
      width: 0%;
    }

    .prog-label { font-size: 0.82rem; color: #999; font-weight: 700; }

    .challenges-row {
      display: flex; gap: 8px; flex-wrap: wrap; margin-top: 14px;
    }

    .ch-badge {
      padding: 6px 14px; border-radius: 20px;
      font-size: 0.8rem; font-weight: 700;
      border: 2px solid #e0e0e0; color: #aaa;
      transition: all 0.3s; cursor: default;
    }

    .ch-badge.done {
      background: var(--verde-palido);
      border-color: var(--verde-claro);
      color: var(--verde);
    }

    .search-section {
      background: #fff;
      border-radius: 20px;
      padding: 26px;
      box-shadow: var(--sombra);
      margin-bottom: 24px;
    }

    .search-section h3 {
      font-family: 'Fredoka One', cursive;
      color: var(--verde); font-size: 1.25rem; margin-bottom: 6px;
    }

    .search-section p { color: #888; font-size: 0.9rem; margin-bottom: 16px; }

    .search-row { display: flex; gap: 10px; }

    .search-input {
      flex: 1; padding: 13px 18px;
      border: 2px solid #e0e0e0; border-radius: 12px;
      font-family: 'Nunito', sans-serif; font-size: 1rem;
      background: var(--cinza); outline: none;
      transition: border 0.2s, background 0.2s;
    }

    .search-input:focus { border-color: var(--verde-claro); background: #fff; }

    .btn-search {
      padding: 13px 22px;
      background: linear-gradient(135deg, var(--verde-medio), var(--verde));
      color: #fff; border: none; border-radius: 12px;
      font-family: 'Fredoka One', cursive; font-size: 1rem;
      cursor: pointer; transition: all 0.2s;
      box-shadow: 0 4px 14px rgba(64,145,108,0.35);
    }

    .btn-search:hover { transform: translateY(-2px); }

    #search-result {
      margin-top: 16px; display: none;
      animation: fadeIn 0.35s ease;
    }

    .result-box {
      border-radius: 14px; padding: 18px 20px;
      display: flex; align-items: center; gap: 16px;
    }

    .result-icon { font-size: 2.8rem; flex-shrink: 0; }
    .result-info h4 { font-size: 1.1rem; margin-bottom: 4px; }
    .result-info p { font-size: 0.88rem; opacity: 0.8; }

    .result-notfound {
      background: #fff3cd; border-left: 4px solid var(--amarelo);
      border-radius: 0 12px 12px 0; padding: 14px 18px;
      color: #856404; font-weight: 700;
    }

    .section-title-sm {
      font-family: 'Fredoka One', cursive;
      color: var(--verde); font-size: 1.5rem;
      margin-bottom: 6px;
    }

    .section-sub { color: #666; font-size: 0.95rem; margin-bottom: 22px; }

    .cards-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(190px, 1fr));
      gap: 18px;
      margin-bottom: 32px;
    }

    .waste-card {
      background: #fff;
      border-radius: 20px;
      padding: 24px 18px 20px;
      box-shadow: var(--sombra);
      text-align: center;
      cursor: pointer;
      border: 3px solid transparent;
      transition: transform 0.25s cubic-bezier(0.34,1.4,0.64,1), box-shadow 0.25s ease, border-color 0.2s;
      position: relative;
      overflow: hidden;
    }

    .waste-card::before {
      content: '';
      position: absolute; top: 0; left: 0; right: 0;
      height: 5px;
      border-radius: 20px 20px 0 0;
      background: var(--accent, #aaa);
    }

    .waste-card:hover {
      transform: translateY(-8px) scale(1.03);
      box-shadow: 0 18px 48px rgba(45,106,79,0.18);
      border-color: var(--accent, var(--verde-claro));
    }

    .waste-card:hover .card-bin-icon { transform: scale(1.18) rotate(-5deg); }
    .waste-card.expanded { border-color: var(--accent, var(--verde-claro)); }

    .card-emoji { font-size: 3rem; margin-bottom: 8px; display: block; }
    .card-bin-icon {
      font-size: 2rem; margin-bottom: 6px; display: block;
      transition: transform 0.3s cubic-bezier(0.34,1.5,0.64,1);
    }

    .card-title { font-family: 'Fredoka One', cursive; font-size: 1.15rem; margin-bottom: 4px; color: var(--accent, var(--verde)); }
    .card-subtitle { font-size: 0.8rem; color: #888; font-weight: 700; text-transform: uppercase; letter-spacing: 0.5px; }

    .card-detail {
      display: none; margin-top: 14px;
      border-top: 1px dashed rgba(0,0,0,0.08);
      padding-top: 14px; text-align: left;
    }

    .card-detail.open { display: block; animation: fadeIn 0.3s ease; }

    .detail-block { margin-bottom: 10px; }
    .detail-block strong { font-size: 0.78rem; text-transform: uppercase; letter-spacing: 0.5px; display: block; margin-bottom: 4px; }
    .detail-block ul { padding-left: 16px; }
    .detail-block li { font-size: 0.83rem; color: #555; margin-bottom: 2px; }
    .ok-list li::marker { color: #2d6a4f; }
    .no-list li { color: #c0392b; }
    .no-list li::marker { color: #c0392b; }

    /* ===== QUIZ (Descarte) ===== */
    .quiz-section {
      background: #fff;
      border-radius: 22px;
      padding: 32px 28px;
      box-shadow: var(--sombra);
      margin-bottom: 36px;
    }

    .quiz-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 22px; flex-wrap: wrap; gap: 12px; }
    .quiz-header h3 { font-family: 'Fredoka One', cursive; color: var(--verde); font-size: 1.4rem; }
    .quiz-meta { display: flex; gap: 14px; }

    .quiz-badge {
      background: var(--verde-palido); color: var(--verde);
      font-weight: 800; font-size: 0.85rem;
      padding: 5px 14px; border-radius: 20px;
    }

    .quiz-progress-wrap {
      background: #e9ecef; border-radius: 8px;
      height: 8px; overflow: hidden; margin-bottom: 24px;
    }

    .quiz-progress-bar {
      height: 100%; border-radius: 8px;
      background: linear-gradient(90deg, var(--verde-claro), var(--verde-medio));
      transition: width 0.5s ease;
    }

    .question-text {
      font-size: 1.1rem; font-weight: 700;
      color: var(--texto); margin-bottom: 20px; line-height: 1.5;
    }

    .options-grid {
      display: grid; grid-template-columns: 1fr 1fr;
      gap: 12px; margin-bottom: 18px;
    }

    .option-btn {
      padding: 14px 16px; border-radius: 12px;
      border: 2px solid #e8e8e8;
      background: var(--cinza);
      font-family: 'Nunito', sans-serif; font-size: 0.95rem; font-weight: 700;
      color: var(--texto); cursor: pointer;
      transition: all 0.2s; text-align: left;
    }

    .option-btn:hover:not(:disabled) {
      border-color: var(--verde-claro);
      background: var(--verde-palido);
      transform: translateY(-2px);
    }

    .option-btn.correct { background: #d4edda; border-color: #28a745; color: #155724; }
    .option-btn.wrong   { background: #f8d7da; border-color: #dc3545; color: #721c24; }
    .option-btn:disabled { cursor: default; transform: none; }

    .quiz-feedback {
      min-height: 36px; font-size: 1rem; font-weight: 700;
      padding: 10px 16px; border-radius: 10px;
      margin-bottom: 16px; display: none;
    }

    .quiz-feedback.show { display: block; animation: fadeIn 0.3s ease; }
    .quiz-feedback.certo  { background: #d4edda; color: #155724; }
    .quiz-feedback.errado { background: #f8d7da; color: #721c24; }

    .quiz-nav { display: flex; justify-content: flex-end; }

    .btn-quiz-next {
      padding: 12px 28px;
      background: linear-gradient(135deg, var(--verde-medio), var(--verde));
      color: #fff; border: none; border-radius: 12px;
      font-family: 'Fredoka One', cursive; font-size: 1rem;
      cursor: pointer; transition: all 0.2s;
      box-shadow: 0 4px 14px rgba(64,145,108,0.35);
    }

    .btn-quiz-next:hover { transform: translateY(-2px); }
    .btn-quiz-next:disabled { opacity: 0.4; cursor: default; transform: none; }

    .quiz-result { display: none; text-align: center; padding: 20px; }
    .quiz-result .result-emoji { font-size: 4.5rem; display: block; margin-bottom: 12px; }
    .quiz-result h4 { font-family: 'Fredoka One', cursive; font-size: 1.8rem; color: var(--verde); margin-bottom: 8px; }
    .quiz-result p { color: #666; margin-bottom: 20px; font-size: 1rem; }

    .btn-replay {
      padding: 12px 28px;
      background: var(--amarelo); color: var(--verde);
      border: none; border-radius: 12px;
      font-family: 'Fredoka One', cursive; font-size: 1rem;
      cursor: pointer; transition: all 0.2s;
      box-shadow: 0 4px 14px rgba(249,199,79,0.5);
    }

    .btn-replay:hover { transform: translateY(-2px); }

    /* ===== TOAST ===== */
    .toast {
      position: fixed;
      bottom: 24px;
      left: 50%;
      transform: translateX(-50%) translateY(80px);
      background: var(--verde);
      color: #fff;
      font-weight: 700;
      padding: 12px 28px;
      border-radius: 40px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.2);
      z-index: 999;
      transition: transform 0.4s cubic-bezier(0.34,1.56,0.64,1);
      white-space: nowrap;
    }

    .toast.show { transform: translateX(-50%) translateY(0); }

    /* ===== RESPONSIVE ===== */
    @media (max-width: 600px) {
      .form-grid { grid-template-columns: 1fr; }
      .stats-grid { grid-template-columns: repeat(3, 1fr); }
      .fact-grid  { grid-template-columns: 1fr; }
      .news-card  { flex-direction: column; }
      .news-accent { width: 100%; height: 8px; }
      .lixeira { width: 80px; }
      .hero h2 { font-size: 1.6rem; }
      .hero::after { display: none; }
      .cards-grid { grid-template-columns: repeat(2, 1fr); }
      .options-grid { grid-template-columns: 1fr; }
      .page-hero h1 { font-size: 1.75rem; }
      .page-hero .leaf-deco { display: none; }
      .search-row { flex-direction: column; }
      nav { padding: 0 14px; }
      .nav-btn { padding: 8px 10px; font-size: 0.82rem; }
    }
  </style>
</head>
<body>

<!-- ========== SPLASH SCREEN ========== -->
<div id="splash">
  <div class="splash-leaves" id="splash-leaves"></div>

  <div class="splash-logo">🌱 Eco<span>Recicla</span></div>
  <div class="splash-tagline">Recicle, aprenda e proteja o planeta 🌍</div>

  <div class="splash-features">
    <div class="splash-feat">
      <span class="sf-icon">♻️</span>
      <div class="sf-label">Registre reciclagens</div>
    </div>
    <div class="splash-feat">
      <span class="sf-icon">🎮</span>
      <div class="sf-label">Jogue e aprenda</div>
    </div>
    <div class="splash-feat">
      <span class="sf-icon">🗑️</span>
      <div class="sf-label">Descarte correto</div>
    </div>
    <div class="splash-feat">
      <span class="sf-icon">⭐</span>
      <div class="sf-label">Ganhe pontos</div>
    </div>
  </div>

  <button class="btn-start" onclick="iniciarApp()">Começar Agora</button>

  <div class="splash-footer">Feito para quem ama o planeta 💚</div>
</div>

<!-- ========== APP SHELL ========== -->
<div id="app-shell">

<nav>
  <div class="nav-logo">🌱 Eco<span>Recicla</span></div>
  <div class="nav-links">
    <button class="nav-btn active" onclick="showPage('home', this)">♻️ Início</button>
    <button class="nav-btn" onclick="showPage('noticias', this)">📰 Notícias</button>
    <button class="nav-btn" onclick="showPage('game', this)">🎮 Jogo</button>
    <button class="nav-btn" onclick="showPage('descarte', this)">🗑️ Descarte</button>
  </div>
  <div class="nav-pontos">⭐ <span id="nav-pts">0</span> pts</div>
</nav>

<!-- ========== HOME PAGE ========== -->
<div id="page-home" class="page active">

  <div class="hero">
    <h2>Recicle e Ganhe Pontos!</h2>
    <p>Registre seus materiais reciclados, suba de nível e ajude o planeta. 🌍</p>
  </div>

  <div class="stats-grid">
    <div class="stat-card">
      <div class="stat-icon">♻️</div>
      <div class="stat-num" id="stat-total">0</div>
      <div class="stat-lbl">Registros</div>
    </div>
    <div class="stat-card">
      <div class="stat-icon">⚖️</div>
      <div class="stat-num" id="stat-kg">0</div>
      <div class="stat-lbl">kg reciclados</div>
    </div>
    <div class="stat-card">
      <div class="stat-icon">🌳</div>
      <div class="stat-num" id="stat-arvores">0</div>
      <div class="stat-lbl">Árvores salvas</div>
    </div>
  </div>

  <div class="card">
    <h3 style="font-family:'Fredoka One',cursive;font-size:1.3rem;color:var(--verde);margin-bottom:18px;">📝 Registrar Reciclagem</h3>

    <div class="form-grid">
      <div>
        <label for="material">Material</label>
        <select id="material">
          <option value="Plástico">♻️ Plástico</option>
          <option value="Papel">📄 Papel</option>
          <option value="Vidro">🍶 Vidro</option>
          <option value="Metal">🥫 Metal</option>
          <option value="Orgânico">🌿 Orgânico</option>
          <option value="Eletrônico">💻 Eletrônico</option>
        </select>
      </div>
      <div>
        <label for="quantidade">Quantidade (kg)</label>
        <input type="number" id="quantidade" placeholder="Ex: 2.5" min="0.1" step="0.1">
      </div>
    </div>

    <button class="btn-primary" onclick="registrarReciclagem()">
      ✅ Registrar Reciclagem
    </button>
  </div>

  <div class="points-display">
    <span class="pts-num" id="pontos-num">0</span>
    <div class="pts-label">Pontos Totais</div>
    <div class="xp-bar-wrap" style="max-width:300px;margin:12px auto 0;">
      <div class="xp-bar" id="xp-bar" style="width:0%"></div>
    </div>
    <div style="font-size:0.82rem;opacity:0.6;margin-top:4px;" id="xp-label">0 / 100 para o próximo nível</div>
    <div class="nivel-badge" id="nivel-badge">🌱 Iniciante</div>
  </div>

  <div class="card">
    <h3 style="font-family:'Fredoka One',cursive;font-size:1.2rem;color:var(--verde);margin-bottom:14px;">📋 Histórico</h3>
    <ul id="lista" style="list-style:none;padding:0;"></ul>
    <p id="empty-msg" style="text-align:center;color:#aaa;font-size:0.95rem;padding:20px 0;">Nenhum registro ainda. Comece a reciclar! 🌿</p>
  </div>
</div>

<!-- ========== NOTICIAS PAGE ========== -->
<div id="page-noticias" class="page">
  <h2 class="page-title">📰 Notícias & Artigos</h2>
  <p class="page-subtitle">Saiba por que reciclar é essencial para o futuro do planeta.</p>

  <div class="fact-grid">
    <div class="fact-card" style="border-color:#4caf50;">
      <div class="fact-num" style="color:#4caf50;">🇧🇷</div>
      <div class="fact-num" style="color:#4caf50;">3%</div>
      <div class="fact-txt">dos resíduos recicláveis no Brasil são efetivamente reciclados</div>
    </div>
    <div class="fact-card" style="border-color:#2196f3;">
      <div class="fact-num" style="color:#2196f3;">80M</div>
      <div class="fact-txt">de toneladas de lixo são geradas no Brasil por ano</div>
    </div>
    <div class="fact-card" style="border-color:#ff9800;">
      <div class="fact-num" style="color:#ff9800;">400</div>
      <div class="fact-txt">anos leva para o plástico se decompor na natureza</div>
    </div>
    <div class="fact-card" style="border-color:#9c27b0;">
      <div class="fact-num" style="color:#9c27b0;">1 ton</div>
      <div class="fact-txt">de papel reciclado salva 20 árvores adultas</div>
    </div>
  </div>

  <div class="news-card">
    <div class="news-accent" style="background:#2196f3;"></div>
    <div class="news-body">
      <span class="news-tag" style="background:#e3f2fd;color:#1565c0;">🌊 Meio Ambiente</span>
      <h3>Plástico nos Oceanos: Uma Crise Que Podemos Reverter</h3>
      <p>Estudos estimam que mais de 8 milhões de toneladas de plástico entram nos oceanos todo ano. A reciclagem adequada de plásticos poderia reduzir em até 80% esse número. Cada garrafa descartada corretamente evita que partículas de microplástico contaminem rios, mares e nossa cadeia alimentar.</p>
      <div class="news-stat">💡 Reciclar 1 kg de plástico economiza o equivalente a 2 litros de petróleo.</div>
      <p>Países como Alemanha e Suécia já reciclam mais de 60% de seus resíduos plásticos. O Brasil, com políticas públicas e conscientização, tem tudo para alcançar esses índices em menos de uma década.</p>
      <div class="news-meta">
        <span>🗞️ EcoMundo</span><span>•</span><span>Maio 2025</span><span>•</span><span>📖 5 min de leitura</span>
      </div>
    </div>
  </div>

  <div class="news-card">
    <div class="news-accent" style="background:#4caf50;"></div>
    <div class="news-body">
      <span class="news-tag" style="background:#e8f5e9;color:#2e7d32;">🌳 Florestas</span>
      <h3>Reciclagem de Papel Salva Florestas Inteiras</h3>
      <p>A indústria de celulose é uma das maiores consumidoras de recursos florestais. Para cada tonelada de papel reciclado, estima-se que 20 árvores adultas deixam de ser cortadas. Além disso, o processo de reciclagem do papel consome 70% menos energia do que fabricar papel virgem.</p>
      <div class="news-stat">🌲 Uma tonelada de papel reciclado economiza 26.000 litros de água.</div>
      <p>Com a digitalização crescente, o consumo de papel caiu, mas ainda representa um enorme impacto ambiental. Pequenos gestos, como separar papel de outros resíduos, fazem uma diferença enorme quando multiplicados por milhões de pessoas.</p>
      <div class="news-meta">
        <span>🗞️ Folha Verde</span><span>•</span><span>Março 2025</span><span>•</span><span>📖 4 min de leitura</span>
      </div>
    </div>
  </div>

  <div class="news-card">
    <div class="news-accent" style="background:#ff9800;"></div>
    <div class="news-body">
      <span class="news-tag" style="background:#fff3e0;color:#e65100;">⚡ Energia</span>
      <h3>Alumínio: O Metal que Vale Ouro para o Planeta</h3>
      <p>Reciclar alumínio é uma das ações mais impactantes que um cidadão pode tomar. A reciclagem de uma lata de alumínio economiza energia suficiente para manter uma TV ligada por 3 horas. O Brasil é líder mundial na reciclagem de latas de alumínio, reciclando mais de 97% das latas produzidas.</p>
      <div class="news-stat">⚡ Reciclar alumínio usa apenas 5% da energia necessária para produzir alumínio novo.</div>
      <p>Esse sucesso se deve em grande parte à atuação de catadores, que representam uma força essencial na cadeia de reciclagem brasileira. Valorizar e formalizar esse setor é fundamental para avançar ainda mais.</p>
      <div class="news-meta">
        <span>🗞️ Jornal Sustentável</span><span>•</span><span>Abril 2025</span><span>•</span><span>📖 3 min de leitura</span>
      </div>
    </div>
  </div>

  <div class="news-card">
    <div class="news-accent" style="background:#9c27b0;"></div>
    <div class="news-body">
      <span class="news-tag" style="background:#f3e5f5;color:#6a1b9a;">🏙️ Cidades</span>
      <h3>Cidades Inteligentes Apostam na Coleta Seletiva Digital</h3>
      <p>Municípios ao redor do mundo estão usando tecnologia e gamificação para engajar cidadãos na reciclagem. Aplicativos que premiam pontos por reciclagem, lixeiras inteligentes com sensores e campanhas em redes sociais têm aumentado as taxas de reciclagem em até 40% em projetos-piloto.</p>
      <div class="news-stat">📱 Cidades com programas de gamificação reciclam 3x mais que a média nacional.</div>
      <p>A ideia é simples: tornar a reciclagem divertida e recompensadora. Quando as pessoas percebem que suas ações têm impacto real e imediato, o comportamento muda. E você pode começar agora mesmo, aqui no EcoRecicla!</p>
      <div class="news-meta">
        <span>🗞️ Tech & Ambiente</span><span>•</span><span>Maio 2025</span><span>•</span><span>📖 6 min de leitura</span>
      </div>
    </div>
  </div>

  <div class="news-card">
    <div class="news-accent" style="background:#e63946;"></div>
    <div class="news-body">
      <span class="news-tag" style="background:#fce4ec;color:#c62828;">🌡️ Clima</span>
      <h3>Reciclagem e Mudanças Climáticas: A Ligação Direta</h3>
      <p>Produzir materiais a partir do zero libera enormes quantidades de CO₂. A reciclagem reduz significativamente essas emissões: reciclar papel reduz 74% das emissões em relação ao processo convencional; para o vidro, a redução é de 20%; para o aço, chega a 86%.</p>
      <div class="news-stat">🌡️ Se o mundo reciclasse 50% mais, evitaríamos 1 bilhão de toneladas de CO₂ por ano.</div>
      <p>Com o aquecimento global se tornando cada vez mais urgente, a reciclagem emerge não apenas como uma questão ambiental, mas como uma estratégia de sobrevivência climática. Cada ação conta — a sua também.</p>
      <div class="news-meta">
        <span>🗞️ Clima em Pauta</span><span>•</span><span>Janeiro 2025</span><span>•</span><span>📖 7 min de leitura</span>
      </div>
    </div>
  </div>
</div>

<!-- ========== GAME PAGE ========== -->
<div id="page-game" class="page">
  <h2 class="page-title">🎮 Jogo da Reciclagem</h2>
  <p class="page-subtitle">Jogue para aprender e ganhe pontos extras na sua conta!</p>

  <div id="game-container">
    <div id="game-play">
      <div class="game-header">
        <div class="game-stat">
          <div class="g-num" id="g-score">0</div>
          <div class="g-lbl">Pontos</div>
        </div>
        <div class="game-stat">
          <div class="g-num" id="g-level">1</div>
          <div class="g-lbl">Nível</div>
        </div>
        <div class="game-stat">
          <div class="g-num" id="g-streak">0</div>
          <div class="g-lbl">Sequência 🔥</div>
        </div>
        <div class="game-stat">
          <div class="g-num" id="g-lives">❤️❤️❤️</div>
          <div class="g-lbl">Vidas</div>
        </div>
      </div>

      <div class="timer-bar-wrap">
        <div class="timer-bar" id="timer-bar"></div>
      </div>

      <div class="item-area">
        <div class="item-card" id="item-card">
          <span class="item-emoji" id="item-emoji">🎯</span>
          <div class="item-name" id="item-name">Pressione Iniciar!</div>
          <div class="item-hint" id="item-hint">Jogue para ganhar pontos extras</div>
        </div>
      </div>

      <div class="lixeiras">
        <div class="lixeira" style="background:#fff9c4;" onclick="guess('Papel')">
          <span class="lid">📄</span>
          <div class="lxname" style="color:#f9a825;">Papel</div>
        </div>
        <div class="lixeira" style="background:#e8f5e9;" onclick="guess('Plástico')">
          <span class="lid">♻️</span>
          <div class="lxname" style="color:#2e7d32;">Plástico</div>
        </div>
        <div class="lixeira" style="background:#e3f2fd;" onclick="guess('Vidro')">
          <span class="lid">🍶</span>
          <div class="lxname" style="color:#1565c0;">Vidro</div>
        </div>
        <div class="lixeira" style="background:#fce4ec;" onclick="guess('Metal')">
          <span class="lid">🥫</span>
          <div class="lxname" style="color:#b71c1c;">Metal</div>
        </div>
        <div class="lixeira" style="background:#f3e5f5;" onclick="guess('Orgânico')">
          <span class="lid">🌿</span>
          <div class="lxname" style="color:#6a1b9a;">Orgânico</div>
        </div>
      </div>

      <div class="game-feedback" id="game-feedback"></div>

      <div style="text-align:center;margin-top:20px;">
        <button class="btn-secondary" id="start-btn" onclick="startGame()">🎮 Iniciar Jogo</button>
      </div>
    </div>

    <div class="game-over-screen" id="game-over">
      <span class="go-emoji" id="go-emoji">🌱</span>
      <h2 id="go-title">Fim de Jogo!</h2>
      <p id="go-msg">Você marcou <strong id="go-score">0</strong> pontos!</p>
      <p style="color:var(--verde);font-weight:700;margin-bottom:20px;" id="go-bonus"></p>
      <button class="btn-secondary" onclick="restartGame()">🔄 Jogar Novamente</button>
    </div>
  </div>

  <div class="card" style="margin-top:24px;">
    <h3 style="font-family:'Fredoka One',cursive;font-size:1.2rem;color:var(--verde);margin-bottom:14px;">📖 Guia de Reciclagem</h3>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;">
      <div style="background:#fff9c4;border-radius:12px;padding:14px;">
        <strong style="color:#f9a825;">📄 Papel</strong>
        <p style="font-size:0.82rem;color:#666;margin-top:4px;">Jornais, revistas, caixas, papelão, papel de escritório</p>
      </div>
      <div style="background:#e8f5e9;border-radius:12px;padding:14px;">
        <strong style="color:#2e7d32;">♻️ Plástico</strong>
        <p style="font-size:0.82rem;color:#666;margin-top:4px;">Garrafas PET, embalagens, sacolas, potes</p>
      </div>
      <div style="background:#e3f2fd;border-radius:12px;padding:14px;">
        <strong style="color:#1565c0;">🍶 Vidro</strong>
        <p style="font-size:0.82rem;color:#666;margin-top:4px;">Garrafas, potes, frascos de perfume, janelas</p>
      </div>
      <div style="background:#fce4ec;border-radius:12px;padding:14px;">
        <strong style="color:#b71c1c;">🥫 Metal</strong>
        <p style="font-size:0.82rem;color:#666;margin-top:4px;">Latas de alumínio, aço, tampas metálicas, panelas</p>
      </div>
    </div>
  </div>
</div>

<!-- ========== DESCARTE PAGE ========== -->
<div id="page-descarte" class="page">

  <div class="page-hero">
    <div class="leaf-deco">🌿</div>
    <h1>🗑️ Descarte Correto</h1>
    <p>Aprenda onde jogar cada tipo de lixo e ajude a proteger o meio ambiente de forma fácil e divertida!</p>
  </div>

  <!-- Desafios -->
  <div class="progress-section">
    <div class="progress-top">
      <h3>🏆 Seus Desafios Sustentáveis</h3>
      <span class="pts-badge" id="challenge-pts">0 / 5 concluídos</span>
    </div>
    <div class="prog-bar-wrap">
      <div class="prog-bar" id="challenge-bar"></div>
    </div>
    <div class="prog-label" id="challenge-label">Complete desafios para subir de nível ecológico! 🌱</div>
    <div class="challenges-row">
      <div class="ch-badge" id="ch1" data-tip="Primeira pesquisa realizada!">🔍 Primeira Pesquisa</div>
      <div class="ch-badge" id="ch2" data-tip="3 lixeiras exploradas!">🗑️ Explorador de Lixeiras</div>
      <div class="ch-badge" id="ch3" data-tip="5 perguntas respondidas!">📝 Quizeiro</div>
      <div class="ch-badge" id="ch4" data-tip="3 acertos seguidos!">✅ Acertador Nato</div>
      <div class="ch-badge" id="ch5" data-tip="Quiz completo com 10/10!">🌟 Mestre da Reciclagem</div>
    </div>
  </div>

  <!-- Busca -->
  <div class="search-section">
    <h3>🔍 Onde Descartar?</h3>
    <p>Digite um objeto e descubra imediatamente como descartá-lo corretamente:</p>
    <div class="search-row">
      <input type="text" class="search-input" id="search-input" placeholder="Ex: garrafa PET, casca de banana, pilha..." onkeydown="if(event.key==='Enter') doSearch()">
      <button class="btn-search" onclick="doSearch()">🔍 Buscar</button>
    </div>
    <div id="search-result"></div>
  </div>

  <!-- Cards de resíduos -->
  <h2 class="section-title-sm">🗑️ Tipos de Resíduos</h2>
  <p class="section-sub">Clique em cada card para ver o que pode e não pode ser descartado naquela lixeira.</p>
  <div class="cards-grid" id="waste-cards"></div>

  <!-- Quiz -->
  <div class="quiz-section">
    <div class="quiz-header">
      <h3>📝 Quiz de Reciclagem</h3>
      <div class="quiz-meta">
        <span class="quiz-badge">❓ <span id="q-num">1</span>/10</span>
        <span class="quiz-badge">⭐ <span id="q-score">0</span> pts</span>
      </div>
    </div>
    <div class="quiz-progress-wrap">
      <div class="quiz-progress-bar" id="quiz-prog" style="width:10%"></div>
    </div>
    <div id="quiz-area">
      <div class="question-text" id="q-text">Carregando…</div>
      <div class="options-grid" id="q-options"></div>
      <div class="quiz-feedback" id="q-feedback"></div>
      <div class="quiz-nav">
        <button class="btn-quiz-next" id="q-next" onclick="nextQuestion()" disabled>Próxima →</button>
      </div>
    </div>
    <div class="quiz-result" id="quiz-result">
      <span class="result-emoji" id="r-emoji">🌟</span>
      <h4 id="r-title">Incrível!</h4>
      <p>Você acertou <strong id="r-score">0</strong> de 10 perguntas!</p>
      <button class="btn-replay" onclick="resetQuiz()">🔄 Jogar Novamente</button>
    </div>
  </div>

</div>

</div><!-- end #app-shell -->

<!-- Toast -->
<div class="toast" id="toast"></div>

<script>
  // ===================== SHARED STATE =====================
  let state = {
    pontos: 0,
    totalKg: 0,
    totalRegistros: 0,
    historico: []
  };

  const niveis = [
    { min: 0,    label: '🌱 Iniciante',    next: 100  },
    { min: 100,  label: '🌿 Aprendiz',     next: 300  },
    { min: 300,  label: '♻️ Reciclador',   next: 600  },
    { min: 600,  label: '🌳 Ecologista',   next: 1000 },
    { min: 1000, label: '🌍 Guardião',     next: 2000 },
    { min: 2000, label: '🌟 Mestre Verde', next: 9999 },
  ];

  const materialInfo = {
    'Plástico':   { icon: '♻️', bg: '#e8f5e9', multi: 10 },
    'Papel':      { icon: '📄', bg: '#fff9c4', multi: 8  },
    'Vidro':      { icon: '🍶', bg: '#e3f2fd', multi: 12 },
    'Metal':      { icon: '🥫', bg: '#fce4ec', multi: 15 },
    'Orgânico':   { icon: '🌿', bg: '#f3e5f5', multi: 5  },
    'Eletrônico': { icon: '💻', bg: '#ede7f6', multi: 20 },
  };

  // ===================== HOME LOGIC =====================
  function registrarReciclagem() {
    const material = document.getElementById('material').value;
    const qtd      = parseFloat(document.getElementById('quantidade').value);

    if (!qtd || qtd <= 0) { showToast('⚠️ Digite uma quantidade válida!'); return; }

    const info   = materialInfo[material];
    const earned = Math.round(qtd * info.multi);

    state.pontos += earned;
    state.totalKg += qtd;
    state.totalRegistros++;
    state.historico.unshift({ material, qtd, earned, ts: new Date() });

    document.getElementById('quantidade').value = '';
    updateUI();
    addHistoryItem(material, qtd, earned, info);
    showToast(`+${earned} pontos por ${qtd}kg de ${material}! 🎉`);
  }

  function addHistoryItem(material, qtd, earned, info) {
    const lista = document.getElementById('lista');
    document.getElementById('empty-msg').style.display = 'none';

    const li = document.createElement('li');
    li.className = 'history-item';
    li.innerHTML = `
      <div class="history-icon" style="background:${info.bg}">${info.icon}</div>
      <div class="history-info">
        <strong>${qtd} kg de ${material}</strong>
        <span>${new Date().toLocaleDateString('pt-BR', {day:'2-digit',month:'short',hour:'2-digit',minute:'2-digit'})}</span>
      </div>
      <div class="history-pts">+${earned}</div>
    `;
    lista.insertBefore(li, lista.firstChild);
  }

  function updateUI() {
    document.getElementById('pontos-num').innerText  = state.pontos;
    document.getElementById('nav-pts').innerText     = state.pontos;
    document.getElementById('stat-total').innerText  = state.totalRegistros;
    document.getElementById('stat-kg').innerText     = state.totalKg.toFixed(1);
    document.getElementById('stat-arvores').innerText = Math.floor(state.totalKg / 10);

    let nivel = niveis[0];
    for (const n of niveis) { if (state.pontos >= n.min) nivel = n; }
    const next = nivel.next === 9999 ? 9999 : nivel.next;
    const prev  = nivel.min;
    const pct   = next === 9999 ? 100 : Math.min(100, Math.round((state.pontos - prev) / (next - prev) * 100));

    document.getElementById('nivel-badge').innerText  = nivel.label;
    document.getElementById('xp-bar').style.width     = pct + '%';
    document.getElementById('xp-label').innerText     = next === 9999 ? 'Nível máximo! 🏆' : `${state.pontos} / ${next} para o próximo nível`;
  }

  // ===================== GAME LOGIC =====================
  const items = [
    { emoji:'📰', name:'Jornal',          hint:'Papel impresso',       cat:'Papel'    },
    { emoji:'📦', name:'Caixa de Papelão',hint:'Embalagem de papelão', cat:'Papel'    },
    { emoji:'📚', name:'Revistas',         hint:'Papel com tinta',      cat:'Papel'    },
    { emoji:'🍶', name:'Garrafa de Vidro', hint:'Vidro transparente',   cat:'Vidro'    },
    { emoji:'🫙', name:'Pote de Vidro',    hint:'Recipiente de vidro',  cat:'Vidro'    },
    { emoji:'🥤', name:'Copo de Vidro',    hint:'Cristal transparente', cat:'Vidro'    },
    { emoji:'🥤', name:'Garrafa PET',      hint:'Plástico reciclável',  cat:'Plástico' },
    { emoji:'🪣', name:'Balde Plástico',   hint:'Plástico resistente',  cat:'Plástico' },
    { emoji:'🛍️', name:'Sacola Plástica',  hint:'Polietileno',          cat:'Plástico' },
    { emoji:'🥫', name:'Lata de Feijão',   hint:'Metal lacrado',        cat:'Metal'    },
    { emoji:'🍺', name:'Lata de Alumínio', hint:'Alumínio leve',        cat:'Metal'    },
    { emoji:'🔩', name:'Parafuso',         hint:'Ferro ou aço',         cat:'Metal'    },
    { emoji:'🍌', name:'Casca de Banana',  hint:'Resíduo orgânico',     cat:'Orgânico' },
    { emoji:'☕', name:'Borra de Café',    hint:'Orgânico úmido',       cat:'Orgânico' },
    { emoji:'🥦', name:'Talos de Legume',  hint:'Resíduo de cozinha',   cat:'Orgânico' },
  ];

  let game = { running:false, score:0, lives:3, streak:0, level:1, timer:null, timerPct:100, current:null };

  function startGame() {
    game = { running:true, score:0, lives:3, streak:0, level:1, timer:null, timerPct:100, current:null };
    document.getElementById('start-btn').style.display   = 'none';
    document.getElementById('game-over').style.display   = 'none';
    document.getElementById('game-play').querySelector('.item-area').style.display = 'flex';
    updateGameUI();
    nextItem();
  }

  function nextItem() {
    clearInterval(game.timer);
    game.current  = items[Math.floor(Math.random() * items.length)];
    game.timerPct = 100;

    document.getElementById('item-emoji').innerText = game.current.emoji;
    document.getElementById('item-name').innerText  = game.current.name;
    document.getElementById('item-hint').innerText  = game.current.hint;
    document.getElementById('game-feedback').innerText = '';

    const speed = Math.max(50, 100 - game.level * 8);
    game.timer = setInterval(() => {
      game.timerPct -= 1;
      document.getElementById('timer-bar').style.width = game.timerPct + '%';
      document.getElementById('timer-bar').style.background =
        game.timerPct > 50 ? 'var(--verde-claro)' : game.timerPct > 25 ? 'var(--laranja)' : 'var(--vermelho)';
      if (game.timerPct <= 0) { clearInterval(game.timer); handleWrong('⏱️ Tempo esgotado!'); }
    }, speed);
  }

  function guess(category) {
    if (!game.running || !game.current) return;
    clearInterval(game.timer);

    const lixeiras = document.querySelectorAll('.lixeira');
    const idx = ['Papel','Plástico','Vidro','Metal','Orgânico'].indexOf(category);

    if (category === game.current.cat) {
      game.score += 10 + game.streak * 2 + game.level * 3;
      game.streak++;
      if (game.streak % 5 === 0) game.level++;
      if (idx >= 0) { lixeiras[idx].classList.add('correct'); setTimeout(()=>lixeiras[idx].classList.remove('correct'),500); }
      document.getElementById('game-feedback').className  = 'game-feedback certo';
      document.getElementById('game-feedback').innerText = game.streak > 1 ? `✅ Correto! 🔥 x${game.streak}` : '✅ Correto!';
      setTimeout(nextItem, 700);
    } else {
      if (idx >= 0) { lixeiras[idx].classList.add('wrong'); setTimeout(()=>lixeiras[idx].classList.remove('wrong'),500); }
      handleWrong(`❌ Era ${game.current.cat}!`);
    }
    updateGameUI();
  }

  function handleWrong(msg) {
    game.lives--;
    game.streak = 0;
    document.getElementById('game-feedback').className  = 'game-feedback errado';
    document.getElementById('game-feedback').innerText = msg;
    updateGameUI();
    if (game.lives <= 0) { setTimeout(endGame, 800); }
    else { setTimeout(nextItem, 1000); }
  }

  function updateGameUI() {
    document.getElementById('g-score').innerText  = game.score;
    document.getElementById('g-level').innerText  = game.level;
    document.getElementById('g-streak').innerText = game.streak;
    document.getElementById('g-lives').innerText  = '❤️'.repeat(game.lives) + '🖤'.repeat(Math.max(0, 3 - game.lives));
  }

  function endGame() {
    clearInterval(game.timer);
    game.running = false;
    document.getElementById('game-play').querySelector('.item-area').style.display = 'none';

    const bonus = Math.floor(game.score / 5);
    state.pontos += bonus;
    updateUI();

    let emoji = '🌱', title = 'Boa tentativa!';
    if (game.score >= 200)      { emoji='🌍'; title='Incrível! Guardião do Planeta!'; }
    else if (game.score >= 100) { emoji='🌳'; title='Muito bom! Ecologista!'; }
    else if (game.score >= 50)  { emoji='♻️'; title='Bem feito! Continue assim!'; }

    document.getElementById('go-emoji').innerText  = emoji;
    document.getElementById('go-title').innerText  = title;
    document.getElementById('go-score').innerText  = game.score;
    document.getElementById('go-bonus').innerText  = `+${bonus} pontos bônus adicionados à sua conta! 🎁`;
    document.getElementById('game-over').style.display   = 'block';
    document.getElementById('start-btn').style.display   = 'inline-block';
    showToast(`+${bonus} pontos bônus do jogo! 🎮`);
  }

  function restartGame() {
    document.getElementById('game-over').style.display = 'none';
    document.getElementById('game-play').querySelector('.item-area').style.display = 'flex';
    startGame();
  }

  // ===================== NAV =====================
  function showPage(id, btn) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
    document.getElementById('page-' + id).classList.add('active');
    if (btn) btn.classList.add('active');
    if (id !== 'game') { clearInterval(game.timer); game.running = false; }
  }

  // ===================== TOAST =====================
  function showToast(msg) {
    const t = document.getElementById('toast');
    t.innerText = msg;
    t.classList.add('show');
    setTimeout(() => t.classList.remove('show'), 3000);
  }

  // ===================== DESCARTE — DATA =====================
  const wasteTypes = [
    { id:'papel',     title:'Papel',           sub:'Lixeira Azul',          emoji:'📄', bin:'🔵', accent:'#3498db',
      ok:['Jornais e revistas','Caixas de papelão secas','Papel de escritório','Cadernos sem espiral','Envelopes sem plástico','Folhas de caderno'],
      no:['Papel higiênico usado','Guardanapo sujo','Papel com resto de alimento','Papel carbono','Papel plastificado'] },
    { id:'plastico',  title:'Plástico',         sub:'Lixeira Vermelha',      emoji:'♻️', bin:'🔴', accent:'#e74c3c',
      ok:['Garrafas PET','Sacolas e embalagens plásticas','Potes de sorvete/margarina','Frascos de produtos de limpeza','Canudos','Tampinhas plásticas'],
      no:['Fraldas descartáveis','Isopor com alimento','Absorventes','Embalagens com resíduo de alimento','Plástico filme sujo'] },
    { id:'vidro',     title:'Vidro',            sub:'Lixeira Verde',         emoji:'🍶', bin:'🟢', accent:'#27ae60',
      ok:['Garrafas de vidro','Potes de geleia/conservas','Frascos de perfume','Copos de vidro','Espelhos','Vidros de janela (cuidado com cortes)'],
      no:['Vidro quebrado sem proteção','Lâmpadas fluorescentes','Cristal com chumbo','Espelhos com mercúrio','Vidros de carro'] },
    { id:'metal',     title:'Metal',            sub:'Lixeira Amarela',       emoji:'🥫', bin:'🟡', accent:'#f39c12',
      ok:['Latas de alumínio','Latas de aço (feijão, milho)','Tampas metálicas','Papel-alumínio limpo','Panelas velhas','Arames e pregos'],
      no:['Latas com resíduo de tinta','Embalagens de agrotóxico','Latas com produto inflamável','Esponjas de aço usadas','Pilhas e baterias'] },
    { id:'organico',  title:'Orgânico',         sub:'Lixeira Marrom',        emoji:'🌿', bin:'🟤', accent:'#8B4513',
      ok:['Cascas de frutas e legumes','Borra de café e filtro de papel','Sobras de alimentos','Folhas e galhos pequenos','Cascas de ovo','Cabelos e pelos'],
      no:['Carne ou ossos (atraem pragas)','Óleo de cozinha','Laticínios em excesso','Embalagens plásticas','Fezes de animais'] },
    { id:'eletronico',title:'Eletrônicos',      sub:'Ponto de Coleta Especial',emoji:'💻',bin:'🔷', accent:'#e67e22',
      ok:['Celulares antigos','Computadores e notebooks','Tablets e e-readers','Televisores','Impressoras e periféricos','Carregadores e cabos'],
      no:['Lixo comum (nunca!)','Lixeiras de metal/plástico','Incineração caseira','Descarte em terrenos','Lixeiras de papel'] },
    { id:'pilhas',    title:'Pilhas & Baterias',sub:'Descarte Especial',     emoji:'🔋', bin:'⚠️', accent:'#9b59b6',
      ok:['Pilhas AA, AAA, C, D','Baterias de celular','Baterias de notebook','Pilhas de relógio','Baterias recarregáveis'],
      no:['Lixo doméstico (tóxico!)','Lixeiras comuns','Descartar no chão','Queimar (libera mercúrio)','Esgoto ou bueiros'] },
    { id:'oleo',      title:'Óleo de Cozinha', sub:'Coleta Específica',      emoji:'🫙', bin:'🟠', accent:'#00bcd4',
      ok:['Óleo vegetal usado','Gordura de fritura','Azeite vencido','Banha reutilizada'],
      no:['Despejar na pia (entope)','Jogar no vaso sanitário','Descarte no lixo seco','Jogar no chão ou gramado','Misturar com água na fossa'] },
  ];

  const searchDB = [
    { terms:['jornal','revista','papel','papelão','caixa','caderno','folha','envelope','impressão','brochura','livro','catálogo'], type:'papel' },
    { terms:['garrafa pet','garrafa','plástico','sacola','pote','isopor','canudo','tampa','embalagem','frascos','copo plástico','tupperware'], type:'plastico' },
    { terms:['vidro','garrafa de vidro','pote de vidro','frasco','espelho','xícara de vidro','copo de vidro','janela'], type:'vidro' },
    { terms:['lata','alumínio','ferro','metal','panela','arame','prego','tampa metálica','papel alumínio','aço','latinha'], type:'metal' },
    { terms:['casca','banana','fruta','legume','resto de comida','sobra','alimento','borra de café','folha seca','galho','ovo','cabelo','pelo'], type:'organico' },
    { terms:['celular','computador','notebook','tablet','tv','televisão','impressora','roteador','teclado','mouse','monitor','eletrônico','eletrodoméstico'], type:'eletronico' },
    { terms:['pilha','bateria','bateria de celular','bateria de carro','pilha aa','pilha recarregável'], type:'pilhas' },
    { terms:['óleo','azeite','gordura','fritura','banha'], type:'oleo' },
  ];

  // ===================== DESCARTE — CHALLENGES =====================
  let challenges = { ch1:false, ch2:false, ch3:false, ch4:false, ch5:false };
  let expandedCards = new Set();
  let quizAnswered = 0, quizStreak = 0;

  function checkChallenge(id) {
    if (challenges[id]) return;
    challenges[id] = true;
    document.getElementById(id).classList.add('done');
    updateProgress();
    const tip = document.getElementById(id).dataset.tip;
    showToast('🏆 Desafio desbloqueado! ' + tip);
    // bonus points
    state.pontos += 25;
    updateUI();
  }

  function updateProgress() {
    const done  = Object.values(challenges).filter(Boolean).length;
    const total = 5;
    document.getElementById('challenge-pts').textContent  = done + ' / ' + total + ' concluídos';
    document.getElementById('challenge-bar').style.width  = (done / total * 100) + '%';
    const labels = [
      'Complete desafios para subir de nível ecológico! 🌱',
      'Ótimo começo! Continue! 🌿',
      'Na metade — você é incrível! ♻️',
      'Quase lá! Mais um desafio! 🌳',
      '🌍 Parabéns, Guardião do Planeta!'
    ];
    document.getElementById('challenge-label').textContent = labels[done] || labels[4];
  }

  // ===================== DESCARTE — CARDS =====================
  function buildCards() {
    const grid = document.getElementById('waste-cards');
    wasteTypes.forEach(w => {
      const card = document.createElement('div');
      card.className = 'waste-card';
      card.id = 'card-' + w.id;
      card.style.setProperty('--accent', w.accent);
      card.innerHTML = `
        <span class="card-emoji">${w.emoji}</span>
        <span class="card-bin-icon">${w.bin}</span>
        <div class="card-title">${w.title}</div>
        <div class="card-subtitle">${w.sub}</div>
        <div class="card-detail" id="detail-${w.id}">
          <div class="detail-block">
            <strong>✅ Pode descartar:</strong>
            <ul class="ok-list">${w.ok.map(i=>`<li>${i}</li>`).join('')}</ul>
          </div>
          <div class="detail-block">
            <strong>❌ NÃO pode:</strong>
            <ul class="no-list">${w.no.map(i=>`<li>${i}</li>`).join('')}</ul>
          </div>
        </div>
      `;
      card.onclick = () => toggleCard(w.id);
      grid.appendChild(card);
    });
  }

  function toggleCard(id) {
    const detail = document.getElementById('detail-' + id);
    const card   = document.getElementById('card-' + id);
    const isOpen = detail.classList.contains('open');

    document.querySelectorAll('.card-detail').forEach(d => d.classList.remove('open'));
    document.querySelectorAll('.waste-card').forEach(c => c.classList.remove('expanded'));

    if (!isOpen) {
      detail.classList.add('open');
      card.classList.add('expanded');
      expandedCards.add(id);
      if (expandedCards.size >= 3) checkChallenge('ch2');
    }
  }

  // ===================== DESCARTE — SEARCH =====================
  function doSearch() {
    const raw = document.getElementById('search-input').value.trim().toLowerCase();
    const res = document.getElementById('search-result');
    if (!raw) return;
    checkChallenge('ch1');

    let found = null;
    for (const entry of searchDB) {
      if (entry.terms.some(t => raw.includes(t) || t.includes(raw))) { found = entry; break; }
    }

    if (!found) {
      res.style.display = 'block';
      res.innerHTML = `<div class="result-notfound">🤔 Não encontramos "${raw}". Tente: garrafa, casca de banana, lata, celular, pilha, óleo…</div>`;
      return;
    }

    const w  = wasteTypes.find(x => x.id === found.type);
    const bg = { papel:'#ebf5fb', plastico:'#fdecea', vidro:'#eafaf1', metal:'#fef9e7', organico:'#fdf2f8', eletronico:'#fef9e7', pilhas:'#f4ecf7', oleo:'#e8f8f5' }[w.id] || '#f0fdf4';

    res.style.display = 'block';
    res.innerHTML = `
      <div class="result-box" style="background:${bg}">
        <span class="result-icon">${w.emoji}</span>
        <div class="result-info">
          <h4>Descarte em: ${w.sub} ${w.bin}</h4>
          <p>${w.ok[0]} e outros itens similares devem ir para a lixeira de ${w.title}.</p>
        </div>
      </div>`;
    showToast('✅ Encontrado! ' + w.title + ' → ' + w.sub);
  }

  // ===================== DESCARTE — QUIZ =====================
  const quizQuestions = [
    { q:'Onde deve ser descartada uma garrafa PET?', opts:['Lixeira Azul','Lixeira Vermelha','Lixeira Marrom','Lixo Orgânico'], ans:1, exp:'Garrafas PET são plástico → lixeira VERMELHA.' },
    { q:'Casca de banana deve ir para qual lixeira?', opts:['Lixeira Verde','Lixeira Azul','Lixeira Marrom','Lixeira Vermelha'], ans:2, exp:'Resíduos orgânicos como cascas vão para a lixeira MARROM.' },
    { q:'Uma pilha usada deve ser descartada:', opts:['Na lixeira comum','No lixo orgânico','Em ponto de coleta especial','Na lixeira azul'], ans:2, exp:'Pilhas contêm metais tóxicos e exigem descarte especial!' },
    { q:'Qual é a cor da lixeira correta para jornal e papelão?', opts:['Amarela','Vermelha','Verde','Azul'], ans:3, exp:'Papel e papelão vão na lixeira AZUL.' },
    { q:'O óleo de cozinha usado NUNCA deve ser:', opts:['Coletado em garrafa pet','Entregue em ponto de coleta','Despejado na pia ou vaso','Reciclado em biodiesel'], ans:2, exp:'Óleo na pia entope encanamentos e polui rios e solos!' },
    { q:'Para onde vão computadores e celulares velhos?', opts:['Lixeira Amarela','Ponto de coleta de eletrônicos','Lixeira Azul','Lixo orgânico'], ans:1, exp:'Eletrônicos têm substâncias tóxicas e precisam de coleta especializada.' },
    { q:'Lata de alumínio (latinha de refrigerante) é:', opts:['Orgânico','Plástico','Metal','Vidro'], ans:2, exp:'Latas de alumínio são metais → lixeira AMARELA.' },
    { q:'Um pote de vidro de geleia deve ir para a lixeira:', opts:['Vermelha','Amarela','Verde','Marrom'], ans:2, exp:'Vidro vai na lixeira VERDE, preferencialmente limpo.' },
    { q:'Papel higiênico usado deve ir:', opts:['Lixeira Azul (papel)','Lixo comum (não reciclável)','Lixeira Marrom','Lixeira Vermelha'], ans:1, exp:'Papel higiênico sujo não pode ser reciclado, vai no lixo comum.' },
    { q:'Por que é importante separar o lixo?', opts:['Para a casa ficar mais organizada','Para facilitar a reciclagem e reduzir poluição','Porque é obrigatório','Para ganhar dinheiro'], ans:1, exp:'A coleta seletiva viabiliza a reciclagem e protege o meio ambiente.' },
  ];

  let qIndex = 0, qCorrect = 0, qStreak = 0, qAnswered = false;
  let quizShuffled = [];

  function shuffleQuiz() {
    quizShuffled = [...quizQuestions].sort(() => Math.random() - 0.5);
    qIndex = 0; qCorrect = 0; qStreak = 0; qAnswered = false;
  }

  function loadQuestion() {
    const q = quizShuffled[qIndex];
    document.getElementById('q-num').textContent   = qIndex + 1;
    document.getElementById('q-score').textContent = qCorrect * 10;
    document.getElementById('quiz-prog').style.width = ((qIndex + 1) / quizShuffled.length * 100) + '%';
    document.getElementById('q-text').textContent  = q.q;
    document.getElementById('q-feedback').classList.remove('show','certo','errado');
    document.getElementById('q-next').disabled = true;
    qAnswered = false;

    const optDiv = document.getElementById('q-options');
    optDiv.innerHTML = '';
    q.opts.forEach((opt, i) => {
      const btn = document.createElement('button');
      btn.className = 'option-btn';
      btn.textContent = opt;
      btn.onclick = () => answerQuiz(i);
      optDiv.appendChild(btn);
    });
  }

  function answerQuiz(chosen) {
    if (qAnswered) return;
    qAnswered = true;
    const q    = quizShuffled[qIndex];
    const btns = document.querySelectorAll('.option-btn');
    btns.forEach(b => b.disabled = true);
    btns[q.ans].classList.add('correct');

    const fb = document.getElementById('q-feedback');
    if (chosen === q.ans) {
      btns[chosen].classList.add('correct');
      qCorrect++; qStreak++; quizAnswered++;
      fb.textContent  = '✅ Correto! ' + q.exp;
      fb.className    = 'quiz-feedback certo show';
      if (quizAnswered >= 5) checkChallenge('ch3');
      if (qStreak >= 3) checkChallenge('ch4');
    } else {
      btns[chosen].classList.add('wrong');
      qStreak = 0;
      fb.textContent = '❌ Errado. ' + q.exp;
      fb.className   = 'quiz-feedback errado show';
    }
    document.getElementById('q-next').disabled     = false;
    document.getElementById('q-score').textContent = qCorrect * 10;
  }

  function nextQuestion() {
    qIndex++;
    if (qIndex >= quizShuffled.length) { showQuizResult(); return; }
    loadQuestion();
  }

  function showQuizResult() {
    document.getElementById('quiz-area').style.display   = 'none';
    document.getElementById('quiz-result').style.display = 'block';
    document.getElementById('r-score').textContent       = qCorrect;

    let emoji = '🌱', title = 'Continue praticando!';
    if (qCorrect === 10)     { emoji='🌟'; title='Perfeito! Mestre da Reciclagem!'; checkChallenge('ch5'); }
    else if (qCorrect >= 8)  { emoji='🌍'; title='Excelente! Guardião do Planeta!'; }
    else if (qCorrect >= 6)  { emoji='🌳'; title='Muito bom! Ecologista de verdade!'; }
    else if (qCorrect >= 4)  { emoji='♻️'; title='Bom trabalho! Continue aprendendo!'; }

    document.getElementById('r-emoji').textContent = emoji;
    document.getElementById('r-title').textContent = title;

    // bonus de pontos pelo quiz
    const bonus = qCorrect * 5;
    state.pontos += bonus;
    updateUI();
    showToast(`Quiz concluído! ${qCorrect}/10 acertos — +${bonus} pontos! 🎉`);
  }

  function resetQuiz() {
    document.getElementById('quiz-area').style.display   = 'block';
    document.getElementById('quiz-result').style.display = 'none';
    shuffleQuiz();
    loadQuestion();
  }

  // ===================== INIT =====================
  buildCards();
  shuffleQuiz();
  loadQuestion();

  // ===================== SPLASH =====================
  function iniciarApp() {
    const splash = document.getElementById('splash');
    splash.classList.add('hiding');
    setTimeout(() => {
      splash.style.display = 'none';
      document.getElementById('app-shell').style.display = 'block';
    }, 700);
  }

  // Generate floating leaves
  (function() {
    const container = document.getElementById('splash-leaves');
    const leafEmojis = ['🍃','🌿','🌱','♻️','🍀'];
    for (let i = 0; i < 18; i++) {
      const el = document.createElement('span');
      el.className = 'splash-leaf';
      el.textContent = leafEmojis[i % leafEmojis.length];
      el.style.left = (Math.random() * 100) + '%';
      el.style.animationDuration = (8 + Math.random() * 12) + 's';
      el.style.animationDelay = '-' + (Math.random() * 15) + 's';
      el.style.fontSize = (1.5 + Math.random() * 2) + 'rem';
      container.appendChild(el);
    }
  })();
</script>
</body>
</html>
