<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Key System Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        @keyframes slideIn {
            from { transform: translateY(20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        .animate-pulse-slow {
            animation: pulse 2s ease-in-out infinite;
        }
        .animate-slide-in {
            animation: slideIn 0.5s ease-out forwards;
        }
        body {
            background: linear-gradient(135deg, #1e3a8a, #3b82f6);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Arial', sans-serif;
        }
    </style>
</head>
<body class="text-white">
    <div class="max-w-md w-full bg-gray-900/80 backdrop-blur-md p-8 rounded-2xl shadow-2xl">
        <h1 class="text-3xl font-bold text-center mb-6 animate-slide-in">Key System Portal</h1>
        <div id="step1" class="space-y-4 animate-slide-in" style="animation-delay: 0.1s;">
            <h2 class="text-xl font-semibold">Step 1: Visit Work.ink</h2>
            <p>Click the button below to visit the Work.ink token generation page.</p>
            <a href="https://work.ink/token" target="_blank" class="block w-full bg-blue-600 hover:bg-blue-700 text-white text-center py-2 rounded-lg transition duration-300 animate-pulse-slow">Generate Token</a>
        </div>
        <div id="step2" class="space-y-4 mt-6 animate-slide-in" style="animation-delay: 0.2s;">
            <h2 class="text-xl font-semibold">Step 2: Validate Your Key</h2>
            <input id="tokenInput" type="text" placeholder="Enter your token" class="w-full p-2 rounded-lg bg-gray-800 text-white border border-gray-700 focus:outline-none focus:ring-2 focus:ring-blue-500">
            <button id="validateBtn" class="w-full bg-green-600 hover:bg-green-700 text-white py-2 rounded-lg transition duration-300 animate-pulse-slow">Validate Key</button>
        </div>
        <div id="result" class="mt-6 hidden animate-slide-in" style="animation-delay: 0.3s;">
            <h2 class="text-xl font-semibold">Result</h2>
            <p id="resultMessage"></p>
            <button id="deleteBtn" class="w-full bg-red-600 hover:bg-red-700 text-white py-2 rounded-lg transition duration-300 mt-4 hidden">Delete Key</button>
        </div>
    </div>

    <script>
        const apiKey = 'fa224a0d-3447-46db-9684-97acde95ef9d';
        const githubToken = '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';
        const repoOwner = 'FOGOTY'; // Replace with your GitHub username
        const repoName = 'fatsxz'; // Replace with your GitHub repository name
        const filePath = 'fattie'; // Path to store keys in GitHub

        async function validateToken(token) {
            try {
                const response = await fetch(`https://work.ink/_api/v2/token/isValid/${token}?deleteToken=0&forbiddenOnFail=1`, {
                    headers: { 'Authorization': `Bearer ${apiKey}` }
                });
                const data = await response.json();
                return data;
            } catch (error) {
                console.error('Validation error:', error);
                return { valid: false };
            }
        }

        async function saveKeyToGitHub(token) {
            try {
                // Get existing keys
                const getContent = await fetch(`https://api.github.com/repos/${repoOwner}/${repoName}/contents/${filePath}`, {
                    headers: { 'Authorization': `Bearer ${githubToken}`, 'Accept': 'application/vnd.github.v3+json' }
                });
                let keys = [];
                if (getContent.ok) {
                    const fileData = await getContent.json();
                    keys = JSON.parse(atob(fileData.content));
                }

                // Add new key
                keys.push({ token, createdAt: Date.now() });

                // Update GitHub file
                const updateContent = await fetch(`https://api.github.com/repos/${repoOwner}/${repoName}/contents/${filePath}`, {
                    method: 'PUT',
                    headers: { 'Authorization': `Bearer ${githubToken}`, 'Accept': 'application/vnd.github.v3+json' },
                    body: JSON.stringify({
                        message: `Add key ${token}`,
                        content: btoa(JSON.stringify(keys)),
                        sha: getContent.ok ? (await getContent.json()).sha : undefined
                    })
                });

                if (updateContent.ok) {
                    return true;
                } else {
                    console.error('GitHub update error:', await updateContent.text());
                    return false;
                }
            } catch (error) {
                console.error('GitHub error:', error);
                return false;
            }
        }

        async function deleteKey(token) {
            try {
                const response = await fetch(`https://work.ink/_api/v2/token/isValid/${token}?deleteToken=1`, {
                    headers: { 'Authorization': `Bearer ${apiKey}` }
                });
                const data = await response.json();
                if (data.deleted) {
                    // Update GitHub by removing the key
                    const getContent = await fetch(`https://api.github.com/repos/${repoOwner}/${repoName}/contents/${filePath}`, {
                        headers: { 'Authorization': `Bearer ${githubToken}`, 'Accept': 'application/vnd.github.v3+json' }
                    });
                    if (getContent.ok) {
                        const fileData = await getContent.json();
                        let keys = JSON.parse(atob(fileData.content));
                        keys = keys.filter(k => k.token !== token);

                        const updateContent = await fetch(`https://api.github.com/repos/${repoOwner}/${repoName}/contents/${filePath}`, {
                            method: 'PUT',
                            headers: { 'Authorization': `Bearer ${githubToken}`, 'Accept': 'application/vnd.github.v3+json' },
                            body: JSON.stringify({
                                message: `Delete key ${token}`,
                                content: btoa(JSON.stringify(keys)),
                                sha: fileData.sha
                            })
                        });

                        return updateContent.ok;
                    }
                }
                return false;
            } catch (error) {
                console.error('Delete error:', error);
                return false;
            }
        }

        document.getElementById('validateBtn').addEventListener('click', async () => {
            const token = document.getElementById('tokenInput').value.trim();
            const resultDiv = document.getElementById('result');
            const resultMessage = document.getElementById('resultMessage');
            const deleteBtn = document.getElementById('deleteBtn');

            if (!token) {
                resultMessage.textContent = 'Please enter a token.';
                resultDiv.classList.remove('hidden');
                return;
            }

            const data = await validateToken(token);
            if (data.valid) {
                const saved = await saveKeyToGitHub(token);
                resultMessage.textContent = saved ? `Key is valid! Saved to GitHub.` : `Key is valid but failed to save to GitHub.`;
                deleteBtn.classList.remove('hidden');
            } else {
                resultMessage.textContent = 'Invalid key.';
                deleteBtn.classList.add('hidden');
            }
            resultDiv.classList.remove('hidden');
        });

        document.getElementById('deleteBtn').addEventListener('click', async () => {
            const token = document.getElementById('tokenInput').value.trim();
            const resultMessage = document.getElementById('resultMessage');
            const deleteBtn = document.getElementById('deleteBtn');

            const deleted = await deleteKey(token);
            resultMessage.textContent = deleted ? 'Key deleted successfully.' : 'Failed to delete key.';
            deleteBtn.classList.add('hidden');
        });
    </script>
</body>
</html>
