<!DOCTYPE html>
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
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow-x: hidden;
        }

        /* Animated background particles */
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
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            animation: float 15s infinite linear;
        }

        @keyframes float {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
        }

        .container {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            max-width: 500px;
            width: 90%;
            text-align: center;
            position: relative;
            z-index: 1;
            animation: slideIn 1s ease-out;
        }

        @keyframes slideIn {
            0% { transform: translateY(50px); opacity: 0; }
            100% { transform: translateY(0); opacity: 1; }
        }

        .title {
            font-size: 2.5rem;
            font-weight: bold;
            color: white;
            margin-bottom: 30px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            animation: glow 2s ease-in-out infinite alternate;
        }

        @keyframes glow {
            from { text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3), 0 0 20px rgba(255, 255, 255, 0.2); }
            to { text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3), 0 0 30px rgba(255, 255, 255, 0.4); }
        }

        .timer-section {
            background: rgba(255, 255, 255, 0.15);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 30px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            animation: pulse 3s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }

        .timer-label {
            color: #e0e0e0;
            font-size: 1.1rem;
            margin-bottom: 15px;
            font-weight: 500;
        }

        .timer-display {
            font-size: 2rem;
            font-weight: bold;
            color: #4ade80;
            text-shadow: 0 0 10px rgba(74, 222, 128, 0.5);
            font-family: 'Courier New', monospace;
            animation: timerGlow 2s ease-in-out infinite alternate;
        }

        @keyframes timerGlow {
            from { text-shadow: 0 0 10px rgba(74, 222, 128, 0.5); }
            to { text-shadow: 0 0 20px rgba(74, 222, 128, 0.8); }
        }

        .buttons-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .btn {
            padding: 15px 25px;
            border: none;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-block;
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }

        .btn:hover::before {
            left: 100%;
        }

        .discord-btn {
            background: linear-gradient(135deg, #5865f2, #4752c4);
            color: white;
            box-shadow: 0 8px 20px rgba(88, 101, 242, 0.3);
        }

        .discord-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 25px rgba(88, 101, 242, 0.4);
        }

        .key-methods {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }

        .method-btn {
            flex: 1;
            padding: 12px 15px;
            font-size: 1rem;
        }

        .linkvertise-btn {
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
            box-shadow: 0 8px 20px rgba(255, 107, 107, 0.3);
        }

        .linkvertise-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 25px rgba(255, 107, 107, 0.4);
        }

        .workink-btn {
            background: linear-gradient(135deg, #00d2d3, #54a0ff);
            color: white;
            box-shadow: 0 8px 20px rgba(0, 210, 211, 0.3);
        }

        .workink-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 25px rgba(0, 210, 211, 0.4);
        }

        .section-title {
            color: #e0e0e0;
            font-size: 1.2rem;
            margin: 25px 0 15px 0;
            font-weight: 600;
        }

        @media (max-width: 480px) {
            .container {
                padding: 25px;
                margin: 20px;
            }
            
            .title {
                font-size: 2rem;
            }
            
            .timer-display {
                font-size: 1.5rem;
            }
            
            .key-methods {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="particles"></div>
    
    <div class="container">
        <h1 class="title">FoggyHub Key System</h1>
        
        <div class="timer-section">
            <div class="timer-label">Current key is valid</div>
            <div class="timer-display" id="timer">Loading...</div>
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

    <script>

        function createParticles() {
            const particles = document.querySelector('.particles');
            
            for (let i = 0; i < 50; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                
                const size = Math.random() * 5 + 2;
                const left = Math.random() * 100;
                const delay = Math.random() * 15;
                
                particle.style.width = size + 'px';
                particle.style.height = size + 'px';
                particle.style.left = left + '%';
                particle.style.animationDelay = -delay + 's';
                
                particles.appendChild(particle);
            }
        }

        // Timer functionality
        function updateTimer() {
            const now = new Date();
            const currentHour = now.getHours();
            const currentMinute = now.getMinutes();
            const currentSecond = now.getSeconds();
            
            let targetHour;
            if (currentHour < 9) {
                targetHour = 9;
            } else if (currentHour < 21) {
                targetHour = 21;
            } else {
                targetHour = 9 + 24; // Next day 9 AM
            }
            
            const target = new Date();
            if (targetHour >= 24) {
                target.setDate(target.getDate() + 1);
                target.setHours(targetHour - 24, 0, 0, 0);
            } else {
                target.setHours(targetHour, 0, 0, 0);
            }
            
            const diff = target - now;
            
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
        

        createParticles();
        updateTimer();
        setInterval(updateTimer, 1000);
        

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
                `;
                
                this.appendChild(ripple);
                
                setTimeout(() => {
                    ripple.remove();
                }, 600);
            });
        });
        

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
    </script>
</body>
</html>
