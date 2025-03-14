<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>個人網站 - 排球少年驚喜</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f4f7f9;
      text-align: center;
      color: #333;
      margin: 0;
      padding: 0;
    }

    h1 {
      color: #4CAF50;
      font-size: 36px;
      margin-top: 50px;
    }

    p {
      font-size: 20px;
      margin: 20px 0;
      color: #555;
    }

    .image-container {
      margin-top: 30px;
    }

    img {
      width: 60%;
      max-width: 500px;
      border-radius: 8px;
    }

    #surpriseButton {
      background-color: #ff8c00;
      color: white;
      padding: 15px 30px;
      font-size: 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      margin-top: 30px;
      transition: background-color 0.3s ease;
    }

    #surpriseButton:hover {
      background-color: #ff7043;
    }

    #clown {
      display: none;
      font-size: 100px;
      color: #ff6347;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      animation: clownAnimation 1s ease-in-out infinite;
    }

    #game-link {
      display: none;
      margin-top: 20px;
      font-size: 20px;
      color: #007BFF;
      text-decoration: none;
      font-weight: bold;
    }

    #game-link:hover {
      text-decoration: underline;
    }

    @keyframes clownAnimation {
      0% {
        transform: translate(-50%, -50%) scale(1);
      }
      50% {
        transform: translate(-50%, -50%) scale(1.2);
      }
      100% {
        transform: translate(-50%, -50%) scale(1);
      }
    }
  </style>
</head>
<body>

  <h1>歡迎來到我的個人網站</h1>
  <p>這裡是我的介紹頁，請享受排球少年和一些驚喜！</p>

  <div class="image-container">
    <img src="https://example.com/haikyuu-image.jpg" alt="排球少年">
  </div>

  <button id="surpriseButton">點擊有驚喜</button>

  <div id="clown">🤡</div>
  <a id="game-link" href="game.html">點我開始小恐龍遊戲</a>

  <script>
    document.getElementById("surpriseButton").onclick = function() {
      // 顯示小丑並顯示遊戲鏈接
      document.getElementById("clown").style.display = "block";
      document.getElementById("game-link").style.display = "inline-block";
    };
  </script>

</body>
</html>
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>小恐龍遊戲</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f4f7f9;
      text-align: center;
      margin: 0;
      padding: 0;
    }

    h1 {
      color: #4CAF50;
      margin-top: 50px;
      font-size: 36px;
    }

    .game-area {
      background-color: #e0e0e0;
      height: 400px;
      width: 100%;
      position: relative;
      overflow: hidden;
    }

    #dino {
      position: absolute;
      bottom: 20px;
      left: 50px;
      width: 40px;
      height: 40px;
      background-color: #ff6347;
      border-radius: 5px;
    }

    .obstacle {
      position: absolute;
      bottom: 20px;
      width: 30px;
      height: 40px;
      background-color: #333;
      animation: moveObstacle 2s linear infinite;
    }

    @keyframes moveObstacle {
      0% {
        left: 100%;
      }
      100% {
        left: -30px;
      }
    }

    .game-over {
      display: none;
      font-size: 30px;
      color: red;
    }
  </style>
</head>
<body>

  <h1>小恐龍遊戲</h1>
  <div class="game-area">
    <div id="dino"></div>
    <div class="obstacle"></div>
    <div class="game-over">遊戲結束！</div>
  </div>

  <script>
    let dino = document.getElementById('dino');
    let gameOverText = document.querySelector('.game-over');
    let isJumping = false;
    
    document.addEventListener('keydown', function(event) {
      if (event.code === 'Space' && !isJumping) {
        jump();
      }
    });

    function jump() {
      isJumping = true;
      let jumpHeight = 0;
      let jumpInterval = setInterval(function() {
        if (jumpHeight < 100) {
          dino.style.bottom = `${20 + jumpHeight}px`;
          jumpHeight += 10;
        } else {
          clearInterval(jumpInterval);
          let fallInterval = setInterval(function() {
            if (jumpHeight > 0) {
              dino.style.bottom = `${20 + jumpHeight}px`;
              jumpHeight -= 10;
            } else {
              clearInterval(fallInterval);
              isJumping = false;
            }
          }, 20);
        }
      }, 20);
    }

    function checkCollision() {
      let dinoRect = dino.getBoundingClientRect();
      let obstacles = document.querySelectorAll('.obstacle');

      obstacles.forEach(obstacle => {
        let obstacleRect = obstacle.getBoundingClientRect();

        if (dinoRect.left < obstacleRect.right &&
            dinoRect.right > obstacleRect.left &&
            dinoRect.bottom > obstacleRect.top) {
          gameOver();
        }
      });
    }

    function gameOver() {
      gameOverText.style.display = 'block';
      document.querySelector('.game-area').classList.add('game-over');
    }

    setInterval(function() {
      checkCollision();
    }, 20);
  </script>

</body>
</html>
