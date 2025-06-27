<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Key System Access</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
      font-family: 'Inter', sans-serif;
      margin: 0;
      padding: 0;
    }
    body {
      background: linear-gradient(to right, #1c1c1c, #2e2e2e);
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      animation: fadeIn 2s ease-in;
    }
    @keyframes fadeIn {
      from {opacity: 0; transform: translateY(10px);}
      to {opacity: 1; transform: translateY(0);}
    }
    h1 {
      font-size: 3rem;
      margin-bottom: 20px;
    }
    button, input {
      margin: 10px;
      padding: 12px 20px;
      border: none;
      border-radius: 8px;
      background: #4e54c8;
      color: white;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    button:hover {
      background: #5658d5;
    }
    input {
      background: #3a3a3a;
      color: white;
      border: 1px solid #666;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <h1>🔐 Work.Ink Key System</h1>
  <div id="step1">
    <p>Step 1: <a href="https://work.ink/token" target="_blank">Get your token</a></p>
  </div>

  <div id="step2">
    <p>Step 2: Paste your token here:</p>
    <input type="text" id="tokenInput" placeholder="Enter your token" />
    <button onclick="validateToken()">Validate Token</button>
  </div>

  <div id="keyDisplay" class="hidden">
    <p>Your generated key:</p>
    <input type="text" id="generatedKey" readonly />
    <button onclick="deleteKey()">❌ Delete Key</button>
  </div>

  <script>
    const githubToken = "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";
    const repoOwner = "FOGOTY";
    const repoName = "fatsxz";
    const fileName = "fattie";

    async function validateToken() {
      const token = document.getElementById('tokenInput').value;
      if (!token) return alert("Please enter a token");

      const res = await fetch(`https://work.ink/_api/v2/token/isValid/${token}`);
      const data = await res.json();

      if (data.valid) {
        const generated = crypto.randomUUID();
        document.getElementById("generatedKey").value = generated;
        document.getElementById("keyDisplay").classList.remove("hidden");
        await saveKeyToGitHub(generated);
      } else {
        alert("Invalid token. Please try again.");
      }
    }

    async function saveKeyToGitHub(newKey) {
      const url = `https://api.github.com/repos/${repoOwner}/${repoName}/contents/${fileName}`;
      const headers = {
        Authorization: `Bearer ${githubToken}`,
        Accept: "application/vnd.github.v3+json"
      };

      let content = {};
      let sha = "";

      const res = await fetch(url, { headers });
      if (res.ok) {
        const data = await res.json();
        content = JSON.parse(atob(data.content));
        sha = data.sha;
      }

      content[newKey] = Date.now();

      const updateRes = await fetch(url, {
        method: "PUT",
        headers,
        body: JSON.stringify({
          message: `Add key ${newKey}`,
          content: btoa(JSON.stringify(content, null, 2)),
          sha: sha || undefined
        })
      });

      if (!updateRes.ok) alert("Failed to save key to GitHub.");
    }

    async function deleteKey() {
      const key = document.getElementById("generatedKey").value;
      const url = `https://api.github.com/repos/${repoOwner}/${repoName}/contents/${fileName}`;

      const headers = {
        Authorization: `Bearer ${githubToken}`,
        Accept: "application/vnd.github.v3+json"
      };

      const res = await fetch(url, { headers });
      if (!res.ok) return alert("Failed to load keys.");

      const data = await res.json();
      const keys = JSON.parse(atob(data.content));
      delete keys[key];

      const updateRes = await fetch(url, {
        method: "PUT",
        headers,
        body: JSON.stringify({
          message: `Delete key ${key}`,
          content: btoa(JSON.stringify(keys, null, 2)),
          sha: data.sha
        })
      });

      if (updateRes.ok) {
        alert("Key deleted!");
        document.getElementById("keyDisplay").classList.add("hidden");
      } else {
        alert("Failed to delete key.");
      }
    }
  </script>
</body>
</html>
