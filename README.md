
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Zep Swipe MVP — SuperApp Experience</title>

<!-- Tailwind -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">

<style>
  body {
    font-family: 'Inter', sans-serif;
    background: linear-gradient(135deg, #060b23, #110a3a, #0d0125);
    color: white;
    overflow-x: hidden;
  }

  h1, h2, h3 {
    font-family: 'Orbitron', sans-serif;
  }

  .gradient-btn {
    background: linear-gradient(90deg, #00f0ff, #ff00d4);
    transition: all 0.3s ease;
  }

  .gradient-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 18px rgba(0,255,255,0.4);
  }

  .glass {
    background: rgba(255,255,255,0.06);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255,255,255,0.1);
  }

  /* Fade-in sections */
  .hidden-section { display: none; }
  .active-section { display: block; }

  .neon-text {
    background: linear-gradient(90deg, #00f0ff, #ff00d4);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  /* Chat area */
  .chat-bubble {
    max-width: 70%;
    margin: 8px;
    padding: 10px 14px;
    border-radius: 14px;
  }
  .chat-me { background: #00f0ff33; align-self: flex-end; }
  .chat-them { background: #ff00d433; align-self: flex-start; }

  /* Footer menu */
  .footer-btn.active {
    background: linear-gradient(90deg, #00f0ff, #ff00d4);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
</style>
</head>
<body class="relative">

<!-- Header -->
<header class="fixed top-0 left-0 w-full glass px-6 py-4 flex justify-between items-center z-40">
  <h1 class="text-2xl font-bold neon-text">Zep Swipe</h1>
  <span class="text-sm text-gray-300">ZAC: <span id="wallet-balance">120</span> ⚡</span>
</header>

<main class="pt-24 pb-20">

  <!-- DASHBOARD -->
  <section id="dashboard" class="active-section px-6 text-center">
    <h2 class="text-3xl font-bold mb-4 neon-text">Welcome to Zep Swipe Light</h2>
    <p class="text-gray-300 mb-6">Explore payments, learn, chat & shop — no login required.</p>
    <div class="flex flex-col gap-4 max-w-sm mx-auto">
      <button onclick="showSection('learn')" class="gradient-btn py-3 rounded-lg text-black font-semibold">🎓 Learn & Earn</button>
      <button onclick="showSection('shop')" class="gradient-btn py-3 rounded-lg text-black font-semibold">🛍️ View Shop</button>
      <button onclick="showSection('chat')" class="gradient-btn py-3 rounded-lg text-black font-semibold">💬 Chat</button>
      <button onclick="unlockFullAccess()" class="border border-cyan-400 py-3 rounded-lg text-cyan-400 font-semibold">🔓 Unlock Full Access</button>
    </div>
  </section>

  <!-- LEARN & EARN -->
  <section id="learn" class="hidden-section px-6 text-center">
    <h2 class="text-3xl font-bold mb-4 neon-text">Learn & Earn 🎓</h2>
    <p class="text-gray-300 mb-6">Complete lessons and quizzes to earn ZAC tokens.</p>
    
    <div class="max-w-md mx-auto glass p-6 rounded-xl">
      <div class="flex justify-between items-center mb-4">
        <span>Level: <span id="level">1</span>/5</span>
        <span>XP: <span id="xp">0</span>/100</span>
      </div>
      <div class="w-full bg-gray-700 h-3 rounded-full mb-4">
        <div id="progress-bar" class="h-3 bg-gradient-to-r from-cyan-400 to-pink-500 rounded-full" style="width: 0%;"></div>
      </div>
      <button id="complete-level" class="gradient-btn py-2 px-4 rounded-lg text-black font-semibold">Complete Lesson</button>
      <p id="badge" class="mt-4 text-sm text-gray-400">Earn XP to unlock badges!</p>
    </div>
  </section>

  <!-- SHOP -->
  <section id="shop" class="hidden-section px-6 text-center">
    <h2 class="text-3xl font-bold mb-4 neon-text">Shop 🛒</h2>
    <p class="text-gray-300 mb-6">Explore items available through Zep Swipe Light mode.</p>
    <div class="grid grid-cols-2 gap-4 max-w-lg mx-auto">
      <div class="glass p-4 rounded-xl">
        <h3>Crypto Hoodie</h3>
        <p class="text-sm text-gray-400">50 ZAC</p>
        <button onclick="promptUnlock()" class="gradient-btn text-black font-semibold mt-2 px-3 py-1 rounded-lg text-sm">Buy</button>
      </div>
      <div class="glass p-4 rounded-xl">
        <h3>Digital Wallet Keychain</h3>
        <p class="text-sm text-gray-400">30 ZAC</p>
        <button onclick="promptUnlock()" class="gradient-btn text-black font-semibold mt-2 px-3 py-1 rounded-lg text-sm">Buy</button>
      </div>
    </div>
  </section>

  <!-- CHAT -->
  <section id="chat" class="hidden-section px-6">
    <h2 class="text-3xl font-bold text-center mb-4 neon-text">Chat 💬</h2>
    <div class="max-w-md mx-auto glass rounded-xl p-4 flex flex-col h-[400px] overflow-y-auto" id="chat-box">
      <div class="chat-bubble chat-them">Hey there 👋</div>
      <div class="chat-bubble chat-them">Welcome to Zep Swipe Light Chat!</div>
    </div>
    <div class="max-w-md mx-auto mt-4 flex gap-2">
      <input id="chat-input" type="text" class="flex-1 p-3 rounded-lg bg-[#0a0a0a] text-white border border-gray-600 focus:outline-none" placeholder="Type a message...">
      <button onclick="sendChat()" class="gradient-btn px-4 rounded-lg text-black font-semibold">Send</button>
    </div>
    <div class="text-center mt-3">
      <button onclick="addContact()" class="text-sm text-cyan-400 underline">➕ Add Contact</button>
    </div>
  </section>

</main>

<!-- FOOTER NAV -->
<footer class="fixed bottom-0 left-0 w-full glass flex justify-around py-3 z-40">
  <button onclick="showSection('dashboard')" class="footer-btn text-sm">🏠 Home</button>
  <button onclick="showSection('learn')" class="footer-btn text-sm">🎓 Learn</button>
  <button onclick="showSection('shop')" class="footer-btn text-sm">🛍️ Shop</button>
  <button onclick="showSection('chat')" class="footer-btn text-sm">💬 Chat</button>
</footer>

<script>
let currentSection = 'dashboard';
let level = 1;
let xp = 0;
let zac = 120;

// Switch sections
function showSection(id) {
  document.getElementById(currentSection).classList.add('hidden-section');
  document.getElementById(currentSection).classList.remove('active-section');
  document.getElementById(id).classList.remove('hidden-section');
  document.getElementById(id).classList.add('active-section');
  currentSection = id;
}

// Learn & Earn logic
document.getElementById('complete-level').addEventListener('click', () => {
  xp += 25;
  if (xp >= 100 && level < 5) {
    level++;
    xp = 0;
    zac += 10;
    document.getElementById('wallet-balance').innerText = zac;
    document.getElementById('badge').innerText = `🎉 Level ${level} unlocked! +10 ZAC reward!`;
  }
  document.getElementById('xp').innerText = xp;
  document.getElementById('level').innerText = level;
  document.getElementById('progress-bar').style.width = `${xp}%`;
});

// Chat logic
function sendChat() {
  const input = document.getElementById('chat-input');
  const chatBox = document.getElementById('chat-box');
  if (input.value.trim() === '') return;
  const msg = document.createElement('div');
  msg.classList.add('chat-bubble', 'chat-me');
  msg.textContent = input.value;
  chatBox.appendChild(msg);
  chatBox.scrollTop = chatBox.scrollHeight;
  input.value = '';
}

function addContact() {
  alert('📱 Contact added from your phonebook (mock action).');
}

// Unlock prompt
function promptUnlock() {
  alert('🔒 Unlock full access by connecting your wallet or phone number.');
}
function unlockFullAccess() {
  alert('🌐 Full mode coming soon! Connect your wallet to unlock all transactions.');
}
</script>
</body>
</html>