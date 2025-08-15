# Apple-Match-only-for-Ashley
Creating an interesting game only for my love, Ashley. Hope her happy everyday!
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>苹果消消乐 - Apple Match</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
            overflow: hidden;
            height: 100vh;
            user-select: none;
        }

        .container {
            width: 100vw;
            height: 100vh;
            position: relative;
            overflow: hidden;
        }

        .screen {
            position: absolute;
            width: 100%;
            height: 100%;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .screen.active {
            display: flex;
        }

        .title {
            font-size: clamp(2rem, 8vw, 4rem);
            color: #ff6b6b;
            text-shadow: 3px 3px 6px rgba(0,0,0,0.3);
            margin-bottom: 2rem;
            animation: bounce 2s infinite;
            text-align: center;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }

        .btn {
            background: linear-gradient(45deg, #ff6b6b, #ffa726);
            color: white;
            border: none;
            padding: 1rem 2rem;
            margin: 0.5rem;
            border-radius: 25px;
            font-size: clamp(1rem, 4vw, 1.2rem);
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
            font-weight: bold;
            min-width: 200px;
            max-width: 90vw;
            text-align: center;
        }

        .btn:hover, .btn:active {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.3);
        }

        .level-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 1rem;
            padding: 1rem;
            max-width: 800px;
            width: 100%;
            max-height: 60vh;
            overflow-y: auto;
        }

        .level-btn {
            aspect-ratio: 1;
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
            color: white;
            border: none;
            border-radius: 15px;
            font-size: clamp(0.8rem, 3vw, 1rem);
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .level-btn:hover, .level-btn:active {
            transform: scale(1.05);
        }

        .game-container {
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .game-header {
            width: 100%;
            max-width: 500px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            padding: 0 1rem;
            flex-wrap: wrap;
            gap: 10px;
        }

        .game-info {
            background: rgba(255,255,255,0.9);
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-weight: bold;
            color: #333;
            font-size: clamp(0.8rem, 3vw, 1rem);
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .game-board {
            width: min(90vw, 400px);
            height: min(90vw, 400px);
            background: rgba(255,255,255,0.95);
            border-radius: 20px;
            padding: 10px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            position: relative;
            overflow: hidden;
        }

        .grid {
            width: 100%;
            height: 100%;
            display: grid;
            grid-template-columns: repeat(8, 1fr);
            grid-template-rows: repeat(8, 1fr);
            gap: 2px;
        }

        .cell {
            background: #f0f0f0;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .cell:hover, .cell:active {
            transform: scale(1.05);
        }

        .cell.selected {
            box-shadow: 0 0 0 3px #ff6b6b;
            animation: pulse 0.5s infinite alternate;
        }

        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.1); }
        }

        .fruit {
            width: 85%;
            height: 85%;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(1rem, 3vw, 1.5rem);
            font-weight: bold;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .apple { background: linear-gradient(45deg, #ff4757, #ff3742); }
        .orange { background: linear-gradient(45deg, #ffa726, #ff9800); }
        .banana { background: linear-gradient(45deg, #ffeb3b, #fdd835); }
        .grape { background: linear-gradient(45deg, #9c27b0, #7b1fa2); }
        .strawberry { background: linear-gradient(45deg, #e91e63, #c2185b); }
        .lemon { background: linear-gradient(45deg, #cddc39, #afb42b); }

        .special-fruit {
            position: relative;
            animation: sparkle 2s infinite;
        }

        @keyframes sparkle {
            0%, 100% { box-shadow: 0 0 10px rgba(255,215,0,0.5); }
            50% { box-shadow: 0 0 20px rgba(255,215,0,0.8); }
        }

        .game-controls {
            display: flex;
            gap: 1rem;
            margin-top: 1rem;
            flex-wrap: wrap;
            justify-content: center;
        }

        .control-btn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 0.8rem 1.5rem;
            border-radius: 20px;
            font-size: clamp(0.8rem, 3vw, 1rem);
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
            font-weight: bold;
        }

        .control-btn:hover, .control-btn:active {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.3);
        }

        .power-ups {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin: 1rem 0;
            flex-wrap: wrap;
        }

        .power-up {
            width: clamp(40px, 8vw, 50px);
            height: clamp(40px, 8vw, 50px);
            border-radius: 50%;
            border: 3px solid #fff;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: white;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            font-size: clamp(0.8rem, 3vw, 1rem);
        }

        .power-up:hover, .power-up:active {
            transform: scale(1.1);
        }

        .power-up.active {
            box-shadow: 0 0 0 3px #ffff00;
        }

        .bomb { background: linear-gradient(45deg, #ff5722, #d84315); }
        .rainbow { background: linear-gradient(45deg, #e91e63, #9c27b0, #3f51b5, #2196f3, #4caf50, #ffeb3b, #ff9800); }
        .hammer { background: linear-gradient(45deg, #795548, #5d4037); }
        .swap { background: linear-gradient(45deg, #607d8b, #455a64); }

        .progress-bar {
            width: 100%;
            max-width: 400px;
            height: 20px;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            margin: 1rem 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(45deg, #4caf50, #8bc34a);
            transition: width 0.5s ease;
            border-radius: 10px;
        }

        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: white;
            padding: 2rem;
            border-radius: 20px;
            text-align: center;
            max-width: 90vw;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal h2 {
            color: #333;
            margin-bottom: 1rem;
            font-size: clamp(1.2rem, 5vw, 1.8rem);
        }

        .modal p {
            color: #666;
            margin-bottom: 1rem;
            line-height: 1.5;
        }

        .combo-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: clamp(1.5rem, 6vw, 2rem);
            font-weight: bold;
            color: #ff6b6b;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            animation: comboShow 1s ease-out forwards;
            pointer-events: none;
            z-index: 100;
        }

        @keyframes comboShow {
            0% {
                transform: translate(-50%, -50%) scale(0);
                opacity: 1;
            }
            50% {
                transform: translate(-50%, -50%) scale(1.2);
            }
            100% {
                transform: translate(-50%, -50%) scale(1);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 主菜单 -->
        <div id="mainMenu" class="screen active">
            <h1 class="title">🍎 苹果消消乐</h1>
            <button class="btn" onclick="showLevelSelect()">开始冒险</button>
            <button class="btn" onclick="showPractice()">练习场</button>
            <button class="btn" onclick="showInstructions()">游戏说明</button>
        </div>

        <!-- 关卡选择 -->
        <div id="levelSelect" class="screen">
            <h2 class="title">选择关卡</h2>
            <div class="level-grid">
                <button class="level-btn" onclick="selectLevel(1)">
                    <div>关卡 1</div>
                    <div>🍎 新手村</div>
                </button>
                <button class="level-btn" onclick="selectLevel(2)">
                    <div>关卡 2</div>
                    <div>🍊 果园探险</div>
                </button>
                <button class="level-btn" onclick="selectLevel(3)">
                    <div>关卡 3</div>
                    <div>🍌 香蕉天堂</div>
                </button>
                <button class="level-btn" onclick="selectLevel(4)">
                    <div>关卡 4</div>
                    <div>🍇 紫色迷境</div>
                </button>
                <button class="level-btn" onclick="selectLevel(5)">
                    <div>关卡 5</div>
                    <div>🍓 草莓乐园</div>
                </button>
                <button class="level-btn" onclick="selectLevel(6)">
                    <div>关卡 6</div>
                    <div>🍋 柠檬挑战</div>
                </button>
            </div>
            <button class="btn" onclick="showMainMenu()">返回主菜单</button>
        </div>

        <!-- 关卡确认 -->
        <div id="levelConfirm" class="screen">
            <h2 class="title" id="levelTitle">关卡 1 - 新手村</h2>
            <div class="modal-content">
                <p id="levelDescription">这是一个适合新手的简单关卡，来熟悉游戏操作吧！</p>
                <div>
                    <button class="btn" onclick="startGame()">开始游戏</button>
                    <button class="btn" onclick="showLevelSelect()">返回选择</button>
                </div>
            </div>
        </div>

        <!-- 练习场 -->
        <div id="practice" class="screen">
            <div class="game-container">
                <div class="game-header">
                    <div class="game-info">生命: <span id="practiceLives">500</span></div>
                    <div class="game-info">得分: <span id="practiceScore">0</span></div>
                    <div class="game-info">练习模式</div>
                </div>
                <div class="game-board">
                    <div id="practiceGrid" class="grid"></div>
                </div>
                <div class="power-ups">
                    <div class="power-up bomb" onclick="usePowerUp('bomb')" title="炸弹">💣</div>
                    <div class="power-up rainbow" onclick="usePowerUp('rainbow')" title="彩虹球">🌈</div>
                    <div class="power-up hammer" onclick="usePowerUp('hammer')" title="锤子">🔨</div>
                    <div class="power-up swap" onclick="usePowerUp('swap')" title="交换">🔄</div>
                </div>
                <div class="game-controls">
                    <button class="control-btn" onclick="pauseGame()">暂停</button>
                    <button class="control-btn" onclick="resetPractice()">重置</button>
                    <button class="control-btn" onclick="showMainMenu()">返回主菜单</button>
                </div>
            </div>
        </div>

        <!-- 游戏界面 -->
        <div id="gameScreen" class="screen">
            <div class="game-container">
                <div class="game-header">
                    <div class="game-info">生命: <span id="lives">500</span></div>
                    <div class="game-info">得分: <span id="score">0</span></div>
                    <div class="game-info">目标: <span id="target">1000</span></div>
                </div>
                <div class="progress-bar">
                    <div id="progressFill" class="progress-fill" style="width: 0%"></div>
                </div>
                <div class="game-board">
                    <div id="gameGrid" class="grid"></div>
                </div>
                <div class="power-ups">
                    <div class="power-up bomb" onclick="usePowerUp('bomb')" title="炸弹">💣</div>
                    <div class="power-up rainbow" onclick="usePowerUp('rainbow')" title="彩虹球">🌈</div>
                    <div class="power-up hammer" onclick="usePowerUp('hammer')" title="锤子">🔨</div>
                    <div class="power-up swap" onclick="usePowerUp('swap')" title="交换">🔄</div>
                </div>
                <div class="game-controls">
                    <button class="control-btn" onclick="pauseGame()">暂停</button>
                    <button class="control-btn" onclick="showLevelSelect()">选择关卡</button>
                    <button class="control-btn" onclick="showMainMenu()">返回主菜单</button>
                </div>
            </div>
        </div>
    </div>

    <!-- 模态框 -->
    <div id="modal" class="modal">
        <div class="modal-content">
            <h2 id="modalTitle"></h2>
            <p id="modalText"></p>
            <button class="btn" id="modalBtn" onclick="closeModal()">确定</button>
        </div>
    </div>

    <!-- 游戏说明模态框 -->
    <div id="instructionsModal" class="modal">
        <div class="modal-content">
            <h2>游戏说明</h2>
            <p><strong>基本玩法：</strong></p>
            <p>• 点击相邻的两个水果交换位置</p>
            <p>• 形成3个或更多相同水果的连线即可消除</p>
            <p>• 消除水果获得分数，达到目标分数即可过关</p>
            <br>
            <p><strong>特殊道具：</strong></p>
            <p>💣 炸弹：消除3x3区域内的所有水果</p>
            <p>🌈 彩虹球：消除场上所有同色水果</p>
            <p>🔨 锤子：直接消除选中的单个水果</p>
            <p>🔄 交换：强制交换两个不相邻的水果</p>
            <button class="btn" onclick="closeInstructions()">开始游戏</button>
        </div>
    </div>
    <script>
        // 全局游戏变量
        let game = null;
        let currentLevel = 1;
        let gameMode = 'normal';

        // 关卡配置
        const levelConfig = {
            1: { target: 1000, description: "这是一个适合新手的简单关卡，来熟悉游戏操作吧！", name: "新手村" },
            2: { target: 1500, description: "果园探险开始了，需要更多的消除技巧！", name: "果园探险" },
            3: { target: 2000, description: "香蕉天堂等你来挑战，目标分数更高了！", name: "香蕉天堂" },
            4: { target: 2500, description: "紫色迷境充满神秘，准备好接受挑战了吗？", name: "紫色迷境" },
            5: { target: 3000, description: "草莓乐园的甜蜜挑战，你能完成吗？", name: "草莓乐园" },
            6: { target: 4000, description: "柠檬挑战是最终考验，证明你的实力吧！", name: "柠檬挑战" }
        };

        // 音效函数
        function playSound(frequency, duration) {
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                oscillator.frequency.setValueAtTime(frequency, audioContext.currentTime);
                gainNode.gain.setValueAtTime(0.1, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + duration);
                
                oscillator.start(audioContext.currentTime);
                oscillator.stop(audioContext.currentTime + duration);
            } catch (e) {
                console.log('音频播放失败');
            }
        }

        // 游戏类
        class AppleMatchGame {
            constructor() {
                this.gridSize = 8;
                this.grid = [];
                this.score = 0;
                this.lives = 500;
                this.target = 1000;
                this.selectedCell = null;
                this.fruits = ['apple', 'orange', 'banana', 'grape', 'strawberry', 'lemon'];
                this.fruitEmojis = {
                    'apple': '🍎',
                    'orange': '🍊', 
                    'banana': '🍌',
                    'grape': '🍇',
                    'strawberry': '🍓',
                    'lemon': '🍋'
                };
                this.isPaused = false;
                this.activePowerUp = null;
                this.combo = 0;
                this.isAnimating = false;
                this.currentGridId = 'gameGrid';
            }

            init() {
                this.initGrid();
                this.generateNewFruits();
                this.render();
                this.updateUI();
            }

            initGrid() {
                this.grid = [];
                for (let i = 0; i < this.gridSize; i++) {
                    this.grid[i] = [];
                    for (let j = 0; j < this.gridSize; j++) {
                        this.grid[i][j] = {
                            fruit: null,
                            special: false
                        };
                    }
                }
            }

            generateNewFruits() {
                for (let i = 0; i < this.gridSize; i++) {
                    for (let j = 0; j < this.gridSize; j++) {
                        if (!this.grid[i][j].fruit) {
                            let newFruit;
                            let attempts = 0;
                            do {
                                newFruit = this.fruits[Math.floor(Math.random() * this.fruits.length)];
                                attempts++;
                            } while (this.wouldCreateMatch(i, j, newFruit) && attempts < 10);
                            
                            this.grid[i][j].fruit = newFruit;
                            this.grid[i][j].special = Math.random() < 0.05;
                        }
                    }
                }
            }

            wouldCreateMatch(row, col, fruit) {
                let horizontalCount = 1;
                for (let i = col - 1; i >= 0 && this.grid[row] && this.grid[row][i] && this.grid[row][i].fruit === fruit; i--) {
                    horizontalCount++;
                }
                for (let i = col + 1; i < this.gridSize && this.grid[row] && this.grid[row][i] && this.grid[row][i].fruit === fruit; i++) {
                    horizontalCount++;
                }
                
                let verticalCount = 1;
                for (let i = row - 1; i >= 0 && this.grid[i] && this.grid[i][col] && this.grid[i][col].fruit === fruit; i--) {
                    verticalCount++;
                }
                for (let i = row + 1; i < this.gridSize && this.grid[i] && this.grid[i][col] && this.grid[i][col].fruit === fruit; i++) {
                    verticalCount++;
                }
                
                return horizontalCount >= 3 || verticalCount >= 3;
            }

            render() {
                const gridElement = document.getElementById(this.currentGridId);
                if (!gridElement) return;
                
                gridElement.innerHTML = '';
                
                for (let i = 0; i < this.gridSize; i++) {
                    for (let j = 0; j < this.gridSize; j++) {
                        const cell = document.createElement('div');
                        cell.className = 'cell';
                        cell.dataset.row = i;
                        cell.dataset.col = j;
                        
                        if (this.grid[i][j].fruit) {
                            const fruit = document.createElement('div');
                            fruit.className = `fruit ${this.grid[i][j].fruit}`;
                            if (this.grid[i][j].special) {
                                fruit.classList.add('special-fruit');
                            }
                            fruit.textContent = this.fruitEmojis[this.grid[i][j].fruit];
                            cell.appendChild(fruit);
                        }
                        
                        cell.addEventListener('click', (e) => this.handleCellClick(e));
                        gridElement.appendChild(cell);
                    }
                }
                this.updateCellDisplay();
            }

            handleCellClick(e) {
                if (this.isPaused || this.isAnimating) return;
                
                const cell = e.currentTarget;
                const row = parseInt(cell.dataset.row);
                const col = parseInt(cell.dataset.col);
                
                if (this.activePowerUp) {
                    this.handlePowerUpClick(row, col);
                    return;
                }
                
                if (this.selectedCell) {
                    if (this.selectedCell.row === row && this.selectedCell.col === col) {
                        this.clearSelection();
                    } else if (this.isAdjacent(this.selectedCell, {row, col})) {
                        this.swapFruits(this.selectedCell, {row, col});
                    } else {
                        this.clearSelection();
                        this.selectCell(row, col);
                    }
                } else {
                    this.selectCell(row, col);
                }
            }

            handlePowerUpClick(row, col) {
                if (this.activePowerUp === 'bomb') {
                    this.useBomb(row, col);
                } else if (this.activePowerUp === 'rainbow') {
                    this.useRainbow(row, col);
                } else if (this.activePowerUp === 'hammer') {
                    this.useHammer(row, col);
                } else if (this.activePowerUp === 'swap') {
                    if (!this.selectedCell) {
                        this.selectCell(row, col);
                    } else {
                        this.forceSwap(this.selectedCell, {row, col});
                    }
                }
            }

            useBomb(row, col) {
                playSound(400, 0.3);
                for (let i = Math.max(0, row - 1); i <= Math.min(this.gridSize - 1, row + 1); i++) {
                    for (let j = Math.max(0, col - 1); j <= Math.min(this.gridSize - 1, col + 1); j++) {
                        this.grid[i][j].fruit = null;
                        this.grid[i][j].special = false;
                    }
                }
                this.score += 200;
                this.activePowerUp = null;
                this.updatePowerUpButtons();
                this.processAfterAction();
            }

            useRainbow(row, col) {
                if (this.grid[row][col].fruit) {
                    const targetFruit = this.grid[row][col].fruit;
                    let count = 0;
                    for (let i = 0; i < this.gridSize; i++) {
                        for (let j = 0; j < this.gridSize; j++) {
                            if (this.grid[i][j].fruit === targetFruit) {
                                this.grid[i][j].fruit = null;
                                this.grid[i][j].special = false;
                                count++;
                            }
                        }
                    }
                    this.score += count * 50;
                    playSound(600, 0.4);
                }
                this.activePowerUp = null;
                this.updatePowerUpButtons();
                this.processAfterAction();
            }

            useHammer(row, col) {
                if (this.grid[row][col].fruit) {
                    this.grid[row][col].fruit = null;
                    this.grid[row][col].special = false;
                    this.score += 50;
                    playSound(500, 0.2);
                }
                this.activePowerUp = null;
                this.updatePowerUpButtons();
                this.processAfterAction();
            }

            forceSwap(cell1, cell2) {
                const temp = {...this.grid[cell1.row][cell1.col]};
                this.grid[cell1.row][cell1.col] = {...this.grid[cell2.row][cell2.col]};
                this.grid[cell2.row][cell2.col] = temp;
                
                this.activePowerUp = null;
                this.clearSelection();
                this.updatePowerUpButtons();
                this.processAfterAction();
                playSound(450, 0.2);
            }

            selectCell(row, col) {
                if (!this.grid[row][col].fruit) return;
                this.selectedCell = {row, col};
                this.updateCellDisplay();
            }

            clearSelection() {
                this.selectedCell = null;
                this.updateCellDisplay();
            }

            updateCellDisplay() {
                const cells = document.querySelectorAll(`#${this.currentGridId} .cell`);
                cells.forEach(cell => cell.classList.remove('selected'));
                
                if (this.selectedCell) {
                    const selectedElement = document.querySelector(`#${this.currentGridId} .cell[data-row="${this.selectedCell.row}"][data-col="${this.selectedCell.col}"]`);
                    if (selectedElement) {
                        selectedElement.classList.add('selected');
                    }
                }
            }

            isAdjacent(cell1, cell2) {
                const rowDiff = Math.abs(cell1.row - cell2.row);
                const colDiff = Math.abs(cell1.col - cell2.col);
                return (rowDiff === 1 && colDiff === 0) || (rowDiff === 0 && colDiff === 1);
            }

            swapFruits(cell1, cell2) {
                const temp = {...this.grid[cell1.row][cell1.col]};
                this.grid[cell1.row][cell1.col] = {...this.grid[cell2.row][cell2.col]};
                this.grid[cell2.row][cell2.col] = temp;
                
                this.render();
                
                setTimeout(() => {
                    if (this.checkAndRemoveMatches()) {
                        this.processMatches();
                    } else {
                        const temp = {...this.grid[cell1.row][cell1.col]};
                        this.grid[cell1.row][cell1.col] = {...this.grid[cell2.row][cell2.col]};
                        this.grid[cell2.row][cell2.col] = temp;
                        this.render();
                    }
                    this.clearSelection();
                }, 100);
            }

            checkAndRemoveMatches() {
                const matches = this.findMatches();
                if (matches.length > 0) {
                    this.removeMatches(matches);
                    return true;
                }
                return false;
            }

            findMatches() {
                const matches = [];
                
                // 检查水平匹配
                for (let i = 0; i < this.gridSize; i++) {
                    let count = 1;
                    let currentFruit = this.grid[i][0].fruit;
                    
                    for (let j = 1; j < this.gridSize; j++) {
                        if (this.grid[i][j].fruit === currentFruit && currentFruit) {
                            count++;
                        } else {
                            if (count >= 3 && currentFruit) {
                                for (let k = j - count; k < j; k++) {
                                    matches.push({row: i, col: k});
                                }
                            }
                            currentFruit = this.grid[i][j].fruit;
                            count = 1;
                        }
                    }
                    if (count >= 3 && currentFruit) {
                        for (let k = this.gridSize - count; k < this.gridSize; k++) {
                            matches.push({row: i, col: k});
                        }
                    }
                }
                
                // 检查垂直匹配
                for (let j = 0; j < this.gridSize; j++) {
                    let count = 1;
                    let currentFruit = this.grid[0][j].fruit;
                    
                    for (let i = 1; i < this.gridSize; i++) {
                        if (this.grid[i][j].fruit === currentFruit && currentFruit) {
                            count++;
                        } else {
                            if (count >= 3 && currentFruit) {
                                for (let k = i - count; k < i; k++) {
                                    matches.push({row: k, col: j});
                                }
                            }
                            currentFruit = this.grid[i][j].fruit;
                            count = 1;
                        }
                    }
                    if (count >= 3 && currentFruit) {
                        for (let k = this.gridSize - count; k < this.gridSize; k++) {
                            matches.push({row: k, col: j});
                        }
                    }
                }
                
                return matches;
            }

            removeMatches(matches) {
                let points = 0;
                matches.forEach(match => {
                    if (this.grid[match.row][match.col].fruit) {
                        points += this.grid[match.row][match.col].special ? 100 : 50;
                        this.grid[match.row][match.col].fruit = null;
                        this.grid[match.row][match.col].special = false;
                    }
                });
                
                this.combo++;
                const comboBonus = this.combo > 1 ? this.combo * 10 : 0;
                this.score += points + comboBonus;
                
                if (this.combo > 1) {
                    this.showComboText(`连击 x${this.combo}!`);
                    playSound(800 + this.combo * 100, 0.15);
                } else {
                    playSound(700, 0.1);
                }
                
                this.updateUI();
            }

            processMatches() {
                this.dropFruits();
                setTimeout(() => {
                    this.generateNewFruits();
                    this.render();
                    
                    setTimeout(() => {
                        if (this.checkAndRemoveMatches()) {
                            this.processMatches();
                        } else {
                            this.combo = 0;
                            this.checkGameStatus();
                        }
                    }, 200);
                }, 300);
            }

            processAfterAction() {
                this.dropFruits();
                setTimeout(() => {
                    this.generateNewFruits();
                    this.render();
                    
                    setTimeout(() => {
                        if (this.checkAndRemoveMatches()) {
                            this.processMatches();
                        } else {
                            this.combo = 0;
                            this.checkGameStatus();
                        }
                    }, 200);
                }, 300);
            }

            dropFruits() {
                for (let j = 0; j < this.gridSize; j++) {
                    for (let i = this.gridSize - 1; i >= 0; i--) {
                        if (!this.grid[i][j].fruit) {
                            for (let k = i - 1; k >= 0; k--) {
                                if (this.grid[k][j].fruit) {
                                    this.grid[i][j] = {...this.grid[k][j]};
                                    this.grid[k][j].fruit = null;
                                    this.grid[k][j].special = false;
                                    break;
                                }
                            }
                        }
                    }
                }
            }

            showComboText(text) {
                const gameBoard = document.querySelector('.game-board');
                const comboElement = document.createElement('div');
                comboElement.className = 'combo-text';
                comboElement.textContent = text;
                gameBoard.appendChild(comboElement);
                
                setTimeout(() => {
                    if (comboElement.parentNode) {
                        comboElement.parentNode.removeChild(comboElement);
                    }
                }, 1000);
            }

            updateUI() {
                if (gameMode === 'practice') {
                    document.getElementById('practiceScore').textContent = this.score;
                    document.getElementById('practiceLives').textContent = this.lives;
                } else {
                    document.getElementById('score').textContent = this.score;
                    document.getElementById('lives').textContent = this.lives;
                    document.getElementById('target').textContent = this.target;
                    
                    const progress = Math.min((this.score / this.target) * 100, 100);
                    document.getElementById('progressFill').style.width = `${progress}%`;
                }
            }

            checkGameStatus() {
                if (gameMode === 'normal' && this.score >= this.target) {
                    playSound(1200, 0.5);
                    showModal('恭喜过关！', `你已经达到目标分数！得分：${this.score}`, () => {
                        showLevelSelect();
                    });
                }
            }

            updatePowerUpButtons() {
                document.querySelectorAll('.power-up').forEach(btn => {
                    btn.classList.remove('active');
                });
            }
        }

        // 界面切换函数
        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            document.getElementById(screenId).classList.add('active');
        }

        function showMainMenu() {
            showScreen('mainMenu');
        }

        function showLevelSelect() {
            showScreen('levelSelect');
        }

        function showPractice() {
            gameMode = 'practice';
            game = new AppleMatchGame();
            game.currentGridId = 'practiceGrid';
            game.score = 0;
            game.lives = 500;
            game.init();
            showScreen('practice');
        }

        function selectLevel(level) {
            currentLevel = level;
            const config = levelConfig[level];
            document.getElementById('levelTitle').textContent = `关卡 ${level} - ${config.name}`;
            document.getElementById('levelDescription').textContent = config.description;
            showScreen('levelConfirm');
        }

        function startGame() {
            gameMode = 'normal';
            game = new AppleMatchGame();
            game.currentGridId = 'gameGrid';
            game.target = levelConfig[currentLevel].target;
            game.score = 0;
            game.lives = 500;
            game.init();
            showScreen('gameScreen');
        }

        function showInstructions() {
            document.getElementById('instructionsModal').classList.add('active');
        }

        function closeInstructions() {
            document.getElementById('instructionsModal').classList.remove('active');
        }

        // 道具使用函数
        function usePowerUp(type) {
            if (!game) return;
            
            document.querySelectorAll('.power-up').forEach(btn => {
                btn.classList.remove('active');
            });
            
            if (game.activePowerUp === type) {
                game.activePowerUp = null;
            } else {
                game.activePowerUp = type;
                document.querySelector(`.power-up.${type}`).classList.add('active');
            }
        }

        // 游戏控制函数
        function pauseGame() {
            if (!game) return;
            
            game.isPaused = !game.isPaused;
            const btn = event.target;
            btn.textContent = game.isPaused ? '继续' : '暂停';
            
            if (game.isPaused) {
                showModal('游戏暂停', '点击继续按钮恢复游戏', () => {
                    game.isPaused = false;
                    btn.textContent = '暂停';
                });
            }
        }

        function resetPractice() {
            if (gameMode === 'practice') {
                showPractice();
            }
        }

        // 模态框函数
        function showModal(title, text, callback) {
            document.getElementById('modalTitle').textContent = title;
            document.getElementById('modalText').textContent = text;
            document.getElementById('modal').classList.add('active');
            
            document.getElementById('modalBtn').onclick = () => {
                closeModal();
                if (callback) callback();
            };
        }

        function closeModal() {
            document.getElementById('modal').classList.remove('active');
        }

        // 初始化
        document.addEventListener('DOMContentLoaded', function() {
            console.log('苹果消消乐游戏已加载');
        });

        // 触摸事件优化
        document.addEventListener('touchstart', function(e) {
            e.preventDefault();
        }, { passive: false });

        document.addEventListener('touchmove', function(e) {
            e.preventDefault();
        }, { passive: false });
    </script>
</body>
</html>
