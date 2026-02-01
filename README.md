
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic-Tac-Toe Game</title>
  <style>
    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #89f7fe, #66a6ff);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .container {
      text-align: center;
    }

    h1 {
      color: #333;
      margin-bottom: 20px;
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-gap: 10px;
      justify-content: center;
      margin-bottom: 20px;
    }

    .cell {
      width: 100px;
      height: 100px;
      background-color: white;
      border-radius: 12px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
      font-size: 2em;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      transition: 0.3s;
    }

    .cell:hover {
      background-color: #f0f0f0;
    }

    #statusText {
      color: #222;
      font-weight: bold;
    }

    button {
      padding: 10px 20px;
      background: #0078ff;
      border: none;
      color: white;
      font-size: 1em;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: #005ecb;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Tic-Tac-Toe</h1>
    <div class="board" id="board">
      <div class="cell" data-index="0"></div>
      <div class="cell" data-index="1"></div>
      <div class="cell" data-index="2"></div>
      <div class="cell" data-index="3"></div>
      <div class="cell" data-index="4"></div>
      <div class="cell" data-index="5"></div>
      <div class="cell" data-index="6"></div>
      <div class="cell" data-index="7"></div>
      <div class="cell" data-index="8"></div>
    </div>
    <h2 id="statusText">Player X's Turn</h2>
    <button id="resetBtn">Restart Game</button>
  </div>

  <script>
    const cells = document.querySelectorAll('.cell');
    const statusText = document.getElementById('statusText');
    const resetBtn = document.getElementById('resetBtn');

    let currentPlayer = 'X';
    let board = ["", "", "", "", "", "", "", "", ""];
    let running = true;

    const winPatterns = [
      [0,1,2],
      [3,4,5],
      [6,7,8],
      [0,3,6],
      [1,4,7],
      [2,5,8],
      [0,4,8],
      [2,4,6]
    ];

    cells.forEach(cell => cell.addEventListener('click', cellClicked));
    resetBtn.addEventListener('click', restartGame);

    function cellClicked() {
      const index = this.getAttribute('data-index');
      if (board[index] !== "" || !running) return;

      updateCell(this, index);
      checkWinner();
    }

    function updateCell(cell, index) {
      board[index] = currentPlayer;
      cell.textContent = currentPlayer;
    }

    function changePlayer() {
      currentPlayer = currentPlayer === "X" ? "O" : "X";
      statusText.textContent = `Player ${currentPlayer}'s Turn`;
    }

    function checkWinner() {
      let roundWon = false;

      for (let i = 0; i < winPatterns.length; i++) {
        const [a, b, c] = winPatterns[i];
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          roundWon = true;
          break;
        }
      }

      if (roundWon) {
        statusText.textContent = `🎉 Player ${currentPlayer} Wins!`;
        running = false;
      } else if (!board.includes("")) {
        statusText.textContent = "😐 It's a Draw!";
        running = false;
      } else {
        changePlayer();
      }
    }

    function restartGame() {
      currentPlayer = 'X';
      board = ["", "", "", "", "", "", "", "", ""];
      statusText.textContent = "Player X's Turn";
      cells.forEach(cell => (cell.textContent = ""));
      running = true;
    }
  </script>
</body>
</html>
