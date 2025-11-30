<!DOCTYPE html>
<html lang="es">

<head>
  <meta charset="UTF-8">
  <title>Panel Institucional de Reportes Nominales</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    :root {
      --bg: #f3f5fa;
      --primary: #003366;
      --primary-light: #145da0;
      --accent: #00b8a9;
      --card-bg: #ffffff;
      --text-main: #1f2933;
      --text-muted: #6b7280;
      --radius-lg: 16px;
      --shadow-soft: 0 10px 22px rgba(15, 23, 42, 0.18);
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      background: var(--bg);
      color: var(--text-main);
    }

    .topbar {
      background: #001a33;
      color: #e5e7eb;
      padding: 6px 18px;
      font-size: 0.78rem;
    }

    .topbar-inner {
      max-width: 1200px;
      margin: 0 auto;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
    }

    .topbar span strong {
      letter-spacing: 0.06em;
      text-transform: uppercase;
    }

    header {
      background: linear-gradient(120deg, var(--primary), var(--primary-light));
      color: #fff;
      padding: 18px 18px 20px;
      box-shadow: 0 8px 20px rgba(15, 23, 42, 0.4);
    }

    .header-inner {
      max-width: 1200px;
      margin: 0 auto;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 18px;
    }

    .logo-block {
      display: flex;
      align-items: center;
      gap: 14px;
    }

    .logo-pair {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .logo-img {
      max-height: 40px;
      width: auto;
      display: block;
    }

    header h1 {
      margin: 0;
      font-size: 1.3rem;
    }

    header p {
      margin: 4px 0 0 0;
      font-size: 0.85rem;
      opacity: 0.92;
    }

    .chip {
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.6);
      padding: 6px 12px;
      font-size: 0.78rem;
      display: inline-flex;
      flex-direction: column;
      text-align: right;
    }

    .chip span.label {
      opacity: 0.8;
    }

    .chip span.value {
      font-weight: 600;
    }

    main {
      max-width: 1200px;
      margin: 20px auto 32px;
      padding: 0 16px;
    }

    .info-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
      margin-bottom: 10px;
      font-size: 0.8rem;
      color: var(--text-muted);
    }

    .info-row span.label {
      font-weight: 600;
      color: var(--text-main);
    }

    #fecha-consulta {
      font-weight: 500;
    }

    .tabs {
      display: flex;
      border-radius: 999px;
      background: #d9e2f4;
      padding: 4px;
      max-width: 480px;
      margin: 0 auto 20px;
    }

    .tab-btn {
      flex: 1;
      border: none;
      background: transparent;
      border-radius: 999px;
      padding: 8px 14px;
      font-size: 0.86rem;
      cursor: pointer;
      color: var(--text-muted);
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      transition: all .18s ease;
    }

    .tab-btn-icon {
      font-size: 1rem;
    }

    .tab-btn.active {
      background: #ffffff;
      color: var(--primary);
      box-shadow: 0 4px 10px rgba(15, 23, 42, 0.18);
    }

    .panel {
      display: none;
    }

    .panel.active {
      display: block;
    }

    .panel-header {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: flex-end;
      gap: 14px;
      margin-bottom: 16px;
    }

    .panel-header h2 {
      margin: 0;
      font-size: 1.15rem;
    }

    .panel-header p {
      margin: 4px 0 0;
      font-size: 0.82rem;
      color: var(--text-muted);
    }

    .filters {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      align-items: center;
    }

    .filters-group {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }

    .filters input,
    .filters select {
      padding: 7px 11px;
      border-radius: 999px;
      border: 1px solid #c6d0e8;
      font-size: 0.8rem;
      min-width: 150px;
      outline: none;
      background: #f9fafb;
    }

    .filters input:focus,
    .filters select:focus {
      border-color: var(--primary-light);
      box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.22);
    }

    .btn-reset {
      border-radius: 999px;
      border: 1px solid var(--primary-light);
      background: #ffffff;
      color: var(--primary-light);
      padding: 7px 12px;
      font-size: 0.78rem;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .btn-reset:hover {
      background: #e5edf8;
    }

    .summary-strip {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-bottom: 14px;
      font-size: 0.8rem;
      color: var(--text-muted);
    }

    .summary-pill {
      background: rgba(255, 255, 255, 0.9);
      border-radius: 999px;
      padding: 6px 10px;
      box-shadow: 0 2px 6px rgba(15, 23, 42, 0.12);
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 16px;
    }

    .card {
      background: var(--card-bg);
      border-radius: var(--radius-lg);
      padding: 14px 15px 12px;
      box-shadow: var(--shadow-soft);
      display: flex;
      flex-direction: column;
      gap: 8px;
      border-top: 4px solid rgba(0, 184, 169, 0.9);
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      gap: 8px;
      align-items: flex-start;
    }

    .card h3 {
      margin: 0;
      font-size: 0.98rem;
      color: var(--primary);
    }

    .tag-region {
      font-size: 0.72rem;
      padding: 4px 9px;
      border-radius: 999px;
      background: #e5f4f4;
      color: #035f5f;
    }

    .card p {
      margin: 0;
      font-size: 0.8rem;
      color: var(--text-muted);
    }

    .link-row {
      margin-top: 10px;
    }

    .btn-link {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      width: 100%;
      border: none;
      border-radius: 999px;
      background: linear-gradient(135deg, var(--primary-light), var(--primary));
      color: #fff;
      padding: 10px 14px;
      font-size: 0.84rem;
      cursor: pointer;
      text-decoration: none;
      text-align: center;
      font-weight: 600;
      letter-spacing: 0.04em;
      text-transform: uppercase;
      box-shadow: 0 4px 10px rgba(15, 23, 42, 0.25);
      transition: transform .1s ease, box-shadow .1s ease, opacity .1s ease;
    }

    .btn-link span.icon {
      font-size: 0.9rem;
    }

    .btn-link:hover {
      transform: translateY(-1px);
      box-shadow: 0 6px 14px rgba(15, 23, 42, 0.3);
      opacity: 0.96;
    }

    .empty {
      text-align: center;
      padding: 40px 18px;
      color: var(--text-muted);
      font-size: 0.86rem;
    }

    .footer-note {
      margin-top: 22px;
      font-size: 0.76rem;
      color: var(--text-muted);
      text-align: right;
    }

    @media(max-width:720px) {
      .header-inner {
        flex-direction: column;
        align-items: flex-start;
      }

      header h1 {
        font-size: 1.1rem;
      }

      .logo-pair {
        flex-wrap: wrap;
      }
    }
  </style>
  <script>
    function activateTab(tabId, btn) {
      document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
      document.getElementById(tabId).classList.add('active');
      document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
    }
    function applyFilters(panelId) {
      const panel = document.getElementById(panelId);
      const search = panel.querySelector('.filter-search').value.toLowerCase();
      const prog = panel.querySelector('.filter-programa').value;
      const region = panel.querySelector('.filter-region').value;
      const cards = panel.querySelectorAll('.card');
      let visibles = 0;
      cards.forEach(card => {
        const cProg = card.getAttribute('data-programa');
        const cRegion = card.getAttribute('data-region');
        const text = card.innerText.toLowerCase();
        let visible = true;
        if (prog && cProg !== prog) { visible = false; }
        if (region && cRegion !== region) { visible = false; }
        if (search && !text.includes(search)) { visible = false; }
        card.style.display = visible ? 'flex' : 'none';
        if (visible) visibles++;
      });
      const counter = panel.querySelector('.summary-count');
      if (counter) { counter.textContent = visibles; }
    }
    function clearFilters(panelId, total) {
      const panel = document.getElementById(panelId);
      const searchInput = panel.querySelector('.filter-search');
      const progSelect = panel.querySelector('.filter-programa');
      const regionSelect = panel.querySelector('.filter-region');
      if (searchInput) searchInput.value = '';
      if (progSelect) progSelect.value = '';
      if (regionSelect) regionSelect.value = '';
      const cards = panel.querySelectorAll('.card');
      cards.forEach(card => {
        card.style.display = 'flex';
      });
      const counter = panel.querySelector('.summary-count');
      if (counter) { counter.textContent = total; }
    }
    function setFechaConsulta() {
      const span = document.getElementById('fecha-consulta');
      if (!span) return;
      const opciones = { year: 'numeric', month: '2-digit', day: '2-digit' };
      const ahora = new Date();
      span.textContent = ahora.toLocaleDateString('es-PE', opciones);
    }
    window.addEventListener('DOMContentLoaded', setFechaConsulta);
  </script>
</head>

<body>
  <div class="topbar">
    <div class="topbar-inner">
      <span><strong>MINEDU</strong> · Dirección de Formación Docente en Servicio (DIFODS)</span>
      <span>Campus virtual SIFODS · Módulo de reportes nominales</span>
    </div>
  </div>
  <header>
    <div class="header-inner">
      <div class="logo-block">
        <!--
            <div class="logo-pair">
        <img src="logo_minedu.svg" class="logo-img" alt="Logo Ministerio de Educación del Perú">
        <img src="logo_sifods.svg" class="logo-img" alt="Logo plataforma SIFODS">
      </div>
      -->
        <div>
          <h1>Acceso a Reportes Nominales</h1>
          <p>Visualización de los reportes por Accion Formativa.</p>
        </div>
      </div>
      <div class="chip">
        <span class="label">Uso interno · Gestión académica</span>
        <span class="value">DIFODS · SIFODS</span>
      </div>
    </div>
  </header>
  <main>
    <div class="info-row">
      <span><span class="label">Fecha de consulta:</span> <span id="fecha-consulta"></span></span>
      <span>Panel de apoyo para seguimiento, validación y cierre de indicadores.</span>
    </div>
    <div class="tabs"><button class="tab-btn active" onclick="activateTab('panel0',this)"><span
          class="tab-btn-icon">📊</span>Reporte de Nominales</button></div>
    <section id="panel0" class="panel active">
      <div class="panel-header">
        <div>
          <h2>Reporte de Nominales</h2>
          <p>Acceso consolidado a reportes nominales vinculados a esta hoja del Indicador 02.</p>
        </div>
        <div class="filters">
          <div class="filters-group"><input type="text" class="filter-search" placeholder="Buscar por texto..."
              onkeyup="applyFilters('panel0')"><select class="filter-programa" onchange="applyFilters('panel0')">
              <option value="">Programa (todos)</option>
              <option value="BIAE">BIAE</option>
              <option value="BICENTENARIO">BICENTENARIO</option>
              <option value="CFI">CFI</option>
              <option value="COMPETENCIA LECTORA">COMPETENCIA LECTORA</option>
              <option value="COMPETENCIA LECTORA CALLAO">COMPETENCIA LECTORA CALLAO</option>
              <option value="CONDORCANQUI">CONDORCANQUI</option>
              <option value="CONSOLIDADO ESTRATEGIAS FORMATIVAS 2025">CONSOLIDADO ESTRATEGIAS FORMATIVAS 2025</option>
              <option value="CONSOLIDADO OS 2025">CONSOLIDADO OS 2025</option>
              <option value="DIBRED">DIBRED</option>
              <option value="DIPLOMADO DE METODOLOGÍAS ACTIVAS">DIPLOMADO DE METODOLOGÍAS ACTIVAS</option>
              <option value="EBA">EBA</option>
              <option value="EDUCUNA">EDUCUNA</option>
              <option value="EIB">EIB</option>
              <option value="EIB UNAP">EIB UNAP</option>
              <option value="EIB UNTRM">EIB UNTRM</option>
              <option value="FLEXIBLES">FLEXIBLES</option>
              <option value="FORMACION FORMADORES">FORMACION FORMADORES</option>
              <option value="INDECOPI">INDECOPI</option>
              <option value="INSCRITOS">INSCRITOS</option>
              <option value="INTELIGENCIA ARTIFICIAL">INTELIGENCIA ARTIFICIAL</option>
              <option value="MULTIGRADO NIVEL 1">MULTIGRADO NIVEL 1</option>
              <option value="MULTIGRADO NIVEL 2">MULTIGRADO NIVEL 2</option>
              <option value="PAD OAM">PAD OAM</option>
              <option value="PDP 1">PDP 1</option>
              <option value="PDP 2">PDP 2</option>
              <option value="PID">PID</option>
              <option value="PID ASESORIAS">PID ASESORIAS</option>
              <option value="PIP">PIP</option>
              <option value="PRONOEI">PRONOEI</option>
              <option value="PRONOEI FOCALIZADO/NO FOCALIZADO/DRE-UGEL">PRONOEI FOCALIZADO/NO FOCALIZADO/DRE-UGEL
              </option>
              <option value="REPORTE DETALLADO ESTRATEGIAS FORMATIVAS">REPORTE DETALLADO ESTRATEGIAS FORMATIVAS</option>
              <option value="SANTA ROSA">SANTA ROSA</option>
              <option value="SOPORTE SOCIOEMOCIONAL">SOPORTE SOCIOEMOCIONAL</option>
            </select><select class="filter-region" onchange="applyFilters('panel0')">
              <option value="">Región (todas)</option>
              <option value="AMAZONAS">AMAZONAS</option>
              <option value="ANCASH">ANCASH</option>
              <option value="APURIMAC">APURIMAC</option>
              <option value="AREQUIPA">AREQUIPA</option>
              <option value="AYACUCHO">AYACUCHO</option>
              <option value="CAJAMARCA">CAJAMARCA</option>
              <option value="CALLAO">CALLAO</option>
              <option value="CUSCO">CUSCO</option>
              <option value="GENERAL">GENERAL</option>
              <option value="HUANCAVELICA">HUANCAVELICA</option>
              <option value="HUANUCO">HUANUCO</option>
              <option value="ICA">ICA</option>
              <option value="JUNIN">JUNIN</option>
              <option value="LA LIBERTAD">LA LIBERTAD</option>
              <option value="LAMBAYEQUE">LAMBAYEQUE</option>
              <option value="LIMA METROPOLITANA">LIMA METROPOLITANA</option>
              <option value="LIMA PROVINCIAS">LIMA PROVINCIAS</option>
              <option value="LORETO">LORETO</option>
              <option value="MADRE DE DIOS">MADRE DE DIOS</option>
              <option value="MOQUEGUA">MOQUEGUA</option>
              <option value="PASCO">PASCO</option>
              <option value="PIURA">PIURA</option>
              <option value="PUNO">PUNO</option>
              <option value="SAN MARTIN">SAN MARTIN</option>
              <option value="SIN REGIÓN">SIN REGIÓN</option>
              <option value="TACNA">TACNA</option>
              <option value="TUMBES">TUMBES</option>
              <option value="UCAYALI">UCAYALI</option>
            </select></div><button type="button" class="btn-reset"
            onclick="clearFilters('panel0',168)"><span>✕</span><span>Limpiar filtros</span></button>
        </div>
      </div>
      <div class="summary-strip">
        <div class="summary-pill">Total enlaces: <strong class="summary-count">168</strong></div>
        <div class="summary-pill">Programas: <strong>33</strong></div>
        <div class="summary-pill">Regiones: <strong>28</strong></div>
      </div>
      <div class="grid">
        <article class="card" data-programa="BIAE" data-region="GENERAL">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ijKEQhAewo-vLk6FTfcSsFVLWnfBtyiW/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="AMAZONAS">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">AMAZONAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1qXEWDYvv49CqdbXvxSNzXPxGBRwo1jkg/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="ANCASH">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">ANCASH</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1gaufRKyiaRVyUPYqPMcmaAIAYmN8Pw_h/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="APURIMAC">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">APURIMAC</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1c9nKoQSZ0IEVibu-3u096iILMWwPUxHt/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="AREQUIPA">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">AREQUIPA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1jpEEqWBwmhitEdedaV-UUOFk2nvFbo8R/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="AYACUCHO">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">AYACUCHO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ktezcQpic3Mf9fvS_3PdLg0-ySBb37to/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="CAJAMARCA">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">CAJAMARCA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ebr4qnqW7qkamvMkanKQGOowiMYQZ1yx/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="CALLAO">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">CALLAO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1W7zRlZbUaKgSAlllVJ7GpFCAvxFpV6EB/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="CUSCO">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">CUSCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1hL8Wq2yJCG52h0Akl3CY1edc5tBLaNm_/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="HUANCAVELICA">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">HUANCAVELICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1SJcWmNvevY8vF49LXdPeQgG5L8eCi_4v/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="HUANUCO">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">HUANUCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1m7dmfqWWRcbrm7DffkSw8QM9OPEGgKkL/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="ICA">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">ICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/11CN75suHREJHq9PqWWGUSRABPdJtilR3/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="JUNIN">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">JUNIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1jvaYfmAfdu28z4Ppt1-5tSDHaDF1uYBU/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="LA LIBERTAD">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">LA LIBERTAD</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/19n8DbSmUrZ3_aAaM_JM0If20My8JHe9W/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="LAMBAYEQUE">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">LAMBAYEQUE</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1l_r2n8lzq1PJ-Stw0RYt34UJEi2d6Oso/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="LIMA METROPOLITANA">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">LIMA METROPOLITANA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Uf4ftyR9LlL1JuKW1l6J-_MzYMRP2wZw/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="LIMA PROVINCIAS">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">LIMA PROVINCIAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1eb_K_jwH07o_5E0KlH79VURPf2aFA5f1/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="LORETO">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">LORETO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1xaHcmBR5jTK5RQpdW6I3zvBZfcqZtT7g/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="MADRE DE DIOS">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">MADRE DE DIOS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1LOyivlf993omXKfw81pQag2TsoELY8mi/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="MOQUEGUA">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">MOQUEGUA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1IRpY_HgNFJ3bo5dPtDFsq-X20ZIgnow_/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="PASCO">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">PASCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1hAuctROjm3EmqPwxJBX8kZTC6-SXMWHU/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="PIURA">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">PIURA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/10DaOt9FXX5V0WBFut1Mo6Ci1QNfEiWRS/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="PUNO">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">PUNO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1wDpskM3omc4djmXS-qCtaroztMS7hLD8/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="SAN MARTIN">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">SAN MARTIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Tm5LqUBEq3ciay4tGMFcksHxsos1krVh/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="TACNA">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">TACNA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1bFXb9zvFN71c7-jDoKgBTWCEPrQyHIp7/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="TUMBES">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">TUMBES</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/13WVl0z4p9yLFUzgOIYa0pOj9x76VjNvs/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="UCAYALI">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">UCAYALI</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1lR4H9d9zKzw0HQXt3PatF92G25lxiLRw/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BIAE" data-region="SIN REGIÓN">
          <div class="card-header">
            <h3>BIAE</h3>
            <span class="tag-region">SIN REGIÓN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/10CAb_JP-CHt5SD466DYAFHj6qee5JHY9/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="BICENTENARIO" data-region="GENERAL">
          <div class="card-header">
            <h3>BICENTENARIO</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1vnvF1cGzwWPxcjz_n7s2mpfEAZSA3K2i/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="CFI" data-region="GENERAL">
          <div class="card-header">
            <h3>CFI</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/18GONtBTuW_TSosLEQFRZ6_Nh6iPkpOwz/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="GENERAL">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1KrQa-wQUysMHBw8yKtp_CQsagUfU-Fyw/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="AMAZONAS">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">AMAZONAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1z96ur4aGc7RV5ZpTUiIZk0yxCxnb-GvY/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="ANCASH">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">ANCASH</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1mmQBm16NJwyRtm-Aay8_xZ9xb-_yfMpp/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="APURIMAC">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">APURIMAC</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1S5i7vIzQWG7tFnH-NuPGgm5jfakkB7HY/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="AREQUIPA">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">AREQUIPA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1iZpsRBqTuzBzZUgAwUnjNKRA__-TmJgm/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="AYACUCHO">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">AYACUCHO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/16_pkteThyScdjiOwnQlPcaESkLjrbXuB/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="CAJAMARCA">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">CAJAMARCA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1dNi2RKtVNRwgktwRsI55lSYJg8zhtk9a/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="CALLAO">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">CALLAO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1SNs-glpC04n3KJGlB1YC_cEpbax9op5q/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="CUSCO">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">CUSCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1idt6U52mnrR9PXJNHOZtsgbY1KTn_P9i/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="HUANCAVELICA">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">HUANCAVELICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1W2tbp8saTLhDp0IgWPMWjldpC0QJyJLj/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="HUANUCO">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">HUANUCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1RLdQaSAMsNDUXTAxsWk7qhPKfOmAEUt4/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="ICA">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">ICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1GF42gGMsXIF6tRh9t6FsUsd_vooPPjb5/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="JUNIN">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">JUNIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1aB_Dzi75PKzXqoC7pZsnsxHlwcsSMiQH/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="LA LIBERTAD">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">LA LIBERTAD</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1W6TnRad6jCsLRC7as-fE4XVJtPB5YKsK/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="LAMBAYEQUE">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">LAMBAYEQUE</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1FPkadu0juiTCioRYE6bdMMJSInzm6YZE/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="LIMA METROPOLITANA">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">LIMA METROPOLITANA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Q8z8xoe1zgsdg78CFrmT9reLH7EkUshQ/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="LIMA PROVINCIAS">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">LIMA PROVINCIAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1KCMHb7Z9y9gWj7sq_zbfFhO7OLJn_QsJ/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="LORETO">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">LORETO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1yI0LZhAuVSCA7m6ONLckfm-EFnEWkE9p/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="MADRE DE DIOS">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">MADRE DE DIOS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1tdfy85HS1HvVpE5gQLd1QZy2l1aCnuTX/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="MOQUEGUA">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">MOQUEGUA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/19MJoM1aVURDWvVKRqEGZMS2ph4YEXzAn/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="PASCO">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">PASCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1VVDbt-BWt10IhnCBT007gY-o0pNy2ICP/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="PIURA">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">PIURA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1WLzp9_JIEPht8W574OwPOdrTt2j_aJhg/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="PUNO">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">PUNO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Hd_D6wT793ocw6Nr0MdYSZOifqtnLotz/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="SAN MARTIN">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">SAN MARTIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1rnDDMGQd0MIJ4ZJtR6BzAYyRMiNZjCgH/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="TACNA">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">TACNA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1D9B14KEGtU7L_PN8Z0yEsTilHrAX-ZX1/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="TUMBES">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">TUMBES</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1WVft5EluewwMfmmX1NNr0ebKEGQn6MLU/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="UCAYALI">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">UCAYALI</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1NhWDOHSd7u8HKhzzv789hlwz5LSR7hrS/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA" data-region="SIN REGIÓN">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA</h3>
            <span class="tag-region">SIN REGIÓN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1nQO8D5nj0peul70LB-DHEQxdARK3Fuew/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="COMPETENCIA LECTORA CALLAO" data-region="CALLAO">
          <div class="card-header">
            <h3>COMPETENCIA LECTORA CALLAO</h3>
            <span class="tag-region">CALLAO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1iypedq08JNdfDj0JYt3rJQSjuwmvrR2g/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="CONDORCANQUI" data-region="GENERAL">
          <div class="card-header">
            <h3>CONDORCANQUI</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ox9CjlZUOZxWmL6GFAkavQXF4xUyybai/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="CONSOLIDADO ESTRATEGIAS FORMATIVAS 2025" data-region="GENERAL">
          <div class="card-header">
            <h3>CONSOLIDADO ESTRATEGIAS FORMATIVAS 2025</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1QRD13PfOtQsO6LyM0kfSLyE98BppJMoo/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="CONSOLIDADO OS 2025" data-region="GENERAL">
          <div class="card-header">
            <h3>CONSOLIDADO OS 2025</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1apibOpu6hiNbDW3vrH4tPz6nc1w2Bn1p/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="DIBRED" data-region="GENERAL">
          <div class="card-header">
            <h3>DIBRED</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1wYlob-OGEf368VRTVlzSkOApryzxcrhl/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="DIPLOMADO DE METODOLOGÍAS ACTIVAS" data-region="GENERAL">
          <div class="card-header">
            <h3>DIPLOMADO DE METODOLOGÍAS ACTIVAS</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1oCp6X9a5sNiOerYygJIMTVu1uyEBiXi9/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="EBA" data-region="GENERAL">
          <div class="card-header">
            <h3>EBA</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1EywKNyruWE8Uhymlyrx5FmR6fmYhDqu-/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="EDUCUNA" data-region="GENERAL">
          <div class="card-header">
            <h3>EDUCUNA</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1d6sHC9NCc2ERsVLZm742eQklXSyIC8Fc/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="EIB UNAP" data-region="GENERAL">
          <div class="card-header">
            <h3>EIB UNAP</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Vw22IrzFrniAxK5VUzFFrQSS9GRlYIrv/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="EIB UNTRM" data-region="GENERAL">
          <div class="card-header">
            <h3>EIB UNTRM</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1yEDch9EwYio1LBftrfljz9ARllRaEaYG/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="FLEXIBLES" data-region="GENERAL">
          <div class="card-header">
            <h3>FLEXIBLES</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1H-yp0cu-MX-_ofdhwyG_fTElcVYvkdg_/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="FORMACION FORMADORES" data-region="GENERAL">
          <div class="card-header">
            <h3>FORMACION FORMADORES</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1L5-f8elXqooVFKZdV1g7M-f7LgpGtUJA/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="GENERAL">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1uYDxoKRzC3Mf4iai4s5VgVA-x3bnYsD1/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="AMAZONAS">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">AMAZONAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1bpv2RAFT1l6iLsI8qDcfx9uvhS6YxX6j/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="ANCASH">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">ANCASH</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1lN_d1WXqzXI_NMTN5UhLax-wNCASrnGJ/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="APURIMAC">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">APURIMAC</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1hHy_O2iC4yjgB5H-AQ24IDgbLYfZRf1R/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="AREQUIPA">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">AREQUIPA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/10NQEbSkRhKdrrvlGjtCRvZF6ERmrs-uo/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="AYACUCHO">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">AYACUCHO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/185OcG6QF-PAUy9PoLEGvdtmLJ4vXawVp/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="CAJAMARCA">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">CAJAMARCA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/182_0ebm7Gh7juFw5tvDY8ZzgoIRKhbMz/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="CALLAO">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">CALLAO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1LTMc3vcQoFjn9fmWxKn4k2pnXa25kKqM/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="CUSCO">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">CUSCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1sga4mM9vtUbJpRNfY9oADnXNm1DTm0uV/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="HUANCAVELICA">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">HUANCAVELICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/10dlEkAeFphE95xbZ_oDjDPum8dq95aS2/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="HUANUCO">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">HUANUCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1BP_ZJiDgE5RNOqOylfxphAyJna5KyNYE/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="ICA">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">ICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1cxZ_MjF1dVWrD3-7iv0P9JIEPyoElJTR/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="JUNIN">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">JUNIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1oQLhBhvy8WkADbFKSGFEbLY3ZtC4U6Vh/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="LA LIBERTAD">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">LA LIBERTAD</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1bInGfVgIL_69ywhW4EzM2hUaXMgIlxfz/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="LAMBAYEQUE">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">LAMBAYEQUE</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Ahgy6SaHBZ1XWIFo7WiW6N0msRtkx0Qh/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="LIMA METROPOLITANA">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">LIMA METROPOLITANA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Jc6HibdhbCvBqD5DSEpU40jMSOlKYdlS/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="LIMA PROVINCIAS">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">LIMA PROVINCIAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1-P_3KDoM0BS6M4THlU3JvJkIZqfU-yma/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="LORETO">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">LORETO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1_xRbuYC2DAy4nuvMJVmvfWj5UzNt547S/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="MADRE DE DIOS">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">MADRE DE DIOS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ge_H1AI6zeJbCj8mzu5oK7Zjn7csKRAp/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="MOQUEGUA">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">MOQUEGUA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1rZscaFFwwjBPIwI4CFg-VfytnqfblTKI/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="PASCO">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">PASCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1qyZkbD7zuNvgs80f6RVr0lGnVzkOzTfr/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="PIURA">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">PIURA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/17hq66JiKXyHQxomeiR65XF4R1X6psPbz/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="PUNO">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">PUNO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1llb1RnNzyEad55gJc1s_Tn5H3YbKoHAw/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="SAN MARTIN">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">SAN MARTIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1LtuAVLG8sDFR3FcNqJv8270yg5ZitwkC/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="TACNA">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">TACNA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1sT-OexeY3_SqBwnYQuHR4oHifOS0yx8m/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="TUMBES">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">TUMBES</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1BpyvSQv79TIuJXaB4pwhNZsCcrpN-ELs/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="UCAYALI">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">UCAYALI</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1eDKI7tQkih1xI53VG29TsFd1NkfPXmAH/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INDECOPI" data-region="SIN REGIÓN">
          <div class="card-header">
            <h3>INDECOPI</h3>
            <span class="tag-region">SIN REGIÓN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1MLJWsLOSogkQrNkCVNSiJBSs1_9Nu1de/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INSCRITOS" data-region="GENERAL">
          <div class="card-header">
            <h3>INSCRITOS</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Ybvpis_gwjOSW4pna6Cq7qHbTekYKT73/edit?usp=drive_link&ouid=114947891880206951532&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="GENERAL">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/15WRMjVPk1xRtsBv9_u9AJi8N76NEKiTA/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="AMAZONAS">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">AMAZONAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1SRyG8PXFuB7lhy2dWl3SFhW1HEW0dm3X/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="ANCASH">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">ANCASH</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1edb616jL_N-gQOOEG04_fMEifb0n6mSo/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="APURIMAC">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">APURIMAC</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1qONBBlhpJjJ5_3lx-ZPgiBy4inNd_Ppn/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="AREQUIPA">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">AREQUIPA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1pJFTbm4UzH9GwMRX4Ka8bhLB5EuuejPB/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="AYACUCHO">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">AYACUCHO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/10jtHh0sy0sbVn29ohSSPSrpsBGvqlRAa/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="CAJAMARCA">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">CAJAMARCA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1vykxr7JvGc_25LLV3bfZVP6N3ThgNzUj/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="CALLAO">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">CALLAO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ZQ49SPYRgL-I42Tg2whof0yRbtNr3URu/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="CUSCO">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">CUSCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1eApTBzFwxKc1XZ2DW-OTtP2EeYi5WA0o/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="HUANCAVELICA">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">HUANCAVELICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ONF6fkJiO3ytxiOm3p78kf53NXXOWhho/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="HUANUCO">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">HUANUCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1arh5dhiUW53TLi-7L6Y3mXDv0VrrvEWb/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="ICA">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">ICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1LXlca3BCeMEQqdX3dkciAJmIoHvBXS7U/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="JUNIN">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">JUNIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ZBuYkVJnxOTRy6ikGP9N1R-bYOjqSCwJ/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="LA LIBERTAD">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">LA LIBERTAD</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/15bYxa4PbnNFAdLZqxiP8mNSl7iw0Ejpj/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="LAMBAYEQUE">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">LAMBAYEQUE</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1SqdcFHXyEVwM8qQZiDopaxNybHnz0Xej/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="LIMA METROPOLITANA">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">LIMA METROPOLITANA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ZhO0qj5zFt--Nw7_Le777qnZ1zHfhTWy/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="LIMA PROVINCIAS">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">LIMA PROVINCIAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1bW9UWsCiNt2uqhoVX1IyA1haVwN_Nu3K/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="LORETO">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">LORETO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1xAMM_-116SoZtnJ3DkG3EMXBE88kKWEL/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="MADRE DE DIOS">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">MADRE DE DIOS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Inz2UuLa5Bod64WObyFyLj2rQ6E_3M7A/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="MOQUEGUA">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">MOQUEGUA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1BTlHKaJxx-VPNg2XKnkXbg664hm2ee3r/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="PASCO">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">PASCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/12EkscTZVxEcy6C7-sBLooK1z-kD_ocw5/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="PIURA">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">PIURA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1OWligl2yGUZ_x6oGhAxr1UeL3Ty-T21E/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="PUNO">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">PUNO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1CaYNvLn4gk9-TiEiIcV30uab5Z00Co12/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="SAN MARTIN">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">SAN MARTIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Jf9r3vCIftX53YylLofxH34_6Wx72ih4/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="TACNA">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">TACNA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Hb2YoTSWOElkyBdIddrMBg72vpzNQH6r/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="TUMBES">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">TUMBES</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1o-qvlSU7B_yjrOUAypJWkNt0kg5zgCwV/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="UCAYALI">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">UCAYALI</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/11ylOdkk-jK0ir8IV7gDT4CJMZgCgW3_C/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="INTELIGENCIA ARTIFICIAL" data-region="SIN REGIÓN">
          <div class="card-header">
            <h3>INTELIGENCIA ARTIFICIAL</h3>
            <span class="tag-region">SIN REGIÓN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1as4M358NvL9_LW9Gq67_A7L09V1duAHh/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="MULTIGRADO NIVEL 1" data-region="GENERAL">
          <div class="card-header">
            <h3>MULTIGRADO NIVEL 1</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1gMgJ2i-cmNPUiSt451MvfBKboL7FHIEh/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="MULTIGRADO NIVEL 2" data-region="GENERAL">
          <div class="card-header">
            <h3>MULTIGRADO NIVEL 2</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1TKVfsGVJd5zWRVRuL8NavMjNY9-K7Bb9/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PAD OAM" data-region="GENERAL">
          <div class="card-header">
            <h3>PAD OAM</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1B6TpOc20PJMI_NWFWATvL_AQE0LaCLAp/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PDP 1" data-region="GENERAL">
          <div class="card-header">
            <h3>PDP 1</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1wvWlngAwI4hOtJTXoyXibUS1Xk3M4qyt/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PDP 2" data-region="GENERAL">
          <div class="card-header">
            <h3>PDP 2</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/16Ii9p9Y8ePJLa_c5lMRYVKwvW9mWodY-/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PID" data-region="GENERAL">
          <div class="card-header">
            <h3>PID</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/125-Xdbfo1QE5hV7qgD8cNVbVSOGOhnJO/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PID ASESORIAS" data-region="GENERAL">
          <div class="card-header">
            <h3>PID ASESORIAS</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1DfOyjkQWEJvUrArguzQVRgnpKr0CFNnt/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PIP" data-region="GENERAL">
          <div class="card-header">
            <h3>PIP</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1XMiVtdM20ymzqiPcjvfDFDr17Xrtfj1Y/edit?usp=sharing&ouid=106295393661798530349&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="GENERAL">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1fFMFcJtsuefHArHgq3DzUigLVuJLed0h/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="AMAZONAS">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">AMAZONAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1h_LouUlRkGGcCGcDASmRb-8_R-jaXdhl/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="ANCASH">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">ANCASH</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1Ep-yOBJ5bHGTmF5DF4VxFdKvQPxc9ipN/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="APURIMAC">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">APURIMAC</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1TTr2yQARV7C816tgVeXhW8kGvUNchrDl/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="AREQUIPA">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">AREQUIPA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1aZ6u_vtWAerwxoJhQmUk6WEpRN17aLMQ/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="AYACUCHO">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">AYACUCHO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/16Wwh8x_ErdEx8frH3SrZaRo88yfngjiR/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="CAJAMARCA">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">CAJAMARCA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1k6QMce0kF7zXq9NODALKtafHcMFpw6EN/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="CALLAO">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">CALLAO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1r0UT9bUwfV_sVaeRvWlZmAsptP1rXwzp/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="CUSCO">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">CUSCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1IJby0fyxN2ehhF1Umv6ABQmeDFblvMr2/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="HUANCAVELICA">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">HUANCAVELICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/12iOsIt1vsj3OB9oct0hR1ux2e5PFBHUW/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="HUANUCO">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">HUANUCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1LrrxPmu0VgL_msolMZO3nhRgrocEqtbx/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="ICA">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">ICA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1SmyP8WCN3uZD_xSPmxjSHMQ0O07-uWjY/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="JUNIN">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">JUNIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1TBL6YheBN5EHR9OCjyUYFyoK2crLgA_n/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="LA LIBERTAD">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">LA LIBERTAD</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/16cdsMgsfN6PXZnzbu4GPAkm5FMuA9EVn/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="LAMBAYEQUE">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">LAMBAYEQUE</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1JK9qIOJVDwKDkvWUmZCtVRRYxEHerC3b/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="EIB" data-region="GENERAL">
          <div class="card-header">
            <h3>EIB</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1TC0xtQJ4V-hOIAGwkeCWSv6_lY4fT6VR/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="LIMA METROPOLITANA">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">LIMA METROPOLITANA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/12lnEHppvge9Dybht8u2DEKCb7lnCtx_e/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="LIMA PROVINCIAS">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">LIMA PROVINCIAS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1gW88ahL3kWhVGSiWCHLeP_xM4Fod5qSv/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="LORETO">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">LORETO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1pqnIjf4uEcUwFlebj45h-p4UP7bHfI1n/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="MADRE DE DIOS">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">MADRE DE DIOS</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/17_zGxUurFQFDgLKNAEKqFdvrS0sfKpVF/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="MOQUEGUA">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">MOQUEGUA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1ihEUGOEECeewEtb9B1MD76gd4dUwCn2i/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="PASCO">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">PASCO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1HNPsB6kpJ32DJM_iFWT1vCpOaqiC6miA/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="PIURA">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">PIURA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1NpSurrJf9HlZ9zzow3aWOvguNjDIa_5P/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="PUNO">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">PUNO</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1tzh3Pd7dNlIy5WaTgZt4HMoXoUQ-TqPI/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="SAN MARTIN">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">SAN MARTIN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/16L_iTEI9CZ87O76K9Ssh5j_T2UIaxq5X/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="TACNA">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">TACNA</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1D6E_n-3N8vF8IbinCFjMCq6_jH5YJdVc/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="TUMBES">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">TUMBES</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1yEh20_Qph2qvFw-PVaw3wNXnMTHe76he/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="UCAYALI">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">UCAYALI</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1MIGwDJYnsvaCTV0dJ3k80W2u0WLFLqwc/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI" data-region="SIN REGIÓN">
          <div class="card-header">
            <h3>PRONOEI</h3>
            <span class="tag-region">SIN REGIÓN</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1_omGc76RiNE0pwHKziatVA0gyaIf4Jig/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="PRONOEI FOCALIZADO/NO FOCALIZADO/DRE-UGEL" data-region="GENERAL">
          <div class="card-header">
            <h3>PRONOEI FOCALIZADO/NO FOCALIZADO/DRE-UGEL</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/14OMQshfQMyzBO2_q5ba57F1JZM0Il44N/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="REPORTE DETALLADO ESTRATEGIAS FORMATIVAS" data-region="GENERAL">
          <div class="card-header">
            <h3>REPORTE DETALLADO ESTRATEGIAS FORMATIVAS</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1TOp9EMrRRsUtLWa_AHhN1Ph6eNtGvgz4/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="SANTA ROSA" data-region="GENERAL">
          <div class="card-header">
            <h3>SANTA ROSA</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1OLl5_vt8PYCa57CUoZPPLGS24HJLEz1N/edit?usp=drive_link&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>

        <article class="card" data-programa="SOPORTE SOCIOEMOCIONAL" data-region="GENERAL">
          <div class="card-header">
            <h3>SOPORTE SOCIOEMOCIONAL</h3>
            <span class="tag-region">GENERAL</span>
          </div>
          <p>Enlace nominal correspondiente al programa en la región indicada. Uso para seguimiento, validación y
            control de indicadores.</p>
          <div class="link-row">
            <a class="btn-link"
              href="https://docs.google.com/spreadsheets/d/1rNKUjtG9ltBGvf4fC5tGp-ASE5MunRHd/edit?usp=sharing&ouid=110241593035439909584&rtpof=true&sd=true"
              target="_blank" rel="noopener noreferrer">
              <span class="icon">📄</span>
              <span>Ver reporte</span>
            </a>
          </div>
        </article>
      </div>
    </section>
    <div class="footer-note">Panel de consulta para equipos de gestión y monitoreo académico.</div>
  </main>
</body>

</html>
