<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Utkarsh Jha — GitHub README</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #0d1117;
      --surface: #161b22;
      --surface2: #1c2128;
      --border: rgba(255,255,255,0.08);
      --border-hover: rgba(255,255,255,0.15);
      --text-primary: #e6edf3;
      --text-secondary: #8b949e;
      --text-muted: #484f58;
      --blue: #58a6ff;
      --blue-bg: rgba(56,139,253,0.1);
      --purple: #bc8cff;
      --purple-bg: rgba(188,140,255,0.1);
      --green: #3fb950;
      --green-bg: rgba(63,185,80,0.08);
      --pink: #f778ba;
      --font-mono: 'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace;
    }

    @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;600&family=Syne:wght@400;500;600;700;800&display=swap');

    body {
      background: var(--bg);
      color: var(--text-primary);
      font-family: 'Syne', sans-serif;
      min-height: 100vh;
      padding: 2rem;
    }

    .readme-card {
      max-width: 820px;
      margin: 0 auto;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 12px;
      overflow: hidden;
    }

    /* --- TOP BAR (like a browser/terminal) --- */
    .top-bar {
      background: var(--surface2);
      border-bottom: 1px solid var(--border);
      padding: 10px 16px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .dot-red { width: 12px; height: 12px; border-radius: 50%; background: #ff5f57; }
    .dot-yellow { width: 12px; height: 12px; border-radius: 50%; background: #febc2e; }
    .dot-green { width: 12px; height: 12px; border-radius: 50%; background: #28c840; }
    .tab-label {
      margin-left: 12px;
      font-family: var(--font-mono);
      font-size: 12px;
      color: var(--text-secondary);
    }
    .tab-label span { color: var(--green); }

    /* --- CONTENT --- */
    .content { padding: 2rem 2.5rem; }

    /* HERO */
    .hero {
      display: flex;
      gap: 2rem;
      align-items: flex-start;
      margin-bottom: 2rem;
    }
    .hero-left { flex: 1; min-width: 0; }
    .hero-right { flex-shrink: 0; }
    .hero-right img {
      width: 190px;
      height: 190px;
      object-fit: cover;
      border-radius: 10px;
      border: 1px solid var(--border);
      display: block;
      filter: brightness(0.95);
    }

    .greeting {
      font-family: var(--font-mono);
      font-size: 12px;
      color: var(--green);
      margin-bottom: 8px;
      letter-spacing: 0.05em;
    }
    h1 {
      font-family: 'Syne', sans-serif;
      font-size: 32px;
      font-weight: 800;
      color: var(--text-primary);
      line-height: 1.1;
      margin-bottom: 6px;
    }
    .tagline {
      font-family: var(--font-mono);
      font-size: 13px;
      color: var(--text-muted);
      margin-bottom: 20px;
      font-style: italic;
    }
    .tagline span { color: var(--purple); font-style: normal; }

    .info-list { display: flex; flex-direction: column; gap: 8px; margin-bottom: 20px; }
    .info-item {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 13px;
      color: var(--text-secondary);
      font-family: var(--font-mono);
    }
    .info-item::before { content: '›'; color: var(--blue); font-size: 16px; line-height: 1; }
    .info-item a { color: var(--pink); text-decoration: none; }
    .info-item a:hover { text-decoration: underline; }
    .info-item strong { color: var(--text-primary); font-weight: 500; }

    /* SOCIAL */
    .social-row { display: flex; gap: 8px; flex-wrap: wrap; }
    .social-btn {
      display: flex;
      align-items: center;
      gap: 6px;
      font-size: 12px;
      font-weight: 600;
      font-family: var(--font-mono);
      padding: 5px 12px;
      border-radius: 6px;
      border: 1px solid var(--border);
      color: var(--text-secondary);
      text-decoration: none;
      background: var(--surface2);
      transition: border-color 0.2s, color 0.2s;
    }
    .social-btn:hover { border-color: var(--border-hover); color: var(--text-primary); }
    .social-btn svg { width: 13px; height: 13px; fill: currentColor; flex-shrink: 0; }

    /* DIVIDER */
    .divider { border: none; border-top: 1px solid var(--border); margin: 1.75rem 0; }

    /* SECTION LABEL */
    .section-label {
      font-family: var(--font-mono);
      font-size: 11px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--text-muted);
      margin-bottom: 1.25rem;
    }
    .section-label span { color: var(--green); }

    /* STACK BLOCKS */
    .stack-block { margin-bottom: 1.5rem; }
    .stack-heading {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-bottom: 10px;
    }
    .stack-category {
      font-family: var(--font-mono);
      font-size: 11px;
      font-weight: 600;
      padding: 2px 10px;
      border-radius: 99px;
      border: 1px solid;
    }
    .cat-web { background: var(--blue-bg); color: var(--blue); border-color: rgba(88,166,255,0.25); }
    .cat-chain { background: var(--purple-bg); color: var(--purple); border-color: rgba(188,140,255,0.25); }
    .stack-name {
      font-size: 13px;
      font-weight: 600;
      color: var(--text-secondary);
    }

    .chips { display: flex; flex-wrap: wrap; gap: 6px; }
    .chip {
      display: flex;
      align-items: center;
      gap: 6px;
      font-size: 12px;
      font-family: var(--font-mono);
      padding: 4px 10px;
      border-radius: 6px;
      border: 1px solid var(--border);
      background: var(--surface2);
      color: var(--text-secondary);
      transition: border-color 0.2s, color 0.2s;
    }
    .chip:hover { border-color: var(--border-hover); color: var(--text-primary); }
    .chip img { width: 14px; height: 14px; object-fit: contain; }

    /* STATS */
    .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
    .stat-card {
      background: var(--surface2);
      border: 1px solid var(--border);
      border-radius: 8px;
      overflow: hidden;
    }
    .stat-card img { width: 100%; display: block; }

    /* FOOTER */
    .footer {
      border-top: 1px solid var(--border);
      padding: 12px 2.5rem;
      font-family: var(--font-mono);
      font-size: 11px;
      color: var(--text-muted);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .footer span { color: var(--green); }
  </style>
</head>
<body>
<div class="readme-card">
  <div class="top-bar">
    <div class="dot-red"></div>
    <div class="dot-yellow"></div>
    <div class="dot-green"></div>
    <span class="tab-label"><span>utkarshjha-2005</span> / README.md</span>
  </div>
  <div class="content">
    <div class="hero">
      <div class="hero-left">
        <p class="greeting">// hi there, I'm</p>
        <h1>Utkarsh Jha</h1>
        <p class="tagline"><span>"</span>Code never lies — sometimes comments do<span>"</span></p>

        <div class="info-list">
          <div class="info-item">Currently exploring <strong>Web3 & Blockchain</strong></div>
          <div class="info-item">Ask me about <strong>Web Development</strong></div>
          <div class="info-item"><a href="mailto:jha.utkarsh2005@gmail.com">jha.utkarsh2005@gmail.com</a></div>
        </div>

        <div class="social-row">
          <a href="https://linkedin.com/in/utkarsh-jha-" class="social-btn" target="_blank">
            <svg viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
            LinkedIn
          </a>
          <a href="https://www.instagram.com/utkarsh_jha_2005/" class="social-btn" target="_blank">
            <svg viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg>
            Instagram
          </a>
          <a href="https://leetcode.com/u/user4171b/" class="social-btn" target="_blank">
            <svg viewBox="0 0 24 24"><path d="M13.483 0a1.374 1.374 0 0 0-.961.438L7.116 6.226l-3.854 4.126a5.266 5.266 0 0 0-1.209 2.104 5.35 5.35 0 0 0-.125.513 5.527 5.527 0 0 0 .062 2.362 5.83 5.83 0 0 0 .349 1.017 5.938 5.938 0 0 0 1.271 1.818l4.277 4.193.039.038c2.248 2.165 5.852 2.133 8.063-.074l2.396-2.392c.54-.54.54-1.414.003-1.955a1.378 1.378 0 0 0-1.951-.003l-2.396 2.392a3.021 3.021 0 0 1-4.205.038l-.02-.019-4.276-4.193c-.652-.64-.972-1.469-.948-2.263a2.68 2.68 0 0 1 .066-.523 2.545 2.545 0 0 1 .619-1.164L9.13 8.114c1.058-1.134 3.204-1.27 4.43-.278l3.501 2.831c.593.48 1.461.387 1.94-.207a1.384 1.384 0 0 0-.207-1.943l-3.5-2.831c-.8-.647-1.766-1.045-2.774-1.202l2.015-2.158A1.384 1.384 0 0 0 13.483 0zm-2.866 12.815a1.38 1.38 0 0 0-1.38 1.382 1.38 1.38 0 0 0 1.38 1.382H20.79a1.38 1.38 0 0 0 1.38-1.382 1.38 1.38 0 0 0-1.38-1.382z"/></svg>
            LeetCode
          </a>
          <a href="https://www.geeksforgeeks.org/user/jhautkarsoko/" class="social-btn" target="_blank">
            <svg viewBox="0 0 24 24"><path d="M21.45 14.315c-.143.28-.334.532-.565.745a3.691 3.691 0 0 1-1.104.695 4.51 4.51 0 0 1-3.116-.016 3.79 3.79 0 0 1-1.106-.695 3.946 3.946 0 0 1-.894-1.407h7.785zm-18.9 0h7.784a3.946 3.946 0 0 1-.894 1.407 3.79 3.79 0 0 1-1.106.695 4.51 4.51 0 0 1-3.116.016 3.691 3.691 0 0 1-1.104-.695 3.584 3.584 0 0 1-.564-.745zM12 2.338L9.698 7.04H4.561l3.696 2.86-1.41 4.348L12 11.39l5.153 2.858-1.41-4.348 3.696-2.86h-5.137z"/></svg>
            GFG
          </a>
        </div>
      </div>

      <div class="hero-right">
        <img src="https://img.freepik.com/premium-vector/utch-man-viewed-from-side-behind-laptop-02-copy-5-01_961307-1185.jpg?w=740" alt="Developer illustration" />
      </div>
    </div>
    <hr class="divider" />
    <p class="section-label"><span>//</span> tech_stack</p>
    <div class="stack-block">
      <div class="stack-heading">
        <span class="stack-category cat-web">Web Dev</span>
        <span class="stack-name">Frontend</span>
      </div>
      <div class="chips">
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" />HTML5</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" />CSS3</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" />JavaScript</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/typescript/typescript-original.svg" />TypeScript</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original-wordmark.svg" />React</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/redux/redux-original.svg" />Redux</div>
        <div class="chip"><img src="https://avatars.githubusercontent.com/u/126103961?s=200&v=4" />Next.js</div>
        <div class="chip"><img src="https://www.vectorlogo.zone/logos/tailwindcss/tailwindcss-icon.svg" />Tailwind CSS</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/sass/sass-original.svg" />Sass</div>
        <div class="chip"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTmnwhTdzPeyGZYH2pD0vbYXAcPV_aBk24R-w&s" />Bootstrap</div>
        <div class="chip"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT4jlBbbeZsWHO-j5J4x7Fu5uO0eV-kNgKSLw&s" />React Native</div>
      </div>
    </div>
    <div class="stack-block">
      <div class="stack-heading">
        <span class="stack-category cat-web">Web Dev</span>
        <span class="stack-name">Backend &amp; Database</span>
      </div>
      <div class="chips">
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nodejs/nodejs-original-wordmark.svg" />Node.js</div>
        <div class="chip"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSFRztssUmVkQcDl8a8Jd4u8mZxOjX5jydMQA&s" />Express</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original-wordmark.svg" />MongoDB</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" />MySQL</div>
        <div class="chip"><img src="https://e7.pngegg.com/pngimages/170/924/png-clipart-microsoft-sql-server-microsoft-azure-sql-database-microsoft-text-logo.png" />SQL Server</div>
        <div class="chip"><img src="https://www.vectorlogo.zone/logos/firebase/firebase-icon.svg" />Firebase</div>
        <div class="chip"><img src="https://pipedream.com/s.v0/app_1dBhP3/logo/96" />Supabase</div>
        <div class="chip"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRdVEuXbieiDLdzyT-lHa1wtFVPK2ONT5utgQ&s" />Clerk</div>
        <div class="chip"><img src="https://tse3.mm.bing.net/th?id=OIP.-AtHh9D_i1lCL04yR64WzgHaHa&pid=Api&P=0&h=180" />WordPress</div>
      </div>
    </div>
    <div class="stack-block">
      <div class="stack-heading">
        <span class="stack-category cat-web">Web Dev</span>
        <span class="stack-name">Languages &amp; Tools</span>
      </div>
      <div class="chips">
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" />Python</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" />Java</div>
        <div class="chip"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg" />C</div>
        <div class="chip"><img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" />Git</div>
      </div>
    </div>
    <div class="stack-block">
      <div class="stack-heading">
        <span class="stack-category cat-chain">Blockchain Dev</span>
        <span class="stack-name">Web3 Stack</span>
      </div>
      <div class="chips">
        <div class="chip"><img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Ethereum_logo_2014.svg" />Solidity</div>
        <div class="chip"><img src="https://seeklogo.com/images/E/ethers-logo-D5B86204D7-seeklogo.com.png" />Ethers.js</div>
        <div class="chip"><img src="https://avatars.githubusercontent.com/u/44036562?s=200&v=4" style="border-radius:3px" />Hardhat</div>
        <div class="chip"><img src="https://upload.wikimedia.org/wikipedia/commons/3/36/MetaMask_Fox.svg" />MetaMask</div>
        <div class="chip"><img src="https://avatars.githubusercontent.com/u/2226135?s=200&v=4" style="border-radius:3px" />IPFS</div>
      </div>
    </div>
    <hr class="divider" />
    <p class="section-label"><span>//</span> github_stats</p>
    <div class="stats-grid">
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api?username=utkarshjha-2005&show_icons=true&locale=en&hide_border=true&bg_color=161b22&title_color=bc8cff&icon_color=3fb950&text_color=8b949e" alt="GitHub stats" />
      </div>
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api/top-langs?username=utkarshjha-2005&show_icons=true&locale=en&layout=compact&hide_border=true&bg_color=161b22&title_color=bc8cff&text_color=8b949e" alt="Top languages" />
      </div>
    </div>

  </div>
  <div class="footer">
    <span>README.md</span>
    <span>made with <span>♥</span> by Utkarsh</span>
  </div>

</div>

</body>
</html>
