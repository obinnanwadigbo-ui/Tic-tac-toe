git clone <your-repo-url>
cd <your-repo-folder>
# Add your code files
git add .
git commit -m "My first commit"
git push# Tic-tac-toe
X and O game
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Super Intelligent Tic Tac Toe AI</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Arial, Helvetica, sans-serif;
    }

    body {
      background: linear-gradient(135deg, #111827, #1f2937);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      color: white;
    }

    .game-container {
      width: 360px;
      text-align: center;
    }

    h1 {
      margin-bottom: 15px;
      font-size: 2rem;
      color: #00e5ff;
    }

    .status {
      margin-bottom: 20px;
      font-size: 1.1rem;
      min-height: 28px;
      font-weight: bold;
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
    }

    .cell {
      width: 110px;
      height: 110px;
      background: #374151;
      border-radius: 15px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 3rem;
      cursor: pointer;
      transition: 0.2s;
      user-select: none;
      box-shadow: 0 5px 15px rgba(0,0,0,0.4);
    }

    .cell:hover {
      background: #4b5563;
      transform: scale(1.03);
    }

    .cell.x {
      color: #00e5ff;
    }

    .cell.o {
      color: #ff4d6d;
    }

    .controls {
      margin-top: 20px;
      display: flex;
      gap: 10px;
      justify-content: center;
    }

    button {
      padding: 12px 20px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      font-size: 1rem;
      font-weight: bold;
      transition: 0.2s;
    }

    .restart-btn {
      background: #00e5ff;
      color: black;
    }

    .restart-btn:hover {
      background: #00c4db;
    }

    .difficulty {
      background: #ff4d6d;
      color: white;
    }

    .difficulty:hover {
      background: #e63c5c;
    }

    .winner {
      animation: glow 0.8s infinite alternate;
    }

    @keyframes glow {
      from {
        box-shadow: 0 0 5px #00e5ff;
      }
      to {
        box-shadow: 0 0 20px #00e5ff;
      }
    }

    @media (max-width: 420px) {
      .game-container {
        width: 95%;
      }

      .cell {
        width: 100%;
        aspect-ratio: 1/1;
      }
    }
  </style>
</head>
<body>

<div class="game-container">
  <h1>Tic Tac Toe AI</h1>

  <div class="status" id="status">Your Turn (X)</div>

  <div class="board" id="board"></div>

  <div class="controls">
    <button class="restart-btn" onclick="restartGame()">Restart</button>
    <button class="difficulty" onclick="toggleDifficulty()">
      AI: Impossible
    </button>
  </div>
</div>

<script>
  const boardElement = document.getElementById("board");
  const statusText = document.getElementById("status");

  let board = Array(9).fill("");
  let gameOver = false;

  const HUMAN = "X";
  const AI = "O";

  let impossibleMode = true;

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

  function createBoard() {
    boardElement.innerHTML = "";

    board.forEach((cell, index) => {
      const div = document.createElement("div");
      div.classList.add("cell");

      if (cell === "X") div.classList.add("x");
      if (cell === "O") div.classList.add("o");

      div.textContent = cell;

      div.addEventListener("click", () => handleMove(index));

      boardElement.appendChild(div);
    });
  }

  function handleMove(index) {
    if (board[index] !== "" || gameOver) return;

    board[index] = HUMAN;
    createBoard();

    if (checkWinner(board, HUMAN)) {
      endGame("You Win 😎");
      return;
    }

    if (isDraw()) {
      endGame("Draw 🤝");
      return;
    }

    statusText.textContent = "AI Thinking...";

    setTimeout(() => {
      aiMove();

      if (checkWinner(board, AI)) {
        endGame("AI Wins 🤖");
        return;
      }

      if (isDraw()) {
        endGame("Draw 🤝");
        return;
      }

      statusText.textContent = "Your Turn (X)";
    }, 350);
  }

  function aiMove() {
    let bestMove;

    if (impossibleMode) {
      bestMove = minimax(board, AI).index;
    } else {
      // Slightly weaker AI occasionally
      if (Math.random() < 0.25) {
        const available = emptyCells(board);
        bestMove = available[Math.floor(Math.random() * available.length)];
      } else {
        bestMove = minimax(board, AI).index;
      }
    }

    board[bestMove] = AI;
    createBoard();
  }

  function minimax(newBoard, player) {
    const availSpots = emptyCells(newBoard);

    if (checkWinner(newBoard, HUMAN)) {
      return { score: -10 };
    }

    if (checkWinner(newBoard, AI)) {
      return { score: 10 };
    }

    if (availSpots.length === 0) {
      return { score: 0 };
    }

    const moves = [];

    for (let i = 0; i < availSpots.length; i++) {
      const move = {};
      move.index = availSpots[i];

      newBoard[availSpots[i]] = player;

      if (player === AI) {
        const result = minimax(newBoard, HUMAN);
        move.score = result.score;
      } else {
        const result = minimax(newBoard, AI);
        move.score = result.score;
      }

      newBoard[availSpots[i]] = "";
      moves.push(move);
    }

    let bestMove;

    if (player === AI) {
      let bestScore = -Infinity;

      for (let i = 0; i < moves.length; i++) {
        if (moves[i].score > bestScore) {
          bestScore = moves[i].score;
          bestMove = i;
        }
      }
    } else {
      let bestScore = Infinity;

      for (let i = 0; i < moves.length; i++) {
        if (moves[i].score < bestScore) {
          bestScore = moves[i].score;
          bestMove = i;
        }
      }
    }

    return moves[bestMove];
  }

  function checkWinner(boardState, player) {
    return winPatterns.some(pattern => {
      return pattern.every(index => boardState[index] === player);
    });
  }

  function isDraw() {
    return board.every(cell => cell !== "");
  }

  function emptyCells(boardState) {
    return boardState
      .map((cell, index) => cell === "" ? index : null)
      .filter(v => v !== null);
  }

  function endGame(message) {
    gameOver = true;
    statusText.textContent = message;

    highlightWinner();
  }

  function highlightWinner() {
    const cells = document.querySelectorAll(".cell");

    winPatterns.forEach(pattern => {
      const [a,b,c] = pattern;

      if (
        board[a] &&
        board[a] === board[b] &&
        board[b] === board[c]
      ) {
        cells[a].classList.add("winner");
        cells[b].classList.add("winner");
        cells[c].classList.add("winner");
      }
    });
  }

  function restartGame() {
    board = Array(9).fill("");
    gameOver = false;
    statusText.textContent = "Your Turn (X)";
    createBoard();
  }

  function toggleDifficulty() {
    impossibleMode = !impossibleMode;

    document.querySelector(".difficulty").textContent =
      impossibleMode ? "AI: Impossible" : "AI: Hard";
  }

  createBoard();
</script>

</body>
</html>
