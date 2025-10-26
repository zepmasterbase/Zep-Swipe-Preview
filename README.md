<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Zep Swipe — Futuristic Neon Web3</title>

<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet" />

<style>
/* General */
body {
  font-family: 'Inter', sans-serif;
  background: #01010f;
  color: #fff;
  overflow-y: auto;
  scroll-behavior: smooth;
}
h1,h2,h3 { font-family:'Orbitron',sans-serif; }
.neon-text {
  background: linear-gradient(90deg,#00f0ff,#ff00d4);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 0 10px #00f0ff, 0 0 20px #ff00d4;
  transition: all 0.5s ease-in-out;
}
.neon-text:hover { text-shadow: 0 0 20px #00f0ff,0 0 30px #ff00d4; }

/* Glass panels */
.glass {
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(12px);
  border:1px solid rgba(255,255,255,0.1);
  border-radius:1rem;
  transition: all 0.3s ease;
}
.glass:hover { box-shadow: 0 0 20px #00f0ff, 0 0 30px #ff00d4; }

/* Buttons */
.gradient-btn {
  background: linear-gradient(90deg,#00ffff,#ff00d4);
  color:#000;font-weight:600;
  border-radius:.6rem;
  transition:.4s;
}
.gradient-btn:hover{
  transform: translateY(-3px) scale(1.05);
  box-shadow:0 0 30px #00ffff, 0 0 40px #ff00d4;
}

/* Footer icons */
.footer-icon { width:24px;height:24px; }

/* Chat bubbles */
.chat-bubble{
  max-width:80%; padding:8px 12px; margin-bottom:8px; border-radius:12px;
  font-size:0.9rem; animation:fadeIn 0.3s ease;
}
.chat-me{align-self:flex-end; background:rgba(0,255,255,0.1); border:1px solid rgba(0,255,255,0.3);}
.chat-them{align-self:flex-start; background:rgba(255,0,212,0.1); border:1px solid rgba(255,0,212,0.3);}
@keyframes fadeIn {from{opacity:0;transform:translateY(5px);}to{opacity:1;transform:translateY(0);}}

/* Animations for sections */
.fade-up { opacity: 0; transform: translateY(20px); transition: all 0.8s ease; }
.fade-up.show { opacity: 1; transform: translateY(0); }

/* Animated neon gradient background */
@keyframes neonBG {
  0% { background-position:0% 50%; }
  50% { background-position:100% 50%; }
  100% { background-position:0% 50%; }
}
body::before {
  content:'';
  position:fixed;top:0;left:0;width:100%;height:100%;
  background: linear-gradient(45deg,#00ffff,#ff00d4,#ff00ff,#00ffff);
  background-size:400% 400%;
  z-index:-1;
  animation: neonBG 15s ease infinite;
  opacity:0.15;
}
</style>
</head>

<body>

<!-- HEADER -->
<header class="fixed top-0 left-0 w-full glass px-6 py-4 flex justify-between items-center z-40">
  <h1 class="text-2xl font-bold neon-text">Zep Swipe</h1>
  <div class="flex items-center gap-2 text-sm text-gray-300">
    <i data-lucide="wallet" class="footer-icon text-cyan-400"></i>
    <span>ZAC: <span id="wallet">120</span></span>
  </div>
</header>

<main class="pt-24 pb-24">

<!-- HOME -->
<section id="home" class="px-6 text-center fade-up">
  <h2 class="text-5xl font-bold mb-4 neon-text">Welcome to Zep Swipe Light</h2>
  <p class="text-gray-300 mb-10 max-w-xl mx-auto text-lg">Explore Africa’s Web3 SuperApp — learn, earn, and connect before you transact.</p>

  <!-- Shortcuts -->
  <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-3xl mx-auto mb-14">
    <button onclick="nav('learn')" class="glass py-6 rounded-xl hover:scale-105 transition flex flex-col items-center">
      <i data-lucide="graduation-cap" class="footer-icon text-cyan-400 mb-2"></i><span>Learn & Earn</span>
    </button>
    <button onclick="nav('shop')" class="glass py-6 rounded-xl hover:scale-105 transition flex flex-col items-center">
      <i data-lucide="shopping-bag" class="footer-icon text-pink-400 mb-2"></i><span>Shop</span>
    </button>
    <button onclick="nav('chat')" class="glass py-6 rounded-xl hover:scale-105 transition flex flex-col items-center">
      <i data-lucide="message-circle" class="footer-icon text-purple-400 mb-2"></i><span>Chat</span>
    </button>
    <button onclick="unlock()" class="glass py-6 rounded-xl hover:scale-105 transition flex flex-col items-center">
      <i data-lucide="unlock" class="footer-icon text-yellow-400 mb-2"></i><span>Unlock</span>
    </button>
  </div>

  <!-- ROADMAP -->
  <h3 class="text-3xl font-bold neon-text mb-6">🚀 2025 Roadmap</h3>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-6 max-w-4xl mx-auto">
    <div class="glass p-5 hover:shadow-cyan-400/50 transition">
      <h4 class="font-semibold text-cyan-400">Q1 — Beta Launch</h4>
      <p class="text-gray-400 text-sm">Zep Swipe Light & Learn + Earn MVP Release.</p>
    </div>
    <div class="glass p-5 hover:shadow-pink-400/50 transition">
      <h4 class="font-semibold text-pink-400">Q2 — On-Chain Rewards</h4>
      <p class="text-gray-400 text-sm">ZAC token integration + wallet XP sync.</p>
    </div>
    <div class="glass p-5 hover:shadow-purple-400/50 transition">
      <h4 class="font-semibold text-purple-400">Q3 — Marketplace</h4>
      <p class="text-gray-400 text-sm">Student-run merchant hubs.</p>
    </div>
    <div class="glass p-5 hover:shadow-green-400/50 transition">
      <h4 class="font-semibold text-green-400">Q4 — Global Rollout</h4>
      <p class="text-gray-400 text-sm">Cross-campus network with smart payments.</p>
    </div>
    <div class="glass p-5 md:col-span-2 hover:shadow-cyan-400/40 transition">
      <h4 class="font-semibold text-cyan-400">🎓 How Students Earn</h4>
      <p class="text-gray-400 text-sm">
        Join Learn & Earn → complete lessons → gain XP → earn ZAC rewards. Top students get NFT badges and leaderboard glory.
      </p>
      <button onclick="nav('learn')" class="gradient-btn px-5 py-2 mt-3">Start Learning</button>
    </div>
  </div>
</section>

<!-- LEARN, SHOP, CHAT Sections remain the same as previous version -->

</main>

<!-- FOOTER -->
<footer class="fixed bottom-0 left-0 w-full glass flex justify-around py-3 text-sm z-40">
  <button onclick="nav('home')" class="flex flex-col items-center"><i data-lucide="home" class="footer-icon text-cyan-400"></i><span>Home</span></button>
  <button onclick="nav('learn')" class="flex flex-col items-center"><i data-lucide="graduation-cap" class="footer-icon text-cyan-400"></i><span>Learn</span></button>
  <button onclick="nav('shop')" class="flex flex-col items-center"><i data-lucide="shopping-bag" class="footer-icon text-pink-400"></i><span>Shop</span></button>
  <button onclick="nav('chat')" class="flex flex-col items-center"><i data-lucide="message-circle" class="footer-icon text-purple-400"></i><span>Chat</span></button>
</footer>

<script>
lucide.createIcons();

// Section fade-in on scroll
const fadeEls = document.querySelectorAll('.fade-up');
window.addEventListener('scroll', () => {
  fadeEls.forEach(el => {
    const top = el.getBoundingClientRect().top;
    const trigger = window.innerHeight - 100;
    if(top < trigger) el.classList.add('show');
  });
});

// Navigation
let current="home";
function nav(id){
  document.getElementById(current).classList.add("hidden");
  document.getElementById(id).classList.remove("hidden");
  current=id;
  window.scrollTo({top:0,behavior:"smooth"});
}

// Unlock prompt
function unlock(){
  alert("🔓 Connect your wallet or phone number to unlock full Zep Swipe access.");
}

// Learn & Earn logic
let xp=0,lvl=1,zac=120;
document.getElementById("next")?.addEventListener("click",()=>{
  xp+=25;
  if(xp>=100 && lvl<5){ xp=0; lvl++; zac+=15;
    document.getElementById("msg").textContent=`🏅 Level ${lvl} unlocked +15 ZAC`;
    document.getElementById("wallet").textContent=zac;
  }
  document.getElementById("xp")?.textContent=xp;
  document.getElementById("lvl")?.textContent=lvl;
  document.getElementById("bar")?.style.width=`${xp}%`;
});

// Chat logic remains same as previous version
</script>
</body>
</html>