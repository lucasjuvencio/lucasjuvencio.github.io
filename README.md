<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
  <title>Painel do Salão</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,500;0,700;1,400;1,500&family=Nunito:wght@300;400;500;600&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #fdf9f7;
      --surface: #ffffff;
      --rose: #c4786a;
      --rose-dark: #a85f52;
      --rose-light: #f2deda;
      --rose-pale: #fdf3f1;
      --gold: #c09a5e;
      --gold-light: #f5e9d4;
      --sage: #8fa888;
      --sage-light: #e8f0e6;
      --text: #2a1f1c;
      --text-mid: #7a5c56;
      --text-soft: #b09490;
      --border: #ede3df;
      --radius: 20px;
      --radius-sm: 12px;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--bg);
      font-family: 'Nunito', sans-serif;
      font-weight: 400;
      color: var(--text);
      min-height: 100vh;
      overflow-x: hidden;
    }

    /* SPLASH */
    #splash {
      position: fixed; inset: 0;
      background: linear-gradient(160deg, #c4786a 0%, #a85f52 60%, #8a4a3e 100%);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 1000;
      transition: opacity 0.7s ease, visibility 0.7s ease;
    }
    #splash.hidden { opacity: 0; visibility: hidden; }
    .splash-logo {
      font-family: 'Playfair Display', serif;
      font-size: 44px;
      font-weight: 400;
      color: white;
      text-align: center;
      line-height: 1.1;
    }
    .splash-logo em { font-style: italic; opacity: 0.82; }
    .splash-sub {
      color: rgba(255,255,255,0.6);
      font-size: 12px;
      letter-spacing: 0.22em;
      text-transform: uppercase;
      margin-top: 12px;
    }
    .splash-dots {
      display: flex;
      gap: 8px;
      margin-top: 40px;
    }
    .splash-dot {
      width: 8px; height: 8px;
      border-radius: 50%;
      background: rgba(255,255,255,0.35);
      animation: dotPulse 1.2s ease-in-out infinite;
    }
    .splash-dot:nth-child(2) { animation-delay: 0.2s; }
    .splash-dot:nth-child(3) { animation-delay: 0.4s; }
    @keyframes dotPulse {
      0%, 100% { background: rgba(255,255,255,0.3); transform: scale(1); }
      50% { background: rgba(255,255,255,0.9); transform: scale(1.3); }
    }

    /* PAGE */
    .page {
      max-width: 560px;
      margin: 0 auto;
      padding: 0 16px 80px;
      opacity: 0;
      transform: translateY(18px);
      transition: opacity 0.55s ease 0.2s, transform 0.55s ease 0.2s;
    }
    .page.visible { opacity: 1; transform: translateY(0); }

    /* HEADER */
    .header { padding: 36px 0 24px; text-align: center; }
    .header-eyebrow {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: var(--gold-light);
      color: var(--gold);
      font-size: 11px;
      font-weight: 600;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      padding: 6px 14px;
      border-radius: 30px;
      margin-bottom: 16px;
    }
    .header h1 {
      font-family: 'Playfair Display', serif;
      font-size: clamp(34px, 9vw, 48px);
      font-weight: 400;
      color: var(--text);
      line-height: 1.1;
    }
    .header h1 em { font-style: italic; color: var(--rose); }
    .header p {
      color: var(--text-mid);
      font-size: 14px;
      line-height: 1.8;
      margin-top: 12px;
      max-width: 360px;
      margin-left: auto; margin-right: auto;
    }

    /* SECTION */
    .section { margin-top: 32px; }
    .section-header {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-bottom: 14px;
      padding: 0 2px;
    }
    .section-header h2 {
      font-family: 'Playfair Display', serif;
      font-size: 20px;
      font-weight: 500;
    }
    .section-pip {
      width: 7px; height: 7px;
      border-radius: 50%;
      background: var(--rose);
      flex-shrink: 0;
    }

    /* OVERVIEW CARDS */
    .overview-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
    }
    .ov-card {
      background: var(--surface);
      border-radius: var(--radius);
      padding: 20px 16px 18px;
      border: 1px solid var(--border);
      box-shadow: 0 2px 18px rgba(180,100,90,0.07);
      position: relative;
      overflow: hidden;
      transition: transform 0.18s ease;
    }
    .ov-card:active { transform: scale(0.97); }
    .ov-card::after {
      content: '';
      position: absolute;
      bottom: -10px; right: -10px;
      width: 60px; height: 60px;
      background: radial-gradient(circle, var(--rose-light) 0%, transparent 70%);
    }
    .ov-card.hero {
      grid-column: span 2;
      background: linear-gradient(135deg, var(--rose) 0%, var(--rose-dark) 100%);
      border-color: transparent;
      box-shadow: 0 6px 28px rgba(180,90,80,0.28);
    }
    .ov-card.hero::after { background: radial-gradient(circle, rgba(255,255,255,0.12) 0%, transparent 70%); }
    .ov-card.hero .ov-value { color: white; }
    .ov-card.hero .ov-label { color: rgba(255,255,255,0.68); }
    .ov-card.hero .ov-icon { color: rgba(255,255,255,0.75); }
    .ov-card.sage {
      background: linear-gradient(135deg, #8fa888, #7a9872);
      border-color: transparent;
      box-shadow: 0 6px 22px rgba(100,150,100,0.22);
    }
    .ov-card.sage .ov-value { color: white; }
    .ov-card.sage .ov-label { color: rgba(255,255,255,0.68); }

    .ov-icon { font-size: 20px; margin-bottom: 10px; display: block; }
    .ov-value {
      font-family: 'Playfair Display', serif;
      font-size: 34px;
      font-weight: 500;
      color: var(--rose);
      line-height: 1;
    }
    .ov-value-sm { font-size: 24px; }
    .ov-value-sub {
      font-family: 'Playfair Display', serif;
      font-size: 15px;
      opacity: 0.6;
    }
    .ov-label {
      font-size: 12px;
      font-weight: 500;
      letter-spacing: 0.05em;
      color: var(--text-soft);
      margin-top: 5px;
      line-height: 1.4;
    }

    /* RING CHARTS */
    .ring-row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
    }
    .ring-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 20px 12px 18px;
      box-shadow: 0 2px 18px rgba(180,100,90,0.07);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 12px;
      cursor: pointer;
      transition: transform 0.18s;
      user-select: none;
    }
    .ring-card:active { transform: scale(0.96); }
    .ring-wrap { position: relative; width: 88px; height: 88px; }
    .ring-svg { width: 88px; height: 88px; transform: rotate(-90deg); }
    .ring-track { fill: none; stroke: var(--rose-light); stroke-width: 9; }
    .ring-fill {
      fill: none; stroke-width: 9;
      stroke-linecap: round;
      stroke-dasharray: 214;
      stroke-dashoffset: 214;
      transition: stroke-dashoffset 1.5s cubic-bezier(0.34, 1.4, 0.64, 1);
    }
    .ring-center {
      position: absolute; inset: 0;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
    }
    .rc-val {
      font-family: 'Playfair Display', serif;
      font-size: 20px; font-weight: 500;
      color: var(--text); line-height: 1;
    }
    .rc-unit { font-size: 10px; color: var(--text-soft); font-weight: 500; }
    .ring-label { font-size: 12px; font-weight: 500; color: var(--text-mid); text-align: center; line-height: 1.4; }

    /* BAR CHART */
    .bar-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 22px 20px;
      box-shadow: 0 2px 18px rgba(180,100,90,0.07);
    }
    .bar-card-title {
      font-family: 'Playfair Display', serif;
      font-size: 17px; font-weight: 500;
      margin-bottom: 18px;
    }
    .bc-row { margin-bottom: 14px; }
    .bc-row:last-child { margin-bottom: 0; }
    .bc-top {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      margin-bottom: 7px;
    }
    .bc-name { font-size: 13px; font-weight: 500; color: var(--text); }
    .bc-vals { display: flex; gap: 8px; align-items: baseline; }
    .bc-money { font-family: 'Playfair Display', serif; font-size: 17px; font-weight: 500; }
    .bc-count { font-size: 11px; color: var(--text-soft); }
    .bc-track { background: var(--rose-light); border-radius: 100px; height: 8px; overflow: hidden; }
    .bc-fill {
      height: 100%; border-radius: 100px; width: 0;
      transition: width 1.3s cubic-bezier(0.34, 1.1, 0.64, 1);
    }
    .fill-rose { background: linear-gradient(to right, var(--rose), #d4927f); }
    .fill-gold { background: linear-gradient(to right, var(--gold), #d4b07a); }
    .fill-sage { background: linear-gradient(to right, var(--sage), #aac4a0); }
    .fill-muted { background: linear-gradient(to right, #c0a0a0, #d4b8b0); }

    /* SEGMENTED BAR */
    .seg-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 22px 20px;
      box-shadow: 0 2px 18px rgba(180,100,90,0.07);
    }
    .seg-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 14px; }
    .seg-title { font-family: 'Playfair Display', serif; font-size: 17px; font-weight: 500; }
    .seg-pct { font-family: 'Playfair Display', serif; font-size: 38px; font-weight: 500; color: var(--rose); line-height: 1; }
    .seg-pct-label { font-size: 11px; color: var(--text-soft); font-weight: 500; text-align: right; }
    .seg-bar { display: flex; border-radius: 100px; overflow: hidden; height: 14px; background: var(--bg); }
    .seg-filled {
      background: linear-gradient(to right, var(--rose), #d4927f);
      border-radius: 100px 0 0 100px;
      width: 0;
      transition: width 1.4s cubic-bezier(0.34, 1.1, 0.64, 1);
    }
    .seg-rest { background: var(--rose-light); flex: 1; border-radius: 0 100px 100px 0; }
    .seg-labels { display: flex; justify-content: space-between; margin-top: 8px; }
    .seg-labels span { font-size: 12px; color: var(--text-soft); }
    .seg-labels strong { color: var(--text-mid); font-weight: 600; }

    /* EXPAND */
    .expand-toggle {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 15px 18px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      cursor: pointer;
      box-shadow: 0 2px 18px rgba(180,100,90,0.07);
      transition: background 0.18s;
      user-select: none;
      -webkit-user-select: none;
    }
    .expand-toggle:active { background: var(--rose-pale); }
    .et-left { display: flex; align-items: center; gap: 12px; }
    .et-icon {
      width: 38px; height: 38px;
      background: var(--rose-pale);
      border-radius: 10px;
      display: flex; align-items: center; justify-content: center;
      font-size: 18px; flex-shrink: 0;
    }
    .et-lbl { font-size: 11px; font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase; color: var(--text-soft); }
    .et-val { font-family: 'Playfair Display', serif; font-size: 19px; font-weight: 500; }
    .et-val span { color: var(--rose); }
    .et-arrow { font-size: 20px; color: var(--text-soft); transition: transform 0.3s ease; flex-shrink: 0; }
    .expand-toggle.open .et-arrow { transform: rotate(180deg); }
    .expand-body {
      max-height: 0; overflow: hidden;
      transition: max-height 0.4s ease;
      background: var(--surface);
      border: 1px solid var(--border);
      border-top: none;
      border-radius: 0 0 var(--radius) var(--radius);
      margin-top: -12px;
    }
    .expand-body.open { max-height: 700px; }
    .expand-inner { padding: 18px 20px 20px; }

    .cli-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 10px 0;
      border-bottom: 1px solid var(--border);
    }
    .cli-row:last-child { border-bottom: none; }
    .cli-name { font-size: 14px; font-weight: 500; }
    .cli-right { display: flex; align-items: center; gap: 8px; }
    .cli-dots { display: flex; gap: 3px; }
    .cli-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--rose-light); }
    .cli-dot.on { background: var(--rose); }
    .cli-num { font-family: 'Playfair Display', serif; font-size: 18px; color: var(--rose); font-weight: 500; min-width: 20px; text-align: right; }

    /* GASTOS */
    .gastos-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
    .gc {
      border-radius: var(--radius);
      padding: 20px 16px;
      border: 1px solid;
      box-shadow: 0 2px 18px rgba(180,100,90,0.07);
    }
    .gc-s { background: var(--gold-light); border-color: #e8d4a8; }
    .gc-p { background: var(--surface); border-color: var(--border); }
    .gc-icon { font-size: 22px; margin-bottom: 8px; display: block; }
    .gc-lbl { font-size: 11px; font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase; color: var(--text-soft); margin-bottom: 4px; }
    .gc-val { font-family: 'Playfair Display', serif; font-size: 26px; font-weight: 500; }
    .gc-s .gc-val { color: var(--gold); }
    .gc-p .gc-val { color: var(--text-mid); }
    .gc-note { font-size: 12px; color: var(--text-soft); margin-top: 4px; line-height: 1.5; }

    /* INSIGHTS SCROLL */
    .insights-scroll {
      display: flex;
      gap: 10px;
      overflow-x: auto;
      padding: 4px 2px 10px;
      scroll-snap-type: x mandatory;
      -webkit-overflow-scrolling: touch;
      scrollbar-width: none;
    }
    .insights-scroll::-webkit-scrollbar { display: none; }
    .i-chip {
      flex-shrink: 0;
      width: calc(85vw - 20px);
      max-width: 330px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 20px 18px;
      box-shadow: 0 2px 18px rgba(180,100,90,0.07);
      scroll-snap-align: start;
      transition: transform 0.15s;
    }
    .i-chip:active { transform: scale(0.97); }
    .ic-em { font-size: 26px; margin-bottom: 10px; display: block; }
    .ic-title { font-family: 'Playfair Display', serif; font-size: 17px; font-weight: 500; margin-bottom: 6px; line-height: 1.3; }
    .ic-text { font-size: 13px; color: var(--text-mid); line-height: 1.68; }
    .ic-badge {
      display: inline-block;
      background: var(--rose-pale);
      color: var(--rose);
      font-size: 11px; font-weight: 600;
      padding: 4px 10px;
      border-radius: 20px;
      margin-top: 10px;
    }
    .scroll-hint { text-align: center; font-size: 11px; color: var(--text-soft); margin-top: 2px; }

    /* NOTE */
    .note {
      background: var(--rose-pale);
      border-left: 3px solid var(--rose-light);
      border-radius: 0 var(--radius-sm) var(--radius-sm) 0;
      padding: 12px 16px;
      font-size: 13px;
      color: var(--text-mid);
      line-height: 1.7;
      margin-top: 10px;
    }

    /* CLOSING */
    .closing-card {
      background: linear-gradient(145deg, var(--rose) 0%, #b06050 100%);
      border-radius: var(--radius);
      padding: 28px 22px;
      color: white;
      box-shadow: 0 8px 32px rgba(180,80,70,0.26);
    }
    .closing-card h2 { font-family: 'Playfair Display', serif; font-size: 22px; font-weight: 400; margin-bottom: 18px; }
    .step { display: flex; gap: 12px; align-items: flex-start; margin-bottom: 12px; }
    .step-n {
      width: 24px; height: 24px; border-radius: 50%;
      background: rgba(255,255,255,0.22);
      font-size: 11px; font-weight: 700;
      display: flex; align-items: center; justify-content: center;
      flex-shrink: 0;
    }
    .step-t { font-size: 14px; color: rgba(255,255,255,0.9); line-height: 1.6; padding-top: 2px; }
    .closing-q {
      margin-top: 20px;
      padding-top: 18px;
      border-top: 1px solid rgba(255,255,255,0.22);
      font-family: 'Playfair Display', serif;
      font-style: italic;
      font-size: 17px;
      color: rgba(255,255,255,0.92);
      text-align: center;
      line-height: 1.65;
    }

    /* ANIMATE IN */
    .ai {
      opacity: 0;
      transform: translateY(14px);
      transition: opacity 0.5s ease, transform 0.5s ease;
    }
    .ai.vis { opacity: 1; transform: translateY(0); }

    footer {
      text-align: center;
      padding: 28px 0 0;
      font-size: 11px;
      color: var(--text-soft);
      letter-spacing: 0.08em;
    }

    @media (min-width: 460px) {
      .overview-grid { grid-template-columns: repeat(4, 1fr); }
      .ov-card.hero { grid-column: span 4; }
    }
  </style>
</head>
<body>

<div id="splash">
  <div class="splash-logo">Painel do<br><em>Salão</em></div>
  <div class="splash-sub">Março · 2026</div>
  <div class="splash-dots">
    <div class="splash-dot"></div>
    <div class="splash-dot"></div>
    <div class="splash-dot"></div>
  </div>
</div>

<div class="page" id="page">

  <header class="header">
    <div class="header-eyebrow">✦ Março de 2026 ✦</div>
    <h1>Painel do <em>Salão</em></h1>
    <p>Cada atendimento anotado é um passo para entender melhor o seu negócio. Aqui está o retrato do mês.</p>
  </header>

  <!-- VISÃO GERAL -->
  <section class="section">
    <div class="section-header">
      <div class="section-pip"></div>
      <h2>Visão Geral</h2>
    </div>
    <div class="overview-grid">
      <div class="ov-card hero ai">
        <span class="ov-icon">💰</span>
        <div class="ov-value">R$&thinsp;<span class="cu" data-t="3500"></span><span class="ov-value-sub">,00</span></div>
        <div class="ov-label">Faturamento registrado</div>
      </div>
      <div class="ov-card ai" style="transition-delay:0.08s">
        <span class="ov-icon">✂️</span>
        <div class="ov-value"><span class="cu" data-t="78"></span></div>
        <div class="ov-label">Atendimentos</div>
      </div>
      <div class="ov-card ai" style="transition-delay:0.14s">
        <span class="ov-icon">👤</span>
        <div class="ov-value"><span class="cu" data-t="44"></span></div>
        <div class="ov-label">Clientes únicas</div>
      </div>
      <div class="ov-card ai" style="transition-delay:0.2s">
        <span class="ov-icon">📅</span>
        <div class="ov-value"><span class="cu" data-t="18"></span></div>
        <div class="ov-label">Dias com registro</div>
      </div>
    </div>
    <div class="note ai" style="transition-delay:0.25s">
      Esses números mostram uma operação ativa e consistente — quase 5 atendimentos por dia útil trabalhado.
    </div>
  </section>

  <!-- MOVIMENTO -->
  <section class="section">
    <div class="section-header">
      <div class="section-pip"></div>
      <h2>Movimento do Mês</h2>
    </div>
    <div class="ring-row ai">
      <div class="ring-card" onclick="this.style.transform='scale(0.96)';setTimeout(()=>this.style.transform='',150)">
        <div class="ring-wrap">
          <svg class="ring-svg" viewBox="0 0 88 88">
            <circle class="ring-track" cx="44" cy="44" r="34"/>
            <circle class="ring-fill" cx="44" cy="44" r="34" stroke="#c4786a" data-pct="61"/>
          </svg>
          <div class="ring-center">
            <span class="rc-val">61%</span>
            <span class="rc-unit">receita</span>
          </div>
        </div>
        <div class="ring-label">pé + mão<br>do faturamento</div>
      </div>
      <div class="ring-card" onclick="this.style.transform='scale(0.96)';setTimeout(()=>this.style.transform='',150)">
        <div class="ring-wrap">
          <svg class="ring-svg" viewBox="0 0 88 88">
            <circle class="ring-track" cx="44" cy="44" r="34"/>
            <circle class="ring-fill" cx="44" cy="44" r="34" stroke="#c09a5e" data-pct="67"/>
          </svg>
          <div class="ring-center">
            <span class="rc-val">67%</span>
            <span class="rc-unit">do total</span>
          </div>
        </div>
        <div class="ring-label">clientes que<br>voltaram</div>
      </div>
    </div>

    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:10px">
      <div class="ov-card sage ai" style="transition-delay:0.1s">
        <span class="ov-icon">🎯</span>
        <div class="ov-value ov-value-sm">R$&thinsp;44</div>
        <div class="ov-label">Ticket médio</div>
      </div>
      <div class="ov-card ai" style="transition-delay:0.16s">
        <span class="ov-icon">🔥</span>
        <div class="ov-value ov-value-sm">7/mar</div>
        <div class="ov-label">Dia + movimentado<br><span style="color:var(--rose);font-weight:600">11 atend.</span></div>
      </div>
    </div>
    <div class="note ai" style="transition-delay:0.2s">
      A sexta-feira foi imbatível: 11 clientes em um único dia. Vale garantir agenda aberta e materiais nas sextas.
    </div>
  </section>

  <!-- RECEITA POR SERVIÇO -->
  <section class="section">
    <div class="section-header">
      <div class="section-pip"></div>
      <h2>Receita por Serviço</h2>
    </div>
    <div class="bar-card ai">
      <div class="bar-card-title">O que mais gerou receita</div>
      <div class="bc-row">
        <div class="bc-top">
          <span class="bc-name">pé + mão</span>
          <div class="bc-vals"><span class="bc-money">R$ 2.130</span><span class="bc-count">29×</span></div>
        </div>
        <div class="bc-track"><div class="bc-fill fill-rose" data-w="100"></div></div>
      </div>
      <div class="bc-row">
        <div class="bc-top">
          <span class="bc-name">mão</span>
          <div class="bc-vals"><span class="bc-money">R$ 680</span><span class="bc-count">17×</span></div>
        </div>
        <div class="bc-track"><div class="bc-fill fill-rose" data-w="32"></div></div>
      </div>
      <div class="bc-row">
        <div class="bc-top">
          <span class="bc-name">pé (avulso)</span>
          <div class="bc-vals"><span class="bc-money">R$ 385</span><span class="bc-count">8×</span></div>
        </div>
        <div class="bc-track"><div class="bc-fill fill-gold" data-w="18"></div></div>
      </div>
      <div class="bc-row">
        <div class="bc-top">
          <span class="bc-name">combos c/ depilação</span>
          <div class="bc-vals"><span class="bc-money">R$ 110+</span><span class="bc-count">3×</span></div>
        </div>
        <div class="bc-track"><div class="bc-fill fill-sage" data-w="12"></div></div>
      </div>
      <div class="bc-row">
        <div class="bc-top">
          <span class="bc-name">esmaltação · sobrancelha · busto</span>
          <div class="bc-vals"><span class="bc-money">R$ 195</span><span class="bc-count">5×</span></div>
        </div>
        <div class="bc-track"><div class="bc-fill fill-muted" data-w="9"></div></div>
      </div>
    </div>
    <div class="note ai">
      pé + mão responde por 61% do faturamento. É o serviço âncora do salão — todo o resto é bônus em cima disso.
    </div>
  </section>

  <!-- CLIENTES -->
  <section class="section">
    <div class="section-header">
      <div class="section-pip"></div>
      <h2>Base de Clientes</h2>
    </div>

    <div class="seg-card ai">
      <div class="seg-header">
        <div class="seg-title">Clientes que voltaram</div>
        <div>
          <div class="seg-pct"><span class="cu" data-t="67"></span>%</div>
          <div class="seg-pct-label">dos atendimentos</div>
        </div>
      </div>
      <div class="seg-bar">
        <div class="seg-filled" data-w="67"></div>
        <div class="seg-rest"></div>
      </div>
      <div class="seg-labels">
        <span><strong>52</strong> de clientes fiéis</span>
        <span><strong>26</strong> novas</span>
      </div>
    </div>

    <div style="margin-top:10px">
      <div class="expand-toggle ai" id="tg-cli" onclick="xp('cli')">
        <div class="et-left">
          <div class="et-icon">👑</div>
          <div class="et-text">
            <div class="et-lbl">Cliente destaque</div>
            <div class="et-val"><span>Ju</span> — 6 visitas</div>
          </div>
        </div>
        <div class="et-arrow">⌄</div>
      </div>
      <div class="expand-body" id="bd-cli">
        <div class="expand-inner">
          <div class="cli-row">
            <span class="cli-name">Ju</span>
            <div class="cli-right">
              <div class="cli-dots">
                <div class="cli-dot on"></div><div class="cli-dot on"></div><div class="cli-dot on"></div>
                <div class="cli-dot on"></div><div class="cli-dot on"></div><div class="cli-dot on"></div>
              </div>
              <span class="cli-num">6</span>
            </div>
          </div>
          <div class="cli-row">
            <span class="cli-name">Sueli</span>
            <div class="cli-right">
              <div class="cli-dots"><div class="cli-dot on"></div><div class="cli-dot on"></div><div class="cli-dot on"></div></div>
              <span class="cli-num">3</span>
            </div>
          </div>
          <div class="cli-row">
            <span class="cli-name">Camila</span>
            <div class="cli-right">
              <div class="cli-dots"><div class="cli-dot on"></div><div class="cli-dot on"></div><div class="cli-dot on"></div></div>
              <span class="cli-num">3</span>
            </div>
          </div>
          <div class="cli-row">
            <span class="cli-name">Rosa</span>
            <div class="cli-right">
              <div class="cli-dots"><div class="cli-dot on"></div><div class="cli-dot on"></div><div class="cli-dot on"></div></div>
              <span class="cli-num">3</span>
            </div>
          </div>
          <div class="cli-row">
            <span class="cli-name">Denise</span>
            <div class="cli-right">
              <div class="cli-dots"><div class="cli-dot on"></div><div class="cli-dot on"></div><div class="cli-dot on"></div></div>
              <span class="cli-num">3</span>
            </div>
          </div>
          <div class="cli-row">
            <span class="cli-name">Marilena</span>
            <div class="cli-right">
              <div class="cli-dots"><div class="cli-dot on"></div><div class="cli-dot on"></div><div class="cli-dot on"></div></div>
              <span class="cli-num">3</span>
            </div>
          </div>
          <div class="cli-row">
            <span class="cli-name" style="font-size:12px;color:var(--text-mid)">Aurélia · Carol · Sandra · Andréia · Amanda · Madá · Silene · Marilene · Gabriela · Severina</span>
            <div class="cli-right">
              <div class="cli-dots"><div class="cli-dot on"></div><div class="cli-dot on"></div></div>
              <span class="cli-num">2</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="note ai">
      Mais de dois terços dos atendimentos foram de clientes que já voltaram. Isso é fidelidade de verdade.
    </div>
  </section>

  <!-- GASTOS -->
  <section class="section">
    <div class="section-header">
      <div class="section-pip"></div>
      <h2>Gastos do Período</h2>
    </div>
    <div class="gastos-grid">
      <div class="gc gc-s ai">
        <span class="gc-icon">🏠</span>
        <div class="gc-lbl">Salão</div>
        <div class="gc-val">R$&thinsp;525</div>
        <div class="gc-note">3 registros: compras, material, marceneiro</div>
      </div>
      <div class="gc gc-p ai" style="transition-delay:0.1s">
        <span class="gc-icon">👜</span>
        <div class="gc-lbl">Pessoal</div>
        <div class="gc-val">R$&thinsp;4.657</div>
        <div class="gc-note">27 registros no mês</div>
      </div>
    </div>

    <div style="margin-top:10px">
      <div class="expand-toggle ai" id="tg-gas" onclick="xp('gas')">
        <div class="et-left">
          <div class="et-icon">🔍</div>
          <div class="et-text">
            <div class="et-lbl">Ver detalhes</div>
            <div class="et-val">Gastos do <span>salão</span></div>
          </div>
        </div>
        <div class="et-arrow">⌄</div>
      </div>
      <div class="expand-body" id="bd-gas">
        <div class="expand-inner">
          <div class="cli-row">
            <span class="cli-name">Compra salão · 17/03</span>
            <span style="font-family:'Playfair Display',serif;font-size:16px;color:var(--gold);font-weight:500">R$ 130</span>
          </div>
          <div class="cli-row">
            <span class="cli-name">Material salão · 19/03</span>
            <span style="font-family:'Playfair Display',serif;font-size:16px;color:var(--gold);font-weight:500">R$ 25</span>
          </div>
          <div class="cli-row">
            <span class="cli-name">Marceneiro Marcos · 20/03</span>
            <span style="font-family:'Playfair Display',serif;font-size:16px;color:var(--gold);font-weight:500">R$ 370</span>
          </div>
        </div>
      </div>
    </div>
    <div class="note ai">
      Separar o que é do salão do que é pessoal já é um grande passo. Com o tempo, fica cada vez mais fácil entender o que o negócio realmente precisa.
    </div>
  </section>

  <!-- INSIGHTS -->
  <section class="section">
    <div class="section-header">
      <div class="section-pip"></div>
      <h2>Destaques do Mês</h2>
    </div>
    <div class="insights-scroll ai">
      <div class="i-chip">
        <span class="ic-em">🌟</span>
        <div class="ic-title">Clientes fiéis já são maioria</div>
        <div class="ic-text">67% dos atendimentos vieram de clientes que já voltaram pelo menos uma vez. É sinal concreto de confiança no trabalho.</div>
        <span class="ic-badge">Ju · Sueli · Camila · Rosa · Denise</span>
      </div>
      <div class="i-chip">
        <span class="ic-em">💅</span>
        <div class="ic-title">pé + mão é o serviço âncora</div>
        <div class="ic-text">O combo foi pedido 29 vezes e gerou R$ 2.130 — mais de metade do faturamento do mês inteiro.</div>
        <span class="ic-badge">61% do faturamento total</span>
      </div>
      <div class="i-chip">
        <span class="ic-em">📆</span>
        <div class="ic-title">Sexta-feira manda no salão</div>
        <div class="ic-text">O dia 7 de março teve 11 clientes — o maior de todos. A sexta tem uma demanda que vale explorar.</div>
        <span class="ic-badge">11 atendimentos em 1 dia</span>
      </div>
      <div class="i-chip">
        <span class="ic-em">📊</span>
        <div class="ic-title">Operação constante e consistente</div>
        <div class="ic-text">18 dias com registro no mês, média de 4,3 atendimentos por dia ativo. O salão está em pleno ritmo.</div>
        <span class="ic-badge">Média de 4,3 atend./dia</span>
      </div>
      <div class="i-chip">
        <span class="ic-em">🏗️</span>
        <div class="ic-title">O espaço está evoluindo</div>
        <div class="ic-text">R$ 370 investidos no marceneiro Marcos mostram que há melhorias sendo feitas — o salão está crescendo.</div>
        <span class="ic-badge">Investimento em estrutura</span>
      </div>
    </div>
    <div class="scroll-hint">← deslize para ver mais →</div>
  </section>

  <!-- PRÓXIMOS PASSOS -->
  <section class="section">
    <div class="section-header">
      <div class="section-pip"></div>
      <h2>Próximos Passos</h2>
    </div>
    <div class="closing-card ai">
      <h2>Continuar é a chave</h2>
      <div class="step"><div class="step-n">1</div><div class="step-t">Continue anotando cada atendimento — nome, serviço e valor. Mesmo que seja rápido.</div></div>
      <div class="step"><div class="step-n">2</div><div class="step-t">Separe os gastos do salão dos pessoais sempre que possível.</div></div>
      <div class="step"><div class="step-n">3</div><div class="step-t">Anote a forma de pagamento quando lembrar — ajuda a entender o fluxo do dinheiro.</div></div>
      <div class="step"><div class="step-n">4</div><div class="step-t">No mês que vem, o painel vai mostrar a evolução comparada com março.</div></div>
      <div class="closing-q">"Quanto mais você registra,<br>mais claro fica o seu próprio negócio."</div>
    </div>
  </section>

  <footer>Painel do Salão · Março 2026</footer>
</div>

<script>
  // Splash
  window.addEventListener('load', () => {
    setTimeout(() => {
      document.getElementById('splash').classList.add('hidden');
      const page = document.getElementById('page');
      page.classList.add('visible');
      setTimeout(initObservers, 100);
    }, 1400);
  });

  // Expand/collapse
  function xp(id) {
    const tg = document.getElementById('tg-' + id);
    const bd = document.getElementById('bd-' + id);
    const open = bd.classList.contains('open');
    bd.classList.toggle('open', !open);
    tg.classList.toggle('open', !open);
  }

  // Count-up
  function countUp(el) {
    if (el.dataset.done) return;
    el.dataset.done = '1';
    const target = parseInt(el.dataset.t);
    const dur = 1300;
    const start = performance.now();
    (function step(now) {
      const p = Math.min((now - start) / dur, 1);
      const ease = 1 - Math.pow(1 - p, 3);
      el.textContent = Math.round(ease * target).toLocaleString('pt-BR');
      if (p < 1) requestAnimationFrame(step);
      else el.textContent = target.toLocaleString('pt-BR');
    })(start);
  }

  // Ring animation
  function animateRing(el) {
    if (el.dataset.done) return;
    el.dataset.done = '1';
    const pct = parseFloat(el.dataset.pct) / 100;
    const circ = 2 * Math.PI * 34; // r=34
    el.style.strokeDasharray = circ;
    el.style.strokeDashoffset = circ;
    requestAnimationFrame(() => {
      el.style.strokeDashoffset = circ * (1 - pct);
    });
  }

  // Bar fills
  function animateBars(container) {
    container.querySelectorAll('.bc-fill[data-w]').forEach(f => {
      if (f.dataset.done) return;
      f.dataset.done = '1';
      setTimeout(() => { f.style.width = f.dataset.w + '%'; }, 80);
    });
  }

  // Seg bar
  function animateSeg(container) {
    container.querySelectorAll('.seg-filled[data-w]').forEach(f => {
      if (f.dataset.done) return;
      f.dataset.done = '1';
      setTimeout(() => { f.style.width = f.dataset.w + '%'; }, 100);
    });
  }

  function initObservers() {
    const io = new IntersectionObserver(entries => {
      entries.forEach(e => {
        if (!e.isIntersecting) return;
        const el = e.target;
        el.classList.add('vis');
        // count-ups inside
        el.querySelectorAll('.cu[data-t]').forEach(countUp);
        // ring fills
        el.querySelectorAll('.ring-fill[data-pct]').forEach(animateRing);
        // bar fills
        animateBars(el);
        // seg bars
        animateSeg(el);
        io.unobserve(el);
      });
    }, { threshold: 0.15 });

    document.querySelectorAll('.ai').forEach(el => io.observe(el));

    // Also observe bar-card and seg-card and ring-row directly
    const io2 = new IntersectionObserver(entries => {
      entries.forEach(e => {
        if (!e.isIntersecting) return;
        animateBars(e.target);
        animateSeg(e.target);
        e.target.querySelectorAll('.ring-fill[data-pct]').forEach(animateRing);
        e.target.querySelectorAll('.cu[data-t]').forEach(countUp);
        io2.unobserve(e.target);
      });
    }, { threshold: 0.2 });
    document.querySelectorAll('.bar-card, .seg-card, .ring-row, .ov-card').forEach(el => io2.observe(el));
  }
</script>
</body>
</html>
