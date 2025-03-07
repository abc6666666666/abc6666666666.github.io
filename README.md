<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>猜數字遊戲</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            text-align: center;
            padding: 20px;
        }
        h1 {
            color: #4CAF50;
        }
        #message {
            font-size: 18px;
            color: #555;
        }
        input[type="number"] {
            padding: 10px;
            font-size: 16px;
            margin: 10px;
            width: 60px;
            text-align: center;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

    <h1>猜數字遊戲</h1>
    <p>我已經選擇了一個1到100之間的數字，請你來猜猜它是什麼！</p>
    <div id="message">請輸入1到100之間的數字。</div>
    <input type="number" id="guess" min="1" max="100">
    <button onclick="checkGuess()">猜猜看！</button>

    <script>
        // 隨機選擇一個1到100之間的數字
        let secretNumber = Math.floor(Math.random() * 100) + 1;
        let attempts = 0;

        // 檢查猜測的函數
        function checkGuess() {
            const userGuess = document.getElementById("guess").value;
            const messageDiv = document.getElementById("message");
            attempts++;

            // 檢查是否為有效數字
            if (userGuess < 1 || userGuess > 100 || isNaN(userGuess)) {
                messageDiv.textContent = "請輸入1到100之間的數字！";
                return;
            }

            // 提示用戶猜測的結果
            if (userGuess < secretNumber) {
                messageDiv.textContent = "猜得太低了，再試一次！";
            } else if (userGuess > secretNumber) {
                messageDiv.textContent = "猜得太高了，再試一次！";
            } else {
                messageDiv.textContent = `恭喜你，猜對了！正確答案是 ${secretNumber}。你總共猜了 ${attempts} 次。`;
                // 重新開始遊戲
                secretNumber = Math.floor(Math.random() * 100) + 1;
                attempts = 0;
            }

            // 清空輸入框
            document.getElementById("guess").value = "";
        }
    </script>

</body>
</html>
