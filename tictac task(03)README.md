# PRODIGY_WD_03
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <style>
        body {
            font-family: Arial;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background: #e6f3ff; /* Light blue background */
        }
        .game {text-align: center;}
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            gap: 5px;
            margin-top: 20px;
        }
        .cell {
            width: 100px;
            height: 100px;
            background: #fff;
            border: 2px solid #333;
            font-size: 2em;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .cell:hover {background: #f0f0f0;}
        .cell.x {color: #ff4136;} /* Red for X */
        .cell.o {color: #0074d9;} /* Blue for O */
        #status {margin-top: 20px; font-size: 1.2em;}
        #reset {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 1em;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }
        #reset:hover {background-color: #45a049;}
    </style>
</head>
<body>
    <div class="game">
        <h1>Tic-Tac-Toe</h1>
        <div class="board" id="board"></div>
        <div id="status"></div>
        <button id="reset">Reset Game</button>
    </div>
    <script>
        const board = document.getElementById('board');
        const status = document.getElementById('status');
        let currentPlayer = 'X', gameState = ['', '', '', '', '', '', '', '', ''];
        const winConditions = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];

        function createBoard() {
            gameState.forEach((_, index) => {
                const cell = document.createElement('div');
                cell.classList.add('cell');
                cell.addEventListener('click', () => handleClick(cell, index));
                board.appendChild(cell);
            });
        }

        function handleClick(cell, index) {
            if (gameState[index] || checkWinner()) return;
            gameState[index] = currentPlayer;
            cell.textContent = currentPlayer;
            cell.classList.add(currentPlayer.toLowerCase());
            if (checkWinner()) {
                status.textContent = `Player ${currentPlayer} wins!`;
            } else if (!gameState.includes('')) {
                status.textContent = "It's a draw!";
            } else {
                currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
                status.textContent = `Player ${currentPlayer}'s turn`;
            }
        }

        function checkWinner() {
            return winConditions.some(condition => {
                return condition.every(index => gameState[index] === currentPlayer);
            });
        }

        function resetGame() {
            gameState = ['', '', '', '', '', '', '', '', ''];
            currentPlayer = 'X';
            status.textContent = `Player ${currentPlayer}'s turn`;
            Array.from(board.children).forEach(cell => {
                cell.textContent = '';
                cell.classList.remove('x', 'o');
            });
        }

        createBoard();
        status.textContent = `Player ${currentPlayer}'s turn`;
        document.getElementById('reset').addEventListener('click', resetGame);
    </script>
</body>
</html>
