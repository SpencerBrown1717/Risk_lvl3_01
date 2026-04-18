<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Real Time Global Risk Management</title>
  <style>
    :root {
      --bg: #050505;
      --bg-soft: rgba(255,255,255,0.04);
      --line: rgba(255,255,255,0.12);
      --line-soft: rgba(255,255,255,0.07);
      --text: rgba(255,255,255,0.96);
      --text-soft: rgba(255,255,255,0.62);
      --text-faint: rgba(255,255,255,0.38);
      --panel: rgba(255,255,255,0.045);
      --panel-border: rgba(255,255,255,0.10);
      --glow: rgba(255,255,255,0.12);
      --shadow: 0 10px 50px rgba(0,0,0,0.45);
    }

    * {
      box-sizing: border-box;
    }

    html, body {
      margin: 0;
      width: 100%;
      height: 100%;
      background: var(--bg);
      color: white;
      font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "Inter", sans-serif;
      overflow: hidden;
    }

    body {
      position: relative;
      background:
        radial-gradient(circle at 50% 45%, rgba(255,255,255,0.045), transparent 22%),
        radial-gradient(circle at 50% 50%, rgba(255,255,255,0.02), transparent 55%),
        linear-gradient(180deg, #080808 0%, #050505 45%, #030303 100%);
    }

    canvas {
      display: block;
      width: 100%;
      height: 100%;
    }

    .overlay {
      position: absolute;
      inset: 0;
      pointer-events: none;
      z-index: 2;
    }

    .topbar {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      padding: clamp(22px, 3vw, 38px) clamp(18px, 3vw, 36px) 0;
      display: flex;
      justify-content: center;
    }

    .title-wrap {
      width: min(980px, 100%);
      text-align: center;
    }

    .eyebrow {
      font-size: 11px;
      letter-spacing: 0.28em;
      text-transform: uppercase;
      color: var(--text-faint);
      margin-bottom: 10px;
    }

    .title {
      margin: 0;
      font-weight: 550;
      font-size: clamp(28px, 4vw, 52px);
      line-height: 1.02;
      letter-spacing: 0.02em;
      color: var(--text);
      text-wrap: balance;
    }

    .subtitle {
      margin: 14px auto 0;
      max-width: 920px;
      font-size: clamp(13px, 1.4vw, 17px);
      line-height: 1.65;
      color: var(--text-soft);
      letter-spacing: 0.02em;
      text-wrap: balance;
    }

    .side {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      width: min(240px, 24vw);
      display: flex;
      flex-direction: column;
      gap: 14px;
    }

    .side.left {
      left: clamp(14px, 2vw, 28px);
    }

    .side.right {
      right: clamp(14px, 2vw, 28px);
    }

    .panel {
      background: linear-gradient(180deg, rgba(255,255,255,0.055), rgba(255,255,255,0.028));
      border: 1px solid var(--panel-border);
      border-radius: 18px;
      box-shadow: var(--shadow);
      padding: 14px 14px 13px;
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
    }

    .panel-label {
      font-size: 10px;
      letter-spacing: 0.22em;
      text-transform: uppercase;
      color: var(--text-faint);
      margin-bottom: 8px;
    }

    .panel-value {
      font-size: clamp(14px, 1.15vw, 16px);
      line-height: 1.45;
      color: var(--text);
    }

    .bottom {
      position: absolute;
      left: 50%;
      bottom: clamp(16px, 2vw, 28px);
      transform: translateX(-50%);
      width: min(1040px, calc(100% - 24px));
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 12px;
    }

    .legend {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
      max-width: 100%;
    }

    .pill {
      padding: 9px 13px;
      border-radius: 999px;
      border: 1px solid var(--line);
      background: rgba(255,255,255,0.035);
      color: rgba(255,255,255,0.78);
      font-size: 10px;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      box-shadow: 0 6px 30px rgba(0,0,0,0.22);
      white-space: nowrap;
    }

    .status-bar {
      width: min(820px, 100%);
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 10px;
    }

    .status {
      border: 1px solid var(--line-soft);
      background: rgba(255,255,255,0.028);
      border-radius: 16px;
      padding: 12px 14px;
      text-align: center;
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
    }

    .status-k {
      display: block;
      font-size: 10px;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--text-faint);
      margin-bottom: 7px;
    }

    .status-v {
      display: block;
      font-size: clamp(13px, 1vw, 15px);
      color: var(--text);
      line-height: 1.35;
    }

    .vignette,
    .scanlines,
    .noise {
      position: absolute;
      inset: 0;
      pointer-events: none;
    }

    .vignette {
      background:
        radial-gradient(circle at center, transparent 38%, rgba(0,0,0,0.20) 72%, rgba(0,0,0,0.42) 100%);
      z-index: 1;
    }

    .scanlines {
      background:
        linear-gradient(
          to bottom,
          rgba(255,255,255,0.022) 0px,
          rgba(255,255,255,0.008) 1px,
          transparent 2px,
          transparent 4px
        );
      opacity: 0.11;
      mix-blend-mode: screen;
      z-index: 3;
    }

    .noise {
      opacity: 0.03;
      background-image:
        radial-gradient(rgba(255,255,255,0.7) 0.4px, transparent 0.4px);
      background-size: 6px 6px;
      z-index: 3;
    }

    @media (max-width: 1100px) {
      .side {
        width: 210px;
      }
    }

    @media (max-width: 920px) {
      .side {
        display: none;
      }

      .bottom {
        width: min(960px, calc(100% - 20px));
      }

      .status-bar {
        grid-template-columns: repeat(2, minmax(0, 1fr));
      }
    }

    @media (max-width: 640px) {
      .topbar {
        padding-top: 18px;
      }

      .eyebrow {
        font-size: 9px;
        letter-spacing: 0.22em;
      }

      .subtitle {
        max-width: 96%;
        line-height: 1.5;
      }

      .legend {
        gap: 8px;
      }

      .pill {
        font-size: 9px;
        padding: 8px 11px;
        letter-spacing: 0.12em;
      }

      .status-bar {
        grid-template-columns: 1fr;
        gap: 8px;
      }

      .status {
        padding: 10px 12px;
      }
    }
  </style>
</head>
<body>
  <canvas id="scene"></canvas>

  <div class="vignette"></div>

  <div class="overlay">
    <div class="topbar">
      <div class="title-wrap">
        <div class="eyebrow">Autonomous Market Intelligence</div>
        <h1 class="title">Real Time Global Risk Management</h1>
        <p class="subtitle">
          Distributed agents monitor global news, macro events, and live markets, then reprice exposure,
          deploy hedges, and escalate warnings the moment conditions change.
        </p>
      </div>
    </div>

    <div class="side left">
      <div class="panel">
        <div class="panel-label">Signal Ingestion</div>
        <div class="panel-value" id="left1">14,920 live inputs across markets and events</div>
      </div>
      <div class="panel">
        <div class="panel-label">Cross Market Analysis</div>
        <div class="panel-value" id="left2">Correlation shifts and anomaly clusters under active review</div>
      </div>
      <div class="panel">
        <div class="panel-label">Risk Coordination</div>
        <div class="panel-value" id="left3">Agents routing hedges and warnings across portfolios</div>
      </div>
    </div>

    <div class="side right">
      <div class="panel">
        <div class="panel-label">Response Latency</div>
        <div class="panel-value" id="right1">41 ms decision cycle</div>
      </div>
      <div class="panel">
        <div class="panel-label">Exposure State</div>
        <div class="panel-value" id="right2">Portfolio risk continuously rebalanced</div>
      </div>
      <div class="panel">
        <div class="panel-label">Escalation Level</div>
        <div class="panel-value" id="right3">Elevated macro and volatility watch</div>
      </div>
    </div>

    <div class="bottom">
      <div class="legend">
        <div class="pill">News</div>
        <div class="pill">Geopolitics</div>
        <div class="pill">Rates</div>
        <div class="pill">FX</div>
        <div class="pill">Equities</div>
        <div class="pill">Credit</div>
        <div class="pill">Commodities</div>
        <div class="pill">Volatility</div>
        <div class="pill">Hedges</div>
        <div class="pill">Warnings</div>
      </div>

      <div class="status-bar">
        <div class="status">
          <span class="status-k">Signal Flow</span>
          <span class="status-v" id="s1">Global event stream active</span>
        </div>
        <div class="status">
          <span class="status-k">Inference</span>
          <span class="status-v" id="s2">Risk engine repricing in real time</span>
        </div>
        <div class="status">
          <span class="status-k">Hedging</span>
          <span class="status-v" id="s3">Protective actions routing across books</span>
        </div>
        <div class="status">
          <span class="status-k">Alerting</span>
          <span class="status-v" id="s4">Escalations synchronized to decision makers</span>
        </div>
      </div>
    </div>
  </div>

  <div class="scanlines"></div>
  <div class="noise"></div>

  <script>
    const canvas = document.getElementById("scene");
    const ctx = canvas.getContext("2d");

    let width = 0;
    let height = 0;
    let dpr = Math.min(window.devicePixelRatio || 1, 2);

    const state = {
      centerX: 0,
      centerY: 0,
      globeR: 0,
      rings: [],
      nodes: [],
      pulses: [],
      traces: [],
      warnings: [],
      stars: []
    };

    const labels = [
      "NEWS", "FX", "RATES", "CREDIT", "VOL", "POLICY", "FLOW", "EVENT",
      "ENERGY", "INDEX", "MACRO", "RISK", "HEDGE", "ALERT", "SHIPPING", "BONDS"
    ];

    const hudSets = {
      left1: [
        "14,920 live inputs across markets and events",
        "16,410 concurrent signals entering the system",
        "13,880 live data points fused across regions",
        "18,020 active feeds under continuous monitoring"
      ],
      left2: [
        "Correlation shifts and anomaly clusters under active review",
        "Shock propagation pathways being mapped in real time",
        "Cross asset dependencies re-evaluated every cycle",
        "Macro and market disruptions being scored continuously"
      ],
      left3: [
        "Agents routing hedges and warnings across portfolios",
        "Distributed systems coordinating protection and escalation",
        "Execution pathways prioritized by emerging risk intensity",
        "Response logic synchronizing positions and alerts"
      ],
      right1: [
        "41 ms decision cycle",
        "38 ms response time",
        "46 ms signal to action",
        "43 ms coordinated update latency"
      ],
      right2: [
        "Portfolio risk continuously rebalanced",
        "Exposure and hedge ratios updating live",
        "Cross asset offsets adjusting in flight",
        "Live protection logic active across positions"
      ],
      right3: [
        "Elevated macro and volatility watch",
        "Regional disruption pathway flagged",
        "Fast moving market stress under review",
        "Event driven escalation threshold raised"
      ],
      s1: [
        "Global event stream active",
        "Multi region monitoring online",
        "News and market ingestion synchronized",
        "Cross venue signal intake stable"
      ],
      s2: [
        "Risk engine repricing in real time",
        "Anomaly detection pipeline fully active",
        "Scenario scoring converging continuously",
        "Decision model evaluating second order effects"
      ],
      s3: [
        "Protective actions routing across books",
        "Hedge allocation logic responding instantly",
        "Execution priorities recalibrated live",
        "Defense posture adapting by region and asset"
      ],
      s4: [
        "Escalations synchronized to decision makers",
        "Warnings pushed as thresholds are crossed",
        "Critical alerts prioritized by severity",
        "Response chain aligned across teams"
      ]
    };

    function rand(min, max) {
      return Math.random() * (max - min) + min;
    }

    function pick(arr) {
      return arr[Math.floor(Math.random() * arr.length)];
    }

    function setCanvasSize() {
      width = window.innerWidth;
      height = window.innerHeight;
      dpr = Math.min(window.devicePixelRatio || 1, 2);

      canvas.width = Math.floor(width * dpr);
      canvas.height = Math.floor(height * dpr);
      canvas.style.width = width + "px";
      canvas.style.height = height + "px";

      ctx.setTransform(dpr, 0, 0, dpr, 0, 0);

      state.centerX = width * 0.5;
      state.centerY = height * 0.56;
      state.globeR = Math.min(width, height) * (width < 700 ? 0.18 : 0.16);

      const base = state.globeR;
      state.rings = [
        { rx: base * 1.55, ry: base * 1.05 },
        { rx: base * 1.95, ry: base * 1.32 },
        { rx: base * 2.38, ry: base * 1.60 }
      ];

      buildStars();
      buildNodes();
    }

    function buildStars() {
      state.stars = [];
      const count = width < 700 ? 60 : 110;

      for (let i = 0; i < count; i++) {
        state.stars.push({
          x: Math.random() * width,
          y: Math.random() * height,
          a: rand(0.08, 0.4),
          r: rand(0.5, 1.4),
          tw: rand(0.001, 0.004)
        });
      }
    }

    function buildNodes() {
      state.nodes = [];
      const count = width < 700 ? 28 : width < 1100 ? 40 : 54;

      for (let i = 0; i < count; i++) {
        const ringIndex = i % state.rings.length;
        const ring = state.rings[ringIndex];

        state.nodes.push({
          ringIndex,
          angle: (Math.PI * 2 * i) / count + rand(-0.14, 0.14),
          speed: rand(0.0008, 0.0022) * (Math.random() > 0.5 ? 1 : -1),
          size: rand(2, 4.2),
          glow: rand(0.15, 0.8),
          label: pick(labels),
          labelOffset: Math.random() * Math.PI * 2,
          type: Math.random() > 0.78 ? "warning" : "signal",
          drift: rand(-0.04, 0.04),
          ring
        });
      }
    }

    function nodePosition(node) {
      const ring = state.rings[node.ringIndex];
      return {
        x: state.centerX + Math.cos(node.angle) * ring.rx,
        y: state.centerY + Math.sin(node.angle) * ring.ry
      };
    }

    function spawnPulse() {
      if (!state.nodes.length) return;

      const fromNode = pick(state.nodes);
      const pos = nodePosition(fromNode);

      state.pulses.push({
        fromX: pos.x,
        fromY: pos.y,
        toX: state.centerX,
        toY: state.centerY,
        t: 0,
        speed: rand(0.014, 0.026),
        size: rand(2.2, 4.6),
        alpha: rand(0.45, 0.9)
      });
    }

    function spawnTrace() {
      if (state.nodes.length < 2) return;

      let a = pick(state.nodes);
      let b = pick(state.nodes);
      if (a === b) return;

      const p1 = nodePosition(a);
      const p2 = nodePosition(b);

      state.traces.push({
        x1: p1.x,
        y1: p1.y,
        x2: p2.x,
        y2: p2.y,
        cx: (p1.x + p2.x) / 2 + rand(-26, 26),
        cy: (p1.y + p2.y) / 2 - rand(18, 52),
        life: 1,
        decay: rand(0.01, 0.02)
      });
    }

    function spawnWarning() {
      const angle = rand(0, Math.PI * 2);
      const radiusX = state.globeR * rand(1.18, 1.5);
      const radiusY = state.globeR * rand(0.95, 1.22);

      state.warnings.push({
        angle,
        rx: radiusX,
        ry: radiusY,
        life: 1,
        growth: rand(0.65, 1.2)
      });
    }

    function drawBackdrop(time) {
      ctx.clearRect(0, 0, width, height);

      const radial = ctx.createRadialGradient(
        state.centerX,
        state.centerY,
        state.globeR * 0.2,
        state.centerX,
        state.centerY,
        Math.max(width, height) * 0.65
      );
      radial.addColorStop(0, "rgba(255,255,255,0.04)");
      radial.addColorStop(0.28, "rgba(255,255,255,0.015)");
      radial.addColorStop(1, "rgba(255,255,255,0)");

      ctx.fillStyle = radial;
      ctx.fillRect(0, 0, width, height);

      ctx.save();
      for (const star of state.stars) {
        const twinkle = star.a + Math.sin(time * star.tw) * 0.08;
        ctx.beginPath();
        ctx.arc(star.x, star.y, star.r, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(255,255,255,${twinkle})`;
        ctx.fill();
      }
      ctx.restore();

      ctx.save();
      ctx.strokeStyle = "rgba(255,255,255,0.03)";
      ctx.lineWidth = 1;

      const gap = width < 700 ? 52 : 58;
      for (let x = 0; x < width; x += gap) {
        ctx.beginPath();
        ctx.moveTo(x, 0);
        ctx.lineTo(x, height);
        ctx.stroke();
      }
      for (let y = 0; y < height; y += gap) {
        ctx.beginPath();
        ctx.moveTo(0, y);
        ctx.lineTo(width, y);
        ctx.stroke();
      }
      ctx.restore();
    }

    function drawRings(time) {
      ctx.save();

      state.rings.forEach((ring, i) => {
        ctx.beginPath();
        ctx.ellipse(state.centerX, state.centerY, ring.rx, ring.ry, 0, 0, Math.PI * 2);
        ctx.strokeStyle = `rgba(255,255,255,${0.06 + i * 0.03})`;
        ctx.lineWidth = 1;
        ctx.stroke();
      });

      for (let i = 0; i < 4; i++) {
        const pulse = (Math.sin(time * 0.0015 + i * 0.8) + 1) * 0.5;
        const r = state.globeR * (1.08 + i * 0.12 + pulse * 0.04);

        ctx.beginPath();
        ctx.arc(state.centerX, state.centerY, r, 0, Math.PI * 2);
        ctx.strokeStyle = `rgba(255,255,255,${0.03 + (0.06 - i * 0.01)})`;
        ctx.lineWidth = 1;
        ctx.stroke();
      }

      ctx.restore();
    }

    function drawGlobe(time) {
      ctx.save();

      const g = ctx.createRadialGradient(
        state.centerX - state.globeR * 0.26,
        state.centerY - state.globeR * 0.28,
        state.globeR * 0.15,
        state.centerX,
        state.centerY,
        state.globeR
      );
      g.addColorStop(0, "rgba(255,255,255,0.18)");
      g.addColorStop(0.42, "rgba(255,255,255,0.075)");
      g.addColorStop(1, "rgba(255,255,255,0.02)");

      ctx.beginPath();
      ctx.arc(state.centerX, state.centerY, state.globeR, 0, Math.PI * 2);
      ctx.fillStyle = g;
      ctx.fill();
      ctx.strokeStyle = "rgba(255,255,255,0.17)";
      ctx.lineWidth = 1.2;
      ctx.stroke();

      ctx.beginPath();
      ctx.ellipse(state.centerX, state.centerY, state.globeR, state.globeR * 0.34, 0, 0, Math.PI * 2);
      ctx.strokeStyle = "rgba(255,255,255,0.09)";
      ctx.stroke();

      ctx.beginPath();
      ctx.ellipse(state.centerX, state.centerY, state.globeR * 0.55, state.globeR, 0, 0, Math.PI * 2);
      ctx.strokeStyle = "rgba(255,255,255,0.09)";
      ctx.stroke();

      for (let i = -2; i <= 2; i++) {
        const rr = state.globeR * Math.cos(i * 0.4);
        if (rr > 2) {
          ctx.beginPath();
          ctx.arc(state.centerX, state.centerY + i * state.globeR * 0.24, rr, 0, Math.PI * 2);
          ctx.strokeStyle = "rgba(255,255,255,0.055)";
          ctx.stroke();
        }
      }

      const sweepAngle = time * 0.001;
      ctx.beginPath();
      ctx.moveTo(state.centerX, state.centerY);
      ctx.arc(state.centerX, state.centerY, state.globeR * 1.16, sweepAngle, sweepAngle + 0.25);
      ctx.closePath();
      ctx.fillStyle = "rgba(255,255,255,0.035)";
      ctx.fill();

      const innerPulse = 0.6 + Math.sin(time * 0.003) * 0.08;
      ctx.beginPath();
      ctx.arc(state.centerX, state.centerY, state.globeR * innerPulse * 0.18, 0, Math.PI * 2);
      ctx.fillStyle = "rgba(255,255,255,0.92)";
      ctx.fill();

      ctx.beginPath();
      ctx.arc(state.centerX, state.centerY, state.globeR * innerPulse * 0.33, 0, Math.PI * 2);
      ctx.strokeStyle = "rgba(255,255,255,0.12)";
      ctx.stroke();

      ctx.restore();
    }

    function drawNodes(time) {
      ctx.save();

      state.nodes.forEach((node, index) => {
        node.angle += node.speed;

        const p = nodePosition(node);
        const pulse = 0.55 + 0.45 * Math.sin(time * 0.003 + node.labelOffset);

        ctx.beginPath();
        ctx.arc(p.x, p.y, node.size + pulse * 1.25, 0, Math.PI * 2);
        ctx.fillStyle = node.type === "warning"
          ? `rgba(255,255,255,${0.14 + pulse * 0.18})`
          : `rgba(255,255,255,${0.11 + pulse * 0.14})`;
        ctx.fill();

        ctx.beginPath();
        ctx.arc(p.x, p.y, Math.max(1.2, node.size * 0.55), 0, Math.PI * 2);
        ctx.fillStyle = "#ffffff";
        ctx.fill();

        ctx.beginPath();
        ctx.moveTo(p.x, p.y);
        ctx.lineTo(state.centerX, state.centerY);
        ctx.strokeStyle = "rgba(255,255,255,0.045)";
        ctx.lineWidth = 1;
        ctx.stroke();

        if (width > 760 && index % 8 === 0) {
          ctx.font = "10px -apple-system, BlinkMacSystemFont, sans-serif";
          ctx.fillStyle = "rgba(255,255,255,0.42)";
          ctx.textAlign = "center";
          ctx.fillText(node.label, p.x, p.y - 12);
        }
      });

      ctx.restore();
    }

    function drawTraces() {
      ctx.save();

      for (let i = state.traces.length - 1; i >= 0; i--) {
        const t = state.traces[i];
        t.life -= t.decay;

        if (t.life <= 0) {
          state.traces.splice(i, 1);
          continue;
        }

        ctx.beginPath();
        ctx.moveTo(t.x1, t.y1);
        ctx.quadraticCurveTo(t.cx, t.cy, t.x2, t.y2);
        ctx.strokeStyle = `rgba(255,255,255,${t.life * 0.18})`;
        ctx.lineWidth = 1.15;
        ctx.stroke();
      }

      ctx.restore();
    }

    function drawPulses() {
      ctx.save();

      for (let i = state.pulses.length - 1; i >= 0; i--) {
        const p = state.pulses[i];
        p.t += p.speed;

        if (p.t >= 1) {
          state.pulses.splice(i, 1);
          continue;
        }

        const x = p.fromX + (p.toX - p.fromX) * p.t;
        const y = p.fromY + (p.toY - p.fromY) * p.t;
        const alpha = p.alpha * (1 - p.t * 0.35);

        ctx.beginPath();
        ctx.arc(x, y, p.size, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(255,255,255,${alpha})`;
        ctx.fill();

        ctx.beginPath();
        ctx.arc(x, y, p.size * 2.4, 0, Math.PI * 2);
        ctx.strokeStyle = `rgba(255,255,255,${alpha * 0.22})`;
        ctx.lineWidth = 1;
        ctx.stroke();
      }

      ctx.restore();
    }

    function drawWarnings() {
      ctx.save();

      for (let i = state.warnings.length - 1; i >= 0; i--) {
        const w = state.warnings[i];
        w.life -= 0.012;

        if (w.life <= 0) {
          state.warnings.splice(i, 1);
          continue;
        }

        const x = state.centerX + Math.cos(w.angle) * w.rx;
        const y = state.centerY + Math.sin(w.angle) * w.ry;
        const rr = 8 + (1 - w.life) * 18 * w.growth;

        ctx.beginPath();
        ctx.arc(x, y, rr, 0, Math.PI * 2);
        ctx.strokeStyle = `rgba(255,255,255,${w.life * 0.28})`;
        ctx.lineWidth = 1.4;
        ctx.stroke();

        ctx.beginPath();
        ctx.arc(x, y, 2.1, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(255,255,255,${w.life * 0.9})`;
        ctx.fill();
      }

      ctx.restore();
    }

    let hudTimer = 0;

    function updateHud(time) {
      if (time - hudTimer < 2400) return;
      hudTimer = time;

      for (const id in hudSets) {
        const el = document.getElementById(id);
        if (el) el.textContent = pick(hudSets[id]);
      }
    }

    function animate(time) {
      drawBackdrop(time);
      drawRings(time);
      drawTraces();
      drawNodes(time);
      drawPulses();
      drawWarnings();
      drawGlobe(time);
      updateHud(time);

      if (Math.random() < 0.17) spawnPulse();
      if (Math.random() < 0.05) spawnTrace();
      if (Math.random() < 0.018) spawnWarning();

      requestAnimationFrame(animate);
    }

    window.addEventListener("resize", setCanvasSize);

    setCanvasSize();
    requestAnimationFrame(animate);
  </script>
</body>
</html>
