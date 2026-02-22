# 📰 AI-Powered Multilingual Newsletter Bot

> Send one Slack message in **any language** → get a professionally designed HTML newsletter in your Gmail inbox within seconds. Built with n8n, Google News RSS, Slack, and Gmail. **100% free to run.**

<div align="center">

![n8n](https://img.shields.io/badge/Built%20with-n8n-FF6D5A?style=for-the-badge&logo=n8n&logoColor=white)
![Slack](https://img.shields.io/badge/Triggered%20by-Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white)
![Gmail](https://img.shields.io/badge/Delivered%20via-Gmail-EA4335?style=for-the-badge&logo=gmail&logoColor=white)
![Free](https://img.shields.io/badge/Cost-100%25%20Free-brightgreen?style=for-the-badge)
![Languages](https://img.shields.io/badge/Languages-6+-blue?style=for-the-badge)

</div>

---

## 🎯 What Is This?

A fully automated newsletter bot that monitors your Slack channel and generates beautiful HTML newsletters on demand.

**You type in Slack:**
```
generate newsletter for cricket
```
```
தமிழ்நாடு அரசியல் செய்திகள்
```
```
AI technology news
```

**Bot delivers:**
- ✅ Instant Slack confirmation — "⏳ Generating..."
- 📧 Professional HTML newsletter to your Gmail
- 💬 Slack reply with top 5 clickable headlines
- 🌍 Full UI in your language (Tamil/Hindi/Malayalam etc.)

---

## 🖼️ Newsletter Layout

```
┌─────────────────────────────────────────────────────────┐
│  ████ GRADIENT TOP STRIPE ████                          │
├─────────────────────────────────────────────────────────┤
│              🔴  Logo Circle                            │
│         DAILY DIGEST · AI-POWERED                       │
│         Topic Name    Newsletter                        │
│         Sunday, 22 February 2026                        │
│         EDITION #444 · 10 STORIES                       │
├─────────────────────────────────────────────────────────┤
│  🔹 Scrolling ticker with article headlines... 🔹       │
├────────────────────────────────┬────────────────────────┤
│  HERO STORY                    │  ┌──────────────────┐  │
│  [Image]  Headline             │  │  LATEST NEWS     │  │
│           Source | Date        │  │  1. Article...   │  │
│           Description...       │  │  2. Article...   │  │
│           [READ FULL STORY]    │  │  3. Article...   │  │
│                                │  │  4. Article...   │  │
│  MORE NEWS ─────────────────   │  ├──────────────────┤  │
│  [Card 1]        [Card 2]      │  │  🏷 TRENDING     │  │
│  Badge Headline  Badge Headline│  │  #Topic #News    │  │
│  Source · Date   Source · Date │  └──────────────────┘  │
│  Description     Description   │                         │
│  Read More →     Read More →   │                         │
├────────────────────────────────┴────────────────────────┤
│  MORE STORIES                                           │
│  [Card]    [Card]    [Card]    [Card]                   │
├─────────────────────────────────────────────────────────┤
│           Dark Footer · Links · Copyright               │
│  ████ GRADIENT BOTTOM STRIPE ████                       │
└─────────────────────────────────────────────────────────┘
```

---

## 🌍 Supported Languages

| Language | Type your query in... | Newsletter UI |
|---|---|---|
| 🇬🇧 English | `cricket news` | LATEST NEWS, Read More → |
| 🇮🇳 Tamil | `தமிழ்நாடு செய்திகள்` | சமீபத்திய செய்திகள், மேலும் படிக்க → |
| 🇮🇳 Hindi | `क्रिकेट समाचार` | ताज़ा खबरें, और पढ़ें → |
| 🇮🇳 Malayalam | `Kerala വാർത്ത` | ഏറ്റവും പുതിയ വാർത്തകൾ |
| 🇮🇳 Telugu | `cricket వార్తలు` | తాజా వార్తలు |
| 🇮🇳 Kannada | `ಕ್ರಿಕೆಟ್ ಸುದ್ದಿ` | ತಾಜಾ ಸುದ್ದಿ |

Language is **automatically detected** using Unicode ranges — no AI API needed!

---

## 🏗️ How It Works

```
Slack Message
      │
      ▼
Extract Topic & Language
(Unicode detection, keyword filter)
      │
      ▼
Is Valid Request?
(contains news / newsletter / செய்தி / समाचार ?)
      │ YES
      ▼
Detect Language & Build Params
(translate topic → English search query)
(build Google News RSS language params)
      │
      ├─────────────────────────────────────┐
      ▼                                     ▼
Send Processing Message              Fetch Google News RSS
"⏳ Generating..."                   (in user's language)
                                           │
                                           ▼
                                     Prepare Articles
                                     (clean, deduplicate,
                                      extract images)
                                           │
                                           ▼
                                     Build Newsletter HTML
                                     (professional template,
                                      unique image per article)
                                           │
                               ┌───────────┴───────────┐
                               ▼                       ▼
                         Send Gmail              Build Slack Message
                         Newsletter              (clickable headlines)
                                                       │
                                                       ▼
                                                Slack Done Reply ✅
```

---

## 🧩 Nodes Explained

| # | Node | Purpose |
|---|---|---|
| 1 | **Slack Trigger** | Fires instantly when message sent in channel |
| 2 | **Extract Topic and Language** | Filters bots, detects language via Unicode |
| 3 | **Is Valid Request?** | Checks for news/newsletter keyword |
| 4 | **Detect Language and Build Params** | Translates topic, builds RSS params |
| 5 | **Send Processing Message** | Sends ⏳ status to Slack |
| 6 | **Fetch Google News RSS** | Gets news in user's language, no API key needed |
| 7 | **Prepare Articles** | Cleans titles, extracts images, deduplicates |
| 8 | **Build Newsletter HTML** | Generates full professional HTML email |
| 9 | **Send Newsletter Email** | Delivers via Gmail OAuth2 |
| 10 | **Build Slack Message** | Formats 5 clickable headline links |
| 11 | **Slack Done Reply** | Posts ✅ success message to channel |

---

## 🚀 Quick Start

### Requirements
- [n8n](https://n8n.io/) — self-hosted or cloud
- Slack workspace with admin access
- Gmail account
- Google News RSS — **no API key needed**

---

### Step 1 — Import Workflow

1. Download `Newsletter-UNIQUE-IMAGES-FINAL.json`
2. Open n8n → **Workflows** → **Import from file**
3. Select the downloaded JSON file

---

### Step 2 — Set Up Slack Credential

1. Go to [api.slack.com/apps](https://api.slack.com/apps) → **Create New App**
2. Choose **From scratch** → give it a name (e.g. `News_bot`)
3. Go to **OAuth & Permissions** → add these Bot Token Scopes:
   - `channels:history`
   - `channels:read`
   - `chat:write`
4. Click **Install to Workspace** → copy the **Bot User OAuth Token** (`xoxb-...`)
5. In n8n → **Credentials** → **New** → search `Slack API` → paste token
6. Enable **Event Subscriptions** in your Slack app:
   - Copy webhook URL from Slack Trigger node in n8n
   - Paste into Request URL → wait for ✅ Verified
   - Add bot event: `message.channels`
   - Click **Save Changes** → **Reinstall to Workspace**

---

### Step 3 — Set Up Gmail Credential

1. In n8n → **Credentials** → **New** → search `Gmail OAuth2`
2. Follow the Google OAuth2 flow
3. Connect your Gmail account

---

### Step 4 — Configure the Workflow

**Update your channel:**
In **Slack Trigger** node → **Channel to Watch** → select your channel

**Update email recipient:**
In **Send Newsletter Email** node → change `sendTo` to your email address

---

### Step 5 — Invite Bot to Channel

In your Slack channel, type:
```
/invite @News_bot
```

---

### Step 6 — Activate

Toggle the workflow **ON** (top right in n8n) ✅

---

## 💬 Usage Examples

### English
```
generate newsletter for cricket
AI technology news
latest news india
stock market news today
generate newsletter for IPL 2026
Elon Musk news
```

### Tamil தமிழ்
```
தமிழ்நாடு அரசியல் செய்திகள்
சினிமா செய்திகள்
விளையாட்டு செய்திகள்
திமுக அதிமுக செய்திகள்
```

### Hindi हिन्दी
```
क्रिकेट समाचार
भारत की ताज़ा खबरें
```

### Mixed
```
Kerala politics news
Chennai business news
Tamil Nadu sports செய்தி
```

---

## 🎨 Image Strategy

Each article in the newsletter gets a **unique image**:

```
Priority 1 → Real image from RSS feed (if available)
Priority 2 → Unique Picsum photo based on article title hash
             Different title = different seed = different image
             Always loads reliably in Gmail ✅
```

```javascript
// Each article title generates a unique number → unique image
const uniqueNum = title.split('')
  .reduce((acc, c) => acc + c.charCodeAt(0), slotIndex * 100);
const seed = uniqueNum % 1000;
// "DMK wins Tamil Nadu election" → seed 472 → unique photo
// "IPL 2026 Final Chennai"       → seed 891 → different photo
```

---

## 🔧 Customization

### Add a new language

In **Detect Language and Build Params** node, add to `uiStrings`:

```javascript
bn: {
  latest_news: 'সর্বশেষ সংবাদ',
  more_news: 'আরও সংবাদ',
  read_more: 'আরও পড়ুন',
  newsletter_word: 'নিউজলেটার',
  edition: 'সংস্করণ',
  stories: 'সংবাদ',
  trending: 'ট্রেন্ডিং',
  breaking: 'ব্রেকিং',
  read_full_story: 'পুরো গল্প পড়ুন',
  daily_digest: 'দৈনিক সংবাদ সারসংক্ষেপ',
  digest_tagline: 'আপনার দৈনিক AI সংবাদ সংকলন',
  more_stories: 'আরও গল্প'
}
```

And add to `langMap`:
```javascript
bn: { hl: 'bn', gl: 'IN', ceid: 'IN:bn' }
```

### Change newsletter accent color

In **Build Newsletter HTML** node, find and replace:
```javascript
'#e53935'   // red accent → change to any hex color
```

### Change news freshness

In **Fetch Google News RSS** node URL, update:
```
when:1d  → last 24 hours
when:2d  → last 48 hours (current default)
when:7d  → last week
```

---

## ⚠️ Duplicate Prevention

The bot uses two layers of protection to avoid processing the same message twice:

**Layer 1 — Bot message filter:**
```javascript
const isBot = !!(($json.bot_id) || $json.subtype === 'bot_message');
// Bot replies are automatically ignored ✅
```

**Layer 2 — Time filter (polling mode only):**

In **Read Slack Messages** node → Filters → Oldest field → switch to Expression:
```
{{ Math.floor(Date.now()/1000) - 70 }}
```
Only messages from the last 70 seconds are processed — so each message runs exactly once.

---

## 📁 Repository Structure

```
📦 slack-newsletter-bot/
 ┣ 📄 README.md
 ┣ 📄 Newsletter-UNIQUE-IMAGES-FINAL.json    ← Import this into n8n
 ┗ 📁 node-code/
    ┣ 📄 01-extract-topic.js
    ┣ 📄 02-detect-language.js
    ┣ 📄 03-prepare-articles.js
    ┗ 📄 04-build-newsletter-html.js
```

---

## 🛠️ Tech Stack

| Tool | Purpose | Cost |
|---|---|---|
| [n8n](https://n8n.io/) | Workflow automation | Free (self-hosted) |
| [Google News RSS](https://news.google.com/rss) | News feed | Free, no API key |
| [Slack API](https://api.slack.com/) | Trigger + reply | Free |
| [Gmail API](https://developers.google.com/gmail) | Email delivery | Free |
| [Picsum Photos](https://picsum.photos/) | Fallback images | Free |

**Total running cost: $0** ✅

---

## 🧪 Testing Checklist

After setup, verify each feature works:

- [ ] Send `generate newsletter for cricket` → newsletter arrives in Gmail
- [ ] Send `தமிழ்நாடு செய்திகள்` → Tamil UI labels appear in newsletter
- [ ] Send `hello` → **no response** (keyword filter working ✅)
- [ ] Send same message twice → **one newsletter only** (duplicate prevention ✅)
- [ ] Open newsletter → all 10 images are **different** from each other ✅
- [ ] Click headline in Slack reply → opens correct article URL ✅
- [ ] Check ticker → scrolls with all article headlines ✅

---

## 🤝 Contributing

Pull requests welcome! Ideas for improvement:

- Add more Indian languages (Bengali, Gujarati, Punjabi, Odia)
- Add daily scheduled digest at a fixed time
- Fetch real article OG images via HTTP Request node
- Add WhatsApp trigger support
- Add topic category tabs (Sports / Politics / Business)

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## ⭐ Support

If this project helped you, please give it a **star** ⭐

Built with ❤️ using n8n + Google News RSS
