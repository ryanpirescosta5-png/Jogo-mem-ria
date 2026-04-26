# Jogo-mem-ria
Jogo-memória 
https://seunome.github.io/jogo-memoria/<!DOCTYPE html><html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Jogo da Memória Educativo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #121212;
      color: white;
    }
    h1 { margin-top: 20px; }
    .grid {
      display: grid;
      grid-template-columns: repeat(4, 100px);
      gap: 10px;
      justify-content: center;
      margin-top: 20px;
    }
    .card {
      width: 100px;
      height: 100px;
      background: #1e1e1e;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
      cursor: pointer;
      border-radius: 10px;
    }
    .flipped {
      background: #4caf50;
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      background: #2196f3;
      color: white;
      cursor: pointer;
    }
  </style>
</head>
<body><h1>🧠 Jogo da Memória Educativo</h1>
<p>Encontre os pares e exercite seu cérebro!</p><div class="grid" id="game"></div>
<button onclick="startGame()">Reiniciar</button><script>
  const emojis = ['📚','📚','🌎','🌎','➕','➕','🧪','🧪','📖','📖','🔬','🔬','🧠','🧠','✏️','✏️'];
  let shuffled = [];
  let first = null;
  let second = null;
  let lock = false;

  function shuffle(array) {
    return array.sort(() => 0.5 - Math.random());
  }

  function startGame() {
    const game = document.getElementById('game');
    game.innerHTML = '';
    shuffled = shuffle([...emojis]);
    first = null;
    second = null;
    lock = false;

    shuffled.forEach((emoji, index) => {
      const card = document.createElement('div');
      card.classList.add('card');
      card.dataset.emoji = emoji;
      card.dataset.index = index;
      card.onclick = () => flipCard(card);
      game.appendChild(card);
    });
  }

  function flipCard(card) {
    if (lock || card.classList.contains('flipped')) return;

    card.textContent = card.dataset.emoji;
    card.classList.add('flipped');

    if (!first) {
      first = card;
      return;
    }

    second = card;
    lock = true;

    if (first.dataset.emoji === second.dataset.emoji) {
      first = null;
      second = null;
      lock = false;
    } else {
      setTimeout(() => {
        first.textContent = '';
        second.textContent = '';
        first.classList.remove('flipped');
        second.classList.remove('flipped');
        first = null;
        second = null;
        lock = false;
      }, 1000);
    }
  }

  startGame();
</script></body>
</html>