<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sai Revu — Frontend Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050a0e;
    --surface: #0d1821;
    --border: #1a2d3d;
    --accent: #00f5c4;
    --accent2: #ff6b35;
    --accent3: #7c3aed;
    --text: #e2eaf0;
    --muted: #4a6175;
    --card: #0a1520;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.15s ease;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1.5px solid var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9998;
    opacity: 0.5;
    transition: all 0.25s ease;
  }

  /* Grid background */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,245,196,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,245,196,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    z-index: 0;
    pointer-events: none;
  }

  /* Animated orbs */
  .orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(80px);
    opacity: 0.12;
    pointer-events: none;
    animation: float 8s ease-in-out infinite;
  }
  .orb-1 { width: 500px; height: 500px; background: var(--accent); top: -200px; right: -100px; animation-delay: 0s; }
  .orb-2 { width: 400px; height: 400px; background: var(--accent3); bottom: 0; left: -150px; animation-delay: -3s; }
  .orb-3 { width: 300px; height: 300px; background: var(--accent2); top: 50%; left: 40%; animation-delay: -6s; }

  @keyframes float {
    0%, 100% { transform: translateY(0) scale(1); }
    50% { transform: translateY(-30px) scale(1.05); }
  }

  /* Layout */
  .container {
    max-width: 900px;
    margin: 0 auto;
    padding: 0 24px;
    position: relative;
    z-index: 1;
  }

  /* Hero */
  .hero {
    padding: 100px 0 60px;
    position: relative;
  }

  .hero-tag {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 20px;
    opacity: 0;
    animation: fadeUp 0.6s ease 0.2s forwards;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .hero-tag::before {
    content: '';
    width: 30px; height: 1px;
    background: var(--accent);
  }

  .hero h1 {
    font-size: clamp(52px, 8vw, 88px);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -3px;
    opacity: 0;
    animation: fadeUp 0.7s ease 0.35s forwards;
  }
  .hero h1 span { color: var(--accent); }
  .hero h1 .outline {
    -webkit-text-stroke: 1.5px var(--text);
    color: transparent;
  }

  .hero-sub {
    margin-top: 28px;
    font-family: 'Space Mono', monospace;
    font-size: 13px;
    color: var(--muted);
    max-width: 500px;
    line-height: 1.8;
    opacity: 0;
    animation: fadeUp 0.7s ease 0.5s forwards;
  }

  .hero-actions {
    margin-top: 40px;
    display: flex;
    gap: 14px;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.7s ease 0.65s forwards;
  }

  .btn {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 12px 24px;
    border-radius: 2px;
    text-decoration: none;
    transition: all 0.3s ease;
    cursor: none;
  }
  .btn-primary {
    background: var(--accent);
    color: var(--bg);
    border: 1px solid var(--accent);
  }
  .btn-primary:hover {
    background: transparent;
    color: var(--accent);
    box-shadow: 0 0 20px rgba(0,245,196,0.3);
  }
  .btn-outline {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
  }
  .btn-outline:hover {
    border-color: var(--accent);
    color: var(--accent);
  }

  /* Status bar */
  .status-bar {
    margin-top: 50px;
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    padding: 16px 0;
    display: flex;
    gap: 40px;
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    opacity: 0;
    animation: fadeUp 0.7s ease 0.8s forwards;
    overflow-x: auto;
    white-space: nowrap;
  }
  .status-item { display: flex; align-items: center; gap: 8px; }
  .dot {
    width: 6px; height: 6px;
    background: var(--accent);
    border-radius: 50%;
    animation: pulse 2s ease infinite;
    flex-shrink: 0;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; box-shadow: 0 0 0 0 rgba(0,245,196,0.4); }
    50% { opacity: 0.7; box-shadow: 0 0 0 6px rgba(0,245,196,0); }
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* Sections */
  section { padding: 80px 0; }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .section-title {
    font-size: clamp(30px, 4vw, 42px);
    font-weight: 800;
    letter-spacing: -1.5px;
    margin-bottom: 40px;
  }

  /* Code block */
  .code-block {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 28px;
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    line-height: 2;
    position: relative;
    overflow: hidden;
  }
  .code-block::before {
    content: '● ● ●';
    position: absolute;
    top: 12px; left: 16px;
    font-size: 10px;
    letter-spacing: 4px;
    color: var(--muted);
  }
  .code-block .lines {
    margin-top: 20px;
  }
  .kw { color: var(--accent3); }
  .str { color: var(--accent2); }
  .prop { color: var(--accent); }
  .cm { color: var(--muted); font-style: italic; }
  .arr { color: #f0c040; }

  /* Skills grid */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }
  .skill-cat {
    background: var(--card);
    padding: 28px;
    transition: background 0.3s ease;
  }
  .skill-cat:hover { background: var(--surface); }
  .skill-cat-title {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 18px;
    display: flex; align-items: center; gap: 8px;
  }
  .skills-list {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }
  .skill-tag {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    padding: 5px 10px;
    border: 1px solid var(--border);
    border-radius: 2px;
    color: var(--text);
    transition: all 0.25s ease;
    letter-spacing: 1px;
  }
  .skill-tag:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(0,245,196,0.05);
  }

  /* Projects */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }
  .project-card {
    background: var(--card);
    padding: 36px;
    position: relative;
    overflow: hidden;
    transition: background 0.3s ease;
    cursor: none;
  }
  .project-card::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent3));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s ease;
  }
  .project-card:hover::after { transform: scaleX(1); }
  .project-card:hover { background: var(--surface); }

  .project-num {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 3px;
    margin-bottom: 16px;
  }
  .project-title {
    font-size: 22px;
    font-weight: 800;
    letter-spacing: -0.5px;
    margin-bottom: 8px;
  }
  .project-desc {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    line-height: 1.8;
    margin-bottom: 20px;
  }
  .project-features {
    display: flex;
    flex-direction: column;
    gap: 6px;
    margin-bottom: 24px;
  }
  .feature {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--text);
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .feature::before {
    content: '→';
    color: var(--accent);
    font-size: 10px;
  }
  .project-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }
  .p-tag {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 1.5px;
    padding: 3px 8px;
    background: rgba(0,245,196,0.07);
    border: 1px solid rgba(0,245,196,0.2);
    color: var(--accent);
    border-radius: 2px;
  }

  /* Stats */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }
  .stat {
    background: var(--card);
    padding: 28px;
    text-align: center;
    transition: background 0.3s ease;
  }
  .stat:hover { background: var(--surface); }
  .stat-num {
    font-size: 40px;
    font-weight: 800;
    letter-spacing: -2px;
    color: var(--accent);
    line-height: 1;
    margin-bottom: 6px;
  }
  .stat-label {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--muted);
  }

  /* Goals */
  .goals-list {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }
  .goal-item {
    border: 1px solid var(--border);
    padding: 18px 24px;
    display: flex;
    align-items: center;
    gap: 16px;
    transition: all 0.3s ease;
    background: var(--card);
    cursor: none;
  }
  .goal-item:first-child { border-radius: 4px 4px 0 0; }
  .goal-item:last-child { border-radius: 0 0 4px 4px; border-top: none; }
  .goal-item + .goal-item { border-top: none; }
  .goal-item:hover {
    background: var(--surface);
    padding-left: 32px;
    border-color: var(--accent);
  }
  .goal-plus {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--accent);
    flex-shrink: 0;
  }
  .goal-text {
    font-size: 14px;
    font-weight: 600;
    letter-spacing: -0.3px;
  }

  /* Socials */
  .socials-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
  }
  .social-link {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 12px 20px;
    border: 1px solid var(--border);
    color: var(--muted);
    text-decoration: none;
    border-radius: 2px;
    transition: all 0.3s ease;
    cursor: none;
  }
  .social-link:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(0,245,196,0.05);
    transform: translateY(-2px);
  }

  /* Quote */
  .quote-block {
    border-left: 2px solid var(--accent);
    padding: 24px 32px;
    background: var(--card);
    border-radius: 0 4px 4px 0;
    font-size: 18px;
    font-weight: 700;
    letter-spacing: -0.5px;
    font-style: italic;
    color: var(--text);
    line-height: 1.5;
  }
  .quote-attr {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 2px;
    margin-top: 12px;
  }

  /* Footer */
  footer {
    border-top: 1px solid var(--border);
    padding: 40px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    flex-wrap: wrap;
    gap: 12px;
  }

  /* Scroll reveal */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.7s cubic-bezier(0.16, 1, 0.3, 1);
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* Typing effect */
  .typed::after {
    content: '|';
    color: var(--accent);
    animation: blink 1s step-end infinite;
  }
  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  /* Noise overlay */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    opacity: 0.025;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 200px;
    pointer-events: none;
    z-index: 999;
  }

  @media (max-width: 640px) {
    .projects-grid { grid-template-columns: 1fr; }
    .status-bar { gap: 20px; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="orb orb-3"></div>

<div class="container">

  <!-- Hero -->
  <section class="hero">
    <div class="hero-tag">Frontend Developer · Hyderabad, India</div>
    <h1>
      Sai<br>
      <span>Revu</span><br>
      <span class="outline">Dev</span>
    </h1>
    <p class="hero-sub">
      // MERN Stack Enthusiast · Problem Solver · Clean Code Advocate<br>
      Building scalable products that look great & perform even better.
    </p>
    <div class="hero-actions">
      <a href="mailto:sairevu03@gmail.com" class="btn btn-primary">Get In Touch</a>
      <a href="https://sai-revu-portfolio.netlify.app/" target="_blank" class="btn btn-outline">View Portfolio</a>
      <a href="https://github.com/saiakhil145" target="_blank" class="btn btn-outline">GitHub</a>
    </div>
    <div class="status-bar">
      <div class="status-item"><div class="dot"></div> Available for opportunities</div>
      <div class="status-item">📍 Hyderabad, India</div>
      <div class="status-item">🎯 SDE Role @ Product Company</div>
      <div class="status-item">⚡ MERN Stack</div>
    </div>
  </section>

  <!-- About -->
  <section class="reveal">
    <div class="section-label">01 · About</div>
    <h2 class="section-title">Who I Am</h2>
    <div class="code-block">
      <div class="lines">
        <div><span class="kw">const</span> <span class="prop">saiRevu</span> = {</div>
        <div>&nbsp;&nbsp;<span class="prop">location</span>: <span class="str">"Hyderabad, India 🇮🇳"</span>,</div>
        <div>&nbsp;&nbsp;<span class="prop">role</span>: <span class="str">"Frontend Developer"</span>,</div>
        <div>&nbsp;&nbsp;<span class="prop">currentFocus</span>: <span class="arr">[</span><span class="str">"React.js"</span>, <span class="str">"Redux Toolkit"</span>, <span class="str">"MERN Stack"</span><span class="arr">]</span>,</div>
        <div>&nbsp;&nbsp;<span class="prop">passionateAbout</span>: <span class="arr">[</span><span class="str">"Clean Code"</span>, <span class="str">"Performance"</span>, <span class="str">"UX"</span><span class="arr">]</span>,</div>
        <div>&nbsp;&nbsp;<span class="prop">askMeAbout</span>: <span class="arr">[</span><span class="str">"Web Dev"</span>, <span class="str">"JavaScript"</span>, <span class="str">"DSA"</span>, <span class="str">"System Design"</span><span class="arr">]</span>,</div>
        <div>&nbsp;&nbsp;<span class="prop">funFact</span>: <span class="str">"I debug with console.log() and I'm not ashamed! 😄"</span></div>
        <div>};</div>
        <br>
        <div><span class="cm">// Currently working on Full-Stack MERN Projects</span></div>
        <div><span class="cm">// Exploring System Design & Scalability</span></div>
        <div><span class="cm">// Daily DSA Practice → LeetCode 300+ solved</span></div>
      </div>
    </div>
  </section>

  <!-- Stats -->
  <section class="reveal">
    <div class="section-label">02 · Numbers</div>
    <h2 class="section-title">At a Glance</h2>
    <div class="stats-row">
      <div class="stat">
        <div class="stat-num">300+</div>
        <div class="stat-label">LeetCode<br>Problems</div>
      </div>
      <div class="stat">
        <div class="stat-num">5+</div>
        <div class="stat-label">Full-Stack<br>Projects</div>
      </div>
      <div class="stat">
        <div class="stat-num">200+</div>
        <div class="stat-label">GitHub<br>Commits</div>
      </div>
      <div class="stat">
        <div class="stat-num">⭐5</div>
        <div class="stat-label">HackerRank<br>Java & JS</div>
      </div>
    </div>
  </section>

  <!-- Skills -->
  <section class="reveal">
    <div class="section-label">03 · Stack</div>
    <h2 class="section-title">Tech Arsenal</h2>
    <div class="skills-grid">
      <div class="skill-cat">
        <div class="skill-cat-title">✨ Frontend Magic</div>
        <div class="skills-list">
          <span class="skill-tag">HTML5</span>
          <span class="skill-tag">CSS3</span>
          <span class="skill-tag">JavaScript</span>
          <span class="skill-tag">React.js</span>
          <span class="skill-tag">Redux Toolkit</span>
          <span class="skill-tag">Tailwind CSS</span>
          <span class="skill-tag">Framer Motion</span>
        </div>
      </div>
      <div class="skill-cat">
        <div class="skill-cat-title">⚡ Backend Power</div>
        <div class="skills-list">
          <span class="skill-tag">Node.js</span>
          <span class="skill-tag">Express.js</span>
          <span class="skill-tag">MongoDB</span>
          <span class="skill-tag">MySQL</span>
          <span class="skill-tag">JWT Auth</span>
          <span class="skill-tag">REST APIs</span>
        </div>
      </div>
      <div class="skill-cat">
        <div class="skill-cat-title">🔧 Tools & Platforms</div>
        <div class="skills-list">
          <span class="skill-tag">Git</span>
          <span class="skill-tag">GitHub</span>
          <span class="skill-tag">Linux</span>
          <span class="skill-tag">Postman</span>
          <span class="skill-tag">AWS</span>
          <span class="skill-tag">VS Code</span>
          <span class="skill-tag">Razorpay</span>
          <span class="skill-tag">Stripe</span>
        </div>
      </div>
    </div>
  </section>

  <!-- Projects -->
  <section class="reveal">
    <div class="section-label">04 · Work</div>
    <h2 class="section-title">Featured Projects</h2>
    <div class="projects-grid">
      <div class="project-card">
        <div class="project-num">PROJECT / 01</div>
        <div class="project-title">💊 Prescripto</div>
        <div class="project-desc">Doctor Appointment System — Full-stack platform with real-time booking, role-based auth, and integrated payments.</div>
        <div class="project-features">
          <div class="feature">Razorpay Payment Integration</div>
          <div class="feature">Role-Based Authentication (JWT)</div>
          <div class="feature">Responsive, Mobile-First Design</div>
          <div class="feature">Real-time Appointment Booking</div>
        </div>
        <div class="project-tags">
          <span class="p-tag">React</span>
          <span class="p-tag">Node.js</span>
          <span class="p-tag">MongoDB</span>
          <span class="p-tag">Express</span>
          <span class="p-tag">Razorpay</span>
        </div>
      </div>
      <div class="project-card">
        <div class="project-num">PROJECT / 02</div>
        <div class="project-title">🛍️ Forever</div>
        <div class="project-desc">E-Commerce Platform — Feature-rich shopping app with smooth animations, admin dashboard, and real payment processing.</div>
        <div class="project-features">
          <div class="feature">Stripe Payment Gateway</div>
          <div class="feature">Framer Motion Animations</div>
          <div class="feature">Admin Dashboard Panel</div>
          <div class="feature">Cart & Order Management</div>
        </div>
        <div class="project-tags">
          <span class="p-tag">React</span>
          <span class="p-tag">Stripe</span>
          <span class="p-tag">Framer</span>
          <span class="p-tag">MongoDB</span>
          <span class="p-tag">Redux</span>
        </div>
      </div>
      <div class="project-card" style="border-top:1px solid var(--border);">
        <div class="project-num">COMING SOON</div>
        <div class="project-title">🤖 AI Chat App</div>
        <div class="project-desc">AI-powered real-time chat application. Exploring LLM integrations, WebSockets, and modern UX patterns.</div>
        <div class="project-features">
          <div class="feature">LLM API Integration</div>
          <div class="feature">Real-time WebSocket Messaging</div>
          <div class="feature">Multi-room Chat Architecture</div>
        </div>
        <div class="project-tags">
          <span class="p-tag">React</span>
          <span class="p-tag">Socket.io</span>
          <span class="p-tag">AI/LLM</span>
          <span class="p-tag">Node.js</span>
        </div>
      </div>
      <div class="project-card" style="border-top:1px solid var(--border);">
        <div class="project-num">COMING SOON</div>
        <div class="project-title">📱 Social Platform</div>
        <div class="project-desc">Full-featured social media application with posts, follows, feeds, and notifications — built to scale.</div>
        <div class="project-features">
          <div class="feature">Real-time Notifications</div>
          <div class="feature">Feed Algorithm</div>
          <div class="feature">Image Upload & CDN</div>
        </div>
        <div class="project-tags">
          <span class="p-tag">MERN</span>
          <span class="p-tag">Redux</span>
          <span class="p-tag">AWS S3</span>
          <span class="p-tag">Socket.io</span>
        </div>
      </div>
    </div>
  </section>

  <!-- Goals -->
  <section class="reveal">
    <div class="section-label">05 · Roadmap</div>
    <h2 class="section-title">2024 Goals</h2>
    <div class="goals-list">
      <div class="goal-item"><span class="goal-plus">+</span><span class="goal-text">Master Advanced React Patterns & Performance Optimization</span></div>
      <div class="goal-item"><span class="goal-plus">+</span><span class="goal-text">Build 5 Major Full-Stack Projects</span></div>
      <div class="goal-item"><span class="goal-plus">+</span><span class="goal-text">Contribute to Open Source Projects</span></div>
      <div class="goal-item"><span class="goal-plus">+</span><span class="goal-text">Land a SDE Role in a Product-Based Company</span></div>
      <div class="goal-item"><span class="goal-plus">+</span><span class="goal-text">Learn System Design & Microservices Architecture</span></div>
      <div class="goal-item"><span class="goal-plus">+</span><span class="goal-text">Achieve 500+ LeetCode Problems Solved</span></div>
    </div>
  </section>

  <!-- Connect -->
  <section class="reveal">
    <div class="section-label">06 · Connect</div>
    <h2 class="section-title">Let's Build Together</h2>
    <div class="socials-grid">
      <a href="https://linkedin.com/in/sai-revu" target="_blank" class="social-link">LinkedIn</a>
      <a href="https://github.com/saiakhil145" target="_blank" class="social-link">GitHub</a>
      <a href="https://leetcode.com/sairevu03" target="_blank" class="social-link">LeetCode</a>
      <a href="https://hackerrank.com/sairevu1" target="_blank" class="social-link">HackerRank</a>
      <a href="https://sai-revu-portfolio.netlify.app/" target="_blank" class="social-link">Portfolio</a>
      <a href="mailto:sairevu03@gmail.com" class="social-link">Email</a>
    </div>
  </section>

  <!-- Quote -->
  <section class="reveal">
    <div class="quote-block">
      "Code is like humor. When you have to explain it, it's bad."
      <div class="quote-attr">— Cory House · saiRevu.philosophy</div>
    </div>
  </section>

  <!-- Footer -->
  <footer>
    <span>© 2024 Sai Revu · Built with ❤️</span>
    <span>sairevu03@gmail.com</span>
    <span>⭐ Star some repos!</span>
  </footer>

</div>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx - 6 + 'px';
    cursor.style.top = my - 6 + 'px';
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx - 18 + 'px';
    ring.style.top = ry - 18 + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, .project-card, .skill-tag, .goal-item').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.transform = 'scale(2.5)';
      ring.style.transform = 'scale(1.5)';
      ring.style.opacity = '1';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.transform = 'scale(1)';
      ring.style.transform = 'scale(1)';
      ring.style.opacity = '0.5';
    });
  });

  // Scroll reveal
  const observer = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), 80);
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // Animate stat numbers
  function animateNum(el, target, suffix = '') {
    let count = 0;
    const step = target / 60;
    const timer = setInterval(() => {
      count = Math.min(count + step, target);
      el.textContent = (suffix === '⭐5' ? '⭐' : '') + (suffix === '⭐5' ? 5 : Math.floor(count)) + (target === 5 ? '' : '+');
      if (count >= target) clearInterval(timer);
    }, 16);
  }

  const statObserver = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        const nums = e.target.querySelectorAll('.stat-num');
        nums.forEach(n => {
          const txt = n.textContent;
          if (txt.includes('300')) animateNum(n, 300);
          else if (txt.includes('5+')) { let c = 0; const t = setInterval(() => { c++; n.textContent = c + '+'; if(c>=5) clearInterval(t); }, 100); }
          else if (txt.includes('200')) animateNum(n, 200);
        });
        statObserver.unobserve(e.target);
      }
    });
  }, { threshold: 0.5 });

  const statsRow = document.querySelector('.stats-row');
  if (statsRow) statObserver.observe(statsRow);
</script>
</body>
</html>
