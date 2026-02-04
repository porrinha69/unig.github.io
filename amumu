<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Mini Pokémon</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #1e1e1e;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    #game {
      width: 360px;
      height: 640px;
      background: #2ecc71;
      position: relative;
      overflow: hidden;
      border-radius: 16px;
    }

    #player {
      width: 32px;
      height: 32px;
      background: red;
      position: absolute;
      top: 300px;
      left: 160px;
    }

    .controls {
      position: absolute;
      bottom: 10px;
      width: 100%;
      display: flex;
      justify-content: space-around;
      gap: 8px;
      padding: 0 10px;
      box-sizing: border-box;
    }

    button {
      padding: 10px 14px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      background: #ecf0f1;
      cursor: pointer;
    }

    button:active {
      transform: scale(0.95);
    }

    #battle {
      position: absolute;
      inset: 0;
      background: #34495e;
      display: none;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 20px;
      box-sizing: border-box;
    }

    #battle h2 {
      margin-bottom: 12px;
    }

    #battle p {
      margin-bottom: 16px;
    }

    #battle .battle-buttons {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      justify-content: center;
    }

    #battle .battle-buttons button {
      min-width: 120px;
    }
  </style>
</head>
<body>
  <div id="game">
    <div id="player"></div>

    <!-- Tela de batalha -->
    <div id="battle">
      <h2>Um Pokémon selvagem apareceu!</h2>
      <p>O que você quer fazer?</p>
      <div class="battle-buttons">
        <button id="fightBtn">Lutar</button>
        <button id="bagBtn">Mochila</button>
        <button id="runBtn">Fugir</button>
      </div>
      <p id="battleMessage"></p>
    </div>

    <!-- Controles -->
    <div class="controls">
      <button id="upBtn">▲</button>
      <button id="leftBtn">◀</button>
      <button id="downBtn">▼</button>
      <button id="rightBtn">▶</button>
    </div>
  </div>

  <script>
    const game = document.getElementById('game');
    const player = document.getElementById('player');
    const battle = document.getElementById('battle');
    const battleMessage = document.getElementById('battleMessage');

    const fightBtn = document.getElementById('fightBtn');
    const bagBtn = document.getElementById('bagBtn');
    const runBtn = document.getElementById('runBtn');

    const upBtn = document.getElementById('upBtn');
    const downBtn = document.getElementById('downBtn');
    const leftBtn = document.getElementById('leftBtn');
    const rightBtn = document.getElementById('rightBtn');

    let inBattle = false;

    function movePlayer(dx, dy) {
      if (inBattle) return;

      const rect = game.getBoundingClientRect();
      const pRect = player.getBoundingClientRect();

      let newLeft = player.offsetLeft + dx;
      let newTop = player.offsetTop + dy;

      // limites do "mapa"
      const maxLeft = rect.width - pRect.width;
      const maxTop = rect.height - pRect.height;

      if (newLeft < 0) newLeft = 0;
      if (newTop < 0) newTop = 0;
      if (newLeft > maxLeft) newLeft = maxLeft;
      if (newTop > maxTop) newTop = maxTop;

      player.style.left = newLeft + 'px';
      player.style.top = newTop + 'px';

      // chance de encontrar batalha
      const chance = Math.random();
      if (chance < 0.2) { // 20% de chance a cada movimento
        startBattle();
      }
    }

    function startBattle() {
      inBattle = true;
      battle.style.display = 'flex';
      battleMessage.textContent = '';
    }

    function endBattle(message) {
      battleMessage.textContent = message;
      // Sai da batalha após um pequeno tempo
      setTimeout(() => {
        battle.style.display = 'none';
        inBattle = false;
        battleMessage.textContent = '';
      }, 1200);
    }

    // Eventos dos botões de movimento
    upBtn.addEventListener('click', () => movePlayer(0, -20));
    downBtn.addEventListener('click', () => movePlayer(0, 20));
    leftBtn.addEventListener('click', () => movePlayer(-20, 0));
    rightBtn.addEventListener('click', () => movePlayer(20, 0));

    // Teclado (setas)
    document.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowUp') movePlayer(0, -20);
      if (e.key === 'ArrowDown') movePlayer(0, 20);
      if (e.key === 'ArrowLeft') movePlayer(-20, 0);
      if (e.key === 'ArrowRight') movePlayer(20, 0);
    });

    // Botões de batalha
    fightBtn.addEventListener('click', () => {
      const win = Math.random() < 0.7; // 70% de chance de ganhar
      if (win) {
        endBattle('Você ganhou a batalha!');
      } else {
        endBattle('Você perdeu a batalha...');
      }
    });

    bagBtn.addEventListener('click', () => {
      endBattle('Você usou um item (ainda não implementado).');
    });

    runBtn.addEventListener('click', () => {
      const escape = Math.random() < 0.9;
      if (escape) {
        endBattle('Você fugiu com sucesso!');
      } else {
        endBattle('Não conseguiu fugir!');
      }
    });
  </script>
</body>
</html>
