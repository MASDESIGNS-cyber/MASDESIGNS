<!DOCTYPE html>

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>MAS Designer — Web Design Studio</title>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }


:root {
  --black: #0a0a0a;
  --white: #f5f2ec;
  --accent: #ff3c1f;
  --mid: #1a1a1a;
  --muted: #555;
}

html { scroll-behavior: smooth; }

body {
  background: var(--black);
  color: var(--white);
  font-family: 'DM Sans', sans-serif;
  font-weight: 300;
  overflow-x: hidden;
  cursor: none;
}

/* Custom cursor */
.cursor {
  position: fixed;
  width: 12px; height: 12px;
  background: var(--accent);
  border-radius: 50%;
  pointer-events: none;
  z-index: 9999;
  transform: translate(-50%, -50%);
  transition: transform 0.1s, width 0.2s, height 0.2s;
}
.cursor-ring {
  position: fixed;
  width: 36px; height: 36px;
  border: 1px solid rgba(255,60,31,0.5);
  border-radius: 50%;
  pointer-events: none;
  z-index: 9998;
  transform: translate(-50%, -50%);
  transition: all 0.12s ease;
}
body:hover .cursor { opacity: 1; }

/* NAV */
nav {
  position: fixed; top: 0; left: 0; right: 0;
  display: flex; align-items: center; justify-content: space-between;
  padding: 28px 60px;
  z-index: 100;
  mix-blend-mode: normal;
}
.nav-logo {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 1.6rem;
  letter-spacing: 0.12em;
  color: var(--white);
  text-decoration: none;
}
.nav-logo span { color: var(--accent); }
.nav-links { display: flex; gap: 40px; list-style: none; }
.nav-links a {
  color: var(--white);
  text-decoration: none;
  font-size: 0.78rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  opacity: 0.6;
  transition: opacity 0.2s;
}
.nav-links a:hover { opacity: 1; }

/* HERO */
.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: 0 60px 80px;
  position: relative;
  overflow: hidden;
}
.hero-bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(ellipse 80% 60% at 70% 40%, #1c0f0a 0%, var(--black) 60%);
}
.hero-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255,60,31,0.06) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,60,31,0.06) 1px, transparent 1px);
  background-size: 80px 80px;
  mask-image: radial-gradient(ellipse 90% 80% at 60% 30%, black 30%, transparent 80%);
}
.hero-number {
  position: absolute;
  right: -40px; top: 50%;
  transform: translateY(-50%) rotate(90deg);
  font-family: 'Bebas Neue', sans-serif;
  font-size: 22vw;
  color: rgba(255,255,255,0.025);
  white-space: nowrap;
  letter-spacing: 0.05em;
  user-select: none;
}
.hero-tag {
  font-size: 0.72rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 28px;
  opacity: 0;
  animation: fadeUp 0.8s 0.2s forwards;
}
.hero-headline {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(5rem, 13vw, 13rem);
  line-height: 0.92;
  letter-spacing: -0.01em;
  position: relative;
  z-index: 2;
  opacity: 0;
  animation: fadeUp 0.8s 0.4s forwards;
}
.hero-headline .line-accent { color: var(--accent); }
.hero-headline .line-outline {
  -webkit-text-stroke: 1px rgba(245,242,236,0.3);
  color: transparent;
}
.hero-sub {
  margin-top: 36px;
  max-width: 380px;
  font-size: 0.95rem;
  line-height: 1.8;
  opacity: 0;
  animation: fadeUp 0.8s 0.6s forwards;
  color: rgba(245,242,236,0.55);
  position: relative; z-index: 2;
}
.hero-cta {
  margin-top: 52px;
  display: flex; align-items: center; gap: 32px;
  opacity: 0;
  animation: fadeUp 0.8s 0.8s forwards;
  position: relative; z-index: 2;
}
.btn-primary {
  display: inline-flex; align-items: center; gap: 12px;
  background: var(--accent);
  color: var(--white);
  text-decoration: none;
  font-size: 0.8rem;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  padding: 18px 40px;
  transition: background 0.2s, transform 0.2s;
}
.btn-primary:hover { background: #e02a10; transform: translateY(-2px); }
.btn-ghost {
  font-size: 0.78rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: rgba(245,242,236,0.5);
  text-decoration: none;
  border-bottom: 1px solid rgba(245,242,236,0.2);
  padding-bottom: 2px;
  transition: color 0.2s, border-color 0.2s;
}
.btn-ghost:hover { color: var(--white); border-color: var(--white); }

/* MARQUEE */
.marquee-wrap {
  border-top: 1px solid rgba(245,242,236,0.08);
  border-bottom: 1px solid rgba(245,242,236,0.08);
  overflow: hidden;
  padding: 18px 0;
  background: var(--mid);
}
.marquee-track {
  display: flex;
  gap: 60px;
  animation: marquee 18s linear infinite;
  white-space: nowrap;
}
.marquee-item {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 1.1rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: rgba(245,242,236,0.4);
  flex-shrink: 0;
}
.marquee-item span { color: var(--accent); margin: 0 28px; }
@keyframes marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }

/* SERVICES */
section { padding: 120px 60px; }
.section-label {
  font-size: 0.7rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 20px;
  display: flex; align-items: center; gap: 14px;
}
.section-label::before {
  content: '';
  display: block;
  width: 30px; height: 1px;
  background: var(--accent);
}
.section-title {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(3rem, 6vw, 6rem);
  line-height: 1;
  margin-bottom: 80px;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2px;
}
.service-card {
  background: var(--mid);
  padding: 50px 40px;
  border-top: 3px solid transparent;
  transition: border-color 0.3s, background 0.3s, transform 0.3s;
  position: relative;
  overflow: hidden;
}
.service-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 30% 30%, rgba(255,60,31,0.08) 0%, transparent 60%);
  opacity: 0;
  transition: opacity 0.3s;
}
.service-card:hover { border-color: var(--accent); background: #1f1f1f; transform: translateY(-4px); }
.service-card:hover::before { opacity: 1; }
.service-num {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 4rem;
  color: rgba(245,242,236,0.06);
  line-height: 1;
  margin-bottom: 24px;
}
.service-icon {
  font-size: 1.6rem;
  margin-bottom: 20px;
}
.service-name {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 1.8rem;
  letter-spacing: 0.05em;
  margin-bottom: 16px;
}
.service-desc {
  font-size: 0.88rem;
  line-height: 1.8;
  color: rgba(245,242,236,0.5);
}

/* STATS */
.stats-section {
  background: var(--accent);
  padding: 80px 60px;
  display: grid;
  grid-template-columns: repeat(4,1fr);
  gap: 2px;
}
.stat-item { padding: 0 40px; border-right: 1px solid rgba(0,0,0,0.15); }
.stat-item:last-child { border-right: none; }
.stat-num {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 5rem;
  line-height: 1;
  color: var(--black);
}
.stat-label {
  font-size: 0.78rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: rgba(0,0,0,0.6);
  margin-top: 8px;
}

/* PROCESS */
.process-list { display: flex; flex-direction: column; gap: 2px; }
.process-item {
  display: grid;
  grid-template-columns: 100px 1fr 200px;
  align-items: center;
  gap: 40px;
  padding: 40px 48px;
  background: var(--mid);
  transition: background 0.2s;
  cursor: default;
}
.process-item:hover { background: #1f1f1f; }
.process-step {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 3.5rem;
  color: rgba(245,242,236,0.12);
}
.process-name {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 1.9rem;
  letter-spacing: 0.04em;
}
.process-tag {
  font-size: 0.72rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--accent);
  text-align: right;
}

/* CONTACT */
.contact-section {
  background: var(--mid);
  text-align: center;
  padding: 140px 60px;
}
.contact-section .section-label { justify-content: center; }
.contact-headline {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(4rem, 9vw, 9rem);
  line-height: 0.95;
  margin-bottom: 48px;
}
.contact-headline em {
  font-style: normal;
  -webkit-text-stroke: 1px rgba(245,242,236,0.25);
  color: transparent;
}
.contact-email {
  display: inline-block;
  font-size: 1.1rem;
  letter-spacing: 0.08em;
  color: var(--accent);
  text-decoration: none;
  border-bottom: 1px solid var(--accent);
  padding-bottom: 4px;
  margin-bottom: 60px;
  transition: opacity 0.2s;
}
.contact-email:hover { opacity: 0.7; }

/* FOOTER */
footer {
  padding: 40px 60px;
  display: flex; align-items: center; justify-content: space-between;
  border-top: 1px solid rgba(245,242,236,0.07);
  font-size: 0.75rem;
  color: rgba(245,242,236,0.3);
}
.footer-logo {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 1.3rem;
  letter-spacing: 0.1em;
}
.footer-logo span { color: var(--accent); }

/* ANIMATIONS */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}

.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.7s, transform 0.7s;
}
.reveal.visible {
  opacity: 1;
  transform: none;
}

@media (max-width: 900px) {
  nav, .hero, section { padding-left: 28px; padding-right: 28px; }
  .nav-links { display: none; }
  .hero-headline { font-size: clamp(4rem, 18vw, 8rem); }
  .services-grid { grid-template-columns: 1fr; }
  .stats-section { grid-template-columns: 1fr 1fr; padding: 60px 28px; }
  .process-item { grid-template-columns: 60px 1fr; }
  .process-tag { display: none; }
}


  </style>
</head>
<body>

  <div class="cursor" id="cursor"></div>
  <div class="cursor-ring" id="cursorRing"></div>

  <!-- NAV -->

  <nav>
    <a href="#" class="nav-logo">MAS<span>.</span></a>
    <ul class="nav-links">
      <li><a href="#services">Services</a></li>
      <li><a href="#process">Process</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <!-- HERO -->

  <section class="hero">
    <div class="hero-bg"></div>
    <div class="hero-grid"></div>
    <div class="hero-number">MAS</div>
    <p class="hero-tag">Web Design Studio</p>
    <h1 class="hero-headline">
      <div>WE BUILD</div>
      <div class="line-accent">BOLD</div>
      <div class="line-outline">WEBSITES</div>
    </h1>
    <p class="hero-sub">MAS Designer crafts high-impact digital experiences that cut through the noise — built to convert, designed to impress.</p>
    <div class="hero-cta">
      <a href="#contact" class="btn-primary">Start a Project →</a>
      <a href="#services" class="btn-ghost">See Our Work</a>
    </div>
  </section>

  <!-- MARQUEE -->

  <div class="marquee-wrap">
    <div class="marquee-track">
      <span class="marquee-item">Web Design <span>✦</span></span>
      <span class="marquee-item">UI/UX Design <span>✦</span></span>
      <span class="marquee-item">Brand Identity <span>✦</span></span>
      <span class="marquee-item">E-Commerce <span>✦</span></span>
      <span class="marquee-item">Landing Pages <span>✦</span></span>
      <span class="marquee-item">SEO Optimization <span>✦</span></span>
      <span class="marquee-item">Web Design <span>✦</span></span>
      <span class="marquee-item">UI/UX Design <span>✦</span></span>
      <span class="marquee-item">Brand Identity <span>✦</span></span>
      <span class="marquee-item">E-Commerce <span>✦</span></span>
      <span class="marquee-item">Landing Pages <span>✦</span></span>
      <span class="marquee-item">SEO Optimization <span>✦</span></span>
    </div>
  </div>

  <!-- SERVICES -->

  <section id="services">
    <div class="section-label">What We Do</div>
    <h2 class="section-title reveal">OUR<br>SERVICES</h2>
    <div class="services-grid">
      <div class="service-card reveal">
        <div class="service-num">01</div>
        <div class="service-icon">◈</div>
        <div class="service-name">Web Design</div>
        <p class="service-desc">Pixel-perfect, responsive websites that capture your brand's essence and keep visitors engaged from the first scroll.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-num">02</div>
        <div class="service-icon">◉</div>
        <div class="service-name">UI / UX</div>
        <p class="service-desc">User-first interfaces engineered for clarity and conversion. Every interaction is intentional, every flow is frictionless.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-num">03</div>
        <div class="service-icon">◫</div>
        <div class="service-name">Brand Identity</div>
        <p class="service-desc">Visual identities that make a statement — from logos and color systems to the full brand experience across every touchpoint.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-num">04</div>
        <div class="service-icon">⬡</div>
        <div class="service-name">E-Commerce</div>
        <p class="service-desc">Online stores built to sell. High-performance shops with seamless checkout flows designed to maximise revenue.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-num">05</div>
        <div class="service-icon">◭</div>
        <div class="service-name">Landing Pages</div>
        <p class="service-desc">Focused, high-converting pages for campaigns, launches, and lead generation. Speed and impact by design.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-num">06</div>
        <div class="service-icon">◬</div>
        <div class="service-name">SEO & Performance</div>
        <p class="service-desc">Sites built fast, coded clean, ranked higher. Technical SEO and performance optimisation baked in from day one.</p>
      </div>
    </div>
  </section>

  <!-- STATS -->

  <div class="stats-section">
    <div class="stat-item reveal">
      <div class="stat-num">120+</div>
      <div class="stat-label">Projects Delivered</div>
    </div>
    <div class="stat-item reveal">
      <div class="stat-num">98%</div>
      <div class="stat-label">Client Satisfaction</div>
    </div>
    <div class="stat-item reveal">
      <div class="stat-num">8+</div>
      <div class="stat-label">Years Experience</div>
    </div>
    <div class="stat-item reveal">
      <div class="stat-num">40+</div>
      <div class="stat-label">Industries Served</div>
    </div>
  </div>

  <!-- PROCESS -->

  <section id="process">
    <div class="section-label">How We Work</div>
    <h2 class="section-title reveal">THE<br>PROCESS</h2>
    <div class="process-list">
      <div class="process-item reveal">
        <div class="process-step">01</div>
        <div>
          <div class="process-name">Discovery</div>
          <p style="font-size:0.85rem;color:rgba(245,242,236,0.45);margin-top:6px;">We learn everything about your business, goals, and audience.</p>
        </div>
        <div class="process-tag">Week 1</div>
      </div>
      <div class="process-item reveal">
        <div class="process-step">02</div>
        <div>
          <div class="process-name">Strategy & Concept</div>
          <p style="font-size:0.85rem;color:rgba(245,242,236,0.45);margin-top:6px;">We define structure, flow, and the visual direction that will set you apart.</p>
        </div>
        <div class="process-tag">Week 1–2</div>
      </div>
      <div class="process-item reveal">
        <div class="process-step">03</div>
        <div>
          <div class="process-name">Design</div>
          <p style="font-size:0.85rem;color:rgba(245,242,236,0.45);margin-top:6px;">High-fidelity mockups crafted with obsessive attention to detail.</p>
        </div>
        <div class="process-tag">Week 2–3</div>
      </div>
      <div class="process-item reveal">
        <div class="process-step">04</div>
        <div>
          <div class="process-name">Build & Launch</div>
          <p style="font-size:0.85rem;color:rgba(245,242,236,0.45);margin-top:6px;">Clean code, fast load times, and a smooth handoff or full deployment.</p>
        </div>
        <div class="process-tag">Week 3–4</div>
      </div>
    </div>
  </section>

  <!-- CONTACT -->

  <section class="contact-section" id="contact">
    <div class="section-label">Get In Touch</div>
    <h2 class="contact-headline reveal">
      LET'S BUILD<br>SOMETHING <em>GREAT</em>
    </h2>
    <br>
    <a href="mailto:hello@masdesigner.com" class="contact-email">hello@masdesigner.com</a>
    <br>
    <a href="mailto:hello@masdesigner.com" class="btn-primary" style="display:inline-flex; margin-top:20px;">Start Your Project →</a>
  </section>

  <!-- FOOTER -->

  <footer>
    <div class="footer-logo">MAS<span>.</span> Designer</div>
    <div>© 2026 MAS Designer. All rights reserved.</div>
    <div>Built Bold. Built Different.</div>
  </footer>

  <script>
    // Cursor
    const cursor = document.getElementById('cursor');
    const ring = document.getElementById('cursorRing');
    let mx = 0, my = 0, rx = 0, ry = 0;
    document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
    (function animCursor() {
      cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
      rx += (mx - rx) * 0.18; ry += (my - ry) * 0.18;
      ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
      requestAnimationFrame(animCursor);
    })();
    document.querySelectorAll('a, button').forEach(el => {
      el.addEventListener('mouseenter', () => { cursor.style.transform = 'translate(-50%,-50%) scale(2.5)'; ring.style.opacity = '0'; });
      el.addEventListener('mouseleave', () => { cursor.style.transform = 'translate(-50%,-50%) scale(1)'; ring.style.opacity = '1'; });
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
    }, { threshold: 0.1 });
    reveals.forEach(el => observer.observe(el));
  </script>

</body>
</html># MASDESIGNS

