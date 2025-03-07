<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>猜數字遊戲</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f8ff;
            text-align: center;
            padding: 50px;
        }
        .container {
            background-color: #ffffff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            margin: 0 auto;
        }
        input {
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .message {
            font-size: 18px;
            margin-top: 20px;
            color: #ff6347;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>猜數字遊戲</h1>
        <p>猜一個 1 到 100 之間的數字！</p>
        <input type="number" id="userGuess" placeholder="輸入你的猜測" min="1" max="100">
        <button onclick="checkGuess()">提交猜測</button>
        <p id="message" class="message"></p>
    </div>

    <script>
        // 隨機生成一個 1 到 100 之間的數字
        let secretNumber = Math.floor(Math.random() * 100) + 1;
        let attempts = 0;

        // 用戶的猜測判斷函數
        function checkGuess() {
            let userGuess = parseInt(document.getElementById('userGuess').value);
            let message = document.getElementById('message');
            attempts++;

            if (isNaN(userGuess) || userGuess < 1 || userGuess > 100) {
                message.textContent = "請輸入 1 到 100 之間的數字！";
                message.style.color = "#ff6347";
                return;
            }

            if (userGuess < secretNumber) {
                message.textContent = "太小了！再試一次！";
                message.style.color = "#ff6347";
            } else if (userGuess > secretNumber) {
                message.textContent = "太大了！再試一次！";
                message.style.color = "#ff6347";
            } else {
                message.textContent = `恭喜你！猜對了！你猜了 ${attempts} 次。`;
                message.style.color = "#32CD32";
                // 重設遊戲
                secretNumber = Math.floor(Math.random() * 100) + 1;
                attempts = 0;
            }
        }
    </script>

</body>
</html>

