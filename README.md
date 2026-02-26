<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rubén Martínez Agramunt</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300;0,400;0,600;0,700;1,300&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #080b0f;
    --surface: #0d1117;
    --border: #1a2332;
    --accent: #00ff9d;
    --accent2: #0affef;
    --accent3: #ff3c5c;
    --dim: #3a4a5c;
    --text: #c9d1d9;
    --muted: #586069;
    --bright: #e6edf3;
  }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    min-height: 100vh;
    padding: 0;
    overflow-x: hidden;
  }

  /* Scanline overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.03) 2px,
      rgba(0,0,0,0.03) 4px
    );
    pointer-events: none;
    z-index: 999;
  }

  .container {
    max-width: 860px;
    margin: 0 auto;
    padding: 60px 40px;
  }

  /* ── HEADER ── */
  .header {
    position: relative;
    margin-bottom: 64px;
    padding-bottom: 40px;
    border-bottom: 1px solid var(--border);
  }

  .ascii-art {
    font-size: 7px;
    line-height: 1.15;
    color: var(--accent);
    opacity: 0.85;
    letter-spacing: 0;
    white-space: pre;
    overflow-x: auto;
    margin-bottom: 28px;
    text-shadow: 0 0 20px var(--accent);
    animation: flicker 8s infinite;
  }

  @keyframes flicker {
    0%, 95%, 100% { opacity: 0.85; }
    96% { opacity: 0.6; }
    97% { opacity: 0.85; }
    98% { opacity: 0.5; }
    99% { opacity: 0.85; }
  }

  .name {
    font-family: 'Syne', sans-serif;
    font-size: 28px;
    font-weight: 800;
    color: var(--bright);
    letter-spacing: -0.5px;
    margin-bottom: 8px;
  }

  .tagline {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
    margin-bottom: 16px;
  }

  .tag {
    font-size: 11px;
    font-weight: 600;
    color: var(--accent);
    border: 1px solid var(--accent);
    padding: 3px 10px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    position: relative;
    background: rgba(0,255,157,0.04);
  }

  .tag::before {
    content: '';
    position: absolute;
    inset: -3px;
    border: 1px solid transparent;
    border-top-color: var(--accent);
    border-bottom-color: var(--accent);
    animation: border-spin 4s linear infinite;
    opacity: 0;
    transition: opacity 0.3s;
  }
  .tag:hover::before { opacity: 1; }

  .motto {
    font-style: italic;
    color: var(--muted);
    font-size: 13px;
    margin-top: 12px;
    padding-left: 12px;
    border-left: 2px solid var(--accent3);
  }
  .motto span { color: var(--accent2); font-style: normal; font-weight: 600; }

  /* ── SECTIONS ── */
  .section {
    margin-bottom: 56px;
    opacity: 0;
    transform: translateY(16px);
    animation: fadeUp 0.5s forwards;
  }

  @keyframes fadeUp {
    to { opacity: 1; transform: translateY(0); }
  }

  .section:nth-child(1) { animation-delay: 0.1s; }
  .section:nth-child(2) { animation-delay: 0.2s; }
  .section:nth-child(3) { animation-delay: 0.3s; }
  .section:nth-child(4) { animation-delay: 0.4s; }
  .section:nth-child(5) { animation-delay: 0.5s; }

  .section-label {
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .section-label::before {
    content: '>';
    color: var(--accent);
    font-weight: 700;
    text-shadow: 0 0 8px var(--accent);
  }
  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, var(--border), transparent);
  }

  /* Code blocks */
  .code-block {
    background: var(--surface);
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent);
    padding: 20px 24px;
    font-size: 13px;
    line-height: 1.7;
    position: relative;
    overflow: hidden;
  }

  .code-block::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(to right, var(--accent), transparent);
  }

  .code-block .kw { color: #ff7b72; }
  .code-block .str { color: #a5d6ff; }
  .code-block .bracket { color: var(--dim); }
  .code-block .var { color: #ffa657; }
  .code-block .comment { color: var(--muted); font-style: italic; }
  .code-block .fn { color: var(--accent2); }

  /* Prose */
  .prose {
    font-size: 14px;
    line-height: 1.8;
    color: var(--text);
  }

  .prose strong {
    color: var(--bright);
    font-weight: 600;
  }

  .prose .highlight {
    color: var(--accent);
    font-weight: 600;
  }

  /* Focus list */
  .focus-list {
    display: grid;
    gap: 1px;
  }

  .focus-item {
    display: grid;
    grid-template-columns: 28px 1fr;
    gap: 12px;
    padding: 14px 0;
    border-bottom: 1px solid var(--border);
    font-size: 13px;
    align-items: start;
    transition: background 0.2s;
    cursor: default;
  }

  .focus-item:hover {
    background: rgba(0,255,157,0.03);
    padding-left: 4px;
  }

  .focus-item:last-child { border-bottom: none; }

  .focus-icon {
    color: var(--accent);
    font-size: 15px;
    opacity: 0.8;
    padding-top: 1px;
  }

  .focus-text strong {
    color: var(--bright);
    display: block;
    margin-bottom: 2px;
  }

  .focus-text span {
    color: var(--muted);
    font-size: 12px;
  }

  /* Tech grid */
  .tech-group {
    margin-bottom: 24px;
  }

  .tech-group-label {
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 10px;
  }

  .tech-pills {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .pill {
    font-size: 12px;
    padding: 5px 14px;
    background: var(--surface);
    border: 1px solid var(--border);
    color: var(--text);
    position: relative;
    cursor: default;
    transition: all 0.2s;
    letter-spacing: 0.5px;
  }

  .pill::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 0;
    background: var(--accent);
    transition: height 0.2s;
  }

  .pill:hover {
    color: var(--bright);
    border-color: var(--accent);
  }

  .pill:hover::after { height: 2px; }

  .pill .dot {
    display: inline-block;
    width: 6px;
    height: 6px;
    border-radius: 50%;
    margin-right: 6px;
    vertical-align: middle;
  }

  /* Principles */
  .principles-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1px;
    background: var(--border);
  }

  .principle {
    background: var(--surface);
    padding: 20px 24px;
    position: relative;
    overflow: hidden;
    transition: background 0.2s;
    cursor: default;
  }

  .principle::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 3px;
    height: 0;
    background: var(--accent);
    transition: height 0.3s;
  }

  .principle:hover { background: #111820; }
  .principle:hover::before { height: 100%; }

  .principle-num {
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 2px;
    margin-bottom: 8px;
    font-weight: 600;
  }

  .principle-title {
    font-size: 13px;
    color: var(--bright);
    font-weight: 700;
    margin-bottom: 6px;
    letter-spacing: 0.3px;
  }

  .principle-desc {
    font-size: 11.5px;
    color: var(--muted);
    line-height: 1.6;
  }

  /* Terminal cursor */
  .cursor {
    display: inline-block;
    width: 8px;
    height: 14px;
    background: var(--accent);
    vertical-align: middle;
    animation: blink 1s step-end infinite;
    box-shadow: 0 0 8px var(--accent);
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  /* Status bar */
  .status-bar {
    position: fixed;
    bottom: 0; left: 0; right: 0;
    background: var(--accent);
    color: #000;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 1px;
    padding: 5px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .status-bar .blink-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #000;
    animation: blink 1.5s ease-in-out infinite;
    display: inline-block;
    margin-right: 6px;
  }

  @media (max-width: 600px) {
    .ascii-art { font-size: 5px; }
    .principles-grid { grid-template-columns: 1fr; }
    .container { padding: 40px 20px; }
  }
</style>
</head>
<body>

<div class="container">

  <!-- HEADER -->
  <div class="header">
    <pre class="ascii-art">██████╗ ██╗   ██╗██████╗ ██████╗  ██████╗██╗  ██╗ ██████╗ ██████╗ ██████╗ ███████╗
██╔══██╗██║   ██║██╔══██╗╚════██╗██╔════╝██║ ██╔╝██╔═══██╗██╔══██╗╚════██╗██╔════╝
██████╔╝██║   ██║██████╔╝ █████╔╝██║     █████╔╝ ██║   ██║██████╔╝ █████╔╝█████╗  
██╔══██╗██║   ██║██╔══██╗ ╚═══██╗██║     ██╔═██╗ ██║   ██║██╔══██╗ ╚═══██╗██╔══╝  
██║  ██║╚██████╔╝██████╔╝██████╔╝╚██████╗██║  ██╗╚██████╔╝██║  ██║██████╔╝███████╗
╚═╝  ╚═╝ ╚═════╝ ╚═════╝ ╚═════╝  ╚═════╝╚═╝  ╚═╝ ╚═════╝ ╚═╝  ╚═╝╚═════╝ ╚══════╝</pre>

    <div class="name">Rubén Martínez Agramunt <span class="cursor"></span></div>
    <div class="tagline">
      <span class="tag">Backend Engineer</span>
      <span class="tag">Security-Minded</span>
      <span class="tag">Built from Scratch</span>
    </div>
    <div class="motto"><span>_</span> I don't build features. I build systems.</div>
  </div>

  <!-- WHOAMI -->
  <div class="section">
    <div class="section-label">whoami</div>
    <div class="prose" style="margin-bottom: 20px;">
      Started in a bedroom — Linux installs, broken configs, shell scripts nobody asked for.<br>
      That obsession with <strong>how things actually work</strong> never left. It evolved into something disciplined.
    </div>
    <div class="code-block">
<span class="var">focus</span> <span class="kw">=</span> <span class="bracket">[</span>
    <span class="str">"backend architecture"</span><span class="comment">,        # not just REST endpoints</span>
    <span class="str">"secure system design"</span><span class="comment">,         # threat models, not afterthoughts</span>
    <span class="str">"infrastructure fundamentals"</span><span class="comment">,  # what runs beneath the code</span>
    <span class="str">"understanding systems under the hood"</span><span class="comment">,</span>
<span class="bracket">]</span>

<span class="comment"># No cargo-culting. No copy-paste engineering. No magic I can't explain.</span>
    </div>
  </div>

  <!-- CURRENT FOCUS -->
  <div class="section">
    <div class="section-label">current_focus</div>
    <div class="code-block" style="margin-bottom: 16px; padding: 10px 20px; font-size: 12px; color: var(--muted);">
      $ cat active_learning.txt
    </div>
    <div class="focus-list">
      <div class="focus-item">
        <div class="focus-icon">🧱</div>
        <div class="focus-text">
          <strong>Secure REST API Design</strong>
          <span>Structure, auth patterns, error boundaries — built right, not bolted on</span>
        </div>
      </div>
      <div class="focus-item">
        <div class="focus-icon">🔐</div>
        <div class="focus-text">
          <strong>Security-First Backend Patterns</strong>
          <span>From the ground up, not retrofitted</span>
        </div>
      </div>
      <div class="focus-item">
        <div class="focus-icon">🐳</div>
        <div class="focus-text">
          <strong>Docker & Containerization</strong>
          <span>Reproducibility by default — if it doesn't run in a container, it doesn't ship</span>
        </div>
      </div>
      <div class="focus-item">
        <div class="focus-icon">📖</div>
        <div class="focus-text">
          <strong>OWASP Top 10 & Real Attack Surfaces</strong>
          <span>Reading the threat landscape, not the marketing deck</span>
        </div>
      </div>
      <div class="focus-item">
        <div class="focus-icon">🧪</div>
        <div class="focus-text">
          <strong>Testable, Readable, Lasting Code</strong>
          <span>Written for the engineer who inherits it at 2am</span>
        </div>
      </div>
    </div>
  </div>

  <!-- TECH STACK -->
  <div class="section">
    <div class="section-label">tech_stack.json</div>
    
    <div class="tech-group">
      <div class="tech-group-label">// Languages</div>
      <div class="tech-pills">
        <div class="pill"><span class="dot" style="background:#3776AB"></span>Python</div>
        <div class="pill"><span class="dot" style="background:#F7DF1E"></span>JavaScript</div>
        <div class="pill"><span class="dot" style="background:#A8B9CC"></span>C</div>
        <div class="pill"><span class="dot" style="background:#ED8B00"></span>Java</div>
      </div>
    </div>

    <div class="tech-group">
      <div class="tech-group-label">// Backend</div>
      <div class="tech-pills">
        <div class="pill"><span class="dot" style="background:#092E20"></span>Django</div>
        <div class="pill"><span class="dot" style="background:#336791"></span>PostgreSQL</div>
        <div class="pill"><span class="dot" style="background:#00ff9d"></span>REST API</div>
      </div>
    </div>

    <div class="tech-group">
      <div class="tech-group-label">// Infrastructure</div>
      <div class="tech-pills">
        <div class="pill"><span class="dot" style="background:#2496ED"></span>Docker</div>
        <div class="pill"><span class="dot" style="background:#FCC624"></span>Linux</div>
        <div class="pill"><span class="dot" style="background:#F05032"></span>Git</div>
      </div>
    </div>
  </div>

  <!-- PRINCIPLES -->
  <div class="section">
    <div class="section-label">principles.txt</div>
    <div class="principles-grid">
      <div class="principle">
        <div class="principle-num">01 //</div>
        <div class="principle-title">Understand before you use</div>
        <div class="principle-desc">If you can't explain why a tool exists, you don't own the decision to use it.</div>
      </div>
      <div class="principle">
        <div class="principle-num">02 //</div>
        <div class="principle-title">Security is architecture, not a feature</div>
        <div class="principle-desc">Threat modeling before line one. Not a checklist at the end.</div>
      </div>
      <div class="principle">
        <div class="principle-num">03 //</div>
        <div class="principle-title">Boring is a compliment</div>
        <div class="principle-desc">Elegant systems are invisible. The best code is the one nobody has to touch.</div>
      </div>
      <div class="principle">
        <div class="principle-num">04 //</div>
        <div class="principle-title">Own the whole stack</div>
        <div class="principle-desc">From TCP handshake to HTTP response. No layer is someone else's problem.</div>
      </div>
    </div>
  </div>

</div>

<!-- STATUS BAR -->
<div class="status-bar">
  <span><span class="blink-dot"></span>SYSTEM ONLINE</span>
  <span>ruben-martinez-agramunt · backend · security · infrastructure</span>
  <span>ES/UTC+1</span>
</div>

<script>
  // Subtle typewriter on motto
  const motto = document.querySelector('.motto');
  motto.style.opacity = '0';
  setTimeout(() => {
    motto.style.transition = 'opacity 0.6s';
    motto.style.opacity = '1';
  }, 800);
</script>

</body>
</html>
```
[1] Simplicity over hype         → complexity is a liability
[2] Security by design           → not bolted on after
[3] Clean, maintainable code     → future-you will thank present-you
[4] Understanding > abstraction  → know what the framework hides
```

> *"The best code is code you can reason about at 2am under pressure."*
