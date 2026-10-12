<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GitHub Overview · Modern Animation</title>
  <style>
    /* RESET & GLOBAL */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: #0b0d15;
      font-family: 'Inter', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 1.5rem;
      position: relative;
      overflow-x: hidden;
    }

    /* Animated background gradient orbs */
    .bg-orb {
      position: fixed;
      width: 60vmax;
      height: 60vmax;
      border-radius: 50%;
      filter: blur(100px);
      opacity: 0.35;
      pointer-events: none;
      z-index: 0;
      animation: floatOrb 24s infinite alternate ease-in-out;
    }

    .orb-1 {
      background: radial-gradient(circle at 30% 30%, #3b82f6, #8b5cf6);
      top: -20vmax;
      left: -20vmax;
    }

    .orb-2 {
      background: radial-gradient(circle at 70% 70%, #ec4899, #f97316);
      bottom: -20vmax;
      right: -20vmax;
      animation-duration: 30s;
      animation-delay: -5s;
    }

    .orb-3 {
      background: radial-gradient(circle at 50% 50%, #06b6d4, #3b82f6);
      top: 30%;
      left: 40%;
      width: 40vmax;
      height: 40vmax;
      opacity: 0.2;
      animation-duration: 18s;
      animation-delay: -8s;
    }

    @keyframes floatOrb {
      0% { transform: translate(0, 0) scale(1); }
      50% { transform: translate(6%, 8%) scale(1.15); }
      100% { transform: translate(-5%, -5%) scale(0.95); }
    }

    /* MAIN CARD – GLASSMORPHISM */
    .dashboard {
      position: relative;
      z-index: 10;
      width: 100%;
      max-width: 1280px;
      background: rgba(15, 20, 30, 0.55);
      backdrop-filter: blur(20px) saturate(180%);
      -webkit-backdrop-filter: blur(20px) saturate(180%);
      border-radius: 3rem;
      padding: 2.5rem 2rem;
      border: 1px solid rgba(255, 255, 255, 0.08);
      box-shadow: 0 30px 50px -20px rgba(0, 0, 0, 0.8),
                  inset 0 0 0 1px rgba(255, 255, 255, 0.03);
      animation: cardReveal 1.2s cubic-bezier(0.2, 0.9, 0.3, 1) forwards;
      opacity: 0;
      transform: scale(0.96) translateY(20px);
    }

    @keyframes cardReveal {
      to {
        opacity: 1;
        transform: scale(1) translateY(0);
      }
    }

    /* HEADER */
    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 2.5rem;
      flex-wrap: wrap;
      gap: 1rem;
    }

    .logo-area {
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .gh-icon {
      width: 48px;
      height: 48px;
      background: linear-gradient(135deg, #6e5494, #2b3137);
      border-radius: 16px;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 10px 20px -5px rgba(110, 84, 148, 0.5);
    }

    .gh-icon svg {
      width: 28px;
      height: 28px;
      fill: white;
    }

    .title-group h1 {
      font-size: 1.8rem;
      font-weight: 700;
      letter-spacing: -0.02em;
      background: linear-gradient(135deg, #ffffff, #b0c4ff);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .title-group p {
      color: rgba(200, 215, 255, 0.6);
      font-size: 0.9rem;
      margin-top: 0.2rem;
      letter-spacing: 0.3px;
    }

    /* Live indicator */
    .live-badge {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      background: rgba(255, 255, 255, 0.05);
      padding: 0.6rem 1.2rem;
      border-radius: 40px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      color: #cbd5e1;
      font-size: 0.85rem;
      font-weight: 500;
      letter-spacing: 0.4px;
    }

    .pulse-dot {
      width: 8px;
      height: 8px;
      background: #10b981;
      border-radius: 50%;
      box-shadow: 0 0 10px #10b981;
      animation: pulse 1.8s infinite;
    }

    @keyframes pulse {
      0% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.5; transform: scale(1.3); }
      100% { opacity: 1; transform: scale(1); }
    }

    /* STATS GRID */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1.5rem;
      margin-bottom: 2.5rem;
    }

    .stat-card {
      background: rgba(255, 255, 255, 0.03);
      border: 1px solid rgba(255, 255, 255, 0.06);
      border-radius: 1.8rem;
      padding: 1.6rem 1.4rem;
      transition: all 0.4s cubic-bezier(0.2, 0.9, 0.3, 1);
      position: relative;
      overflow: hidden;
      opacity: 0;
      animation: fadeSlideUp 0.8s ease forwards;
      animation-delay: calc(var(--i, 0) * 0.08s);
    }

    .stat-card:nth-child(1) { --i: 1; }
    .stat-card:nth-child(2) { --i: 2; }
    .stat-card:nth-child(3) { --i: 3; }
    .stat-card:nth-child(4) { --i: 4; }

    @keyframes fadeSlideUp {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .stat-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at var(--x, 50%) var(--y, 0%), rgba(120, 140, 255, 0.15), transparent 70%);
      opacity: 0;
      transition: opacity 0.5s;
      pointer-events: none;
    }

    .stat-card:hover::before {
      opacity: 1;
    }

    .stat-card:hover {
      transform: translateY(-6px) scale(1.02);
      border-color: rgba(120, 140, 255, 0.3);
      box-shadow: 0 25px 35px -15px rgba(80, 100, 255, 0.3);
    }

    .stat-icon {
      font-size: 1.8rem;
      margin-bottom: 0.75rem;
      display: inline-block;
      background: linear-gradient(135deg, #a5b4fc, #818cf8);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .stat-label {
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 1px;
      color: rgba(180, 200, 255, 0.6);
      font-weight: 600;
      margin-bottom: 0.4rem;
    }

    .stat-value {
      font-size: 2rem;
      font-weight: 800;
      color: #f1f5ff;
      line-height: 1.2;
      letter-spacing: -0.02em;
    }

    .stat-change {
      font-size: 0.8rem;
      margin-top: 0.5rem;
      color: #34d399;
      display: flex;
      align-items: center;
      gap: 0.3rem;
    }

    .stat-change.negative {
      color: #f87171;
    }

    /* README SECTION – YOU ASKED FOR "NO README ADD PART" */
    .readme-section {
      background: rgba(0, 0, 0, 0.35);
      border-radius: 2rem;
      border: 1px solid rgba(255, 255, 255, 0.06);
      padding: 1.8rem 2rem;
      margin-top: 0.5rem;
      transition: all 0.4s ease;
      backdrop-filter: blur(10px);
      animation: fadeSlideUp 1s ease forwards;
      animation-delay: 0.5s;
      opacity: 0;
      position: relative;
      overflow: hidden;
    }

    .readme-section::after {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: conic-gradient(from 0deg, transparent, rgba(100, 150, 255, 0.05), transparent 30%);
      animation: rotateGlow 12s linear infinite;
      pointer-events: none;
    }

    @keyframes rotateGlow {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    .readme-header {
      display: flex;
      align-items: center;
      gap: 0.8rem;
      margin-bottom: 1.2rem;
      position: relative;
      z-index: 2;
    }

    .readme-header .icon {
      font-size: 1.8rem;
    }

    .readme-header h2 {
      font-size: 1.3rem;
      font-weight: 600;
      color: #e2e8ff;
      letter-spacing: -0.01em;
    }

    .readme-badge {
      background: #3b82f6;
      font-size: 0.7rem;
      padding: 0.2rem 0.7rem;
      border-radius: 20px;
      color: white;
      font-weight: 600;
      letter-spacing: 0.5px;
      margin-left: auto;
    }

    .readme-content {
      position: relative;
      z-index: 2;
      color: #cbd5e1;
      font-size: 0.95rem;
      line-height: 1.7;
      border-left: 3px solid #3b82f6;
      padding-left: 1.4rem;
    }

    .readme-content .greeting {
      font-size: 1.2rem;
      font-weight: 600;
      color: #f1f5ff;
      margin-bottom: 0.5rem;
    }

    .readme-content .highlight {
      color: #93c5fd;
      font-weight: 600;
    }

    .readme-content .code-block {
      background: rgba(0, 0, 0, 0.4);
      border-radius: 12px;
      padding: 0.8rem 1.2rem;
      margin: 1rem 0;
      font-family: 'JetBrains Mono', 'Fira Code', monospace;
      font-size: 0.85rem;
      color: #a5b4fc;
      border: 1px solid rgba(255, 255, 255, 0.05);
      overflow-x: auto;
      white-space: nowrap;
    }

    .readme-content .code-block span.keyword {
      color: #f472b6;
    }

    .readme-content .code-block span.string {
      color: #34d399;
    }

    /* subtle line decoration */
    .glow-line {
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(100, 150, 255, 0.3), transparent);
      margin: 2rem 0 0.5rem;
      position: relative;
      z-index: 2;
    }

    /* FOOTER */
    .footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 2rem;
      color: rgba(160, 180, 220, 0.5);
      font-size: 0.8rem;
      position: relative;
      z-index: 2;
    }

    .footer a {
      color: #93c5fd;
      text-decoration: none;
      border-bottom: 1px dotted rgba(147, 197, 253, 0.4);
    }

    /* RESPONSIVE */
    @media (max-width: 700px) {
      .dashboard {
        padding: 1.8rem 1.2rem;
        border-radius: 2rem;
      }
      .header {
        flex-direction: column;
        align-items: flex-start;
      }
      .title-group h1 {
        font-size: 1.5rem;
      }
      .stat-value {
        font-size: 1.6rem;
      }
      .readme-section {
        padding: 1.4rem;
      }
      .readme-content {
        font-size: 0.9rem;
      }
    }

    @media (max-width: 480px) {
      .stats-grid {
        grid-template-columns: 1fr 1fr;
        gap: 1rem;
      }
      .stat-card {
        padding: 1.2rem 1rem;
      }
      .stat-value {
        font-size: 1.3rem;
      }
      .live-badge {
        font-size: 0.75rem;
        padding: 0.4rem 1rem;
      }
      .readme-badge {
        display: none;
      }
    }
  </style>
</head>
<body>
  <!-- Animated Background Orbs -->
  <div class="bg-orb orb-1"></div>
  <div class="bg-orb orb-2"></div>
  <div class="bg-orb orb-3"></div>

  <!-- Main Dashboard -->
  <div class="dashboard">

    <!-- Header -->
    <div class="header">
      <div class="logo-area">
        <div class="gh-icon">
          <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 .5C5.37.5 0 5.78 0 12.292c0 5.211 3.438 9.63 8.205 11.188.6.111.82-.254.82-.567 0-.28-.01-1.022-.015-2.005-3.338.711-4.042-1.582-4.042-1.582-.546-1.361-1.335-1.725-1.335-1.725-1.087-.731.084-.716.084-.716 1.205.082 1.838 1.215 1.838 1.215 1.07 1.803 2.809 1.282 3.495.981.108-.763.417-1.282.76-1.577-2.665-.295-5.466-1.309-5.466-5.827 0-1.287.465-2.339 1.235-3.164-.135-.298-.54-1.497.105-3.121 0 0 1.005-.316 3.3 1.209.96-.262 1.98-.392 3-.398 1.02.006 2.04.136 3 .398 2.28-1.525 3.285-1.209 3.285-1.209.645 1.624.24 2.823.12 3.121.765.825 1.23 1.877 1.23 3.164 0 4.53-2.805 5.527-5.475 5.817.42.354.81 1.077.81 2.182 0 1.578-.015 2.846-.015 3.229 0 .309.21.678.825.561C20.565 21.917 24 17.495 24 12.292 24 5.78 18.63.5 12 .5z"/>
          </svg>
        </div>
        <div class="title-group">
          <h1>GitHub Overview</h1>
          <p>@octocat · Real-time metrics</p>
        </div>
      </div>
      <div class="live-badge">
        <span class="pulse-dot"></span>
        LIVE · UPDATED NOW
      </div>
    </div>

    <!-- Stats Grid -->
    <div class="stats-grid">
      <div class="stat-card">
        <div class="stat-icon">📦</div>
        <div class="stat-label">Repositories</div>
        <div class="stat-value">87</div>
        <div class="stat-change">↑ 12 this month</div>
      </div>
      <div class="stat-card">
        <div class="stat-icon">⭐</div>
        <div class="stat-label">Total Stars</div>
        <div class="stat-value">3.2k</div>
        <div class="stat-change">↑ 214 this week</div>
      </div>
      <div class="stat-card">
        <div class="stat-icon">🍴</div>
        <div class="stat-label">Forks</div>
        <div class="stat-value">468</div>
        <div class="stat-change">↑ 31 this month</div>
      </div>
      <div class="stat-card">
        <div class="stat-icon">👥</div>
        <div class="stat-label">Followers</div>
        <div class="stat-value">1.8k</div>
        <div class="stat-change">↑ 5.3% this week</div>
      </div>
    </div>

    <!-- README SECTION (the part you asked for) -->
    <div class="readme-section">
      <div class="readme-header">
        <span class="icon">📄</span>
        <h2>README.md</h2>
        <span class="readme-badge">main branch</span>
      </div>
      <div class="readme-content">
        <div class="greeting">👋 Hi, I'm Octocat!</div>
        <p>I'm a <span class="highlight">full-stack developer</span> passionate about open source, developer tools, and building delightful user experiences.</p>
        <div class="code-block">
          <span class="keyword">const</span> <span class="string">skills</span> = [<span class="string">'React'</span>, <span class="string">'Node.js'</span>, <span class="string">'TypeScript'</span>, <span class="string">'Rust'</span>];
        </div>
        <p>🚀 Currently working on <span class="highlight">next-gen animation libraries</span> and contributing to the community. Always open to collaborate on interesting projects.</p>
        <p style="margin-top: 0.8rem; font-size: 0.9rem; color: #9ca3af;">— This README is part of your GitHub overview dashboard —</p>
      </div>
    </div>

    <!-- subtle glow line -->
    <div class="glow-line"></div>

    <!-- Footer -->
    <div class="footer">
      <span>✨ Animated with pure CSS · Glassmorphism</span>
      <span><a href="#">View full profile →</a></span>
    </div>

  </div>

  <!-- micro-interaction: subtle parallax on mouse move (optional, just for extra flair) -->
  <script>
    (function() {
      const dashboard = document.querySelector('.dashboard');
      if (!dashboard) return;

      // Track mouse for subtle tilt effect
      dashboard.addEventListener('mousemove', (e) => {
        const rect = dashboard.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        const centerX = rect.width / 2;
        const centerY = rect.height / 2;
        const rotateX = (y - centerY) / 40;
        const rotateY = (centerX - x) / 40;

        dashboard.style.transform = `perspective(1200px) rotateX(${rotateX * 0.4}deg) rotateY(${rotateY * 0.4}deg) scale(1)`;
      });

      dashboard.addEventListener('mouseleave', () => {
        dashboard.style.transform = 'perspective(1200px) rotateX(0deg) rotateY(0deg) scale(1)';
      });

      // Update stat card radial gradient position on hover
      const cards = document.querySelectorAll('.stat-card');
      cards.forEach(card => {
        card.addEventListener('mousemove', (e) => {
          const rect = card.getBoundingClientRect();
          const x = ((e.clientX - rect.left) / rect.width) * 100;
          const y = ((e.clientY - rect.top) / rect.height) * 100;
          card.style.setProperty('--x', x + '%');
          card.style.setProperty('--y', y + '%');
        });
      });
    })();
  </script>
</body>
</html>
