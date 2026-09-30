<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Work Roll Bending | Flatness Control Simulator</title>
  <style>
    :root {
      --bg: #0a0f15;
      --surface: #111922;
      --surface-2: #16212c;
      --surface-3: #1b2936;
      --line: rgba(157, 182, 204, 0.17);
      --line-bright: rgba(157, 205, 232, 0.38);
      --text: #edf6fc;
      --muted: #91a8b9;
      --muted-2: #668195;
      --cyan: #55e8f6;
      --cyan-deep: #1aa8c2;
      --blue: #5b9cff;
      --amber: #ffbf63;
      --orange: #ff845d;
      --green: #72e0a2;
      --red: #ff7c81;
      --shadow: 0 24px 70px rgba(0, 0, 0, 0.35);
      --radius: 18px;
      --small-radius: 12px;
    }

    * { box-sizing: border-box; }

    html, body {
      width: 100%;
      height: 100%;
      margin: 0;
      overflow: hidden;
      background: var(--bg);
      color: var(--text);
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    body {
      display: grid;
      place-items: center;
      background:
        radial-gradient(circle at 8% 12%, rgba(38, 120, 151, 0.13), transparent 31%),
        radial-gradient(circle at 94% 87%, rgba(74, 77, 151, 0.13), transparent 30%),
        #0a0f15;
    }

    button, input { font: inherit; }

    button { color: inherit; }

    .app-shell {
      width: 100vw;
      height: 100vh;
      min-width: 900px;
      min-height: 560px;
      padding: clamp(14px, 1.5vw, 26px);
      display: grid;
      grid-template-rows: auto minmax(0, 1fr) auto;
      gap: clamp(10px, 1.2vw, 18px);
      background:
        linear-gradient(115deg, rgba(255,255,255,0.018), transparent 40%),
        linear-gradient(180deg, rgba(16, 26, 35, 0.6), rgba(9, 14, 20, 0.75));
    }

    .topbar {
      min-height: 58px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 18px;
    }

    .brand-lockup {
      display: flex;
      align-items: center;
      gap: 13px;
      min-width: 0;
    }

    .brand-mark {
      width: 45px;
      height: 45px;
      flex: 0 0 auto;
      display: grid;
      place-items: center;
      border: 1px solid rgba(85, 232, 246, 0.42);
      border-radius: 14px;
      background:
        linear-gradient(145deg, rgba(85, 232, 246, 0.19), rgba(85, 232, 246, 0.02)),
        #11202a;
      color: var(--cyan);
      font-size: 12px;
      font-weight: 800;
      letter-spacing: 0.13em;
      box-shadow: inset 0 0 20px rgba(85, 232, 246, 0.06), 0 8px 22px rgba(0,0,0,0.22);
    }

    .eyebrow,
    .section-kicker,
    .metric-label,
    .profile-axis-label,
    .footer-label {
      color: var(--muted-2);
      font-size: 10px;
      font-weight: 800;
      letter-spacing: 0.16em;
      text-transform: uppercase;
    }

    .eyebrow { margin-bottom: 3px; }

    h1, h2, p { margin: 0; }

    h1 {
      max-width: 850px;
      overflow: hidden;
      color: var(--text);
      font-size: clamp(18px, 1.75vw, 29px);
      font-weight: 720;
      letter-spacing: -0.035em;
      line-height: 1.05;
      text-overflow: ellipsis;
      white-space: nowrap;
    }

    .topbar-tools {
      display: flex;
      align-items: center;
      justify-content: flex-end;
      gap: 8px;
      flex-wrap: wrap;
    }

    .live-chip,
    .mode-chip,
    .small-chip,
    .footer-chip {
      border: 1px solid var(--line);
      border-radius: 999px;
      background: rgba(18, 29, 39, 0.78);
      color: var(--muted);
      font-size: 10px;
      font-weight: 750;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      white-space: nowrap;
    }

    .live-chip,
    .mode-chip { padding: 9px 12px; }

    .live-chip {
      display: inline-flex;
      align-items: center;
      gap: 7px;
      color: var(--green);
      border-color: rgba(114, 224, 162, 0.28);
      background: rgba(44, 125, 87, 0.12);
    }

    .live-dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: currentColor;
      box-shadow: 0 0 0 4px rgba(114, 224, 162, 0.1), 0 0 14px currentColor;
      animation: pulse 1.8s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 0.7; transform: scale(0.86); }
      50% { opacity: 1; transform: scale(1.12); }
    }

    .fullscreen-btn {
      min-height: 34px;
      padding: 0 12px;
      border: 1px solid var(--line-bright);
      border-radius: 10px;
      background: rgba(25, 38, 49, 0.78);
      color: var(--muted);
      cursor: pointer;
      font-size: 11px;
      font-weight: 750;
      letter-spacing: 0.04em;
      transition: 160ms ease;
    }

    .fullscreen-btn:hover { color: var(--text); border-color: var(--cyan); background: rgba(38, 70, 81, 0.75); }

    .main-grid {
      min-height: 0;
      display: grid;
      grid-template-columns: minmax(0, 1.86fr) minmax(350px, 1fr);
      gap: clamp(10px, 1.2vw, 18px);
    }

    .panel {
      min-width: 0;
      min-height: 0;
      border: 1px solid var(--line);
      border-radius: var(--radius);
      background:
        linear-gradient(145deg, rgba(255,255,255,0.027), transparent 28%),
        rgba(16, 25, 34, 0.94);
      box-shadow: var(--shadow), inset 0 1px 0 rgba(255,255,255,0.025);
    }

    .process-panel {
      padding: clamp(14px, 1.35vw, 22px);
      display: grid;
      grid-template-rows: auto minmax(0, 1fr) auto;
      gap: 12px;
      overflow: hidden;
    }

    .panel-head {
      min-height: 42px;
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 14px;
    }

    .panel-title {
      color: var(--text);
      font-size: clamp(13px, 1.05vw, 16px);
      font-weight: 780;
      letter-spacing: 0.06em;
      text-transform: uppercase;
    }

    .panel-subtitle {
      margin-top: 4px;
      color: var(--muted);
      font-size: 11px;
      line-height: 1.35;
    }

    .panel-head .small-chip {
      padding: 8px 10px;
      color: var(--cyan);
      border-color: rgba(85, 232, 246, 0.23);
      background: rgba(26, 168, 194, 0.08);
    }

    .process-stage {
      position: relative;
      min-height: 0;
      overflow: hidden;
      border: 1px solid rgba(124, 177, 204, 0.22);
      border-radius: 15px;
      background: #0b131a;
      isolation: isolate;
    }

    .process-stage::before {
      content: "";
      position: absolute;
      inset: 0;
      z-index: 1;
      pointer-events: none;
      background: linear-gradient(180deg, rgba(255,255,255,0.025), transparent 22%, transparent 78%, rgba(0,0,0,0.15));
    }

    #processCanvas {
      display: block;
      width: 100%;
      height: 100%;
    }

    .stage-label {
      position: absolute;
      z-index: 2;
      pointer-events: none;
      color: rgba(232, 246, 252, 0.92);
      font-size: clamp(10px, 0.82vw, 13px);
      font-weight: 800;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      text-shadow: 0 2px 12px rgba(0,0,0,0.7);
    }

    .stage-label.top { top: 16px; left: 20px; }
    .stage-label.bottom { bottom: 16px; left: 20px; }

    .stage-label.top::before,
    .stage-label.bottom::before {
      content: "";
      display: inline-block;
      width: 9px;
      height: 9px;
      margin-right: 7px;
      border: 1px solid rgba(85, 232, 246, 0.6);
      border-radius: 50%;
      background: rgba(85, 232, 246, 0.3);
      vertical-align: 0;
      box-shadow: 0 0 12px rgba(85, 232, 246, 0.36);
    }

    .stage-title,
    .stage-flow,
    .stage-gap-readout {
      position: absolute;
      z-index: 2;
      pointer-events: none;
      color: var(--muted-2);
      font-size: 10px;
      font-weight: 780;
      letter-spacing: 0.13em;
      text-transform: uppercase;
    }

    .stage-title { top: 17px; right: 19px; }

    .stage-flow {
      top: 50%;
      left: 12%;
      transform: translateY(-50%);
      color: rgba(143, 192, 212, 0.75);
    }

    .stage-flow span {
      display: inline-block;
      margin-left: 7px;
      color: var(--cyan);
      font-size: 16px;
      vertical-align: -1px;
    }

    .stage-gap-readout {
      top: 50%;
      right: 8.4%;
      transform: translateY(-50%);
      color: var(--amber);
      text-align: right;
    }

    .stage-gap-readout strong {
      display: block;
      margin-top: 4px;
      color: var(--text);
      font-size: 12px;
      letter-spacing: 0.02em;
    }

    .process-footer {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      min-height: 28px;
      color: var(--muted);
      font-size: 10px;
    }

    .process-footer-left,
    .process-footer-right {
      display: flex;
      align-items: center;
      gap: 12px;
      min-width: 0;
    }

    .legend-item {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      white-space: nowrap;
    }

    .legend-swatch {
      width: 18px;
      height: 4px;
      border-radius: 99px;
      background: var(--cyan);
      box-shadow: 0 0 9px rgba(85,232,246,0.45);
    }

    .legend-swatch.defect { background: var(--amber); box-shadow: 0 0 9px rgba(255,191,99,0.4); }
    .legend-swatch.center { background: var(--orange); box-shadow: 0 0 9px rgba(255,132,93,0.4); }

    .dashboard-panel {
      padding: clamp(13px, 1.15vw, 19px);
      display: grid;
      grid-template-rows: auto auto auto minmax(205px, 1fr) auto;
      gap: 10px;
      overflow: auto;
      scrollbar-width: thin;
      scrollbar-color: rgba(146, 180, 199, 0.35) transparent;
    }

    .dashboard-panel::-webkit-scrollbar { width: 7px; }
    .dashboard-panel::-webkit-scrollbar-thumb { background: rgba(146, 180, 199, 0.25); border-radius: 10px; }

    .dashboard-head { min-height: 38px; }

    .scenario-module,
    .control-module,
    .profile-card {
      border: 1px solid var(--line);
      border-radius: var(--small-radius);
      background: linear-gradient(145deg, rgba(255,255,255,0.025), rgba(255,255,255,0.008));
    }

    .scenario-module { padding: 11px; }

    .scenario-tabs {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 7px;
      margin-top: 8px;
    }

    .scenario-tab {
      min-height: 45px;
      padding: 6px 8px;
      border: 1px solid rgba(147, 181, 201, 0.15);
      border-radius: 9px;
      background: rgba(15, 25, 34, 0.75);
      color: var(--muted);
      cursor: pointer;
      text-align: left;
      transition: 160ms ease;
    }

    .scenario-tab:hover { border-color: rgba(85, 232, 246, 0.38); color: var(--text); }

    .scenario-tab.active {
      border-color: rgba(85, 232, 246, 0.58);
      background: linear-gradient(145deg, rgba(23, 125, 143, 0.28), rgba(26, 168, 194, 0.06));
      color: var(--text);
      box-shadow: inset 0 0 20px rgba(85, 232, 246, 0.035), 0 0 16px rgba(26, 168, 194, 0.08);
    }

    .scenario-tab strong,
    .scenario-tab span { display: block; }
    .scenario-tab strong { font-size: 11px; font-weight: 800; }
    .scenario-tab span { margin-top: 2px; color: var(--muted-2); font-size: 9px; }
    .scenario-tab.active span { color: rgba(208, 245, 250, 0.68); }

    .scenario-description {
      min-height: 30px;
      margin-top: 8px;
      color: var(--muted);
      font-size: 10px;
      line-height: 1.35;
    }

    .metrics-grid {
      display: grid;
      grid-template-columns: 1.45fr 1fr 1fr;
      gap: 8px;
    }

    .metric-card {
      min-width: 0;
      min-height: 77px;
      padding: 10px;
      overflow: hidden;
      border: 1px solid var(--line);
      border-radius: var(--small-radius);
      background: rgba(12, 20, 28, 0.74);
    }

    .metric-card.status-card { border-color: rgba(255, 191, 99, 0.24); }
    .metric-value {
      margin-top: 8px;
      color: var(--text);
      font-size: clamp(13px, 1.05vw, 17px);
      font-weight: 800;
      letter-spacing: -0.02em;
      line-height: 1.08;
      white-space: nowrap;
    }

    .status-card .metric-value { color: var(--amber); font-size: clamp(11px, 0.86vw, 14px); }
    .status-card.met { border-color: rgba(114, 224, 162, 0.32); }
    .status-card.met .metric-value { color: var(--green); }

    .metric-detail {
      margin-top: 5px;
      overflow: hidden;
      color: var(--muted-2);
      font-size: 9px;
      text-overflow: ellipsis;
      white-space: nowrap;
    }

    .profile-card {
      min-height: 205px;
      padding: 10px 10px 8px;
      display: grid;
      grid-template-rows: auto minmax(0, 1fr) auto;
      overflow: hidden;
    }

    .profile-head {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 8px;
    }

    .profile-title {
      color: var(--text);
      font-size: 11px;
      font-weight: 820;
      letter-spacing: 0.08em;
      text-transform: uppercase;
    }

    .profile-subtitle {
      margin-top: 3px;
      color: var(--muted-2);
      font-size: 9px;
      line-height: 1.25;
    }

    .profile-condition {
      padding: 5px 7px;
      border: 1px solid rgba(255, 191, 99, 0.23);
      border-radius: 6px;
      color: var(--amber);
      background: rgba(255, 191, 99, 0.08);
      font-size: 8px;
      font-weight: 800;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      white-space: nowrap;
    }

    #rollProfileSvg {
      width: 100%;
      height: 100%;
      min-height: 145px;
      display: block;
      overflow: visible;
    }

    .profile-legend {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
      color: var(--muted-2);
      font-size: 9px;
    }

    .profile-legend .gap-key {
      display: inline-flex;
      align-items: center;
      gap: 5px;
      color: var(--cyan);
      font-weight: 750;
    }

    .gap-key i {
      width: 18px;
      height: 3px;
      border-radius: 99px;
      background: var(--cyan);
      box-shadow: 0 0 10px rgba(85,232,246,0.7);
    }

    .control-module { padding: 11px; }

    .control-head {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
    }

    .control-title {
      color: var(--text);
      font-size: 11px;
      font-weight: 800;
      letter-spacing: 0.07em;
      text-transform: uppercase;
    }

    .bend-readout {
      color: var(--cyan);
      font-size: 13px;
      font-variant-numeric: tabular-nums;
      font-weight: 850;
    }

    .range-wrap { margin-top: 10px; }

    input[type="range"] {
      width: 100%;
      height: 6px;
      appearance: none;
      border-radius: 99px;
      outline: none;
      background: linear-gradient(90deg, rgba(255,132,93,0.75), rgba(132,161,177,0.38) 50%, rgba(85,232,246,0.85));
      cursor: ew-resize;
    }

    input[type="range"]::-webkit-slider-thumb {
      width: 17px;
      height: 17px;
      appearance: none;
      border: 2px solid #d6fbff;
      border-radius: 50%;
      background: #1bc1d4;
      box-shadow: 0 0 0 4px rgba(85,232,246,0.12), 0 0 16px rgba(85,232,246,0.55);
    }

    input[type="range"]::-moz-range-thumb {
      width: 13px;
      height: 13px;
      border: 2px solid #d6fbff;
      border-radius: 50%;
      background: #1bc1d4;
      box-shadow: 0 0 0 4px rgba(85,232,246,0.12), 0 0 16px rgba(85,232,246,0.55);
    }

    .range-labels {
      display: flex;
      justify-content: space-between;
      margin-top: 5px;
      color: var(--muted-2);
      font-size: 8px;
      font-weight: 750;
      letter-spacing: 0.07em;
      text-transform: uppercase;
    }

    .action-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 7px;
      margin-top: 10px;
    }

    .action-btn,
    .reset-btn {
      min-height: 37px;
      border: 1px solid transparent;
      border-radius: 9px;
      cursor: pointer;
      font-size: 10px;
      font-weight: 850;
      letter-spacing: 0.04em;
      transition: transform 130ms ease, box-shadow 130ms ease, background 130ms ease, border-color 130ms ease;
    }

    .action-btn:active,
    .reset-btn:active { transform: translateY(1px) scale(0.99); }

    .action-btn.decrease {
      border-color: rgba(255, 132, 93, 0.36);
      background: linear-gradient(145deg, rgba(159, 62, 47, 0.53), rgba(91, 39, 37, 0.54));
      color: #ffd9c6;
    }

    .action-btn.decrease:hover { border-color: var(--orange); box-shadow: 0 0 18px rgba(255,132,93,0.16); }

    .action-btn.increase {
      border-color: rgba(85, 232, 246, 0.42);
      background: linear-gradient(145deg, rgba(21, 129, 149, 0.58), rgba(24, 74, 94, 0.57));
      color: #d6fbff;
    }

    .action-btn.increase:hover { border-color: var(--cyan); box-shadow: 0 0 18px rgba(85,232,246,0.16); }

    .reset-btn {
      grid-column: 1 / -1;
      border-color: rgba(157, 182, 204, 0.24);
      background: rgba(43, 55, 66, 0.68);
      color: var(--text);
    }

    .reset-btn:hover { border-color: rgba(237, 246, 252, 0.62); background: rgba(62, 76, 88, 0.8); }

    .control-note {
      margin-top: 8px;
      color: var(--muted-2);
      font-size: 9px;
      line-height: 1.3;
    }

    .bottom-bar {
      min-height: 24px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      color: var(--muted-2);
      font-size: 9px;
    }

    .bottom-bar strong { color: var(--muted); font-weight: 750; }

    .key-hint { letter-spacing: 0.04em; white-space: nowrap; }

    .svg-profile-bg { fill: url(#profileBg); stroke: rgba(157,182,204,0.16); stroke-width: 1; }
    .svg-grid-line { stroke: rgba(124,177,204,0.13); stroke-width: 1; }
    .svg-grid-line.major { stroke: rgba(124,177,204,0.22); }
    .svg-axis-text { fill: rgba(164,194,210,0.68); font-size: 9px; font-weight: 800; letter-spacing: 1px; }
    .svg-note-text { fill: rgba(159,188,205,0.5); font-size: 8px; font-weight: 700; letter-spacing: 0.7px; }
    .roll-body { stroke: rgba(207,234,244,0.44); stroke-width: 1.2; }
    .roll-cap { stroke: rgba(217,245,252,0.42); stroke-width: 1; }
    .roll-axis { fill: none; stroke: rgba(220,242,249,0.28); stroke-width: 1.2; stroke-dasharray: 5 5; }
    .roll-shine { fill: none; stroke: rgba(247,253,255,0.24); stroke-width: 2.2; stroke-linecap: round; }
    .gap-band { fill: url(#gapBand); opacity: 0.6; filter: url(#gapGlow); }
    .gap-line { fill: none; stroke: var(--cyan); stroke-width: 2.4; stroke-linecap: round; stroke-linejoin: round; filter: url(#gapGlow); }
    .gap-line.secondary { opacity: 0.74; stroke-width: 1.2; }
    .gap-core { fill: none; stroke: #e7feff; stroke-width: 1.1; stroke-dasharray: 2 4; opacity: 0.85; }
    .gap-measure { stroke: rgba(114,224,162,0.9); stroke-width: 1.1; }
    .svg-defect-note { fill: var(--amber); font-size: 9px; font-weight: 850; letter-spacing: 0.9px; }

    @media (max-width: 1160px) {
      .main-grid { grid-template-columns: minmax(0, 1.68fr) minmax(330px, 1fr); }
      .metrics-grid { grid-template-columns: 1.25fr 1fr 1fr; }
      .metric-value { font-size: 12px; }
    }

    @media (max-height: 700px) {
      .app-shell { padding: 11px 15px; gap: 9px; }
      .topbar { min-height: 48px; }
      .brand-mark { width: 37px; height: 37px; border-radius: 11px; }
      .panel-head { min-height: 33px; }
      .process-panel, .dashboard-panel { padding: 12px; gap: 8px; }
      .profile-card { min-height: 180px; }
      #rollProfileSvg { min-height: 124px; }
      .scenario-module, .control-module { padding: 9px; }
      .scenario-tab { min-height: 39px; }
      .metric-card { min-height: 68px; padding: 8px; }
      .metric-value { margin-top: 5px; }
      .action-btn, .reset-btn { min-height: 32px; }
    }

    @media (max-width: 950px) {
      html, body { overflow: auto; }
      .app-shell { width: 100%; min-width: 0; height: auto; min-height: 100vh; }
      .main-grid { grid-template-columns: 1fr; grid-template-rows: minmax(520px, 1fr) auto; }
      .dashboard-panel { overflow: visible; }
      .process-stage { min-height: 430px; }
    }
  </style>
</head>
<body>
  <main class="app-shell">
    <header class="topbar">
      <div class="brand-lockup">
        <div class="brand-mark" aria-hidden="true">WRB</div>
        <div>
          <div class="eyebrow">Flat rolling · technological control loop</div>
          <h1>Work Roll Bending / Flatness Control</h1>
        </div>
      </div>
      <div class="topbar-tools">
        <div class="live-chip"><span class="live-dot"></span> Live model</div>
        <div class="mode-chip" id="modeChip">Scenario A · Wavy edges</div>
        <button class="fullscreen-btn" id="fullscreenBtn" type="button" title="Enter full-screen presentation mode">⛶ Fullscreen</button>
      </div>
    </header>

    <section class="main-grid">
      <section class="panel process-panel" aria-labelledby="processTitle">
        <div class="panel-head">
          <div>
            <div class="panel-title" id="processTitle">Top-down rolling view</div>
            <div class="panel-subtitle">Strip flow, roll-gap correction zone and live flatness signature</div>
          </div>
          <div class="small-chip">Input → output</div>
        </div>

        <div class="process-stage" id="processStage">
          <canvas id="processCanvas" aria-label="Animated top-down view of a strip passing through the work roll gap"></canvas>
          <div class="stage-label top">Drive Side (DS)</div>
          <div class="stage-label bottom">Operator Side (OS)</div>
          <div class="stage-title">Top-down strip path</div>
          <div class="stage-flow">Strip flow <span>→</span></div>
          <div class="stage-gap-readout">Work roll gap<strong id="gapMoment">Level profile</strong></div>
        </div>

        <div class="process-footer">
          <div class="process-footer-left">
            <span class="legend-item"><i class="legend-swatch"></i> Flat strip target</span>
            <span class="legend-item"><i class="legend-swatch defect"></i> Edge wave</span>
            <span class="legend-item"><i class="legend-swatch center"></i> Center buckle</span>
          </div>
          <div class="process-footer-right"><span class="footer-label">Model speed</span><strong id="speedReadout">0.90 m/s</strong></div>
        </div>
      </section>

      <aside class="panel dashboard-panel" aria-labelledby="dashboardTitle">
        <div class="panel-head dashboard-head">
          <div>
            <div class="panel-title" id="dashboardTitle">Control dashboard</div>
            <div class="panel-subtitle">Operator command → roll deflection → strip shape</div>
          </div>
        </div>

        <section class="scenario-module" aria-labelledby="scenarioHeading">
          <div class="section-kicker" id="scenarioHeading">Starting operational condition</div>
          <div class="scenario-tabs" role="tablist" aria-label="Flatness scenarios">
            <button class="scenario-tab active" data-scenario="edges" type="button" role="tab" aria-selected="true">
              <strong>Scenario A</strong><span>Wavy edges · low bending</span>
            </button>
            <button class="scenario-tab" data-scenario="center" type="button" role="tab" aria-selected="false">
              <strong>Scenario B</strong><span>Center buckles · high bending</span>
            </button>
          </div>
          <p class="scenario-description" id="scenarioDescription">Low bending leaves the roll ends converging and produces moving waves at DS and OS. Increase bending to recover the flat target.</p>
        </section>

        <section class="metrics-grid" aria-label="Live engineering metrics">
          <div class="metric-card status-card" id="statusCard">
            <div class="metric-label">Shape status</div>
            <div class="metric-value" id="statusText">Shape Error: Out of Tolerance</div>
            <div class="metric-detail" id="statusDetail">Edge wave amplitude is high</div>
          </div>
          <div class="metric-card">
            <div class="metric-label">Total roll bending force</div>
            <div class="metric-value" id="forceText">800 kN</div>
            <div class="metric-detail" id="forceDetail">Low-force condition</div>
          </div>
          <div class="metric-card">
            <div class="metric-label">Mechanical crown deviation</div>
            <div class="metric-value" id="crownText">−840 μm</div>
            <div class="metric-detail">From level roll profile</div>
          </div>
        </section>

        <section class="profile-card" aria-labelledby="profileTitle">
          <div class="profile-head">
            <div>
              <div class="profile-title" id="profileTitle">3D work roll gap profile</div>
              <div class="profile-subtitle">Exaggerated transverse deflection · DS ↔ OS</div>
            </div>
            <div class="profile-condition" id="profileCondition">Under-bent</div>
          </div>

          <svg id="rollProfileSvg" viewBox="0 0 520 320" role="img" aria-label="Dynamic isometric graphic of upper and lower work rolls and their gap">
            <defs>
              <linearGradient id="profileBg" x1="0" y1="0" x2="0" y2="1">
                <stop offset="0" stop-color="#0d1821" />
                <stop offset="1" stop-color="#0a1118" />
              </linearGradient>
              <linearGradient id="upperRollGradient" x1="0" y1="0" x2="0" y2="1">
                <stop offset="0" stop-color="#7794a4" />
                <stop offset="0.2" stop-color="#496574" />
                <stop offset="0.52" stop-color="#263d4b" />
                <stop offset="0.8" stop-color="#152a37" />
                <stop offset="1" stop-color="#0e202c" />
              </linearGradient>
              <linearGradient id="lowerRollGradient" x1="0" y1="0" x2="0" y2="1">
                <stop offset="0" stop-color="#537382" />
                <stop offset="0.28" stop-color="#304e5d" />
                <stop offset="0.57" stop-color="#1a3340" />
                <stop offset="0.86" stop-color="#112632" />
                <stop offset="1" stop-color="#0b1b26" />
              </linearGradient>
              <linearGradient id="upperCapGradient" x1="0" y1="0" x2="1" y2="0">
                <stop offset="0" stop-color="#9fb6c1" stop-opacity="0.7" />
                <stop offset="0.45" stop-color="#42606f" stop-opacity="0.75" />
                <stop offset="1" stop-color="#102431" stop-opacity="0.95" />
              </linearGradient>
              <linearGradient id="lowerCapGradient" x1="0" y1="0" x2="1" y2="0">
                <stop offset="0" stop-color="#7e9daa" stop-opacity="0.65" />
                <stop offset="0.48" stop-color="#355363" stop-opacity="0.8" />
                <stop offset="1" stop-color="#0e202b" stop-opacity="0.95" />
              </linearGradient>
              <linearGradient id="gapBand" x1="0" y1="0" x2="0" y2="1">
                <stop offset="0" stop-color="#55e8f6" stop-opacity="0.04" />
                <stop offset="0.5" stop-color="#55e8f6" stop-opacity="0.85" />
                <stop offset="1" stop-color="#55e8f6" stop-opacity="0.04" />
              </linearGradient>
              <filter id="gapGlow" x="-50%" y="-50%" width="200%" height="200%">
                <feGaussianBlur stdDeviation="3.2" result="blur" />
                <feMerge><feMergeNode in="blur" /><feMergeNode in="SourceGraphic" /></feMerge>
              </filter>
              <filter id="softGlow" x="-30%" y="-30%" width="160%" height="160%">
                <feGaussianBlur stdDeviation="7" />
              </filter>
            </defs>

            <rect class="svg-profile-bg" x="0.5" y="0.5" width="519" height="319" rx="14" />
            <g id="profileGrid" aria-hidden="true"></g>
            <text class="svg-axis-text" x="58" y="30">DRIVE SIDE</text>
            <text class="svg-axis-text" x="402" y="30">OPERATOR SIDE</text>
            <text class="svg-note-text" x="18" y="288">ROLL PROFILE · EXAGGERATED SCALE</text>

            <g id="gapGroup">
              <path id="gapBandPath" class="gap-band"></path>
              <path id="gapTopPath" class="gap-line secondary"></path>
              <path id="gapBottomPath" class="gap-line secondary"></path>
              <path id="gapCorePath" class="gap-core"></path>
              <line id="gapMeasure" class="gap-measure" x1="260" x2="260" y1="0" y2="0"></line>
            </g>

            <g id="upperRollGroup">
              <path id="upperRollBody" class="roll-body" fill="url(#upperRollGradient)"></path>
              <ellipse id="upperLeftCap" class="roll-cap" fill="url(#upperCapGradient)"></ellipse>
              <ellipse id="upperRightCap" class="roll-cap" fill="url(#upperCapGradient)"></ellipse>
              <path id="upperAxis" class="roll-axis"></path>
              <path id="upperShine" class="roll-shine"></path>
            </g>
            <g id="lowerRollGroup">
              <path id="lowerRollBody" class="roll-body" fill="url(#lowerRollGradient)"></path>
              <ellipse id="lowerLeftCap" class="roll-cap" fill="url(#lowerCapGradient)"></ellipse>
              <ellipse id="lowerRightCap" class="roll-cap" fill="url(#lowerCapGradient)"></ellipse>
              <path id="lowerAxis" class="roll-axis"></path>
              <path id="lowerShine" class="roll-shine"></path>
            </g>

            <text id="profileShapeText" class="svg-defect-note" x="258" y="55" text-anchor="middle">EDGE CONVERGENCE</text>
            <text id="profileGapText" class="svg-note-text" x="258" y="273" text-anchor="middle">MICRO-GAP: 27–58 px</text>
          </svg>

          <div class="profile-legend">
            <span class="gap-key"><i></i> Micro-gap varies with bending</span>
            <span id="profileRangeText">Edge gap 27 · centre gap 38</span>
          </div>
        </section>

        <section class="control-module" aria-labelledby="controlTitle">
          <div class="control-head">
            <div class="control-title" id="controlTitle">Work roll bending command</div>
            <div class="bend-readout" id="bendReadout">−70%</div>
          </div>
          <div class="range-wrap">
            <input id="bendSlider" type="range" min="-100" max="100" step="1" value="-70" aria-label="Manual work roll bending command" />
            <div class="range-labels"><span>Natural / low</span><span>Level</span><span>Over-bent / high</span></div>
          </div>
          <div class="action-grid">
            <button class="action-btn decrease" id="decreaseBtn" type="button" title="Reduce the work roll bending force">− Decrease Bending (-)</button>
            <button class="action-btn increase" id="increaseBtn" type="button" title="Increase the work roll bending force">＋ Increase Bending (+)</button>
            <button class="reset-btn" id="resetBtn" type="button" title="Return to a level roll profile">↺ Reset / Level</button>
          </div>
          <div class="control-note">Each button click changes the command by 10% of the operating range. Use the slider for a continuous what-if response.</div>
        </section>
      </aside>
    </section>

    <footer class="bottom-bar">
      <div><strong>Teaching model:</strong> positive bending opens the centre gap; low bending leaves edge convergence and wavy edges.</div>
      <div class="key-hint">Keyboard: ← / → bend · Space level</div>
    </footer>
  </main>

  <script>
    (() => {
      "use strict";

      const $ = (selector) => document.querySelector(selector);
      const canvas = $("#processCanvas");
      const ctx = canvas.getContext("2d");
      const svgNs = "http://www.w3.org/2000/svg";

      const ui = {
        modeChip: $("#modeChip"),
        scenarioDescription: $("#scenarioDescription"),
        statusCard: $("#statusCard"),
        statusText: $("#statusText"),
        statusDetail: $("#statusDetail"),
        forceText: $("#forceText"),
        forceDetail: $("#forceDetail"),
        crownText: $("#crownText"),
        bendReadout: $("#bendReadout"),
        bendSlider: $("#bendSlider"),
        gapMoment: $("#gapMoment"),
        profileCondition: $("#profileCondition"),
        profileShapeText: $("#profileShapeText"),
        profileGapText: $("#profileGapText"),
        profileRangeText: $("#profileRangeText"),
        speedReadout: $("#speedReadout")
      };

      const profile = {
        x0: 68,
        x1: 452,
        upperBase: 103,
        lowerBase: 217,
        radius: 28,
        samples: 51
      };

      const scenarios = {
        edges: {
          start: -70,
          mode: "Scenario A · Wavy edges",
          description: "Low bending leaves the roll ends converging and produces moving waves at DS and OS. Increase bending to recover the flat target."
        },
        center: {
          start: 70,
          mode: "Scenario B · Center buckles",
          description: "High bending opens the roll gap at the centre and drives a longitudinal buckle. Decrease bending to tighten the crown and flatten the strip."
        }
      };

      const state = {
        scenario: "edges",
        targetBend: scenarios.edges.start,
        currentBend: scenarios.edges.start,
        simTime: 0,
        lastFrame: performance.now(),
        lastUiUpdate: 0,
        dpr: Math.min(window.devicePixelRatio || 1, 2),
        canvasWidth: 0,
        canvasHeight: 0
      };

      function clamp(value, min, max) {
        return Math.max(min, Math.min(max, value));
      }

      function lerp(a, b, amount) {
        return a + (b - a) * amount;
      }

      function smoothstep(edge0, edge1, value) {
        const t = clamp((value - edge0) / (edge1 - edge0), 0, 1);
        return t * t * (3 - 2 * t);
      }

      function formatSigned(value, suffix = "") {
        const rounded = Math.round(value);
        if (rounded === 0) return `0${suffix}`;
        return `${rounded > 0 ? "+" : "−"}${Math.abs(rounded)}${suffix}`;
      }

      function formatNumber(value) {
        return Math.round(value).toLocaleString("en-US").replace(/,/g, " ");
      }

      function setTargetBend(value) {
        state.targetBend = clamp(Math.round(value), -100, 100);
        ui.bendSlider.value = String(state.targetBend);
      }

      function selectScenario(name) {
        if (!scenarios[name]) return;
        state.scenario = name;
        setTargetBend(scenarios[name].start);
        ui.modeChip.textContent = scenarios[name].mode;
        ui.scenarioDescription.textContent = scenarios[name].description;
        document.querySelectorAll(".scenario-tab").forEach((button) => {
          const active = button.dataset.scenario === name;
          button.classList.toggle("active", active);
          button.setAttribute("aria-selected", String(active));
        });
      }

      function defectAmplitudes(bend) {
        const under = clamp(-bend / 100, 0, 1);
        const over = clamp(bend / 100, 0, 1);
        return {
          edge: 33 * Math.pow(under, 0.86),
          center: 38 * Math.pow(over, 0.86)
        };
      }

      function rollProfile(bend) {
        const points = [];
        const upperTop = [];
        const upperBottom = [];
        const lowerTop = [];
        const lowerBottom = [];
        const gapCore = [];
        const bendRatio = bend / 100;
        const centerBow = bendRatio * 14;
        const edgeConvergence = bend < 0 ? (-bend / 100) * 42 : 0;
        const r = profile.radius;

        for (let i = 0; i < profile.samples; i += 1) {
          const u = (i / (profile.samples - 1)) * 2 - 1;
          const x = profile.x0 + ((i / (profile.samples - 1)) * (profile.x1 - profile.x0));
          const centerDeflection = centerBow * (1 - u * u);
          const edgePull = edgeConvergence * u * u;
          const upperCenter = profile.upperBase - centerDeflection + edgePull * 0.52;
          const lowerCenter = profile.lowerBase + centerDeflection - edgePull * 0.52;
          const upTop = upperCenter - r;
          const upBottom = upperCenter + r;
          const lowTop = lowerCenter - r;
          const lowBottom = lowerCenter + r;

          points.push({x, upperCenter, lowerCenter, upTop, upBottom, lowTop, lowBottom, gap: lowTop - upBottom});
          upperTop.push({x, y: upTop});
          upperBottom.push({x, y: upBottom});
          lowerTop.push({x, y: lowTop});
          lowerBottom.push({x, y: lowBottom});
          gapCore.push({x, y: (upBottom + lowTop) / 2});
        }

        const gaps = points.map((point) => point.gap);
        return {
          points,
          upperTop,
          upperBottom,
          lowerTop,
          lowerBottom,
          gapCore,
          minGap: Math.min(...gaps),
          maxGap: Math.max(...gaps),
          edgeGap: gaps[0],
          centerGap: gaps[Math.floor(gaps.length / 2)]
        };
      }

      function pathFrom(points) {
        return points.map((point, index) => `${index === 0 ? "M" : "L"}${point.x.toFixed(1)},${point.y.toFixed(1)}`).join(" ");
      }

      function closedBand(topPoints, bottomPoints) {
        const top = pathFrom(topPoints);
        const bottom = pathFrom([...bottomPoints].reverse());
        return `${top} ${bottom} Z`;
      }

      function buildGrid() {
        const grid = $("#profileGrid");
        grid.innerHTML = "";
        for (let i = 0; i <= 8; i += 1) {
          const x = profile.x0 + (i / 8) * (profile.x1 - profile.x0);
          const line = document.createElementNS(svgNs, "line");
          line.setAttribute("x1", x);
          line.setAttribute("x2", x);
          line.setAttribute("y1", 45);
          line.setAttribute("y2", 267);
          line.setAttribute("class", i === 0 || i === 4 || i === 8 ? "svg-grid-line major" : "svg-grid-line");
          grid.appendChild(line);
        }
        for (let i = 0; i <= 5; i += 1) {
          const y = 52 + (i / 5) * 205;
          const line = document.createElementNS(svgNs, "line");
          line.setAttribute("x1", 36);
          line.setAttribute("x2", 484);
          line.setAttribute("y1", y);
          line.setAttribute("y2", y);
          line.setAttribute("class", i === 0 || i === 5 ? "svg-grid-line major" : "svg-grid-line");
          grid.appendChild(line);
        }
      }

      function updateRollProfile(bend) {
        const data = rollProfile(bend);
        const p = data.points;

        $("#upperRollBody").setAttribute("d", closedBand(data.upperTop, data.upperBottom));
        $("#lowerRollBody").setAttribute("d", closedBand(data.lowerTop, data.lowerBottom));
        $("#upperAxis").setAttribute("d", pathFrom(p.map((point) => ({x: point.x, y: point.upperCenter}))));
        $("#lowerAxis").setAttribute("d", pathFrom(p.map((point) => ({x: point.x, y: point.lowerCenter}))));
        $("#upperShine").setAttribute("d", pathFrom(p.map((point) => ({x: point.x, y: point.upperCenter - 9}))));
        $("#lowerShine").setAttribute("d", pathFrom(p.map((point) => ({x: point.x, y: point.lowerCenter - 8}))));
        $("#gapBandPath").setAttribute("d", closedBand(data.upperBottom, data.lowerTop));
        $("#gapTopPath").setAttribute("d", pathFrom(data.upperBottom));
        $("#gapBottomPath").setAttribute("d", pathFrom(data.lowerTop));
        $("#gapCorePath").setAttribute("d", pathFrom(data.gapCore));

        [
          ["#upperLeftCap", p[0].x, p[0].upperCenter],
          ["#upperRightCap", p[p.length - 1].x, p[p.length - 1].upperCenter],
          ["#lowerLeftCap", p[0].x, p[0].lowerCenter],
          ["#lowerRightCap", p[p.length - 1].x, p[p.length - 1].lowerCenter]
        ].forEach(([selector, cx, cy]) => {
          const ellipse = $(selector);
          ellipse.setAttribute("cx", cx);
          ellipse.setAttribute("cy", cy);
          ellipse.setAttribute("rx", 16);
          ellipse.setAttribute("ry", profile.radius);
        });

        const mid = p[Math.floor(p.length / 2)];
        const measure = $("#gapMeasure");
        measure.setAttribute("x1", mid.x);
        measure.setAttribute("x2", mid.x);
        measure.setAttribute("y1", mid.upBottom + 3);
        measure.setAttribute("y2", mid.lowTop - 3);

        let shapeText = "LEVEL PROFILE";
        let condition = "Level";
        let moment = "Level profile";
        if (bend < -4) {
          shapeText = "EDGE CONVERGENCE";
          condition = "Under-bent";
          moment = "Edges close first";
        } else if (bend > 4) {
          shapeText = "CENTRE OPENING";
          condition = "Over-bent";
          moment = "Centre opens first";
        }
        ui.profileShapeText.textContent = shapeText;
        ui.profileCondition.textContent = condition;
        ui.gapMoment.textContent = moment;
        ui.profileGapText.textContent = `MICRO-GAP: ${Math.round(data.minGap)}–${Math.round(data.maxGap)} px`;
        ui.profileRangeText.textContent = `Edge gap ${Math.round(data.edgeGap)} · centre gap ${Math.round(data.centerGap)}`;
      }

      function updateTelemetry(bend) {
        const amplitudes = defectAmplitudes(bend);
        const error = Math.max(amplitudes.edge, amplitudes.center);
        const met = Math.abs(bend) <= 4;
        const force = clamp(1500 + bend * 10, 300, 2700);
        const crown = bend * 12;

        ui.statusCard.classList.toggle("met", met);
        ui.statusText.textContent = met ? "Target Shape Met (Flat Strip)" : "Shape Error: Out of Tolerance";
        if (met) {
          ui.statusDetail.textContent = "Edge and centre flatness within tolerance";
        } else if (amplitudes.edge > amplitudes.center) {
          ui.statusDetail.textContent = `Wavy edges · ${Math.round(amplitudes.edge)} px signature`;
        } else {
          ui.statusDetail.textContent = `Centre buckle · ${Math.round(amplitudes.center)} px signature`;
        }

        ui.forceText.textContent = `${formatNumber(force)} kN`;
        ui.forceDetail.textContent = bend < -4 ? "Low-force / under-bent" : bend > 4 ? "High-force / over-bent" : "Nominal level force";
        ui.crownText.textContent = formatSigned(crown, " μm");
        ui.bendReadout.textContent = formatSigned(bend, "%");
        ui.bendSlider.setAttribute("aria-valuetext", `${Math.round(bend)} percent bending command`);

        const speed = 0.9 + Math.abs(bend) * 0.001;
        ui.speedReadout.textContent = `${speed.toFixed(2)} m/s`;
      }

      function drawRoundedRect(context, x, y, width, height, radius) {
        const r = Math.min(radius, width / 2, height / 2);
        context.beginPath();
        context.moveTo(x + r, y);
        context.arcTo(x + width, y, x + width, y + height, r);
        context.arcTo(x + width, y + height, x, y + height, r);
        context.arcTo(x, y + height, x, y, r);
        context.arcTo(x, y, x + width, y, r);
        context.closePath();
      }

      function drawArrow(context, x1, y1, x2, y2, color, alpha = 0.7) {
        const angle = Math.atan2(y2 - y1, x2 - x1);
        const head = 8;
        context.save();
        context.globalAlpha = alpha;
        context.strokeStyle = color;
        context.fillStyle = color;
        context.lineWidth = 1.5;
        context.beginPath();
        context.moveTo(x1, y1);
        context.lineTo(x2, y2);
        context.stroke();
        context.beginPath();
        context.moveTo(x2, y2);
        context.lineTo(x2 - head * Math.cos(angle - Math.PI / 6), y2 - head * Math.sin(angle - Math.PI / 6));
        context.lineTo(x2 - head * Math.cos(angle + Math.PI / 6), y2 - head * Math.sin(angle + Math.PI / 6));
        context.closePath();
        context.fill();
        context.restore();
      }

      function drawProcess() {
        const width = state.canvasWidth;
        const height = state.canvasHeight;
        if (!width || !height) return;

        const bend = state.currentBend;
        const amplitudes = defectAmplitudes(bend);
        const edgeAmp = amplitudes.edge;
        const centerAmp = amplitudes.center;
        const centerY = height * 0.54;
        const halfWidth = Math.min(height * 0.16, 74);
        const gapX = width * 0.61;
        const startX = 14;
        const endX = width - 15;
        const exitLength = Math.max(1, endX - gapX);
        const phaseSpeed = 3.25;

        ctx.save();
        ctx.setTransform(state.dpr, 0, 0, state.dpr, 0, 0);
        ctx.clearRect(0, 0, width, height);

        const background = ctx.createLinearGradient(0, 0, 0, height);
        background.addColorStop(0, "#0c171f");
        background.addColorStop(0.52, "#09121a");
        background.addColorStop(1, "#0c161d");
        ctx.fillStyle = background;
        ctx.fillRect(0, 0, width, height);

        ctx.save();
        ctx.strokeStyle = "rgba(125, 175, 199, 0.075)";
        ctx.lineWidth = 1;
        const gridSize = Math.max(36, width / 18);
        for (let x = 0; x < width; x += gridSize) {
          ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, height); ctx.stroke();
        }
        for (let y = 0; y < height; y += gridSize) {
          ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(width, y); ctx.stroke();
        }
        ctx.restore();

        function stripValues(x) {
          if (x < gapX) {
            return {top: centerY - halfWidth, bottom: centerY + halfWidth, center: centerY, wave: 0};
          }
          const travel = x - gapX;
          const envelope = smoothstep(0, Math.min(130, exitLength * 0.38), travel);
          const phase = travel * 0.075 - state.simTime * phaseSpeed;
          const wave = 0.72 * Math.sin(phase) + 0.2 * Math.sin(phase * 1.83 + 1.1) + 0.08 * Math.sin(phase * 3.15 - 0.6);
          if (edgeAmp > centerAmp) {
            const edgeWave = edgeAmp * envelope * wave;
            return {top: centerY - halfWidth + edgeWave, bottom: centerY + halfWidth - edgeWave, center: centerY, wave};
          }
          const centerWave = centerAmp * envelope * wave;
          return {top: centerY - halfWidth, bottom: centerY + halfWidth, center: centerY + centerWave, wave};
        }

        const samples = Math.max(100, Math.ceil(width / 4));
        const upperBoundary = [];
        const lowerBoundary = [];
        const centerLine = [];
        for (let i = 0; i <= samples; i += 1) {
          const x = startX + (i / samples) * (endX - startX);
          const values = stripValues(x);
          upperBoundary.push({x, y: values.top});
          lowerBoundary.push({x, y: values.bottom});
          centerLine.push({x, y: values.center});
        }

        const stripPath = new Path2D();
        stripPath.moveTo(upperBoundary[0].x, upperBoundary[0].y);
        upperBoundary.slice(1).forEach((point) => stripPath.lineTo(point.x, point.y));
        [...lowerBoundary].reverse().forEach((point) => stripPath.lineTo(point.x, point.y));
        stripPath.closePath();

        ctx.save();
        ctx.shadowColor = "rgba(0,0,0,0.42)";
        ctx.shadowBlur = 18;
        ctx.shadowOffsetY = 8;
        const stripGradient = ctx.createLinearGradient(0, centerY - halfWidth, 0, centerY + halfWidth);
        stripGradient.addColorStop(0, "#9eb3bf");
        stripGradient.addColorStop(0.18, "#657d8b");
        stripGradient.addColorStop(0.48, "#3f5967");
        stripGradient.addColorStop(0.79, "#5f7785");
        stripGradient.addColorStop(1, "#233b49");
        ctx.fillStyle = stripGradient;
        ctx.fill(stripPath);
        ctx.restore();

        ctx.save();
        ctx.clip(stripPath);
        const sheen = ctx.createLinearGradient(0, 0, width, 0);
        sheen.addColorStop(0, "rgba(255,255,255,0.02)");
        sheen.addColorStop(0.48, "rgba(213,249,255,0.08)");
        sheen.addColorStop(0.7, "rgba(255,255,255,0.02)");
        sheen.addColorStop(1, "rgba(255,255,255,0.08)");
        ctx.fillStyle = sheen;
        ctx.fillRect(0, centerY - halfWidth - 4, width, halfWidth * 2 + 8);
        ctx.globalAlpha = 0.32;
        ctx.strokeStyle = "#d9f8ff";
        ctx.lineWidth = 1;
        for (let yFactor of [0.22, 0.78]) {
          ctx.beginPath();
          for (let i = 0; i <= samples; i += 1) {
            const point = upperBoundary[i];
            const bottom = lowerBoundary[i];
            const y = point.y + (bottom.y - point.y) * yFactor;
            if (i === 0) ctx.moveTo(point.x, y); else ctx.lineTo(point.x, y);
          }
          ctx.stroke();
        }
        ctx.restore();

        function drawLine(points, color, widthValue, alpha = 1, dash = []) {
          ctx.save();
          ctx.globalAlpha = alpha;
          ctx.strokeStyle = color;
          ctx.lineWidth = widthValue;
          ctx.lineCap = "round";
          ctx.lineJoin = "round";
          ctx.setLineDash(dash);
          ctx.beginPath();
          points.forEach((point, index) => index === 0 ? ctx.moveTo(point.x, point.y) : ctx.lineTo(point.x, point.y));
          ctx.stroke();
          ctx.restore();
        }

        drawLine(upperBoundary, edgeAmp > 0 ? "#ffbf63" : "#8dc5d2", edgeAmp > 0 ? 5 : 1.4, edgeAmp > 0 ? 0.19 : 0.66);
        drawLine(lowerBoundary, edgeAmp > 0 ? "#ffbf63" : "#8dc5d2", edgeAmp > 0 ? 5 : 1.4, edgeAmp > 0 ? 0.19 : 0.66);
        drawLine(upperBoundary, edgeAmp > 0 ? "#ffd18a" : "#c8e9f0", 1.2, 0.92);
        drawLine(lowerBoundary, edgeAmp > 0 ? "#ffd18a" : "#c8e9f0", 1.2, 0.92);

        if (centerAmp > 0) {
          drawLine(centerLine, "#ff845d", 9, 0.2);
          drawLine(centerLine, "#ffb18f", 2.2, 0.95);
        }
        drawLine(centerLine, centerAmp > 0 ? "#ffd2b6" : "#76ddea", 1.2, centerAmp > 0 ? 0.9 : 0.72, [8, 8]);

        // Mill housing and the roll-gap/contact line.
        const housingTop = centerY - halfWidth - 58;
        const housingBottom = centerY + halfWidth + 58;
        ctx.save();
        ctx.fillStyle = "rgba(22, 40, 51, 0.72)";
        ctx.strokeStyle = "rgba(122, 173, 195, 0.34)";
        ctx.lineWidth = 1;
        drawRoundedRect(ctx, gapX - 31, housingTop, 62, housingBottom - housingTop, 11);
        ctx.fill();
        ctx.stroke();
        ctx.fillStyle = "rgba(123, 166, 184, 0.26)";
        ctx.fillRect(gapX - 28, housingTop + 13, 9, housingBottom - housingTop - 26);
        ctx.fillRect(gapX + 19, housingTop + 13, 9, housingBottom - housingTop - 26);
        ctx.restore();

        ctx.save();
        ctx.setLineDash([6, 5]);
        ctx.strokeStyle = "rgba(85, 232, 246, 0.95)";
        ctx.shadowColor = "rgba(85,232,246,0.7)";
        ctx.shadowBlur = 12;
        ctx.lineWidth = 2;
        ctx.beginPath(); ctx.moveTo(gapX, housingTop + 3); ctx.lineTo(gapX, housingBottom - 3); ctx.stroke();
        ctx.restore();

        ctx.save();
        ctx.fillStyle = "rgba(205, 237, 244, 0.72)";
        ctx.font = "700 10px Inter, system-ui, sans-serif";
        ctx.letterSpacing = "1px";
        ctx.textAlign = "center";
        ctx.fillText("ROLL GAP", gapX, housingTop - 10);
        ctx.fillStyle = "rgba(120, 166, 184, 0.62)";
        ctx.font = "700 9px Inter, system-ui, sans-serif";
        ctx.fillText("CORRECTION ZONE", gapX, housingBottom + 19);
        ctx.restore();

        drawArrow(ctx, 58, centerY + halfWidth + 34, gapX - 56, centerY + halfWidth + 34, "#7fbacb", 0.58);
        drawArrow(ctx, gapX + 54, centerY + halfWidth + 34, width - 58, centerY + halfWidth + 34, "#55e8f6", 0.58);

        // Defect callouts are deliberately restrained so the shape remains the focus.
        const calloutX = Math.min(width - 155, gapX + exitLength * 0.35);
        if (edgeAmp > centerAmp && edgeAmp > 2) {
          ctx.save();
          ctx.fillStyle = "rgba(255,191,99,0.95)";
          ctx.font = "800 10px Inter, system-ui, sans-serif";
          ctx.fillText("WAVY EDGES", calloutX, centerY - halfWidth - edgeAmp - 10);
          ctx.strokeStyle = "rgba(255,191,99,0.6)";
          ctx.lineWidth = 1;
          ctx.beginPath(); ctx.moveTo(calloutX + 3, centerY - halfWidth - edgeAmp - 5); ctx.lineTo(calloutX - 14, centerY - halfWidth - 1); ctx.stroke();
          ctx.restore();
        } else if (centerAmp > 2) {
          ctx.save();
          ctx.fillStyle = "rgba(255,132,93,0.98)";
          ctx.font = "800 10px Inter, system-ui, sans-serif";
          ctx.fillText("CENTER BUCKLE", calloutX, centerY - centerAmp - 10);
          ctx.strokeStyle = "rgba(255,132,93,0.66)";
          ctx.lineWidth = 1;
          ctx.beginPath(); ctx.moveTo(calloutX + 3, centerY - centerAmp - 5); ctx.lineTo(calloutX - 14, centerY - 2); ctx.stroke();
          ctx.restore();
        }

        ctx.restore();
      }

      function resizeCanvas() {
        const rect = canvas.getBoundingClientRect();
        state.dpr = Math.min(window.devicePixelRatio || 1, 2);
        state.canvasWidth = Math.max(1, rect.width);
        state.canvasHeight = Math.max(1, rect.height);
        canvas.width = Math.floor(state.canvasWidth * state.dpr);
        canvas.height = Math.floor(state.canvasHeight * state.dpr);
        drawProcess();
      }

      function animationFrame(now) {
        const delta = Math.min(0.05, Math.max(0, (now - state.lastFrame) / 1000));
        state.lastFrame = now;
        state.simTime += delta;
        state.currentBend = lerp(state.currentBend, state.targetBend, 1 - Math.pow(0.0004, delta));
        if (Math.abs(state.currentBend - state.targetBend) < 0.02) state.currentBend = state.targetBend;

        drawProcess();
        updateRollProfile(state.currentBend);
        if (now - state.lastUiUpdate > 65) {
          updateTelemetry(state.currentBend);
          state.lastUiUpdate = now;
        }
        requestAnimationFrame(animationFrame);
      }

      document.querySelectorAll(".scenario-tab").forEach((button) => {
        button.addEventListener("click", () => selectScenario(button.dataset.scenario));
      });

      $("#increaseBtn").addEventListener("click", () => setTargetBend(state.targetBend + 10));
      $("#decreaseBtn").addEventListener("click", () => setTargetBend(state.targetBend - 10));
      $("#resetBtn").addEventListener("click", () => setTargetBend(0));
      ui.bendSlider.addEventListener("input", (event) => setTargetBend(Number(event.target.value)));

      document.addEventListener("keydown", (event) => {
        if (event.key === "ArrowRight") {
          event.preventDefault();
          setTargetBend(state.targetBend + 10);
        } else if (event.key === "ArrowLeft") {
          event.preventDefault();
          setTargetBend(state.targetBend - 10);
        } else if (event.code === "Space") {
          event.preventDefault();
          setTargetBend(0);
        }
      });

      $("#fullscreenBtn").addEventListener("click", async () => {
        try {
          if (!document.fullscreenElement) {
            await document.documentElement.requestFullscreen();
          } else {
            await document.exitFullscreen();
          }
        } catch (error) {
          // Fullscreen can be blocked by the browser; the simulation remains fully usable.
        }
      });

      buildGrid();
      updateTelemetry(state.currentBend);
      updateRollProfile(state.currentBend);

      if ("ResizeObserver" in window) {
        const observer = new ResizeObserver(resizeCanvas);
        observer.observe($("#processStage"));
      } else {
        window.addEventListener("resize", resizeCanvas);
      }
      resizeCanvas();
      requestAnimationFrame(animationFrame);
    })();
  </script>
</body>
</html>
