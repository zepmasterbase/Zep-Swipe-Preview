<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Zep Swipe — Futuristic Metaverse Campus</title>

<!-- Tailwind + Lucide + Fonts -->
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700&family=Roboto:wght@400;500&display=swap" rel="stylesheet" />

<style>
/* Base & Background */
body {
  font-family: 'Roboto', sans-serif;
  background: radial-gradient(circle at top left, #0a0a10, #0f0f25 80%);
  color: #fff;
  overflow-x: hidden;
  scroll-behavior: smooth;
  perspective: 1000px;
  position: relative;
}

/* Animated Cyber Grid */
body::before {
  content: "";
  position: fixed;
  top:0; left:0;
  width:100%; height:100%;
  background: repeating-linear-gradient(
    45deg,
    rgba(0,255,255,0.05) 0px,
    rgba(0,255,255,0.05) 1px,
    transparent 1px,
    transparent 20px
  );
  background-size: 200% 200%;
  z-index: -2;
  animation: gridMove 25s linear infinite;
}
@keyframes gridMove {
  0% { background-position: 0 0; }
  100% { background-position: 200% 200%; }
}

/* Neon Text */
.neon-text {
  font-family: 'Orbitron', sans-serif;
  background: linear-gradient(90deg, #0ff, #ff0, #ff00ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 0 10px #0ff, 0 0 20px #ff0, 0 0 40px #ff00ff;
  transition: all 0.4s ease;
}
.neon-text:hover {
  text-shadow: 0 0 20px #0ff, 0 0 40px #ff0, 0 0 70px #ff00ff;
}

/* Glass Panels */
.glass {
  background: rgba(255,255,255,0.03);
  backdrop-filter: blur(35px);
  border: 1px solid rgba(0,255,255,0.25);
  border-radius: 2rem;
  transition: all 0.4s ease;
  transform-style: preserve-3d;
}
.glass:hover {
  box-shadow: 0 0 30px #0ff, 0 0 50px #ff0, 0 0 80px #ff00ff;
  transform: scale(1.05) translateZ(20px);
}

/* Buttons */
.neon-btn {
  background: linear-gradient(90deg, #0ff, #ff0, #ff00ff);
  color: #0a0a10;
  font-weight: 600;
  border-radius: 1.5rem;
  padding: 0.75rem 2.5rem;
  transition: all 0.4s ease;
}
.neon-btn:hover {
  transform: translateY(-3px) scale(1.1);
  box-shadow: 0 0 25px #0ff, 0 0 40px #ff0, 0 0 60px #ff00ff;
}

/* Footer Icons */
.footer-icon { width:28px; height:28px; }

/* Fade-up Animations */
.fade-up { opacity: 0; transform: translateY(30px); transition: all 0.8s cubic-bezier(0.68,-0.55,0.27,1.55); }
.fade-up.show { opacity: 1; transform: translateY(0); }

/* Sections */
section { padding: 6rem 1rem; }
section#home { text-align: center; }
.grid-button i { font-size: 2.5rem; margin-bottom: 0.5rem; }

/* Footer */
footer button span { font-size: 0.75rem; }

/* Floating Neon Orbs */
.neon-orb {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  mix-blend-mode: screen;
  animation: floatOrb ease-in-out infinite;
  transform-style: preserve-3d;
}
@keyframes floatOrb {
  0% { transform: translateY(0) scale(1); opacity:0.3; }
  50% { transform: translateY(-70px) scale(1.3); opacity:0.8; }
  100% { transform: translateY(0) scale(1); opacity:0.3; }
}
</style>
</head>

<body>

<header class="fixed top-0 left-0 w-full glass px-8 py-4 flex justify-between items-center z-50">
  <h1 class="text-3xl md:text-4xl font-bold neon-text">Zep Swipe</h1>
  <div class="flex items-center gap-4 text-sm text-cyan-300">
    <i data-lucide="wallet" class="footer-icon text-cyan-400"></i>
    <span>Balance: <span id="wallet">120</span> ZAC</span>
  </div>
</header>

<main class="pt-32 pb-32">

<section id="home" class="fade-up">
  <h2 class="text-5xl md:text-6xl font-bold neon-text mb-6">Welcome to Zep Swipe</h2>
  <p class="text-cyan-300 mb-12 max-w-3xl mx-auto text-lg md:text-xl">
    Africa’s Student & Vendor SuperApp — Learn, Chat, Shop & Transact seamlessly with a futuristic neon campus vibe.
  </p>

  <div class="grid grid-cols-2 md:grid-cols-4 gap-10 max-w-6xl mx-auto">
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
const orbs = [];
for(let i=0;i<15;i++){
  const orb = document.createElement('div');
  orb.classList.add('neon-orb');
  const size = Math.random()*50+30;
  orb.style.width = orb.style.height = size + 'px';
  const colors = [
    "rgba(0,255,255,0.7)",
    "rgba(255,0,255,0.7)",
    "rgba(255,255,0,0.7)",
    "rgba(0,255,128,0.7)"
  ];
  orb.style.background = `radial-gradient(circle, ${colors[Math.floor(Math.random()*4)]}, transparent)`;
  orb.style.top = Math.random()*window.innerHeight + 'px';
  orb.style.left = Math.random()*window.innerWidth + 'px';
  orb.style.animationDuration = (Math.random()*10 + 5) + 's';
  orb.style.animationDirection = Math.random() > 0.5 ? 'normal' : 'reverse';
  orbsContainer.appendChild(orb);
  orbs.push(orb);
}

// 3D Parallax Effect
window.addEventListener('mousemove', e => {
  const x = (e.clientX / window.innerWidth - 0.5) * 30; // rotation X
  const y = (e.clientY / window.innerHeight - 0.5) * 30; // rotation Y
  document.querySelectorAll('.glass').forEach(el => {
    el.style.transform = `rotateY(${x}deg) rotateX(${-y}deg) scale(1.05)`;
  });
  orbs.forEach((orb, idx) => {
    const speed = (idx+1)/30;
    orb.style.transform = `translate3d(${x*speed}px, ${-y*speed}px, 0) scale(${1 + speed/2})`;
  });
});
</script>

</body>
</html>