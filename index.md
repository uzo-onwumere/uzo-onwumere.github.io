
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Uzoma Onwumere — Penetration Tester</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=DM+Mono:ital,wght@0,300;0,400;0,500;1,300&family=Syne:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #0a0c0f;
      --bg2: #0f1215;
      --bg3: #151a1f;
      --border: rgba(255,255,255,0.06);
      --border2: rgba(255,255,255,0.12);
      --text: #e8eaed;
      --muted: #6b7280;
      --accent: #00d4aa;
      --accent2: #0099ff;
      --red: #ff4757;
      --font-display: 'Syne', sans-serif;
      --font-mono: 'DM Mono', monospace;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-mono);
      font-size: 14px;
      line-height: 1.7;
      overflow-x: hidden;
      cursor: none;
    }

    .cursor {
      position: fixed;
      width: 8px;
      height: 8px;
      background: var(--accent);
      border-radius: 50%;
      pointer-events: none;
      z-index: 9999;
      transform: translate(-50%, -50%);
      transition: transform 0.1s, background 0.2s;
    }
    .cursor-ring {
      position: fixed;
      width: 28px;
      height: 28px;
      border: 1px solid rgba(0,212,170,0.4);
      border-radius: 50%;
      pointer-events: none;
      z-index: 9998;
      transform: translate(-50%, -50%);
      transition: transform 0.15s ease, width 0.2s, height 0.2s, border-color 0.2s;
    }

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
      z-index: 100;
    }

    body::after {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(0,212,170,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,212,170,0.03) 1px, transparent 1px);
      background-size: 40px 40px;
      pointer-events: none;
      z-index: 0;
    }

    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 500;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 3rem;
      height: 60px;
      border-bottom: 1px solid var(--border);
      background: rgba(10,12,15,0.85);
      backdrop-filter: blur(12px);
    }
    .nav-logo { font-family: var(--font-mono); font-size: 13px; color: var(--accent); letter-spacing: 0.05em; }
    .nav-logo span { color: var(--muted); }
    .nav-links { display: flex; gap: 2rem; }
    .nav-links a { font-size: 12px; color: var(--muted); text-decoration: none; letter-spacing: 0.08em; transition: color 0.2s; }
    .nav-links a:hover { color: var(--accent); }

    section { position: relative; z-index: 1; }

    #hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 0 3rem;
      padding-top: 60px;
    }
    .hero-inner { max-width: 900px; }

    .terminal-prompt {
      font-size: 12px;
      color: var(--muted);
      margin-bottom: 2rem;
      display: flex;
      align-items: center;
      gap: 8px;
      opacity: 0;
      animation: fadeUp 0.5s ease forwards;
    }
    .prompt-symbol { color: var(--accent); }
    .blink {
      display: inline-block;
      width: 8px;
      height: 14px;
      background: var(--accent);
      animation: blink 1s step-end infinite;
      vertical-align: middle;
      margin-left: 2px;
    }
    @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

    .hero-name {
      font-family: var(--font-display);
      font-size: clamp(3rem, 8vw, 7rem);
      font-weight: 700;
      line-height: 0.9;
      letter-spacing: -0.02em;
      color: var(--text);
      margin-bottom: 1rem;
      opacity: 0;
      animation: fadeUp 0.6s ease 0.1s forwards;
    }
    .hero-name .accent-word { color: var(--accent); }

    .hero-role {
      font-size: 13px;
      color: var(--muted);
      letter-spacing: 0.15em;
      text-transform: uppercase;
      margin-bottom: 2rem;
      opacity: 0;
      animation: fadeUp 0.6s ease 0.2s forwards;
    }
    .hero-role .sep { margin: 0 12px; color: var(--border2); }

    .hero-desc {
      font-size: 15px;
      color: #9ca3af;
      line-height: 1.8;
      max-width: 580px;
      margin-bottom: 3rem;
      opacity: 0;
      animation: fadeUp 0.6s ease 0.3s forwards;
      font-family: var(--font-mono);
      font-weight: 300;
    }

    .hero-cta {
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
      opacity: 0;
      animation: fadeUp 0.6s ease 0.4s forwards;
    }
    .btn {
      font-family: var(--font-mono);
      font-size: 12px;
      letter-spacing: 0.08em;
      padding: 10px 24px;
      border-radius: 3px;
      text-decoration: none;
      transition: all 0.2s;
      cursor: none;
    }
    .btn-primary { background: var(--accent); color: #000; font-weight: 500; border: 1px solid var(--accent); }
    .btn-primary:hover { background: transparent; color: var(--accent); }
    .btn-ghost { background: transparent; color: var(--muted); border: 1px solid var(--border2); }
    .btn-ghost:hover { border-color: var(--accent); color: var(--accent); }

    .hero-scroll {
      position: absolute;
      bottom: 2rem;
      left: 3rem;
      font-size: 11px;
      color: var(--muted);
      letter-spacing: 0.1em;
      display: flex;
      align-items: center;
      gap: 8px;
      opacity: 0;
      animation: fadeUp 0.6s ease 0.8s forwards;
    }
    .scroll-line { width: 40px; height: 1px; background: var(--border2); position: relative; overflow: hidden; }
    .scroll-line::after {
      content: '';
      position: absolute;
      left: -100%; top: 0;
      width: 100%; height: 100%;
      background: var(--accent);
      animation: slide 2s ease infinite;
    }
    @keyframes slide { 0%{left:-100%} 100%{left:100%} }

    .status-bar {
      position: absolute;
      top: 50%; right: 3rem;
      transform: translateY(-50%);
      display: flex;
      flex-direction: column;
      gap: 1rem;
      opacity: 0;
      animation: fadeIn 0.8s ease 0.6s forwards;
    }
    .status-item { display: flex; align-items: center; gap: 8px; font-size: 11px; color: var(--muted); }
    .status-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--accent); animation: pulse 2s ease infinite; }
    .status-dot.amber { background: #f59e0b; animation-delay: 0.5s; }
    .status-dot.blue { background: var(--accent2); animation-delay: 1s; }
    @keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.4;transform:scale(0.8)} }

    @keyframes fadeUp { from{opacity:0;transform:translateY(20px)} to{opacity:1;transform:translateY(0)} }
    @keyframes fadeIn { from{opacity:0} to{opacity:1} }

    #about { padding: 8rem 3rem; border-top: 1px solid var(--border); }
    .section-label {
      font-size: 11px;
      color: var(--accent);
      letter-spacing: 0.2em;
      text-transform: uppercase;
      margin-bottom: 3rem;
      display: flex;
      align-items: center;
      gap: 12px;
    }
    .section-label::after { content: ''; flex: 1; max-width: 60px; height: 1px; background: var(--border2); }

    .about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; max-width: 1000px; }
    .about-text { font-size: 14px; color: #9ca3af; line-height: 1.9; font-weight: 300; }
    .about-text p { margin-bottom: 1.25rem; }
    .about-text strong { color: var(--text); font-weight: 500; }

    .spec-list { display: flex; flex-direction: column; gap: 12px; }
    .spec-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px 14px;
      border: 1px solid var(--border);
      border-radius: 3px;
      background: var(--bg2);
      transition: border-color 0.2s;
    }
    .spec-row:hover { border-color: var(--border2); }
    .spec-key { font-size: 11px; color: var(--muted); letter-spacing: 0.05em; }
    .spec-val { font-size: 12px; color: var(--text); }
    .spec-val.green { color: var(--accent); }
    .spec-val.blue { color: var(--accent2); }
    .spec-val.amber { color: #f59e0b; }

    #certs { padding: 6rem 3rem; border-top: 1px solid var(--border); }
    .cert-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(170px, 1fr)); gap: 12px; max-width: 1000px; }
    .cert-card {
      border: 1px solid var(--border);
      border-radius: 3px;
      padding: 1.25rem;
      background: var(--bg2);
      transition: border-color 0.2s, background 0.2s;
      position: relative;
      overflow: hidden;
    }
    .cert-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; }
    .cert-card.active::before { background: var(--accent); }
    .cert-card.progress::before { background: #f59e0b; }
    .cert-card.planned::before { background: var(--border2); }
    .cert-card:hover { border-color: var(--border2); background: var(--bg3); }
    .cert-issuer { font-size: 10px; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 6px; }
    .cert-name { font-size: 14px; color: var(--text); font-family: var(--font-display); font-weight: 500; margin-bottom: 8px; }
    .cert-status { font-size: 10px; padding: 2px 8px; border-radius: 2px; display: inline-block; letter-spacing: 0.06em; }
    .status-earned { background: rgba(0,212,170,0.1); color: var(--accent); }
    .status-progress { background: rgba(245,158,11,0.1); color: #f59e0b; }
    .status-next { background: rgba(255,255,255,0.04); color: var(--muted); }

    #repos { padding: 6rem 3rem; border-top: 1px solid var(--border); }
    .repo-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 12px; max-width: 1000px; }
    .repo-card {
      border: 1px solid var(--border);
      border-radius: 3px;
      padding: 1.5rem;
      background: var(--bg2);
      text-decoration: none;
      display: block;
      transition: border-color 0.2s, transform 0.2s;
      position: relative;
    }
    .repo-card:hover { border-color: var(--accent); transform: translateY(-2px); }
    .repo-icon { width: 32px; height: 32px; border-radius: 3px; display: flex; align-items: center; justify-content: center; font-size: 16px; margin-bottom: 1rem; }
    .repo-name { font-size: 13px; color: var(--accent); margin-bottom: 6px; font-family: var(--font-mono); }
    .repo-desc { font-size: 12px; color: var(--muted); line-height: 1.6; margin-bottom: 1rem; font-weight: 300; }
    .repo-tags { display: flex; flex-wrap: wrap; gap: 6px; }
    .repo-tag { font-size: 10px; padding: 2px 8px; background: var(--bg3); border: 1px solid var(--border); border-radius: 2px; color: var(--muted); }
    .repo-arrow { position: absolute; top: 1.5rem; right: 1.5rem; font-size: 14px; color: var(--border2); transition: color 0.2s, transform 0.2s; }
    .repo-card:hover .repo-arrow { color: var(--accent); transform: translate(2px,-2px); }

    #contact { padding: 8rem 3rem; border-top: 1px solid var(--border); }
    .contact-inner { max-width: 600px; }
    .contact-heading { font-family: var(--font-display); font-size: clamp(2rem, 4vw, 3.5rem); font-weight: 700; line-height: 1.1; margin-bottom: 1.5rem; color: var(--text); }
    .contact-heading .accent-word { color: var(--accent); }
    .contact-sub { font-size: 13px; color: var(--muted); line-height: 1.8; margin-bottom: 3rem; font-weight: 300; }
    .contact-links { display: flex; flex-direction: column; gap: 1px; }
    .contact-link {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 14px 0;
      border-bottom: 1px solid var(--border);
      text-decoration: none;
      color: var(--text);
      transition: color 0.2s;
      font-size: 13px;
    }
    .contact-link:hover { color: var(--accent); }
    .contact-link-label { color: var(--muted); font-size: 11px; letter-spacing: 0.08em; }

    footer {
      padding: 2rem 3rem;
      border-top: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 11px;
      color: var(--muted);
      position: relative;
      z-index: 1;
    }

    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }
    ::-webkit-scrollbar-thumb:hover { background: var(--accent); }

    .reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease; }
    .reveal.visible { opacity: 1; transform: none; }

    @media (max-width: 768px) {
      nav { padding: 0 1.5rem; }
      #hero, #about, #certs, #repos, #contact { padding-left: 1.5rem; padding-right: 1.5rem; }
      .about-grid { grid-template-columns: 1fr; gap: 2rem; }
      .status-bar { display: none; }
      footer { flex-direction: column; gap: 0.5rem; text-align: center; }
    }
  </style>
</head>
<body>

  <div class="cursor" id="cursor"></div>
  <div class="cursor-ring" id="cursor-ring"></div>

  <nav>
    <div class="nav-logo"><span>~/</span>uzo-onwumere</div>
    <div class="nav-links">
      <a href="#about">about</a>
      <a href="#certs">certs</a>
      <a href="#repos">work</a>
      <a href="#contact">contact</a>
    </div>
  </nav>

  <section id="hero">
    <div class="hero-inner">
      <div class="terminal-prompt">
        <span class="prompt-symbol">$</span>
        <span>whoami</span>
        <span class="blink"></span>
      </div>
      <h1 class="hero-name">
        Uzoma<br><span class="accent-word">Onwumere</span>
      </h1>
      <div class="hero-role">
        CTI Analyst<span class="sep">/</span>Penetration Tester<span class="sep">/</span>TS/SCI &middot; CI Poly
      </div>
      <p class="hero-desc">
        Four years tracking adversaries in threat intelligence. Now learning to think like one.
        Transitioning into offensive security and DFIR &mdash; building the technical depth to match my analytical background.
      </p>
      <div class="hero-cta">
        <a href="#repos" class="btn btn-primary">view my work</a>
        <a href="https://app.hackthebox.com/users/2715427" target="_blank" class="btn btn-ghost">HackTheBox profile</a>
      </div>
    </div>

    <div class="status-bar">
      <div class="status-item">
        <div class="status-dot"></div>
        <span>eJPT &mdash; active</span>
      </div>
      <div class="status-item">
        <div class="status-dot amber"></div>
        <span>HTB machines &mdash; in progress</span>
      </div>
      <div class="status-item">
        <div class="status-dot blue"></div>
        <span>home lab &mdash; online</span>
      </div>
    </div>

    <div class="hero-scroll">
      <div class="scroll-line"></div>
      scroll
    </div>
  </section>

  <section id="about">
    <div class="section-label reveal">// about</div>
    <div class="about-grid">
      <div class="about-text reveal">
        <p>My background is in <strong>Cyber Threat Intelligence</strong> &mdash; four years of tracking threat actors, mapping TTPs to MITRE ATT&amp;CK, and delivering finished intelligence to operational and executive stakeholders.</p>
        <p>I'm now transitioning into <strong>penetration testing and DFIR</strong> &mdash; not away from CTI, but deeper into it. Understanding how adversaries actually execute gives me an edge most analysts don't have.</p>
        <p>My home lab runs on a <strong>Ryzen 9 9950X3D</strong> workstation under CachyOS Linux with VMware Workstation Pro, running a Windows Server 2019 Active Directory environment built specifically for pentesting practice and malware analysis.</p>
      </div>
      <div class="spec-list reveal">
        <div class="spec-row">
          <span class="spec-key">clearance</span>
          <span class="spec-val green">TS/SCI &middot; CI Poly &mdash; active</span>
        </div>
        <div class="spec-row">
          <span class="spec-key">experience</span>
          <span class="spec-val">4 years CTI</span>
        </div>
        <div class="spec-row">
          <span class="spec-key">current focus</span>
          <span class="spec-val amber">PNPT &middot; HTB machines</span>
        </div>
        <div class="spec-row">
          <span class="spec-key">host OS</span>
          <span class="spec-val">CachyOS Linux</span>
        </div>
        <div class="spec-row">
          <span class="spec-key">lab</span>
          <span class="spec-val">VMware &middot; Win Server 2019 AD</span>
        </div>
        <div class="spec-row">
          <span class="spec-key">attack OS</span>
          <span class="spec-val">Kali Linux</span>
        </div>
        <div class="spec-row">
          <span class="spec-key">roadmap</span>
          <span class="spec-val blue">Pentest+ &rarr; PNPT &rarr; OSCP &rarr; GPEN</span>
        </div>
      </div>
    </div>
  </section>

  <section id="certs">
    <div class="section-label reveal">// certifications</div>
    <div class="cert-grid">
      <div class="cert-card active reveal">
        <div class="cert-issuer">CompTIA</div>
        <div class="cert-name">CySA+</div>
        <span class="cert-status status-earned">earned</span>
      </div>
      <div class="cert-card active reveal">
        <div class="cert-issuer">CompTIA</div>
        <div class="cert-name">Security+</div>
        <span class="cert-status status-earned">earned</span>
      </div>
      <div class="cert-card active reveal">
        <div class="cert-issuer">CompTIA</div>
        <div class="cert-name">Network+</div>
        <span class="cert-status status-earned">earned</span>
      </div>
      <div class="cert-card active reveal">
        <div class="cert-issuer">CompTIA</div>
        <div class="cert-name">A+</div>
        <span class="cert-status status-earned">earned</span>
      </div>
      <div class="cert-card progress reveal">
        <div class="cert-issuer">eLearnSecurity</div>
        <div class="cert-name">eJPT</div>
        <span class="cert-status status-earned">earned</span>
      </div>
      <div class="cert-card planned reveal">
        <div class="cert-issuer">TCM Security</div>
        <div class="cert-name">PNPT</div>
        <span class="cert-status status-progress">in progress</span>
      </div>
      <div class="cert-card planned reveal">
        <div class="cert-issuer">CompTIA</div>
        <div class="cert-name">Pentest+</div>
        <span class="cert-status status-earned">earned</span>
      </div>
      <div class="cert-card planned reveal">
        <div class="cert-issuer">Offensive Security</div>
        <div class="cert-name">OSCP</div>
        <span class="cert-status status-next">roadmap</span>
      </div>
      <div class="cert-card planned reveal">
        <div class="cert-issuer">GIAC</div>
        <div class="cert-name">GPEN</div>
        <span class="cert-status status-next">roadmap</span>
      </div>
    </div>
  </section>

  <section id="repos">
    <div class="section-label reveal">// repositories</div>
    <div class="repo-grid">
      <a href="https://github.com/uzo-onwumere/ctf-writeups" target="_blank" class="repo-card reveal">
        <div class="repo-arrow">&#8599;</div>
        <div class="repo-icon" style="background:rgba(0,212,170,0.08);">&#9658;</div>
        <div class="repo-name">ctf-writeups</div>
        <div class="repo-desc">Detailed machine walkthrough notes from HackTheBox and VulnHub. Covers enumeration, exploitation, and privilege escalation methodology.</div>
        <div class="repo-tags">
          <span class="repo-tag">hackthebox</span>
          <span class="repo-tag">vulnhub</span>
          <span class="repo-tag">oscp-prep</span>
        </div>
      </a>
      <a href="https://github.com/uzo-onwumere/pentest-toolkit" target="_blank" class="repo-card reveal">
        <div class="repo-arrow">&#8599;</div>
        <div class="repo-icon" style="background:rgba(0,153,255,0.08);">&#9881;</div>
        <div class="repo-name">pentest-toolkit</div>
        <div class="repo-desc">Custom Python scripts for recon, enumeration, and post-exploitation. Built and tested against personal lab environments.</div>
        <div class="repo-tags">
          <span class="repo-tag">python</span>
          <span class="repo-tag">recon</span>
          <span class="repo-tag">automation</span>
        </div>
      </a>
      <a href="https://github.com/uzo-onwumere/blog" target="_blank" class="repo-card reveal">
        <div class="repo-arrow">&#8599;</div>
        <div class="repo-icon" style="background:rgba(255,71,87,0.08);">&#10022;</div>
        <div class="repo-name">blog</div>
        <div class="repo-desc">Long-form technical writing on penetration testing, threat intelligence, and the CTI-to-offensive pivot.</div>
        <div class="repo-tags">
          <span class="repo-tag">jekyll</span>
          <span class="repo-tag">writeups</span>
          <span class="repo-tag">cti</span>
        </div>
      </a>
    </div>
  </section>

  <section id="contact">
    <div class="contact-inner">
      <div class="section-label reveal">// contact</div>
      <h2 class="contact-heading reveal">Let's<br><span class="accent-word">connect.</span></h2>
      <p class="contact-sub reveal">
        Open to penetration testing roles &mdash; especially positions that value a CTI background.<br>
        TS/SCI with CI Poly. Based in the Greater St. Louis, MO area.
      </p>
      <div class="contact-links reveal">
        <a href="https://www.linkedin.com/in/uzoma-onwumere-160966273" target="_blank" class="contact-link">
          <span class="contact-link-label">LinkedIn</span>
          <span>linkedin.com/in/uzoma-onwumere-160966273 &#8599;</span>
        </a>
        <a href="https://app.hackthebox.com/users/2715427" target="_blank" class="contact-link">
          <span class="contact-link-label">HackTheBox</span>
          <span>app.hackthebox.com/users/2715427 &#8599;</span>
        </a>
        <a href="https://github.com/uzo-onwumere" target="_blank" class="contact-link">
          <span class="contact-link-label">GitHub</span>
          <span>github.com/uzo-onwumere &#8599;</span>
        </a>
        <a href="mailto:uzoman.onwumere@gmail.com" class="contact-link">
          <span class="contact-link-label">Email</span>
          <span>uzoman.onwumere@gmail.com &#8599;</span>
        </a>
      </div>
    </div>
  </section>

  <footer>
    <span>uzoma onwumere &mdash; penetration tester</span>
    <span>built with GitHub Pages</span>
  </footer>

  <script>
    const cursor = document.getElementById('cursor');
    const ring = document.getElementById('cursor-ring');
    let mx = 0, my = 0, rx = 0, ry = 0;
    document.addEventListener('mousemove', function(e) {
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
    document.querySelectorAll('a, button').forEach(function(el) {
      el.addEventListener('mouseenter', function() {
        ring.style.width = '44px';
        ring.style.height = '44px';
        ring.style.borderColor = 'rgba(0,212,170,0.6)';
      });
      el.addEventListener('mouseleave', function() {
        ring.style.width = '28px';
        ring.style.height = '28px';
        ring.style.borderColor = 'rgba(0,212,170,0.4)';
      });
    });

    const reveals = document.querySelectorAll('.reveal');
    const obs = new IntersectionObserver(function(entries) {
      entries.forEach(function(e, i) {
        if (e.isIntersecting) {
          setTimeout(function() { e.target.classList.add('visible'); }, i * 80);
          obs.unobserve(e.target);
        }
      });
    }, { threshold: 0.1 });
    reveals.forEach(function(el) { obs.observe(el); });
  </script>

</body>
</html>

