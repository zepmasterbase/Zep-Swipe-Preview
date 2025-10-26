<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Zep Swipe — Neon Campus Web3 App</title>

<!-- Tailwind + Lucide + Fonts -->
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700&family=Roboto:wght@400;500&display=swap" rel="stylesheet" />

<style>
/* Base */
body {
  font-family: 'Roboto', sans-serif;
  background: rgba(10,10,20,0.9); /* clearer background */
  overflow-x: hidden;
  color: #fff;
  scroll-behavior: smooth;
  position: relative;
}

/* Neon Text with Gradient Glow */
.neon-text {
  font-family: 'Orbitron', sans-serif;
  background: linear-gradient(45deg, #0ff, #ff0, #f0f);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 0 5px #0ff, 0 0 10px #ff0, 0 0 20px #f0f, 0 0 40px #0ff;
  transition: all 0.3s ease;
}
.neon-text:hover {
  text-shadow: 0 0 10px #0ff, 0 0 20px #ff0, 0 0 40px #f0f, 0 0 60px #0ff;
}

/* Glass Panels */
.glass {
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(0,255,255,0.2);
  border-radius: 1rem;
  transition: all 0.3s ease;
}
.glass:hover {
  box-shadow: 0 0 25px #0ff, 0 0 40px #ff0;
}

/* Buttons */
.neon-btn {
  background: linear-gradient(90deg, #0ff, #ff0, #f0f);
  color: #111124;
  font-weight: 600;
  border-radius: 1rem;
  padding: 0.5rem 1.5rem;
  transition: all 0.3s ease;
}
.neon-btn:hover {
  transform: translateY(-2px) scale(1.05);
  box-shadow: 0 0 15px #0ff, 0 0 25px #ff0, 0 0 35px #f0f;
}

/* Footer Icons */
.footer-icon { width:28px;height:28px; }

/* Fade-up animations */
.fade-up { opacity: 0; transform: translateY(20px); transition: all 0.7s ease; }
.fade-up.show { opacity: 1; transform: translateY(0); }

/* Sections */
section { padding: 4rem 1rem; }
section#home { text-align: center; }
.grid-button i { font-size: 2rem; margin-bottom: 0.5rem; }

/* Footer */
footer button span { font-size: 0.75rem; }

/* Floating Neon Orbs */
.neon-orb {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  mix-blend-mode: screen;
  animation: floatOrb linear infinite;
}
@keyframes floatOrb {
  0% { transform: translateY(0) scale(1); opacity: 0.6; }
  50% { transform: translateY(-40px) scale(1.2); opacity: 1; }
  100% { transform: translateY(0) scale(1); opacity: 0.6; }
}
</style>
</head>

<body>

<header class="fixed top-0 left-0 w-full glass px-6 py-4 flex justify-between items-center z-50">
  <h1 class="text-3xl font-bold neon-text">Zep Swipe</h1>
  <div class="flex items-center gap-3 text-sm text-cyan-200">
    <i data-lucide="wallet" class="footer-icon text-cyan-400"></i>
    <span>Balance: <span id="wallet">120</span> ZAC</span>
  </div>
</header>

<main class="pt-28 pb-28">

<section id="home" class="fade-up">
  <h2 class="text-5xl font-bold neon-text mb-6">Welcome to Zep Swipe</h2>
  <p class="text-cyan-300 mb-12 max-w-2xl mx-auto text-lg">
    Africa’s Student & Vendor SuperApp — Learn, Chat, Shop & Transact seamlessly with a neon campus vibe.
  </p>

  <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-4xl mx-auto">
    <button onclick="window.location.href='/dashboards/learn'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition grid-button">
      <i data-lucide="graduation-cap" class="footer-icon text-cyan-400"></i>
      <span>Learn & Earn</span>
    </button>
    <button onclick="window.location.href='/dashboards/marketplace'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition grid-button">
      <i data-lucide="shopping-bag" class="footer-icon text-magenta-400"></i>
      <span>Marketplace</span>
    </button>
    <button onclick="window.location.href='/dashboards/chat'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition grid-button">
      <i data-lucide="message-circle" class="footer-icon text-purple-400"></i>
      <span>Chat</span>
    </button>
    <button onclick="window.location.href='/dashboards/wallet'" class="glass py-6 rounded-xl flex flex-col items-center hover:scale-105 transition grid-button">
      <i data-lucide="credit-card" class="footer-icon text-yellow-400"></i>
      <span>Wallet</span>
    </button>
  </div>
</section>

</main>

<footer class="fixed bottom-0 left-0 w-full glass flex justify-around py-3 text-sm z-50">
  <button onclick="window.location.href='/dashboards/home'" class="flex flex-col items-center">
    <i data-lucide="home" class="footer-icon text-cyan-400"></i><span>Home</span>
  </button>
  <button onclick="window.location.href='/dashboards/learn'" class="flex flex-col items-center">
    <i data-lucide="graduation-cap" class="footer-icon text-cyan-400"></i><span>Learn</span>
  </button>
  <button onclick="window.location.href='/dashboards/marketplace'" class="flex flex-col items-center">
    <i data-lucide="shopping-bag" class="footer-icon text-magenta-400"></i><span>Shop</span>
  </button>
  <button onclick="window.location.href='/dashboards/chat'" class="flex flex-col items-center">
    <i data-lucide="message-circle" class="footer-icon text-purple-400"></i><span>Chat</span>
  </button>
  <button onclick="window.location.href='/dashboards/wallet'" class="flex flex-col items-center">
    <i data-lucide="credit-card" class="footer-icon text-yellow-400"></i><span>Wallet</span>
  </button>
</footer>

<!-- Neon Orbs -->
<div id="orbs-container"></div>

<script>
lucide.createIcons();

// Fade-up animation
const fadeEls = document.querySelectorAll('.fade-up');
window.addEventListener('scroll', () => {
  fadeEls.forEach(el => {
    if(el.getBoundingClientRect().top < window.innerHeight - 100) el.classList.add('show');
  });
});

// Create Neon Orbs
const orbsContainer = document.getElementById('orbs-container');
for(let i=0;i<10;i++){
  const orb = document.createElement('div');
  orb.classList.add('neon-orb');
  const size = Math.random()*30+20;
  orb.style.width = orb.style.height = size + 'px';
  orb.style.background = `radial-gradient(circle, rgba(${Math.floor(Math.random()*255)},${Math.floor(Math.random()*255)},255,0.7), transparent)`;
  orb.style.top = Math.random()*window.innerHeight + 'px';
  orb.style.left = Math.random()*window.innerWidth + 'px';
  orb.style.animationDuration = (Math.random()*10 + 5) + 's';
  orbsContainer.appendChild(orb);
}
</script>

</body>
</html>