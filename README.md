ash

cat > /mnt/user-data/outputs/ecorecicla-descarte.html << 'HTMLEOF'
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EcoRecicla — Descarte Correto</title>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --verde: #2d6a4f;
      --verde-medio: #40916c;
      --verde-claro: #74c69d;
      --verde-palido: #d8f3dc;
      --amarelo: #f9c74f;
      --laranja: #f77f00;
      --branco: #ffffff;
      --cinza: #f8f9fa;
      --texto: #1b2d27;
      --sombra: 0 8px 32px rgba(45,106,79,0.13);
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Nunito', sans-serif;
      background: linear-gradient(160deg, #e9f7ef 0%, #d8f3dc 60%, #b7e4c7 100%);
      min-height: 100vh;
      color: var(--texto);
    }

    /* ===== NAV ===== */
    nav {
      background: var(--verde);
      padding: 0 28px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      position: sticky;
      top: 0;
      z-index: 200;
      box-shadow: 0 4px 24px rgba(0,0,0,0.18);
    }
    .nav-logo {
      font-family: 'Fredoka One', cursive;
      color: #fff;
      font-size: 1.55rem;
      padding: 14px 0;
      letter-spacing: 1px;
    }
    .nav-logo span { color: var(--amarelo); }
    .nav-links { display: flex; gap: 4px; flex-wrap: wrap; }
    .nav-btn {
      background: none; border: none;
      color: rgba(255,255,255,0.75);
      font-family: 'Nunito', sans-serif;
      font-size: 0.92rem; font-weight: 700;
      padding: 10px 14px; border-radius: 8px;
      cursor: pointer; transition: all 0.2s;
    }
    .nav-btn:hover, .nav-btn.active {
      background: rgba(255,255,255,0.18);
      color: #fff;
    }
    .nav-pontos {
      background: var(--amarelo); color: var(--verde);
      font-weight: 800; font-size: 0.88rem;
      padding: 7px 15px; border-radius: 20px;
      white-space: nowrap;
    }

    /* ===== LAYOUT ===== */
    .page { display: none; }
    .page.active { display: block; animation: fadeIn 0.4s ease; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }
    .container { max-width: 920px; margin: 0 auto; padding: 32px 18px 60px; }

    /* ===== PAGE HEADER ===== */
    .page-hero {
      background: linear-gradient(135deg, #1b4332 0%, var(--verde) 55%, var(--verde-medio) 100%);
      border-radius: 26px;
      padding: 42px 36px;
      color: #fff;
      margin-bottom: 32px;
      position: relative;
      overflow: hidden;
    }
    .page-hero::before {
      content: '';
      position: absolute; inset: 0;
      background: url("data:image/svg+xml,%3Csvg width='80' height='80' viewBox='0 0 80 80' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.04'%3E%3Cpath d='M50 50c0-5.523 4.477-10 10-10s10 4.477 10 10-4.477 10-10 10c0 5.523-4.477 10-10 10s-10-4.477-10-10 4.477-10 10-10zM10 10c0-5.523 4.477-10 10-10s10 4.477 10 10-4.477 10-10 10c0 5.523-4.477 10-10 10S0 25.523 0 20s4.477-10 10-10zm40 0c0-5.523 4.477-10 10-10s10 4.477 10 10-4.477 10-10 10c0 5.523-4.477 10-10 10S40 25.523 40 20s4.477-10 10-10z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
      pointer-events: none;
    }
    .page-hero .leaf-deco {
      position: absolute; right: 28px; top: 50%; transform: translateY(-50%);
      font-size: 8rem; opacity: 0.12; pointer-events: none;
    }
    .page-hero h1 {
      font-family: 'Fredoka One', cursive;
      font-size: 2.4rem; margin-bottom: 10px; position: relative;
    }
    .page-hero p { font-size: 1.05rem; opacity: 0.88; max-width: 460px; position: relative; }

    /* ===== PROGRESS BAR ===== */
    .progress-section {
      background: #fff;
      border-radius: 20px;
      padding: 22px 26px;
      box-shadow: var(--sombra);
      margin-bottom: 30px;
    }
    .progress-top {
      display: flex; justify-content: space-between; align-items: center;
      margin-bottom: 10px;
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

    /* ===== SEARCH ===== */
    .search-section {
      background: #fff;
      border-radius: 20px;
      padding: 26px;
      box-shadow: var(--sombra);
      margin-bottom: 30px;
    }
    .search-section h3 {
      font-family: 'Fredoka One', cursive;
      color: var(--verde); font-size: 1.25rem; margin-bottom: 6px;
    }
    .search-section p { color: #888; font-size: 0.9rem; margin-bottom: 16px; }
    .search-row {
      display: flex; gap: 10px;
    }
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
    .btn-search:hover { transform: translateY(-2px); box-shadow: 0 8px 22px rgba(64,145,108,0.45); }
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
    .result-notfound { background: #fff3cd; border-left: 4px solid var(--amarelo); border-radius: 0 12px 12px 0; padding: 14px 18px; color: #856404; font-weight: 700; }

    /* ===== CARDS GRID ===== */
    .section-title {
      font-family: 'Fredoka One', cursive;
      color: var(--verde); font-size: 1.6rem;
      margin-bottom: 6px;
    }
    .section-sub { color: #666; font-size: 0.95rem; margin-bottom: 22px; }
    .cards-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 18px;
      margin-bottom: 36px;
    }
    .waste-card {
      background: #fff;
      border-radius: 20px;
      padding: 24px 18px 20px;
      box-shadow: var(--sombra);
      text-align: center;
      cursor: pointer;
      border: 3px solid transparent;
      transition: transform 0.25s cubic-bezier(0.34,1.4,0.64,1),
                  box-shadow 0.25s ease,
                  border-color 0.2s;
      position: relative;
      overflow: hidden;
    }
    .waste-card::before {
      content: '';
      position: absolute; top: 0; left: 0; right: 0;
      height: 5px;
      border-radius: 20px 20px 0 0;
    }
    .waste-card:hover {
      transform: translateY(-8px) scale(1.03);
      box-shadow: 0 18px 48px rgba(45,106,79,0.18);
    }
    .waste-card:hover .card-bin-icon { transform: scale(1.18) rotate(-5deg); }
    .waste-card.expanded { border-color: var(--verde-claro); }
    .card-emoji { font-size: 3rem; margin-bottom: 8px; display: block; }
    .card-bin-icon {
      font-size: 2rem; margin-bottom: 6px; display: block;
      transition: transform 0.3s cubic-bezier(0.34,1.5,0.64,1);
    }
    .card-title { font-family: 'Fredoka One', cursive; font-size: 1.15rem; margin-bottom: 4px; }
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

    /* card theme colors */
    .card-azul   ::before, .card-azul   { --accent: #3498db; }
    .card-vermelho::before, .card-vermelho { --accent: #e74c3c; }
    .card-verde  ::before, .card-verde   { --accent: #27ae60; }
    .card-amarelo::before, .card-amarelo { --accent: #f39c12; }
    .card-marrom ::before, .card-marrom  { --accent: #8B4513; }
    .card-laranja::before, .card-laranja { --accent: #e67e22; }
    .card-roxo   ::before, .card-roxo    { --accent: #9b59b6; }
    .card-ciano  ::before, .card-ciano   { --accent: #00bcd4; }

    .waste-card::before { background: var(--accent, #aaa); }
    .waste-card:hover { border-color: var(--accent, var(--verde-claro)) !important; }
    .card-title { color: var(--accent, var(--verde)); }

    /* ===== QUIZ ===== */
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
      color: var(--texto); margin-bottom: 20px;
      line-height: 1.5;
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
    .quiz-result {
      display: none; text-align: center; padding: 20px;
    }
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
      position: fixed; bottom: 24px; left: 50%;
      transform: translateX(-50%) translateY(80px);
      background: var(--verde); color: #fff;
      font-weight: 700; padding: 12px 26px;
      border-radius: 40px; box-shadow: 0 8px 24px rgba(0,0,0,0.2);
      z-index: 999; transition: transform 0.4s cubic-bezier(0.34,1.5,0.64,1);
      white-space: nowrap; font-size: 0.95rem;
    }
    .toast.show { transform: translateX(-50%) translateY(0); }

    /* ===== RESPONSIVE ===== */
    @media (max-width: 640px) {
      .cards-grid { grid-template-columns: repeat(2, 1fr); }
      .options-grid { grid-template-columns: 1fr; }
      .page-hero h1 { font-size: 1.75rem; }
      .page-hero .leaf-deco { display: none; }
      .search-row { flex-direction: column; }
      nav { padding: 0 14px; }
      .nav-links { gap: 2px; }
      .nav-btn { padding: 8px 10px; font-size: 0.82rem; }
    }
  </style>
</head>
<body>

<nav>
  <div class="nav-logo">🌱 Eco<span>Recicla</span></div>
  <div class="nav-links">
    <button class="nav-btn" onclick="showPage('home',this)">♻️ Início</button>
    <button class="nav-btn" onclick="showPage('noticias',this)">📰 Notícias</button>
    <button class="nav-btn" onclick="showPage('game',this)">🎮 Jogo</button>
    <button class="nav-btn active" onclick="showPage('descarte',this)">🗑️ Descarte</button>
  </div>
  <div class="nav-pontos">⭐ <span id="nav-pts">0</span> pts</div>
</nav>

<!-- ===== OUTRAS PÁGINAS (placeholder) ===== -->
<div id="page-home"     class="page"><div style="padding:60px;text-align:center;color:#888;font-size:1.1rem;">← Conteúdo original do EcoRecicla aqui</div></div>
<div id="page-noticias" class="page"><div style="padding:60px;text-align:center;color:#888;font-size:1.1rem;">← Seção de Notícias aqui</div></div>
<div id="page-game"     class="page"><div style="padding:60px;text-align:center;color:#888;font-size:1.1rem;">← Jogo da Reciclagem aqui</div></div>

<!-- ===== DESCARTE CORRETO PAGE ===== -->
<div id="page-descarte" class="page active">
<div class="container">

  <!-- HERO -->
  <div class="page-hero">
    <div class="leaf-deco">🌿</div>
    <h1>♻️ Descarte Correto</h1>
    <p>Aprenda onde jogar cada tipo de lixo e ajude a proteger o meio ambiente de forma fácil e divertida!</p>
  </div>

  <!-- PROGRESSO DE DESAFIOS -->
  <div class="progress-section">
    <div class="progress-top">
      <h3>🏆 Seus Desafios Sustentáveis</h3>
      <div class="pts-badge" id="challenge-pts">0 / 5 concluídos</div>
    </div>
    <div class="prog-bar-wrap">
      <div class="prog-bar" id="challenge-bar" style="width:0%"></div>
    </div>
    <div class="prog-label" id="challenge-label">Complete desafios para subir de nível ecológico! 🌱</div>
    <div class="challenges-row">
      <div class="ch-badge" id="ch1" data-tip="Pesquisar um objeto">🔍 Primeira Pesquisa</div>
      <div class="ch-badge" id="ch2" data-tip="Ver detalhes de 3 lixeiras">🗑️ Explorador de Lixeiras</div>
      <div class="ch-badge" id="ch3" data-tip="Responder 5 perguntas do quiz">📝 Quizeiro</div>
      <div class="ch-badge" id="ch4" data-tip="Acertar 3 seguidas no quiz">✅ Acertador Nato</div>
      <div class="ch-badge" id="ch5" data-tip="Terminar o quiz com 100%">🌟 Mestre da Reciclagem</div>
    </div>
  </div>

  <!-- BUSCADOR -->
  <div class="search-section">
    <h3>🔍 Onde Descartar?</h3>
    <p>Digite um objeto e descubra imediatamente como descartá-lo corretamente:</p>
    <div class="search-row">
      <input type="text" class="search-input" id="search-input" placeholder="Ex: garrafa PET, casca de banana, pilha, celular…" onkeydown="if(event.key==='Enter')doSearch()">
      <button class="btn-search" onclick="doSearch()">🔍 Buscar</button>
    </div>
    <div id="search-result"></div>
  </div>

  <!-- CARDS DE RESÍDUOS -->
  <h2 class="section-title">🗑️ Tipos de Resíduos</h2>
  <p class="section-sub">Clique em cada card para ver o que pode e não pode ser descartado naquela lixeira.</p>

  <div class="cards-grid" id="waste-cards"></div>

  <!-- QUIZ -->
  <div class="quiz-section">
    <div class="quiz-header">
      <h3>📝 Quiz de Reciclagem</h3>
      <div class="quiz-meta">
        <div class="quiz-badge">❓ <span id="q-num">1</span>/10</div>
        <div class="quiz-badge" style="background:#fff9c4;color:#856404;">⭐ <span id="q-score">0</span> pts</div>
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
      <p id="r-msg">Você acertou <strong id="r-score">0</strong> de 10 perguntas!</p>
      <button class="btn-replay" onclick="resetQuiz()">🔄 Jogar Novamente</button>
    </div>
  </div>

</div><!-- /container -->
</div><!-- /page-descarte -->

<div class="toast" id="toast"></div>

<script>
// ==================== DATA ====================
const wasteTypes = [
  {
    id: 'papel', title: 'Papel', sub: 'Lixeira Azul', emoji: '📄', bin: '🔵',
    color: 'card-azul',
    ok:  ['Jornais e revistas', 'Caixas de papelão secas', 'Papel de escritório', 'Cadernos sem espiral', 'Envelopes sem plástico', 'Folhas de caderno'],
    no:  ['Papel higiênico usado', 'Guardanapo sujo', 'Papel com resto de alimento', 'Papel carbono', 'Papel plastificado']
  },
  {
    id: 'plastico', title: 'Plástico', sub: 'Lixeira Vermelha', emoji: '♻️', bin: '🔴',
    color: 'card-vermelho',
    ok:  ['Garrafas PET', 'Sacolas e embalagens plásticas', 'Potes de sorvete/margarina', 'Frascos de produtos de limpeza', 'Canudos', 'Tampinhas plásticas'],
    no:  ['Fraldas descartáveis', 'Isopor com alimento', 'Absorventes', 'Embalagens com resíduo de alimento', 'Plástico filme sujo']
  },
  {
    id: 'vidro', title: 'Vidro', sub: 'Lixeira Verde', emoji: '🍶', bin: '🟢',
    color: 'card-verde',
    ok:  ['Garrafas de vidro', 'Potes de geleia/conservas', 'Frascos de perfume', 'Copos de vidro', 'Espelhos', 'Vidros de janela (cuidado com cortes)'],
    no:  ['Vidro quebrado sem proteção', 'Lâmpadas fluorescentes', 'Cristal com chumbo', 'Espelhos com mercúrio', 'Vidros de carro']
  },
  {
    id: 'metal', title: 'Metal', sub: 'Lixeira Amarela', emoji: '🥫', bin: '🟡',
    color: 'card-amarelo',
    ok:  ['Latas de alumínio', 'Latas de aço (feijão, milho)', 'Tampas metálicas', 'Papel-alumínio limpo', 'Panelas velhas', 'Arames e pregos'],
    no:  ['Latas com resíduo de tinta', 'Embalagens de agrotóxico', 'Latas com produto inflamável', 'Esponjas de aço usadas', 'Pilhas e baterias']
  },
  {
    id: 'organico', title: 'Orgânico', sub: 'Lixeira Marrom', emoji: '🌿', bin: '🟤',
    color: 'card-marrom',
    ok:  ['Cascas de frutas e legumes', 'Borra de café e filtro de papel', 'Sobras de alimentos', 'Folhas e galhos pequenos', 'Cascas de ovo', 'Cabelos e pelos'],
    no:  ['Carne ou ossos (atraem pragas)', 'Óleo de cozinha', 'Laticínios em excesso', 'Embalagens plásticas', 'Fezes de animais']
  },
  {
    id: 'eletronico', title: 'Eletrônicos', sub: 'Ponto de Coleta Especial', emoji: '💻', bin: '🔷',
    color: 'card-laranja',
    ok:  ['Celulares antigos', 'Computadores e notebooks', 'Tablets e e-readers', 'Televisores', 'Impressoras e periféricos', 'Carregadores e cabos'],
    no:  ['Lixo comum (nunca!)', 'Lixeiras de metal/plástico', 'Incineração caseira', 'Descarte em terrenos', 'Lixeiras de papel']
  },
  {
    id: 'pilhas', title: 'Pilhas & Baterias', sub: 'Descarte Especial', emoji: '🔋', bin: '⚠️',
    color: 'card-roxo',
    ok:  ['Pilhas AA, AAA, C, D', 'Baterias de celular', 'Baterias de notebook', 'Pilhas de relógio', 'Baterias recarregáveis'],
    no:  ['Lixo doméstico (tóxico!)', 'Lixeiras comuns', 'Descartar no chão', 'Queimar (libera mercúrio)', 'Esgoto ou bueiros']
  },
  {
    id: 'oleo', title: 'Óleo de Cozinha', sub: 'Coleta Específica', emoji: '🫙', bin: '🟠',
    color: 'card-ciano',
    ok:  ['Óleo vegetal usado', 'Gordura de fritura', 'Azeite vencido', 'Banha reutilizada'],
    no:  ['Despejar na pia (entope)', 'Jogar no vaso sanitário', 'Descarte no lixo seco', 'Jogar no chão ou gramado', 'Misturar com água na fossa']
  },
];

const searchDB = [
  // papel
  {terms:['jornal','revista','papel','papelão','caixa','caderno','folha','envelope','impressão','brochura','livro','catálogo'],type:'papel'},
  // plastico
  {terms:['garrafa pet','garrafa','plástico','sacola','pote','isopor','canudo','tampa','embalagem','frascos','copo plástico','tupperware'],type:'plastico'},
  // vidro
  {terms:['vidro','garrafa de vidro','pote de vidro','frasco','espelho','xícara de vidro','copo de vidro','janela'],type:'vidro'},
  // metal
  {terms:['lata','alumínio','ferro','metal','panela','arame','prego','Tampa metálica','papel alumínio','aço','latinha'],type:'metal'},
  // organico
  {terms:['casca','banana','fruta','legume','resto de comida','sobra','alimento','borra de café','folha seca','galho','ovo','cabelo','pelo'],type:'organico'},
  // eletronico
  {terms:['celular','computador','notebook','tablet','tv','televisão','impressora','roteador','teclado','mouse','monitor','eletrônico','eletrodoméstico'],type:'eletronico'},
  // pilhas
  {terms:['pilha','bateria','bateria de celular','bateria de carro','pilha aa','pilha recarregável'],type:'pilhas'},
  // oleo
  {terms:['óleo','azeite','gordura','fritura','banha'],type:'oleo'},
];

// ==================== CHALLENGES ====================
let challenges = { ch1:false, ch2:false, ch3:false, ch4:false, ch5:false };
let expandedCards = new Set();
let quizAnswered = 0, quizStreak = 0, quizScore = 0;

function checkChallenge(id) {
  if (challenges[id]) return;
  challenges[id] = true;
  document.getElementById(id).classList.add('done');
  updateProgress();
  showToast('🏆 Desafio desbloqueado! ' + document.getElementById(id).dataset.tip);
}

function updateProgress() {
  const done = Object.values(challenges).filter(Boolean).length;
  const total = 5;
  document.getElementById('challenge-pts').textContent = done + ' / ' + total + ' concluídos';
  document.getElementById('challenge-bar').style.width = (done / total * 100) + '%';
  const labels = ['Comece explorando o site! 🌱','Ótimo começo! Continue! 🌿','Na metade — você é incrível! ♻️','Quase lá! Mais um desafio! 🌳','🌍 Parabéns, Guardião do Planeta!'];
  document.getElementById('challenge-label').textContent = labels[done] || labels[4];
  document.getElementById('nav-pts').textContent = done * 25;
}

// ==================== CARDS ====================
function buildCards() {
  const grid = document.getElementById('waste-cards');
  wasteTypes.forEach(w => {
    const card = document.createElement('div');
    card.className = 'waste-card ' + w.color;
    card.id = 'card-' + w.id;
    card.innerHTML = `
      <span class="card-emoji">${w.emoji}</span>
      <span class="card-bin-icon">${w.bin}</span>
      <div class="card-title">${w.title}</div>
      <div class="card-subtitle">${w.sub}</div>
      <div class="card-detail" id="detail-${w.id}">
        <div class="detail-block">
          <strong style="color:#27ae60;">✅ Pode descartar:</strong>
          <ul class="ok-list">${w.ok.map(i=>`<li>${i}</li>`).join('')}</ul>
        </div>
        <div class="detail-block">
          <strong style="color:#c0392b;">❌ NÃO pode:</strong>
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
  // close all
  document.querySelectorAll('.card-detail').forEach(d => d.classList.remove('open'));
  document.querySelectorAll('.waste-card').forEach(c => c.classList.remove('expanded'));
  if (!isOpen) {
    detail.classList.add('open');
    card.classList.add('expanded');
    expandedCards.add(id);
    if (expandedCards.size >= 3) checkChallenge('ch2');
  }
}

// ==================== SEARCH ====================
function doSearch() {
  const raw   = document.getElementById('search-input').value.trim().toLowerCase();
  const res   = document.getElementById('search-result');
  if (!raw) return;

  checkChallenge('ch1');

  let found = null;
  for (const entry of searchDB) {
    if (entry.terms.some(t => raw.includes(t) || t.includes(raw))) { found = entry; break; }
  }

  if (!found) {
    res.style.display = 'block';
    res.innerHTML = `<div class="result-notfound">🤔 Não encontramos "${raw}". Tente palavras como: garrafa, casca de banana, lata, celular, pilha, óleo…</div>`;
    return;
  }

  const w = wasteTypes.find(x => x.id === found.type);
  const bgMap = {
    paper:'#ebf5fb',plastico:'#fdecea',vidro:'#eafaf1',metal:'#fef9e7',
    organico:'#f5eef8',eletronico:'#fef5e7',pilhas:'#f4ecf7',oleo:'#e8f8f5'
  };
  const bg = { papel:'#ebf5fb',plastico:'#fdecea',vidro:'#eafaf1',metal:'#fef9e7',
               organico:'#fdf2f8',eletronico:'#fef9e7',pilhas:'#f4ecf7',oleo:'#e8f8f5' }[w.id] || '#f0fdf4';

  res.style.display = 'block';
  res.innerHTML = `
    <div class="result-box" style="background:${bg}">
      <div class="result-icon">${w.emoji}</div>
      <div class="result-info">
        <h4 style="color:var(--verde);">Descarte em: ${w.sub} ${w.bin}</h4>
        <p>${w.ok[0]} e outros itens similares devem ir para a lixeira de <strong>${w.title}</strong>.</p>
      </div>
    </div>
  `;
  showToast('✅ Encontrado! ' + w.title + ' → ' + w.sub);
}

// ==================== QUIZ ====================
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
  document.getElementById('q-num').textContent  = qIndex + 1;
  document.getElementById('q-score').textContent = qCorrect * 10;
  document.getElementById('quiz-prog').style.width = ((qIndex + 1) / quizShuffled.length * 100) + '%';
  document.getElementById('q-text').textContent = q.q;
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
  const q = quizShuffled[qIndex];
  const btns = document.querySelectorAll('.option-btn');
  btns.forEach(b => b.disabled = true);
  btns[q.ans].classList.add('correct');

  const fb = document.getElementById('q-feedback');
  if (chosen === q.ans) {
    btns[chosen].classList.add('correct');
    qCorrect++; qStreak++; quizAnswered++;
    fb.textContent = '✅ Correto! ' + q.exp;
    fb.className = 'quiz-feedback certo show';
    if (quizAnswered >= 5) checkChallenge('ch3');
    if (qStreak >= 3) checkChallenge('ch4');
  } else {
    btns[chosen].classList.add('wrong');
    qStreak = 0;
    fb.textContent = '❌ Errado. ' + q.exp;
    fb.className = 'quiz-feedback errado show';
  }
  document.getElementById('q-next').disabled = false;
  document.getElementById('q-score').textContent = qCorrect * 10;
}

function nextQuestion() {
  qIndex++;
  if (qIndex >= quizShuffled.length) {
    showQuizResult(); return;
  }
  loadQuestion();
}

function showQuizResult() {
  document.getElementById('quiz-area').style.display  = 'none';
  document.getElementById('quiz-result').style.display = 'block';
  document.getElementById('r-score').textContent = qCorrect;

  let emoji = '🌱', title = 'Continue praticando!';
  if (qCorrect === 10) { emoji='🌟'; title='Perfeito! Mestre da Reciclagem!'; checkChallenge('ch5'); }
  else if (qCorrect >= 8) { emoji='🌍'; title='Excelente! Guardião do Planeta!'; }
  else if (qCorrect >= 6) { emoji='🌳'; title='Muito bom! Ecologista de verdade!'; }
  else if (qCorrect >= 4) { emoji='♻️'; title='Bom trabalho! Continue aprendendo!'; }

  document.getElementById('r-emoji').textContent = emoji;
  document.getElementById('r-title').textContent  = title;
  showToast('Quiz concluído! ' + qCorrect + '/10 acertos 🎉');
}

function resetQuiz() {
  document.getElementById('quiz-area').style.display   = 'block';
  document.getElementById('quiz-result').style.display = 'none';
  shuffleQuiz();
  loadQuestion();
}

// ==================== NAV ====================
function showPage(id, btn) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  if (btn) btn.classList.add('active');
}

// ==================== TOAST ====================
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3200);
}

// ==================== INIT ====================
buildCards();
shuffleQuiz();
loadQuestion();
</script>
</body>
</html>
HTMLEOF
echo "Done"
Saída

Done
