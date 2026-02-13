# Bodiff --git a/README.md b/README.md
index 7909a9fd4d7ff258b4975c1b2b936fca81137886..1a97f070ff8f60acd729a720a82556ddf4c05d81 100644
--- a/README.md
+++ b/README.md
@@ -1,56 +1,94 @@
 # 🎯 BookieVerse - P2P Sportsbook
 
 ## What is This?
 
-A peer-to-peer sportsbook where **users are their own bookies**. Set your own lines, take action from others, compete for profit. We take 5% rake on every settled bet.
+A virtual-currency peer-to-peer sportsbook where **users challenge each other**. Set lines, take action from friends/community, and compete for leaderboard status using coins (no real-money wagering).
 
 **Demo:** [Your Render URL will go here]
 
 ## Features
 
 - 🏦 **Be the Bookie** - Set your own spreads, moneylines, totals
 - 🎯 **Take Action** - Bet against other users' lines
 - 📊 **Track Performance** - Win/loss records, profit/loss tracking
 - 🏆 **Leaderboard** - Compete for top profit
-- 💰 **$10,000 Play Money** - Start betting immediately
+- 🪙 **Daily Free Coins** - Claim 5 free coins every 24 hours
+- 🛒 **Coin Shop** - View launch coin bundles for continued play
 
 ## Quick Deploy to Render (FREE)
 
 ### Step 1: Push to GitHub
 
+If this folder already has a `.git` directory (most users here), use this:
+
+```bash
+git add .
+git commit -m "Initial commit"
+git branch -M main
+git remote add origin https://github.com/YOUR_USERNAME/bookieverse.git
+git push -u origin main
+```
+
+If this is a brand-new folder with no git history yet, run:
+
 ```bash
 git init
 git add .
 git commit -m "Initial commit"
 git branch -M main
 git remote add origin https://github.com/YOUR_USERNAME/bookieverse.git
 git push -u origin main
 ```
 
+If `origin` already exists, replace the remote URL instead of adding a new one:
+
+```bash
+git remote set-url origin https://github.com/YOUR_USERNAME/bookieverse.git
+git push -u origin main
+```
+
+### Create a ZIP you can upload/download
+
+If you need a single file to upload to GitHub, run:
+
+```bash
+./scripts/make_download_zip.sh
+```
+
+This creates `Bookieverse-upload.zip` in the repo root.
+
+If your editor file panel does not allow direct downloads, run the app and open:
+
+- `/download/zip` (example: `http://localhost:8000/download/zip`)
+
+Your browser will download the zip file directly.
+
 ### Step 2: Deploy on Render
 
+> Optional (recommended): this repo now includes `render.yaml` so Render can auto-detect build/start/health settings.
+
 1. Go to **https://render.com**
 2. Sign up with GitHub
 3. Click **"New +"** → **"Web Service"**
 4. Connect your **bookieverse** repository
 5. Settings:
    - **Name:** bookieverse
    - **Build Command:** `pip install -r requirements.txt`
    - **Start Command:** `uvicorn main:app --host 0.0.0.0 --port $PORT`
 6. Click **"Create Web Service"**
 
 ### Step 3: It's Live!
 
 Your app will be at: `https://bookieverse-XXXX.onrender.com/app`
 
 ---
 
 ## Local Development
 
 ### Prerequisites
 
 - Python 3.8+
 - pip
 
 ### Setup
 
@@ -77,52 +115,57 @@ bookieverse/
 ├── main.py              # FastAPI backend + API routes
 ├── index.html           # Frontend UI
 ├── requirements.txt     # Python dependencies
 └── README.md           # This file
 ```
 
 ---
 
 ## API Endpoints
 
 ### Authentication
 - `POST /api/auth/register` - Create new account
 - `POST /api/auth/login` - Login
 
 ### Lines
 - `GET /api/lines` - Get all open lines
 - `POST /api/lines` - Create a new line (requires auth)
 - `POST /api/lines/take` - Take a line (requires auth)
 
 ### Bets
 - `GET /api/bets` - Get user's bets (requires auth)
 - `POST /api/bets/{bet_id}/settle` - Settle a bet (requires auth)
 
 ### Other
 - `GET /api/games` - Get available games
-- `GET /api/leaderboard` - Get top users by profit
-- `GET /api/user` - Get current user info (requires auth)
+- `GET /healthz` - Health check endpoint for deploy monitoring
+- `GET /download/zip` - Browser download endpoint for `Bookieverse-upload.zip`
+- `GET /api/leaderboard` - Get top users by profit + rank tier
+- `GET /api/user` - Get current user wallet/tier info (requires auth)
+- `GET /api/wallet/shop` - Get coin package pricing
+- `GET /api/activity` - Get social activity feed (requires auth)
+- `GET /api/sports` - List supported sports and launch bet types
 
 Full API docs at: `/docs`
 
 ---
 
 ## Environment Variables
 
 Optional environment variables:
 
 ```bash
 SECRET_KEY=your-secret-key-here
 PORT=8000
 ```
 
 ---
 
 ## Tech Stack
 
 - **Backend:** FastAPI (Python)
 - **Frontend:** Vanilla JavaScript + HTML/CSS
 - **Database:** In-memory (for beta testing)
 - **Hosting:** Render.com (free tier)
 
 ---
 
@@ -163,25 +206,40 @@ PORT=8000
 MIT License - feel free to use this for your own projects!
 
 ---
 
 ## Support
 
 - **Issues:** https://github.com/YOUR_USERNAME/bookieverse/issues
 - **Twitter:** @yourhandle
 - **Email:** your@email.com
 
 ---
 
 ## Acknowledgments
 
 Built with ❤️ by [Your Name]
 
 Inspired by the idea that everyone should be able to be their own bookie.
 
 ---
 
 ## Legal
 
 This is a **play money** betting platform for entertainment purposes only. No real money gambling is involved. Users receive virtual currency ($10,000 play money) to bet with.
 
 If you plan to add real money betting, consult with legal counsel about gambling licenses in your jurisdiction.
+
+
+## Deployment Readiness
+
+- GitHub Actions CI runs dependency install + syntax/import smoke checks on push/PR.
+- `/healthz` can be used by hosting platforms and uptime monitors for basic health checks.
+
+
+## Deployment Files Checklist
+
+- `main.py` (FastAPI app entrypoint)
+- `requirements.txt` (Python deps)
+- `render.yaml` (Render infrastructure config)
+- `.github/workflows/ci.yml` (GitHub CI checks)
+- `README.md` + `DEPLOY_GUIDE.md` (deployment docs)
okieverse-Codex
