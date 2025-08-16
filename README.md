# Apple-Match-only-for-Ashley
Creating an interesting game only for my love, Ashley. Hope her happy everyday!
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>苹果消消乐 - 献给最爱的Ashley</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            overflow-x: hidden;
            user-select: none;
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
        }

        .container {
            width: 100vw;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            position: relative;
        }

        /* 爱心动画背景 */
        .hearts-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .heart {
            position: absolute;
            color: rgba(255, 182, 193, 0.6);
            font-size: 20px;
            animation: floatHeart 6s infinite linear;
        }

        @keyframes floatHeart {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
        }

        /* 主菜单 */
        .main-menu {
            text-align: center;
            z-index: 10;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 2rem;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            max-width: 90vw;
        }

        .game-title {
            font-size: clamp(1.5rem, 5vw, 3rem);
            background: linear-gradient(45deg, #ff6b6b, #ee5a52, #ff8a80);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .subtitle {
            font-size: clamp(0.8rem, 3vw, 1.2rem);
            color: #666;
            margin-bottom: 2rem;
            font-style: italic;
        }

        .menu-button {
            display: block;
            width: 100%;
            max-width: 280px;
            margin: 0.8rem auto;
            padding: 1rem 2rem;
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            color: white;
            border: none;
            border-radius: 25px;
            font-size: clamp(0.9rem, 3vw, 1.1rem);
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        .menu-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
        }

        .menu-button:active {
            transform: translateY(0);
        }

        /* 关卡选择界面 */
        .level-select {
            display: none;
            text-align: center;
            z-index: 10;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 1.5rem;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            max-width: 95vw;
            max-height: 90vh;
            overflow-y: auto;
        }

        .level-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 1rem;
            margin: 1.5rem 0;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        .level-button {
            aspect-ratio: 1;
            background: linear-gradient(45deg, #4CAF50, #45a049);
            color: white;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-size: clamp(0.8rem, 2.5vw, 1rem);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        .level-button:hover {
            transform: scale(1.05);
        }

        .level-button.special {
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
        }

        .level-button.practice {
            background: linear-gradient(45deg, #9c27b0, #673ab7);
        }

        .love-quote {
            font-style: italic;
            color: #666;
            font-size: clamp(0.7rem, 2vw, 0.9rem);
            margin-top: 0.5rem;
        }

        /* 游戏界面 */
        .game-screen {
            display: none;
            width: 100vw;
            height: 100vh;
            position: relative;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.5rem 1rem;
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(10px);
        }

        .score-info {
            font-size: clamp(0.8rem, 2.5vw, 1rem);
            font-weight: bold;
            color: #333;
        }

        .game-controls {
            display: flex;
            gap: 0.5rem;
        }

        .control-btn {
            padding: 0.5rem 1rem;
            background: rgba(255, 255, 255, 0.8);
            border: 1px solid #ddd;
            border-radius: 15px;
            cursor: pointer;
            font-size: clamp(0.7rem, 2vw, 0.9rem);
            transition: all 0.3s ease;
        }

        .control-btn:hover {
            background: rgba(255, 255, 255, 1);
            transform: scale(1.05);
        }

        .game-board {
            width: 100%;
            height: calc(100vh - 120px);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .grid-container {
            width: min(90vw, 90vh, 400px);
            height: min(90vw, 90vh, 400px);
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 10px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            position: relative;
        }

        .game-grid {
            width: 100%;
            height: 100%;
            display: grid;
            grid-template-columns: repeat(8, 1fr);
            grid-template-rows: repeat(8, 1fr);
            gap: 2px;
            background: #f0f0f0;
            border-radius: 10px;
            overflow: hidden;
        }

        .grid-cell {
            background: white;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            border-radius: 5px;
        }

        .grid-cell:hover {
            transform: scale(1.05);
            z-index: 5;
        }

        .grid-cell.selected {
            background: rgba(255, 107, 107, 0.3);
            box-shadow: inset 0 0 0 2px #ff6b6b;
        }

        .apple-icon {
            width: 80%;
            height: 80%;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(1rem, 3vw, 1.5rem);
            color: white;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
        }

        /* 苹果类型颜色 */
        .apple-red { background: linear-gradient(45deg, #ff4444, #cc3333); }
        .apple-green { background: linear-gradient(45deg, #44ff44, #33cc33); }
        .apple-yellow { background: linear-gradient(45deg, #ffff44, #cccc33); }
        .apple-blue { background: linear-gradient(45deg, #4444ff, #3333cc); }
        .apple-purple { background: linear-gradient(45deg, #ff44ff, #cc33cc); }
        .apple-orange { background: linear-gradient(45deg, #ff8844, #cc6633); }

        /* 特殊道具 */
        .special-item {
            background: linear-gradient(45deg, #ffd700, #ffed4e) !important;
            animation: glow 2s infinite;
            box-shadow: 0 0 10px rgba(255, 215, 0, 0.8);
        }

        @keyframes glow {
            0%, 100% { box-shadow: 0 0 10px rgba(255, 215, 0, 0.8); }
            50% { box-shadow: 0 0 20px rgba(255, 215, 0, 1); }
        }

        /* 道具栏 */
        .power-ups {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin: 1rem 0;
            flex-wrap: wrap;
        }

        .power-up {
            padding: 0.8rem;
            background: rgba(255, 255, 255, 0.9);
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            min-width: 60px;
            text-align: center;
            font-size: clamp(0.7rem, 2vw, 0.9rem);
        }

        .power-up:hover {
            transform: scale(1.1);
            border-color: #ff6b6b;
        }

        .power-up.active {
            background: #ff6b6b;
            color: white;
            border-color: #ee5a52;
        }

        /* 粒子效果 */
        .particle {
            position: absolute;
            pointer-events: none;
            border-radius: 50%;
            z-index: 1000;
        }

        @keyframes particle-float {
            0% {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
            100% {
                opacity: 0;
                transform: translateY(-100px) scale(0);
            }
        }

        /* 连击效果 */
        .combo-display {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 2rem;
            font-weight: bold;
            color: #ff6b6b;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
            z-index: 100;
            pointer-events: none;
            animation: combo-pop 1s ease-out;
        }

        @keyframes combo-pop {
            0% {
                transform: translate(-50%, -50%) scale(0);
                opacity: 0;
            }
            50% {
                transform: translate(-50%, -50%) scale(1.2);
                opacity: 1;
            }
            100% {
                transform: translate(-50%, -50%) scale(1);
                opacity: 0;
            }
        }

        /* 成就系统 */
        .achievement-popup {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            color: white;
            padding: 1rem;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            z-index: 1000;
            transform: translateX(400px);
            transition: transform 0.5s ease;
            max-width: 300px;
        }

        .achievement-popup.show {
            transform: translateX(0);
        }

        /* 暂停菜单 */
        .pause-menu {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }

        .pause-content {
            background: white;
            padding: 2rem;
            border-radius: 20px;
            text-align: center;
            max-width: 90vw;
        }

        /* 响应式设计 */
        @media (max-width: 480px) {
            .game-header {
                padding: 0.3rem 0.5rem;
            }
            
            .control-btn {
                padding: 0.3rem 0.6rem;
                font-size: 0.7rem;
            }
            
            .power-ups {
                gap: 0.5rem;
            }
            
            .power-up {
                padding: 0.5rem;
                min-width: 50px;
                font-size: 0.7rem;
            }
        }

        @media (max-height: 600px) {
            .game-board {
                padding: 0.5rem;
            }
            
            .grid-container {
                width: min(85vw, 85vh, 350px);
                height: min(85vw, 85vh, 350px);
            }
        }

        /* 特殊日期效果 */
        .special-date {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 999;
        }

        .firework {
            position: absolute;
            border-radius: 50%;
            animation: firework 2s ease-out infinite;
        }

        @keyframes firework {
            0% {
                transform: scale(0);
                opacity: 1;
            }
            100% {
                transform: scale(1);
                opacity: 0;
            }
        }

        /* 加载动画 */
        .loading {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            font-size: 1.5rem;
            color: white;
        }

        .loading::after {
            content: "";
            width: 20px;
            height: 20px;
            border: 2px solid white;
            border-top: 2px solid transparent;
            border-radius: 50%;
            margin-left: 10px;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .hidden {
            display: none !important;
        }

        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
    </style>
</head>
<body>
    <!-- 爱心背景动画 -->
    <div class="hearts-bg" id="heartsBackground"></div>
    
    <!-- 特殊日期效果 -->
    <div class="special-date" id="specialDateEffect"></div>

    <!-- 主菜单 -->
    <div class="container">
        <div class="main-menu" id="mainMenu">
            <h1 class="game-title">🍎 苹果消消乐 🍎</h1>
            <p class="subtitle">献给最爱的Ashley ❤️</p>
            <button class="menu-button" onclick="showLevelSelect()">🎮 开始冒险</button>
            <button class="menu-button" onclick="showAchievements()">🏆 成就系统</button>
            <button class="menu-button" onclick="showSettings()">⚙️ 游戏设置</button>
            <button class="menu-button" onclick="showLoveMessages()">💝 专属情话</button>
        </div>
    </div>

    <!-- 关卡选择 -->
    <div class="level-select" id="levelSelect">
        <h2 style="color: #ff6b6b; margin-bottom: 1rem;">选择关卡</h2>
        <div class="level-grid" id="levelGrid"></div>
        <button class="menu-button" onclick="showMainMenu()" style="max-width: 200px; margin-top: 1rem;">返回主菜单</button>
    </div>

    <!-- 游戏界面 -->
    <div class="game-screen" id="gameScreen">
        <div class="game-header">
            <div class="score-info">
                <div>关卡: <span id="currentLevel">1</span></div>
                <div>分数: <span id="score">0</span></div>
                <div>目标: <span id="target">1000</span></div>
                <div>步数: <span id="moves">30</span></div>
            </div>
            <div class="game-controls">
                <button class="control-btn" onclick="pauseGame()">⏸️ 暂停</button>
                <button class="control-btn" onclick="showHint()">💡 提示</button>
                <button class="control-btn" onclick="restartLevel()">🔄 重开</button>
                <button class="control-btn" onclick="backToLevelSelect()">🏠 返回</button>
            </div>
        </div>
        
        <div class="game-board">
            <div class="power-ups" id="powerUps">
                <div class="power-up" data-power="bomb" title="炸弹 - 消除3x3范围">💣<br>×<span class="count">3</span></div>
                <div class="power-up" data-power="lightning" title="闪电 - 消除整行">⚡<br>×<span class="count">3</span></div>
                <div class="power-up" data-power="rainbow" title="彩虹 - 消除所有同色">🌈<br>×<span class="count">2</span></div>
                <div class="power-up" data-power="hammer" title="锤子 - 消除单个">🔨<br>×<span class="count">5</span></div>
                <div class="power-up" data-power="shuffle" title="重排 - 打乱棋盘">🔀<br>×<span class="count">2</span></div>
                <div class="power-up" data-power="time" title="时光 - 增加5步">⏰<br>×<span class="count">2</span></div>
            </div>
            
            <div class="grid-container">
                <div class="game-grid" id="gameGrid"></div>
            </div>
        </div>
    </div>

    <!-- 暂停菜单 -->
    <div class="pause-menu" id="pauseMenu">
        <div class="pause-content">
            <h3 style="color: #ff6b6b; margin-bottom: 1rem;">游戏暂停</h3>
            <button class="menu-button" onclick="resumeGame()">继续游戏</button>
            <button class="menu-button" onclick="restartLevel()">重新开始</button>
            <button class="menu-button" onclick="backToLevelSelect()">返回关卡</button>
            <button class="menu-button" onclick="backToMainMenu()">主菜单</button>
        </div>
    </div>

    <!-- 成就弹窗 -->
    <div class="achievement-popup" id="achievementPopup">
        <h4>🎉 成就解锁!</h4>
        <p id="achievementText"></p>
    </div>

    <!-- 音频元素 -->
    <audio id="matchSound" preload="auto">
        <source src="data:audio/wav;base64,UklGRnoGAABXQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YQoGAACBhYqFbF1fdJivrJBhNjVgodDbq2EcBj+a2/LDciUFLIHO8tiJNwgZaLvt559NEAxQp+PwtmMcBjiR1/LMeSwFJHfH8N2QQAoUXrTp66hVFApGn+DyvmwhCTul4PjJfzEIHm+98+WUQQ4PXsb42f1sHg0qeNj+w7nE" type="audio/wav">
    </audio>
    <audio id="comboSound" preload="auto">
        <source src="data:audio/wav;base64,UklGRnoGAABXQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YQoGAACBhYqFbF1fdJivrJBhNjVgodDbq2EcBj+a2/LDciUFLIHO8tiJNwgZaLvt559NEAxQp+PwtmMcBjiR1/LMeSwFJHfH8N2QQAoUXrTp66hVFApGn+DyvmwhCTul4PjJfzEIHm+98+WUQQ4PXsb42f1sHg0qeNj+w7nE" type="audio/wav">
    </audio>

<script>
// 继续下一部分的JavaScript代码...
// 游戏状态管理
class GameState {
    constructor() {
        this.currentLevel = 1;
        this.score = 0;
        this.moves = 30;
        this.target = 1000;
        this.combo = 0;
        this.selectedCell = null;
        this.grid = [];
        this.powerUps = {
            bomb: 3,
            lightning: 3,
            rainbow: 2,
            hammer: 5,
            shuffle: 2,
            time: 2
        };
        this.activePowerUp = null;
        this.achievements = new Set();
        this.isPaused = false;
        this.isGameActive = false;
        this.totalMatches = 0;
        this.maxCombo = 0;
        this.totalScore = 0;
        this.gamesPlayed = 0;
        this.perfectGames = 0;
        this.initializeAudio();
    }

    initializeAudio() {
        this.sounds = {
            match: new Audio('data:audio/wav;base64,UklGRnoGAABXQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YQoGAACBhYqFbF1fdJivrJBhNjVgodDbq2EcBj+a2/LDciUFLIHO8tiJNwgZaLvt559NEAxQp+PwtmMcBjiR1/LMeSwFJHfH8N2QQAoUXrTp66hVFApGn+DyvmwhCTul4PjJfzEIHm+98+WUQQ4PXsb42f1sHg0qeNj+w7nE'),
            combo: new Audio('data:audio/wav;base64,UklGRnoGAABXQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YQoGAACBhYqFbF1fdJivrJBhNjVgodDbq2EcBj+a2/LDciUFLIHO8tiJNwgZaLvt559NEAxQp+PwtmMcBjiR1/LMeSwFJHfH8N2QQAoUXrTp66hVFApGn+DyvmwhCTul4PjJfzEIHm+98+WUQQ4PXsb42f1sHg0qeNj+w7nE'),
            powerUp: new Audio('data:audio/wav;base64,UklGRnoGAABXQVZFZm10IBAAAAABAAEAQB8AAEAfAAABAAgAZGF0YQoGAACBhYqFbF1fdJivrJBhNjVgodDbq2EcBj+a2/LDciUFLIHO8tiJNwgZaLvt559NEAxQp+PwtmMcBjiR1/LMeSwFJHfH8N2QQAoUXrTp66hVFApGn+DyvmwhCTul4PjJfzEIHm+98+WUQQ4PXsb42f1sHg0qeNj+w7nE')
        };
        
        // 设置音量
        Object.values(this.sounds).forEach(audio => {
            audio.volume = 0.3;
        });
    }

    playSound(type) {
        if (this.sounds[type]) {
            this.sounds[type].currentTime = 0;
            this.sounds[type].play().catch(() => {});
        }
    }
}

// 全局游戏状态
const gameState = new GameState();

// 关卡数据和情话
const LEVELS = [
    { id: 1, name: "初遇", target: 1000, moves: 25, quote: "就像第一次见到你，心跳不已 💕", special: false },
    { id: 2, name: "怦然心动", target: 1200, moves: 24, quote: "每一个眼神交汇，都是命运的安排 ✨", special: false },
    { id: 3, name: "甜蜜约会", target: 1500, moves: 23, quote: "和你在一起的每一秒都是甜蜜的 🍯", special: false },
    { id: 4, name: "告白时刻", target: 1800, moves: 22, quote: "三个字，说给全世界听：我爱你 💖", special: true },
    { id: 5, name: "牵手漫步", target: 2000, moves: 21, quote: "十指紧扣，走过春夏秋冬 🌸", special: false },
    { id: 6, name: "浪漫晚餐", target: 2300, moves: 20, quote: "烛光晚餐，你是我唯一的风景 🕯️", special: false },
    { id: 7, name: "星空许愿", target: 2600, moves: 19, quote: "对着流星许愿，愿与你白头偕老 🌟", special: false },
    { id: 8, name: "生日惊喜", target: 3000, moves: 18, quote: "3月25日，为你准备最美的惊喜 🎂", special: true },
    { id: 9, name: "情人节", target: 3300, moves: 17, quote: "玫瑰花海，不及你的笑颜 🌹", special: true },
    { id: 10, name: "永恒承诺", target: 3600, moves: 16, quote: "此生此世，只想和你在一起 💍", special: true },
    { id: 11, name: "梦中情人", target: 4000, moves: 15, quote: "梦里梦外，都是你的身影 💭", special: false },
    { id: 12, name: "心有灵犀", target: 4500, moves: 14, quote: "不用言语，我们就能读懂彼此 💫", special: false }
];

// 苹果类型定义
const APPLE_TYPES = [
    { type: 'red', emoji: '🍎', class: 'apple-red' },
    { type: 'green', emoji: '🍏', class: 'apple-green' },
    { type: 'yellow', emoji: '🍌', class: 'apple-yellow' },
    { type: 'blue', emoji: '🫐', class: 'apple-blue' },
    { type: 'purple', emoji: '🍇', class: 'apple-purple' },
    { type: 'orange', emoji: '🍊', class: 'apple-orange' }
];

// 成就系统
const ACHIEVEMENTS = [
    { id: 'first_match', name: '初次消除', desc: '完成第一次消除', icon: '🎯' },
    { id: 'combo_master', name: '连击高手', desc: '达成10连击', icon: '⚡' },
    { id: 'score_hunter', name: '分数猎人', desc: '单局得分超过5000', icon: '🏆' },
    { id: 'perfect_level', name: '完美通关', desc: '剩余步数≥10通关', icon: '💎' },
    { id: 'power_master', name: '道具大师', desc: '使用所有类型道具', icon: '🎮' },
    { id: 'ashley_special', name: '最爱的Ashley', desc: '专属成就：为爱而战', icon: '👑' },
    { id: 'love_master', name: '爱情达人', desc: '完成所有特殊关卡', icon: '💕' }
];

// 初始化游戏
function initializeGame() {
    createHeartBackground();
    checkSpecialDate();
    generateLevelButtons();
    setupEventListeners();
    loadGameData();
}

// 创建爱心背景动画
function createHeartBackground() {
    const heartsContainer = document.getElementById('heartsBackground');
    
    function createHeart() {
        const heart = document.createElement('div');
        heart.className = 'heart';
        heart.innerHTML = ['❤️', '💕', '💖', '💘'][Math.floor(Math.random() * 4)];
        heart.style.left = Math.random() * 100 + '%';
        heart.style.animationDelay = Math.random() * 6 + 's';
        heart.style.animationDuration = (6 + Math.random() * 4) + 's';
        heartsContainer.appendChild(heart);
        
        setTimeout(() => {
            heart.remove();
        }, 10000);
    }
    
    setInterval(createHeart, 2000);
    
    // 立即创建几个爱心
    for (let i = 0; i < 3; i++) {
        setTimeout(createHeart, i * 1000);
    }
}

// 检查特殊日期
function checkSpecialDate() {
    const today = new Date();
    const month = today.getMonth() + 1;
    const date = today.getDate();
    
    // 3月25日 - Ashley的生日
    if (month === 3 && date === 25) {
        createSpecialEffect('birthday');
        showAchievement('ashley_special');
    }
    // 2月14日 - 情人节
    else if (month === 2 && date === 14) {
        createSpecialEffect('valentine');
    }
    // 其他浪漫日期可以继续添加
}

// 创建特殊日期效果
function createSpecialEffect(type) {
    const effectContainer = document.getElementById('specialDateEffect');
    
    if (type === 'birthday') {
        // 生日烟花效果
        for (let i = 0; i < 20; i++) {
            setTimeout(() => {
                const firework = document.createElement('div');
                firework.className = 'firework';
                firework.style.left = Math.random() * 100 + '%';
                firework.style.top = Math.random() * 100 + '%';
                firework.style.background = `hsl(${Math.random() * 360}, 70%, 60%)`;
                firework.style.width = firework.style.height = Math.random() * 100 + 50 + 'px';
                effectContainer.appendChild(firework);
                
                setTimeout(() => firework.remove(), 2000);
            }, i * 200);
        }
        
        // 显示特殊祝福
        setTimeout(() => {
            alert('🎂 生日快乐，我最爱的Ashley！🎂\n愿你每天都像今天一样美丽动人！');
        }, 1000);
    } else if (type === 'valentine') {
        // 情人节玫瑰花瓣效果
        for (let i = 0; i < 30; i++) {
            setTimeout(() => {
                const petal = document.createElement('div');
                petal.innerHTML = '🌹';
                petal.style.position = 'absolute';
                petal.style.left = Math.random() * 100 + '%';
                petal.style.top = '-50px';
                petal.style.fontSize = Math.random() * 20 + 10 + 'px';
                petal.style.animation = 'floatHeart 8s linear forwards';
                petal.style.pointerEvents = 'none';
                effectContainer.appendChild(petal);
                
                setTimeout(() => petal.remove(), 8000);
            }, i * 300);
        }
    }
}

// 生成关卡按钮
function generateLevelButtons() {
    const levelGrid = document.getElementById('levelGrid');
    levelGrid.innerHTML = '';
    
    // 练习场
    const practiceBtn = document.createElement('button');
    practiceBtn.className = 'level-button practice';
    practiceBtn.innerHTML = `
        <div style="font-size: 1.2em;">🎯</div>
        <div>练习场</div>
        <div class="love-quote">熟能生巧</div>
    `;
    practiceBtn.onclick = () => startLevel(0); // 0表示练习模式
    levelGrid.appendChild(practiceBtn);
    
    // 正常关卡
    LEVELS.forEach(level => {
        const button = document.createElement('button');
        button.className = `level-button ${level.special ? 'special' : ''}`;
        button.innerHTML = `
            <div style="font-size: 1.2em;">${level.special ? '💎' : '🍎'}</div>
            <div>${level.name}</div>
            <div class="love-quote">"${level.quote}"</div>
        `;
        button.onclick = () => selectLevel(level.id);
        levelGrid.appendChild(button);
    });
}

// 选择关卡
function selectLevel(levelId) {
    const level = LEVELS.find(l => l.id === levelId);
    if (!level) return;
    
    // 显示关卡信息和开始按钮
    const confirmDiv = document.createElement('div');
    confirmDiv.style.cssText = `
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: white;
        padding: 2rem;
        border-radius: 20px;
        box-shadow: 0 8px 32px rgba(0,0,0,0.3);
        text-align: center;
        z-index: 1000;
        max-width: 90vw;
    `;
    
    confirmDiv.innerHTML = `
        <h3 style="color: #ff6b6b; margin-bottom: 1rem;">关卡 ${level.id}: ${level.name}</h3>
        <p style="color: #666; margin-bottom: 1rem; font-style: italic;">"${level.quote}"</p>
        <p style="margin-bottom: 1.5rem;">
            目标分数: ${level.target}<br>
            可用步数: ${level.moves}
        </p>
        <div style="display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;">
            <button onclick="startLevel(${level.id}); this.parentElement.parentElement.remove();" 
                    style="padding: 0.8rem 1.5rem; background: #ff6b6b; color: white; border: none; border-radius: 15px; cursor: pointer;">
                开始游戏
            </button>
            <button onclick="this.parentElement.parentElement.remove();" 
                    style="padding: 0.8rem 1.5rem; background: #ccc; color: white; border: none; border-radius: 15px; cursor: pointer;">
                取消
            </button>
        </div>
    `;
    
    document.body.appendChild(confirmDiv);
}

// 开始关卡
function startLevel(levelId) {
    if (levelId === 0) {
        // 练习模式
        gameState.currentLevel = 0;
        gameState.target = 999999; // 无限目标
        gameState.moves = 999; // 无限步数
        gameState.score = 0;
        
        // 练习模式下所有道具都很多
        gameState.powerUps = {
            bomb: 99,
            lightning: 99,
            rainbow: 99,
            hammer: 99,
            shuffle: 99,
            time: 99
        };
    } else {
        const level = LEVELS.find(l => l.id === levelId);
        if (!level) return;
        
        gameState.currentLevel = levelId;
        gameState.target = level.target;
        gameState.moves = level.moves;
        gameState.score = 0;
        gameState.combo = 0;
        
        // 重置道具数量
        gameState.powerUps = {
            bomb: 3,
            lightning: 3,
            rainbow: 2,
            hammer: 5,
            shuffle: 2,
            time: 2
        };
    }
    
    gameState.selectedCell = null;
    gameState.activePowerUp = null;
    gameState.isGameActive = true;
    
    // 切换到游戏界面
    showGameScreen();
    initializeGameBoard();
    updateUI();
    
    // 显示关卡开始动画
    showLevelStartAnimation();
}

// 显示关卡开始动画
function showLevelStartAnimation() {
    const gameScreen = document.getElementById('gameScreen');
    const overlay = document.createElement('div');
    overlay.style.cssText = `
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(255, 107, 107, 0.9);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
        animation: fadeOut 2s forwards;
    `;
    
    if (gameState.currentLevel === 0) {
        overlay.innerHTML = `
            <div style="text-align: center; color: white;">
                <h1 style="font-size: 2.5rem; margin-bottom: 1rem;">🎯 练习场 🎯</h1>
                <p style="font-size: 1.2rem;">熟能生巧，为爱而练！</p>
            </div>
        `;
    } else {
        const level = LEVELS.find(l => l.id === gameState.currentLevel);
        overlay.innerHTML = `
            <div style="text-align: center; color: white;">
                <h1 style="font-size: 2.5rem; margin-bottom: 1rem;">关卡 ${level.id}</h1>
                <h2 style="font-size: 1.8rem; margin-bottom: 1rem;">${level.name}</h2>
                <p style="font-size: 1.2rem; font-style: italic;">"${level.quote}"</p>
            </div>
        `;
    }
    
    gameScreen.appendChild(overlay);
    
    // 添加渐出动画的CSS
    const style = document.createElement('style');
    style.textContent = `
        @keyframes fadeOut {
            0% { opacity: 1; }
            70% { opacity: 1; }
            100% { opacity: 0; visibility: hidden; }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        overlay.remove();
        style.remove();
    }, 2000);
}

// 初始化游戏棋盘
function initializeGameBoard() {
    gameState.grid = [];
    const gameGrid = document.getElementById('gameGrid');
    gameGrid.innerHTML = '';
    
    // 创建8x8网格
    for (let row = 0; row < 8; row++) {
        gameState.grid[row] = [];
        for (let col = 0; col < 8; col++) {
            const cell = document.createElement('div');
            cell.className = 'grid-cell';
            cell.dataset.row = row;
            cell.dataset.col = col;
            
            // 创建苹果
            const apple = createRandomApple();
            gameState.grid[row][col] = apple;
            cell.appendChild(createAppleElement(apple));
            
            // 添加点击事件
            cell.addEventListener('click', () => handleCellClick(row, col));
            
            gameGrid.appendChild(cell);
        }
    }
    
    // 确保初始状态没有匹配
    while (hasMatches()) {
        shuffleBoard();
    }
    
    // 如果是练习模式，随机添加一些特殊道具
    if (gameState.currentLevel === 0) {
        addRandomSpecialItems();
    }
}

// 创建随机苹果
function createRandomApple() {
    const types = [...APPLE_TYPES];
    const randomType = types[Math.floor(Math.random() * types.length)];
    
    // 小概率生成特殊道具
    if (Math.random() < 0.05) {
        return {
            type: 'special',
            specialType: ['bomb', 'lightning', 'rainbow'][Math.floor(Math.random() * 3)],
            emoji: ['💥', '⚡', '🌈'][Math.floor(Math.random() * 3)],
            class: 'special-item'
        };
    }
    
    return randomType;
}

// 创建苹果元素
function createAppleElement(apple) {
    const appleDiv = document.createElement('div');
    appleDiv.className = `apple-icon ${apple.class || ''}`;
    appleDiv.textContent = apple.emoji;
    
    if (apple.type === 'special') {
        appleDiv.classList.add('special-item');
    }
    
    return appleDiv;
}

// 处理单元格点击
function handleCellClick(row, col) {
    if (!gameState.isGameActive || gameState.isPaused) return;
    
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    
    // 如果有激活的道具
    if (gameState.activePowerUp) {
        usePowerUp(gameState.activePowerUp, row, col);
        gameState.activePowerUp = null;
        updatePowerUpUI();
        return;
    }
    
    // 选择单元格
    if (!gameState.selectedCell) {
        selectCell(row, col);
    } else {
        const selectedRow = gameState.selectedCell.row;
        const selectedCol = gameState.selectedCell.col;
        
        // 如果点击同一个单元格，取消选择
        if (selectedRow === row && selectedCol === col) {
            deselectCell();
            return;
        }
        
        // 检查是否为相邻单元格
        if (isAdjacent(selectedRow, selectedCol, row, col)) {
            swapCells(selectedRow, selectedCol, row, col);
            deselectCell();
        } else {
            // 选择新单元格
            deselectCell();
            selectCell(row, col);
        }
    }
}

// 选择单元格
function selectCell(row, col) {
    gameState.selectedCell = { row, col };
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    cell.classList.add('selected');
}

// 取消选择单元格
function deselectCell() {
    if (gameState.selectedCell) {
        const { row, col } = gameState.selectedCell;
        const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
        cell?.classList.remove('selected');
        gameState.selectedCell = null;
    }
}

// 检查是否相邻
function isAdjacent(row1, col1, row2, col2) {
    const rowDiff = Math.abs(row1 - row2);
    const colDiff = Math.abs(col1 - col2);
    return (rowDiff === 1 && colDiff === 0) || (rowDiff === 0 && colDiff === 1);
}

// 交换单元格
function swapCells(row1, col1, row2, col2) {
    // 交换网格中的数据
    const temp = gameState.grid[row1][col1];
    gameState.grid[row1][col1] = gameState.grid[row2][col2];
    gameState.grid[row2][col2] = temp;
    
    // 更新UI
    updateCellDisplay(row1, col1);
    updateCellDisplay(row2, col2);
    
    // 检查匹配
    const matches = findMatches();
    if (matches.length > 0) {
        gameState.moves--;
        processMatches(matches);
    } else {
        // 如果没有匹配，交换回来
        setTimeout(() => {
            gameState.grid[row1][col1] = gameState.grid[row2][col2];
            gameState.grid[row2][col2] = temp;
            updateCellDisplay(row1, col1);
            updateCellDisplay(row2, col2);
        }, 300);
    }
    
    updateUI();
}

// 继续下一部分...
// 更新单元格显示
function updateCellDisplay(row, col) {
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    const apple = gameState.grid[row][col];
    
    if (cell && apple) {
        cell.innerHTML = '';
        cell.appendChild(createAppleElement(apple));
    }
}

// 寻找匹配
function findMatches() {
    const matches = [];
    
    // 检查水平匹配
    for (let row = 0; row < 8; row++) {
        let count = 1;
        let currentType = gameState.grid[row][0].type;
        
        for (let col = 1; col < 8; col++) {
            if (gameState.grid[row][col].type === currentType && currentType !== 'special') {
                count++;
            } else {
                if (count >= 3) {
                    for (let i = col - count; i < col; i++) {
                        matches.push({ row, col: i });
                    }
                }
                count = 1;
                currentType = gameState.grid[row][col].type;
            }
        }
        
        if (count >= 3) {
            for (let i = 8 - count; i < 8; i++) {
                matches.push({ row, col: i });
            }
        }
    }
    
    // 检查垂直匹配
    for (let col = 0; col < 8; col++) {
        let count = 1;
        let currentType = gameState.grid[0][col].type;
        
        for (let row = 1; row < 8; row++) {
            if (gameState.grid[row][col].type === currentType && currentType !== 'special') {
                count++;
            } else {
                if (count >= 3) {
                    for (let i = row - count; i < row; i++) {
                        matches.push({ row: i, col });
                    }
                }
                count = 1;
                currentType = gameState.grid[row][col].type;
            }
        }
        
        if (count >= 3) {
            for (let i = 8 - count; i < 8; i++) {
                matches.push({ row: i, col });
            }
        }
    }
    
    return matches;
}

// 检查是否有匹配
function hasMatches() {
    return findMatches().length > 0;
}

// 处理匹配
function processMatches(matches) {
    if (matches.length === 0) return;
    
    gameState.combo++;
    gameState.totalMatches += matches.length;
    
    // 计算得分
    const baseScore = matches.length * 10;
    const comboBonus = gameState.combo * 5;
    const levelMultiplier = Math.max(1, gameState.currentLevel * 0.1);
    const finalScore = Math.round(baseScore * (1 + comboBonus / 100) * levelMultiplier);
    
    gameState.score += finalScore;
    gameState.totalScore += finalScore;
    
    // 播放音效
    gameState.playSound('match');
    if (gameState.combo > 3) {
        gameState.playSound('combo');
    }
    
    // 显示得分动画
    showScoreAnimation(finalScore, matches[0].row, matches[0].col);
    
    // 显示连击效果
    if (gameState.combo > 1) {
        showComboEffect();
    }
    
    // 创建粒子效果
    matches.forEach(match => {
        createParticleEffect(match.row, match.col);
    });
    
    // 移除匹配的单元格
    matches.forEach(match => {
        gameState.grid[match.row][match.col] = null;
        const cell = document.querySelector(`[data-row="${match.row}"][data-col="${match.col}"]`);
        if (cell) {
            cell.innerHTML = '';
            cell.style.background = '#f0f0f0';
        }
    });
    
    // 延迟处理下落和补充
    setTimeout(() => {
        dropCells();
        setTimeout(() => {
            fillEmptyCells();
            setTimeout(() => {
                const newMatches = findMatches();
                if (newMatches.length > 0) {
                    processMatches(newMatches);
                } else {
                    gameState.combo = 0;
                    checkLevelComplete();
                    checkAchievements();
                }
            }, 300);
        }, 300);
    }, 300);
    
    updateUI();
}

// 显示得分动画
function showScoreAnimation(score, row, col) {
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    if (!cell) return;
    
    const scoreElement = document.createElement('div');
    scoreElement.textContent = `+${score}`;
    scoreElement.style.cssText = `
        position: absolute;
        color: #ff6b6b;
        font-weight: bold;
        font-size: 1.2rem;
        pointer-events: none;
        z-index: 100;
        animation: scoreFloat 1s ease-out forwards;
    `;
    
    const rect = cell.getBoundingClientRect();
    scoreElement.style.left = rect.left + rect.width / 2 + 'px';
    scoreElement.style.top = rect.top + rect.height / 2 + 'px';
    
    document.body.appendChild(scoreElement);
    
    setTimeout(() => scoreElement.remove(), 1000);
}

// 显示连击效果
function showComboEffect() {
    const gameGrid = document.getElementById('gameGrid');
    const comboElement = document.createElement('div');
    comboElement.className = 'combo-display';
    comboElement.textContent = `${gameState.combo}连击! 🔥`;
    
    gameGrid.appendChild(comboElement);
    
    // 更新最大连击记录
    if (gameState.combo > gameState.maxCombo) {
        gameState.maxCombo = gameState.combo;
    }
    
    setTimeout(() => comboElement.remove(), 1000);
}

// 创建粒子效果
function createParticleEffect(row, col) {
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    if (!cell) return;
    
    const rect = cell.getBoundingClientRect();
    const colors = ['#ff6b6b', '#4ecdc4', '#45b7d1', '#96ceb4', '#feca57', '#ff9ff3'];
    
    for (let i = 0; i < 8; i++) {
        const particle = document.createElement('div');
        particle.className = 'particle';
        particle.style.cssText = `
            left: ${rect.left + rect.width / 2}px;
            top: ${rect.top + rect.height / 2}px;
            width: ${Math.random() * 6 + 4}px;
            height: ${Math.random() * 6 + 4}px;
            background: ${colors[Math.floor(Math.random() * colors.length)]};
            animation: particle-float 1s ease-out forwards;
            transform: translate(${(Math.random() - 0.5) * 100}px, ${(Math.random() - 0.5) * 100}px);
        `;
        
        document.body.appendChild(particle);
        setTimeout(() => particle.remove(), 1000);
    }
}

// 下落处理
function dropCells() {
    for (let col = 0; col < 8; col++) {
        let writeIndex = 7; // 从底部开始写入
        
        // 从底部向上遍历
        for (let row = 7; row >= 0; row--) {
            if (gameState.grid[row][col] !== null) {
                if (writeIndex !== row) {
                    gameState.grid[writeIndex][col] = gameState.grid[row][col];
                    gameState.grid[row][col] = null;
                    updateCellDisplay(writeIndex, col);
                    updateCellDisplay(row, col);
                }
                writeIndex--;
            }
        }
    }
}

// 补充空单元格
function fillEmptyCells() {
    for (let col = 0; col < 8; col++) {
        for (let row = 0; row < 8; row++) {
            if (gameState.grid[row][col] === null) {
                gameState.grid[row][col] = createRandomApple();
                updateCellDisplay(row, col);
            }
        }
    }
}

// 道具系统
function usePowerUp(powerType, row, col) {
    if (gameState.powerUps[powerType] <= 0) return;
    
    gameState.powerUps[powerType]--;
    gameState.playSound('powerUp');
    
    switch (powerType) {
        case 'bomb':
            useBomb(row, col);
            break;
        case 'lightning':
            useLightning(row, col);
            break;
        case 'rainbow':
            useRainbow(row, col);
            break;
        case 'hammer':
            useHammer(row, col);
            break;
        case 'shuffle':
            shuffleBoard();
            break;
        case 'time':
            gameState.moves += 5;
            showMessage('获得5步额外步数！⏰');
            break;
    }
    
    updateUI();
    checkAchievements();
}

// 炸弹道具
function useBomb(centerRow, centerCol) {
    const matches = [];
    
    for (let row = Math.max(0, centerRow - 1); row <= Math.min(7, centerRow + 1); row++) {
        for (let col = Math.max(0, centerCol - 1); col <= Math.min(7, centerCol + 1); col++) {
            matches.push({ row, col });
        }
    }
    
    // 创建爆炸效果
    createExplosionEffect(centerRow, centerCol);
    
    setTimeout(() => processMatches(matches), 300);
}

// 闪电道具
function useLightning(row, col) {
    const matches = [];
    
    // 消除整行
    for (let c = 0; c < 8; c++) {
        matches.push({ row, col: c });
    }
    
    // 消除整列
    for (let r = 0; r < 8; r++) {
        matches.push({ row: r, col });
    }
    
    // 创建闪电效果
    createLightningEffect(row, col);
    
    setTimeout(() => processMatches(matches), 300);
}

// 彩虹道具
function useRainbow(row, col) {
    const targetType = gameState.grid[row][col].type;
    const matches = [];
    
    // 找出所有相同类型的苹果
    for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
            if (gameState.grid[r][c].type === targetType) {
                matches.push({ row: r, col: c });
            }
        }
    }
    
    // 创建彩虹效果
    createRainbowEffect();
    
    setTimeout(() => processMatches(matches), 500);
}

// 锤子道具
function useHammer(row, col) {
    const matches = [{ row, col }];
    processMatches(matches);
}

// 创建爆炸效果
function createExplosionEffect(centerRow, centerCol) {
    const cell = document.querySelector(`[data-row="${centerRow}"][data-col="${centerCol}"]`);
    if (!cell) return;
    
    const explosion = document.createElement('div');
    explosion.innerHTML = '💥';
    explosion.style.cssText = `
        position: absolute;
        font-size: 4rem;
        z-index: 100;
        pointer-events: none;
        animation: explosionAnim 0.5s ease-out forwards;
    `;
    
    const rect = cell.getBoundingClientRect();
    explosion.style.left = rect.left + rect.width / 2 - 32 + 'px';
    explosion.style.top = rect.top + rect.height / 2 - 32 + 'px';
    
    document.body.appendChild(explosion);
    
    // 添加爆炸动画
    const style = document.createElement('style');
    style.textContent = `
        @keyframes explosionAnim {
            0% { transform: scale(0) rotate(0deg); opacity: 1; }
            50% { transform: scale(1.5) rotate(180deg); opacity: 1; }
            100% { transform: scale(2) rotate(360deg); opacity: 0; }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        explosion.remove();
        style.remove();
    }, 500);
}

// 创建闪电效果
function createLightningEffect(row, col) {
    const gameGrid = document.getElementById('gameGrid');
    const lightning = document.createElement('div');
    lightning.innerHTML = '⚡';
    lightning.style.cssText = `
        position: absolute;
        font-size: 3rem;
        color: #ffff00;
        z-index: 100;
        pointer-events: none;
        animation: lightningAnim 0.3s ease-out forwards;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
    `;
    
    gameGrid.appendChild(lightning);
    
    const style = document.createElement('style');
    style.textContent = `
        @keyframes lightningAnim {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0); }
            50% { opacity: 1; transform: translate(-50%, -50%) scale(2); }
            100% { opacity: 0; transform: translate(-50%, -50%) scale(1); }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        lightning.remove();
        style.remove();
    }, 300);
}

// 创建彩虹效果
function createRainbowEffect() {
    const gameGrid = document.getElementById('gameGrid');
    const rainbow = document.createElement('div');
    rainbow.innerHTML = '🌈';
    rainbow.style.cssText = `
        position: absolute;
        font-size: 4rem;
        z-index: 100;
        pointer-events: none;
        animation: rainbowAnim 0.8s ease-out forwards;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
    `;
    
    gameGrid.appendChild(rainbow);
    
    const style = document.createElement('style');
    style.textContent = `
        @keyframes rainbowAnim {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0) rotate(0deg); }
            50% { opacity: 1; transform: translate(-50%, -50%) scale(1.5) rotate(180deg); }
            100% { opacity: 0; transform: translate(-50%, -50%) scale(2) rotate(360deg); }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        rainbow.remove();
        style.remove();
    }, 800);
}

// 随机添加特殊道具（练习模式用）
function addRandomSpecialItems() {
    const specialCount = 5; // 添加5个特殊道具
    let added = 0;
    
    while (added < specialCount) {
        const row = Math.floor(Math.random() * 8);
        const col = Math.floor(Math.random() * 8);
        
        if (gameState.grid[row][col].type !== 'special') {
            gameState.grid[row][col] = {
                type: 'special',
                specialType: ['bomb', 'lightning', 'rainbow'][Math.floor(Math.random() * 3)],
                emoji: ['💥', '⚡', '🌈'][Math.floor(Math.random() * 3)],
                class: 'special-item'
            };
            updateCellDisplay(row, col);
            added++;
        }
    }
}

// 洗牌
function shuffleBoard() {
    const allApples = [];
    
    // 收集所有苹果
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            allApples.push(gameState.grid[row][col]);
        }
    }
    
    // 洗牌
    for (let i = allApples.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [allApples[i], allApples[j]] = [allApples[j], allApples[i]];
    }
    
    // 重新放置
    let index = 0;
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            gameState.grid[row][col] = allApples[index++];
            updateCellDisplay(row, col);
        }
    }
    
    // 确保洗牌后没有匹配
    while (hasMatches()) {
        // 如果还有匹配，继续洗牌
        for (let i = allApples.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [allApples[i], allApples[j]] = [allApples[j], allApples[i]];
        }
        
        index = 0;
        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                gameState.grid[row][col] = allApples[index++];
                updateCellDisplay(row, col);
            }
        }
    }
}

// 道具栏交互
function setupPowerUpInteraction() {
    const powerUps = document.querySelectorAll('.power-up');
    
    powerUps.forEach(powerUp => {
        powerUp.addEventListener('click', () => {
            const powerType = powerUp.dataset.power;
            
            if (gameState.powerUps[powerType] > 0) {
                // 取消之前的选择
                powerUps.forEach(p => p.classList.remove('active'));
                
                if (gameState.activePowerUp === powerType) {
                    // 取消选择
                    gameState.activePowerUp = null;
                } else {
                    // 选择新道具
                    gameState.activePowerUp = powerType;
                    powerUp.classList.add('active');
                }
            } else {
                showMessage('道具数量不足！');
            }
        });
    });
}

// 更新道具UI
function updatePowerUpUI() {
    const powerUps = document.querySelectorAll('.power-up');
    
    powerUps.forEach(powerUp => {
        const powerType = powerUp.dataset.power;
        const count = gameState.powerUps[powerType];
        const countSpan = powerUp.querySelector('.count');
        
        if (countSpan) {
            countSpan.textContent = count;
        }
        
        // 移除激活状态
        powerUp.classList.remove('active');
        
        // 如果数量为0，添加禁用样式
        if (count <= 0) {
            powerUp.style.opacity = '0.5';
            powerUp.style.cursor = 'not-allowed';
        } else {
            powerUp.style.opacity = '1';
            powerUp.style.cursor = 'pointer';
        }
    });
}

// 检查关卡完成
function checkLevelComplete() {
    if (gameState.currentLevel === 0) return; // 练习模式不检查完成
    
    if (gameState.score >= gameState.target) {
        // 关卡完成
        gameState.isGameActive = false;
        showLevelComplete();
        checkAchievements();
        saveGameData();
    } else if (gameState.moves <= 0) {
        // 游戏失败
        gameState.isGameActive = false;
        showGameOver();
    }
}

// 显示关卡完成
function showLevelComplete() {
    const level = LEVELS.find(l => l.id === gameState.currentLevel);
    const starsEarned = calculateStars();
    
    const overlay = document.createElement('div');
    overlay.style.cssText = `
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.8);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
    `;
    
    overlay.innerHTML = `
        <div style="background: white; padding: 2rem; border-radius: 20px; text-align: center; max-width: 90vw;">
            <h2 style="color: #ff6b6b; margin-bottom: 1rem;">🎉 关卡完成！</h2>
            <h3 style="margin-bottom: 1rem;">${level.name}</h3>
            <p style="font-style: italic; color: #666; margin-bottom: 1.5rem;">"${level.quote}"</p>
            <div style="margin-bottom: 1.5rem;">
                <div>得分: ${gameState.score}</div>
                <div>剩余步数: ${gameState.moves}</div>
                <div>最高连击: ${gameState.maxCombo}</div>
                <div style="font-size: 2rem; margin: 1rem 0;">${'⭐'.repeat(starsEarned)}</div>
            </div>
            <div style="display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;">
                <button onclick="restartLevel(); this.parentElement.parentElement.parentElement.remove();" 
                        style="padding: 0.8rem 1.5rem; background: #4CAF50; color: white; border: none; border-radius: 15px; cursor: pointer;">
                    重新挑战
                </button>
                <button onclick="nextLevel(); this.parentElement.parentElement.parentElement.remove();" 
                        style="padding: 0.8rem 1.5rem; background: #ff6b6b; color: white; border: none; border-radius: 15px; cursor: pointer;">
                    下一关
                </button>
                <button onclick="backToLevelSelect(); this.parentElement.parentElement.parentElement.remove();" 
                        style="padding: 0.8rem 1.5rem; background: #ccc; color: white; border: none; border-radius: 15px; cursor: pointer;">
                    返回选关
                </button>
            </div>
        </div>
    `;
    
    document.body.appendChild(overlay);
    
    // 添加庆祝动画
    createCelebrationEffect();
}

// 显示游戏失败
function showGameOver() {
    const overlay = document.createElement('div');
    overlay.style.cssText = `
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.8);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
    `;
    
    overlay.innerHTML = `
        <div style="background: white; padding: 2rem; border-radius: 20px; text-align: center; max-width: 90vw;">
            <h2 style="color: #666; margin-bottom: 1rem;">😢 关卡失败</h2>
            <p style="margin-bottom: 1rem;">差一点就成功了！</p>
            <p style="margin-bottom: 1.5rem;">得分: ${gameState.score} / ${gameState.target}</p>
            <div style="display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;">
                <button onclick="restartLevel(); this.parentElement.parentElement.parentElement.remove();" 
                        style="padding: 0.8rem 1.5rem; background: #ff6b6b; color: white; border: none; border-radius: 15px; cursor: pointer;">
                    重新尝试
                </button>
                <button onclick="backToLevelSelect(); this.parentElement.parentElement.parentElement.remove();" 
                        style="padding: 0.8rem 1.5rem; background: #ccc; color: white; border: none; border-radius: 15px; cursor: pointer;">
                    返回选关
                </button>
            </div>
        </div>
    `;
    
    document.body.appendChild(overlay);
}

// 计算星级评价
function calculateStars() {
    const percentage = gameState.score / gameState.target;
    const remainingMoves = gameState.moves;
    
    if (percentage >= 1.5 && remainingMoves >= 10) return 3;
    if (percentage >= 1.2 && remainingMoves >= 5) return 2;
    if (percentage >= 1.0) return 1;
    return 0;
}

// 创建庆祝动画
function createCelebrationEffect() {
    const colors = ['#ff6b6b', '#4ecdc4', '#45b7d1', '#96ceb4', '#feca57', '#ff9ff3'];
    
    for (let i = 0; i < 50; i++) {
        setTimeout(() => {
            const confetti = document.createElement('div');
            confetti.innerHTML = ['🎉', '🎊', '✨', '⭐', '💖'][Math.floor(Math.random() * 5)];
            confetti.style.cssText = `
                position: fixed;
                font-size: ${Math.random() * 20 + 10}px;
                left: ${Math.random() * 100}vw;
                top: -50px;
                z-index: 1001;
                pointer-events: none;
                animation: confettiFall ${Math.random() * 3 + 2}s linear forwards;
            `;
            
            document.body.appendChild(confetti);
            
            setTimeout(() => confetti.remove(), 5000);
        }, i * 50);
    }
    
    // 添加掉落动画
    const style = document.createElement('style');
    style.textContent = `
        @keyframes confettiFall {
            0% {
                transform: translateY(-50px) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => style.remove(), 5000);
}

// 继续第四部分...
// 成就系统
function checkAchievements() {
    // 初次消除
    if (!gameState.achievements.has('first_match') && gameState.totalMatches > 0) {
        unlockAchievement('first_match');
    }
    
    // 连击高手
    if (!gameState.achievements.has('combo_master') && gameState.maxCombo >= 10) {
        unlockAchievement('combo_master');
    }
    
    // 分数猎人
    if (!gameState.achievements.has('score_hunter') && gameState.score >= 5000) {
        unlockAchievement('score_hunter');
    }
    
    // 完美通关
    if (!gameState.achievements.has('perfect_level') && gameState.moves >= 10 && gameState.score >= gameState.target) {
        unlockAchievement('perfect_level');
        gameState.perfectGames++;
    }
    
    // 道具大师 - 检查是否使用过所有类型道具
    const powerUpTypes = Object.keys(gameState.powerUps);
    let usedAllPowerUps = true;
    powerUpTypes.forEach(type => {
        if (gameState.powerUps[type] === 5 || gameState.powerUps[type] === 3 || gameState.powerUps[type] === 2) {
            // 如果道具数量还是初始值，说明没用过
            if ((type === 'hammer' && gameState.powerUps[type] === 5) ||
                (['bomb', 'lightning'].includes(type) && gameState.powerUps[type] === 3) ||
                (['rainbow', 'shuffle', 'time'].includes(type) && gameState.powerUps[type] === 2)) {
                usedAllPowerUps = false;
            }
        }
    });
    if (!gameState.achievements.has('power_master') && !usedAllPowerUps) {
        unlockAchievement('power_master');
    }
    
    // Ashley专属成就
    if (!gameState.achievements.has('ashley_special') && gameState.gamesPlayed >= 5) {
        unlockAchievement('ashley_special');
    }
    
    // 爱情达人 - 完成所有特殊关卡
    const specialLevels = LEVELS.filter(l => l.special);
    let completedSpecial = true;
    // 这里简化处理，假设玩过就算完成
    if (!gameState.achievements.has('love_master') && gameState.currentLevel >= 10) {
        unlockAchievement('love_master');
    }
}

// 解锁成就
function unlockAchievement(achievementId) {
    if (gameState.achievements.has(achievementId)) return;
    
    gameState.achievements.add(achievementId);
    const achievement = ACHIEVEMENTS.find(a => a.id === achievementId);
    
    if (achievement) {
        showAchievement(achievement);
        saveGameData();
    }
}

// 显示成就弹窗
function showAchievement(achievement) {
    const popup = document.getElementById('achievementPopup');
    const text = document.getElementById('achievementText');
    
    text.innerHTML = `
        <div style="font-size: 2rem; margin-bottom: 0.5rem;">${achievement.icon}</div>
        <strong>${achievement.name}</strong><br>
        <small>${achievement.desc}</small>
    `;
    
    popup.classList.add('show');
    
    setTimeout(() => {
        popup.classList.remove('show');
    }, 4000);
}

// UI更新函数
function updateUI() {
    document.getElementById('currentLevel').textContent = gameState.currentLevel === 0 ? '练习' : gameState.currentLevel;
    document.getElementById('score').textContent = gameState.score;
    document.getElementById('target').textContent = gameState.currentLevel === 0 ? '∞' : gameState.target;
    document.getElementById('moves').textContent = gameState.currentLevel === 0 ? '∞' : gameState.moves;
    
    updatePowerUpUI();
}

// 界面切换函数
function showMainMenu() {
    document.getElementById('mainMenu').style.display = 'block';
    document.getElementById('levelSelect').style.display = 'none';
    document.getElementById('gameScreen').style.display = 'none';
}

function showLevelSelect() {
    document.getElementById('mainMenu').style.display = 'none';
    document.getElementById('levelSelect').style.display = 'block';
    document.getElementById('gameScreen').style.display = 'none';
}

function showGameScreen() {
    document.getElementById('mainMenu').style.display = 'none';
    document.getElementById('levelSelect').style.display = 'none';
    document.getElementById('gameScreen').style.display = 'block';
}

// 游戏控制函数
function pauseGame() {
    gameState.isPaused = true;
    document.getElementById('pauseMenu').style.display = 'flex';
}

function resumeGame() {
    gameState.isPaused = false;
    document.getElementById('pauseMenu').style.display = 'none';
}

function restartLevel() {
    const level = gameState.currentLevel;
    document.getElementById('pauseMenu').style.display = 'none';
    startLevel(level);
}

function nextLevel() {
    if (gameState.currentLevel < LEVELS.length) {
        startLevel(gameState.currentLevel + 1);
    } else {
        backToLevelSelect();
    }
}

function backToLevelSelect() {
    gameState.isGameActive = false;
    gameState.isPaused = false;
    document.getElementById('pauseMenu').style.display = 'none';
    showLevelSelect();
}

function backToMainMenu() {
    gameState.isGameActive = false;
    gameState.isPaused = false;
    document.getElementById('pauseMenu').style.display = 'none';
    showMainMenu();
}

// 提示系统
function showHint() {
    // 寻找可能的移动
    const possibleMoves = findPossibleMoves();
    
    if (possibleMoves.length > 0) {
        const hint = possibleMoves[0];
        highlightHint(hint.from.row, hint.from.col, hint.to.row, hint.to.col);
        showMessage('💡 试试这个移动！');
    } else {
        showMessage('💡 没有可用移动，使用洗牌道具！');
    }
}

// 寻找可能的移动
function findPossibleMoves() {
    const moves = [];
    
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            // 检查右边
            if (col < 7) {
                if (wouldCreateMatch(row, col, row, col + 1)) {
                    moves.push({
                        from: { row, col },
                        to: { row, col: col + 1 }
                    });
                }
            }
            
            // 检查下边
            if (row < 7) {
                if (wouldCreateMatch(row, col, row + 1, col)) {
                    moves.push({
                        from: { row, col },
                        to: { row: row + 1, col }
                    });
                }
            }
        }
    }
    
    return moves;
}

// 检查交换是否会产生匹配
function wouldCreateMatch(row1, col1, row2, col2) {
    // 临时交换
    const temp = gameState.grid[row1][col1];
    gameState.grid[row1][col1] = gameState.grid[row2][col2];
    gameState.grid[row2][col2] = temp;
    
    // 检查是否有匹配
    const hasMatch = findMatches().length > 0;
    
    // 交换回来
    gameState.grid[row2][col2] = gameState.grid[row1][col1];
    gameState.grid[row1][col1] = temp;
    
    return hasMatch;
}

// 高亮提示
function highlightHint(fromRow, fromCol, toRow, toCol) {
    const fromCell = document.querySelector(`[data-row="${fromRow}"][data-col="${fromCol}"]`);
    const toCell = document.querySelector(`[data-row="${toRow}"][data-col="${toCol}"]`);
    
    if (fromCell && toCell) {
        fromCell.style.boxShadow = '0 0 0 3px #ffff00';
        toCell.style.boxShadow = '0 0 0 3px #ffff00';
        
        setTimeout(() => {
            fromCell.style.boxShadow = '';
            toCell.style.boxShadow = '';
        }, 2000);
    }
}

// 显示消息
function showMessage(message) {
    const messageDiv = document.createElement('div');
    messageDiv.style.cssText = `
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: rgba(0, 0, 0, 0.8);
        color: white;
        padding: 1rem 2rem;
        border-radius: 10px;
        z-index: 1000;
        font-size: 1.1rem;
        text-align: center;
        max-width: 80vw;
        animation: messageShow 2s ease-out forwards;
    `;
    
    messageDiv.textContent = message;
    document.body.appendChild(messageDiv);
    
    // 添加消息动画
    const style = document.createElement('style');
    style.textContent = `
        @keyframes messageShow {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
            20% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
            80% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
            100% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        messageDiv.remove();
        style.remove();
    }, 2000);
}

// 其他界面功能
function showAchievements() {
    const overlay = document.createElement('div');
    overlay.style.cssText = `
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.8);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
        padding: 1rem;
    `;
    
    const achievementsList = ACHIEVEMENTS.map(achievement => {
        const unlocked = gameState.achievements.has(achievement.id);
        return `
            <div style="display: flex; align-items: center; padding: 0.8rem; margin: 0.5rem 0; 
                        background: ${unlocked ? '#e8f5e8' : '#f5f5f5'}; border-radius: 10px;
                        opacity: ${unlocked ? '1' : '0.6'};">
                <div style="font-size: 2rem; margin-right: 1rem;">${achievement.icon}</div>
                <div>
                    <div style="font-weight: bold; color: ${unlocked ? '#4CAF50' : '#666'};">
                        ${achievement.name} ${unlocked ? '✓' : ''}
                    </div>
                    <div style="font-size: 0.9rem; color: #666;">${achievement.desc}</div>
                </div>
            </div>
        `;
    }).join('');
    
    overlay.innerHTML = `
        <div style="background: white; padding: 2rem; border-radius: 20px; max-width: 90vw; max-height: 90vh; overflow-y: auto;">
            <h2 style="color: #ff6b6b; margin-bottom: 1rem; text-align: center;">🏆 成就系统</h2>
            <div style="margin-bottom: 1rem; text-align: center; color: #666;">
                已解锁: ${gameState.achievements.size} / ${ACHIEVEMENTS.length}
            </div>
            ${achievementsList}
            <button onclick="this.parentElement.parentElement.remove();" 
                    style="width: 100%; padding: 0.8rem; background: #ff6b6b; color: white; 
                           border: none; border-radius: 15px; cursor: pointer; margin-top: 1rem;">
                关闭
            </button>
        </div>
    `;
    
    document.body.appendChild(overlay);
}

function showSettings() {
    const overlay = document.createElement('div');
    overlay.style.cssText = `
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.8);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
    `;
    
    overlay.innerHTML = `
        <div style="background: white; padding: 2rem; border-radius: 20px; text-align: center; max-width: 90vw;">
            <h2 style="color: #ff6b6b; margin-bottom: 1rem;">⚙️ 游戏设置</h2>
            <div style="margin: 1rem 0;">
                <label style="display: block; margin-bottom: 0.5rem;">音效音量</label>
                <input type="range" min="0" max="1" step="0.1" value="0.3" 
                       onchange="updateVolume(this.value)" 
                       style="width: 200px;">
            </div>
            <div style="margin: 1rem 0;">
                <button onclick="resetGameData()" 
                        style="padding: 0.8rem 1.5rem; background: #f44336; color: white; 
                               border: none; border-radius: 15px; cursor: pointer; margin: 0.5rem;">
                    重置游戏数据
                </button>
            </div>
            <div style="margin: 1rem 0; font-size: 0.9rem; color: #666;">
                <div>总游戏次数: ${gameState.gamesPlayed}</div>
                <div>总得分: ${gameState.totalScore}</div>
                <div>完美通关: ${gameState.perfectGames}</div>
                <div>最高连击: ${gameState.maxCombo}</div>
            </div>
            <button onclick="this.parentElement.parentElement.remove();" 
                    style="padding: 0.8rem 1.5rem; background: #ff6b6b; color: white; 
                           border: none; border-radius: 15px; cursor: pointer;">
                关闭
            </button>
        </div>
    `;
    
    document.body.appendChild(overlay);
}

function showLoveMessages() {
    const loveMessages = [
        "每天醒来第一个想到的就是你 💕",
        "你的笑容是我最大的幸福 😊",
        "和你在一起，时间总是过得太快 ⏰",
        "你就是我心中的那颗最亮的星 ⭐",
        "爱你不是三分钟热度，而是深思熟虑后的决定 💖",
        "想和你一起看遍世界的风景 🌍",
        "你的存在让我的世界变得完整 🌈",
        "愿意为你变成更好的自己 💪",
        "每一个平凡的日子，因为有你而变得特别 ✨",
        "我的心里只有一个位置，那就是专属于你的 👑"
    ];
    
    const randomMessage = loveMessages[Math.floor(Math.random() * loveMessages.length)];
    
    const overlay = document.createElement('div');
    overlay.style.cssText = `
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.8);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
    `;
    
    overlay.innerHTML = `
        <div style="background: linear-gradient(135deg, #ff6b6b, #ee5a52); 
                    color: white; padding: 3rem; border-radius: 20px; text-align: center; 
                    max-width: 90vw; box-shadow: 0 8px 32px rgba(0,0,0,0.3);">
            <h2 style="margin-bottom: 2rem;">💝 专属Ashley的情话</h2>
            <p style="font-size: 1.3rem; line-height: 1.6; margin-bottom: 2rem; font-style: italic;">
                "${randomMessage}"
            </p>
            <div style="margin-bottom: 2rem;">
                <div style="font-size: 3rem;">❤️</div>
            </div>
            <button onclick="this.parentElement.parentElement.remove();" 
                    style="padding: 1rem 2rem; background: rgba(255,255,255,0.2); 
                           color: white; border: 2px solid white; border-radius: 25px; 
                           cursor: pointer; font-size: 1rem;">
                我收到了你的爱 💕
            </button>
        </div>
    `;
    
    document.body.appendChild(overlay);
}

// 数据存储
function saveGameData() {
    const data = {
        achievements: Array.from(gameState.achievements),
        totalScore: gameState.totalScore,
        gamesPlayed: gameState.gamesPlayed,
        perfectGames: gameState.perfectGames,
        maxCombo: gameState.maxCombo
    };
    
    try {
        localStorage.setItem('appleGameData', JSON.stringify(data));
    } catch (e) {
        console.log('无法保存游戏数据');
    }
}

function loadGameData() {
    try {
        const data = localStorage.getItem('appleGameData');
        if (data) {
            const parsed = JSON.parse(data);
            gameState.achievements = new Set(parsed.achievements || []);
            gameState.totalScore = parsed.totalScore || 0;
            gameState.gamesPlayed = parsed.gamesPlayed || 0;
            gameState.perfectGames = parsed.perfectGames || 0;
            gameState.maxCombo = parsed.maxCombo || 0;
        }
    } catch (e) {
        console.log('无法加载游戏数据');
    }
}

function resetGameData() {
    if (confirm('确定要重置所有游戏数据吗？这将清除所有成就和统计信息。')) {
        localStorage.removeItem('appleGameData');
        gameState.achievements.clear();
        gameState.totalScore = 0;
        gameState.gamesPlayed = 0;
        gameState.perfectGames = 0;
        gameState.maxCombo = 0;
        showMessage('游戏数据已重置！');
        
        // 关闭设置窗口
        const overlay = document.querySelector('div[style*="position: fixed"]');
        if (overlay) overlay.remove();
    }
}

function updateVolume(volume) {
    Object.values(gameState.sounds).forEach(audio => {
        audio.volume = parseFloat(volume);
    });
}

// 设置事件监听器
function setupEventListeners() {
    setupPowerUpInteraction();
    
    // 键盘事件
    document.addEventListener('keydown', (e) => {
        if (!gameState.isGameActive) return;
        
        switch (e.key) {
            case 'Escape':
                if (gameState.isPaused) {
                    resumeGame();
                } else {
                    pauseGame();
                }
                break;
            case 'h':
            case 'H':
                showHint();
                break;
            case 'r':
            case 'R':
                if (e.ctrlKey || e.metaKey) {
                    e.preventDefault();
                    restartLevel();
                }
                break;
        }
    });
    
    // 触摸设备优化
    document.addEventListener('touchstart', (e) => {
        // 防止双击缩放
        if (e.touches.length > 1) {
            e.preventDefault();
        }
    }, { passive: false });
    
    // 防止页面滚动
    document.addEventListener('touchmove', (e) => {
        e.preventDefault();
    }, { passive: false });
}

// 响应式设计调整
function adjustForMobile() {
    const isMobile = window.innerWidth <= 768;
    
    if (isMobile) {
        // 调整按钮大小
        document.querySelectorAll('.control-btn').forEach(btn => {
            btn.style.padding = '0.4rem 0.8rem';
            btn.style.fontSize = '0.8rem';
        });
        
        // 调整道具栏
        document.querySelectorAll('.power-up').forEach(powerUp => {
            powerUp.style.padding = '0.6rem';
            powerUp.style.fontSize = '0.8rem';
        });
    }
}

// 窗口大小改变时调整
window.addEventListener('resize', adjustForMobile);

// 游戏初始化
document.addEventListener('DOMContentLoaded', () => {
    initializeGame();
    adjustForMobile();
    
    // 增加游戏次数
    gameState.gamesPlayed++;
    saveGameData();
});

// 页面卸载时保存数据
window.addEventListener('beforeunload', saveGameData);

// 防止页面刷新丢失游戏状态
window.addEventListener('beforeunload', (e) => {
    if (gameState.isGameActive) {
        e.preventDefault();
        e.returnValue = '游戏正在进行中，确定要离开吗？';
    }
});

// 添加页面可见性API支持
document.addEventListener('visibilitychange', () => {
    if (document.hidden && gameState.isGameActive && !gameState.isPaused) {
        pauseGame();
    }
});
</script>
</body>
</html>
