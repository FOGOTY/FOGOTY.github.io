
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
            background: #1a1a1a;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow-x: hidden;
            padding: 20px;
            color: #ffffff;
        }

        .container {
            background: #2a2a2a;
            border-radius: 16px;
            border: 1px solid #3a3a3a;
            padding: 32px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            max-width: 1000px;
            width: 100%;
            text-align: center;
            position: relative;
            animation: containerEntry 0.6s ease-out;
        }

        @keyframes containerEntry {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .title {
            font-size: 2.8rem;
            font-weight: 900; /* Made bolder */
            margin-bottom: 32px;
            letter-spacing: -0.02em;
            background: linear-gradient(90deg, #ff0000, #ff8000, #ffff00, #80ff00, #00ff00, #00ffff, #0080ff, #0000ff, #8000ff, #ff00ff, #ff0080, #ff0000);
            background-size: 200% auto;
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: gradientShift 8s linear infinite;
        }

        @keyframes gradientShift {
            0% { background-position: 0% center; }
            100% { background-position: 200% center; }
        }

        .tabs {
            display: flex;
            margin-bottom: 24px;
            background: #1e1e1e;
            border-radius: 12px;
            padding: 4px;
            gap: 4px;
            border: 1px solid #3a3a3a;
        }

        .tab {
            flex: 1;
            padding: 12px 20px;
            background: #000000;
            border: none;
            border-radius: 10px;
            color: #ffffff;
            font-weight: 500;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }

        .tab.active {
            background: #ffffff;
            color: #000000;
            font-weight: 700;
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.7);
        }

        .tab:hover:not(.active) {
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.7);
            transform: translateY(-2px);
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

        .current-time-section {
            background: #1e1e1e;
            border-radius: 12px;
            padding: 24px;
            margin-bottom: 24px;
            border: 1px solid #3a3a3a;
        }

        .time-label {
            color: #9ca3af;
            font-size: 0.9rem;
            margin-bottom: 8px;
            font-weight: 500;
        }

        .time-display {
            font-size: 2rem;
            font-weight: 600;
            color: #ffffff;
            font-family: 'SF Mono', 'Monaco', 'Inconsolata', monospace;
            margin: 8px 0;
        }

        .timezone-info {
            color: #6b7280;
            font-size: 0.8rem;
            margin-top: 12px;
            font-style: italic;
        }

        .discord-btn {
            background: #000000;
            border: none;
            border-radius: 12px;
            padding: 16px 24px;
            color: white;
            font-size: 0.95rem;
            font-weight: 600;
            cursor: pointer;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s ease;
            margin-bottom: 24px;
        }

        .discord-btn:hover {
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.7);
            transform: translateY(-2px);
        }

        .section-title {
            color: #ffffff;
            font-size: 1.2rem;
            margin: 24px 0 16px 0;
            font-weight: 600;
        }

        .key-methods {
            display: flex;
            gap: 12px;
            margin-top: 16px;
        }

        .method-btn {
            flex: 1;
            padding: 14px 20px;
            font-size: 0.95rem;
            background: #000000;
            border: none;
            border-radius: 12px;
            color: white;
            font-weight: 600;
            cursor: pointer;
            text-decoration: none;
            display: inline-block;
            transition: all 0.3s ease;
        }

        .method-btn:hover {
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.7);
            transform: translateY(-2px);
        }

        .script-section {
            background: #1e1e1e;
            border-radius: 12px;
            padding: 24px;
            margin-bottom: 20px;
            border: 1px solid #3a3a3a;
        }

        .script-title {
            color: #ffffff;
            font-size: 1.2rem;
            font-weight: 600;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .code-block {
            background: #111111;
            border: 1px solid #3a3a3a;
            border-radius: 8px;
            padding: 16px;
            margin: 16px 0;
            font-family: 'SF Mono', 'Monaco', 'Inconsolata', monospace;
            font-size: 0.85rem;
            color: #e5e5e5;
            word-break: break-all;
            position: relative;
        }

        .copy-btn {
            background: #000000;
            border: 1px solid #ffffff;
            border-radius: 6px;
            padding: 6px 12px;
            color: #ffffff;
            font-size: 0.75rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .copy-btn:hover {
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.7);
            transform: translateY(-2px);
        }

        .supported-games {
            text-align: left;
            margin-top: 20px;
        }

        .supported-games h4 {
            color: #ffffff;
            margin-bottom: 16px;
            font-size: 1rem;
            font-weight: 600;
            text-align: center;
        }

        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 8px;
        }

        .game-tag {
            background: #000000;
            border: 1px solid #3a3a3a;
            border-radius: 8px;
            padding: 10px 14px;
            color: #ffffff;
            font-size: 0.8rem;
            font-weight: 500;
            text-align: center;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .game-tag:hover {
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.7);
            transform: translateY(-2px);
        }

        .warning-box {
            margin-top: 20px;
            padding: 16px;
            background: #2d1b1b;
            border: 1px solid #5b2c2c;
            border-radius: 8px;
        }

        .warning-text {
            color: #ef4444;
            font-size: 0.85rem;
            margin-bottom: 8px;
            font-weight: 500;
        }

        .info-link {
            color: #60a5fa;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.2s ease;
        }

        .info-link:hover {
            color: #93c5fd;
        }

        /* Toggle switches like in the images */
        .toggle-section {
            background: #1e1e1e;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 24px;
            border: 1px solid #3a3a3a;
        }

        .toggle-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid #3a3a3a;
        }

        .toggle-item:last-child {
            border-bottom: none;
        }

        .toggle-label {
            color: #ffffff;
            font-weight: 500;
            font-size: 0.9rem;
        }

        .toggle-switch {
            position: relative;
            width: 44px;
            height: 24px;
            background: #000000;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 1px solid #ffffff;
        }

        .toggle-switch::before {
            content: '';
            position: absolute;
            top: 2px;
            left: 2px;
            width: 20px;
            height: 20px;
            background: #ffffff;
            border-radius: 50%;
            transition: all 0.3s ease;
        }

        .toggle-switch.active {
            background: #ffffff;
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.7);
        }

        .toggle-switch.active::before {
            background: #000000;
            transform: translateX(20px);
        }

        .toggle-switch:hover {
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.7);
        }

        /* Executors section styles */
        .executors-section {
            background: #1e1e1e;
            border-radius: 12px;
            padding: 24px;
            margin-bottom: 20px;
            border: 1px solid #3a3a3a;
        }

        .executor-category {
            margin-bottom: 30px;
        }

        .executor-category:last-child {
            margin-bottom: 0;
        }

        .category-title {
            color: #ffffff;
            font-size: 1.1rem;
            margin-bottom: 16px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 8px;
            justify-content: center;
        }

        .executor-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 12px;
        }

        .executor-item {
            background: #000000;
            border: 1px solid #3a3a3a;
            border-radius: 10px;
            padding: 16px;
            display: flex;
            flex-direction: column;
            transition: all 0.3s ease;
        }

        .executor-item:hover {
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.3);
            transform: translateY(-3px);
        }

        .executor-name {
            color: #ffffff;
            font-weight: 600;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .executor-price {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 0.7rem;
            font-weight: 700;
            margin-left: auto;
        }

        .price-free {
            background: #16a34a;
            color: white;
        }

        .price-paid {
            background: #9333ea;
            color: white;
        }

        .executor-download {
            background: #000000;
            border: 1px solid #ffffff;
            border-radius: 8px;
            padding: 10px 16px;
            color: #ffffff;
            font-weight: 600;
            cursor: pointer;
            text-decoration: none;
            text-align: center;
            transition: all 0.3s ease;
            margin-top: auto;
        }

        .executor-download:hover {
            background: #ffffff;
            color: #000000;
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.7);
        }

        @media (max-width: 768px) {
            .container {
                padding: 24px;
                margin: 15px;
            }
            
            .title {
                font-size: 2.2rem;
                margin-bottom: 24px;
            }
            
            .time-display {
                font-size: 1.6rem;
            }
            
            .current-time-section, .script-section, .executors-section, .toggle-section {
                padding: 16px;
            }
            
            .key-methods {
                flex-direction: column;
                gap: 8px;
            }

            .tabs {
                flex-direction: column;
                gap: 4px;
            }

            .tab {
                padding: 12px 16px;
            }

            .games-grid {
                grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
                gap: 6px;
            }

            .copy-btn {
                position: relative;
                top: auto;
                right: auto;
                margin-top: 12px;
                display: block;
                width: 100%;
            }

            .executor-list {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 20px;
                margin: 10px;
            }
            
            .title {
                font-size: 1.8rem;
            }
            
            .time-display {
                font-size: 1.4rem;
            }
            
            .games-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="title">FoggyHub</h1>
        
        <div class="tabs">
            <button class="tab active" data-tab="key-system">
                <span>🔑 Key System</span>
            </button>
            <button class="tab" data-tab="main-script">
                <span>📜 Main Script</span>
            </button>
            <button class="tab" data-tab="executors">
                <span>⚙️ Executors</span>
            </button>
        </div>

        <div class="tab-content active" id="key-system">
            <div class="current-time-section">
                <div class="time-label">⏰ Current Time</div>
                <div class="time-display" id="current-timer">Loading...</div>
                <div class="timezone-info">🌍 Script Developer Timezone (GMT+3)</div>
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

        <div class="tab-content" id="executors">
            <div class="executors-section">
                <div class="executor-category">
                    <h3 class="category-title">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-pc-case"><rect width="14" height="20" x="5" y="2" rx="2"/><path d="M15 14h.01"/><path d="M9 6h6"/><path d="M9 10h6"/></svg>
                        PC Executors
                    </h3>
                    
                    <h4 class="section-title">Free</h4>
                    <div class="executor-list">
                        <div class="executor-item">
                            <div class="executor-name">
                                Swift
                                <span class="executor-price price-free">FREE</span>
                            </div>
                            <a href="https://getswift.vip/" target="_blank" class="executor-download">Download</a>
                        </div>
                        
                        <div class="executor-item">
                            <div class="executor-name">
                                Velocity
                                <span class="executor-price price-free">FREE</span>
                            </div>
                            <a href="https://getvelocity.lol/" target="_blank" class="executor-download">Download</a>
                        </div>
                        
                        <div class="executor-item">
                            <div class="executor-name">
                                Valex
                                <span class="executor-price price-free">FREE</span>
                            </div>
                            <a href="https://www.valex.io/" target="_blank" class="executor-download">Download</a>
                        </div>

                        <div class="executor-item">
                            <div class="executor-name">
                                Volcano
                                <span class="executor-price price-free">FREE</span>
                            </div>
                            <a href="https://volcano.wtf/" target="_blank" class="executor-download">Download</a>
                        </div>
                        
                        <div class="executor-item">
                            <div class="executor-name">
                                Bunni
                                <span class="executor-price price-free">FREE</span>
                            </div>
                            <a href="https://discord.gg/PNKAqSeFsM" target="_blank" class="executor-download">Join Discord</a>
                        </div>
                    </div>
                    
                    <h4 class="section-title">Paid</h4>
                    <div class="executor-list">
                        <div class="executor-item">
                            <div class="executor-name">
                                Wave
                                <span class="executor-price price-paid">PAID</span>
                            </div>
                            <a href="https://getwave.gg/" target="_blank" class="executor-download">Download</a>
                        </div>
                        
                        <div class="executor-item">
                            <div class="executor-name">
                                Zenith
                                <span class="executor-price price-paid">PAID</span>
                            </div>
                            <a href="https://zenith.win/" target="_blank" class="executor-download">Download</a>
                        </div>
                        
                        <div class="executor-item">
                            <div class="executor-name">
                                Potassium
                                <span class="executor-price price-paid">PAID</span>
                            </div>
                            <a href="https://discord.gg/2Ner6qHYMT" target="_blank" class="executor-download">Join Discord</a>
                        </div>
                    </div>
                </div>
                
                <div class="executor-category">
                    <h3 class="category-title">
                        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-smartphone"><rect width="14" height="20" x="5" y="2" rx="2" ry="2"/><path d="M12 18h.01"/></svg>
                        Mobile Executors
                    </h3>
                    
                    <h4 class="section-title">Free</h4>
                    <div class="executor-list">
                        <div class="executor-item">
                            <div class="executor-name">
                                Krnl
                                <span class="executor-price price-free">FREE</span>
                            </div>
                            <a href="https://krnl.cat/" target="_blank" class="executor-download">Download</a>
                        </div>
                        
                        <div class="executor-item">
                            <div class="executor-name">
                                Cryptic
                                <span class="executor-price price-free">FREE</span>
                            </div>
                            <a href="https://getcryptic.net/" target="_blank" class="executor-download">Download</a>
                        </div>
                        
                        <div class="executor-item">
                            <div class="executor-name">
                                Arceus
                                <span class="executor-price price-free">FREE</span>
                            </div>
                            <a href="https://spdmteam.com/" target="_blank" class="executor-download">Download</a>
                        </div>
                        
                        <div class="executor-item">
                            <div class="executor-name">
                                Delta
                                <span class="executor-price price-free">FREE</span>
                            </div>
                            <a href="https://deltaexploits.gg/" target="_blank" class="executor-download">Download</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        function updateCurrentTime() {
            const now = new Date();
            const utc = now.getTime() + (now.getTimezoneOffset() * 60000);
            const gmt3Time = new Date(utc + (3 * 3600000));
            
            const hours = gmt3Time.getHours().toString().padStart(2, '0');
            const minutes = gmt3Time.getMinutes().toString().padStart(2, '0');
            const seconds = gmt3Time.getSeconds().toString().padStart(2, '0');
            
            const currentTimerDisplay = document.getElementById('current-timer');
            currentTimerDisplay.textContent = `${hours}:${minutes}:${seconds}`;
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
                copyBtn.style.background = '#000000';
                copyBtn.style.boxShadow = '0 0 10px rgba(0, 255, 0, 0.7)';
                
                setTimeout(() => {
                    copyBtn.textContent = originalText;
                    copyBtn.style.background = '';
                    copyBtn.style.boxShadow = '';
                }, 2000);
            }).catch(() => {
                const copyBtn = document.querySelector('.copy-btn');
                const originalText = copyBtn.textContent;
                copyBtn.textContent = '❌ Failed';
                copyBtn.style.background = '#000000';
                copyBtn.style.boxShadow = '0 0 10px rgba(255, 0, 0, 0.7)';
                
                setTimeout(() => {
                    copyBtn.textContent = originalText;
                    copyBtn.style.background = '';
                    copyBtn.style.boxShadow = '';
                }, 2000);
            });
        }

        // Initialize toggle switches
        function initToggles() {
            const toggles = document.querySelectorAll('.toggle-switch');
            
            toggles.forEach(toggle => {
                toggle.addEventListener('click', () => {
                    toggle.classList.toggle('active');
                });
            });
        }

        document.addEventListener('DOMContentLoaded', () => {
            initTabs();
            initToggles();
            updateCurrentTime();
            setInterval(updateCurrentTime, 1000);
        });

        // Security features
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
