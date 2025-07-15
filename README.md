<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Video with Animated Hearts</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background: #fff;
    }
    .heart {
      position: absolute;
      font-size: 40px;
      color: #e255a2;
      animation: floatUp 6s linear infinite;
      pointer-events: none;
    }
    @keyframes floatUp {
      0% { transform: translateY(100vh) scale(1); opacity: 1; }
      100% { transform: translateY(-10vh) scale(1.5); opacity: 0; }
    }
    .content {
      position: relative;
      z-index: 1;
      background: rgba(255,255,255,0.85);
      max-width: 60vw;
      margin: 40px auto;
      padding: 24px;
      border-radius: 24px;
    }
  </style>
</head>
<body>
  <!-- Static background hearts -->
  <div id="background-hearts" style="position:fixed; top:0; left:0; width:100vw; height:100vh; z-index:0; pointer-events:none;"></div>
  <div class="content">
    <h1>ALAABUUUUUUU'💖</h1>
    <p>YOU'RE COMPLETELY MY KIND OF WEIRD AND I'M SO GLAD THAT WE MET!💙</p>
    <div style="position:relative; padding-bottom:56.25%; height:0; overflow:hidden; max-width:100%;">
      <iframe src="https://player.vimeo.com/video/1101252754"
      id="vimeo-player" width="2920" height="1920" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute; top:0; left:0; width:100%; height:100%; max-width:100vw;"></iframe>
    </div>
  </div>
  <script>
    function createHeart() {
      const heartEmojis = ['❤', '💖', '💙', '💜', '💚', '💛', '🧡', '🤍', '💗', '💘'];
      const heartColors = ['#e255a2', '#ff69b4', '#2196f3', '#9c27b0', '#4caf50', '#ffeb3b', '#ff9800', '#f44336', '#00bcd4', '#fff'];
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.textContent = heartEmojis[Math.floor(Math.random() * heartEmojis.length)];
      heart.style.left = Math.random() * window.innerWidth + 'px';
      heart.style.top = '100vh';
      heart.style.fontSize = (20 + Math.random() * 40) + 'px';
      heart.style.color = heartColors[Math.floor(Math.random() * heartColors.length)];
      document.body.appendChild(heart);

      setTimeout(() => {
        heart.remove();
      }, 6000);
    }

    setInterval(createHeart, 500);

    // Add a few static hearts in the background
    function addBackgroundHearts(num) {
      const container = document.getElementById('background-hearts');
      const heartEmojis = ['❤', '💖', '💙', '💜', '💚', '💛', '🧡', '🤍', '💗', '💘'];
      const heartColors = ['#e255a2', '#ff69b4', '#2196f3', '#9c27b0', '#4caf50', '#ffeb3b', '#ff9800', '#f44336', '#00bcd4', '#fff'];
      for (let i = 0; i < num; i++) {
        const heart = document.createElement('div');
        heart.className = 'heart';
        heart.textContent = heartEmojis[Math.floor(Math.random() * heartEmojis.length)];
        heart.style.left = Math.random() * window.innerWidth + 'px';
        heart.style.top = Math.random() * window.innerHeight + 'px';
        heart.style.fontSize = (20 + Math.random() * 40) + 'px';
        heart.style.opacity = 0.3 + Math.random() * 0.4;
        heart.style.color = heartColors[Math.floor(Math.random() * heartColors.length)];
        heart.style.animation = 'none';
        container.appendChild(heart);
      }
    }
    addBackgroundHearts(30); // Add 20 static hearts
    // Show custom message and heart animation when video ends
    function showEndMessage() {
      // Create overlay
      const overlay = document.createElement('div');
      overlay.style.position = 'fixed';
      overlay.style.top = 0;
      overlay.style.left = 0;
      overlay.style.width = '100vw';
      overlay.style.height = '100vh';
      overlay.style.background = 'rgba(255,255,255,0.95)';
      overlay.style.zIndex = 9999;
      overlay.style.display = 'flex';
      overlay.style.flexDirection = 'column';
      overlay.style.justifyContent = 'center';
      overlay.style.alignItems = 'center';
      overlay.innerHTML = '<h2 style="font-size:3em; color:#e255a2;"> you are my favourite notification💖</h2>';
      document.body.appendChild(overlay);
      // Burst of hearts animation
      for (let i = 0; i < 40; i++) {
        setTimeout(() => {
          createHeart();
        }, i * 80);
      }
    }

    // Vimeo Player API integration
    function setupVimeoEndListener() {
      const iframe = document.getElementById('vimeo-player');
      if (!iframe) return;
      // Load Vimeo Player API
      const script = document.createElement('script');
      script.src = 'https://player.vimeo.com/api/player.js';
      script.onload = function() {
        const player = new Vimeo.Player(iframe);
        player.on('ended', showEndMessage);
      };
      document.body.appendChild(script);
    }
    setupVimeoEndListener();
  </script>
</body>
</html>
