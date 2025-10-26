<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Zep Swipe — Futuristic SuperApp MVP</title>

<!-- TailwindCSS -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Lucide Icons -->
<script src="https://unpkg.com/lucide@latest"></script>

<!-- Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">

<style>
  body {
    font-family: 'Inter', sans-serif;
    background: radial-gradient(circle at 20% 20%, #0b0c1a, #08051b, #05021a);
    color: white;
    overflow-x: hidden;
    scroll-behavior: smooth;
  }

  h1, h2, h3 { font-family: 'Orbitron', sans-serif; }

  .neon-text {
    background: linear-gradient(90deg, #00f0ff, #ff00d4);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    text-shadow: 0 0 20px rgba(0,255,255,0.3);
  }

  .glass {
    background: rgba(255,255,255,0.06);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 1rem;
  }

  .gradient-btn {
    background: linear-gradient(90deg, #00f0ff, #ff00d4);
    color: black;
    font-weight: 600;
    border-radius: 0.6rem;
    transition: 0.3s ease;
  }

  .gradient-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 20px rgba(0,255,255,0.4);
  }

  .hidden-section { display: none; }
  .active-section { display: block; }

  .footer-icon { width: 22px; height: 22px; }
</style>
</head>
<body class="relative">

<!-- HEADER -->
<header class="fixed top-0 left-0 w-full glass px-6 py-4 flex justify-between items-center z-40">
  <h1 class="text-2xl font-bold neon-text">Zep Swipe</h1>
  <div class="flex items-center gap-2">
    <i data-lucide="wallet" class="footer-icon text-cyan-400"></i>
    <span class="text-sm text-gray-300">ZAC: <span id="wallet-balance">120</span></span>
  </div>
</header>

<main class="pt-24 pb-20">

  <!-- HOME -->
  <section id="dashboard" class="active-section px-6 text-center">
    <h2 class="text-3xl md:text-4xl font-bold mb-4 neon-text">Welcome to Zep Swipe Light</h2>
    <p class="text-gray-300 mb-8 max-w-lg mx-auto">Explore payments, chat, shop, and learn in the futuristic SuperApp for students — no login required.</p>

    <div class="grid grid-cols-2 gap-4 max-w-md mx-auto mb-10">
      <button onclick="showSection('learn')" class="glass py-4 rounded-xl hover:scale-105 transition flex flex-col items-center">
        <i data-lucide="graduation-cap" class="footer-icon text-cyan-400 mb-1"></i>
        <span>Learn & Earn</span>
      </button>
      <button onclick="showSection('shop')" class="glass py-4 rounded-xl hover:scale-105 transition flex flex-col items-center">
        <i data-lucide="shopping-bag" class="footer-icon text-pink-400 mb-1"></i>
        <span>Shop</span>
      </button>
      <button onclick="showSection('chat')" class="glass py-4 rounded-xl hover:scale-105 transition flex flex-col items-center">
        <i data-lucide="message-circle" class="footer-icon text-purple-400 mb-1"></i>
        <span>Chat</span>
      </button>
      <button onclick="unlockFullAccess()" class="glass py-4 rounded-xl hover:scale-105 transition flex flex-col items-center">
        <i data-lucide="unlock" class="footer-icon text-yellow-400 mb-1"></i>
        <span>Unlock Full</span>
      </button>
    </div>

    <!-- ROADMAP -->
    <div class="max-w-3xl mx-auto">
      <h3 class="text-2xl font-bold neon-text mb-4">🚀 2025 Roadmap</h3>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div class="glass p-4 rounded-xl text-left">
          <h4 class="font-semibold text-cyan-400 mb-2">Q1 — Beta Launch</h4>
          <p class="text-gray-400 text-sm">Launch Zep Swipe Light, enable Learn & Earn and in-app chat prototype.</p>
        </div>
        <div class="glass p-4 rounded-xl text-left">
          <h4 class="font-semibold text-pink-400 mb-2">Q2 — On-Chain Rewards</h4>
          <p class="text-gray-400 text-sm">Integrate mock wallet and simulate tokenized rewards using $ZAC.</p>
        </div>
        <div class="glass p-4 rounded-xl text-left">
          <h4 class="font-semibold text-purple-400 mb-2">Q3 — Marketplace Expansion</h4>
          <p class="text-gray-400 text-sm">Enable student merchants and cross-campus transactions.</p>
        </div>
        <div class="glass p-4 rounded-xl text-left">
          <h4 class="font-semibold text-green-400 mb-2">Q4 — Full Zep Network</h4>
          <p class="text-gray-400 text-sm">Launch wallet connection, live leaderboard, and token staking.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- LEARN -->
  <section id="learn" class="hidden-section px-6 text-center">
    <h2 class="text-3xl font-bold mb-4 neon-text">Learn & Earn</h2>
    <p class="text-gray-300 mb-6">Progress through lessons to earn rewards.</p>
    <div class="max-w-md mx-auto glass p-6 rounded-xl">
      <div class="flex justify-between items-center mb-3">
        <span>Level: <span id="level">1</span>/5</span>
        <span>XP: <span id="xp">0</span>/100</span>
      </div>
      <div class="w-full bg-gray-700 h-3 rounded-full mb-4">
        <div id="progress-bar" class="h-3 bg-gradient-to-r from-cyan-400 to-pink-500 rounded-full" style="width: 0%;"></div>
      </div>
      <button id="complete-level" class="gradient-btn px-4 py-2 rounded-lg mt-2">Complete Lesson</button>
      <p id="badge" class="mt-3 text-sm text-gray-400">Earn XP to unlock ZAC rewards</p>
    </div>
  </section>

  <!-- SHOP -->
  <section id="shop" class="hidden-section px-6 text-center">
    <h2 class="text-3xl font-bold mb-4 neon-text">Shop</h2>
    <p class="text-gray-300 mb-6">Discover digital-first student products.</p>
    <div class="grid grid-cols-2 gap-4 max-w-lg mx-auto">
      <div class="glass p-4 rounded-xl">
        <h3>Crypto Hoodie</h3>
        <p class="text-sm text-gray-400">50 ZAC</p>
        <button onclick="promptUnlock()" class="gradient-btn text-black px-3 py-1 rounded-lg mt-2">Buy</button>
      </div>
      <div class="glass p-4 rounded-xl">
        <h3>Wallet Keychain</h3>
        <p class="text-sm text-gray-400">30 ZAC</p>
        <button onclick="promptUnlock()" class="gradient-btn text-black px-3 py-1 rounded-lg mt-2">Buy</button>
      </div>
    </div>
  </section>

  <!-- CHAT -->
  <section id="chat" class="hidden-section px-6 text-center">
    <h2 class="text-3xl font-bold mb-4 neon-text">Chat</h2>
    <div id="chat-box" class="max-w-md mx-auto glass p-4 rounded-xl flex flex-col h-[400px] overflow-y-auto">
      <div class="self-start glass p-2 rounded-lg mb-2 text-sm text-gray-200">👋 Welcome to Zep Chat!</div>
    </div>
    <div class="flex gap-2 max-w-md mx-auto mt-3">
      <input id="chat-input" type="text" placeholder="Type a message..." class="flex-1 p-2 rounded-lg bg-[#0a0a0a] border border-gray-600 focus:outline-none text-white">
      <button onclick="sendChat()" class="gradient-btn px-4 py-2 rounded-lg">Send</button>
    </div>
    <button onclick="addContact()" class="mt-3 text-sm text-cyan-400 underline">➕ Add Contact</button>
  </section>

</main>

<!-- FOOTER NAV -->
<footer class="fixed bottom-0 left-0 w-full glass flex justify-around py-3 z-40 text-sm">
  <button onclick="showSection('dashboard')" class="footer-btn flex flex-col items-center">
    <i data-lucide="home" class="footer-icon"></i><span>Home</span>
  </button>
  <button onclick="showSection('learn')" class="footer-btn flex flex-col items-center">
    <i data-lucide="graduation-cap" class="footer-icon"></i><span>Learn</span>
  </button>
  <button onclick="showSection('shop')" class="footer-btn flex flex-col items-center">
    <i data-lucide="shopping-bag" class="footer-icon"></i><span>Shop</span>
  </button>
  <button onclick="showSection('chat')" class="footer-btn flex flex-col items-center">
    <i data-lucide="message-circle" class="footer-icon"></i><span>Chat</span>
  </button>
</footer>

<script>
// Initialize icons
lucide.createIcons();

// Section navigation
let currentSection = 'dashboard';
function showSection(id) {
  document.getElementById(currentSection).classList.add('hidden-section');
  document.getElementById(id).classList.remove('hidden-section');
  currentSection = id;
}

// Learn system
let xp = 0, level = 1, zac = 120;
document.getElementById('complete-level').addEventListener('click', () => {
  xp += 25;
  if (xp >= 100 && level < 5) {
    xp = 0;
    level++;
    zac += 10;
    document.getElementById('wallet-balance').textContent = zac;
    document.getElementById('badge').textContent = `🏅 Level ${level} unlocked! +10 ZAC`;
  }
  document.getElementById('xp').textContent = xp;
  document.getElementById('level').textContent = level;
  document.getElementById('progress-bar').style.width = `${xp}%`;
});

// Chat system
function sendChat() {
  const input = document.getElementById('chat-input');
  const msg = input.value.trim();
  if (!msg) return;
  const chatBox = document.getElementById('chat-box');
  const div = document.createElement('div');
  div.className = 'self-end glass p-2 rounded-lg mb-2 text-sm text-white bg-opacity-30';
  div.textContent = msg;
  chatBox.appendChild(div);
  input.value = '';
  chatBox.scrollTop = chatBox.scrollHeight;
}

function addContact() { alert('📱 Contact added (mock action).'); }
function promptUnlock() { alert('🔓 Unlock full access to buy using your wallet.'); }
function unlockFullAccess() { alert('🌐 Connect wallet or phone to unlock full access.'); }
</script>
</body>
</html>