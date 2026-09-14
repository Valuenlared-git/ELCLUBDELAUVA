<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Climate Spiral Style: La Espiral Tradwife & Desajuste Laboral</title>
  
  <!-- CDN Chart.js & PapaParse -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/papaparse@5.4.1/papaparse.min.js"></script>
  
  <!-- Tipografía técnica y monoespaciada -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --spiral-bg: #050814;
      --spiral-card: rgba(10, 16, 33, 0.78);
      --spiral-border: rgba(56, 189, 248, 0.18);
      --spiral-border-glow: rgba(56, 189, 248, 0.4);
      --spiral-text: #f0f6fc;
      --spiral-muted: #8b9bb4;
      
      /* Escala térmica Climate Spiral */
      --heat-cold: #1e40af;
      --heat-cyan: #06b6d4;
      --heat-yellow: #facc15;
      --heat-orange: #fb923c;
      --heat-red: #f43f5e;
      --heat-hot: #ff0055;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--spiral-bg);
      background-image: 
        radial-gradient(circle at 50% 15%, rgba(6, 182, 212, 0.12) 0%, transparent 55%),
        radial-gradient(circle at 80% 85%, rgba(244, 63, 94, 0.08) 0%, transparent 50%);
      color: var(--spiral-text);
      font-family: 'Space Grotesk', -apple-system, sans-serif;
      padding: 2.25rem 1.25rem;
      min-height: 100vh;
      -webkit-font-smoothing: antialiased;
    }

    .container {
      max-width: 1240px;
      margin: 0 auto;
    }

    /* Header */
    header {
      border-bottom: 1px solid var(--spiral-border);
      padding-bottom: 1.75rem;
      margin-bottom: 2rem;
      position: relative;
    }

    .kicker-spiral {
      display: inline-flex;
      align-items: center;
      gap: 0.5rem;
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.76rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.12em;
      color: var(--heat-cyan);
      background: rgba(6, 182, 212, 0.1);
      border: 1px solid rgba(6, 182, 212, 0.3);
      padding: 0.35rem 0.85rem;
      border-radius: 9999px;
      margin-bottom: 0.9rem;
    }

    .pulse-dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: var(--heat-hot);
      box-shadow: 0 0 8px var(--heat-hot);
      animation: pulse 1.5s infinite alternate;
    }

    @keyframes pulse {
      from { transform: scale(0.9); opacity: 0.7; }
      to { transform: scale(1.3); opacity: 1; }
    }

    h1 {
      font-size: 2.4rem;
      font-weight: 700;
      line-height: 1.15;
      letter-spacing: -0.03em;
      margin-bottom: 0.65rem;
      background: linear-gradient(135deg, #ffffff 40%, #06b6d4 85%, #f43f5e 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    .lead {
      color: var(--spiral-muted);
      font-size: 1.05rem;
      line-height: 1.6;
      max-width: 980px;
    }

    /* Pestañas de control radial */
    .tabs-bar {
      display: flex;
      gap: 0.6rem;
      border-bottom: 1px solid var(--spiral-border);
      margin-bottom: 2rem;
      overflow-x: auto;
      padding-bottom: 0.25rem;
    }

    .tab-spiral {
      background: rgba(10, 16, 33, 0.5);
      border: 1px solid var(--spiral-border);
      color: var(--spiral-muted);
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.82rem;
      font-weight: 600;
      padding: 0.7rem 1.25rem;
      cursor: pointer;
      border-radius: 0.5rem 0.5rem 0 0;
      transition: all 0.2s ease;
      display: flex;
      align-items: center;
      gap: 0.5rem;
      white-space: nowrap;
    }

    .tab-spiral:hover {
      color: #fff;
      border-color: var(--spiral-border-glow);
    }

    .tab-spiral.active {
      color: #fff;
      background: rgba(6, 182, 212, 0.12);
      border-color: var(--heat-cyan);
      border-bottom: 2px solid var(--heat-cyan);
      box-shadow: 0 -3px 15px rgba(6, 182, 212, 0.15);
    }

    /* Thermal Indicator Cards */
    .thermal-kpi-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
      gap: 1.25rem;
      margin-bottom: 2.5rem;
    }

    .thermal-card {
      background: var(--spiral-card);
      border: 1px solid var(--spiral-border);
      backdrop-filter: blur(10px);
      border-radius: 0.85rem;
      padding: 1.35rem;
      position: relative;
      overflow: hidden;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
    }

    .thermal-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 3px;
      background: linear-gradient(90deg, var(--heat-cyan), var(--heat-yellow), var(--heat-red));
    }

    .card-meta {
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.72rem;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: var(--spiral-muted);
    }

    .card-val {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 2.2rem;
      font-weight: 700;
      margin: 0.35rem 0 0.2rem;
      color: #fff;
      letter-spacing: -0.02em;
    }

    .card-desc {
      font-size: 0.82rem;
      color: var(--spiral-muted);
      line-height: 1.4;
    }

    /* Grid de gráficos */
    .charts-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 1.75rem;
      margin-bottom: 2rem;
    }

    @media (max-width: 920px) {
      .charts-grid {
        grid-template-columns: 1fr;
      }
      h1 {
        font-size: 1.85rem;
      }
    }

    .spiral-chart-box {
      background: var(--spiral-card);
      border: 1px solid var(--spiral-border);
      backdrop-filter: blur(10px);
      border-radius: 0.85rem;
      padding: 1.6rem;
      display: flex;
      flex-direction: column;
      position: relative;
      box-shadow: 0 4px 24px rgba(0, 0, 0, 0.35);
    }

    .spiral-chart-box.full {
      grid-column: 1 / -1;
    }

    .chart-title {
      font-size: 1.15rem;
      font-weight: 700;
      color: #fff;
      margin-bottom: 0.25rem;
    }

    .chart-sub {
      font-size: 0.83rem;
      color: var(--spiral-muted);
      margin-bottom: 1.25rem;
      line-height: 1.4;
    }

    .canvas-wrap {
      position: relative;
      flex-grow: 1;
      min-height: 310px;
      max-height: 360px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    /* Radial Canvas Wrapper */
    #spiralCanvasWrap {
      position: relative;
      width: 100%;
      height: 380px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    #climateSpiralCanvas {
      max-width: 100%;
      max-height: 100%;
    }

    .hidden {
      display: none !important;
    }

    /* Footer Legend */
    .spiral-legend {
      display: flex;
      align-items: center;
      gap: 1rem;
      margin-top: 1rem;
      padding-top: 0.85rem;
      border-top: 1px solid rgba(255, 255, 255, 0.08);
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.72rem;
      color: var(--spiral-muted);
      justify-content: space-between;
      flex-wrap: wrap;
    }

    .gradient-bar {
      width: 140px;
      height: 6px;
      border-radius: 3px;
      background: linear-gradient(90deg, #1e40af, #06b6d4, #facc15, #fb923c, #f43f5e);
      display: inline-block;
    }
  </style>
</head>
<body>

  <div class="container">
    <header>
      <div class="kicker-spiral">
        <span class="pulse-dot"></span>
        Visualización Radial // Trayectoria Térmica 2021-2026
      </div>
      <h1>La Espiral del Modelo Tradwife vs. El Mercado Laboral</h1>
      <p class="lead">
        Inspirado en los gráficos Climate Spiral: examinamos cómo la intensificación de las narrativas digitales sobre roles tradicionales se acelera concéntricamente frente al calentamiento estructural del desempleo femenino y la informalidad urbana.
      </p>
    </header>

    <!-- Navegación de Pestañas -->
    <div class="tabs-bar">
      <button class="tab-spiral active" data-target="tradwife">
        <span>🌀</span> Espiral de Percepción (Encuesta)
      </button>
      <button class="tab-spiral" data-target="macro">
        <span>🌡️</span> Espiral Laboral Urbana (18-65 años)
      </button>
      <button class="tab-spiral" data-target="tesis">
        <span>⚡</span> Tesis Crítica: La Trampa Económica
      </button>
    </div>

    <!-- SECCIÓN 1: TRADWIFE RADIAL -->
    <section id="tab-tradwife" class="tab-view">
      <div class="thermal-kpi-grid">
        <div class="thermal-card">
          <div class="card-meta">Muestra Procesada</div>
          <div class="card-val" id="kpi-total">38</div>
          <div class="card-desc">Respuestas de usuarios analizadas</div>
        </div>
        <div class="thermal-card">
          <div class="card-meta">Anomalía de Ficción</div>
          <div class="card-val" style="color: var(--heat-yellow);">73.7%</div>
          <div class="card-desc">Sostienen que las redes distorsionan la vida familiar</div>
        </div>
        <div class="thermal-card">
          <div class="card-meta">Índice de Aceleración</div>
          <div class="card-val" style="color: var(--heat-red);">94.7%</div>
          <div class="card-desc">Afirman que el algoritmo modifica roles sociales</div>
        </div>
        <div class="thermal-card">
          <div class="card-meta">Frecuencia / Vector Central</div>
          <div class="card-val" style="color: var(--heat-cyan);">Instagram</div>
          <div class="card-desc">Eje de mayor recirculación y alcance</div>
        </div>
      </div>

      <div class="charts-grid">
        <!-- Gráfico Radial 1 -->
        <div class="spiral-chart-box">
          <h2 class="chart-title">1. Proyección Polar: Representación en Redes</h2>
          <p class="chart-sub">Distribución polar de la percepción estética (P20: positiva vs. neutra vs. crítica)</p>
          <div class="canvas-wrap">
            <canvas id="chartPolarPres"></canvas>
          </div>
          <div class="spiral-legend">
            <span>Escala concéntrica</span>
            <span><span class="gradient-bar"></span> Centro a Periferia</span>
          </div>
        </div>

        <!-- Gráfico Radial 2 -->
        <div class="spiral-chart-box">
          <h2 class="chart-title">2. Radar: Arquetipos de la "Mujer Ideal"</h2>
          <p class="chart-sub">Frecuencia radial de atributos construidos por el algoritmo digital (P22)</p>
          <div class="canvas-wrap">
            <canvas id="chartRadarIdeal"></canvas>
          </div>
          <div class="spiral-legend">
            <span>Atributos proyectados</span>
            <span style="color: var(--heat-cyan);">Vectores multidimensionales</span>
          </div>
        </div>

        <!-- Gráfico Radial 3 -->
        <div class="spiral-chart-box">
          <h2 class="chart-title">3. Brecha de Autenticidad Familiar</h2>
          <p class="chart-sub">¿Refleja el feed la vida real cotidiana? (P21)</p>
          <div class="canvas-wrap">
            <canvas id="chartDoughnutReal"></canvas>
          </div>
          <div class="spiral-legend">
            <span>Dispersión concéntrica</span>
            <span style="color: var(--heat-orange);">Ruptura Algorítmica</span>
          </div>
        </div>

        <!-- Gráfico Radial 4 -->
        <div class="spiral-chart-box">
          <h2 class="chart-title">4. Impacto en los Roles de Género</h2>
          <p class="chart-sub">Efecto percibido sobre la reconfiguración del rol de la mujer (P25)</p>
          <div class="canvas-wrap">
            <canvas id="chartBarImpact"></canvas>
          </div>
          <div class="spiral-legend">
            <span>Resonancia social</span>
            <span style="color: var(--heat-red);">Intensidad Crítica</span>
          </div>
        </div>
      </div>
    </section>

    <!-- SECCIÓN 2: ESPIRAL CLIMÁTICA LABORAL -->
    <section id="tab-macro" class="tab-view hidden">
      <div class="thermal-kpi-grid">
        <div class="thermal-card">
          <div class="card-meta">Tasa Informalidad (18-65)</div>
          <div class="card-val" style="color: var(--heat-red);">36.8%</div>
          <div class="card-desc">Trabajadoras y trabajadores urbanos sin derechos previsionales</div>
        </div>
        <div class="thermal-card">
          <div class="card-meta">Desocupación Jefas Mujeres</div>
          <div class="card-val" style="color: var(--heat-orange);">9.4%</div>
          <div class="card-desc">Frente al 6.2% registrado en jefes varones</div>
        </div>
        <div class="thermal-card">
          <div class="card-meta">Brecha de Desempleo</div>
          <div class="card-val" style="color: var(--heat-yellow);">+51.6%</div>
          <div class="card-desc">Mayor sobrecarga de vulnerabilidad en jefaturas femeninas</div>
        </div>
        <div class="thermal-card">
          <div class="card-meta">Hogares Monomarentales</div>
          <div class="card-val" style="color: var(--heat-cyan);">41.5%</div>
          <div class="card-desc">Jefatura exclusiva de mujeres en aglomerados urbanos</div>
        </div>
      </div>

      <div class="spiral-chart-box full">
        <h2 class="chart-title">Espiral Climática de la Informalidad Laboral (2021 – 2024)</h2>
        <p class="chart-sub">
          Visualización estilo Climate Spiral: el incremento semestral de la informalidad urbana se desplaza hacia anillos exteriores de mayor riesgo térmico socioeconómico.
        </p>
        <div id="spiralCanvasWrap">
          <canvas id="climateSpiralCanvas" width="500" height="380"></canvas>
        </div>
        <div class="spiral-legend">
          <span>Eje concéntrico: Nivel de Informalidad (%)</span>
          <span><span class="gradient-bar"></span> 33% (Frío) a 39% (Alerta Roja)</span>
        </div>
      </div>

      <div class="charts-grid" style="margin-top: 1.75rem;">
        <div class="spiral-chart-box">
          <h2 class="chart-title">Desocupación: Jefas de Hogar vs. Jefes Varones</h2>
          <p class="chart-sub">Evolución semestral en hogares urbanos</p>
          <div class="canvas-wrap">
            <canvas id="chartDesocupMacro"></canvas>
          </div>
        </div>
        <div class="spiral-chart-box">
          <h2 class="chart-title">La Brecha de Precarización</h2>
          <p class="chart-sub">Distancia porcentual sostenida en hogares monoparentales</p>
          <div class="canvas-wrap">
            <canvas id="chartRadarMacro"></canvas>
          </div>
        </div>
      </div>
    </section>

    <!-- SECCIÓN 3: TESIS CRUZADA -->
    <section id="tab-tesis" class="tab-view hidden">
      <div class="spiral-chart-box full" style="border-left: 4px solid var(--heat-red);">
        <h2 class="chart-title" style="color: var(--heat-orange);">El Desfase Térmico: Ficción Algorítmica vs. Seguridad Económica</h2>
        <p class="chart-sub" style="font-size: 0.95rem; color: #cbd5e1; margin-bottom: 0;">
          El mandato Tradwife postula el retiro de la mujer del empleo remunerado bajo la premisa del <strong>"varón como único proveedor económico"</strong>. En los hechos, la espiral de informalidad (+36%) y la elevada proporción de hogares liderados por mujeres (41.5%) demuestran que la dependencia económica absoluta no garantiza estabilidad familiar, sino un riesgo extremo de caída bajo la línea de pobreza ante el desempleo conyugal o la separación.
        </p>
      </div>

      <div class="spiral-chart-box full" style="margin-top: 1.5rem;">
        <h2 class="chart-title">Contraste Térmico de Variables</h2>
        <p class="chart-sub">Proclama en redes vs. realidad económica objetiva</p>
        <div class="canvas-wrap" style="max-height: 380px;">
          <canvas id="chartCruceSpiral"></canvas>
        </div>
      </div>
    </section>
  </div>

  <script>
    // Configuración global estética Climate Spiral
    Chart.defaults.color = '#8b9bb4';
    Chart.defaults.borderColor = 'rgba(56, 189, 248, 0.15)';
    Chart.defaults.font.family = "'Space Grotesk', sans-serif";

    // 1. Gráfico Polar (P20: Representación Tradicional)
    new Chart(document.getElementById('chartPolarPres'), {
      type: 'polarArea',
      data: {
        labels: ['Positiva / Idealizada', 'No segura / Ambiguo', 'Neutral', 'Negativa'],
        datasets: [{
          data: [13, 12, 8, 5],
          backgroundColor: [
            'rgba(244, 63, 94, 0.75)',   // Rojo cálido
            'rgba(250, 204, 21, 0.7)',   // Amarillo
            'rgba(6, 182, 212, 0.65)',   // Cian
            'rgba(30, 64, 175, 0.6)'     // Azul frío
          ],
          borderColor: '#050814',
          borderWidth: 2
        }]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: { position: 'bottom', labels: { boxWidth: 12, padding: 12 } }
        },
        scales: {
          r: {
            grid: { color: 'rgba(56, 189, 248, 0.15)' },
            angleLines: { color: 'rgba(56, 189, 248, 0.15)' },
            ticks: { backdropColor: 'transparent', color: '#8b9bb4' }
          }
        }
      }
    });

    // 2. Gráfico Radar (P22: Arquetipos de la Mujer Ideal)
    new Chart(document.getElementById('chartRadarIdeal'), {
      type: 'radar',
      data: {
        labels: ['Belleza física', 'Independiente', 'Buena esposa', 'Cuidado hogar', 'Buena madre', 'Ama de casa'],
        datasets: [{
          label: 'Frecuencia de mención',
          data: [16, 6, 5, 4, 3, 3],
          backgroundColor: 'rgba(6, 182, 212, 0.25)',
          borderColor: '#06b6d4',
          pointBackgroundColor: '#facc15',
          pointBorderColor: '#ffffff',
          pointHoverRadius: 6,
          borderWidth: 2.5
        }]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: { legend: { display: false } },
        scales: {
          r: {
            grid: { color: 'rgba(56, 189, 248, 0.15)' },
            angleLines: { color: 'rgba(56, 189, 248, 0.15)' },
            ticks: { backdropColor: 'transparent', color: '#8b9bb4', stepSize: 4 }
          }
        }
      }
    });

    // 3. Gráfico Anular Concéntrico (P21: Fidelidad Real)
    new Chart(document.getElementById('chartDoughnutReal'), {
      type: 'doughnut',
      data: {
        labels: ['Mayormente no', 'Casi nunca', 'A veces', 'No'],
        datasets: [{
          data: [15, 9, 10, 4],
          backgroundColor: [
            '#f43f5e',
            '#fb923c',
            '#06b6d4',
            '#1e40af'
          ],
          borderColor: '#050814',
          borderWidth: 3
        }]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        cutout: '68%',
        plugins: {
          legend: { position: 'bottom', labels: { boxWidth: 12, padding: 12 } }
        }
      }
    });

    // 4. Gráfico de Barras con Gradiente Térmico (P25: Roles de Género)
    new Chart(document.getElementById('chartBarImpact'), {
      type: 'bar',
      data: {
        labels: ['Tal Vez', 'Sí', 'No'],
        datasets: [{
          data: [19, 17, 2],
          backgroundColor: ['#facc15', '#f43f5e', '#1e40af'],
          borderRadius: 6
        }]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: { legend: { display: false } },
        scales: {
          x: { grid: { display: false } },
          y: { grid: { color: 'rgba(56, 189, 248, 0.12)' }, ticks: { stepSize: 5 } }
        }
      }
    });

    // 5. RENDER MANUAL DE LA CLIMATE SPIRAL EN CANVAS HTML5
    function drawClimateSpiral() {
      const canvas = document.getElementById('climateSpiralCanvas');
      if (!canvas) return;
      const ctx = canvas.getContext('2d');
      const width = canvas.width;
      const height = canvas.height;
      const centerX = width / 2;
      const centerY = height / 2;

      ctx.clearRect(0, 0, width, height);

      // Datos de la serie semestral de informalidad urbana
      const dataPoints = [
        { label: '2021-I', val: 33.3 },
        { label: '2021-II', val: 34.2 },
        { label: '2022-I', val: 35.9 },
        { label: '2022-II', val: 36.5 },
        { label: '2023-I', val: 37.1 },
        { label: '2023-II', val: 36.8 },
        { label: '2024-I', val: 38.2 }
      ];

      // Anillos concéntricos de referencia (30%, 35%, 40%)
      const rings = [
        { val: '32%', r: 50 },
        { val: '35%', r: 90 },
        { val: '38%', r: 130 },
        { val: '40%', r: 160 }
      ];

      ctx.lineWidth = 1;
      ctx.strokeStyle = 'rgba(56, 189, 248, 0.16)';
      ctx.fillStyle = '#8b9bb4';
      ctx.font = '10px JetBrains Mono';

      rings.forEach(ring => {
        ctx.beginPath();
        ctx.arc(centerX, centerY, ring.r, 0, Math.PI * 2);
        ctx.stroke();
        ctx.fillText(ring.val, centerX + 5, centerY - ring.r + 12);
      });

      // Ejes radiales (12 semestres/meses virtuales)
      for (let i = 0; i < 8; i++) {
        const angle = (i / 8) * Math.PI * 2;
        ctx.beginPath();
        ctx.moveTo(centerX, centerY);
        ctx.lineTo(centerX + Math.cos(angle) * 165, centerY + Math.sin(angle) * 165);
        ctx.strokeStyle = 'rgba(255, 255, 255, 0.05)';
        ctx.stroke();
      }

      // Dibujamos la espiral continua calculada
      ctx.beginPath();
      let coords = [];

      dataPoints.forEach((dp, i) => {
        const angle = (i / 7) * Math.PI * 2 - Math.PI / 2;
        // Mapeo del radio entre 50 y 160 según el porcentaje
        const radius = 40 + ((dp.val - 32) / (39 - 32)) * 115;
        const x = centerX + Math.cos(angle) * radius;
        const y = centerY + Math.sin(angle) * radius;
        coords.push({ x, y, dp, angle });
      });

      // Gradiente a lo largo del trazo
      const gradient = ctx.createLinearGradient(centerX - 100, centerY - 100, centerX + 150, centerY + 150);
      gradient.addColorStop(0, '#1e40af'); // Azul frío inicio
      gradient.addColorStop(0.3, '#06b6d4'); // Cian
      gradient.addColorStop(0.65, '#facc15'); // Amarillo
      gradient.addColorStop(1, '#f43f5e'); // Rojo térmico final

      ctx.strokeStyle = gradient;
      ctx.lineWidth = 4;
      ctx.shadowColor = '#f43f5e';
      ctx.shadowBlur = 10;

      coords.forEach((pt, idx) => {
        if (idx === 0) ctx.moveTo(pt.x, pt.y);
        else ctx.lineTo(pt.x, pt.y);
      });
      ctx.stroke();
      ctx.shadowBlur = 0;

      // Puntos y etiquetas de semestres
      coords.forEach(pt => {
        ctx.beginPath();
        ctx.arc(pt.x, pt.y, 5, 0, Math.PI * 2);
        ctx.fillStyle = '#ffffff';
        ctx.fill();
        ctx.strokeStyle = '#f43f5e';
        ctx.lineWidth = 2;
        ctx.stroke();

        ctx.fillStyle = '#f0f6fc';
        ctx.font = '10px JetBrains Mono';
        const offsetX = Math.cos(pt.angle) * 15;
        const offsetY = Math.sin(pt.angle) * 15;
        ctx.fillText(`${pt.dp.label} (${pt.dp.val}%)`, pt.x + offsetX - 15, pt.y + offsetY);
      });
    }

    // 6. Desocupación Comparativa (Macro)
    new Chart(document.getElementById('chartDesocupMacro'), {
      type: 'bar',
      data: {
        labels: ['2022-I', '2022-II', '2023-I', '2023-II', '2024-I'],
        datasets: [
          {
            label: 'Jefas Mujeres (%)',
            data: [9.1, 8.8, 9.6, 9.4, 10.2],
            backgroundColor: '#fb923c',
            borderRadius: 5
          },
          {
            label: 'Jefes Varones (%)',
            data: [6.1, 5.9, 6.3, 6.2, 6.7],
            backgroundColor: '#06b6d4',
            borderRadius: 5
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          x: { grid: { display: false } },
          y: { grid: { color: 'rgba(56, 189, 248, 0.12)' }, ticks: { callback: v => v + '%' } }
        }
      }
    });

    // 7. Radar Macro
    new Chart(document.getElementById('chartRadarMacro'), {
      type: 'radar',
      data: {
        labels: ['2022-I', '2022-II', '2023-I', '2023-II', '2024-I'],
        datasets: [
          {
            label: 'Brecha de Género (%)',
            data: [49.2, 49.1, 52.4, 51.6, 52.2],
            borderColor: '#f43f5e',
            backgroundColor: 'rgba(244, 63, 94, 0.25)',
            borderWidth: 2
          }
        ]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          r: {
            grid: { color: 'rgba(56, 189, 248, 0.15)' },
            ticks: { backdropColor: 'transparent', color: '#8b9bb4' }
          }
        }
      }
    });

    // 8. Tesis Cruzada (Barras Térmicas Horizontales)
    new Chart(document.getElementById('chartCruceSpiral'), {
      type: 'bar',
      data: {
        labels: [
          'Proclama "Hombre Proveedor Único" (RRSS Tradwife)',
          'Hogares Urbanos con Jefatura Femenina Exclusiva',
          'Informalidad Laboral Urbana (Población 18-65)',
          'Riesgo de Indefensión Económica sin Ingresos Propios'
        ],
        datasets: [{
          data: [78.0, 41.5, 36.8, 84.2],
          backgroundColor: ['#06b6d4', '#facc15', '#fb923c', '#f43f5e'],
          borderRadius: 6
        }]
      },
      options: {
        indexAxis: 'y',
        responsive: true,
        maintainAspectRatio: false,
        plugins: { legend: { display: false } },
        scales: {
          x: { max: 100, grid: { color: 'rgba(56, 189, 248, 0.12)' }, ticks: { callback: v => v + '%' } },
          y: { grid: { display: false } }
        }
      }
    });

    // Navegación de Pestañas
    document.querySelectorAll('.tab-spiral').forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.tab-spiral').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');

        const target = btn.getAttribute('data-target');
        document.querySelectorAll('.tab-view').forEach(s => s.classList.add('hidden'));
        document.getElementById(`tab-${target}`).classList.remove('hidden');

        if (target === 'macro') {
          setTimeout(drawClimateSpiral, 50);
        }
      });
    });

    window.addEventListener('DOMContentLoaded', () => {
      drawClimateSpiral();
    });
  </script>
</body>
</html>
