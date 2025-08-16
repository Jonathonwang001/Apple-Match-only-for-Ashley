# Apple-Match-only-for-Ashley
Creating an interesting game only for my love, Ashley. Hope her happy everyday!
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>💖 Ashley专属水果匹配游戏 💖</title>
    <meta name="description" content="为我最爱的Ashley定制的生日专属游戏 - 3月25日生日快乐！">
    <style>
        /* 基础重置 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: 'PingFang SC', 'Helvetica Neue', Arial, sans-serif;
            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 50%, #ffd1ff 100%);
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
            color: #fff;
            user-select: none;
        }

        /* Ashley专属背景动画 */
        .love-background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .heart {
            position: absolute;
            font-size: 24px;
            animation: floatHeart 8s infinite linear;
            opacity: 0.6;
        }

        .heart:nth-child(1) { left: 5%; animation-delay: 0s; }
        .heart:nth-child(2) { left: 15%; animation-delay: 1s; }
        .heart:nth-child(3) { left: 30%; animation-delay: 2s; }
        .heart:nth-child(4) { left: 50%; animation-delay: 3s; }
        .heart:nth-child(5) { left: 70%; animation-delay: 4s; }
        .heart:nth-child(6) { left: 85%; animation-delay: 5s; }

        @keyframes floatHeart {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% { opacity: 0.6; }
            90% { opacity: 0.6; }
            100% {
                transform: translateY(-20vh) rotate(360deg);
                opacity: 0;
            }
        }

        /* 主容器 */
        #gameContainer {
            width: 100%;
            max-width: 100vw;
            margin: 0;
            position: relative;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* 屏幕管理 */
        .screen {
            display: none;
            width: 100%;
            min-height: 100vh;
            padding: 10px;
            text-align: center;
            color: #fff;
            animation: fadeIn 0.5s ease-in-out;
            overflow-y: auto;
        }

        .screen.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Ashley专属主菜单 */
        .ashley-header h1 {
            font-size: clamp(1.8rem, 6vw, 3rem);
            font-weight: 900;
            background: linear-gradient(45deg, #ff6b9d, #c44569, #f8b500, #ff6b9d);
            background-size: 400% 400%;
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: ashleyGradient 3s ease-in-out infinite;
            margin: 20px 0;
            text-shadow: 2px 2px 10px rgba(255, 107, 157, 0.5);
        }

        @keyframes ashleyGradient {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .love-subtitle {
            font-size: clamp(0.9rem, 3vw, 1.2rem);
            color: #ffe4e1;
            margin-bottom: 20px;
            font-weight: 600;
            line-height: 1.5;
            padding: 0 10px;
        }

        .romantic-message {
            background: rgba(255, 182, 193, 0.2);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 15px;
            margin: 20px auto;
            max-width: 90%;
            border: 1px solid rgba(255, 182, 193, 0.3);
            animation: gentlePulse 3s ease-in-out infinite;
        }

        @keyframes gentlePulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }

        .romantic-message p {
            margin: 8px 0;
            font-size: clamp(0.9rem, 2.5vw, 1.1rem);
        }

        /* 生日特殊效果检测 */
        .birthday-special {
            background: linear-gradient(135deg, #ff6b9d, #ffd700, #ff6b9d);
            background-size: 200% 200%;
            animation: birthdayGlow 2s ease-in-out infinite;
            padding: 20px;
            border-radius: 20px;
            margin: 20px auto;
            max-width: 90%;
            border: 2px solid #ffd700;
            box-shadow: 0 0 30px rgba(255, 215, 0, 0.5);
        }

        @keyframes birthdayGlow {
            0%, 100% { 
                background-position: 0% 50%; 
                box-shadow: 0 0 30px rgba(255, 215, 0, 0.5);
            }
            50% { 
                background-position: 100% 50%; 
                box-shadow: 0 0 50px rgba(255, 215, 0, 0.8);
            }
        }

        .birthday-message {
            font-size: clamp(1.1rem, 3vw, 1.5rem);
            font-weight: 700;
            color: #fff;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            animation: birthdayTextGlow 2s ease-in-out infinite;
        }

        @keyframes birthdayTextGlow {
            0%, 100% { text-shadow: 2px 2px 4px rgba(0,0,0,0.5), 0 0 20px rgba(255,215,0,0.5); }
            50% { text-shadow: 2px 2px 4px rgba(0,0,0,0.7), 0 0 30px rgba(255,215,0,0.8); }
        }

        /* 按钮样式 */
        .ashley-btn {
            background: linear-gradient(45deg, #ff6b9d, #c44569);
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: clamp(1rem, 3vw, 1.2rem);
            font-weight: 700;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 6px 20px rgba(255, 107, 157, 0.4);
            margin: 8px;
            min-width: 200px;
            width: 90%;
            max-width: 300px;
        }

        .ashley-btn:hover, .ashley-btn:active {
            transform: translateY(-3px) scale(1.02);
            box-shadow: 0 10px 25px rgba(255, 107, 157, 0.6);
        }

        .high-score {
            margin: 20px 0;
            font-size: clamp(1rem, 3vw, 1.2rem);
            color: #ffd700;
            font-weight: 600;
        }

        /* 难度选择 */
        .difficulty-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            padding: 20px 10px;
            max-width: 800px;
            margin: 0 auto;
        }

        .difficulty-card {
            background: rgba(255, 182, 193, 0.2);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255, 182, 193, 0.3);
            border-radius: 15px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            color: white;
        }

        .difficulty-card:hover, .difficulty-card:active {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(255, 182, 193, 0.4);
        }

        .difficulty-icon {
            font-size: 40px;
            margin-bottom: 10px;
        }

        .difficulty-name {
            font-size: 1.3rem;
            font-weight: 700;
            margin-bottom: 8px;
        }

        .difficulty-desc {
            font-size: 1rem;
            margin-bottom: 10px;
            opacity: 0.9;
        }

        .difficulty-stats {
            display: flex;
            justify-content: space-around;
            font-size: 0.85rem;
        }

        /* 游戏界面布局 */
        .game-layout {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 10px;
            width: 100%;
            max-width: 100vw;
        }

        /* 手机端状态栏 */
        .mobile-status-bar {
            width: 100%;
            background: rgba(255, 182, 193, 0.3);
            backdrop-filter: blur(10px);
            padding: 12px;
            border-radius: 15px;
            margin-bottom: 10px;
        }

        .ashley-game-title {
            font-size: clamp(1rem, 4vw, 1.3rem);
            font-weight: 700;
            text-align: center;
            margin-bottom: 8px;
            background: linear-gradient(45deg, #ff6b9d, #c44569);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .mobile-stats {
            display: flex;
            justify-content: space-around;
            font-size: clamp(0.8rem, 3vw, 1rem);
            font-weight: 600;
        }

        .mobile-stats span {
            background: rgba(255, 255, 255, 0.2);
            padding: 6px 10px;
            border-radius: 15px;
            backdrop-filter: blur(5px);
        }

        /* 游戏网格 */
        .game-area {
            width: 100%;
            display: flex;
            justify-content: center;
            margin: 10px 0;
        }

        .grid-container {
            background: rgba(255, 182, 193, 0.2);
            backdrop-filter: blur(15px);
            border-radius: 20px;
            padding: 15px;
            border: 2px solid rgba(255, 182, 193, 0.4);
            box-shadow: 0 8px 25px rgba(255, 182, 193, 0.3);
        }

        .game-grid {
            display: grid;
            gap: 4px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 10px;
        }

        /* 响应式网格大小 */
        .game-grid.size-6 {
            grid-template-columns: repeat(6, 1fr);
            width: min(90vw, 360px);
            height: min(90vw, 360px);
        }

        .game-grid.size-7 {
            grid-template-columns: repeat(7, 1fr);
            width: min(90vw, 350px);
            height: min(90vw, 350px);
        }

        .game-grid.size-8 {
            grid-template-columns: repeat(8, 1fr);
            width: min(90vw, 320px);
            height: min(90vw, 320px);
        }

        .game-grid.size-9 {
            grid-template-columns: repeat(9, 1fr);
            width: min(90vw, 300px);
            height: min(90vw, 300px);
        }

        /* 游戏格子 */
        .cell {
            aspect-ratio: 1;
            background: linear-gradient(135deg, #ffe4e1, #ffc0cb);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s ease;
            border: 1px solid rgba(255, 182, 193, 0.3);
            box-shadow: 0 2px 8px rgba(255, 182, 193, 0.2);
            position: relative;
            overflow: hidden;
        }

        .cell:active {
            transform: scale(0.95);
        }

        .cell.selected {
            background: linear-gradient(135deg, #ff6b9d, #c44569);
            transform: scale(1.1);
            box-shadow: 0 0 20px rgba(255, 107, 157, 0.6);
            animation: selectedPulse 1.5s ease-in-out infinite;
        }

        @keyframes selectedPulse {
            0%, 100% { box-shadow: 0 0 20px rgba(255, 107, 157, 0.6); }
            50% { box-shadow: 0 0 30px rgba(255, 107, 157, 0.9); }
        }

        .cell.hint {
            animation: hintBlink 1s ease-in-out 3;
        }

        @keyframes hintBlink {
            0%, 100% { background: linear-gradient(135deg, #ffe4e1, #ffc0cb); }
            50% { background: linear-gradient(135deg, #00ff88, #00cc66); }
        }

        /* 水果样式 */
        .fruit {
            font-size: clamp(18px, 5vw, 28px);
            filter: drop-shadow(1px 1px 3px rgba(255, 182, 193, 0.5));
            animation: fruitPop 0.3s ease-out;
        }

        @keyframes fruitPop {
            0% { transform: scale(0) rotate(180deg); opacity: 0; }
            100% { transform: scale(1) rotate(0deg); opacity: 1; }
        }

        /* 特殊水果效果 */
        .special-1 { animation: specialGlow1 2s ease-in-out infinite; }
        .special-2 { animation: specialGlow2 2s ease-in-out infinite; }
        .special-3 { animation: specialGlow3 2s ease-in-out infinite; }
        .special-4 { animation: specialGlow4 2s ease-in-out infinite; }

        @keyframes specialGlow1 {
            0%, 100% { filter: drop-shadow(0 0 5px #ffd700); }
            50% { filter: drop-shadow(0 0 15px #ffd700); }
        }

        @keyframes specialGlow2 {
            0%, 100% { filter: drop-shadow(0 0 5px #ff6b6b); }
            50% { filter: drop-shadow(0 0 15px #ff6b6b); }
        }

        @keyframes specialGlow3 {
            0%, 100% { filter: drop-shadow(0 0 5px #4ecdc4); }
            50% { filter: drop-shadow(0 0 15px #4ecdc4); }
        }

        @keyframes specialGlow4 {
            0%, 100% { filter: drop-shadow(0 0 8px #ff00ff); }
            50% { filter: drop-shadow(0 0 20px #ff00ff); }
        }

        /* 手机端道具栏 */
        .mobile-powers-container {
            width: 100%;
            background: rgba(255, 182, 193, 0.3);
            backdrop-filter: blur(10px);
            padding: 10px;
            border-radius: 15px;
            margin: 10px 0;
        }

        .mobile-power-ups {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 6px;
        }

        .powerup-btn {
            background: linear-gradient(135deg, rgba(255, 107, 157, 0.8), rgba(196, 69, 105, 0.8));
            border: 1px solid rgba(255, 182, 193, 0.4);
            border-radius: 10px;
            padding: 8px 4px;
            cursor: pointer;
            transition: all 0.2s ease;
            color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 60px;
            position: relative;
            backdrop-filter: blur(5px);
        }

        .powerup-btn:active {
            transform: scale(0.95);
        }

        .powerup-btn.active {
            background: linear-gradient(135deg, #ff6b9d, #c44569);
            box-shadow: 0 0 15px rgba(255, 107, 157, 0.6);
            animation: activePowerup 2s ease-in-out infinite;
        }

        @keyframes activePowerup {
            0%, 100% { box-shadow: 0 0 15px rgba(255, 107, 157, 0.6); }
            50% { box-shadow: 0 0 25px rgba(255, 107, 157, 0.9); }
        }

        .powerup-btn.disabled {
            background: rgba(100, 100, 100, 0.5);
            opacity: 0.4;
        }

        .powerup-icon {
            font-size: clamp(16px, 4vw, 24px);
            margin-bottom: 2px;
        }

        .powerup-name {
            font-size: clamp(8px, 2vw, 10px);
            font-weight: 600;
            text-align: center;
        }

        .powerup-count {
            position: absolute;
            top: -5px;
            right: -5px;
            background: linear-gradient(45deg, #ff6b9d, #c44569);
            color: white;
            border-radius: 50%;
            width: 18px;
            height: 18px;
            font-size: 10px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid #fff;
        }

        /* 控制按钮 */
        .game-controls {
            display: flex;
            justify-content: center;
            gap: 8px;
            margin: 15px 0;
            flex-wrap: wrap;
        }

        .control-btn {
            background: linear-gradient(45deg, rgba(255, 107, 157, 0.9), rgba(196, 69, 105, 0.9));
            color: white;
            border: 1px solid rgba(255, 182, 193, 0.5);
            padding: 10px 15px;
            font-size: clamp(0.8rem, 2.5vw, 1rem);
            font-weight: 600;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.2s ease;
            backdrop-filter: blur(5px);
            min-width: 70px;
        }

        .control-btn:active {
            transform: scale(0.95);
        }

        .control-btn:disabled {
            background: rgba(100, 100, 100, 0.5);
            opacity: 0.5;
        }

        /* 返回按钮 */
        .back-btn {
            background: linear-gradient(45deg, #ff6b9d, #c44569);
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: clamp(0.9rem, 3vw, 1.1rem);
            font-weight: 600;
            border-radius: 25px;
            cursor: pointer;
            margin: 20px;
            transition: all 0.2s ease;
        }

        .back-btn:active {
            transform: scale(0.95);
        }

        /* 成就系统 */
        .achievements-container {
            padding: 20px 10px;
            max-width: 600px;
            margin: 0 auto;
        }

        .achievement-item {
            display: flex;
            align-items: center;
            gap: 15px;
            padding: 15px;
            margin: 10px 0;
            border-radius: 12px;
            background: rgba(255, 182, 193, 0.2);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 182, 193, 0.3);
        }

        .achievement-item.achieved {
            background: rgba(76, 175, 80, 0.3);
            border-color: rgba(76, 175, 80, 0.5);
        }

        .achievement-item.locked {
            opacity: 0.5;
        }

        .achievement-icon {
            font-size: 2rem;
            min-width: 50px;
            text-align: center;
        }

        .achievement-info {
            flex: 1;
            text-align: left;
        }

        .achievement-name {
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 4px;
        }

        .achievement-desc {
            font-size: 0.9rem;
            opacity: 0.8;
        }

        .achievement-status {
            font-size: 1.5rem;
        }

        /* 情书界面 */
        .love-letter-container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background: rgba(255, 182, 193, 0.2);
            backdrop-filter: blur(15px);
            border-radius: 20px;
            border: 2px solid rgba(255, 182, 193, 0.3);
        }

        .letter-header h2 {
            font-size: clamp(1.5rem, 5vw, 2.5rem);
            background: linear-gradient(45deg, #ff6b9d, #c44569);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
        }

        .letter-content {
            text-align: left;
            line-height: 1.6;
            font-size: clamp(0.9rem, 3vw, 1.1rem);
        }

        .letter-content p {
            margin: 15px 0;
        }

        .love-list {
            list-style: none;
            padding: 0;
            margin: 20px 0;
        }

        .love-list li {
            margin: 10px 0;
            padding-left: 10px;
        }

        .letter-signature {
            text-align: center;
            font-style: italic;
            font-weight: bold;
            margin: 30px 0 20px 0;
            font-size: clamp(1rem, 3vw, 1.2rem);
        }

        .letter-interactive {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin: 20px 0;
        }

        .love-btn {
            background: linear-gradient(45deg, #ff6b9d, #c44569);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 25px;
            font-size: clamp(0.9rem, 3vw, 1rem);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .love-btn:active {
            transform: scale(0.95);
        }

        /* 游戏结束界面 */
        .game-over-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(10px);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 10000;
            padding: 20px;
        }

        .game-over-content {
            background: linear-gradient(135deg, #ff6b9d, #c44569);
            color: white;
            padding: 30px 20px;
            border-radius: 20px;
            text-align: center;
            max-width: 400px;
            width: 100%;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
        }

        .game-over-content h2 {
            font-size: clamp(1.8rem, 5vw, 2.5rem);
            margin-bottom: 20px;
        }

        .final-stats {
            margin: 20px 0;
            text-align: left;
        }

        .stat-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid rgba(255,255,255,0.2);
            font-size: clamp(0.9rem, 3vw, 1rem);
        }

        .stat-value {
            color: #ffd700;
            font-weight: bold;
        }

        .new-record {
            background: rgba(255, 215, 0, 0.3);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            font-weight: bold;
            animation: celebration 2s ease-in-out infinite;
        }

        @keyframes celebration {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .game-over-buttons {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
        }

        .restart-btn, .home-btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 25px;
            font-size: clamp(0.9rem, 3vw, 1rem);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .restart-btn {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
            color: white;
        }

        .home-btn {
            background: linear-gradient(45deg, #ff6b6b, #ee5a6f);
            color: white;
        }

        .restart-btn:active, .home-btn:active {
            transform: scale(0.95);
        }

        /* 成就通知 */
        .achievement-notification {
            position: fixed;
            top: 20px;
            right: 20px;
            left: 20px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(31, 38, 135, 0.37);
            z-index: 10000;
            transform: translateY(-200px);
            transition: transform 0.5s ease;
            text-align: center;
        }

        .achievement-notification.show {
            transform: translateY(0);
        }

        .achievement-title {
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 8px;
            color: #ffd700;
        }

        /* 粒子效果 */
        .particle {
            position: absolute;
            pointer-events: none;
            font-size: 20px;
            opacity: 0.8;
            animation: particleFloat 2s ease-out forwards;
        }

        @keyframes particleFloat {
            0% {
                transform: translateY(0) scale(1);
                opacity: 1;
            }
            100% {
                transform: translateY(-60px) scale(0);
                opacity: 0;
            }
        }

        /* 消息提示 */
        .temporary-message {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0, 0, 0, 0.8);
            color: white;
            padding: 15px 25px;
            border-radius: 25px;
            font-size: clamp(1rem, 3vw, 1.2rem);
            font-weight: 600;
            z-index: 10000;
            backdrop-filter: blur(10px);
            animation: messageShow 2s ease-out forwards;
        }

        @keyframes messageShow {
            0% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
            25% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
        75% { opacity: 1; transform: translate(-50%, -50%) scale(1); }
        100% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
    }

    /* 加载界面 */
    .loading-content {
        text-align: center;
        padding: 50px 20px;
    }

    .loading-heart {
        font-size: 60px;
        animation: loadingPulse 1.5s ease-in-out infinite;
        margin-bottom: 20px;
    }

    @keyframes loadingPulse {
        0%, 100% { transform: scale(1); }
        50% { transform: scale(1.2); }
    }

    .loading-text {
        font-size: clamp(1rem, 3vw, 1.2rem);
        margin-bottom: 20px;
        color: #ffe4e1;
    }

    .loading-bar {
        width: 80%;
        height: 8px;
        background: rgba(255, 255, 255, 0.2);
        border-radius: 4px;
        margin: 0 auto;
        overflow: hidden;
    }

    .loading-progress {
        height: 100%;
        background: linear-gradient(45deg, #ff6b9d, #c44569);
        border-radius: 4px;
        animation: loadingProgress 3s ease-in-out infinite;
    }

    @keyframes loadingProgress {
        0% { width: 0%; }
        50% { width: 70%; }
        100% { width: 100%; }
    }

    /* 练习模式特殊样式 */
    #practice .mobile-stats span:nth-child(2) {
        background: linear-gradient(45deg, #4ecdc4, #44a08d);
    }

    /* 桌面端适配 */
    @media (min-width: 768px) {
        #gameContainer {
            max-width: 1200px;
            margin: 20px auto;
            border-radius: 25px;
            border: 2px solid rgba(255, 182, 193, 0.3);
            box-shadow: 0 20px 60px rgba(255, 182, 193, 0.4);
        }

        .game-layout {
            flex-direction: row;
            justify-content: space-between;
            align-items: flex-start;
            gap: 20px;
        }

        .left-panel, .right-panel {
            width: 250px;
            flex-shrink: 0;
        }

        .desktop-only {
            display: block !important;
        }

        .mobile-only {
            display: none !important;
        }

        .ashley-btn {
            width: auto;
            min-width: 250px;
        }

        .difficulty-grid {
            grid-template-columns: repeat(2, 1fr);
        }

        .mobile-status-bar,
        .mobile-powers-container {
            display: none;
        }

        .game-grid.size-6 { width: 360px; height: 360px; }
        .game-grid.size-7 { width: 420px; height: 420px; }
        .game-grid.size-8 { width: 480px; height: 480px; }
        .game-grid.size-9 { width: 540px; height: 540px; }

        .cell {
            border-radius: 12px;
        }

        .fruit {
            font-size: 32px;
        }

        .powerup-btn {
            min-height: 80px;
            padding: 10px;
        }

        .powerup-icon {
            font-size: 28px;
        }

        .powerup-name {
            font-size: 11px;
        }
    }

    /* 隐藏类 */
    .desktop-only {
        display: none;
    }

    .mobile-only {
        display: block;
    }
    </style>
</head>
<body>
    <div id="gameContainer">
        <!-- 爱心飘落背景 -->
        <div class="love-background">
            <div class="heart">💖</div>
            <div class="heart">💕</div>
            <div class="heart">💝</div>
            <div class="heart">💗</div>
            <div class="heart">💓</div>
            <div class="heart">🌹</div>
        </div>
        
        <!-- 主菜单 -->
        <div id="menu" class="screen active">
            <div class="ashley-header">
                <h1>💖 Ashley专属水果匹配 💖</h1>
                <div class="love-subtitle">
                    🌹 为我最爱的Ashley定制的专属游戏 🌹<br>
                    💕 生日快乐，我的宝贝！ 💕
                </div>
                
                <!-- 生日特殊效果检测 -->
                <div id="birthdaySpecial" class="birthday-special" style="display: none;">
                    <div class="birthday-message">
                        🎂✨ 今天是Ashley的生日！3月25日！✨🎂<br>
                        🎉 生日快乐我的宝贝，愿你永远快乐！ 🎉
                    </div>
                </div>
                
                <div class="romantic-message">
                    <p>🎂 每一个水果都代表我对你的爱 🎂</p>
                    <p>✨ 希望每一天都像游戏一样甜蜜 ✨</p>
                </div>
            </div>
            
            <div class="menu-buttons">
                <button class="ashley-btn" onclick="showDifficultySelect()">
                    🎮 开始甜蜜冒险
                </button>
                <button class="ashley-btn" onclick="startPractice()">
                    🌟 练习模式
                </button>
                <button class="ashley-btn" onclick="showScreen('achievements')">
                    🏆 我们的成就
                </button>
                <button class="ashley-btn" onclick="showScreen('loveLetter')">
                    💌 写给Ashley的情书
                </button>
            </div>
            
            <div class="high-score">
                🎯 最高分数: <span id="highScoreDisplay">0</span>
            </div>
        </div>

        <!-- 难度选择 -->
        <div id="difficultySelect" class="screen">
            <h2>💕 选择甜蜜难度 💕</h2>
            <div class="love-subtitle">为Ashley选择最适合的挑战等级</div>
            
            <div class="difficulty-grid">
                <div class="difficulty-card" onclick="startGame('easy')">
                    <div class="difficulty-icon">🌸</div>
                    <div class="difficulty-name">温柔模式</div>
                    <div class="difficulty-desc">6x6网格，像你一样温柔</div>
                    <div class="difficulty-stats">
                        <span>💝 生命: 30</span>
                        <span>🍓 道具丰富</span>
                    </div>
                </div>
                
                <div class="difficulty-card" onclick="startGame('normal')">
                    <div class="difficulty-icon">💖</div>
                    <div class="difficulty-name">甜蜜模式</div>
                    <div class="difficulty-desc">7x7网格，甜蜜的挑战</div>
                    <div class="difficulty-stats">
                        <span>💝 生命: 25</span>
                        <span>🍓 均衡体验</span>
                    </div>
                </div>
                
                <div class="difficulty-card" onclick="startGame('hard')">
                    <div class="difficulty-icon">🔥</div>
                    <div class="difficulty-name">激情模式</div>
                    <div class="difficulty-desc">8x8网格，激情四射</div>
                    <div class="difficulty-stats">
                        <span>💝 生命: 20</span>
                        <span>🍓 更多挑战</span>
                    </div>
                </div>
                
                <div class="difficulty-card" onclick="startGame('expert')">
                    <div class="difficulty-icon">👑</div>
                    <div class="difficulty-name">女王模式</div>
                    <div class="difficulty-desc">9x9网格，Ashley女王专属</div>
                    <div class="difficulty-stats">
                        <span>💝 生命: 15</span>
                        <span>🍓 极限挑战</span>
                    </div>
                </div>
            </div>
            
            <button class="back-btn" onclick="showScreen('menu')">
                💕 返回主菜单
            </button>
        </div>

        <!-- 主游戏界面 -->
        <div id="game" class="screen">
            <!-- 手机端状态栏 -->
            <div class="mobile-status-bar mobile-only">
                <div class="ashley-game-title">💖 Ashley的甜蜜时光 💖</div>
                <div class="mobile-stats">
                    <span id="mobileScore">💎 0</span>
                    <span id="mobileLives">💝 30</span>
                    <span id="mobileCombo">⭐ 0</span>
                </div>
            </div>
            
            <div class="game-layout">
                <!-- 左侧面板 - 桌面端 -->
                <div class="left-panel desktop-only">
                    <div class="ashley-love-panel">
                        <h3>💕 Ashley专区 💕</h3>
                        <div class="love-stats">
                            <div class="love-stat">
                                <span class="stat-icon">💎</span>
                                <span class="stat-label">甜蜜分数</span>
                                <span id="score" class="stat-value">0</span>
                            </div>
                            <div class="love-stat">
                                <span class="stat-icon">💝</span>
                                <span class="stat-label">爱心生命</span>
                                <span id="lives" class="stat-value">30</span>
                            </div>
                            <div class="love-stat">
                                <span class="stat-icon">⭐</span>
                                <span class="stat-label">连击之星</span>
                                <span id="combo" class="stat-value">0</span>
                            </div>
                            <div class="love-stat" id="multiplierStat" style="display:none;">
                                <span class="stat-icon">✨</span>
                                <span class="stat-label">魔法倍数</span>
                                <span id="multiplier" class="stat-value">1x</span>
                            </div>
                        </div>
                        
                        <div class="ashley-message-area">
                            <div id="ashleyMessage" class="ashley-message">
                                💕 加油呀宝贝，你是最棒的！
                            </div>
                        </div>
                        
                        <div class="special-date-reminder">
                            <div id="dateMessage" class="date-message"></div>
                        </div>
                    </div>
                </div>

                <!-- 游戏区域 -->
                <div class="game-area">
                    <div class="grid-container">
                        <div id="gameGrid" class="game-grid"></div>
                    </div>
                </div>

                <!-- 右侧面板 - 桌面端 -->
                <div class="right-panel desktop-only">
                    <div class="ashley-powers">
                        <h3>💖 Ashley的魔法道具 💖</h3>
                        <div id="desktopPowerUps" class="power-ups"></div>
                    </div>
                </div>
            </div>

            <!-- 手机端道具栏 -->
            <div class="mobile-powers-container mobile-only">
                <div id="mobilePowerUps" class="mobile-power-ups"></div>
            </div>

            <!-- 游戏控制 -->
            <div class="game-controls">
                <button id="pauseBtn" class="control-btn" onclick="pauseGame()">⏸️ 暂停</button>
                <button class="control-btn" onclick="getHint()">💡 提示</button>
                <button class="control-btn" onclick="showScreen('menu')">🏠 主菜单</button>
            </div>
        </div>

        <!-- 练习模式 -->
        <div id="practice" class="screen">
            <div class="ashley-header">
                <h2>🌟 Ashley的练习花园 🌟</h2>
                <div class="love-subtitle">在这里尽情练习，没有压力哦～</div>
            </div>
            
            <!-- 手机端状态栏 -->
            <div class="mobile-status-bar mobile-only">
                <div class="ashley-game-title">🌟 练习模式 🌟</div>
                <div class="mobile-stats">
                    <span id="mobilePracticeScore">💎 0</span>
                    <span id="mobilePracticeLives">💝 ∞</span>
                    <span id="mobilePracticeCombo">⭐ 0</span>
                </div>
            </div>
            
            <div class="game-layout">
                <div class="left-panel desktop-only">
                    <div class="ashley-love-panel">
                        <h3>💕 练习统计 💕</h3>
                        <div class="love-stats">
                            <div class="love-stat">
                                <span class="stat-icon">💎</span>
                                <span class="stat-label">练习分数</span>
                                <span id="practiceScore" class="stat-value">0</span>
                            </div>
                            <div class="love-stat">
                                <span class="stat-icon">💝</span>
                                <span class="stat-label">无限生命</span>
                                <span class="stat-value">∞</span>
                            </div>
                            <div class="love-stat">
                                <span class="stat-icon">⭐</span>
                                <span class="stat-label">连击记录</span>
                                <span id="practiceCombo" class="stat-value">0</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="game-area">
                    <div class="grid-container">
                        <div id="practiceGrid" class="game-grid size-7"></div>
                    </div>
                </div>

                <div class="right-panel desktop-only">
                    <div class="ashley-powers">
                        <h3>💖 无限道具 💖</h3>
                        <div id="practicePowerUps" class="power-ups"></div>
                    </div>
                </div>
            </div>

            <!-- 手机端道具栏 -->
            <div class="mobile-powers-container mobile-only">
                <div id="mobilePracticePowerUps" class="mobile-power-ups"></div>
            </div>

            <div class="game-controls">
                <button class="control-btn" onclick="getHint()">💡 提示</button>
                <button class="control-btn" onclick="resetPractice()">🔄 重置</button>
                <button class="control-btn" onclick="showScreen('menu')">🏠 主菜单</button>
            </div>
        </div>

        <!-- 成就界面 -->
        <div id="achievements" class="screen">
            <div class="ashley-header">
                <h2>🏆 我们的甜蜜成就 🏆</h2>
                <div class="love-subtitle">每一个成就都是我们爱情的见证</div>
            </div>
            
            <div class="achievements-container">
                <div id="achievementsList"></div>
            </div>
            
            <button class="back-btn" onclick="showScreen('menu')">💕 返回主菜单</button>
        </div>

        <!-- 情书界面 -->
        <div id="loveLetter" class="screen">
            <div class="love-letter-container">
                <div class="letter-header">
                    <h2>💌 写给Ashley的情书 💌</h2>
                    <div class="love-subtitle">今天是我们相爱的每一天</div>
                </div>
                
                <div class="letter-content">
                    <p>💕 我最亲爱的Ashley，</p>
                    <p>这个游戏是我为你精心制作的生日礼物。每一行代码都充满了我对你的爱，每一个动画都承载着我对你的思念。</p>
                    <p>🌹 在这个特殊的日子里，我想对你说：</p>
                    <div class="love-list">
                        <div>💖 你是我生命中最美好的存在</div>
                        <div>🎂 希望你的每个生日都充满快乐和惊喜</div>
                        <div>✨ 愿我们的爱情像游戏中的连击一样，永远持续</div>
                        <div>🌟 你的笑容是我最大的成就奖励</div>
                        <div>💝 永远爱你，我的宝贝Ashley</div>
                    </div>
                    <p class="letter-signature">💕 永远爱你的<br>你最爱的人 💕</p>
                    
                    <div class="letter-interactive">
                        <button class="love-btn" onclick="showLoveAnimation()">💖 给Ashley一个大大的拥抱</button>
                        <button class="love-btn" onclick="playBirthdaySong()">🎵 播放生日快乐歌</button>
                    </div>
                </div>
            </div>
            
            <button class="back-btn" onclick="showScreen('menu')">💕 返回主菜单</button>
        </div>

        <!-- 加载界面 -->
        <div id="loading" class="screen" style="display: none;">
            <div class="loading-content">
                <div class="loading-heart">💖</div>
                <div class="loading-text">正在为Ashley准备甜蜜惊喜...</div>
                <div class="loading-bar">
                    <div class="loading-progress"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // ===========================================
        // 💖 Ashley专属水果匹配游戏 JavaScript 💖
        // ===========================================
        
        // 游戏配置
        const gameConfig = {
            fruits: ['🍎', '🍊', '🍌', '🍇', '🍓', '🥝', '🍑', '🥭'],
            specialFruits: ['⭐', '💎', '🌟', '💖'],
            difficulties: {
                easy: { size: 6, lives: 30, powerUpChance: 0.15 },
                normal: { size: 7, lives: 25, powerUpChance: 0.12 },
                hard: { size: 8, lives: 20, powerUpChance: 0.10 },
                expert: { size: 9, lives: 15, powerUpChance: 0.08 }
            },
            powerUps: [
                { id: 'bomb', name: '爆弹', icon: '💣', cost: 1 },
                { id: 'lightning', name: '闪电', icon: '⚡', cost: 1 },
                { id: 'rainbow', name: '彩虹', icon: '🌈', cost: 2 },
                { id: 'star', name: '星星', icon: '⭐', cost: 2 },
                { id: 'heart', name: '爱心', icon: '💖', cost: 3 },
                { id: 'magic', name: '魔法', icon: '✨', cost: 3 }
            ]
        };

        // 游戏状态
        let gameState = {
            currentScreen: 'menu',
            gameMode: 'normal', // normal, practice
            difficulty: 'normal',
            score: 0,
            lives: 25,
            combo: 0,
            multiplier: 1,
            grid: [],
            selectedCells: [],
            powerUps: {},
            activePowerUp: null,
            isPaused: false,
            isGameOver: false,
            bestScore: 0,
            achievements: {},
            stats: {
                gamesPlayed: 0,
                totalScore: 0,
                maxCombo: 0,
                powerUpsUsed: 0
            }
        };

        // 成就系统
        const achievements = {
            firstGame: { 
                id: 'firstGame', 
                name: '初次相遇', 
                desc: '完成第一次游戏', 
                icon: '🎮',
                condition: () => gameState.stats.gamesPlayed >= 1
            },
            combo10: { 
                id: 'combo10', 
                name: '甜蜜连击', 
                desc: '达到10连击', 
                icon: '⭐',
                condition: () => gameState.stats.maxCombo >= 10
            },
            score1000: { 
                id: 'score1000', 
                name: '千分之爱', 
                desc: '单局得分达到1000', 
                icon: '💎',
                condition: () => gameState.bestScore >= 1000
            },
            birthday: { 
                id: 'birthday', 
                name: '生日快乐', 
                desc: '在Ashley生日当天游戏', 
                icon: '🎂',
                condition: () => isBirthday()
            },
            powerUser: { 
                id: 'powerUser', 
                name: '道具大师', 
                desc: '使用道具10次', 
                icon: '🔮',
                condition: () => gameState.stats.powerUpsUsed >= 10
            }
        };

        // Ashley专属消息
        const ashleyMessages = [
            '💕 加油呀宝贝，你是最棒的！',
            '🌟 哇塞，你好厉害呀！',
            '💖 我就知道你可以的！',
            '🎉 太棒了，继续加油！',
            '✨ 你真的很优秀呢！',
            '🌹 我的小天才！',
            '💝 爱你哦，继续努力！',
            '🎂 你让我好骄傲！'
        ];

        // 初始化游戏
        function init() {
            console.log('💖 初始化Ashley专属水果匹配游戏...');
            
            // 加载存档
            loadGame();
            
            // 检查生日特殊效果
            checkBirthdaySpecial();
            
            // 更新最高分显示
            updateHighScore();
            
            // 初始化成就系统
            initAchievements();
            
            // 设置日期消息
            updateDateMessage();
            
            console.log('💕 游戏初始化完成！为Ashley准备好了！');
        }

        // 检查是否为Ashley生日
        function isBirthday() {
            const today = new Date();
            return (today.getMonth() === 2 && today.getDate() === 25); // 3月25日
        }

        // 检查生日特殊效果
        function checkBirthdaySpecial() {
            if (isBirthday()) {
                document.getElementById('birthdaySpecial').style.display = 'block';
                // 生日特殊效果
                document.body.style.background = 'linear-gradient(135deg, #ffd700 0%, #ff6b9d 50%, #ffd700 100%)';
                // 添加更多爱心
                addBirthdayHearts();
            }
        }

        // 添加生日爱心效果
        function addBirthdayHearts() {
            const loveBackground = document.querySelector('.love-background');
            for (let i = 0; i < 5; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.className = 'heart';
                    heart.textContent = '🎂';
                    heart.style.left = Math.random() * 100 + '%';
                    heart.style.animationDelay = '0s';
                    heart.style.animationDuration = (Math.random() * 3 + 5) + 's';
                    loveBackground.appendChild(heart);
                }, i * 1000);
            }
        }

        // 更新日期消息
        function updateDateMessage() {
            const dateMsg = document.getElementById('dateMessage');
            const today = new Date();
            const month = today.getMonth() + 1;
            const date = today.getDate();
            
            if (isBirthday()) {
                dateMsg.textContent = '🎂 今天是Ashley的生日！生日快乐宝贝！ 🎂';
                dateMsg.style.animation = 'birthdayTextGlow 2s ease-in-out infinite';
            } else {
                const daysUntilBirthday = getDaysUntilBirthday();
                dateMsg.textContent = `💕 距离Ashley生日还有 ${daysUntilBirthday} 天 💕`;
            }
        }

        // 计算距离生日天数
        function getDaysUntilBirthday() {
            const today = new Date();
            const thisYear = today.getFullYear();
            let birthday = new Date(thisYear, 2, 25); // 3月25日
            
            if (birthday < today) {
                birthday = new Date(thisYear + 1, 2, 25);
            }
            
            const diffTime = birthday - today;
            return Math.ceil(diffTime / (1000 * 60 * 60 * 24));
        }

        // 显示屏幕
        function showScreen(screenName) {
            console.log(`💖 切换到屏幕: ${screenName}`);
            
            // 隐藏所有屏幕
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            
            // 显示目标屏幕
            const targetScreen = document.getElementById(screenName);
            if (targetScreen) {
                targetScreen.classList.add('active');
                gameState.currentScreen = screenName;
            }
            
            // 屏幕特殊处理
            if (screenName === 'achievements') {
                renderAchievements();
            }
        }

        // 显示难度选择
        function showDifficultySelect() {
            showScreen('difficultySelect');
        }

        // 开始游戏
        function startGame(difficulty = 'normal') {
            console.log(`💖 开始游戏，难度: ${difficulty}`);
            
            gameState.gameMode = 'normal';
            gameState.difficulty = difficulty;
            gameState.isGameOver = false;
            gameState.isPaused = false;
            
            const config = gameConfig.difficulties[difficulty];
            gameState.score = 0;
            gameState.lives = config.lives;
            gameState.combo = 0;
            gameState.multiplier = 1;
            gameState.selectedCells = [];
            gameState.activePowerUp = null;
            
            // 初始化道具
            initPowerUps();
            
            // 创建网格
            createGrid(config.size);
            
            // 显示游戏屏幕
            showScreen('game');
            
            // 更新UI
            updateUI();
            
            // 显示开始消息
            showAshleyMessage('💖 开始甜蜜冒险吧，Ashley！');
        }

        // 开始练习模式
        function startPractice() {
            console.log('🌟 开始练习模式');
            
            gameState.gameMode = 'practice';
            gameState.difficulty = 'normal';
            gameState.isGameOver = false;
            gameState.isPaused = false;
            
            gameState.score = 0;
            gameState.lives = Infinity;
            gameState.combo = 0;
            gameState.multiplier = 1;
            gameState.selectedCells = [];
            gameState.activePowerUp = null;
            
            // 练习模式有无限道具
            initPowerUps(true);
            
            // 创建7x7网格
            createGrid(7);
            
            // 显示练习屏幕
            showScreen('practice');
            
            // 更新UI
            updateUI();
            
            showAshleyMessage('🌟 在练习花园里尽情享受吧！');
        }

        // 重置练习
        function resetPractice() {
            startPractice();
            showTemporaryMessage('🌟 练习重置完成！');
        }

        // 初始化道具
        function initPowerUps(unlimited = false) {
            gameState.powerUps = {};
            gameConfig.powerUps.forEach(powerUp => {
                gameState.powerUps[powerUp.id] = unlimited ? 999 : Math.floor(Math.random() * 3) + 1;
            });
            updatePowerUpsUI();
        }

        // 创建游戏网格
        function createGrid(size) {
            console.log(`💕 创建 ${size}x${size} 网格`);
            
            gameState.grid = [];
            const gameGrid = document.getElementById(gameState.gameMode
            === 'practice' ? 'practiceGrid' : 'gameGrid');
            const practiceGrid = document.getElementById('practiceGrid');
            
            // 清空现有网格
            if (gameGrid) {
                gameGrid.innerHTML = '';
                gameGrid.className = `game-grid size-${size}`;
            }
            if (practiceGrid) {
                practiceGrid.innerHTML = '';
                practiceGrid.className = `game-grid size-${size}`;
            }
            
            const currentGrid = gameState.gameMode === 'practice' ? practiceGrid : gameGrid;
            
            // 创建网格数据和DOM
            for (let row = 0; row < size; row++) {
                gameState.grid[row] = [];
                for (let col = 0; col < size; col++) {
                    // 创建单元格数据
                    const cell = {
                        row: row,
                        col: col,
                        fruit: getRandomFruit(),
                        isSpecial: false,
                        element: null
                    };
                    
                    // 创建DOM元素
                    const cellElement = document.createElement('div');
                    cellElement.className = 'cell';
                    cellElement.dataset.row = row;
                    cellElement.dataset.col = col;
                    cellElement.addEventListener('click', () => handleCellClick(row, col));
                    cellElement.addEventListener('touchstart', (e) => {
                        e.preventDefault();
                        handleCellClick(row, col);
                    });
                    
                    const fruitElement = document.createElement('div');
                    fruitElement.className = 'fruit';
                    fruitElement.textContent = cell.fruit;
                    cellElement.appendChild(fruitElement);
                    
                    cell.element = cellElement;
                    gameState.grid[row][col] = cell;
                    currentGrid.appendChild(cellElement);
                }
            }
            
            // 确保有有效移动
            if (!hasValidMoves()) {
                shuffleGrid();
            }
        }

        // 获取随机水果
        function getRandomFruit() {
            const fruits = gameConfig.fruits;
            return fruits[Math.floor(Math.random() * fruits.length)];
        }

        // 处理单元格点击
        function handleCellClick(row, col) {
            if (gameState.isPaused || gameState.isGameOver) return;
            
            const cell = gameState.grid[row][col];
            if (!cell) return;
            
            // 如果使用道具模式
            if (gameState.activePowerUp) {
                usePowerUp(gameState.activePowerUp, row, col);
                return;
            }
            
            // 正常选择模式
            const cellIndex = gameState.selectedCells.findIndex(c => c.row === row && c.col === col);
            
            if (cellIndex !== -1) {
                // 取消选择
                gameState.selectedCells.splice(cellIndex, 1);
                cell.element.classList.remove('selected');
            } else {
                // 选择单元格
                if (gameState.selectedCells.length === 0) {
                    // 第一个选择
                    gameState.selectedCells.push({row, col});
                    cell.element.classList.add('selected');
                } else if (gameState.selectedCells.length === 1) {
                    // 第二个选择，检查是否相邻
                    const first = gameState.selectedCells[0];
                    if (isAdjacent(first, {row, col})) {
                        gameState.selectedCells.push({row, col});
                        cell.element.classList.add('selected');
                        
                        // 延迟交换
                        setTimeout(() => {
                            swapCells(first, {row, col});
                        }, 200);
                    } else {
                        // 不相邻，重新选择
                        clearSelection();
                        gameState.selectedCells.push({row, col});
                        cell.element.classList.add('selected');
                    }
                }
            }
        }

        // 检查是否相邻
        function isAdjacent(cell1, cell2) {
            const rowDiff = Math.abs(cell1.row - cell2.row);
            const colDiff = Math.abs(cell1.col - cell2.col);
            return (rowDiff === 1 && colDiff === 0) || (rowDiff === 0 && colDiff === 1);
        }

        // 交换单元格
        function swapCells(pos1, pos2) {
            const cell1 = gameState.grid[pos1.row][pos1.col];
            const cell2 = gameState.grid[pos2.row][pos2.col];
            
            // 交换水果
            const tempFruit = cell1.fruit;
            cell1.fruit = cell2.fruit;
            cell2.fruit = tempFruit;
            
            // 更新显示
            cell1.element.querySelector('.fruit').textContent = cell1.fruit;
            cell2.element.querySelector('.fruit').textContent = cell2.fruit;
            
            // 添加交换动画
            cell1.element.style.transform = 'scale(1.1)';
            cell2.element.style.transform = 'scale(1.1)';
            
            setTimeout(() => {
                cell1.element.style.transform = 'scale(1)';
                cell2.element.style.transform = 'scale(1)';
                
                // 检查匹配
                const matches = findMatches();
                if (matches.length > 0) {
                    processMatches(matches);
                } else {
                    // 没有匹配，交换回来
                    setTimeout(() => {
                        const tempFruit = cell1.fruit;
                        cell1.fruit = cell2.fruit;
                        cell2.fruit = tempFruit;
                        
                        cell1.element.querySelector('.fruit').textContent = cell1.fruit;
                        cell2.element.querySelector('.fruit').textContent = cell2.fruit;
                        
                        // 扣血（练习模式不扣血）
                        if (gameState.gameMode !== 'practice') {
                            gameState.lives--;
                            showTemporaryMessage('💔 没有匹配，失去一条生命');
                            updateUI();
                            
                            if (gameState.lives <= 0) {
                                gameOver();
                            }
                        } else {
                            showTemporaryMessage('🌟 练习模式：没有匹配，再试试别的组合吧！');
                        }
                    }, 500);
                }
                
                clearSelection();
            }, 300);
        }

        // 清除选择
        function clearSelection() {
            gameState.selectedCells.forEach(pos => {
                const cell = gameState.grid[pos.row][pos.col];
                if (cell && cell.element) {
                    cell.element.classList.remove('selected');
                }
            });
            gameState.selectedCells = [];
        }

        // 寻找匹配
        function findMatches() {
            const matches = [];
            const size = gameState.grid.length;
            
            // 检查水平匹配
            for (let row = 0; row < size; row++) {
                let count = 1;
                let currentFruit = gameState.grid[row][0].fruit;
                
                for (let col = 1; col < size; col++) {
                    if (gameState.grid[row][col].fruit === currentFruit) {
                        count++;
                    } else {
                        if (count >= 3) {
                            for (let i = col - count; i < col; i++) {
                                matches.push({row: row, col: i});
                            }
                        }
                        count = 1;
                        currentFruit = gameState.grid[row][col].fruit;
                    }
                }
                
                // 检查行末
                if (count >= 3) {
                    for (let i = size - count; i < size; i++) {
                        matches.push({row: row, col: i});
                    }
                }
            }
            
            // 检查垂直匹配
            for (let col = 0; col < size; col++) {
                let count = 1;
                let currentFruit = gameState.grid[0][col].fruit;
                
                for (let row = 1; row < size; row++) {
                    if (gameState.grid[row][col].fruit === currentFruit) {
                        count++;
                    } else {
                        if (count >= 3) {
                            for (let i = row - count; i < row; i++) {
                                matches.push({row: i, col: col});
                            }
                        }
                        count = 1;
                        currentFruit = gameState.grid[row][col].fruit;
                    }
                }
                
                // 检查列末
                if (count >= 3) {
                    for (let i = size - count; i < size; i++) {
                        matches.push({row: i, col: col});
                    }
                }
            }
            
            // 去重
            const uniqueMatches = [];
            const seen = new Set();
            matches.forEach(match => {
                const key = `${match.row}-${match.col}`;
                if (!seen.has(key)) {
                    seen.add(key);
                    uniqueMatches.push(match);
                }
            });
            
            return uniqueMatches;
        }

        // 处理匹配
        function processMatches(matches) {
            console.log(`💖 找到 ${matches.length} 个匹配！`);
            
            // 计算分数
            const baseScore = matches.length * 10;
            const comboBonus = gameState.combo * 5;
            const multiplierBonus = baseScore * (gameState.multiplier - 1);
            const totalScore = baseScore + comboBonus + multiplierBonus;
            
            gameState.score += totalScore;
            gameState.combo++;
            
            // 更新最大连击记录
            if (gameState.combo > gameState.stats.maxCombo) {
                gameState.stats.maxCombo = gameState.combo;
            }
            
            // 更新倍数
            if (gameState.combo >= 5 && gameState.combo % 5 === 0) {
                gameState.multiplier = Math.min(gameState.multiplier + 0.5, 5);
                document.getElementById('multiplierStat').style.display = 'block';
            }
            
            // 添加特殊效果
            matches.forEach(match => {
                const cell = gameState.grid[match.row][match.col];
                createParticleEffect(cell.element, totalScore >= 50 ? '💎' : '⭐');
                
                // 添加消除动画
                cell.element.style.animation = 'fruitPop 0.5s reverse';
            });
            
            // 延迟后移除匹配的单元格
            setTimeout(() => {
                removeMatches(matches);
                dropFruits();
                
                setTimeout(() => {
                    fillEmptySpaces();
                    
                    // 检查是否有新的匹配（连击）
                    setTimeout(() => {
                        const newMatches = findMatches();
                        if (newMatches.length > 0) {
                            processMatches(newMatches);
                        } else {
                            // 连击结束，重置combo如果没有持续匹配
                            if (gameState.combo > 0) {
                                setTimeout(() => {
                                    gameState.combo = 0;
                                    gameState.multiplier = 1;
                                    document.getElementById('multiplierStat').style.display = 'none';
                                    updateUI();
                                }, 2000);
                            }
                            
                            // 检查是否还有有效移动
                            if (!hasValidMoves()) {
                                if (gameState.gameMode !== 'practice') {
                                    showTemporaryMessage('💫 没有更多移动了，重新洗牌！');
                                }
                                shuffleGrid();
                            }
                        }
                        updateUI();
                    }, 300);
                }, 300);
            }, 500);
            
            // 显示Ashley鼓励消息
            showRandomAshleyMessage();
            
            // 检查成就
            checkAchievements();
        }

        // 移除匹配的单元格
        function removeMatches(matches) {
            matches.forEach(match => {
                const cell = gameState.grid[match.row][match.col];
                cell.fruit = null;
                if (cell.element.querySelector('.fruit')) {
                    cell.element.querySelector('.fruit').textContent = '';
                    cell.element.classList.add('matched');
                }
            });
        }

        // 下落水果
        function dropFruits() {
            const size = gameState.grid.length;
            
            for (let col = 0; col < size; col++) {
                // 从底部开始，找到空位
                let writeIndex = size - 1;
                
                for (let row = size - 1; row >= 0; row--) {
                    if (gameState.grid[row][col].fruit !== null) {
                        if (row !== writeIndex) {
                            // 移动水果
                            gameState.grid[writeIndex][col].fruit = gameState.grid[row][col].fruit;
                            gameState.grid[writeIndex][col].element.querySelector('.fruit').textContent = 
                                gameState.grid[row][col].fruit;
                            
                            // 清空原位置
                            gameState.grid[row][col].fruit = null;
                            gameState.grid[row][col].element.querySelector('.fruit').textContent = '';
                            gameState.grid[row][col].element.classList.add('matched');
                            
                            // 移除新位置的matched类
                            gameState.grid[writeIndex][col].element.classList.remove('matched');
                        } else {
                            gameState.grid[writeIndex][col].element.classList.remove('matched');
                        }
                        writeIndex--;
                    }
                }
            }
        }

        // 填充空位
        function fillEmptySpaces() {
            const size = gameState.grid.length;
            
            for (let col = 0; col < size; col++) {
                for (let row = 0; row < size; row++) {
                    if (gameState.grid[row][col].fruit === null) {
                        gameState.grid[row][col].fruit = getRandomFruit();
                        const fruitElement = gameState.grid[row][col].element.querySelector('.fruit');
                        fruitElement.textContent = gameState.grid[row][col].fruit;
                        fruitElement.style.animation = 'fruitPop 0.4s ease-out';
                        gameState.grid[row][col].element.classList.remove('matched');
                    }
                }
            }
        }

        // 检查是否有有效移动
        function hasValidMoves() {
            const size = gameState.grid.length;
            
            for (let row = 0; row < size; row++) {
                for (let col = 0; col < size; col++) {
                    // 尝试与右边交换
                    if (col < size - 1) {
                        if (wouldCreateMatch(row, col, row, col + 1)) {
                            return true;
                        }
                    }
                    
                    // 尝试与下面交换
                    if (row < size - 1) {
                        if (wouldCreateMatch(row, col, row + 1, col)) {
                            return true;
                        }
                    }
                }
            }
            
            return false;
        }

        // 检查交换是否会创造匹配
        function wouldCreateMatch(row1, col1, row2, col2) {
            // 临时交换
            const temp = gameState.grid[row1][col1].fruit;
            gameState.grid[row1][col1].fruit = gameState.grid[row2][col2].fruit;
            gameState.grid[row2][col2].fruit = temp;
            
            // 检查是否有匹配
            const matches = findMatches();
            
            // 交换回来
            gameState.grid[row2][col2].fruit = gameState.grid[row1][col1].fruit;
            gameState.grid[row1][col1].fruit = temp;
            
            return matches.length > 0;
        }

        // 洗牌网格
        function shuffleGrid() {
            console.log('🔀 洗牌网格...');
            
            const size = gameState.grid.length;
            const fruits = [];
            
            // 收集所有水果
            for (let row = 0; row < size; row++) {
                for (let col = 0; col < size; col++) {
                    fruits.push(gameState.grid[row][col].fruit);
                }
            }
            
            // 洗牌
            for (let i = fruits.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [fruits[i], fruits[j]] = [fruits[j], fruits[i]];
            }
            
            // 重新分配
            let index = 0;
            for (let row = 0; row < size; row++) {
                for (let col = 0; col < size; col++) {
                    gameState.grid[row][col].fruit = fruits[index];
                    gameState.grid[row][col].element.querySelector('.fruit').textContent = fruits[index];
                    gameState.grid[row][col].element.classList.remove('matched');
                    index++;
                }
            }
            
            // 确保洗牌后有有效移动
            let attempts = 0;
            while (!hasValidMoves() && attempts < 10) {
                // 如果还是没有有效移动，再次洗牌
                for (let i = fruits.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [fruits[i], fruits[j]] = [fruits[j], fruits[i]];
                }
                
                index = 0;
                for (let row = 0; row < size; row++) {
                    for (let col = 0; col < size; col++) {
                        gameState.grid[row][col].fruit = fruits[index];
                        gameState.grid[row][col].element.querySelector('.fruit').textContent = fruits[index];
                        index++;
                    }
                }
                attempts++;
            }
        }

        // 获取提示
        function getHint() {
            console.log('💡 获取提示...');
            
            const size = gameState.grid.length;
            
            for (let row = 0; row < size; row++) {
                for (let col = 0; col < size; col++) {
                    // 检查与右边交换
                    if (col < size - 1) {
                        if (wouldCreateMatch(row, col, row, col + 1)) {
                            showHint(row, col, row, col + 1);
                            return;
                        }
                    }
                    
                    // 检查与下面交换
                    if (row < size - 1) {
                        if (wouldCreateMatch(row, col, row + 1, col)) {
                            showHint(row, col, row + 1, col);
                            return;
                        }
                    }
                }
            }
            
            showTemporaryMessage('💫 没有找到明显的提示，试试洗牌吧！');
        }

        // 显示提示
        function showHint(row1, col1, row2, col2) {
            const cell1 = gameState.grid[row1][col1].element;
            const cell2 = gameState.grid[row2][col2].element;
            
            cell1.classList.add('hint');
            cell2.classList.add('hint');
            
            setTimeout(() => {
                cell1.classList.remove('hint');
                cell2.classList.remove('hint');
            }, 4500);
            
            showAshleyMessage('💡 看看这两个位置哦！');
        }

        // 道具系统
        function updatePowerUpsUI() {
            const desktopContainer = document.getElementById('desktopPowerUps');
            const mobileContainer = document.getElementById('mobilePowerUps');
            const practiceDesktop = document.getElementById('practicePowerUps');
            const practiceMobile = document.getElementById('mobilePracticePowerUps');
            
            const containers = [desktopContainer, mobileContainer, practiceDesktop, practiceMobile].filter(c => c);
            
            containers.forEach(container => {
                container.innerHTML = '';
                
                gameConfig.powerUps.forEach(powerUp => {
                    const count = gameState.powerUps[powerUp.id] || 0;
                    const button = document.createElement('button');
                    button.className = 'powerup-btn';
                    button.onclick = () => selectPowerUp(powerUp.id);
                    
                    if (count === 0 && gameState.gameMode !== 'practice') {
                        button.classList.add('disabled');
                    }
                    
                    if (gameState.activePowerUp === powerUp.id) {
                        button.classList.add('active');
                    }
                    
                    button.innerHTML = `
                        <div class="powerup-icon">${powerUp.icon}</div>
                        <div class="powerup-name">${powerUp.name}</div>
                        ${gameState.gameMode !== 'practice' && count > 0 ? 
                          `<div class="powerup-count">${count}</div>` : ''}
                    `;
                    
                    container.appendChild(button);
                });
            });
        }

        // 选择道具
        function selectPowerUp(powerUpId) {
            const count = gameState.powerUps[powerUpId] || 0;
            
            if (gameState.gameMode !== 'practice' && count === 0) {
                showTemporaryMessage('💔 道具数量不足！');
                return;
            }
            
            if (gameState.activePowerUp === powerUpId) {
                // 取消选择
                gameState.activePowerUp = null;
                showAshleyMessage('💕 取消了道具选择');
            } else {
                // 选择道具
                gameState.activePowerUp = powerUpId;
                const powerUp = gameConfig.powerUps.find(p => p.id === powerUpId);
                showAshleyMessage(`✨ 选择了${powerUp.name}道具，点击网格使用！`);
            }
            
            updatePowerUpsUI();
        }

        // 使用道具
        function usePowerUp(powerUpId, row, col) {
            const powerUp = gameConfig.powerUps.find(p => p.id === powerUpId);
            if (!powerUp) return;
            
            console.log(`✨ 使用道具: ${powerUp.name} 在 (${row}, ${col})`);
            
            // 消耗道具
            if (gameState.gameMode !== 'practice') {
                if (gameState.powerUps[powerUpId] > 0) {
                    gameState.powerUps[powerUpId]--;
                    gameState.stats.powerUpsUsed++;
                } else {
                    showTemporaryMessage('💔 道具数量不足！');
                    return;
                }
            }
            
            // 执行道具效果
            switch (powerUpId) {
                case 'bomb':
                    useBombPowerUp(row, col);
                    break;
                case 'lightning':
                    useLightningPowerUp(row, col);
                    break;
                case 'rainbow':
                    useRainbowPowerUp(row, col);
                    break;
                case 'star':
                    useStarPowerUp(row, col);
                    break;
                case 'heart':
                    useHeartPowerUp();
                    break;
                case 'magic':
                    useMagicPowerUp();
                    break;
            }
            
            // 取消道具选择
            gameState.activePowerUp = null;
            updatePowerUpsUI();
            updateUI();
            
            checkAchievements();
        }

        // 炸弹道具 - 炸掉周围3x3区域
        function useBombPowerUp(centerRow, centerCol) {
            const matches = [];
            const size = gameState.grid.length;
            
            for (let row = Math.max(0, centerRow - 1); row <= Math.min(size - 1, centerRow + 1); row++) {
                for (let col = Math.max(0, centerCol - 1); col <= Math.min(size - 1, centerCol + 1); col++) {
                    matches.push({row, col});
                    const cell = gameState.grid[row][col];
                    createParticleEffect(cell.element, '💥');
                }
            }
            
            setTimeout(() => {
                processMatches(matches);
            }, 300);
            
            showAshleyMessage('💥 轰！炸弹威力好大呀！');
        }

        // 闪电道具 - 清除整行或整列
        function useLightningPowerUp(row, col) {
            const matches = [];
            const size = gameState.grid.length;
            const isRow = Math.random() < 0.5;
            
            if (isRow) {
                // 清除整行
                for (let c = 0; c < size; c++) {
                    matches.push({row, col: c});
                    const cell = gameState.grid[row][c];
                    createParticleEffect(cell.element, '⚡');
                }
                showAshleyMessage('⚡ 闪电横扫整行！');
            } else {
                // 清除整列
                for (let r = 0; r < size; r++) {
                    matches.push({row: r, col});
                    const cell = gameState.grid[r][col];
                    createParticleEffect(cell.element, '⚡');
                }
                showAshleyMessage('⚡ 闪电纵贯整列！');
            }
            
            setTimeout(() => {
                processMatches(matches);
            }, 300);
        }

        // 彩虹道具 - 清除所有同种水果
        function useRainbowPowerUp(row, col) {
            const targetFruit = gameState.grid[row][col].fruit;
            const matches = [];
            const size = gameState.grid.length;
            
            for (let r = 0; r < size; r++) {
                for (let c = 0; c < size; c++) {
                    if (gameState.grid[r][c].fruit === targetFruit) {
                        matches.push({row: r, col: c});
                        createParticleEffect(gameState.grid[r][c].element, '🌈');
                    }
                }
            }
            
            setTimeout(() => {
                processMatches(matches);
            }, 300);
            
            showAshleyMessage(`🌈 彩虹清除了所有${targetFruit}！`);
        }

        // 星星道具 - 随机清除15个格子
        function useStarPowerUp(row, col) {
            const matches = [];
            const size = gameState.grid.length;
            const allPositions = [];
            
            // 收集所有位置
            for (let r = 0; r < size; r++) {
                for (let c = 0; c < size; c++) {
                    allPositions.push({row: r, col: c});
                }
            }
            
            // 随机选择15个位置
            const selectedCount = Math.min(15, allPositions.length);
            for (let i = 0; i < selectedCount; i++) {
                const randomIndex = Math.floor(Math.random() * allPositions.length);
                const pos = allPositions.splice(randomIndex, 1)[0];
                matches.push(pos);
                createParticleEffect(gameState.grid[pos.row][pos.col].element, '⭐');
            }
            
            setTimeout(() => {
                processMatches(matches);
            }, 300);
            
            showAshleyMessage('⭐ 星星的魔法闪闪发光！');
        }

        // 爱心道具 - 恢复生命
        function useHeartPowerUp() {
            if (gameState.gameMode !== 'practice') {
                const config = gameConfig.difficulties[gameState.difficulty];
                const healAmount = Math.min(5, config.lives - gameState.lives);
                gameState.lives += healAmount;
                
                showTemporaryMessage(`💖 恢复了${healAmount}点生命！`);
                showAshleyMessage('💖 爱心的力量让你重新充满活力！');
            } else {
                showAshleyMessage('💖 练习模式已经是无限生命啦！');
            }
        }

        // 魔法道具 - 重新洗牌并获得高分
        function useMagicPowerUp() {
            shuffleGrid();
            gameState.score += 100;
            gameState.combo += 3;
            
            showTemporaryMessage('✨ 魔法重置了棋盘并奖励了分数！');
            showAshleyMessage('✨ 魔法的力量改变了一切！');
        }

        // 创建粒子效果
        function createParticleEffect(element, particle) {
            const rect = element.getBoundingClientRect();
            const containerRect = document.getElementById('gameContainer').getBoundingClientRect();
            
            for (let i = 0; i < 3; i++) {
                setTimeout(() => {
                    const particleElement = document.createElement('div');
                    particleElement.className = 'particle';
                    particleElement.textContent = particle;
                    particleElement.style.position = 'absolute';
                    particleElement.style.left = (rect.left - containerRect.left + Math.random() * rect.width) + 'px';
                    particleElement.style.top = (rect.top - containerRect.top + Math.random() * rect.height)
                    + 'px';
                    particleElement.style.fontSize = '20px';
                    particleElement.style.color = '#ff6b9d';
                    particleElement.style.animation = 'particleFloat 1s ease-out forwards';
                    particleElement.style.pointerEvents = 'none';
                    particleElement.style.zIndex = '1000';
                    
                    document.getElementById('gameContainer').appendChild(particleElement);
                    
                    setTimeout(() => {
                        if (particleElement.parentNode) {
                            particleElement.parentNode.removeChild(particleElement);
                        }
                    }, 1000);
                }, i * 100);
            }
        }

        // 显示Ashley消息
        function showAshleyMessage(message) {
            const messageElement = document.getElementById('ashleyMessage');
            if (messageElement) {
                messageElement.textContent = message;
                messageElement.style.animation = 'messageGlow 0.5s ease-in-out';
                
                setTimeout(() => {
                    messageElement.style.animation = '';
                }, 500);
            }
        }

        // 显示随机Ashley鼓励消息
        function showRandomAshleyMessage() {
            const message = ashleyMessages[Math.floor(Math.random() * ashleyMessages.length)];
            showAshleyMessage(message);
        }

        // 显示临时消息
        function showTemporaryMessage(message) {
            // 创建临时消息元素
            const msgElement = document.createElement('div');
            msgElement.className = 'temporary-message';
            msgElement.textContent = message;
            msgElement.style.cssText = `
                position: fixed;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                background: linear-gradient(45deg, #ff6b9d, #c44569);
                color: white;
                padding: 15px 25px;
                border-radius: 25px;
                font-size: 16px;
                font-weight: bold;
                z-index: 10000;
                box-shadow: 0 10px 30px rgba(255, 107, 157, 0.3);
                animation: messagePopup 3s ease-in-out forwards;
            `;
            
            document.body.appendChild(msgElement);
            
            setTimeout(() => {
                if (msgElement.parentNode) {
                    msgElement.parentNode.removeChild(msgElement);
                }
            }, 3000);
        }

        // 更新UI
        function updateUI() {
            // 更新分数和生命
            const scoreElements = ['score', 'practiceScore', 'mobileScore', 'mobilePracticeScore'];
            const livesElements = ['lives', 'mobileLives'];
            const comboElements = ['combo', 'practiceCombo', 'mobileCombo', 'mobilePracticeCombo'];
            const multiplierElements = ['multiplier'];
            
            scoreElements.forEach(id => {
                const element = document.getElementById(id);
                if (element) {
                    element.textContent = gameState.score.toLocaleString();
                }
            });
            
            livesElements.forEach(id => {
                const element = document.getElementById(id);
                if (element) {
                    if (gameState.gameMode === 'practice') {
                        element.textContent = '∞';
                    } else {
                        element.textContent = gameState.lives;
                    }
                }
            });
            
            comboElements.forEach(id => {
                const element = document.getElementById(id);
                if (element) {
                    element.textContent = gameState.combo;
                }
            });
            
            multiplierElements.forEach(id => {
                const element = document.getElementById(id);
                if (element) {
                    element.textContent = gameState.multiplier.toFixed(1) + 'x';
                }
            });
            
            // 更新最高分
            if (gameState.score > gameState.bestScore) {
                gameState.bestScore = gameState.score;
                updateHighScore();
                
                if (gameState.gameMode !== 'practice') {
                    showTemporaryMessage('🎉 新的最高分！Ashley一定很骄傲！');
                }
            }
        }

        // 更新最高分显示
        function updateHighScore() {
            const highScoreElement = document.getElementById('highScoreDisplay');
            if (highScoreElement) {
                highScoreElement.textContent = gameState.bestScore.toLocaleString();
            }
        }

        // 暂停游戏
        function pauseGame() {
            gameState.isPaused = !gameState.isPaused;
            const pauseBtn = document.getElementById('pauseBtn');
            
            if (gameState.isPaused) {
                pauseBtn.textContent = '▶️ 继续';
                showAshleyMessage('⏸️ 暂停了，休息一下吧～');
                showTemporaryMessage('⏸️ 游戏已暂停');
            } else {
                pauseBtn.textContent = '⏸️ 暂停';
                showAshleyMessage('💕 继续我们的甜蜜冒险！');
                showTemporaryMessage('▶️ 游戏继续');
            }
        }

        // 游戏结束
        function gameOver() {
            console.log('💔 游戏结束');
            
            gameState.isGameOver = true;
            gameState.stats.gamesPlayed++;
            gameState.stats.totalScore += gameState.score;
            
            clearSelection();
            
            // 保存游戏数据
            saveGame();
            
            // 检查成就
            checkAchievements();
            
            // 显示游戏结束消息
            setTimeout(() => {
                let gameOverMessage = '💔 游戏结束了，但Ashley依然爱你！\n\n';
                gameOverMessage += `💎 最终分数: ${gameState.score.toLocaleString()}\n`;
                gameOverMessage += `⭐ 最高连击: ${gameState.stats.maxCombo}\n`;
                
                if (gameState.score === gameState.bestScore && gameState.score > 0) {
                    gameOverMessage += '🎉 恭喜！这是你的最高分！\n';
                }
                
                gameOverMessage += '\n💕 要再试一次吗？Ashley相信你可以做得更好！';
                
                if (confirm(gameOverMessage)) {
                    startGame(gameState.difficulty);
                } else {
                    showScreen('menu');
                }
            }, 1000);
        }

        // 成就系统
        function initAchievements() {
            // 初始化成就状态
            Object.keys(achievements).forEach(key => {
                if (!(key in gameState.achievements)) {
                    gameState.achievements[key] = false;
                }
            });
        }

        function checkAchievements() {
            Object.keys(achievements).forEach(key => {
                const achievement = achievements[key];
                if (!gameState.achievements[key] && achievement.condition()) {
                    unlockAchievement(key);
                }
            });
        }

        function unlockAchievement(achievementId) {
            gameState.achievements[achievementId] = true;
            const achievement = achievements[achievementId];
            
            console.log(`🏆 解锁成就: ${achievement.name}`);
            
            // 显示成就解锁动画
            showAchievementUnlock(achievement);
            
            // 保存进度
            saveGame();
        }

        function showAchievementUnlock(achievement) {
            const achievementElement = document.createElement('div');
            achievementElement.className = 'achievement-unlock';
            achievementElement.innerHTML = `
                <div class="achievement-icon">${achievement.icon}</div>
                <div class="achievement-info">
                    <div class="achievement-title">🎉 成就解锁！</div>
                    <div class="achievement-name">${achievement.name}</div>
                    <div class="achievement-desc">${achievement.desc}</div>
                </div>
            `;
            
            achievementElement.style.cssText = `
                position: fixed;
                top: 20px;
                right: 20px;
                background: linear-gradient(45deg, #ff6b9d, #c44569);
                color: white;
                padding: 20px;
                border-radius: 15px;
                box-shadow: 0 10px 30px rgba(255, 107, 157, 0.4);
                z-index: 10000;
                animation: achievementSlide 4s ease-in-out forwards;
                max-width: 300px;
                font-family: Arial, sans-serif;
            `;
            
            document.body.appendChild(achievementElement);
            
            setTimeout(() => {
                if (achievementElement.parentNode) {
                    achievementElement.parentNode.removeChild(achievementElement);
                }
            }, 4000);
        }

        function renderAchievements() {
            const container = document.getElementById('achievementsList');
            container.innerHTML = '';
            
            Object.keys(achievements).forEach(key => {
                const achievement = achievements[key];
                const isUnlocked = gameState.achievements[key];
                
                const achievementCard = document.createElement('div');
                achievementCard.className = `achievement-card ${isUnlocked ? 'unlocked' : 'locked'}`;
                achievementCard.innerHTML = `
                    <div class="achievement-icon">${isUnlocked ? achievement.icon : '🔒'}</div>
                    <div class="achievement-info">
                        <div class="achievement-name">${achievement.name}</div>
                        <div class="achievement-desc">${achievement.desc}</div>
                        ${isUnlocked ? '<div class="achievement-status">✅ 已解锁</div>' : 
                          '<div class="achievement-status">🔒 未解锁</div>'}
                    </div>
                `;
                
                container.appendChild(achievementCard);
            });
        }

        // 情书界面特效
        function showLoveAnimation() {
            // 创建爱心雨效果
            for (let i = 0; i < 20; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.textContent = ['💖', '💕', '💝', '💗', '💓'][Math.floor(Math.random() * 5)];
                    heart.style.cssText = `
                        position: fixed;
                        left: ${Math.random() * 100}%;
                        top: -50px;
                        font-size: ${20 + Math.random() * 30}px;
                        animation: heartRain ${3 + Math.random() * 2}s linear forwards;
                        z-index: 10000;
                        pointer-events: none;
                    `;
                    
                    document.body.appendChild(heart);
                    
                    setTimeout(() => {
                        if (heart.parentNode) {
                            heart.parentNode.removeChild(heart);
                        }
                    }, 5000);
                }, i * 100);
            }
            
            showTemporaryMessage('💖💖💖 给Ashley最大最温暖的拥抱！💖💖💖');
        }

        function playBirthdaySong() {
            // 模拟播放生日快乐歌（由于无法播放真实音频，用动画效果代替）
            const notes = ['🎵', '🎶', '🎼', '♪', '♫', '♬'];
            
            for (let i = 0; i < 12; i++) {
                setTimeout(() => {
                    const note = document.createElement('div');
                    note.textContent = notes[Math.floor(Math.random() * notes.length)];
                    note.style.cssText = `
                        position: fixed;
                        left: ${20 + i * 7}%;
                        top: 30%;
                        font-size: 30px;
                        color: #ff6b9d;
                        animation: noteFloat 2s ease-out forwards;
                        z-index: 10000;
                        pointer-events: none;
                    `;
                    
                    document.body.appendChild(note);
                    
                    setTimeout(() => {
                        if (note.parentNode) {
                            note.parentNode.removeChild(note);
                        }
                    }, 2000);
                }, i * 200);
            }
            
            showTemporaryMessage('🎂🎵 生日快乐歌为Ashley响起！🎵🎂');
        }

        // 存储系统
        function saveGame() {
            const saveData = {
                bestScore: gameState.bestScore,
                achievements: gameState.achievements,
                stats: gameState.stats
            };
            
            try {
                localStorage.setItem('ashleyFruitMatch', JSON.stringify(saveData));
                console.log('💾 游戏数据已保存');
            } catch (error) {
                console.log('💔 保存失败:', error);
            }
        }

        function loadGame() {
            try {
                const savedData = localStorage.getItem('ashleyFruitMatch');
                if (savedData) {
                    const data = JSON.parse(savedData);
                    gameState.bestScore = data.bestScore || 0;
                    gameState.achievements = data.achievements || {};
                    gameState.stats = {...gameState.stats, ...data.stats};
                    console.log('💖 游戏数据已加载');
                }
            } catch (error) {
                console.log('💔 加载失败:', error);
            }
        }

        // 移动端适配
        function handleResize() {
            // 重新调整游戏网格大小
            const gameGrid = document.getElementById('gameGrid');
            const practiceGrid = document.getElementById('practiceGrid');
            
            [gameGrid, practiceGrid].forEach(grid => {
                if (grid && grid.children.length > 0) {
                    const size = Math.sqrt(grid.children.length);
                    const isMobile = window.innerWidth < 768;
                    
                    if (isMobile) {
                        const gridSize = Math.min(window.innerWidth - 40, 350);
                        grid.style.width = gridSize + 'px';
                        grid.style.height = gridSize + 'px';
                    }
                }
            });
        }

        // 事件监听
        window.addEventListener('resize', handleResize);
        window.addEventListener('orientationchange', () => {
            setTimeout(handleResize, 100);
        });

        // 防止页面滚动（移动端）
        document.addEventListener('touchmove', function(e) {
            if (gameState.currentScreen === 'game' || gameState.currentScreen === 'practice') {
                e.preventDefault();
            }
        }, { passive: false });

        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', function() {
            console.log('💖 Ashley专属水果匹配游戏加载中...');
            
            // 显示加载界面
            showScreen('loading');
            
            // 模拟加载过程
            setTimeout(() => {
                init();
                showScreen('menu');
                console.log('🎮 游戏准备就绪！为Ashley献上最甜蜜的游戏体验！');
            }, 2000);
        });

        // 添加额外的动画样式
        const style = document.createElement('style');
        style.textContent = `
            @keyframes messagePopup {
                0% { 
                    opacity: 0; 
                    transform: translate(-50%, -50%) scale(0.5); 
                }
                15% { 
                    opacity: 1; 
                    transform: translate(-50%, -50%) scale(1.1); 
                }
                25% { 
                    opacity: 1; 
                    transform: translate(-50%, -50%) scale(1); 
                }
                85% { 
                    opacity: 1; 
                    transform: translate(-50%, -50%) scale(1); 
                }
                100% { 
                    opacity: 0; 
                    transform: translate(-50%, -50%) scale(0.8); 
                }
            }
            
            @keyframes achievementSlide {
                0% { 
                    transform: translateX(400px); 
                    opacity: 0; 
                }
                15% { 
                    transform: translateX(0); 
                    opacity: 1; 
                }
                85% { 
                    transform: translateX(0); 
                    opacity: 1; 
                }
                100% { 
                    transform: translateX(400px); 
                    opacity: 0; 
                }
            }
            
            @keyframes heartRain {
                0% { 
                    top: -50px; 
                    opacity: 1; 
                    transform: rotate(0deg); 
                }
                100% { 
                    top: calc(100vh + 50px); 
                    opacity: 0; 
                    transform: rotate(360deg); 
                }
            }
            
            @keyframes noteFloat {
                0% { 
                    opacity: 0; 
                    transform: translateY(0) scale(0.5); 
                }
                50% { 
                    opacity: 1; 
                    transform: translateY(-30px) scale(1.2); 
                }
                100% { 
                    opacity: 0; 
                    transform: translateY(-60px) scale(1); 
                }
            }
            
            @keyframes particleFloat {
                0% { 
                    opacity: 1; 
                    transform: translateY(0) scale(1); 
                }
                100% { 
                    opacity: 0; 
                    transform: translateY(-50px) scale(1.5); 
                }
            }
            
            @keyframes messageGlow {
                0% { 
                    box-shadow: 0 0 5px rgba(255, 107, 157, 0.3); 
                }
                50% { 
                    box-shadow: 0 0 20px rgba(255, 107, 157, 0.8); 
                }
                100% { 
                    box-shadow: 0 0 5px rgba(255, 107, 157, 0.3); 
                }
            }
            
            @keyframes birthdayTextGlow {
                0%, 100% { 
                    color: #ff6b9d; 
                    text-shadow: 0 0 5px rgba(255, 107, 157, 0.5); 
                }
                50% { 
                    color: #ffd700; 
                    text-shadow: 0 0 20px rgba(255, 215, 0, 0.8); 
                }
            }
        `;
        
        document.head.appendChild(style);
        
        // 全局函数导出（供HTML调用）
        window.showScreen = showScreen;
        window.showDifficultySelect = showDifficultySelect;
        window.startGame = startGame;
        window.startPractice = startPractice;
        window.resetPractice = resetPractice;
        window.pauseGame = pauseGame;
        window.getHint = getHint;
        window.showLoveAnimation = showLoveAnimation;
        window.playBirthdaySong = playBirthdaySong;
        
        console.log('💕 Ashley专属水果匹配游戏 - 所有系统加载完成！');
        
    </script>
</body>
</html>
