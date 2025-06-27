<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Secure Access - Key System</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to bottom right, #1f1f1f, #3c3c3c);
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      overflow: hidden;
    }

    .container {
      text-align: center;
      background: #2c2c2c;
      border-radius: 16px;
      padding: 40px;
      box-shadow: 0 0 30px rgba(0, 0, 0, 0.4);
      animation: fadeIn 1.2s ease-in-out;
    }

    button {
      background-color: #0078d7;
      border: none;
      padding: 12px 24px;
      font-size: 16px;
      border-radius: 8px;
      cursor: pointer;
      color: white;
      transition: 0.3s;
      margin-top: 20px;
    }

    button:hover {
      background-color: #005aa7;
    }

    @keyframes fadeIn {
      from {opacity: 0; transform: scale(0.9);}
      to {opacity: 1; transform: scale(1);}
    }

    .key-box {
      margin-top: 20px;
      background: #1e1e1e;
      padding: 10px;
      border-radius: 8px;
      font-size: 14px;
      word-break: break-all;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🔑 Get Access Key</h1>
    <p>Click below and complete the steps to get your access key.</p>
    <button onclick="startKeyFlow()">Get My Key</button>
    <div id="result" class="key-box" style="display:none;"></div>
    <button id="deleteBtn" style="display:none;" onclick="deleteKey()">Delete My Key</button>
  </div>

  <script>
    const githubToken = "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";
    const repoOwner = "FOGOTY"; // CHANGE TO YOUR GITHUB USERNAME
    const repoName = "fatsxz"; // CHANGE TO YOUR REPO NAME
    const fileName = "fattie";

    async function startKeyFlow() {
      const adUrl = "https://work.ink/token?apiKey=fa224a0d-3447-46db-9684-97acde95ef9d";
      window.open(adUrl, "_blank");

      const tokenPrompt = prompt("Paste the token here after completing ad (you'll be redirected):");
      if (!tokenPrompt) return alert("No token provided.");

      const token = tokenPrompt.trim();

      const valid = await validateToken(token);
      if (!valid) return alert("Invalid token!");

      const generatedKey = crypto.randomUUID();
      const content = `Token: ${token}, Key: ${generatedKey}, Date: ${new Date().toISOString()}`;

      await uploadToGitHub(content);

      const resultBox = document.getElementById("result");
      resultBox.innerText = `Your Key: ${generatedKey}`;
      resultBox.style.display = "block";

      document.getElementById("deleteBtn").style.display = "inline-block";
      localStorage.setItem("my_key", generatedKey); // Save locally for delete
    }

    async function validateToken(token) {
      try {
        const res = await fetch(`https://work.ink/_api/v2/token/isValid/${token}?deleteToken=1`);
        const data = await res.json();
        return data.valid;
      } catch (e) {
        console.error("Token validation failed:", e);
        return false;
      }
    }

    async function uploadToGitHub(text) {
      const api = `https://api.github.com/repos/${repoOwner}/${repoName}/contents/${fileName}`;
      const headers = {
        Authorization: `Bearer ${githubToken}`,
        "Content-Type": "application/json",
      };

      let existing = "";
      let sha = "";
      try {
        const res = await fetch(api, { headers });
        const data = await res.json();
        existing = atob(data.content);
        sha = data.sha;
      } catch {}

      const updatedContent = existing + "\n" + text;
      const encoded = btoa(updatedContent);

      const res = await fetch(api, {
        method: "PUT",
        headers,
        body: JSON.stringify({
          message: "Added new key",
          content: encoded,
          sha: sha || undefined,
        }),
      });

      if (!res.ok) {
        alert("Failed to upload key.");
        console.error(await res.text());
      }
    }

    async function deleteKey() {
      const key = localStorage.getItem("my_key");
      if (!key) return alert("No key found to delete.");

      const api = `https://api.github.com/repos/${repoOwner}/${repoName}/contents/${fileName}`;
      const headers = {
        Authorization: `Bearer ${githubToken}`,
        "Content-Type": "application/json",
      };

      const res = await fetch(api, { headers });
      const data = await res.json();
      const content = atob(data.content);
      const sha = data.sha;

      const updatedContent = content
        .split("\n")
        .filter(line => !line.includes(key))
        .join("\n");

      const encoded = btoa(updatedContent);

      const update = await fetch(api, {
        method: "PUT",
        headers,
        body: JSON.stringify({
          message: "Deleted key",
          content: encoded,
          sha,
        }),
      });

      if (update.ok) {
        alert("Key deleted.");
        document.getElementById("result").innerText = "";
        document.getElementById("deleteBtn").style.display = "none";
      } else {
        alert("Failed to delete.");
        console.error(await update.text());
      }
    }
  </script>
</body>
</html>
