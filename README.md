# Apple-Match-only-for-Ashley
Creating an interesting game only for my love, Ashley. Hope her happy everyday!
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Apple-Match-only-for-Ashley | 为我最爱的Ashley定制的专属游戏 ❤️</title>
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
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            overflow-x: hidden;
            touch-action: manipulation;
        }

        .container {
            width: 100%;
            max-width: 420px;
            margin: 0 auto;
            padding: 10px;
            position: relative;
        }

        .screen {
            display: none;
            animation: fadeIn 0.5s ease-in-out;
        }

        .screen.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .header {
            text-align: center;
            margin-bottom: 20px;
        }

        .title {
            font-size: clamp(24px, 6vw, 32px);
            font-weight: bold;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            background: linear-gradient(45deg, #ff6b6b, #feca57);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .love-message {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 20px;
            margin: 15px 0;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
            line-height: 1.6;
        }

        .btn {
            background: linear-gradient(45deg, #ff6b6b, #feca57);
            color: white;
            border: none;
            padding: 15px 25px;
            font-size: 16px;
            border-radius: 25px;
            cursor: pointer;
            margin: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
            font-weight: bold;
            min-height: 50px;
            touch-action: manipulation;
        }

        .btn:hover, .btn:active {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.3);
        }

        /* 关卡网格优化 */
        .level-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin: 20px 0;
            max-height: 60vh;
            overflow-y: auto;
            padding: 10px;
        }

        .level-card {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 12px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
            min-height: 120px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .level-card.unlocked:hover, .level-card.unlocked:active {
            transform: scale(1.05);
            border-color: #feca57;
            background: rgba(255, 255, 255, 0.25);
        }

        .level-card.completed {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
        }

        .level-number {
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .level-name {
            font-size: 12px;
            margin-bottom: 5px;
            font-weight: bold;
            color: #feca57;
        }

        .level-difficulty {
            font-size: 14px;
            margin-bottom: 3px;
        }

        .level-target, .level-moves {
            font-size: 10px;
            opacity: 0.9;
        }

        /* 游戏界面优化 */
        .game-wrapper {
            width: 100%;
            max-width: 400px;
            margin: 0 auto;
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(0,0,0,0.3);
            padding: 12px;
            border-radius: 15px;
            margin-bottom: 10px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .game-info {
            font-weight: bold;
            font-size: 14px;
            display: flex;
            align-items: center;
            gap: 5px;
            min-width: 80px;
        }

        .progress-container {
            margin-bottom: 10px;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: rgba(255,255,255,0.3);
            border-radius: 4px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4ecdc4, #44a08d);
            transition: width 0.3s ease;
        }

        .game-board-container {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 15px;
            margin-bottom: 10px;
        }

        .game-board {
            position: relative;
            width: 100%;
            max-width: 320px;
            margin: 0 auto;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(8, 1fr);
            gap: 2px;
            background: rgba(0,0,0,0.2);
            padding: 5px;
            border-radius: 10px;
            aspect-ratio: 1;
        }

        .cell {
            background: rgba(255,255,255,0.8);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
            aspect-ratio: 1;
            min-height: 35px;
        }

        .cell:hover, .cell:active {
            transform: scale(1.1);
            z-index: 10;
        }

        .cell.selected {
            background: linear-gradient(45deg, #ff6b6b, #feca57);
            box-shadow: 0 0 15px rgba(255,107,107,0.7);
        }

        .fruit {
            font-size: clamp(18px, 4vw, 24px);
            transition: all 0.3s ease;
            user-select: none;
            -webkit-user-select: none;
        }

        .special-fruit { animation: glow 2s ease-in-out infinite alternate; }
        .ultra-fruit { animation: rainbow 3s linear infinite; }
        .mega-fruit { animation: pulse 1s ease-in-out infinite; }
        .legendary-fruit { animation: legendary 2s ease-in-out infinite; }

        @keyframes glow {
            from { filter: drop-shadow(0 0 5px #ffd700); }
            to { filter: drop-shadow(0 0 15px #ffd700); }
        }

        @keyframes rainbow {
            0% { filter: hue-rotate(0deg); }
            100% { filter: hue-rotate(360deg); }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        @keyframes legendary {
            0%, 100% { filter: drop-shadow(0 0 10px #ff1493) brightness(1.2); }
            50% { filter: drop-shadow(0 0 20px #00ffff) brightness(1.5); }
        }

        /* 道具区域优化 */
        .power-ups-container {
            margin: 10px 0;
        }

        .power-ups {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 8px;
            background: rgba(0,0,0,0.3);
            padding: 12px;
            border-radius: 15px;
            max-height: 200px;
            overflow-y: auto;
        }

        .power-up {
            background: rgba(255,255,255,0.2);
            border: 2px solid transparent;
            border-radius: 12px;
            padding: 8px;
            font-size: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            min-height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            touch-action: manipulation;
        }

        .power-up:hover, .power-up:active {
            background: rgba(255,255,255,0.4);
            transform: scale(1.05);
        }

        .power-up.active {
            border-color: #feca57;
            background: linear-gradient(45deg, #ff6b6b, #feca57);
            box-shadow: 0 0 15px rgba(255,107,107,0.5);
        }

        .power-up.disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }

        .power-up-count {
            position: absolute;
            top: -5px;
            right: -5px;
            background: #ff6b6b;
            color: white;
            border-radius: 10px;
            width: 18px;
            height: 18px;
            font-size: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        /* 控制按钮优化 */
        .game-controls {
            display: flex;
            justify-content: space-between;
            gap: 8px;
            margin-top: 10px;
        }

        .control-btn {
            flex: 1;
            background: rgba(255,255,255,0.2);
            color: white;
            border: none;
            padding: 12px 8px;
            border-radius: 15px;
            cursor: pointer;
            font-size: 12px;
            font-weight: bold;
            transition: all 0.3s ease;
            touch-action: manipulation;
            min-height: 45px;
        }

        .control-btn:hover, .control-btn:active {
            background: rgba(255,255,255,0.4);
            transform: translateY(-2px);
        }

        /* 特效动画 */
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        @keyframes particleFloat {
            0% { opacity: 1; transform: translateY(0) scale(1); }
            100% { opacity: 0; transform: translateY(-50px) scale(1.5); }
        }

        @keyframes scorePopup {
            0% { opacity: 0; transform: translateY(0) scale(0.5); }
            50% { opacity: 1; transform: translateY(-20px) scale(1.2); }
            100% { opacity: 0; transform: translateY(-40px) scale(1); }
        }

        @keyframes screenEffectFade {
            0% { opacity: 0; transform: scale(0.5) rotate(0deg); }
            50% { opacity: 1; transform: scale(1) rotate(180deg); }
            100% { opacity: 0; transform: scale(1.5) rotate(360deg); }
        }

        @keyframes achievementShow {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0.5); }
            20% { opacity: 1; transform: translate(-50%, -50%) scale(1.1); }
            80% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
            100% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
        }

        @keyframes fadeInOut {
            0%, 100% { opacity: 0; }
            20%, 80% { opacity: 1; }
        }

        .combo-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 20px;
            font-weight: bold;
            z-index: 1000;
            pointer-events: none;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
            animation: scorePopup 1.5s ease-out forwards;
        }

        /* 成就样式 */
        .achievement {
            display: flex;
            align-items: center;
            background: rgba(255,255,255,0.1);
            border-radius: 15px;
            padding: 15px;
            margin: 10px 0;
            transition: all 0.3s ease;
        }

        .achievement.unlocked {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
        }

        .achievement.locked {
            opacity: 0.5;
        }

        .achievement-icon {
            font-size: 32px;
            margin-right: 15px;
        }

        .achievement-info {
            flex: 1;
        }

        .achievement-name {
            font-weight: bold;
            font-size: 16px;
            margin-bottom: 5px;
        }

        .achievement-desc {
            font-size: 12px;
            opacity: 0.8;
            margin-bottom: 5px;
        }

        .achievement-status {
            font-size: 10px;
            font-weight: bold;
        }

        /* 暂停覆盖层 */
        .pause-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 10000;
            flex-direction: column;
        }

        .pause-content {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            text-align: center;
            border: 1px solid rgba(255,255,255,0.2);
        }

        /* 移动端优化 */
        @media (max-width: 480px) {
            .container {
                padding: 5px;
            }
            
            .game-header {
                padding: 8px;
                font-size: 12px;
            }
            
            .game-board-container {
                padding: 10px;
            }
            
            .power-ups {
                grid-template-columns: repeat(3, 1fr);
                gap: 6px;
                padding: 8px;
            }
            
            .power-up {
                min-height: 45px;
                font-size: 18px;
                padding: 6px;
            }
            
            .control-btn {
                font-size: 11px;
                padding: 10px 6px;
                min-height: 40px;
            }
            
            .cell {
                min-height: 30px;
            }
            
            .fruit {
                font-size: 16px;
            }
        }

        @media (max-height: 700px) {
            .love-message {
                padding: 15px;
                margin: 10px 0;
            }
            
            .power-ups {
                max-height: 120px;
            }
            
            .level-grid {
                max-height: 50vh;
            }
        }

        /* 横屏优化 */
        @media (orientation: landscape) and (max-height: 500px) {
            .container {
                max-width: 600px;
            }
            
            .game-wrapper {
                display: flex;
                flex-direction: row;
                align-items: flex-start;
                gap: 10px;
            }
            
            .game-board-container {
                flex: 1;
                margin-bottom: 0;
            }
            
            .game-side {
                width: 200px;
                display: flex;
                flex-direction: column;
                gap: 10px;
            }
            
            .power-ups {
                grid-template-columns: repeat(2, 1fr);
                max-height: none;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 主菜单 -->
        <div id="mainMenu" class="screen active">
            <div class="header">
                <h1 class="title">🍎 Apple Match</h1>
                <div class="love-message">
                    <p>❤️ 为我最爱的Ashley定制的专属游戏 ❤️</p>
                    <p>希望每一天都充满快乐和甜蜜！</p>
                </div>
            </div>
            <div style="text-align: center;">
                <button class="btn" onclick="showLevelSelect()">🎮 开始冒险</button>
                <button class="btn" onclick="showPractice()">🏃‍♀️ 练习场</button>
                <button class="btn" onclick="showAchievements()">🏆 成就系统</button>
                <button class="btn" onclick="showInstructions()">📚 游戏说明</button>
            </div>
        </div>

        <!-- 关卡选择 -->
        <div id="levelSelect" class="screen">
            <h2 class="title">选择关卡</h2>
            <div class="love-message">
                <p>每一关都是我对你爱的表达 💕</p>
                <p>所有关卡都为你开放，随心选择吧！</p>
            </div>
            <div id="levelGrid" class="level-grid">
                <!-- 关卡将通过JavaScript生成 -->
            </div>
            <div style="text-align: center; margin-top: 15px;">
                <button class="btn" onclick="showMainMenu()">🏠 返回主菜单</button>
            </div>
        </div>

        <!-- 关卡确认 -->
        <div id="levelConfirm" class="screen">
            <h2 class="title" id="levelTitle">关卡 1 - 爱的起点</h2>
            <div class="love-message">
                <p id="levelDescription">这是一个适合新手的简单关卡，来熟悉游戏操作吧！</p>
                <div style="margin-top: 20px;">
                    <button class="btn" onclick="startGame()">🚀 开始游戏</button>
                    <button class="btn" onclick="showLevelSelect()">🔙 返回选择</button>
                    <button class="btn" onclick="showInstructions()">❓ 查看说明</button>
                </div>
            </div>
        </div>
        <!-- 游戏界面 -->
        <div id="gameScreen" class="screen">
            <div class="game-wrapper">
                <div class="game-main">
                    <!-- 游戏状态信息 -->
                    <div class="game-header">
                        <div class="game-info">❤️ <span id="lives">30</span></div>
                        <div class="game-info">🎯 <span id="score">0</span></div>
                        <div class="game-info">⭐ <span id="target">10000</span></div>
                    </div>
                    
                    <!-- 进度条 -->
                    <div class="progress-container">
                        <div class="progress-bar">
                            <div id="progressFill" class="progress-fill" style="width: 0%"></div>
                        </div>
                    </div>

                    <!-- 游戏棋盘 -->
                    <div class="game-board-container">
                        <div class="game-board">
                            <div id="gameGrid" class="grid">
                                <!-- 棋盘格子将通过JavaScript生成 -->
                            </div>
                        </div>
                    </div>

                    <!-- 道具区域 -->
                    <div class="power-ups-container">
                        <div id="gamePowerUps" class="power-ups">
                            <!-- 道具将通过JavaScript生成 -->
                        </div>
                    </div>

                    <!-- 控制按钮 -->
                    <div class="game-controls">
                        <button class="control-btn" onclick="pauseGame()">⏸️ 暂停</button>
                        <button class="control-btn" onclick="showLevelSelect()">🏠 返回</button>
                        <button class="control-btn" onclick="startGame()">🔄 重新开始</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- 练习模式 -->
        <div id="practice" class="screen">
            <div class="game-wrapper">
                <div class="game-main">
                    <div class="game-header">
                        <div class="game-info">💕 <span id="practiceLives">∞</span></div>
                        <div class="game-info">🎯 <span id="practiceScore">0</span></div>
                        <div class="love-message" style="margin: 10px 0; padding: 10px; font-size: 14px;">
                            Ashley专属练习场 - 无限步数，尽情享受！
                        </div>
                    </div>

                    <div class="game-board-container">
                        <div class="game-board">
                            <div id="practiceGrid" class="grid">
                                <!-- 练习棋盘 -->
                            </div>
                        </div>
                    </div>

                    <div class="power-ups-container">
                        <div id="practicePowerUps" class="power-ups">
                            <!-- 练习道具 -->
                        </div>
                    </div>

                    <div class="game-controls">
                        <button class="control-btn" onclick="resetPractice()">🔄 重置</button>
                        <button class="control-btn" onclick="showMainMenu()">🏠 返回</button>
                    </div>
                </div>
            </div>
        </div>

        <!-- 成就系统 -->
        <div id="achievements" class="screen">
            <h2 class="title">🏆 Ashley的成就殿堂</h2>
            <div class="love-message">
                <p>记录着我们一起游戏的美好时光 ❤️</p>
            </div>
            <div id="achievementList" style="max-height: 60vh; overflow-y: auto; margin: 20px 0;">
                <!-- 成就列表将通过JavaScript生成 -->
            </div>
            <div style="text-align: center;">
                <button class="btn" onclick="showMainMenu()">🏠 返回主菜单</button>
            </div>
        </div>

        <!-- 游戏说明 -->
        <div id="instructionsModal" class="screen">
            <h2 class="title">📚 游戏说明</h2>
            <div class="love-message" style="text-align: left; max-height: 60vh; overflow-y: auto;">
                <h3>🎯 游戏目标</h3>
                <p>• 交换相邻水果形成3个或更多相同水果的连线</p>
                <p>• 达到目标分数即可过关</p>
                <p>• 每次交换消耗1步，用完步数游戏结束</p>
                
                <h3>🍎 水果类型</h3>
                <p>• 🍎🍊🍌🍇🥝🍓🥭🍑 - 普通水果</p>
                <p>• ✨ - 特殊水果（2倍分数）</p>
                <p>• 🌟 - 超级水果（3倍分数）</p>
                <p>• 💎 - 巨型水果（5倍分数）</p>
                <p>• 👑 - 传说水果（8倍分数）</p>

                <h3>🔥 12种超级道具</h3>
                <p>• 💣 炸弹 - 3×3区域爆炸消除</p>
                <p>• 🌈 彩虹球 - 消除所有同色水果</p>
                <p>• 🔨 锤子 - 精准消除指定水果</p>
                <p>• 🔄 交换 - 强制交换任意两个水果</p>
                <p>• ⚡ 闪电 - 十字形消除</p>
                <p>• ❄️ 冰冻 - 时间暂停+10步</p>
                <p>• ✨ 倍数 - 接下来5次得分×5</p>
                <p>• 🔀 洗牌 - 重新打乱所有水果</p>
                <p>• ☄️ 流星 - 对角线攻击</p>
                <p>• 🌪️ 龙卷风 - 随机消除15个水果</p>
                <p>• 🎭 魔法 - 随机变换水果类型</p>
                <p>• ⏰ 时光 - 回到上一步状态</p>

                <h3>🎮 操作方法</h3>
                <p>• 点击选择水果，再点击相邻水果进行交换</p>
                <p>• 点击道具图标激活，然后点击棋盘使用</p>
                <p>• 连续消除可获得连击奖励</p>
                
                <h3>⌨️ 键盘快捷键</h3>
                <p>• ESC - 暂停/恢复游戏</p>
                <p>• R - 重置练习模式</p>
                <p>• 1-9 - 快速选择道具</p>
            </div>
            <div style="text-align: center; margin-top: 15px;">
                <button class="btn" onclick="showMainMenu()">🏠 返回主菜单</button>
            </div>
        </div>
    </div>

    <script>
        // 游戏全局变量
        let game = null;
        let gameMode = 'normal';
        let currentLevel = 1;

        // 关卡配置（所有关卡默认解锁）
        const levelConfig = {
            1: { name: "爱的起点", target: 8000, moves: 25, difficulty: 1, description: "就像我们初次相遇，简单而美好。让我们从这里开始我们的甜蜜冒险吧！🌸" },
            2: { name: "心动时刻", target: 12000, moves: 25, difficulty: 1, description: "每一次心跳都是为了你。感受这份悸动，让爱意在指尖绽放！💓" },
            3: { name: "甜蜜邂逅", target: 15000, moves: 25, difficulty: 2, description: "就像蜂蜜一样甜蜜的相遇，让每一个瞬间都充满幸福的味道。🍯" },
            4: { name: "浪漫花园", target: 18000, moves: 25, difficulty: 2, description: "在这个充满鲜花的花园里，我想和你一起漫步到永远。🌹" },
            5: { name: "星空下的誓言", target: 22000, moves: 25, difficulty: 2, description: "在满天繁星的见证下，我向你许下永恒的诺言。✨" },
            6: { name: "月光小夜曲", target: 28000, moves: 25, difficulty: 3, description: "月光如水，爱意如诗。让我为你弹奏一首专属的小夜曲。🌙" },
            7: { name: "彩虹桥约定", target: 35000, moves: 25, difficulty: 3, description: "风雨过后见彩虹，就像我们的爱情，历经考验更加美丽。🌈" },
            8: { name: "海滩漫步", target: 42000, moves: 25, difficulty: 3, description: "在这片美丽的海滩上，让我们留下专属于我们的足迹。🏖️" },
            9: { name: "魔法城堡", target: 50000, moves: 25, difficulty: 4, description: "在这座充满魔法的城堡里，你就是我唯一的公主。👸" },
            10: { name: "时光隧道", target: 60000, moves: 25, difficulty: 4, description: "愿时光慢一些，让我能更久地凝视你美丽的笑容。⏰" },
            11: { name: "梦想天空", target: 70000, moves: 25, difficulty: 4, description: "在这片梦想的天空下，让我们一起飞向更广阔的未来。☁️" },
            12: { name: "极光之舞", target: 80000, moves: 25, difficulty: 5, description: "就像北极光一样绚烂多彩，我们的爱情照亮整个世界。🌌" },
            13: { name: "钻石之心", target: 90000, moves: 25, difficulty: 5, description: "你就像最珍贵的钻石，在我心中闪闪发光，永远无可替代。💎" },
            14: { name: "天使之翼", target: 100000, moves: 25, difficulty: 5, description: "你是降临在我生命中的天使，带给我无尽的快乐和温暖。👼" },
            15: { name: "永恒国度", target: 120000, moves: 25, difficulty: 6, description: "在爱的永恒国度里，我们将永远幸福地生活在一起。Ashley，我爱你！❤️" }
        };

        // 成就配置
        const achievementConfig = {
            firstWin: { name: "初次胜利", desc: "完成第一个关卡", icon: "🎉", unlocked: false },
            speedRunner: { name: "闪电通关", desc: "15秒内完成任意关卡", icon: "⚡", unlocked: false },
            comboMaster: { name: "连击大师", desc: "达到10连击", icon: "🔥", unlocked: false },
            perfectScore: { name: "完美分数", desc: "单局得分超过50000", icon: "⭐", unlocked: false },
            powerUpLover: { name: "道具达人", desc: "累计使用50次道具", icon: "🎯", unlocked: false },
            legendary: { name: "传说玩家", desc: "完成所有关卡", icon: "👑", unlocked: false },
            ashley: { name: "最爱的Ashley", desc: "专属于Ashley的特殊成就", icon: "💖", unlocked: true }
        };

        // 音效系统
        function playEnhancedSound(type, pitch = 1) {
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                let frequency = 440;
                let duration = 0.3;
                
                switch(type) {
                    case 'match':
                        frequency = 523 * pitch;
                        duration = 0.2;
                        break;
                    case 'combo':
                        frequency = 659 * pitch;
                        duration = 0.4;
                        break;
                    case 'super_combo':
                        frequency = 784 * pitch;
                        duration = 0.6;
                        break;
                    case 'legendary_combo':
                        frequency = 880 * pitch;
                        duration = 0.8;
                        break;
                    case 'powerup':
                        frequency = 698 * pitch;
                        duration = 0.5;
                        break;
                    case 'victory':
                        frequency = 523;
                        duration = 1.0;
                        break;
                    case 'invalid':
                        frequency = 200;
                        duration = 0.1;
                        break;
                }
                
                oscillator.frequency.setValueAtTime(frequency, audioContext.currentTime);
                oscillator.type = type === 'victory' ? 'square' : 'sine';
                
                gainNode.gain.setValueAtTime(0.1, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + duration);
                
                oscillator.start(audioContext.currentTime);
                oscillator.stop(audioContext.currentTime + duration);
            } catch (error) {
                // 静默处理音效错误
            }
        }

        // 超级水果消除游戏主类
        class SuperAppleMatchGame {
            constructor() {
                this.gridSize = 8;
                this.fruits = ['🍎', '🍊', '🍌', '🍇', '🥝', '🍓', '🥭', '🍑'];
                this.grid = [];
                this.selectedCell = null;
                this.score = 0;
                this.lives = 30;
                this.target = 10000;
                this.currentGridId = 'gameGrid';
                this.isAnimating = false;
                this.isPaused = false;
                this.gameStartTime = Date.now();
                
                // 连击系统
                this.combo = 0;
                this.maxCombo = 0;
                this.totalMatches = 0;
                
                // 道具系统
                this.powerUps = {
                    bomb: 3, rainbow: 2, hammer: 5, swap: 3,
                    lightning: 3, freeze: 2, multiplier: 2, shuffle: 2,
                    meteor: 1, tornado: 1, magic: 2, time: 2
                };
                this.activePowerUp = null;
                this.powerUpUsageCount = 0;
                
                // 特殊水果概率
                this.specialFruitChance = 0.15;
                this.legendaryFruitChance = 0.03;
                
                // 倍数系统
                this.multiplier = 1;
                this.multiplierTimeLeft = 0;
                this.frozenTime = 0;
                
                // 历史状态（用于时光机器）
                this.previousGameState = null;
                
                // 连击效果配置
                this.comboEffects = {
                    3: { text: "不错！", color: "#4ecdc4", shake: false },
                    5: { text: "很棒！", color: "#45b7d1", shake: false },
                    8: { text: "出色！", color: "#f39c12", shake: true },
                    10: { text: "完美！", color: "#e74c3c", shake: true },
                    15: { text: "不可思议！", color: "#9b59b6", shake: true },
                    20: { text: "传说级！", color: "#ff1493", shake: true }
                };
            }

            init() {
                this.initGrid();
                this.generateInitialFruits();
                this.render();
                this.updateUI();
                this.updatePowerUpDisplay();
                this.addEventListeners();
            }

            initGrid() {
                this.grid = [];
                for (let i = 0; i < this.gridSize; i++) {
                    this.grid[i] = [];
                    for (let j = 0; j < this.gridSize; j++) {
                        this.grid[i][j] = { fruit: null, special: 0 };
                    }
                }
            }

            generateInitialFruits() {
                let attempts = 0;
                const maxAttempts = 100;
                
                do {
                    this.initGrid();
                    for (let i = 0; i < this.gridSize; i++) {
                        for (let j = 0; j < this.gridSize; j++) {
                            this.grid[i][j] = this.generateRandomFruit();
                        }
                    }
                    attempts++;
                } while (this.findMatches().length > 0 && attempts < maxAttempts);
                
                // 如果仍有匹配，强制清除
                if (attempts >= maxAttempts) {
                    const matches = this.findMatches();
                    matches.forEach(match => {
                        this.grid[match.row][match.col] = this.generateRandomFruit();
                    });
                }
            }

            generateRandomFruit() {
                const fruit = this.fruits[Math.floor(Math.random() * this.fruits.length)];
                let special = 0;
                const rand = Math.random();
                
                if (rand < this.legendaryFruitChance) {
                    special = 4; // 传说级（👑效果）
                } else if (rand < this.specialFruitChance) {
                    if (rand < 0.05) special = 3; // 巨型水果（💎效果）
                    else if (rand < 0.10) special = 2; // 超级水果（🌟效果）
                    else special = 1; // 特殊水果（✨效果）
                }
                
                return { fruit, special };
            }

            generateNewFruits() {
                for (let col = 0; col < this.gridSize; col++) {
                    for (let row = 0; row < this.gridSize; row++) {
                        if (!this.grid[row][col].fruit) {
                            this.grid[row][col] = this.generateRandomFruit();
                        }
                    }
                }
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
                            fruit.className = 'fruit';
                            fruit.textContent = this.grid[i][j].fruit;
                            
                            // 添加特殊效果类
                            switch(this.grid[i][j].special) {
                                case 1: 
                                    fruit.classList.add('special-fruit');
                                    fruit.title = '特殊水果 - 2倍分数';
                                    break;
                                case 2: 
                                    fruit.classList.add('ultra-fruit');
                                    fruit.title = '超级水果 - 3倍分数';
                                    break;
                                case 3: 
                                    fruit.classList.add('mega-fruit');
                                    fruit.title = '巨型水果 - 5倍分数';
                                    break;
                                case 4: 
                                    fruit.classList.add('legendary-fruit');
                                    fruit.title = '传说水果 - 8倍分数';
                                    break;
                            }
                            
                            cell.appendChild(fruit);
                        }
                        
                        cell.addEventListener('click', (e) => this.handleCellClick(i, j, e));
                        cell.addEventListener('touchstart', (e) => {
                            e.preventDefault();
                            this.handleCellClick(i, j, e);
                        }, { passive: false });
                        
                        gridElement.appendChild(cell);
                    }
                }
            }
        </script>
            handleCellClick(row, col, event) {
                if (this.isAnimating || this.isPaused || this.lives <= 0) return;
                if (event) event.preventDefault();
                
                // 如果激活了道具
                if (this.activePowerUp) {
                    this.usePowerUp(row, col);
                    return;
                }
                
                // 正常的水果交换逻辑
                if (this.selectedCell) {
                    if (this.selectedCell.row === row && this.selectedCell.col === col) {
                        // 取消选择
                        this.clearSelection();
                    } else if (this.isAdjacent(this.selectedCell.row, this.selectedCell.col, row, col)) {
                        // 执行交换
                        this.swapAndCheck(this.selectedCell.row, this.selectedCell.col, row, col);
                        this.clearSelection();
                    } else {
                        // 选择新的格子
                        this.selectCell(row, col);
                    }
                } else {
                    this.selectCell(row, col);
                }
            }

            selectCell(row, col) {
                if (!this.grid[row][col].fruit) return;
                
                this.selectedCell = { row, col };
                this.updateCellSelection();
                playEnhancedSound('select', 1.2);
            }

            clearSelection() {
                this.selectedCell = null;
                this.updateCellSelection();
            }

            updateCellSelection() {
                const cells = document.querySelectorAll(`#${this.currentGridId} .cell`);
                cells.forEach(cell => cell.classList.remove('selected'));
                
                if (this.selectedCell) {
                    const selectedElement = document.querySelector(
                        `#${this.currentGridId} .cell[data-row="${this.selectedCell.row}"][data-col="${this.selectedCell.col}"]`
                    );
                    if (selectedElement) {
                        selectedElement.classList.add('selected');
                    }
                }
            }

            isAdjacent(row1, col1, row2, col2) {
                const rowDiff = Math.abs(row1 - row2);
                const colDiff = Math.abs(col1 - col2);
                return (rowDiff === 1 && colDiff === 0) || (rowDiff === 0 && colDiff === 1);
            }

            swapAndCheck(row1, col1, row2, col2) {
                // 保存游戏状态用于时光机器
                this.saveGameState();
                
                // 执行交换
                const temp = this.grid[row1][col1];
                this.grid[row1][col1] = this.grid[row2][col2];
                this.grid[row2][col2] = temp;
                
                // 检查是否有匹配
                const matches = this.findMatches();
                if (matches.length > 0) {
                    this.lives--;
                    this.processMatches();
                } else {
                    // 无匹配，交换回来
                    this.grid[row2][col2] = this.grid[row1][col1];
                    this.grid[row1][col1] = temp;
                    playEnhancedSound('invalid');
                    this.shakeGrid();
                }
                
                this.render();
                this.updateUI();
            }

            findMatches() {
                const matches = [];
                
                // 水平匹配
                for (let row = 0; row < this.gridSize; row++) {
                    let count = 1;
                    let currentFruit = this.grid[row][0].fruit;
                    
                    for (let col = 1; col < this.gridSize; col++) {
                        if (this.grid[row][col].fruit === currentFruit && currentFruit) {
                            count++;
                        } else {
                            if (count >= 3 && currentFruit) {
                                for (let i = col - count; i < col; i++) {
                                    matches.push({ row, col: i });
                                }
                            }
                            count = 1;
                            currentFruit = this.grid[row][col].fruit;
                        }
                    }
                    
                    if (count >= 3 && currentFruit) {
                        for (let i = this.gridSize - count; i < this.gridSize; i++) {
                            matches.push({ row, col: i });
                        }
                    }
                }
                
                // 垂直匹配
                for (let col = 0; col < this.gridSize; col++) {
                    let count = 1;
                    let currentFruit = this.grid[0][col].fruit;
                    
                    for (let row = 1; row < this.gridSize; row++) {
                        if (this.grid[row][col].fruit === currentFruit && currentFruit) {
                            count++;
                        } else {
                            if (count >= 3 && currentFruit) {
                                for (let i = row - count; i < row; i++) {
                                    matches.push({ row: i, col });
                                }
                            }
                            count = 1;
                            currentFruit = this.grid[row][col].fruit;
                        }
                    }
                    
                    if (count >= 3 && currentFruit) {
                        for (let i = this.gridSize - count; i < this.gridSize; i++) {
                            matches.push({ row: i, col });
                        }
                    }
                }
                
                return matches;
            }

            async processMatches() {
                this.isAnimating = true;
                let matches = this.findMatches();
                let totalMatches = 0;
                
                while (matches.length > 0) {
                    totalMatches += matches.length;
                    this.combo++;
                    
                    // 计算分数
                    let matchScore = this.calculateScore(matches);
                    this.score += matchScore;
                    
                    // 显示分数动画
                    this.showScoreAnimation(matches, matchScore);
                    
                    // 播放音效
                    this.playComboSound();
                    
                    // 消除匹配的水果
                    matches.forEach(match => {
                        this.grid[match.row][match.col] = { fruit: null, special: 0 };
                    });
                    
                    await this.animateMatchRemoval(matches);
                    
                    // 下落动画
                    await this.dropFruits();
                    
                    // 生成新水果
                    this.generateNewFruits();
                    this.render();
                    
                    // 检查新匹配
                    matches = this.findMatches();
                    
                    await new Promise(resolve => setTimeout(resolve, 300));
                }
                
                // 连击结束，重置连击计数
                if (this.combo > this.maxCombo) {
                    this.maxCombo = this.combo;
                }
                
                this.totalMatches += totalMatches;
                this.combo = 0;
                this.multiplierTimeLeft = Math.max(0, this.multiplierTimeLeft - 1);
                
                this.updateUI();
                this.checkGameEnd();
                this.isAnimating = false;
                
                // 检查成就
                this.checkAchievements();
            }

            calculateScore(matches) {
                let baseScore = matches.length * 100;
                let specialBonus = 0;
                
                // 计算特殊水果奖励
                matches.forEach(match => {
                    const special = this.grid[match.row][match.col].special;
                    switch (special) {
                        case 1: specialBonus += 100; break;  // 特殊水果 2倍
                        case 2: specialBonus += 200; break;  // 超级水果 3倍
                        case 3: specialBonus += 400; break;  // 巨型水果 5倍
                        case 4: specialBonus += 700; break;  // 传说水果 8倍
                    }
                });
                
                let totalScore = (baseScore + specialBonus) * this.multiplier;
                
                // 连击奖励
                if (this.combo > 1) {
                    totalScore *= (1 + (this.combo - 1) * 0.2);
                }
                
                return Math.floor(totalScore);
            }

            playComboSound() {
                if (this.combo <= 3) {
                    playEnhancedSound('match', 1 + (this.combo * 0.2));
                } else if (this.combo <= 7) {
                    playEnhancedSound('combo', 1 + (this.combo * 0.1));
                } else if (this.combo <= 12) {
                    playEnhancedSound('super_combo', 1 + (this.combo * 0.05));
                } else {
                    playEnhancedSound('legendary_combo', 1.5);
                }
            }

            showScoreAnimation(matches, score) {
                if (matches.length === 0) return;
                
                const gridElement = document.getElementById(this.currentGridId);
                if (!gridElement) return;
                
                // 在第一个匹配位置显示分数
                const firstMatch = matches[0];
                const cellElement = gridElement.querySelector(
                    `.cell[data-row="${firstMatch.row}"][data-col="${firstMatch.col}"]`
                );
                
                if (cellElement) {
                    const scoreElement = document.createElement('div');
                    scoreElement.className = 'combo-text';
                    scoreElement.textContent = `+${score.toLocaleString()}`;
                    
                    // 连击特效
                    const comboEffect = this.getComboEffect(this.combo);
                    if (comboEffect) {
                        scoreElement.style.color = comboEffect.color;
                        if (comboEffect.shake) {
                            gridElement.style.animation = 'shake 0.5s ease-in-out';
                            setTimeout(() => {
                                gridElement.style.animation = '';
                            }, 500);
                        }
                        
                        // 显示连击文字
                        if (this.combo > 2) {
                            const comboText = document.createElement('div');
                            comboText.className = 'combo-text';
                            comboText.textContent = comboEffect.text;
                            comboText.style.top = '30%';
                            comboText.style.fontSize = '16px';
                            comboText.style.color = comboEffect.color;
                            cellElement.appendChild(comboText);
                        }
                    }
                    
                    cellElement.appendChild(scoreElement);
                }
            }

            getComboEffect(combo) {
                for (let threshold of Object.keys(this.comboEffects).sort((a, b) => b - a)) {
                    if (combo >= parseInt(threshold)) {
                        return this.comboEffects[threshold];
                    }
                }
                return null;
            }

            async animateMatchRemoval(matches) {
                const cells = matches.map(match => {
                    return document.querySelector(
                        `#${this.currentGridId} .cell[data-row="${match.row}"][data-col="${match.col}"]`
                    );
                }).filter(cell => cell);
                
                // 粒子特效
                cells.forEach(cell => {
                    this.createParticleEffect(cell);
                    cell.style.animation = 'fadeOut 0.3s ease-out forwards';
                });
                
                return new Promise(resolve => setTimeout(resolve, 400));
            }

            createParticleEffect(element) {
                const rect = element.getBoundingClientRect();
                const colors = ['#ff6b6b', '#4ecdc4', '#45b7d1', '#feca57', '#ff9ff3'];
                
                for (let i = 0; i < 8; i++) {
                    const particle = document.createElement('div');
                    particle.style.cssText = `
                        position: fixed;
                        width: 6px;
                        height: 6px;
                        background: ${colors[Math.floor(Math.random() * colors.length)]};
                        border-radius: 50%;
                        left: ${rect.left + rect.width / 2}px;
                        top: ${rect.top + rect.height / 2}px;
                        pointer-events: none;
                        z-index: 1000;
                        animation: particleFloat 1s ease-out forwards;
                        transform: rotate(${i * 45}deg) translateX(30px);
                    `;
                    
                    document.body.appendChild(particle);
                    setTimeout(() => particle.remove(), 1000);
                }
            }

            async dropFruits() {
                let moved = true;
                
                while (moved) {
                    moved = false;
                    
                    for (let col = 0; col < this.gridSize; col++) {
                        for (let row = this.gridSize - 1; row > 0; row--) {
                            if (!this.grid[row][col].fruit && this.grid[row - 1][col].fruit) {
                                this.grid[row][col] = this.grid[row - 1][col];
                                this.grid[row - 1][col] = { fruit: null, special: 0 };
                                moved = true;
                            }
                        }
                    }
                    
                    if (moved) {
                        this.render();
                        await new Promise(resolve => setTimeout(resolve, 150));
                    }
                }
            }

            shakeGrid() {
                const gridElement = document.getElementById(this.currentGridId);
                if (gridElement) {
                    gridElement.style.animation = 'shake 0.3s ease-in-out';
                    setTimeout(() => {
                        gridElement.style.animation = '';
                    }, 300);
                }
            }

            // 道具系统
            selectPowerUp(powerUpType) {
                if (this.powerUps[powerUpType] <= 0 || this.isAnimating) return;
                
                this.activePowerUp = this.activePowerUp === powerUpType ? null : powerUpType;
                this.updatePowerUpDisplay();
                playEnhancedSound('powerup');
                
                // 显示使用提示
                this.showPowerUpHint(powerUpType);
            }

            showPowerUpHint(powerUpType) {
                const hints = {
                    bomb: "点击任意位置引爆💣",
                    rainbow: "消除所有同色水果🌈",
                    hammer: "精准消除指定水果🔨",
                    swap: "强制交换两个水果🔄",
                    lightning: "十字形消除⚡",
                    freeze: "时间暂停+10步❄️",
                    multiplier: "5倍得分奖励✨",
                    shuffle: "重新洗牌🔀",
                    meteor: "对角线攻击☄️",
                    tornado: "随机消除15个🌪️",
                    magic: "变换水果类型🎭",
                    time: "回到上一步状态⏰"
                };
                
                this.showTemporaryMessage(hints[powerUpType] || "点击棋盘使用道具", 2000);
            }

            showTemporaryMessage(message, duration = 2000) {
                const messageDiv = document.createElement('div');
                messageDiv.innerHTML = `
                    <div style="
                        position: fixed;
                        top: 50%;
                        left: 50%;
                        transform: translate(-50%, -50%);
                        background: rgba(0,0,0,0.8);
                        color: white;
                        padding: 15px 20px;
                        border-radius: 15px;
                        font-size: 16px;
                        z-index: 10000;
                        text-align: center;
                        animation: fadeInOut ${duration/1000}s ease-in-out;
                    ">
                        ${message}
                    </div>
                `;
                document.body.appendChild(messageDiv);
                setTimeout(() => messageDiv.remove(), duration);
            }

            usePowerUp(row, col) {
                if (!this.activePowerUp || this.powerUps[this.activePowerUp] <= 0) return;
                
                this.saveGameState(); // 保存状态
                this.powerUps[this.activePowerUp]--;
                this.powerUpUsageCount++;
                
                switch (this.activePowerUp) {
                    case 'bomb':
                        this.useBomb(row, col);
                        break;
                    case 'rainbow':
                        this.useRainbow(row, col);
                        break;
                    case 'hammer':
                        this.useHammer(row, col);
                        break;
                    case 'swap':
                        this.useSwap(row, col);
                        break;
                    case 'lightning':
                        this.useLightning(row, col);
                        break;
                    case 'freeze':
                        this.useFreeze();
                        break;
                    case 'multiplier':
                        this.useMultiplier();
                        break;
                    case 'shuffle':
                        this.useShuffle();
                        break;
                    case 'meteor':
                        this.useMeteor(row, col);
                        break;
                    case 'tornado':
                        this.useTornado();
                        break;
                    case 'magic':
                        this.useMagic(row, col);
                        break;
                    case 'time':
                        this.useTime();
                        break;
                }
                
                this.activePowerUp = null;
                this.updatePowerUpDisplay();
                this.render();
                this.updateUI();
                
                setTimeout(() => this.processMatches(), 300);
            }

            useBomb(centerRow, centerCol) {
                const affected = [];
                for (let dr = -1; dr <= 1; dr++) {
                    for (let dc = -1; dc <= 1; dc++) {
                        const r = centerRow + dr;
                        const c = centerCol + dc;
                        if (r >= 0 && r < this.gridSize && c >= 0 && c < this.gridSize) {
                            if (this.grid[r][c].fruit) {
                                affected.push({row: r, col: c});
                                this.grid[r][c] = { fruit: null, special: 0 };
                            }
                        }
                    }
                }
                this.showExplosionEffect(centerRow, centerCol);
                playEnhancedSound('powerup', 0.8);
            }

            useRainbow(row, col) {
                const targetFruit = this.grid[row][col].fruit;
                if (!targetFruit) return;
                
                let removed = 0;
                for (let r = 0; r < this.gridSize; r++) {
                    for (let c = 0; c < this.gridSize; c++) {
                        if (this.grid[r][c].fruit === targetFruit) {
                            this.grid[r][c] = { fruit: null, special: 0 };
                            removed++;
                        }
                    }
                }
                
                this.score += removed * 200;
                this.showRainbowEffect();
                playEnhancedSound('powerup', 1.2);
            }

            useHammer(row, col) {
                if (this.grid[row][col].fruit) {
                    this.grid[row][col] = { fruit: null, special: 0 };
                    this.score += 150;
                    this.showHammerEffect(row, col);
                    playEnhancedSound('powerup', 1.0);
                }
            }

            useSwap(row, col) {
                if (this.selectedCell && this.selectedCell.row !== row && this.selectedCell.col !== col) {
                    // 交换选中的和目标格子
                    const temp = this.grid[this.selectedCell.row][this.selectedCell.col];
                    this.grid[this.selectedCell.row][this.selectedCell.col] = this.grid[row][col];
                    this.grid[row][col] = temp;
                    this.clearSelection();
                    playEnhancedSound('powerup', 1.1);
                } else {
                    this.selectCell(row, col);
                    this.showTemporaryMessage("再选择一个位置进行交换", 1500);
                }
            }

            useLightning(row, col) {
                // 十字形消除
                let removed = 0;
                
                // 水平消除
                for (let c = 0; c < this.gridSize; c++) {
                    if (this.grid[row][c].fruit) {
                        this.grid[row][c] = { fruit: null, special: 0 };
                        removed++;
                    }
                }
                
                // 垂直消除
                for (let r = 0; r < this.gridSize; r++) {
                    if (this.grid[r][col].fruit) {
                        this.grid[r][col] = { fruit: null, special: 0 };
                        removed++;
                    }
                }
                
                this.score += removed * 120;
                this.showLightningEffect(row, col);
                playEnhancedSound('powerup', 1.3);
            }

            useFreeze() {
                this.lives += 10;
                this.frozenTime = 3;
                this.showTemporaryMessage("❄️ 时间暂停！获得10步奖励！", 2000);
                playEnhancedSound('powerup', 0.9);
            }

            useMultiplier() {
                this.multiplier = 5;
                this.multiplierTimeLeft = 5;
                this.showTemporaryMessage("✨ 接下来5次得分×5！", 2000);
                playEnhancedSound('powerup', 1.4);
            }

            useShuffle() {
                // 收集所有水果
                const allFruits = [];
                for (let r = 0; r < this.gridSize; r++) {
                    for (let c = 0; c < this.gridSize; c++) {
                        if (this.grid[r][c].fruit) {
                            allFruits.push(this.grid[r][c]);
                        }
                    }
                }
                
                // 洗牌
                for (let i = allFruits.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [allFruits[i], allFruits[j]] = [allFruits[j], allFruits[i]];
                }
                
                // 重新分布
                let fruitIndex = 0;
                for (let r = 0; r < this.gridSize; r++) {
                    for (let c = 0; c < this.gridSize; c++) {
                        if (fruitIndex < allFruits.length) {
                            this.grid[r][c] = allFruits[fruitIndex++];
                        } else {
                            this.grid[r][c] = { fruit: null, special: 0 };
                        }
                    }
                }
                
                this.showShuffleEffect();
                playEnhancedSound('powerup', 1.2);
            }

            useMeteor(row, col) {
                // 对角线攻击
                let removed = 0;
                const directions = [[-1, -1], [-1, 1], [1, -1], [1, 1]];
                
                directions.forEach(([dr, dc]) => {
                    for (let i = 1; i < this.gridSize; i++) {
                        const r = row + dr * i;
                        const c = col + dc * i;
                        if (r >= 0 && r < this.gridSize && c >= 0 && c < this.gridSize) {
                            if (this.grid[r][c].fruit) {
                                this.grid[r][c] = { fruit: null, special: 0 };
                                removed++;
                            }
                        } else break;
                    }
                });
                
                this.score += removed * 150;
                this.showMeteorEffect(row, col);
                playEnhancedSound('powerup', 1.1);
            }

            useTornado() {
                const positions = [];
                for (let r = 0; r < this.gridSize; r++) {
                    for (let c = 0; c < this.gridSize; c++) {
                        if (this.grid[r][c].fruit) {
                            positions.push({row: r, col: c});
                        }
                    }
                }
                
                // 随机选择15个位置
                const toRemove = positions.sort(() => 0.5 - Math.random()).slice(0, 15);
                toRemove.forEach(pos => {
                    this.grid[pos.row][pos.col] = { fruit: null, special: 0 };
                });
                
                this.score += toRemove.length * 180;
                this.showTornadoEffect();
                playEnhancedSound('powerup', 1.5);
            }

            useMagic(row, col) {
                if (this.grid[row][col].fruit) {
                    const newFruit = this.fruits[Math.floor(Math.random() * this.fruits.length)];
                    this.grid[row][col] = { 
                        fruit: newFruit, 
                        special: Math.random() < 0.3 ? Math.floor(Math.random() * 4) + 1 : 0 
                    };
                    this.showMagicEffect(row, col);
                    playEnhancedSound('powerup', 1.2);
                }
            }

            useTime() {
                if (this.previousGameState) {
                    // 恢复到之前的状态
                    this.grid = JSON.parse(JSON.stringify(this.previousGameState.grid));
                    this.score = this.previousGameState.score;
                    this.lives = this.previousGameState.lives;
                    this.showTemporaryMessage("⏰ 时光倒流！回到上一步！", 2000);
                    playEnhancedSound('powerup', 0.8);
                }
            }

            saveGameState() {
                this.previousGameState = {
                    grid: JSON.parse(JSON.stringify(this.grid)),
                    score: this.score,
                    lives: this.lives
                };
            }

            // 特效方法
            showExplosionEffect(row, col) {
                const element = document.querySelector(`#${this.currentGridId} .cell[data-row="${row}"][data-col="${col}"]`);
                if (element) {
                    element.innerHTML = '<div style="font-size: 30px; animation: screenEffectFade 1s ease-out;">💥</div>';
                }
            }

            showRainbowEffect() {
                const gridElement = document.getElementById(this.currentGridId);
                if (gridElement) {
                    gridElement.style.animation = 'rainbow 1s linear';
                    setTimeout(() => gridElement.style.animation = '', 1000);
                }
            }

            showHammerEffect(row, col) {
                const element = document.querySelector(`#${this.currentGridId} .cell[data-row="${row}"][data-col="${col}"]`);
                if (element) {
                    element.innerHTML = '<div style="font-size: 25px; animation: screenEffectFade 0.8s ease-out;">🔨</div>';
                }
            }

            showLightningEffect(row, col) {
                const gridElement = document.getElementById(this.currentGridId);
                if (gridElement) {
                    const lightning = document.createElement('div');
                    lightning.innerHTML = '⚡';
                    lightning.style.cssText = `
                        position: absolute;
                        top: 50%;
                        left: 50%;
                        transform: translate(-50%, -50%);
                        font-size: 60px;
                        z-index: 100;
                        animation: screenEffectFade 1s ease-out;
                        pointer-events: none;
                    `;
                    gridElement.appendChild(lightning);
                    setTimeout(() => lightning.remove(), 1000);
                }
            }

            showShuffleEffect() {
                const gridElement = document.getElementById(this.currentGridId);
                if (gridElement) {
                    gridElement.style.animation = 'shake 0.8s ease-in-out';
                    setTimeout(() => gridElement.style.animation = '', 800);
                }
            }

            showMeteorEffect(row, col) {
                const element = document.querySelector(`#${this.currentGridId} .cell[data-row="${row}"][data-col="${col}"]`);
                if (element) {
                    element.innerHTML = '<div style="font-size: 30px; animation: screenEffectFade 1.2s ease-out;">☄️</div>';
                }
            }

            showTornadoEffect() {
                const gridElement = document.getElementById(this.currentGridId);
                if (gridElement) {
                    const tornado = document.createElement('div');
                    tornado.innerHTML = '🌪️';
                    tornado.style.cssText = `
                        position: absolute;
                        top: 50%;
                        left: 50%;
                        transform: translate(-50%, -50%);
                        font-size: 50px;
                        z-index: 100;
                        animation: screenEffectFade 1.5s ease-out;
                        pointer-events: none;
                    `;
                    gridElement.appendChild(tornado);
                    setTimeout(() => tornado.remove(), 1500);
                }
            }

            showMagicEffect(row, col) {
                const element = document.querySelector(`#${this.currentGridId} .cell[data-row="${row}"][data-col="${col}"]`);
                if (element) {
                    element.innerHTML = '<div style="font-size: 25px; animation: screenEffectFade 1s ease-out;">✨</div>';
                }
            }

            updatePowerUpDisplay() {
                const container = document.getElementById(this.currentGridId === 'gameGrid' ? 'gamePowerUps' : 'practicePowerUps');
                if (!container) return;
                
                container.innerHTML = '';
                
                const powerUpList = [
                    { type: 'bomb', icon: '💣', name: '炸弹' },
                    { type: 'rainbow', icon: '🌈', name: '彩虹' },
                    { type: 'hammer', icon: '🔨', name: '锤子' },
                    { type: 'swap', icon: '🔄', name: '交换' },
                    { type: 'lightning', icon: '⚡', name: '闪电' },
                    { type: 'freeze', icon: '❄️', name: '冰冻' },
                    { type: 'multiplier', icon: '✨', name: '倍数' },
                    { type: 'shuffle', icon: '🔀', name: '洗牌' },
                    { type: 'meteor', icon: '☄️', name: '流星' },
                    { type: 'tornado', icon: '🌪️', name: '龙卷风' },
                    { type: 'magic', icon: '🎭', name: '魔法' },
                    { type: 'time', icon: '⏰', name: '时光' }
                ];
                
                powerUpList.forEach(powerUp => {
                    const count = this.powerUps[powerUp.type] || 0;
                    const button = document.createElement('button');
                    button.className = `powerup-btn ${this.activePowerUp === powerUp.type ? 'active' : ''} ${count <= 0 ? 'disabled' : ''}`;
                    button.innerHTML = `
                        <div class="powerup-icon">${powerUp.icon}</div>
                        <div class="powerup-name">${powerUp.name}</div>
                        <div class="powerup-count">${count}</div>
                    `;
                    button.onclick = () => this.selectPowerUp(powerUp.type);
                    container.appendChild(button);
                });
            }

            // 成就系统
            checkAchievements() {
                const newAchievements = [];
                
                // 检查分数成就
                if (this.score >= 1000000 && !this.achievements.millionaire) {
                    this.achievements.millionaire = true;
                    newAchievements.push({ id: 'millionaire', name: '百万富翁', desc: '获得1,000,000分' });
                }
                
                if (this.score >= 500000 && !this.achievements.richman) {
                    this.achievements.richman = true;
                    newAchievements.push({ id: 'richman', name: '富豪', desc: '获得500,000分' });
                }
                
                // 检查连击成就
                if (this.maxCombo >= 20 && !this.achievements.combomaster) {
                    this.achievements.combomaster = true;
                    newAchievements.push({ id: 'combomaster', name: '连击大师', desc: '达成20连击' });
                }
                
                if (this.maxCombo >= 10 && !this.achievements.combokiller) {
                    this.achievements.combokiller = true;
                    newAchievements.push({ id: 'combokiller', name: '连击杀手', desc: '达成10连击' });
                }
                
                // 检查生存成就
                if (this.totalMatches >= 1000 && !this.achievements.survivor) {
                    this.achievements.survivor = true;
                    newAchievements.push({ id: 'survivor', name: '生存专家', desc: '累计消除1000个匹配' });
                }
                
                // 检查道具使用成就
                if (this.powerUpUsageCount >= 100 && !this.achievements.poweruser) {
                    this.achievements.poweruser = true;
                    newAchievements.push({ id: 'poweruser', name: '道具专家', desc: '使用100个道具' });
                }
                
                // 检查特殊成就
                if (this.score > 0 && this.lives === this.maxLives && !this.achievements.perfect) {
                    this.achievements.perfect = true;
                    newAchievements.push({ id: 'perfect', name: '完美主义者', desc: '在满血状态下获得分数' });
                }
                
                // 显示新成就
                newAchievements.forEach(achievement => {
                    this.showAchievementNotification(achievement);
                });
                
                // 保存成就
                this.saveAchievements();
            }

            showAchievementNotification(achievement) {
                const notification = document.createElement('div');
                notification.className = 'achievement-notification';
                notification.innerHTML = `
                    <div class="achievement-content">
                        <div class="achievement-title">🏆 成就解锁！</div>
                        <div class="achievement-name">${achievement.name}</div>
                        <div class="achievement-desc">${achievement.desc}</div>
                    </div>
                `;
                
                document.body.appendChild(notification);
                
                // 动画效果
                setTimeout(() => notification.classList.add('show'), 100);
                setTimeout(() => notification.classList.remove('show'), 4000);
                setTimeout(() => notification.remove(), 4500);
                
                playEnhancedSound('achievement', 1.0);
            }

            saveAchievements() {
                localStorage.setItem('fruitMatchAchievements', JSON.stringify(this.achievements));
            }

            loadAchievements() {
                const saved = localStorage.getItem('fruitMatchAchievements');
                if (saved) {
                    this.achievements = { ...this.achievements, ...JSON.parse(saved) };
                }
            }

            // 游戏结束检查
            checkGameEnd() {
                if (this.lives <= 0) {
                    this.gameOver();
                }
            }

            gameOver() {
                this.isGameOver = true;
                this.saveHighScore();
                
                // 显示游戏结束界面
                const gameOverDiv = document.createElement('div');
                gameOverDiv.className = 'game-over-overlay';
                gameOverDiv.innerHTML = `
                    <div class="game-over-content">
                        <h2>🎮 游戏结束</h2>
                        <div class="final-stats">
                            <div class="stat-item">
                                <span class="stat-label">最终分数:</span>
                                <span class="stat-value">${this.score.toLocaleString()}</span>
                            </div>
                            <div class="stat-item">
                                <span class="stat-label">最高连击:</span>
                                <span class="stat-value">${this.maxCombo}</span>
                            </div>
                            <div class="stat-item">
                                <span class="stat-label">总消除数:</span>
                                <span class="stat-value">${this.totalMatches}</span>
                            </div>
                            <div class="stat-item">
                                <span class="stat-label">道具使用:</span>
                                <span class="stat-value">${this.powerUpUsageCount}</span>
                            </div>
                            ${this.score > this.highScore ? '<div class="new-record">🎉 新纪录！</div>' : ''}
                        </div>
                        <div class="game-over-buttons">
                            <button onclick="game.restart()" class="restart-btn">重新开始</button>
                            <button onclick="game.goHome()" class="home-btn">返回主页</button>
                        </div>
                    </div>
                `;
                
                document.body.appendChild(gameOverDiv);
                playEnhancedSound('gameover', 1.0);
            }

            restart() {
                document.querySelector('.game-over-overlay')?.remove();
                this.init(this.difficulty);
                this.render();
                this.updateUI();
            }

            goHome() {
                document.querySelector('.game-over-overlay')?.remove();
                this.showScreen('menu');
            }

            // 暂停/恢复游戏
            pauseGame() {
                if (this.isGameOver) return;
                
                this.isPaused = !this.isPaused;
                this.updateUI();
                
                if (this.isPaused) {
                    this.showTemporaryMessage("⏸️ 游戏已暂停", 1000);
                } else {
                    this.showTemporaryMessage("▶️ 游戏继续", 1000);
                }
            }

            // 获取帮助提示
            getHint() {
                if (this.isAnimating || this.isPaused || this.lives <= 0) return;
                
                // 寻找可能的匹配
                const possibleMoves = [];
                
                for (let row = 0; row < this.gridSize; row++) {
                    for (let col = 0; col < this.gridSize; col++) {
                        if (!this.grid[row][col].fruit) continue;
                        
                        // 检查相邻位置
                        const directions = [[-1, 0], [1, 0], [0, -1], [0, 1]];
                        
                        directions.forEach(([dr, dc]) => {
                            const newRow = row + dr;
                            const newCol = col + dc;
                            
                            if (newRow >= 0 && newRow < this.gridSize && 
                                newCol >= 0 && newCol < this.gridSize) {
                                
                                // 模拟交换
                                const temp = this.grid[row][col];
                                this.grid[row][col] = this.grid[newRow][newCol];
                                this.grid[newRow][newCol] = temp;
                                
                                // 检查是否产生匹配
                                const matches = this.findMatches();
                                if (matches.length > 0) {
                                    possibleMoves.push({
                                        from: { row, col },
                                        to: { row: newRow, col: newCol },
                                        matches: matches.length
                                    });
                                }
                                
                                // 恢复原状
                                this.grid[newRow][newCol] = this.grid[row][col];
                                this.grid[row][col] = temp;
                            }
                        });
                    }
                }
                
                if (possibleMoves.length > 0) {
                    // 选择最佳移动
                    const bestMove = possibleMoves.sort((a, b) => b.matches - a.matches)[0];
                    this.highlightHint(bestMove.from, bestMove.to);
                } else {
                    this.showTemporaryMessage("💡 没有发现可行的移动，试试使用道具！", 2000);
                }
            }

            highlightHint(from, to) {
                // 高亮提示的两个格子
                const fromElement = document.querySelector(
                    `#${this.currentGridId} .cell[data-row="${from.row}"][data-col="${from.col}"]`
                );
                const toElement = document.querySelector(
                    `#${this.currentGridId} .cell[data-row="${to.row}"][data-col="${to.col}"]`
                );
                
                [fromElement, toElement].forEach(element => {
                    if (element) {
                        element.classList.add('hint');
                        setTimeout(() => element.classList.remove('hint'), 3000);
                    }
                });
                
                this.showTemporaryMessage("💡 建议交换高亮的两个水果！", 2000);
                playEnhancedSound('hint', 1.0);
            }

            // 保存和加载高分
            saveHighScore() {
                if (this.score > this.highScore) {
                    this.highScore = this.score;
                    localStorage.setItem('fruitMatchHighScore', this.highScore.toString());
                }
            }

            loadHighScore() {
                const saved = localStorage.getItem('fruitMatchHighScore');
                this.highScore = saved ? parseInt(saved) : 0;
            }

            // 更新UI显示
            updateUI() {
                // 更新分数和生命值
                const scoreElement = document.getElementById(this.currentGridId === 'gameGrid' ? 'score' : 'practiceScore');
                const livesElement = document.getElementById(this.currentGridId === 'gameGrid' ? 'lives' : 'practiceLives');
                const comboElement = document.getElementById(this.currentGridId === 'gameGrid' ? 'combo' : 'practiceCombo');
                const multiplierElement = document.getElementById(this.currentGridId === 'gameGrid' ? 'multiplier' : 'practiceMultiplier');
                
                if (scoreElement) scoreElement.textContent = `分数: ${this.score.toLocaleString()}`;
                if (livesElement) {
                    livesElement.textContent = `生命: ${this.lives}`;
                    livesElement.className = this.lives <= 3 ? 'low-lives' : '';
                }
                if (comboElement) {
                    comboElement.textContent = `连击: ${this.combo}`;
                    comboElement.className = this.combo > 5 ? 'high-combo' : '';
                }
                if (multiplierElement) {
                    if (this.multiplier > 1) {
                        multiplierElement.textContent = `倍数: ${this.multiplier}x (剩余${this.multiplierTimeLeft}次)`;
                        multiplierElement.style.display = 'block';
                        multiplierElement.className = 'active-multiplier';
                    } else {
                        multiplierElement.style.display = 'none';
                    }
                }
                
                // 更新道具显示
                this.updatePowerUpDisplay();
                
                // 更新暂停按钮
                const pauseBtn = document.getElementById(this.currentGridId === 'gameGrid' ? 'pauseBtn' : 'practicePauseBtn');
                if (pauseBtn) {
                    pauseBtn.textContent = this.isPaused ? '▶️ 继续' : '⏸️ 暂停';
                    pauseBtn.disabled = this.isGameOver;
                }
            }

            // 屏幕管理
            showScreen(screenName) {
                // 隐藏所有屏幕
                document.querySelectorAll('.screen').forEach(screen => {
                    screen.classList.remove('active');
                });
                
                // 显示目标屏幕
                const targetScreen = document.getElementById(screenName);
                if (targetScreen) {
                    targetScreen.classList.add('active');
                }
                
                // 根据屏幕执行特定操作
                if (screenName === 'menu') {
                    this.loadHighScore();
                    document.getElementById('highScoreDisplay').textContent = this.highScore.toLocaleString();
                } else if (screenName === 'achievements') {
                    this.displayAchievements();
                }
            }

            displayAchievements() {
                const container = document.getElementById('achievementsList');
                if (!container) return;
                
                container.innerHTML = '';
                
                const allAchievements = [
                    { id: 'richman', name: '富豪', desc: '获得500,000分', icon: '💰' },
                    { id: 'millionaire', name: '百万富翁', desc: '获得1,000,000分', icon: '🏆' },
                    { id: 'combokiller', name: '连击杀手', desc: '达成10连击', icon: '⚔️' },
                    { id: 'combomaster', name: '连击大师', desc: '达成20连击', icon: '🎯' },
                    { id: 'survivor', name: '生存专家', desc: '累计消除1000个匹配', icon: '🛡️' },
                    { id: 'poweruser', name: '道具专家', desc: '使用100个道具', icon: '🔧' },
                    { id: 'perfect', name: '完美主义者', desc: '在满血状态下获得分数', icon: '✨' }
                ];
                
                allAchievements.forEach(achievement => {
                    const achieved = this.achievements[achievement.id];
                    const div = document.createElement('div');
                    div.className = `achievement-item ${achieved ? 'achieved' : 'locked'}`;
                    div.innerHTML = `
                        <div class="achievement-icon">${achievement.icon}</div>
                        <div class="achievement-info">
                            <div class="achievement-name">${achievement.name}</div>
                            <div class="achievement-desc">${achievement.desc}</div>
                        </div>
                        <div class="achievement-status">${achieved ? '✅' : '🔒'}</div>
                    `;
                    container.appendChild(div);
                });
            }

            // 游戏初始化完成
            initComplete() {
                console.log('🎮 水果匹配游戏初始化完成');
                console.log('🎯 支持的功能:');
                console.log('   • 多种游戏模式（简单、普通、困难、专家）');
                console.log('   • 12种强力道具系统');
                console.log('   • 特殊水果和连击系统');
                console.log('   • 成就和排行榜系统');
                console.log('   • 练习模式');
                console.log('   • 音效和动画效果');
                console.log('🚀 游戏已准备就绪！');
            }
        }

        // 创建游戏实例
        const game = new FruitMatchGame();

        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', function() {
            game.loadHighScore();
            game.loadAchievements();
            game.initComplete();
        });
