<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Zep Swipe — Futuristic Web3 SuperApp</title>

<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet" />

<style>
body {
  font-family: 'Inter', sans-serif;
  background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
  color: #fff;
  overflow-y: auto;
  scroll-behavior: smooth;
}
h1,h2,h3 { font-family:'Orbitron',sans-serif; }
.neon-text {
  background: linear-gradient(90deg,#00f0ff,#ff00d4);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 0 8px rgba(0,255,255,0.5),0 0 12px rgba(255,0,212,0.4);
}
.glass {
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: 1rem;
}
.gradient-btn {
  background: linear-gradient(90deg,#00ffff,#ff00d4);
  color:#000;font-weight:600;
  border-radius:.6rem;
  transition:.3s;
}
.gradient-btn:hover{
  transform: translateY(-2px);
  box-shadow:0 0 25px rgba(0,255,255,0.5);
}
.footer-icon{width:24px;height:24px;}
.hidden{display:none;}
.chat-bubble{
  max-width:80%; padding:8px 12px; margin-bottom:8px; border-radius:12px;
  font-size:0.9rem; animation:fadeIn 0.3s ease;
}
.chat-me{align-self:flex-end; background:rgba(0,255,255,0.1); border:1px solid rgba(0,255,255,0.3);}
.chat-them{align-self:flex-start; background:rgba(255,0,212,0.1); border:1px solid rgba(255,0,212,0.3);}
@keyframes fadeIn {from{opacity:0;transform:translateY(5px);}to{opacity:1;transform:translateY(0);}}
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
<section id="home" class="px-6 text-center">
  <h2 class="text-4xl font-bold mb-4 neon-text">Welcome to Zep Swipe Light</h2>
  <p class="text-gray-300 mb-8 max-w-lg mx-auto">Explore Africa’s Web3 SuperApp — learn, earn, and connect freely before you transact.</p>

  <!-- Shortcuts -->
  <div class="grid grid-cols-2 gap-4 max-w-md mx-auto mb-10">
    <button onclick="nav('learn')" class="glass py-4 rounded-xl hover:scale-105 transition flex flex-col items-center">
      <i data-lucide="graduation-cap" class="footer-icon text-cyan-400 mb-1"></i><span>Learn & Earn</span>
    </button>
    <button onclick="nav('shop')" class="glass py-4 rounded-xl hover:scale-105 transition flex flex-col items-center">
      <i data-lucide="shopping-bag" class="footer-icon text-pink-400 mb-1"></i><span>Shop</span>
    </button>
    <button onclick="nav('chat')" class="glass py-4 rounded-xl hover:scale-105 transition flex flex-col items-center">
      <i data-lucide="message-circle" class="footer-icon text-purple-400 mb-1"></i><span>Chat</span>
    </button>
    <button onclick="unlock()" class="glass py-4 rounded-xl hover:scale-105 transition flex flex-col items-center">
      <i data-lucide="unlock" class="footer-icon text-yellow-400 mb-1"></i><span>Unlock</span>
    </button>
  </div>

  <!-- ROADMAP -->
  <h3 class="text-2xl font-bold neon-text mb-4">🚀 2025 Roadmap</h3>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-4 max-w-3xl mx-auto">
    <div class="glass p-4 text-left hover:shadow-cyan-400/40 transition">
      <h4 class="font-semibold text-cyan-400">Q1 — Beta Launch</h4>
      <p class="text-gray-400 text-sm">Zep Swipe Light & Learn + Earn MVP Release.</p>
    </div>
    <div class="glass p-4 text-left hover:shadow-pink-400/40 transition">
      <h4 class="font-semibold text-pink-400">Q2 — On-Chain Rewards</h4>
      <p class="text-gray-400 text-sm">ZAC token integration + wallet XP sync.</p>
    </div>
    <div class="glass p-4 text-left hover:shadow-purple-400/40 transition">
      <h4 class="font-semibold text-purple-400">Q3 — Marketplace</h4>
      <p class="text-gray-400 text-sm">Student-run merchant hubs.</p>
    </div>
    <div class="glass p-4 text-left hover:shadow-green-400/40 transition">
      <h4 class="font-semibold text-green-400">Q4 — Global Rollout</h4>
      <p class="text-gray-400 text-sm">Cross-campus network with smart payments.</p>
    </div>
    <div class="glass p-4 text-left md:col-span-2 hover:shadow-cyan-400/30 transition">
      <h4 class="font-semibold text-cyan-400">🎓 How Students Earn</h4>
      <p class="text-gray-400 text-sm">
        Join Learn & Earn → complete lessons → gain XP → earn ZAC rewards. Top students get NFT badges and leaderboard glory.
      </p>
      <button onclick="nav('learn')" class="gradient-btn px-4 py-2 mt-3">Start Learning</button>
    </div>
  </div>
</section>

<!-- LEARN -->
<section id="learn" class="hidden px-6 text-center">
  <h2 class="text-3xl font-bold mb-4 neon-text">Learn & Earn</h2>
  <div class="max-w-md mx-auto glass p-6 rounded-xl">
    <div class="flex justify-between mb-2 text-sm">
      <span>Level: <span id="lvl">1</span>/5</span>
      <span>XP: <span id="xp">0</span>/100</span>
    </div>
    <div class="w-full bg-gray-700 h-3 rounded-full mb-4">
      <div id="bar" class="h-3 bg-gradient-to-r from-cyan-400 to-pink-500 rounded-full" style="width:0%"></div>
    </div>
    <button id="next" class="gradient-btn px-4 py-2 mt-2">Complete Lesson</button>
    <p id="msg" class="mt-3 text-sm text-gray-400">Earn XP to unlock ZAC rewards 🎯</p>
  </div>
</section>

<!-- SHOP -->
<section id="shop" class="hidden px-6 text-center">
  <h2 class="text-3xl font-bold mb-4 neon-text">Shop</h2>
  <div class="max-w-md mx-auto glass p-6 rounded-xl text-gray-300">
    <p class="mb-3">Student deals and campus offers coming soon!</p>
    <button onclick="nav('learn')" class="gradient-btn px-4 py-2">Earn ZAC to Spend</button>
  </div>
</section>

<!-- CHAT -->
<section id="chat" class="hidden px-6 text-center">
  <h2 class="text-3xl font-bold mb-4 neon-text">Chat</h2>
  <div class="glass p-4 rounded-xl max-w-md mx-auto mb-4">
    <select id="contacts" class="w-full p-2 rounded-lg bg-[#0a0a0a] border border-gray-600 mb-2 text-sm text-white">
      <option value="">Select Contact</option>
    </select>
    <div class="flex gap-2">
      <input id="newContact" placeholder="Add contact name" class="flex-1 p-2 rounded-lg bg-[#0a0a0a] border border-gray-600 text-white">
      <button onclick="addContact()" class="gradient-btn px-3 py-1">Add</button>
    </div>
  </div>
  <div id="chatBox" class="max-w-md mx-auto glass p-4 rounded-xl flex flex-col h-[350px] overflow-y-auto"></div>
  <div class="flex gap-2 max-w-md mx-auto mt-3">
    <input id="msgInput" placeholder="Type a message..." class="flex-1 p-2 rounded-lg bg-[#0a0a0a] border border-gray-600 text-white">
    <button onclick="sendMsg()" class="gradient-btn px-4 py-2">Send</button>
  </div>
</section>

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

// Learn & Earn
let xp=0,lvl=1,zac=120;
document.getElementById("next").onclick=()=>{
  xp+=25;
  if(xp>=100&&lvl<5){xp=0;lvl++;zac+=15;
    document.getElementById("msg").textContent=`🏅 Level ${lvl} unlocked +15 ZAC`;
    document.getElementById("wallet").textContent=zac;
  }
  document.getElementById("xp").textContent=xp;
  document.getElementById("lvl").textContent=lvl;
  document.getElementById("bar").style.width=`${xp}%`;
};

// Chat
let chats={},contactsSel=document.getElementById("contacts");
function addContact(){
  const n=document.getElementById("newContact").value.trim();
  if(!n)return alert("Enter a name");
  if(chats[n])return alert("Already added");
  chats[n]=[];
  const o=document.createElement("option");o.value=n;o.textContent=n;
  contactsSel.appendChild(o);
  document.getElementById("newContact").value="";
}
function sendMsg(){
  const c=contactsSel.value;if(!c)return alert("Select a contact first");
  const t=document.getElementById("msgInput"),m=t.value.trim();if(!m)return;
  const box=document.getElementById("chatBox");
  const msg=document.createElement("div");
  msg.className="chat-bubble chat-me"; msg.textContent=m; box.appendChild(msg);
  chats[c].push({from:"me",text:m});
  setTimeout(()=>{
    const r=document.createElement("div");
    r.className="chat-bubble chat-them"; r.textContent=`${c}: Got your message! 🔥`;
    box.appendChild(r); box.scrollTop=box.scrollHeight;
  },700);
  t.value=""; box.scrollTop=box.scrollHeight;
}
</script>
</body>
</html>