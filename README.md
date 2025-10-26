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
  background: radial-gradient(circle at top, #0a0a1a, #05050d);
  color: #fff;
  overflow-x: hidden;
  scroll-behavior: smooth;
  position: relative;
}

/* Neon Gradient Text */
.neon-text {
  font-family: 'Orbitron', sans-serif;
  background: linear-gradient(90deg, #0ff, #ff0, #f0f);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 0 5px #0ff, 0 0 15px #ff0, 0 0 25px #f0f, 0 0 50px #0ff;
  transition: all 0.3s ease;
}
.neon-text:hover {
  text-shadow: 0 0 10px #0ff, 0 0 25px #ff0, 0 0 40px #f0f, 0 0 80px #0ff;
}

/* Glassmorphism Panels */
.glass {
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(0,255,255,0.15);
  border-radius: 1.5rem;
  transition: all 0.3s ease;
}
.glass:hover {
  box-shadow: 0 0 25px #0ff, 0 0 40px #ff0, 0 0 50px #f0f;
  transform: scale(1.02);
}

/* Buttons */
.neon-btn {
  background: linear-gradient(90deg, #0ff, #ff0, #f0f);
  color: #111124;
  font-weight: 600;
  border-radius: 1rem;
  padding: 0.75rem 1.75rem;
  transition: all 0.3s ease;
}
.neon-btn:hover {
  transform: translateY(-2px) scale(1.08);
  box-shadow: 0 0 15px #0ff, 0 0 25px #ff0, 0 0 35px #f0f;
}

/* Footer Icons */
.footer-icon { width:28px;height:28px; }

/* Fade-up Animations */
.fade-up { opacity: 0; transform: translateY(30px); transition: all 0.7s ease; }
.fade-up.show { opacity: 1; transform: translateY(0); }

/* Sections */
section { padding: 6rem 1rem; }
section#home { text-align: center; }
.grid-button i { font-size: 2.2rem; margin-bottom: 0.5rem; }

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
  0% { transform: translateY(0) scale(1); opacity: 0.5; }
  50% { transform: translateY(-50px) scale(1.3); opacity: 1; }
  100% { transform: translateY(0) scale(1); opacity: 0.5; }
}
</style>
</head>

<body>

<header class="fixed top-0 left-0 w-full glass px-6 py-4 flex justify-between items-center z-50">
  <h1 class="text-3xl md:text-4xl font-bold neon-text">Zep Swipe</h1>
  <div class="flex items-center gap-3 text-sm text-cyan-200">
    <i data-lucide="wallet" class="footer-icon text-cyan-400"></i>
    <span>Balance: <span id="wallet">120</span> ZAC</span>
  </div>
</header>

<main class="pt-32 pb-28">

<section id="home" class="fade-up">
  <h2 class="text-5xl md:text-6xl font-bold neon-text mb-6">Welcome to Zep Swipe</h2>
  <p class="text-cyan-300 mb-12 max-w-3xl mx-auto text-lg md:text-xl">
    Africa’s Student & Vendor SuperApp — Learn, Chat, Shop & Transact seamlessly with a neon campus vibe.
  </p>

  <div class="grid grid-cols-2 md:grid-cols-4 gap-8 max-w-5xl mx-auto">
    <button onclick="window.location.href='/dashboards/learn'" class="glass py-6 rounded-2xl flex flex-col items-center hover:scale-105 transition grid-button">
      <i data-lucide="graduation-cap" class="footer-icon text-cyan-400"></i>
      <span>Learn & Earn</span>
    </button>
    <button onclick="window.location.href='/dashboards/marketplace'" class="glass py-6 rounded-2xl flex flex-col items-center hover:scale-105 transition grid-button">
      <i data-lucide="shopping-bag" class="footer-icon text-magenta-400"></i>
      <span>Marketplace</span>
    </button>
    <button onclick="window.location.href='/dashboards/chat'" class="glass py-6 rounded-2xl flex flex-col items-center hover:scale-105 transition grid-button">
      <i data-lucide="message-circle" class="footer-icon text-purple-400"></i>
      <span>Chat</span>
    </button>
    <button onclick="window.location.href='/dashboards/wallet'" class="glass py-6 rounded-2xl flex flex-col items-center hover:scale-105 transition grid-button">
      <i data-lucide="credit-card" class="footer-icon text-yellow-400"></i>
      <span>Wallet</span>
    </button>
  </div>
</section>

</main>

<footer class="fixed bottom-0 left-0 w-full glass flex justify-around py-4 text-sm z-50">
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

// Neon Orbs
const orbsContainer = document.getElementById('orbs-container');
for(let i=0;i<12;i++){
  const orb = document.createElement('div');
  orb.classList.add('neon-orb');
  const size = Math.random()*35+25;
  orb.style.width = orb.style.height = size + 'px';
  const r = Math.floor(Math.random()*255);
  const g = Math.floor(Math.random()*255);
  const b = 255;
  orb.style.background = `radial-gradient(circle, rgba(${r},${g},${b},0.7), transparent)`;
  orb.style.top = Math.random()*window.innerHeight + 'px';
  orb.style.left = Math.random()*window.innerWidth + 'px';
  orb.style.animationDuration = (Math.random()*12 + 6) + 's';
  orbsContainer.appendChild(orb);
}
</script>

</body>
</html>