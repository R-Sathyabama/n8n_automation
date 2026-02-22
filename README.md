# 📰 AI-Powered Multilingual Newsletter Bot

> Automatically generates and delivers beautifully designed HTML newsletters via Gmail — triggered by a simple Slack message in any language.

![n8n](https://img.shields.io/badge/n8n-workflow-orange?style=flat-square&logo=n8n)
![Slack](https://img.shields.io/badge/Slack-triggered-4A154B?style=flat-square&logo=slack)
![Gmail](https://img.shields.io/badge/Gmail-delivery-EA4335?style=flat-square&logo=gmail)
![Google News](https://img.shields.io/badge/Google%20News-RSS-4285F4?style=flat-square&logo=google)
![Languages](https://img.shields.io/badge/Languages-6+-brightgreen?style=flat-square)

---

## ✨ What It Does

Just type a message in Slack like:

```
generate newsletter for AI technology
தமிழ்நாடு அரசியல் செய்திகள்
cricket world cup news
Kerala business news
```

Within seconds, the bot:
1. 🔍 Detects your language automatically
2. 📡 Fetches latest news from Google News RSS
3. 🎨 Generates a professional HTML newsletter
4. 📧 Sends it to your Gmail inbox
5. ✅ Replies in Slack with clickable top headlines

---

## 🖼️ Newsletter Preview

The newsletter features a clean, professional light theme with:
- 🔴 Gradient header with topic initial logo
- 📜 Scrolling news ticker
- 🗞️ Hero story with image
- 📰 Two-column layout (main + sidebar)
- 📋 Latest news sidebar with numbered items
- 🏷️ Trending hashtags
- 📱 More stories section
- 🌐 Full multilingual UI support

---

## 🌍 Supported Languages

| Language | Script | Google News |
|----------|--------|-------------|
| English | Latin | ✅ |
| Tamil (தமிழ்) | Tamil | ✅ |
| Hindi (हिन्दी) | Devanagari | ✅ |
| Malayalam (മലയാളം) | Malayalam | ✅ |
| Telugu (తెలుగు) | Telugu | ✅ |
| Kannada (ಕನ್ನಡ) | Kannada | ✅ |

---

## 🏗️ Architecture

```
Slack Message (every 1 min poll)
        ↓
Extract Topic & Language (Unicode detection)
        ↓
Is Valid Request? (has news/newsletter keyword?)
        ↓ YES
Detect Language & Build Params
        ↓
┌───────────────────┐
│ Send Processing   │  → Slack: "⏳ Generating..."
│ Fetch Google News │  → RSS feed in user's language
└───────────────────┘
        ↓
Prepare Articles (clean, deduplicate, extract images)
        ↓
Build Newsletter HTML (professional email template)
        ↓
┌───────────────────┐
│ Send Gmail        │  → HTML newsletter to inbox
│ Build Slack Msg   │  → Clickable headlines
└───────────────────┘
        ↓
Slack Done Reply ✅
```

---

## 🧩 Workflow Nodes

| # | Node | Type | Purpose |
|---|------|------|---------|
| 1 | Every 1 Minute | Schedule Trigger | Polls Slack every minute |
| 2 | Read Slack Messages | Slack | Reads last 5 messages (last 70 sec) |
| 3 | Extract Topic and Language | Code | Detects language, filters bots |
| 4 | Is Valid Request? | IF | Skips if no news keyword |
| 5 | Detect Language and Build Params | Code | Translates topic, builds RSS params |
| 6 | Send Processing Message | Slack | Sends "⏳ Generating..." |
| 7 | Fetch Google News RSS | RSS Feed | Fetches news in user's language |
| 8 | Prepare Articles | Code | Cleans and structures articles |
| 9 | Build Newsletter HTML | Code | Generates full HTML email |
| 10 | Send Newsletter Email | Gmail | Delivers newsletter |
| 11 | Build Slack Message | Code | Formats clickable headlines |
| 12 | Slack Done Reply | Slack | Posts success message |

---

## 🚀 Setup Guide

### Prerequisites
- [n8n](https://n8n.io/) (self-hosted or cloud)
- Slack workspace with admin access
- Gmail account
- Google account (for Slack OAuth)

### Step 1 — Import Workflow
1. Download `Newsletter-SLACK-TRIGGER-FINAL.json`
2. Open n8n → **Workflows** → **Import from file**
3. Select the JSON file

### Step 2 — Configure Credentials

#### Slack OAuth2
1. Go to [api.slack.com/apps](https://api.slack.com/apps) → Create New App
2. Add Bot Token Scopes: `channels:history`, `channels:read`, `chat:write`
3. Install to workspace → copy **Bot User OAuth Token**
4. In n8n → Credentials → New → Slack OAuth2 → paste token

#### Gmail OAuth2
1. In n8n → Credentials → New → Gmail OAuth2
2. Follow Google OAuth flow
3. Connect your Gmail account

### Step 3 — Update Channel ID
In **Read Slack Messages** node:
- Change `channelId` to your Slack channel ID
- Find channel ID: Right-click channel in Slack → **Copy Link** → ID is at the end

### Step 4 — Update Email Address
In **Send Newsletter Email** node:
- Change `sendTo` to your email address

### Step 5 — Set Time Filter
In **Read Slack Messages** node → **Filters**:
- **Oldest** → switch to Expression mode → `{{ Math.floor(Date.now()/1000) - 70 }}`
- This ensures each message is processed only once

### Step 6 — Activate
Toggle workflow **ON** in top right corner ✅

---

## 💬 Usage Examples

### English
```
generate newsletter for AI technology
cricket world cup news
latest news india
stock market news today
```

### Tamil
```
தமிழ்நாடு அரசியல் செய்திகள்
சினிமா செய்திகள்
விளையாட்டு செய்திகள்
```

### Hindi
```
क्रिकेट समाचार
भारत की ताज़ा खबरें
```

### Mixed
```
Tamil Nadu politics news
Kerala business செய்தி
```

---

## 📁 File Structure

```
📦 slack-newsletter-bot
 ┣ 📄 Newsletter-SLACK-TRIGGER-FINAL.json   ← Main n8n workflow
 ┣ 📄 README.md                              ← This file
 ┗ 📁 node-code/
    ┣ 📄 extract-topic.js                   ← Node 3 code
    ┣ 📄 detect-language.js                 ← Node 5 code
    ┣ 📄 prepare-articles.js                ← Node 8 code
    ┗ 📄 build-newsletter-html.js           ← Node 9 code
```

---

## ⚙️ How Language Detection Works

```javascript
// Unicode range detection — no API needed
if (/[\u0B80-\u0BFF]/.test(text)) → Tamil
if (/[\u0D00-\u0D7F]/.test(text)) → Malayalam
if (/[\u0900-\u097F]/.test(text)) → Hindi
if (/[\u0C00-\u0C7F]/.test(text)) → Telugu
if (/[\u0C80-\u0CFF]/.test(text)) → Kannada
```

Translation dictionary converts native language topics to English for Google News search, then fetches results in the original language using proper `hl`, `gl`, and `ceid` parameters.

---

## 🎨 Newsletter Design

| Section | Details |
|---------|---------|
| Header | White background, gradient logo circle, centered layout |
| Ticker | Scrolling marquee with article headlines |
| Hero | 52/48 split — image + full story details |
| More News | Two equal cards side by side |
| Sidebar | Numbered list + trending hashtags |
| More Stories | 4-column grid |
| Footer | Dark slate with links |
| Images | Picsum Photos (reliable in Gmail) |

---

## 🔧 Customization

### Change newsletter recipient
In **Send Newsletter Email** node → update `sendTo` field

### Change Slack channel
In **Read Slack Messages** node → update `channelId`

### Add more languages
In **Detect Language and Build Params** node → add to `translations` object and `uiStrings`

### Change polling frequency
In **Every 1 Minute** node → adjust interval (remember to update Oldest filter accordingly)

---

## 🛠️ Tech Stack

- **[n8n](https://n8n.io/)** — Workflow automation
- **[Google News RSS](https://news.google.com/rss)** — Free news feed, no API key
- **[Slack API](https://api.slack.com/)** — Message trigger and reply
- **[Gmail API](https://developers.google.com/gmail)** — Newsletter delivery
- **[Picsum Photos](https://picsum.photos/)** — Reliable placeholder images

---

## 📝 License

MIT License — feel free to use, modify, and distribute.

---

## 🙋 Author

Built with ❤️ using n8n automation + Google News RSS

If this helped you, please ⭐ star the repo!
