<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Zep Swipe — Student & Vendor SuperApp</title>

<!-- Tailwind + Lucide + Fonts -->
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet" />

<style>
body {
  font-family: 'Inter', sans-serif;
  background: #0a0a1a;
  color: #fff;
  overflow-y: auto;
  scroll-behavior: smooth;
}
h1,h2,h3,h4 { font-family:'Orbitron',sans-serif; }

/* Neon Gradient Text */
.neon-text {
  background: linear-gradient(90deg,#00ffea,#ff00ff,#ffcc00,#00ffea);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 0 10px #00ffea, 0 0 20px #ff00ff, 0 0 30px #ffcc00;
  transition: all 0.5s ease-in-out;
}
.neon-text:hover { text-shadow: 0 0 25px #00ffea, 0 0 35px #ff00ff, 0 0 45px #ffcc00; }

/* Glass Panels */
.glass {
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(14px);
  border:1px solid rgba(255,255,255,0.15);
  border-radius:1rem;
  transition: all 0.3s ease;
}
.glass:hover { box-shadow: 0 0 25px #00ffea, 0 0 35px #ff00ff, 0 0 45px #ffcc00; }

/* Gradient Buttons */
.gradient-btn {
  background: linear-gradient(135deg,#00ffea,#ff00ff,#ffcc00);
  color:#000;font-weight:600;
  border-radius:.8rem;
  transition:.4s;
}
.gradient-btn:hover{
  transform: translateY(-3px) scale(1.05);
  box-shadow:0 0 35px #00ffea, 0 0 45px #ff00ff, 0 0 55px #ffcc00;
}

/* Footer Icons */
.footer-icon { width:28px;height:28px; }

/* Chat Bubbles */
.chat-bubble{
  max-width:80%; padding:10px 14px; margin-bottom:10px; border-radius:14px;
  font-size:0.95rem; animation:fadeIn 0.3s ease;
}
.chat-me{align-self:flex-end; background:rgba(0,255,234,0.15); border:1px solid rgba(0,255,234,0.4);}
.chat-them{align-self:flex-start; background:rgba(255,0,255,0.15); border:1px solid rgba(255,0,255,0.4);}

@keyframes fadeIn {from{opacity:0;transform:translateY(5px);}to{opacity:1;transform:translateY(0);}}
.fade-up { opacity: 0; transform: translateY(20px); transition: all 0.8s ease; }
.fade-up.show { opacity: 1; transform: translateY(0); }

/* Animated Neon Background */
@keyframes neonBG {
  0% { background-position:0% 50%; }
  50% { background-position:100% 50%; }
  100% { background-position:0% 50%; }
}
body::before {
  content:'';
  position:fixed;top:0;left:0;width:100%;height:100%;
  background: linear-gradient(45deg,#00ffea,#ff00ff,#ffcc00,#00ffea);
  background-size:400% 400%;
  z-index:-1;
  animation: neonBG 15s ease infinite;
  opacity:0.18;
}
</style>
</head>
<body>

<!-- HEADER -->
<header class="fixed top-0 left-0 w-full glass px-6 py-4 flex justify-between items-center z-40">
  <h1 class="text-2xl font-bold neon-text">Zep Swipe</h1>
  <div class="flex items-center gap-2 text-sm text-gray-200">
    <i data-lucide="wallet" class="footer-icon text-cyan-400"></i>
    <span>Balance: <span id="wallet">120</span> ZAC</span>
  </div>
</header>

<main class="pt-24 pb-24">

<!-- HOME -->
<section id="home" class="px-6 text-center fade-up">
  <h2 class="text-5xl font-bold mb-4 neon-text">Welcome to Zep Swipe</h2>
  <p class="text-gray-300 mb-10 max-w-xl mx-auto text-lg">
    Africa’s Student & Vendor SuperApp — Learn, Chat, Shop & Transact seamlessly.
  </p>

  <!-- Quick Actions -->
  <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-3xl mx-auto mb-14">
    <button onclick="window.location.href='/dashboards/learn'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition">
      <i data-lucide="graduation-cap" class="footer-icon text-teal-400 mb-2"></i>
      <span>Learn & Earn</span>
    </button>
    <button onclick="window.location.href='/dashboards/marketplace'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition">
      <i data-lucide="shopping-bag" class="footer-icon text-magenta-400 mb-2"></i>
      <span>Marketplace</span>
    </button>
    <button onclick="window.location.href='/dashboards/chat'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition">
      <i data-lucide="message-circle" class="footer-icon text-purple-400 mb-2"></i>
      <span>Chat</span>
    </button>
    <button onclick="window.location.href='/dashboards/wallet'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition">
      <i data-lucide="credit-card" class="footer-icon text-yellow-400 mb-2"></i>
      <span>Wallet</span>
    </button>
  </div>
</section>

<!-- LEARN & EARN -->
<section id="learn" class="px-6 hidden fade-up">
  <h2 class="text-4xl font-bold mb-6 neon-text">Learn & Earn XP</h2>
  <div class="glass p-6 max-w-xl mx-auto">
    <p class="text-gray-300 mb-4">Complete lessons → gain XP → earn ZAC tokens.</p>
    <div class="bg-gray-900 rounded-full h-4 w-full mb-2">
      <div id="bar" class="bg-teal-400 h-4 rounded-full w-0"></div>
    </div>
    <p>Level: <span id="lvl">1</span> | XP: <span id="xp">0</span></p>
    <button id="next" class="gradient-btn px-4 py-2 mt-3">Complete Lesson</button>
    <p id="msg" class="text-green-400 mt-2"></p>
  </div>
</section>

<!-- MARKETPLACE -->
<section id="shop" class="px-6 hidden fade-up">
  <h2 class="text-4xl font-bold mb-6 neon-text">Marketplace</h2>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 max-w-5xl mx-auto">
    <div class="glass p-4 flex flex-col">
      <h4 class="font-semibold text-teal-400 mb-2">Product 1</h4>
      <p class="text-gray-200 mb-2">Awesome student-made item.</p>
      <button onclick="window.location.href='/dashboards/product/1'" class="gradient-btn py-2">Buy for 50 ZAC</button>
    </div>
    <div class="glass p-4 flex flex-col">
      <h4 class="font-semibold text-magenta-400 mb-2">Service 1</h4>
      <p class="text-gray-200 mb-2">Vendor service offering.</p>
      <button onclick="window.location.href='/dashboards/service/1'" class="gradient-btn py-2">Request Service</button>
    </div>
  </div>
</section>

<!-- CHAT -->
<section id="chat" class="px-6 hidden fade-up">
  <h2 class="text-4xl font-bold mb-6 neon-text">Chat</h2>
  <div class="glass p-4 max-w-xl mx-auto flex flex-col h-96 overflow-y-auto" id="chat-box"></div>
  <div class="flex max-w-xl mx-auto mt-3 gap-2">
    <input id="msg-input" type="text" placeholder="Type message..." class="flex-1 p-2 rounded-md text-black" />
    <button id="send-msg" class="gradient-btn px-4">Send</button>
  </div>
</section>

<!-- WALLET & WITHDRAW -->
<section id="wallet" class="px-6 hidden fade-up">
  <h2 class="text-4xl font-bold mb-6 neon-text">Wallet</h2>
  <div class="glass p-6 max-w-xl mx-auto flex flex-col gap-4">
    <p>Balance: <span id="wallet-balance">120</span> ZAC</p>
    <button onclick="window.location.href='/dashboards/request-money'" class="gradient-btn py-2">Request Money</button>
    <button onclick="window.location.href='/dashboards/withdraw'" class="gradient-btn py-2">Withdraw Funds</button>
  </div>
</section>

</main>

<!-- FOOTER -->
<footer class="fixed bottom-0 left-0 w-full glass flex justify-around py-3 text-sm z-40">
  <button onclick="window.location.href='/dashboards/home'" class="flex flex-col items-center"><i data-lucide="home" class="footer-icon text-teal-400"></i><span>Home</span></button>
  <button onclick="window.location.href='/dashboards/learn'" class="flex flex-col items-center"><i data-lucide="graduation-cap" class="footer-icon text-teal-400"></i><span>Learn</span></button>
  <button onclick="window.location.href='/dashboards/marketplace'" class="flex flex-col items-center"><i data-lucide="shopping-bag" class="footer-icon text-magenta-400"></i><span>Shop</span></button>
  <button onclick="window.location.href='/dashboards/chat'" class="flex flex-col items-center"><i data-lucide="message-circle" class="footer-icon text-purple-400"></i><span>Chat</span></button>
  <button onclick="window.location.href='/dashboards/wallet'" class="flex flex-col items-center"><i data-lucide="credit-card" class="footer-icon text-yellow-400"></i><span>Wallet</span></button>
</footer>

<script>
lucide.createIcons();

// Fade-in sections
const fadeEls = document.querySelectorAll('.fade-up');
window.addEventListener('scroll', () => {
  fadeEls.forEach(el => {
    if(el.getBoundingClientRect().top < window.innerHeight - 100) el.classList.add('show');
  });
});

// Navigation for internal sections
let current="home";
function nav(id){
  document.getElementById(current).classList.add("hidden");
  document.getElementById(id).classList.remove("hidden");
  current=id;
  window.scrollTo({top:0,behavior:"smooth"});
}

// Learn & Earn Logic
let xp=0,lvl=1,zac=120;
document.getElementById("next")?.addEventListener("click",()=>{
  xp+=25;
  if(xp>=100){ xp=0; lvl++; zac+=15;
    document.getElementById("msg").textContent=`🏅 Level ${lvl} unlocked +15 ZAC`;
    document.getElementById("wallet").textContent=zac;
    document.getElementById("wallet-balance").textContent=zac;
  }
  document.getElementById("xp").textContent=xp;
  document.getElementById("lvl").textContent=lvl;
  document.getElementById("bar").style.width=`${xp}%`;
});

// Chat Logic
const chatBox=document.getElementById("chat-box");
document.getElementById("send-msg")?.addEventListener("click",()=>{
  const input=document.getElementById("msg-input");
  if(!input.value) return;
  const div=document.createElement("div");
  div.textContent=input.value;
  div.className="chat-bubble chat-me";
  chatBox.appendChild(div);
  input.value="";
  chatBox.scrollTop=chatBox.scrollHeight;
});
</script>
</body>
</html>