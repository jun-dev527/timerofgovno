<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Таймер</title>
    <style>
        body {
            font-family: sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 20px;
            padding-top: 50px;
            background-color: #f4f4f4;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
        }

        button#startBtn {
            background-color: #4CAF50;
            color: white;
        }

        button#stopBtn {
            background-color: #f44336;
            color: white;
        }

        #timerDisplay {
            font-size: 24px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div id="timerDisplay">Прошло 0 сек</div>
    <button id="startBtn">Старт</button>
    <button id="stopBtn" disabled>Стоп</button>

    <script>
        let secondsPassed = 0;
        let intervalId;
        const timerDisplay = document.getElementById('timerDisplay');
        const startBtn = document.getElementById('startBtn');
        const stopBtn = document.getElementById('stopBtn');

        startBtn.addEventListener('click', () => {
            startBtn.disabled = true;
            stopBtn.disabled = false;
            intervalId = setInterval(() => {
                secondsPassed++;
                timerDisplay.textContent = `Прошло ${secondsPassed} сек`;
            }, 1000);
        });

        stopBtn.addEventListener('click', () => {
            clearInterval(intervalId);
            startBtn.disabled = false;
            stopBtn.disabled = true;
        });
    </script>
</body>
</html>
