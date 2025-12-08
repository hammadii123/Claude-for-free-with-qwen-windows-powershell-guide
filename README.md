# 🚀 Use Claude Code with Qwen Models **100% Free** on Windows (PowerShell Guide)

This guide will show you how to run **Claude Code** locally while using **Qwen models for free**, fully optimized for **Windows 10/11 PowerShell**.

You will install the required tools, extract your Qwen access token, configure Claude Code Router, and start coding with Qwen models inside Claude Code — all for free.

---

## 🧩 Prerequisites

Make sure you have installed the following:

* **Qwen CLI** (already authenticated)
* **Node.js v18+**
  (Download from: [https://nodejs.org](https://nodejs.org))

---

## 📌 Step 1 — Install Claude Code Router + Qwen Code (Global)

Open PowerShell and run:

```powershell
npm install -g @qwen-code/qwen-code@latest
```

Then install Claude Code + Router:

```powershell
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```

---

## 📌 Step 2 — Extract Your Qwen Access Token

Go to:

```
C:\Users\YOUR_USERNAME\.qwen\oauth_creds.json
```

Example content:

```json
{
  "access_token": "YOUR_QWEN_ACCESS_TOKEN_HERE",
  "token_type": "Bearer",
  "refresh_token": "YOUR_REFRESH_TOKEN",
  "resource_url": "portal.qwen.ai",
  "expiry_date": 1764876220290
}
```

👉 Copy the value of **access_token**
This will be used in the Claude Code Router config.

---

## 📌 Step 3 — Create Router Folders (Auto)

Paste this into PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude-code-router", "$env:USERPROFILE\.claude"
```

This creates:

```
C:\Users\YourName\.claude-code-router
C:\Users\YourName\.claude
```

---

## 📌 Step 4 — Create the Router Config File

Run this entire block in PowerShell (it will auto-create config.json):

```powershell
@"
{  
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,

  "Providers": [
    {
      "name": "qwen",
      "api_base_url": "https://portal.qwen.ai/v1/chat/completions",
      "api_key": "YOUR_QWEN_ACCESS_TOKEN_HERE",
      "models": [
        "qwen3-coder-plus",
        "qwen3-coder-plus",
        "qwen3-coder-plus"
      ]
    }
  ],

  "Router": {
    "default": "qwen,qwen3-coder-plus",
    "background": "qwen,qwen3-coder-plus",
    "think": "qwen,qwen3-coder-plus",
    "longContext": "qwen,qwen3-coder-plus",
    "longContextThreshold": 60000,
    "webSearch": "qwen,qwen3-coder-plus"
  }
}
"@ | Out-File -FilePath "$env:USERPROFILE\.claude-code-router\config.json" -Encoding UTF8
```

Now open the file:

```powershell
notepad "$env:USERPROFILE\.claude-code-router\config.json"
```

Replace:

```
YOUR_QWEN_ACCESS_TOKEN_HERE
```

with your real access token from Step 2.

Save and close.

---

## 📌 Step 5 — Start Using Claude Code with Qwen

Restart the router:

```powershell
ccr restart
```

Start Claude Code:

```powershell
ccr code
```

Test it:

```
> hi
```

If it responds — congratulations!
You’re now using **Claude Code with free Qwen models**.

---

# 🔄 Token Refresh Guide (Fix 401 Unauthorized)

You may sometimes get:

```
401 Unauthorized
```

This means your Qwen OAuth token expired.

### ✔️ Fix:

#### **1. Refresh your Qwen login**

If the access_token in both files matches:

```
config.json
oauth_creds.json
```

Delete this file:

```
C:\Users\YourName\.qwen\oauth_creds.json
```

Or Run this command simply:

```
del "$env:USERPROFILE\.qwen\oauth_creds.json"
```

Then run:

```
qwen
```

This will prompt login again and generate a new token.

---

#### **2. Update Claude Router Config**

Open:

```powershell
notepad "$env:USERPROFILE\.claude-code-router\config.json"
```

Replace the old `api_key` with your new `access_token`.

---

#### **3. Restart router**

```powershell
ccr restart
```

Done.

---

# ✅ All Set!

You now have the perfect setup to use **Claude Code with Qwen (free)** on Windows.

---

# ✍️ By Hammad Mustafa
