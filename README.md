# game_tick
<!DOCTYPE html>
<html>
  <head>
    <title>Tic Tac Toe</title>
    <link rel="stylesheet" type="text/css" href="style.css">
  </head>
  <body>
    <h1>Tic Tac Toe</h1>
    <div id="board">
      <button id="1"></button>
      <button id="2"></button>
      <button id="3"></button>
      <button id="4"></button>
      <button id="5"></button>
      <button id="6"></button>
      <button id="7"></button>
      <button id="8"></button>
      <button id="9"></button>
    </div>
    <script src="script.js"></script>
  </body>
</html>

<!--- css part --->
#board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
  margin-top: 20px;
}

button {
  font-size: 40px;
  height: 100px;
}


<!---- java Script-->
// Game variables
let currentPlayer = 'X';
let gameOver = false;
let moves = 0;

// Winning combinations
const winningCombos = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
  [1, 4, 7],
  [2, 5, 8],
  [3, 6, 9],
  [1, 5, 9],
  [3, 5, 7],
];

// Get the board buttons
const buttons = document.querySelectorAll('button');

// Add click event listeners to each button
buttons.forEach(button => {
  button.addEventListener('click', () => {
    // If game is over, exit
    if (gameOver) return;

    // If button is already clicked, exit
    if (button.innerText !== '') return;

    // Update button text with current player
    button.innerText = currentPlayer;

    // Increment move count
    moves++;

    // Check for win or draw
    checkWin();

    // Switch to other player
    switchPlayer();
  });
});

// Check for win or draw
function checkWin() {
  winningCombos.forEach(combo => {
    if (
      buttons[combo[0] - 1].innerText === currentPlayer &&
      buttons[combo[1] - 1].innerText === currentPlayer &&
      buttons[combo[2] - 1].innerText === currentPlayer
    ) {
      // Player has won
      gameOver = true;
      alert(`Congratulations! ${currentPlayer} wins.`);
    }
  });

  if (!gameOver && moves === 9) {
    // Draw
    gameOver = true;
    alert('Draw! match is only drawn after all boxes are filled and nobody has won.');
  }
}

// Switch to other player
function switchPlayer() {
  currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
}

