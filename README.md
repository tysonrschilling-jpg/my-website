<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tyson Schilling — Creative Agency</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Mono:wght@300;400&family=Bebas+Neue&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --black: #0a0a0a;
    --off-black: #111111;
    --surface: #161616;
    --border: rgba(255,255,255,0.08);
    --muted: rgba(255,255,255,0.35);
    --mid: rgba(255,255,255,0.6);
    --white: #f5f2ed;
    --accent: #4f9eff;
    --accent-dim: rgba(79,158,255,0.1);
    --font-display: 'Bebas Neue', sans-serif;
    --font-serif: 'Cormorant Garamond', Georgia, serif;
    --font-mono: 'DM Mono', monospace;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: var(--font-serif);
    font-size: 18px;
    line-height: 1.6;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  #cursor {
    position: fixed;
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.15s ease, width 0.3s ease, height 0.3s ease, background 0.3s ease;
    mix-blend-mode: difference;
  }
  #cursor-ring {
    position: fixed;
    width: 36px; height: 36px;
    border: 1px solid rgba(200,185,122,0.5);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.08s ease;
  }
  body:hover #cursor { opacity: 1; }

  /* Nav */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 28px 48px;
    mix-blend-mode: difference;
  }

  .nav-logo {
    font-family: var(--font-mono);
    font-size: 13px;
    letter-spacing: 0.12em;
    color: var(--white);
    text-decoration: none;
    text-transform: uppercase;
  }

  .nav-links {
    display: flex;
    gap: 40px;
    list-style: none;
  }
  .nav-links a {
    font-family: var(--font-mono);
    font-size: 12px;
    letter-spacing: 0.1em;
    color: var(--mid);
    text-decoration: none;
    text-transform: uppercase;
    transition: color 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -2px; left: 0; right: 0;
    height: 1px;
    background: var(--accent);
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.3s ease;
  }
  .nav-links a:hover { color: var(--white); }
  .nav-links a:hover::after { transform: scaleX(1); }

  /* Hero */
  #hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 0 48px 60px;
    position: relative;
    overflow: hidden;
  }

  .hero-bg-text {
    position: absolute;
    top: 50%;
    left: -20px;
    transform: translateY(-50%);
    font-family: var(--font-display);
    font-size: clamp(180px, 28vw, 380px);
    color: rgba(255,255,255,0.025);
    pointer-events: none;
    white-space: nowrap;
    user-select: none;
    letter-spacing: -0.02em;
  }

  .hero-meta {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    width: 100%;
  }

  .hero-title {
    font-family: var(--font-display);
    font-size: clamp(72px, 12vw, 160px);
    line-height: 0.9;
    letter-spacing: 0.02em;
    color: var(--white);
    animation: fadeUp 1s ease both;
  }

  .hero-title em {
    font-style: italic;
    font-family: var(--font-serif);
    font-size: 0.55em;
    color: var(--accent);
    display: block;
    line-height: 1.2;
    letter-spacing: 0.01em;
    margin-bottom: 8px;
  }

  .hero-right {
    text-align: right;
    animation: fadeUp 1s 0.2s ease both;
  }

  .hero-tagline {
    font-family: var(--font-serif);
    font-style: italic;
    font-size: 22px;
    color: var(--mid);
    max-width: 280px;
    line-height: 1.5;
    margin-bottom: 32px;
  }

  .hero-time {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 0.15em;
    color: var(--muted);
    text-transform: uppercase;
  }

  .hero-location {
    display: flex;
    align-items: center;
    gap: 6px;
    justify-content: flex-end;
    margin-top: 4px;
  }
  .hero-location::before {
    content: '';
    display: inline-block;
    width: 6px; height: 6px;
    background: var(--accent);
    border-radius: 50%;
    animation: pulse 2s infinite;
  }

  .scroll-hint {
    position: absolute;
    bottom: 60px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    animation: fadeIn 1s 1s ease both;
  }
  .scroll-hint span {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 0.2em;
    color: var(--muted);
    text-transform: uppercase;
    writing-mode: vertical-lr;
  }
  .scroll-line {
    width: 1px;
    height: 60px;
    background: linear-gradient(to bottom, var(--muted), transparent);
    animation: scrollLine 1.5s infinite ease-in-out;
  }

  /* Marquee */
  .marquee-section {
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    padding: 18px 0;
    overflow: hidden;
    background: var(--surface);
  }
  .marquee-track {
    display: flex;
    animation: marquee 18s linear infinite;
    white-space: nowrap;
  }
  .marquee-item {
    font-family: var(--font-display);
    font-size: 15px;
    letter-spacing: 0.25em;
    color: var(--muted);
    padding: 0 48px;
    text-transform: uppercase;
    flex-shrink: 0;
  }
  .marquee-item span {
    color: var(--accent);
    margin-right: 16px;
  }

  /* Sections */
  section {
    padding: 120px 48px;
  }

  .section-label {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 0.2em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 64px;
    display: flex;
    align-items: center;
    gap: 16px;
  }
  .section-label::before {
    content: '';
    display: block;
    width: 32px;
    height: 1px;
    background: var(--accent);
  }

  /* About */
  #about {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: start;
  }
  .about-left .section-label { margin-bottom: 48px; }

  .about-statement {
    font-family: var(--font-serif);
    font-size: clamp(32px, 4vw, 52px);
    font-weight: 300;
    line-height: 1.15;
    color: var(--white);
    margin-bottom: 40px;
  }
  .about-statement em {
    font-style: italic;
    color: var(--accent);
  }

  .about-body {
    font-family: var(--font-serif);
    font-size: 19px;
    color: var(--mid);
    line-height: 1.8;
    max-width: 480px;
    margin-bottom: 48px;
  }

  .about-cta {
    display: inline-flex;
    align-items: center;
    gap: 12px;
    font-family: var(--font-mono);
    font-size: 12px;
    letter-spacing: 0.12em;
    color: var(--white);
    text-decoration: none;
    text-transform: uppercase;
    border-bottom: 1px solid var(--accent);
    padding-bottom: 4px;
    transition: gap 0.3s;
  }
  .about-cta:hover { gap: 20px; }
  .about-cta::after { content: '→'; }

  .about-stats {
    padding-top: 80px;
  }

  .stat {
    border-top: 1px solid var(--border);
    padding: 32px 0;
    display: flex;
    justify-content: space-between;
    align-items: baseline;
  }
  .stat-num {
    font-family: var(--font-display);
    font-size: 72px;
    color: var(--white);
    line-height: 1;
    letter-spacing: 0.02em;
  }
  .stat-label {
    font-family: var(--font-serif);
    font-style: italic;
    font-size: 17px;
    color: var(--muted);
    text-align: right;
    max-width: 140px;
    line-height: 1.4;
  }

  /* Projects */
  #projects {
    background: var(--off-black);
  }

  .projects-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-bottom: 80px;
  }

  .projects-title {
    font-family: var(--font-display);
    font-size: clamp(48px, 7vw, 96px);
    line-height: 0.9;
    letter-spacing: 0.02em;
  }

  .project-list {
    display: flex;
    flex-direction: column;
    gap: 0;
  }

  .project-item {
    border-top: 1px solid var(--border);
    padding: 40px 0;
    display: grid;
    grid-template-columns: 60px 1fr auto 120px;
    align-items: center;
    gap: 32px;
    cursor: none;
    transition: background 0.3s;
    position: relative;
  }
  .project-item:last-child { border-bottom: 1px solid var(--border); }
  .project-item:hover { background: var(--accent-dim); }
  .project-item:hover .project-arrow { transform: translate(4px, -4px); }

  .project-num {
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
  }

  .project-info { display: flex; flex-direction: column; gap: 6px; }

  .project-name {
    font-family: var(--font-serif);
    font-size: 28px;
    font-weight: 300;
    color: var(--white);
    letter-spacing: 0.01em;
  }

  .project-desc {
    font-family: var(--font-serif);
    font-style: italic;
    font-size: 16px;
    color: var(--muted);
  }

  .project-tags {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    justify-content: flex-end;
  }

  .tag {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 0.1em;
    color: var(--muted);
    border: 1px solid var(--border);
    padding: 4px 10px;
    text-transform: uppercase;
    border-radius: 2px;
  }

  .project-arrow {
    font-size: 20px;
    color: var(--accent);
    transition: transform 0.3s ease;
    text-align: right;
  }

  /* Contact */
  #contact {
    min-height: 80vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
    position: relative;
    overflow: hidden;
  }

  .contact-bg {
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at center, rgba(200,185,122,0.04) 0%, transparent 70%);
    pointer-events: none;
  }

  .contact-eyebrow {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 0.25em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 40px;
  }

  .contact-heading {
    font-family: var(--font-display);
    font-size: clamp(64px, 11vw, 144px);
    line-height: 0.88;
    letter-spacing: 0.02em;
    color: var(--white);
    margin-bottom: 60px;
  }
  .contact-heading em {
    font-style: italic;
    font-family: var(--font-serif);
    font-size: 0.45em;
    display: block;
    color: var(--accent);
    letter-spacing: 0.05em;
    margin-bottom: 8px;
    line-height: 1.3;
  }

  .contact-email {
    display: inline-block;
    font-family: var(--font-serif);
    font-size: clamp(18px, 3vw, 32px);
    font-style: italic;
    color: var(--mid);
    text-decoration: none;
    border-bottom: 1px solid var(--border);
    padding-bottom: 4px;
    transition: color 0.3s, border-color 0.3s;
    margin-bottom: 64px;
  }
  .contact-email:hover { color: var(--white); border-color: var(--accent); }

  .contact-socials {
    display: flex;
    justify-content: center;
    gap: 48px;
  }

  .social-link {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 0.15em;
    color: var(--muted);
    text-decoration: none;
    text-transform: uppercase;
    transition: color 0.3s;
    position: relative;
  }
  .social-link:hover { color: var(--white); }

  /* Footer */
  footer {
    border-top: 1px solid var(--border);
    padding: 32px 48px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .footer-copy {
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
  }
  .footer-back {
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    transition: color 0.3s;
  }
  .footer-back:hover { color: var(--accent); }

  /* Animations */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(40px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.6); }
  }
  @keyframes scrollLine {
    0% { transform: scaleY(1); transform-origin: top; }
    50% { transform: scaleY(0.3); transform-origin: top; }
    51% { transform: scaleY(0.3); transform-origin: bottom; }
    100% { transform: scaleY(1); transform-origin: bottom; }
  }
  @keyframes marquee {
    0% { transform: translateX(0); }
    100% { transform: translateX(-50%); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: none;
  }

  /* Noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='1'/%3E%3C/svg%3E");
    opacity: 0.018;
    pointer-events: none;
    z-index: 9000;
  }

  @media (max-width: 768px) {
    nav { padding: 24px; }
    section { padding: 80px 24px; }
    #hero { padding: 0 24px 48px; }
    #about { grid-template-columns: 1fr; gap: 48px; }
    .projects-header { flex-direction: column; gap: 24px; align-items: flex-start; }
    .project-item { grid-template-columns: 1fr; gap: 12px; }
    .project-num, .project-arrow { display: none; }
    footer { flex-direction: column; gap: 16px; text-align: center; }
    .hero-meta { flex-direction: column; gap: 32px; align-items: flex-start; }
    .hero-right { text-align: left; }
    body { cursor: auto; }
    #cursor, #cursor-ring { display: none; }
  }
</style>
</head>
<body>

<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">TS</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-bg-text">SCHILLING</div>

  <div class="scroll-hint" aria-hidden="true">
    <div class="scroll-line"></div>
    <span>Scroll</span>
  </div>

  <div class="hero-meta">
    <h1 class="hero-title">
      <em>Creative Agency</em>
      TYSON<br>SCHILLING
    </h1>
    <div class="hero-right">
      <p class="hero-tagline">Crafting digital experiences that make people stop and feel something.</p>
      <div class="hero-time">
        <div id="clock">—</div>
        <div class="hero-location">
          <span class="hero-mono" style="font-family: var(--font-mono); font-size: 11px; letter-spacing: 0.15em; color: var(--muted);">Vancouver, BC</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-section" aria-hidden="true">
  <div class="marquee-track" id="marquee">
    <span class="marquee-item"><span>✦</span> Brand Strategy</span>
    <span class="marquee-item"><span>✦</span> Web Development</span>
    <span class="marquee-item"><span>✦</span> Motion Design</span>
    <span class="marquee-item"><span>✦</span> Creative Direction</span>
    <span class="marquee-item"><span>✦</span> Digital Experiences</span>
    <span class="marquee-item"><span>✦</span> Identity Systems</span>
    <span class="marquee-item"><span>✦</span> Brand Strategy</span>
    <span class="marquee-item"><span>✦</span> Web Development</span>
    <span class="marquee-item"><span>✦</span> Motion Design</span>
    <span class="marquee-item"><span>✦</span> Creative Direction</span>
    <span class="marquee-item"><span>✦</span> Digital Experiences</span>
    <span class="marquee-item"><span>✦</span> Identity Systems</span>
  </div>
</div>

<!-- ABOUT -->
<div id="about">
  <div class="about-left reveal">
    <div class="section-label">About</div>
    <h2 class="about-statement">
      Where <em>craft</em> meets ambition — and brands find their edge.
    </h2>
    <p class="about-body">
      I'm a creative director and developer based in Vancouver. I work with brands that aren't afraid to be remembered — building digital platforms where design, motion, and code converge into something rare.
    </p>
    <a href="#contact" class="about-cta">Start a project</a>
  </div>
  <div class="about-stats reveal">
    <div class="stat">
      <span class="stat-num">40+</span>
      <span class="stat-label">Projects launched worldwide</span>
    </div>
    <div class="stat">
      <span class="stat-num">8</span>
      <span class="stat-label">Years in creative craft</span>
    </div>
    <div class="stat">
      <span class="stat-num">∞</span>
      <span class="stat-label">Obsession with the details</span>
    </div>
  </div>
</div>

<!-- PROJECTS -->
<section id="projects">
  <div class="projects-header reveal">
    <div class="section-label">Selected Work</div>
    <h2 class="projects-title">PROJECTS</h2>
  </div>
  <div class="project-list">
    <div class="project-item reveal">
      <span class="project-num">01</span>
      <div class="project-info">
        <span class="project-name">Meridian Studio</span>
        <span class="project-desc">Full brand identity & digital presence for a boutique architecture firm</span>
      </div>
      <div class="project-tags">
        <span class="tag">Branding</span>
        <span class="tag">Web</span>
      </div>
      <div class="project-arrow">↗</div>
    </div>
    <div class="project-item reveal">
      <span class="project-num">02</span>
      <div class="project-info">
        <span class="project-name">Vaulted</span>
        <span class="project-desc">E-commerce platform and motion-forward campaign for a luxury goods brand</span>
      </div>
      <div class="project-tags">
        <span class="tag">Motion</span>
        <span class="tag">Dev</span>
      </div>
      <div class="project-arrow">↗</div>
    </div>
    <div class="project-item reveal">
      <span class="project-num">03</span>
      <div class="project-info">
        <span class="project-name">North Current</span>
        <span class="project-desc">Creative direction and web build for an independent outdoor media company</span>
      </div>
      <div class="project-tags">
        <span class="tag">Direction</span>
        <span class="tag">Web</span>
      </div>
      <div class="project-arrow">↗</div>
    </div>
    <div class="project-item reveal">
      <span class="project-num">04</span>
      <div class="project-info">
        <span class="project-name">Palette Agency</span>
        <span class="project-desc">White-label development partner for a creative agency network</span>
      </div>
      <div class="project-tags">
        <span class="tag">Agency</span>
        <span class="tag">Dev</span>
      </div>
      <div class="project-arrow">↗</div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-bg"></div>
  <p class="contact-eyebrow reveal">Let's collaborate</p>
  <h2 class="contact-heading reveal">
    <em>Ready when you are</em>
    GET IN<br>TOUCH
  </h2>
  <a href="mailto:hello@tysonschilling.com" class="contact-email reveal">hello@tysonschilling.com</a>
  <div class="contact-socials reveal">
    <a href="#" class="social-link">Instagram</a>
    <a href="#" class="social-link">LinkedIn</a>
    <a href="#" class="social-link">Twitter / X</a>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <span class="footer-copy">© 2026 Tyson Schilling. All rights reserved.</span>
  <a href="#hero" class="footer-back">Back to top ↑</a>
</footer>

<script>
  // Clock
  function updateClock() {
    const el = document.getElementById('clock');
    if (!el) return;
    const now = new Date();
    const h = String(now.getHours()).padStart(2,'0');
    const m = String(now.getMinutes()).padStart(2,'0');
    const s = String(now.getSeconds()).padStart(2,'0');
    el.textContent = h + ':' + m + ':' + s;
  }
  updateClock();
  setInterval(updateClock, 1000);

  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursor-ring');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });

  function animRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animRing);
  }
  animRing();

  document.querySelectorAll('a, button, .project-item').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.width = '20px';
      cursor.style.height = '20px';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.width = '10px';
      cursor.style.height = '10px';
    });
  });

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 80);
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });
  reveals.forEach(r => observer.observe(r));

  // Nav hide/show on scroll
  let lastY = 0;
  const nav = document.querySelector('nav');
  window.addEventListener('scroll', () => {
    const y = window.scrollY;
    if (y > lastY && y > 120) {
      nav.style.transform = 'translateY(-100%)';
      nav.style.transition = 'transform 0.4s ease';
    } else {
      nav.style.transform = 'translateY(0)';
    }
    lastY = y;
  });
</script>
</body>
</html>
