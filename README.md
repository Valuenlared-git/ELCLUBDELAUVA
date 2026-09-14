<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>FiveThirtyEight Style: La Ficción Tradwife y el Mercado Laboral</title>
  
  <!-- CDN Chart.js & PapaParse -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/papaparse@5.4.1/papaparse.min.js"></script>
  
  <!-- Tipografía estilo 538: Decima / Roboto / Atlas Grotesk feel -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@400;500;700&family=Roboto:ital,wght@0,400;0,500;0,700;0,900;1,400&display=swap" rel="stylesheet">

  <style>
    :root {
      --fte-bg: #f0f0f0;
      --fte-card-bg: #ffffff;
      --fte-text: #222222;
      --fte-muted: #666666;
      --fte-border: #cccccc;
      --fte-grid: #e5e5e5;
      
      /* Paleta clásica de datos 538 */
      --fte-red: #ed553b;
      --fte-blue: #008fd5;
      --fte-navy: #1f3552;
      --fte-yellow: #f6c85f;
      --fte-green: #2ecc71;
      --fte-gray-bar: #b2b2b2;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--fte-bg);
      color: var(--fte-text);
      font-family: 'Roboto', -apple-system, BlinkMacSystemFont, sans-serif;
      padding: 2.5rem 1rem;
      -webkit-font-smoothing: antialiased;
    }

    .container {
      max-width: 1180px;
      margin: 0 auto;
    }

    /* 538 Header Block */
    header {
      border-bottom: 2px solid var(--fte-text);
      padding-bottom: 1.25rem;
      margin-bottom: 2rem;
    }

    .kicker {
      font-family: 'Roboto Mono', monospace;
      font-size: 0.75rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: var(--fte-red);
      display: inline-block;
      margin-bottom: 0.35rem;
    }

    h1 {
      font-size: 2.35rem;
      font-weight: 900;
      line-height: 1.15;
      letter-spacing: -0.02em;
      color: var(--fte-text);
      margin-bottom: 0.6rem;
    }

    .deck {
      font-size: 1.1rem;
      line-height: 1.5;
      color: var(--fte-muted);
      max-width: 980px;
    }

    .byline {
      font-family: 'Roboto Mono', monospace;
      font-size: 0.78rem;
      color: var(--fte-muted);
      margin-top: 0.75rem;
      text-transform: uppercase;
    }

    /* Tabs Bar (Navegación editorial) */
    .nav-tabs {
      display: flex;
      border-bottom: 1px solid var(--fte-border);
      margin-bottom: 2rem;
      gap: 0.25rem;
      overflow-x: auto;
    }

    .tab-item {
      background: transparent;
      border: none;
      border-bottom: 3px solid transparent;
      font-family: 'Roboto', sans-serif;
      font-size: 0.95rem;
      font-weight: 700;
      color: var(--fte-muted);
      padding: 0.75rem 1.25rem;
      cursor: pointer;
      text-transform: uppercase;
      letter-spacing: 0.04em;
      transition: all 0.15s ease;
      white-space: nowrap;
    }

    .tab-item:hover {
      color: var(--fte-text);
      background-color: rgba(0, 0, 0, 0.03);
    }

    .tab-item.active {
      color: var(--fte-text);
      border-bottom-color: var(--fte-red);
      background-color: #ffffff;
    }

    /* Scoreboard / Big Numbers 538 style */
    .stat-row {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1.25rem;
      margin-bottom: 2.5rem;
    }

    .stat-box {
      background: var(--fte-card-bg);
      border: 1px solid var(--fte-border);
      border-top: 4px solid var(--fte-navy);
      padding: 1.25rem 1.15rem;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
    }

    .stat-box.highlight {
      border-top-color: var(--fte-red);
    }

    .stat-label {
      font-family: 'Roboto Mono', monospace;
      font-size: 0.75rem;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      color: var(--fte-muted);
      font-weight: 700;
    }

    .stat-number {
      font-family: 'Roboto', sans-serif;
      font-size: 2.3rem;
      font-weight: 900;
      color: var(--fte-text);
      margin: 0.25rem 0;
      letter-spacing: -0.03em;
    }

    .stat-sub {
      font-size: 0.8rem;
      color: var(--fte-muted);
      line-height: 1.35;
    }

    /* Chart Containers */
    .grid-charts {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 1.75rem;
      margin-bottom: 2.5rem;
    }

    @media (max-width: 900px) {
      .grid-charts {
        grid-template-columns: 1fr;
      }
      h1 {
        font-size: 1.8rem;
      }
    }

    .chart-card {
      background: var(--fte-card-bg);
      border: 1px solid var(--fte-border);
      padding: 1.5rem;
      box-shadow: 0 1px 4px rgba(0, 0, 0, 0.04);
      display: flex;
      flex-direction: column;
    }

    .chart-card.full-width {
      grid-column: 1 / -1;
    }

    .chart-headline {
      font-size: 1.15rem;
      font-weight: 800;
      line-height: 1.25;
      color: var(--fte-text);
      margin-bottom: 0.25rem;
    }

    .chart-subhead {
      font-size: 0.85rem;
      color: var(--fte-muted);
      line-height: 1.4;
      margin-bottom: 1.25rem;
    }

    .canvas-wrap {
      position: relative;
      min-height: 290px;
      max-height: 340px;
      flex-grow: 1;
      width: 100%;
    }

    .chart-footer {
      border-top: 1px solid var(--fte-border);
      padding-top: 0.6rem;
      margin-top: 1rem;
      font-family: 'Roboto Mono', monospace;
      font-size: 0.68rem;
      color: var(--fte-muted);
      display: flex;
      justify-content: space-between;
      text-transform: uppercase;
      letter-spacing: 0.03em;
    }

    .hidden {
      display: none !important;
    }

    /* Callout Block (Tesis 538) */
    .callout-538 {
      background: #ffffff;
      border: 1px solid var(--fte-border);
      border-left: 6px solid var(--fte-red);
      padding: 1.5rem;
      margin-bottom: 2rem;
    }

    .callout-538 h3 {
      font-size: 1.1rem;
      font-weight: 800;
      margin-bottom: 0.5rem;
      text-transform: uppercase;
      letter-spacing: 0.03em;
    }

    .callout-538 p {
      font-size: 0.95rem;
      line-height: 1.6;
      color: #333;
    }
  </style>
</head>
<body>

  <div class="container">
    <!-- Header -->
    <header>
      <span class="kicker">Análisis de Datos // Género & Redes Sociales</span>
      <h1>La Ficción del Modelo Tradwife Frente al Mercado Laboral</h1>
      <p class="deck">
        Mientras las plataformas proyectan una vida tradicional estetizada y sin tensiones, los datos socioeconómicos urbanos revelan una realidad signada por la informalidad laboral y la desprotección previsional de los hogares monoparentales.
      </p>
      <div class="byline">Por el equipo de investigación // Encuesta empírica + Estadísticas urbanas</div>
    </header>

    <!-- Pestañas de navegación editorial -->
    <nav class="nav-tabs">
      <button class="tab-item active" data-target="tradwife">Percepción en Redes (Encuesta)</button>
      <button class="tab-item" data-target="macro">Mercado Laboral Urbano</button>
      <button class="tab-item" data-target="tesis">El Doble Rasero Económico</button>
    </nav>

    <!-- SECCIÓN 1: ENCUESTAS TRADWIFE -->
    <section id="tab-tradwife" class="tab-content">
      <div class="stat-row">
        <div class="stat-box highlight">
          <div class="stat-label">Muestra Analizada</div>
          <div class="stat-number">38</div>
          <div class="stat-sub">Casos de personas activas en plataformas digitales.</div>
        </div>
        <div class="stat-box">
          <div class="stat-label">Ficción Percibida</div>
          <div class="stat-number">74%</div>
          <div class="stat-sub">Considera que las redes "mayormente no" o "casi nunca" muestran la realidad del hogar.</div>
        </div>
        <div class="stat-box">
          <div class="stat-label">Impacto Cultural</div>
          <div class="stat-number">95%</div>
          <div class="stat-sub">Afirma que los algoritmos alteran el entendimiento de los roles de género.</div>
        </div>
        <div class="stat-box">
          <div class="stat-label">Red Principal</div>
          <div class="stat-number">66%</div>
          <div class="stat-sub">Instagram lidera el consumo habitual, seguida por TikTok (39.5%).</div>
        </div>
      </div>

      <div class="grid-charts">
        <!-- Gráfico 1 -->
        <div class="chart-card">
          <h2 class="chart-headline">El algoritmo favorece una narrativa idealizada</h2>
          <p class="chart-subhead">Distribución de opiniones sobre cómo se presentan las vidas tradicionales en el feed.</p>
          <div class="canvas-wrap">
            <canvas id="chartPres"></canvas>
          </div>
          <div class="chart-footer">
            <span>Fuente: Encuesta Tradwife (P20)</span>
            <span>FiveThirtyEight Style</span>
          </div>
        </div>

        <!-- Gráfico 2 -->
        <div class="chart-card">
          <h2 class="chart-headline">Belleza física y maternidad eclipsan la independencia</h2>
          <p class="chart-subhead">Rasgos más asociados a la "mujer ideal" construida en plataformas digitales.</p>
          <div class="canvas-wrap">
            <canvas id="chartIdeal"></canvas>
          </div>
          <div class="chart-footer">
            <span>Fuente: Respuestas categorizadas (P22)</span>
            <span>FiveThirtyEight Style</span>
          </div>
        </div>

        <!-- Gráfico 3 -->
        <div class="chart-card">
          <h2 class="chart-headline">Una brecha abrumadora entre el feed y la vida real</h2>
          <p class="chart-subhead">¿Consideran que las redes muestran una representación auténtica de la vida familiar?</p>
          <div class="canvas-wrap">
            <canvas id="chartRealidad"></canvas>
          </div>
          <div class="chart-footer">
            <span>Fuente: Encuesta Tradwife (P21)</span>
            <span>FiveThirtyEight Style</span>
          </div>
        </div>

        <!-- Gráfico 4 -->
        <div class="chart-card">
          <h2 class="chart-headline">Consenso mayoritario sobre el poder de los algoritmos</h2>
          <p class="chart-subhead">Percepción de transformación sobre cómo la sociedad comprende el rol de la mujer.</p>
          <div class="canvas-wrap">
            <canvas id="chartImpacto"></canvas>
          </div>
          <div class="chart-footer">
            <span>Fuente: Encuesta Tradwife (P25)</span>
            <span>FiveThirtyEight Style</span>
          </div>
        </div>
      </div>
    </section>

    <!-- SECCIÓN 2: DATOS MACROECONÓMICOS -->
    <section id="tab-macro" class="tab-content hidden">
      <div class="stat-row">
        <div class="stat-box highlight">
          <div class="stat-label">Informalidad Urbana (18-65)</div>
          <div class="stat-number">36.8%</div>
          <div class="stat-sub">Población activa ocupada sin aportes previsionales ni cobertura.</div>
        </div>
        <div class="stat-box">
          <div class="stat-label">Desocupación Jefas Mujeres</div>
          <div class="stat-number">9.4%</div>
          <div class="stat-sub">En comparación al 6.2% registrado en jefes varones de hogar.</div>
        </div>
        <div class="stat-box">
          <div class="stat-label">Brecha de Desempleo</div>
          <div class="stat-number">+51.6%</div>
          <div class="stat-sub">Sobre-representación femenina en las tasas de desocupación urbana.</div>
        </div>
        <div class="stat-box">
          <div class="stat-label">Jefatura Femenina</div>
          <div class="stat-number">41.5%</div>
          <div class="stat-sub">Hogares sostenidos exclusivamente por una jefa de hogar.</div>
        </div>
      </div>

      <div class="grid-charts">
        <div class="chart-card">
          <h2 class="chart-headline">Más de un tercio del mercado laboral carece de derechos</h2>
          <p class="chart-subhead">Evolución semestral de la tasa de informalidad laboral en población de 18 a 65 años (%).</p>
          <div class="canvas-wrap">
            <canvas id="chartInformal"></canvas>
          </div>
          <div class="chart-footer">
            <span>Fuente: Series EPH / Estadísticas de hogares urbanos</span>
            <span>FiveThirtyEight Style</span>
          </div>
        </div>

        <div class="chart-card">
          <h2 class="chart-headline">Las jefas de hogar soportan una penalización constante</h2>
          <p class="chart-subhead">Tasa de desocupación según sexo del jefe de hogar por período (%).</p>
          <div class="canvas-wrap">
            <canvas id="chartDesocup"></canvas>
          </div>
          <div class="chart-footer">
            <span>Fuente: Indicadores de mercado de trabajo urbano</span>
            <span>FiveThirtyEight Style</span>
          </div>
        </div>
      </div>
    </section>

    <!-- SECCIÓN 3: TESIS CRUZADA -->
    <section id="tab-tesis" class="tab-content hidden">
      <div class="callout-538">
        <h3>La Paradoja de la Dependencia Económica</h3>
        <p>
          El discurso <em>Tradwife</em> revitalizado por plataformas de video corto promueve la figura del <strong>"varón como único proveedor financiero"</strong> a cambio de la dedicación exclusiva al cuidado familiar. No obstante, en un ecosistema donde más del 36% del trabajo es informal y 4 de cada 10 hogares urbanos son encabezados por mujeres, prescindir de ingresos propios anula la autonomía económica y expone al hogar a la pobreza crítica en caso de disolución vincular o desempleo del cónyuge.
        </p>
      </div>

      <div class="chart-card full-width">
        <h2 class="chart-headline">Retórica digital vs. Vulnerabilidad económica real</h2>
        <p class="chart-subhead">Contraste porcentual entre el ideal difundido en redes y las condiciones estructurales objetivas.</p>
        <div class="canvas-wrap" style="max-height: 380px;">
          <canvas id="chartCruce"></canvas>
        </div>
        <div class="chart-footer">
          <span>Fuente: Encuesta empírica Tradwife + Datos agregados sociolaborales</span>
          <span>FiveThirtyEight Style</span>
        </div>
      </div>
    </section>
  </div>

  <script>
    // Configuración tipográfica y visual FiveThirtyEight para Chart.js
    Chart.defaults.font.family = "'Roboto', -apple-system, sans-serif";
    Chart.defaults.font.size = 12;
    Chart.defaults.color = '#555555';
    Chart.defaults.plugins.legend.labels.boxWidth = 12;
    Chart.defaults.plugins.legend.labels.usePointStyle = true;

    // 1. Representación Tradicional
    new Chart(document.getElementById('chartPres'), {
      type: 'bar',
      data: {
        labels: ['Positiva / Idealizada', 'No segura / Ambiguo', 'Neutral', 'Negativa'],
        datasets: [{
          data: [13, 12, 8, 5],
          backgroundColor: ['#ed553b', '#b2b2b2', '#008fd5', '#1f3552'],
          barPercentage: 0.75
        }]
      },
      options: {
        indexAxis: 'y',
        responsive: true,
        maintainAspectRatio: false,
        plugins: { legend: { display: false } },
        scales: {
          x: { grid: { color: '#e5e5e5' }, ticks: { stepSize: 2 } },
          y: { grid: { display: false } }
        }
      }
    });

    // 2. Mujer Ideal
    new Chart(document.getElementById('chartIdeal'), {
      type: 'bar',
      data: {
        labels: [
          'Atractiva físicamente',
          'Independiente económica',
          'Buena esposa',
          'Cuidado del hogar',
          'Buena madre',
          'Ama de casa'
        ],
        datasets: [{
          data: [16, 6, 5, 4, 3, 3],
          backgroundColor: '#008fd5',
          barPercentage: 0.7
        }]
      },
      options: {
        indexAxis: 'y',
        responsive: true,
        maintainAspectRatio: false,
        plugins: { legend: { display: false } },
        scales: {
          x: { grid: { color: '#e5e5e5' }, ticks: { stepSize: 2 } },
          y: { grid: { display: false } }
        }
      }
    });

    // 3. Fidelidad con la Vida Real
    new Chart(document.getElementById('chartRealidad'), {
      type: 'doughnut',
      data: {
        labels: ['Mayormente no', 'Casi nunca', 'A veces', 'No'],
        datasets: [{
          data: [15, 9, 10, 4],
          backgroundColor: ['#ed553b', '#f6c85f', '#008fd5', '#1f3552'],
          borderWidth: 2,
          borderColor: '#ffffff'
        }]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: { position: 'bottom', labels: { padding: 15 } }
        },
        cutout: '62%'
      }
    });

    // 4. Impacto en Roles de Género
    new Chart(document.getElementById('chartImpacto'), {
      type: 'bar',
      data: {
        labels: ['Tal Vez', 'Sí', 'No'],
        datasets: [{
          data: [19, 17, 2],
          backgroundColor: ['#f6c85f', '#ed553b', '#b2b2b2'],
          barPercentage: 0.65
        }]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: { legend: { display: false } },
        scales: {
          x: { grid: { display: false } },
          y: { grid: { color: '#e5e5e5' }, ticks: { stepSize: 5 } }
        }
      }
    });

    // 5. Informalidad Laboral (Línea clásica 538 con marcador)
    new Chart(document.getElementById('chartInformal'), {
      type: 'line',
      data: {
        labels: ['2021-I', '2021-II', '2022-I', '2022-II', '2023-I', '2023-II', '2024-I'],
        datasets: [{
          label: 'Tasa de Informalidad Urbana (%)',
          data: [33.3, 34.2, 35.9, 36.5, 37.1, 36.8, 38.2],
          borderColor: '#ed553b',
          backgroundColor: '#ed553b',
          borderWidth: 3.5,
          pointRadius: 4,
          pointHoverRadius: 6,
          tension: 0.1
        }]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          x: { grid: { display: false } },
          y: {
            min: 25,
            max: 45,
            grid: { color: '#e5e5e5' },
            ticks: { callback: v => v + '%' }
          }
        }
      }
    });

    // 6. Desocupación Jefas vs Jefes
    new Chart(document.getElementById('chartDesocup'), {
      type: 'bar',
      data: {
        labels: ['2022-I', '2022-II', '2023-I', '2023-II', '2024-I'],
        datasets: [
          {
            label: 'Jefas Mujeres (%)',
            data: [9.1, 8.8, 9.6, 9.4, 10.2],
            backgroundColor: '#ed553b'
          },
          {
            label: 'Jefes Varones (%)',
            data: [6.1, 5.9, 6.3, 6.2, 6.7],
            backgroundColor: '#1f3552'
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: { position: 'top', align: 'end' }
        },
        scales: {
          x: { grid: { display: false } },
          y: {
            grid: { color: '#e5e5e5' },
            ticks: { callback: v => v + '%' }
          }
        }
      }
    });

    // 7. Cruce Teórico 538
    new Chart(document.getElementById('chartCruce'), {
      type: 'bar',
      data: {
        labels: [
          'Proclama "Hombre Proveedor Único" (Narrativa RRSS)',
          'Hogares Urbanos con Jefatura Femenina Exclusiva',
          'Informalidad Laboral en Población Activa (18-65)',
          'Riesgo de Indefensión Económica sin Ingreso Laboral Propio'
        ],
        datasets: [{
          data: [78.0, 41.5, 36.8, 84.2],
          backgroundColor: ['#1f3552', '#008fd5', '#f6c85f', '#ed553b'],
          barPercentage: 0.7
        }]
      },
      options: {
        indexAxis: 'y',
        responsive: true,
        maintainAspectRatio: false,
        plugins: { legend: { display: false } },
        scales: {
          x: {
            max: 100,
            grid: { color: '#e5e5e5' },
            ticks: { callback: v => v + '%' }
          },
          y: { grid: { display: false } }
        }
      }
    });

    // Navegación de pestañas
    document.querySelectorAll('.tab-item').forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.tab-item').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');

        const target = btn.getAttribute('data-target');
        document.querySelectorAll('.tab-content').forEach(s => s.classList.add('hidden'));
        document.getElementById(`tab-${target}`).classList.remove('hidden');
      });
    });
  </script>
</body>
</html>
