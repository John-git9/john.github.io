<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <title>Авто-звук</title>
  <style>
    body {
      background: #0f0c1a;
      color: #e0d6ff;
      font-family: sans-serif;
      text-align: center;
      padding: 20vh 10%;
    }
    button {
      background: #6a0dad;
      color: white;
      border: none;
      padding: 12px 24px;
      margin-top: 20px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover { opacity: 0.9; }
    h1 {
      text-shadow: 0 0 10px #a366ff;
    }
  </style>
</head>
<body>

  <h1>🔊 Звук загружается...</h1>
  <p id="status">Ожидание взаимодействия для включения звука (политика браузера)</p>

  <!-- Аудио в Base64: 0.5 секунды тона 440 Гц (A4), MP3, ~2 КБ -->
  <audio id="sound" src="diadia-sasha.mp3"></audio>

  <script>
    const audio = document.getElementById('sound');
    const status = document.getElementById('status');

    // Пытаемся проиграть при загрузке
    const tryPlay = () => {
      audio.play()
        .then(() => {
          status.textContent = '✅ Звук воспроизведён!';
        })
        .catch(err => {
          status.textContent = '🔇 Автоплей заблокирован. Нажмите кнопку ниже.';
          document.body.insertAdjacentHTML('beforeend', 
            '<button onclick="document.getElementById(\'sound\').play().then(()=>this.textContent=\'✅ Играет!\').catch(()=>{}); this.disabled=true;">▶️ Включить звук</button>'
          );
        });
    };

    // Сразу пробуем (иногда срабатывает на некоторых устройствах)
    tryPlay();

    // И по первому клику — точно сработает
    document.addEventListener('click', tryPlay, { once: true });
  </script>

</body>
</html>
