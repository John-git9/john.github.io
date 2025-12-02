<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Авто-звук</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: #0f0c1a;
      color: #e0d6ff;
      font-family: 'Segoe UI', sans-serif;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      overflow: hidden;
      user-select: none;
      transition: background 0.3s;
    }

    body:active {
      background: #1a142d;
    }

    body:hover::before {
      opacity: 0.15;
    }

    /* Неоновая подсветка при наведении */
    body::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: radial-gradient(circle at center, #a366ff 0%, transparent 70%);
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.4s;
    }

    h1 {
      font-size: 2.8rem;
      text-shadow: 0 0 12px #a366ff, 0 0 20px #7a3dd1;
      margin-bottom: 1rem;
      letter-spacing: 1px;
    }

    #status {
      font-size: 1.2rem;
      opacity: 0.8;
      max-width: 80%;
      line-height: 1.5;
    }

    /* Скрыть стандартные элементы управления */
    audio { display: none; }
  </style>
</head>
<body>

  <h1>🔊 Кликни в любом месте</h1>
  <p id="status">Первое касание разрешит звук (политика браузера)</p>

  <!-- Base64: 440 Гц, 0.5 сек, MP3 (~2 КБ) -->
  <audio id="sound" src="diadia-sasha.mp3"></audio>
  <script>
    const audio = document.getElementById('sound');
    const status = document.getElementById('status');
    const body = document.body;

    const enableSound = () => {
      // Размучиваем и играем
      audio.muted = false;
      audio
        .play()
        .then(() => {
          status.textContent = '✅ Звук включён! Кликай ещё — будет играть.';
          body.style.background = '#140f28';
          document.querySelector('h1').textContent = '🎧 Звук активен!';
        })
        .catch(err => {
          console.warn('Audio play failed:', err);
        });
    };

    // Первое касание/клик — включает звук
    body.addEventListener('click', enableSound, { once: true });
    body.addEventListener('touchstart', enableSound, { once: true });
  </script>

</body>
</html>
