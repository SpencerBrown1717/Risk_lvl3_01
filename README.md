<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Real Time Global Risk Management</title>
<style>
  * {
    box-sizing: border-box;
  }

  html, body {
    margin: 0;
    width: 100%;
    height: 100%;
    background: #050505;
    color: #fff;
    font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", sans-serif;
    overflow: hidden;
  }

  canvas {
    display: block;
  }

  .overlay {
    position: absolute;
    inset: 0;
    pointer-events: none;
  }

  .title {
    position: absolute;
    top: 34px;
    left: 50%;
    transform: translateX(-50%);
    text-align: center;
    z-index: 10;
  }

  .title h1 {
    margin: 0;
    font-size: 30px;
    font-weight: 500;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    opacity: 0.96;
  }

  .title p {
    margin: 10px 0 0;
    font-size: 13px;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: rgba(255,255,255,0.55);
  }

  .hud-left,
  .hud-right {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    z-index: 10;
    width: 200px;
  }

  .hud-left {
    left: 34px;
    text-align: left;
  }

  .hud-right {
    right: 34px;
    text-align: right;
  }

  .hud-label {
    font-size: 11px;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: rgba(255,255,255,0.42);
    margin-bottom: 10px;
  }

  .hud-value {
    font-size: 15px;
    letter-spacing: 0.08em;
    color: rgba(255,255,255,0.92);
    margin-bottom: 22px;
  }

  .footer {
    position: absolute;
    bottom: 24px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 14px;
    z-index: 10;
    flex-wrap: wrap;
    justify-content: center;
  }

  .pill {
    border: 1px solid rgba(255,255,255,0.14);
    background: rgba(255,255,255,0.04);
    color: rgba(255,255,255,0.78);
    padding: 8px 12px;
    border-radius: 999px;
    font-size: 11px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    backdrop-filter: blur(8px);
  }

  .scanline {
    position: absolute;
    inset: 0;
    background:
      linear-gradient(
        to bottom,
        rgba(255,255,255,0.03) 0px,
        rgba(255,255,255,0.01) 1px,
        transparent 2px,
        transparent 4px
      );
    opacity: 0.12;
    mix-blend-mode: screen;
  }

  @media (max-width: 900px) {
    .hud-left,
    .hud-right {
      display: none;
    }

    .title h1 {
      font-size: 22px;
    }

    .title p {
      font-size: 11px;
      letter-spacing: 0.14em;
      padding: 0 18px;
    }

    .footer {
      bottom: 18px;
      gap: 10px;
      padding: 0 14px;
    }

    .pill {
      font-size: 10px;
      padding: 7px 10px;
    }
  }
</style>
</head>
<body>
  <canvas id="scene"></canvas>

  <div class="overlay">
    <div class="title">
      <h1>Real Time Global Risk Management</h1>
      <p>Agents monitor news, events, and markets to update positions, hedges, and warnings instantly</p>
    </div>

    <div class="hud-left">
      <div class="hud-label">Global Inputs</div>
      <div class="hud-value" id="inputCount">12,480 live signals</div>

      <div class="hud-label">Active Risk Sweep</div>
      <div class="hud-value" id="sweepStatus">Cross market correlation scan</div>

      <div class="hud-label">Decision Engine</div>
      <div class="hud-value" id="decisionStatus">Hedging and alert routing</div>
    </div>

    <div class="hud-right">
      <div class="hud-label">Latency</div>
      <div class="hud-value" id="latency">42 ms response</div>

      <div class="hud-label">Exposure State</div>
      <div class="hud-value" id="exposure">Continuously rebalanced</div>

      <div class="hud-label">Alert Level</div>
      <div class="hud-value" id="alertLevel">Elevated macro watch</div>
    </div>

    <div class="footer">
      <div class="pill">News</div>
      <div class="pill">Macro</div>
      <div class="pill">FX</div>
      <div class="pill">Rates</div>
      <div class="pill">Equities</div>
      <div class="pill">Commodities</div>
      <div class="pill">Hedges</div>
      <div class="pill">Warnings</div>
    </div>

    <div class="scanline"></div>
  </div>

<script>
const canvas = document.getElementById("scene");
const ctx = canvas.getContext("2d");

let w = canvas.width = window.innerWidth;
let h = canvas.height = window.innerHeight;
let cx = w / 2;
let cy = h / 2;

const globe = {
  x: cx,
  y: cy + 10,
  r: Math.min(w, h) * 0.16
};

const nodes = [];
const pulses = [];
const arcs = [];
const warnings = [];

const orbitBands = [1.55, 1.95, 2.35];
const labels = [
  "NEWS", "FX", "RATES", "INDEX", "VOL", "BONDS", "CREDIT", "OIL",
  "GOLD", "SHIPPING", "POLICY", "EVENT", "RISK", "HEDGE", "ALERT", "FLOW"
];

function resize() {
  w = canvas.width = window.innerWidth;
  h = canvas.height = window.innerHeight;
  cx = w / 2;
  cy = h / 2;
  globe.x = cx;
  globe.y = cy + 10;
  globe.r = Math.min(w, h) * 0.16;
  buildNodes();
}

function rand(min, max) {
  return Math.random() * (max - min) + min;
}

function pick(arr) {
  return arr[Math.floor(Math.random() * arr.length)];
}

function buildNodes() {
  nodes.length = 0;
  const total = window.innerWidth < 900 ? 34 : 56;

  for (let i = 0; i < total; i++) {
    const band = orbitBands[i % orbitBands.length];
    const angle = (Math.PI * 2 * i) / total + rand(-0.12, 0.12);
    const radius = globe.r * band + rand(-18, 18);

    nodes.push({
      angle,
      radius,
      speed: rand(0.0008, 0.0022) * (Math.random() > 0.5 ? 1 : -1),
      size: rand(2, 4.2),
      type: Math.random() > 0.75 ? "risk" : "signal",
      label: pick(labels),
      pulseOffset: rand(0, Math.PI * 2)
    });
  }
}

function screenPos(node) {
  return {
    x: globe.x + Math.cos(node.angle) * node.radius,
    y: globe.y + Math.sin(node.angle) * node.radius * 0.72
  };
}

function spawnPulse() {
  const node = pick(nodes);
  const start = screenPos(node);

  pulses.push({
    fromX: start.x,
    fromY: start.y,
    toX: globe.x,
    toY: globe.y,
    t: 0,
    speed: rand(0.015, 0.03),
    size: rand(2.2, 4.8)
  });
}

function spawnArc() {
  const a = pick(nodes);
  const b = pick(nodes);
  if (a === b) return;

  const p1 = screenPos(a);
  const p2 = screenPos(b);

  arcs.push({
    x1: p1.x,
    y1: p1.y,
    x2: p2.x,
    y2: p2.y,
    life: 1,
    decay: rand(0.008, 0.018)
  });
}

function spawnWarning() {
  warnings.push({
    angle: rand(0, Math.PI * 2),
    life: 1,
    radius: globe.r + rand(14, 34)
  });
}

function drawBackground() {
  const gradient = ctx.createRadialGradient(cx, cy, globe.r * 0.25, cx, cy, Math.max(w, h) * 0.65);
  gradient.addColorStop(0, "rgba(255,255,255,0.035)");
  gradient.addColorStop(0.45, "rgba(255,255,255,0.015)");
  gradient.addColorStop(1, "rgba(0,0,0,0)");

  ctx.fillStyle = "#050505";
  ctx.fillRect(0, 0, w, h);

  ctx.fillStyle = gradient;
  ctx.fillRect(0, 0, w, h);
}

function drawGrid() {
  ctx.save();
  ctx.strokeStyle = "rgba(255,255,255,0.035)";
  ctx.lineWidth = 1;

  const gap = 48;
  for (let x = 0; x < w; x += gap) {
    ctx.beginPath();
    ctx.moveTo(x, 0);
    ctx.lineTo(x, h);
    ctx.stroke();
  }
  for (let y = 0; y < h; y += gap) {
    ctx.beginPath();
    ctx.moveTo(0, y);
    ctx.lineTo(w, y);
    ctx.stroke();
  }
  ctx.restore();
}

function drawOrbits(time) {
  ctx.save();
  orbitBands.forEach((band, i) => {
    const r = globe.r * band;
    ctx.beginPath();
    ctx.ellipse(globe.x, globe.y, r, r * 0.72, 0, 0, Math.PI * 2);
    ctx.strokeStyle = `rgba(255,255,255,${0.06 + i * 0.03})`;
    ctx.lineWidth = 1;
    ctx.stroke();
  });

  for (let i = 0; i < 3; i++) {
    const rr = globe.r + (Math.sin(time * 0.0015 + i) + 1) * 18 + i * 18;
    ctx.beginPath();
    ctx.arc(globe.x, globe.y, rr, 0, Math.PI * 2);
    ctx.strokeStyle = `rgba(255,255,255,${0.08 - i * 0.015})`;
    ctx.lineWidth = 1;
    ctx.stroke();
  }
  ctx.restore();
}

function drawGlobe(time) {
  ctx.save();

  const globeGradient = ctx.createRadialGradient(
    globe.x - globe.r * 0.25,
    globe.y - globe.r * 0.3,
    globe.r * 0.15,
    globe.x,
    globe.y,
    globe.r
  );
  globeGradient.addColorStop(0, "rgba(255,255,255,0.16)");
  globeGradient.addColorStop(0.45, "rgba(255,255,255,0.07)");
  globeGradient.addColorStop(1, "rgba(255,255,255,0.02)");

  ctx.beginPath();
  ctx.arc(globe.x, globe.y, globe.r, 0, Math.PI * 2);
  ctx.fillStyle = globeGradient;
  ctx.fill();
  ctx.strokeStyle = "rgba(255,255,255,0.18)";
  ctx.lineWidth = 1.2;
  ctx.stroke();

  ctx.beginPath();
  ctx.ellipse(globe.x, globe.y, globe.r, globe.r * 0.35, 0, 0, Math.PI * 2);
  ctx.strokeStyle = "rgba(255,255,255,0.10)";
  ctx.stroke();

  ctx.beginPath();
  ctx.ellipse(globe.x, globe.y, globe.r * 0.55, globe.r, 0, 0, Math.PI * 2);
  ctx.strokeStyle = "rgba(255,255,255,0.10)";
  ctx.stroke();

  for (let i = -2; i <= 2; i++) {
    ctx.beginPath();
    ctx.arc(globe.x, globe.y + i * globe.r * 0.25, globe.r * Math.cos(i * 0.42), 0, Math.PI * 2);
    ctx.strokeStyle = "rgba(255,255,255,0.06)";
    ctx.stroke();
  }

  const sweep = time * 0.0012;
  ctx.beginPath();
  ctx.moveTo(globe.x, globe.y);
  ctx.arc(globe.x, globe.y, globe.r * 1.15, sweep, sweep + 0.22);
  ctx.closePath();
  ctx.fillStyle = "rgba(255,255,255,0.035)";
  ctx.fill();

  ctx.restore();
}

function drawNodes(time) {
  ctx.save();

  nodes.forEach((node, idx) => {
    node.angle += node.speed;

    const p = screenPos(node);
    const pulse = 0.55 + 0.45 * Math.sin(time * 0.003 + node.pulseOffset);

    ctx.beginPath();
    ctx.arc(p.x, p.y, node.size + pulse * 1.2, 0, Math.PI * 2);
    ctx.fillStyle = node.type === "risk"
      ? `rgba(255,255,255,${0.18 + pulse * 0.15})`
      : `rgba(255,255,255,${0.12 + pulse * 0.16})`;
    ctx.fill();

    ctx.beginPath();
    ctx.arc(p.x, p.y, node.size * 0.55, 0, Math.PI * 2);
    ctx.fillStyle = "#ffffff";
    ctx.fill();

    if (idx % 7 === 0) {
      ctx.font = "10px -apple-system, BlinkMacSystemFont, sans-serif";
      ctx.fillStyle = "rgba(255,255,255,0.45)";
      ctx.textAlign = "center";
      ctx.fillText(node.label, p.x, p.y - 12);
    }

    ctx.beginPath();
    ctx.moveTo(p.x, p.y);
    ctx.lineTo(globe.x, globe.y);
    ctx.strokeStyle = "rgba(255,255,255,0.055)";
    ctx.lineWidth = 1;
    ctx.stroke();
  });

  ctx.restore();
}

function drawArcs() {
  ctx.save();
  arcs.forEach((arc, i) => {
    arc.life -= arc.decay;
    if (arc.life <= 0) {
      arcs.splice(i, 1);
      return;
    }

    const mx = (arc.x1 + arc.x2) / 2;
    const my = (arc.y1 + arc.y2) / 2 - 40;

    ctx.beginPath();
    ctx.moveTo(arc.x1, arc.y1);
    ctx.quadraticCurveTo(mx, my, arc.x2, arc.y2);
    ctx.strokeStyle = `rgba(255,255,255,${arc.life * 0.22})`;
    ctx.lineWidth = 1.2;
    ctx.stroke();
  });
  ctx.restore();
}

function drawPulses() {
  ctx.save();
  pulses.forEach((pulse, i) => {
    pulse.t += pulse.speed;
    if (pulse.t >= 1) {
      pulses.splice(i, 1);
      return;
    }

    const x = pulse.fromX + (pulse.toX - pulse.fromX) * pulse.t;
    const y = pulse.fromY + (pulse.toY - pulse.fromY) * pulse.t;

    ctx.beginPath();
    ctx.arc(x, y, pulse.size, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(255,255,255,${0.45 * (1 - pulse.t) + 0.25})`;
    ctx.fill();

    ctx.beginPath();
    ctx.arc(x, y, pulse.size * 2.3, 0, Math.PI * 2);
    ctx.strokeStyle = `rgba(255,255,255,${0.18 * (1 - pulse.t)})`;
    ctx.lineWidth = 1;
    ctx.stroke();
  });
  ctx.restore();
}

function drawWarnings() {
  ctx.save();
  warnings.forEach((w, i) => {
    w.life -= 0.01;
    if (w.life <= 0) {
      warnings.splice(i, 1);
      return;
    }

    const x = globe.x + Math.cos(w.angle) * w.radius;
    const y = globe.y + Math.sin(w.angle) * w.radius * 0.72;

    ctx.beginPath();
    ctx.arc(x, y, 8 + (1 - w.life) * 12, 0, Math.PI * 2);
    ctx.strokeStyle = `rgba(255,255,255,${w.life * 0.35})`;
    ctx.lineWidth = 1.5;
    ctx.stroke();

    ctx.beginPath();
    ctx.arc(x, y, 2.2, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(255,255,255,${w.life * 0.9})`;
    ctx.fill();
  });
  ctx.restore();
}

const leftStats = [
  "12,480 live signals",
  "16,240 live signals",
  "14,920 live signals",
  "18,110 live signals"
];

const sweepStats = [
  "Cross market correlation scan",
  "Macro shock propagation map",
  "Event clustering and anomaly review",
  "Volatility transmission analysis"
];

const decisionStats = [
  "Hedging and alert routing",
  "Position adjustment engine live",
  "News to execution pathway active",
  "Risk repricing in motion"
];

const latencyStats = [
  "42 ms response",
  "37 ms response",
  "51 ms response",
  "44 ms response"
];

const exposureStats = [
  "Continuously rebalanced",
  "Hedge ratios updating",
  "Portfolio stress reduced",
  "Cross asset offsets active"
];

const alertStats = [
  "Elevated macro watch",
  "Regional disruption flagged",
  "Volatility spike detected",
  "Event risk intensifying"
];

let statTimer = 0;

function updateHud(time) {
  if (time - statTimer > 2400) {
    statTimer = time;
    document.getElementById("inputCount").textContent = pick(leftStats);
    document.getElementById("sweepStatus").textContent = pick(sweepStats);
    document.getElementById("decisionStatus").textContent = pick(decisionStats);
    document.getElementById("latency").textContent = pick(latencyStats);
    document.getElementById("exposure").textContent = pick(exposureStats);
    document.getElementById("alertLevel").textContent = pick(alertStats);
  }
}

function animate(time) {
  drawBackground();
  drawGrid();
  drawOrbits(time);
  drawArcs();
  drawNodes(time);
  drawPulses();
  drawWarnings();
  drawGlobe(time);
  updateHud(time);

  if (Math.random() < 0.16) spawnPulse();
  if (Math.random() < 0.045) spawnArc();
  if (Math.random() < 0.02) spawnWarning();

  requestAnimationFrame(animate);
}

buildNodes();
animate(0);

window.addEventListener("resize", resize);
</script>
</body>
</html>
