<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Portfolio — Your Name</title>
  <link rel="preconnect" href="https://fonts.googleapis.com"/>
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Mono:ital,wght@0,300;0,400;0,500;1,300&family=Cormorant+Garamond:ital,wght@0,300;0,600;1,300&display=swap" rel="stylesheet"/>

  <style>
    /* ─── VARIABLES ─────────────────────────────── */
    :root {
      --bg:       #060608;
      --surface:  #0e0e12;
      --text:     #f0ece0;
      --muted:    #8a8778;
      --accent:   #d4ff00;
      --accent2:  #ff3c6e;
      --border:   rgba(240,236,224,0.1);
      --font-display: 'Bebas Neue', sans-serif;
      --font-body:    'DM Mono', monospace;
      --font-serif:   'Cormorant Garamond', serif;
    }

    /* ─── RESET ─────────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-body);
      font-size: 14px;
      line-height: 1.7;
      overflow-x: hidden;
      cursor: none;
    }
    a { color: inherit; text-decoration: none; }
    img { display: block; width: 100%; }

    /* ─── NOISE OVERLAY ─────────────────────────── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='1'/%3E%3C/svg%3E");
      opacity: 0.035;
      pointer-events: none;
      z-index: 9999;
    }

    /* ─── CUSTOM CURSOR ─────────────────────────── */
    #cursor-dot {
      position: fixed;
      width: 8px; height: 8px;
      background: var(--accent);
      border-radius: 50%;
      pointer-events: none;
      z-index: 10000;
      transform: translate(-50%, -50%);
      transition: width .15s, height .15s, background .15s;
    }
    #cursor-ring {
      position: fixed;
      width: 36px; height: 36px;
      border: 1.5px solid rgba(212,255,0,0.5);
      border-radius: 50%;
      pointer-events: none;
      z-index: 9999;
      transform: translate(-50%, -50%);
      transition: width .3s ease, height .3s ease, border-color .3s ease, transform .08s linear;
    }
    body.hovering #cursor-dot { width: 12px; height: 12px; background: var(--accent2); }
    body.hovering #cursor-ring { width: 60px; height: 60px; border-color: var(--accent2); }

    /* ─── SCROLLBAR ─────────────────────────────── */
    ::-webkit-scrollbar { width: 3px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--accent); border-radius: 2px; }

    /* ─── PROGRESS BAR ──────────────────────────── */
    #progress {
      position: fixed;
      top: 0; left: 0;
      height: 2px;
      background: var(--accent);
      width: 0%;
      z-index: 9998;
      transition: width .1s linear;
    }

    /* ─── NAV ───────────────────────────────────── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.6rem 3rem;
      z-index: 900;
      mix-blend-mode: difference;
    }
    .nav-logo {
      font-family: var(--font-display);
      font-size: 1.4rem;
      letter-spacing: 0.1em;
      color: var(--text);
    }
    .nav-links { display: flex; gap: 2.5rem; list-style: none; }
    .nav-links a {
      font-size: 11px;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--text);
      position: relative;
      padding-bottom: 2px;
    }
    .nav-links a::after {
      content: '';
      position: absolute;
      bottom: -2px; left: 0;
      width: 0; height: 1px;
      background: var(--accent);
      transition: width .35s ease;
    }
    .nav-links a:hover::after { width: 100%; }

    /* ─── HERO ──────────────────────────────────── */
    #hero {
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
      padding: 0 3rem 4rem;
      position: relative;
      overflow: hidden;
    }
    .hero-bg-grid {
      position: absolute;
      inset: 0;
      background-image:
        linear-gradient(var(--border) 1px, transparent 1px),
        linear-gradient(90deg, var(--border) 1px, transparent 1px);
      background-size: 60px 60px;
      opacity: 0.4;
    }
    .hero-bg-glow {
      position: absolute;
      width: 600px; height: 600px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(212,255,0,0.07) 0%, transparent 70%);
      top: 10%; right: -100px;
      pointer-events: none;
      animation: glow-drift 8s ease-in-out infinite alternate;
    }
    @keyframes glow-drift {
      from { transform: translate(0, 0) scale(1); }
      to   { transform: translate(-60px, 40px) scale(1.1); }
    }

    .hero-tag {
      font-size: 11px;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 1.2rem;
      opacity: 0;
      animation: fade-up .8s .3s ease forwards;
    }
    .hero-name {
      font-family: var(--font-display);
      font-size: clamp(5rem, 14vw, 13rem);
      line-height: 0.9;
      letter-spacing: -0.01em;
      display: block;
      opacity: 0;
      animation: fade-up .8s .5s ease forwards;
      position: relative;
      z-index: 1;
    }
    .hero-name span.accent { color: var(--accent); }
    .hero-subtitle {
      font-family: var(--font-serif);
      font-style: italic;
      font-size: clamp(1.2rem, 2.5vw, 2rem);
      font-weight: 300;
      color: var(--muted);
      margin-top: 1.2rem;
      opacity: 0;
      animation: fade-up .8s .7s ease forwards;
    }
    .hero-bottom {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-top: 3rem;
      opacity: 0;
      animation: fade-up .8s .9s ease forwards;
    }
    .hero-scroll-hint {
      display: flex;
      align-items: center;
      gap: .8rem;
      font-size: 11px;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--muted);
    }
    .scroll-line {
      width: 40px; height: 1px;
      background: var(--muted);
      position: relative;
      overflow: hidden;
    }
    .scroll-line::after {
      content: '';
      position: absolute;
      inset: 0;
      background: var(--accent);
      transform: translateX(-100%);
      animation: slide-line 2s 1.5s ease infinite;
    }
    @keyframes slide-line {
      0%   { transform: translateX(-100%); }
      50%  { transform: translateX(0); }
      100% { transform: translateX(100%); }
    }
    .hero-location {
      font-size: 11px;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--muted);
    }
    .hero-location span { color: var(--accent2); }

    @keyframes fade-up {
      from { opacity: 0; transform: translateY(30px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ─── SECTION SHARED ────────────────────────── */
    section { padding: 7rem 3rem; }
    .section-label {
      font-size: 10px;
      letter-spacing: 0.3em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 3rem;
      display: flex;
      align-items: center;
      gap: 1rem;
    }
    .section-label::before {
      content: '';
      display: inline-block;
      width: 24px; height: 1px;
      background: var(--accent);
    }

    /* ─── REVEAL ANIMATION ──────────────────────── */
    .reveal {
      opacity: 0;
      transform: translateY(50px);
      transition: opacity .8s ease, transform .8s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }
    .reveal-delay-1 { transition-delay: .1s; }
    .reveal-delay-2 { transition-delay: .2s; }
    .reveal-delay-3 { transition-delay: .3s; }
    .reveal-delay-4 { transition-delay: .4s; }

    /* ─── ABOUT ─────────────────────────────────── */
    #about { background: var(--surface); }
    .about-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 6rem;
      align-items: center;
    }
    .about-headline {
      font-family: var(--font-display);
      font-size: clamp(3rem, 6vw, 5.5rem);
      line-height: 0.95;
      letter-spacing: 0.02em;
    }
    .about-headline em {
      font-family: var(--font-serif);
      font-style: italic;
      color: var(--muted);
      font-size: 0.7em;
    }
    .about-body {
      color: var(--muted);
      line-height: 2;
      font-size: 13px;
    }
    .about-body p + p { margin-top: 1.2rem; }
    .about-body strong { color: var(--text); font-weight: 500; }
    .about-stats {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 2rem;
      margin-top: 3rem;
    }
    .stat {
      border-top: 1px solid var(--border);
      padding-top: 1.2rem;
    }
    .stat-number {
      font-family: var(--font-display);
      font-size: 2.8rem;
      color: var(--accent);
      line-height: 1;
    }
    .stat-label {
      font-size: 11px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--muted);
      margin-top: .3rem;
    }
    .about-img-wrap {
      position: relative;
    }
    .about-img-placeholder {
      width: 100%;
      aspect-ratio: 3/4;
      background: linear-gradient(135deg, #1a1a20, #0e0e12);
      border: 1px solid var(--border);
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: var(--font-serif);
      font-style: italic;
      color: var(--muted);
      font-size: 1rem;
      position: relative;
      overflow: hidden;
    }
    .about-img-placeholder::before {
      content: '';
      position: absolute;
      inset: 0;
      background: repeating-linear-gradient(
        45deg,
        transparent, transparent 30px,
        rgba(212,255,0,0.02) 30px, rgba(212,255,0,0.02) 31px
      );
    }
    .about-img-accent {
      position: absolute;
      bottom: -15px; right: -15px;
      width: 100px; height: 100px;
      background: var(--accent);
      z-index: -1;
    }

    /* ─── PROJECTS ──────────────────────────────── */
    #projects { padding-bottom: 0; }
    .projects-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-bottom: 3rem;
    }
    .projects-title {
      font-family: var(--font-display);
      font-size: clamp(2.5rem, 5vw, 4.5rem);
      line-height: 1;
    }
    .view-all {
      font-size: 11px;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--muted);
      display: flex;
      align-items: center;
      gap: .5rem;
      transition: color .3s;
    }
    .view-all:hover { color: var(--accent); }

    /* Horizontal scroll */
    .projects-track-wrap {
      overflow-x: auto;
      overflow-y: hidden;
      padding: 2rem 3rem 4rem;
      margin: 0 -3rem;
      scrollbar-width: none;
      cursor: grab;
    }
    .projects-track-wrap:active { cursor: grabbing; }
    .projects-track-wrap::-webkit-scrollbar { display: none; }
    .projects-track {
      display: flex;
      gap: 2rem;
      width: max-content;
    }

    .project-card {
      width: 380px;
      flex-shrink: 0;
      background: var(--surface);
      border: 1px solid var(--border);
      position: relative;
      overflow: hidden;
      transition: transform .4s ease, border-color .4s ease;
    }
    .project-card:hover {
      transform: translateY(-8px);
      border-color: var(--accent);
    }
    .project-card::before {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(to bottom, transparent 40%, rgba(6,6,8,0.95));
      z-index: 1;
      pointer-events: none;
    }
    .card-thumb {
      width: 100%;
      height: 240px;
      background: linear-gradient(135deg, var(--c1), var(--c2));
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: var(--font-display);
      font-size: 5rem;
      letter-spacing: 0.05em;
      color: rgba(0,0,0,0.15);
      transition: transform .5s ease;
    }
    .project-card:hover .card-thumb { transform: scale(1.05); }
    .card-body {
      padding: 1.5rem;
      position: relative;
      z-index: 2;
    }
    .card-tags {
      display: flex;
      gap: .5rem;
      flex-wrap: wrap;
      margin-bottom: .8rem;
    }
    .tag {
      font-size: 9px;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      padding: .25rem .6rem;
      background: rgba(212,255,0,0.08);
      color: var(--accent);
      border: 1px solid rgba(212,255,0,0.2);
    }
    .card-title {
      font-family: var(--font-display);
      font-size: 1.8rem;
      letter-spacing: 0.05em;
      margin-bottom: .5rem;
    }
    .card-desc {
      font-size: 12px;
      color: var(--muted);
      line-height: 1.8;
    }
    .card-link {
      display: inline-flex;
      align-items: center;
      gap: .4rem;
      font-size: 11px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--accent);
      margin-top: 1.2rem;
      position: relative;
    }
    .card-link::after {
      content: '';
      position: absolute;
      bottom: -2px; left: 0;
      width: 100%; height: 1px;
      background: var(--accent);
      transform: scaleX(0);
      transform-origin: right;
      transition: transform .3s ease;
    }
    .project-card:hover .card-link::after {
      transform: scaleX(1);
      transform-origin: left;
    }

    /* Project card colors */
    .pc-1 { --c1: #1a2a1a; --c2: #0a3a0a; }
    .pc-2 { --c1: #2a1a1a; --c2: #3a0a0a; }
    .pc-3 { --c1: #1a1a2a; --c2: #0a0a3a; }
    .pc-4 { --c1: #2a2a1a; --c2: #3a3a0a; }

    /* ─── SKILLS ────────────────────────────────── */
    #skills { background: var(--surface); }
    .skills-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 5rem;
    }
    .skills-col-title {
      font-family: var(--font-display);
      font-size: 2rem;
      letter-spacing: 0.05em;
      margin-bottom: 2.5rem;
      color: var(--muted);
    }
    .skill-row {
      margin-bottom: 1.6rem;
    }
    .skill-meta {
      display: flex;
      justify-content: space-between;
      margin-bottom: .5rem;
      font-size: 11px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
    }
    .skill-pct { color: var(--accent); }
    .skill-bar {
      height: 2px;
      background: var(--border);
      position: relative;
      overflow: hidden;
    }
    .skill-fill {
      position: absolute;
      top: 0; left: 0; bottom: 0;
      background: var(--accent);
      width: 0;
      transition: width 1.2s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .skill-fill.animate { width: var(--w); }

    .tech-tags {
      display: flex;
      flex-wrap: wrap;
      gap: .8rem;
    }
    .tech-tag {
      font-size: 11px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: .5rem 1rem;
      border: 1px solid var(--border);
      color: var(--muted);
      transition: all .3s ease;
      position: relative;
      overflow: hidden;
    }
    .tech-tag::before {
      content: '';
      position: absolute;
      inset: 0;
      background: var(--accent);
      transform: translateX(-100%);
      transition: transform .3s ease;
      z-index: -1;
    }
    .tech-tag:hover {
      color: var(--bg);
      border-color: var(--accent);
    }
    .tech-tag:hover::before { transform: translateX(0); }

    /* ─── CONTACT ───────────────────────────────── */
    #contact {
      min-height: 80vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      position: relative;
      overflow: hidden;
    }
    .contact-bg-text {
      position: absolute;
      font-family: var(--font-display);
      font-size: clamp(8rem, 22vw, 20rem);
      color: rgba(240,236,224,0.02);
      line-height: 1;
      pointer-events: none;
      user-select: none;
      top: 50%; right: -2%;
      transform: translateY(-50%);
      white-space: nowrap;
    }
    .contact-cta {
      font-family: var(--font-display);
      font-size: clamp(3rem, 7vw, 6.5rem);
      line-height: 0.95;
      max-width: 60%;
    }
    .contact-cta em {
      font-family: var(--font-serif);
      font-style: italic;
      color: var(--muted);
    }
    .contact-links {
      display: flex;
      gap: 2rem;
      margin-top: 3.5rem;
      flex-wrap: wrap;
    }
    .contact-btn {
      display: inline-flex;
      align-items: center;
      gap: .8rem;
      font-size: 12px;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      padding: 1rem 2rem;
      border: 1px solid var(--border);
      color: var(--text);
      position: relative;
      overflow: hidden;
      transition: color .3s ease, border-color .3s ease;
    }
    .contact-btn::before {
      content: '';
      position: absolute;
      inset: 0;
      background: var(--accent);
      transform: translateY(100%);
      transition: transform .35s cubic-bezier(0.4, 0, 0.2, 1);
      z-index: -1;
    }
    .contact-btn:hover { color: var(--bg); border-color: var(--accent); }
    .contact-btn:hover::before { transform: translateY(0); }
    .contact-btn.primary { background: var(--accent); color: var(--bg); border-color: var(--accent); }
    .contact-btn.primary::before { background: var(--text); }
    .contact-btn.primary:hover { color: var(--bg); border-color: var(--text); }
    .contact-email {
      font-family: var(--font-serif);
      font-style: italic;
      font-size: clamp(1rem, 2vw, 1.5rem);
      color: var(--muted);
      margin-top: 1.5rem;
    }
    .contact-email a { color: var(--accent); border-bottom: 1px solid rgba(212,255,0,0.3); }
    .contact-email a:hover { border-bottom-color: var(--accent); }

    /* ─── FOOTER ────────────────────────────────── */
    footer {
      padding: 2rem 3rem;
      border-top: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 11px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--muted);
    }
    footer .footer-accent { color: var(--accent); }

    /* ─── RESPONSIVE ────────────────────────────── */
    @media (max-width: 768px) {
      nav { padding: 1.4rem 1.5rem; }
      .nav-links { display: none; }
      section { padding: 5rem 1.5rem; }
      #hero { padding: 0 1.5rem 3rem; }
      .about-grid { grid-template-columns: 1fr; gap: 3rem; }
      .about-img-wrap { display: none; }
      .skills-grid { grid-template-columns: 1fr; gap: 3rem; }
      .contact-cta { max-width: 100%; }
      footer { flex-direction: column; gap: 1rem; text-align: center; }
      .projects-track-wrap { padding: 2rem 1.5rem 4rem; margin: 0 -1.5rem; }
    }
  </style>
</head>
<body>

  <!-- Cursor -->
  <div id="cursor-dot"></div>
  <div id="cursor-ring"></div>

  <!-- Scroll progress -->
  <div id="progress"></div>

  <!-- ─── NAV ───────────────────────────────────── -->
  <nav>
    <div class="nav-logo">YN</div>
    <ul class="nav-links">
      <li><a href="#about">About</a></li>
      <li><a href="#projects">Work</a></li>
      <li><a href="#skills">Skills</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <!-- ─── HERO ──────────────────────────────────── -->
  <section id="hero">
    <div class="hero-bg-grid"></div>
    <div class="hero-bg-glow"></div>

    <p class="hero-tag">Available for work &nbsp;·&nbsp; Based in Sydney, AU</p>
    <span class="hero-name" id="scramble-name">YOUR<br><span class="accent">NAME</span></span>
    <p class="hero-subtitle">Cybersecurity &amp; Information Technology</p>

    <div class="hero-bottom">
      <div class="hero-scroll-hint">
        <div class="scroll-line"></div>
        Scroll to explore
      </div>
      <div class="hero-location">Currently in <span>Sydney ✦</span></div>
    </div>
  </section>

  <!-- ─── ABOUT ─────────────────────────────────── -->
  <section id="about">
    <div class="section-label">About me</div>
    <div class="about-grid">
      <div>
        <h2 class="about-headline reveal">
          BUILDING<br>
          <em>things that</em><br>
          MATTER
        </h2>
        <div class="about-stats reveal reveal-delay-2">
          <div class="stat">
            <div class="stat-number">3+</div>
            <div class="stat-label">Years experience</div>
          </div>
          <div class="stat">
            <div class="stat-number">20+</div>
            <div class="stat-label">Projects shipped</div>
          </div>
          <div class="stat">
            <div class="stat-number">12</div>
            <div class="stat-label">Happy clients</div>
          </div>
          <div class="stat">
            <div class="stat-number">∞</div>
            <div class="stat-label">Cups of coffee</div>
          </div>
        </div>
      </div>
      <div>
        <div class="about-body reveal reveal-delay-1">
          <p>
            Hey! I'm a <strong>Cybersecurity Student</strong> passionate about protecting
            and securing digital environments. I love the intersection of technology and security 
            especially in the blue team.
          </p>
          <p>
            I specialise in <strong> Networking, Cybersecurity, risk analysis and incidence response</strong>,
            with a strong eye for blue teaming. Hands on experience through Uni external platforms like TryHackMe,
            HackTheBox and LetsDefend.io strengthens my understandings and skills regarding Cybersecurity.
          </p>
        </div>
  </section>

  <!-- ─── PROJECTS ──────────────────────────────── -->
  <section id="projects">
    <div class="projects-header reveal">
      <div>
        <div class="section-label">Selected work</div>
        <h2 class="projects-title">PROJECTS</h2>
      </div>
      <a href="#" class="view-all">View all →</a>
    </div>

    <div class="projects-track-wrap" id="drag-track">
      <div class="projects-track">

        <div class="project-card pc-1 reveal">
          <div class="card-thumb">01</div>
          <div class="card-body">
            <div class="card-tags">
              <span class="tag">React</span>
              <span class="tag">Node.js</span>
              <span class="tag">Postgres</span>
            </div>
            <h3 class="card-title">PROJECT ALPHA</h3>
            <p class="card-desc">A full-stack SaaS dashboard with real-time analytics, role-based auth, and a sleek UI built in React.</p>
            <a href="#" class="card-link">View project →</a>
          </div>
        </div>

        <div class="project-card pc-2 reveal reveal-delay-1">
          <div class="card-thumb">02</div>
          <div class="card-body">
            <div class="card-tags">
              <span class="tag">Next.js</span>
              <span class="tag">Tailwind</span>
              <span class="tag">Prisma</span>
            </div>
            <h3 class="card-title">E-COMMERCE</h3>
            <p class="card-desc">A high-performance e-commerce platform with server-side rendering, optimised images, and seamless checkout.</p>
            <a href="#" class="card-link">View project →</a>
          </div>
        </div>

        <div class="project-card pc-3 reveal reveal-delay-2">
          <div class="card-thumb">03</div>
          <div class="card-body">
            <div class="card-tags">
              <span class="tag">Python</span>
              <span class="tag">ML</span>
              <span class="tag">FastAPI</span>
            </div>
            <h3 class="card-title">AI TOOL</h3>
            <p class="card-desc">A machine learning pipeline that classifies and summarises documents with 94% accuracy using a fine-tuned BERT model.</p>
            <a href="#" class="card-link">View project →</a>
          </div>
        </div>

        <div class="project-card pc-4 reveal reveal-delay-3">
          <div class="card-thumb">04</div>
          <div class="card-body">
            <div class="card-tags">
              <span class="tag">React Native</span>
              <span class="tag">Expo</span>
              <span class="tag">Firebase</span>
            </div>
            <h3 class="card-title">MOBILE APP</h3>
            <p class="card-desc">A cross-platform productivity app with offline-first sync, push notifications, and 4.8★ App Store rating.</p>
            <a href="#" class="card-link">View project →</a>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- ─── SKILLS ────────────────────────────────── -->
  <section id="skills">
    <div class="section-label">Expertise</div>
    <div class="skills-grid">
      <div class="reveal">
        <h3 class="skills-col-title">PROFICIENCY</h3>

        <div class="skill-row">
          <div class="skill-meta"><span>Frontend</span><span class="skill-pct">92%</span></div>
          <div class="skill-bar"><div class="skill-fill" style="--w:92%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span>Backend</span><span class="skill-pct">85%</span></div>
          <div class="skill-bar"><div class="skill-fill" style="--w:85%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span>UI / UX Design</span><span class="skill-pct">78%</span></div>
          <div class="skill-bar"><div class="skill-fill" style="--w:78%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span>DevOps / Cloud</span><span class="skill-pct">70%</span></div>
          <div class="skill-bar"><div class="skill-fill" style="--w:70%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span>Machine Learning</span><span class="skill-pct">65%</span></div>
          <div class="skill-bar"><div class="skill-fill" style="--w:65%"></div></div>
        </div>
      </div>

      <div class="reveal reveal-delay-2">
        <h3 class="skills-col-title">TECHNOLOGIES</h3>
        <div class="tech-tags">
          <span class="tech-tag">JavaScript</span>
          <span class="tech-tag">TypeScript</span>
          <span class="tech-tag">Python</span>
          <span class="tech-tag">React</span>
          <span class="tech-tag">Next.js</span>
          <span class="tech-tag">Node.js</span>
          <span class="tech-tag">PostgreSQL</span>
          <span class="tech-tag">MongoDB</span>
          <span class="tech-tag">Docker</span>
          <span class="tech-tag">AWS</span>
          <span class="tech-tag">Git</span>
          <span class="tech-tag">Figma</span>
          <span class="tech-tag">GraphQL</span>
          <span class="tech-tag">Redis</span>
          <span class="tech-tag">Tailwind</span>
        </div>
      </div>
    </div>
  </section>

  <!-- ─── CONTACT ───────────────────────────────── -->
  <section id="contact">
    <div class="contact-bg-text">HELLO</div>
    <div class="section-label">Get in touch</div>
    <h2 class="contact-cta reveal">
      LET'S BUILD<br>
      <em>something</em><br>
      TOGETHER
    </h2>
    <p class="contact-email reveal reveal-delay-1">
      Drop me a line at <a href="mailto:hello@yourname.com">hello@yourname.com</a>
    </p>
    <div class="contact-links reveal reveal-delay-2">
      <a href="mailto:hello@yourname.com" class="contact-btn primary">Say hello →</a>
      <a href="https://github.com/yourusername" class="contact-btn">GitHub</a>
      <a href="https://linkedin.com/in/yourusername" class="contact-btn">LinkedIn</a>
      <a href="#" class="contact-btn">Download CV</a>
    </div>
  </section>

  <!-- ─── FOOTER ────────────────────────────────── -->
  <footer>
    <div>© 2026 <span class="footer-accent">Your Name</span> — All rights reserved</div>
    <div>Built with <span class="footer-accent">❤</span> &amp; pure HTML/CSS</div>
  </footer>

  <!-- ─── SCRIPTS ──────────────────────────────── -->
  <script>
    /* ── Custom cursor ────────────────────────── */
    const dot  = document.getElementById('cursor-dot');
    const ring = document.getElementById('cursor-ring');
    let mx = 0, my = 0, rx = 0, ry = 0;

    document.addEventListener('mousemove', e => {
      mx = e.clientX; my = e.clientY;
      dot.style.left  = mx + 'px';
      dot.style.top   = my + 'px';
    });

    (function animRing() {
      rx += (mx - rx) * 0.12;
      ry += (my - ry) * 0.12;
      ring.style.left = rx + 'px';
      ring.style.top  = ry + 'px';
      requestAnimationFrame(animRing);
    })();

    document.querySelectorAll('a, button, .project-card, .tech-tag, .contact-btn')
      .forEach(el => {
        el.addEventListener('mouseenter', () => document.body.classList.add('hovering'));
        el.addEventListener('mouseleave', () => document.body.classList.remove('hovering'));
      });

    /* ── Scroll progress bar ──────────────────── */
    const prog = document.getElementById('progress');
    window.addEventListener('scroll', () => {
      const pct = window.scrollY / (document.body.scrollHeight - window.innerHeight) * 100;
      prog.style.width = pct + '%';
    });

    /* ── Scroll reveal ────────────────────────── */
    const reveals = document.querySelectorAll('.reveal');
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          e.target.classList.add('visible');
          // Animate skill bars when visible
          e.target.querySelectorAll('.skill-fill').forEach(bar => bar.classList.add('animate'));
        }
      });
    }, { threshold: 0.15 });
    reveals.forEach(el => observer.observe(el));

    /* Also observe skill fills in skills section directly */
    const skillObs = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) e.target.classList.add('animate');
      });
    }, { threshold: 0.5 });
    document.querySelectorAll('.skill-fill').forEach(el => skillObs.observe(el));

    /* ── Text scramble on hero name ───────────── */
    const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%&';
    const target = document.getElementById('scramble-name');
    const originalHTML = target.innerHTML;
    const originalText = 'YOUR\nNAME'; // Change to your name

    function scramble(el, text, duration = 1200) {
      let frame = 0;
      const totalFrames = duration / 16;
      const lines = text.split('\n');

      const raf = setInterval(() => {
        frame++;
        const progress = frame / totalFrames;

        let result = '';
        lines.forEach((line, li) => {
          if (li > 0) result += '<br>';
          if (li === 1) result += '<span class="accent">';
          line.split('').forEach((char, i) => {
            const charProgress = Math.max(0, (progress * lines.join('').length - i) / 1.5);
            if (charProgress >= 1) {
              result += char;
            } else if (charProgress > 0) {
              result += chars[Math.floor(Math.random() * chars.length)];
            } else {
              result += chars[Math.floor(Math.random() * chars.length)];
            }
          });
          if (li === 1) result += '</span>';
        });

        el.innerHTML = result;
        if (frame >= totalFrames) {
          clearInterval(raf);
          el.innerHTML = originalHTML;
        }
      }, 16);
    }

    // Run on load
    setTimeout(() => scramble(target, originalText, 1400), 600);

    // Re-run on hover
    target.addEventListener('mouseenter', () => scramble(target, originalText, 900));

    /* ── Drag to scroll (projects) ────────────── */
    const track = document.getElementById('drag-track');
    let isDown = false, startX, scrollLeft;

    track.addEventListener('mousedown', e => {
      isDown = true;
      track.style.cursor = 'grabbing';
      startX = e.pageX - track.offsetLeft;
      scrollLeft = track.scrollLeft;
    });
    track.addEventListener('mouseleave', () => { isDown = false; track.style.cursor = 'grab'; });
    track.addEventListener('mouseup',    () => { isDown = false; track.style.cursor = 'grab'; });
    track.addEventListener('mousemove',  e => {
      if (!isDown) return;
      e.preventDefault();
      const x = e.pageX - track.offsetLeft;
      track.scrollLeft = scrollLeft - (x - startX) * 1.5;
    });

    /* ── Parallax on hero glow ────────────────── */
    const glow = document.querySelector('.hero-bg-glow');
    document.addEventListener('mousemove', e => {
      const xPct = (e.clientX / window.innerWidth  - 0.5) * 40;
      const yPct = (e.clientY / window.innerHeight - 0.5) * 40;
      glow.style.transform = `translate(${xPct}px, ${yPct}px)`;
    });

    /* ── Tilt on project cards ────────────────── */
    document.querySelectorAll('.project-card').forEach(card => {
      card.addEventListener('mousemove', e => {
        const rect = card.getBoundingClientRect();
        const x = (e.clientX - rect.left) / rect.width  - 0.5;
        const y = (e.clientY - rect.top)  / rect.height - 0.5;
        card.style.transform = `
          perspective(600px)
          rotateY(${x * 12}deg)
          rotateX(${-y * 12}deg)
          translateY(-8px)
        `;
      });
      card.addEventListener('mouseleave', () => {
        card.style.transform = '';
        card.style.transition = 'transform .5s ease';
      });
      card.addEventListener('mouseenter', () => {
        card.style.transition = 'transform .1s ease';
      });
    });
  </script>
</body>
</html>
