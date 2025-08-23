# Apple-Match-only-for-Ashley
Creating an interesting game only for my love, Ashley.
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>水果消消乐 - 献给最爱的Ashley</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background: linear-gradient(135deg, #ff9a9e, #fecfef, #fecfef);
            min-height: 100vh;
            overflow-x: hidden;
            /* 移除触摸防护 */
            touch-action: manipulation;
            -webkit-touch-callout: none;
            -webkit-user-select: none;
            user-select: none;
        }
        
        /* 修复按钮触摸问题 */
        button, .level-button, .control-btn, .power-up {
            /* 关键修复：确保触摸事件正常 */
            touch-action: manipulation;
            -webkit-touch-callout: none;
            -webkit-tap-highlight-color: transparent;
            cursor: pointer;
            border: none;
            background: none;
            outline: none;
            /* 增加触摸区域 */
            min-height: 44px;
            min-width: 44px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .hearts-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
            overflow: hidden;
        }
        
        .heart {
            position: absolute;
            font-size: 1.5rem;
            animation: floatHeart 8s linear infinite;
            opacity: 0.6;
        }
        
        @keyframes floatHeart {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 0.6;
            }
            90% {
                opacity: 0.6;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
        }
        
        /* 主菜单样式 */
        .main-menu {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 2rem;
            text-align: center;
        }
        
        .game-title {
            font-size: clamp(2rem, 8vw, 4rem);
            color: #fff;
            text-shadow: 0 4px 8px rgba(0,0,0,0.3);
            margin-bottom: 1rem;
            font-weight: bold;
        }
        
        .subtitle {
            font-size: clamp(1rem, 4vw, 1.5rem);
            color: #fff;
            opacity: 0.9;
            margin-bottom: 3rem;
            font-style: italic;
        }
        
        .menu-buttons {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            width: 100%;
            max-width: 300px;
        }
        
        .menu-btn {
            padding: 1rem 2rem;
            font-size: 1.2rem;
            background: rgba(255, 255, 255, 0.9);
            color: #ff6b6b;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            font-weight: bold;
            /* 修复触摸 */
            touch-action: manipulation;
            min-height: 60px;
        }
        
        .menu-btn:hover, .menu-btn:active {
            background: #fff;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
        }
        
        /* 关卡选择界面 */
        .level-select {
            display: none;
            padding: 2rem;
            min-height: 100vh;
        }
        
        .level-select h2 {
            color: #fff;
            text-align: center;
            margin-bottom: 2rem;
            font-size: clamp(1.5rem, 6vw, 2.5rem);
            text-shadow: 0 2px 4px rgba(0,0,0,0.3);
        }
        
        .level-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1rem;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .level-button {
            background: rgba(255, 255, 255, 0.95);
            border: none;
            border-radius: 20px;
            padding: 1.5rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            text-align: center;
            /* 修复触摸 */
            touch-action: manipulation;
            min-height: 120px;
        }
        
        .level-button:hover, .level-button:active {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
        }
        
        .level-button.special {
            background: linear-gradient(135deg, #ff6b6b, #ee5a52);
            color: white;
        }
        
        .level-button.practice {
            background: linear-gradient(135deg, #4ecdc4, #44a08d);
            color: white;
        }
        
        .love-quote {
            font-style: italic;
            color: #666;
            margin-top: 0.5rem;
            font-size: 0.9rem;
        }
        
        .level-button.special .love-quote,
        .level-button.practice .love-quote {
            color: rgba(255, 255, 255, 0.8);
        }
        
        /* 游戏界面 */
        .game-screen {
            display: none;
            padding: 1rem;
            min-height: 100vh;
        }
        
        .game-header {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 1rem;
            margin-bottom: 1rem;
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 1rem;
            text-align: center;
        }
        
        .stat-item {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .stat-label {
            font-size: 0.8rem;
            color: #666;
            margin-bottom: 0.2rem;
        }
        
        .stat-value {
            font-size: 1.2rem;
            font-weight: bold;
            color: #ff6b6b;
        }
        
        .game-container {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .game-grid {
            display: grid;
            grid-template-columns: repeat(8, 1fr);
            gap: 2px;
            background: rgba(255, 255, 255, 0.9);
            padding: 1rem;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            aspect-ratio: 1;
        }
        
        .grid-cell {
            background: #f8f9fa;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
            /* 修复触摸 */
            touch-action: manipulation;
            min-height: 40px;
        }
        
        .grid-cell:hover, .grid-cell:active {
            background: #e9ecef;
        }
        
        .grid-cell.selected {
            background: #fff3cd;
            box-shadow: 0 0 0 2px #ffc107;
        }
        
        .apple-icon {
            font-size: clamp(1.2rem, 4vw, 2rem);
            transition: all 0.2s ease;
            pointer-events: none;
        }
        
        .special-item {
            position: relative;
            animation: specialGlow 2s ease-in-out infinite alternate;
        }
        
        @keyframes specialGlow {
            0% { filter: brightness(1) drop-shadow(0 0 5px rgba(255, 215, 0, 0.5)); }
            100% { filter: brightness(1.2) drop-shadow(0 0 10px rgba(255, 215, 0, 0.8)); }
        }

        
.special-bomb {
    animation: bombPulse 1.5s ease-in-out infinite alternate;
}

        .special-lightning {
            animation: lightningFlicker 1s ease-in-out infinite alternate;
        }
        
        @keyframes bombPulse {
            0% { 
                filter: brightness(1) drop-shadow(0 0 8px rgba(255, 0, 0, 0.6));
                transform: scale(1);
            }
            100% { 
                filter: brightness(1.3) drop-shadow(0 0 15px rgba(255, 0, 0, 0.9));
                transform: scale(1.1);
            }
        }
        
        @keyframes lightningFlicker {
            0% { 
                filter: brightness(1) drop-shadow(0 0 8px rgba(255, 255, 0, 0.6));
                transform: rotate(-2deg);
            }
            100% { 
                filter: brightness(1.4) drop-shadow(0 0 15px rgba(255, 255, 0, 0.9));
                transform: rotate(2deg);
            }
        }

        .power-ups {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 0.5rem;
            background: rgba(255, 255, 255, 0.9);
            padding: 1rem;
            border-radius: 15px;
        }
        
        .power-up {
            background: #f8f9fa;
            border: 2px solid #dee2e6;
            border-radius: 12px;
            padding: 0.8rem;
            cursor: pointer;
            transition: all 0.2s ease;
            text-align: center;
            position: relative;
            /* 修复触摸 */
            touch-action: manipulation;
            min-height: 60px;
        }
        
        .power-up:hover, .power-up:active {
            background: #e9ecef;
            transform: translateY(-1px);
        }
        
        .power-up.active {
            background: #fff3cd;
            border-color: #ffc107;
        }
        
        .power-up .icon {
            font-size: 1.5rem;
            margin-bottom: 0.2rem;
        }
        
        .power-up .name {
            font-size: 0.8rem;
            color: #666;
            margin-bottom: 0.2rem;
        }
        
        .power-up .count {
            background: #ff6b6b;
            color: white;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            font-size: 0.7rem;
            display: flex;
            align-items: center;
            justify-content: center;
            position: absolute;
            top: -5px;
            right: -5px;
        }
        
        .controls {
            display: flex;
            justify-content: space-between;
            gap: 1rem;
            flex-wrap: wrap;
        }
        
        .control-btn {
            padding: 0.8rem 1.2rem;
            background: #ff6b6b;
            color: white;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 0.9rem;
            transition: all 0.2s ease;
            flex: 1;
            min-width: 80px;
            /* 修复触摸 */
            touch-action: manipulation;
            min-height: 44px;
        }
        
        .control-btn:hover, .control-btn:active {
            background: #ee5a52;
            transform: translateY(-1px);
        }
        
        .control-btn.secondary {
            background: #6c757d;
        }
        
        .control-btn.secondary:hover, .control-btn.secondary:active {
            background: #545b62;
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
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        
        .pause-content {
            background: white;
            padding: 2rem;
            border-radius: 20px;
            text-align: center;
            max-width: 90vw;
        }
        
        .pause-content h3 {
            color: #ff6b6b;
            margin-bottom: 1.5rem;
        }
        
        .pause-buttons {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        
        /* 成就弹窗 */
        .achievement-popup {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #4CAF50;
            color: white;
            padding: 1rem 1.5rem;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            transform: translateX(100%);
            transition: transform 0.5s ease;
            z-index: 1001;
            max-width: 300px;
        }
        
        .achievement-popup.show {
            transform: translateX(0);
        }
        
        /* 动画和效果 */
        .combo-display {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(255, 107, 107, 0.9);
            color: white;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            font-weight: bold;
            z-index: 100;
            animation: comboAnim 1s ease-out forwards;
            pointer-events: none;
        }
        
        @keyframes comboAnim {
            0% {
                opacity: 0;
                transform: translate(-50%, -50%) scale(0.5);
            }
            50% {
                opacity: 1;
                transform: translate(-50%, -50%) scale(1.2);
            }
            100% {
                opacity: 0;
                transform: translate(-50%, -50%) scale(1);
            }
        }
        
        .particle {
            position: fixed;
            border-radius: 50%;
            pointer-events: none;
            z-index: 100;
        }
        
        @keyframes particle-float {
            0% {
                opacity: 1;
                transform: scale(1);
            }
            100% {
                opacity: 0;
                transform: scale(0);
            }
        }
        
        /* 移动端优化 */
        @media (max-width: 768px) {
            .game-header {
                grid-template-columns: repeat(2, 1fr);
                gap: 0.5rem;
                padding: 0.8rem;
            }
            
            .power-ups {
                grid-template-columns: repeat(6, 1fr);
                padding: 0.8rem;
            }
            
            .power-up {
                padding: 0.6rem 0.4rem;
            }
            
            .power-up .icon {
                font-size: 1.2rem;
            }
            
            .power-up .name {
                font-size: 0.7rem;
            }
            
            .controls {
                gap: 0.5rem;
            }
            
            .control-btn {
                padding: 0.6rem 0.8rem;
                font-size: 0.8rem;
            }
        }
        
        @media (max-width: 480px) {
            .main-menu {
                padding: 1rem;
            }
            
            .level-select {
                padding: 1rem;
            }
            
            .level-grid {
                grid-template-columns: 1fr;
                gap: 0.8rem;
            }
            
            .game-screen {
                padding: 0.5rem;
            }
        }
    </style>
</head>
<body>
    <!-- 爱心背景 -->
    <div class="hearts-bg" id="heartsBackground"></div>
    
    <!-- 主菜单 -->
    <div class="main-menu" id="mainMenu">
        <h1 class="game-title">🍎 水果消消乐</h1>
        <p class="subtitle">献给最爱的Ashley ❤️</p>
        <div class="menu-buttons">
            <button class="menu-btn" onclick="showLevelSelect()">开始游戏 🎮</button>
            <button class="menu-btn" onclick="showAchievements()">成就系统 🏆</button>
            <button class="menu-btn" onclick="showLoveMessages()">专属情话 💕</button>
            <button class="menu-btn" onclick="showSettings()">游戏说明 ⚙️</button>
        </div>
    </div>
    
    <!-- 关卡选择 -->
    <div class="level-select" id="levelSelect">
        <h2>选择关卡</h2>
        <div class="level-grid" id="levelGrid"></div>
        <div style="text-align: center; margin-top: 2rem;">
            <button class="menu-btn" onclick="showMainMenu()">返回主菜单</button>
        </div>
    </div>
    <!-- 游戏界面 -->
    <div class="game-screen" id="gameScreen">
        <!-- 游戏状态栏 -->
        <div class="game-header">
            <div class="stat-item">
                <div class="stat-label">关卡</div>
                <div class="stat-value" id="currentLevel">1</div>
            </div>
            <div class="stat-item">
                <div class="stat-label">得分</div>
                <div class="stat-value" id="score">0</div>
            </div>
            <div class="stat-item">
                <div class="stat-label">目标</div>
                <div class="stat-value" id="target">1000</div>
            </div>
            <div class="stat-item">
                <div class="stat-label">剩余步数</div>
                <div class="stat-value" id="moves">25</div>
            </div>
        </div>
        
        <div class="game-container">
            <!-- 游戏网格 -->
            <div class="game-grid" id="gameGrid"></div>
            
            <!-- 道具栏 -->
            <div class="power-ups" id="powerUps">
                <div class="power-up" data-power="bomb">
                    <div class="icon">💥</div>
                    <div class="name">炸弹</div>
                    <div class="count">3</div>
                </div>
                <div class="power-up" data-power="lightning">
                    <div class="icon">⚡</div>
                    <div class="name">闪电</div>
                    <div class="count">3</div>
                </div>
                <div class="power-up" data-power="rainbow">
                    <div class="icon">🌈</div>
                    <div class="name">彩虹</div>
                    <div class="count">2</div>
                </div>
                <div class="power-up" data-power="hammer">
                    <div class="icon">🔨</div>
                    <div class="name">锤子</div>
                    <div class="count">5</div>
                </div>
                <div class="power-up" data-power="shuffle">
                    <div class="icon">🔄</div>
                    <div class="name">洗牌</div>
                    <div class="count">2</div>
                </div>
                <div class="power-up" data-power="time">
                    <div class="icon">⏰</div>
                    <div class="name">时光</div>
                    <div class="count">2</div>
                </div>
            </div>
            
            <!-- 控制按钮 -->
            <div class="controls">
                <button class="control-btn secondary" onclick="showHint()">提示 💡</button>
                <button class="control-btn secondary" onclick="showGameInstructions()">说明 📖</button>
                <button class="control-btn secondary" onclick="pauseGame()">暂停 ⏸️</button>
                <button class="control-btn secondary" onclick="restartLevel()">重新开始 🔄</button>
                <button class="control-btn secondary" onclick="backToLevelSelect()">返回选关 ⬅️</button>
            </div>
        </div>
    </div>
    
    <!-- 暂停菜单 -->
    <div class="pause-menu" id="pauseMenu">
        <div class="pause-content">
            <h3>游戏暂停</h3>
            <div class="pause-buttons">
                <button class="menu-btn" onclick="resumeGame()">继续游戏 ▶️</button>
                <button class="menu-btn" onclick="restartLevel()">重新开始 🔄</button>
                <button class="menu-btn" onclick="backToLevelSelect()">返回选关 ⬅️</button>
                <button class="menu-btn" onclick="backToMainMenu()">主菜单 🏠</button>
            </div>
        </div>
    </div>
    
    <!-- 成就弹窗 -->
    <div class="achievement-popup" id="achievementPopup">
        <div id="achievementText"></div>
    </div>
    
    <!-- 特殊日期效果容器 -->
    <div id="specialDateEffect" style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 999;"></div>

<script>
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
            match: this.createBeep(200, 0.1),
            combo: this.createBeep(300, 0.15),
            powerUp: this.createBeep(400, 0.2)
        };
    }

    createBeep(frequency, duration) {
        // 简化的音效生成
        return {
            play: () => {
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
                    // 静默处理音效错误
                }
            }
        };
    }

    playSound(type) {
        if (this.sounds[type]) {
            this.sounds[type].play();
        }
    }
}

// 全局游戏状态
const gameState = new GameState();

// 关卡数据和情话
const LEVELS = [
    { id: 1, name: "初遇", target: 1800, moves: 450, quote: "就像第一次见到你，心跳不已 💕", special: false },
    { id: 2, name: "怦然心动", target: 2300, moves: 440, quote: "每一个眼神交汇，都是命运的安排 ✨", special: false },
    { id: 3, name: "甜蜜约会", target: 2500, moves: 430, quote: "和你在一起的每一秒都是甜蜜的 🍯", special: false },
    { id: 4, name: "告白时刻", target: 2800, moves: 420, quote: "三个字，说给全世界听：我爱你 💖", special: true },
    { id: 5, name: "牵手漫步", target: 3000, moves: 410, quote: "十指紧扣，走过春夏秋冬 🌸", special: false },
    { id: 6, name: "浪漫晚餐", target: 3500, moves: 400, quote: "烛光晚餐，你是我唯一的风景 🕯️", special: false },
    { id: 7, name: "星空许愿", target: 4000, moves: 390, quote: "对着流星许愿，愿与你白头偕老 🌟", special: false },
    { id: 8, name: "生日惊喜", target: 4500, moves: 380, quote: "3月25日，为你准备最美的惊喜 🎂", special: true },
    { id: 9, name: "情人节", target: 5000, moves: 370, quote: "玫瑰花海，不及你的笑颜 🌹", special: true },
    { id: 10, name: "永恒承诺", target: 5600, moves: 360, quote: "此生此世，只想和你在一起 💍", special: true },
    { id: 11, name: "梦中情人", target: 6000, moves: 350, quote: "梦里梦外，都是你的身影 💭", special: false },
    { id: 12, name: "心有灵犀", target: 6500, moves: 340, quote: "不用言语，我们就能读懂彼此 💫", special: false },
    { id: 13, name: "甜蜜回忆", target: 7000, moves: 330, quote: "每一个回忆都是我们爱情的见证 📸", special: false },
    { id: 14, name: "浪漫旅程", target: 7500, moves: 320, quote: "和你走过的每一处风景都成了诗 🗺️", special: false },
    { id: 15, name: "幸福密码", target: 8000, moves: 310, quote: "你就是我幸福生活的全部密码 🔐", special: true },
    { id: 16, name: "终极挑战", target: 9000, moves: 300, quote: "最终关卡：用爆炸的力量见证我们的爱！🏁", special: true }
];

// 苹果类型定义 - 支持关卡渐进式增加
const APPLE_TYPES = [
    { type: 'red', emoji: '🍎', class: 'apple-red' },
    { type: 'green', emoji: '🍏', class: 'apple-green' },
    { type: 'yellow', emoji: '🍌', class: 'apple-yellow' },
    { type: 'blue', emoji: '🫐', class: 'apple-blue' },
    { type: 'purple', emoji: '🍇', class: 'apple-purple' },
    { type: 'orange', emoji: '🍊', class: 'apple-orange' },
    // 新增水果类型 - 后期关卡解锁
    { type: 'peach', emoji: '🍑', class: 'apple-peach' },
    { type: 'strawberry', emoji: '🍓', class: 'apple-strawberry' },
    { type: 'watermelon', emoji: '🍉', class: 'apple-watermelon' },
    { type: 'pineapple', emoji: '🍍', class: 'apple-pineapple' },
    { type: 'kiwi', emoji: '🥝', class: 'apple-kiwi' },
    { type: 'mango', emoji: '🥭', class: 'apple-mango' }
];

// 成就系统
const ACHIEVEMENTS = [
    { id: 'first_match', name: '初次消除', desc: '完成第一次消除', icon: '🎯' },
    { id: 'combo_master', name: '连击高手', desc: '达成10连击', icon: '⚡' },
    { id: 'score_hunter', name: '分数猎人', desc: '单局得分超过5000', icon: '🏆' },
    { id: 'perfect_level', name: '完美通关', desc: '剩余步数≥200通关', icon: '💎' },
    { id: 'power_master', name: '道具大师', desc: '使用所有类型道具', icon: '🎮' },
    { id: 'ashley_special', name: '最爱的Ashley', desc: '专属成就：为爱而战', icon: '👑' },
    { id: 'love_master', name: '爱情达人', desc: '完成所有特殊关卡', icon: '💕' }
];

// 初始化游戏
function initializeGame() {
    createHeartBackground();
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
        heart.innerHTML = ['❤️', '💋', '💕', '💖', '💘'][Math.floor(Math.random() * 5)];
        heart.style.left = Math.random() * 100 + '%';
        heart.style.animationDelay = Math.random() * 6 + 's';
        heart.style.animationDuration = (6 + Math.random() * 4) + 's';
        heartsContainer.appendChild(heart);
        
        setTimeout(() => {
            if (heart.parentNode) heart.remove();
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
    
    // 1月17日 - 初次见面纪念日
    if (month === 1 && date === 17) {
        createSpecialEffect('firstmeet');
    }
    // 1月21日 - 确定关系纪念日
    else if (month === 1 && date === 21) {
        createSpecialEffect('together');
    }
    // 2月14日 - 情人节
    else if (month === 2 && date === 14) {
        createSpecialEffect('valentine');
    }
    // 3月25日 - Ashley的生日
    else if (month === 3 && date === 25) {
        createSpecialEffect('birthday');
        setTimeout(() => showAchievement(ACHIEVEMENTS.find(a => a.id === 'ashley_special')), 2000);
    }
    // 6月28日 - 婚礼日
    else if (month === 6 && date === 28) {
        createSpecialEffect('wedding');
    }
    // 10月22日 - 登记结婚纪念日
    else if (month === 10 && date === 22) {
        createSpecialEffect('certificate');
    }
}
    
// 创建特殊日期效果
function createSpecialEffect(type) {
    const effectContainer = document.getElementById('specialDateEffect');
    
    if (type === 'firstmeet') {
        // 初次见面星星和邂逅效果
        for (let i = 0; i < 30; i++) {
            setTimeout(() => {
                const star = document.createElement('div');
                star.innerHTML = ['💕', '🤩', '💘', '🫶', '✨'][Math.floor(Math.random() * 5)];
                star.style.cssText = `
                    position: absolute;
                    left: ${Math.random() * 100}%;
                    top: ${Math.random() * 100}%;
                    font-size: ${Math.random() * 25 + 15}px;
                    animation: starTwinkle 4s ease-in-out forwards;
                    pointer-events: none;
                `;
                effectContainer.appendChild(star);
                
                setTimeout(() => {
                    if (star.parentNode) star.remove();
                }, 4000);
            }, i * 120);
        }
        
        // 添加星星闪烁动画
        const style = document.createElement('style');
        style.textContent = `
            @keyframes starTwinkle {
                0% { transform: scale(0) rotate(0deg); opacity: 0; }
                25% { transform: scale(1.3) rotate(90deg); opacity: 1; }
                50% { transform: scale(0.8) rotate(180deg); opacity: 0.7; }
                75% { transform: scale(1.1) rotate(270deg); opacity: 1; }
                100% { transform: scale(0) rotate(360deg); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
        
        // 显示特殊祝福
        setTimeout(() => {
            showMessage('✨ 亲爱的Ashley，还记得1月17日吗？✨\n那是我们第一次见面的神奇日子，命运让我们相遇，从此改变了我的人生！\n感谢上天让我遇见了你，我的天使！');
        }, 1000);
        
        setTimeout(() => {
            style.remove();
        }, 35000);
        
    } else if (type === 'together') {
        // 确定关系爱心锁和玫瑰效果
        for (let i = 0; i < 25; i++) {
            setTimeout(() => {
                const love = document.createElement('div');
                love.innerHTML = ['💞', '🥰', '👩🏻‍❤️‍👨🏻', '💋', '💗'][Math.floor(Math.random() * 5)];
                love.style.cssText = `
                    position: absolute;
                    left: ${Math.random() * 100}%;
                    top: -50px;
                    font-size: ${Math.random() * 30 + 20}px;
                    animation: loveGrow 6s ease-out forwards;
                    pointer-events: none;
                `;
                effectContainer.appendChild(love);
                
                setTimeout(() => {
                    if (love.parentNode) love.remove();
                }, 6000);
            }, i * 180);
        }
        
        // 添加爱心生长动画
        const style = document.createElement('style');
        style.textContent = `
            @keyframes loveGrow {
                0% {
                    transform: translateY(0) scale(0) rotate(0deg);
                    opacity: 0;
                }
                30% {
                    transform: translateY(200px) scale(1.2) rotate(120deg);
                    opacity: 1;
                }
                70% {
                    transform: translateY(400px) scale(0.9) rotate(240deg);
                    opacity: 0.8;
                }
                100% {
                    transform: translateY(calc(100vh + 50px)) scale(0.7) rotate(360deg);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);
        
        // 显示特殊祝福
        setTimeout(() => {
            showMessage('💕 我最珍爱的Ashley，1月21日是我们确定关系的甜蜜日子 💕\n从那天起，你就是我的女朋友，我的心从此只为你跳动！\n谢谢你愿意成为我的女朋友，让我的世界充满了爱与希望！');
        }, 1000);
        
        setTimeout(() => {
            style.remove();
        }, 35000);
        
    } else if (type === 'valentine') {
        // 情人节玫瑰花瓣效果
        for (let i = 0; i < 40; i++) {
            setTimeout(() => {
                const heart = document.createElement('div');
                heart.innerHTML = ['🌸', '💖', '💕', '🌹', '💝'][Math.floor(Math.random() * 5)];
                heart.style.cssText = `
                    position: absolute;
                    left: ${Math.random() * 100}%;
                    top: -50px;
                    font-size: ${Math.random() * 35 + 15}px;
                    animation: heartFall 5s ease-in forwards;
                    pointer-events: none;
                `;
                effectContainer.appendChild(heart);
                
                setTimeout(() => {
                    if (heart.parentNode) heart.remove();
                }, 5000);
            }, i * 100);
        }
        
        // 添加爱心飘落动画
        const style = document.createElement('style');
        style.textContent = `
            @keyframes heartFall {
                0% {
                    transform: translateY(0) rotate(0deg);
                    opacity: 0;
                }
                10% {
                    opacity: 1;
                }
                90% {
                    opacity: 0.8;
                }
                100% {
                    transform: translateY(calc(100vh + 50px)) rotate(360deg);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);
        
        // 显示特殊祝福
        setTimeout(() => {
            showMessage('💖 我的挚爱Ashley，情人节快乐！💖\n每一天和你在一起都是情人节，你是我心中永远的挚爱！\n我爱你不是因为你是谁，而是因为在你面前我是谁！');
        }, 1000);
        
        setTimeout(() => {
            style.remove();
        }, 35000);
        
    } else if (type === 'birthday') {
        // 生日蛋糕和气球效果
        for (let i = 0; i < 30; i++) {
            setTimeout(() => {
                const balloon = document.createElement('div');
                balloon.innerHTML = ['🎂', '🎈', '🎉', '🎊', '🌟'][Math.floor(Math.random() * 5)];
                balloon.style.cssText = `
                    position: absolute;
                    left: ${Math.random() * 100}%;
                    top: 100vh;
                    font-size: ${Math.random() * 30 + 20}px;
                    animation: balloonFloat 6s ease-out forwards;
                    pointer-events: none;
                `;
                effectContainer.appendChild(balloon);
                
                setTimeout(() => {
                    if (balloon.parentNode) balloon.remove();
                }, 6000);
            }, i * 100);
        }
        
        // 添加气球上升动画
        const style = document.createElement('style');
        style.textContent = `
            @keyframes balloonFloat {
                0% { transform: translateY(0) scale(0); opacity: 0; }
                20% { opacity: 1; transform: scale(1); }
                100% { transform: translateY(-100vh) scale(1.2); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
        
        // 显示特殊祝福
        setTimeout(() => {
            showMessage('🎂 最美丽的Ashley，生日快乐！🎂\n愿你在我的陪伴下永远美丽动人，我爱你！\n在这特殊的日子里，我想对你说：遇见你是我最大的幸运！');
        }, 1000);
        
        setTimeout(() => {
            style.remove();
        }, 35000);
        
    } else if (type === 'wedding') {
        // 婚礼日白玫瑰和教堂钟声效果
        for (let i = 0; i < 35; i++) {
            setTimeout(() => {
                const flower = document.createElement('div');
                flower.innerHTML = ['🎉', '🤍', '🕊️', '💒', '🌹'][Math.floor(Math.random() * 5)];
                flower.style.cssText = `
                    position: absolute;
                    left: ${Math.random() * 100}%;
                    top: -50px;
                    font-size: ${Math.random() * 25 + 15}px;
                    animation: weddingFloat 8s linear forwards;
                    pointer-events: none;
                `;
                effectContainer.appendChild(flower);
                
                setTimeout(() => {
                    if (flower.parentNode) flower.remove();
                }, 8000);
            }, i * 200);
        }
        
        // 添加婚礼漂浮动画
        const style = document.createElement('style');
        style.textContent = `
            @keyframes weddingFloat {
                0% {
                    transform: translateY(0) rotate(0deg);
                    opacity: 0;
                }
                10% {
                    opacity: 1;
                }
                90% {
                    opacity: 0.8;
                }
                100% {
                    transform: translateY(calc(100vh + 50px)) rotate(360deg);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);
        
        // 显示特殊祝福
        setTimeout(() => {
            showMessage('💒 最美的Ashley，6月28日是我们举办婚礼的神圣日子 💒\n在众人的祝福下，我们交换了誓言，你是我今生唯一的新娘！\n那一天，我对全世界宣告：你是我最珍贵的宝贝！');
        }, 1000);
        
        setTimeout(() => {
            style.remove();
        }, 35000);
        
    } else if (type === 'certificate') {
        // 登记结婚纪念日钻戒效果
        for (let i = 0; i < 25; i++) {
            setTimeout(() => {
                const ring = document.createElement('div');
                ring.innerHTML = '💍';
                ring.style.cssText = `
                    position: absolute;
                    left: ${Math.random() * 100}%;
                    top: ${Math.random() * 100}%;
                    font-size: ${Math.random() * 30 + 20}px;
                    animation: ringSparkle 3s ease-out forwards;
                    pointer-events: none;
                `;
                effectContainer.appendChild(ring);
                
                setTimeout(() => {
                    if (ring.parentNode) ring.remove();
                }, 3000);
            }, i * 150);
        }
        
        // 添加钻戒闪烁动画
        const style = document.createElement('style');
        style.textContent = `
            @keyframes ringSparkle {
                0% { transform: scale(0) rotate(0deg); opacity: 1; }
                50% { transform: scale(1.2) rotate(180deg); opacity: 1; }
                100% { transform: scale(0.8) rotate(360deg); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
        
        // 显示特殊祝福
        setTimeout(() => {
            showMessage('💍 亲爱的Ashley，还记得10月22日这个特殊的日子吗？💍\n那一天我们领取了结婚证，从此你是我法定的妻子！\n从那一刻起，我们就是法律认可的夫妻，此生此世永不分离！');
        }, 1000);
        
        setTimeout(() => {
            style.remove();
        }, 35000);
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
            <div style="font-size: 1.2em;">${level.special ? '🧜🏼‍♀️' : '❣️'}</div>
            <div>${level.name}</div>
            <div class="love-quote">"${level.quote}"</div>
        `;
        button.onclick = () => selectLevel(level.id);
        levelGrid.appendChild(button);
    });
}

// 继续第三部分...
// 选择关卡
function selectLevel(levelId) {
    if (levelId <= LEVELS.length) {
        startLevel(levelId);
    }
}

// 开始关卡
function startLevel(levelId) {
    const level = LEVELS.find(l => l.id === levelId);
    
    if (levelId === 0) {
        // 练习模式
        gameState.currentLevel = 0;
        gameState.target = Infinity;
        gameState.moves = Infinity;
        // 练习模式重置道具
        gameState.powerUps = {
            bomb: 99,
            lightning: 99,
            rainbow: 99,
            hammer: 99,
            shuffle: 99,
            time: 99
        };
    } else if (level) {
        gameState.currentLevel = level.id;
        gameState.target = level.target;
        gameState.moves = level.moves;
        // 重置道具
        gameState.powerUps = {
            bomb: 40,
            lightning: 40,
            rainbow: 40,
            hammer: 40,
            shuffle: 40,
            time: 40
        };
    }
    
    gameState.score = 0;
    gameState.combo = 0;
    gameState.selectedCell = null;
    gameState.activePowerUp = null;
    gameState.isGameActive = true;
    gameState.isPaused = false;
    
    initializeGrid();
    showGameScreen();
    updateUI();
}

// 创建随机苹果 - 根据关卡渐进式增加种类
function createRandomApple() {
    // 根据当前关卡确定可用的苹果种类数量
    let availableTypeCount;
    
    if (gameState.currentLevel === 0) {
        // 练习模式：使用所有类型
        availableTypeCount = APPLE_TYPES.length;
    } else if (gameState.currentLevel <= 2) {
        // 第1-2关：4种基础苹果
        availableTypeCount = 5;
     } else if (gameState.currentLevel <= 3) {
        // 第1-2关：4种基础苹果
        availableTypeCount = 6;
    } else if (gameState.currentLevel <= 4) {
        // 第3-4关：5种苹果
        availableTypeCount = 6;
    } else if (gameState.currentLevel <= 6) {
        // 第5-6关：6种苹果
        availableTypeCount = 7;
    } else if (gameState.currentLevel <= 8) {
        // 第7-8关：7种苹果
        availableTypeCount = 7;
    } else if (gameState.currentLevel <= 10) {
        // 第9-10关：8种苹果
        availableTypeCount = 8;
    } else if (gameState.currentLevel <= 11) {
        // 第11-12关：9种苹果
        availableTypeCount = 8;
    } else if (gameState.currentLevel <= 12) {
        // 第11-12关：9种苹果
        availableTypeCount = 9;
    } else {
        // 更高关卡：使用所有类型
        availableTypeCount = APPLE_TYPES.length;
    }
    
    // 从可用类型中随机选择
    const availableTypes = APPLE_TYPES.slice(0, availableTypeCount);
    const randomType = availableTypes[Math.floor(Math.random() * availableTypes.length)];
    
    // 第15-16关都有特殊水果，但概率不同
    if (gameState.currentLevel === 15) {  // 第15关5%概率
        const bombChance = 0.06;      // 💥炸弹6%概率
        const lightningChance = 0.04; // 🌪龙卷风4%概率
        
        const random = Math.random();
        if (random < bombChance) {
            return { type: 'bomb_fruit', emoji: '💥', class: 'special-bomb' };
        } else if (random < bombChance + lightningChance) {
            return { type: 'lightning_fruit', emoji: '🌪', class: 'special-lightning' };
        }
    } else if (gameState.currentLevel === 16) {  // 第16关10%概率
        const bombChance = 0.06;      // 💥炸弹6%概率
        const lightningChance = 0.04; // 🌪龙卷风4%概率
        
        const random = Math.random();
        if (random < bombChance) {
            return { type: 'bomb_fruit', emoji: '💥', class: 'special-bomb' };
        } else if (random < bombChance + lightningChance) {
            return { type: 'lightning_fruit', emoji: '🌪', class: 'special-lightning' };
        }
    }
    
    return {
        type: randomType.type,
        emoji: randomType.emoji,
        class: randomType.class
    };
}

// 初始化游戏网格
function initializeGrid() {
    const gridElement = document.getElementById('gameGrid');
    gridElement.innerHTML = '';
    
    // 创建8x8网格
    gameState.grid = [];
    for (let row = 0; row < 8; row++) {
        gameState.grid[row] = [];
        for (let col = 0; col < 8; col++) {
            gameState.grid[row][col] = createRandomApple();
            
            // 创建DOM元素
            const cell = document.createElement('div');
            cell.className = 'grid-cell';
            cell.dataset.row = row;
            cell.dataset.col = col;
            
            const appleElement = createAppleElement(gameState.grid[row][col]);
            cell.appendChild(appleElement);
            
            // 绑定触摸事件
            bindCellEvents(cell, row, col);
            
            gridElement.appendChild(cell);
        }
    }
    
    // 确保初始状态没有匹配
    while (hasMatches()) {
        for (let row = 0; row < 8; row++) {
            for (let col = 0; col < 8; col++) {
                gameState.grid[row][col] = createRandomApple();
                updateCellDisplay(row, col);
            }
        }
    }
    
    // 练习模式添加特殊道具
    if (gameState.currentLevel === 0) {
        setTimeout(() => {
            addRandomSpecialItems();
        }, 1000);
    }
}

// 创建苹果元素
function createAppleElement(apple) {
    const element = document.createElement('div');
    element.className = `apple-icon ${apple.class || ''}`;
    element.textContent = apple.emoji;
    return element;
}

// 绑定单元格事件
function bindCellEvents(cell, row, col) {
    let touchStartTime;
    let touchStartPos;
    
    // 统一的点击处理函数
    function handleCellClick(e) {
        e.preventDefault();
        if (!gameState.isGameActive || gameState.isPaused) return;
        
        handleCellInteraction(row, col);
    }
    
    // 鼠标事件
    cell.addEventListener('click', handleCellClick);
    
    // 触摸事件 - 修复触摸响应问题
    cell.addEventListener('touchstart', (e) => {
        e.preventDefault();
        touchStartTime = Date.now();
        touchStartPos = {
            x: e.touches[0].clientX,
            y: e.touches[0].clientY
        };
        
        // 添加视觉反馈
        cell.style.backgroundColor = '#e9ecef';
    }, { passive: false });
    
    cell.addEventListener('touchend', (e) => {
        e.preventDefault();
        
        // 移除视觉反馈
        cell.style.backgroundColor = '';
        
        const touchEndTime = Date.now();
        const touchDuration = touchEndTime - touchStartTime;
        
        // 如果是短触摸（类似点击），处理交互
        if (touchDuration < 500) {
            handleCellClick(e);
        }
    }, { passive: false });
    
    // 防止触摸移动时的误操作
    cell.addEventListener('touchmove', (e) => {
        const currentPos = {
            x: e.touches[0].clientX,
            y: e.touches[0].clientY
        };
        
        const distance = Math.sqrt(
            Math.pow(currentPos.x - touchStartPos.x, 2) + 
            Math.pow(currentPos.y - touchStartPos.y, 2)
        );
        
        // 如果移动距离太大，取消视觉反馈
        if (distance > 20) {
            cell.style.backgroundColor = '';
        }
    }, { passive: true });
}

// 处理单元格交互
function handleCellInteraction(row, col) {
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);

    // 检查是否点击了特殊水果
    if (gameState.grid[row][col]) {
        const fruit = gameState.grid[row][col];
        if (fruit.type === 'bomb_fruit') {
            triggerSpecialBombEffect(row, col);
            return;
        }
        if (fruit.type === 'lightning_fruit') {
            triggerSpecialLightningEffect(row, col);
            return;
        }
    }
    
    // 如果有激活的道具
    if (gameState.activePowerUp) {
        usePowerUp(gameState.activePowerUp, row, col);
        gameState.activePowerUp = null;
        
        // 移除道具选择状态
        document.querySelectorAll('.power-up').forEach(p => p.classList.remove('active'));
        return;
    }
    
    // 正常交换逻辑
    if (gameState.selectedCell) {
        const [selectedRow, selectedCol] = gameState.selectedCell;
        
        // 检查是否是相邻单元格
        if (isAdjacent(selectedRow, selectedCol, row, col)) {
            attemptSwap(selectedRow, selectedCol, row, col);
        }
        
        // 清除选择
        clearSelection();
    } else {
        // 选择当前单元格
        gameState.selectedCell = [row, col];
        cell.classList.add('selected');
    }
}

// 检查是否相邻
function isAdjacent(row1, col1, row2, col2) {
    const rowDiff = Math.abs(row1 - row2);
    const colDiff = Math.abs(col1 - col2);
    return (rowDiff === 1 && colDiff === 0) || (rowDiff === 0 && colDiff === 1);
}

// 尝试交换
function attemptSwap(row1, col1, row2, col2) {
    // 临时交换
    const temp = gameState.grid[row1][col1];
    gameState.grid[row1][col1] = gameState.grid[row2][col2];
    gameState.grid[row2][col2] = temp;
    
    // 检查是否产生匹配
    const matches = findMatches();
    
    if (matches.length > 0) {
        // 有匹配，执行交换
        updateCellDisplay(row1, col1);
        updateCellDisplay(row2, col2);
        
        // 减少步数（练习模式除外）
        if (gameState.currentLevel !== 0) {
            gameState.moves--;
        }
        
        // 处理匹配
        setTimeout(() => {
            processMatches(matches);
        }, 300);
        
        // 播放交换音效
        gameState.playSound('match');
        
    } else {
        // 没有匹配，交换回来
        gameState.grid[row2][col2] = gameState.grid[row1][col1];
        gameState.grid[row1][col1] = temp;
        
        // 显示无效移动提示
        showMessage('无效移动！');
    }
    
    updateUI();
}

// 清除选择状态
function clearSelection() {
    document.querySelectorAll('.grid-cell').forEach(cell => {
        cell.classList.remove('selected');
    });
    gameState.selectedCell = null;
}

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
    const checked = new Set();
    
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
                        const key = `${row}-${i}`;
                        if (!checked.has(key)) {
                            matches.push({ row, col: i });
                            checked.add(key);
                        }
                    }
                }
                count = 1;
                currentType = gameState.grid[row][col].type;
            }
        }
        
        // 检查行末尾
        if (count >= 3) {
            for (let i = 8 - count; i < 8; i++) {
                const key = `${row}-${i}`;
                if (!checked.has(key)) {
                    matches.push({ row, col: i });
                    checked.add(key);
                }
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
                        const key = `${i}-${col}`;
                        if (!checked.has(key)) {
                            matches.push({ row: i, col });
                            checked.add(key);
                        }
                    }
                }
                count = 1;
                currentType = gameState.grid[row][col].type;
            }
        }
        
        // 检查列末尾
        if (count >= 3) {
            for (let i = 8 - count; i < 8; i++) {
                const key = `${i}-${col}`;
                if (!checked.has(key)) {
                    matches.push({ row: i, col });
                    checked.add(key);
                }
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
    const comboBonus = Math.min(gameState.combo * 5, 100); // 最大连击奖励100%
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
    if (matches.length > 0) {
        showScoreAnimation(finalScore, matches[0].row, matches[0].col);
    }
    
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
    
    // 添加动画
    const style = document.createElement('style');
    style.textContent = `
        @keyframes scoreFloat {
            0% { 
                opacity: 1; 
                transform: translateY(0) scale(1);
            }
            100% { 
                opacity: 0; 
                transform: translateY(-50px) scale(1.2);
            }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        scoreElement.remove();
        style.remove();
    }, 1000);
}

// 显示连击效果
function showComboEffect() {
    const gameGrid = document.getElementById('gameGrid');
    const comboElement = document.createElement('div');
    comboElement.className = 'combo-display';
    
    // 根据连击数显示不同的效果
    let comboText = `${gameState.combo}连击! `;
    if (gameState.combo >= 5) comboText += '💥💥💥💥💥';
    else if (gameState.combo >= 4) comboText += '☄️☄️☄️☄️';
    else if (gameState.combo >= 3) comboText += '❤️‍🔥❤️‍🔥❤️‍🔥';
    else if (gameState.combo >= 2) comboText += '🌋🌋';
    else comboText += '🔥🔥';
    
    comboElement.textContent = comboText;
    
    gameGrid.appendChild(comboElement);
    
    // 更新最大连击记录
    if (gameState.combo > gameState.maxCombo) {
        gameState.maxCombo = gameState.combo;
    }
    
    setTimeout(() => {
        if (comboElement.parentNode) {
            comboElement.remove();
        }
    }, 1000);
}

// 创建粒子效果
function createParticleEffect(row, col) {
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    if (!cell) return;
    
    const rect = cell.getBoundingClientRect();
    const colors = ['#ff6b6b', '#4ecdc4', '#45b7d1', '#96ceb4', '#feca57', '#ff9ff3'];
    
    for (let i = 0; i < 6; i++) {
        const particle = document.createElement('div');
        particle.className = 'particle';
        particle.style.cssText = `
            position: fixed;
            left: ${rect.left + rect.width / 2}px;
            top: ${rect.top + rect.height / 2}px;
            width: ${Math.random() * 6 + 4}px;
            height: ${Math.random() * 6 + 4}px;
            background: ${colors[Math.floor(Math.random() * colors.length)]};
            border-radius: 50%;
            pointer-events: none;
            z-index: 100;
            animation: particle-float 0.8s ease-out forwards;
        `;
        
        // 随机方向
        const angle = (Math.PI * 2 * i) / 6;
        const distance = Math.random() * 50 + 30;
        const endX = rect.left + rect.width / 2 + Math.cos(angle) * distance;
        const endY = rect.top + rect.height / 2 + Math.sin(angle) * distance;
        
        particle.style.setProperty('--end-x', endX + 'px');
        particle.style.setProperty('--end-y', endY + 'px');
        
        document.body.appendChild(particle);
        setTimeout(() => {
            if (particle.parentNode) particle.remove();
        }, 800);
    }
    
    // 添加粒子动画
    if (!document.querySelector('#particleStyle')) {
        const style = document.createElement('style');
        style.id = 'particleStyle';
        style.textContent = `
            @keyframes particle-float {
                0% {
                    opacity: 1;
                    transform: scale(1);
                }
                100% {
                    opacity: 0;
                    transform: scale(0) translate(var(--end-x, 0), var(--end-y, 0));
                }
            }
        `;
        document.head.appendChild(style);
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
                    
                    // 清除原位置
                    const oldCell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
                    if (oldCell) {
                        oldCell.innerHTML = '';
                        oldCell.style.background = '';
                    }
                }
                writeIndex--;
            }
        }
    }
}

// 补充空单元格
function fillEmptyCells() {
    let hasEmptyCells = false;
    
    for (let col = 0; col < 8; col++) {
        let writeIndex = 7; // 从底部开始写入
        
        // 先移动现有的苹果到底部
        for (let row = 7; row >= 0; row--) {
            if (gameState.grid[row][col] !== null) {
                if (writeIndex !== row) {
                    gameState.grid[writeIndex][col] = gameState.grid[row][col];
                    gameState.grid[row][col] = null;
                    updateCellDisplay(writeIndex, col);
                    hasEmptyCells = true;
                    
                    // 清除原位置
                    const oldCell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
                    if (oldCell) {
                        oldCell.innerHTML = '';
                        oldCell.style.background = '';
                    }
                }
                writeIndex--;
            }
        }
        
        // 填充顶部的空白位置，使用智能填充增加combo概率
        for (let row = 0; row <= writeIndex; row++) {
            const newApple = generateSmartApple(row, col);
            gameState.grid[row][col] = newApple;
            updateCellDisplay(row, col);
            hasEmptyCells = true;
            
            // 恢复背景色
            const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
            if (cell) {
                cell.style.background = '';
            }
        }
    }
    
    if (hasEmptyCells) {
        setTimeout(() => {
            const newMatches = findMatches();
            if (newMatches.length > 0) {
                processMatches(newMatches);
            } else {
                gameState.combo = 0;
                
                // 小概率触发幸运重排增加combo机会
                if (Math.random() < 0.08) {
                    setTimeout(() => {
                        triggerLuckyReshuffle();
                    }, 200);
                }
                
                checkLevelComplete();
                checkAchievements();
            }
        }, 300);
    }
}


// 继续第四部分...
// 道具系统
function setupPowerUpInteraction() {
    document.querySelectorAll('.power-up').forEach(powerUp => {
        // 移除旧的事件监听器
        powerUp.replaceWith(powerUp.cloneNode(true));
    });
    
    // 重新获取元素并绑定事件
    document.querySelectorAll('.power-up').forEach(powerUp => {
        const powerType = powerUp.dataset.power;
        
        // 统一的点击处理
        function handlePowerUpClick(e) {
            e.preventDefault();
            e.stopPropagation();
            
            if (!gameState.isGameActive || gameState.isPaused) return;
            
            const count = gameState.powerUps[powerType];
            if (count <= 0) {
                showMessage('道具已用完！');
                return;
            }
            
            // 切换道具状态
            if (gameState.activePowerUp === powerType) {
                gameState.activePowerUp = null;
                powerUp.classList.remove('active');
            } else {
                // 移除其他道具的激活状态
                document.querySelectorAll('.power-up').forEach(p => p.classList.remove('active'));
                gameState.activePowerUp = powerType;
                powerUp.classList.add('active');
                showMessage(`已选择${getPowerUpName(powerType)}道具，点击网格使用！`);
            }
        }
        
        // 鼠标事件
        powerUp.addEventListener('click', handlePowerUpClick);
        
        // 触摸事件
        let touchStartTime = 0;
        
        powerUp.addEventListener('touchstart', (e) => {
            e.preventDefault();
            touchStartTime = Date.now();
            powerUp.style.backgroundColor = '#e9ecef';
        }, { passive: false });
        
        powerUp.addEventListener('touchend', (e) => {
            e.preventDefault();
            powerUp.style.backgroundColor = '';
            
            const touchDuration = Date.now() - touchStartTime;
            if (touchDuration < 500) {
                handlePowerUpClick(e);
            }
        }, { passive: false });
    });
}

// 获取道具名称
function getPowerUpName(powerType) {
    const names = {
        bomb: '炸弹',
        lightning: '闪电',
        rainbow: '彩虹',
        hammer: '锤子',
        shuffle: '洗牌',
        time: '时光'
    };
    return names[powerType] || '未知道具';
}

// 使用道具
function usePowerUp(powerType, targetRow, targetCol) {
    if (gameState.powerUps[powerType] <= 0) {
        showMessage('道具数量不足！');
        return;
    }
    
    gameState.powerUps[powerType]--;
    gameState.playSound('powerUp');
    
    switch (powerType) {
        case 'bomb':
            useBomb(targetRow, targetCol);
            break;
        case 'lightning':
            useLightning(targetRow, targetCol);
            break;
        case 'rainbow':
            useRainbow(targetRow, targetCol);
            break;
        case 'hammer':
            useHammer(targetRow, targetCol);
            break;
        case 'shuffle':
            useShuffle();
            break;
        case 'time':
            useTime();
            break;
    }
    
    updatePowerUpUI();
}

// 炸弹道具 - 消除3x3范围
function useBomb(centerRow, centerCol) {
    const affectedCells = [];
    
    for (let row = Math.max(0, centerRow - 1); row <= Math.min(7, centerRow + 1); row++) {
        for (let col = Math.max(0, centerCol - 1); col <= Math.min(7, centerCol + 1); col++) {
            if (gameState.grid[row][col]) {
                affectedCells.push({ row, col });
            }
        }
    }
    
    // 创建爆炸效果
    createBombEffect(centerRow, centerCol);
    
    // 延迟处理消除
    setTimeout(() => {
        affectedCells.forEach(cell => {
            createParticleEffect(cell.row, cell.col);
            gameState.grid[cell.row][cell.col] = null;
            
            const cellElement = document.querySelector(`[data-row="${cell.row}"][data-col="${cell.col}"]`);
            if (cellElement) {
                cellElement.innerHTML = '';
                cellElement.style.background = '#f0f0f0';
            }
        });
        
        // 计算得分
        const score = affectedCells.length * 15;
        gameState.score += score;
        showScoreAnimation(score, centerRow, centerCol);
        
        // 处理下落
        setTimeout(() => {
            dropCells();
            setTimeout(() => {
                fillEmptyCells();
                checkForMatches();
            }, 300);
        }, 300);
        
    }, 500);
}

// 闪电道具 - 消除整行和整列
function useLightning(targetRow, targetCol) {
    const affectedCells = [];
    
    // 消除整行
    for (let col = 0; col < 8; col++) {
        if (gameState.grid[targetRow][col]) {
            affectedCells.push({ row: targetRow, col });
        }
    }
    
    // 消除整列
    for (let row = 0; row < 8; row++) {
        if (gameState.grid[row][targetCol] && row !== targetRow) {
            affectedCells.push({ row, col: targetCol });
        }
    }
    
    // 创建闪电效果
    createLightningEffect(targetRow, targetCol);
    
    setTimeout(() => {
        affectedCells.forEach(cell => {
            createParticleEffect(cell.row, cell.col);
            gameState.grid[cell.row][cell.col] = null;
            
            const cellElement = document.querySelector(`[data-row="${cell.row}"][data-col="${cell.col}"]`);
            if (cellElement) {
                cellElement.innerHTML = '';
                cellElement.style.background = '#f0f0f0';
            }
        });
        
        const score = affectedCells.length * 20;
        gameState.score += score;
        showScoreAnimation(score, targetRow, targetCol);
        
        setTimeout(() => {
            dropCells();
            setTimeout(() => {
                fillEmptyCells();
                checkForMatches();
            }, 300);
        }, 300);
        
    }, 800);
}

// 彩虹道具 - 消除同类型所有苹果
function useRainbow(targetRow, targetCol) {
    const targetType = gameState.grid[targetRow][targetCol]?.type;
    if (!targetType) return;
    
    const affectedCells = [];
    
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            if (gameState.grid[row][col]?.type === targetType) {
                affectedCells.push({ row, col });
            }
        }
    }
    
    // 创建彩虹效果
    createRainbowEffect();
    
    setTimeout(() => {
        affectedCells.forEach(cell => {
            createParticleEffect(cell.row, cell.col);
            gameState.grid[cell.row][cell.col] = null;
            
            const cellElement = document.querySelector(`[data-row="${cell.row}"][data-col="${cell.col}"]`);
            if (cellElement) {
                cellElement.innerHTML = '';
                cellElement.style.background = '#f0f0f0';
            }
        });
        
        const score = affectedCells.length * 25;
        gameState.score += score;
        showScoreAnimation(score, targetRow, targetCol);
        
        setTimeout(() => {
            dropCells();
            setTimeout(() => {
                fillEmptyCells();
                checkForMatches();
            }, 300);
        }, 300);
        
    }, 1000);
}

// 锤子道具 - 消除单个苹果
function useHammer(targetRow, targetCol) {
    if (!gameState.grid[targetRow][targetCol]) return;
    
    createParticleEffect(targetRow, targetCol);
    gameState.grid[targetRow][targetCol] = null;
    
    const cellElement = document.querySelector(`[data-row="${targetRow}"][data-col="${targetCol}"]`);
    if (cellElement) {
        cellElement.innerHTML = '';
        cellElement.style.background = '#f0f0f0';
    }
    
    gameState.score += 10;
    showScoreAnimation(10, targetRow, targetCol);
    
    setTimeout(() => {
        dropCells();
        setTimeout(() => {
            fillEmptyCells();
            checkForMatches();
        }, 300);
    }, 300);
}

// 洗牌道具 - 重新排列网格
function useShuffle() {
    const allApples = [];
    
    // 收集所有苹果
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            if (gameState.grid[row][col]) {
                allApples.push(gameState.grid[row][col]);
            }
        }
    }
    
    // 洗牌
    for (let i = allApples.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [allApples[i], allApples[j]] = [allApples[j], allApples[i]];
    }
    
    // 重新分配
    let appleIndex = 0;
    for (let row = 0; row < 8; row++) {
        for (let col = 0; col < 8; col++) {
            if (appleIndex < allApples.length) {
                gameState.grid[row][col] = allApples[appleIndex++];
            } else {
                gameState.grid[row][col] = createRandomApple();
            }
            updateCellDisplay(row, col);
        }
    }
    
    // 创建洗牌动画效果
    createShuffleEffect();
    showMessage('网格已重新洗牌！');
    
    setTimeout(checkForMatches, 1000);
}

// 时光道具 - 增加步数
function useTime() {
    if (gameState.currentLevel === 0) {
        showMessage('练习模式无需增加步数！');
        return;
    }
    
    const bonusMoves = 5;
    gameState.moves += bonusMoves;
    
    createTimeEffect();
    showMessage(`获得额外${bonusMoves}步！`);
    updateUI();
}

// 道具效果动画
function createBombEffect(centerRow, centerCol) {
    const cell = document.querySelector(`[data-row="${centerRow}"][data-col="${centerCol}"]`);
    if (!cell) return;
    
    const explosion = document.createElement('div');
    explosion.innerHTML = '💥';
    explosion.style.cssText = `
        position: absolute;
        font-size: 3rem;
        z-index: 200;
        animation: explode 0.5s ease-out forwards;
        pointer-events: none;
    `;
    
    cell.appendChild(explosion);
    
    const style = document.createElement('style');
    style.textContent = `
        @keyframes explode {
            0% { transform: scale(0); opacity: 1; }
            50% { transform: scale(1.5); opacity: 1; }
            100% { transform: scale(2); opacity: 0; }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        explosion.remove();
        style.remove();
    }, 500);
}

function createLightningEffect(targetRow, targetCol) {
    const gameGrid = document.getElementById('gameGrid');
    
    // 垂直闪电
    const vLightning = document.createElement('div');
    vLightning.style.cssText = `
        position: absolute;
        left: ${(targetCol * 12.5)}%;
        top: 0;
        width: 12.5%;
        height: 100%;
        background: linear-gradient(180deg, #ffff00, #ffffff, #ffff00);
        z-index: 150;
        opacity: 0.8;
        animation: lightning 0.8s ease-out forwards;
        pointer-events: none;
    `;
    
    // 水平闪电
    const hLightning = document.createElement('div');
    hLightning.style.cssText = `
        position: absolute;
        left: 0;
        top: ${(targetRow * 12.5)}%;
        width: 100%;
        height: 12.5%;
        background: linear-gradient(90deg, #ffff00, #ffffff, #ffff00);
        z-index: 150;
        opacity: 0.8;
        animation: lightning 0.8s ease-out forwards;
        pointer-events: none;
    `;
    
    gameGrid.appendChild(vLightning);
    gameGrid.appendChild(hLightning);
    
    const style = document.createElement('style');
    style.textContent = `
        @keyframes lightning {
            0% { opacity: 0; }
            20% { opacity: 1; }
            40% { opacity: 0.2; }
            60% { opacity: 1; }
            80% { opacity: 0.3; }
            100% { opacity: 0; }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        vLightning.remove();
        hLightning.remove();
        style.remove();
    }, 800);
}

function createRainbowEffect() {
    const gameGrid = document.getElementById('gameGrid');
    const rainbow = document.createElement('div');
    rainbow.style.cssText = `
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(45deg, 
            #ff0000, #ff7f00, #ffff00, #00ff00, 
            #0000ff, #4b0082, #9400d3);
        z-index: 150;
        opacity: 0;
        animation: rainbow 1s ease-in-out forwards;
        pointer-events: none;
    `;
    
    gameGrid.appendChild(rainbow);
    
    const style = document.createElement('style');
    style.textContent = `
        @keyframes rainbow {
            0% { opacity: 0; }
            50% { opacity: 0.6; }
            100% { opacity: 0; }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        rainbow.remove();
        style.remove();
    }, 1000);
}

function createShuffleEffect() {
    const gameGrid = document.getElementById('gameGrid');
    gameGrid.style.animation = 'shake 0.5s ease-in-out';
    
    const style = document.createElement('style');
    style.textContent = `
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        gameGrid.style.animation = '';
        style.remove();
    }, 500);
}

function createTimeEffect() {
    const gameGrid = document.getElementById('gameGrid');
    const timeRipple = document.createElement('div');
    timeRipple.innerHTML = '⏰';
    timeRipple.style.cssText = `
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        font-size: 4rem;
        z-index: 200;
        animation: timeRipple 1s ease-out forwards;
        pointer-events: none;
    `;
    
    gameGrid.appendChild(timeRipple);
    
    const style = document.createElement('style');
    style.textContent = `
        @keyframes timeRipple {
            0% { 
                transform: translate(-50%, -50%) scale(0); 
                opacity: 1; 
            }
            50% { 
                transform: translate(-50%, -50%) scale(1.2); 
                opacity: 0.8; 
            }
            100% { 
                transform: translate(-50%, -50%) scale(2); 
                opacity: 0; 
            }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        timeRipple.remove();
        style.remove();
    }, 1000);
}


// 特殊炸弹水果效果
function triggerSpecialBombEffect(row, col) {
    // 创建超级爆炸动画
    const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
    if (cell) {
        const explosion = document.createElement('div');
        explosion.innerHTML = '💥';
        explosion.style.cssText = `
            position: absolute;
            font-size: 4rem;
            z-index: 300;
            animation: superExplode 1.2s ease-out forwards;
            pointer-events: none;
        `;
        cell.appendChild(explosion);
        
        // 添加震屏效果
        document.body.style.animation = 'screenShake 0.5s ease-in-out';
    }
    
    // 消除3x3范围
    const affectedCells = [];
    for (let r = Math.max(0, row - 1); r <= Math.min(7, row + 1); r++) {
        for (let c = Math.max(0, col - 1); c <= Math.min(7, col + 1); c++) {
            if (gameState.grid[r][c]) {
                affectedCells.push({ row: r, col: c });
            }
        }
    }
    
    // 添加爆炸样式
    const style = document.createElement('style');
    style.textContent = `
        @keyframes superExplode {
            0% { transform: scale(0); opacity: 1; }
            30% { transform: scale(2); opacity: 1; }
            60% { transform: scale(3); opacity: 0.8; }
            100% { transform: scale(4); opacity: 0; }
        }
        @keyframes screenShake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        affectedCells.forEach(cell => {
            createParticleEffect(cell.row, cell.col);
            gameState.grid[cell.row][cell.col] = null;
            
            const cellElement = document.querySelector(`[data-row="${cell.row}"][data-col="${cell.col}"]`);
            if (cellElement) {
                cellElement.innerHTML = '';
                cellElement.style.background = '#f0f0f0';
            }
        });
        
        const score = affectedCells.length * 30;
        gameState.score += score;
        showScoreAnimation(score, row, col);
        
        document.body.style.animation = '';
        
        setTimeout(() => {
            dropCells();
            setTimeout(() => {
                fillEmptyCells();
                checkForMatches();
            }, 300);
        }, 300);
        
        style.remove();
    }, 800);
    
    showMessage('💥 超级爆炸！Ashley的力量无人能敌！');
}

// 特殊闪电水果效果
function triggerSpecialLightningEffect(row, col) {
    // 创建超级闪电动画
    const gameGrid = document.getElementById('gameGrid');
    
    // X形闪电效果
    const lightning1 = document.createElement('div');
    lightning1.style.cssText = `
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(45deg, transparent 48%, #ffff00 49%, #ffffff 50%, #ffff00 51%, transparent 52%);
        z-index: 200;
        opacity: 0;
        animation: superLightning 1.5s ease-out forwards;
        pointer-events: none;
    `;
    
    const lightning2 = document.createElement('div');
    lightning2.style.cssText = `
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(-45deg, transparent 48%, #ffff00 49%, #ffffff 50%, #ffff00 51%, transparent 52%);
        z-index: 200;
        opacity: 0;
        animation: superLightning 1.5s ease-out forwards;
        pointer-events: none;
    `;
    
    gameGrid.appendChild(lightning1);
    gameGrid.appendChild(lightning2);
    
   // 消除以🌪为中心的5格X形对角线
    const affectedCells = [];
    const range = 2; // 每边延伸2格，总共5格
    
    // 左上到右下的对角线
    for (let offset = -range; offset <= range; offset++) {
        const r = row + offset;
        const c = col + offset;
        if (r >= 0 && r < 8 && c >= 0 && c < 8) {
            if (gameState.grid[r][c]) {
                affectedCells.push({ row: r, col: c });
            }
        }
    }
    
    // 左下到右上的对角线
    for (let offset = -range; offset <= range; offset++) {
        const r = row + offset;
        const c = col - offset;
        if (r >= 0 && r < 8 && c >= 0 && c < 8) {
            if (gameState.grid[r][c]) {
                affectedCells.push({ row: r, col: c });
            }
        }
    }
    
    // 添加闪电样式
    const style = document.createElement('style');
    style.textContent = `
        @keyframes superLightning {
            0% { opacity: 0; }
            10% { opacity: 1; }
            20% { opacity: 0.3; }
            30% { opacity: 1; }
            40% { opacity: 0.2; }
            50% { opacity: 1; }
            60% { opacity: 0.4; }
            70% { opacity: 1; }
            100% { opacity: 0; }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        affectedCells.forEach(cell => {
            createParticleEffect(cell.row, cell.col);
            gameState.grid[cell.row][cell.col] = null;
            
            const cellElement = document.querySelector(`[data-row="${cell.row}"][data-col="${cell.col}"]`);
            if (cellElement) {
                cellElement.innerHTML = '';
                cellElement.style.background = '#f0f0f0';
            }
        });
        
        const score = affectedCells.length * 25;
        gameState.score += score;
        showScoreAnimation(score, row, col);
        
        setTimeout(() => {
            dropCells();
            setTimeout(() => {
                fillEmptyCells();
                checkForMatches();
            }, 300);
        }, 300);
        
        lightning1.remove();
        lightning2.remove();
        style.remove();
    }, 1000);
    
    showMessage('🌪 X型风暴卷走一切，Ashley的能量满满！');
}
    
// 更新道具UI
function updatePowerUpUI() {
    Object.keys(gameState.powerUps).forEach(powerType => {
        const powerUpElement = document.querySelector(`[data-power="${powerType}"]`);
        if (powerUpElement) {
            const countElement = powerUpElement.querySelector('.count');
            if (countElement) {
                const count = gameState.powerUps[powerType];
                countElement.textContent = count;
                
                // 数量不足时的视觉效果
                if (count <= 0) {
                    powerUpElement.style.opacity = '0.5';
                    countElement.style.background = '#ccc';
                } else {
                    powerUpElement.style.opacity = '1';
                    countElement.style.background = '#ff6b6b';
                }
            }
        }
    });
    
    // 重新设置事件监听器
    setupPowerUpInteraction();
}

// 检查匹配（在道具使用后）
function checkForMatches() {
    const matches = findMatches();
    if (matches.length > 0) {
        setTimeout(() => processMatches(matches), 100);
    }
}

// 添加特殊道具到练习模式
function addRandomSpecialItems() {
    const specialPositions = [
        { row: 2, col: 2 },
        { row: 2, col: 5 },
        { row: 5, col: 2 },
        { row: 5, col: 5 }
    ];
    
    specialPositions.forEach(pos => {
        if (Math.random() > 0.7) { // 30%概率生成特殊道具
            const specialItem = {
                type: 'special',
                emoji: ['⭐', '💎', '🔥', '✨'][Math.floor(Math.random() * 4)],
                class: 'special-item'
            };
            
            gameState.grid[pos.row][pos.col] = specialItem;
            updateCellDisplay(pos.row, pos.col);
            
            // 添加特殊发光效果
            const cell = document.querySelector(`[data-row="${pos.row}"][data-col="${pos.col}"]`);
            if (cell) {
                cell.classList.add('special-item');
            }
        }
    });
}

// 检查关卡完成
function checkLevelComplete() {
    if (gameState.currentLevel === 0) return; // 练习模式无需检查
    
    if (gameState.score >= gameState.target) {
        // 胜利
        setTimeout(() => {
            showLevelComplete(true);
        }, 500);
    } else if (gameState.moves <= 0) {
        // 失败
        setTimeout(() => {
            showLevelComplete(false);
        }, 500);
    }
}

// 显示关卡完成界面
function showLevelComplete(success) {
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
        animation: fadeIn 0.5s ease-out;
    `;
    
    const currentLevel = LEVELS.find(l => l.id === gameState.currentLevel);
    
    if (success) {
        // 胜利界面
        overlay.innerHTML = `
            <div style="background: linear-gradient(135deg, #4CAF50, #45a049); 
                        color: white; padding: 2rem; border-radius: 20px; text-align: center; 
                        max-width: 90vw; animation: successBounce 0.6s ease-out;">
                <h2 style="margin-bottom: 1rem;">🎉 关卡完成！</h2>
                <div style="font-size: 1.2rem; margin-bottom: 1rem;">
                    ${currentLevel ? `"${currentLevel.quote}"` : ''}
                </div>
                <div style="margin-bottom: 2rem;">
                    <div>得分: ${gameState.score} / ${gameState.target}</div>
                    <div>剩余步数: ${gameState.moves}</div>
                    <div>最高连击: ${gameState.maxCombo}</div>
                </div>
                <div style="display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;">
                    <button onclick="handleNextLevel(this);" 
                            style="padding: 1rem 2rem; background: rgba(255,255,255,0.2); 
                                   color: white; border: 2px solid white; border-radius: 25px; 
                                   cursor: pointer; font-size: 1rem; touch-action: manipulation;">
                        ${gameState.currentLevel < LEVELS.length ? '下一关 ▶️' : '返回选关 🏠'}
                    </button>
                    <button onclick="handleRestartLevel(this);"
                            style="padding: 1rem 2rem; background: rgba(255,255,255,0.2); 
                                   color: white; border: 2px solid white; border-radius: 25px; 
                                   cursor: pointer; font-size: 1rem;">
                        重新挑战 🔄
                    </button>
                </div>
            </div>
        `;
        
        // 庆祝效果
        createCelebrationEffect();
        
    } else {
        // 失败界面
        overlay.innerHTML = `
            <div style="background: linear-gradient(135deg, #f44336, #d32f2f); 
                        color: white; padding: 2rem; border-radius: 20px; text-align: center; 
                        max-width: 90vw;">
                <h2 style="margin-bottom: 1rem;">😔 挑战失败</h2>
                <div style="font-size: 1.1rem; margin-bottom: 1rem;">
                    别灰心，再试一次！
                </div>
                <div style="margin-bottom: 2rem;">
                    <div>得分: ${gameState.score} / ${gameState.target}</div>
                    <div>差距: ${gameState.target - gameState.score}</div>
                </div>
                <div style="display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;">
                    <button onclick="restartLevel(); this.parentElement.parentElement.parentElement.remove();" 
                            style="padding: 1rem 2rem; background: rgba(255,255,255,0.2); 
                                   color: white; border: 2px solid white; border-radius: 25px; 
                                   cursor: pointer; font-size: 1rem;">
                        重新挑战 🔄
                    </button>
                    <button onclick="backToLevelSelect(); this.parentElement.parentElement.parentElement.remove();" 
                            style="padding: 1rem 2rem; background: rgba(255,255,255,0.2); 
                                   color: white; border: 2px solid white; border-radius: 25px; 
                                   cursor: pointer; font-size: 1rem;">
                        返回选关 ⬅️
                    </button>
                </div>
            </div>
        `;
    }
    
    document.body.appendChild(overlay);
    
    // 添加动画样式
    const style = document.createElement('style');
    style.textContent = `
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        @keyframes successBounce {
            0% { transform: scale(0.3); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => style.remove(), 2000);
    
    // 更新游戏统计
    gameState.gamesPlayed++;
    if (success) {
        gameState.totalScore += gameState.score;
    }
    saveGameData();
}

// 处理重新挑战
function handleRestart() {
    const overlay = document.querySelector('div[style*="position: fixed"]');
    if (overlay) overlay.remove();
    setTimeout(() => {
        startLevel(gameState.currentLevel);
    }, 100);
}

// 处理下一关
function handleNextLevel() {
    const overlay = document.querySelector('div[style*="position: fixed"]');
    if (overlay) overlay.remove();
    setTimeout(() => {
        if (gameState.currentLevel < LEVELS.length) {
            nextLevel();
        } else {
            backToLevelSelect();
        }
    }, 100);
}

// 处理下一关
function handleNextLevel(button) {
    // 防止重复点击
    if (button.clicked) return;
    button.clicked = true;
    
    // 改变重新挑战按钮的文字为"进入游戏"
    const restartButton = button.parentElement.querySelector('button:last-child');
    if (restartButton) {
        restartButton.innerHTML = '进入游戏 🎮';
    }
    
    // 执行下一关逻辑（背景会切换到下一关）
    setTimeout(function() {
        if (gameState.currentLevel < LEVELS.length) {
            gameState.currentLevel++;
            startLevel(gameState.currentLevel);
        } else {
            backToLevelSelect();
        }
    }, 100);
}

    
// 创建庆祝效果
function createCelebrationEffect() {
    for (let i = 0; i < 50; i++) {
        setTimeout(() => {
            const confetti = document.createElement('div');
            confetti.innerHTML = ['🎊', '🎉', '✨', '🌟', '💫'][Math.floor(Math.random() * 5)];
            confetti.style.cssText = `
                position: fixed;
                left: ${Math.random() * 100}%;
                top: -50px;
                font-size: ${Math.random() * 20 + 10}px;
                z-index: 999;
                animation: confettiFall ${Math.random() * 3 + 2}s linear forwards;
                pointer-events: none;
            `;
            
            document.body.appendChild(confetti);
            
            setTimeout(() => {
                if (confetti.parentNode) confetti.remove();
            }, 5000);
        }, i * 100);
    }
    
    // 添加庆祝动画
    const style = document.createElement('style');
    style.textContent = `
        @keyframes confettiFall {
            0% {
                transform: translateY(0) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(calc(100vh + 50px)) rotate(360deg);
                opacity: 0;
            }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => style.remove(), 8000);
}
// 下一关
function nextLevel() {
    if (gameState.currentLevel < LEVELS.length) {
        startLevel(gameState.currentLevel + 1);
    } else {
        backToLevelSelect();
        showMessage('🎉 恭喜完成所有关卡！');
    }
}

// 成就系统
function checkAchievements() {
    const newAchievements = [];
    
    // 检查各种成就条件
    if (gameState.totalMatches >= 1 && !gameState.achievements.has('first_match')) {
        newAchievements.push('first_match');
    }
    
    if (gameState.maxCombo >= 10 && !gameState.achievements.has('combo_master')) {
        newAchievements.push('combo_master');
    }
    
    if (gameState.score >= 5000 && !gameState.achievements.has('score_hunter')) {
        newAchievements.push('score_hunter');
    }
    
    if (gameState.moves >= 200 && gameState.score >= gameState.target && !gameState.achievements.has('perfect_level')) {
        newAchievements.push('perfect_level');
        gameState.perfectGames++;
    }
    
    // 检查是否使用过所有道具
    const usedAllPowerUps = Object.values(gameState.powerUps).every(count => count < 40);
    if (usedAllPowerUps && !gameState.achievements.has('power_master')) {
        newAchievements.push('power_master');
    }
    
    // 特殊成就 - Ashley专属
    const completedSpecialLevels = LEVELS.filter(l => l.special).every(level => 
        gameState.currentLevel >= level.id
    );
    if (completedSpecialLevels && !gameState.achievements.has('love_master')) {
        newAchievements.push('love_master');
    }
    
    // 显示新获得的成就
    newAchievements.forEach(achievementId => {
        gameState.achievements.add(achievementId);
        const achievement = ACHIEVEMENTS.find(a => a.id === achievementId);
        if (achievement) {
            setTimeout(() => {
                showAchievement(achievement);
            }, Math.random() * 2000);
        }
    });
    
    saveGameData();
}

// 显示成就弹窗
function showAchievement(achievement) {
    const popup = document.getElementById('achievementPopup');
    const text = document.getElementById('achievementText');
    
    text.innerHTML = `
        <div style="font-size: 1.5rem; margin-bottom: 0.5rem;">${achievement.icon}</div>
        <div style="font-weight: bold; margin-bottom: 0.2rem;">${achievement.name}</div>
        <div style="font-size: 0.9rem;">${achievement.desc}</div>
    `;
    
    popup.classList.add('show');
    
    // 播放成就音效
    gameState.playSound('powerUp');
    
    setTimeout(() => {
        popup.classList.remove('show');
    }, 4000);
}

// 界面控制函数
function showMainMenu() {
    document.getElementById('mainMenu').style.display = 'flex';
    document.getElementById('levelSelect').style.display = 'none';
    document.getElementById('gameScreen').style.display = 'none';
    document.getElementById('pauseMenu').style.display = 'none';
}

function showLevelSelect() {
    document.getElementById('mainMenu').style.display = 'none';
    document.getElementById('levelSelect').style.display = 'block';
    document.getElementById('gameScreen').style.display = 'none';
    document.getElementById('pauseMenu').style.display = 'none';
}

function showGameScreen() {
    document.getElementById('mainMenu').style.display = 'none';
    document.getElementById('levelSelect').style.display = 'none';
    document.getElementById('gameScreen').style.display = 'block';
    document.getElementById('pauseMenu').style.display = 'none';
}

// 更新游戏UI
function updateUI() {
    document.getElementById('currentLevel').textContent = 
        gameState.currentLevel === 0 ? '练习' : gameState.currentLevel;
    document.getElementById('score').textContent = gameState.score;
    document.getElementById('target').textContent = 
        gameState.currentLevel === 0 ? '∞' : gameState.target;
    document.getElementById('moves').textContent = 
        gameState.currentLevel === 0 ? '∞' : gameState.moves;
    
    updatePowerUpUI();
}

// 游戏控制函数
function pauseGame() {
    if (!gameState.isGameActive) return;
    
    gameState.isPaused = true;
    document.getElementById('pauseMenu').style.display = 'flex';
}

function resumeGame() {
    gameState.isPaused = false;
    document.getElementById('pauseMenu').style.display = 'none';
}

function restartLevel() {
    if (gameState.currentLevel === 0) {
        startLevel(0); // 重新开始练习模式
    } else {
        startLevel(gameState.currentLevel);
    }
    resumeGame();
}

function backToLevelSelect() {
    showLevelSelect();
    gameState.isGameActive = false;
    gameState.isPaused = false;
}

function backToMainMenu() {
    showMainMenu();
    gameState.isGameActive = false;
    gameState.isPaused = false;
}

// 提示功能
function showHint() {
    if (gameState.currentLevel === 0) {
        showMessage('练习模式：尝试使用各种道具组合！');
        return;
    }
    
    // 简单的提示逻辑
    const possibleMoves = findPossibleMoves();
    
    if (possibleMoves.length > 0) {
        const randomMove = possibleMoves[Math.floor(Math.random() * possibleMoves.length)];
        const { row1, col1, row2, col2 } = randomMove;
        
        // 高亮提示的位置
        const cell1 = document.querySelector(`[data-row="${row1}"][data-col="${col1}"]`);
        const cell2 = document.querySelector(`[data-row="${row2}"][data-col="${col2}"]`);
        
        if (cell1 && cell2) {
            cell1.style.border = '3px solid #ffc107';
            cell2.style.border = '3px solid #ffc107';
            
            setTimeout(() => {
                cell1.style.border = '';
                cell2.style.border = '';
            }, 2000);
        }
        
        showMessage('💡 试试这里！');
    } else {
        showMessage('没有可行的移动，试试使用道具！');
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
                    moves.push({ row1: row, col1: col, row2: row, col2: col + 1 });
                }
            }
            // 检查下边
            if (row < 7) {
                if (wouldCreateMatch(row, col, row + 1, col)) {
                    moves.push({ row1: row, col1: col, row2: row + 1, col2: col });
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
    
    const hasMatch = findMatches().length > 0;
    
    // 交换回来
    gameState.grid[row2][col2] = gameState.grid[row1][col1];
    gameState.grid[row1][col1] = temp;
    
    return hasMatch;
}

// 显示消息 - 优化版本（原配色+响应式布局）
function showMessage(message) {
    // 移除可能存在的旧消息框
    const existingMessage = document.getElementById('specialMessage');
    if (existingMessage) {
        existingMessage.remove();
    }
    
    // 检测屏幕尺寸
    const isMobile = window.innerWidth <= 768;
    const isSmallMobile = window.innerWidth <= 480;
    
    // 创建消息框
    const messageBox = document.createElement('div');
    messageBox.id = 'specialMessage';
    
    // 根据屏幕大小设置样式
    const boxWidth = isSmallMobile ? '90%' : (isMobile ? '85%' : '60%');
    const maxWidth = isSmallMobile ? '320px' : (isMobile ? '400px' : '500px');
    const fontSize = isSmallMobile ? '14px' : (isMobile ? '16px' : '18px');
    const padding = isSmallMobile ? '20px' : (isMobile ? '25px' : '30px');
    
    messageBox.style.cssText = `
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: rgba(0, 0, 0, 0.6);
        color: white;
        padding: ${padding};
        border-radius: 20px;
        font-size: ${fontSize};
        text-align: center;
        box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        z-index: 10000;
        width: ${boxWidth};
        max-width: ${maxWidth};
        max-height: 70vh;
        overflow-y: auto;
        animation: messagePopIn 0.5s ease-out;
        line-height: 1.6;
        pointer-events: auto;
        border: 2px solid rgba(255,255,255,0.1);
        backdrop-filter: blur(10px);
    `;
    
    // 创建关闭按钮
    const closeButton = document.createElement('button');
    closeButton.innerHTML = '✕';
    const buttonSize = isSmallMobile ? '16px' : '18px';
    const buttonTop = isSmallMobile ? '8px' : '10px';
    const buttonRight = isSmallMobile ? '12px' : '15px';
    
    closeButton.style.cssText = `
        position: absolute;
        top: ${buttonTop};
        right: ${buttonRight};
        background: rgba(255,255,255,0.1);
        border: none;
        color: white;
        font-size: ${buttonSize};
        cursor: pointer;
        padding: 6px;
        border-radius: 50%;
        transition: all 0.3s;
        touch-action: manipulation;
        width: 28px;
        height: 28px;
        display: flex;
        align-items: center;
        justify-content: center;
        line-height: 1;
    `;
    
    // 关闭按钮悬停效果
    closeButton.onmouseover = () => {
        closeButton.style.backgroundColor = 'rgba(255,255,255,0.2)';
        closeButton.style.transform = 'scale(1.1)';
    };
    closeButton.onmouseout = () => {
        closeButton.style.backgroundColor = 'rgba(255,255,255,0.1)';
        closeButton.style.transform = 'scale(1)';
    };
    
    // 点击关闭
    closeButton.onclick = () => {
        messageBox.style.animation = 'messagePopOut 0.3s ease-in forwards';
        setTimeout(() => messageBox.remove(), 300);
    };
    
    // 触摸关闭
    closeButton.ontouchend = (e) => {
        e.preventDefault();
        messageBox.style.animation = 'messagePopOut 0.3s ease-in forwards';
        setTimeout(() => messageBox.remove(), 300);
    };
    
    // 添加消息文本
    const messageText = document.createElement('div');
    messageText.innerHTML = message.replace(/\n/g, '<br>');
    messageText.style.cssText = `
        padding-right: ${isSmallMobile ? '35px' : '40px'};
        word-wrap: break-word;
        word-break: break-word;
    `;
    
    messageBox.appendChild(messageText);
    messageBox.appendChild(closeButton);
    
    // 添加动画样式
    const style = document.createElement('style');
    style.textContent = `
        @keyframes messagePopIn {
            0% {
                transform: translate(-50%, -50%) scale(0.5);
                opacity: 0;
            }
            100% {
                transform: translate(-50%, -50%) scale(1);
                opacity: 1;
            }
        }
        @keyframes messagePopOut {
            0% {
                transform: translate(-50%, -50%) scale(1);
                opacity: 1;
            }
            100% {
                transform: translate(-50%, -50%) scale(0.5);
                opacity: 0;
            }
        }
    `;
    document.head.appendChild(style);
    
    document.body.appendChild(messageBox);
    
    // 20秒后自动关闭
    setTimeout(() => {
        if (messageBox.parentNode) {
            messageBox.style.animation = 'messagePopOut 0.3s ease-in forwards';
            setTimeout(() => {
                messageBox.remove();
                style.remove();
            }, 300);
        }
    }, 20000);
}

// 菜单功能
function showAchievements() {
    // 创建成就弹窗
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
        <div style="background: linear-gradient(135deg, #6a11cb, #2575fc); 
                    color: white; padding: 2rem; border-radius: 20px; 
                    max-width: 90vw; max-height: 90vh; overflow-y: auto;">
            <h2 style="text-align: center; margin-bottom: 1.5rem;">🏆 成就系统 🏆</h2>
            
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); 
                        gap: 1rem; margin-bottom: 2rem;">
                ${ACHIEVEMENTS.map(achievement => {
                    const unlocked = gameState.achievements.has(achievement.id);
                    return `
                        <div style="background: rgba(255, 255, 255, ${unlocked ? '0.15' : '0.1'}); 
                                    padding: 1rem; border-radius: 15px; text-align: center;">
                            <div style="font-size: 2rem;">${unlocked ? achievement.icon : '🔒'}</div>
                            <div style="font-weight: bold; margin: 0.5rem 0;">${achievement.name}</div>
                            <div style="font-size: 0.9rem; opacity: 0.9;">${achievement.desc}</div>
                            <div style="margin-top: 0.5rem; font-size: 0.8rem; opacity: 0.7;">
                                ${unlocked ? '已解锁' : '未解锁'}
                            </div>
                        </div>
                    `;
                }).join('')}
            </div>
            
            <div style="background: rgba(255, 255, 255, 0.1); padding: 1rem; border-radius: 15px; 
                        margin-bottom: 1.5rem;">
                <h3 style="text-align: center; margin-bottom: 1rem;">📊 游戏统计</h3>
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 0.5rem;">
                    <div>游戏局数:</div>
                    <div style="text-align: right;">${gameState.gamesPlayed}</div>
                    <div>总得分:</div>
                    <div style="text-align: right;">${gameState.totalScore}</div>
                    <div>完美通关:</div>
                    <div style="text-align: right;">${gameState.perfectGames}</div>
                    <div>最高连击:</div>
                    <div style="text-align: right;">${gameState.maxCombo}</div>
                    <div>总消除数:</div>
                    <div style="text-align: right;">${gameState.totalMatches}</div>
                </div>
            </div>
            
            <div style="display: flex; justify-content: center; gap: 1rem;">
                <button onclick="this.parentElement.parentElement.parentElement.remove();" 
                        style="padding: 0.8rem 1.5rem; background: rgba(255,255,255,0.2); 
                               color: white; border: 2px solid white; border-radius: 25px; 
                               cursor: pointer;">
                    关闭
                </button>
                <button onclick="resetAchievements(); this.parentElement.parentElement.parentElement.remove();" 
                        style="padding: 0.8rem 1.5rem; background: rgba(255,0,0,0.3); 
                               color: white; border: 2px solid #ff6b6b; border-radius: 25px; 
                               cursor: pointer;">
                    重置成就
                </button>
            </div>
        </div>
    `;
    
    document.body.appendChild(overlay);
}

// 添加这个新函数到代码中
function resetAchievements() {
    if (confirm("确定要清空所有成就和游戏记录吗？此操作不可撤销！")) {
        // 重置成就数据
        gameState.achievements = new Set();
        gameState.totalScore = 0;
        gameState.gamesPlayed = 0;
        gameState.perfectGames = 0;
        gameState.maxCombo = 0;
        gameState.totalMatches = 0;
        
        // 清除本地存储
        localStorage.removeItem('appleGameSave');
        
        // 显示成功消息
        showMessage("🎮 所有成就和记录已重置！");
        
        // 重新加载页面以应用更改
        setTimeout(() => location.reload(), 2000);
    }
}

function showLoveMessages() {
    const loveMessages = [
        "💕 Ashley，你知道吗？每次看到你的笑容，我的世界都变得明亮起来",
        "🌟 这个游戏里的每一关，都代表着我对你的一份爱意",
        "💖 就像消除游戏一样，我想要消除你所有的烦恼，只留下快乐",
        "🍎 红苹果代表我的心，绿苹果代表我们的希望，彩虹苹果代表我们美好的未来",
        "✨ 3月25日是你的生日，但对我来说，每一天都是因为有你而值得庆祝的日子",
        "💫 无论游戏有多少关卡，我的爱意永远不会有终点",
        "🌈 愿我们的爱情像彩虹一样，绚烂而永恒",
        "👑 Ashley，你就是我心中的女王，这个游戏献给最美丽的你",
        "👀 Ashley，你的一个眼神，就能让我的心跳像游戏连击一样加速跳动！",
        "🌟 收集游戏里的每一颗星星，都不及你在我生命里闪耀的万分之一光芒",
        "🏆 遇见你，就像找到了游戏里最稀有的隐藏道具，是我生命中最珍贵的幸运",
        "⏳ 和你在一起的每一刻，都像是游戏通关时的完美动画，充满喜悦与满足",
        "🎉 我的爱就像无限续命的道具，永远为你准备着，Ashley",
        "🧱 无论生活抛出多少“障碍砖块”，我都会像最熟练的玩家一样，为你铺平道路，因为你就是我的终极目标",
        "👸 Ashley，你不仅是我心中的女王，更是我生命这场游戏里唯一的、永恒的MVP",
        "💗 我们的爱情故事，是我最引以为傲的“成就系统”，而每一天和你在一起，都在解锁新的甜蜜勋章",
        "🎮 生活这场游戏或许有挑战，但牵着你的手，就像拥有了无敌模式，无所畏惧",
        "🍀 亲爱的Ashley，你是我所有好运的来源，比任何游戏里的四叶草都要灵验",
        "💖 想你的心情，就像等待游戏加载时的期待，每一次“进入游戏”（见到你）都让我怦然心动",
        "🌌 Ashley，你的笑容是我每日签到必领的最佳奖励，点亮我的整个世界",
        "🔮 我们的未来，就像精心设计的游戏关卡，充满未知的惊喜，而我迫不及待想和你一起探索每一关",
        "🔋 对你的爱意，永远满格，电量充足，Ashley，你是我永不掉线的连接",
        "💂 献给我最爱的Ashley：你让平凡的日子变成了史诗级的冒险，而我是你最忠诚的骑士",
        "🎇 和你在一起的每一刻，都像是达成游戏全成就时爆发的庆祝烟火，绚烂夺目，充满纯粹的幸福",
        "📇 想你的感觉，就像在玩一个停不下来的游戏，每一个操作键都刻着你的名字",
        "💌 Ashley，每次收到你的消息，都让我心跳加速，迫不及待点开"
    ];
    
    const randomMessage = loveMessages[Math.floor(Math.random() * loveMessages.length)];
    
    // 创建美丽的弹窗
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
        animation: fadeIn 0.5s ease-out;
    `;
    
    overlay.innerHTML = `
        <div style="background: linear-gradient(135deg, #ff9a9e, #fecfef); 
                    color: white; padding: 2rem; border-radius: 20px; text-align: center; 
                    max-width: 90vw; box-shadow: 0 10px 30px rgba(0,0,0,0.3);">
            <h2 style="margin-bottom: 1rem;">💕 专属情话</h2>
            <p style="font-size: 1.1rem; line-height: 1.6; margin-bottom: 2rem; font-style: italic;">
                ${randomMessage}
            </p>
            <button onclick="this.parentElement.parentElement.remove();" 
                    style="padding: 1rem 2rem; background: rgba(255,255,255,0.2); 
                           color: white; border: 2px solid white; border-radius: 25px; 
                           cursor: pointer; font-size: 1rem;">
                收到你的爱 💖
            </button>
        </div>
    `;
    
    document.body.appendChild(overlay);
    
    // 创建飘落的爱心
    for (let i = 0; i < 20; i++) {
        setTimeout(() => {
            const heart = document.createElement('div');
            heart.innerHTML = ['💕', '💖', '💗', '💝'][Math.floor(Math.random() * 4)];
            heart.style.cssText = `
                position: fixed;
                left: ${Math.random() * 100}%;
                top: -50px;
                font-size: ${Math.random() * 20 + 15}px;
                z-index: 999;
                animation: floatHeart 6s linear forwards;
                pointer-events: none;
            `;
            
            document.body.appendChild(heart);
            
            setTimeout(() => {
                if (heart.parentNode) heart.remove();
            }, 6000);
        }, i * 200);
    }
}

function showSettings() {
    const settings = `
    ⚙️ 游戏设置 ⚙️

    🎮 游戏说明:
    • 交换相邻的苹果来消除3个或更多相同的苹果
    • 达到目标分数即可过关
    • 使用道具帮助完成挑战

    💎 道具说明:
    💥 炸弹 - 消除3x3范围内的所有苹果
    ⚡ 闪电 - 消除整行和整列的苹果  
    🌈 彩虹 - 消除所有相同类型的苹果
    🔨 锤子 - 消除单个苹果
    🔄 洗牌 - 重新排列整个棋盘
    ⏰ 时光 - 增加5步额外步数
    🌪 风暴 - X型风暴卷走一切

    💕 特别提醒:
    这个游戏是专门为Ashley制作的，每一个细节都充满了爱意！
    
    💖 制作者的话:
    Ashley，希望你能喜欢这个小游戏，就像我喜欢你一样！
    `;
    
    alert(settings);
}

// 游戏内说明弹窗（保持游戏状态）
function showGameInstructions() {
    // 暂停游戏但不显示暂停菜单
    const wasGameActive = gameState.isGameActive;
    const wasPaused = gameState.isPaused;
    gameState.isPaused = true;
    
    // 创建说明弹窗
    const overlay = document.createElement('div');
    overlay.id = 'gameInstructionsOverlay';
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
        animation: fadeIn 0.3s ease-out;
    `;
    
    overlay.innerHTML = `
        <div style="background: linear-gradient(135deg, #667eea, #764ba2); 
                    color: white; padding: 2rem; border-radius: 20px; 
                    max-width: 90vw; max-height: 90vh; overflow-y: auto;
                    box-shadow: 0 10px 30px rgba(0,0,0,0.3);">
            
            <h2 style="text-align: center; margin-bottom: 1.5rem;">📖 游戏说明</h2>
            
            <div style="background: rgba(255, 255, 255, 0.1); padding: 1.2rem; 
                        border-radius: 15px; margin-bottom: 1.5rem;">
                <h3 style="margin-bottom: 1rem; color: #ffd700;">🎮 游戏规则</h3>
                <div style="line-height: 1.6;">
                    • 点击相邻的苹果进行交换<br>
                    • 形成3个或更多相同苹果的连线即可消除<br>
                    • 达到目标分数即可过关<br>
                    • 注意剩余步数，用完就失败了<br>
                    • 连击可以获得更多分数奖励
                </div>
            </div>
            
            <div style="background: rgba(255, 255, 255, 0.1); padding: 1.2rem; 
                        border-radius: 15px; margin-bottom: 1.5rem;">
                <h3 style="margin-bottom: 1rem; color: #ffd700;"> 道具详解</h3>
                <div style="display: grid; grid-template-columns: auto 1fr; gap: 0.8rem; align-items: center;">
                    <div style="font-size: 1.5rem;">💥</div>
                    <div><strong>炸弹:</strong> 消除点击位置周围3×3范围内的所有水果</div>
                    
                    <div style="font-size: 1.5rem;">⚡</div>
                    <div><strong>闪电:</strong> 消除点击位置的整行和整列水果</div>
                    
                    <div style="font-size: 1.5rem;">🌈</div>
                    <div><strong>彩虹:</strong> 消除与点击水果相同类型的所有水果</div>
                    
                    <div style="font-size: 1.5rem;">🔨</div>
                    <div><strong>锤子:</strong> 直接敲掉一个水果</div>
                    
                    <div style="font-size: 1.5rem;">🔄</div>
                    <div><strong>洗牌:</strong> 重新随机排列整个棋盘</div>
                    
                    <div style="font-size: 1.5rem;">⏰</div>
                    <div><strong>时光:</strong> 增加5步额外操作机会</div>
                                        
                    <div style="font-size: 1.5rem;">🌪</div>
                    <div><strong>时光:</strong> X型风暴卷走一切，Ashley的能量满满</div>
                </div>
            </div>
            
            <div style="background: rgba(255, 255, 255, 0.1); padding: 1.2rem; 
                        border-radius: 15px; margin-bottom: 1.5rem;">
                <h3 style="margin-bottom: 1rem; color: #ffd700;">💡 游戏技巧</h3>
                <div style="line-height: 1.6;">
                    • 优先寻找能形成4个或5个连线的机会<br>
                    • 合理使用道具，关键时刻能扭转局势<br>
                    • 注意连击，连续消除能获得额外分数<br>
                    • 特殊关卡，会有额外道具扭转乾坤<br>
                    • 练习模式可以无限练习，熟悉各种道具
                </div>
            </div>
            
            <div style="text-align: center; font-style: italic; opacity: 0.8; margin-bottom: 1.5rem;">
                💕 这个游戏是专门为Ashley制作的爱心之作 💕
            </div>
            
            <div style="text-align: center;">
                <button onclick="closeGameInstructions()" 
                        style="padding: 1rem 2rem; background: rgba(255,255,255,0.2); 
                               color: white; border: 2px solid white; border-radius: 25px; 
                               cursor: pointer; font-size: 1.1rem; font-weight: bold;
                               transition: all 0.3s;">
                    继续游戏 ▶️
                </button>
            </div>
        </div>
    `;
    
    document.body.appendChild(overlay);
    
    // 添加淡入动画样式
    const style = document.createElement('style');
    style.textContent = `
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => style.remove(), 500);
}

// 关闭游戏说明并恢复游戏状态
function closeGameInstructions() {
    const overlay = document.getElementById('gameInstructionsOverlay');
    if (overlay) {
        overlay.style.animation = 'fadeOut 0.3s ease-in forwards';
        
        const style = document.createElement('style');
        style.textContent = `
            @keyframes fadeOut {
                from { opacity: 1; }
                to { opacity: 0; }
            }
        `;
        document.head.appendChild(style);
        
        setTimeout(() => {
            overlay.remove();
            style.remove();
            
            // 恢复游戏状态
            gameState.isPaused = false;
        }, 300);
    }
}

// 智能生成苹果，增加combo概率 - 增强版
function generateSmartApple(row, col) {
    // 根据关卡动态获取可用苹果类型
    let availableTypeCount;
    if (gameState.currentLevel === 0) {
        availableTypeCount = APPLE_TYPES.length;
    } else if (gameState.currentLevel <= 2) {
        availableTypeCount = 4;
    } else if (gameState.currentLevel <= 4) {
        availableTypeCount = 5;
    } else if (gameState.currentLevel <= 6) {
        availableTypeCount = 6;
    } else if (gameState.currentLevel <= 8) {
        availableTypeCount = 7;
    } else if (gameState.currentLevel <= 10) {
        availableTypeCount = 8;
    } else if (gameState.currentLevel <= 12) {
        availableTypeCount = 9;
    } else {
        availableTypeCount = APPLE_TYPES.length;
    }

    const appleTypes = APPLE_TYPES.slice(0, availableTypeCount).map(apple => apple.type);

    // 创建类型到表情符号的映射
    const typeToEmoji = {};
    APPLE_TYPES.slice(0, availableTypeCount).forEach(apple => {
        typeToEmoji[apple.type] = apple.emoji;
    });
    
    // 根据当前连击数动态调整智能生成概率
    let smartGenerationChance = 0.45; // 基础概率45%
    
    if (gameState.combo >= 3) {
        smartGenerationChance = 0.50; // 3连击后提升到50%
    }
    if (gameState.combo >= 5) {
        smartGenerationChance = 0.75; // 5连击后提升到75%
    }
    if (gameState.combo >= 7) {
        smartGenerationChance = 0.85; // 7连击后提升到85%
    }
    if (gameState.combo >= 10) {
        smartGenerationChance = 0.15; // 7连击后提升到85%
    }
    
    // 智能生成逻辑 - 增强连击机会
    if (Math.random() < smartGenerationChance) {
        const potentialMatches = [];
        
        // 1. 检查垂直连击机会（下方两个相同）
        if (row < 6) {
            const apple1 = gameState.grid[row + 1] && gameState.grid[row + 1][col];
            const apple2 = gameState.grid[row + 2] && gameState.grid[row + 2][col];
            if (apple1 && apple2 && apple1.type === apple2.type && apple1.type !== 'special') {
                potentialMatches.push(apple1.type);
            }
        }
        
        // 2. 检查上方两个相同（更容易触发连锁）
        if (row > 1) {
            const apple1 = gameState.grid[row - 1] && gameState.grid[row - 1][col];
            const apple2 = gameState.grid[row - 2] && gameState.grid[row - 2][col];
            if (apple1 && apple2 && apple1.type === apple2.type && apple1.type !== 'special') {
                potentialMatches.push(apple1.type);
            }
        }
        
        // 3. 检查水平连击机会（左侧两个相同）
        if (col > 1) {
            const leftApple1 = gameState.grid[row] && gameState.grid[row][col - 1];
            const leftApple2 = gameState.grid[row] && gameState.grid[row][col - 2];
            if (leftApple1 && leftApple2 && leftApple1.type === leftApple2.type && leftApple1.type !== 'special') {
                potentialMatches.push(leftApple1.type);
            }
        }
        
        // 4. 检查水平连击机会（右侧两个相同）
        if (col < 6) {
            const rightApple1 = gameState.grid[row] && gameState.grid[row][col + 1];
            const rightApple2 = gameState.grid[row] && gameState.grid[row][col + 2];
            if (rightApple1 && rightApple2 && rightApple1.type === rightApple2.type && rightApple1.type !== 'special') {
                potentialMatches.push(rightApple1.type);
            }
        }
        
        // 5. 检查中间插入的可能性（左右各一个相同）
        if (col > 0 && col < 7) {
            const leftApple = gameState.grid[row] && gameState.grid[row][col - 1];
            const rightApple = gameState.grid[row] && gameState.grid[row][col + 1];
            if (leftApple && rightApple && leftApple.type === rightApple.type && leftApple.type !== 'special') {
                potentialMatches.push(leftApple.type);
            }
        }
        
        // 6. 检查上下插入的可能性
        if (row > 0 && row < 7) {
            const topApple = gameState.grid[row - 1] && gameState.grid[row - 1][col];
            const bottomApple = gameState.grid[row + 1] && gameState.grid[row + 1][col];
            if (topApple && bottomApple && topApple.type === bottomApple.type && topApple.type !== 'special') {
                potentialMatches.push(topApple.type);
            }
        }
        
        // 如果找到了潜在的连击机会，根据连击数调整成功率
        if (potentialMatches.length > 0) {
            let successChance = 0.75; // 基础75%
            
            if (gameState.combo >= 3) {
                successChance = 0.85; // 连击时提升到85%
            }
            if (gameState.combo >= 5) {
                successChance = 0.92; // 高连击时提升到92%
            }
            
            if (Math.random() < successChance) {
                const chosenType = potentialMatches[Math.floor(Math.random() * potentialMatches.length)];
                return {
                    type: chosenType,
                    emoji: typeToEmoji[chosenType],
                    class: `apple-${chosenType}`
                };
            }
        }
    }
    
    // 增加附近相似苹果的概率 - 根据连击数动态调整
    let nearbyChance = 0.25; // 基础25%
    if (gameState.combo >= 3) nearbyChance = 0.40; // 连击时提升到40%
    if (gameState.combo >= 5) nearbyChance = 0.25; // 高连击时提升到25%
    
    if (Math.random() < nearbyChance) {
        const nearbyTypes = [];
        
        // 收集附近的苹果类型，优先选择出现频率高的
        const typeCount = {};
        
        for (let r = Math.max(0, row - 1); r <= Math.min(7, row + 1); r++) {
            for (let c = Math.max(0, col - 1); c <= Math.min(7, col + 1); c++) {
                if (gameState.grid[r] && gameState.grid[r][c] && gameState.grid[r][c].type !== 'special') {
                    const type = gameState.grid[r][c].type;
                    typeCount[type] = (typeCount[type] || 0) + 1;
                    nearbyTypes.push(type);
                }
            }
        }
        
        if (nearbyTypes.length > 0) {
            // 优先选择附近出现次数较多的类型
            const sortedTypes = Object.keys(typeCount).sort((a, b) => typeCount[b] - typeCount[a]);
            const chosenType = sortedTypes.length > 0 ? sortedTypes[0] : nearbyTypes[Math.floor(Math.random() * nearbyTypes.length)];
            
            return {
                type: chosenType,
                emoji: typeToEmoji[chosenType],
                class: `apple-${chosenType}`
            };
        }
    }
    
    // 特殊情况：如果当前连击数≥8，给予额外的"连击续命"机会
    if (gameState.combo >= 8 && Math.random() < 0.3) {
        // 寻找全局最可能形成匹配的类型
        const globalTypeCount = {};
        
        for (let r = 0; r < 8; r++) {
            for (let c = 0; c < 8; c++) {
                if (gameState.grid[r] && gameState.grid[r][c] && gameState.grid[r][c].type !== 'special') {
                    const type = gameState.grid[r][c].type;
                    globalTypeCount[type] = (globalTypeCount[type] || 0) + 1;
                }
            }
        }
        
        // 选择出现次数最多的类型之一
        const commonTypes = Object.keys(globalTypeCount)
            .sort((a, b) => globalTypeCount[b] - globalTypeCount[a])
            .slice(0, Math.min(3, Object.keys(globalTypeCount).length)); // 取前3种最常见的
            
        if (commonTypes.length > 0) {
            const chosenType = commonTypes[Math.floor(Math.random() * commonTypes.length)];
            return {
                type: chosenType,
                emoji: typeToEmoji[chosenType],
                class: `apple-${chosenType}`
            };
        }
    }
    
    // 其他情况随机生成，但避免立即形成匹配（保持挑战性）
    let attempts = 0;
    let randomType;
    
    do {
        randomType = appleTypes[Math.floor(Math.random() * appleTypes.length)];
        attempts++;
    } while (attempts < 5 && wouldCreateImmediateMatch(row, col, randomType));
    
    return {
        type: randomType,
        emoji: typeToEmoji[randomType],
        class: `apple-${randomType}`
    };
}

// 检查是否会立即形成匹配（避免太容易）
function wouldCreateImmediateMatch(row, col, type) {
    // 临时放置苹果
    const tempApple = { type: type };
    const originalApple = gameState.grid[row][col];
    gameState.grid[row][col] = tempApple;
    
    let wouldMatch = false;
    
    // 检查水平匹配
    let horizontalCount = 1;
    
    // 向左计数
    for (let c = col - 1; c >= 0 && gameState.grid[row][c] && gameState.grid[row][c].type === type; c--) {
        horizontalCount++;
    }
    
    // 向右计数
    for (let c = col + 1; c < 8 && gameState.grid[row][c] && gameState.grid[row][c].type === type; c++) {
        horizontalCount++;
    }
    
    if (horizontalCount >= 3) wouldMatch = true;
    
    // 检查垂直匹配
    let verticalCount = 1;
    
    // 向上计数
    for (let r = row - 1; r >= 0 && gameState.grid[r][col] && gameState.grid[r][col].type === type; r--) {
        verticalCount++;
    }
    
    // 向下计数
    for (let r = row + 1; r < 8 && gameState.grid[r][col] && gameState.grid[r][col].type === type; r++) {
        verticalCount++;
    }
    
    if (verticalCount >= 3) wouldMatch = true;
    
    // 恢复原状态
    gameState.grid[row][col] = originalApple;
    
    return wouldMatch;
}

// 幸运重排：小概率触发，轻微调整棋盘增加combo机会
function triggerLuckyReshuffle() {
    let adjustmentsMade = 0;
    const maxAdjustments = 3; // 最多调整3个位置
    
    for (let attempts = 0; attempts < 30 && adjustmentsMade < maxAdjustments; attempts++) {
        const row1 = Math.floor(Math.random() * 8);
        const col1 = Math.floor(Math.random() * 8);
        const row2 = Math.floor(Math.random() * 8);
        const col2 = Math.floor(Math.random() * 8);
        
        // 确保不是同一个位置且都有苹果
        if ((row1 === row2 && col1 === col2) || 
            !gameState.grid[row1][col1] || !gameState.grid[row2][col2] ||
            gameState.grid[row1][col1].type === 'special' || gameState.grid[row2][col2].type === 'special') {
            continue;
        }
        
        // 临时交换
        const temp = gameState.grid[row1][col1];
        gameState.grid[row1][col1] = gameState.grid[row2][col2];
        gameState.grid[row2][col2] = temp;
        
        // 检查是否产生了新的潜在匹配机会（不是立即匹配）
        const hasNewOpportunity = (
            hasNearMatch(row1, col1) || hasNearMatch(row2, col2)
        ) && !hasMatches(); // 不产生立即匹配
        
        if (hasNewOpportunity) {
            adjustmentsMade++;
            updateCellDisplay(row1, col1);
            updateCellDisplay(row2, col2);
            // 保持这个有利的交换
        } else {
            // 撤销交换
            gameState.grid[row2][col2] = gameState.grid[row1][col1];
            gameState.grid[row1][col1] = temp;
        }
    }
    
    if (adjustmentsMade > 0) {
        // 显示微妙的提示
        setTimeout(() => {
            showMessage('✨ 感受到了幸运女神的眷顾...', 2000);
        }, 500);
    }
}

// 检查是否有接近匹配的情况（2个相邻的相同苹果）
function hasNearMatch(row, col) {
    const apple = gameState.grid[row][col];
    if (!apple || apple.type === 'special') return false;
    
    const type = apple.type;
    
    // 检查水平方向是否有2个相邻
    let horizontalNear = 1;
    
    // 向左检查
    for (let c = col - 1; c >= 0 && gameState.grid[row][c] && gameState.grid[row][c].type === type; c--) {
        horizontalNear++;
        if (horizontalNear >= 2) return true;
    }
    
    horizontalNear = 1; // 重置
    // 向右检查
    for (let c = col + 1; c < 8 && gameState.grid[row][c] && gameState.grid[row][c].type === type; c++) {
        horizontalNear++;
        if (horizontalNear >= 2) return true;
    }
    
    // 检查垂直方向是否有2个相邻
    let verticalNear = 1;
    
    // 向上检查
    for (let r = row - 1; r >= 0 && gameState.grid[r][col] && gameState.grid[r][col].type === type; r--) {
        verticalNear++;
        if (verticalNear >= 2) return true;
    }
    
    verticalNear = 1; // 重置
    // 向下检查
    for (let r = row + 1; r < 8 && gameState.grid[r][col] && gameState.grid[r][col].type === type; r++) {
        verticalNear++;
        if (verticalNear >= 2) return true;
    }
    
    return false;
}

    
// 数据持久化
function saveGameData() {
    const saveData = {
        achievements: Array.from(gameState.achievements),
        totalScore: gameState.totalScore,
        gamesPlayed: gameState.gamesPlayed,
        perfectGames: gameState.perfectGames,
        maxCombo: gameState.maxCombo,
        totalMatches: gameState.totalMatches
    };
    
    localStorage.setItem('appleGameSave', JSON.stringify(saveData));
}

function loadGameData() {
    try {
        const saveData = localStorage.getItem('appleGameSave');
        if (saveData) {
            const data = JSON.parse(saveData);
            gameState.achievements = new Set(data.achievements || []);
            gameState.totalScore = data.totalScore || 0;
            gameState.gamesPlayed = data.gamesPlayed || 0;
            gameState.perfectGames = data.perfectGames || 0;
            gameState.maxCombo = data.maxCombo || 0;
            gameState.totalMatches = data.totalMatches || 0;
        }
    } catch (e) {
        console.log('加载存档失败，使用默认数据');
    }
}

// 设置事件监听器
function setupEventListeners() {
    // 防止页面滑动
    document.addEventListener('touchmove', function(e) {
        if (e.target.closest('.game-grid') || e.target.closest('.power-ups')) {
            e.preventDefault();
        }
    }, { passive: false });
    
    // 防止双击缩放
    document.addEventListener('touchstart', function(e) {
        if (e.touches.length > 1) {
            e.preventDefault();
        }
    }, { passive: false });
    
    let lastTouchEnd = 0;
    document.addEventListener('touchend', function(e) {
        const now = Date.now();
        if (now - lastTouchEnd <= 300) {
            e.preventDefault();
        }
        lastTouchEnd = now;
    }, { passive: false });
    
    // 键盘控制（可选）
    document.addEventListener('keydown', function(e) {
        if (gameState.isPaused) return;
        
        switch(e.key) {
            case 'Escape':
                if (gameState.isGameActive) {
                    pauseGame();
                } else {
                    backToMainMenu();
                }
                break;
            case 'r':
            case 'R':
                if (gameState.isGameActive) {
                    restartLevel();
                }
                break;
            case 'h':
            case 'H':
                if (gameState.isGameActive) {
                    showHint();
                }
                break;
        }
    });
}

// 页面加载完成后初始化游戏
document.addEventListener('DOMContentLoaded', function() {
    initializeGame();
    
    // 总是显示欢迎消息
    setTimeout(() => {
        showMessage('💕 欢迎来到Ashley的专属游戏世界！');
    }, 500);
    
    // 检查并显示特殊日期效果（在欢迎消息后）
    setTimeout(() => {
        checkSpecialDate();
    }, 800);
    
    // Ashley专属成就检查
    if (!gameState.achievements.has('ashley_special')) {
        setTimeout(() => {
            const achievement = ACHIEVEMENTS.find(a => a.id === 'ashley_special');
            showAchievement(achievement);
            gameState.achievements.add('ashley_special');
            saveGameData();
        }, 5000);
    }
});

// 窗口大小改变时重新调整
window.addEventListener('resize', function() {
    // 延迟执行以避免频繁调用
    setTimeout(() => {
        if (gameState.isGameActive) {
            updateUI();
        }
    }, 100);
});

// 页面可见性变化时暂停游戏
document.addEventListener('visibilitychange', function() {
    if (document.hidden && gameState.isGameActive && !gameState.isPaused) {
        pauseGame();
    }
});

</script>
</body>
</html>
