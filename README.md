# Apple-Match-only-for-Ashley
Creating an interesting game only for my love, Ashley. Hope her happy everyday!
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="format-detection" content="telephone=no">
    <title>苹果消消乐 - 为Ashley定制</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            -webkit-touch-callout: none;
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            user-select: none;
        }

        html, body {
            height: 100%;
            width: 100%;
            overflow: hidden;
            position: fixed;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 30%, #fad0c4 100%);
        }

        /* 强制全屏显示 */
        .app-container {
            width: 100vw;
            height: 100vh;
            height: 100dvh; /* 动态视口高度 */
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        .screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: max(env(safe-area-inset-top), 20px) env(safe-area-inset-right) max(env(safe-area-inset-bottom), 20px) env(safe-area-inset-left);
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
        }

        .screen.active {
            display: flex;
        }

        .love-message {
            background: rgba(255,255,255,0.95);
            padding: 20px;
            border-radius: 20px;
            margin: 10px 20px;
            text-align: center;
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
            font-size: 16px;
            color: #ff6b6b;
            font-weight: bold;
            animation: heartbeat 2s infinite;
        }

        @keyframes heartbeat {
            0%, 50%, 100% { transform: scale(1); }
            25%, 75% { transform: scale(1.05); }
        }

        .title {
            font-size: clamp(2rem, 8vw, 4rem);
            color: #ff6b6b;
            text-shadow: 3px 3px 6px rgba(0,0,0,0.3);
            margin-bottom: 20px;
            animation: bounce 2s infinite;
            text-align: center;
            font-weight: bold;
            line-height: 1.2;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-15px); }
            60% { transform: translateY(-8px); }
        }

        .btn {
            background: linear-gradient(45deg, #ff6b6b, #ffa726);
            color: white;
            border: none;
            padding: 15px 25px;
            margin: 8px 10px;
            border-radius: 25px;
            font-size: clamp(16px, 4vw, 20px);
            cursor: pointer;
            box-shadow: 0 8px 20px rgba(0,0,0,0.25);
            transition: all 0.3s ease;
            font-weight: bold;
            min-width: 200px;
            min-height: 50px;
            text-align: center;
            touch-action: manipulation;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .btn:active {
            transform: scale(0.95);
            box-shadow: 0 4px 15px rgba(0,0,0,0.4);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 25px rgba(0,0,0,0.3);
        }

        .level-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            padding: 10px;
            width: min(95vw, 600px);
            max-height: 60vh;
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
        }

        .level-btn {
            aspect-ratio: 1.1;
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
            color: white;
            border: none;
            border-radius: 20px;
            font-size: 14px;
            cursor: pointer;
            box-shadow: 0 6px 20px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            touch-action: manipulation;
            min-height: 100px;
        }

        .level-btn:active {
            transform: scale(0.95);
        }

        .level-btn.unlocked {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
        }

        .level-btn.locked {
            background: linear-gradient(45deg, #666, #444);
            opacity: 0.6;
        }

        .level-btn.completed {
            background: linear-gradient(45deg, #ffd700, #ffb347);
        }

        /* 游戏界面完全重新设计 */
        .game-wrapper {
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            padding: max(env(safe-area-inset-top), 10px) env(safe-area-inset-right) max(env(safe-area-inset-bottom), 10px) env(safe-area-inset-left);
            gap: 8px;
        }

        .game-header {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 8px;
            width: 100%;
            margin-bottom: 5px;
        }

        .game-info {
            background: rgba(255,255,255,0.9);
            padding: 8px 12px;
            border-radius: 15px;
            font-weight: bold;
            color: #333;
            font-size: clamp(12px, 3.5vw, 16px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            text-align: center;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 40px;
        }

        .progress-container {
            width: 100%;
            margin: 5px 0;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: rgba(255,255,255,0.3);
            border-radius: 10px;
            overflow: hidden;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.2);
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4caf50, #8bc34a);
            transition: width 0.5s ease;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(76,175,80,0.5);
        }

        /* 游戏网格完全重构 */
        .game-board-container {
            flex: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            min-height: 0; /* 重要：允许收缩 */
        }

        .game-board {
            width: min(95vw, 95vh, 450px);
            height: min(95vw, 95vh, 450px);
            background: rgba(255,255,255,0.98);
            border-radius: 20px;
            padding: 8px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
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
            border-radius: 15px;
            overflow: hidden;
        }

        .cell {
            background: #f5f5f5;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
            touch-action: manipulation;
            border-radius: 4px;
            min-height: 0;
        }

        .cell:active {
            transform: scale(0.9);
            background: #e0e0e0;
        }

        .cell.selected {
            background: #ffeb3b;
            box-shadow: inset 0 0 0 3px #ff6b6b;
            animation: selectedGlow 0.8s infinite alternate;
        }

        @keyframes selectedGlow {
            from { transform: scale(1); box-shadow: inset 0 0 0 3px #ff6b6b; }
            to { transform: scale(1.05); box-shadow: inset 0 0 0 3px #ff1744; }
        }

        .fruit {
            width: 90%;
            height: 90%;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(14px, 3vw, 24px);
            font-weight: bold;
            transition: all 0.2s ease;
            cursor: pointer;
            position: relative;
            overflow: hidden;
        }

        /* 水果类型样式 */
        .apple { background: linear-gradient(135deg, #ff6b6b, #ff5252); box-shadow: 0 4px 8px rgba(255,107,107,0.3); }
        .orange { background: linear-gradient(135deg, #ffa726, #ff9800); box-shadow: 0 4px 8px rgba(255,167,38,0.3); }
        .banana { background: linear-gradient(135deg, #ffeb3b, #fdd835); box-shadow: 0 4px 8px rgba(255,235,59,0.3); }
        .grape { background: linear-gradient(135deg, #ab47bc, #8e24aa); box-shadow: 0 4px 8px rgba(171,71,188,0.3); }
        .strawberry { background: linear-gradient(135deg, #ec407a, #e91e63); box-shadow: 0 4px 8px rgba(236,64,122,0.3); }
        .lemon { background: linear-gradient(135deg, #cddc39, #afb42b); box-shadow: 0 4px 8px rgba(205,220,57,0.3); }
        .cherry { background: linear-gradient(135deg, #f44336, #d32f2f); box-shadow: 0 4px 8px rgba(244,67,54,0.3); }
        .kiwi { background: linear-gradient(135deg, #4caf50, #388e3c); box-shadow: 0 4px 8px rgba(76,175,80,0.3); }

        /* 超级水果效果大幅增强 */
        .special-fruit {
            animation: specialGlow 1.5s infinite, rotate 3s infinite linear;
            box-shadow: 0 0 20px rgba(255,215,0,0.8), 0 0 40px rgba(255,215,0,0.4);
        }

        .ultra-fruit {
            animation: ultraGlow 1s infinite, rainbow 2s infinite, pulse 0.8s infinite;
            box-shadow: 0 0 25px rgba(255,255,255,0.9), 0 0 50px rgba(255,255,255,0.5);
        }

        .mega-fruit {
            animation: megaGlow 0.8s infinite, megaRotate 4s infinite, megaPulse 1.2s infinite;
            box-shadow: 0 0 30px rgba(255,0,255,1), 0 0 60px rgba(255,0,255,0.6), 0 0 90px rgba(255,0,255,0.3);
        }

        .legendary-fruit {
            animation: legendaryGlow 0.6s infinite, legendaryRotate 2s infinite, legendaryPulse 0.4s infinite;
            box-shadow: 0 0 40px rgba(0,255,255,1), 0 0 80px rgba(0,255,255,0.8), 0 0 120px rgba(0,255,255,0.4);
        }

        @keyframes specialGlow {
            0%, 100% { filter: brightness(1) saturate(1); }
            50% { filter: brightness(1.4) saturate(1.5); }
        }

        @keyframes ultraGlow {
            0%, 100% { filter: brightness(1.2) saturate(1.3); }
            50% { filter: brightness(1.6) saturate(1.8); }
        }

        @keyframes megaGlow {
            0%, 100% { filter: brightness(1.4) saturate(1.6) hue-rotate(0deg); }
            33% { filter: brightness(1.8) saturate(2) hue-rotate(120deg); }
            66% { filter: brightness(1.6) saturate(1.8) hue-rotate(240deg); }
        }

        @keyframes legendaryGlow {
            0%, 100% { filter: brightness(1.6) saturate(2) hue-rotate(0deg); }
            25% { filter: brightness(2) saturate(2.5) hue-rotate(90deg); }
            50% { filter: brightness(1.8) saturate(2.2) hue-rotate(180deg); }
            75% { filter: brightness(2.2) saturate(2.8) hue-rotate(270deg); }
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        @keyframes rainbow {
            0% { filter: hue-rotate(0deg); }
            100% { filter: hue-rotate(360deg); }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        @keyframes megaRotate {
            0% { transform: rotate(0deg) scale(1); }
            25% { transform: rotate(90deg) scale(1.1); }
            50% { transform: rotate(180deg) scale(1); }
            75% { transform: rotate(270deg) scale(1.1); }
            100% { transform: rotate(360deg) scale(1); }
        }

        @keyframes megaPulse {
            0%, 100% { transform: scale(1); }
            33% { transform: scale(1.15); }
            66% { transform: scale(0.95); }
        }

        @keyframes legendaryRotate {
            0% { transform: rotate(0deg) scale(1) skew(0deg); }
            50% { transform: rotate(180deg) scale(1.2) skew(5deg); }
            100% { transform: rotate(360deg) scale(1) skew(0deg); }
        }

        @keyframes legendaryPulse {
            0%, 100% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.25); opacity: 0.8; }
        }

        /* 超级道具区域增强 */
        .power-ups-container {
            width: 100%;
            padding: 8px 0;
        }

        .power-ups {
            display: flex;
            gap: 8px;
            justify-content: center;
            flex-wrap: wrap;
            width: 100%;
            padding: 0 5px;
        }

        .power-up {
            width: clamp(45px, 8vw, 60px);
            height: clamp(45px, 8vw, 60px);
            border-radius: 50%;
            border: 3px solid #fff;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: white;
            transition: all 0.3s ease;
            box-shadow: 0 6px 18px rgba(0,0,0,0.25);
            font-size: clamp(16px, 3.5vw, 20px);
            touch-action: manipulation;
            position: relative;
            overflow: hidden;
        }

        .power-up:active {
            transform: scale(0.9);
        }

        .power-up.active {
            animation: activePowerUp 0.6s infinite alternate;
            box-shadow: 0 0 0 4px #ffff00, 0 6px 18px rgba(0,0,0,0.25);
            border-color: #ffff00;
        }

        @keyframes activePowerUp {
            from { transform: scale(1) rotate(-3deg); }
            to { transform: scale(1.15) rotate(3deg); }
        }

        .power-up.disabled {
            opacity: 0.4;
            pointer-events: none;
            filter: grayscale(0.8);
        }

        .power-up-count {
            position: absolute;
            top: -8px;
            right: -8px;
            background: linear-gradient(45deg, #ff4444, #cc0000);
            color: white;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 11px;
            font-weight: bold;
            box-shadow: 0 2px 8px rgba(0,0,0,0.3);
            border: 2px solid white;
        }

        /* 12种超级道具样式 */
        .bomb { background: linear-gradient(45deg, #ff5722, #d84315); }
        .rainbow { background: linear-gradient(45deg, #e91e63, #9c27b0, #3f51b5, #4caf50, #ffeb3b, #ff9800); animation: rainbow 2s infinite; }
        .hammer { background: linear-gradient(45deg, #795548, #5d4037); }
        .swap { background: linear-gradient(45deg, #607d8b, #455a64); }
        .lightning { background: linear-gradient(45deg, #ffeb3b, #ffc107); }
        .freeze { background: linear-gradient(45deg, #03a9f4, #0277bd); }
        .multiplier { background: linear-gradient(45deg, #9c27b0, #673ab7); }
        .shuffle { background: linear-gradient(45deg, #4caf50, #388e3c); }
        .meteor { background: linear-gradient(45deg, #ff6b35, #f7931e); }
        .tornado { background: linear-gradient(45deg, #00c9ff, #92fe9d); }
        .magic { background: linear-gradient(45deg, #a8edea, #fed6e3); }
        .time { background: linear-gradient(45deg, #ffecd2, #fcb69f); }

        /* 控制按钮区域 */
        .game-controls {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
            justify-content: center;
            width: 100%;
            padding: 5px 10px;
        }

        .control-btn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 20px;
            font-size: clamp(12px, 3vw, 16px);
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
            font-weight: bold;
            flex: 1;
            min-width: 80px;
            max-width: 120px;
            touch-action: manipulation;
            min-height: 40px;
        }

        .control-btn:active {
            transform: scale(0.95);
        }

        /* 各种特效增强 */
        .combo-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: clamp(24px, 8vw, 48px);
            font-weight: bold;
            color: #ff6b6b;
            text-shadow: 3px 3px 6px rgba(0,0,0,0.7);
            animation: comboShow 1.5s ease-out forwards;
            pointer-events: none;
            z-index: 1000;
            white-space: nowrap;
        }

        @keyframes comboShow {
            0% {
                transform: translate(-50%, -50%) scale(0) rotate(-180deg);
                opacity: 0;
            }
            15% {
                opacity: 1;
            }
            30% {
                transform: translate(-50%, -50%) scale(1.4) rotate(0deg);
            }
            100% {
                transform: translate(-50%, -50%) scale(1) translateY(-120px) rotate(10deg);
                opacity: 0;
            }
        }

        /* 响应式适配增强 */
        @media screen and (max-height: 600px) {
            .game-header { gap: 5px; }
            .game-info { padding: 6px 8px; min-height: 35px; }
            .power-ups { gap: 6px; }
            .power-up { width: clamp(40px, 7vw, 50px); height: clamp(40px, 7vw, 50px); }
        }

        @media screen and (max-height: 500px) and (orientation: landscape) {
            .game-wrapper { gap: 5px; }
            .title { font-size: clamp(1.5rem, 6vw, 2.5rem); margin-bottom: 10px; }
            .btn { padding: 10px 20px; margin: 5px; min-height: 40px; }
        }

        /* iOS安全区域适配 */
        @supports (padding: max(0px)) {
            .game-wrapper {
                padding-top: max(env(safe-area-inset-top), 10px);
                padding-bottom: max(env(safe-area-inset-bottom), 10px);
            }
        }

        /* 防止iOS缩放 */
        input, select, textarea, button {
            font-size: 16px;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- 主菜单 -->
        <div id="mainMenu" class="screen active">
            <div class="love-message">
                ❤️ 为我最爱的Ashley定制的专属游戏 ❤️<br>
                希望每一天都充满快乐和甜蜜！
            </div>
            <h1 class="title">🍎 苹果消消乐</h1>
            <button class="btn" onclick="showLevelSelect()">🎮 开始冒险</button>
            <button class="btn" onclick="showPractice()">🏃‍♀️ 练习场</button>
            <button class="btn" onclick="showInstructions()">📚 游戏说明</button>
            <button class="btn" onclick="showAchievements()">🏆 成就系统</button>
        </div>

        <!-- 关卡选择（增加到15个关卡） -->
        <div id="levelSelect" class="screen">
            <h2 class="title">选择关卡</h2>
            <div class="level-grid" id="levelGrid">
                <!-- 关卡将通过JavaScript生成 -->
            </div>
            <button class="btn" onclick="showMainMenu()">返回主菜单</button>
        </div>

        <!-- 其他界面保持不变，继续在第二部分提供JavaScript... -->
        <!-- 关卡确认 -->
        <div id="levelConfirm" class="screen">
            <h2 class="title" id="levelTitle">关卡 1 - 新手村</h2>
            <div class="love-message">
                <p id="levelDescription">这是一个适合新手的简单关卡，来熟悉游戏操作吧！</p>
                <div style="margin-top: 20px;">
                    <button class="btn" onclick="startGame()">🚀 开始游戏</button>
                    <button class="btn" onclick="showLevelSelect()">🔙 返回选择</button>
                </div>
            </div>
        </div>

        <!-- 练习场 -->
        <div id="practice" class="screen">
            <div class="game-wrapper">
                <div class="game-header">
                    <div class="game-info">❤️ <span id="practiceLives">∞</span></div>
                    <div class="game-info">⭐ <span id="practiceScore">0</span></div>
                    <div class="game-info">🎯 练习模式</div>
                </div>
                <div class="game-board-container">
                    <div class="game-board">
                        <div id="practiceGrid" class="grid"></div>
                    </div>
                </div>
                <div class="power-ups-container">
                    <div class="power-ups" id="practicePowerUps">
                        <!-- 道具将通过JavaScript生成 -->
                    </div>
                </div>
                <div class="game-controls">
                    <button class="control-btn" onclick="pauseGame()">⏸️ 暂停</button>
                    <button class="control-btn" onclick="resetPractice()">🔄 重置</button>
                    <button class="control-btn" onclick="showMainMenu()">🏠 返回</button>
                </div>
            </div>
        </div>

        <!-- 游戏界面 -->
        <div id="gameScreen" class="screen">
            <div class="game-wrapper">
                <div class="game-header">
                    <div class="game-info">❤️ <span id="lives">30</span></div>
                    <div class="game-info">⭐ <span id="score">0</span></div>
                    <div class="game-info">🎯 <span id="target">1000</span></div>
                </div>
                <div class="progress-container">
                    <div class="progress-bar">
                        <div id="progressFill" class="progress-fill" style="width: 0%"></div>
                    </div>
                </div>
                <div class="game-board-container">
                    <div class="game-board">
                        <div id="gameGrid" class="grid"></div>
                    </div>
                </div>
                <div class="power-ups-container">
                    <div class="power-ups" id="gamePowerUps">
                        <!-- 道具将通过JavaScript生成 -->
                    </div>
                </div>
                <div class="game-controls">
                    <button class="control-btn" onclick="pauseGame()">⏸️ 暂停</button>
                    <button class="control-btn" onclick="showLevelSelect()">📋 关卡</button>
                    <button class="control-btn" onclick="showMainMenu()">🏠 返回</button>
                </div>
            </div>
        </div>

        <!-- 成就系统 -->
        <div id="achievements" class="screen">
            <h2 class="title">🏆 成就系统</h2>
            <div id="achievementList" class="love-message" style="max-height: 60vh; overflow-y: auto;">
                <!-- 成就列表将通过JavaScript生成 -->
            </div>
            <button class="btn" onclick="showMainMenu()">返回主菜单</button>
        </div>

        <!-- 游戏说明 -->
        <div id="instructionsModal" class="screen">
            <h2 class="title">📚 游戏说明</h2>
            <div class="love-message" style="text-align: left; max-height: 70vh; overflow-y: auto;">
                <p><strong>🎮 基本玩法：</strong></p>
                <p>• 点击相邻的两个水果交换位置</p>
                <p>• 形成3个或更多相同水果的连线即可消除</p>
                <p>• 消除水果获得分数，达到目标分数即可过关</p>
                <br>
                <p><strong>✨ 特殊水果：</strong></p>
                <p>🌟 特殊水果：发光效果，消除得分翻倍</p>
                <p>🌈 超级水果：彩虹效果，消除得分x3</p>
                <p>💎 传说水果：终极效果，消除得分x5</p>
                <br>
                <p><strong>🔥 超级道具：</strong></p>
                <p>💣 炸弹：消除3x3区域</p>
                <p>🌈 彩虹球：消除所有同色水果</p>
                <p>🔨 锤子：直接消除单个水果</p>
                <p>🔄 交换：强制交换任意两个水果</p>
                <p>⚡ 闪电：消除整行和整列</p>
                <p>❄️ 冰冻：暂停时间，额外10步</p>
                <p>✨ 倍数：接下来得分x5</p>
                <p>🔀 洗牌：重新排列所有水果</p>
                <p>☄️ 流星：对角线消除</p>
                <p>🌪️ 龙卷风：随机消除15个水果</p>
                <p>🎭 魔法：变换所有水果类型</p>
                <p>⏰ 时光：回到上一步状态</p>
                <br>
                <p><strong>🔥 连击系统：</strong></p>
                <p>连续消除会获得连击奖励，最高可达50连击！</p>
            </div>
            <button class="btn" onclick="showMainMenu()">开始游戏</button>
        </div>
    </div>

    <script>
        // 全局游戏变量
        let game = null;
        let currentLevel = 1;
        let gameMode = 'normal';
        let achievements = [];
        let gameHistory = [];

        // 15个关卡配置
        const levelConfig = {
            1: { target: 800, moves: 30, description: "Ashley的第一步冒险！熟悉游戏操作的温馨关卡 ❤️", name: "爱的起点", difficulty: 1 },
            2: { target: 1200, moves: 25, description: "果园里的第一次挑战，相信你可以的！", name: "甜蜜果园", difficulty: 1 },
            3: { target: 1800, moves: 20, description: "香蕉天堂在等你，加油我的宝贝！", name: "香蕉天堂", difficulty: 2 },
            4: { target: 2500, moves: 25, description: "紫色迷境充满神秘，但你最聪明！", name: "紫色迷境", difficulty: 2 },
            5: { target: 3200, moves: 20, description: "草莓乐园的甜蜜挑战，就像我们的爱情", name: "草莓乐园", difficulty: 2 },
            6: { target: 4000, moves: 18, description: "柠檬挑战有点酸，但爱让一切变甜", name: "柠檬挑战", difficulty: 3 },
            7: { target: 5000, moves: 22, description: "樱桃小镇欢迎我们的公主！", name: "樱桃小镇", difficulty: 3 },
            8: { target: 6500, moves: 20, description: "猕猴桃森林的绿色奇迹等你发现", name: "奇异森林", difficulty: 3 },
            9: { target: 8000, moves: 18, description: "彩虹桥连接着我们的心", name: "彩虹桥", difficulty: 4 },
            10: { target: 10000, moves: 25, description: "水晶宫里的终极考验，我永远支持你", name: "水晶宫", difficulty: 4 },
            11: { target: 12500, moves: 20, description: "星空花园，像你眼中的星星一样美丽", name: "星空花园", difficulty: 4 },
            12: { target: 15000, moves: 22, description: "魔法城堡需要真正的公主来拯救", name: "魔法城堡", difficulty: 5 },
            13: { target: 18000, moves: 18, description: "天空之城，我们爱情的最高殿堂", name: "天空之城", difficulty: 5 },
            14: { target: 22000, moves: 20, description: "无尽深渊也阻止不了我的爱", name: "无尽深渊", difficulty: 5 },
            15: { target: 30000, moves: 25, description: "永恒国度，就像我们的爱情一样永恒 💖", name: "永恒国度", difficulty: 6 }
        };

        // 成就系统
        const achievementConfig = {
            firstWin: { name: "初次胜利", desc: "完成第一个关卡", icon: "🏆", unlocked: false },
            comboMaster: { name: "连击大师", desc: "达到10连击", icon: "🔥", unlocked: false },
            powerUpLover: { name: "道具爱好者", desc: "使用50个道具", icon: "✨", unlocked: false },
            speedRunner: { name: "速度之王", desc: "在15秒内完成一个关卡", icon: "⚡", unlocked: false },
            perfectScore: { name: "完美分数", desc: "单局得分超过50000", icon: "💯", unlocked: false },
            legendary: { name: "传说玩家", desc: "完成所有关卡", icon: "👑", unlocked: false },
            lovelyAshley: { name: "最爱的Ashley", desc: "专属成就 - 你就是我的全世界", icon: "💕", unlocked: true }
        };

        // 超强音效系统
        function playEnhancedSound(type = 'match', intensity = 1, pitch = 1) {
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                const filterNode = audioContext.createBiquadFilter();
                
                oscillator.connect(filterNode);
                filterNode.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                let frequency, duration, volume, filterFreq;
                
                switch(type) {
                    case 'match':
                        frequency = 440 + (pitch * 100);
                        duration = 0.15;
                        volume = 0.1 * intensity;
                        filterFreq = 1000;
                        break;
                    case 'combo':
                        frequency = 523 + (intensity * 50);
                        duration = 0.25;
                        volume = 0.15 * intensity;
                        filterFreq = 2000;
                        break;
                    case 'super_combo':
                        frequency = 659 + (intensity * 80);
                        duration = 0.4;
                        volume = 0.2 * intensity;
                        filterFreq = 3000;
                        break;
                    case 'legendary_combo':
                        frequency = 880 + (intensity * 100);
                        duration = 0.6;
                        volume = 0.25 * intensity;
                        filterFreq = 4000;
                        break;
                    case 'powerup':
                        frequency = 1047;
                        duration = 0.3;
                        volume = 0.2;
                        filterFreq = 2500;
                        break;
                    case 'victory':
                        frequency = 1319;
                        duration = 1.0;
                        volume = 0.3;
                        filterFreq = 5000;
                        break;
                }
                
                oscillator.frequency.setValueAtTime(frequency, audioContext.currentTime);
                filterNode.frequency.setValueAtTime(filterFreq, audioContext.currentTime);
                filterNode.Q.setValueAtTime(10, audioContext.currentTime);
                gainNode.gain.setValueAtTime(volume, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + duration);
                
                oscillator.start(audioContext.currentTime);
                oscillator.stop(audioContext.currentTime + duration);
            } catch (e) {
                console.log('音频播放失败');
            }
        }

        // 超级增强游戏类
        class SuperAppleMatchGame {
            constructor() {
                this.gridSize = 8;
                this.grid = [];
                this.score = 0;
                this.lives = 30;
                this.target = 1000;
                this.selectedCell = null;
                this.fruits = ['apple', 'orange', 'banana', 'grape', 'strawberry', 'lemon', 'cherry', 'kiwi'];
                this.fruitEmojis = {
                    'apple': '🍎', 'orange': '🍊', 'banana': '🍌', 'grape': '🍇',
                    'strawberry': '🍓', 'lemon': '🍋', 'cherry': '🍒', 'kiwi': '🥝'
                };
                this.isPaused = false;
                this.activePowerUp = null;
                this.combo = 0;
                this.maxCombo = 0;
                this.isAnimating = false;
                this.currentGridId = 'gameGrid';
                this.multiplier = 1;
                this.multiplierTimeLeft = 0;
                this.frozenTime = 0;
                this.powerUpUsageCount = 0;
                this.gameStartTime = Date.now();
                this.totalMatches = 0;
                
                // 特殊水果概率（大幅提升）
                this.specialFruitChance = 0.12;
                this.ultraFruitChance = 0.06;
                this.megaFruitChance = 0.03;
                this.legendaryFruitChance = 0.01;
                
                // 12种超级道具
                this.powerUps = {
                    bomb: 5, rainbow: 3, hammer: 8, swap: 5,
                    lightning: 3, freeze: 3, multiplier: 2, shuffle: 3,
                    meteor: 2, tornado: 2, magic: 1, time: 2
                };
                
                // 20种连击效果
                this.comboEffects = {
                    3: { text: "太棒了！", color: "#4caf50", shake: false, sound: 'combo' },
                    5: { text: "连击开始！", color: "#ff9800", shake: false, sound: 'combo' },
                    7: { text: "Amazing！", color: "#f44336", shake: true, sound: 'combo' },
                    10: { text: "Perfect！", color: "#9c27b0", shake: true, sound: 'super_combo' },
                    12: { text: "Fantastic！", color: "#3f51b5", shake: true, sound: 'super_combo' },
                    15: { text: "Incredible！", color: "#ff6b6b", shake: true, sound: 'super_combo' },
                    18: { text: "Marvelous！", color: "#00bcd4", shake: true, sound: 'super_combo' },
                    20: { text: "Legendary！", color: "#ffd700", shake: true, sound: 'legendary_combo' },
                    25: { text: "Godlike！", color: "#ff4081", shake: true, sound: 'legendary_combo' },
                    30: { text: "Unstoppable！", color: "#7c4dff", shake: true, sound: 'legendary_combo' },
                    35: { text: "Phenomenal！", color: "#ff5722", shake: true, sound: 'legendary_combo' },
                    40: { text: "Otherworldly！", color: "#4caf50", shake: true, sound: 'legendary_combo' },
                    45: { text: "Divine！", color: "#ff9800", shake: true, sound: 'legendary_combo' },
                    50: { text: "ASHLEY'S LOVE！💖", color: "#e91e63", shake: true, sound: 'legendary_combo' }
                };
                
                this.previousGameState = null;
            }

            // 初始化游戏
            init() {
                this.saveGameState();
                this.initGrid();
                this.generateNewFruits();
                this.render();
                this.updateUI();
                this.updatePowerUpDisplay();
            }

            // 保存游戏状态（用于时光道具）
            saveGameState() {
                this.previousGameState = {
                    grid: JSON.parse(JSON.stringify(this.grid)),
                    score: this.score,
                    lives: this.lives,
                    combo: this.combo
                };
            }

            // 初始化网格
            initGrid() {
                this.grid = [];
                for (let i = 0; i < this.gridSize; i++) {
                    this.grid[i] = [];
                    for (let j = 0; j < this.gridSize; j++) {
                        this.grid[i][j] = {
                            fruit: null,
                            special: 0 // 0=普通，1=特殊，2=超级，3=传说，4=神话
                        };
                    }
                }
            }

            // 生成新水果（增强版）
            generateNewFruits() {
                for (let i = 0; i < this.gridSize; i++) {
                    for (let j = 0; j < this.gridSize; j++) {
                        if (!this.grid[i][j].fruit) {
                            let newFruit;
                            let attempts = 0;
                            do {
                                newFruit = this.fruits[Math.floor(Math.random() * this.fruits.length)];
                                attempts++;
                            } while (this.wouldCreateMatch(i, j, newFruit) && attempts < 20);
                            
                            this.grid[i][j].fruit = newFruit;
                            
                            // 增强特殊水果生成
                            const random = Math.random();
                            if (random < this.legendaryFruitChance) {
                                this.grid[i][j].special = 4; // 神话
                            } else if (random < this.megaFruitChance) {
                                this.grid[i][j].special = 3; // 传说
                            } else if (random < this.ultraFruitChance) {
                                this.grid[i][j].special = 2; // 超级
                            } else if (random < this.specialFruitChance) {
                                this.grid[i][j].special = 1; // 特殊
                            } else {
                                this.grid[i][j].special = 0; // 普通
                            }
                        }
                    }
                }
            }

            // 智能匹配检测
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

            // 增强渲染系统
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
                            
                            // 根据特殊等级添加效果
                            switch(this.grid[i][j].special) {
                                case 1: fruit.classList.add('special-fruit'); break;
                                case 2: fruit.classList.add('ultra-fruit'); break;
                                case 3: fruit.classList.add('mega-fruit'); break;
                                case 4: fruit.classList.add('legendary-fruit'); break;
                            }
                            
                            fruit.textContent = this.fruitEmojis[this.grid[i][j].fruit];
                            cell.appendChild(fruit);
                        }
                        
                        cell.addEventListener('click', (e) => this.handleCellClick(e));
                        cell.addEventListener('touchstart', (e) => {
                            e.preventDefault();
                            this.handleCellClick(e);
                        }, { passive: false });
                        
                        gridElement.appendChild(cell);
                    }
                }
                this.updateCellDisplay();
            }

            // 处理点击事件
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
                        if (this.lives > 0) this.lives--;
                        this.updateUI();
                    } else {
                        this.clearSelection();
                        this.selectCell(row, col);
                    }
                } else {
                    this.selectCell(row, col);
                }
            }

            // 处理道具点击
            handlePowerUpClick(row, col) {
                if (this.powerUps[this.activePowerUp] <= 0) {
                    this.activePowerUp = null;
                    this.updatePowerUpDisplay();
                    return;
                }

                this.saveGameState();
                
                switch(this.activePowerUp) {
                    case 'bomb': this.useBomb(row, col); break;
                    case 'rainbow': this.useRainbow(row, col); break;
                    case 'hammer': this.useHammer(row, col); break;
                    case 'swap':
                        if (!this.selectedCell) {
                            this.selectCell(row, col);
                        } else {
                            this.forceSwap(this.selectedCell, {row, col});
                        }
                        return;
                    case 'lightning': this.useLightning(row, col); break;
                    case 'freeze': this.useFreeze(); break;
                    case 'multiplier': this.useMultiplier(); break;
                    case 'shuffle': this.useShuffle(); break;
                    case 'meteor': this.useMeteor(row, col); break;
                    case 'tornado': this.useTornado(); break;
                    case 'magic': this.useMagic(); break;
                    case 'time': this.useTimeMachine(); break;
                }
                
                this.powerUps[this.activePowerUp]--;
                this.powerUpUsageCount++;
                this.activePowerUp = null;
                this.updatePowerUpDisplay();
                this.processAfterAction();
            }

            // 12种超级道具效果

            // 1. 增强炸弹
            useBomb(row, col) {
                playEnhancedSound('powerup');
                this.createExplosionEffect(row, col);
                let destroyed = 0;
                
                for (let i = Math.max(0, row - 1); i <= Math.min(this.gridSize - 1, row + 1); i++) {
                    for (let j = Math.max(0, col - 1); j <= Math.min(this.gridSize - 1, col + 1); j++) {
                        if (this.grid[i][j].fruit) {
                            destroyed++;
                            const specialBonus = (this.grid[i][j].special + 1) * 50;
                            this.grid[i][j].fruit = null;
                            this.grid[i][j].special = 0;
                            this.createParticleEffect(i, j, '💥');
                        }
                    }
                }
                
                const points = destroyed * 80 * this.multiplier;
                this.addScore(points);
                this.showScorePopup(row, col, `+${points}`);
                this.shakeBoard();
            }

            // 2. 增强彩虹球
            useRainbow(row, col) {
                if (this.grid[row][col].fruit) {
                    const targetFruit = this.grid[row][col].fruit;
                    let count = 0;
                    const positions = [];
                    
                    for (let i = 0; i < this.gridSize; i++) {
                        for (let j = 0; j < this.gridSize; j++) {
                            if (this.grid[i][j].fruit === targetFruit) {
                                this.grid[i][j].fruit = null;
                                this.grid[i][j].special = 0;
                                count++;
                                positions.push({i, j});
                            }
                        }
                    }
                    
                    // 彩虹特效
                    positions.forEach(pos => {
                        setTimeout(() => {
                            this.createParticleEffect(pos.i, pos.j, '🌈');
                        }, Math.random() * 300);
                    });
                    
                    const points = count * 120 * this.multiplier;
                    this.addScore(points);
                    this.showScorePopup(row, col, `+${points}`);
                    playEnhancedSound('powerup', 1.5);
                }
            }

            // 3. 增强锤子
            useHammer(row, col) {
                if (this.grid[row][col].fruit) {
                    const specialMultiplier = (this.grid[row][col].special + 1);
                    const points = specialMultiplier * 100 * this.multiplier;
                    this.grid[row][col].fruit = null;
                    this.grid[row][col].special = 0;
                    this.addScore(points);
                    this.showScorePopup(row, col, `+${points}`);
                    playEnhancedSound('powerup');
                    this.createParticleEffect(row, col, '🔨');
                }
            }

            // 4. 增强闪电
            useLightning(row, col) {
                let destroyed = 0;
                const positions = [];
                
                // 消除整行
                for (let j = 0; j < this.gridSize; j++) {
                    if (this.grid[row][j].fruit) {
                        destroyed++;
                        this.grid[row][j].fruit = null;
                        this.grid[row][j].special = 0;
                        positions.push({i: row, j});
                    }
                }
                
                // 消除整列
                for (let i = 0; i < this.gridSize; i++) {
                    if (this.grid[i][col].fruit) {
                        destroyed++;
                        this.grid[i][col].fruit = null;
                        this.grid[i][col].special = 0;
                        positions.push({i, j: col});
                    }
                }
                
                // 闪电特效
                positions.forEach(pos => {
                    setTimeout(() => {
                        this.createParticleEffect(pos.i, pos.j, '⚡');
                    }, Math.random() * 200);
                });
                
                const points = destroyed * 90 * this.multiplier;
                this.addScore(points);
                this.showScorePopup(row, col, `+${points}`);
                playEnhancedSound('powerup', 2);
                this.shakeBoard();
            }

            // 5. 冰冻时间
            useFreeze() {
                this.frozenTime = 10; // 暂停时间，额外10步
                this.lives += 10;
                this.updateUI();
                this.showScorePopup(4, 4, "时间冰冻！+10步");
                playEnhancedSound('powerup', 1.2);
                this.createScreenEffect('❄️');
            }

            // 6. 分数倍数
            useMultiplier() {
                this.multiplier = 5;
                this.multiplierTimeLeft = 5; // 5次操作内得分x5
                this.showScorePopup(4, 4, "得分x5！");
                playEnhancedSound('powerup', 1.8);
                this.createScreenEffect('✨');
            }

            // 7. 洗牌
            useShuffle() {
                const fruits = [];
                const specials = [];
                
                // 收集所有水果和特殊属性
                for (let i = 0; i < this.gridSize; i++) {
                    for (let j = 0; j < this.gridSize; j++) {
                        if (this.grid[i][j].fruit) {
                            fruits.push(this.grid[i][j].fruit);
                            specials.push(this.grid[i][j].special);
                        }
                    }
                }
                
                // 清空网格
                this.initGrid();
                
                // 重新随机分配
                for (let k = 0; k < fruits.length; k++) {
                    let placed = false;
                    while (!placed) {
                        const i = Math.floor(Math.random() * this.gridSize);
                        const j = Math.floor(Math.random() * this.gridSize);
                        if (!this.grid[i][j].fruit) {
                            this.grid[i][j].fruit = fruits[k];
                            this.grid[i][j].special = specials[k];
                            placed = true;
                        }
                    }
                }
                
                this.render();
                this.showScorePopup(4, 4, "重新洗牌！");
                playEnhancedSound('powerup');
                this.createScreenEffect('🔀');
            }

            // 8. 流星攻击
            useMeteor(row, col) {
                let destroyed = 0;
                const positions = [];
                
                // 对角线消除
                const directions = [[-1, -1], [-1, 1], [1, -1], [1, 1]];
                directions.forEach(dir => {
                    for (let step = 0; step < this.gridSize; step++) {
                        const newRow = row + dir[0] * step;
                        const newCol = col + dir[1] * step;
                        if (newRow >= 0 && newRow < this.gridSize && newCol >= 0 && newCol < this.gridSize) {
                            if (this.grid[newRow][newCol].fruit) {
                                destroyed++;
                                this.grid[newRow][newCol].fruit = null;
                                this.grid[newRow][newCol].special = 0;
                                positions.push({i: newRow, j: newCol});
                            }
                        }
                    }
                });
                
                // 流星特效
                positions.forEach((pos, index) => {
                    setTimeout(() => {
                        this.createParticleEffect(pos.i, pos.j, '☄️');
                    }, index * 50);
                });
                
                const points = destroyed * 110 * this.multiplier;
                this.addScore(points);
                this.showScorePopup(row, col, `+${points}`);
                playEnhancedSound('powerup', 2.2);
                this.shakeBoard();
            }

            // 9. 龙卷风
            useTornado() {
                const positions = [];
                let destroyed = 0;
                
                // 随机选择15个有水果的位置
                const availablePositions = [];
                for (let i = 0; i < this.gridSize; i++) {
                    for (let j = 0; j < this.gridSize; j++) {
                        if (this.grid[i][j].fruit) {
                            availablePositions.push({i, j});
                        }
                    }
                }
                
                const targets = availablePositions
                    .sort(() => Math.random() - 0.5)
                    .slice(0, Math.min(15, availablePositions.length));
                
                targets.forEach(pos => {
                    if (this.grid[pos.i][pos.j].fruit) {
                        destroyed++;
                        this.grid[pos.i][pos.j].fruit = null;
                        this.grid[pos.i][pos.j].special = 0;
                        positions.push(pos);
                    }
                });
                
                // 龙卷风螺旋特效
                positions.forEach((pos, index) => {
                    setTimeout(() => {
                        this.createParticleEffect(pos.i, pos.j, '🌪️');
                    }, index * 80);
                });
                
                const points = destroyed * 95 * this.multiplier;
                this.addScore(points);
                this.showScorePopup(4, 4, `+${points}`);
                playEnhancedSound('powerup', 2.5);
                this.createScreenEffect('🌪️');
            }

            // 10. 魔法变换
            useMagic() {
                const newFruitType = this.fruits[Math.floor(Math.random() * this.fruits.length)];
                let transformed = 0;
                
                for (let i = 0; i < this.gridSize; i++) {
                    for (let j = 0; j < this.gridSize; j++) {
                        if (this.grid[i][j].fruit && Math.random() < 0.6) {
                            this.grid[i][j].fruit = newFruitType;
                            transformed++;
                            setTimeout(() => {
                                this.createParticleEffect(i, j, '🎭');
                            }, Math.random() * 500);
                        }
                    }
                }
                
                this.render();
                const points = transformed * 60 * this.multiplier;
                this.addScore(points);
                this.showScorePopup(4, 4, `魔法变换！+${points}`);
                playEnhancedSound('powerup', 1.5);
                this.createScreenEffect('✨');
            }

            // 11. 时光机器
            useTimeMachine() {
                if (this.previousGameState) {
                    this.grid = JSON.parse(JSON.stringify(this.previousGameState.grid));
                    this.score = this.previousGameState.score;
                    this.lives = this.previousGameState.lives;
                    this.combo = this.previousGameState.combo;
                    
                    this.render();
                    this.updateUI();
                    this.showScorePopup(4, 4, "时光倒流！");
                    playEnhancedSound('powerup', 1.3);
                    this.createScreenEffect('⏰');
                }
            }

            // 强制交换
            forceSwap(pos1, pos2) {
                const temp = { ...this.grid[pos1.row][pos1.col] };
                this.grid[pos1.row][pos1.col] = { ...this.grid[pos2.row][pos2.col] };
                this.grid[pos2.row][pos2.col] = temp;
                
                this.render();
                this.clearSelection();
                this.showScorePopup(pos1.row, pos1.col, "强制交换！");
                playEnhancedSound('powerup');
            }

            // 创建各种特效
            createExplosionEffect(row, col) {
                const cell = document.querySelector(`[data-row="${row}"][data-col="${col}"]`);
                if (cell) {
                    cell.style.background = 'radial-gradient(circle, #ff6b6b 0%, #ff8e53 100%)';
                    setTimeout(() => {
                        cell.style.background = '';
                    }, 300);
                }
            }

            createParticleEffect(row, col, emoji) {
                const gameBoard = document.querySelector('.game-board');
                if (!gameBoard) return;
                
                const particle = document.createElement('div');
                particle.textContent = emoji;
                particle.style.cssText = `
                    position: absolute;
                    font-size: 24px;
                    pointer-events: none;
                    z-index: 1000;
                    animation: particleFloat 1s ease-out forwards;
                `;
                
                const rect = gameBoard.getBoundingClientRect();
                const cellSize = rect.width / 8;
                particle.style.left = `${col * cellSize + cellSize/2}px`;
                particle.style.top = `${row * cellSize + cellSize/2}px`;
                
                gameBoard.appendChild(particle);
                
                setTimeout(() => {
                    if (particle.parentNode) {
                        particle.parentNode.removeChild(particle);
                    }
                }, 1000);
            }

            createScreenEffect(emoji) {
                const gameBoard = document.querySelector('.game-board');
                if (!gameBoard) return;
                
                for (let i = 0; i < 20; i++) {
                    setTimeout(() => {
                        const effect = document.createElement('div');
                        effect.textContent = emoji;
                        effect.style.cssText = `
                            position: absolute;
                            font-size: ${16 + Math.random() * 16}px;
                            pointer-events: none;
                            z-index: 1000;
                            left: ${Math.random() * 100}%;
                            top: ${Math.random() * 100}%;
                            animation: screenEffectFade 2s ease-out forwards;
                        `;
                        gameBoard.appendChild(effect);
                        
                        setTimeout(() => {
                            if (effect.parentNode) {
                                effect.parentNode.removeChild(effect);
                            }
                        }, 2000);
                    }, i * 100);
                }
            }

            // 震动效果
            shakeBoard() {
                const gameBoard = document.querySelector('.game-board');
                if (gameBoard) {
                    gameBoard.style.animation = 'shake 0.5s ease-in-out';
                    setTimeout(() => {
                        gameBoard.style.animation = '';
                    }, 500);
                }
            }

            // 显示分数弹出
            showScorePopup(row, col, text) {
                const gameBoard = document.querySelector('.game-board');
                if (!gameBoard) return;
                
                const popup = document.createElement('div');
                popup.textContent = text;
                popup.style.cssText = `
                    position: absolute;
                    color: #ff6b6b;
                    font-weight: bold;
                    font-size: 20px;
                    pointer-events: none;
                    z-index: 1000;
                    animation: scorePopup 1s ease-out forwards;
                    text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
                `;
                
                const rect = gameBoard.getBoundingClientRect();
                const cellSize = rect.width / 8;
                popup.style.left = `${col * cellSize + cellSize/2}px`;
                popup.style.top = `${row * cellSize + cellSize/2}px`;
                
                gameBoard.appendChild(popup);
                
                setTimeout(() => {
                    if (popup.parentNode) {
                        popup.parentNode.removeChild(popup);
                    }
                }, 1000);
            }

            // 选择和交换逻辑
            selectCell(row, col) {
                if (this.grid[row][col].fruit) {
                    this.clearSelection();
                    this.selectedCell = {row, col};
                    this.updateCellDisplay();
                }
            }

            clearSelection() {
                this.selectedCell = null;
                this.updateCellDisplay();
            }

            isAdjacent(pos1, pos2) {
                const rowDiff = Math.abs(pos1.row - pos2.row);
                const colDiff = Math.abs(pos1.col - pos2.col);
                return (rowDiff === 1 && colDiff === 0) || (rowDiff === 0 && colDiff === 1);
            }

            updateCellDisplay() {
                const cells = document.querySelectorAll(`#${this.currentGridId} .cell`);
                cells.forEach(cell => {
                    cell.classList.remove('selected');
                    if (this.selectedCell && 
                        cell.dataset.row == this.selectedCell.row && 
                        cell.dataset.col == this.selectedCell.col) {
                        cell.classList.add('selected');
                    }
                });
            }

            // 水果交换和匹配检测
            swapFruits(pos1, pos2) {
                const temp = { ...this.grid[pos1.row][pos1.col] };
                this.grid[pos1.row][pos1.col] = { ...this.grid[pos2.row][pos2.col] };
                this.grid[pos2.row][pos2.col] = temp;
                
                const matches = this.findMatches();
                if (matches.length > 0) {
                    this.render();
                    this.clearSelection();
                    this.processMatches(matches);
                } else {
                    // 交换回来
                    const temp = { ...this.grid[pos1.row][pos1.col] };
                    this.grid[pos1.row][pos1.col] = { ...this.grid[pos2.row][pos2.col] };
                    this.grid[pos2.row][pos2.col] = temp;
                    this.lives++; // 恢复生命
                }
                
                this.render();
                this.clearSelection();
            }

            // 寻找匹配
            findMatches() {
                const matches = [];
                const visited = new Set();
                
                // 检查水平匹配
                for (let row = 0; row < this.gridSize; row++) {
                    let count = 1;
                    let currentFruit = this.grid[row][0].fruit;
                    
                    for (let col = 1; col < this.gridSize; col++) {
                        if (this.grid[row][col].fruit === currentFruit && currentFruit !== null) {
                            count++;
                        } else {
                            if (count >= 3) {
                                for (let i = col - count; i < col; i++) {
                                    matches.push({row, col: i});
                                }
                            }
                            count = 1;
                            currentFruit = this.grid[row][col].fruit;
                        }
                    }
                    if (count >= 3) {
                        for (let i = this.gridSize - count; i < this.gridSize; i++) {
                            matches.push({row, col: i});
                        }
                    }
                }
                
                // 检查垂直匹配
                for (let col = 0; col < this.gridSize; col++) {
                    let count = 1;
                    let currentFruit = this.grid[0][col].fruit;
                    
                    for (let row = 1; row < this.gridSize; row++) {
                        if (this.grid[row][col].fruit === currentFruit && currentFruit !== null) {
                            count++;
                        } else {
                            if (count >= 3) {
                                for (let i = row - count; i < row; i++) {
                                    matches.push({row: i, col});
                                }
                            }
                            count = 1;
                            currentFruit = this.grid[row][col].fruit;
                        }
                    }
                    if (count >= 3) {
                        for (let i = this.gridSize - count; i < this.gridSize; i++) {
                            matches.push({row: i, col});
                        }
                    }
                }
                
                return matches.filter((match, index, self) => 
                    self.findIndex(m => m.row === match.row && m.col === match.col) === index
                );
            }

            // 处理匹配
            processMatches(matches) {
                if (matches.length === 0) return;
                
                this.isAnimating = true;
                this.combo++;
                this.maxCombo = Math.max(this.maxCombo, this.combo);
                
                let totalScore = 0;
                let specialBonusTotal = 0;
                
                // 计算得分
                matches.forEach(match => {
                    const cell = this.grid[match.row][match.col];
                    let baseScore = 100;
                    let specialMultiplier = 1;
                    
                    switch(cell.special) {
                        case 1: specialMultiplier = 2; break;
                        case 2: specialMultiplier = 3; break;
                        case 3: specialMultiplier = 5; break;
                        case 4: specialMultiplier = 8; break;
                    }
                    
                    const comboMultiplier = 1 + (this.combo * 0.1);
                    const score = baseScore * specialMultiplier * comboMultiplier * this.multiplier;
                    totalScore += score;
                    specialBonusTotal += (specialMultiplier - 1) * baseScore;
                    
                    // 清除水果
                    cell.fruit = null;
                    cell.special = 0;
                    
                    // 粒子效果
                    setTimeout(() => {
                        this.createParticleEffect(match.row, match.col, '✨');
                    }, Math.random() * 200);
                });
                
                this.addScore(Math.floor(totalScore));
                
                // 播放连击音效
                if (this.combo >= 20) {
                    playEnhancedSound('legendary_combo', this.combo / 10);
                } else if (this.combo >= 10) {
                    playEnhancedSound('super_combo', this.combo / 5);
                } else {
                    playEnhancedSound('combo', Math.min(this.combo / 3, 3));
                }
                
                // 显示连击效果
                this.showComboEffect();
                
                // 倍数递减
                if (this.multiplierTimeLeft > 0) {
                    this.multiplierTimeLeft--;
                    if (this.multiplierTimeLeft === 0) {
                        this.multiplier = 1;
                    }
                }
                
                // 延迟处理重力和新匹配
                setTimeout(() => {
                    this.applyGravity();
                    this.generateNewFruits();
                    this.render();
                    
                    setTimeout(() => {
                        const newMatches = this.findMatches();
                        if (newMatches.length > 0) {
                            this.processMatches(newMatches);
                        } else {
                            this.combo = 0;
                            this.isAnimating = false;
                            this.checkGameStatus();
                        }
                    }, 300);
                }, 200);
            }

            // 显示连击效果
            showComboEffect() {
                if (this.combo < 3) return;
                
                const effect = this.comboEffects[this.combo] || 
                    this.comboEffects[Object.keys(this.comboEffects).reverse().find(key => key <= this.combo)];
                
                if (!effect) return;
                
                const gameBoard = document.querySelector('.game-board');
                if (!gameBoard) return;
                
                const comboText = document.createElement('div');
                comboText.className = 'combo-text';
                comboText.textContent = `${this.combo} 连击！${effect.text}`;
                comboText.style.color = effect.color;
                
                gameBoard.appendChild(comboText);
                
                if (effect.shake) {
                    this.shakeBoard();
                }
                
                setTimeout(() => {
                    if (comboText.parentNode) {
                        comboText.parentNode.removeChild(comboText);
                    }
                }, 1500);
            }

            // 重力效果
            applyGravity() {
                let moved = false;
                
                do {
                    moved = false;
                    for (let col = 0; col < this.gridSize; col++) {
                        for (let row = this.gridSize - 2; row >= 0; row--) {
                            if (this.grid[row][col].fruit && !this.grid[row + 1][col].fruit) {
                                this.grid[row + 1][col] = { ...this.grid[row][col] };
                                this.grid[row][col] = { fruit: null, special: 0 };
                                moved = true;
                            }
                        }
                    }
                } while (moved);
            }

            // 其他辅助方法
            addScore(points) {
                this.score += points;
                this.totalMatches++;
                this.updateUI();
                this.checkAchievements();
            }

            processAfterAction() {
                this.applyGravity();
                this.generateNewFruits();
                this.render();
                
                setTimeout(() => {
                    const matches = this.findMatches();
                    if (matches.length > 0) {
                        this.processMatches(matches);
                    }
                }, 200);
            }

            updateUI() {
                const elements = {
                    lives: document.getElementById('lives'),
                    score: document.getElementById('score'),
                    target: document.getElementById('target'),
                    progressFill: document.getElementById('progressFill'),
                    practiceLives: document.getElementById('practiceLives'),
                    practiceScore: document.getElementById('practiceScore')
                };
                
                if (elements.lives) elements.lives.textContent = this.lives;
                if (elements.score) elements.score.textContent = this.score.toLocaleString();
                if (elements.target) elements.target.textContent = this.target.toLocaleString();
                if (elements.progressFill) {
                    const progress = Math.min((this.score / this.target) * 100, 100);
                    elements.progressFill.style.width = `${progress}%`;
                }
                if (elements.practiceLives) elements.practiceLives.textContent = '∞';
                if (elements.practiceScore) elements.practiceScore.textContent = this.score.toLocaleString();
            }

            updatePowerUpDisplay() {
                const containers = ['gamePowerUps', 'practicePowerUps'];
                
                containers.forEach(containerId => {
                    const container = document.getElementById(containerId);
                    if (!container) return;
                    
                    container.innerHTML = '';
                    
                    Object.keys(this.powerUps).forEach(powerUp => {
                        const button = document.createElement('button');
                        button.className = `power-up ${powerUp}`;
                        button.textContent = this.getPowerUpEmoji(powerUp);
                        
                        if (this.powerUps[powerUp] > 0) {
                            const count = document.createElement('span');
                            count.className = 'power-up-count';
                            count.textContent = this.powerUps[powerUp];
                            button.appendChild(count);
                        } else {
                            button.classList.add('disabled');
                        }
                        
                        if (this.activePowerUp === powerUp) {
                            button.classList.add('active');
                        }
                        
                        button.addEventListener('click', () => this.selectPowerUp(powerUp));
                        container.appendChild(button);
                    });
                });
            }

            getPowerUpEmoji(powerUp) {
                const emojis = {
                    bomb: '💣', rainbow: '🌈', hammer: '🔨', swap: '🔄',
                    lightning: '⚡', freeze: '❄️', multiplier: '✨', shuffle: '🔀',
                    meteor: '☄️', tornado: '🌪️', magic: '🎭', time: '⏰'
                };
                return emojis[powerUp] || '❓';
            }

            selectPowerUp(powerUp) {
                if (this.powerUps[powerUp] <= 0) return;
                
                if (this.activePowerUp === powerUp) {
                    this.activePowerUp = null;
                } else {
                    this.activePowerUp = powerUp;
                }
                
                this.updatePowerUpDisplay();
                
                // 特殊道具立即生效
                if (['freeze', 'multiplier', 'shuffle', 'tornado', 'magic', 'time'].includes(powerUp) && this.activePowerUp === powerUp) {
                    setTimeout(() => this.handlePowerUpClick(0, 0), 100);
                }
            }

            checkGameStatus() {
                if (this.score >= this.target) {
                    this.winGame();
                } else if (this.lives <= 0) {
                    this.gameOver();
                }
            }

            winGame() {
                playEnhancedSound('victory');
                const gameTime = (Date.now() - this.gameStartTime) / 1000;
                
                // 解锁成就
                if (currentLevel === 1 && !achievementConfig.firstWin.unlocked) {
                    achievementConfig.firstWin.unlocked = true;
                    this.showAchievement('firstWin');
                }
                
                if (gameTime < 15 && !achievementConfig.speedRunner.unlocked) {
                    achievementConfig.speedRunner.unlocked = true;
                    this.showAchievement('speedRunner');
                }
                
                if (this.score > 50000 && !achievementConfig.perfectScore.unlocked) {
                    achievementConfig.perfectScore.unlocked = true;
                    this.showAchievement('perfectScore');
                }
                
                if (this.maxCombo >= 10 && !achievementConfig.comboMaster.unlocked) {
                    achievementConfig.comboMaster.unlocked = true;
                    this.showAchievement('comboMaster');
                }
                
                if (this.powerUpUsageCount >= 50 && !achievementConfig.powerUpLover.unlocked) {
                    achievementConfig.powerUpLover.unlocked = true;
                    this.showAchievement('powerUpLover');
                }
                
                // 解锁下一关
                if (currentLevel < 15) {
                    localStorage.setItem(`level_${currentLevel + 1}_unlocked`, 'true');
                }
                
                if (currentLevel === 15 && !achievementConfig.legendary.unlocked) {
                    achievementConfig.legendary.unlocked = true;
                    this.showAchievement('legendary');
                }
                
                localStorage.setItem(`level_${currentLevel}_completed`, 'true');
                localStorage.setItem('achievements', JSON.stringify(achievementConfig));
                
                setTimeout(() => {
                    alert(`🎉 恭喜Ashley过关！\n得分: ${this.score.toLocaleString()}\n最高连击: ${this.maxCombo}\n用时: ${Math.floor(gameTime)}秒`);
                    showLevelSelect();
                }, 1000);
            }

            gameOver() {
                setTimeout(() => {
                    alert(`游戏结束！\n得分: ${this.score.toLocaleString()}\n最高连击: ${this.maxCombo}`);
                    showLevelSelect();
                }, 500);
            }

            showAchievement(achievementId) {
                const achievement = achievementConfig[achievementId];
                if (!achievement) return;
                
                const popup = document.createElement('div');
                popup.innerHTML = `
                    <div style="
                        position: fixed;
                        top: 50%;
                        left: 50%;
                        transform: translate(-50%, -50%);
                        background: linear-gradient(45deg, #ffd700, #ffed4e);
                        color: #333;
                        padding: 20px;
                        border-radius: 20px;
                        text-align: center;
                        z-index: 10000;
                        box-shadow: 0 10px 30px rgba(0,0,0,0.3);
                        animation: achievementShow 3s ease-out forwards;
                    ">
                        <div style="font-size: 48px; margin-bottom: 10px;">${achievement.icon}</div>
                        <div style="font-weight: bold; font-size: 18px; margin-bottom: 5px;">成就解锁！</div>
                        <div style="font-size: 16px; margin-bottom: 5px;">${achievement.name}</div>
                        <div style="font-size: 14px; opacity: 0.8;">${achievement.desc}</div>
                    </div>
                `;
                
                document.body.appendChild(popup);
                
                setTimeout(() => {
                    if (popup.parentNode) {
                        popup.parentNode.removeChild(popup);
                    }
                }, 3000);
            }

            checkAchievements() {
                // 检查各种成就条件
                if (this.maxCombo >= 10 && !achievementConfig.comboMaster.unlocked) {
                    achievementConfig.comboMaster.unlocked = true;
                    this.showAchievement('comboMaster');
                }
                
                if (this.powerUpUsageCount >= 50 && !achievementConfig.powerUpLover.unlocked) {
                    achievementConfig.powerUpLover.unlocked = true;
                    this.showAchievement('powerUpLover');
                }
                
                if (this.score > 50000 && !achievementConfig.perfectScore.unlocked) {
                    achievementConfig.perfectScore.unlocked = true;
                    this.showAchievement('perfectScore');
                }
            }
        }

        // 全局函数
        function showMainMenu() {
            hideAllScreens();
            document.getElementById('mainMenu').classList.add('active');
        }

        function showLevelSelect() {
            hideAllScreens();
            document.getElementById('levelSelect').classList.add('active');
            generateLevelGrid();
        }

        function showPractice() {
            hideAllScreens();
            document.getElementById('practice').classList.add('active');
            gameMode = 'practice';
            game = new SuperAppleMatchGame();
            game.currentGridId = 'practiceGrid';
            game.lives = 9999;
            game.target = 999999;
            game.init();
        }

        function showInstructions() {
            hideAllScreens();
            document.getElementById('instructionsModal').classList.add('active');
        }

        function showAchievements() {
            hideAllScreens();
            document.getElementById('achievements').classList.add('active');
            generateAchievementList();
        }

        function hideAllScreens() {
            const screens = document.querySelectorAll('.screen');
            screens.forEach(screen => screen.classList.remove('active'));
        }

        function generateLevelGrid() {
            const container = document.getElementById('levelGrid');
            if (!container) return;
            
            container.innerHTML = '';
            
            for (let level = 1; level <= 15; level++) {
                const config = levelConfig[level];
                const isUnlocked = level === 1 || localStorage.getItem(`level_${level}_unlocked`) === 'true';
                const isCompleted = localStorage.getItem(`level_${level}_completed`) === 'true';
                
                const levelCard = document.createElement('div');
                levelCard.className = `level-card ${isUnlocked ? 'unlocked' : 'locked'}`;
                
                if (isCompleted) {
                    levelCard.classList.add('completed');
                }
                
                const difficultyStars = '⭐'.repeat(config.difficulty);
                const difficultyText = ['', '新手', '简单', '普通', '困难', '专家', '传说'][config.difficulty];
                
                levelCard.innerHTML = `
                    <div class="level-number">${level}</div>
                    <div class="level-name">${config.name}</div>
                    <div class="level-difficulty">${difficultyStars}</div>
                    <div class="level-difficulty-text">${difficultyText}</div>
                    <div class="level-target">目标: ${config.target.toLocaleString()}</div>
                    <div class="level-moves">步数: ${config.moves}</div>
                    ${isCompleted ? '<div class="level-completed">✅ 已完成</div>' : ''}
                    ${!isUnlocked ? '<div class="level-locked">🔒 未解锁</div>' : ''}
                `;
                
                if (isUnlocked) {
                    levelCard.addEventListener('click', () => selectLevel(level));
                    levelCard.addEventListener('touchstart', () => selectLevel(level), { passive: true });
                }
                
                container.appendChild(levelCard);
            }
        }

        function selectLevel(level) {
            currentLevel = level;
            const config = levelConfig[level];
            
            document.getElementById('levelTitle').textContent = `关卡 ${level} - ${config.name}`;
            document.getElementById('levelDescription').innerHTML = `
                <p>${config.description}</p>
                <div style="margin-top: 15px; font-size: 14px; color: #666;">
                    <div>🎯 目标得分: ${config.target.toLocaleString()}</div>
                    <div>👆 可用步数: ${config.moves}</div>
                    <div>⭐ 难度等级: ${'⭐'.repeat(config.difficulty)}</div>
                </div>
            `;
            
            hideAllScreens();
            document.getElementById('levelConfirm').classList.add('active');
        }

        function startGame() {
            hideAllScreens();
            document.getElementById('gameScreen').classList.add('active');
            
            gameMode = 'normal';
            game = new SuperAppleMatchGame();
            game.currentGridId = 'gameGrid';
            game.target = levelConfig[currentLevel].target;
            game.lives = levelConfig[currentLevel].moves;
            game.gameStartTime = Date.now();
            
            // 根据关卡调整道具数量
            const levelMultiplier = Math.floor((currentLevel - 1) / 3) + 1;
            Object.keys(game.powerUps).forEach(powerUp => {
                game.powerUps[powerUp] *= levelMultiplier;
            });
            
            game.init();
        }

        function resetPractice() {
            if (game && gameMode === 'practice') {
                game = new SuperAppleMatchGame();
                game.currentGridId = 'practiceGrid';
                game.lives = 9999;
                game.target = 999999;
                game.init();
            }
        }

        function pauseGame() {
            if (game) {
                game.isPaused = !game.isPaused;
                const pauseBtn = document.querySelector('.control-btn');
                if (pauseBtn) {
                    pauseBtn.textContent = game.isPaused ? '▶️ 继续' : '⏸️ 暂停';
                }
                
                if (game.isPaused) {
                    const overlay = document.createElement('div');
                    overlay.id = 'pauseOverlay';
                    overlay.innerHTML = `
                        <div style="
                            position: fixed;
                            top: 50%;
                            left: 50%;
                            transform: translate(-50%, -50%);
                            background: rgba(0,0,0,0.8);
                            color: white;
                            padding: 30px;
                            border-radius: 20px;
                            text-align: center;
                            z-index: 10000;
                            font-size: 24px;
                        ">
                            ⏸️ 游戏已暂停<br>
                            <small style="font-size: 16px; opacity: 0.8;">点击继续按钮恢复游戏</small>
                        </div>
                    `;
                    document.body.appendChild(overlay);
                } else {
                    const overlay = document.getElementById('pauseOverlay');
                    if (overlay) {
                        overlay.remove();
                    }
                }
            }
        }

        function generateAchievementList() {
            const container = document.getElementById('achievementList');
            if (!container) return;
            
            container.innerHTML = '<h3 style="margin-top: 0;">🏆 成就列表</h3>';
            
            Object.entries(achievementConfig).forEach(([key, achievement]) => {
                const achievementDiv = document.createElement('div');
                achievementDiv.className = `achievement ${achievement.unlocked ? 'unlocked' : 'locked'}`;
                achievementDiv.innerHTML = `
                    <div class="achievement-icon">${achievement.icon}</div>
                    <div class="achievement-info">
                        <div class="achievement-name">${achievement.name}</div>
                        <div class="achievement-desc">${achievement.desc}</div>
                        <div class="achievement-status">
                            ${achievement.unlocked ? '✅ 已解锁' : '🔒 未解锁'}
                        </div>
                    </div>
                `;
                container.appendChild(achievementDiv);
            });
        }

        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', function() {
            // 加载保存的成就数据
            const savedAchievements = localStorage.getItem('achievements');
            if (savedAchievements) {
                try {
                    const parsed = JSON.parse(savedAchievements);
                    Object.assign(achievementConfig, parsed);
                } catch (e) {
                    console.log('加载成就数据失败');
                }
            }
            
            // 显示主菜单
            showMainMenu();
            
            // 添加键盘支持
            document.addEventListener('keydown', function(e) {
                if (!game || game.isPaused || game.isAnimating) return;
                
                switch(e.key) {
                    case 'Escape':
                        pauseGame();
                        break;
                    case 'r':
                    case 'R':
                        if (gameMode === 'practice') {
                            resetPractice();
                        }
                        break;
                    case '1':
                    case '2':
                    case '3':
                    case '4':
                    case '5':
                    case '6':
                    case '7':
                    case '8':
                    case '9':
                        const powerUpIndex = parseInt(e.key) - 1;
                        const powerUpKeys = Object.keys(game.powerUps);
                        if (powerUpKeys[powerUpIndex]) {
                            game.selectPowerUp(powerUpKeys[powerUpIndex]);
                        }
                        break;
                }
            });
            
            // 防止页面滚动
            document.addEventListener('touchmove', function(e) {
                if (e.target.closest('.game-board')) {
                    e.preventDefault();
                }
            }, { passive: false });
            
            // 添加音效提示
            setTimeout(() => {
                const audioTip = document.createElement('div');
                audioTip.innerHTML = `
                    <div style="
                        position: fixed;
                        bottom: 20px;
                        right: 20px;
                        background: rgba(0,0,0,0.7);
                        color: white;
                        padding: 10px 15px;
                        border-radius: 10px;
                        font-size: 12px;
                        z-index: 1000;
                        animation: fadeInOut 4s ease-in-out forwards;
                    ">
                        🔊 点击任意位置启用音效
                    </div>
                `;
                document.body.appendChild(audioTip);
                
                const enableAudio = () => {
                    try {
                        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                        audioContext.resume();
                        audioTip.remove();
                        document.removeEventListener('click', enableAudio);
                        document.removeEventListener('touchstart', enableAudio);
                    } catch (e) {
                        console.log('音频初始化失败');
                    }
                };
                
                document.addEventListener('click', enableAudio);
                document.addEventListener('touchstart', enableAudio);
                
                setTimeout(() => {
                    if (audioTip.parentNode) {
                        audioTip.remove();
                    }
                }, 4000);
            }, 2000);
        });

        // 添加特殊日期彩蛋
        function checkSpecialDates() {
            const now = new Date();
            const month = now.getMonth() + 1;
            const day = now.getDate();
            
            // 情人节彩蛋
            if (month === 2 && day === 14) {
                document.body.style.background = 'linear-gradient(45deg, #ff69b4, #ff1493)';
                setTimeout(() => {
                    alert("💕 情人节快乐，我的Ashley！今天所有道具翻倍！");
                    if (game) {
                        Object.keys(game.powerUps).forEach(key => {
                            game.powerUps[key] *= 2;
                        });
                        game.updatePowerUpDisplay();
                    }
                }, 3000);
            }
            
            // 生日彩蛋（可以设置Ashley的生日）
            if (month === 8 && day === 15) { // 假设8月15日是生日
                document.body.style.background = 'linear-gradient(45deg, #ffd700, #ff69b4)';
                setTimeout(() => {
                    alert("🎂 生日快乐Ashley！专属传说水果概率大增！");
                    if (game) {
                        game.legendaryFruitChance = 0.1;
                        game.specialFruitChance = 0.3;
                    }
                }, 3000);
            }
        }

        // 页面可见性变化处理
        document.addEventListener('visibilitychange', function() {
            if (document.hidden && game && !game.isPaused) {
                pauseGame(); // 页面隐藏时自动暂停
            }
        });

        // 移动端优化
        function optimizeForMobile() {
            const isMobile = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);
            if (isMobile) {
                document.body.classList.add('mobile');
                
                // 禁用长按菜单
                document.addEventListener('contextmenu', e => e.preventDefault());
                
                // 优化触摸响应
                let touchStartTime = 0;
                document.addEventListener('touchstart', () => {
                    touchStartTime = Date.now();
                });
                
                document.addEventListener('touchend', (e) => {
                    const touchDuration = Date.now() - touchStartTime;
                    if (touchDuration > 500) { // 长按
                        e.preventDefault();
                        return false;
                    }
                });
            }
        }

        // 检查特殊日期
        checkSpecialDates();
        
        // 移动端优化
        optimizeForMobile();

        // 全局错误处理
        window.addEventListener('error', function(e) {
            console.log('游戏运行出现错误，但不影响游戏体验');
        });

    </script>
</body>
</html>


