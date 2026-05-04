# Tecxo-Style Ads Broadcasting Bot

A Telegram ad broadcasting bot inspired by @TecxoAdsBot. Users login their Telegram account, set an ad message + interval, and the bot broadcasts that ad to ALL their groups continuously.

## Features
- 📊 Dashboard with status
- 👤 Multi-account hosting (up to 5 per user)
- ✍️ Set custom ad message (text/photo/video)
- ⏱️ Set time interval (60s – 86400s)
- ▶️ Start / ⏸ Stop ads
- 📝 Real-time logs sent to a separate Logs Bot
- 📈 Analytics per account
- 🗑️ Delete accounts
- 🔐 Sessions stored securely (SQLite + Pyrogram session string)

## Setup

### 1. Get Telegram API credentials
- Go to https://my.telegram.org → API Development Tools
- Create app → copy `API_ID` and `API_HASH`

### 2. Local test
```bash
pip install -r requirements.txt
cp .env.example .env
# fill values in .env
python bot.py
```

### 3. Deploy to Render
1. Push this folder to a GitHub repo
2. On Render → **New → Background Worker**
3. Connect GitHub repo
4. Build Command: `pip install -r requirements.txt`
5. Start Command: `python bot.py`
6. Add Environment Variables (from `.env.example`)
7. **Important**: Add a **Persistent Disk** (1 GB) mounted at `/data` so SQLite + sessions survive restarts.
8. Deploy

### 4. Use the bot
1. Open your bot on Telegram → `/start`
2. Tap **Add Accounts** → send phone number `+91xxxxxxxxxx`
3. Enter OTP received on Telegram (format: `1 2 3 4 5` with spaces, to avoid Telegram auto-revoking it)
4. If 2FA enabled → enter password
5. Tap **Set Ad Message** → send any text/photo
6. Tap **Set Time Interval** → enter seconds (e.g. `300`)
7. Tap **Start Ads ▶️**
8. Logs will be sent to the Logs Bot (`@your_logs_bot`) — start it once with `/start` to receive them.

## Notes / Warnings
- Using userbots to mass-send messages can get accounts **banned by Telegram**. Use slow intervals (≥ 60s) and only on groups you own / are allowed.
- Keep `API_ID` & `API_HASH` private.
- The Logs Bot only DMs the user who hosted the account — they must `/start` it first.
