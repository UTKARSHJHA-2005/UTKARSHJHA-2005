<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>GitHub README Generator</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;600&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0d1117;--surface:#161b22;--surface2:#1c2128;--surface3:#21262d;
  --border:rgba(255,255,255,0.08);--border-hover:rgba(255,255,255,0.18);
  --text:#e6edf3;--text2:#8b949e;--text3:#484f58;
  --blue:#58a6ff;--blue-dim:rgba(56,139,253,0.12);
  --purple:#bc8cff;--purple-dim:rgba(188,140,255,0.12);
  --green:#3fb950;--green-dim:rgba(63,185,80,0.1);
  --pink:#f778ba;--amber:#e3b341;
}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--text);font-family:'Syne',sans-serif;min-height:100vh}

/* LAYOUT */
.app{display:grid;grid-template-columns:420px 1fr;min-height:100vh}

/* SIDEBAR */
.sidebar{background:var(--surface);border-right:1px solid var(--border);overflow-y:auto;padding:0}
.sidebar-header{padding:1.25rem 1.5rem;border-bottom:1px solid var(--border);background:var(--surface2);position:sticky;top:0;z-index:10}
.sidebar-header h1{font-size:16px;font-weight:700;color:var(--text);letter-spacing:-0.02em}
.sidebar-header p{font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--text3);margin-top:3px}

.form-body{padding:1.25rem 1.5rem;display:flex;flex-direction:column;gap:1.25rem}

.section-group{background:var(--surface2);border:1px solid var(--border);border-radius:8px;overflow:hidden}
.section-group-title{padding:10px 14px;font-family:'JetBrains Mono',monospace;font-size:11px;font-weight:600;color:var(--text3);background:var(--surface3);border-bottom:1px solid var(--border);letter-spacing:0.08em;text-transform:uppercase}

.field{padding:10px 14px;border-bottom:1px solid var(--border)}
.field:last-child{border-bottom:none}
.field label{display:block;font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--text2);margin-bottom:6px}
.field input,.field textarea{width:100%;background:var(--surface);border:1px solid var(--border);border-radius:6px;padding:7px 10px;font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--text);outline:none;transition:border-color 0.2s}
.field input:focus,.field textarea:focus{border-color:var(--blue)}
.field textarea{resize:vertical;min-height:60px}
.field input::placeholder,.field textarea::placeholder{color:var(--text3)}

/* TECH CHECKBOXES */
.tech-grid{display:grid;grid-template-columns:1fr 1fr;gap:5px;padding:10px 14px}
.tech-check{display:flex;align-items:center;gap:7px;cursor:pointer;padding:4px 6px;border-radius:5px;transition:background 0.15s}
.tech-check:hover{background:rgba(255,255,255,0.04)}
.tech-check input[type=checkbox]{width:13px;height:13px;accent-color:var(--blue);cursor:pointer;flex-shrink:0}
.tech-check img{width:14px;height:14px;object-fit:contain}
.tech-check span{font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--text2)}
.tech-section-label{grid-column:1/-1;font-family:'JetBrains Mono',monospace;font-size:10px;font-weight:600;color:var(--text3);text-transform:uppercase;letter-spacing:0.1em;padding:6px 6px 2px;border-top:1px solid var(--border);margin-top:4px}
.tech-section-label:first-child{border-top:none;margin-top:0}

/* GENERATE BUTTON */
.gen-btn{margin:0 1.5rem 1.5rem;padding:11px;background:var(--blue);color:#0d1117;font-family:'JetBrains Mono',monospace;font-size:13px;font-weight:600;border:none;border-radius:8px;cursor:pointer;transition:opacity 0.2s,transform 0.1s;letter-spacing:0.02em}
.gen-btn:hover{opacity:0.88}
.gen-btn:active{transform:scale(0.98)}

/* PREVIEW PANEL */
.preview-panel{display:flex;flex-direction:column;overflow:hidden}
.preview-tabs{display:flex;background:var(--surface);border-bottom:1px solid var(--border);padding:0 1.5rem;gap:0}
.tab-btn{padding:12px 16px;font-family:'JetBrains Mono',monospace;font-size:12px;font-weight:500;color:var(--text2);border:none;background:none;cursor:pointer;border-bottom:2px solid transparent;transition:color 0.2s,border-color 0.2s;margin-bottom:-1px}
.tab-btn.active{color:var(--blue);border-bottom-color:var(--blue)}
.tab-btn:hover:not(.active){color:var(--text)}

.copy-btn{margin-left:auto;padding:6px 14px;background:var(--green-dim);border:1px solid rgba(63,185,80,0.25);border-radius:6px;color:var(--green);font-family:'JetBrains Mono',monospace;font-size:11px;font-weight:600;cursor:pointer;align-self:center;transition:background 0.2s}
.copy-btn:hover{background:rgba(63,185,80,0.2)}
.copy-btn.copied{color:var(--text);background:rgba(255,255,255,0.05);border-color:var(--border)}

.tab-content{flex:1;overflow:auto;display:none}
.tab-content.active{display:block}

/* PREVIEW */
#preview-frame{width:100%;height:100%;border:none;background:var(--bg)}

/* CODE OUTPUT */
#code-output{margin:0;padding:1.5rem;font-family:'JetBrains Mono',monospace;font-size:12px;line-height:1.7;color:#adbac7;background:var(--bg);white-space:pre-wrap;word-break:break-all;min-height:100%}

/* EMPTY STATE */
.empty-state{display:flex;flex-direction:column;align-items:center;justify-content:center;height:100%;gap:12px;color:var(--text3);font-family:'JetBrains Mono',monospace;font-size:13px}
.empty-state .icon{font-size:40px;opacity:0.3}

/* SCROLLBAR */
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border-hover);border-radius:3px}
</style>
</head>
<body>

<div class="app">

  <!-- ===== SIDEBAR ===== -->
  <div class="sidebar">
    <div class="sidebar-header">
      <h1>README Generator</h1>
      <p>// fill in your details → get your code</p>
    </div>

    <div class="form-body">

      <!-- PROFILE -->
      <div class="section-group">
        <div class="section-group-title">Profile</div>
        <div class="field"><label>Full Name</label><input id="f-name" placeholder="Utkarsh Jha" /></div>
        <div class="field"><label>Tagline / Quote</label><input id="f-tagline" placeholder="Code never lies — sometimes comments do" /></div>
        <div class="field"><label>Currently Exploring</label><input id="f-exploring" placeholder="Web3 & Blockchain" /></div>
        <div class="field"><label>Ask Me About</label><input id="f-askme" placeholder="Web Development" /></div>
        <div class="field"><label>Email</label><input id="f-email" type="email" placeholder="you@example.com" /></div>
        <div class="field"><label>Profile Image URL (optional)</label><input id="f-img" placeholder="https://..." /></div>
      </div>

      <!-- SOCIAL -->
      <div class="section-group">
        <div class="section-group-title">Social Links</div>
        <div class="field"><label>GitHub Username</label><input id="f-github" placeholder="utkarshjha-2005" /></div>
        <div class="field"><label>LinkedIn URL</label><input id="f-linkedin" placeholder="https://linkedin.com/in/..." /></div>
        <div class="field"><label>Instagram URL</label><input id="f-instagram" placeholder="https://instagram.com/..." /></div>
        <div class="field"><label>LeetCode URL</label><input id="f-leetcode" placeholder="https://leetcode.com/u/..." /></div>
        <div class="field"><label>GeeksForGeeks URL</label><input id="f-gfg" placeholder="https://geeksforgeeks.org/user/..." /></div>
      </div>

      <!-- TECH STACK -->
      <div class="section-group">
        <div class="section-group-title">Tech Stack</div>
        <div class="tech-grid" id="tech-grid">
          <!-- injected by JS -->
        </div>
      </div>

    </div>

    <button class="gen-btn" onclick="generate()">⚡ Generate README</button>
  </div>

  <!-- ===== PREVIEW PANEL ===== -->
  <div class="preview-panel">
    <div class="preview-tabs">
      <button class="tab-btn active" onclick="switchTab('preview',this)">Preview</button>
      <button class="tab-btn" onclick="switchTab('html',this)">HTML Code</button>
      <button class="tab-btn" onclick="switchTab('markdown',this)">Markdown</button>
      <button class="copy-btn" id="copy-btn" onclick="copyCode()">Copy</button>
    </div>

    <div class="tab-content active" id="tab-preview">
      <div class="empty-state" id="empty-state">
        <div class="icon">📄</div>
        <span>Fill in your details and click Generate</span>
      </div>
      <iframe id="preview-frame" style="display:none"></iframe>
    </div>

    <div class="tab-content" id="tab-html">
      <pre id="code-output">// Your HTML code will appear here after generating...</pre>
    </div>

    <div class="tab-content" id="tab-markdown">
      <pre id="md-output">// Your Markdown will appear here after generating...</pre>
    </div>
  </div>

</div>

<script>
const TECHS = [
  // Web Dev - Frontend
  {cat:'webfront', label:'HTML5',      img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg'},
  {cat:'webfront', label:'CSS3',       img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg'},
  {cat:'webfront', label:'JavaScript', img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg'},
  {cat:'webfront', label:'TypeScript', img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/typescript/typescript-original.svg'},
  {cat:'webfront', label:'React',      img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original-wordmark.svg'},
  {cat:'webfront', label:'Redux',      img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/redux/redux-original.svg'},
  {cat:'webfront', label:'Next.js',    img:'https://avatars.githubusercontent.com/u/126103961?s=200&v=4'},
  {cat:'webfront', label:'Tailwind',   img:'https://www.vectorlogo.zone/logos/tailwindcss/tailwindcss-icon.svg'},
  {cat:'webfront', label:'Sass',       img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/sass/sass-original.svg'},
  {cat:'webfront', label:'Bootstrap',  img:'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTmnwhTdzPeyGZYH2pD0vbYXAcPV_aBk24R-w&s'},
  {cat:'webfront', label:'React Native',img:'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT4jlBbbeZsWHO-j5J4x7Fu5uO0eV-kNgKSLw&s'},
  // Web Dev - Backend
  {cat:'webback',  label:'Node.js',    img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/nodejs/nodejs-original-wordmark.svg'},
  {cat:'webback',  label:'Express',    img:'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSFRztssUmVkQcDl8a8Jd4u8mZxOjX5jydMQA&s'},
  {cat:'webback',  label:'MongoDB',    img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original-wordmark.svg'},
  {cat:'webback',  label:'MySQL',      img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg'},
  {cat:'webback',  label:'SQL Server', img:'https://e7.pngegg.com/pngimages/170/924/png-clipart-microsoft-sql-server-microsoft-azure-sql-database-microsoft-text-logo.png'},
  {cat:'webback',  label:'Firebase',   img:'https://www.vectorlogo.zone/logos/firebase/firebase-icon.svg'},
  {cat:'webback',  label:'Supabase',   img:'https://pipedream.com/s.v0/app_1dBhP3/logo/96'},
  {cat:'webback',  label:'Clerk',      img:'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRdVEuXbieiDLdzyT-lHa1wtFVPK2ONT5utgQ&s'},
  {cat:'webback',  label:'WordPress',  img:'https://tse3.mm.bing.net/th?id=OIP.-AtHh9D_i1lCL04yR64WzgHaHa&pid=Api&P=0&h=180'},
  // Languages & Tools
  {cat:'tools',    label:'Python',     img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg'},
  {cat:'tools',    label:'Java',       img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg'},
  {cat:'tools',    label:'C',          img:'https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg'},
  {cat:'tools',    label:'Git',        img:'https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg'},
  // Blockchain
  {cat:'chain',    label:'Solidity',   img:'https://upload.wikimedia.org/wikipedia/commons/0/05/Ethereum_logo_2014.svg'},
  {cat:'chain',    label:'Ethers.js',  img:'https://seeklogo.com/images/E/ethers-logo-D5B86204D7-seeklogo.com.png'},
  {cat:'chain',    label:'Hardhat',    img:'https://avatars.githubusercontent.com/u/44036562?s=200&v=4'},
  {cat:'chain',    label:'MetaMask',   img:'https://upload.wikimedia.org/wikipedia/commons/3/36/MetaMask_Fox.svg'},
  {cat:'chain',    label:'IPFS',       img:'https://avatars.githubusercontent.com/u/2226135?s=200&v=4'},
  {cat:'chain',    label:'Web3.js',    img:'https://avatars.githubusercontent.com/u/6250754?s=200&v=4'},
  {cat:'chain',    label:'Truffle',    img:'https://avatars.githubusercontent.com/u/22205159?s=200&v=4'},
];

const CAT_LABELS = {
  webfront: 'Web Dev — Frontend',
  webback:  'Web Dev — Backend & Database',
  tools:    'Web Dev — Languages & Tools',
  chain:    'Blockchain Dev — Web3 Stack',
};

// Build checkbox grid
function buildTechGrid() {
  const grid = document.getElementById('tech-grid');
  let currentCat = null;
  TECHS.forEach((t, i) => {
    if (t.cat !== currentCat) {
      currentCat = t.cat;
      const lbl = document.createElement('div');
      lbl.className = 'tech-section-label';
      lbl.textContent = CAT_LABELS[t.cat];
      grid.appendChild(lbl);
    }
    const label = document.createElement('label');
    label.className = 'tech-check';
    label.innerHTML = `
      <input type="checkbox" data-idx="${i}" ${['HTML5','CSS3','JavaScript','React','Next.js','Node.js','Git'].includes(t.label)?'checked':''} />
      <img src="${t.img}" alt="${t.label}" />
      <span>${t.label}</span>`;
    grid.appendChild(label);
  });
}
buildTechGrid();

// Pre-fill with Utkarsh's data
document.getElementById('f-name').value = 'Utkarsh Jha';
document.getElementById('f-tagline').value = 'Code never lies — sometimes comments do';
document.getElementById('f-exploring').value = 'Web3 & Blockchain';
document.getElementById('f-askme').value = 'Web Development';
document.getElementById('f-email').value = 'jha.utkarsh2005@gmail.com';
document.getElementById('f-img').value = 'https://img.freepik.com/premium-vector/utch-man-viewed-from-side-behind-laptop-02-copy-5-01_961307-1185.jpg?w=740';
document.getElementById('f-github').value = 'utkarshjha-2005';
document.getElementById('f-linkedin').value = 'https://linkedin.com/in/utkarsh-jha-';
document.getElementById('f-instagram').value = 'https://www.instagram.com/utkarsh_jha_2005/';
document.getElementById('f-leetcode').value = 'https://leetcode.com/u/user4171b/';
document.getElementById('f-gfg').value = 'https://www.geeksforgeeks.org/user/jhautkarsoko/';
// Check all of Utkarsh's techs
document.querySelectorAll('#tech-grid input[type=checkbox]').forEach(cb => {
  const idx = parseInt(cb.dataset.idx);
  const name = TECHS[idx].label;
  if(['HTML5','CSS3','JavaScript','TypeScript','React','Redux','Next.js','Tailwind','Sass','Bootstrap','React Native',
      'Node.js','Express','MongoDB','MySQL','SQL Server','Firebase','Supabase','Clerk','WordPress',
      'Python','Java','C','Git','Solidity','Ethers.js','Hardhat','MetaMask','IPFS'].includes(name)) {
    cb.checked = true;
  }
});

let currentTab = 'preview';
let generatedHTML = '';

function switchTab(tab, btn) {
  currentTab = tab;
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
  document.getElementById('tab-' + tab).classList.add('active');
}

function copyCode() {
  const text = currentTab === 'markdown'
    ? document.getElementById('md-output').textContent
    : generatedHTML;
  if (!text || text.startsWith('//')) return;
  navigator.clipboard.writeText(text).then(() => {
    const btn = document.getElementById('copy-btn');
    btn.textContent = '✓ Copied!';
    btn.classList.add('copied');
    setTimeout(() => { btn.textContent = 'Copy'; btn.classList.remove('copied'); }, 2000);
  });
}

function getSelectedTechs() {
  const selected = {webfront:[], webback:[], tools:[], chain:[]};
  document.querySelectorAll('#tech-grid input[type=checkbox]:checked').forEach(cb => {
    const t = TECHS[parseInt(cb.dataset.idx)];
    selected[t.cat].push(t);
  });
  return selected;
}

function chipHtml(t) {
  return `<div class="chip"><img src="${t.img}" />${t.label}</div>`;
}

function stackBlock(catClass, badgeLabel, stackName, techs) {
  if (!techs.length) return '';
  return `
    <div class="stack-block">
      <div class="stack-heading">
        <span class="stack-category ${catClass}">${badgeLabel}</span>
        <span class="stack-name">${stackName}</span>
      </div>
      <div class="chips">
        ${techs.map(chipHtml).join('\n        ')}
      </div>
    </div>`;
}

function socialBtn(href, icon, label) {
  if (!href) return '';
  return `<a href="${href}" class="social-btn" target="_blank">${icon}${label}</a>`;
}

const ICONS = {
  linkedin: `<svg viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>`,
  instagram:`<svg viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg>`,
  leetcode: `<svg viewBox="0 0 24 24"><path d="M13.483 0a1.374 1.374 0 0 0-.961.438L7.116 6.226l-3.854 4.126a5.266 5.266 0 0 0-1.209 2.104 5.35 5.35 0 0 0-.125.513 5.527 5.527 0 0 0 .062 2.362 5.83 5.83 0 0 0 .349 1.017 5.938 5.938 0 0 0 1.271 1.818l4.277 4.193.039.038c2.248 2.165 5.852 2.133 8.063-.074l2.396-2.392c.54-.54.54-1.414.003-1.955a1.378 1.378 0 0 0-1.951-.003l-2.396 2.392a3.021 3.021 0 0 1-4.205.038l-.02-.019-4.276-4.193c-.652-.64-.972-1.469-.948-2.263a2.68 2.68 0 0 1 .066-.523 2.545 2.545 0 0 1 .619-1.164L9.13 8.114c1.058-1.134 3.204-1.27 4.43-.278l3.501 2.831c.593.48 1.461.387 1.94-.207a1.384 1.384 0 0 0-.207-1.943l-3.5-2.831c-.8-.647-1.766-1.045-2.774-1.202l2.015-2.158A1.384 1.384 0 0 0 13.483 0zm-2.866 12.815a1.38 1.38 0 0 0-1.38 1.382 1.38 1.38 0 0 0 1.38 1.382H20.79a1.38 1.38 0 0 0 1.38-1.382 1.38 1.38 0 0 0-1.38-1.382z"/></svg>`,
  gfg:      `<svg viewBox="0 0 24 24"><path d="M21.45 14.315c-.143.28-.334.532-.565.745a3.691 3.691 0 0 1-1.104.695 4.51 4.51 0 0 1-3.116-.016 3.79 3.79 0 0 1-1.106-.695 3.946 3.946 0 0 1-.894-1.407h7.785zm-18.9 0h7.784a3.946 3.946 0 0 1-.894 1.407 3.79 3.79 0 0 1-1.106.695 4.51 4.51 0 0 1-3.116.016 3.691 3.691 0 0 1-1.104-.695 3.584 3.584 0 0 1-.564-.745zM12 2.338L9.698 7.04H4.561l3.696 2.86-1.41 4.348L12 11.39l5.153 2.858-1.41-4.348 3.696-2.86h-5.137z"/></svg>`,
};

function buildReadmeHTML(data) {
  const { name, tagline, exploring, askme, email, img, github, linkedin, instagram, leetcode, gfg, techs } = data;

  const socialBtns = [
    socialBtn(linkedin,   ICONS.linkedin,   'LinkedIn'),
    socialBtn(instagram,  ICONS.instagram,  'Instagram'),
    socialBtn(leetcode,   ICONS.leetcode,   'LeetCode'),
    socialBtn(gfg,        ICONS.gfg,        'GFG'),
  ].filter(Boolean).join('\n          ');

  const imgHtml = img ? `
      <div class="hero-right">
        <img src="${img}" alt="Profile illustration" />
      </div>` : '';

  const stackHtml = [
    stackBlock('cat-web',   'Web Dev',        'Frontend',              techs.webfront),
    stackBlock('cat-web',   'Web Dev',        'Backend &amp; Database', techs.webback),
    stackBlock('cat-web',   'Web Dev',        'Languages &amp; Tools',  techs.tools),
    stackBlock('cat-chain', 'Blockchain Dev', 'Web3 Stack',             techs.chain),
  ].filter(Boolean).join('\n');

  const statsHtml = github ? `
    <hr class="divider" />
    <p class="section-label"><span>//</span> github_stats</p>
    <div class="stats-grid">
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api?username=${github}&show_icons=true&hide_border=true&bg_color=161b22&title_color=bc8cff&icon_color=3fb950&text_color=8b949e" alt="GitHub stats" />
      </div>
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api/top-langs?username=${github}&layout=compact&hide_border=true&bg_color=161b22&title_color=bc8cff&text_color=8b949e" alt="Top languages" />
      </div>
    </div>` : '';

  return `<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>${name} — README</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;600&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{--bg:#0d1117;--surface:#161b22;--surface2:#1c2128;--border:rgba(255,255,255,0.08);--border-hover:rgba(255,255,255,0.18);--text:#e6edf3;--text2:#8b949e;--text3:#484f58;--blue:#58a6ff;--blue-dim:rgba(56,139,253,0.12);--purple:#bc8cff;--purple-dim:rgba(188,140,255,0.12);--green:#3fb950;--pink:#f778ba;}
body{background:var(--bg);color:var(--text);font-family:'Syne',sans-serif;min-height:100vh;padding:2rem;}
.readme-card{max-width:820px;margin:0 auto;background:var(--surface);border:1px solid var(--border);border-radius:12px;overflow:hidden;}
.top-bar{background:var(--surface2);border-bottom:1px solid var(--border);padding:10px 16px;display:flex;align-items:center;gap:8px;}
.dot-r{width:12px;height:12px;border-radius:50%;background:#ff5f57;}
.dot-y{width:12px;height:12px;border-radius:50%;background:#febc2e;}
.dot-g{width:12px;height:12px;border-radius:50%;background:#28c840;}
.tab-label{margin-left:12px;font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--text2);}
.tab-label span{color:var(--green);}
.content{padding:2rem 2.5rem;}
.hero{display:flex;gap:2rem;align-items:flex-start;margin-bottom:2rem;}
.hero-left{flex:1;min-width:0;}
.hero-right{flex-shrink:0;}
.hero-right img{width:190px;height:190px;object-fit:cover;border-radius:10px;border:1px solid var(--border);display:block;}
.greeting{font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--green);margin-bottom:8px;}
h1{font-family:'Syne',sans-serif;font-size:32px;font-weight:800;color:var(--text);line-height:1.1;margin-bottom:6px;}
.tagline{font-family:'JetBrains Mono',monospace;font-size:13px;color:var(--text3);margin-bottom:20px;font-style:italic;}
.tagline span{color:var(--purple);font-style:normal;}
.info-list{display:flex;flex-direction:column;gap:8px;margin-bottom:20px;}
.info-item{display:flex;align-items:center;gap:10px;font-size:13px;color:var(--text2);font-family:'JetBrains Mono',monospace;}
.info-item::before{content:'›';color:var(--blue);font-size:16px;line-height:1;}
.info-item a{color:var(--pink);text-decoration:none;}
.info-item strong{color:var(--text);font-weight:500;}
.social-row{display:flex;gap:8px;flex-wrap:wrap;}
.social-btn{display:flex;align-items:center;gap:6px;font-size:12px;font-weight:600;font-family:'JetBrains Mono',monospace;padding:5px 12px;border-radius:6px;border:1px solid var(--border);color:var(--text2);text-decoration:none;background:var(--surface2);}
.social-btn svg{width:13px;height:13px;fill:currentColor;flex-shrink:0;}
.divider{border:none;border-top:1px solid var(--border);margin:1.75rem 0;}
.section-label{font-family:'JetBrains Mono',monospace;font-size:11px;letter-spacing:0.1em;text-transform:uppercase;color:var(--text3);margin-bottom:1.25rem;}
.section-label span{color:var(--green);}
.stack-block{margin-bottom:1.5rem;}
.stack-heading{display:flex;align-items:center;gap:10px;margin-bottom:10px;}
.stack-category{font-family:'JetBrains Mono',monospace;font-size:11px;font-weight:600;padding:2px 10px;border-radius:99px;border:1px solid;}
.cat-web{background:var(--blue-dim);color:var(--blue);border-color:rgba(88,166,255,0.25);}
.cat-chain{background:var(--purple-dim);color:var(--purple);border-color:rgba(188,140,255,0.25);}
.stack-name{font-size:13px;font-weight:600;color:var(--text2);}
.chips{display:flex;flex-wrap:wrap;gap:6px;}
.chip{display:flex;align-items:center;gap:6px;font-size:12px;font-family:'JetBrains Mono',monospace;padding:4px 10px;border-radius:6px;border:1px solid var(--border);background:var(--surface2);color:var(--text2);}
.chip img{width:14px;height:14px;object-fit:contain;}
.stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
.stat-card{background:var(--surface2);border:1px solid var(--border);border-radius:8px;overflow:hidden;}
.stat-card img{width:100%;display:block;}
.footer{border-top:1px solid var(--border);padding:12px 2.5rem;font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--text3);display:flex;justify-content:space-between;align-items:center;}
.footer span{color:var(--green);}
</style>
</head>
<body>
<div class="readme-card">
  <div class="top-bar">
    <div class="dot-r"></div><div class="dot-y"></div><div class="dot-g"></div>
    <span class="tab-label"><span>${github || 'username'}</span> / README.md</span>
  </div>
  <div class="content">
    <div class="hero">
      <div class="hero-left">
        <p class="greeting">// hi there, I'm</p>
        <h1>${name}</h1>
        <p class="tagline"><span>"</span>${tagline}<span>"</span></p>
        <div class="info-list">
          ${exploring ? `<div class="info-item">Currently exploring <strong>${exploring}</strong></div>` : ''}
          ${askme    ? `<div class="info-item">Ask me about <strong>${askme}</strong></div>` : ''}
          ${email    ? `<div class="info-item"><a href="mailto:${email}">${email}</a></div>` : ''}
        </div>
        <div class="social-row">
          ${socialBtns}
        </div>
      </div>${imgHtml}
    </div>
    <hr class="divider" />
    <p class="section-label"><span>//</span> tech_stack</p>
    ${stackHtml}
    ${statsHtml}
  </div>
  <div class="footer">
    <span>README.md</span>
    <span>made with <span>♥</span> by ${name}</span>
  </div>
</div>
</body>
</html>`;
}

function buildMarkdown(data) {
  const { name, tagline, exploring, askme, email, img, github, linkedin, instagram, leetcode, gfg, techs } = data;
  let md = '';
  md += `<h1 align="center">Hi 👋, I'm ${name}</h1>\n`;
  md += `<h3 align="center">${tagline}</h3>\n\n`;
  if (img) md += `<img src="${img}" width="300" align="right" />\n\n`;
  if (exploring) md += `🌱 Currently exploring **${exploring}**\n\n`;
  if (askme)     md += `💬 Ask me about **${askme}**\n\n`;
  if (email)     md += `📫 Reach me at **${email}**\n\n`;
  md += `### Connect with me:\n`;
  if (linkedin)  md += `[![LinkedIn](https://img.shields.io/badge/LinkedIn-blue?style=flat&logo=linkedin)](${linkedin}) `;
  if (instagram) md += `[![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=flat&logo=instagram&logoColor=white)](${instagram}) `;
  if (leetcode)  md += `[![LeetCode](https://img.shields.io/badge/LeetCode-FFA116?style=flat&logo=leetcode&logoColor=black)](${leetcode}) `;
  if (gfg)       md += `[![GFG](https://img.shields.io/badge/GeeksForGeeks-0F9D58?style=flat&logo=geeksforgeeks&logoColor=white)](${gfg})`;
  md += '\n\n';
  md += `### 🌐 Web Dev — Frontend\n`;
  techs.webfront.forEach(t => { md += `![${t.label}](https://img.shields.io/badge/${encodeURIComponent(t.label)}-informational?style=flat&logo=${t.label.toLowerCase()}) `; });
  md += '\n\n';
  md += `### ⚙️ Web Dev — Backend & Database\n`;
  techs.webback.forEach(t => { md += `![${t.label}](https://img.shields.io/badge/${encodeURIComponent(t.label)}-informational?style=flat) `; });
  md += '\n\n';
  md += `### 🔧 Web Dev — Languages & Tools\n`;
  techs.tools.forEach(t => { md += `![${t.label}](https://img.shields.io/badge/${encodeURIComponent(t.label)}-informational?style=flat) `; });
  md += '\n\n';
  if (techs.chain.length) {
    md += `### ⛓️ Blockchain Dev — Web3 Stack\n`;
    techs.chain.forEach(t => { md += `![${t.label}](https://img.shields.io/badge/${encodeURIComponent(t.label)}-informational?style=flat) `; });
    md += '\n\n';
  }
  if (github) {
    md += `### 📊 GitHub Stats\n`;
    md += `![GitHub Stats](https://github-readme-stats.vercel.app/api?username=${github}&show_icons=true&hide_border=true)\n`;
    md += `![Top Languages](https://github-readme-stats.vercel.app/api/top-langs?username=${github}&layout=compact&hide_border=true)\n`;
  }
  return md;
}

function generate() {
  const data = {
    name:       document.getElementById('f-name').value.trim() || 'Your Name',
    tagline:    document.getElementById('f-tagline').value.trim(),
    exploring:  document.getElementById('f-exploring').value.trim(),
    askme:      document.getElementById('f-askme').value.trim(),
    email:      document.getElementById('f-email').value.trim(),
    img:        document.getElementById('f-img').value.trim(),
    github:     document.getElementById('f-github').value.trim(),
    linkedin:   document.getElementById('f-linkedin').value.trim(),
    instagram:  document.getElementById('f-instagram').value.trim(),
    leetcode:   document.getElementById('f-leetcode').value.trim(),
    gfg:        document.getElementById('f-gfg').value.trim(),
    techs:      getSelectedTechs(),
  };

  generatedHTML = buildReadmeHTML(data);
  const md = buildMarkdown(data);

  // Update preview
  document.getElementById('empty-state').style.display = 'none';
  const frame = document.getElementById('preview-frame');
  frame.style.display = 'block';
  frame.style.height = '100%';
  frame.srcdoc = generatedHTML;

  // Update code
  document.getElementById('code-output').textContent = generatedHTML;
  document.getElementById('md-output').textContent = md;
}
</script>
</body>
</html>
