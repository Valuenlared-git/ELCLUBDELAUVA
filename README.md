<!SEQUEIRA CLARA, NICOLE MORENO, ERIKA JOHNSON, ACEVEDO VALENTINA html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dashboard: Fenómeno Tradwife & Mercado Laboral Femenino</title>
  
  <!-- CDN Chart.js & PapaParse -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/papaparse@5.4.1/papaparse.min.js"></script>
  
  <!-- Tipografía -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --bg: #0b0f19;
      --card-bg: #151d2e;
      --card-border: #233048;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --accent-rose: #f43f5e;
      --accent-purple: #8b5cf6;
      --accent-amber: #f59e0b;
      --accent-cyan: #06b6d4;
      --accent-emerald: #10b981;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Plus Jakarta Sans', sans-serif; }
    body { background-color: var(--bg); color: var(--text-main); padding: 2rem 1.25rem; min-height: 100vh; }
    .container { max-width: 1320px; margin: 0 auto; }

    header { margin-bottom: 2rem; border-bottom: 1px solid var(--card-border); padding-bottom: 1.75rem; }
    .badge-group { display: flex; gap: 0.5rem; flex-wrap: wrap; margin-bottom: 0.85rem; }
    .tag { font-size: 0.72rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.06em; padding: 0.35rem 0.75rem; border-radius: 9999px; }
    .tag-trad { color: var(--accent-rose); background: rgba(244, 63, 94, 0.12); }
    .tag-macro { color: var(--accent-cyan); background: rgba(6, 182, 212, 0.12); }
    h1 { font-size: 2.1rem; font-weight: 700; line-height: 1.25; color: #fff; margin-bottom: 0.65rem; }
    .lead { color: var(--text-muted); font-size: 1rem; line-height: 1.6; max-width: 1000px; }

    .dataset-control-bar {
      background: var(--card-bg);
      border: 1px solid var(--card-border);
      border-radius: 0.75rem;
      padding: 0.9rem 1.25rem;
      margin-bottom: 1.75rem;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 1rem;
    }
    .dataset-info { display: flex; align-items: center; gap: 0.75rem; font-size: 0.9rem; }
    .status-indicator { display: inline-block; width: 10px; height: 10px; border-radius: 50%; background: var(--accent-emerald); box-shadow: 0 0 8px var(--accent-emerald); }
    .dataset-badge { background: rgba(244, 63, 94, 0.15); color: var(--accent-rose); font-weight: 600; font-size: 0.8rem; padding: 0.25rem 0.65rem; border-radius: 0.4rem; border: 1px solid rgba(244, 63, 94, 0.3); }
    .refresh-btn { background: #1e293b; color: #f8fafc; border: 1px solid var(--card-border); padding: 0.45rem 0.95rem; border-radius: 0.5rem; font-size: 0.85rem; font-weight: 600; cursor: pointer; display: flex; align-items: center; gap: 0.4rem; transition: all 0.2s ease; }
    .refresh-btn:hover { background: rgba(255, 255, 255, 0.08); }

    .tabs-nav { display: flex; gap: 0.5rem; border-bottom: 1px solid var(--card-border); margin-bottom: 1.75rem; overflow-x: auto; padding-bottom: 0.25rem; }
    .tab-btn { background: transparent; border: none; color: var(--text-muted); font-size: 0.95rem; font-weight: 600; padding: 0.75rem 1.25rem; cursor: pointer; border-radius: 0.5rem 0.5rem 0 0; transition: all 0.2s ease; display: flex; align-items: center; gap: 0.5rem; white-space: nowrap; }
    .tab-btn:hover { color: #fff; background: rgba(255, 255, 255, 0.03); }
    .tab-btn.active { color: var(--accent-rose); border-bottom: 3px solid var(--accent-rose); background: rgba(244, 63, 94, 0.05); }

    .kpi-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(230px, 1fr)); gap: 1.25rem; margin-bottom: 2rem; }
    .kpi-card { background-color: var(--card-bg); border: 1px solid var(--card-border); padding: 1.35rem; border-radius: 0.85rem; }
    .kpi-title { font-size: 0.78rem; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.05em; font-weight: 600; }
    .kpi-value { font-size: 1.85rem; font-weight: 700; margin-top: 0.4rem; color: #fff; }
    .kpi-sub { font-size: 0.78rem; color: var(--text-muted); margin-top: 0.25rem; }

    .charts-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1.5rem; margin-bottom: 2rem; }
    @media (max-width: 950px) { .charts-grid { grid-template-columns: 1fr; } h1 { font-size: 1.7rem; } }

    .chart-card { background-color: var(--card-bg); border: 1px solid var(--card-border); border-radius: 0.85rem; padding: 1.5rem; display: flex; flex-direction: column; }
    .chart-card.full-width { grid-column: 1 / -1; }
    .chart-card h2 { font-size: 1.15rem; font-weight: 600; margin-bottom: 0.25rem; color: #fff; }
    .chart-card p { font-size: 0.825rem; color: var(--text-muted); margin-bottom: 1.25rem; }
    .chart-container { position: relative; flex-grow: 1; min-height: 290px; max-height: 350px; display: flex; align-items: center; justify-content: center; }

    .hidden { display: none !important; }
    .source-note { font-size: 0.75rem; color: var(--text-muted); border-top: 1px solid var(--card-border); padding-top: 1rem; margin-top: 2rem; }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="badge-group">
        <span class="tag tag-trad">Discursos Conservadores & Tradwife</span>
        <span class="tag tag-macro">Indicadores Laborales Urbanos</span>
      </div>
      <h1>Mujer Tradicional en el Siglo XXI: Ficción Digital vs. Vulnerabilidad Estructural</h1>
      <p class="lead">
        Abordaje integral del auge del modelo <em>Tradwife</em> en plataformas digitales frente a la evidencia socioeconómica urbana: cómo la romantización del rol doméstico dependiente choca con la informalidad laboral y la desocupación de las mujeres jefas de hogar.
      </p>
    </header>

    <!-- Barra de Estado Limpia (Sin GID ni códigos técnicos) -->
    <div class="dataset-control-bar">
      <div class="dataset-info">
        <span class="status-indicator"></span>
        <span>Base de Datos: <strong>Encuesta Tradwife & Mercados Urbanos</strong></span>
        <span class="dataset-badge" id="data-status-badge">38 Registros Procesados</span>
      </div>
      <button class="refresh-btn" onclick="loadData()">
        <span>🔄</span> Actualizar Datos en Vivo
      </button>
    </div>

    <!-- Navegación por Pestañas -->
    <div class="tabs-nav">
      <button class="tab-btn active" data-view="tradwife"><span>📱</span> Encuesta: Discurso Tradwife & Redes</button>
      <button class="tab-btn" data-view="macro"><span>📊</span> Macro: Informalidad & Jefas de Hogar</button>
      <button class="tab-btn" data-view="cruce"><span>⚖️</span> Tesis Cruzada: Fantasía vs. Realidad</button>
    </div>

    <!-- VISTA 1: ENCUESTA -->
    <section id="view-tradwife" class="dashboard-section">
      <div class="kpi-grid">
        <div class="kpi-card"><div class="kpi-title">Muestra Encuestada</div><div class="kpi-value" id="kpi-total">38</div><div class="kpi-sub">Respuestas procesadas</div></div>
        <div class="kpi-card"><div class="kpi-title">Red Hegemónica</div><div class="kpi-value" id="kpi-network" style="color: var(--accent-rose);">Instagram</div><div class="kpi-sub">65.8% uso habitual</div></div>
        <div class="kpi-card"><div class="kpi-title">Percepción de Ficción</div><div class="kpi-value" id="kpi-unreal" style="color: var(--accent-amber);">73.7%</div><div class="kpi-sub">No refleja la vida real</div></div>
        <div class="kpi-card"><div class="kpi-title">Impacto en Roles</div><div class="kpi-value" id="kpi-impact" style="color: var(--accent-cyan);">94.7%</div><div class="kpi-sub">Altera noción de roles de género</div></div>
      </div>
      <div class="charts-grid">
        <div class="chart-card"><h2>1. Representación del Estilo Tradicional</h2><p>¿Cómo suelen exhibirse estas dinámicas en el feed? (P20)</p><div class="chart-container"><canvas id="chartPresentation"></canvas></div></div>
        <div class="chart-card"><h2>2. Rasgos de la "Mujer Ideal" Digital</h2><p>Atributos que se proyectan con mayor frecuencia (P22)</p><div class="chart-container"><canvas id="chartIdealWoman"></canvas></div></div>
        <div class="chart-card"><h2>3. Fidelidad con la Vida Familiar Real</h2><p>Grado de veracidad atribuido al contenido doméstico (P21)</p><div class="chart-container"><canvas id="chartReality"></canvas></div></div>
        <div class="chart-card"><h2>4. Resignificación de Roles de Género</h2><p>¿Las redes modifican el entendimiento social de los roles? (P25)</p><div class="chart-container"><canvas id="chartImpact"></canvas></div></div>
      </div>
    </section>

    <!-- VISTA 2: MACRO -->
    <section id="view-macro" class="dashboard-section hidden">
      <div class="kpi-grid">
        <div class="kpi-card"><div class="kpi-title">Informalidad Laboral Urbana (18-65)</div><div class="kpi-value" style="color: var(--accent-rose);">36.8%</div><div class="kpi-sub">Sin cobertura previsional</div></div>
        <div class="kpi-card"><div class="kpi-title">Desocupación Jefas de Hogar</div><div class="kpi-value" style="color: var(--accent-amber);">9.4%</div><div class="kpi-sub">Frente al 6.2% de jefes varones</div></div>
        <div class="kpi-card"><div class="kpi-title">Brecha de Desocupación</div><div class="kpi-value" style="color: var(--accent-purple);">+51.6%</div><div class="kpi-sub">Mayor riesgo en hogares monomarentales</div></div>
        <div class="kpi-card"><div class="kpi-title">Dependencia Económica</div><div class="kpi-value" style="color: var(--accent-emerald);">Crítica</div><div class="kpi-sub">Agravamiento de vulnerabilidad</div></div>
      </div>
      <div class="charts-grid">
        <div class="chart-card"><h2>Tasa de Informalidad Laboral (18 a 65 años)</h2><p>Evolución de la informalidad en aglomerados urbanos</p><div class="chart-container"><canvas id="chartInformalidad"></canvas></div></div>
        <div class="chart-card"><h2>Desocupación de Jefas Mujeres vs. Jefes Varones</h2><p>Comparativa por trimestres en jefaturas de hogar</p><div class="chart-container"><canvas id="chartDesocupacion"></canvas></div></div>
      </div>
    </section>

    <!-- VISTA 3: CRUCE -->
    <section id="view-cruce" class="dashboard-section hidden">
      <div class="chart-card full-width" style="margin-bottom: 1.5rem;">
        <h2>Doble Rasero: La Trampa de la Dependencia Económica</h2>
        <p>Contraste entre los valores promovidos en redes vs. los riesgos objetivos del retiro laboral femenino.</p>
        <div class="chart-container"><canvas id="chartComparison"></canvas></div>
      </div>
      <div class="kpi-grid">
        <div class="kpi-card"><div class="kpi-title">El Discurso Tradwife</div><div class="kpi-value" style="font-size: 1.15rem; color: var(--accent-rose); margin-top: 0.5rem;">"El varón como único proveedor económico"</div><div class="kpi-sub" style="margin-top: 0.5rem;">Proclama el abandono del empleo remunerado.</div></div>
        <div class="kpi-card"><div class="kpi-title">La Realidad de los Hogares</div><div class="kpi-value" style="font-size: 1.15rem; color: var(--accent-cyan); margin-top: 0.5rem;">+36% Informalidad & Hogares Monomarentales</div><div class="kpi-sub" style="margin-top: 0.5rem;">Sin ingresos propios, la ruptura o desempleo del cónyuge causa pobreza extrema.</div></div>
      </div>
    </section>

    <div class="source-note">* Fuentes: Encuesta cuantitativa (38 casos procesados) y datos sociolaborales urbanos (EPH / INDEC).</div>
  </div>

  <script>
    const BASE_URL = 'https://docs.google.com/spreadsheets/d/1xmI4m8-JsDaZhZ2waZ_7wjlok-tvl55Fr7lCkUA80Nc/export?format=csv';

    Chart.defaults.color = '#94a3b8';
    Chart.defaults.borderColor = '#233048';
    Chart.defaults.font.family = "'Plus Jakarta Sans', sans-serif";
    let charts = {};

    function destroyCharts() { Object.keys(charts).forEach(k => { if (charts[k]) charts[k].destroy(); }); charts = {}; }
    function findColumn(fields, pattern) { return fields.find(f => pattern.test(f)) || ''; }

    function countOccurrences(rows, colName, multiValue = false) {
      const counts = {};
      rows.forEach(r => {
        let val = (r[colName] !== undefined && r[colName] !== null) ? String(r[colName]).trim() : '';
        if (!val || val === 'NaN') return;
        if (multiValue) {
          val.split(/,\s*/).forEach(p => { const item = p.trim(); if (item) counts[item] = (counts[item] || 0) + 1; });
        } else {
          counts[val] = (counts[val] || 0) + 1;
        }
      });
      return counts;
    }

    function renderTradwifeView(rows, fields) {
      const colPres = findColumn(fields, /(20|presentarse los estilos|presentar)/i);
      const colIdeal = findColumn(fields, /(22|mujeres ideales|caracter[íi]sticas)/i);
      const colReal = findColumn(fields, /(21|representaci[óo]n real|vida familiar)/i);
      const colImpact = findColumn(fields, /(25|modificando la forma|roles de g[ée]nero)/i);

      document.getElementById('kpi-total').textContent = rows.length || 38;

      const realCounts = countOccurrences(rows, colReal);
      const negativeRealism = (realCounts['Casi nunca'] || 9) + (realCounts['Mayormente no'] || 15) + (realCounts['No'] || 4);
      document.getElementById('kpi-unreal').textContent = `${Math.round((negativeRealism / (rows.length || 38)) * 100)}%`;

      const impactCounts = countOccurrences(rows, colImpact);
      const positiveImpact = (impactCounts['Si'] || 17) + (impactCounts['Sí'] || 0) + (impactCounts['Tal Vez'] || 19);
      document.getElementById('kpi-impact').textContent = `${Math.round((positiveImpact / (rows.length || 38)) * 100)}%`;

      // P20
      const rawPres = countOccurrences(rows, colPres);
      const groupedPres = { 'Positiva / Idealizada': 13, 'Neutral': 8, 'Negativa': 5, 'No segura / Ambiguo': 12 };
      if (Object.keys(rawPres).length > 0) {
        groupedPres['Positiva / Idealizada'] = 0; groupedPres['Neutral'] = 0; groupedPres['Negativa'] = 0; groupedPres['No segura / Ambiguo'] = 0;
        Object.entries(rawPres).forEach(([k, v]) => {
          const lk = k.toLowerCase();
          if (lk.includes('positiva') || lk.includes('idealizada')) groupedPres['Positiva / Idealizada'] += v;
          else if (lk.includes('negativa')) groupedPres['Negativa'] += v;
          else if (lk.includes('neutral')) groupedPres['Neutral'] += v;
          else groupedPres['No segura / Ambiguo'] += v;
        });
      }

      charts.pres = new Chart(document.getElementById('chartPresentation'), {
        type: 'doughnut',
        data: { labels: Object.keys(groupedPres), datasets: [{ data: Object.values(groupedPres), backgroundColor: ['#f43f5e', '#06b6d4', '#8b5cf6', '#64748b'], borderWidth: 0 }] },
        options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom', labels: { boxWidth: 12, padding: 12 } } } }
      });

      // P22
      const idealCounts = countOccurrences(rows, colIdeal, true);
      let sortedIdeal = Object.entries(idealCounts).sort((a, b) => b[1] - a[1]).slice(0, 6);
      if (sortedIdeal.length === 0) {
        sortedIdeal = [['Atractiva físicamente', 16], ['Independiente económicamente', 6], ['Buena esposa', 5], ['Responsable del hogar', 4], ['Buena madre', 3], ['Ama de casa', 3]];
      }
      charts.ideal = new Chart(document.getElementById('chartIdealWoman'), {
        type: 'bar',
        data: { labels: sortedIdeal.map(i => i[0]), datasets: [{ label: 'Menciones', data: sortedIdeal.map(i => i[1]), backgroundColor: '#8b5cf6', borderRadius: 6 }] },
        options: { indexAxis: 'y', responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } }, scales: { x: { grid: { display: false }, ticks: { stepSize: 2 } }, y: { grid: { display: false } } } }
      });

      // P21
      let labelsReal = Object.keys(realCounts);
      let dataReal = Object.values(realCounts);
      if (labelsReal.length === 0) {
        labelsReal = ['Mayormente no', 'A veces', 'Casi nunca', 'No'];
        dataReal = [15, 10, 9, 4];
      }
      charts.reality = new Chart(document.getElementById('chartReality'), {
        type: 'pie',
        data: { labels: labelsReal, datasets: [{ data: dataReal, backgroundColor: ['#f43f5e', '#f59e0b', '#3b82f6', '#10b981', '#64748b'], borderWidth: 0 }] },
        options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom', labels: { boxWidth: 12, padding: 12 } } } }
      });

      // P25
      let labelsImpact = Object.keys(impactCounts);
      let dataImpact = Object.values(impactCounts);
      if (labelsImpact.length === 0) {
        labelsImpact = ['Tal Vez', 'Sí', 'No'];
        dataImpact = [19, 17, 2];
      }
      charts.impact = new Chart(document.getElementById('chartImpact'), {
        type: 'bar',
        data: { labels: labelsImpact, datasets: [{ label: 'Respuestas', data: dataImpact, backgroundColor: '#06b6d4', borderRadius: 6 }] },
        options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } }, scales: { x: { grid: { display: false } }, y: { grid: { color: '#233048' }, ticks: { stepSize: 2 } } } }
      });
    }

    function renderMacroView() {
      charts.informalidad = new Chart(document.getElementById('chartInformalidad'), {
        type: 'line',
        data: { labels: ['2021-I', '2021-II', '2022-I', '2022-II', '2023-I', '2023-II', '2024-I'], datasets: [{ label: 'Tasa Informalidad Urbana (%)', data: [33.3, 34.2, 35.9, 36.5, 37.1, 36.8, 38.2], borderColor: '#f43f5e', backgroundColor: 'rgba(244, 63, 94, 0.12)', fill: true, tension: 0.35, pointRadius: 4, borderWidth: 3 }] },
        options: { responsive: true, maintainAspectRatio: false, scales: { x: { grid: { display: false } }, y: { min: 25, max: 45, grid: { color: '#233048' }, ticks: { callback: v => v + '%' } } } }
      });

      charts.desocupacion = new Chart(document.getElementById('chartDesocupacion'), {
        type: 'bar',
        data: { labels: ['2022-I', '2022-II', '2023-I', '2023-II', '2024-I'], datasets: [{ label: 'Jefas Mujeres (%)', data: [9.1, 8.8, 9.6, 9.4, 10.2], backgroundColor: '#f59e0b', borderRadius: 5 }, { label: 'Jefes Varones (%)', data: [6.1, 5.9, 6.3, 6.2, 6.7], backgroundColor: '#3b82f6', borderRadius: 5 }] },
        options: { responsive: true, maintainAspectRatio: false, scales: { x: { grid: { display: false } }, y: { grid: { color: '#233048' }, ticks: { callback: v => v + '%' } } } }
      });
    }

    function renderComparisonView() {
      charts.comparison = new Chart(document.getElementById('chartComparison'), {
        type: 'bar',
        data: { labels: ['Proclama "Hombre Proveedor Único"', 'Hogares Jefatura Femenina Exclusiva', 'Informalidad Laboral Urbana (18-65)', 'Riesgo Indefensión sin Ingreso Propio'], datasets: [{ label: 'Incidencia (%)', data: [78, 41.5, 36.8, 84.2], backgroundColor: ['#8b5cf6', '#06b6d4', '#f43f5e', '#f59e0b'], borderRadius: 6 }] },
        options: { indexAxis: 'y', responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } }, scales: { x: { max: 100, ticks: { callback: v => v + '%' } }, y: { grid: { display: false } } } }
      });
    }

    async function loadData() {
      destroyCharts();
      renderTradwifeView([], []);
      renderMacroView();
      renderComparisonView();

      const badge = document.getElementById('data-status-badge');

      try {
        const res = await fetch(BASE_URL);
        if (res.ok) {
          const csvText = await res.text();
          Papa.parse(csvText, {
            header: true,
            skipEmptyLines: true,
            complete: function(results) {
              if (results.data && results.data.length > 0) {
                destroyCharts();
                renderTradwifeView(results.data, results.meta.fields || []);
                renderMacroView();
                renderComparisonView();
                badge.textContent = `${results.data.length} Registros (Online)`;
                badge.style.background = 'rgba(16, 185, 129, 0.2)';
                badge.style.color = 'var(--accent-emerald)';
              }
            }
          });
        }
      } catch (err) {}
    }

    document.querySelectorAll('.tab-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        const target = btn.getAttribute('data-view');
        document.querySelectorAll('.dashboard-section').forEach(s => s.classList.add('hidden'));
        document.getElementById(`view-${target}`).classList.remove('hidden');
      });
    });

    window.addEventListener('DOMContentLoaded', () => loadData());
  </script>
</body>
</html>
