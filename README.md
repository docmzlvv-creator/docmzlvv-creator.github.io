# docmzlvv-creator.github.io
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Таймер 42 часа</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: #111;
            color: #fff;
            font-family: Arial, sans-serif;
            margin: 0;
        }
        #timer {
            font-size: 3rem;
            font-weight: bold;
            background: #222;
            padding: 20px 40px;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
        }
    </style>
</head>
<body>

    <div id="timer">Загрузка...</div>

    <script>
        const TARGET_DATE = new Date('2026-08-02T18:45:00Z').getTime();
        const TOTAL_HOURS = 42;
        const STORAGE_KEY = 'timer_end_time_42h';

        // Проверяем, было ли уже сохранено время окончания
        let endTime = localStorage.getItem(STORAGE_KEY);

        if (!endTime) {
            // Если нет, устанавливаем время окончания через 42 часа от текущего момента
            endTime = new Date().getTime() + TOTAL_HOURS * 60 * 60 * 1000;
            localStorage.setItem(STORAGE_KEY, endTime);
        }

        function updateTimer() {
            const now = new Date().getTime();
            const distance = endTime - now;

            if (distance <= 0) {
                document.getElementById("timer").innerHTML = "Время вышло!";
                localStorage.removeItem(STORAGE_KEY); // Сброс при желании
                return;
            }

            const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((distance % (1000 * 60)) / 1000);

            // Форматируем вывод с ведущими нулями
            document.getElementById("timer").innerHTML = 
                String(hours).padStart(2, '0') + ":" + 
                String(minutes).padStart(2, '0') + ":" + 
                String(seconds).padStart(2, '0');
        }

        setInterval(updateTimer, 1000);
        updateTimer();
    </script>
</body>
</html>
