
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
            background: linear-gradient(135deg, #2c3e50 0%, #34495e 25%, #3d4f63 50%, #2c3e50 75%, #1a252f 100%);
            background-size: 400% 400%;
            animation: gradientShift 15s ease infinite;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow-x: hidden;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }


        .particles {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: 0;
        }

        .particle {
            position: absolute;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 50%;
            animation: float 20s infinite linear;
        }

        .particle:nth-child(odd) {
            background: rgba(74, 222, 128, 0.1);
        }

        .particle:nth-child(even) {
            background: rgba(59, 130, 246, 0.1);
        }

        @keyframes float {
            0% { transform: translateY(100vh) rotate(0deg) scale(0); opacity: 0; }
            10% { opacity: 1; transform: translateY(90vh) rotate(36deg) scale(1); }
            90% { opacity: 1; transform: translateY(-10vh) rotate(324deg) scale(1); }
            100% { transform: translateY(-100vh) rotate(360deg) scale(0); opacity: 0; }
        }

        .container {
            background: rgba(45, 55, 72, 0.95);
            backdrop-filter: blur(25px);
            border-radius: 25px;
            padding: 50px;
            box-shadow: 
                0 25px 50px rgba(0, 0, 0, 0.3),
                0 0 0 1px rgba(255, 255, 255, 0.1),
                inset 0 1px 0 rgba(255, 255, 255, 0.1);
            max-width: 900px;
            width: 95%;
            min-height: 80vh;
            text-align: center;
            position: relative;
            z-index: 1;
            animation: containerEntry 1.2s cubic-bezier(0.4, 0, 0.2, 1);
        }

        @keyframes containerEntry {
            0% { 
                transform: translateY(100px) scale(0.8); 
                opacity: 0;
                filter: blur(10px);
            }
            100% { 
                transform: translateY(0) scale(1); 
                opacity: 1;
                filter: blur(0);
            }
        }

        .title {
            font-size: 4rem;
            font-weight: 900;
            background: linear-gradient(135deg, #4ade80, #3b82f6, #8b5cf6);
            background-size: 200% 200%;
            animation: gradientText 3s ease infinite;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 40px;
            text-shadow: 0 0 30px rgba(74, 222, 128, 0.3);
            filter: drop-shadow(0 0 10px rgba(74, 222, 128, 0.2));
        }

        @keyframes gradientText {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .tabs {
            display: flex;
            margin-bottom: 30px;
            background: rgba(30, 41, 59, 0.8);
            border-radius: 15px;
            padding: 5px;
            gap: 5px;
        }

        .tab {
            flex: 1;
            padding: 15px 20px;
            background: transparent;
            border: none;
            border-radius: 10px;
            color: #94a3b8;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
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
            background: linear-gradient(135deg, #4ade80, #3b82f6);
            opacity: 0;
            transition: opacity 0.3s ease;
            border-radius: 10px;
        }

        .tab.active {
            color: white;
            transform: translateY(-2px);
        }

        .tab.active::before {
            opacity: 1;
        }

        .tab span {
            position: relative;
            z-index: 1;
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .timer-section {
            background: linear-gradient(135deg, rgba(30, 41, 59, 0.8), rgba(51, 65, 85, 0.6));
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            border: 1px solid rgba(148, 163, 184, 0.2);
            animation: pulse 4s ease-in-out infinite;
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
            background: linear-gradient(90deg, transparent, rgba(74, 222, 128, 0.1), transparent);
            animation: shine 3s infinite;
        }

        @keyframes shine {
            0% { left: -100%; }
            100% { left: 100%; }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); box-shadow: 0 0 20px rgba(74, 222, 128, 0.2); }
            50% { transform: scale(1.02); box-shadow: 0 0 30px rgba(74, 222, 128, 0.4); }
        }

        .timer-label {
            color: #e2e8f0;
            font-size: 1.2rem;
            margin-bottom: 15px;
            font-weight: 600;
        }

        .timer-display {
            font-size: 2.5rem;
            font-weight: 900;
            background: linear-gradient(135deg, #4ade80, #22c55e);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-family: 'Courier New', monospace;
            animation: timerGlow 2s ease-in-out infinite alternate;
            filter: drop-shadow(0 0 15px rgba(74, 222, 128, 0.5));
        }

        @keyframes timerGlow {
            from { filter: drop-shadow(0 0 15px rgba(74, 222, 128, 0.5)); }
            to { filter: drop-shadow(0 0 25px rgba(74, 222, 128, 0.8)); }
        }

        .timezone-info {
            color: #94a3b8;
            font-size: 0.9rem;
            margin-top: 15px;
            font-style: italic;
        }

        .script-section {
            background: linear-gradient(135deg, rgba(30, 41, 59, 0.8), rgba(51, 65, 85, 0.6));
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 25px;
            border: 1px solid rgba(148, 163, 184, 0.2);
        }

        .script-title {
            color: #e2e8f0;
            font-size: 1.3rem;
            font-weight: 700;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .code-block {
            background: rgba(15, 23, 42, 0.8);
            border: 1px solid rgba(148, 163, 184, 0.2);
            border-radius: 15px;
            padding: 20px;
            margin: 15px 0;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            color: #4ade80;
            word-break: break-all;
            position: relative;
            overflow: hidden;
        }

        .code-block::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 2px;
            background: linear-gradient(90deg, #4ade80, #3b82f6, #8b5cf6);
            animation: codeGlow 2s linear infinite;
        }

        @keyframes codeGlow {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        .copy-btn {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(74, 222, 128, 0.2);
            border: 1px solid rgba(74, 222, 128, 0.3);
            border-radius: 8px;
            padding: 8px 12px;
            color: #4ade80;
            font-size: 0.8rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .copy-btn:hover {
            background: rgba(74, 222, 128, 0.3);
            transform: translateY(-2px);
        }

        .supported-games {
            text-align: left;
            margin-top: 20px;
        }

        .supported-games h4 {
            color: #e2e8f0;
            margin-bottom: 15px;
            font-size: 1.1rem;
        }

        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
        }

        .game-tag {
            background: linear-gradient(135deg, rgba(74, 222, 128, 0.1), rgba(59, 130, 246, 0.1));
            border: 1px solid rgba(74, 222, 128, 0.2);
            border-radius: 10px;
            padding: 8px 12px;
            color: #4ade80;
            font-size: 0.85rem;
            text-align: center;
            animation: gameTagFloat 3s ease-in-out infinite;
        }

        .game-tag:nth-child(odd) {
            animation-delay: 0.5s;
        }

        .game-tag:nth-child(even) {
            animation-delay: 1s;
        }

        @keyframes gameTagFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
        }

        .btn {
            padding: 18px 30px;
            border: none;
            border-radius: 15px;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            text-decoration: none;
            display: inline-block;
            position: relative;
            overflow: hidden;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .btn:hover::before {
            left: 100%;
        }

        .btn:hover {
            transform: translateY(-5px) scale(1.05);
        }

        .discord-btn {
            background: linear-gradient(135deg, #5865f2, #4f46e5);
            color: white;
            box-shadow: 
                0 10px 25px rgba(88, 101, 242, 0.4),
                0 0 0 1px rgba(88, 101, 242, 0.2);
            margin-bottom: 25px;
        }

        .discord-btn:hover {
            box-shadow: 
                0 15px 35px rgba(88, 101, 242, 0.6),
                0 0 0 1px rgba(88, 101, 242, 0.3);
        }

        .key-methods {
            display: flex;
            gap: 15px;
            margin-top: 25px;
        }

        .method-btn {
            flex: 1;
            padding: 15px 20px;
            font-size: 1rem;
        }

        .linkvertise-btn {
            background: linear-gradient(135deg, #ef4444, #dc2626);
            color: white;
            box-shadow: 
                0 10px 25px rgba(239, 68, 68, 0.4),
                0 0 0 1px rgba(239, 68, 68, 0.2);
        }

        .linkvertise-btn:hover {
            box-shadow: 
                0 15px 35px rgba(239, 68, 68, 0.6),
                0 0 0 1px rgba(239, 68, 68, 0.3);
        }

        .workink-btn {
            background: linear-gradient(135deg, #06b6d4, #0891b2);
            color: white;
            box-shadow: 
                0 10px 25px rgba(6, 182, 212, 0.4),
                0 0 0 1px rgba(6, 182, 212, 0.2);
        }

        .workink-btn:hover {
            box-shadow: 
                0 15px 35px rgba(6, 182, 212, 0.6),
                0 0 0 1px rgba(6, 182, 212, 0.3);
        }

        .section-title {
            color: #e2e8f0;
            font-size: 1.4rem;
            margin: 30px 0 20px 0;
            font-weight: 700;
        }

        .info-link {
            color: #3b82f6;
            text-decoration: none;
            font-weight: 600;
            transition: color 0.3s ease;
        }

        .info-link:hover {
            color: #60a5fa;
        }

        @media (max-width: 480px) {
            .container {
                padding: 25px;
                margin: 20px;
            }
            
            .title {
                font-size: 2.2rem;
            }
            
            .timer-display {
                font-size: 2rem;
            }
            
            .key-methods {
                flex-direction: column;
            }

            .tabs {
                flex-direction: column;
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
                <div class="timer-label">⏰ Current key is valid</div>
                <div class="timer-display" id="timer">Loading...</div>
                <div class="timezone-info">🌍 Times are in GMT+3 timezone</div>
            </div>
            
            <a href="https://discord.gg/aSSsMuBbu7" target="_blank" class="btn discord-btn">
                🔗 Join Discord Server
            </a>
            
            <div class="section-title">Get Your Key</div>
            <div class="key-methods">
                <a href="https://link-center.net/1091169/vZ0nqAWy9tn2" target="_blank" class="btn method-btn linkvertise-btn">
                    Linkvertise
                </a>
                <a href="https://workink.net/20Fk/va4ajr2d" target="_blank" class="btn method-btn workink-btn">
                    Workink
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
                    </div>
                </div>

                <div style="margin-top: 25px; padding: 20px; background: rgba(239, 68, 68, 0.1); border: 1px solid rgba(239, 68, 68, 0.2); border-radius: 15px;">
                    <p style="color: #fca5a5; font-size: 0.95rem; margin-bottom: 10px;">
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
            
            for (let i = 0; i < 80; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                
                const size = Math.random() * 8 + 3;
                const left = Math.random() * 100;
                const delay = Math.random() * 20;
                
                particle.style.width = size + 'px';
                particle.style.height = size + 'px';
                particle.style.left = left + '%';
                particle.style.animationDelay = -delay + 's';
                particle.style.animationDuration = (15 + Math.random() * 10) + 's';
                
                particles.appendChild(particle);
            }
        }


        function updateTimer() {
            const now = new Date();
            const utc = now.getTime() + (now.getTimezoneOffset() * 60000);
            const gmt3Time = new Date(utc + (3 * 3600000));
            
            const currentHour = gmt3Time.getHours();
            
            let targetHour;
            if (currentHour < 9) {
                targetHour = 9;
            } else if (currentHour < 21) {
                targetHour = 21;
            } else {
                targetHour = 9 + 24;
            }
            
            const target = new Date(gmt3Time);
            if (targetHour >= 24) {
                target.setDate(target.getDate() + 1);
                target.setHours(targetHour - 24, 0, 0, 0);
            } else {
                target.setHours(targetHour, 0, 0, 0);
            }
            
            const diff = target - gmt3Time;
            
            if (diff <= 0) {
                updateTimer();
                return;
            }
            
            const hours = Math.floor(diff / (1000 * 60 * 60));
            const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((diff % (1000 * 60)) / 1000);
            
            const timerDisplay = document.getElementById('timer');
            timerDisplay.textContent = `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
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
                copyBtn.style.background = 'rgba(74, 222, 128, 0.3)';
                
                setTimeout(() => {
                    copyBtn.textContent = originalText;
                    copyBtn.style.background = 'rgba(74, 222, 128, 0.2)';
                }, 2000);
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
                        animation: ripple 0.6s linear;
                        width: ${size}px;
                        height: ${size}px;
                        left: ${x}px;
                        top: ${y}px;
                        pointer-events: none;
                    `;
                    
                    this.appendChild(ripple);
                    
                    setTimeout(() => {
                        ripple.remove();
                    }, 600);
                });
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


        createParticles();
        initTabs();
        initRippleEffect();
        updateTimer();
        setInterval(updateTimer, 1000);
    </script>
</body>
</html>
