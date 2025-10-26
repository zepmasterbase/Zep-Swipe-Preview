
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Zep Swipe — Neon Campus Wallet</title>

<!-- Tailwind + Fonts -->
<script src="https://cdn.tailwindcss.com"></script>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700&family=Roboto:wght@400;500&display=swap" rel="stylesheet" />

<style>
body {
  font-family: 'Roboto', sans-serif;
  background: #1b0f3a;
  color: #fff;
  margin: 0;
  padding: 0;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
}

/* Gradient Neon Text */
.neon-text {
  font-family: 'Orbitron', sans-serif;
  font-weight: 700;
  font-size: 2.5rem;
  background: linear-gradient(90deg, #00f0ff, #ff00f0);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-align: center;
  margin-top: 3rem;
  margin-bottom: 1rem;
}

/* Subtitle */
.subtitle {
  color: #c0bdf4;
  text-align: center;
  max-width: 320px;
  margin-bottom: 2rem;
  line-height: 1.5;
}

/* Buttons */
.btn {
  display: block;
  width: 260px;
  text-align: center;
  font-weight: 500;
  padding: 0.75rem 1rem;
  border-radius: 1rem;
  margin: 0.5rem auto;
  cursor: pointer;
  transition: all 0.3s ease;
}

/* Gradient Neon Button */
.btn-gradient {
  background: linear-gradient(90deg, #00f0ff, #ff00f0);
  color: #1b0f3a;
}

.btn-gradient:hover {
  opacity: 0.9;
  transform: scale(1.05);
}

/* Outlined Button */
.btn-outline {
  border: 2px solid #7c63ff;
  color: #c0bdf4;
  background: transparent;
}

.btn-outline:hover {
  background: rgba(124, 99, 255, 0.2);
  transform: scale(1.03);
}
</style>
</head>
<body>

<h1 class="neon-text">Zep Swipe — Neon Campus Wallet</h1>
<p class="subtitle">
Earn <span style="color:#ff00f0;">$ZAC</span> for learning and engagement. Redeem, spend, or stake with friends — your Web3 wallet built for African students.
</p>

<button class="btn btn-gradient">Connect Wallet</button>
<button class="btn btn-outline">Connect with Mobile Number</button>
<button class="btn btn-outline">Start Quiz</button>

</body>
</html>