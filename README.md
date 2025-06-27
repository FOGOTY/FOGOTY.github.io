
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Key System Gateway</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap');

        :root {
            --primary-color: #00aaff;
            --secondary-color: #0a192f;
            --text-color: #ccd6f6;
            --text-secondary: #8892b0;
            --border-color: #1a3b5c;
            --success-color: #64ffda;
            --error-color: #ff6b6b;
            --bg-color: #0a192f;
            --bg-light: #112240;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            perspective: 1000px;
            overflow: hidden;
            background: radial-gradient(ellipse at bottom, #1b2735 0%, #090a0f 100%);
        }

        .container {
            width: 90%;
            max-width: 600px;
            background: var(--bg-light);
            padding: 40px;
            border-radius: 20px;
            border: 1px solid var(--border-color);
            box-shadow: 0 10px 30px rgba(2, 12, 27, 0.7);
            text-align: center;
            animation: fadeIn 1s ease-out;
            transform-style: preserve-3d;
            transition: transform 0.5s ease;
        }

        .container:hover {
            transform: rotateY(1deg) rotateX(1deg);
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        header h1 {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 10px;
            background: linear-gradient(90deg, var(--primary-color), var(--success-color));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        header p {
            color: var(--text-secondary);
            margin-bottom: 30px;
            font-size: 1.1rem;
        }

        .step {
            background: var(--bg-color);
            padding: 25px;
            margin-bottom: 25px;
            border-radius: 10px;
            border: 1px solid var(--border-color);
            transition: all 0.3s ease;
        }
        
        .step h2 {
            color: var(--primary-color);
            margin-bottom: 15px;
            font-size: 1.5rem;
        }

        .step p {
            color: var(--text-secondary);
            line-height: 1.6;
        }

        .btn {
            display: inline-block;
            background: transparent;
            color: var(--primary-color);
            border: 2px solid var(--primary-color);
            padding: 12px 30px;
            border-radius: 5px;
            text-decoration: none;
            font-weight: 600;
            font-size: 1rem;
            margin-top: 20px;
            cursor: pointer;
            transition: all 0.3s ease-in-out;
            position: relative;
            overflow: hidden;
        }
        
        .btn:hover {
            background: var(--primary-color);
            color: var(--bg-light);
            box-shadow: 0 0 20px var(--primary-color);
        }

        .input-group {
            position: relative;
            margin-top: 20px;
        }

        .key-input {
            width: 100%;
            padding: 15px;
            background: var(--bg-color);
            border: 1px solid var(--border-color);
            border-radius: 5px;
            color: var(--text-color);
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .key-input:focus {
            outline: none;
            border-color: var(--primary-color);
        }
        
        .message-area {
            margin-top: 25px;
            min-height: 50px;
            font-weight: 600;
            animation: slideIn 0.5s ease-out;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .message-area .success { color: var(--success-color); }
        .message-area .error { color: var(--error-color); }
        .message-area .info { color: var(--text-secondary); }

        .loader {
            border: 4px solid var(--border-color);
            border-top: 4px solid var(--primary-color);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
            display: none;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .key-display {
            background: var(--bg-color);
            padding: 20px;
            border-radius: 5px;
            border: 1px solid var(--border-color);
            margin-top: 20px;
        }
        .key-display p {
            word-wrap: break-word;
            color: var(--text-secondary);
        }
        .key-display p span {
            font-weight: 700;
            color: var(--success-color);
        }
        .btn-delete {
            background: transparent;
            color: var(--error-color);
            border: 2px solid var(--error-color);
        }
        .btn-delete:hover {
            background: var(--error-color);
            color: var(--bg-light);
            box-shadow: 0 0 20px var(--error-color);
        }

    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>Key System Gateway</h1>
            <p>Complete the steps to generate and secure your access key.</p>
        </header>

        <main id="main-content">
            
            <div id="step1" class="step">
                <h2>Step 1: Get Your Token</h2>
                <p>Click the button below to complete the advertiser's tasks. After you finish, you will be given a token. Copy it and return here for Step 2.</p>
                <a href="#" id="get-token-btn" class="btn" target="_blank" rel="noopener noreferrer">Generate Token</a>
            </div>

            <div id="step2" class="step">
                <h2>Step 2: Validate & Save Key</h2>
                <p>Paste the token you received from Step 1 into the field below to validate it and save it to your secure storage.</p>
                <div class="input-group">
                    <input type="text" id="key-input-field" class="key-input" placeholder="Paste your token here...">
                </div>
                <button id="validate-btn" class="btn">Validate & Save Key</button>
            </div>

            <div id="loader" class="loader"></div>
            <div id="message-area" class="message-area"></div>
            <div id="result-area"></div>

        </main>
    </div>

    <script>
        // --- CONFIGURATION ---
        // !!! IMPORTANT SECURITY WARNING !!!
        // DO NOT use your real Personal Access Token (PAT) here in a public website.
        // This is for demonstration only. In a real application, this must be handled
        // by a backend server to keep it secret and secure.
        const GITHUB_PAT = "ghp_dUMMYtOKENfORdEMONSTRATIONpURPOSES"; // <--- DO NOT USE A REAL ONE HERE PUBLICLY
        const GITHUB_USERNAME = "FOGOTY"; // <--- REPLACE WITH YOUR GITHUB USERNAME
        const GITHUB_REPO = "fattie"; // <--- REPLACE WITH YOUR REPO NAME
        
        // This is the ad-link you create on work.ink. 
        // Its "Destination URL" MUST be set to: https://work.ink/token
        const WORK_INK_URL = "https://work.ink/20Fk/va4ajr2d"; // <--- REPLACE WITH YOUR ACTUAL WORK.INK LINK
        // --- END CONFIGURATION ---


        // --- DOM Elements ---
        const getTokenBtn = document.getElementById('get-token-btn');
        const validateBtn = document.getElementById('validate-btn');
        const keyInputField = document.getElementById('key-input-field');
        const loader = document.getElementById('loader');
        const messageArea = document.getElementById('message-area');
        const resultArea = document.getElementById('result-area');

        // --- Initial Setup ---
        getTokenBtn.href = WORK_INK_URL;

        // --- Event Listeners ---
        validateBtn.addEventListener('click', handleValidation);

        // --- Functions ---
        
        /**
         * Main function to handle the validation and saving process.
         */
        async function handleValidation() {
            const token = keyInputField.value.trim();
            if (!token) {
                showMessage('error', 'Please paste a token before validating.');
                return;
            }

            if (GITHUB_PAT === "ghp_dUMMYtOKENfORdEMONSTRATIONpURPOSES" || GITHUB_USERNAME === "YOUR_GITHUB_USERNAME" || GITHUB_REPO === "YOUR_REPO_NAME" || WORK_INK_URL === "https://work.ink/YOUR/LINK") {
                 showMessage('error', 'ERROR: Please update the configuration variables in the script first.');
                 return;
            }

            toggleLoading(true);
            clearMessages();

            try {
                // 1. Validate the token with work.ink API
                const validationResponse = await validateWorkInkToken(token);

                if (validationResponse.valid) {
                    showMessage('success', 'Token is valid! Saving to GitHub...');
                    
                    // 2. Save the valid key to GitHub
                    const githubResponse = await saveKeyToGitHub(token, validationResponse.info);
                    
                    if (githubResponse.success) {
                        showMessage('success', 'Key successfully saved and secured!');
                        displayKeyResult(token, githubResponse.sha);
                    } else {
                        showMessage('error', `GitHub Error: ${githubResponse.message}`);
                    }

                } else {
                    showMessage('error', 'Invalid Token. Please try the steps again.');
                }
            } catch (error) {
                console.error("Validation Error:", error);
                showMessage('error', 'An unexpected error occurred. Please check the console.');
            } finally {
                toggleLoading(false);
            }
        }

        /**
         * Validates a token using the work.ink API.
         * @param {string} token - The token to validate.
         * @returns {Promise<object>} The JSON response from the API.
         */
        async function validateWorkInkToken(token) {
            const apiUrl = `https://work.ink/_api/v2/token/isValid/${token}`;
            const response = await fetch(apiUrl);
            if (!response.ok) {
                throw new Error(`API request failed with status ${response.status}`);
            }
            return response.json();
        }

        /**
         * Saves key information to a file in a GitHub repository.
         * @param {string} token - The key/token itself.
         * @param {object} keyInfo - The info object from the work.ink response.
         * @returns {Promise<object>} An object indicating success or failure.
         */
        async function saveKeyToGitHub(token, keyInfo) {
            const apiUrl = `https://api.github.com/repos/${GITHUB_USERNAME}/${GITHUB_REPO}/contents/keys/${token}.json`;
            
            const fileContent = JSON.stringify({
                message: "Generated via Key System Gateway",
                keyData: keyInfo
            }, null, 2);

            const encodedContent = btoa(fileContent); // Base64 encode the content

            const body = {
                message: `Create key: ${token}`,
                content: encodedContent,
                committer: {
                    name: "Key System Bot",
                    email: "bot@example.com"
                }
            };

            try {
                const response = await fetch(apiUrl, {
                    method: 'PUT',
                    headers: {
                        'Authorization': `token ${GITHUB_PAT}`,
                        'Accept': 'application/vnd.github.v3+json',
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(body)
                });

                if (response.status === 201 || response.status === 200) {
                    const data = await response.json();
                    return { success: true, sha: data.content.sha };
                } else {
                    const errorData = await response.json();
                    return { success: false, message: errorData.message || `HTTP ${response.status}` };
                }
            } catch (error) {
                console.error("GitHub Save Error:", error);
                return { success: false, message: error.message };
            }
        }
        
        /**
         * Deletes a key file from the GitHub repository.
         * @param {string} token - The key/token to delete.
         * @param {string} sha - The blob SHA of the file to delete.
         */
        async function deleteKeyFromGitHub(token, sha) {
            const confirmation = confirm(`Are you sure you want to permanently delete the key: ${token}? This cannot be undone.`);
            if (!confirmation) return;
            
            toggleLoading(true);
            clearMessages();
            
            const apiUrl = `https://api.github.com/repos/${GITHUB_USERNAME}/${GITHUB_REPO}/contents/keys/${token}.json`;
            const body = {
                message: `Delete key: ${token}`,
                sha: sha,
                 committer: {
                    name: "Key System Bot",
                    email: "bot@example.com"
                }
            };
            
             try {
                const response = await fetch(apiUrl, {
                    method: 'DELETE',
                    headers: {
                        'Authorization': `token ${GITHUB_PAT}`,
                        'Accept': 'application/vnd.github.v3+json',
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(body)
                });
                
                if (response.ok) {
                    showMessage('success', `Key ${token} has been successfully deleted.`);
                    resultArea.innerHTML = '';
                } else {
                     const errorData = await response.json();
                     showMessage('error', `Failed to delete key: ${errorData.message}`);
                }
             } catch(error) {
                 console.error("GitHub Delete Error:", error);
                 showMessage('error', 'An error occurred during deletion.');
             } finally {
                 toggleLoading(false);
             }
        }


        // --- UI Helper Functions ---

        function toggleLoading(isLoading) {
            loader.style.display = isLoading ? 'block' : 'none';
            validateBtn.disabled = isLoading;
        }

        function showMessage(type, text) {
            messageArea.innerHTML = `<p class="${type}">${text}</p>`;
        }
        
        function clearMessages() {
            messageArea.innerHTML = '';
            resultArea.innerHTML = '';
        }

        function displayKeyResult(token, sha) {
            keyInputField.value = ''; // Clear input field
            resultArea.innerHTML = `
                <div class="key-display">
                    <p>Your Key: <span>${token}</span></p>
                    <button class="btn btn-delete" onclick="deleteKeyFromGitHub('${token}', '${sha}')">Delete Key</button>
                </div>
            `;
        }

    </script>
</body>
</html>
