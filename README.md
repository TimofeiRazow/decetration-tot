<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Telegram Web App</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
</head>
<body>

    <h1>Отправка сообщения боту</h1>

    <form id="messageForm">
        <label for="message">Введите сообщение:</label>
        <input type="text" id="message" name="message" required>
        <button type="submit">Отправить</button>
    </form>

    <p id="response"></p>

    <script>
        // Инициализация Telegram Web App
        const tg = window.Telegram.WebApp;

        // Получаем user_id из initDataUnsafe
        const user = tg.initDataUnsafe.user;
        const chatId = user.id;  // Это и есть user_id, который используется как chat_id для бота

        // Форма для отправки сообщения
        document.getElementById('messageForm').addEventListener('submit', async function(event) {
            event.preventDefault();  // Останавливаем стандартное поведение формы

            // Получаем текст сообщения из формы
            const message = document.getElementById('message').value;

            // Отправляем запрос на сервер, который отправит сообщение в бот
            const response = await fetch('https://your-server.com/api/send-message', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    chat_id: chatId,   // Используем chat_id пользователя
                    text: message      // Сообщение для бота
                })
            });

            // Отображаем результат отправки
            const result = await response.json();
            document.getElementById('response').innerText = result.status;
        });
    </script>
</body>
</html>
