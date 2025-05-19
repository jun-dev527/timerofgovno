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
            background-color:lightgoldenrodyellow;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            margin: 0 5px;
        }

        button#startBtn {
            background-color: #4CAF50;
            color: white;
        }

        button#stopBtn {
            background-color: #f44336;
            color: white;
        }
        button#resetTimeBtn {
            background-color: #2196F3;
            color: white;
        }
        

        #timerDisplay {
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 20px;
        }
        
        .buttons-container {
            display: flex;
            gap: 10px;
        }
    </style>
</head>
<body>
    <div id="timerDisplay">00:00:00</div>
    <div class="buttons-container">
        <button id="startBtn">Старт</button>
        <button id="stopBtn" disabled>Стоп</button>
        <button id="resetTimeBtn" disabled>Рестарт</button>
    </div>

    <script>
        let secondsPassed = 0;
        let intervalId = null;
        const timerDisplay = document.getElementById('timerDisplay');
        const startBtn = document.getElementById('startBtn');
        const stopBtn = document.getElementById('stopBtn');
        const resetTimeBtn = document.getElementById('resetTimeBtn');

        function formatTime(totalSeconds) {
            const hours = Math.floor(totalSeconds / 3600);
            const minutes = Math.floor((totalSeconds % 3600) / 60);
            const seconds = totalSeconds % 60;
            
            return [
                hours.toString().padStart(2, '0'),
                minutes.toString().padStart(2, '0'),
                seconds.toString().padStart(2, '0')
            ].join(':');
        }

        function updateTimerDisplay() {
            timerDisplay.textContent = formatTime(secondsPassed);
        }

        function startTimer() {
            if (intervalId !== null) return;
            
            startBtn.disabled = true;
            stopBtn.disabled = false;
            resetTimeBtn.disabled = false;
            
            intervalId = setInterval(() => {
                secondsPassed++;
                updateTimerDisplay();
            }, 1000);
        }

        function stopTimer() {
            clearInterval(intervalId);
            intervalId = null;
            startBtn.disabled = false;
            stopBtn.disabled = true;
        }

        function resetTimer() {
            secondsPassed = 0;
            updateTimerDisplay();
            if (intervalId === null) {
                resetTimeBtn.disabled = true;
            }
        }

        startBtn.addEventListener('click', startTimer);
        stopBtn.addEventListener('click', stopTimer);
        resetTimeBtn.addEventListener('click', resetTimer);
        
        // Инициализация
        updateTimerDisplay();
    </script>
</body>
</html>
