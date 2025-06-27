<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>f0g0tt HTML Viewer</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --bg-primary: #0f172a;
            --bg-secondary: #1e293b;
            --bg-tertiary: #334155;
            --accent-primary: #3b82f6;
            --accent-secondary: #60a5fa;
            --text-primary: #f8fafc;
            --text-secondary: #94a3b8;
            --success: #10b981;
            --danger: #ef4444;
            --warning: #f59e0b;
            --border-radius: 12px;
            --border-radius-sm: 8px;
            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            --shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3), 0 4px 6px -4px rgba(0, 0, 0, 0.3);
            --glow: 0 0 15px rgba(59, 130, 246, 0.5);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background-color: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            padding: 2rem;
            line-height: 1.5;
            overflow-x: hidden;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background-color: var(--bg-secondary);
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            overflow: hidden;
            animation: fadeIn 0.5s ease-out;
            transition: var(--transition);
        }

        .container:hover {
            transform: translateY(-2px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.3), 0 8px 10px -6px rgba(0, 0, 0, 0.3);
        }

        .tabs {
            display: flex;
            background-color: var(--bg-tertiary);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            position: relative;
        }

        .tab-indicator {
            position: absolute;
            bottom: 0;
            left: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--accent-primary), var(--accent-secondary));
            border-radius: 3px 3px 0 0;
            transition: var(--transition);
            z-index: 1;
        }

        .tab-btn {
            padding: 1rem 1.5rem;
            background: none;
            border: none;
            cursor: pointer;
            font-size: 0.9rem;
            font-weight: 600;
            color: var(--text-secondary);
            transition: var(--transition);
            position: relative;
            z-index: 2;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .tab-btn:hover {
            color: var(--text-primary);
            background-color: rgba(255, 255, 255, 0.05);
        }

        .tab-btn.active {
            color: var(--text-primary);
        }

        .tab-btn i {
            font-size: 0.9rem;
        }

        .tab-content {
            display: none;
            padding: 1.5rem;
            animation: fadeIn 0.4s ease-out;
        }

        .tab-content.active {
            display: block;
        }

        .code-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1.5rem;
            margin-top: 1rem;
        }

        @media (max-width: 768px) {
            .code-container {
                grid-template-columns: 1fr;
            }
        }

        .editor-section, .preview-section {
            display: flex;
            flex-direction: column;
            gap: 0.75rem;
        }

        .section-title {
            font-size: 0.9rem;
            font-weight: 600;
            color: var(--text-primary);
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .section-title i {
            color: var(--accent-primary);
        }

        #htmlCode {
            width: 100%;
            height: 400px;
            padding: 1rem;
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: var(--border-radius-sm);
            font-family: 'Fira Code', 'Consolas', 'Monaco', monospace;
            font-size: 0.9rem;
            line-height: 1.6;
            resize: none;
            background-color: var(--bg-tertiary);
            color: var(--text-primary);
            transition: var(--transition);
        }

        #htmlCode:focus {
            outline: none;
            border-color: var(--accent-primary);
            box-shadow: var(--glow);
        }

        #previewFrame {
            width: 100%;
            height: 400px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: var(--border-radius-sm);
            background-color: white;
            transition: var(--transition);
        }

        #previewFrame:hover {
            border-color: var(--accent-primary);
            box-shadow: var(--glow);
        }

        .action-buttons {
            display: flex;
            gap: 0.75rem;
            margin-top: 0.5rem;
            flex-wrap: wrap;
        }

        .btn {
            padding: 0.6rem 1rem;
            border: none;
            border-radius: var(--border-radius-sm);
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: 500;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .btn:hover {
            transform: translateY(-2px);
        }

        .btn i {
            font-size: 0.9rem;
        }

        .btn-primary {
            background-color: var(--accent-primary);
            color: white;
        }

        .btn-primary:hover {
            background-color: var(--accent-secondary);
            box-shadow: var(--glow);
        }

        .btn-success {
            background-color: var(--success);
            color: white;
        }

        .btn-success:hover {
            background-color: #0d9f6e;
            box-shadow: 0 0 15px rgba(16, 185, 129, 0.5);
        }

        .btn-danger {
            background-color: var(--danger);
            color: white;
        }

        .btn-danger:hover {
            background-color: #dc2626;
            box-shadow: 0 0 15px rgba(239, 68, 68, 0.5);
        }

        .btn-secondary {
            background-color: var(--bg-tertiary);
            color: var(--text-primary);
        }

        .btn-secondary:hover {
            background-color: #3c4a60;
        }

        .toast {
            position: fixed;
            bottom: 1.5rem;
            right: 1.5rem;
            padding: 0.8rem 1.5rem;
            background-color: var(--success);
            color: white;
            border-radius: var(--border-radius-sm);
            box-shadow: var(--shadow);
            opacity: 0;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 0.75rem;
            z-index: 1000;
            transform: translateY(20px);
        }

        .toast.show {
            opacity: 1;
            transform: translateY(0);
        }

        .toast i {
            font-size: 1.1rem;
        }

        .status-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 1rem;
            padding-top: 1rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.8rem;
            color: var(--text-secondary);
        }

        .status-item {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .status-item i {
            font-size: 0.9rem;
        }

        .theme-toggle {
            background: none;
            border: none;
            color: var(--text-secondary);
            cursor: pointer;
            font-size: 1rem;
            transition: var(--transition);
        }

        .theme-toggle:hover {
            color: var(--text-primary);
            transform: rotate(30deg);
        }

        /* About tab styling */
        .about-content {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        .about-content h2 {
            color: var(--accent-primary);
            font-weight: 700;
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .about-content h2 i {
            font-size: 1.3rem;
        }

        .about-content p {
            color: var(--text-secondary);
            line-height: 1.7;
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 1rem;
            margin-top: 1rem;
        }

        .feature-card {
            background-color: var(--bg-tertiary);
            border-radius: var(--border-radius-sm);
            padding: 1.25rem;
            transition: var(--transition);
            border-left: 3px solid var(--accent-primary);
        }

        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: var(--shadow);
        }

        .feature-card h3 {
            color: var(--text-primary);
            font-size: 1rem;
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .feature-card p {
            font-size: 0.85rem;
            color: var(--text-secondary);
        }

        /* Loading animation */
        .loading {
            display: inline-block;
            width: 1rem;
            height: 1rem;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: var(--accent-primary);
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Tooltip */
        .tooltip {
            position: relative;
            display: inline-block;
        }

        .tooltip .tooltip-text {
            visibility: hidden;
            width: 120px;
            background-color: var(--bg-tertiary);
            color: var(--text-primary);
            text-align: center;
            border-radius: var(--border-radius-sm);
            padding: 0.5rem;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            transform: translateX(-50%);
            opacity: 0;
            transition: var(--transition);
            font-size: 0.75rem;
            box-shadow: var(--shadow);
        }

        .tooltip:hover .tooltip-text {
            visibility: visible;
            opacity: 1;
        }

        /* Responsive adjustments */
        @media (max-width: 600px) {
            body {
                padding: 1rem;
            }
            
            .tabs {
                flex-wrap: wrap;
            }
            
            .tab-btn {
                padding: 0.75rem 1rem;
                font-size: 0.8rem;
            }
            
            .tab-content {
                padding: 1rem;
            }
            
            .features-grid {
                grid-template-columns: 1fr;
            }
        }

        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: var(--bg-secondary);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--accent-primary);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--accent-secondary);
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="tabs">
            <div class="tab-indicator" id="tabIndicator"></div>
            <button class="tab-btn active" onclick="openTab('htmlTab')">
                <i class="fas fa-code"></i> Editor
            </button>
            <button class="tab-btn" onclick="openTab('aboutTab')">
                <i class="fas fa-info-circle"></i> About
            </button>
            <div style="flex-grow: 1;"></div>
            <button class="theme-toggle" id="themeToggle" title="Toggle theme">
                <i class="fas fa-moon"></i>
            </button>
        </div>

        <div id="htmlTab" class="tab-content active">
            <div class="code-container">
                <div class="editor-section">
                    <div class="section-title">
                        <i class="fas fa-file-code"></i> HTML Editor
                    </div>
                    <textarea id="htmlCode" placeholder="<!DOCTYPE html>
<html>
<head>
    <title>My Awesome Page</title>
</head>
<body>
    <!-- Start coding here... -->
</body>
</html>">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;title&gt;My Page&lt;/title&gt;
    &lt;style&gt;
        body { 
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, #0f172a, #1e293b);
            color: white;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0;
            padding: 2rem;
        }
        .card {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 12px;
            padding: 2rem;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            max-width: 600px;
            width: 100%;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        h1 {
            color: #3b82f6;
            margin-bottom: 1rem;
        }
    &lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div class=&quot;card&quot;&gt;
        &lt;h1&gt;Hello Developer!&lt;/h1&gt;
        &lt;p&gt;This is a live preview of your HTML code.&lt;/p&gt;
        &lt;p&gt;Try editing the code to see instant changes.&lt;/p&gt;
    &lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</textarea>
                    <div class="action-buttons">
                        <button class="btn btn-primary" id="runBtn" onclick="runCode()">
                            <i class="fas fa-play"></i> Run
                        </button>
                        <button class="btn btn-success" id="copyBtn" onclick="copyCode()">
                            <i class="fas fa-copy"></i> Copy
                        </button>
                        <button class="btn btn-danger" id="clearBtn" onclick="clearCode()">
                            <i class="fas fa-trash-alt"></i> Clear
                        </button>
                        <button class="btn btn-secondary" id="formatBtn" onclick="formatCode()">
                            <i class="fas fa-align-left"></i> Format
                        </button>
                        <button class="btn btn-secondary" id="saveBtn" onclick="saveCode()">
                            <i class="fas fa-save"></i> Save
                        </button>
                    </div>
                </div>
                <div class="preview-section">
                    <div class="section-title">
                        <i class="fas fa-eye"></i> Live Preview
                    </div>
                    <iframe id="previewFrame"></iframe>
                </div>
            </div>
            <div class="status-bar">
                <div class="status-item">
                    <i class="fas fa-code-branch"></i>
                    <span>f0g0tt HTML Viewer | t.me/fagottv</span>
                </div>
                <div class="status-item">
                    <i class="fas fa-keyboard"></i>
                    <span id="charCount">0 characters</span>
                </div>
                <div class="status-item">
                    <i class="fas fa-clock"></i>
                    <span id="lastUpdated">Just now</span>
                </div>
            </div>
        </div>

        <div id="aboutTab" class="tab-content">
            <div class="about-content">
                <h2><i class="fas fa-star"></i> f0g0tt HTML Viewer</h2>
                <p>
                    A modern, feature-rich HTML code editor with live preview capabilities. 
                    Designed for developers who want a sleek, dark-themed environment with 
                    smooth animations and intuitive controls.
                </p>
                
                <h3><i class="fas fa-bolt"></i> Features</h3>
                <div class="features-grid">
                    <div class="feature-card">
                        <h3><i class="fas fa-laptop-code"></i> Live Preview</h3>
                        <p>See your HTML changes in real-time as you type with the instant preview panel.</p>
                    </div>
                    <div class="feature-card">
                        <h3><i class="fas fa-moon"></i> Dark Theme</h3>
                        <p>Eyes-friendly dark theme with customizable accent colors and smooth transitions.</p>
                    </div>
                    <div class="feature-card">
                        <h3><i class="fas fa-magic"></i> Code Formatting</h3>
                        <p>Automatically format your HTML code for better readability with a single click.</p>
                    </div>
                    <div class="feature-card">
                        <h3><i class="fas fa-clipboard"></i> One-Click Copy</h3>
                        <p>Copy your entire code to clipboard instantly with the copy button.</p>
                    </div>
                    <div class="feature-card">
                        <h3><i class="fas fa-file-download"></i> Save/Load</h3>
                        <p>Save your work locally and load it later to continue where you left off.</p>
                    </div>
                    <div class="feature-card">
                        <h3><i class="fas fa-tachometer-alt"></i> Performance</h3>
                        <p>Optimized for smooth performance even with large code snippets.</p>
                    </div>
                </div>
                
                <div class="action-buttons" style="margin-top: 1.5rem;">
                    <button class="btn btn-primary" onclick="openTab('htmlTab')">
                        <i class="fas fa-arrow-left"></i> Back to Editor
                    </button>
                </div>
            </div>
        </div>
    </div>

    <div id="toast" class="toast">
        <i class="fas fa-check-circle"></i>
        <span>Code copied to clipboard!</span>
    </div>

    <script>
        // Tab functionality with indicator animation
        function openTab(tabId) {
            const tabContents = document.getElementsByClassName('tab-content');
            const tabButtons = document.getElementsByClassName('tab-btn');
            
            for (let i = 0; i < tabContents.length; i++) {
                tabContents[i].classList.remove('active');
                tabButtons[i].classList.remove('active');
            }
            
            document.getElementById(tabId).classList.add('active');
            event.currentTarget.classList.add('active');
            
            // Update tab indicator position
            const tabIndicator = document.getElementById('tabIndicator');
            const activeTab = event.currentTarget;
            const tabRect = activeTab.getBoundingClientRect();
            const tabsRect = activeTab.parentElement.getBoundingClientRect();
            
            tabIndicator.style.width = `${tabRect.width}px`;
            tabIndicator.style.left = `${tabRect.left - tabsRect.left}px`;
        }

        // Initialize tab indicator position
        function initTabIndicator() {
            const tabIndicator = document.getElementById('tabIndicator');
            const activeTab = document.querySelector('.tab-btn.active');
            
            if (activeTab) {
                const tabRect = activeTab.getBoundingClientRect();
                const tabsRect = activeTab.parentElement.getBoundingClientRect();
                
                tabIndicator.style.width = `${tabRect.width}px`;
                tabIndicator.style.left = `${tabRect.left - tabsRect.left}px`;
            }
        }

        // Run code in preview
        function runCode() {
            const htmlCode = document.getElementById('htmlCode').value;
            const previewFrame = document.getElementById('previewFrame');
            const frameDoc = previewFrame.contentDocument || previewFrame.contentWindow.document;
            
            frameDoc.open();
            frameDoc.write(htmlCode);
            frameDoc.close();
            
            // Update last updated time
            updateLastUpdated();
        }

        // Copy code to clipboard
        function copyCode() {
            const htmlCode = document.getElementById('htmlCode');
            htmlCode.select();
            document.execCommand('copy');
            
            // Show toast notification
            showToast('Code copied to clipboard!', 'success');
        }

        // Clear the editor
        function clearCode() {
            if (confirm('Are you sure you want to clear the editor? All your code will be lost.')) {
                document.getElementById('htmlCode').value = '';
                updateCharCount();
                showToast('Editor cleared', 'warning');
            }
        }

        // Format code
        function formatCode() {
            const htmlCode = document.getElementById('htmlCode');
            let code = htmlCode.value;
            
            // Simple formatting (in a real app, use a proper formatter library)
            try {
                // Indent tags
                code = code.replace(/</g, '\n<');
                code = code.replace(/>/g, '>\n');
                
                // Remove excessive newlines
                code = code.replace(/\n+/g, '\n');
                code = code.trim();
                
                htmlCode.value = code;
                showToast('Code formatted', 'success');
            } catch (e) {
                showToast('Formatting failed', 'danger');
                console.error(e);
            }
        }

        // Save code to localStorage
        function saveCode() {
            const htmlCode = document.getElementById('htmlCode').value;
            localStorage.setItem('savedHtmlCode', htmlCode);
            showToast('Code saved locally', 'success');
        }

        // Load code from localStorage
        function loadCode() {
            const savedCode = localStorage.getItem('savedHtmlCode');
            if (savedCode) {
                document.getElementById('htmlCode').value = savedCode;
                runCode();
                showToast('Code loaded from storage', 'success');
            }
        }

        // Show toast notification
        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast');
            const toastIcon = toast.querySelector('i');
            const toastText = toast.querySelector('span');
            
            // Set toast style based on type
            switch (type) {
                case 'success':
                    toast.style.backgroundColor = 'var(--success)';
                    toastIcon.className = 'fas fa-check-circle';
                    break;
                case 'danger':
                    toast.style.backgroundColor = 'var(--danger)';
                    toastIcon.className = 'fas fa-exclamation-circle';
                    break;
                case 'warning':
                    toast.style.backgroundColor = 'var(--warning)';
                    toastIcon.className = 'fas fa-exclamation-triangle';
                    break;
                default:
                    toast.style.backgroundColor = 'var(--accent-primary)';
                    toastIcon.className = 'fas fa-info-circle';
            }
            
            toastText.textContent = message;
            toast.classList.add('show');
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // Update character count
        function updateCharCount() {
            const htmlCode = document.getElementById('htmlCode').value;
            const charCount = document.getElementById('charCount');
            const count = htmlCode.length;
            
            charCount.textContent = `${count} character${count !== 1 ? 's' : ''}`;
        }

        // Update last updated time
        function updateLastUpdated() {
            const lastUpdated = document.getElementById('lastUpdated');
            const now = new Date();
            const timeString = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
            
            lastUpdated.textContent = `Updated at ${timeString}`;
        }

        // Toggle theme
        function toggleTheme() {
            const body = document.body;
            const themeToggle = document.getElementById('themeToggle');
            const icon = themeToggle.querySelector('i');
            
            if (body.classList.contains('light-theme')) {
                body.classList.remove('light-theme');
                icon.className = 'fas fa-moon';
                themeToggle.title = 'Switch to light theme';
                showToast('Dark theme activated', 'success');
            } else {
                body.classList.add('light-theme');
                icon.className = 'fas fa-sun';
                themeToggle.title = 'Switch to dark theme';
                showToast('Light theme activated', 'success');
            }
        }

        // Initialize with default code
        window.onload = function() {
            initTabIndicator();
            runCode();
            
            // Set up event listeners
            document.getElementById('htmlCode').addEventListener('input', function() {
                updateCharCount();
            });
            
            document.getElementById('themeToggle').addEventListener('click', toggleTheme);
            
            // Load saved code if available
            loadCode();
            
            // Auto-run code when typing (with debounce)
            let timeout;
            document.getElementById('htmlCode').addEventListener('input', function() {
                clearTimeout(timeout);
                timeout = setTimeout(runCode, 1000);
            });
            
            // Initialize character count
            updateCharCount();
        };

        // Light theme styles (added dynamically when toggled)
        const lightThemeStyles = `
            .light-theme {
                --bg-primary: #f8fafc;
                --bg-secondary: #ffffff;
                --bg-tertiary: #f1f5f9;
                --text-primary: #0f172a;
                --text-secondary: #64748b;
                --accent-primary: #2563eb;
                --accent-secondary: #3b82f6;
            }
            
            .light-theme #htmlCode,
            .light-theme .feature-card {
                background-color: white;
                border: 1px solid #e2e8f0;
            }
            
            .light-theme #previewFrame {
                border: 1px solid #e2e8f0;
            }
            
            .light-theme .tabs {
                background-color: #f1f5f9;
                border-bottom: 1px solid #e2e8f0;
            }
            
            .light-theme .status-bar {
                border-top: 1px solid #e2e8f0;
            }
        `;
        
        // Add light theme styles to head
        const styleElement = document.createElement('style');
        styleElement.id = 'lightThemeStyles';
        styleElement.textContent = lightThemeStyles;
        document.head.appendChild(styleElement);
    </script>
</body>
</html>
