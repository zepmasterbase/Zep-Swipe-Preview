<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Zep Swipe — MVP with Learn & Earn + Light Mode</title>

  <!-- Tailwind CDN (fast prototyping) -->
  <script src="https://cdn.tailwindcss.com"></script>

  <!-- Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">

  <style>
    :root{
      --glass-bg: rgba(255,255,255,0.06);
      --accent-a: #00f0ff;
      --accent-b: #ff00d4;
      --accent-c: #8b5cf6;
    }
    html,body { height:100%; }
    body{
      margin:0;
      font-family: 'Inter', sans-serif;
      background: linear-gradient(135deg,#081028 0%, #1b123a 60%, #0b1220 100%);
      color: #e6eef8;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      overflow-x:hidden;
    }

    /* Canvas background */
    canvas#bg { position: fixed; inset:0; width:100%; height:100%; z-index:-2; }

    /* subtle radial vignette */
    .vignette { position: fixed; inset:0; background: radial-gradient(60% 60% at 50% 20%, rgba(0,0,0,0.12), rgba(0,0,0,0.6)); z-index:-1; pointer-events:none; }

    /* Neon heading */
    .neon {
      background: linear-gradient(90deg, var(--accent-a), var(--accent-b), var(--accent-c));
      -webkit-background-clip:text; background-clip:text;
      -webkit-text-fill-color:transparent;
      text-shadow: 0 0 6px rgba(0,240,255,0.12), 0 0 18px rgba(255,0,212,0.06);
    }

    /* glass cards */
    .glass {
      background: var(--glass-bg);
      backdrop-filter: blur(8px) saturate(120%);
      border: 1px solid rgba(255,255,255,0.06);
      border-radius: 14px;
    }

    /* gradient button */
    .glow-btn {
      background: linear-gradient(90deg, rgba(0,240,255,0.95), rgba(255,0,212,0.95));
      color:#071026;
      font-weight:600;
      border-radius: 10px;
      padding: .65rem 1.15rem;
      transition: transform .15s ease, box-shadow .2s ease;
      box-shadow: 0 6px 18px rgba(0,240,255,0.08), 0 2px 8px rgba(255,0,212,0.04);
    }
    .glow-btn:hover { transform: translateY(-3px); box-shadow: 0 12px 36px rgba(0,240,255,0.12), 0 6px 24px rgba(255,0,212,0.08); }

    /* small utilities */
    .muted { color: #9fb0cc; }
    .badge {
      background: linear-gradient(90deg, rgba(0,240,255,0.9), rgba(139,92,246,0.9));
      padding:.25rem .6rem; border-radius:999px; color:#071026; font-weight:600; font-size:.85rem;
    }

    /* progress bar */
    .progress-track { background: rgba(255,255,255,0.06); border-radius:12px; height:14px; overflow:hidden; }
    .progress-fill { height:100%; background: linear-gradient(90deg,var(--accent-a),var(--accent-b)); width:0%; transition:width .6s cubic-bezier(.2,.9,.3,1); }

    /* fade-up animation */
    .fade-up { opacity:0; transform: translateY(18px); transition: all .7s cubic-bezier(.15,.6,.3,1); }
    .visible { opacity:1; transform:translateY(0); }

    /* responsive tweaks */
    @media (min-width:768px){
      .hero-title { font-size: clamp(2.1rem, 4vw, 3.8rem); }
    }
  </style>
</head>
<body>

  <!-- Particle Canvas + Vignette -->
  <canvas id="bg"></canvas>
  <div class="vignette"></div>

  <!-- NAV -->
  <header class="fixed top-4 left-1/2 transform -translate-x-1/2 w-[94%] max-w-5xl z-40">
    <div class="flex justify-between items-center glass px-4 py-3">
      <div class="flex items-center gap-3">
        <div class="rounded-md px-3 py-1 badge">ZEP</div>
        <a href="#top" class="text-xl font-bold neon">Zep Swipe</a>
        <span class="ml-3 muted">MVP</span>
      </div>

      <div class="flex items-center gap-3">
        <div id="modeLabel" class="text-sm px-3 py-1 glass rounded-md muted">Zep Swipe Light</div>
        <div class="glass px-3 py-1 rounded-md flex items-center gap-2">
          <div class="text-xs muted">ZAC</div>
          <div id="zacBalance" class="font-semibold">0</div>
        </div>
        <button id="connectBtn" class="glow-btn">Connect Wallet</button>
      </div>
    </div>
  </header>

  <!-- MAIN -->
  <main class="pt-28 pb-20">
    <section class="max-w-5xl mx-auto px-4 lg:px-0 grid grid-cols-1 lg:grid-cols-3 gap-6">
      <!-- LEFT: Hero / Quick actions -->
      <div class="col-span-2 space-y-6">
        <div class="glass p-6 fade-up" id="heroCard">
          <div class="flex justify-between items-start">
            <div>
              <h1 class="hero-title neon text-3xl font-bold">Zep Swipe — Learn • Earn • Explore</h1>
              <p class="muted mt-2">A lightweight cyber-futuristic landing page that lets students learn and earn tokens before they transact.</p>
            </div>
            <div class="text-right">
              <div class="muted text-sm">Mode</div>
              <div id="modeToggleWrap" class="mt-2">
                <label class="inline-flex items-center gap-2">
                  <input id="lightModeToggle" type="checkbox" checked class="rounded"/>
                  <span class="text-sm">Light (Explore)</span>
                </label>
              </div>
            </div>
          </div>

          <div class="mt-6 flex flex-col sm:flex-row gap-3">
            <button id="openLearnBtn" class="glow-btn">Learn & Earn</button>
            <button id="openShopBtn" class="px-4 py-2 glass rounded-md">Shop (Demo)</button>
            <button id="openChatBtn" class="px-4 py-2 glass rounded-md">Chat (Demo)</button>
          </div>

          <div class="mt-6 grid grid-cols-1 sm:grid-cols-3 gap-3">
            <div class="glass p-3 rounded-md text-center">
              <div class="muted text-sm">Level</div>
              <div id="levelDisplay" class="text-xl font-bold">1</div>
            </div>
            <div class="glass p-3 rounded-md text-center">
              <div class="muted text-sm">XP</div>
              <div id="xpDisplay" class="text-xl font-bold">0</div>
            </div>
            <div class="glass p-3 rounded-md text-center">
              <div class="muted text-sm">Badges</div>
              <div id="badgesDisplay" class="text-xl font-bold">0</div>
            </div>
          </div>

          <div class="mt-6">
            <div class="flex justify-between items-center mb-2">
              <div class="muted text-sm">Progress to next level</div>
              <div class="text-sm font-semibold" id="progressPct">0%</div>
            </div>
            <div class="progress-track">
              <div id="progressFill" class="progress-fill"></div>
            </div>
          </div>
        </div>

        <!-- Learn & Earn / Dashboard -->
        <div class="glass p-6 fade-up" id="dashboard">
          <div class="flex justify-between items-center">
            <h2 class="neon font-semibold text-xl">Student Dashboard</h2>
            <div class="muted text-sm">University: <strong id="studentUni">Cape Town Uni</strong></div>
          </div>

          <div class="mt-4 grid md:grid-cols-2 gap-4">
            <div class="glass p-4 rounded-md">
              <div class="flex justify-between items-center">
                <div>
                  <div class="muted text-sm">Learn & Earn</div>
                  <div class="font-semibold">5 Levels • Earn ZAC</div>
                </div>
                <div>
                  <button id="dashboardLearnBtn" class="glow-btn text-sm">Open</button>
                </div>
              </div>
              <div class="mt-3 muted text-sm">Complete lessons / quizzes to unlock levels.</div>
            </div>

            <div class="glass p-4 rounded-md">
              <div class="flex justify-between items-center">
                <div>
                  <div class="muted text-sm">Shop (demo)</div>
                  <div class="font-semibold">View items, try checkout</div>
                </div>
                <div>
                  <button id="shopDemoBtn" class="px-3 py-2 glass rounded-md">Browse</button>
                </div>
              </div>
              <div class="mt-3 muted text-sm">Transactions require wallet / phone connect.</div>
            </div>
          </div>

          <!-- Leaderboard -->
          <div class="mt-6">
            <div class="flex justify-between items-center">
              <h3 class="font-semibold">University Leaderboard</h3>
              <div class="muted text-sm">Top students (mock)</div>
            </div>
            <div id="leaderboard" class="mt-3 space-y-2">
              <!-- populated by JS -->
            </div>
          </div>
        </div>
      </div>

      <!-- RIGHT: Shop / Quick profile -->
      <aside class="space-y-6">
        <div class="glass p-4 fade-up">
          <div class="flex items-center gap-3">
            <div class="rounded-full bg-gradient-to-tr from-cyan-400 to-purple-500 w-12 h-12 flex items-center justify-center text-xl font-bold">S</div>
            <div>
              <div class="muted text-xs">Student</div>
              <div id="studentName" class="font-semibold">Sam Student</div>
            </div>
          </div>

          <div class="mt-4">
            <div class="muted text-xs">Wallet Balance</div>
            <div class="text-2xl font-bold"><span id="walletZac">0</span> <span class="muted text-sm">ZAC</span></div>
          </div>

        </div>

        <div class="glass p-4 fade-up">
          <h4 class="font-semibold">Quick Actions</h4>
          <div class="mt-3 grid grid-cols-1 gap-2">
            <button id="claimDemoBtn" class="px-3 py-2 glass rounded-md">Claim Demo Item</button>
            <button id="viewLevelsBtn" class="px-3 py-2 glass rounded-md">View Levels</button>
          </div>
        </div>

        <div class="glass p-4 fade-up">
          <h4 class="font-semibold">University</h4>
          <div class="mt-2">
            <select id="uniSelect" class="w-full p-2 rounded-md bg-[#071026]">
              <option>Cape Town Uni</option>
              <option>University of Nairobi</option>
              <option>University of Lagos</option>
              <option>Makerere University</option>
            </select>
          </div>
        </div>

      </aside>
    </section>
  </main>

  <!-- FOOTER -->
  <footer class="fixed bottom-4 left-1/2 transform -translate-x-1/2 w-[94%] max-w-4xl z-40">
    <div class="glass px-4 py-3 flex justify-between items-center">
      <div class="flex items-center gap-4">
        <button id="chatBtn" class="px-3 py-2 glass rounded-md">Chat</button>
        <button id="shopBtn" class="px-3 py-2 glass rounded-md">Shop</button>
        <!-- Learn & Earn icon in footer -->
        <button id="footerLearnBtn" class="px-3 py-2 glass rounded-md">Learn & Earn</button>
      </div>
      <div class="muted text-sm">© 2025 Zep Swipe — Futuristic Neon Glass</div>
    </div>
  </footer>

  <!-- MODALS / OVERLAYS -->
  <div id="modalRoot"></div>

  <script>
  /* ===========================
     State + Persistence (localStorage demo)
     - user: {name, uni, level, xp, badges, zac, lightMode}
     - leaderboards per uni
     - NOTE: Replace localStorage logic with Firestore reads/writes for production.
     =========================== */

  const DEFAULT_USER = {
    id: 'user-' + Math.random().toString(36).slice(2,8),
    name: 'Sam Student',
    uni: 'Cape Town Uni',
    level: 1,
    xp: 0,
    badges: [],
    zac: 0,
    lightMode: true
  };

  // Keys
  const KEY_USER = 'zep_user_v1';
  const KEY_LEADER = 'zep_leader_v1';

  // Load or create user
  let user = JSON.parse(localStorage.getItem(KEY_USER) || 'null') || DEFAULT_USER;
  // Ensure badges array
  if(!Array.isArray(user.badges)) user.badges = [];

  // Load or init leaderboard
  let leaderData = JSON.parse(localStorage.getItem(KEY_LEADER) || 'null');
  if(!leaderData){
    leaderData = {
      'Cape Town Uni': [
        {name:'Ayo', xp:140},
        {name:'Lindi', xp:120},
        {name:'Sam Student', xp:0}
      ],
      'University of Nairobi': [
        {name:'Esther', xp:200},
        {name:'Juma', xp:160}
      ]
    };
    localStorage.setItem(KEY_LEADER, JSON.stringify(leaderData));
  }

  // Save helper
  function saveUser(){
    localStorage.setItem(KEY_USER, JSON.stringify(user));
    // (Optional) syncToFirestore(user) // placeholder for real DB
  }

  // UI binding
  const zacBalanceEls = [document.getElementById('zacBalance'), document.getElementById('walletZac')];
  function renderUI(){
    document.getElementById('studentName').textContent = user.name;
    document.getElementById('studentUni').textContent = user.uni;
    document.getElementById('levelDisplay').textContent = user.level;
    document.getElementById('xpDisplay').textContent = user.xp;
    document.getElementById('badgesDisplay').textContent = user.badges.length;
    zacBalanceEls.forEach(e => e.textContent = user.zac);
    document.getElementById('modeLabel').textContent = user.lightMode ? 'Zep Swipe Light' : 'Zep Swipe Full';
    document.getElementById('lightModeToggle').checked = user.lightMode;
    // progress (levels require 100 XP each for demo)
    const nextLevelXP = 100;
    const pct = Math.min(100, Math.round((user.xp % nextLevelXP) / nextLevelXP * 100));
    document.getElementById('progressPct').textContent = pct + '%';
    document.getElementById('progressFill').style.width = pct + '%';
    // leaderboard render
    renderLeaderboard();
  }

  function renderLeaderboard(){
    const list = leaderData[user.uni] || [];
    // include current user if missing
    if(!list.some(x => x.name === user.name)){
      list.push({name: user.name, xp: user.xp});
      leaderData[user.uni] = list;
    }
    // sort desc
    const sorted = [...list].sort((a,b)=> b.xp - a.xp).slice(0,6);
    const wrap = document.getElementById('leaderboard');
    wrap.innerHTML = '';
    sorted.forEach((r, idx) => {
      const el = document.createElement('div');
      el.className = 'glass p-3 rounded-md flex items-center justify-between';
      el.innerHTML = `<div class="flex items-center gap-3"><div class="w-8 h-8 rounded-full bg-gradient-to-tr from-cyan-400 to-purple-500 flex items-center justify-center text-sm font-semibold">${idx+1}</div>
                      <div><div class="font-semibold">${r.name}</div><div class="muted text-xs">xp ${r.xp}</div></div></div>
                      <div class="text-sm muted">${r.name===user.name? 'You': ''}</div>`;
      wrap.appendChild(el);
    });
  }

  // initial render
  renderUI();

  /* ===========================
     Light Mode / Transaction gating
  ============================*/
  document.getElementById('lightModeToggle').addEventListener('change', (e)=>{
    user.lightMode = e.target.checked;
    saveUser(); renderUI();
  });

  // "attemptTransaction" - used when user tries to buy or checkout
  function attemptTransaction(){
    if(user.lightMode){
      showModal({
        title: 'Unlock full access',
        html: `<p class="muted">To perform transactions you must connect your wallet or provide your phone number.</p>
               <div class="mt-4 flex gap-2"><button id="doConnect" class="glow-btn">Connect Wallet</button>
               <button id="doPhone" class="px-3 py-2 glass rounded-md">Use Phone</button></div>`,
        onOpen(mod){
          mod.querySelector('#doConnect').addEventListener('click', ()=>{ connectWalletMock(); mod.remove(); });
          mod.querySelector('#doPhone').addEventListener('click', ()=>{ phoneAuthMock(); mod.remove(); });
        }
      });
      return false;
    }
    return true;
  }

  function connectWalletMock(){
    // simple mock: flip mode off and mark as connected
    user.lightMode = false;
    user.zac += 5; // welcome bonus
    saveUser(); renderUI(); toast('Wallet connected — welcome bonus 5 ZAC!');
  }
  function phoneAuthMock(){
    user.lightMode = false;
    user.zac += 3;
    saveUser(); renderUI(); toast('Phone linked — welcome bonus 3 ZAC!');
  }

  // Connect button
  document.getElementById('connectBtn').addEventListener('click', ()=>{
    attemptTransaction();
  });

  /* ===========================
     Learn & Earn module
     - 5 levels
     - mini lessons and quizzes
     - rewards ZAC tokens (mock)
     =========================== */

  const LEVELS = [
    {id:1, title:'Level 1 — Intro to Crypto', xpReq:100, rewardZac:5, quiz:[{q:'What stores transaction history?', a:'Blockchain'}]},
    {id:2, title:'Level 2 — Wallet Basics', xpReq:100, rewardZac:7, quiz:[{q:'Private keys should be?', a:'Private'}]},
    {id:3, title:'Level 3 — Payments', xpReq:100, rewardZac:10, quiz:[{q:'Transaction confirmations are by?', a:'Network'}]},
    {id:4, title:'Level 4 — Security', xpReq:100, rewardZac:12, quiz:[{q:'Never share your?', a:'Private key'}]},
    {id:5, title:'Level 5 — Advanced', xpReq:100, rewardZac:20, quiz:[{q:'Smart contracts run on?', a:'Blockchain'}]}
  ];

  // Open Learn modal
  document.getElementById('openLearnBtn').addEventListener('click', ()=> openLearnModal());
  document.getElementById('dashboardLearnBtn').addEventListener('click', ()=> openLearnModal());
  document.getElementById('footerLearnBtn').addEventListener('click', ()=> openLearnModal());

  function openLearnModal(){
    // modal lists levels and progress; allow entering the next locked/unlocked level
    const content = document.createElement('div');
    content.innerHTML = `
      <div>
        <p class="muted">Complete mini lessons or a short quiz to earn XP and ZAC. Progress unlocks next level.</p>
        <div id="levelsWrap" class="mt-4 space-y-3"></div>
      </div>
    `;
    showModal({
      title: 'Learn & Earn',
      htmlNode: content,
      onOpen(mod){
        renderLevels(mod.querySelector('#levelsWrap'));
      }
    });
  }

  function renderLevels(container){
    container.innerHTML = '';
    LEVELS.forEach(l=>{
      const levelXP = l.xpReq;
      const attained = user.level > l.id || (user.level === l.id && (user.xp % levelXP) === 0 && user.xp !== 0);
      const isUnlocked = user.level >= l.id;
      const div = document.createElement('div');
      div.className = 'glass p-3 rounded-md flex items-center justify-between';
      div.innerHTML = `<div>
          <div class="font-semibold">${l.title}</div>
          <div class="muted text-xs">Reward: ${l.rewardZac} ZAC • XP to clear: ${levelXP}</div>
        </div>
        <div class="flex flex-col items-end gap-2">
          <div class="muted text-xs">Level ${l.id}</div>
          <div class="flex gap-2">
            <button class="px-3 py-1 glass rounded-md btn-enter" data-level="${l.id}" ${isUnlocked? '':'disabled'}>Enter</button>
            <button class="px-3 py-1 glass rounded-md btn-preview" data-level="${l.id}">Preview</button>
          </div>
        </div>`;
      container.appendChild(div);
    });

    // attach handlers
    container.querySelectorAll('.btn-preview').forEach(b=>{
      b.addEventListener('click', (e)=>{
        const lv = Number(e.currentTarget.dataset.level);
        showLessonPreview(lv);
      });
    });
    container.querySelectorAll('.btn-enter').forEach(b=>{
      b.addEventListener('click', (e)=>{
        const lv = Number(e.currentTarget.dataset.level);
        if(lv > user.level){
          toast('Level locked. Complete previous levels first.');
          return;
        }
        openLevelFlow(lv);
      });
    });
  }

  function showLessonPreview(levelId){
    const L = LEVELS.find(x=>x.id===levelId);
    showModal({
      title: `Preview • ${L.title}`,
      html: `<p class="muted">Short mini-lesson: ${L.title}. This level covers core concepts.</p><div class="mt-4 muted text-sm">Example quiz question: ${L.quiz[0].q}</div>`,
    });
  }

  function openLevelFlow(levelId){
    const L = LEVELS.find(x=>x.id===levelId);
    // For demo: show mini-lesson then a quiz (single question)
    showModal({
      title: `${L.title}`,
      html: `<div>
          <p class="muted">Mini-lesson (brief): <strong>${L.title}</strong> — learn key ideas.</p>
          <div class="mt-4">
            <p class="muted text-sm">Ready for a quick quiz to earn XP & ZAC?</p>
            <div class="mt-4"><button id="startQuiz" class="glow-btn">Start Quiz</button></div>
          </div>
        </div>`,
      onOpen(mod){
        mod.querySelector('#startQuiz').addEventListener('click', ()=>{
          openQuiz(L, mod);
        });
      }
    });
  }

  function openQuiz(levelObj, parentModal){
    // small one-question quiz for demo
    const q = levelObj.quiz[0];
    parentModal.innerHTML = `<div>
      <p class="muted font-semibold">${q.q}</p>
      <input id="quizAns" class="w-full mt-3 p-2 rounded-md bg-[#071026]" placeholder="Your answer">
      <div class="mt-3 flex gap-2">
        <button id="submitQuiz" class="glow-btn">Submit</button>
        <button id="cancelQuiz" class="px-3 py-2 glass rounded-md">Cancel</button>
      </div>
    </div>`;
    parentModal.querySelector('#submitQuiz').addEventListener('click', ()=>{
      const ans = parentModal.querySelector('#quizAns').value.trim().toLowerCase();
      // naive check: see if answer includes expected word
      const expected = q.a.toLowerCase();
      if(ans.includes(expected) || expected.includes(ans) || ans.length>0 && expected.length>0 && expected.split(' ')[0]===ans.split(' ')[0]){
        // correct
        rewardForLevel(levelObj);
        parentModal.remove();
      } else {
        // wrong - allow retry or show correct and still grant partial XP
        showModal({title:'Not quite', html:`<p class="muted">Answer expected: <strong>${q.a}</strong></p><div class="mt-3"><button class="glow-btn" id="grantPartial">Grant Partial XP</button></div>`, onOpen(mod){
          mod.querySelector('#grantPartial').addEventListener('click', ()=>{ partialReward(levelObj); mod.remove(); });
        }});
      }
    });
    parentModal.querySelector('#cancelQuiz').addEventListener('click', ()=> parentModal.remove());
  }

  function rewardForLevel(levelObj){
    // award full XP and ZAC if not already completed that level
    const levelIndex = levelObj.id;
    // compute current cumulative completed levels via badges array
    if(user.level > levelIndex){ toast('Level already completed.'); return; }
    // award xp
    const xpGain = levelObj.xpReq;
    user.xp += xpGain;
    user.zac += levelObj.rewardZac;
    // add badge
    user.badges.push({level: levelIndex, title: levelObj.title, awardedAt: Date.now()});
    // progress to next level if xp threshold met
    const levelsCompleted = Math.floor(user.xp / 100) + 1; // demo logic
    user.level = Math.min(5, levelsCompleted);
    saveUser(); renderUI(); toast(`Level ${levelIndex} cleared! +${levelObj.rewardZac} ZAC • +${xpGain} XP`);
    // update leaderboard
    updateLeaderboard(user.uni, user.name, user.xp);
  }

  function partialReward(levelObj){
    user.xp += Math.floor(levelObj.xpReq * 0.3);
    user.zac += Math.max(1, Math.floor(levelObj.rewardZac * 0.3));
    saveUser(); renderUI(); toast(`Partial reward granted: +${Math.max(1, Math.floor(levelObj.rewardZac * 0.3))} ZAC`);
    updateLeaderboard(user.uni, user.name, user.xp);
  }

  /* Leaderboard update helper */
  function updateLeaderboard(uni, name, xp){
    if(!leaderData[uni]) leaderData[uni] = [];
    const list = leaderData[uni];
    const found = list.find(x=>x.name===name);
    if(found){ found.xp = xp; } else { list.push({name, xp}); }
    localStorage.setItem(KEY_LEADER, JSON.stringify(leaderData));
    renderLeaderboard();
    // optional: syncLeaderToFirestore(uni, list)
  }

  /* ===========================
     Simple modal & toast utilities
  =========================== */
  function showModal({title='Modal', html='', htmlNode=null, onOpen=null}){
    const root = document.getElementById('modalRoot');
    const overlay = document.createElement('div');
    overlay.className = 'fixed inset-0 z-50 flex items-center justify-center';
    overlay.innerHTML = `
      <div class="absolute inset-0 bg-black/60 backdrop-blur-sm" id="modalBg"></div>
      <div class="glass p-5 rounded-lg max-w-xl w-[90%] z-60">
        <div class="flex justify-between items-start">
          <div><h3 class="font-semibold">${title}</h3><div class="muted text-sm mt-2" id="modalSub"></div></div>
          <button id="closeModal" class="px-2 py-1 glass rounded-md">Close</button>
        </div>
        <div class="mt-4" id="modalContent"></div>
      </div>`;
    root.appendChild(overlay);

    const contentWrap = overlay.querySelector('#modalContent');
    if(htmlNode) contentWrap.appendChild(htmlNode);
    else contentWrap.innerHTML = html;

    overlay.querySelector('#closeModal').addEventListener('click', ()=> overlay.remove());
    overlay.querySelector('#modalBg').addEventListener('click', ()=> overlay.remove());

    if(typeof onOpen === 'function') onOpen(contentWrap);
    return overlay;
  }

  // Toast
  function toast(msg, ms=2600){
    const t = document.createElement('div');
    t.className = 'fixed bottom-24 left-1/2 transform -translate-x-1/2 z-50 glass px-4 py-2 rounded-md';
    t.textContent = msg;
    document.body.appendChild(t);
    setTimeout(()=> t.style.opacity = '0', ms-300);
    setTimeout(()=> t.remove(), ms);
  }

  /* ===========================
     Demo shop/chat handlers - show gating when attempting transaction
  =========================== */
  document.getElementById('openShopBtn').addEventListener('click', ()=> {
    showModal({title:'Shop (Demo)', html:`<p class="muted">Preview items. Try to checkout to see authentication gating.</p><div class="mt-3"><button id="tryBuy" class="glow-btn">Try Checkout</button></div>`, onOpen(mod){
      mod.querySelector('#tryBuy').addEventListener('click', ()=>{
        const allowed = attemptTransaction();
        if(allowed) toast('Demo checkout success (mock).');
      });
    }});
  });

  document.getElementById('openChatBtn').addEventListener('click', ()=> {
    showModal({title:'Chat (Demo)', html:`<p class="muted">Demo chat. You can explore in Light mode.</p>`});
  });

  document.getElementById('dashboardLearnBtn').addEventListener('click', openLearnModal);
  document.getElementById('shopDemoBtn').addEventListener('click', ()=> document.getElementById('openShopBtn').click());
  document.getElementById('chatBtn').addEventListener('click', ()=> document.getElementById('openChatBtn').click());
  document.getElementById('shopBtn').addEventListener('click', ()=> document.getElementById('openShopBtn').click());
  document.getElementById('claimDemoBtn').addEventListener('click', ()=> toast('Claimed demo item.'));

  // change uni
  document.getElementById('uniSelect').addEventListener('change', (e)=>{ user.uni = e.target.value; saveUser(); renderUI(); });

  // view levels quick link
  document.getElementById('viewLevelsBtn').addEventListener('click', openLearnModal);

  /* ===========================
     Particle background (lightweight metaverse shimmer)
     - comet trails and connecting lines
     =========================== */
  const canvas = document.getElementById('bg');
  const ctx = canvas.getContext('2d');
  let W = canvas.width = innerWidth;
  let H = canvas.height = innerHeight;

  // configuration
  const PARTICLE_COUNT = Math.round(Math.max(30, Math.min(120, W * H / 60000))); // adapt to screen
  const particles = [];
  const MAX_LINK = 120;

  function rand(min,max){ return Math.random()*(max-min)+min; }

  class P {
    constructor(){
      this.reset(true);
    }
    reset(init=false){
      this.x = rand(0,W);
      this.y = rand(0,H);
      this.vx = rand(-0.6,0.6);
      this.vy = rand(-0.2, -1.2);
      this.r = rand(0.8,2.8);
      this.alpha = rand(0.15,0.8);
      this.h = rand(180,260);
      if(!init){
        // place at bottom to create rising-orb effect sometimes
        if(Math.random() < 0.4){ this.y = H + 10; this.vy *= -1; }
      }
      // trail
      this.history = [];
    }
    step(){
      this.x += this.vx;
      this.y += this.vy;
      // bounce softly on sides
      if(this.x < -20 || this.x > W+20 || this.y < -30) this.reset();
      // save trail
      this.history.push({x:this.x, y:this.y});
      if(this.history.length>10) this.history.shift();
    }
    draw(ctx){
      // trail
      for(let i=0;i<this.history.length;i++){
        const s = this.history[i];
        const t = i/this.history.length;
        ctx.beginPath();
        ctx.fillStyle = `hsla(${this.h},100%,60%,${this.alpha * (t*0.25)})`;
        ctx.arc(s.x, s.y, this.r * (0.6 + t*0.6), 0, Math.PI*2);
        ctx.fill();
      }
      // head
      ctx.beginPath();
      const g = ctx.createRadialGradient(this.x, this.y, 0, this.x, this.y, this.r*6);
      g.addColorStop(0, `hsla(${this.h},100%,70%,${this.alpha})`);
      g.addColorStop(0.6, `hsla(${this.h},100%,60%,${this.alpha*0.12})`);
      g.addColorStop(1, `rgba(0,0,0,0)`);
      ctx.fillStyle = g;
      ctx.arc(this.x, this.y, this.r*6, 0, Math.PI*2);
      ctx.fill();
    }
  }

  function initParticles(){
    particles.length = 0;
    for(let i=0;i<PARTICLE_COUNT;i++) particles.push(new P());
  }
  initParticles();

  function anim(){
    ctx.fillStyle = 'rgba(6,10,20,0.28)'; // persistent fade for trailing effect
    ctx.fillRect(0,0,W,H);

    // draw connecting lines
    for(let i=0;i<particles.length;i++){
      const a = particles[i];
      a.step();
      a.draw(ctx);
      for(let j=i+1;j<particles.length;j++){
        const b = particles[j];
        const dx = a.x - b.x;
        const dy = a.y - b.y;
        const dist = Math.sqrt(dx*dx + dy*dy);
        if(dist < MAX_LINK){
          ctx.beginPath();
          const alpha = 0.12 * (1 - dist/MAX_LINK);
          ctx.strokeStyle = `rgba(120,180,255,${alpha})`;
          ctx.lineWidth = 0.6;
          ctx.moveTo(a.x, a.y);
          ctx.lineTo(b.x, b.y);
          ctx.stroke();
        }
      }
    }
    requestAnimationFrame(anim);
  }
  anim();

  onresize = ()=> {
    W = canvas.width = innerWidth; H = canvas.height = innerHeight;
    initParticles();
  };

  /* ===========================
     Optional: Firestore integration notes
     - Below comments show where to plug Firestore for production.
     ===========================
     
     // 1) Add Firebase SDKs:
     // <script src="https://www.gstatic.com/firebasejs/9.x.x/firebase-app-compat.js"></script>
     // <script src="https://www.gstatic.com/firebasejs/9.x.x/firebase-firestore-compat.js"></script>

     // 2) Initialize:
     // const firebaseConfig = { apiKey: "...", authDomain: "...", projectId: "..." };
     // firebase.initializeApp(firebaseConfig);
     // const db = firebase.firestore();

     // 3) Save user:
     // function syncToFirestore(user){
     //   db.collection('users').doc(user.id).set(user, {merge:true});
     // }

     // 4) Leaderboard:
     // db.collection('leaderboards').doc(user.uni).set({ list: leaderData[user.uni] })

     // For real on-chain rewards, integrate with smart contract / backend to mint or transfer ZAC tokens.

  ============================ */

  /* ===========================
     Small onboarding: if new user, show a brief modal
  =========================== */
  const isNew = !localStorage.getItem(KEY_USER);
  if(isNew){
    showModal({title:'Welcome to Zep Swipe Light', html:`<p class="muted">Explore the app in <strong>Zep Swipe Light</strong> mode. When you're ready to transact, connect your wallet or phone.</p><div class="mt-4"><button id="startExplore" class="glow-btn">Start Exploring</button></div>`, onOpen(mod){
      mod.querySelector('#startExplore').addEventListener('click', ()=>{ document.querySelector('[data-ripple]')?.click; mod.remove(); });
    }});
  }

  </script>

</body>
</html>