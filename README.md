<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>کی دوز | بازی مدرن</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Vazirmatn', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: background 0.5s ease;
        }

        /* تم‌های مختلف */
        body.theme-purple {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        body.theme-blue {
            background: linear-gradient(135deg, #2193b0 0%, #6dd5ed 100%);
        }

        body.theme-green {
            background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
        }

        body.theme-dark {
            background: linear-gradient(135deg, #2c3e50 0%, #3498db 100%);
        }

        body.theme-sunset {
            background: linear-gradient(135deg, #ff6b6b 0%, #feca57 100%);
        }

        .game-container {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 30px;
            padding: 30px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            width: 90%;
            max-width: 500px;
            transition: all 0.3s ease;
        }

        /* منوی اصلی */
        .main-menu {
            text-align: center;
        }

        .game-title {
            font-size: 4rem;
            font-weight: 900;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .menu-buttons {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin: 30px 0;
        }

        .menu-btn {
            padding: 15px 30px;
            font-size: 1.2rem;
            border: none;
            border-radius: 15px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        .menu-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }

        .menu-btn.secondary {
            background: linear-gradient(135deg, #ff6b6b, #feca57);
        }

        /* صفحه بازی */
        .game-board {
            text-align: center;
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding: 10px;
            background: rgba(102, 126, 234, 0.1);
            border-radius: 15px;
        }

        .player-turn {
            font-size: 1.2rem;
            font-weight: bold;
            color: #333;
        }

        .player-turn span {
            color: #667eea;
            font-size: 1.4rem;
        }

        .back-btn {
            padding: 8px 15px;
            border: none;
            border-radius: 10px;
            background: #ff6b6b;
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .back-btn:hover {
            background: #ff5252;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin: 20px 0;
            background: rgba(102, 126, 234, 0.2);
            padding: 10px;
            border-radius: 20px;
        }

        .cell {
            aspect-ratio: 1;
            background: white;
            border-radius: 15px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 4rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        .cell:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.4);
        }

        .cell.x {
            color: #667eea;
        }

        .cell.o {
            color: #ff6b6b;
        }

        .cell.winner {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white !important;
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0%, 100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.05);
            }
        }

        .game-status {
            font-size: 1.5rem;
            margin: 20px 0;
            padding: 15px;
            border-radius: 15px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            font-weight: bold;
        }

        .reset-btn {
            padding: 12px 30px;
            font-size: 1.1rem;
            border: none;
            border-radius: 15px;
            background: linear-gradient(135deg, #ff6b6b, #feca57);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            width: 100%;
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(255, 107, 107, 0.4);
        }

        /* صفحه تنظیمات */
        .settings-panel {
            text-align: center;
        }

        .settings-panel h2 {
            color: #333;
            margin-bottom: 30px;
            font-size: 2rem;
        }

        .settings-option {
            margin: 20px 0;
            text-align: right;
        }

        .settings-option label {
            display: block;
            margin-bottom: 10px;
            color: #333;
            font-weight: bold;
        }

        .theme-selector {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-top: 10px;
        }

        .theme-option {
            padding: 15px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            color: white;
            transition: all 0.3s ease;
        }

        .theme-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }

        .theme-option.purple {
            background: linear-gradient(135deg, #667eea, #764ba2);
        }

        .theme-option.blue {
            background: linear-gradient(135deg, #2193b0, #6dd5ed);
        }

        .theme-option.green {
            background: linear-gradient(135deg, #11998e, #38ef7d);
        }

        .theme-option.dark {
            background: linear-gradient(135deg, #2c3e50, #3498db);
        }

        .theme-option.sunset {
            background: linear-gradient(135deg, #ff6b6b, #feca57);
        }

        .hidden {
            display: none;
        }

        .game-mode-select {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }

        .mode-btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 10px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
        }

        .mode-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
        }

        .footer-text {
            margin-top: 20px;
            color: #666;
            font-size: 0.9rem;
        }
    </style>
</head>
<body class="theme-purple">
    <div class="game-container" id="gameContainer">
        <!-- منوی اصلی -->
        <div id="mainMenu" class="main-menu">
            <h1 class="game-title">کی دوز</h1>
            <div class="menu-buttons">
                <button class="menu-btn" onclick="showGameMode()">شروع بازی</button>
                <button class="menu-btn secondary" onclick="showSettings()">تنظیمات</button>
            </div>
            <div class="footer-text">یک بازی مدرن و جذاب</div>
        </div>

        <!-- انتخاب حالت بازی -->
        <div id="gameModeMenu" class="main-menu hidden">
            <h2 class="game-title" style="font-size: 2rem;">انتخاب حالت بازی</h2>
            <div class="menu-buttons">
                <button class="menu-btn" onclick="startGame('ai')">بازی با ربات</button>
                <button class="menu-btn secondary" onclick="startGame('twoPlayer')">دو نفره</button>
                <button class="menu-btn" style="background: #666;" onclick="backToMain()">بازگشت</button>
            </div>
        </div>

        <!-- صفحه تنظیمات -->
        <div id="settingsMenu" class="settings-panel hidden">
            <h2>تنظیمات بازی</h2>
            <div class="settings-option">
                <label>رنگ پس زمینه:</label>
                <div class="theme-selector">
                    <button class="theme-option purple" onclick="changeTheme('purple')">بنفش</button>
                    <button class="theme-option blue" onclick="changeTheme('blue')">آبی</button>
                    <button class="theme-option green" onclick="changeTheme('green')">سبز</button>
                    <button class="theme-option dark" onclick="changeTheme('dark')">تیره</button>
                    <button class="theme-option sunset" onclick="changeTheme('sunset')">غروب</button>
                </div>
            </div>
            <button class="menu-btn" style="margin-top: 20px;" onclick="backToMain()">بازگشت به منو</button>
        </div>

        <!-- صفحه بازی -->
        <div id="gameBoard" class="game-board hidden">
            <div class="game-header">
                <button class="back-btn" onclick="backToMain()">← بازگشت</button>
                <div class="player-turn" id="turnIndicator">نوبت: <span id="currentPlayer">X</span></div>
            </div>
            
            <div class="board" id="board">
                <!-- سلول‌های بازی با جاوااسکریپت ساخته می‌شوند -->
            </div>

            <div class="game-status" id="gameStatus">در جریان...</div>
            <button class="reset-btn" id="resetBtn" onclick="resetGame()">بازی جدید</button>
        </div>
    </div>

    <script>
        // متغیرهای اصلی بازی
        let currentGameMode = 'twoPlayer'; // 'ai' یا 'twoPlayer'
        let board = ['', '', '', '', '', '', '', '', ''];
        let currentPlayer = 'X';
        let gameActive = true;
        let gameType = 'mainMenu';
        let aiTimeout = null;

        // سلول‌های برنده
        const winningConditions = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8], // ردیف‌ها
            [0, 3, 6], [1, 4, 7], [2, 5, 8], // ستون‌ها
            [0, 4, 8], [2, 4, 6] // قطرها
        ];

        // ایجاد سلول‌های بازی
        function createBoard() {
            const boardElement = document.getElementById('board');
            boardElement.innerHTML = '';
            for (let i = 0; i < 9; i++) {
                const cell = document.createElement('div');
                cell.classList.add('cell');
                cell.setAttribute('data-index', i);
                cell.onclick = () => handleCellClick(i);
                boardElement.appendChild(cell);
            }
        }

        // به‌روزرسانی نمایش صفحه
        function updateBoardDisplay() {
            const cells = document.querySelectorAll('.cell');
            cells.forEach((cell, index) => {
                cell.textContent = board[index];
                if (board[index] === 'X') {
                    cell.classList.add('x');
                    cell.classList.remove('o');
                } else if (board[index] === 'O') {
                    cell.classList.add('o');
                    cell.classList.remove('x');
                } else {
                    cell.classList.remove('x', 'o');
                }
            });
        }

        // بررسی برنده
        function checkWinner() {
            for (let condition of winningConditions) {
                const [a, b, c] = condition;
                if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                    return board[a];
                }
            }
            return null;
        }

        // بررسی مساوی
        function checkDraw() {
            return board.every(cell => cell !== '');
        }

        // حرکت ربات
        function makeAIMove() {
            if (!gameActive || currentGameMode !== 'ai' || currentPlayer !== 'O') return;

            // سلول‌های خالی را پیدا کن
            const emptyCells = board.reduce((acc, cell, index) => {
                if (cell === '') acc.push(index);
                return acc;
            }, []);

            if (emptyCells.length > 0) {
                // ربات هوشمند: اولویت با بردن یا جلوگیری از باخت
                let move = null;

                // چک کردن برای برد ربات
                for (let cell of emptyCells) {
                    board[cell] = 'O';
                    if (checkWinner() === 'O') {
                        move = cell;
                        board[cell] = '';
                        break;
                    }
                    board[cell] = '';
                }

                // چک کردن برای جلوگیری از برد بازیکن
                if (move === null) {
                    for (let cell of emptyCells) {
                        board[cell] = 'X';
                        if (checkWinner() === 'X') {
                            move = cell;
                            board[cell] = '';
                            break;
                        }
                        board[cell] = '';
                    }
                }

                // اگر حرکت خاصی نبود، وسط یا گوشه یا تصادفی
                if (move === null) {
                    const preferredMoves = [4, 0, 2, 6, 8, 1, 3, 5, 7];
                    for (let cell of preferredMoves) {
                        if (emptyCells.includes(cell)) {
                            move = cell;
                            break;
                        }
                    }
                }

                if (move !== null) {
                    setTimeout(() => {
                        board[move] = 'O';
                        updateBoardDisplay();
                        const winner = checkWinner();
                        if (winner) {
                            document.getElementById('gameStatus').textContent = `بازیکن ${winner} برنده شد! 🎉`;
                            gameActive = false;
                            highlightWinningCells(winner);
                        } else if (checkDraw()) {
                            document.getElementById('gameStatus').textContent = 'مساوی! 🤝';
                            gameActive = false;
                        } else {
                            currentPlayer = 'X';
                            document.getElementById('currentPlayer').textContent = 'X';
                        }
                    }, 500);
                }
            }
        }

        // هایلایت سلول‌های برنده
        function highlightWinningCells(winner) {
            for (let condition of winningConditions) {
                const [a, b, c] = condition;
                if (board[a] === winner && board[b] === winner && board[c] === winner) {
                    document.querySelectorAll('.cell')[a].classList.add('winner');
                    document.querySelectorAll('.cell')[b].classList.add('winner');
                    document.querySelectorAll('.cell')[c].classList.add('winner');
                    break;
                }
            }
        }

        // کلیک روی سلول
        function handleCellClick(index) {
            if (!gameActive) return;
            if (board[index] !== '') return;
            if (currentGameMode === 'ai' && currentPlayer !== 'X') return;

            // حرکت بازیکن
            board[index] = currentPlayer;
            updateBoardDisplay();

            const winner = checkWinner();
            if (winner) {
                document.getElementById('gameStatus').textContent = `بازیکن ${winner} برنده شد! 🎉`;
                gameActive = false;
                highlightWinningCells(winner);
            } else if (checkDraw()) {
                document.getElementById('gameStatus').textContent = 'مساوی! 🤝';
                gameActive = false;
            } else {
                // تغییر نوبت
                currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
                document.getElementById('currentPlayer').textContent = currentPlayer;

                // اگر حالت ربات است و نوبت O است، ربات حرکت کند
                if (currentGameMode === 'ai' && currentPlayer === 'O' && gameActive) {
                    makeAIMove();
                }
            }
        }

        // شروع بازی
        function startGame(mode) {
            currentGameMode = mode;
            resetGame();
            
            document.getElementById('mainMenu').classList.add('hidden');
            document.getElementById('gameModeMenu').classList.add('hidden');
            document.getElementById('settingsMenu').classList.add('hidden');
            document.getElementById('gameBoard').classList.remove('hidden');
            
            createBoard();
            updateBoardDisplay();
            document.getElementById('currentPlayer').textContent = 'X';
            document.getElementById('gameStatus').textContent = 'در جریان...';
        }

        // ریست کردن بازی
        function resetGame() {
            board = ['', '', '', '', '', '', '', '', ''];
            currentPlayer = 'X';
            gameActive = true;
            
            // پاک کردن هایلایت‌ها
            document.querySelectorAll('.cell').forEach(cell => {
                cell.classList.remove('winner');
            });
            
            updateBoardDisplay();
            document.getElementById('currentPlayer').textContent = 'X';
            document.getElementById('gameStatus').textContent = 'در جریان...';
            
            // اگر تایمر قبلی هست، پاک کن
            if (aiTimeout) {
                clearTimeout(aiTimeout);
            }
        }

        // نمایش منوی انتخاب حالت بازی
        function showGameMode() {
            document.getElementById('mainMenu').classList.add('hidden');
            document.getElementById('gameModeMenu').classList.remove('hidden');
            document.getElementById('settingsMenu').classList.add('hidden');
            document.getElementById('gameBoard').classList.add('hidden');
        }

        // نمایش تنظیمات
        function showSettings() {
            document.getElementById('mainMenu').classList.add('hidden');
            document.getElementById('gameModeMenu').classList.add('hidden');
            document.getElementById('settingsMenu').classList.remove('hidden');
            document.getElementById('gameBoard').classList.add('hidden');
        }

        // بازگشت به منوی اصلی
        function backToMain() {
            document.getElementById('mainMenu').classList.remove('hidden');
            document.getElementById('gameModeMenu').classList.add('hidden');
            document.getElementById('settingsMenu').classList.add('hidden');
            document.getElementById('gameBoard').classList.add('hidden');
            
            // پاک کردن تایمر ربات اگر وجود دارد
            if (aiTimeout) {
                clearTimeout(aiTimeout);
            }
        }

        // تغییر تم
        function changeTheme(theme) {
            document.body.className = '';
            document.body.classList.add(`theme-${theme}`);
        }

        // مقداردهی اولیه
        createBoard();
    </script>
</body>
</html>
