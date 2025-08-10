
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FoggyHub Key System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 25%, #334155 50%, #1e293b 75%, #0f172a 100%);
            background-size: 400% 400%;
            animation: gradientShift 15s ease infinite;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow-x: hidden;
            padding: 20px;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: 0;
            pointer-events: none;
        }

        .particle {
            position: absolute;
            background: rgba(255, 255, 255, 0.08);
            border-radius: 50%;
            animation: float 25s infinite linear;
        }

        .particle:nth-child(odd) {
            background: rgba(74, 222, 128, 0.15);
        }

        .particle:nth-child(even) {
            background: rgba(59, 130, 246, 0.15);
        }

        .particle:nth-child(3n) {
            background: rgba(168, 85, 247, 0.12);
        }

        @keyframes float {
            0% { transform: translateY(100vh) rotate(0deg) scale(0); opacity: 0; }
            10% { opacity: 1; transform: translateY(90vh) rotate(36deg) scale(1); }
            90% { opacity: 1; transform: translateY(-10vh) rotate(324deg) scale(1); }
            100% { transform: translateY(-100vh) rotate(360deg) scale(0); opacity: 0; }
        }

        .container {
            background: rgba(15, 23, 42, 0.95);
            backdrop-filter: blur(30px);
            border-radius: 35px;
            padding: 60px;
            box-shadow: 
                0 35px 70px rgba(0, 0, 0, 0.5),
                0 0 0 1px rgba(255, 255, 255, 0.1),
                inset 0 1px 0 rgba(255, 255, 255, 0.15);
            max-width: 1200px;
            width: 100%;
            min-height: 90vh;
            text-align: center;
            position: relative;
            z-index: 1;
            animation: containerEntry 1.5s cubic-bezier(0.4, 0, 0.2, 1);
            border: 2px solid rgba(74, 222, 128, 0.1);
        }

        @keyframes containerEntry {
            0% { 
                transform: translateY(100px) scale(0.7); 
                opacity: 0;
                filter: blur(20px);
            }
            100% { 
                transform: translateY(0) scale(1); 
                opacity: 1;
                filter: blur(0);
            }
        }

        .title {
            font-size: 5.5rem;
            font-weight: 900;
            background: linear-gradient(135deg, #4ade80 0%, #3b82f6 35%, #8b5cf6 70%, #ec4899 100%);
            background-size: 300% 300%;
            animation: gradientText 4s ease infinite;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 50px;
            text-shadow: 0 0 50px rgba(74, 222, 128, 0.5);
            filter: drop-shadow(0 0 20px rgba(74, 222, 128, 0.3));
            position: relative;
            animation: titleFloat 6s ease-in-out infinite;
        }

        @keyframes titleFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }

        @keyframes gradientText {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .tabs {
            display: flex;
            margin-bottom: 40px;
            background: rgba(30, 41, 59, 0.9);
            border-radius: 25px;
            padding: 8px;
            gap: 8px;
            border: 1px solid rgba(74, 222, 128, 0.2);
            animation: tabsGlow 3s ease-in-out infinite alternate;
        }

        @keyframes tabsGlow {
            from { box-shadow: 0 0 20px rgba(74, 222, 128, 0.2); }
            to { box-shadow: 0 0 35px rgba(74, 222, 128, 0.4); }
        }

        .tab {
            flex: 1;
            padding: 20px 30px;
            background: transparent;
            border: none;
            border-radius: 18px;
            color: #94a3b8;
            font-weight: 700;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            overflow: hidden;
        }

        .tab::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(135deg, #4ade80, #3b82f6, #8b5cf6);
            opacity: 0;
            transition: all 0.4s ease;
            border-radius: 18px;
        }

        .tab.active {
            color: white;
            transform: translateY(-3px) scale(1.02);
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
        }

        .tab.active::before {
            opacity: 1;
            animation: tabPulse 2s ease-in-out infinite;
        }

        @keyframes tabPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .tab span {
            position: relative;
            z-index: 1;
        }

        .tab:hover:not(.active) {
            color: #e2e8f0;
            transform: translateY(-2px);
            background: rgba(74, 222, 128, 0.1);
        }

        .tab-content {
            display: none;
            animation: fadeInUp 0.7s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeInUp {
            from { 
                opacity: 0; 
                transform: translateY(30px) scale(0.95); 
            }
            to { 
                opacity: 1; 
                transform: translateY(0) scale(1); 
            }
        }

        .timer-section {
            background: linear-gradient(135deg, rgba(15, 23, 42, 0.9), rgba(30, 41, 59, 0.8));
            border-radius: 30px;
            padding: 45px;
            margin-bottom: 40px;
            border: 2px solid rgba(74, 222, 128, 0.3);
            animation: timerPulse 4s ease-in-out infinite;
            position: relative;
            overflow: hidden;
        }

        .timer-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(74, 222, 128, 0.2), transparent);
            animation: shine 4s infinite;
        }

        @keyframes shine {
            0% { left: -100%; }
            100% { left: 100%; }
        }

        @keyframes timerPulse {
            0%, 100% { 
                transform: scale(1); 
                box-shadow: 0 0 30px rgba(74, 222, 128, 0.3);
                border-color: rgba(74, 222, 128, 0.3);
            }
            50% { 
                transform: scale(1.02); 
                box-shadow: 0 0 50px rgba(74, 222, 128, 0.5);
                border-color: rgba(74, 222, 128, 0.5);
            }
        }

        .timer-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 20px;
        }

        .timer-box {
            background: rgba(15, 23, 42, 0.8);
            border-radius: 20px;
            padding: 25px;
            border: 2px solid rgba(74, 222, 128, 0.2);
        }

        .timer-label {
            color: #e2e8f0;
            font-size: 1.2rem;
            margin-bottom: 15px;
            font-weight: 700;
            animation: labelGlow 3s ease-in-out infinite alternate;
        }

        @keyframes labelGlow {
            from { text-shadow: 0 0 10px rgba(226, 232, 240, 0.5); }
            to { text-shadow: 0 0 20px rgba(226, 232, 240, 0.8); }
        }

        .timer-display {
            font-size: 2.5rem;
            font-weight: 900;
            background: linear-gradient(135deg, #4ade80, #22c55e, #16a34a);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-family: 'Courier New', monospace;
            animation: timerGlow 2s ease-in-out infinite alternate;
            filter: drop-shadow(0 0 25px rgba(74, 222, 128, 0.7));
            margin: 15px 0;
        }

        .countdown-display {
            font-size: 2.2rem;
            font-weight: 900;
            background: linear-gradient(135deg, #ef4444, #dc2626, #b91c1c);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-family: 'Courier New', monospace;
            animation: countdownGlow 2s ease-in-out infinite alternate;
            filter: drop-shadow(0 0 25px rgba(239, 68, 68, 0.7));
            margin: 15px 0;
        }

        @keyframes timerGlow {
            from { 
                filter: drop-shadow(0 0 25px rgba(74, 222, 128, 0.7));
                transform: scale(1);
            }
            to { 
                filter: drop-shadow(0 0 40px rgba(74, 222, 128, 1));
                transform: scale(1.05);
            }
        }

        @keyframes countdownGlow {
            from { 
                filter: drop-shadow(0 0 25px rgba(239, 68, 68, 0.7));
                transform: scale(1);
            }
            to { 
                filter: drop-shadow(0 0 40px rgba(239, 68, 68, 1));
                transform: scale(1.05);
            }
        }

        .validity-info {
            color: #fbbf24;
            font-size: 1rem;
            margin-top: 15px;
            font-weight: 600;
            animation: validityPulse 3s ease-in-out infinite;
        }

        @keyframes validityPulse {
            0%, 100% { text-shadow: 0 0 10px rgba(251, 191, 36, 0.5); }
            50% { text-shadow: 0 0 20px rgba(251, 191, 36, 0.8); }
        }

        .timezone-info {
            color: #94a3b8;
            font-size: 1rem;
            margin-top: 20px;
            font-style: italic;
            animation: infoFade 4s ease-in-out infinite alternate;
            grid-column: 1 / -1;
            text-align: center;
        }

        @keyframes infoFade {
            from { opacity: 0.7; }
            to { opacity: 1; }
        }

        .script-section {
            background: linear-gradient(135deg, rgba(15, 23, 42, 0.9), rgba(30, 41, 59, 0.8));
            border-radius: 30px;
            padding: 40px;
            margin-bottom: 30px;
            border: 2px solid rgba(59, 130, 246, 0.3);
            animation: sectionFloat 8s ease-in-out infinite;
        }

        @keyframes sectionFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
        }

        .script-title {
            color: #e2e8f0;
            font-size: 1.6rem;
            font-weight: 800;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            animation: titleShimmer 3s ease-in-out infinite;
        }

        @keyframes titleShimmer {
            0%, 100% { text-shadow: 0 0 10px rgba(226, 232, 240, 0.5); }
            50% { text-shadow: 0 0 20px rgba(226, 232, 240, 0.8); }
        }

        .code-block {
            background: rgba(15, 23, 42, 0.95);
            border: 2px solid rgba(74, 222, 128, 0.3);
            border-radius: 20px;
            padding: 30px;
            margin: 25px 0;
            font-family: 'Courier New', monospace;
            font-size: 1rem;
            color: #4ade80;
            word-break: break-all;
            position: relative;
            overflow: hidden;
            animation: codeBlockPulse 5s ease-in-out infinite;
        }

        @keyframes codeBlockPulse {
            0%, 100% { box-shadow: 0 0 20px rgba(74, 222, 128, 0.3); }
            50% { box-shadow: 0 0 40px rgba(74, 222, 128, 0.5); }
        }

        .code-block::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, #4ade80, #3b82f6, #8b5cf6, #ec4899);
            animation: codeGlow 3s linear infinite;
        }

        @keyframes codeGlow {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        .copy-btn {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(74, 222, 128, 0.2);
            border: 2px solid rgba(74, 222, 128, 0.4);
            border-radius: 12px;
            padding: 12px 18px;
            color: #4ade80;
            font-size: 0.9rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            animation: copyBtnFloat 4s ease-in-out infinite;
        }

        @keyframes copyBtnFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-3px); }
        }

        .copy-btn:hover {
            background: rgba(74, 222, 128, 0.4);
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 5px 15px rgba(74, 222, 128, 0.4);
        }

        .supported-games {
            text-align: left;
            margin-top: 30px;
        }

        .supported-games h4 {
            color: #e2e8f0;
            margin-bottom: 20px;
            font-size: 1.3rem;
            font-weight: 700;
            text-align: center;
        }

        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
        }

        .game-tag {
            background: linear-gradient(135deg, rgba(74, 222, 128, 0.15), rgba(59, 130, 246, 0.15));
            border: 2px solid rgba(74, 222, 128, 0.3);
            border-radius: 15px;
            padding: 12px 16px;
            color: #4ade80;
            font-size: 0.95rem;
            font-weight: 600;
            text-align: center;
            animation: gameTagFloat 4s ease-in-out infinite;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .game-tag:hover {
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 10px 25px rgba(74, 222, 128, 0.3);
            border-color: rgba(74, 222, 128, 0.5);
        }

        .game-tag:nth-child(odd) {
            animation-delay: 0.5s;
        }

        .game-tag:nth-child(even) {
            animation-delay: 1s;
        }

        .game-tag:nth-child(3n) {
            animation-delay: 1.5s;
        }

        @keyframes gameTagFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-8px); }
        }

        .btn {
            padding: 22px 40px;
            border: none;
            border-radius: 20px;
            font-size: 1.2rem;
            font-weight: 800;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            text-decoration: none;
            display: inline-block;
            position: relative;
            overflow: hidden;
            text-transform: uppercase;
            letter-spacing: 2px;
            animation: btnFloat 6s ease-in-out infinite;
        }

        @keyframes btnFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-3px); }
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            transition: left 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .btn:hover::before {
            left: 100%;
        }

        .btn:hover {
            transform: translateY(-8px) scale(1.08);
        }

        .discord-btn {
            background: linear-gradient(135deg, #5865f2, #4f46e5, #4338ca);
            color: white;
            box-shadow: 
                0 15px 35px rgba(88, 101, 242, 0.5),
                0 0 0 2px rgba(88, 101, 242, 0.3);
            margin-bottom: 35px;
            animation: discordPulse 3s ease-in-out infinite;
        }

        @keyframes discordPulse {
            0%, 100% { box-shadow: 0 15px 35px rgba(88, 101, 242, 0.5), 0 0 0 2px rgba(88, 101, 242, 0.3); }
            50% { box-shadow: 0 20px 45px rgba(88, 101, 242, 0.7), 0 0 0 3px rgba(88, 101, 242, 0.5); }
        }

        .discord-btn:hover {
            box-shadow: 
                0 25px 50px rgba(88, 101, 242, 0.8),
                0 0 0 3px rgba(88, 101, 242, 0.5);
        }

        .key-methods {
            display: flex;
            gap: 20px;
            margin-top: 35px;
        }

        .method-btn {
            flex: 1;
            padding: 20px 25px;
            font-size: 1.1rem;
        }

        .linkvertise-btn {
            background: linear-gradient(135deg, #ef4444, #dc2626, #b91c1c);
            color: white;
            box-shadow: 
                0 15px 35px rgba(239, 68, 68, 0.5),
                0 0 0 2px rgba(239, 68, 68, 0.3);
            animation: linkvertisePulse 4s ease-in-out infinite;
        }

        @keyframes linkvertisePulse {
            0%, 100% { box-shadow: 0 15px 35px rgba(239, 68, 68, 0.5), 0 0 0 2px rgba(239, 68, 68, 0.3); }
            50% { box-shadow: 0 20px 45px rgba(239, 68, 68, 0.7), 0 0 0 3px rgba(239, 68, 68, 0.5); }
        }

        .linkvertise-btn:hover {
            box-shadow: 
                0 25px 50px rgba(239, 68, 68, 0.8),
                0 0 0 3px rgba(239, 68, 68, 0.5);
        }

        .section-title {
            color: #e2e8f0;
            font-size: 1.8rem;
            margin: 40px 0 25px 0;
            font-weight: 800;
            animation: sectionTitleGlow 3s ease-in-out infinite alternate;
        }

        @keyframes sectionTitleGlow {
            from { text-shadow: 0 0 15px rgba(226, 232, 240, 0.5); }
            to { text-shadow: 0 0 30px rgba(226, 232, 240, 0.8); }
        }

        .info-link {
            color: #3b82f6;
            text-decoration: none;
            font-weight: 700;
            transition: all 0.3s ease;
            animation: linkPulse 5s ease-in-out infinite;
        }

        @keyframes linkPulse {
            0%, 100% { text-shadow: 0 0 5px rgba(59, 130, 246, 0.5); }
            50% { text-shadow: 0 0 15px rgba(59, 130, 246, 0.8); }
        }

        .info-link:hover {
            color: #60a5fa;
            text-shadow: 0 0 20px rgba(96, 165, 250, 0.8);
        }

        .warning-box {
            margin-top: 30px; 
            padding: 25px; 
            background: rgba(239, 68, 68, 0.15); 
            border: 2px solid rgba(239, 68, 68, 0.3); 
            border-radius: 20px;
            animation: warningPulse 4s ease-in-out infinite;
        }

        @keyframes warningPulse {
            0%, 100% { 
                box-shadow: 0 0 20px rgba(239, 68, 68, 0.3);
                border-color: rgba(239, 68, 68, 0.3);
            }
            50% { 
                box-shadow: 0 0 35px rgba(239, 68, 68, 0.5);
                border-color: rgba(239, 68, 68, 0.5);
            }
        }

        .warning-text {
            color: #fca5a5; 
            font-size: 1.05rem; 
            margin-bottom: 15px;
            font-weight: 600;
        }

        /* Mobile Optimizations */
        @media (max-width: 768px) {
            .container {
                padding: 30px;
                margin: 10px;
                min-height: 95vh;
                border-radius: 25px;
            }
            
            .title {
                font-size: 3.5rem;
                margin-bottom: 30px;
            }
            
            .timer-grid {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .timer-display, .countdown-display {
                font-size: 2rem;
            }
            
            .timer-section {
                padding: 30px;
                margin-bottom: 25px;
            }
            
            .script-section {
                padding: 25px;
            }
            
            .key-methods {
                flex-direction: column;
                gap: 15px;
            }

            .tabs {
                flex-direction: column;
                gap: 5px;
            }

            .tab {
                padding: 15px 20px;
                font-size: 1rem;
            }

            .games-grid {
                grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
                gap: 10px;
            }

            .btn {
                padding: 18px 30px;
                font-size: 1rem;
            }

            .code-block {
                padding: 20px;
                font-size: 0.9rem;
            }

            .copy-btn {
                position: relative;
                top: auto;
                right: auto;
                margin-top: 15px;
                display: block;
                width: 100%;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 20px;
                margin: 5px;
            }
            
            .title {
                font-size: 2.8rem;
            }
            
            .timer-display, .countdown-display {
                font-size: 1.6rem;
            }
            
            .timer-section, .script-section {
                padding: 20px;
            }
            
            .btn {
                padding: 15px 25px;
                font-size: 0.95rem;
                letter-spacing: 1px;
            }
            
            .games-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="particles"></div>
    
    <div class="container">
        <h1 class="title">FoggyHub</h1>
        
        <div class="tabs">
            <button class="tab active" data-tab="key-system">
                <span>🔑 Key System</span>
            </button>
            <button class="tab" data-tab="main-script">
                <span>📜 Main Script</span>
            </button>
        </div>

        <div class="tab-content active" id="key-system">
            <div class="timer-section">
                <div class="timer-grid">
                    <div class="timer-box">
                        <div class="timer-label">⏰ Current Time</div>
                        <div class="timer-display" id="current-timer">Loading...</div>
                    </div>
                    <div class="timer-box">
                        <div class="timer-label">🔑 Key Valid Until</div>
                        <div class="countdown-display" id="countdown-timer">Loading...</div>
                        <div class="validity-info" id="validity-info">Calculating...</div>
                    </div>
                    <div class="timezone-info">🌍 Script Developer Timezone (GMT+3)</div>
                </div>
            </div>
            
            <a href="https://discord.gg/aSSsMuBbu7" target="_blank" class="btn discord-btn">
                🔗 Join Discord Server
            </a>
            
            <div class="section-title">Get Your Key</div>
            <div class="key-methods">
                <a href="https://link-hub.net/1091169/imIkteK0Kk7p" target="_blank" class="btn method-btn linkvertise-btn">
                    Linkvertise
                </a>
            </div>
        </div>

        <div class="tab-content" id="main-script">
            <div class="script-section">
                <div class="script-title">
                    🚀 Main Script Loader
                </div>
                
                <div class="code-block">
                    <button class="copy-btn" onclick="copyScript()">📋 Copy</button>
                    <code id="script-code">loadstring(game:HttpGet("https://raw.githubusercontent.com/FOGOTY/foggy-loader/refs/heads/main/loader"))()</code>
                </div>

                <div class="supported-games">
                    <h4>🎮 Games Supported:</h4>
                    <div class="games-grid">
                        <div class="game-tag">MM2</div>
                        <div class="game-tag">Built A Boat</div>
                        <div class="game-tag">Arsenal</div>
                        <div class="game-tag">Tower Of Hell</div>
                        <div class="game-tag">Legends Of Speed</div>
                        <div class="game-tag">Elementary Power Tycoon</div>
                        <div class="game-tag">Fisch</div>
                        <div class="game-tag">Obby On a Bike</div>
                        <div class="game-tag">Broken Bones 4</div>
                        <div class="game-tag">Blox Fruits</div>
                        <div class="game-tag">Blade Ball</div>
                        <div class="game-tag">Rivals</div>
                        <div class="game-tag">Dead Rails</div>
                        <div class="game-tag">Slap Battles</div>
                        <div class="game-tag">Brookhaven</div>
                        <div class="game-tag">99 Nights In The Forest</div>
                        <div class="game-tag">Grow A Garden</div>
                        <div class="game-tag">Steal A Brainrot</div>
                    </div>
                </div>

                <div class="warning-box">
                    <p class="warning-text">
                        ⚠️ If your executor is not supported, check this:
                    </p>
                    <a href="https://raw.githubusercontent.com/FOGOTY/foggyhubdata/refs/heads/main/data" target="_blank" class="info-link">
                        https://raw.githubusercontent.com/FOGOTY/foggyhubdata/refs/heads/main/data
                    </a>
                </div>
            </div>
        </div>
    </div>

    <script>
        function createParticles() {
            const particles = document.querySelector('.particles');
            
            for (let i = 0; i < 120; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                
                const size = Math.random() * 10 + 4;
                const left = Math.random() * 100;
                const delay = Math.random() * 25;
                
                particle.style.width = size + 'px';
                particle.style.height = size + 'px';
                particle.style.left = left + '%';
                particle.style.animationDelay = -delay + 's';
                particle.style.animationDuration = (20 + Math.random() * 15) + 's';
                
                particles.appendChild(particle);
            }
        }

        function updateTimers() {
            const now = new Date();
            const utc = now.getTime() + (now.getTimezoneOffset() * 60000);
            const gmt3Time = new Date(utc + (3 * 3600000));
            
            // Current time display
            const hours = gmt3Time.getHours().toString().padStart(2, '0');
            const minutes = gmt3Time.getMinutes().toString().padStart(2, '0');
            const seconds = gmt3Time.getSeconds().toString().padStart(2, '0');
            
            const currentTimerDisplay = document.getElementById('current-timer');
            currentTimerDisplay.textContent = `${hours}:${minutes}:${seconds}`;
            
            // Key validity countdown
            const currentHour = gmt3Time.getHours();
            const currentMinute = gmt3Time.getMinutes();
            const currentSecond = gmt3Time.getSeconds();
            
            let targetHour, nextValidityTime;
            
            // Determine next validity time (9:00 or 21:00)
            if (currentHour < 9 || (currentHour === 9 && currentMinute === 0 && currentSecond === 0)) {
                targetHour = 9;
                nextValidityTime = new Date(gmt3Time);
                nextValidityTime.setHours(9, 0, 0, 0);
            } else if (currentHour < 21 || (currentHour === 21 && currentMinute === 0 && currentSecond === 0)) {
                targetHour = 21;
                nextValidityTime = new Date(gmt3Time);
                nextValidityTime.setHours(21, 0, 0, 0);
            } else {
                // After 21:00, next validity is 9:00 tomorrow
                targetHour = 9;
                nextValidityTime = new Date(gmt3Time);
                nextValidityTime.setDate(nextValidityTime.getDate() + 1);
                nextValidityTime.setHours(9, 0, 0, 0);
            }
            
            // Calculate time remaining
            const timeRemaining = nextValidityTime.getTime() - gmt3Time.getTime();
            
            if (timeRemaining > 0) {
                const hoursLeft = Math.floor(timeRemaining / (1000 * 60 * 60));
                const minutesLeft = Math.floor((timeRemaining % (1000 * 60 * 60)) / (1000 * 60));
                const secondsLeft = Math.floor((timeRemaining % (1000 * 60)) / 1000);
                
                const countdownDisplay = document.getElementById('countdown-timer');
                countdownDisplay.textContent = `${hoursLeft.toString().padStart(2, '0')}:${minutesLeft.toString().padStart(2, '0')}:${secondsLeft.toString().padStart(2, '0')}`;
                
                const validityInfo = document.getElementById('validity-info');
                const nextTimeStr = targetHour === 9 ? '09:00' : '21:00';
                const dayText = targetHour === 9 && currentHour >= 21 ? ' (Tomorrow)' : '';
                validityInfo.textContent = `⏳ Until ${nextTimeStr} GMT+3${dayText}`;
            } else {
                // Exactly at validity time
                const countdownDisplay = document.getElementById('countdown-timer');
                countdownDisplay.textContent = '00:00:00';
                
                const validityInfo = document.getElementById('validity-info');
                validityInfo.textContent = '✅ Key Valid Now!';
            }
        }

        function initTabs() {
            const tabs = document.querySelectorAll('.tab');
            const contents = document.querySelectorAll('.tab-content');
            
            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    const targetTab = tab.dataset.tab;
                    
                    tabs.forEach(t => t.classList.remove('active'));
                    contents.forEach(c => c.classList.remove('active'));
                    
                    tab.classList.add('active');
                    document.getElementById(targetTab).classList.add('active');
                    
                    tab.style.transform = 'translateY(-3px) scale(0.95)';
                    setTimeout(() => {
                        tab.style.transform = '';
                    }, 150);
                });
            });
        }

        function copyScript() {
            const scriptText = document.getElementById('script-code').textContent;
            navigator.clipboard.writeText(scriptText).then(() => {
                const copyBtn = document.querySelector('.copy-btn');
                const originalText = copyBtn.textContent;
                copyBtn.textContent = '✅ Copied!';
                copyBtn.style.background = 'rgba(74, 222, 128, 0.4)';
                copyBtn.style.transform = 'scale(1.1)';
                
                setTimeout(() => {
                    copyBtn.textContent = originalText;
                    copyBtn.style.background = 'rgba(74, 222, 128, 0.2)';
                    copyBtn.style.transform = '';
                }, 2500);
            }).catch(() => {
                const copyBtn = document.querySelector('.copy-btn');
                const originalText = copyBtn.textContent;
                copyBtn.textContent = '❌ Failed';
                copyBtn.style.background = 'rgba(239, 68, 68, 0.3)';
                
                setTimeout(() => {
                    copyBtn.textContent = originalText;
                    copyBtn.style.background = 'rgba(74, 222, 128, 0.2)';
                }, 2500);
            });
        }

        function initRippleEffect() {
            document.querySelectorAll('.btn').forEach(btn => {
                btn.addEventListener('click', function(e) {
                    const ripple = document.createElement('span');
                    const rect = this.getBoundingClientRect();
                    const size = Math.max(rect.width, rect.height);
                    const x = e.clientX - rect.left - size / 2;
                    const y = e.clientY - rect.top - size / 2;
                    
                    ripple.style.cssText = `
                        position: absolute;
                        border-radius: 50%;
                        background: rgba(255, 255, 255, 0.6);
                        transform: scale(0);
                        animation: ripple 0.8s linear;
                        width: ${size}px;
                        height: ${size}px;
                        left: ${x}px;
                        top: ${y}px;
                        pointer-events: none;
                        z-index: 0;
                    `;
                    
                    this.appendChild(ripple);
                    
                    setTimeout(() => {
                        ripple.remove();
                    }, 800);
                });
            });
        }

        function initHoverEffects() {
            document.querySelectorAll('.game-tag').forEach(tag => {
                tag.addEventListener('mouseenter', function() {
                    this.style.background = 'linear-gradient(135deg, rgba(74, 222, 128, 0.25), rgba(59, 130, 246, 0.25))';
                    this.style.borderColor = 'rgba(74, 222, 128, 0.6)';
                });
                
                tag.addEventListener('mouseleave', function() {
                    this.style.background = '';
                    this.style.borderColor = '';
                });
            });
        }

        function initScrollAnimations() {
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.style.opacity = '1';
                        entry.target.style.transform = 'translateY(0)';
                    }
                });
            }, { threshold: 0.1 });

            document.querySelectorAll('.script-section, .timer-section').forEach(el => {
                el.style.opacity = '0';
                el.style.transform = 'translateY(30px)';
                el.style.transition = 'all 0.6s ease';
                observer.observe(el);
            });
        }

        const style = document.createElement('style');
        style.textContent = `
            @keyframes ripple {
                to {
                    transform: scale(4);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);

        document.addEventListener('DOMContentLoaded', () => {
            createParticles();
            initTabs();
            initRippleEffect();
            initHoverEffects();
            initScrollAnimations();
            updateTimers();
            setInterval(updateTimers, 1000);
        });

        if ('ontouchstart' in window) {
            document.querySelectorAll('.btn, .tab, .game-tag').forEach(el => {
                el.addEventListener('touchstart', function() {
                    this.style.transform = 'scale(0.95)';
                });
                
                el.addEventListener('touchend', function() {
                    setTimeout(() => {
                        this.style.transform = '';
                    }, 150);
                });
            });
        }
    </script>
    
    <script>
        document.addEventListener('contextmenu', event => event.preventDefault());
    </script>
    
    <script>
        let devToolsOpen = false;
        const threshold = 160;
        setInterval(() => {
            if (window.outerWidth - window.innerWidth > threshold || 
                window.outerHeight - window.innerHeight > threshold) {
                if (!devToolsOpen) {
                    devToolsOpen = true;
                    alert('Developer tools detected! Please close them.');
                }
            } else {
                devToolsOpen = false;
            }
        }, 1000);

        document.addEventListener('keydown', (e) => {
            if (e.key === 'F12' || 
                (e.ctrlKey && e.shiftKey && ['I', 'C', 'J'].includes(e.key)) ||
                (e.ctrlKey && e.key === 'U')) {
                e.preventDefault();
                alert('Access to developer tools is restricted.');
            }
        });
    </script>
</body>
</html>
