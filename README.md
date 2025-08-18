# Apple-Match-only-for-Ashley
Creating an interesting game only for my love, Ashley. Hope her happy everyday!
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>苹果消消乐 - 献给最爱的Ashley</title>
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
        <h1 class="game-title">🍎 苹果消消乐</h1>
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
    { id: 1, name: "初遇", target: 1800, moves: 1000, quote: "就像第一次见到你，心跳不已 💕", special: false },
    { id: 2, name: "怦然心动", target: 2300, moves: 840, quote: "每一个眼神交汇，都是命运的安排 ✨", special: false },
    { id: 3, name: "甜蜜约会", target: 2500, moves: 830, quote: "和你在一起的每一秒都是甜蜜的 🍯", special: false },
    { id: 4, name: "告白时刻", target: 2800, moves: 820, quote: "三个字，说给全世界听：我爱你 💖", special: true },
    { id: 5, name: "牵手漫步", target: 3000, moves: 810, quote: "十指紧扣，走过春夏秋冬 🌸", special: false },
    { id: 6, name: "浪漫晚餐", target: 3500, moves: 800, quote: "烛光晚餐，你是我唯一的风景 🕯️", special: false },
    { id: 7, name: "星空许愿", target: 4000, moves: 890, quote: "对着流星许愿，愿与你白头偕老 🌟", special: false },
    { id: 8, name: "生日惊喜", target: 4600, moves: 880, quote: "3月25日，为你准备最美的惊喜 🎂", special: true },
    { id: 9, name: "情人节", target: 5300, moves: 870, quote: "玫瑰花海，不及你的笑颜 🌹", special: true },
    { id: 10, name: "永恒承诺", target: 6600, moves: 860, quote: "此生此世，只想和你在一起 💍", special: true },
    { id: 11, name: "梦中情人", target: 7000, moves: 850, quote: "梦里梦外，都是你的身影 💭", special: false },
    { id: 12, name: "心有灵犀", target: 8000, moves: 840, quote: "不用言语，我们就能读懂彼此 💫", special: false }
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
    
    // 3月25日 - Ashley的生日
    if (month === 3 && date === 25) {
        createSpecialEffect('birthday');
        setTimeout(() => showAchievement(ACHIEVEMENTS.find(a => a.id === 'ashley_special')), 2000);
    }
    // 2月14日 - 情人节
    else if (month === 2 && date === 14) {
        createSpecialEffect('valentine');
    }
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
                firework.style.cssText = `
                    position: absolute;
                    width: ${Math.random() * 100 + 50}px;
                    height: ${Math.random() * 100 + 50}px;
                    left: ${Math.random() * 100}%;
                    top: ${Math.random() * 100}%;
                    background: hsl(${Math.random() * 360}, 70%, 60%);
                    border-radius: 50%;
                    animation: fireworkAnim 2s ease-out forwards;
                `;
                effectContainer.appendChild(firework);
                
                setTimeout(() => {
                    if (firework.parentNode) firework.remove();
                }, 2000);
            }, i * 200);
        }
        
        // 添加烟花动画
        const style = document.createElement('style');
        style.textContent = `
            @keyframes fireworkAnim {
                0% { transform: scale(0); opacity: 1; }
                50% { transform: scale(1.5); opacity: 0.8; }
                100% { transform: scale(3); opacity: 0; }
            }
        `;
        document.head.appendChild(style);
        
        // 显示特殊祝福
        setTimeout(() => {
            showMessage('🎂 生日快乐，我最爱的Ashley！🎂\n愿你每天都像今天一样美丽动人！');
        }, 1000);
        
        setTimeout(() => {
            style.remove();
        }, 5000);
        
    } else if (type === 'valentine') {
        // 情人节玫瑰花瓣效果
        for (let i = 0; i < 30; i++) {
            setTimeout(() => {
                const petal = document.createElement('div');
                petal.innerHTML = '🌹';
                petal.style.cssText = `
                    position: absolute;
                    left: ${Math.random() * 100}%;
                    top: -50px;
                    font-size: ${Math.random() * 20 + 10}px;
                    animation: floatHeart 8s linear forwards;
                    pointer-events: none;
                `;
                effectContainer.appendChild(petal);
                
                setTimeout(() => {
                    if (petal.parentNode) petal.remove();
                }, 8000);
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
            bomb: 30,
            lightning: 30,
            rainbow: 20,
            hammer: 50,
            shuffle: 20,
            time: 20
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

// 创建随机苹果
function createRandomApple() {
    const randomType = APPLE_TYPES[Math.floor(Math.random() * APPLE_TYPES.length)];
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
    if (gameState.combo >= 10) comboText += '🔥🔥🔥';
    else if (gameState.combo >= 5) comboText += '🔥🔥';
    else comboText += '🔥';
    
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
    for (let col = 0; col < 8; col++) {
        for (let row = 0; row < 8; row++) {
            if (gameState.grid[row][col] === null) {
                gameState.grid[row][col] = createRandomApple();
                updateCellDisplay(row, col);
                
                // 恢复背景色
                const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
                if (cell) {
                    cell.style.background = '';
                }
            }
        }
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
                    <button onclick="nextLevel(); this.parentElement.parentElement.parentElement.remove();" 
                            style="padding: 1rem 2rem; background: rgba(255,255,255,0.2); 
                                   color: white; border: 2px solid white; border-radius: 25px; 
                                   cursor: pointer; font-size: 1rem;">
                        ${gameState.currentLevel < LEVELS.length ? '下一关 ▶️' : '返回选关 🏠'}
                    </button>
                    <button onclick="restartLevel(); this.parentElement.parentElement.parentElement.remove();" 
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
    
    if (gameState.moves >= 10 && gameState.score >= gameState.target && !gameState.achievements.has('perfect_level')) {
        newAchievements.push('perfect_level');
        gameState.perfectGames++;
    }
    
    // 检查是否使用过所有道具
    const usedAllPowerUps = Object.values(gameState.powerUps).every(count => count < 3);
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

// 显示消息
function showMessage(message) {
    // 移除已存在的消息
    const existingMessage = document.querySelector('.game-message');
    if (existingMessage) {
        existingMessage.remove();
    }
    
    const messageDiv = document.createElement('div');
    messageDiv.className = 'game-message';
    messageDiv.textContent = message;
    messageDiv.style.cssText = `
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: rgba(0, 0, 0, 0.8);
        color: white;
        padding: 1rem 2rem;
        border-radius: 20px;
        font-size: 1.1rem;
        z-index: 999;
        animation: messageAnim 2s ease-out forwards;
        pointer-events: none;
        text-align: center;
        max-width: 80vw;
    `;
    
    document.body.appendChild(messageDiv);
    
    // 添加动画
    const style = document.createElement('style');
    style.textContent = `
        @keyframes messageAnim {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
            10% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
            90% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
            100% { opacity: 0; transform: translate(-50%, -50%) scale(1.1); }
        }
    `;
    document.head.appendChild(style);
    
    setTimeout(() => {
        messageDiv.remove();
        style.remove();
    }, 2000);
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
        "👑 Ashley，你就是我心中的女王，这个游戏献给最美丽的你"
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

    💕 特别提醒:
    这个游戏是专门为Ashley制作的，每一个细节都充满了爱意！
    
    💖 制作者的话:
    Ashley，希望你能喜欢这个小游戏，就像我喜欢你一样！
    `;
    
    alert(settings);
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
    
    // 显示欢迎消息
    setTimeout(() => {
        if (Math.random() > 0.7) {
            showMessage('💕 欢迎来到Ashley的专属游戏世界！');
        }
    }, 1000);
    
    // Ashley专属成就检查
    if (!gameState.achievements.has('ashley_special')) {
        setTimeout(() => {
            const achievement = ACHIEVEMENTS.find(a => a.id === 'ashley_special');
            showAchievement(achievement);
            gameState.achievements.add('ashley_special');
            saveGameData();
        }, 3000);
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
