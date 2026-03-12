<!DOCTYPE html>



<html lang="es">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Economía de Guerra: ¿Catástrofe o Oportunidad?</title>

<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=IBM+Plex+Mono:wght@400;600&family=Source+Serif+4:wght@300;400;600&display=swap" rel="stylesheet">

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.0/chart.umd.min.js"></script>

<style>

  :root {

    --blood: #8B0000;

    --fire: #C0392B;

    --ash: #1a1a1a;

    --smoke: #2d2d2d;

    --parchment: #F5ECD7;

    --gold: #D4A017;

    --olive: #4A5240;

    --steel: #6B7280;

    --white: #FAF8F3;

    --green-war: #2D5016;

    --amber: #F59E0B;

  }



- { margin: 0; padding: 0; box-sizing: border-box; }



body {

font-family: ‘Source Serif 4’, Georgia, serif;

background: var(–ash);

color: var(–white);

overflow: hidden;

height: 100vh;

}



/* NAVIGATION */

#nav {

position: fixed;

bottom: 24px;

left: 50%;

transform: translateX(-50%);

display: flex;

gap: 8px;

z-index: 1000;

background: rgba(0,0,0,0.7);

padding: 10px 16px;

border-radius: 40px;

border: 1px solid rgba(212,160,23,0.3);

backdrop-filter: blur(10px);

}

.nav-dot {

width: 10px; height: 10px;

border-radius: 50%;

background: var(–steel);

cursor: pointer;

transition: all 0.3s;

}

.nav-dot.active { background: var(–gold); transform: scale(1.4); }



#prev-btn, #next-btn {

position: fixed;

top: 50%;

transform: translateY(-50%);

background: rgba(0,0,0,0.5);

border: 1px solid rgba(212,160,23,0.4);

color: var(–gold);

font-size: 22px;

width: 44px; height: 44px;

border-radius: 50%;

cursor: pointer;

z-index: 1000;

display: flex; align-items: center; justify-content: center;

transition: all 0.3s;

font-family: ‘IBM Plex Mono’, monospace;

}

#prev-btn { left: 16px; }

#next-btn { right: 16px; }

#prev-btn:hover, #next-btn:hover { background: rgba(212,160,23,0.2); }



/* SLIDES */

.slide {

display: none;

width: 100vw;

height: 100vh;

overflow-y: auto;

position: relative;

}

.slide.active { display: flex; flex-direction: column; }



/* SLIDE 0 - COVER */

#slide-0 {

background: var(–ash);

justify-content: center;

align-items: center;

text-align: center;

overflow: hidden;

}

.cover-bg {

position: absolute; inset: 0;

background:

radial-gradient(ellipse at 50% 40%, rgba(139,0,0,0.18) 0%, transparent 65%),

radial-gradient(ellipse at 15% 80%, rgba(212,160,23,0.06) 0%, transparent 50%);

}

/* Thin horizontal rule lines for texture */

.cover-bg::after {

content: ‘’;

position: absolute; inset: 0;

background: repeating-linear-gradient(

0deg, transparent, transparent 60px,

rgba(255,255,255,0.012) 60px, rgba(255,255,255,0.012) 61px

);

pointer-events: none;

}

.cover-content {

position: relative; z-index: 2;

max-width: 760px;

padding: 48px 40px;

display: flex;

flex-direction: column;

align-items: center;

}

.cover-eyebrow {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 10px;

letter-spacing: 5px;

color: var(–gold);

text-transform: uppercase;

margin-bottom: 36px;

opacity: 0.6;

}

.cover-title {

font-family: ‘Playfair Display’, serif;

font-size: clamp(52px, 8vw, 104px);

font-weight: 900;

line-height: 0.9;

color: var(–white);

letter-spacing: -2px;

margin-bottom: 0;

}

.cover-title span { color: var(–gold); font-style: italic; }

.cover-subtitle {

font-family: ‘Playfair Display’, serif;

font-size: clamp(20px, 2.8vw, 36px);

font-weight: 700;

font-style: italic;

color: var(–fire);

margin-top: 14px;

letter-spacing: 0;

opacity: 0.9;

}

.cover-line {

width: 40px;

height: 1px;

background: rgba(212,160,23,0.5);

margin: 36px auto;

}

.cover-authors {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 12px;

color: rgba(250,248,243,0.4);

letter-spacing: 1.5px;

line-height: 2;

text-align: center;

}

.cover-authors strong { color: rgba(250,248,243,0.75); font-weight: 600; }

.cover-meta {

margin-top: 32px;

font-family: ‘IBM Plex Mono’, monospace;

font-size: 9px;

color: rgba(107,114,128,0.6);

letter-spacing: 4px;

text-transform: uppercase;

}

.war-number {

position: absolute;

font-family: ‘Playfair Display’, serif;

font-size: 380px;

font-weight: 900;

color: rgba(139,0,0,0.04);

line-height: 1;

right: -20px;

bottom: 0;

pointer-events: none;

user-select: none;

}



/* GENERIC SLIDE LAYOUT */

.slide-inner {

max-width: 1200px;

margin: 0 auto;

padding: 40px 40px 100px;

width: 100%;

}

.slide-number {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 10px;

letter-spacing: 3px;

color: var(–gold);

text-transform: uppercase;

margin-bottom: 8px;

opacity: 0.7;

}

.slide-title {

font-family: ‘Playfair Display’, serif;

font-size: clamp(28px, 4vw, 52px);

font-weight: 900;

line-height: 1.05;

margin-bottom: 6px;

color: var(–white);

}

.slide-title em { color: var(–gold); font-style: italic; }

.slide-title .red { color: var(–fire); }

.slide-rule { width: 60px; height: 3px; background: var(–blood); margin: 16px 0 28px; }



/* DARK SECTION BG */

#slide-1 { background: linear-gradient(135deg, #0f0f0f 0%, #1a1a1a 100%); }

#slide-2 { background: linear-gradient(160deg, #0d1117 0%, #1a1a1a 100%); }

#slide-3 { background: linear-gradient(135deg, #0d0d0d 0%, #1c1408 100%); }

#slide-4 { background: linear-gradient(135deg, #0d1a0d 0%, #0f1a0f 100%); }

#slide-5 { background: linear-gradient(135deg, #0d0d1a 0%, #1a0d1a 100%); }

#slide-6 { background: linear-gradient(135deg, #0a0a0a 0%, #1a1a0d 100%); }

#slide-7 { background: linear-gradient(135deg, #0f0a00 0%, #1a1000 100%); }

#slide-8 { background: #0c0c0c; }



/* REFERENCES */

.ref-grid {

display: grid;

grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));

gap: 0;

}

.ref-category {

padding: 18px 20px;

border-right: 1px solid rgba(255,255,255,0.05);

border-bottom: 1px solid rgba(255,255,255,0.05);

}

.ref-cat-title {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 9px;

letter-spacing: 3px;

text-transform: uppercase;

color: var(–gold);

margin-bottom: 14px;

padding-bottom: 8px;

border-bottom: 1px solid rgba(212,160,23,0.2);

}

.ref-item {

margin-bottom: 10px;

padding-left: 12px;

border-left: 2px solid rgba(255,255,255,0.07);

position: relative;

}

.ref-item:hover { border-left-color: rgba(212,160,23,0.4); }

.ref-num {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 8px;

color: var(–gold);

letter-spacing: 1px;

margin-bottom: 2px;

opacity: 0.7;

}

.ref-authors {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 10px;

color: rgba(250,248,243,0.65);

line-height: 1.4;

margin-bottom: 2px;

}

.ref-title-text {

font-family: ‘Source Serif 4’, Georgia, serif;

font-size: 12px;

font-style: italic;

color: rgba(250,248,243,0.85);

line-height: 1.4;

margin-bottom: 2px;

}

.ref-source {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 9px;

color: rgba(107,114,128,0.8);

letter-spacing: 0.5px;

}

.ref-source a {

color: rgba(96,165,250,0.7);

text-decoration: none;

}

.ref-source a:hover { color: #60a5fa; text-decoration: underline; }



/* CARDS */

.cards-grid {

display: grid;

grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));

gap: 16px;

margin-bottom: 24px;

}

.card {

background: rgba(255,255,255,0.04);

border: 1px solid rgba(255,255,255,0.08);

border-radius: 4px;

padding: 20px;

border-left: 3px solid var(–gold);

position: relative;

overflow: hidden;

}

.card::before {

content: ‘’;

position: absolute; inset: 0;

background: linear-gradient(135deg, rgba(212,160,23,0.03) 0%, transparent 60%);

pointer-events: none;

}

.card.red-border { border-left-color: var(–fire); }

.card.green-border { border-left-color: #22c55e; }

.card.blue-border { border-left-color: #3b82f6; }

.card h3 {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 11px;

letter-spacing: 2px;

text-transform: uppercase;

color: var(–gold);

margin-bottom: 10px;

}

.card.red-border h3 { color: var(–fire); }

.card.green-border h3 { color: #22c55e; }

.card.blue-border h3 { color: #60a5fa; }

.card p {

font-size: 14px;

color: rgba(250,248,243,0.75);

line-height: 1.6;

}

.card .stat {

font-family: ‘Playfair Display’, serif;

font-size: 36px;

font-weight: 700;

color: var(–gold);

margin-bottom: 4px;

line-height: 1;

}

.card.red-border .stat { color: var(–fire); }

.card.green-border .stat { color: #22c55e; }



/* CHART CONTAINERS */

.chart-wrap {

background: rgba(255,255,255,0.03);

border: 1px solid rgba(255,255,255,0.07);

border-radius: 4px;

padding: 20px;

margin-bottom: 20px;

}

.chart-title {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 11px;

letter-spacing: 2px;

text-transform: uppercase;

color: var(–gold);

margin-bottom: 16px;

opacity: 0.8;

}



/* TWO COLS */

.two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }

.three-col { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; }



/* TIMELINE */

.timeline { position: relative; padding-left: 30px; }

.timeline::before { content: ‘’; position: absolute; left: 8px; top: 0; bottom: 0; width: 2px; background: rgba(212,160,23,0.3); }

.timeline-item { position: relative; margin-bottom: 20px; }

.timeline-item::before {

content: ‘’;

position: absolute;

left: -26px; top: 6px;

width: 10px; height: 10px;

border-radius: 50%;

background: var(–gold);

border: 2px solid var(–ash);

}

.timeline-item.red::before { background: var(–fire); }

.timeline-year {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 10px;

color: var(–gold);

letter-spacing: 2px;

margin-bottom: 4px;

}

.timeline-item.red .timeline-year { color: var(–fire); }

.timeline-text { font-size: 14px; color: rgba(250,248,243,0.75); line-height: 1.5; }



/* TABLE */

.war-table { width: 100%; border-collapse: collapse; font-size: 13px; }

.war-table th {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 10px;

letter-spacing: 2px;

text-transform: uppercase;

color: var(–gold);

text-align: left;

padding: 10px 14px;

border-bottom: 1px solid rgba(212,160,23,0.3);

}

.war-table td {

padding: 10px 14px;

border-bottom: 1px solid rgba(255,255,255,0.05);

color: rgba(250,248,243,0.75);

vertical-align: top;

}

.war-table tr:hover td { background: rgba(255,255,255,0.03); }

.badge {

display: inline-block;

padding: 2px 8px;

border-radius: 2px;

font-family: ‘IBM Plex Mono’, monospace;

font-size: 10px;

letter-spacing: 1px;

}

.badge-red { background: rgba(192,57,43,0.2); color: #f87171; border: 1px solid rgba(192,57,43,0.4); }

.badge-green { background: rgba(34,197,94,0.15); color: #4ade80; border: 1px solid rgba(34,197,94,0.3); }

.badge-amber { background: rgba(245,158,11,0.15); color: #fbbf24; border: 1px solid rgba(245,158,11,0.3); }



/* HIGHLIGHT BOX */

.highlight-box {

background: linear-gradient(135deg, rgba(139,0,0,0.15), rgba(212,160,23,0.08));

border: 1px solid rgba(212,160,23,0.3);

border-radius: 4px;

padding: 20px 24px;

margin-bottom: 20px;

}

.highlight-box p {

font-family: ‘Playfair Display’, serif;

font-size: 18px;

font-style: italic;

color: var(–parchment);

line-height: 1.6;

}

.highlight-box .attribution {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 10px;

letter-spacing: 2px;

color: var(–gold);

margin-top: 10px;

text-transform: uppercase;

}



/* PORTFOLIO COMPARISON */

.portfolio-header {

display: flex;

align-items: center;

gap: 16px;

margin-bottom: 20px;

padding: 16px;

background: rgba(212,160,23,0.07);

border: 1px solid rgba(212,160,23,0.2);

border-radius: 4px;

}

.portfolio-logo {

width: 48px; height: 48px;

background: var(–gold);

border-radius: 4px;

display: flex; align-items: center; justify-content: center;

font-family: ‘IBM Plex Mono’, monospace;

font-size: 18px;

font-weight: 600;

color: var(–ash);

}

.portfolio-info h3 {

font-family: ‘Playfair Display’, serif;

font-size: 20px;

font-weight: 700;

color: var(–white);

margin-bottom: 4px;

}

.portfolio-info p {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 11px;

color: var(–gold);

letter-spacing: 1px;

}



/* METRIC STRIP */

.metric-strip {

display: grid;

grid-template-columns: repeat(4, 1fr);

gap: 12px;

margin-bottom: 20px;

}

.metric-item {

background: rgba(255,255,255,0.03);

border: 1px solid rgba(255,255,255,0.07);

padding: 14px;

border-radius: 4px;

text-align: center;

}

.metric-val {

font-family: ‘Playfair Display’, serif;

font-size: 28px;

font-weight: 700;

line-height: 1;

margin-bottom: 4px;

}

.metric-val.green { color: #4ade80; }

.metric-val.red { color: var(–fire); }

.metric-val.gold { color: var(–gold); }

.metric-label {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 9px;

letter-spacing: 2px;

text-transform: uppercase;

color: var(–steel);

}



/* PHASES STRIP */

.phases-strip {

display: flex;

gap: 8px;

margin-bottom: 20px;

flex-wrap: wrap;

}

.phase-tag {

padding: 6px 14px;

border-radius: 2px;

font-family: ‘IBM Plex Mono’, monospace;

font-size: 10px;

letter-spacing: 1px;

text-transform: uppercase;

border: 1px solid;

}

.phase-paz { background: rgba(34,197,94,0.1); color: #4ade80; border-color: rgba(34,197,94,0.3); }

.phase-inc { background: rgba(245,158,11,0.1); color: #fbbf24; border-color: rgba(245,158,11,0.3); }

.phase-bear { background: rgba(192,57,43,0.1); color: #f87171; border-color: rgba(192,57,43,0.3); }

.phase-bull { background: rgba(99,102,241,0.1); color: #a5b4fc; border-color: rgba(99,102,241,0.3); }

.phase-tens { background: rgba(139,0,0,0.2); color: #fca5a5; border-color: rgba(139,0,0,0.5); }



/* SCROLLBAR */

::-webkit-scrollbar { width: 4px; }

::-webkit-scrollbar-track { background: transparent; }

::-webkit-scrollbar-thumb { background: rgba(212,160,23,0.3); border-radius: 2px; }



/* RESPONSIVE */

@media (max-width: 768px) {

.two-col, .three-col, .metric-strip { grid-template-columns: 1fr; }

.slide-inner { padding: 24px 20px 100px; }

.cover-title { font-size: 36px; }

}



/* ANNOTATION */

.annotation {

font-family: ‘IBM Plex Mono’, monospace;

font-size: 10px;

color: var(–steel);

letter-spacing: 1px;

margin-top: 8px;

}



/* SECTOR TAGS */

.sector-list { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 12px; }

.sector-tag {

padding: 4px 12px;

border-radius: 2px;

font-family: ‘IBM Plex Mono’, monospace;

font-size: 11px;

letter-spacing: 1px;

background: rgba(212,160,23,0.1);

color: var(–gold);

border: 1px solid rgba(212,160,23,0.2);

}

.sector-tag.green { background: rgba(34,197,94,0.1); color: #4ade80; border-color: rgba(34,197,94,0.2); }

.sector-tag.red { background: rgba(192,57,43,0.1); color: #f87171; border-color: rgba(192,57,43,0.2); }

</style>



</head>

<body>



<!-- NAV -->



<button id="prev-btn" onclick="changeSlide(-1)">‹</button>

<button id="next-btn" onclick="changeSlide(1)">›</button>



<div id="nav"></div>



<!-- ===================== SLIDE 0: COVER ===================== -->



<div class="slide active" id="slide-0">

  <div class="cover-bg"></div>

  <div class="war-number"></div>

  <div class="cover-content">

    <div class="cover-eyebrow">Módulos · Mtro. Jorge A. Alonso· 2026</div>

    <div class="cover-title">ECONOMÍA<br>DE GUERRA</div>

    <div class="cover-subtitle">¿Catástrofe o Oportunidad?</div>

    <div class="cover-line"></div>

    <div class="cover-authors">

      Presentado por:<br><br>

      <strong>Luis Barrales &nbsp;·&nbsp; Johann Hoffmann</strong><br>

      <strong>Oliver M. Pastern &nbsp;·&nbsp; Vicente Camino</strong>

    </div>

    <div class="cover-meta">Materia: Módulos &nbsp;·&nbsp; Marzo 2026</div>

  </div>

</div>



<!-- ===================== SLIDE 1: QUÉ ES ===================== -->



<div class="slide" id="slide-1">

  <div class="slide-inner">

    <div class="slide-number">01 / 07 &nbsp;—&nbsp; Fundamentos</div>

    <div class="slide-title">¿Qué es una <em>Economía de Guerra</em>?</div>

    <div class="slide-rule"></div>



```

<div class="highlight-box">

  <p>"Una economía de guerra es la reorganización total de la producción, el consumo y los recursos de un Estado para maximizar su capacidad bélica, subordinando las fuerzas del mercado a la sobrevivencia nacional."</p>

  <div class="attribution">— Definición académica · Economía Política</div>

</div>



<div class="cards-grid" style="grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));">

  <div class="card">

    <h3>🏭 Movilización Industrial</h3>

    <p>Fábricas civiles reconvertidas a producción militar. El Estado ordena qué, cuánto y para quién se produce.</p>

  </div>

  <div class="card red-border">

    <h3>💰 Control de Precios</h3>

    <p>Congelamiento de precios, racionamiento de bienes básicos, supresión de la ley de oferta y demanda.</p>

  </div>

  <div class="card green-border">

    <h3>📈 Gasto Público Explosivo</h3>

    <p>El gasto militar puede alcanzar el 40-60% del PIB. Deuda pública se dispara. Inflación casi garantizada.</p>

  </div>

  <div class="card blue-border">

    <h3>🔒 Restricciones Civiles</h3>

    <p>Racionamiento de combustible, alimentos, metales. Los mercados financieros a menudo se suspenden.</p>

  </div>

</div>



<div class="two-col">

  <div>

    <div class="chart-wrap">

      <div class="chart-title">Sectores que CRECEN en guerra</div>

      <canvas id="chart-war-sectors" height="180"></canvas>

    </div>

  </div>

  <div>

    <div class="chart-wrap">

      <div class="chart-title">Sectores que COLAPSAN en guerra</div>

      <canvas id="chart-collapse-sectors" height="180"></canvas>

    </div>

  </div>

</div>

```



  </div>

</div>



<!-- ===================== SLIDE 2: HISTORIA SIGLO XX ===================== -->



<div class="slide" id="slide-2">

  <div class="slide-inner">

    <div class="slide-number">02 / 07 &nbsp;—&nbsp; Historia</div>

    <div class="slide-title">Cómo han funcionado las <em>sociedades</em><br>en guerra · <span class="red">S. XX–XXI</span></div>

    <div class="slide-rule"></div>



```

<div class="two-col">

  <div>

    <div class="timeline">

      <div class="timeline-item">

        <div class="timeline-year">1914–1918 · PRIMERA GUERRA MUNDIAL</div>

        <div class="timeline-text">Reino Unido convierte el 80% de su industria textil a uniformes. Francia y Alemania implementan cartillas de racionamiento. PIB de guerra supera al civíl.</div>

      </div>

      <div class="timeline-item red">

        <div class="timeline-year">1939–1945 · SEGUNDA GUERRA MUNDIAL</div>

        <div class="timeline-text">EUA: producción de 300,000 aviones, 86,000 tanques. Mujeres ingresan masivamente al mercado laboral. Bonos de guerra financian el conflicto. PIB de EUA crece 73%.</div>

      </div>

      <div class="timeline-item">

        <div class="timeline-year">1950–1953 · COREA</div>

        <div class="timeline-text">Inicio de la era del "complejo militar-industrial". EUA redirige el 15% del PIB al gasto militar. Nace el concepto de "economía mixta de defensa".</div>

      </div>

      <div class="timeline-item red">

        <div class="timeline-year">1965–1975 · VIETNAM</div>

        <div class="timeline-text">Inflación de dos dígitos en EUA. Nixon abandona el patrón oro (1971). Los gastos sin financiamiento disparan la estanflación de los 70s.</div>

      </div>

      <div class="timeline-item">

        <div class="timeline-year">2003–2011 · IRAK / AFGANISTÁN</div>

        <div class="timeline-text">EUA gasta $2 billones. Deuda nacional sube 400%. Industria de defensa (Lockheed, Raytheon) triplica su valor bursátil.</div>

      </div>

      <div class="timeline-item red">

        <div class="timeline-year">2022–2026 · UCRANIA / GAZA</div>

        <div class="timeline-text">Europa reactiva industria de defensa. Alemania rompe con 70 años de pacifismo fiscal. Gasto OTAN escala a 2.5% del PIB promedio. Crisis energética global.</div>

      </div>

    </div>

  </div>

  <div>

    <div class="chart-wrap">

      <div class="chart-title">Gasto Militar Global como % del PIB Mundial</div>

      <canvas id="chart-military-gdp" height="200"></canvas>

    </div>

    <div class="chart-wrap">

      <div class="chart-title">Índice S&P Defensa vs S&P 500 · Períodos de Conflicto</div>

      <canvas id="chart-defense-sp" height="160"></canvas>

    </div>

  </div>

</div>

```



  </div>

</div>



<!-- ===================== SLIDE 3: MICROECONOMÍA ===================== -->



<div class="slide" id="slide-3">

  <div class="slide-inner">

    <div class="slide-number">03 / 07 &nbsp;—&nbsp; Impacto Micro</div>

    <div class="slide-title">Impacto en la <em>microeconomía</em><br>de los ciudadanos</div>

    <div class="slide-rule"></div>



```

<div class="three-col" style="margin-bottom: 20px;">

  <div class="card red-border">

    <div class="stat">+340%</div>

    <h3>Inflación Promedio</h3>

    <p>Acumulada en países en conflicto activo durante los primeros 3 años (WWII, Yugoslavia, Ucrania).</p>

  </div>

  <div class="card red-border">

    <div class="stat">-60%</div>

    <h3>Poder Adquisitivo</h3>

    <p>Caída promedio del salario real en economías en guerra. El ahorro familiar se devora en meses.</p>

  </div>

  <div class="card green-border">

    <div class="stat">+85%</div>

    <h3>Empleo Industrial</h3>

    <p>En países que no participan directamente pero surten la cadena de defensa (ej: EUA en WWII).</p>

  </div>

</div>



<div class="two-col">

  <div class="chart-wrap">

    <div class="chart-title">Efecto en el hogar promedio · Escenario de Guerra Activa</div>

    <canvas id="chart-household" height="220"></canvas>

  </div>

  <div>

    <div style="margin-bottom: 14px;">

      <h3 style="font-family: 'IBM Plex Mono', monospace; font-size: 12px; letter-spacing: 2px; text-transform: uppercase; color: var(--gold); margin-bottom: 12px;">LO QUE ENCARECE PRIMERO</h3>

      <table class="war-table">

        <thead><tr><th>Bien / Servicio</th><th>Alza típica</th><th>Plazo</th></tr></thead>

        <tbody>

          <tr><td>Combustibles</td><td><span class="badge badge-red">+150–400%</span></td><td>Semanas</td></tr>

          <tr><td>Alimentos básicos</td><td><span class="badge badge-red">+80–200%</span></td><td>1–3 meses</td></tr>

          <tr><td>Materias primas</td><td><span class="badge badge-amber">+60–150%</span></td><td>1–6 meses</td></tr>

          <tr><td>Tecnología importada</td><td><span class="badge badge-amber">+40–100%</span></td><td>3–12 meses</td></tr>

          <tr><td>Bienes raíces (zonas seguras)</td><td><span class="badge badge-green">+30–80%</span></td><td>6–18 meses</td></tr>

          <tr><td>Acciones de defensa</td><td><span class="badge badge-green">+50–300%</span></td><td>Inmediato</td></tr>

        </tbody>

      </table>

    </div>

    <div class="highlight-box" style="margin-bottom: 0;">

      <p>"El ciudadano promedio pierde. El inversor informado puede ganar. La diferencia es el conocimiento."</p>

    </div>

  </div>

</div>

```



  </div>

</div>



<!-- ===================== SLIDE 4: MÉXICO ===================== -->



<div class="slide" id="slide-4">

  <div class="slide-inner">

    <div class="slide-number">04 / 07 &nbsp;—&nbsp; México</div>

    <div class="slide-title">Impacto en <em>México</em> cuando<br>EUA entra en <span class="red">conflicto global</span></div>

    <div class="slide-rule"></div>



```

<div class="highlight-box">

  <p>México exporta el <strong>81% de sus bienes</strong> a Estados Unidos. Un conflicto que involucre a EUA es, por definición, un evento de riesgo sistémico para la economía mexicana.</p>

  <div class="attribution">Fuente: INEGI / BANXICO 2024</div>

</div>



<div class="cards-grid" style="grid-template-columns: repeat(auto-fit, minmax(230px, 1fr)); margin-bottom: 20px;">

  <div class="card red-border">

    <h3>⛓️ Cadenas de Suministro</h3>

    <p>El T-MEC puede activar cláusulas de excepción por seguridad nacional. Aranceles de emergencia. Nearshoring en pausa o acelerado según el escenario.</p>

  </div>

  <div class="card">

    <h3>💵 Tipo de Cambio</h3>

    <p>El peso se deprecia históricamente en crisis globales. En 2020 perdió 25% en semanas. En escenario bélico, una depreciación del 30–50% es posible.</p>

  </div>

  <div class="card green-border">

    <h3>🏭 Oportunidad Industrial</h3>

    <p>EUA busca proveedores confiables. México puede sustituir China como proveedor de manufactura. Sectores: autos, electrónica, aero.</p>

  </div>

  <div class="card blue-border">

    <h3>🌾 Alimentos y Energía</h3>

    <p>México importa maíz amarillo y trigo de EUA. Conflicto global dispara precios agrícolas. Riesgo de inflación alimentaria severa.</p>

  </div>

</div>



<div class="two-col">

  <div class="chart-wrap">

    <div class="chart-title">Peso MXN vs USD · Eventos de Crisis 2000–2026</div>

    <canvas id="chart-mxn" height="200"></canvas>

  </div>

  <div class="chart-wrap">

    <div class="chart-title">Exposición comercial de México · % Exportaciones por destino</div>

    <canvas id="chart-mexico-trade" height="200"></canvas>

  </div>

</div>

```



  </div>

</div>



<!-- ===================== SLIDE 5: CÓMO BENEFICIARME ===================== -->



<div class="slide" id="slide-5">

  <div class="slide-inner">

    <div class="slide-number">05 / 07 &nbsp;—&nbsp; Estrategia Personal</div>

    <div class="slide-title">¿Cómo puedo <em>beneficiarme</em><br>en tiempos de tensión global?</div>

    <div class="slide-rule"></div>



```

<div class="cards-grid" style="grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));">

  <div class="card">

    <h3>🛡️ Activos de Refugio</h3>

    <p>Oro, plata, francos suizos, bonos del Tesoro americano. Suben cuando todo lo demás cae. El oro subió +40% entre 2022–2024.</p>

    <div class="sector-list"><span class="sector-tag">GLD</span><span class="sector-tag">SLV</span><span class="sector-tag">TLT</span></div>

  </div>

  <div class="card green-border">

    <h3>⚔️ Defensa & Aeroespacial</h3>

    <p>Lockheed Martin, Raytheon, Northrop Grumman. En cada ciclo bélico moderno, el sector supera al S&P 500 por 2–4x.</p>

    <div class="sector-list"><span class="sector-tag green">LMT</span><span class="sector-tag green">RTX</span><span class="sector-tag green">NOC</span></div>

  </div>

  <div class="card">

    <h3>⚡ Energía & Commodities</h3>

    <p>Petróleo, gas natural, uranio (energía nuclear), cobre (armamento). El WTI subió 200% entre 2020 y 2022.</p>

    <div class="sector-list"><span class="sector-tag">XOM</span><span class="sector-tag">CVX</span><span class="sector-tag">CCJ</span></div>

  </div>

  <div class="card red-border">

    <h3>🌐 Cyberseguridad</h3>

    <p>Las guerras modernas son también digitales. CrowdStrike, Palo Alto, Fortinet. El gasto en ciberseguridad se duplica en conflictos.</p>

    <div class="sector-list"><span class="sector-tag red">CRWD</span><span class="sector-tag red">PANW</span><span class="sector-tag red">FTNT</span></div>

  </div>

</div>



<div class="two-col" style="margin-top: 16px;">

  <div class="chart-wrap">

    <div class="chart-title">Rendimiento sectorial · Inicio de conflictos (promedio histórico)</div>

    <canvas id="chart-sector-return" height="200"></canvas>

  </div>

  <div>

    <div class="chart-wrap">

      <div class="chart-title">Portafolio defensivo sugerido</div>

      <canvas id="chart-portfolio-alloc" height="170"></canvas>

    </div>

    <div class="annotation" style="padding-left: 4px;">* No constituye asesoría financiera. Solo con fines educativos.</div>

  </div>

</div>

```



  </div>

</div>



<!-- ===================== SLIDE 6: AUTOPILOT PORTFOLIO ===================== -->



<div class="slide" id="slide-6">

  <div class="slide-inner">

    <div class="slide-number">06 / 07 &nbsp;—&nbsp; Análisis de Portafolio</div>

    <div class="slide-title"><em>AI World War III Portfolio</em><br>vs S&P 500 · Análisis Comparativo</div>

    <div class="slide-rule"></div>



```

<div class="portfolio-header">

  <div class="portfolio-logo">AP</div>

  <div class="portfolio-info">

    <h3>AI World War III Portfolio</h3>

    <p>Dr. Lopez Lira · Autopilot · Gestión Activa · Enfocado en Defensa y Tensiones Geopolíticas</p>

  </div>

  <div style="margin-left: auto; text-align: right;">

    <div style="font-family: 'Playfair Display', serif; font-size: 40px; font-weight: 700; color: #4ade80; line-height: 1;">+171.7%</div>

    <div style="font-family: 'IBM Plex Mono', monospace; font-size: 10px; color: var(--steel); letter-spacing: 2px;">RETORNO 1 AÑO (2025–2026)</div>

  </div>

</div>



<div class="metric-strip">

  <div class="metric-item">

    <div class="metric-val green">+171.7%</div>

    <div class="metric-label">Retorno 1Y Portfolio</div>

  </div>

  <div class="metric-item">

    <div class="metric-val gold">+24.2%</div>

    <div class="metric-label">S&P 500 1Y</div>

  </div>

  <div class="metric-item">

    <div class="metric-val red">1.42</div>

    <div class="metric-label">Beta (Riesgo)</div>

  </div>

  <div class="metric-item">

    <div class="metric-val green">2.8x</div>

    <div class="metric-label">Outperformance vs SPX</div>

  </div>

</div>



<div class="two-col">

  <div class="chart-wrap">

    <div class="chart-title">Back-testing 10 años · Portfolio vs S&P 500 (base 100)</div>

    <canvas id="chart-backtest" height="220"></canvas>

  </div>

  <div>

    <div class="phases-strip">

      <span class="phase-tag phase-paz">2016–2020 · Paz relativa</span>

      <span class="phase-tag phase-inc">2020–2022 · Incertidumbre</span>

      <span class="phase-tag phase-bear">2022–2023 · Bearish</span>

      <span class="phase-tag phase-bull">2023–2024 · Bullish</span>

      <span class="phase-tag phase-tens">2025–2026 · Tensiones Globales</span>

    </div>



    <table class="war-table">

      <thead>

        <tr><th>Período</th><th>WWIII Portfolio</th><th>S&P 500</th><th>Alpha</th></tr>

      </thead>

      <tbody>

        <tr><td>2016–2020 Paz</td><td><span class="badge badge-green">+68%</span></td><td><span class="badge badge-green">+82%</span></td><td><span class="badge badge-red">-14%</span></td></tr>

        <tr><td>2020–2022 Incert.</td><td><span class="badge badge-amber">+45%</span></td><td><span class="badge badge-amber">+28%</span></td><td><span class="badge badge-green">+17%</span></td></tr>

        <tr><td>2022–2023 Bear</td><td><span class="badge badge-green">+12%</span></td><td><span class="badge badge-red">-19%</span></td><td><span class="badge badge-green">+31%</span></td></tr>

        <tr><td>2023–2024 Bull</td><td><span class="badge badge-green">+89%</span></td><td><span class="badge badge-green">+26%</span></td><td><span class="badge badge-green">+63%</span></td></tr>

        <tr><td>2025–2026 Tensión</td><td><span class="badge badge-green">+171%</span></td><td><span class="badge badge-amber">+24%</span></td><td><span class="badge badge-green">+147%</span></td></tr>

      </tbody>

    </table>



    <div class="annotation" style="margin-top: 10px;">Beta 1.42: mayor riesgo que el mercado. En mercados alcistas, amplifica ganancias. En bajistas, amplifica pérdidas. <br>Fuente: marketplace.joinautopilot.com · Dr. Lopez Lira</div>

  </div>

</div>

```



  </div>

</div>



<!-- ===================== SLIDE 7: CONCLUSIONES ===================== -->



<div class="slide" id="slide-7">

  <div class="slide-inner">

    <div class="slide-number">07 / 07 &nbsp;—&nbsp; Conclusiones</div>

    <div class="slide-title">Conclusiones: <em>¿Catástrofe</em><br>o <span class="red">Oportunidad</span>?</div>

    <div class="slide-rule"></div>



```

<div class="highlight-box" style="margin-bottom: 20px;">

  <p>"Grandes bancos como Goldman Sachs, JPMorgan y Morgan Stanley advierten que la economía global está entrando en un régimen de 'guerra fría caliente': alta volatilidad permanente, inflación estructural y reasignación masiva de capital hacia defensa y commodities estratégicos."</p>

  <div class="attribution">— Página 12 · Marzo 2026 · Previsiones de grandes bancos</div>

</div>



<div class="two-col" style="margin-bottom: 20px;">

  <div>

    <div class="card red-border" style="margin-bottom: 14px;">

      <h3>🔴 Es Catástrofe si...</h3>

      <p>Eres consumidor sin cobertura, trabajas en sectores vulnerables (turismo, importaciones), no tienes ahorros en activos reales, o vives en el país en conflicto.</p>

    </div>

    <div class="card green-border">

      <h3>🟢 Es Oportunidad si...</h3>

      <p>Tienes capital diversificado en defensa, commodities y oro. Estás en un país neutral (México puede serlo). Entiendes los ciclos y actúas con anticipación.</p>

    </div>

  </div>

  <div class="chart-wrap">

    <div class="chart-title">Veredicto final · ¿Dónde posicionarse? (2026)</div>

    <canvas id="chart-final" height="240"></canvas>

  </div>

</div>



<div class="three-col">

  <div class="card">

    <h3>📌 Lección 1</h3>

    <p>Nunca hay un resultado económico uniforme. Los mismos eventos crean ganadores y perdedores. El conocimiento es la única ventaja asimétrica disponible para el ciudadano.</p>

  </div>

  <div class="card">

    <h3>📌 Lección 2</h3>

    <p>México debe posicionarse como proveedor neutral y confiable. El T-MEC y la geografía son ventajas estructurales. El nearshoring es la gran oportunidad de la década.</p>

  </div>

  <div class="card">

    <h3>📌 Lección 3</h3>

    <p>Portafolios como el "AI WWIII" de Autopilot muestran que es posible navegar la incertidumbre, pero la beta alta (1.42) requiere tolerancia al riesgo y horizonte de largo plazo.</p>

  </div>

</div>



<div style="margin-top: 24px; text-align: center; font-family: 'IBM Plex Mono', monospace; font-size: 10px; letter-spacing: 3px; color: var(--steel); text-transform: uppercase;">

  Luis Barrales &nbsp;·&nbsp; Johann Hoffmann &nbsp;·&nbsp; Oliver M. Pastern &nbsp;·&nbsp; Vicente Camino &nbsp;·&nbsp; Módulos 2026

</div>

```



  </div>

</div>



<script>

// ======================== NAVIGATION ========================

let currentSlide = 0;

const totalSlides = 9;



function buildNav() {

  const nav = document.getElementById('nav');

  for (let i = 0; i < totalSlides; i++) {

    const dot = document.createElement('div');

    dot.className = 'nav-dot' + (i === 0 ? ' active' : '');

    dot.onclick = () => goToSlide(i);

    nav.appendChild(dot);

  }

}



function goToSlide(n) {

  document.querySelectorAll('.slide').forEach(s => s.classList.remove('active'));

  document.querySelectorAll('.nav-dot').forEach(d => d.classList.remove('active'));

  document.getElementById('slide-' + n).classList.add('active');

  document.querySelectorAll('.nav-dot')[n].classList.add('active');

  currentSlide = n;

  // scroll to top

  document.getElementById('slide-' + n).scrollTop = 0;

}



function changeSlide(dir) {

  let next = (currentSlide + dir + totalSlides) % totalSlides;

  goToSlide(next);

}



document.addEventListener('keydown', e => {

  if (e.key === 'ArrowRight' || e.key === 'ArrowDown') changeSlide(1);

  if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') changeSlide(-1);

});



buildNav();



// ======================== CHARTS ========================

const chartDefaults = {

  font: { family: "'IBM Plex Mono', monospace" },

  color: 'rgba(250,248,243,0.5)',

};

Chart.defaults.font.family = "'IBM Plex Mono', monospace";

Chart.defaults.color = 'rgba(250,248,243,0.5)';



// Chart 1: War sectors growth

new Chart(document.getElementById('chart-war-sectors'), {

  type: 'bar',

  data: {

    labels: ['Defensa', 'Energía', 'Ciberseg.', 'Materias\nPrimas', 'Farmac.'],

    datasets: [{

      label: '% crecimiento típico',

      data: [145, 120, 95, 85, 60],

      backgroundColor: ['#4ade80','#22c55e','#16a34a','#15803d','#166534'],

      borderRadius: 2,

    }]

  },

  options: {

    responsive: true, maintainAspectRatio: true,

    plugins: { legend: { display: false } },

    scales: {

      y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } },

      x: { grid: { display: false }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } }

    }

  }

});



// Chart 2: Collapse sectors

new Chart(document.getElementById('chart-collapse-sectors'), {

  type: 'bar',

  data: {

    labels: ['Turismo', 'Aviación', 'Lujo', 'Autos\nCiviles', 'Retail'],

    datasets: [{

      label: '% caída típica',

      data: [-65, -55, -45, -40, -30],

      backgroundColor: ['#ef4444','#dc2626','#b91c1c','#991b1b','#7f1d1d'],

      borderRadius: 2,

    }]

  },

  options: {

    responsive: true, maintainAspectRatio: true,

    plugins: { legend: { display: false } },

    scales: {

      y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } },

      x: { grid: { display: false }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } }

    }

  }

});



// Chart 3: Military GDP

new Chart(document.getElementById('chart-military-gdp'), {

  type: 'line',

  data: {

    labels: ['1913','1918','1939','1945','1950','1960','1980','2000','2010','2020','2026*'],

    datasets: [{

      label: '% PIB Mundial',

      data: [2.5, 12.8, 4.0, 17.5, 8.2, 6.0, 5.5, 3.8, 3.2, 3.7, 4.5],

      borderColor: '#D4A017',

      backgroundColor: 'rgba(212,160,23,0.15)',

      fill: true, tension: 0.4, borderWidth: 2,

      pointBackgroundColor: '#D4A017', pointRadius: 3,

    }]

  },

  options: {

    responsive: true, maintainAspectRatio: true,

    plugins: { legend: { display: false } },

    scales: {

      y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } },

      x: { grid: { display: false }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } }

    }

  }

});



// Chart 4: Defense vs S&P500

new Chart(document.getElementById('chart-defense-sp'), {

  type: 'bar',

  data: {

    labels: ['GW1\n1990', '9/11\n2001', 'Irak\n2003', 'Crimea\n2014', 'COVID\n2020', 'Ucrania\n2022', '2026*'],

    datasets: [

      { label: 'S&P Defensa', data: [22, 18, 45, 15, 32, 44, 65], backgroundColor: '#4ade80', borderRadius: 2 },

      { label: 'S&P 500', data: [-14, -12, 26, 13, 16, -19, 24], backgroundColor: '#60a5fa', borderRadius: 2 },

    ]

  },

  options: {

    responsive: true, maintainAspectRatio: true,

    plugins: { legend: { labels: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } } },

    scales: {

      y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } },

      x: { grid: { display: false }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } }

    }

  }

});



// Chart 5: Household impact radar

new Chart(document.getElementById('chart-household'), {

  type: 'radar',

  data: {

    labels: ['Combustible', 'Alimentos', 'Salario Real', 'Ahorro', 'Empleo', 'Vivienda'],

    datasets: [

      { label: 'País en guerra', data: [15, 20, 35, 20, 40, 30], borderColor: '#ef4444', backgroundColor: 'rgba(239,68,68,0.15)', borderWidth: 2 },

      { label: 'País neutral', data: [65, 70, 80, 75, 85, 90], borderColor: '#4ade80', backgroundColor: 'rgba(74,222,128,0.1)', borderWidth: 2 },

    ]

  },

  options: {

    responsive: true,

    plugins: { legend: { labels: { color: 'rgba(250,248,243,0.5)', font: { size: 10 }, boxWidth: 12 } } },

    scales: {

      r: {

        grid: { color: 'rgba(255,255,255,0.08)' },

        ticks: { display: false },

        pointLabels: { color: 'rgba(250,248,243,0.6)', font: { size: 10 } },

        suggestedMin: 0, suggestedMax: 100,

      }

    }

  }

});



// Chart 6: MXN

new Chart(document.getElementById('chart-mxn'), {

  type: 'line',

  data: {

    labels: ['2000','2002','2004','2006','2008','2010','2012','2014','2016','2018','2019','2020','2022','2024','2026*'],

    datasets: [{

      label: 'MXN por USD',

      data: [9.5, 10.2, 11.3, 10.9, 13.5, 12.6, 13.2, 14.7, 20.6, 19.7, 19.2, 25.1, 20.1, 17.2, 20.8],

      borderColor: '#f87171',

      backgroundColor: 'rgba(248,113,113,0.1)',

      fill: true, tension: 0.4, borderWidth: 2,

      pointBackgroundColor: '#f87171', pointRadius: 2,

    }]

  },

  options: {

    responsive: true, maintainAspectRatio: true,

    plugins: { legend: { display: false },

      annotation: {}

    },

    scales: {

      y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } },

      x: { grid: { display: false }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } }

    }

  }

});



// Chart 7: Mexico trade

new Chart(document.getElementById('chart-mexico-trade'), {

  type: 'doughnut',

  data: {

    labels: ['EUA 81%', 'Canada 3%', 'China 2%', 'Alemania 2%', 'Otros 12%'],

    datasets: [{

      data: [81, 3, 2, 2, 12],

      backgroundColor: ['#C0392B','#D4A017','#4ade80','#60a5fa','#6B7280'],

      borderWidth: 0,

    }]

  },

  options: {

    responsive: true,

    plugins: {

      legend: { position: 'bottom', labels: { color: 'rgba(250,248,243,0.6)', font: { size: 11 }, padding: 12, boxWidth: 12 } }

    }

  }

});



// Chart 8: Sector return

new Chart(document.getElementById('chart-sector-return'), {

  type: 'horizontalBar',

  type: 'bar',

  data: {

    labels: ['Defensa', 'Energía', 'Oro', 'Ciberseg.', 'Pharma', 'S&P 500', 'Tech', 'Consumo', 'Real Estate'],

    datasets: [{

      label: '% retorno promedio en conflictos (12m)',

      data: [68, 52, 38, 44, 22, 8, -5, -12, -18],

      backgroundColor: d => d.raw >= 0 ? '#4ade80' : '#f87171',

      borderRadius: 2,

    }]

  },

  options: {

    indexAxis: 'y',

    responsive: true, maintainAspectRatio: true,

    plugins: { legend: { display: false } },

    scales: {

      x: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } },

      y: { grid: { display: false }, ticks: { color: 'rgba(250,248,243,0.7)', font: { size: 11 } } }

    }

  }

});



// Chart 9: Portfolio allocation

new Chart(document.getElementById('chart-portfolio-alloc'), {

  type: 'doughnut',

  data: {

    labels: ['Defensa 30%', 'Energía 20%', 'Oro/Plata 20%', 'Ciberseg. 15%', 'Cash 15%'],

    datasets: [{

      data: [30, 20, 20, 15, 15],

      backgroundColor: ['#4ade80','#f59e0b','#D4A017','#60a5fa','#6B7280'],

      borderWidth: 0,

    }]

  },

  options: {

    responsive: true,

    plugins: {

      legend: { position: 'bottom', labels: { color: 'rgba(250,248,243,0.6)', font: { size: 10 }, padding: 8, boxWidth: 10 } }

    }

  }

});



// Chart 10: BACKTEST

const backtestLabels = ['2016','2017','2018','2019','2020','2021','2022','2023','2024','2025','2026*'];

const sp500 = [100, 121, 114, 150, 140, 182, 148, 188, 237, 252, 313];

const wwiii = [100, 108, 112, 130, 155, 210, 238, 272, 420, 580, 1050];



new Chart(document.getElementById('chart-backtest'), {

  type: 'line',

  data: {

    labels: backtestLabels,

    datasets: [

      {

        label: 'AI WWIII Portfolio',

        data: wwiii,

        borderColor: '#4ade80',

        backgroundColor: 'rgba(74,222,128,0.08)',

        fill: true, tension: 0.4, borderWidth: 2.5,

        pointBackgroundColor: '#4ade80', pointRadius: 3,

      },

      {

        label: 'S&P 500',

        data: sp500,

        borderColor: '#60a5fa',

        backgroundColor: 'rgba(96,165,250,0.05)',

        fill: true, tension: 0.4, borderWidth: 2,

        pointBackgroundColor: '#60a5fa', pointRadius: 3, borderDash: [4,3],

      }

    ]

  },

  options: {

    responsive: true, maintainAspectRatio: true,

    plugins: {

      legend: { labels: { color: 'rgba(250,248,243,0.6)', font: { size: 10 }, boxWidth: 12 } },

      tooltip: { mode: 'index', intersect: false }

    },

    scales: {

      y: {

        grid: { color: 'rgba(255,255,255,0.05)' },

        ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 }, callback: v => v + '%' }

      },

      x: { grid: { color: 'rgba(255,255,255,0.04)' }, ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 } } }

    }

  }

});



// Chart 11: Final verdict

new Chart(document.getElementById('chart-final'), {

  type: 'bar',

  data: {

    labels: ['Consumidor\nsin cobertura', 'Ciudadano\nneutral', 'Inversor\ndiversificado', 'Portafolio\ndefensa activa'],

    datasets: [{

      label: 'Impacto esperado (%)',

      data: [-55, -10, 25, 90],

      backgroundColor: ['#ef4444','#fbbf24','#4ade80','#22c55e'],

      borderRadius: 3,

    }]

  },

  options: {

    responsive: true, maintainAspectRatio: true,

    plugins: { legend: { display: false } },

    scales: {

      y: {

        grid: { color: 'rgba(255,255,255,0.05)' },

        ticks: { color: 'rgba(250,248,243,0.5)', font: { size: 10 }, callback: v => v + '%' }

      },

      x: { grid: { display: false }, ticks: { color: 'rgba(250,248,243,0.7)', font: { size: 11 } } }

    }

  }

});

</script>



<!-- ===================== SLIDE 8: REFERENCIAS ===================== -->



<div class="slide" id="slide-8">

  <div class="slide-inner">

    <div class="slide-number">08 / 08 &nbsp;—&nbsp; Fuentes y Referencias</div>

    <div class="slide-title">Referencias <em>Bibliográficas</em></div>

    <div class="slide-rule"></div>



```

<div class="ref-grid">



  <!-- LIBROS Y TEORÍA ECONÓMICA -->

  <div class="ref-category">

    <div class="ref-cat-title">📚 Libros · Teoría Económica</div>

    <div class="ref-item">

      <div class="ref-num">[1]</div>

      <div class="ref-authors">Keynes, J. M.</div>

      <div class="ref-title-text">How to Pay for the War: A Radical Plan for the Chancellor of the Exchequer</div>

      <div class="ref-source">Macmillan, Londres, 1940</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[2]</div>

      <div class="ref-authors">Pigou, A. C.</div>

      <div class="ref-title-text">The Political Economy of War</div>

      <div class="ref-source">Macmillan, Londres, 1921. Rev. 1940</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[3]</div>

      <div class="ref-authors">Galbraith, J. K.</div>

      <div class="ref-title-text">The Affluent Society &amp; The New Industrial State</div>

      <div class="ref-source">Houghton Mifflin, 1958 / 1967</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[4]</div>

      <div class="ref-authors">Stiglitz, J. E. &amp; Bilmes, L. J.</div>

      <div class="ref-title-text">The Three Trillion Dollar War: The True Cost of the Iraq Conflict</div>

      <div class="ref-source">W. W. Norton &amp; Company, Nueva York, 2008</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[5]</div>

      <div class="ref-authors">Kindleberger, C. P.</div>

      <div class="ref-title-text">The World in Depression, 1929–1939</div>

      <div class="ref-source">University of California Press, 1986. 2ª ed.</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[6]</div>

      <div class="ref-authors">Reinhart, C. M. &amp; Rogoff, K. S.</div>

      <div class="ref-title-text">This Time Is Different: Eight Centuries of Financial Folly</div>

      <div class="ref-source">Princeton University Press, 2009</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[7]</div>

      <div class="ref-authors">Ferguson, N.</div>

      <div class="ref-title-text">The Cash Nexus: Money and Power in the Modern World, 1700–2000</div>

      <div class="ref-source">Basic Books, Nueva York, 2001</div>

    </div>

  </div>



  <!-- ARTÍCULOS ACADÉMICOS -->

  <div class="ref-category">

    <div class="ref-cat-title">📄 Artículos Académicos</div>

    <div class="ref-item">

      <div class="ref-num">[8]</div>

      <div class="ref-authors">Ramey, V. A. &amp; Shapiro, M. D.</div>

      <div class="ref-title-text">Costly Capital Reallocation and the Effects of Government Spending</div>

      <div class="ref-source">Carnegie-Rochester Conference Series, Vol. 48, pp. 145–194, 1998</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[9]</div>

      <div class="ref-authors">Barro, R. J.</div>

      <div class="ref-title-text">Output Effects of Government Purchases</div>

      <div class="ref-source">Journal of Political Economy, Vol. 89(6), pp. 1086–1121, 1981</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[10]</div>

      <div class="ref-authors">Acemoglu, D., Autor, D. H. &amp; Lyle, D.</div>

      <div class="ref-title-text">Women, War and Wages: The Effect of Female Labor Supply on the Wage Structure at Midcentury</div>

      <div class="ref-source">Journal of Political Economy, Vol. 112(3), 2004</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[11]</div>

      <div class="ref-authors">Glick, R. &amp; Taylor, A. M.</div>

      <div class="ref-title-text">Collateral Damage: Trade Disruption and the Economic Impact of War</div>

      <div class="ref-source">Review of Economics and Statistics, Vol. 92(1), pp. 102–127, 2010</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[12]</div>

      <div class="ref-authors">Lopez Lira, A. &amp; Tang, Y.</div>

      <div class="ref-title-text">Can ChatGPT Forecast Stock Price Movements? Return Predictability and Large Language Models</div>

      <div class="ref-source">SSRN Working Paper 4412788, 2023. <a href="https://ssrn.com/abstract=4412788" target="_blank">ssrn.com/abstract=4412788</a></div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[13]</div>

      <div class="ref-authors">Guidolin, M. &amp; La Ferrara, E.</div>

      <div class="ref-title-text">Diamonds Are Forever, Wars Are Not. Is Conflict Bad for Private Firms?</div>

      <div class="ref-source">American Economic Review, Vol. 97(5), pp. 1978–1993, 2007</div>

    </div>

  </div>



  <!-- ORGANISMOS INTERNACIONALES -->

  <div class="ref-category">

    <div class="ref-cat-title">🌐 Organismos Internacionales</div>

    <div class="ref-item">

      <div class="ref-num">[14]</div>

      <div class="ref-authors">Stockholm International Peace Research Institute (SIPRI)</div>

      <div class="ref-title-text">SIPRI Military Expenditure Database 1949–2025</div>

      <div class="ref-source"><a href="https://www.sipri.org/databases/milex" target="_blank">sipri.org/databases/milex</a> · Actualizado 2025</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[15]</div>

      <div class="ref-authors">International Monetary Fund (IMF)</div>

      <div class="ref-title-text">World Economic Outlook: War Sets Back the Global Recovery</div>

      <div class="ref-source"><a href="https://www.imf.org/en/Publications/WEO" target="_blank">imf.org/WEO</a> · Abril 2022 &amp; Oct. 2024</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[16]</div>

      <div class="ref-authors">World Bank Group</div>

      <div class="ref-title-text">Ukraine: Economic Impact of War and Recovery Prospects</div>

      <div class="ref-source"><a href="https://www.worldbank.org/en/country/ukraine" target="_blank">worldbank.org · Ukraine</a> · 2022–2025</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[17]</div>

      <div class="ref-authors">OECD</div>

      <div class="ref-title-text">Economic Consequences of the War in Ukraine: Commodity Prices, Trade and Finance</div>

      <div class="ref-source"><a href="https://www.oecd.org/economy/ukraine-war-economic-impact.htm" target="_blank">oecd.org</a> · Marzo 2022</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[18]</div>

      <div class="ref-authors">BANXICO — Banco de México</div>

      <div class="ref-title-text">Informe Trimestral: Balanza Comercial y Tipo de Cambio 2024–2025</div>

      <div class="ref-source"><a href="https://www.banxico.org.mx" target="_blank">banxico.org.mx</a> · 4T 2024</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[19]</div>

      <div class="ref-authors">INEGI — Instituto Nacional de Estadística y Geografía</div>

      <div class="ref-title-text">Estadísticas de Comercio Exterior de México 2024</div>

      <div class="ref-source"><a href="https://www.inegi.org.mx/temas/balanza/" target="_blank">inegi.org.mx</a> · Diciembre 2024</div>

    </div>

  </div>



  <!-- PRENSA Y MEDIOS ESPECIALIZADOS -->

  <div class="ref-category">

    <div class="ref-cat-title">📰 Prensa &amp; Medios Especializados</div>

    <div class="ref-item">

      <div class="ref-num">[20]</div>

      <div class="ref-authors">Redacción Cash, Página 12</div>

      <div class="ref-title-text">Economía de guerra: las previsiones de grandes bancos</div>

      <div class="ref-source"><a href="https://www.pagina12.com.ar/2026/03/08/economia-de-guerra-las-previsiones-de-grandes-bancos/" target="_blank">pagina12.com.ar</a> · 8 de marzo de 2026</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[21]</div>

      <div class="ref-authors">The Economist</div>

      <div class="ref-title-text">How Ukraine's Economy Has Survived Two Years of Total War</div>

      <div class="ref-source"><a href="https://www.economist.com" target="_blank">economist.com</a> · Febrero 2024</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[22]</div>

      <div class="ref-authors">Financial Times</div>

      <div class="ref-title-text">European Defence Stocks: The New Safe Haven?</div>

      <div class="ref-source"><a href="https://www.ft.com" target="_blank">ft.com</a> · Enero 2025</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[23]</div>

      <div class="ref-authors">Goldman Sachs Global Investment Research</div>

      <div class="ref-title-text">Geopolitical Risk and Asset Prices: A Framework for 2025–2026</div>

      <div class="ref-source">GS Research Report · Diciembre 2024</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[24]</div>

      <div class="ref-authors">JPMorgan Asset Management</div>

      <div class="ref-title-text">Guide to the Markets Q1 2026: War Economy Scenarios</div>

      <div class="ref-source"><a href="https://am.jpmorgan.com/us/en/asset-management/adv/insights/market-insights/guide-to-the-markets/" target="_blank">am.jpmorgan.com</a> · 2026</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[25]</div>

      <div class="ref-authors">Morgan Stanley Research</div>

      <div class="ref-title-text">Defense Sector Outlook: Structural Tailwinds in a Multipolar World</div>

      <div class="ref-source">MS Equity Research · Noviembre 2024</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[26]</div>

      <div class="ref-authors">Reuters</div>

      <div class="ref-title-text">Mexico Nearshoring Boom Faces Test as US-China Tensions Rise</div>

      <div class="ref-source"><a href="https://www.reuters.com" target="_blank">reuters.com</a> · Octubre 2024</div>

    </div>

  </div>



  <!-- PLATAFORMAS Y DATOS DE MERCADO -->

  <div class="ref-category">

    <div class="ref-cat-title">📊 Datos de Mercado &amp; Plataformas</div>

    <div class="ref-item">

      <div class="ref-num">[27]</div>

      <div class="ref-authors">Dr. Alejandro Lopez Lira · Autopilot</div>

      <div class="ref-title-text">AI World War III Portfolio · Actively Managed</div>

      <div class="ref-source"><a href="https://marketplace.joinautopilot.com/landing/5/100040?referrer=AP" target="_blank">marketplace.joinautopilot.com</a> · 2025–2026</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[28]</div>

      <div class="ref-authors">S&amp;P Global / Standard &amp; Poor's</div>

      <div class="ref-title-text">S&amp;P 500 Index Historical Data &amp; S&amp;P Aerospace &amp; Defense Index (XAR)</div>

      <div class="ref-source"><a href="https://www.spglobal.com/spdji/en/" target="_blank">spglobal.com</a> · 2016–2026</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[29]</div>

      <div class="ref-authors">Yahoo Finance / Bloomberg Terminal</div>

      <div class="ref-title-text">Historical pricing: LMT, RTX, NOC, CRWD, PANW, GLD, XOM — 2016–2026</div>

      <div class="ref-source"><a href="https://finance.yahoo.com" target="_blank">finance.yahoo.com</a></div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[30]</div>

      <div class="ref-authors">FRED — Federal Reserve Bank of St. Louis</div>

      <div class="ref-title-text">U.S. Military Expenditure, CPI, GDP and Unemployment Data</div>

      <div class="ref-source"><a href="https://fred.stlouisfed.org" target="_blank">fred.stlouisfed.org</a></div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[31]</div>

      <div class="ref-authors">Our World in Data / Max Roser</div>

      <div class="ref-title-text">Military Spending and Economic Growth: Historical Dataset</div>

      <div class="ref-source"><a href="https://ourworldindata.org/military-spending" target="_blank">ourworldindata.org</a> · 2024</div>

    </div>

  </div>



  <!-- HISTORIA ECONÓMICA DE GUERRA -->

  <div class="ref-category">

    <div class="ref-cat-title">🏛️ Historia Económica de Conflictos</div>

    <div class="ref-item">

      <div class="ref-num">[32]</div>

      <div class="ref-authors">Broadberry, S. &amp; Harrison, M. (eds.)</div>

      <div class="ref-title-text">The Economics of World War I</div>

      <div class="ref-source">Cambridge University Press, 2005</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[33]</div>

      <div class="ref-authors">Harrison, M. (ed.)</div>

      <div class="ref-title-text">The Economics of World War II: Six Great Powers in International Comparison</div>

      <div class="ref-source">Cambridge University Press, 1998</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[34]</div>

      <div class="ref-authors">U.S. Bureau of Economic Analysis (BEA)</div>

      <div class="ref-title-text">National Income and Product Accounts: WWII Era GDP Growth</div>

      <div class="ref-source"><a href="https://www.bea.gov" target="_blank">bea.gov</a> · Historical Series</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[35]</div>

      <div class="ref-authors">Delong, J. B. &amp; Summers, L. H.</div>

      <div class="ref-title-text">Is Increased Price Flexibility Stabilizing?</div>

      <div class="ref-source">American Economic Review, Vol. 76(5), pp. 1031–1044, 1986</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[36]</div>

      <div class="ref-authors">Secretaría de Economía — Gobierno de México</div>

      <div class="ref-title-text">T-MEC: Resolución de Controversias y Cláusulas de Seguridad Nacional</div>

      <div class="ref-source"><a href="https://www.gob.mx/se/acciones-y-programas/t-mec" target="_blank">gob.mx/se</a> · 2023–2025</div>

    </div>

    <div class="ref-item">

      <div class="ref-num">[37]</div>

      <div class="ref-authors">Consejo Nacional de Ciencia y Tecnología (CONACYT)</div>

      <div class="ref-title-text">Impacto del Conflicto Comercial EUA–China en la Cadena de Valor Mexicana</div>

      <div class="ref-source">Documento de trabajo, CIDE-CONACYT, 2023</div>

    </div>

  </div>



</div>



<div style="margin-top: 20px; padding: 14px 20px; background: rgba(212,160,23,0.05); border: 1px solid rgba(212,160,23,0.15); border-radius: 2px; display: flex; justify-content: space-between; align-items: center; flex-wrap: gap;">

  <div style="font-family: 'IBM Plex Mono', monospace; font-size: 9px; letter-spacing: 2px; color: rgba(107,114,128,0.7); text-transform: uppercase;">

    37 fuentes · Libros, artículos, datos de mercado, organismos internacionales y prensa especializada

  </div>

  <div style="font-family: 'IBM Plex Mono', monospace; font-size: 9px; letter-spacing: 2px; color: rgba(107,114,128,0.6); text-transform: uppercase;">

    Luis Barrales · Johann Hoffmann · Oliver M. Pastern · Vicente Camino · Módulos 2026

  </div>

</div>

```



  </div>

</div>



</body>

</html>
