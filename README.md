<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Zep Swipe — Futuristic Web3 SuperApp</title>

<!-- Tailwind + Lucide + Fonts -->
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet" />

<style>
body {
  font-family: 'Inter', sans-serif;
  background: linear-gradient(135deg,#0f0c29,#302b63,#24243e);
  color: #fff;
  overflow-y: auto;
  scroll-behavior: smooth;
}
h1,h2,h3,h4 { font-family:'Orbitron',sans-serif; }

/* Neon Text */
.neon-text {
  background: linear-gradient(120deg,#ff00ff,#ff79c6,#00ffff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 0 12px #ff00ff, 0 0 18px #ff79c6, 0 0 24px #00ffff;
  transition: all 0.4s ease-in-out;
}
.neon-text:hover {
  text-shadow: 0 0 20px #ff00ff, 0 0 28px #ff79c6, 0 0 36px #00ffff;
}

/* Glass Panels */
.glass {
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(15px);
  border:1px solid rgba(255,255,255,0.1);
  border-radius:1rem;
  transition: all 0.3s ease;
}
.glass:hover {
  box-shadow: 0 0 25px rgba(255,0,255,0.4),0 0 35px rgba(0,255,255,0.3);
}

/* Buttons */
.gradient-btn {
  background: linear-gradient(135deg,#ff00ff,#ff79c6,#00ffff);
  color:#0f0c29;
  font-weight:600;
  border-radius:1rem;
  padding:0.5rem 1.5rem;
  transition: all 0.3s ease;
}
.gradient-btn:hover {
  transform: translateY(-2px) scale(1.05);
  box-shadow: 0 0 20px #ff00ff, 0 0 25px #ff79c6, 0 0 30px #00ffff;
}

/* Footer Icons */
.footer-icon { width:26px;height:26px; }

/* Fade animations */
.fade-up { opacity: 0; transform: translateY(20px); transition: all 0.7s ease; }
.fade-up.show { opacity: 1; transform: translateY(0); }
</style>
</head>

<body>

<header class="fixed top-0 left-0 w-full glass px-6 py-4 flex justify-between items-center z-40">
  <h1 class="text-2xl font-bold neon-text">Zep Swipe</h1>
  <div class="flex items-center gap-2 text-sm text-gray-200">
    <i data-lucide="wallet" class="footer-icon text-pink-400"></i>
    <span>Balance: <span id="wallet">120</span> ZAC</span>
  </div>
</header>

<main class="pt-24 pb-24">

<section id="home" class="px-6 text-center fade-up">
  <h2 class="text-5xl font-bold mb-4 neon-text">Welcome to Zep Swipe</h2>
  <p class="text-pink-200 mb-10 max-w-xl mx-auto text-lg">
    Africa’s Student & Vendor SuperApp — Learn, Chat, Shop & Transact seamlessly.
  </p>

  <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-3xl mx-auto mb-14">
    <button onclick="window.location.href='/dashboards/learn'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition">
      <i data-lucide="graduation-cap" class="footer-icon text-pink-400 mb-2"></i>
      <span>Learn & Earn</span>
    </button>
    <button onclick="window.location.href='/dashboards/marketplace'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition">
      <i data-lucide="shopping-bag" class="footer-icon text-cyan-400 mb-2"></i>
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

</main>

<footer class="fixed bottom-0 left-0 w-full glass flex justify-around py-3 text-sm z-40">
  <button onclick="window.location.href='/dashboards/home'" class="flex flex-col items-center">
    <i data-lucide="home" class="footer-icon text-pink-400"></i><span>Home</span>
  </button>
  <button onclick="window.location.href='/dashboards/learn'" class="flex flex-col items-center">
    <i data-lucide="graduation-cap" class="footer-icon text-pink-400"></i><span>Learn</span>
  </button>
  <button onclick="window.location.href='/dashboards/marketplace'" class="flex flex-col items-center">
    <i data-lucide="shopping-bag" class="footer-icon text-cyan-400"></i><span>Shop</span>
  </button>
  <button onclick="window.location.href='/dashboards/chat'" class="flex flex-col items-center">
    <i data-lucide="message-circle" class="footer-icon text-purple-400"></i><span>Chat</span>
  </button>
  <button onclick="window.location.href='/dashboards/wallet'" class="flex flex-col items-center">
    <i data-lucide="credit-card" class="footer-icon text-yellow-400"></i><span>Wallet</span>
  </button>
</footer>

<script>
lucide.createIcons();

// Fade-up on scroll
const fadeEls = document.querySelectorAll('.fade-up');
window.addEventListener('scroll', () => {
  fadeEls.forEach(el => {
    if(el.getBoundingClientRect().top < window.innerHeight - 100) el.classList.add('show');
  });
});
</script>
</body>
</html>