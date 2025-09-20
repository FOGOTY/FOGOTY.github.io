
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
            font-family: 'Inter', 'Segoe UI', system-ui, sans-serif;
            background: #0d1117;
            background-image: 
                radial-gradient(circle at 20% 80%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
                radial-gradient(circle at 80% 20%, rgba(255, 128, 0, 0.15) 0%, transparent 50%),
                radial-gradient(circle at 40% 40%, rgba(120, 119, 198, 0.2) 0%, transparent 50%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow-x: hidden;
            padding: 20px;
            color: #e6edf3;
        }

        .noise::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.02;
            background: 
                repeating-conic-gradient(from 0deg at 50% 50%, transparent 0deg, #fff 0.1deg, transparent 0.2deg);
            pointer-events: none;
            z-index: 1;
        }

        .floating-shapes {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: 0;
            pointer-events: none;
        }

        .shape {
            position: absolute;
            border-radius: 50%;
            background: linear-gradient(135deg, rgba(120, 119, 198, 0.1), rgba(255, 128, 0, 0.05));
            animation: float 20s infinite linear;
        }

        .shape:nth-child(2n) {
            background: linear-gradient(135deg, rgba(255, 128, 0, 0.08), rgba(120, 119, 198, 0.05));
            animation-duration: 25s;
        }

        .shape:nth-child(3n) {
            background: linear-gradient(135deg, rgba(88, 166, 255, 0.06), transparent);
            animation-duration: 30s;
        }

        @keyframes float {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
        }

        .container {
            background: rgba(13, 17, 23, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 16px;
            border: 1px solid rgba(48, 54, 61, 0.8);
            padding: 40px;
            box-shadow: 
                0 16px 70px rgba(0, 0, 0, 0.6),
                inset 0 1px 0 rgba(255, 255, 255, 0.05);
            max-width: 1000px;
            width: 100%;
            text-align: center;
            position: relative;
            z-index: 2;
        }

        .title {
            font-size: 3.5rem;
            font-weight: 800;
            background: linear-gradient(135deg, #58a6ff 0%, #7877c6 50%, #ff8000 100%);
            background-size: 200% 200%;
            animation: gradientShift 3s ease infinite;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 40px;
            letter-spacing: -0.02em;
        }

        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .tabs {
            display: flex;
            margin-bottom: 32px;
            background: rgba(33, 38, 45, 0.8);
            border-radius: 12px;
            padding: 6px;
            gap: 6px;
            border: 1px solid rgba(48, 54, 61, 0.5);
        }

        .tab {
            flex: 1;
            padding: 14px 24px;
            background: transparent;
            border: none;
            border-radius: 8px;
            color: #7d8590;
            font-weight: 600;
            font-size: 0.95rem;
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
        }

        .tab.active {
            background: linear-gradient(135deg, rgba(88, 166, 255, 0.15), rgba(120, 119, 198, 0.15));
            color: #e6edf3;
            border: 1px solid rgba(88, 166, 255, 0.3);
        }

        .tab:hover:not(.active) {
            color: #e6edf3;
            background: rgba(48, 54, 61, 0.5);
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .timer-section {
            background: rgba(33, 38, 45, 0.6);
            border-radius: 12px;
            padding: 32px;
            margin-bottom: 32px;
            border: 1px solid rgba(48, 54, 61, 0.5);
        }

        .timer-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 24px;
            margin-bottom: 16px;
        }

        .timer-box {
            background: rgba(21, 26, 32, 0.8);
            border-radius: 10px;
            padding: 20px;
            border: 1px solid rgba(48, 54, 61, 0.4);
        }

        .timer-label {
            color: #7d8590;
            font-size: 0.9rem;
            margin-bottom: 12px;
            font-weight: 600;
        }

        .timer-display {
            font-size: 2rem;
            font-weight: 700;
            color: #58a6ff;
            font-family: 'SF Mono', 'Monaco', 'Inconsolata', monospace;
            margin: 10px 0;
        }

        .countdown-display {
            font-size: 2rem;
            font-weight: 700;
            color: #ff7b72;
            font-family: 'SF Mono', 'Monaco', 'Inconsolata', monospace;
            margin: 10px 0;
        }

        .validity-info {
            color: #f0883e;
            font-size: 0.85rem;
            margin-top: 12px;
            font-weight: 500;
        }

        .timezone-info {
            color: #7d8590;
            font-size: 0.85rem;
            margin-top: 16px;
            grid-column: 1 / -1;
            text-align: center;
            font-style: italic;
        }

        .discord-btn {
            background: linear-gradient(135deg, #5865f2 0%, #4752c4 100%);
            border: none;
            border-radius: 10px;
            padding: 16px 32px;
            color: white;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            transition: all 0.2s ease;
            margin-bottom: 32px;
            box-shadow: 0 4px 12px rgba(88, 101, 242, 0.3);
        }

        .discord-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(88, 101, 242, 0.4);
        }

        .section-title {
            color: #e6edf3;
            font-size: 1.4rem;
            margin: 32px 0 20px 0;
            font-weight: 700;
        }

        .key-methods {
            display: flex;
            gap: 16px;
            margin-top: 24px;
        }

        .method-btn {
            flex: 1;
            padding: 16px 24px;
            font-size: 1rem;
            background: linear-gradient(135deg, #da3633 0%, #c5282a 100%);
            border: none;
            border-radius: 10px;
            color: white;
            font-weight: 600;
            cursor: pointer;
            text-decoration: none;
            display: inline-block;
            transition: all 0.2s ease;
            box-shadow: 0 4px 12px rgba(218, 54, 51, 0.3);
        }

        .method-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(218, 54, 51, 0.4);
        }

        .script-section {
            background: rgba(33, 38, 45, 0.6);
            border-radius: 12px;
            padding: 32px;
            margin-bottom: 24px;
            border: 1px solid rgba(48, 54, 61, 0.5);
        }

        .script-title {
            color: #e6edf3;
            font-size: 1.3rem;
            font-weight: 700;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .code-block {
            background: rgba(21, 26, 32, 0.9);
            border: 1px solid rgba(48, 54, 61, 0.6);
            border-radius: 8px;
            padding: 20px;
            margin: 20px 0;
            font-family: 'SF Mono', 'Monaco', 'Inconsolata', monospace;
            font-size: 0.9rem;
            color: #58a6ff;
            word-break: break-all;
            position: relative;
        }

        .copy-btn {
            position: absolute;
            top: 12px;
            right: 12px;
            background: rgba(88, 166, 255, 0.15);
            border: 1px solid rgba(88, 166, 255, 0.3);
            border-radius: 6px;
            padding: 8px 12px;
            color: #58a6ff;
            font-size: 0.8rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .copy-btn:hover {
            background: rgba(88, 166, 255, 0.25);
            border-color: rgba(88, 166, 255, 0.5);
        }

        .supported-games {
            text-align: left;
            margin-top: 24px;
        }

        .supported-games h4 {
            color: #e6edf3;
            margin-bottom: 16px;
            font-size: 1.1rem;
            font-weight: 600;
            text-align: center;
        }

        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 12px;
        }

        .game-tag {
            background: rgba(33, 38, 45, 0.8);
            border: 1px solid rgba(48, 54, 61, 0.6);
            border-radius: 8px;
            padding: 10px 14px;
            color: #7d8590;
            font-size: 0.85rem;
            font-weight: 500;
            text-align: center;
            transition: all 0.2s ease;
            cursor: pointer;
        }

        .game-tag:hover {
            background: rgba(48, 54, 61, 0.8);
            border-color: rgba(88, 166, 255, 0.3);
            color: #e6edf3;
            transform: translateY(-2px);
        }

        .warning-box {
            margin-top: 24px;
            padding: 20px;
            background: rgba(218, 54, 51, 0.1);
            border: 1px solid rgba(218, 54, 51, 0.3);
            border-radius: 8px;
        }

        .warning-text {
            color: #ff7b72;
            font-size: 0.9rem;
            margin-bottom: 12px;
            font-weight: 500;
        }

        .info-link {
            color: #58a6ff;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.2s ease;
        }

        .info-link:hover {
            color: #79c0ff;
        }

        @media (max-width: 768px) {
            .container {
                padding: 24px;
                margin: 10px;
            }
            
            .title {
                font-size: 2.5rem;
                margin-bottom: 24px;
            }
            
            .timer-grid {
                grid-template-columns: 1fr;
                gap: 16px;
            }
            
            .timer-display, .countdown-display {
                font-size: 1.6rem;
            }
            
            .timer-section, .script-section {
                padding: 20px;
            }
            
            .key-methods {
                flex-direction: column;
                gap: 12px;
            }

            .tabs {
                flex-direction: column;
                gap: 4px;
            }

            .tab {
                padding: 12px 16px;
                font-size: 0.9rem;
            }

            .games-grid {
                grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
                gap: 8px;
            }

            .copy-btn {
                position: relative;
                top: auto;
                right: auto;
                margin-top: 12px;
                display: block;
                width: 100%;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 16px;
                margin: 5px;
            }
            
            .title {
                font-size: 2rem;
            }
            
            .timer-display, .countdown-display {
                font-size: 1.4rem;
            }
            
            .timer-section, .script-section {
                padding: 16px;
            }
            
            .games-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body class="noise">
    <div class="floating-shapes"></div>
    
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
            
            <a href="https://discord.gg/aSSsMuBbu7" target="_blank" class="discord-btn">
                🔗 Join Discord Server
            </a>
            
            <div class="section-title">Get Your Key</div>
            <div class="key-methods">
                <a href="https://authguard.org/a/931" target="_blank" class="method-btn">
                    Get Key Here
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
                        <div class="game-tag">Muscle Legends</div>
                        <div class="game-tag">Restaurant Tycoon 3</div>
                    </div>
                </div>

                <div class="warning-box">
                    <p class="warning-text">
                        ⚠️ If it says game is not supported but it is in supported list, take script here:
                    </p>
                    <a href="https://raw.githubusercontent.com/FOGOTY/foggyhubdata/refs/heads/main/data" target="_blank" class="info-link">
                        https://raw.githubusercontent.com/FOGOTY/foggyhubdata/refs/heads/main/data
                    </a>
                </div>
            </div>
        </div>
    </div>

    <script>
        function createFloatingShapes() {
            const container = document.querySelector('.floating-shapes');
            
            for (let i = 0; i < 20; i++) {
                const shape = document.createElement('div');
                shape.className = 'shape';
                
                const size = Math.random() * 80 + 20;
                const left = Math.random() * 100;
                const delay = Math.random() * 20;
                
                shape.style.width = size + 'px';
                shape.style.height = size + 'px';
                shape.style.left = left + '%';
                shape.style.animationDelay = -delay + 's';
                shape.style.animationDuration = (15 + Math.random() * 15) + 's';
                
                container.appendChild(shape);
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
                });
            });
        }

        function copyScript() {
            const scriptText = document.getElementById('script-code').textContent;
            navigator.clipboard.writeText(scriptText).then(() => {
                const copyBtn = document.querySelector('.copy-btn');
                const originalText = copyBtn.textContent;
                copyBtn.textContent = '✅ Copied!';
                copyBtn.style.background = 'rgba(46, 160, 67, 0.25)';
                
                setTimeout(() => {
                    copyBtn.textContent = originalText;
                    copyBtn.style.background = '';
                }, 2000);
            }).catch(() => {
                const copyBtn = document.querySelector('.copy-btn');
                const originalText = copyBtn.textContent;
                copyBtn.textContent = '❌ Failed';
                copyBtn.style.background = 'rgba(218, 54, 51, 0.25)';
                
                setTimeout(() => {
                    copyBtn.textContent = originalText;
                    copyBtn.style.background = '';
                }, 2000);
            });
        }

        document.addEventListener('DOMContentLoaded', () => {
            createFloatingShapes();
            initTabs();
            updateTimers();
            setInterval(updateTimers, 1000);
        });

        // Keep the security features from original
        document.addEventListener('contextmenu', event => event.preventDefault());
        
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
