# PRODIGY_WD_03
Task : 3 Tic-Tac-Toe Web application
*<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe Web Application</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
        }

        .tic-tac-toe {
            text-align: center;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 10px;
        }

        .cell {
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #333;
            color: white;
            font-size: 32px;
            cursor: pointer;
            border-radius: 10px;
        }

        .cell:hover {
            background-color: #555;
        }

        .message {
            margin-top: 20px;
            font-size: 24px;
        }

        .restart {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
            border: none;
            background-color: #333;
            color: white;
            border-radius: 5px;
            transition: background-color 0.3s;
        }

        .restart:hover {
            background-color: #555;
        }
    </style>
</head>
<body>
    <div class="tic-tac-toe">
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
        <div class="message" id="message">Player X's Turn</div>
        <button class="restart" onclick="restartGame()">Restart Game</button>
    </div>

    <script>
        let board = ["", "", "", "", "", "", "", "", ""];
        let currentPlayer = "X";
        let gameActive = true;

        const winningConditions = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],
            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],
            [0, 4, 8],
            [2, 4, 6]
        ];

        const boardElement = document.getElementById("board");
        const messageElement = document.getElementById("message");

        boardElement.addEventListener("click", handleCellClick);

        function handleCellClick(event) {
            const clickedCell = event.target;
            const clickedCellIndex = clickedCell.getAttribute("data-index");

            if (board[clickedCellIndex] !== "" || !gameActive) {
                return;
            }

            updateCell(clickedCell, clickedCellIndex);
            checkResult();
        }

        function updateCell(clickedCell, index) {
            board[index] = currentPlayer;
            clickedCell.textContent = currentPlayer;
        }

        function checkResult() {
            let roundWon = false;

            for (let i = 0; i < winningConditions.length; i++) {
                const winCondition = winningConditions[i];
                let a = board[winCondition[0]];
                let b = board[winCondition[1]];
                let c = board[winCondition[2]];

                if (a === "" || b === "" || c === "") {
                    continue;
                }

                if (a === b && b === c) {
                    roundWon = true;
                    break;
                }
            }

            if (roundWon) {
                messageElement.textContent = `Player ${currentPlayer} Wins!`;
                gameActive = false;
                return;
            }

            if (!board.includes("")) {
                messageElement.textContent = "It's a Draw!";
                gameActive = false;
                return;
            }

            currentPlayer = currentPlayer === "X" ? "O" : "X";
            messageElement.textContent = `Player ${currentPlayer}'s Turn`;
        }

        function restartGame() {
            board = ["", "", "", "", "", "", "", "", ""];
            currentPlayer = "X";
            gameActive = true;
            messageElement.textContent = `Player ${currentPlayer}'s Turn`;

            document.querySelectorAll(".cell").forEach(cell => cell.textContent = "");
        }
    </script>
</body>
</html>
